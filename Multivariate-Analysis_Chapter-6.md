Chapter 6 Factor Analysis
================
Oktsa Dwika Rahmashari
2023-10-20

# FACTOR ANALYSIS

## Install Packages

Install the package ‘psych’ and ‘GPArotation’

``` r
library(psych)
library(GPArotation)
```

    ## 
    ## Attaching package: 'GPArotation'

    ## The following objects are masked from 'package:psych':
    ## 
    ##     equamax, varimin

## Input Part

Import the data

``` r
data = read.csv("C:/Users/Avita/Documents/Multivariate-Analysis/Data/EFA.csv",header=T)
head(data)
```

    ##   Price Safety Exterior_Looks Space_comfort Technology After_Sales_Service
    ## 1     4      4              5             4          3                   4
    ## 2     3      5              3             3          4                   4
    ## 3     4      4              3             4          5                   5
    ## 4     4      4              4             3          3                   4
    ## 5     5      5              4             4          5                   4
    ## 6     4      4              5             3          4                   5
    ##   Resale_Value Fuel_Type Fuel_Efficiency Color Maintenance Test_drive
    ## 1            5         4               4     2           4          2
    ## 2            3         4               3     4           3          2
    ## 3            5         4               5     4           5          4
    ## 4            5         5               4     4           4          2
    ## 5            5         3               4     5           5          5
    ## 6            3         4               3     2           3          2
    ##   Product_reviews Testimonials
    ## 1               4            3
    ## 2               2            2
    ## 3               4            3
    ## 4               5            3
    ## 5               5            2
    ## 6               2            3

## Computation Part

### 1. Check Correlation

Check the correlation among the features

``` r
datcorr = cor(data) # Calculate the correlation matrix stored in a variable named “datcorr”
datKMO =KMO(datcorr) #Calculate KMO statistics
print(datKMO$MSA) # Display KM values
```

    ## [1] 0.614451

### 2. Check Independent (Barlett’s Sphericity)

Calculate Bartlett’s Sphericity to check if the variables are
independent

``` r
datcorr = cor(data) # Calculate the correlation matrix stored in variable named “datcorr”
datKMO =KMO(datcorr) # Calculate KMO statistics.
n=90 # Specify the number of samples.
datBart=cortest.bartlett(datcorr,n) # Calculate Bartlett's Sphericity statistic.
print(datBart$p.value) # display p-value
```

    ## [1] 1.930071e-16

**Hypothesis Testing**

H0 :R=I (That is, the variables are not related to each other)

p-value \< 0.05, then reject H0. So, the data is related to each other

### 3. Compute Eigen Vector

Compute the eigen value to select the suitable number of factors

``` r
datEig = eigen(datcorr) #calculate the eigen value
datEigmean = mean(datEig$values) #calculate mean of eigen value
print(datEigmean)
```

    ## [1] 1

``` r
datEig$values>=1
```

    ##  [1]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [13] FALSE FALSE

``` r
numfac = sum(datEig$values>=1) #select eigen value that greater than mean of eigen value (1)
print(numfac)
```

    ## [1] 5

From the output, it can be seen that the number of factors is equal to
5.

### 4. Apply Factor based on PCA

Apply the factor based on PCA

