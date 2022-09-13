# Programming with OpenMP

OpenMP is an open API specification for easy parallel programming in C and C++. [Main website](http://www.openmp.org)

OpenMP programming is mainly based on compiler directives.

```cpp
void daxpy(int n, double a, double *x, double *y, double *z)
{
int i;
#pragma omp parallel for //the loop below will be executed on multiple cores
for (i=0; i<n; i++)
  z[i] = a*x[i] + y[i];
}
```
