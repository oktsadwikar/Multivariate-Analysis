Chapter 3 Multivariate Analysis Compare Mean
================
Oktsa Dwika Rahmashari
2023-10-20

# MULTIVARIATE ANALYSIS FOR COMPARE MEAN

## A. ONE SAMPLE T-TEST

### 1. Hypothesis testing : Hotelling’s T Square

H0 : Mu = Mu0 vs H1 : Mu =/ Mu0

#### **1.1 Hotelling’s T square Manual**

    # Input Part
    Xbar = matrix(c(),,)
    S = matrix(c(),,)
    mu = matrix(c(),,)
    n = 
    p = 
    alfa =
    n_p = n-p

    # Computation Part
    ## Calculate T Square
    T2=n*t(Xbar-mu)%*%solve(S)%*%(Xbar-mu)
    paste("Hotelling's T2 is:",T2)

    ## Calculate Critical Value
    T2_cri=(((n-1)*p)/(n-p))*qf(alfa,p,n_p,lower.tail = FALSE)
    paste("Critical value: ",T2_cri)

    ## Conclusion
    if(T2 < T2_cri){
      paste("Since T2 = ",T2, "< Critical Value = ",T2_cri,
          "so we cannot reject H0 at the significant level", alfa)
    }else if(T2 = T2_cri){
       paste("Since T2 = ",T2, "= Critical Value = ",T2_cri,
          "so we cannot reject H0 at the significant level", alfa)
    }else{
      paste("Since T2 = ",T2, "> Critical Value = ",T2_cri,
          "so we reject H0 at the significant level", alfa)
    }

**Explaination:**

- Xbar = mean of the sample

- mu = plausible value for the population mean

- S = covariance matrix

- n = number of sample

- p = number of variable

- alfa = significant level

- n_p = number of sample - number of variable

**Example 3.1:**

``` r
# Input Part
Xbar = matrix(c(4.64,45.4,9.965),3,1)
S = matrix(c(2.879,10.01,-1.81,10.01,199.788,-5.64,-1.81,-5.64,3.628),3,3)
mu = matrix(c(4,50,10),3,1)
n = 20
p = 3
alfa = 0.05
n_p = n-p

# Computation Part
## Calculate T Square
T2=n*t(Xbar-mu)%*%solve(S)%*%(Xbar-mu)
paste("Hotelling's T2 is:",T2)
```

    ## [1] "Hotelling's T2 is: 9.74303756432536"

``` r
## Calculate Critical Value
T2_cri=(((n-1)*p)/(n-p))*qf(alfa,p,n_p,lower.tail = FALSE)
paste("Critical value: ",T2_cri)
```

    ## [1] "Critical value:  10.7186047019865"

``` r
## Conclusion
if(T2 < T2_cri){
  paste("Since T2 = ",T2, "< Critical Value = ",T2_cri,
      "so we cannot reject H0 at the significant level", alfa)
}else if(T2 == T2_cri){
   paste("Since T2 = ",T2, "= Critical Value = ",T2_cri,
      "so we cannot reject H0 at the significant level", alfa)
}else{
  paste("Since T2 = ",T2, "> Critical Value = ",T2_cri,
      "so we reject H0 at the significant level", alfa)
}
```

    ## [1] "Since T2 =  9.74303756432536 < Critical Value =  10.7186047019865 so we cannot reject H0 at the significant level 0.05"

#### 1.2 Hotelling’s Testing using packages Installing the package:

``` r
library(DescTools)
```

    ## Warning: package 'DescTools' was built under R version 4.1.3

``` r
library(MASS)
```

    ## Warning: package 'MASS' was built under R version 4.1.3

**The computation:**

    # Input Part
    x = matrix(c(),,)
    mu0 = c()

    # Computation Part
    ## Hotelling's T2 Test using F distribution
    HotellingsT2Test(x,mu=mu0)
    ## Hotelling's T2 Test using Chi-squared distribution
    HotellingsT2Test(x,mu=mu0,test="chi")

**Explaination:**

- x = a numeric dataframe or matrix

- mu0 = plausible value for the population mean

**Example 3.2:**

``` r
# Input Part
x=matrix(c(6,10,8,9,6,3),3,2)
x
```

    ##      [,1] [,2]
    ## [1,]    6    9
    ## [2,]   10    6
    ## [3,]    8    3

``` r
mu0=c(9,5)

# Computation Part
## Hotelling's T2 Test using F distribution
HotellingsT2Test(x,mu=mu0)
```

    ## 
    ##  Hotelling's one sample T2-test
    ## 
    ## data:  x
    ## T.2 = 0.19444, df1 = 2, df2 = 1, p-value = 0.8485
    ## alternative hypothesis: true location is not equal to c(9,5)

``` r
## Hotelling's T2 Test using Chi-squared distribution
HotellingsT2Test(x,mu=mu0,test="chi")
```

    ## 
    ##  Hotelling's one sample T2-test
    ## 
    ## data:  x
    ## T.2 = 0.77778, df = 2, p-value = 0.6778
    ## alternative hypothesis: true location is not equal to c(9,5)

### **2. Confidence Regions and Simultaneous Comparisons of Component Means**

#### **2.1 The 100(1-alfa)% Simultaneous T2 Intervals for the two components means**

