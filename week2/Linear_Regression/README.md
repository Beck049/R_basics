# Linear Regression

## set up
```r
library(jtools) 

fb=read.csv("Facebook_conversion_data.csv")
```

## Linear Regression

```r
relation <- lm(Total_Conversion~Spent,data=fb)
summary(relation)
```

> lm( fitting_formula, dataframe ) <br>
> > **fitting_formula** <br>
> > Yvar ~ Xvar : <br>
> > Yvar is  dependent  (predicted) <br>
> > Xvar is independent (predictor) <br>

```cml
Call:
lm(formula = Total_Conversion ~ Spent, data = fb)

Residuals:
    Min      1Q  Median      3Q     Max 
-12.395  -0.576  -0.007   0.066  35.118 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)    
(Intercept) 0.933613   0.106096     8.8   <2e-16 ***
Spent       0.037422   0.001051    35.6   <2e-16 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 3.088 on 1141 degrees of freedom
Multiple R-squared:  0.5262,	Adjusted R-squared:  0.5258 
F-statistic:  1267 on 1 and 1141 DF,  p-value: < 2.2e-16
```

## Prediction
```r
a <- data.frame(Spent = c(170, 280, 390))   # let Spent = c(170, 280, 390)
result <-  predict(relation,a)    # use the relation we set above
result
```
> predict( object, newdata, interval ) <br>
> >  **object** : the class inheriting from 'lm' <br>
> > **newdata **: input data to predict <br>
> > **interval**: type of interval calculation <br>
```cml
        1         2         3 
 7.295392 11.411837 15.528281 
```
predict the corresponding Total_Conversion
using given values of Spent ( c(170, 280, 390) )

## Visualize

### plot()
```r
# Plot the chart.
plot( fb$Spent, fb$Total_Conversion, 
      col = "black",
      main = "Spent and Conversion Regression",
      abline(lm(Total_Conversion~Spent,data=fb)), 
      xlab = "Amount spent on campaign",
      ylab = "Total number of conversions")
```

### ggplot
```r
#plot the data together with the fitted line
ggplot(fb, aes(Spent, Total_Conversion)) 
+ geom_point() 
+ geom_smooth(method = "lm") 
+ labs(x = "Amount spent on campaign", y = "Total number of conversions")
```

## Multiple Regressors
```r
relation <- lm(Total_Conversion ~ Spent + gender_factor + age_factor, data=fb)
summary(relation)
```

### visualize
```r
plot_coefs(relation)
```
