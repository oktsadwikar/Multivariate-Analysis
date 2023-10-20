Chapter 4 MANOVA
================
Oktsa Dwika Rahmashari
2023-10-20

# **MANOVA**

H0 : Miu1=Miu2=…=MiuN

Reject H0 if p-value\<alfa

## Assumption Check

There are 3 assumption for MANOVA test

1.  Independent samples

2.  Equality in covariance matrices

3.  Multivariate normal distribution

**Example (using iris Dataset):**

The computation for input part:

Import Iris Dataset

``` r
data(iris)
data = iris
data
```

    ##     Sepal.Length Sepal.Width Petal.Length Petal.Width    Species
    ## 1            5.1         3.5          1.4         0.2     setosa
    ## 2            4.9         3.0          1.4         0.2     setosa
    ## 3            4.7         3.2          1.3         0.2     setosa
    ## 4            4.6         3.1          1.5         0.2     setosa
    ## 5            5.0         3.6          1.4         0.2     setosa
    ## 6            5.4         3.9          1.7         0.4     setosa
    ## 7            4.6         3.4          1.4         0.3     setosa
    ## 8            5.0         3.4          1.5         0.2     setosa
    ## 9            4.4         2.9          1.4         0.2     setosa
    ## 10           4.9         3.1          1.5         0.1     setosa
    ## 11           5.4         3.7          1.5         0.2     setosa
    ## 12           4.8         3.4          1.6         0.2     setosa
    ## 13           4.8         3.0          1.4         0.1     setosa
    ## 14           4.3         3.0          1.1         0.1     setosa
    ## 15           5.8         4.0          1.2         0.2     setosa
    ## 16           5.7         4.4          1.5         0.4     setosa
    ## 17           5.4         3.9          1.3         0.4     setosa
    ## 18           5.1         3.5          1.4         0.3     setosa
    ## 19           5.7         3.8          1.7         0.3     setosa
    ## 20           5.1         3.8          1.5         0.3     setosa
    ## 21           5.4         3.4          1.7         0.2     setosa
    ## 22           5.1         3.7          1.5         0.4     setosa
    ## 23           4.6         3.6          1.0         0.2     setosa
    ## 24           5.1         3.3          1.7         0.5     setosa
    ## 25           4.8         3.4          1.9         0.2     setosa
    ## 26           5.0         3.0          1.6         0.2     setosa
    ## 27           5.0         3.4          1.6         0.4     setosa
    ## 28           5.2         3.5          1.5         0.2     setosa
    ## 29           5.2         3.4          1.4         0.2     setosa
    ## 30           4.7         3.2          1.6         0.2     setosa
    ## 31           4.8         3.1          1.6         0.2     setosa
    ## 32           5.4         3.4          1.5         0.4     setosa
    ## 33           5.2         4.1          1.5         0.1     setosa
    ## 34           5.5         4.2          1.4         0.2     setosa
    ## 35           4.9         3.1          1.5         0.2     setosa
    ## 36           5.0         3.2          1.2         0.2     setosa
    ## 37           5.5         3.5          1.3         0.2     setosa
    ## 38           4.9         3.6          1.4         0.1     setosa
    ## 39           4.4         3.0          1.3         0.2     setosa
    ## 40           5.1         3.4          1.5         0.2     setosa
    ## 41           5.0         3.5          1.3         0.3     setosa
    ## 42           4.5         2.3          1.3         0.3     setosa
    ## 43           4.4         3.2          1.3         0.2     setosa
    ## 44           5.0         3.5          1.6         0.6     setosa
    ## 45           5.1         3.8          1.9         0.4     setosa
    ## 46           4.8         3.0          1.4         0.3     setosa
    ## 47           5.1         3.8          1.6         0.2     setosa
    ## 48           4.6         3.2          1.4         0.2     setosa
    ## 49           5.3         3.7          1.5         0.2     setosa
    ## 50           5.0         3.3          1.4         0.2     setosa
    ## 51           7.0         3.2          4.7         1.4 versicolor
    ## 52           6.4         3.2          4.5         1.5 versicolor
    ## 53           6.9         3.1          4.9         1.5 versicolor
    ## 54           5.5         2.3          4.0         1.3 versicolor
    ## 55           6.5         2.8          4.6         1.5 versicolor
    ## 56           5.7         2.8          4.5         1.3 versicolor
    ## 57           6.3         3.3          4.7         1.6 versicolor
    ## 58           4.9         2.4          3.3         1.0 versicolor
    ## 59           6.6         2.9          4.6         1.3 versicolor
    ## 60           5.2         2.7          3.9         1.4 versicolor
    ## 61           5.0         2.0          3.5         1.0 versicolor
    ## 62           5.9         3.0          4.2         1.5 versicolor
    ## 63           6.0         2.2          4.0         1.0 versicolor
    ## 64           6.1         2.9          4.7         1.4 versicolor
    ## 65           5.6         2.9          3.6         1.3 versicolor
    ## 66           6.7         3.1          4.4         1.4 versicolor
    ## 67           5.6         3.0          4.5         1.5 versicolor
    ## 68           5.8         2.7          4.1         1.0 versicolor
    ## 69           6.2         2.2          4.5         1.5 versicolor
    ## 70           5.6         2.5          3.9         1.1 versicolor
    ## 71           5.9         3.2          4.8         1.8 versicolor
    ## 72           6.1         2.8          4.0         1.3 versicolor
    ## 73           6.3         2.5          4.9         1.5 versicolor
    ## 74           6.1         2.8          4.7         1.2 versicolor
    ## 75           6.4         2.9          4.3         1.3 versicolor
    ## 76           6.6         3.0          4.4         1.4 versicolor
    ## 77           6.8         2.8          4.8         1.4 versicolor
    ## 78           6.7         3.0          5.0         1.7 versicolor
    ## 79           6.0         2.9          4.5         1.5 versicolor
    ## 80           5.7         2.6          3.5         1.0 versicolor
    ## 81           5.5         2.4          3.8         1.1 versicolor
    ## 82           5.5         2.4          3.7         1.0 versicolor
    ## 83           5.8         2.7          3.9         1.2 versicolor
    ## 84           6.0         2.7          5.1         1.6 versicolor
    ## 85           5.4         3.0          4.5         1.5 versicolor
    ## 86           6.0         3.4          4.5         1.6 versicolor
    ## 87           6.7         3.1          4.7         1.5 versicolor
    ## 88           6.3         2.3          4.4         1.3 versicolor
    ## 89           5.6         3.0          4.1         1.3 versicolor
    ## 90           5.5         2.5          4.0         1.3 versicolor
    ## 91           5.5         2.6          4.4         1.2 versicolor
    ## 92           6.1         3.0          4.6         1.4 versicolor
    ## 93           5.8         2.6          4.0         1.2 versicolor
    ## 94           5.0         2.3          3.3         1.0 versicolor
    ## 95           5.6         2.7          4.2         1.3 versicolor
    ## 96           5.7         3.0          4.2         1.2 versicolor
    ## 97           5.7         2.9          4.2         1.3 versicolor
    ## 98           6.2         2.9          4.3         1.3 versicolor
    ## 99           5.1         2.5          3.0         1.1 versicolor
    ## 100          5.7         2.8          4.1         1.3 versicolor
    ## 101          6.3         3.3          6.0         2.5  virginica
    ## 102          5.8         2.7          5.1         1.9  virginica
    ## 103          7.1         3.0          5.9         2.1  virginica
    ## 104          6.3         2.9          5.6         1.8  virginica
    ## 105          6.5         3.0          5.8         2.2  virginica
    ## 106          7.6         3.0          6.6         2.1  virginica
    ## 107          4.9         2.5          4.5         1.7  virginica
    ## 108          7.3         2.9          6.3         1.8  virginica
    ## 109          6.7         2.5          5.8         1.8  virginica
    ## 110          7.2         3.6          6.1         2.5  virginica
    ## 111          6.5         3.2          5.1         2.0  virginica
    ## 112          6.4         2.7          5.3         1.9  virginica
    ## 113          6.8         3.0          5.5         2.1  virginica
    ## 114          5.7         2.5          5.0         2.0  virginica
    ## 115          5.8         2.8          5.1         2.4  virginica
    ## 116          6.4         3.2          5.3         2.3  virginica
    ## 117          6.5         3.0          5.5         1.8  virginica
    ## 118          7.7         3.8          6.7         2.2  virginica
    ## 119          7.7         2.6          6.9         2.3  virginica
    ## 120          6.0         2.2          5.0         1.5  virginica
    ## 121          6.9         3.2          5.7         2.3  virginica
    ## 122          5.6         2.8          4.9         2.0  virginica
    ## 123          7.7         2.8          6.7         2.0  virginica
    ## 124          6.3         2.7          4.9         1.8  virginica
    ## 125          6.7         3.3          5.7         2.1  virginica
    ## 126          7.2         3.2          6.0         1.8  virginica
    ## 127          6.2         2.8          4.8         1.8  virginica
    ## 128          6.1         3.0          4.9         1.8  virginica
    ## 129          6.4         2.8          5.6         2.1  virginica
    ## 130          7.2         3.0          5.8         1.6  virginica
    ## 131          7.4         2.8          6.1         1.9  virginica
    ## 132          7.9         3.8          6.4         2.0  virginica
    ## 133          6.4         2.8          5.6         2.2  virginica
    ## 134          6.3         2.8          5.1         1.5  virginica
    ## 135          6.1         2.6          5.6         1.4  virginica
    ## 136          7.7         3.0          6.1         2.3  virginica
    ## 137          6.3         3.4          5.6         2.4  virginica
    ## 138          6.4         3.1          5.5         1.8  virginica
    ## 139          6.0         3.0          4.8         1.8  virginica
    ## 140          6.9         3.1          5.4         2.1  virginica
    ## 141          6.7         3.1          5.6         2.4  virginica
    ## 142          6.9         3.1          5.1         2.3  virginica
    ## 143          5.8         2.7          5.1         1.9  virginica
    ## 144          6.8         3.2          5.9         2.3  virginica
    ## 145          6.7         3.3          5.7         2.5  virginica
    ## 146          6.7         3.0          5.2         2.3  virginica
    ## 147          6.3         2.5          5.0         1.9  virginica
    ## 148          6.5         3.0          5.2         2.0  virginica
    ## 149          6.2         3.4          5.4         2.3  virginica
    ## 150          5.9         3.0          5.1         1.8  virginica