**The computation:**

    # Input Part
    Xbar=matrix(c(),,)
    S = matrix(c(),,)
    n =
    p =
    alfa =
    df1 = 1 - alfa
    n_p = n-p

    # Computation Part
    L1=Xbar[1,1]-(sqrt(((n-1)*p)/(n-p)*qf(df1,p,n_p))*sqrt(S[1,1]/n))
    U1=Xbar[1,1]+(sqrt(((n-1)*p)/(n-p)*qf(df1,p,n_p))*sqrt(S[1,1]/n))
    paste("The lower bound L1 : ",L1,"/ The upper bound U1 : ",U1)

**Example 3.3:**

``` r
# Input Part
Xbar = matrix(c(4.64,45.4,9.965),3,1)
S = matrix(c(2.879,10.01,-1.81,10.01,199.788,-5.64,-1.81,-5.64,3.628),3,3)
n = 20
p = 3
alfa = 0.05
df1 = 1 - alfa
n_p = n-p

# Computation Part
L1=Xbar[1,1]-(sqrt(((n-1)*p)/(n-p)*qf(df1,p,n_p))*sqrt(S[1,1]/n))
U1=Xbar[1,1]+(sqrt(((n-1)*p)/(n-p)*qf(df1,p,n_p))*sqrt(S[1,1]/n))
paste("The lower bound L1 : ",L1,"/ The upper bound U1 : ",U1)
```

    ## [1] "The lower bound L1 :  3.39784737376965 / The upper bound U1 :  5.88215262623035"

#### 2.2 The simultaneous 100(1-alfa)% Bonferroni Confidence interval

**The Computation:**

    # Input Part
    Xbar=matrix(c(),,)
    S = matrix(c(),,)
    n =
    p =
    alfa =
    df1 = 1 - (alfa/(2*p))
    df2 = n-1

    # Computation Part
    L_1=Xbar[1,1]-((qt(df1,df2))*sqrt(S[1,1]/n))
    U_1=Xbar[1,1]+((qt(df1,df2))*sqrt(S[1,1]/n))
    paste("The lower bound L1 : ",L_1,"/ The upper bound U1 : ",U_1)

**Example 3.4:**

``` r
# Input Part
Xbar = matrix(c(4.64,45.4,9.965),3,1)
S = matrix(c(2.879,10.01,-1.81,10.01,199.788,-5.64,-1.81,-5.64,3.628),3,3)
n = 20
p = 3
alfa = 0.05
df1 = 1 - (alfa/(2*p))
df2 = n-1

# Computation Part
L_1=Xbar[1,1]-((qt(df1,df2))*sqrt(S[1,1]/n))
U_1=Xbar[1,1]+((qt(df1,df2))*sqrt(S[1,1]/n))
paste("The lower bound L1 : ",L_1,"/ The upper bound U1 : ",U_1)
```

    ## [1] "The lower bound L1 :  3.64401530485706 / The upper bound U1 :  5.63598469514294"

## B. COMPARING MEAN VECTORS FROM TWO INDEPENDENT POPULATIONS

### 1. Assumption Testing - Homogeneity of covariance matrices

#### 1.1 Using Package Installing package

``` r
library(biotools)
```

    ## Warning: package 'biotools' was built under R version 4.1.3

    ## ---
    ## biotools version 4.2

**The computation:**

    # Input Part
    ## Sample 1
    vecmu1 = matrix(c(),,)
    Sigma1 = matrix(c(),,)
    n1 = 
    set.seed(123)
    sample1=mvrnorm(n1,vecmu1,Sigma1)

    ## Sample 2
    vecmu2= matrix(c(),,)
    Sigma2 = matrix(c(),,)
    n2 =
    set.seed(321)
    sample2=mvrnorm(n2,vecmu2,Sigma2)
    head(sample2)

    # Computation Part
    nrow = n1+n2
    c1 = matrix(0,nrow,1)
    head(c1)
    c1[1:n1]=1
    c1[n1+1:nrow]=2
    head(c1) #show the first six rows of the c1
    tail(c1) #show the last six rows of c1

    # Concatenate data 1 and data 2
    sample_merge = rbind(sample1,sample2)
    sample_merge

    results = boxM(data=sample_merge,group=c1)
    results

**Example:**

``` r
# Input Part
## Sample 1
vecmu1 = matrix(c(-4,4),2,1)
Sigma1 = matrix(c(16,-2,-2,9),2,2)
n1 = 15
set.seed(123)
sample1=mvrnorm(n1,vecmu1,Sigma1)

## Sample 2
vecmu2= matrix(c(3,2),2,1)
Sigma2 = matrix(c(7,5,5,12),2,2)
n2 = 18
set.seed(321)
sample2=mvrnorm(n2,vecmu2,Sigma2)
head(sample2)
```

    ##           [,1]     [,2]
    ## [1,] 5.5103467 8.234181
    ## [2,] 0.7950548 0.111115
    ## [3,] 0.8894439 2.034941
    ## [4,] 2.9357250 1.493331
    ## [5,] 1.0844439 2.617797
    ## [6,] 5.3512240 1.771559

``` r
# Computation Part
nrow = n1+n2
c1 = matrix(0,nrow,1)
head(c1)
```

    ##      [,1]
    ## [1,]    0
    ## [2,]    0
    ## [3,]    0
    ## [4,]    0
    ## [5,]    0
    ## [6,]    0