``` r
datFa = principal(datcorr,nfactors=5,rotate="none")
datFa
```

    ## Principal Components Analysis
    ## Call: principal(r = datcorr, nfactors = 5, rotate = "none")
    ## Standardized loadings (pattern matrix) based upon correlation matrix
    ##                       PC1   PC2   PC3   PC4   PC5   h2   u2 com
    ## Price                0.50 -0.22 -0.33  0.36 -0.18 0.57 0.43 3.4
    ## Safety              -0.11  0.44 -0.31 -0.43  0.19 0.52 0.48 3.3
    ## Exterior_Looks      -0.07  0.36  0.11  0.74  0.15 0.71 0.29 1.6
    ## Space_comfort        0.36  0.72 -0.14  0.08 -0.16 0.71 0.29 1.7
    ## Technology           0.31  0.37 -0.12 -0.07 -0.37 0.39 0.61 3.2
    ## After_Sales_Service  0.52  0.38 -0.19 -0.23  0.42 0.68 0.32 3.6
    ## Resale_Value         0.44 -0.56 -0.29  0.24  0.24 0.71 0.29 3.3
    ## Fuel_Type            0.32  0.52 -0.37 -0.02 -0.18 0.54 0.46 2.8
    ## Fuel_Efficiency      0.74 -0.11  0.09 -0.12  0.30 0.68 0.32 1.5
    ## Color                0.46 -0.33  0.29 -0.54 -0.19 0.73 0.27 3.5
    ## Maintenance          0.66 -0.35 -0.09  0.04 -0.17 0.59 0.41 1.7
    ## Test_drive           0.38  0.24  0.46  0.10  0.50 0.67 0.33 3.5
    ## Product_reviews      0.59  0.04  0.29  0.19 -0.29 0.55 0.45 2.2
    ## Testimonials         0.12  0.31  0.75 -0.01 -0.18 0.70 0.30 1.5
    ## 
    ##                        PC1  PC2  PC3  PC4  PC5
    ## SS loadings           2.76 2.16 1.46 1.33 1.04
    ## Proportion Var        0.20 0.15 0.10 0.09 0.07
    ## Cumulative Var        0.20 0.35 0.46 0.55 0.63
    ## Proportion Explained  0.31 0.25 0.17 0.15 0.12
    ## Cumulative Proportion 0.31 0.56 0.73 0.88 1.00
    ## 
    ## Mean item complexity =  2.6
    ## Test of the hypothesis that 5 components are sufficient.
    ## 
    ## The root mean square of the residuals (RMSR) is  0.09 
    ## 
    ## Fit based upon off diagonal values = 0.8

from the output, known that the for PC5 only has 1 variable. The goals
for factor analysis is “grouping” thus we don’t want that PC has only 1
variable. So we reduce the number of factors

``` r
datFa1 = principal(datcorr,nfactors=4,rotate="none")
datFa1
```

    ## Principal Components Analysis
    ## Call: principal(r = datcorr, nfactors = 4, rotate = "none")
    ## Standardized loadings (pattern matrix) based upon correlation matrix
    ##                       PC1   PC2   PC3   PC4   h2   u2 com
    ## Price                0.50 -0.22 -0.33  0.36 0.54 0.46 3.1
    ## Safety              -0.11  0.44 -0.31 -0.43 0.49 0.51 2.9
    ## Exterior_Looks      -0.07  0.36  0.11  0.74 0.69 0.31 1.5
    ## Space_comfort        0.36  0.72 -0.14  0.08 0.68 0.32 1.6
    ## Technology           0.31  0.37 -0.12 -0.07 0.26 0.74 2.3
    ## After_Sales_Service  0.52  0.38 -0.19 -0.23 0.51 0.49 2.6
    ## Resale_Value         0.44 -0.56 -0.29  0.24 0.65 0.35 2.9
    ## Fuel_Type            0.32  0.52 -0.37 -0.02 0.51 0.49 2.5
    ## Fuel_Efficiency      0.74 -0.11  0.09 -0.12 0.59 0.41 1.1
    ## Color                0.46 -0.33  0.29 -0.54 0.69 0.31 3.2
    ## Maintenance          0.66 -0.35 -0.09  0.04 0.56 0.44 1.6
    ## Test_drive           0.38  0.24  0.46  0.10 0.42 0.58 2.6
    ## Product_reviews      0.59  0.04  0.29  0.19 0.47 0.53 1.7
    ## Testimonials         0.12  0.31  0.75 -0.01 0.67 0.33 1.4
    ## 
    ##                        PC1  PC2  PC3  PC4
    ## SS loadings           2.76 2.16 1.46 1.33
    ## Proportion Var        0.20 0.15 0.10 0.09
    ## Cumulative Var        0.20 0.35 0.46 0.55
    ## Proportion Explained  0.36 0.28 0.19 0.17
    ## Cumulative Proportion 0.36 0.64 0.83 1.00
    ## 
    ## Mean item complexity =  2.2
    ## Test of the hypothesis that 4 components are sufficient.
    ## 
    ## The root mean square of the residuals (RMSR) is  0.09 
    ## 
    ## Fit based upon off diagonal values = 0.78