Setting the group labels as factor type in R

``` r
data$Species = factor(data$Species)
data
```

    ##     Sepal.Length Sepal.Width Petal.Length Petal.Width    Species
    ## 1            5.1         3.5          1.4         0.2     setosa
    ## 2            4.9         3.0          1.4         0.2     setosa
    ## 3            4.7         3.2          1.3         0.2     setosa
    ## 4            4.6         3.1          1.5         0.2     setosa
    ## 5            5.0         3.6          1.4         0.2     setosa
    ## 6            5.4         3.9          1.7         0.4     setosa
    ## 7            4.6         3.4          1.4         0.3     setosa
    ## 8            5.0         3.4          1.5         0.2     setosa
    ## 9            4.4         2.9          1.4         0.2     setosa
    ## 10           4.9         3.1          1.5         0.1     setosa
    ## 11           5.4         3.7          1.5         0.2     setosa
    ## 12           4.8         3.4          1.6         0.2     setosa
    ## 13           4.8         3.0          1.4         0.1     setosa
    ## 14           4.3         3.0          1.1         0.1     setosa
    ## 15           5.8         4.0          1.2         0.2     setosa
    ## 16           5.7         4.4          1.5         0.4     setosa
    ## 17           5.4         3.9          1.3         0.4     setosa
    ## 18           5.1         3.5          1.4         0.3     setosa
    ## 19           5.7         3.8          1.7         0.3     setosa
    ## 20           5.1         3.8          1.5         0.3     setosa
    ## 21           5.4         3.4          1.7         0.2     setosa
    ## 22           5.1         3.7          1.5         0.4     setosa
    ## 23           4.6         3.6          1.0         0.2     setosa
    ## 24           5.1         3.3          1.7         0.5     setosa
    ## 25           4.8         3.4          1.9         0.2     setosa
    ## 26           5.0         3.0          1.6         0.2     setosa
    ## 27           5.0         3.4          1.6         0.4     setosa
    ## 28           5.2         3.5          1.5         0.2     setosa
    ## 29           5.2         3.4          1.4         0.2     setosa
    ## 30           4.7         3.2          1.6         0.2     setosa
    ## 31           4.8         3.1          1.6         0.2     setosa
    ## 32           5.4         3.4          1.5         0.4     setosa
    ## 33           5.2         4.1          1.5         0.1     setosa
    ## 34           5.5         4.2          1.4         0.2     setosa
    ## 35           4.9         3.1          1.5         0.2     setosa
    ## 36           5.0         3.2          1.2         0.2     setosa
    ## 37           5.5         3.5          1.3         0.2     setosa
    ## 38           4.9         3.6          1.4         0.1     setosa
    ## 39           4.4         3.0          1.3         0.2     setosa
    ## 40           5.1         3.4          1.5         0.2     setosa
    ## 41           5.0         3.5          1.3         0.3     setosa
    ## 42           4.5         2.3          1.3         0.3     setosa
    ## 43           4.4         3.2          1.3         0.2     setosa
    ## 44           5.0         3.5          1.6         0.6     setosa
    ## 45           5.1         3.8          1.9         0.4     setosa
    ## 46           4.8         3.0          1.4         0.3     setosa
    ## 47           5.1         3.8          1.6         0.2     setosa
    ## 48           4.6         3.2          1.4         0.2     setosa
    ## 49           5.3         3.7          1.5         0.2     setosa
    ## 50           5.0         3.3          1.4         0.2     setosa
    ## 51           7.0         3.2          4.7         1.4 versicolor
    ## 52           6.4         3.2          4.5         1.5 versicolor
    ## 53           6.9         3.1          4.9         1.5 versicolor
    ## 54           5.5         2.3          4.0         1.3 versicolor
    ## 55           6.5         2.8          4.6         1.5 versicolor
    ## 56           5.7         2.8          4.5         1.3 versicolor
    ## 57           6.3         3.3          4.7         1.6 versicolor
    ## 58           4.9         2.4          3.3         1.0 versicolor
    ## 59           6.6         2.9          4.6         1.3 versicolor
    ## 60           5.2         2.7          3.9         1.4 versicolor
    ## 61           5.0         2.0          3.5         1.0 versicolor
    ## 62           5.9         3.0          4.2         1.5 versicolor
    ## 63           6.0         2.2          4.0         1.0 versicolor
    ## 64           6.1         2.9          4.7         1.4 versicolor
    ## 65           5.6         2.9          3.6         1.3 versicolor
    ## 66           6.7         3.1          4.4         1.4 versicolor
    ## 67           5.6         3.0          4.5         1.5 versicolor
    ## 68           5.8         2.7          4.1         1.0 versicolor
    ## 69           6.2         2.2          4.5         1.5 versicolor
    ## 70           5.6         2.5          3.9         1.1 versicolor
    ## 71           5.9         3.2          4.8         1.8 versicolor
    ## 72           6.1         2.8          4.0         1.3 versicolor
    ## 73           6.3         2.5          4.9         1.5 versicolor
    ## 74           6.1         2.8          4.7         1.2 versicolor
    ## 75           6.4         2.9          4.3         1.3 versicolor
    ## 76           6.6         3.0          4.4         1.4 versicolor
    ## 77           6.8         2.8          4.8         1.4 versicolor
    ## 78           6.7         3.0          5.0         1.7 versicolor
    ## 79           6.0         2.9          4.5         1.5 versicolor
    ## 80           5.7         2.6          3.5         1.0 versicolor
    ## 81           5.5         2.4          3.8         1.1 versicolor
    ## 82           5.5         2.4          3.7         1.0 versicolor
    ## 83           5.8         2.7          3.9         1.2 versicolor
    ## 84           6.0         2.7          5.1         1.6 versicolor
    ## 85           5.4         3.0          4.5         1.5 versicolor
    ## 86           6.0         3.4          4.5         1.6 versicolor
    ## 87           6.7         3.1          4.7         1.5 versicolor
    ## 88           6.3         2.3          4.4         1.3 versicolor
    ## 89           5.6         3.0          4.1         1.3 versicolor
    ## 90           5.5         2.5          4.0         1.3 versicolor
    ## 91           5.5         2.6          4.4         1.2 versicolor
    ## 92           6.1         3.0          4.6         1.4 versicolor
    ## 93           5.8         2.6          4.0         1.2 versicolor
    ## 94           5.0         2.3          3.3         1.0 versicolor
    ## 95           5.6         2.7          4.2         1.3 versicolor
    ## 96           5.7         3.0          4.2         1.2 versicolor
    ## 97           5.7         2.9          4.2         1.3 versicolor
    ## 98           6.2         2.9          4.3         1.3 versicolor
    ## 99           5.1         2.5          3.0         1.1 versicolor
    ## 100          5.7         2.8          4.1         1.3 versicolor
    ## 101          6.3         3.3          6.0         2.5  virginica
    ## 102          5.8         2.7          5.1         1.9  virginica
    ## 103          7.1         3.0          5.9         2.1  virginica
    ## 104          6.3         2.9          5.6         1.8  virginica
    ## 105          6.5         3.0          5.8         2.2  virginica
    ## 106          7.6         3.0          6.6         2.1  virginica
    ## 107          4.9         2.5          4.5         1.7  virginica
    ## 108          7.3         2.9          6.3         1.8  virginica
    ## 109          6.7         2.5          5.8         1.8  virginica
    ## 110          7.2         3.6          6.1         2.5  virginica
    ## 111          6.5         3.2          5.1         2.0  virginica
    ## 112          6.4         2.7          5.3         1.9  virginica
    ## 113          6.8         3.0          5.5         2.1  virginica
    ## 114          5.7         2.5          5.0         2.0  virginica
    ## 115          5.8         2.8          5.1         2.4  virginica
    ## 116          6.4         3.2          5.3         2.3  virginica
    ## 117          6.5         3.0          5.5         1.8  virginica
    ## 118          7.7         3.8          6.7         2.2  virginica
    ## 119          7.7         2.6          6.9         2.3  virginica
    ## 120          6.0         2.2          5.0         1.5  virginica
    ## 121          6.9         3.2          5.7         2.3  virginica
    ## 122          5.6         2.8          4.9         2.0  virginica
    ## 123          7.7         2.8          6.7         2.0  virginica
    ## 124          6.3         2.7          4.9         1.8  virginica
    ## 125          6.7         3.3          5.7         2.1  virginica
    ## 126          7.2         3.2          6.0         1.8  virginica
    ## 127          6.2         2.8          4.8         1.8  virginica
    ## 128          6.1         3.0          4.9         1.8  virginica
    ## 129          6.4         2.8          5.6         2.1  virginica
    ## 130          7.2         3.0          5.8         1.6  virginica
    ## 131          7.4         2.8          6.1         1.9  virginica
    ## 132          7.9         3.8          6.4         2.0  virginica
    ## 133          6.4         2.8          5.6         2.2  virginica
    ## 134          6.3         2.8          5.1         1.5  virginica
    ## 135          6.1         2.6          5.6         1.4  virginica
    ## 136          7.7         3.0          6.1         2.3  virginica
    ## 137          6.3         3.4          5.6         2.4  virginica
    ## 138          6.4         3.1          5.5         1.8  virginica
    ## 139          6.0         3.0          4.8         1.8  virginica
    ## 140          6.9         3.1          5.4         2.1  virginica
    ## 141          6.7         3.1          5.6         2.4  virginica
    ## 142          6.9         3.1          5.1         2.3  virginica
    ## 143          5.8         2.7          5.1         1.9  virginica
    ## 144          6.8         3.2          5.9         2.3  virginica
    ## 145          6.7         3.3          5.7         2.5  virginica
    ## 146          6.7         3.0          5.2         2.3  virginica
    ## 147          6.3         2.5          5.0         1.9  virginica
    ## 148          6.5         3.0          5.2         2.0  virginica
    ## 149          6.2         3.4          5.4         2.3  virginica
    ## 150          5.9         3.0          5.1         1.8  virginica