``` r
c1[1:n1]=1
c1[(n1+1):nrow]=2
head(c1) #show the first six rows of the c1
```

    ##      [,1]
    ## [1,]    1
    ## [2,]    1
    ## [3,]    1
    ## [4,]    1
    ## [5,]    1
    ## [6,]    1

``` r
tail(c1) #show the last six rows of c1
```

    ##       [,1]
    ## [28,]    2
    ## [29,]    2
    ## [30,]    2
    ## [31,]    2
    ## [32,]    2
    ## [33,]    2

``` r
# Concatenate data 1 and data 2
sample_merge = rbind(sample1,sample2)
sample_merge
```

    ##             [,1]       [,2]
    ##  [1,] -3.1322443 -1.6108443
    ##  [2,] -3.4673482  2.3595178
    ##  [3,] -8.6562247 11.1580161
    ##  [4,] -4.8009419  2.1009176
    ##  [5,] -4.1549088  5.4647142
    ##  [6,] -9.9419932  8.7932015
    ##  [7,] -5.6484219  5.0940852
    ##  [8,]  1.7375988  5.5655994
    ##  [9,] -0.7564780  5.3333290
    ## [10,] -1.7818427  5.2929309
    ## [11,] -7.5503481 10.0214833
    ## [12,] -6.0397142  2.0190970
    ## [13,] -5.6894484  3.9868506
    ## [14,] -3.5848260  7.3166773
    ## [15,] -2.7522651 -0.1065934
    ## [16,]  5.5103467  8.2341812
    ## [17,]  0.7950548  0.1111150
    ## [18,]  0.8894439  2.0349414
    ## [19,]  2.9357250  1.4933314
    ## [20,]  1.0844439  2.6177966
    ## [21,]  5.3512240  1.7715595
    ## [22,]  5.7593925  3.6138172
    ## [23,]  3.3163300  2.8691403
    ## [24,]  7.6132230  0.6974787
    ## [25,]  1.1705787  0.6102549
    ## [26,]  5.5945054  1.9843307
    ## [27,]  6.8303480  6.4122950
    ## [28,]  5.9587880  1.0313813
    ## [29,]  7.2905293 10.5057686
    ## [30,] -0.4223532 -1.1521998
    ## [31,] -0.7136533  0.6205268
    ## [32,]  4.1913898  3.3463793
    ## [33,]  3.6657706  3.5080341

``` r
results = boxM(data=sample_merge,group=c1)
results
```

    ## 
    ##  Box's M-test for Homogeneity of Covariance Matrices
    ## 
    ## data:  sample_merge
    ## Chi-Sq (approx.) = 10.001, df = 3, p-value = 0.01856

#### 1.2 Manual Way

##### 1.2.1 X2 Approximation The Computation

**The computation, for g = 2**

    # Input Part
    S1 = matrix(c(),,)
    S2 = matrix(c(),,)
    n1 =
    n2 =
    v1 = n1-1
    v2 = n2-1
    g =
    p =
    Sp = (v1*S1+v2*s2)/(n1+n2-2)
    alfa =
    df1 = 1-alfa
    df2 = (1/2)*(g-1)*p*(p+1)

    # Computation Part
    lnM = ((1/2)*((v1*log(det(S1)))+(v2*log(det(S2)))))-((1/2)*(v1+v2)*log(det(Sp)))
    paste("lnM: ", lnM)

    c1 = ((1/v1)+(1/v2)-(1/(v1+v2)))*(((2*p^2)+(3*p)-1)/(6*(p+1)*(g-1)))
    paste("c1: ",c1)

    U = -2*(1-c1)*lnM
    cri_val = qchisq(df1,df2)

    # Conclusion
    if(U < cri_val){
        paste("Since U =", U, " < critical value = ", cri_val,", then do not reject H0.")
    }else if(U == cri_val){
        paste("Since U =", U, " = critical value = ", cri_val,", then do not reject H0.")
    }else{
        paste("Since U =", U, " > critical value = ", cri_val,", then reject H0.")
    }

**Example:**

``` r
# Input Part
S1 = matrix(c(2,1,1,6),2,2)
S2 = matrix(c(2,1,1,4),2,2)
n1 = 50
n2 = 50
v1 = n1-1
v2 = n2-1
g = 2
p = 2
Sp = ((v1*S1)+(v2*S2))/(n1+n2-2)
alfa = 0.05
df1 = 1-alfa
df2 = (1/2)*(g-1)*p*(p+1)

# Computation Part
lnM = ((1/2)*((v1*log(det(S1)))+(v2*log(det(S2)))))-((1/2)*(v1+v2)*log(det(Sp)))
paste("lnM: ", lnM)
```

    ## [1] "lnM:  -1.2407714540595"

``` r
c1 = ((1/v1)+(1/v2)-(1/(v1+v2)))*(((2*p^2)+(3*p)-1)/(6*(p+1)*(g-1)))
paste("c1: ",c1)
```

    ## [1] "c1:  0.022108843537415"

``` r
U = -2*(1-c1)*lnM
cri_val = qchisq(df1,df2)

# Conclusion
if(U < cri_val){
    paste("Since U =", U, " < critical value = ", cri_val,", then do not reject H0.")
}else if(U == cri_val){
    paste("Since U =", U, " = critical value = ", cri_val,", then do not reject H0.")
}else{
    paste("Since U =", U, " > critical value = ", cri_val,", then reject H0.")
}
```

    ## [1] "Since U = 2.42667886423201  < critical value =  7.81472790325118 , then do not reject H0."

