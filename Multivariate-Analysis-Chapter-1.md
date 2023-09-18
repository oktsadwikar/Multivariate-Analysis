Multivariate-Analysis Chapter 1
================
Oktsa Dwika Rahmashari
2023-09-18

**CHAPTER 1**

**A. Vectors and Matrices**

The computation:

    X = matrix(c(), nrow, ncol)

Explaination:

- c() is used to input the elements of the matrix

- nrow = the number of rows from the matrix, ex: 1, 2, 3, etc

- ncol = the number of columns from the matrix, ex: 1, 2, 3, etc.

So, the size of the matrix is nrow x ncol.

**Example:**

``` r
X = matrix(c(2,3,7,4),4,1)
X
```

    ##      [,1]
    ## [1,]    2
    ## [2,]    3
    ## [3,]    7
    ## [4,]    4

**B. Expectation**

1.  **Using Manual Way**

<!-- -->

    # Input Part
    X = c()
    prob = c()

    # Computation Part
    Exp_X = X %*% prob

Explaination:

- X = the value of the vector X

- prob = probability function of X

**Example:**

``` r
X = c(-1,0,1)
X
```

    ## [1] -1  0  1

``` r
prob = c(0.3,0.3,0.4)
prob
```

    ## [1] 0.3 0.3 0.4

``` r
Exp_X = X%*%prob
Exp_X
```

    ##      [,1]
    ## [1,]  0.1

2.  **Using Function**

<!-- -->

    # Input Part
    vals = c()
    probs = c()

    # calculate expected value
    weighted.mean(vals, probs)

Explaination:

- vals = the value of data or observation

- probs = probability function of observation

**Example:**

``` r
vals = c(-1,0,1)
probs = c(0.3,0.3,0.4)
weighted.mean(vals, probs)
```

    ## [1] 0.1

**C. Covariance Matrix**

The computation:

    # Input Part
    data = data.frame(V1 = c()
                      V2 = c()
                      ...
                      Vn = c())

    # Computation Part
    cov(data)

Explaination:

- data = data frame

- Vi = the value of variable i, where i = 1,2,…,n

**Example:**

``` r
data = data.frame(V1 = c(84, 82, 81, 89, 73, 94, 92, 70, 88, 95),
                  V2 = c(85, 82, 72, 77, 75, 89, 95, 84, 77, 94),
                  V3 = c(97, 94, 93, 95, 88, 82, 78, 84, 69, 78))

cov(data)
```

    ##           V1        V2        V3
    ## V1  72.17778  36.88889 -27.15556
    ## V2  36.88889  62.66667 -26.77778
    ## V3 -27.15556 -26.77778  83.95556

**D. Mean Vector and Covariance Matrix for Linear Combination of Random
Variables**

In general, consider the q linear combinations of the p random variables
1,2,…,p.

The computation:

    # Input Part
    mu = matrix(c(),,)
    sigma = matrix(c(),,)
    C = matrix(c(),,)

    # Computation Part
    MuZ = C%*%mu
    MuZ

    SigZ = C%*%sigma%*%t(C)
    SigZ

Explaination:

- mu = the expectation or mean vector

- sigma = the covariance matrix

- C = the combination matrix

- MuZ = the mean vector for Linear Combination

- SigZ = the covariance matrix for Linear Combination

**Example:**

``` r
mu = matrix(c(2,3,-1,5),4,1)
sigma = matrix(c(11,-8,3,9,-8,9,-3,-6,3,-3,2,3,9,6,3,9),4,4)
C = matrix(c(3,-1,2,1,-3,-2,-4,1,4,-1,-2,-5),3,4)

MuZ = C%*%mu
paste("so the mean vector for linear combination is")
```

    ## [1] "so the mean vector for linear combination is"

``` r
MuZ
```

    ##      [,1]
    ## [1,]    8
    ## [2,]  -22
    ## [3,]  -31

