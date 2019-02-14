INTRODUCTION TO R PROGRAMMING
========================================================
### Author: Tue Vu 
#### Advanced Computing and Data Science group- CCIT\CITI
#### Research Assistant Professor - Glenn Department of Civil Engineering, Clemson University

### Exercise Link: <https://vuminhtue.shinyapps.io/R3_QA1/>
### Survey Link: <https://www.surveymonkey.com/r/26SZF3F>


1.Input to R
========================================================
In R, the **>** is command prompt

```r
getwd()
setwd("C:/R/")
?getwd #getting help
rm(list=ls()) #clean memory
dev.off()  #remove existing plots
```

Symbol **<-** is assignment operator


```r
a <- 2
print(a)

string <- "Hello world"
print(string)
```

Character **#** is used to comment


```r
#Assign value to a
a <- 2
```

2.Printing variables
========================================================

Another way to print out the variable

```r
a
string
```

The **[1]** shows that a is a vector and **2** is the first element


```r
a <- 10:50
a
```
The **:** creates integer sequences

Print working directory

```r
getwd()
```
Set working directory

```r
setwd('C:/R/')
getwd()
```


3.Objects
========================================================
## Classes of objects
- characters **a**, **b**
- numeric: **2.3**
- interger: **5** or **5L**
- complex: **2e+3**
- logical: **TRUE**/**FALSE**


## Typical object is a vector
- A vector can contain same class object

```r
str <- c("a","b","c")
class(str)
a <- rnorm(5)
class(a)
b <- 4:7
class(b)
c <- 6i ^ (-3:3)
class(c)
d <- 1:10 < 5
class(d)
```

4.List
========================================================
A vector that contains objects from different class is call **list**

```r
list1 <- c(str,a,b,c,d)
list1
list1[27]
```
5.Number
========================================================
- In R, the number is considered as numeric

```r
e<-5
class(e)
```
- To get an integer, insert **L** as suffix

```r
f<-5L
class(f)
```
- Special number: **Inf**: infinity

```r
g<-5/0
class(g)
```
- **NaN** (Not a Number) or **NA** (Not Applicable) are undefined values and sometimes refered as missing values

```r
h <- 0/0
i <- NA
h
i
```
6.Vector
========================================================
A vector of objects can be created using **c()** function

```r
str <- c("a","b","c")
a   <- c(4,5.6,20)
b   <- c("TRUE","FALSE")
```
A vector having different objects: **coercion **

```r
str1 <- c("a","b","c",5, 4.5)
str1
class(str1)
b1<- c(5, FALSE)
b1
class(b1)
```
How about 
```
c1 <- c("6.5",TRUE)
```
7.Explitcit Coercion
========================================================
Convert objects from one class to another, using **as.** function

```r
a <- 0:5
class(a)
as.numeric(a)
as.logical(a)
as.character(a)
```

How about Nonsensical Coercion 
```
str <- c("a","b","c")
class(str)
as.numeric(str)
as.logical(str)
as.character(str)
```
8.Matrices
========================================================
Matrics are vectors with dimension attribute.
The dimension attribute is itself an integer vector of length 2 **(nrow, ncol)**

```r
m <- matrix(1:12,nrow=3,ncol=4)
m
dim(m)
```
Another way to create matrices

```r
m <- 1:12
dim(m) <- c(3,4)
m
#Transpose matrics
t(m)
#Diagonal of matrics
diag(m)
```
9.Merging Matrices
========================================================
Merging matrices by row and column using **rbind** and **cbind**

```r
m2 <- letters[seq(from=1,to=12)]
dim(m2) <- c(3,4)
m2
cbind(m,m2)
rbind(m,m2)
```
10.Factors
========================================================
Factors are used to represent categorical data

```r
m <- c("John","Mary","John","John","Jeff","Mary")
factor(m)
table(m)
```
11.Missing values and Inf
========================================================
In order to test the missing values or bad values **NaN, NA, Inf, #DIV0** use some math operations:
- is.na() test **NA** value
- is.nan() test **NaN** value
- is.infinite() test **Inf** value
- NaN is NA but the reverse is false


```r
v <- c(TRUE, 6, 1/0,NA, NaN,-6/0)
v
is.na(v)
is.nan(v)
```
How about
```
is.infinite(v)
```
12.Data Frames
========================================================
### Data frame is used to store tabular data, a table or 2-D array structure in which:
- Each column contains values of one variable and 
- Each row containts one set of value from each column

### Data Frame characteristics:
- Column name should not be empty
- Row name should be unique
- Data can be numeric, integer, character, factor
- Each column contains same number of data items

========================================================
### Examples

```r
data(iris)
dim(iris)
head(iris)
```



```r
names(iris)
nrow(iris)
ncol(iris)
```
13.Names
========================================================
R Objects have names

```r
names(iris)
#Change name
names(iris) <- c("a", "b", "c","d","e")
head(iris)
```
14.Reading and Writing Tables
===================
## Reading Table
Most popular syntax for reading table in R
- **read.table**: read table in text format
- **read.csv**: read table in csv format
- **read.xlsx**: read table in excel format (require xlsx packages)
- **readLines**: read lines of a text file
- **source**: read R code

## Writing Table
Similarly there are syntax for writing table:
- **write.table**: read table in text format
- **write.csv**: read table in csv format
- **write.xlsx**: read table in excel format (require xlsx packages)
- **writeLines**: read lines of a text file

===================
## Examples
The following csv files are downloaded from website:

```r
#https://support.spatialkey.com/spatialkey-sample-csv-data/
#Read sale transaction file:
saledata <- read.csv("http://samplecsvs.s3.amazonaws.com/SalesJan2009.csv")

dim(saledata)
names(saledata)
saledata$City[5]
```
Writing the output to local computer

```r
write.csv(saledata,"SaleStatistics.csv")
```

===================

Reading txt file

```r
#poem <- readLines("http://lib.ru/SHAKESPEARE/sonnets.txt")
#poem[10:20]
```

Writing the output to local computer

```r
#writeLines(poem[10:20],"Sonet1.txt")
```

15.Subsetting
===================
## In order to extract the necessary information, subsetting is used

```r
str <- c("a", "b","c","d")
str
str[1]
str[2:4]
```

## Subsetting list

```r
list1 <- list(l1=str,l2=4:6)
list1
#Use $ to call a variable name
list1$l1[3]
```

===================
## Subsetting matrix

```r
m <- matrix(1:12,nrow=3,ncol=4)
m
m[2,3]
```
### Subsetting by row or column

```r
m[2,]
m[,4]
```

### Subsetting NA/NaN

```r
a <- c(1:5,NaN,TRUE)
a
ind <- is.nan(a)
ind
a[ind]
a[!ind]
```

16.Vectors Operation
==================

```r
a <- 3:7
b <- 20:24
a+b
a>b
a>5
a*b
a/b
```
17.Matrices Operation
==================

```r
m1 <- matrix(1:9,nrow=3,ncol=3)
m2 <- matrix(rep(10,9),3,3)
m1
m2
m1+m2
m1*m2
m1 %*% m2
```
18.Control Structure
==================
Control the flow of program execution:
- if, else
- for loop
- while loop

==================
### If
Syntax
```
If (<condition>){
  #do task 1
} else {
  #do task 2
}
```
Example

```r
a=5
if (a>3){
  print("a is bigger than 3")
} else {
  print("a is NOT bigger than 3")
}
```

Syntax
```
If (<condition 1>){
  #do task 1
} else if (<condition 2>) {
  #do task 2
} else {
  #do the rest
}
```

==================
### For loop
Syntax
```
for (<loop sequence>){
  #do task
}
```
Example

```r
for (i in 1:5){
  print(i)
}
```

```r
for (i in seq(1,5)){
  print(i)
}
```
Short Syntax

```r
for (i in 1:5) print(i)
```

```r
for (i in seq(1,5)) print(letters[i])
```

==================
### While
Looping while the testing condition is valid

```r
a <- 1
while(a<5){
  print(a)
  a <- a+1
}
```
19.Function
==================
- created using **function()**
- can be passed as argument to other function
- can be nested (defined inside another function)

Syntax
```
f <- function(arguments){
  #do function task
}
```
R built-in function of square root

```r
x <- 25
sqrt(x)
```
Create own function

```r
squareroot <- function(a){
  a^0.5
}
squareroot(49)
```
20.Function: Dates
==================
function **as.Date()**

```r
today_date <- Sys.Date()
print(today_date)
date1 <- as.Date("2017-12-02")
print(date1)
#different between date
print(today_date-date1)

time_now <- Sys.time()
print(time_now)
```
21.Looping on the command line
==================
There are functions in R that make looping easier:

- apply: apply function over margins of array
- lapply: looping over list and evaluate function on element
- sapply: similar to lapply, but simpler
- mapply: multivariate version of lapply
- tapply: apply function over subsets of vector


==================
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

==================
### lapply & sapply
lapply & sapply applies the FUN to  each element of a list

```r
list1 <- list(l1 = seq(1,10),l2=20:29,l3=rnorm(4))
lapply(list1,mean)
sapply(list1,mean)
```

22.Random number & seed
==================
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


23.Random number: Normal Distribution
==================
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

24.Other built-in Distribution
==================
- Normal (rnorm, dnorm, pnorm, qnorm)
- Poisson (rpois, dpois, ppois, qpois)
- Binomial (rbinom, dbinom, pbinom, qbinom)
- Exponential (rexp, dexp, pexp, qexp)
- Gamma (rgamma, dgamma, pgamma, qgamma)