##### 1.2.2 F Approximation The Computation (continuity from X2 Approximation):

**The computation:**

    # Computation Part
    c2 = ((1/v1^2)+(1/v2^2)-(1/(v1+v2)^2))*(((p-1)*(p+2))/(6*(g-1)))
    paste("c1: ",c1)
    a1 = 1/2*(g-1)*p*(p+1)
    a2 = (a1+2)/abs(c2-c1^2)
    b1 = (1-c1-(a1/a2))/a1
    b2 = (1-c1+(2/a2))/a2

    if(c2 > c1^2){
        F = -2*b1*lnM
    }else if(c2 < c1^2){
        F = (-2*a2*b2*lnM)/(a1*(1+(2*b2*lnM)))
    }else{
        F = NULL
    }
    cri_val = qf(df1,a1,a2)

    # Conclusion
    if(is.null (F)==0){
        if(F<cri_val){
            paste("Since F =", F, " < critical value = ", cri_val,", then do not reject H0.")
        }else if(F==cri_val){
            paste("Since F =", F, " = critical value = ", cri_val,", then do not reject H0.")
        }else{
            paste("Since F =", F, " > critical value = ", cri_val,", then reject H0.")
        }
    }else{
        print("we cannot conclude the distribution of F.")
    }

**Continuity example 3.10:**

``` r
# Computation Part
c2 = ((1/v1^2)+(1/v2^2)-(1/(v1+v2)^2))*(((p-1)*(p+2))/(6*(g-1)))
paste("c1: ",c1)
```

    ## [1] "c1:  0.022108843537415"

``` r
a1 = 1/2*(g-1)*p*(p+1)
a2 = (a1+2)/abs(c2-c1^2)
b1 = (1-c1-(a1/a2))/a1
b2 = (1-c1+(2/a2))/a2

if(c2 > c1^2){
    F = -2*b1*lnM
}else if(c2 < c1^2){
    F = (-2*a2*b2*lnM)/(a1*(1+(2*b2*lnM)))
}else{
    F = NULL
}
cri_val = qf(df1,a1,a2)

# Conclusion
if(is.null (F)==0){
    if(F<cri_val){
        paste("Since F =", F, " < critical value = ", cri_val,", then do not reject H0.")
    }else if(F==cri_val){
        paste("Since F =", F, " = critical value = ", cri_val,", then do not reject H0.")
    }else{
        paste("Since F =", F, " > critical value = ", cri_val,", then reject H0.")
    }
}else{
    print("we cannot conclude the distribution of F.")
}
```

    ## [1] "Since F = 0.808895047212868  < critical value =  2.60490930108373 , then do not reject H0."

### 2. Two Sample when Sigma1=Sigma2

#### 2.1 Hotelling’s Testing Manual Computation

**The computation**

    # Input Part
    s1=matrix(c(),,)
    s2=matrix(c(),,)
    xbar1=matrix(c(),,)
    xbar2=matrix(c(),,)
    n1=
    n2=
    p =
    Sp=(((n1-1)/(n1+n2-2))*s1)+(((n2-1)/(n1+n2-2))*s2)
    alfa =
    df1 = 1-alfa
    df2 = n1+n2-p-1

    # Computation Part
    ## Calculate T2
    T2=t(xbar1-xbar2)%*%solve(((1/n1)+(1/n2))*Sp)%*%(xbar1-xbar2)
    paste("The T2 value : ",T2)

    ## Calculate Critical Value
    cri_val=((n1+n2-2)*p)/(n1+n2-p-1)*qf(df1,p,df2)
    paste("the critical value : ", cri_val)

    ## Conclusion
    if(T2 < cri_val){
      paste("Since T2 = ",T2, "< Critical Value = ",cri_val,
          "so we cannot reject H0 at the significant level", alfa)
    }else if(T2 == cri_val){
       paste("Since T2 = ",T2, "= Critical Value = ",cri_val,
          "so we cannot reject H0 at the significant level", alfa)
    }else{
      paste("Since T2 = ",T2, "> Critical Value = ",cri_val,
          "so we reject H0 at the significant level", alfa)
    }

**Example 3.5:**

``` r
# Input Part
s1=matrix(c(2,1,1,6),2,2)
s2=matrix(c(2,1,1,4),2,2)
xbar1=matrix(c(8.3,4.1),2,1)
xbar2=matrix(c(10.2,3.9),2,1)
n1= 50
n2= 50
p = 2
Sp=(((n1-1)/(n1+n2-2))*s1)+(((n2-1)/(n1+n2-2))*s2)
alfa = 0.05
df1 = 1-alfa
df2 = n1+n2-p-1

# Computation Part
## Calculate T2
T2=t(xbar1-xbar2)%*%solve(((1/n1)+(1/n2))*Sp)%*%(xbar1-xbar2)
paste("The T2 value : ",T2)
```

    ## [1] "The T2 value :  52.4722222222221"

``` r
## Calculate Critical Value
cri_val=((n1+n2-p)*2)/(n1+n2-p-1)*qf(df1,p,df2)
paste("the critical value : ", cri_val)
```

    ## [1] "the critical value :  6.24408853948819"