``` r
summary(datFa1)
```

    ## 
    ## Factor analysis with Call: principal(r = datcorr, nfactors = 4, rotate = "none")
    ## 
    ## Test of the hypothesis that 4 factors are sufficient.
    ## The degrees of freedom for the model is 41  and the objective function was  1.34 
    ## 
    ## The root mean square of the residuals (RMSA) is  0.09

Rotate the pc because from the previous PC, product reviews is not about
fincance like others features in pc1

``` r
datFaVarMax = principal(datcorr,nfactors=4,rotate="varimax")
datFaVarMax
```

    ## Principal Components Analysis
    ## Call: principal(r = datcorr, nfactors = 4, rotate = "varimax")
    ## Standardized loadings (pattern matrix) based upon correlation matrix
    ##                       RC1   RC2   RC3   RC4   h2   u2 com
    ## Price                0.71  0.13 -0.05 -0.13 0.54 0.46 1.2
    ## Safety              -0.37  0.50 -0.27  0.15 0.49 0.51 2.7
    ## Exterior_Looks       0.03  0.05  0.27 -0.78 0.69 0.31 1.2
    ## Space_comfort       -0.03  0.76  0.23 -0.24 0.68 0.32 1.4
    ## Technology           0.04  0.49  0.11  0.01 0.26 0.74 1.1
    ## After_Sales_Service  0.14  0.66  0.12  0.20 0.51 0.49 1.4
    ## Resale_Value         0.78 -0.14 -0.14  0.08 0.65 0.35 1.2
    ## Fuel_Type            0.07  0.70 -0.05 -0.11 0.51 0.49 1.1
    ## Fuel_Efficiency      0.51  0.24  0.36  0.37 0.59 0.41 3.2
    ## Color                0.19 -0.05  0.28  0.76 0.69 0.31 1.4
    ## Maintenance          0.68  0.08  0.13  0.27 0.56 0.44 1.4
    ## Test_drive           0.05  0.15  0.63 -0.01 0.42 0.58 1.1
    ## Product_reviews      0.38  0.14  0.55  0.02 0.47 0.53 2.0
    ## Testimonials        -0.30 -0.03  0.76  0.01 0.67 0.33 1.3
    ## 
    ##                        RC1  RC2  RC3  RC4
    ## SS loadings           2.27 2.13 1.76 1.56
    ## Proportion Var        0.16 0.15 0.13 0.11
    ## Cumulative Var        0.16 0.31 0.44 0.55
    ## Proportion Explained  0.29 0.28 0.23 0.20
    ## Cumulative Proportion 0.29 0.57 0.80 1.00
    ## 
    ## Mean item complexity =  1.5
    ## Test of the hypothesis that 4 components are sufficient.
    ## 
    ## The root mean square of the residuals (RMSR) is  0.09 
    ## 
    ## Fit based upon off diagonal values = 0.78

now it make sense

### Other Method for Factor Analysis

There is other method that we can use to do factor analysis