**Assumption Check**

- Cond. 1 =\> Independent samples: (Hold)

- Cond. 2 =\> Equality in covariance matrices:we assume that all groups
  have the same covariance matrix Sigma

- Cond. 3 =\> Multivariate normal: Assumed that each population is
  multivariate normal (Since the sample size n are large, based on the
  central limit theorem, we assumed that each population is multivariate
  normal.

## 1. The Computation for MANOVA test using function

``` r
res.man = manova(cbind(Sepal.Length, Sepal.Width,Petal.Length,Petal.Width) ~ Species, data = data)
res.man
```

    ## Call:
    ##    manova(cbind(Sepal.Length, Sepal.Width, Petal.Length, Petal.Width) ~ 
    ##     Species, data = data)
    ## 
    ## Terms:
    ##                  Species Residuals
    ## Sepal.Length     63.2121   38.9562
    ## Sepal.Width      11.3449   16.9620
    ## Petal.Length    437.1028   27.2226
    ## Petal.Width      80.4133    6.1566
    ## Deg. of Freedom        2       147
    ## 
    ## Residual standard errors: 0.5147894 0.3396877 0.4303345 0.20465
    ## Estimated effects may be unbalanced

``` r
summary(res.man)
```

    ##            Df Pillai approx F num Df den Df    Pr(>F)    
    ## Species     2 1.1919   53.466      8    290 < 2.2e-16 ***
    ## Residuals 147                                            
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

**Explaination:**

- cbind() = the variables

- species = group

**Conclusion:**

Since p-value\<alfa, then reject H0. So, we can conclude that at least 2
mean vector are different.

## 2. The Computation for MANOVA test manually

``` r
# Split data based on species
data_new = split(data,data$Species)
data_new
```

    ## $setosa
    ##    Sepal.Length Sepal.Width Petal.Length Petal.Width Species
    ## 1           5.1         3.5          1.4         0.2  setosa
    ## 2           4.9         3.0          1.4         0.2  setosa
    ## 3           4.7         3.2          1.3         0.2  setosa
    ## 4           4.6         3.1          1.5         0.2  setosa
    ## 5           5.0         3.6          1.4         0.2  setosa
    ## 6           5.4         3.9          1.7         0.4  setosa
    ## 7           4.6         3.4          1.4         0.3  setosa
    ## 8           5.0         3.4          1.5         0.2  setosa
    ## 9           4.4         2.9          1.4         0.2  setosa
    ## 10          4.9         3.1          1.5         0.1  setosa
    ## 11          5.4         3.7          1.5         0.2  setosa
    ## 12          4.8         3.4          1.6         0.2  setosa
    ## 13          4.8         3.0          1.4         0.1  setosa
    ## 14          4.3         3.0          1.1         0.1  setosa
    ## 15          5.8         4.0          1.2         0.2  setosa
    ## 16          5.7         4.4          1.5         0.4  setosa
    ## 17          5.4         3.9          1.3         0.4  setosa
    ## 18          5.1         3.5          1.4         0.3  setosa
    ## 19          5.7         3.8          1.7         0.3  setosa
    ## 20          5.1         3.8          1.5         0.3  setosa
    ## 21          5.4         3.4          1.7         0.2  setosa
    ## 22          5.1         3.7          1.5         0.4  setosa
    ## 23          4.6         3.6          1.0         0.2  setosa
    ## 24          5.1         3.3          1.7         0.5  setosa
    ## 25          4.8         3.4          1.9         0.2  setosa
    ## 26          5.0         3.0          1.6         0.2  setosa
    ## 27          5.0         3.4          1.6         0.4  setosa
    ## 28          5.2         3.5          1.5         0.2  setosa
    ## 29          5.2         3.4          1.4         0.2  setosa
    ## 30          4.7         3.2          1.6         0.2  setosa
    ## 31          4.8         3.1          1.6         0.2  setosa
    ## 32          5.4         3.4          1.5         0.4  setosa
    ## 33          5.2         4.1          1.5         0.1  setosa
    ## 34          5.5         4.2          1.4         0.2  setosa
    ## 35          4.9         3.1          1.5         0.2  setosa
    ## 36          5.0         3.2          1.2         0.2  setosa
    ## 37          5.5         3.5          1.3         0.2  setosa
    ## 38          4.9         3.6          1.4         0.1  setosa
    ## 39          4.4         3.0          1.3         0.2  setosa
    ## 40          5.1         3.4          1.5         0.2  setosa
    ## 41          5.0         3.5          1.3         0.3  setosa
    ## 42          4.5         2.3          1.3         0.3  setosa
    ## 43          4.4         3.2          1.3         0.2  setosa
    ## 44          5.0         3.5          1.6         0.6  setosa
    ## 45          5.1         3.8          1.9         0.4  setosa
    ## 46          4.8         3.0          1.4         0.3  setosa
    ## 47          5.1         3.8          1.6         0.2  setosa
    ## 48          4.6         3.2          1.4         0.2  setosa
    ## 49          5.3         3.7          1.5         0.2  setosa
    ## 50          5.0         3.3          1.4         0.2  setosa
    ## 
    ## $versicolor
    ##     Sepal.Length Sepal.Width Petal.Length Petal.Width    Species
    ## 51           7.0         3.2          4.7         1.4 versicolor
    ## 52           6.4         3.2          4.5         1.5 versicolor
    ## 53           6.9         3.1          4.9         1.5 versicolor
    ## 54           5.5         2.3          4.0         1.3 versicolor
    ## 55           6.5         2.8          4.6         1.5 versicolor
    ## 56           5.7         2.8          4.5         1.3 versicolor
    ## 57           6.3         3.3          4.7         1.6 versicolor
    ## 58           4.9         2.4          3.3         1.0 versicolor
    ## 59           6.6         2.9          4.6         1.3 versicolor
    ## 60           5.2         2.7          3.9         1.4 versicolor
    ## 61           5.0         2.0          3.5         1.0 versicolor
    ## 62           5.9         3.0          4.2         1.5 versicolor
    ## 63           6.0         2.2          4.0         1.0 versicolor
    ## 64           6.1         2.9          4.7         1.4 versicolor
    ## 65           5.6         2.9          3.6         1.3 versicolor
    ## 66           6.7         3.1          4.4         1.4 versicolor
    ## 67           5.6         3.0          4.5         1.5 versicolor
    ## 68           5.8         2.7          4.1         1.0 versicolor
    ## 69           6.2         2.2          4.5         1.5 versicolor
    ## 70           5.6         2.5          3.9         1.1 versicolor
    ## 71           5.9         3.2          4.8         1.8 versicolor
    ## 72           6.1         2.8          4.0         1.3 versicolor
    ## 73           6.3         2.5          4.9         1.5 versicolor
    ## 74           6.1         2.8          4.7         1.2 versicolor
    ## 75           6.4         2.9          4.3         1.3 versicolor
    ## 76           6.6         3.0          4.4         1.4 versicolor
    ## 77           6.8         2.8          4.8         1.4 versicolor
    ## 78           6.7         3.0          5.0         1.7 versicolor
    ## 79           6.0         2.9          4.5         1.5 versicolor
    ## 80           5.7         2.6          3.5         1.0 versicolor
    ## 81           5.5         2.4          3.8         1.1 versicolor
    ## 82           5.5         2.4          3.7         1.0 versicolor
    ## 83           5.8         2.7          3.9         1.2 versicolor
    ## 84           6.0         2.7          5.1         1.6 versicolor
    ## 85           5.4         3.0          4.5         1.5 versicolor
    ## 86           6.0         3.4          4.5         1.6 versicolor
    ## 87           6.7         3.1          4.7         1.5 versicolor
    ## 88           6.3         2.3          4.4         1.3 versicolor
    ## 89           5.6         3.0          4.1         1.3 versicolor
    ## 90           5.5         2.5          4.0         1.3 versicolor
    ## 91           5.5         2.6          4.4         1.2 versicolor
    ## 92           6.1         3.0          4.6         1.4 versicolor
    ## 93           5.8         2.6          4.0         1.2 versicolor
    ## 94           5.0         2.3          3.3         1.0 versicolor
    ## 95           5.6         2.7          4.2         1.3 versicolor
    ## 96           5.7         3.0          4.2         1.2 versicolor
    ## 97           5.7         2.9          4.2         1.3 versicolor
    ## 98           6.2         2.9          4.3         1.3 versicolor
    ## 99           5.1         2.5          3.0         1.1 versicolor
    ## 100          5.7         2.8          4.1         1.3 versicolor
    ## 
    ## $virginica
    ##     Sepal.Length Sepal.Width Petal.Length Petal.Width   Species
    ## 101          6.3         3.3          6.0         2.5 virginica
    ## 102          5.8         2.7          5.1         1.9 virginica
    ## 103          7.1         3.0          5.9         2.1 virginica
    ## 104          6.3         2.9          5.6         1.8 virginica
    ## 105          6.5         3.0          5.8         2.2 virginica
    ## 106          7.6         3.0          6.6         2.1 virginica
    ## 107          4.9         2.5          4.5         1.7 virginica
    ## 108          7.3         2.9          6.3         1.8 virginica
    ## 109          6.7         2.5          5.8         1.8 virginica
    ## 110          7.2         3.6          6.1         2.5 virginica
    ## 111          6.5         3.2          5.1         2.0 virginica
    ## 112          6.4         2.7          5.3         1.9 virginica
    ## 113          6.8         3.0          5.5         2.1 virginica
    ## 114          5.7         2.5          5.0         2.0 virginica
    ## 115          5.8         2.8          5.1         2.4 virginica
    ## 116          6.4         3.2          5.3         2.3 virginica
    ## 117          6.5         3.0          5.5         1.8 virginica
    ## 118          7.7         3.8          6.7         2.2 virginica
    ## 119          7.7         2.6          6.9         2.3 virginica
    ## 120          6.0         2.2          5.0         1.5 virginica
    ## 121          6.9         3.2          5.7         2.3 virginica
    ## 122          5.6         2.8          4.9         2.0 virginica
    ## 123          7.7         2.8          6.7         2.0 virginica
    ## 124          6.3         2.7          4.9         1.8 virginica
    ## 125          6.7         3.3          5.7         2.1 virginica
    ## 126          7.2         3.2          6.0         1.8 virginica
    ## 127          6.2         2.8          4.8         1.8 virginica
    ## 128          6.1         3.0          4.9         1.8 virginica
    ## 129          6.4         2.8          5.6         2.1 virginica
    ## 130          7.2         3.0          5.8         1.6 virginica
    ## 131          7.4         2.8          6.1         1.9 virginica
    ## 132          7.9         3.8          6.4         2.0 virginica
    ## 133          6.4         2.8          5.6         2.2 virginica
    ## 134          6.3         2.8          5.1         1.5 virginica
    ## 135          6.1         2.6          5.6         1.4 virginica
    ## 136          7.7         3.0          6.1         2.3 virginica
    ## 137          6.3         3.4          5.6         2.4 virginica
    ## 138          6.4         3.1          5.5         1.8 virginica
    ## 139          6.0         3.0          4.8         1.8 virginica
    ## 140          6.9         3.1          5.4         2.1 virginica
    ## 141          6.7         3.1          5.6         2.4 virginica
    ## 142          6.9         3.1          5.1         2.3 virginica
    ## 143          5.8         2.7          5.1         1.9 virginica
    ## 144          6.8         3.2          5.9         2.3 virginica
    ## 145          6.7         3.3          5.7         2.5 virginica
    ## 146          6.7         3.0          5.2         2.3 virginica
    ## 147          6.3         2.5          5.0         1.9 virginica
    ## 148          6.5         3.0          5.2         2.0 virginica
    ## 149          6.2         3.4          5.4         2.3 virginica
    ## 150          5.9         3.0          5.1         1.8 virginica

``` r
n = nrow(data)
n
```

    ## [1] 150

``` r
p = 4
p
```

    ## [1] 4

``` r
# Data Setose
setosa = data_new$setosa
setosa
```

    ##    Sepal.Length Sepal.Width Petal.Length Petal.Width Species
    ## 1           5.1         3.5          1.4         0.2  setosa
    ## 2           4.9         3.0          1.4         0.2  setosa
    ## 3           4.7         3.2          1.3         0.2  setosa
    ## 4           4.6         3.1          1.5         0.2  setosa
    ## 5           5.0         3.6          1.4         0.2  setosa
    ## 6           5.4         3.9          1.7         0.4  setosa
    ## 7           4.6         3.4          1.4         0.3  setosa
    ## 8           5.0         3.4          1.5         0.2  setosa
    ## 9           4.4         2.9          1.4         0.2  setosa
    ## 10          4.9         3.1          1.5         0.1  setosa
    ## 11          5.4         3.7          1.5         0.2  setosa
    ## 12          4.8         3.4          1.6         0.2  setosa
    ## 13          4.8         3.0          1.4         0.1  setosa
    ## 14          4.3         3.0          1.1         0.1  setosa
    ## 15          5.8         4.0          1.2         0.2  setosa
    ## 16          5.7         4.4          1.5         0.4  setosa
    ## 17          5.4         3.9          1.3         0.4  setosa
    ## 18          5.1         3.5          1.4         0.3  setosa
    ## 19          5.7         3.8          1.7         0.3  setosa
    ## 20          5.1         3.8          1.5         0.3  setosa
    ## 21          5.4         3.4          1.7         0.2  setosa
    ## 22          5.1         3.7          1.5         0.4  setosa
    ## 23          4.6         3.6          1.0         0.2  setosa
    ## 24          5.1         3.3          1.7         0.5  setosa
    ## 25          4.8         3.4          1.9         0.2  setosa
    ## 26          5.0         3.0          1.6         0.2  setosa
    ## 27          5.0         3.4          1.6         0.4  setosa
    ## 28          5.2         3.5          1.5         0.2  setosa
    ## 29          5.2         3.4          1.4         0.2  setosa
    ## 30          4.7         3.2          1.6         0.2  setosa
    ## 31          4.8         3.1          1.6         0.2  setosa
    ## 32          5.4         3.4          1.5         0.4  setosa
    ## 33          5.2         4.1          1.5         0.1  setosa
    ## 34          5.5         4.2          1.4         0.2  setosa
    ## 35          4.9         3.1          1.5         0.2  setosa
    ## 36          5.0         3.2          1.2         0.2  setosa
    ## 37          5.5         3.5          1.3         0.2  setosa
    ## 38          4.9         3.6          1.4         0.1  setosa
    ## 39          4.4         3.0          1.3         0.2  setosa
    ## 40          5.1         3.4          1.5         0.2  setosa
    ## 41          5.0         3.5          1.3         0.3  setosa
    ## 42          4.5         2.3          1.3         0.3  setosa
    ## 43          4.4         3.2          1.3         0.2  setosa
    ## 44          5.0         3.5          1.6         0.6  setosa
    ## 45          5.1         3.8          1.9         0.4  setosa
    ## 46          4.8         3.0          1.4         0.3  setosa
    ## 47          5.1         3.8          1.6         0.2  setosa
    ## 48          4.6         3.2          1.4         0.2  setosa
    ## 49          5.3         3.7          1.5         0.2  setosa
    ## 50          5.0         3.3          1.4         0.2  setosa

``` r
xbar_setosa = colMeans(setosa[1:4])
xbar_setosa
```

    ## Sepal.Length  Sepal.Width Petal.Length  Petal.Width 
    ##        5.006        3.428        1.462        0.246

``` r
x1bar = matrix(xbar_setosa,4,1)
x1bar
```

    ##       [,1]
    ## [1,] 5.006
    ## [2,] 3.428
    ## [3,] 1.462
    ## [4,] 0.246

``` r
s1_s = cov(setosa[1:4])
s1_s
```

    ##              Sepal.Length Sepal.Width Petal.Length Petal.Width
    ## Sepal.Length   0.12424898 0.099216327  0.016355102 0.010330612
    ## Sepal.Width    0.09921633 0.143689796  0.011697959 0.009297959
    ## Petal.Length   0.01635510 0.011697959  0.030159184 0.006069388
    ## Petal.Width    0.01033061 0.009297959  0.006069388 0.011106122

``` r
s1 = matrix(s1_s,4,4)
s1
```

    ##            [,1]        [,2]        [,3]        [,4]
    ## [1,] 0.12424898 0.099216327 0.016355102 0.010330612
    ## [2,] 0.09921633 0.143689796 0.011697959 0.009297959
    ## [3,] 0.01635510 0.011697959 0.030159184 0.006069388
    ## [4,] 0.01033061 0.009297959 0.006069388 0.011106122

``` r
n1 = nrow(setosa)
n1
```

    ## [1] 50

``` r
# Data Versicolor
versicolor = data_new$versicolor
xbar_vc = colMeans(versicolor[1:4])
xbar_vc
```

    ## Sepal.Length  Sepal.Width Petal.Length  Petal.Width 
    ##        5.936        2.770        4.260        1.326

``` r
x2bar = matrix(xbar_vc,4,1)
x2bar
```

    ##       [,1]
    ## [1,] 5.936
    ## [2,] 2.770
    ## [3,] 4.260
    ## [4,] 1.326

``` r
s2_vc = cov(versicolor[1:4])
s2_vc
```

    ##              Sepal.Length Sepal.Width Petal.Length Petal.Width
    ## Sepal.Length   0.26643265  0.08518367   0.18289796  0.05577959
    ## Sepal.Width    0.08518367  0.09846939   0.08265306  0.04120408
    ## Petal.Length   0.18289796  0.08265306   0.22081633  0.07310204
    ## Petal.Width    0.05577959  0.04120408   0.07310204  0.03910612

``` r
s2 = matrix(s2_vc,4,4)
s2
```

    ##            [,1]       [,2]       [,3]       [,4]
    ## [1,] 0.26643265 0.08518367 0.18289796 0.05577959
    ## [2,] 0.08518367 0.09846939 0.08265306 0.04120408
    ## [3,] 0.18289796 0.08265306 0.22081633 0.07310204
    ## [4,] 0.05577959 0.04120408 0.07310204 0.03910612

``` r
n2 = nrow(versicolor)
n2
```

    ## [1] 50

``` r
# Data Virginica
virginica = data_new$virginica
xbar_v = colMeans(virginica[1:4])
xbar_v
```

    ## Sepal.Length  Sepal.Width Petal.Length  Petal.Width 
    ##        6.588        2.974        5.552        2.026

``` r
x3bar = matrix(xbar_v,4,1)
x3bar
```

    ##       [,1]
    ## [1,] 6.588
    ## [2,] 2.974
    ## [3,] 5.552
    ## [4,] 2.026

``` r
s3_v = cov(virginica[1:4])
s3_v
```

    ##              Sepal.Length Sepal.Width Petal.Length Petal.Width
    ## Sepal.Length   0.40434286  0.09376327   0.30328980  0.04909388
    ## Sepal.Width    0.09376327  0.10400408   0.07137959  0.04762857
    ## Petal.Length   0.30328980  0.07137959   0.30458776  0.04882449
    ## Petal.Width    0.04909388  0.04762857   0.04882449  0.07543265

``` r
s3 = matrix(s3_v,4,4)
s3
```

    ##            [,1]       [,2]       [,3]       [,4]
    ## [1,] 0.40434286 0.09376327 0.30328980 0.04909388
    ## [2,] 0.09376327 0.10400408 0.07137959 0.04762857
    ## [3,] 0.30328980 0.07137959 0.30458776 0.04882449
    ## [4,] 0.04909388 0.04762857 0.04882449 0.07543265

``` r
n3 = nrow(virginica)
n3
```

    ## [1] 50

``` r
alfa = 0.05

# Calculate W
W = ((n1-1)*s1)+((n2-1)*s2)+((n3-1)*s3)
W
```

    ##         [,1]    [,2]    [,3]   [,4]
    ## [1,] 38.9562 13.6300 24.6246 5.6450
    ## [2,] 13.6300 16.9620  8.1208 4.8084
    ## [3,] 24.6246  8.1208 27.2226 6.2718
    ## [4,]  5.6450  4.8084  6.2718 6.1566

``` r
# Calculate Xbar total
xbar = ((n1*x1bar)+(n2*x2bar)+(n3*x3bar))/(n1+n2+n3)
xbar
```

    ##          [,1]
    ## [1,] 5.843333
    ## [2,] 3.057333
    ## [3,] 3.758000
    ## [4,] 1.199333

``` r
# Calculate B
B = (n1*(x1bar - xbar)%*%t(x1bar - xbar))+(n2*(x2bar - xbar)%*%t(x2bar - xbar))+(n3*(x3bar - xbar)%*%t(x3bar - xbar))
B
```

    ##           [,1]      [,2]     [,3]      [,4]
    ## [1,]  63.21213 -19.95267 165.2484  71.27933
    ## [2,] -19.95267  11.34493 -57.2396 -22.93267
    ## [3,] 165.24840 -57.23960 437.1028 186.77400
    ## [4,]  71.27933 -22.93267 186.7740  80.41333

``` r
# calculate lamda
lamda = det(W)/det(B+W)
lamda
```

    ## [1] 0.02343863

``` r
# Calculate Comp Value
comp_val = ((n-p-2)/p)*((1-sqrt(lamda))/sqrt(lamda))
comp_val
```

    ## [1] 199.1453

``` r
# Calculate Cri_val
cri_val = qf(1-alfa,2*p,2*(n-p-2))
cri_val
```

    ## [1] 1.970619

``` r
## Conclusion
if(comp_val < cri_val){
  paste("Since Computational Value = ",comp_val, "< Critical Value = ",cri_val,
      "so we cannot reject H0 at the significant level", alfa)
}else if(comp_val == cri_val){
   paste("Since Computational Value = ",comp_val, "= Critical Value = ",cri_val,
      "so we cannot reject H0 at the significant level", alfa)
}else{
  paste("Since Computational Value = ",comp_val, "> Critical Value = ",cri_val,
      "so we reject H0 at the significant level", alfa)
}
```

    ## [1] "Since Computational Value =  199.145343540084 > Critical Value =  1.9706194163219 so we reject H0 at the significant level 0.05"

**Conclusion:**

Since comp_val\>cri_val, then reject H0. So, we can conclude that at
least 2 mean vector are different.

**EXAMPLE 4.2**

**Input Part**

``` r
X1 = c(21,25,20,24,31,23,24,28,34,29,35,32,33,38,34,35)
X2 = c(12,8,12,10,9,12,13,10,10,14,11,13,14,12,13,13)
Level = matrix(0,16,1)
Level[1:4]="Level 1"
Level[5:8]="Level 2"
Level[9:12]="Level 3"
Level[13:16]="Level 4"
head(Level)
```

    ##      [,1]     
    ## [1,] "Level 1"
    ## [2,] "Level 1"
    ## [3,] "Level 1"
    ## [4,] "Level 1"
    ## [5,] "Level 2"
    ## [6,] "Level 2"

``` r
tail(Level)
```

    ##       [,1]     
    ## [11,] "Level 3"
    ## [12,] "Level 3"
    ## [13,] "Level 4"
    ## [14,] "Level 4"
    ## [15,] "Level 4"
    ## [16,] "Level 4"

``` r
data_nitro = data.frame(X1,X2,Level)
data_nitro
```

    ##    X1 X2   Level
    ## 1  21 12 Level 1
    ## 2  25  8 Level 1
    ## 3  20 12 Level 1
    ## 4  24 10 Level 1
    ## 5  31  9 Level 2
    ## 6  23 12 Level 2
    ## 7  24 13 Level 2
    ## 8  28 10 Level 2
    ## 9  34 10 Level 3
    ## 10 29 14 Level 3
    ## 11 35 11 Level 3
    ## 12 32 13 Level 3
    ## 13 33 14 Level 4
    ## 14 38 12 Level 4
    ## 15 34 13 Level 4
    ## 16 35 13 Level 4

**Assumption Check**

- Cond. 1 =\> Independent samples: (Hold)

- Cond. 2 =\> Equality in covariance matrices:

``` r
library(biotools)
```

    ## Warning: package 'biotools' was built under R version 4.1.3

    ## Loading required package: MASS

    ## Warning: package 'MASS' was built under R version 4.1.3

    ## ---
    ## biotools version 4.2

``` r
homogeneity = boxM(data_nitro[,1:2],data_nitro[,3])
homogeneity
```

    ## 
    ##  Box's M-test for Homogeneity of Covariance Matrices
    ## 
    ## data:  data_nitro[, 1:2]
    ## Chi-Sq (approx.) = 5.6432, df = 9, p-value = 0.775

Because p-value \< 0.05, then we cannot reject H0. So we can assumed
that all groups have the same covariance matrix Sigma

- Cond. 3 =\> Multivariate normal

**MANOVA test**

``` r
nitro.man = manova(cbind(X1,X2) ~ Level, data = data_nitro)
summary(nitro.man, test="Wilks")
```

    ##           Df    Wilks approx F num Df den Df    Pr(>F)    
    ## Level      3 0.025465   19.311      6     22 9.717e-08 ***
    ## Residuals 12                                              
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Since p-value \< 0.05, then reject H0. So, we can conclude that at least
two vector miu are different.

## Pair Comparisons

Do the pair comparisons if we reject H0 for the MANOVA test, because it
indicates that at least two mean vector are different and we want to
know which group is different.

To Explain this, we will use **example 4.1.**

#### First, do the MANOVA TEST

H0 : Miu1=Miu2=Miu3

**Input Part**

``` r
# Input Part
X1bar = matrix(c(2.006,0.48,0.082,0.36),4,1)
X2bar = matrix(c(2.167,0.596,0.124,0.418),4,1)
X3bar = matrix(c(2.273,0.521,0.125,0.383),4,1)

S1=matrix(c(0.291,-0.001,0.002,0.01,-0.001,0.011,0.001,0.003,0.002,0.001,0.001,0.001,0.01,0.003,0.001,0.01),4,4)
S2=matrix(c(0.561,0.011,0.001,0.037,0.011,0.025,0.004,0.007,0.001,0.004,0.005,0.002,0.037,0.007,0.002,0.019),4,4)
S3=matrix(c(0.261,0.03,0.003,0.018,0.03,0.017,-0.001,0.006,0.003,-0.001,0.004,0.001,0.018,0.006,0.001,0.013),4,4)

n1 = 271
n2 = 138 
n3 = 107
n = n1+n2+n3
p = 4 
g = 3
alfa = 0.05
```

**Computation Part**

``` r
# Computation Part
## Calculate W
W = (n1-1)*S1 + (n2-1)*S2 + (n3-1)*S3

## Calculate Xbar Total
xbar = (n1*X1bar+n2*X2bar+n3*X3bar)/(n1+n2+n3)

## Calculate B
B = (n1*(X1bar - xbar)%*%t(X1bar - xbar)) + (n2*(X2bar - xbar)%*%t(X2bar - xbar)) + (n3*(X3bar - xbar)%*%t(X3bar - xbar))

## Calculate Lamda
lamda = det(W)/det(B+W)

## Calculate Computational Value
comp_val = ((n - p - 2)/p)*((1 - sqrt(lamda))/sqrt(lamda))
comp_val
```

    ## [1] 18.62007

``` r
## Calculate Critical Value
cri_val = qf(1 - alfa,2*p,2*(n-p-2))

## Conclusion
if(comp_val < cri_val){
  paste("Since Computational Value = ",comp_val, "< Critical Value = ",cri_val,
      "so we cannot reject H0 at the significant level", alfa)
}else if(comp_val == cri_val){
   paste("Since Computational Value = ",comp_val, "= Critical Value = ",cri_val,
      "so we cannot reject H0 at the significant level", alfa)
}else{
  paste("Since Computational Value = ",comp_val, "> Critical Value = ",cri_val,
      "so we reject H0 at the significant level", alfa)
}
```

    ## [1] "Since Computational Value =  18.6200740392198 > Critical Value =  1.94746468922519 so we reject H0 at the significant level 0.05"

Because we reject H0, so at least two vector miu are different.

Then we can do the Pairwise Comparisons using Bonferroni Method.

#### Second, do the Pairwise Comparisons

We can use the MANOVA test results to estimate the magnitudes of the
differences. A comparison of the variable X3, costs of plant operation
and maintenance labor, between privately owned nursing homes and
government-owned nursing homes can be made by estimating Tao13 - Tao33.

``` r
# Computation Part
## Calculate Tao1
T1 = X1bar - xbar

## Calculate Tao3
T3 = X3bar - xbar

## Calculate Tao13 - Tao33
T1_T3 = T1 - T3
T13_T33 = T1_T3[3]

## Calculate w33
w33 = W[3,3]

## Calculate standard deviation or sqrt(var)
stdev = sqrt(((1/n1)+(1/n3))*w33/(n-g))

## Calculate t table
t = qt(alfa/(p*g*(g-1)),n-g, lower.tail=FALSE)

## Calculate Lower and Upper
L = T13_T33 - (t*stdev)
paste("The Lower bound is", L)
```

    ## [1] "The Lower bound is -0.0600376544467082"

``` r
U = T13_T33 + (t*stdev)
paste("The Upper bound is", U)
```

    ## [1] "The Upper bound is -0.0259623455532918"

Because the 95% confidence interval is (-0.0600376,-0.02596), doesn’t
include zero (0), then we can conclude that the average maintenance and
labor cost for government-owned nursing homes and privately are
different. Since the interval is a negative value for both lower and
upper bound, we can conclude that the average maintenance and labor cost
for government-owned nursing homes is higher by 0.02596 to 0.0600376
hour per patient day than for privately owned nursing homes.