``` r
## Conclusion
if(T2 < cri_val){
  paste("Since T2 = ",T2, "< Critical Value = ",cri_val,
      "so we cannot reject H0 at the significant level", alfa)
}else if(T2 == cri_val){
   paste("Since T2 = ",T2, "= Critical Value = ",cri_val,
      "so we cannot reject H0 at the significant level", alfa)
}else{
  paste("Since T2 = ",T2, "> Critical Value = ",cri_val,
      "so we reject H0 at the significant level", alfa)
}
```

    ## [1] "Since T2 =  52.4722222222221 > Critical Value =  6.24408853948819 so we reject H0 at the significant level 0.05"

#### 2.2 Hypothesis Testing Using Package Installing the package

``` r
library(corpcor)
library(Hotelling)
```

Simulate 2 samples from two independent samples with common covariance
matrix.

**The computation:**

    # Input Part
    ## Sample 1
    vecmu1 = matrix(c(),,)
    Sigma1 = matrix(c(),,)
    n1 = 
    set.seed(123)
    sample1=mvrnorm(n1,vecmu1,Sigma1)

    ## Sample 2
    vecmu2= matrix(c(),,)
    Sigma2 = matrix(c(),,)
    n2 =
    set.seed(321)
    sample2=mvrnorm(n2,vecmu2,Sigma2)
    head(sample2)

    # Computation Part
    Htest1 = hotelling.test(sample1,sample2,var.equal=TRUE)
    Htest1

**Explaination:**

- sample1 = matrix containing data points from sample 1

- sample2 = matrix containing data points from sample 2

- var.equal = assumption of the variance, TRUE if equal and FALSE if not
  equal

**Example:**

``` r
# Input Part
## Sample 1
vecmu1 = matrix(c(-4,4),2,1)
Sigma1 = matrix(c(16,-2,-2,9),2,2)
n1 = 15
set.seed(123)
sample1=mvrnorm(n1,vecmu1,Sigma1)

## Sample 2
vecmu2= matrix(c(3,2),2,1)
Sigma2 = matrix(c(16,-2,-2,9),2,2)
n2 = 18
set.seed(321)
sample2=mvrnorm(n2,vecmu2,Sigma2)
head(sample2)
```

    ##           [,1]         [,2]
    ## [1,] -4.131078  2.154652686
    ## [2,]  5.464656  0.001495897
    ## [3,]  3.407248 -0.870009030
    ## [4,]  3.550146  2.176263288
    ## [5,]  2.748896 -0.909195642
    ## [6,]  2.747029  5.295693290

``` r
# Computation Part
Htest1 = hotelling.test(sample1,sample2,var.equal=TRUE)
Htest1
```

    ## Test stat:  31.314 
    ## Numerator df:  2 
    ## Denominator df:  30 
    ## P-value:  2.829e-05

#### 2.3 The 100(1-alfa)% simultaneous confidence intervals

**The computation:**

    # Input Part
    xbar1 = matrix(c(),,)
    xbar2 = matrix(c(),,)
    S1 = matrix(c(),,)
    S2 = matrix(c(),,)
    n1 =
    n2 =
    p =
    Sp=(((n1-1)/(n1+n2-2))*s1)+(((n2-1)/(n1+n2-2))*s2)
    alfa = 0.05
    df1 = 1-alfa
    df2 = n1+n2-p-1
    c2 = ((n1+n2-2)*2)/(n1+n2-2-1)*qf(df1,p,df2)

    # Computation Part
    L1=(xbar1[1,1]-xbar2[1,1])-(sqrt(c2)*sqrt(((1/n1)+(1/n2))*Sp[1,1]))
    paste("The lower bound L1: ",L1)

    U1=(xbar1[1,1]-xbar2[1,1])+(sqrt(c2)*sqrt(((1/n1)+(1/n2))*Sp[1,1]))
    paste("The upper bound U1: ",U1)

**Example 3.6:**

``` r
# Input Part
s1=matrix(c(2,1,1,6),2,2)
s2=matrix(c(2,1,1,4),2,2)
xbar1=matrix(c(8.3,4.1),2,1)
xbar2=matrix(c(10.2,3.9),2,1)
n1= 50
n2= 50
p = 2
Sp=(((n1-1)/(n1+n2-2))*s1)+(((n2-1)/(n1+n2-2))*s2)
alfa = 0.05
df1 = 1-alfa
df2 = n1+n2-p-1
c2 = ((n1+n2-2)*2)/(n1+n2-2-1)*qf(df1,p,df2)

# Computation Part
L1=(xbar1[1,1]-xbar2[1,1])-(sqrt(c2)*sqrt(((1/n1)+(1/n2))*Sp[1,1]))
paste("The lower bound L1: ",L1)
```

    ## [1] "The lower bound L1:  -2.60677229937162"

``` r
U1=(xbar1[1,1]-xbar2[1,1])+(sqrt(c2)*sqrt(((1/n1)+(1/n2))*Sp[1,1]))
paste("The upper bound U1: ",U1)
```

    ## [1] "The upper bound U1:  -1.19322770062837"

#### 2.4 The Bonferroni Confidence Interval

**The computation**

    # Input Part
    s1=matrix(c(),,)
    s2=matrix(c(),,)
    xbar1 = matrix(c(),,)
    xbar2 = matrix(c(),,)
    n1 =
    n2 =
    p =
    Sp=(((n1-1)/(n1+n2-2))*s1)+(((n2-1)/(n1+n2-2))*s2)
    alfa = 0.05
    df1 = 1-(alfa/(2*p))
    df2 = n1+n2-2

    # Computation Part
    L1 = (xbar1[1,1]-xbar2[1,1])-(qt(df1,df2)*sqrt(((1/n1)+(1/n2))*Sp[1,1]))
    paste("The lower bound L1: ",L1)

    U1 = (xbar1[1,1]-xbar2[1,1])+(qt(df1,df2)*sqrt(((1/n1)+(1/n2))*Sp[1,1]))
    paste("The lower bound U1: ",U1)

