# Short demo of glm() using simulated data

In order to demonstrate the glm() function for a logistic regression, I will first create some simulated data. Simulations are incredibly useful in population health research because they allow us to generate a world where we know the underlying truth. Here, I am using a simulated dataset to create a reproducible example. 

If you are interested in learning more about the role of simulated data in health research, you may wish to read this paper: Morris, T. P., White, I. R., & Crowther, M. J. (2019). Using simulation studies to evaluate statistical methods. Statistics in Medicine, 38(11), 2074-2102. https://doi.org/10.1002/sim.8086.

```r
################
#Simulated Data#
################

# Set random seed. This will generate the same random data each time you run this code.
set.seed(27)

# Sample size
n <- 1000

# Generate data
df2 <- data.frame(W1=runif(n, min=0.5, max=1),
		  W2=runif(n, min=0, max=1))
df2 <-  transform(df2, #add Y
		  Y=rbinom(n, 1, 1 / (1 + exp(-(-3*W1 - 2*W2 + 2))) ) )
 
# Summary of the variables in dataset ‘df2'
summary(df2)
head(df2)
```

Next, run a multivariable logistic regression.

```r
# Run a multivariable logistic regression
logistic1 <- glm(Y ~ W1 + W2, data=df2, family="binomial")

# Summarize results
summary(logistic1)
```