``` r
SigZ = C%*%sigma%*%t(C)
paste("so the covariance matrix for linear combination is")
```

    ## [1] "so the covariance matrix for linear combination is"

``` r
SigZ
```

    ##      [,1] [,2] [,3]
    ## [1,]   23  -42  -78
    ## [2,]   18  118  234
    ## [3,]    6  102  197

**E. Data Manipulation**

For data manipulation, we will use ‘dplyr’ and ‘tidyverse’ packages.

``` r
# Installing the package
library('dplyr')
```

    ## Warning: package 'dplyr' was built under R version 4.1.3

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library('tidyverse')
```

    ## Warning: package 'tidyverse' was built under R version 4.1.3

    ## Warning: package 'tibble' was built under R version 4.1.3

    ## Warning: package 'tidyr' was built under R version 4.1.3

    ## Warning: package 'readr' was built under R version 4.1.3

    ## Warning: package 'purrr' was built under R version 4.1.3

    ## Warning: package 'stringr' was built under R version 4.1.3

    ## Warning: package 'forcats' was built under R version 4.1.3

    ## Warning: package 'lubridate' was built under R version 4.1.3

    ## -- Attaching core tidyverse packages ------------------------ tidyverse 2.0.0 --
    ## v forcats   1.0.0     v readr     2.1.4
    ## v ggplot2   3.4.3     v stringr   1.5.0
    ## v lubridate 1.9.2     v tibble    3.2.1
    ## v purrr     1.0.1     v tidyr     1.3.0

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()
    ## i Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

Create Data Frame for the data that will be manipulated.

    # Input Part
    df1 = data.frame((V1 = c()
                      V2 = c()
                      ...
                      Vn = c())
    df2 = data.frame((V1 = c()
                      V2 = c()
                      ...
                      Vn = c())
    )

1.  **Inner Join Function**

<!-- -->

    # Computation Part
    df_ij = inner_join(df1, df2, by = " ")
    df_ij

Explaination : Merge 2 dataframe by variable inside ” “, then the output
will show only for the same value of variable inside” ”

2.  **Left Join using Inner Join**

<!-- -->

    # Computation Part
    df_ij2= df1 %>% inner_join(df2,by=" ")
    df_ij2

3.  **Outer Join**

<!-- -->

    # Computation Part
    df_U = full_join(df1,df2,by = "")
    df_U

Explaination: Merge 2 dataframe by variable inside ” “, then the output
will show all of the data and the missing data will show NA.

4.  **Left Join**

<!-- -->

    # Computation Part
    df_L = left_join(df1, df2, by=" ")
    df_L

Explaination: Combine right table (df2) to the left table (df1) by
variable inside ” ” from the left table (df1)

5.  **Right Join**

<!-- -->

    # Computation Part
    df_R = right_join(df1, df2, by=" ")
    df_R

Explaination: Combine left table (df1) to the right table (df2) by
variable inside ” ” from the right table (df2).

**Example:**

``` r
# Input part
df1=data.frame(CustomerId=c(1:6),Product=c("Oven","Television","Mobile","WashingMachine","Lightings","Ipad"),NumbProduct=c(10,5,16,2,22,7))
df2=data.frame(CustomerId=c(2,4,6,7,8),State=c("California","Newyork","Santiago","Texas","Indiana"))
```

``` r
# Inner Join Function
df_ij=inner_join(df1,df2,by="CustomerId") 
df_ij
```

    ##   CustomerId        Product NumbProduct      State
    ## 1          2     Television           5 California
    ## 2          4 WashingMachine           2    Newyork
    ## 3          6           Ipad           7   Santiago

``` r
# Left Join using Inner Join
df_ij2= df1 %>% inner_join(df2,by="CustomerId")
df_ij2
```

    ##   CustomerId        Product NumbProduct      State
    ## 1          2     Television           5 California
    ## 2          4 WashingMachine           2    Newyork
    ## 3          6           Ipad           7   Santiago

``` r
# Outer Join
df_U = full_join(df1,df2,by="CustomerId")
df_U
```

    ##   CustomerId        Product NumbProduct      State
    ## 1          1           Oven          10       <NA>
    ## 2          2     Television           5 California
    ## 3          3         Mobile          16       <NA>
    ## 4          4 WashingMachine           2    Newyork
    ## 5          5      Lightings          22       <NA>
    ## 6          6           Ipad           7   Santiago
    ## 7          7           <NA>          NA      Texas
    ## 8          8           <NA>          NA    Indiana

``` r
# Left Join
df_L = left_join(df1, df2, by="CustomerId")
df_L
```

    ##   CustomerId        Product NumbProduct      State
    ## 1          1           Oven          10       <NA>
    ## 2          2     Television           5 California
    ## 3          3         Mobile          16       <NA>
    ## 4          4 WashingMachine           2    Newyork
    ## 5          5      Lightings          22       <NA>
    ## 6          6           Ipad           7   Santiago

``` r
# Right Join
df_R = right_join(df1, df2, by="CustomerId")
df_R
```

    ##   CustomerId        Product NumbProduct      State
    ## 1          2     Television           5 California
    ## 2          4 WashingMachine           2    Newyork
    ## 3          6           Ipad           7   Santiago
    ## 4          7           <NA>          NA      Texas
    ## 5          8           <NA>          NA    Indiana

6.  **Check Information of data**

``` r
# Computation Part
df_U %>% glimpse()
```

    ## Rows: 8
    ## Columns: 4
    ## $ CustomerId  <dbl> 1, 2, 3, 4, 5, 6, 7, 8
    ## $ Product     <chr> "Oven", "Television", "Mobile", "WashingMachine", "Lightin~
    ## $ NumbProduct <dbl> 10, 5, 16, 2, 22, 7, NA, NA
    ## $ State       <chr> NA, "California", NA, "Newyork", NA, "Santiago", "Texas", ~

``` r
glimpse(df_U)
```

    ## Rows: 8
    ## Columns: 4
    ## $ CustomerId  <dbl> 1, 2, 3, 4, 5, 6, 7, 8
    ## $ Product     <chr> "Oven", "Television", "Mobile", "WashingMachine", "Lightin~
    ## $ NumbProduct <dbl> 10, 5, 16, 2, 22, 7, NA, NA
    ## $ State       <chr> NA, "California", NA, "Newyork", NA, "Santiago", "Texas", ~

``` r
df1 %>% full_join(df2, by="CustomerId") %>% glimpse()
```

    ## Rows: 8
    ## Columns: 4
    ## $ CustomerId  <dbl> 1, 2, 3, 4, 5, 6, 7, 8
    ## $ Product     <chr> "Oven", "Television", "Mobile", "WashingMachine", "Lightin~
    ## $ NumbProduct <dbl> 10, 5, 16, 2, 22, 7, NA, NA
    ## $ State       <chr> NA, "California", NA, "Newyork", NA, "Santiago", "Texas", ~

7.  **Check missing data for each column**

``` r
results = apply(is.na(df_U),2,which)
results
```

    ## $CustomerId
    ## integer(0)
    ## 
    ## $Product
    ## [1] 7 8
    ## 
    ## $NumbProduct
    ## [1] 7 8
    ## 
    ## $State
    ## [1] 1 3 5

``` r
results2 = apply(is.na(df_L),2,which)
results2
```

    ## $CustomerId
    ## integer(0)
    ## 
    ## $Product
    ## integer(0)
    ## 
    ## $NumbProduct
    ## integer(0)
    ## 
    ## $State
    ## [1] 1 3 5

Explainatuon : is.na to check missing value, 2 means we check the
column. if we use 1, means we check the row

8.  **Filter out the missing values by drop_na**

``` r
df_UC = drop_na(df_U)
df_UC
```

    ##   CustomerId        Product NumbProduct      State
    ## 1          2     Television           5 California
    ## 2          4 WashingMachine           2    Newyork
    ## 3          6           Ipad           7   Santiago