**Example 3.7:**

``` r
# Input Part
s1=matrix(c(2,1,1,6),2,2)
s2=matrix(c(2,1,1,4),2,2)
xbar1=matrix(c(8.3,4.1),2,1)
xbar2=matrix(c(10.2,3.9),2,1)
n1= 50
n2= 50
Sp=(((n1-1)/(n1+n2-2))*s1)+(((n2-1)/(n1+n2-2))*s2)
alfa = 0.05
df1 = 1-(alfa/(2*p))
df2 = n1+n2-2

# Computation Part
L1 = (xbar1[1,1]-xbar2[1,1])-(qt(df1,df2)*sqrt(((1/n1)+(1/n2))*Sp[1,1]))
paste("The lower bound L1: ",L1)
```

    ## [1] "The lower bound L1:  -2.54385234819145"

``` r
U1 = (xbar1[1,1]-xbar2[1,1])+(qt(df1,df2)*sqrt(((1/n1)+(1/n2))*Sp[1,1]))
paste("The lower bound U1: ",U1)
```

    ## [1] "The lower bound U1:  -1.25614765180855"

### 3. Two Sample when Sigma1=/Sigma2

#### 3.1 Hotelling’s Testing Manual Computation

**The computation**

    # Input Part
    s1=matrix(c(),,)
    s2=matrix(c(),,)
    xbar1=matrix(c(),,)
    xbar2=matrix(c(),,)
    n1=
    n2=
    s =(1/n1)*s1+(1/n2)*s2
    alfa =
    p =

    # Computation Part
    ## Calculate Stat-Value
    stat_val = t(xbar1-xbar2)%*%solve(s)%*%(xbar1-xbar2)
    paste("The Statistical value : ",stat_val)

    ## Calculate Critical Value
    cri_val=qchisq(1-alfa,p)
    paste("the critical value : ", cri_val)

    ## Conclusion
    if(stat_val < cri_val){
      paste("Since statistical value = ",stat_val, "< Critical Value = ",cri_val,
          "so we cannot reject H0 at the significant level", alfa)
    }else if(stat_val == cri_val){
       paste("Since statistical value = ",stat_val, "= Critical Value = ",cri_val,
          "so we cannot reject H0 at the significant level", alfa)
    }else{
      paste("Since statistical value = ",stat_val, "> Critical Value = ",cri_val,
          "so we reject H0 at the significant level", alfa)
    }

**Example 3.8:**

``` r
# Input Part
s1= matrix(c(13825.3,23823.4,23823.4,73107.4),2,2)
s2= matrix(c(8632.0,19616.7,19616.7,55964.5),2,2)
xbar1=matrix(c(204.4,556.6),2,1)
xbar2=matrix(c(130.0,355.0),2,1)
n1= 45
n2= 55
s =(1/n1)*s1+(1/n2)*s2
alfa = 0.05
p = 2

# Computation Part
## Calculate Stat-Value
stat_val = t(xbar1-xbar2)%*%solve(s)%*%(xbar1-xbar2)
paste("The Statistical value : ",stat_val)
```

    ## [1] "The Statistical value :  15.6585290974643"

``` r
## Calculate Critical Value
cri_val=qchisq(1-alfa,p)
paste("the critical value : ", cri_val)
```

    ## [1] "the critical value :  5.99146454710798"

``` r
## Conclusion
if(stat_val < cri_val){
  paste("Since statistical value = ",stat_val, "< Critical Value = ",cri_val,
      "so we cannot reject H0 at the significant level", alfa)
}else if(stat_val == cri_val){
   paste("Since statistical value = ",stat_val, "= Critical Value = ",cri_val,
      "so we cannot reject H0 at the significant level", alfa)
}else{
  paste("Since statistical value = ",stat_val, "> Critical Value = ",cri_val,
      "so we reject H0 at the significant level", alfa)
}
```

    ## [1] "Since statistical value =  15.6585290974643 > Critical Value =  5.99146454710798 so we reject H0 at the significant level 0.05"

#### 3.2 Hypothesis Testing Using Package Installing the package

``` r
library(corpcor)
library(Hotelling)
```

Simulate 2 samples from two independent samples with common covariance
matrix

    # Input Part
    ## Sample 1
    vecmu1 = matrix(c(),,)
    Sigma1 = matrix(c(),,)
    n1 = 
    set.seed(123)
    sample1=mvrnorm(n1,vecmu1,Sigma1)

    ## Sample 2
    vecmu2= matrix(c(),,)
    Sigma2 = matrix(c(),,)
    n2 =
    set.seed(321)
    sample2=mvrnorm(n2,vecmu2,Sigma2)
    head(sample2)

    # Computation Part
    Htest2 = hotelling.test(sample1,sample2,var.equal=FALSE)
    Htest2

**Explaination:**

- sample1 = matrix containing data points from sample 1

- sample2 = matrix containing data points from sample 2

- var.equal = assumption of the variance, TRUE if equal and FALSE if not
  equal

**Example:**