``` r
fa(datcorr,nfactors=4,rotate="varimax",fm="pa")
```

    ## Factor Analysis using method =  pa
    ## Call: fa(r = datcorr, nfactors = 4, rotate = "varimax", fm = "pa")
    ## Standardized loadings (pattern matrix) based upon correlation matrix
    ##                       PA1   PA2   PA3   PA4   h2   u2 com
    ## Price                0.53  0.11  0.00 -0.05 0.30 0.70 1.1
    ## Safety              -0.27  0.36 -0.18  0.06 0.23 0.77 2.5
    ## Exterior_Looks       0.00  0.04  0.19 -0.55 0.34 0.66 1.3
    ## Space_comfort       -0.03  0.75  0.22 -0.22 0.67 0.33 1.4
    ## Technology           0.04  0.35  0.10  0.01 0.13 0.87 1.2
    ## After_Sales_Service  0.16  0.53  0.10  0.12 0.33 0.67 1.4
    ## Resale_Value         0.72 -0.14 -0.14  0.06 0.57 0.43 1.2
    ## Fuel_Type            0.04  0.56  0.00 -0.07 0.32 0.68 1.0
    ## Fuel_Efficiency      0.49  0.23  0.30  0.29 0.47 0.53 2.9
    ## Color                0.20 -0.03  0.27  0.70 0.60 0.40 1.5
    ## Maintenance          0.60  0.08  0.11  0.23 0.44 0.56 1.4
    ## Test_drive           0.10  0.15  0.41 -0.02 0.20 0.80 1.4
    ## Product_reviews      0.34  0.14  0.43  0.03 0.32 0.68 2.2
    ## Testimonials        -0.23 -0.01  0.67  0.00 0.51 0.49 1.2
    ## 
    ##                        PA1  PA2  PA3  PA4
    ## SS loadings           1.73 1.54 1.14 1.01
    ## Proportion Var        0.12 0.11 0.08 0.07
    ## Cumulative Var        0.12 0.23 0.32 0.39
    ## Proportion Explained  0.32 0.28 0.21 0.19
    ## Cumulative Proportion 0.32 0.60 0.81 1.00
    ## 
    ## Mean item complexity =  1.5
    ## Test of the hypothesis that 4 factors are sufficient.
    ## 
    ## df null model =  91  with the objective function =  2.97
    ## df of  the model are 41  and the objective function was  0.57 
    ## 
    ## The root mean square of the residuals (RMSR) is  0.05 
    ## The df corrected root mean square of the residuals is  0.07 
    ## 
    ## Fit based upon off diagonal values = 0.94
    ## Measures of factor score adequacy             
    ##                                                    PA1  PA2  PA3  PA4
    ## Correlation of (regression) scores with factors   0.86 0.86 0.80 0.80
    ## Multiple R square of scores with factors          0.74 0.74 0.65 0.64
    ## Minimum correlation of possible factor scores     0.49 0.47 0.29 0.29

it shows that the results is the same when we use the fa fuction with fm
= pa and rotate varimax

**Try set other parameter**

``` r
fa(datcorr,nfactors=4,rotate="varimax",fm="ml")
```

    ## Factor Analysis using method =  ml
    ## Call: fa(r = datcorr, nfactors = 4, rotate = "varimax", fm = "ml")
    ## Standardized loadings (pattern matrix) based upon correlation matrix
    ##                       ML3   ML2   ML1   ML4   h2   u2 com
    ## Price                0.52  0.12 -0.02  0.01 0.29 0.71 1.1
    ## Safety              -0.24  0.35  0.03 -0.17 0.21 0.79 2.3
    ## Exterior_Looks      -0.04  0.05 -0.42  0.18 0.21 0.79 1.4
    ## Space_comfort       -0.02  0.79 -0.20  0.23 0.71 0.29 1.3
    ## Technology           0.04  0.35  0.04  0.09 0.13 0.87 1.2
    ## After_Sales_Service  0.22  0.44  0.04  0.10 0.25 0.75 1.6
    ## Resale_Value         0.75 -0.19  0.02 -0.13 0.61 0.39 1.2
    ## Fuel_Type            0.06  0.57 -0.05  0.01 0.34 0.66 1.0
    ## Fuel_Efficiency      0.51  0.17  0.21  0.29 0.42 0.58 2.3
    ## Color                0.18 -0.01  0.89  0.26 0.90 0.10 1.3
    ## Maintenance          0.60  0.10  0.26  0.09 0.45 0.55 1.5
    ## Test_drive           0.12  0.12 -0.05  0.42 0.21 0.79 1.4
    ## Product_reviews      0.32  0.16  0.03  0.45 0.33 0.67 2.1
    ## Testimonials        -0.23  0.00  0.02  0.66 0.49 0.51 1.2
    ## 
    ##                        ML3  ML2  ML1  ML4
    ## SS loadings           1.76 1.52 1.14 1.13
    ## Proportion Var        0.13 0.11 0.08 0.08
    ## Cumulative Var        0.13 0.23 0.32 0.40
    ## Proportion Explained  0.32 0.27 0.21 0.20
    ## Cumulative Proportion 0.32 0.59 0.80 1.00
    ## 
    ## Mean item complexity =  1.5
    ## Test of the hypothesis that 4 factors are sufficient.
    ## 
    ## df null model =  91  with the objective function =  2.97
    ## df of  the model are 41  and the objective function was  0.55 
    ## 
    ## The root mean square of the residuals (RMSR) is  0.05 
    ## The df corrected root mean square of the residuals is  0.08 
    ## 
    ## Fit based upon off diagonal values = 0.93
    ## Measures of factor score adequacy             
    ##                                                    ML3  ML2  ML1  ML4
    ## Correlation of (regression) scores with factors   0.87 0.87 0.93 0.80
    ## Multiple R square of scores with factors          0.76 0.75 0.86 0.64
    ## Minimum correlation of possible factor scores     0.52 0.50 0.72 0.28

