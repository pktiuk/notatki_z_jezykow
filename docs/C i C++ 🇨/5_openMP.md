# Programming with OpenMP

OpenMP is an open, multi-platform API specification for easy parallel programming in Fortran, C and C++. [Main website](http://www.openmp.org)

OpenMP programming is mainly based on compiler directives.

`#pragma omp <directive> [clause [...]]`

For function usage you have to include `omp.h`

```c
#include <omp.h>
...
iam = omp_get_thread_num();
```

Simple usage example

```cpp
void daxpy(int n, double a, double *x, double *y, double *z)
{
int i;
#pragma omp parallel for //the loop below will be executed on multiple cores
for (i=0; i<n; i++)
  z[i] = a*x[i] + y[i];
}
```

Compile it with

```bash
gcc -fopenmp prg-omp.c
```

Loop iterations are shared among threads. All the variables are shared except loop variable `i`, which is private.

## Cmake

//TODO

## Threads management

[Link do docs](https://www.openmp.org/spec-html/5.1/openmp.html)

Managing threads numbers

```c
omp_set_num_threads(x);
omp_get_num_threads(); // returns the number of threads
omp_get_thread_num(); // returns the identifier of the thread (starting from 0, main thread is always 0)
```

We can also use env variable `OMP_NUM_THREADS`

```bash
OMP_NUM_THREADS=10 app
```

### Scheduling

`schedule(type[,chunk])`

//TODO S2 - slajd 24

## Loop Parallelization

General usage

```c
#pragma omp parallel for [clause [...]]
for (index=first; test_expr; increment_expr) {
// loop body
}
```

**NOTE** - inside of loop we can't use `break` `continue` etc (//TODO check this sentence)

Thank to clause we may define variables scope, way of obtaining results etc.

Clauses:

- private -each thread has a different replica
- shared - each threads can read and write
- reduction - used when neither private or shared can be used
- firstprivate, lastprivate
- default - forces to specify scope of all of variables

By default all of variables are **shared** with following exceptions:

- Index variable of the parallelized loop
- Local variables of the called subroutines (except if they are declared static)
- Automatic variables declared inside the loop

```c
sum = 0;
//for sum shared we have races for private we won't get any result
#pragma omp parallel for reduction(+:sum)
for (i=0; i<n; i++) {
  sum = sum + x[i]*x[i];
}
```

**Reduction** - allows easy aggregation of results

`reduction (operator : list)`

Available operators: `+`, `*`, `-`, `&`, `|`, `ˆ`, `&&`, `||`, `max`, `min`

**firstprivate, lastprivate** - in general private variables have undefined value during the first execution and after execution

- `firstprivate` initializes to the value of selected variable the begining of the block.

```c
#include <stdio.h>
#include <omp.h>

int main (void)
{
    int i = 10;
    #pragma omp parallel firstprivate(i)
    {
        //in case of regular private variable we would get random values
        printf("thread %d: i = %d\n", omp_get_thread_num(), i);
        i = 1000;
    }
    printf("i = %d\n", i);
    return 0;
}
```

- `lastprivate` the value of the variable after the block is the one of the “last” iteration of the loop

```c
alpha = 5.0;
#pragma omp parallel for firstprivate(alpha) lastprivate(i)
for (i=0; i<n; i++) {
  z[i] = alpha*x[i];
}
k = i;
/* i has value n*/
```

**if clause** - runs loop in pararell only if the expression is true (because of the overhead linked with initializing threads)

```c
#pragma omp parallel for if(n>5000)
for (i=0; i<n; i++)
  z[i] = a*x[i] + y[i];
```

## Parallel Regions

Pragma `parallel` executes block of code in replicated threads.

```c
#pragma omp parallel [clause [clause ...]]
{
// block
}
```

Example

```c
#pragma omp parallel private(myid)
{
  myid = omp_get_thread_num();
  printf("I am thread %d\n",myid);
}
```

They are used for sharing work in a bit different manner.

- Each thread works on a part of the data structure, or
- Each thread performs a different operation

Possible mechanisms for worksharing:

- Based on the thread identifier

```c
#pragma omp parallel private(myid)
{
  nthreads = omp_get_num_threads();
  myid = omp_get_thread_num();
  dowork(myid, nthreads);
}
```

- Parallel task queue

```c
int get_next_task() {
  static int index = 0;
  int result;
  #pragma omp critical
  {
    if (index==MAXIDX) result=-1;
    else { index++; result=index; }
  }
  return result;
}
...
int myindex;
#pragma omp parallel private(myindex)
{
  myindex = get_next_task();
  while (myindex>-1) {
    process_task(myindex);
    myindex = get_next_task();
  }
}
```

- Using OpenMP specific constructs - thank to them programmer doesn't have to worry about splitting workload. Types:
  - for construct to split iterations of loops
  - Sections to distinguish different parts of the code
  - Code to be executed by a single thread

### Worksharing constructs

#### The `for` construct

```c
#pragma omp parallel
{
  ...
  #pragma omp for
  for (i=1; i<n; i++)
    b[i] = (a[i] + a[i-1]) / 2.0;
}
```

The loop iterations are **not** replicated but shared among the threads
`parallel` and `for` directives can be combined in one.

#### Loop Construct - `nowait`

`nowait` Clause - removes implicit barrier after for loop

```c
void a8(int n, int m, float *a, float *b, float *y, float *z)
{
  int i;
  #pragma omp parallel
  {
    #pragma omp for nowait
    for (i=1; i<n; i++)
      b[i] = (a[i] + a[i-1]) / 2.0;

    //loop below can start execution before the one above will finish
    #pragma omp for
    for (i=0; i<m; i++)
      y[i] = sqrt(z[i]);
  }
}
```

#### `sections` Construct

represents pliece of code, which can be split into small independent sections

- Individually they represent little work, or
- Each fragment is inherently sequential
  It can also be combined with parallel

```c
#pragma omp parallel sections
{
  #pragma omp section
  Xaxis();
  #pragma omp section
  Yaxis();
  #pragma omp section
  Zaxis();
}
```

A thread may execute more than one section
Clauses: private, first/lastprivate, reduction, nowait

#### `single` and `master` Construct

Code fragments that must be executed by a single thread

```c
#pragma omp parallel
{
  // we will see info about starting and ending work1
  // only once
  #pragma omp single
    printf("work1 starts\n");

  //Other threads will wait until "work1 starts" will be printed
  work1();

  #pragma omp single
    printf("work1 ends\n");


  #pragma omp single nowait
    printf("work1 ended in all of the threads, work2 started\n");
  work2();
}
```

`master` Directive

Differences with single:

- It does not require all threads to reach this construction
- There is no implicit barrier (other threads simply skip this code)

```c
#pragma omp parallel
{
  #pragma omp master
    printf("Begin work\n");
  #pragma omp for
    for (i=0; i<n; i++)
      calc1();

  //this will be launched after finishing loop above
  #pragma omp master
    printf("Work finished\n");
}
```

Some allowed clauses: private, firstprivate, nowait

## Synchronization

The main point of synchronization is avoiding race conditions.

The most basic way of avoiding this is mutual exclusion. (directive `critical`, `atomic` or locks - `_lock` routines).

### `critical` directive

`#pragma omp critical [(Name)]`

Allows execution of critical section by only one thread at once

```c
cur_max = -100000;
#pragma omp parallel for
for (i=0; i<n; i++) {
  #pragma omp critical
  if (a[i] > cur_max) {
    cur_max = a[i];
  }
}
```

When a thread reaches the `if` block (the critical section), it waits until no other thread is executing it at the same time.

Code above is not optimal, because entering critical section costs, and we can limit it

```c
cur_max = -100000;
#pragma omp parallel for
for (i=0; i<n; i++) {
  if (a[i] > cur_max) {
    #pragma omp critical
    if (a[i] > cur_max)
      cur_max = a[i];
  }
}
```

We can also use named critical sections

```c
cur_max = -100000;
cur_min = 100000;
#pragma omp parallel for
for (i=0; i<n; i++) {
  if (a[i] > cur_max) {
    #pragma omp critical (maxlock)
    if (a[i] > cur_max)
      cur_max = a[i];
  }
  if (a[i] < cur_min) {
    #pragma omp critical (minlock)
    if (a[i] < cur_min)
      cur_min = a[i];
  }
}
```

### `atomic` directive

It is much more efficient than critical section, but supports only very simple operations.

```c
#pragma omp atomic
x <binop>= exp
```

where `<binop>` can be `+, *, -, /, %, &, |, ^, <<, >>`

```c
#pragma omp parallel for shared(x, index, n)
for (i=0; i<n; i++) {
  #pragma omp atomic
  x[index[i]] += work1(i);
}
```

### `barrier` directive

When reaching a barrier, threads wait for the rest to arrive

```c
#pragma omp parallel private(index)
{
  index = generate_next_index();
  while (index>0) {
    add_index(index);
    index = generate_next_index();
  }
  #pragma omp barrier
  index = get_next_index();
  while (index>0) {
    process_index(index);
    index = get_next_index();
  }
}
```

### `ordered` directive

Ensures, that portions of code in the loops are executed in the original sequential order

```c
#pragma omp parallel for ordered
for (i=0; i<n; i++) {
  a[i] = ...
  /* complex computation */
  #pragma omp ordered
  fprintf(fd, "%d %g\n", i, a[i]);
}
```

**Only one** ordered section is allowed per iteration

//TODO ask about this ❗
// std::cout << "xx"


## Programming GPU

OpenMP can be also used for harnessing compute resources of GPUs like Nvidia.

There are some additional clauses like `target`, 


`target` construct consists of a target directive and an execution region. target directive defines a target region, a block of computation that operates within a distinct data environment and is intended to be offloaded onto a parallel computation device during execution ( GPU in our case). Data used within the region may be implicitly or explicitly mapped to the device. OpenMP is allowed within target regions, but only a subset will run well on GPUs.

This target platform can be a GPU, CPU, or different kind of accelerator

```cpp
while (iter < iter_max )
{
    error = 0.0;
    //Moves this region of code to the GPU and implicitly maps data.
    #pragma omp target
    {
        #pragma omp parallel for reduction(max:error)
        for( int j = 1; j < n-1; j++) {
            ANew[j] = A [j-1] + A[j+1];
        }
    }
    iter++;
}
```

`target data` - allows to map data to the device.

`#pragma omp target date map(map-type: list)`

mapping types:

- `to` - data is copied from the host to the device
- `from` - data is copied from the device to the host
- `alloc` - allocates memory ot the device. If the data is already present on the device a reference counter is incremented

```cpp
while (iter < iter_max )
{
    error = 0.0;
    //Moves this region of code to the GPU and explicitly maps data.
    #pragma omp target data map(to:A[:n]) map(from:ANew[:n])
    {
        #pragma omp parallel for reduction(max:error)
        for( int j = 1; j < n-1; j++) {
            ANew[j] = A [j-1] + A[j+1];
        }
    }
    iter++;
}
```

### `teams` and `distribute`

`teams` directve creates a league of thread teams where the master thread of each team executes the region. Each of these master threads executes sequentially. In other words, teams directive spawn one or more thread teams with the same number of threads. The execution continues on the master threads of each team (redundantly). There is no synchronization allowed between teams.

![teams](https://passlab.github.io/OpenMPProgrammingBook/_images/teams.jpeg)

OpenMP calls that somewhere a team, which might be a thread on the CPU or maying a CUDA threadblock or OpenCL workgroup. It will choose how many teams to create based on where you're running, only a few on a CPU (like 1 per CPU core) or lots on a GPU (1000's possibly). teams allow OpenMP code to scale from small CPUs to large GPUs because each one works completely independently of the other teams.

`distribute` directive is used to distribute the iterations of a loop across the master threads of the teams.

There's a good chance that we don't want the loop to be run redundantly in every master thread of ```teams``` though, that seems wasteful and potentially dangerous. With the usage of ```distribute``` construct the iterations of the next loop are broken into groups that are *distributed* to the master threads of the teams. The iterations are distributed statically and there is no guarantee about the order teams will execute. Also it does not generate parallelism/worksharing within the thread teams.

```cpp
#pragma omp target teams distribute
    for( int j = 1; j < n-1; j++) {
       for( int i = 1; i < m-1; i++) {
            Anew[j][i] = 0.25 * ( A[j][i+1] + A [j][i-1]
                            + A[j-1][i] + A[j+1][i]);
            error = fmax (error, fabs(Anew[j][i] - A[j][i]));
    }}
```

In many cases compilers can deal with distributing load by themselves using the `teams loop` construct, which is a shortcut for specifying a teams construct containing a loop construct and no other statements

```cpp
#pragma omp target teams loop reduction(max:error) 
for( int j = 1; j < n-1; j++) {
  #pragma omp loop reduction(max:error)
  for( int i = 1; i < m-1; i++ ) {
      Anew[j][i] = 0.25f * ( A[j][i+1] + A[j][i-1]
                            + A[j-1][i] + A[j+1][i]);
      error = fmaxf( error, fabsf(Anew[j][i]-A[j][i]));
  }
}
```

General execution model for OpenMP:

![OpenMP execution model](./assets/OpenMP-40-Execution-model.png)
 source: https://www.researchgate.net/figure/OpenMP-40-Execution-model_fig1_335478417