``` r
# Input Part
## Sample 1
vecmu1 = matrix(c(-4,4),2,1)
Sigma1 = matrix(c(16,-2,-2,9),2,2)
n1 = 15
set.seed(123)
sample1=mvrnorm(n1,vecmu1,Sigma1)

## Sample 2
vecmu2= matrix(c(3,2),2,1)
Sigma2 = matrix(c(7,5,5,12),2,2)
n2 = 18
set.seed(321)
sample2=mvrnorm(n2,vecmu2,Sigma2)
head(sample2)
```

    ##           [,1]     [,2]
    ## [1,] 5.5103467 8.234181
    ## [2,] 0.7950548 0.111115
    ## [3,] 0.8894439 2.034941
    ## [4,] 2.9357250 1.493331
    ## [5,] 1.0844439 2.617797
    ## [6,] 5.3512240 1.771559

``` r
# Computation Part
Htest2 = hotelling.test(sample1,sample2,var.equal=FALSE)
Htest2
```

    ## Test stat:  66.68 
    ## Numerator df:  2 
    ## Denominator df:  25.7962004275097 
    ## P-value:  9.553e-08

#### **3.3 Confidence Interval**

    # Input Part
    xbar1 = matrix(c(),,)
    xbar2 = matrix(c(),,)
    S1 = matrix(c(),,)
    S2 = matrix(c(),,)
    n1 =
    n2 =
    p =
    s =(1/n1)*s1+(1/n2)*s2
    alfa = 0.05
    df1 = 1-alfa

    # Computation Part
    L1=(xbar1[1,1]-xbar2[1,1])-(sqrt(qchisq(df1,p))*sqrt(s[1,1]))
    paste("The lower bound L1: ",L1)

    U1=(xbar1[1,1]-xbar2[1,1])+(sqrt(qchisq(df1,p))*sqrt(s[1,1]))
    paste("The upper bound U1: ",U1)

**Example:**

``` r
# Input Part
s1= matrix(c(13825.3,23823.4,23823.4,73107.4),2,2)
s2= matrix(c(8632.0,19616.7,19616.7,55964.5),2,2)
xbar1=matrix(c(204.4,556.6),2,1)
xbar2=matrix(c(130.0,355.0),2,1)
n1= 45
n2= 55
p = 2
s =(1/n1)*s1+(1/n2)*s2
alfa = 0.05
df1 = 1-alfa

# Computation part
L1=(xbar1[1,1]-xbar2[1,1])-(sqrt(qchisq(df1,p))*sqrt(s[1,1]))
paste("The lower bound L1: ",L1)
```

    ## [1] "The lower bound L1:  21.664014919943"

``` r
U1=(xbar1[1,1]-xbar2[1,1])+(sqrt(qchisq(df1,p))*sqrt(s[1,1]))
paste("The upper bound U1: ",U1)
```

    ## [1] "The upper bound U1:  127.135985080057"

## C. PAIRED COMPARISON

### 1.1 Hypothesis Testing Paired Comparison - 2 Dependent Sample Using Package

``` r
# Install Package
library(DescTools)
```

**The Computation**

    # Input Part
    data1= matrix(c(),,)
    data2= matrix(c(),,)
    diff = data1-data2
    muH0 = c()

    # Computation Part
    Htest = HotellingsT2Test(diff, mu=muH0)

**Example:**

``` r
# Input Part
data1= matrix(c(6,6,18,8,11,34,28,71,43,33,20,27,23,64,44,30,75,26,124,54,30,14),11,2)
data2= matrix(c(25,28,36,35,15,44,42,54,34,29,39,15,13,22,29,31,64,30,64,56,20,21),11,2)
diff = data1-data2
muH0 = c(0,0)

# Computation Part
Htest = HotellingsT2Test(diff, mu=muH0)
Htest
```

    ## 
    ##  Hotelling's one sample T2-test
    ## 
    ## data:  diff
    ## T.2 = 6.1377, df1 = 2, df2 = 9, p-value = 0.02083
    ## alternative hypothesis: true location is not equal to c(0,0)

### 1.2 Hypothesis Testing Paired Comparison - 2 Dependent Sample Manual Way

**The computation**

    # Input Part
    x1 = matrix(c(),,)
    x2 = matrix(c(),,)
    d = x1-x2
    dmean = colMeans(d)
    dbar = matrix(c(dmean[1],dmean[2]),2,1)
    sd = cov(d)
    n = 
    p = 
    alfa =
    df1 = 1-alfa
    df2 = n-p

    # Computation Part
    ## Statistical Value
    T2 = n*t(dbar)%*%solve(sd)%*%dbar
    paste("The Statistical value : ",T2)

    ## Critical Value
    cri_val=(((n-1)*p)/(n-p))*qf(df1,p,df2)
    paste("The Critical value : ",cri_val)

    ## Conclusion
    if(T2 < cri_val){
      paste("Since statistical value = ",T2, "< Critical Value = ",cri_val,
          "so we cannot reject H0 at the significant level", alfa)
    }else if(T2 == cri_val){
       paste("Since statistical value = ",T2, "= Critical Value = ",cri_val,
          "so we cannot reject H0 at the significant level", alfa)
    }else{
      paste("Since statistical value = ",T2, "> Critical Value = ",cri_val,
          "so we reject H0 at the significant level", alfa)
    }

**Example:**

