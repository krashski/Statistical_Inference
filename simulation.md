# A Demonstration of the Central Limit Theorem Using The Exponential Distribution
Russ Boucher  
March 5, 2015  

## Overview
The purpose of this project is to investigate the exponential distribution in R and compare it with the Central Limit Theorem. The exponential distribution can be simulated in R using the `rexp(n, lambda)` function, where n is the number of observations and lambda is the rate parameter. 

There are four parts to this project:
* Run a simulation to generate a distribution of 1000 means of 40 exponentials 
* Compare the sample mean to the theoretical mean
* Compare the sample variance to the theoretical variance
* Showing that the distribution is approximately normal

## Simulations

```r
# set the random seed
set.seed(42)

# generate a distribution of 1000 means of 40 exponentials using rexp(n, lambda)
# lambda is set to 0.2 for the simulation                                                                   
mns = NULL
n <- 40
lambda <- 0.2
for (i in 1:1000){
   mns  = c(mns, mean(rexp(n, lambda)))
}
```


## Sample Mean versus Theoretical Mean

```r
### 1. Show the sample mean and compare it to the theoretical mean
mean(mns) # sample mean
```

```
## [1] 4.986508
```

```r
print(1/lambda) # theoretical mean
```

```
## [1] 5
```




```r
# plot a histogram of the 40 means
hist(mns, main = "Histogram of Means of 40 Exponentials", xlab = "Average", col = "red")
```

![](simulation_files/figure-html/histogram-1.png) 

## Sample Variance versus Theoretical Variance

```r
### 2. Show how variable the sample is (via variance) and compare it
### to the theoretical variance of the distribution
var(mns) # sample variance
```

```
## [1] 0.6344405
```

```r
print(1/(lambda^2 * n)) # theoretical variance
```

```
## [1] 0.625
```


## Distribution

```r
### 3. Show that the distribution is approximately normal
# convert the means to standard (Z) scores
mns_scale <- scale(mns)
```



```r
# Q-Q plot of sample quantiles against theoretical quantiles
# A linear trend suggests the distribution is normal
qqnorm(mns_scale, main = "Normal Q-Q Plot of the Distribution of the Means of 40 Exponentials")
abline(0, 1, lty = 3)
```

![](simulation_files/figure-html/Q-Q_plot-1.png) 
