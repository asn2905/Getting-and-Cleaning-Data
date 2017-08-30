Regression Models Course Project
=================================
##Executive Summary

This assignment is exploring the relationship between a set of variables and miles per gallon (MPG) (outcome), particularly:

The report set out to determine which transmission type produces a higher MPG. The mtcars dataset was used for this analysis. A t-test between automatic and manual transmission vehicles shows that manual transmission vehicles have a 7.245 greater MPG than automatic transmission vehicles. After fitting multiple linear regressions, analysis showed that the manual transmission contributed less significantly to MPG, only an improvement of 1.81 MPG. Other variables, weight, horsepower, and number of cylinders contributed more significantly to the overall MPG of vehicles.

###Loading Required Libraries & Data
```{}
library(ggplot2)
data(mtcars)
head(mtcars, n=3)
dim(mtcars)
mtcars$cyl <- as.factor(mtcars$cyl)
mtcars$vs <- as.factor(mtcars$vs)
mtcars$am <- factor(mtcars$am)
mtcars$gear <- factor(mtcars$gear)
mtcars$carb <- factor(mtcars$carb)
attach(mtcars)
```

###Exploratory Analysis

See Appendix Figure I Exploratory Box graph that compares Automatic and Manual transmission MPG. The graph leads us to believe that there is a significant increase in MPG when for vehicles with a manual transmission vs automatic.

Starting Statistical Inference

T-Test transmission type and MPG

```{}
testResults <- t.test(mpg ~ am)
testResults$p.value
```

The T-Test rejects the null hypothesis that the difference between transmission types is 0.
```{}
testResults$estimate
```

###Starting Regression Analysis

Fit the full model of the data
```{}
fullModelFit <- lm(mpg ~ ., data = mtcars)
summary(fullModelFit)  
summary(fullModelFit)$coeff
```

Since none of the coefficients have a p-value less than 0.05 we cannot conclude which variables are more statistically significant.

```{}
stepFit <- step(fullModelFit)
summary(stepFit) 
summary(stepFit)$coeff 
```

The new model has 4 variables (cylinders, horsepower, weight, transmission). The R-squared value of 0.8659 confirms that this model explains about 87% of the variance in MPG. The p-values also are statistically significantly because they have a p-value less than 0.05. The coefficients conclude that increasing the number of cylinders from 4 to 6 with decrease the MPG by 3.03. Further increasing the cylinders to 8 with decrease the MPG by 2.16. Increasing the horsepower is decreases MPG 3.21 for every 100 horsepower. Weight decreases the MPG by 2.5 for each 1000 lbs increase. A Manual transmission improves the MPG by 1.81.

## Appendix
```{}
boxplot(mpg ~ am, 
          xlab="Transmission Type (0 = Automatic, 1 = Manual)", 
          ylab="MPG",
          main="MPG by Transmission Type")
```

```{}
par(mfrow = c(2, 2))
plot(stepFit)
```

##End