``` r
# Input Part
x1 = matrix(c(6,6,18,8,11,34,28,71,43,33,20,27,23,64,44,30,75,26,124,54,30,14),11,2)
x2 = matrix(c(25,28,36,35,15,44,42,54,34,29,39,15,13,22,29,31,64,30,64,56,20,21),11,2)
d = x1-x2
dmean = colMeans(d)
dbar = matrix(c(dmean[1],dmean[2]),2,1)
sd = cov(d)
n = 11
p = 2
alfa = 0.05
df1 = 1-alfa
df2 = n-p

# Computation Part
## Statistical Value
T2 = n*t(dbar)%*%solve(sd)%*%dbar
paste("The Statistical value : ",T2)
```

    ## [1] "The Statistical value :  13.6393121401747"

``` r
## Critical Value
cri_val=(((n-1)*p)/(n-p))*qf(df1,p,df2)
paste("The Critical value : ",cri_val)
```

    ## [1] "The Critical value :  9.45887717576388"

``` r
## Conclusion
if(T2 < cri_val){
  paste("Since statistical value = ",T2, "< Critical Value = ",cri_val,
      "so we cannot reject H0 at the significant level", alfa)
}else if(T2 == cri_val){
   paste("Since statistical value = ",T2, "= Critical Value = ",cri_val,
      "so we cannot reject H0 at the significant level", alfa)
}else{
  paste("Since statistical value = ",T2, "> Critical Value = ",cri_val,
      "so we reject H0 at the significant level", alfa)
}
```

    ## [1] "Since statistical value =  13.6393121401747 > Critical Value =  9.45887717576388 so we reject H0 at the significant level 0.05"

### 1.3 The 100(1-alfa)% Confidence Interval

**The computation:**

    # Input Part
    x1 = matrix(c(),,)
    x2 = matrix(c(),,)
    d = x1-x2
    dmean = colMeans(d)
    dbar = matrix(c(dmean[1],dmean[2]),2,1)
    sd = cov(d)
    n = 
    p = 
    alfa =
    df1 = 1-alfa
    df2 = n-p

    # Computation Part
    L1 = dbar[1,1]-(sqrt(((n-1)*p/(n-p))*qf(df1,p,df2))*sqrt(sd[1,1]/n))
    paste("The lower bound L1: ",L1)
    U1 = dbar[1,1]+(sqrt(((n-1)*p/(n-p))*qf(df1,p,df2))*sqrt(sd[1,1]/n))
    paste("The Upper bound U1: ",U1)

**Example:**

``` r
# Input Part
x1 = matrix(c(6,6,18,8,11,34,28,71,43,33,20,27,23,64,44,30,75,26,124,54,30,14),11,2)
x2 = matrix(c(25,28,36,35,15,44,42,54,34,29,39,15,13,22,29,31,64,30,64,56,20,21),11,2)
d = x1-x2
dmean = colMeans(d)
dbar = matrix(c(dmean[1],dmean[2]),2,1)
sd = cov(d)
n = 11
p = 2
alfa = 0.05
df1 = 1-alfa
df2 = n-p

# Computation Part
L1 = dbar[1,1]-(sqrt(((n-1)*p/(n-p))*qf(df1,p,df2))*sqrt(sd[1,1]/n))
paste("The lower bound L1: ",L1)
```

    ## [1] "The lower bound L1:  -22.4532723477659"

``` r
U1 = dbar[1,1]+(sqrt(((n-1)*p/(n-p))*qf(df1,p,df2))*sqrt(sd[1,1]/n))
paste("The Upper bound U1: ",U1)
```

    ## [1] "The Upper bound U1:  3.72599962049317"

### 1.4 The 100(1-alfa)% Bonfferoni Confidence Interval

**The Computation**

    # Input Part
    x1 = matrix(c(),,)
    x2 = matrix(c(),,)
    d = x1-x2
    dmean = colMeans(d)
    dbar = matrix(c(dmean[1],dmean[2]),2,1)
    sd = cov(d)
    n = 
    p = 
    alfa =
    df1 = 1-(alfa/(2*p))
    df2 = n-1

    # Computation Part
    L1 = dbar[1,1]-(qt(df1,df2)*sqrt(sd[1,1]/n))
    paste("The lower bound L1: ",L1)

    U1 = dbar[1,1]+(qt(df1,df2)*sqrt(sd[1,1]/n))
    paste("The lower bound U1: ",U1)

**Example:**

``` r
# Input Part
x1 = matrix(c(6,6,18,8,11,34,28,71,43,33,20,27,23,64,44,30,75,26,124,54,30,14),11,2)
x2 = matrix(c(25,28,36,35,15,44,42,54,34,29,39,15,13,22,29,31,64,30,64,56,20,21),11,2)
d = x1-x2
dmean = colMeans(d)
dbar = matrix(c(dmean[1],dmean[2]),2,1)
sd = cov(d)
n = 11
p = 2
alfa = 0.05
df1 = 1-(alfa/(2*p))
df2 = n-1

# Computation Part
L1 = dbar[1,1]-(qt(df1,df2)*sqrt(sd[1,1]/n))
paste("The lower bound L1: ",L1)
```

    ## [1] "The lower bound L1:  -20.5731072688261"

``` r
U1 = dbar[1,1]+(qt(df1,df2)*sqrt(sd[1,1]/n))
paste("The lower bound U1: ",U1)
```

    ## [1] "The lower bound U1:  1.84583454155338"
