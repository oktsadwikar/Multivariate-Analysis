Assignment Chapter 1
================
Oktsa Dwika R
8/9/2023

# MULTIVARIATE ANALYSIS : CHAPTER 1 - ASSIGNMENT

## 1. Find xTAx, xTy, yBT, and xTAy by applying R coding to get solution.

**Answer :**

Input data

- Matrix A

``` r
A = matrix(c(1,-1,4,1,1,3,4,3,2),3,3)
A
```

    ##      [,1] [,2] [,3]
    ## [1,]    1    1    4
    ## [2,]   -1    1    3
    ## [3,]    4    3    2

- Matrix B

``` r
B = matrix(c(3,7,2,-2,1,3,4,0,5),3,3)
B
```

    ##      [,1] [,2] [,3]
    ## [1,]    3   -2    4
    ## [2,]    7    1    0
    ## [3,]    2    3    5

- Matrix x

``` r
x = matrix(c(1,-1,2),3,1)
x
```

    ##      [,1]
    ## [1,]    1
    ## [2,]   -1
    ## [3,]    2

- Matrix y

``` r
y = matrix(c(3,2,1),3,1)
y
```

    ##      [,1]
    ## [1,]    3
    ## [2,]    2
    ## [3,]    1

Then, we calculate the matrix.

### 1.1 xTAx

``` r
V = t(x)%*%A%*%x
paste("So, the result of the matrix multiplication above is ", V, ".")
```

    ## [1] "So, the result of the matrix multiplication above is  14 ."

### 1.2 xTy

``` r
W = t(x)%*%y
paste("So, the result of the matrix multiplication above is ",W, ".")
```

    ## [1] "So, the result of the matrix multiplication above is  3 ."

### 1.3 yBT

    Z = y%*%t(B)

``` r
paste("This will show error because the number column of matrix y = ", ncol(y)," which is not equal to the number rows of matrix B transpose= ", nrow(t(B)))
```

    ## [1] "This will show error because the number column of matrix y =  1  which is not equal to the number rows of matrix B transpose=  3"

The results of this matrix multiplication above is error because the
number of columns of matrix y is not equal with the number of rows of
the matrix B transpose. To prove this statement, let’s check the number
of columns of matrix y and the number of rows of matrix B transpose.

- Number of columns of matrix y

``` r
ncol_y = ncol(y)
paste("The number of columns of matrix y is ", ncol_y, ".")
```

    ## [1] "The number of columns of matrix y is  1 ."

- Number of rows of matrix B transpose

``` r
nrow_Bt = nrow(t(B))
paste("The number of columns of matrix y is ", nrow_Bt, ".")
```

    ## [1] "The number of columns of matrix y is  3 ."

### 1.4 xTAy

``` r
Results = t(x)%*%A%*%y
paste("So, the result of the matrix multiplication above is ", Results, ".")
```

    ## [1] "So, the result of the matrix multiplication above is  47 ."

## 2. Are the following statements true? Please verify the answer based on the given matrices by applying R coding.

2.1 det(AB) = det(A)det(B)

2.2 (AB)T = BTAT

**Answer :**

Input Data

- Matrix A

``` r
A = matrix(c(5,2,3,4,-3,7,4,1,2),3,3)
A
```

    ##      [,1] [,2] [,3]
    ## [1,]    5    4    4
    ## [2,]    2   -3    1
    ## [3,]    3    7    2

- Matrix B

``` r
B = matrix(c(1,0,1,0,1,2,1,0,3),3,3)
B
```

    ##      [,1] [,2] [,3]
    ## [1,]    1    0    1
    ## [2,]    0    1    0
    ## [3,]    1    2    3

Then, calculate statement 2.1 and 2.2

### 2.1 det(AB) = det(A)det(B)

- Calculate det(AB) and let det_AB be the variable of det(AB)

``` r
det_AB = det(A%*%B)
print(det_AB)
```

    ## [1] 46

- Calculate det(A)det(B) and let det_AxB be the variable of det(A)det(B)

``` r
det_AxB = det(A)%*%det(B)
print(det_AxB)
```

    ##      [,1]
    ## [1,]   46

- Comparing the results Since det(AB) = 46 and det(A)det(B) = 46, so
  det(AB)=det(A)det(B). Or we can conclude that the statement is True.

We also could compare these matrices using fuction all() below:

``` r
if(all(det_AB,det_AxB) == TRUE){
  paste("Since det(AB) = ",det_AB," = det(A)det(B) = ",det_AxB,"then the statement is True.")
}else{
  paste("Since det(AB) = ",det_AB," is not equal with det(A)det(B) = ",det_AxB,"then the statement is False.")
}
```

    ## Warning in all(det_AB, det_AxB): coercing argument of type 'double' to logical

    ## Warning in all(det_AB, det_AxB): coercing argument of type 'double' to logical

    ## [1] "Since det(AB) =  46  = det(A)det(B) =  46 then the statement is True."

### **2.2 (AB)T = BTAT**

- Calculate (AB)T and let AB_t be the variable of (AB)T

``` r
AB_t = t(A%*%B)
print(AB_t)
```

    ##      [,1] [,2] [,3]
    ## [1,]    9    3    5
    ## [2,]   12   -1   11
    ## [3,]   17    5    9

- Calculate BTAT and let Bt_At be the variable of BTAT

``` r
Bt_At = t(B)%*%t(A)
print(Bt_At)
```

    ##      [,1] [,2] [,3]
    ## [1,]    9    3    5
    ## [2,]   12   -1   11
    ## [3,]   17    5    9

- Comparing the results Since each element of matrix (AB)T is equal to
  each element of matrix BTAT, so we can conclude that (AB)T = BTAT or
  the statement is True.

We also could compare these matrices using fuction all() below:

``` r
all(AB_t,Bt_At)
```

    ## Warning in all(AB_t, Bt_At): coercing argument of type 'double' to logical

    ## Warning in all(AB_t, Bt_At): coercing argument of type 'double' to logical

    ## [1] TRUE

``` r
paste("Since all(AB_t,Bt_At) = ", all(AB_t,Bt_At), ". So, we can conclude that (AB)T = BTAT or the statement is True. " )
```

    ## Warning in all(AB_t, Bt_At): coercing argument of type 'double' to logical

    ## Warning in all(AB_t, Bt_At): coercing argument of type 'double' to logical

    ## [1] "Since all(AB_t,Bt_At) =  TRUE . So, we can conclude that (AB)T = BTAT or the statement is True. "
