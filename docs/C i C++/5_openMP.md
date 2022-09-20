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
