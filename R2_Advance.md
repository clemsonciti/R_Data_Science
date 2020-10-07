RIntro_R2_Advance
========================================================
author:  Tue Vu
date:    Feb 2019

1.Looping on the command line
========================================================

There are functions in R that make looping easier:

- apply: apply function over margins of array
- lapply: looping over list and evaluate function on element
- sapply: similar to lapply, but simpler
- mapply: multivariate version of lapply
- tapply: apply function over subsets of vector


========================================================

### apply
- Most often used to apply function to row or column of matrix
- Not really faster than loop but simpler coding

```r
str(apply)
m <- matrix(1:12,3,4)
print(m)
apply(m,1,sum)
apply(m,2,sum)
```

Additional shortcut as builtin function:

```r
rowSums(m)
colSums(m)
```

```
rowMeans, colMeans
```

========================================================

### lapply & sapply

lapply & sapply applies the FUN to  each element of a list

```r
list1 <- list(l1 = seq(1,10),l2=20:29,l3=rnorm(4))
lapply(list1,mean)
sapply(list1,mean)
```

2.Random number & seed
========================================================

Create random number using **runif**

```r
runif(1)
runif(3)
runif(2,10,20)
```

Create random number integer using **sample**

```r
sample(12,5)
sample(12)
sample(letters,4)
```

Using seed

```r
set.seed(1234)
runif(3)
```


3.Random number: Normal Distribution
========================================================

Generating Random number from Linear Model:

y=ax+b

```r
#rnorm(x,mean,sd)
set.seed(12)
x <- rnorm(500,mean=0,sd=1)
a <- 30
b <- rnorm(500,20,2)
y <- a*x+b
plot(x,y)
```

4.Other built-in Distribution
========================================================

- Normal (rnorm, dnorm, pnorm, qnorm)
- Poisson (rpois, dpois, ppois, qpois)
- Binomial (rbinom, dbinom, pbinom, qbinom)
- Exponential (rexp, dexp, pexp, qexp)
- Gamma (rgamma, dgamma, pgamma, qgamma)

5.Computation time
========================================================

- Examine how much time is spent in programming's parts
- Useful for optimization your code with parallel computation


```r
system.time(runif(300^3)*3)
```

```
   user  system elapsed 
   0.86    0.00    0.86 
```

```r
system.time(Sys.sleep(20))
```

```
   user  system elapsed 
   0.00    0.00   20.02 
```
user: time charged to the CPU for this expr
elapsed: "wall clock" time

6.Profiler
=========================================================

system.time() allows to test certain functions or code blocks
In order to know all functions, Profiler is used **Rprof**


```r
Rprof()  # Turn on the profiler
lm(y~x)
runif(10^5)
sample(12*10^5,10^5)
Sys.sleep(5)
Rprof(NULL)   # Turn off the profiler
summaryRprof()
```


7.Parallel Computing
=========================================================

The **doParallel** package is a "parallel backend" for the foreach package. It provides a mechanism needed to execute foreach loops in parallel. 

The **foreach** package must be used in order to execute code in parallel. The user must register a parallel backend to use, otherwise foreach will execute tasks sequentially, even when the %dopar% operator is used

User must register a parallel backend to use.
To register **doParallel** to be used with **foreach**, you must call the **registerDoParallel** function.

Install package: doParallel

```r
install.packages("doParallel")
```

Using some intensive computing function:

This function generates a square matrix of uniformly distributed random numbers, finds the corresponding (complex) eigenvalues and then selects the eigenvalue with the largest modulus. The dimensions of the matrix and the standard deviation of the random numbers are given as input parameters.

```r
max.eig <- function(N, sigma) {
     d <- matrix(rnorm(N**2, sd = sigma), nrow = N)
     E <- eigen(d)$values
     abs(E)[[1]]
 }
```

Using **foreach** package
========================================================

Sample 1:

```r
library(foreach)
foreach(i=1:4) %do% max.eig(i,1)
```

Using parameter **.combine**

```r
foreach(i=1:4, .combine='c') %do% max.eig(i,1)
```

**Nested** foreach

```r
k=1
foreach(i=1:4) %:%
   foreach(j=1:4) %do%{
      max.eig(k,1)
      k=k+1
    }      
```

using doParallel
========================================================

Check number of available processing cpus:

```r
library(doParallel)
co <- detectCores()-1
cl <- makeCluster(co)
registerDoParallel(cl)
```

Apply **doParallel** to **foreach**

```r
system.time(foreach(i=1:200, .combine='c') %do% max.eig(i,1))
system.time(foreach(i=1:200, .combine='c') %dopar% max.eig(i,1))
stopCluster(cl)
```


8.Configure and run R in Clemson University's fastest supercomputer: Palmetto;
========================================================

- Login to your Palmetto account
https://www.palmetto.clemson.edu/palmetto/userguide_basic_usage.html#logging-in

- Request a compute node:

```
$ qsub -I -l select=1:ncpus=2:mem=8gb,walltime=1:00:00
```
- Load R module

```
$ module load r/3.6.0-gcc/8.3.1
```
- Open R and run in Interactive mode:
```
$ R
> install.packages("doParallel")
```

- Run R in batch mode
```
$ Rscript a.R
$ R CMD BATCH a.R # Will write separate output file
```


9.How to run R in JupyterHub in Palmetto (large data debugging)
========================================================

Documentation: 
https://www.palmetto.clemson.edu/palmetto/jupyterhub_index.html

Spawning a Jupyterhub with minimum resources

Open R/3.4.2 in Jupyter Notebook

Execute some test runs
```{r}
library(ggplot2)
set.seed(12)
x <- rnorm(500000,mean=0,sd=1)
a <- 30
b <- rnorm(500000,20,2)
y <- a*x+b
qplot(x,y)
```