``` r
FA1=fa(datcorr,nfactors=3,rotate="varimax",fm="pa")
FA1
```

    ## Factor Analysis using method =  pa
    ## Call: fa(r = datcorr, nfactors = 3, rotate = "varimax", fm = "pa")
    ## Standardized loadings (pattern matrix) based upon correlation matrix
    ##                       PA1   PA2   PA3   h2   u2 com
    ## Price                0.48  0.14 -0.02 0.25 0.75 1.2
    ## Safety              -0.20  0.29 -0.12 0.14 0.86 2.2
    ## Exterior_Looks      -0.18  0.17  0.03 0.06 0.94 2.0
    ## Space_comfort       -0.09  0.82  0.17 0.70 0.30 1.1
    ## Technology           0.06  0.34  0.10 0.13 0.87 1.2
    ## After_Sales_Service  0.21  0.47  0.15 0.29 0.71 1.6
    ## Resale_Value         0.67 -0.12 -0.12 0.48 0.52 1.1
    ## Fuel_Type            0.04  0.56 -0.01 0.32 0.68 1.0
    ## Fuel_Efficiency      0.56  0.18  0.38 0.49 0.51 2.0
    ## Color                0.37 -0.14  0.34 0.27 0.73 2.3
    ## Maintenance          0.65  0.05  0.15 0.45 0.55 1.1
    ## Test_drive           0.07  0.16  0.40 0.19 0.81 1.4
    ## Product_reviews      0.30  0.16  0.41 0.29 0.71 2.2
    ## Testimonials        -0.27  0.00  0.68 0.53 0.47 1.3
    ## 
    ##                        PA1  PA2  PA3
    ## SS loadings           1.86 1.57 1.16
    ## Proportion Var        0.13 0.11 0.08
    ## Cumulative Var        0.13 0.25 0.33
    ## Proportion Explained  0.40 0.34 0.25
    ## Cumulative Proportion 0.40 0.75 1.00
    ## 
    ## Mean item complexity =  1.6
    ## Test of the hypothesis that 3 factors are sufficient.
    ## 
    ## df null model =  91  with the objective function =  2.97
    ## df of  the model are 52  and the objective function was  0.84 
    ## 
    ## The root mean square of the residuals (RMSR) is  0.07 
    ## The df corrected root mean square of the residuals is  0.09 
    ## 
    ## Fit based upon off diagonal values = 0.88
    ## Measures of factor score adequacy             
    ##                                                    PA1  PA2  PA3
    ## Correlation of (regression) scores with factors   0.87 0.88 0.81
    ## Multiple R square of scores with factors          0.76 0.77 0.66
    ## Minimum correlation of possible factor scores     0.52 0.54 0.32

``` r
summary(FA1)
```

    ## 
    ## Factor analysis with Call: fa(r = datcorr, nfactors = 3, rotate = "varimax", fm = "pa")
    ## 
    ## Test of the hypothesis that 3 factors are sufficient.
    ## The degrees of freedom for the model is 52  and the objective function was  0.84 
    ## 
    ## The root mean square of the residuals (RMSA) is  0.07 
    ## The df corrected root mean square of the residuals is  0.09
