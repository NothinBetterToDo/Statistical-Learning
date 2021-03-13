## [Box-Cox Transformation](#Box-Cox)

Some machine learning models assume data is normally distributed. Therefore, results will be biased when this assumption is not met. The unequal variance in a data is called heteroscedasticity. Higher variance in certain data points will make those estimation erros larger and push a model to fit those points. 

A Box-Cox transformation, is one of the methods that can deal with heteroscedasticity. This approach is a logarithmic transformation, that shrinks the larger range to reduce its variability and stretches out smaller range to enlarge its variability. 


The idea is to find best value of ![lambda](https://latex.codecogs.com/gif.latex?%5Clambda):

```markdown
t(y), or transform vector of Y, so that it can become closer to normal distribution. 
```
We will need to find the power transformation, lambda, that maximizes the likelihood when a 
specified set of explanatory variables is fitted to the following equation as the response: 

![Power Transformation](https://latex.codecogs.com/gif.latex?t%28y%29%20%3D%20%5Cfrac%7B%28y%5E%7B%5Clambda%7D-1%29%7D%7B%5Clambda%20%7D)






The value of lambda can be positive or negative, but not zero. 

For lambda = 0, the Box-Cox transformation is defined as log(y). 

For lambda = -1, the formula:

![Example 1](https://latex.codecogs.com/gif.latex?%5Cfrac%7By%5E%7B-1%7D-1%7D%7B-1%7D%20%3D%20%5Cfrac%7B%5Cfrac%7B1%7D%7By%7D%20-%201%7D%7B-1%7D%20%3D%201%20-%20%5Cfrac%7B1%7D%7By%7D)





We can use Q-Q plot to check if we need any transformation. 





## [De-Trending](#De-Trending) 

Trend: increase/decrease of data over time and a trend in a time-series could cause issue with a factor-based analysis. De-trending can be used on either response, or predictors. 

One method of de-trending by using 1-dimensional regression (linear fit): 

![Linear Fit Example](https://latex.codecogs.com/gif.latex?y%20%3D%20a_%7B0%7D%20&plus;%20a_%7B1%7Dx)










## [PCA](#PCA) 

PCA is a dimensionality reduction technique, when we have too many predictors and/or high correlction between some of the predictors. PCA transforms data, by changing the coordinates to remove correlation and ranking coordinates by importance (in order of the amount of variants). 

There are 2 benefits on concentrating on the first n principal components: 
- reduce effect of randomness
- earlier principal components are likely to have higher signal-to-noise ratio (driven by actual effects, than random effects)

Principal components are orthogonal with each other. The steps are outlined below:

  ![scale](https://latex.codecogs.com/gif.latex?scale%20%5Cfrac%7B1%7D%7Bm%7D%20%5Csum_i%20x_%7Bij%7D%20%3D%20u_%7Bj%7D%20%3D%200)

- find all the eigenvectors ![xtx](https://latex.codecogs.com/gif.latex?X%5E%7BT%7DX)
- V: matrix of eigenvectors (sorted by eigenvalue)
- V = [V1, V2...], where ![j](https://latex.codecogs.com/gif.latex?V_%7Bj%7D%20%3D%20jth%5Crightarrow%20X%5E%7BT%7DX)


- PCA Linear transformation, where 1st component is XV1, 2nd = XV2

- kth new factor vlaue for ith data point: ![kth](https://latex.codecogs.com/gif.latex?t_%7Bik%7D%20%3D%20%5Csum_%7Bm%7D%5E%7Bj%3D1%7D%20x_%7Bij%7D%20v_%7Bjk%7D)




Doing so, PCA eliminates correlation between factors. If want to have fewer variables, only include the first n principal components. We can also deal with non-linear functions using kernels (similar to SVM modeling). 


Decode unscale coefficients:

![Y 1step](https://latex.codecogs.com/gif.latex?%5Chat%7BY%7D%20%3D%20%5Chat%7B%5Cbeta%7D%20&plus;%20%5Csum_%7Bk%7D%5E%7Bi%3D1%7D%20%5Chat%7B%5Cbeta_%7Bi%7D%20%7D%20*%20z_%7Bi%7D)



![Y_2step](https://latex.codecogs.com/gif.latex?%5Chat%7BY%7D%20%3D%20%5Chat%7B%5Cbeta%20%7D%20&plus;%20%5Csum_%7Bk%7D%5E%7Bi%3D1%7D%20%5Chat%7B%5Cbeta%20_%7Bi%7D%7D%20*%20%28%5Cfrac%7Bx_%7Bi%7D%20-%20%5Cbar%7Bx%7D%20%7D%7Bs_%7Bi%7D%7D%29)




![Y_3step](https://latex.codecogs.com/gif.latex?%5Chat%7BY%7D%20%3D%20%5Chat%7B%5Cbeta%7D%20&plus;%20%5Csum_%7Bk%7D%5E%7Bi%3D1%7D%20%5Cfrac%7B%5Chat%7B%5Cbeta%20x_%7Bi%7D%7D%7D%7Bs_%7Bi%7D%7D%20-%20%5Csum_%7Bk%7D%5E%7Bi%3D1%7D%20%5Cleft%20%28%20%5Cfrac%7B%5Chat%7B%5Cbeta%20%5Cbar%7Bx_%7Bi%7D%7D%7D%7D%20%7Bs_%7Bi%7D%7D%20%5Cright%20%29)


![Y_4step](https://latex.codecogs.com/gif.latex?%5Chat%7BY%7D%20%3D%20%5Cbeta%20-%20%5Csum_%7Bk%7D%5E%7Bi%3D1%7D%20%5Cleft%20%28%20%5Cfrac%7B%5Chat%7B%5Cbeta%20%5Cbar%7Bx_%7Bi%7D%7D%7D%7D%7Bs_%7Bi%7D%7D%20%5Cright%20%29%20&plus;%20%5Csum_%7Bk%7D%5E%7Bi%3D1%7D%20%5Cleft%20%28%20%5Cfrac%7B%5Chat%7B%5Cbeta%20_%7Bi%7D%7D%7D%7Bs_%7Bi%7D%7D%20x_%7Bi%7D%5Cright%20%29)







Question: A = n x n matrix. A scalar ![lambda](https://latex.codecogs.com/gif.latex?%5Clambda) is called an eigenvalue of A, if there is a non-zero vector ![x](https://latex.codecogs.com/gif.latex?%5Cbar%7Bx%7D) such that ![A](https://latex.codecogs.com/gif.latex?A%5Cbar%7Bx%7D%20%3D%20%5Clambda%20%5Cbar%7Bx%7D). 

Such a vector ![x](https://latex.codecogs.com/gif.latex?%5Cbar%7Bx%7D) is called an eigenvector of A corresponding to ![lambda](https://latex.codecogs.com/gif.latex?%5Clambda). 



Show that x = ![x](https://latex.codecogs.com/gif.latex?%5Cbar%7Bx%7D) is an eigenvector of ![A](https://latex.codecogs.com/gif.latex?A%5Cbar%7Bx%7D%20%3D%20%5Clambda%20%5Cbar%7Bx%7D) corresponding to ![lambda](https://latex.codecogs.com/gif.latex?%5Clambda) = 4. 


![Eq1](https://latex.codecogs.com/gif.latex?A%5Cbar%7Bx%7D%20%3D%20%5Clambda%20%5Cbar%7Bx%7D)

![Eq2](https://latex.codecogs.com/gif.latex?%5Cbegin%7Bpmatrix%7D%203%20%26%202%5C%5C%203%20%26%20-2%5C%5C%20%5Cend%7Bpmatrix%7D%20%5Cbegin%7Bpmatrix%7D%202%5C%5C%201%5C%5C%20%5Cend%7Bpmatrix%7D%20%3D%204%5Cbegin%7Bpmatrix%7D%202%5C%5C%201%5C%5C%20%5Cend%7Bpmatrix%7D)

![Eq3](https://latex.codecogs.com/gif.latex?%5Cbegin%7Bbmatrix%7D%203.2%20&plus;%202.1%5C%5C%203.2%20&plus;%28-2%29.1%20%5C%5C%20%5Cend%7Bbmatrix%7D%20%3D%20%5Cbegin%7Bbmatrix%7D%208%5C%5C%204%5C%5C%20%5Cend%7Bbmatrix%7D)

![Eq4](https://latex.codecogs.com/gif.latex?%5Cbegin%7Bpmatrix%7D%208%5C%5C%204%5C%5C%20%5Cend%7Bpmatrix%7D%20%3D%20%5Cbegin%7Bpmatrix%7D%208%5C%5C%204%5C%5C%20%5Cend%7Bpmatrix%7D)



This means if lambda is an eigenvalue of A, and x is an eigenvector belonging to lambda, any non-zero multiple of x will be an eigenvector. 




![Assuming](https://latex.codecogs.com/gif.latex?Assuming%3A%20A%5Cbar%7Bx%7D%20%3D%20%5Clambda%20%5Cbar%7Bx%7D)




![Proof](https://latex.codecogs.com/gif.latex?A%28%5Calpha%20%5Cbar%7Bx%7D%29%20%3D%20%5Calpha%20A%5Cbar%7Bx%7D%20%3D%20%5Calpha%20%5Clambda%20%5Cbar%7Bx%7D%20%3D%20%5Clambda%20%28%5Calpha%20%5Cbar%7Bx%7D%29)





## [Regression](#Regression)

It can be used to determine how do systems work (descriptive), and what will happen in the future (predictive). 

But we need to take note that correlation does not mean causation. So just because there's a correlation and our regression model can make good predictions, it does not mean the predictors caused the response. 

We can also adjust the data so the fit is linear:
- Quadratic regression 
- Response transform, log(y)
- Box-Cox transformation
- Variable interaction, add interaction term e.g. x1x2


We can determine whether the fitted line is good or not, by looking at the sum of squared errors. The coefficients for x  change as we move the line, and the best-fit regression line is the one that minimizes sum of squared errors. The sum of squared errors (SSE) is a convex quadratic function and we need to minimize it, by taking partial derivatives of the sum of squared errors term with respect to each constant & set to zero and solve these equations simultaneously to find the minimum SSE.

Data point i prediction error: 

![pred error](https://latex.codecogs.com/gif.latex?y%20-%20%5Chat%7By%7D%20%3D%20y_%7Bi%7D%20-%20%28a_%7B0%7D%20&plus;%20a_%7B1%7D%20x_%7Bi%7D%29)




Sum of squared errors: 

![sse1](https://latex.codecogs.com/gif.latex?%5Csum_%7Bi%3D1%7D%5E%7Bn%7D%20%5Cleft%20%28%20y_%7Bi%7D%20-%20%5Chat%7By_%7Bi%7D%7D%20%5Cright%20%29%5E%7B2%7D)





![sse2](https://latex.codecogs.com/gif.latex?%3D%20%5Csum%20%5Cleft%20%28%20y_%7Bi%7D%20-%20%28a_%7B0%7D%20&plus;%20a_%7B1%7Dx_%7Bi%7D%29%20%5Cright%20%29%5E%7B2%7D)



How can we measure model quality?

**Likelihood**

The most basic is likelihood. We can measure the probability (density) for any parameter set, and whichever set of parameters gives the highest probability density is called the maximum likelihood (best fit set of parameters). 

Assume:
- error is normally distributed with mean = 0, and variant sigma squared. 
- independent
- identically distributed

Then the set of parameters that minimizes the SSE is the maximum likelihood fit (MLE). 

![SSE](https://latex.codecogs.com/gif.latex?Minimize%20%5Csum_%7Bn%7D%5E%7Bi%3D1%7D%5Cleft%20%28%20z_%7Bi%7D%20-%20%28a_%7B0%7D%20&plus;%20%5Csum_%7Bm%7D%5E%7Bj%3D1%7D%20a_%7Bj%7Dx_%7Bij%7D%29%5E%7B2%7D%20%5Cright%20%29)





where xij = observed predictor value, a0 - am = parameters to fit. 

We can use likelihood to compare 2 different models by using the likelihood ratio and conduct a hypothesis test. 




**Akaike Information Criterion(AIC)** 

Aikaike's information criterion (AIC) is known as a penalized log-likelihood. Adding extra parameters can lead to overfitting to fit random effects. Smallest AIC is preferred - encourages fewer parameters k, and higher likelihood.
```
- L*: maximum likelihood value
- k: number of parameters being estimated
```


![AIC](https://latex.codecogs.com/gif.latex?AIC%20%3D%202k%20-%202%20ln%20%28L%5E%7B*%7D%29)




![AIC Substitute](https://latex.codecogs.com/gif.latex?AIC%20%3D%202%28m&plus;1%29%20-%202%20ln%5Cleft%20%28%20%5Cfrac%7B1%7D%7B%5Csigma%20%5Csqrt%7B2%5Cpi%20%7D%5E%7Bn%7D%7D%20e%5E%7B-%5Cfrac%7B1%7D%7B2%5Csigma%20%5E%7B2%7D%7D%7D%20%5Csum_%7Bn%7D%5E%7Bi%3D1%7D%20%28z%7B_%7Bi%7D%7D%20-%20%28a%5E%7B_%7B0%7D%7D%20&plus;%20%5Csum_%7Bm%7D%5E%7Bj%3D1%7D%20a_%7Bj%7D%20x_%7Bij%7D%29%29%5E%7B2%7D%20%5Cright%20%29)





**Corrected AIC***

AIC has nice properties if there are infinitely manay data points to fit the model. There's a correction term we can add to AIC to deal with data where data set is not infinite.


![Corrected AIC](https://latex.codecogs.com/gif.latex?AIC_%7Bc%7D%20%3D%20AIC%20&plus;%20%5Cfrac%7B2k%28k&plus;1%29%7D%7Bn-k%3D1%7D%20%3D%202k%20-%202%20ln%28L%5E%7B*%7D%29%29%20&plus;%20%5Cfrac%7B2k%28k&plus;1%29%29%7D%7Bn-k-1%7D)




We can calculate the relative probability that one of the models is better than the other. 

Example: 

- Model 1: AIC = 80
- Model 2: AIC = 85



![AIC Example 1](https://latex.codecogs.com/gif.latex?e%5E%5Cfrac%7B%28AIC_%7B1%7D%20-%20AIC_%7B2%7D%29%7D%7B2%7D)





![AIC Example 2](https://latex.codecogs.com/gif.latex?e%5E%7B%5Cfrac%7B80-85%7D%7B2%7D%7D%20%5Capprox%208.2%25)




It is much more likely that the first model is better. 



**Bayesian Information Criterion(BIC)**

![BIC Formula](https://latex.codecogs.com/gif.latex?BIC%20%3D%20k%20ln%28n%29%20-%202%20ln%20%28L%5E%7B*%7D%29)




```
L* = maximum likelihood value

k  = number of parameters being estimated

n  = number of data points 
```

Similar to AIC:
- penalty term for BIC > AIC, so encourages models with fewer parameters than AIC does
- Only use BIC when data points > parameters 

When comparing 2 models on the same dataset by their BIC
- difference > 10, smaller BIC is **very likely** better
- 6 < difference < 10, then smaller BIC is **likely** better
- 2 < difference < 6, then smaller BIC is **somewhat likely** better
- 0 < difference < 2, then smaller BIC is **slightly likely** better 

The difference between AIC and BIC:
- AIC: frequentist point of view
- BIC: Bayesian point of view


**Regression Output**

- P-values:
  - if > 0.05, remove the attribute. 
  - Higher thresholds, more factors can be included but might include irrelevant factor
  - Lower thresholds, less factors can be included and might leave out relevant factor
  - But with large amounts of data, p-values can be significant/small even when the factor is not related to the response 
  
- Confidence Interval (CI): where the coefficient probably lies, and how close to zero 

- T-Statistic: coeff / standard error, related to p-value

- Coefficient: not much difference even if very low p-value, then it isn't very meaningful

- R-squared: estimate how much variations the model accounts for 
  - e.g. R-squared = 80% , the model accounts for 80% of variability in the data & the rest are randomness or other factors 


## [Advanced Regression](#Advanced Regression)

We can use trees to divide data set, and speficy different modesl for each subset of the data. 

1. Classification Problems
   - CART (Classification and Regression Trees)
2. Decision Making
   - Decision Tree

Trees Branching

- Common practice is to branch one factor at a time
- Use half of the data, and build a regression model 
   - calculate variance of the response for all data points in the leaf
   - test spliting to determine total variance of the 2 branches & choose the lowest 
   - if enough data points make the split
   - can go backwars & prune the tree using the other half of data
- Common rule is to stop branching if a leaf would contain < than 5% of the data points, or low improvement benefit 


**Random Forests**

- if it's a regression tree, use the average predicted response
- if it's a classication tree, use the most common predicted response

Pros: better overall estimates, averages between trees somehow neutralizes overfitting
Cons: harder to explain/interpret, can't given specific model from the data


**Logistic Regression**

This model is useful when response is a probability (number between 0 and 1) and binary (either 0,1). 

![logit 1](https://latex.codecogs.com/gif.latex?log%20%5Cfrac%7Bp%7D%7B1-p%7D%20%3D%20a_%7B0%7D%20&plus;%20a_%7B1%7D%20x_%7B1%7D%20&plus;%20a_%7B2%7Dx_%7B2%7D%20&plus;%20...%20&plus;%20a_%7Bj%7Dx_%7Bj%7D)



![logit 2](https://latex.codecogs.com/gif.latex?p%20%3D%20%5Cfrac%7B1%7D%7B1&plus;e%5E%7B-%28a_%7B0%7D%20&plus;%20a_%7B1%7D%20x_%7B1%7D%20&plus;%20a_%7B2%7Dx_%7B2%7D%20&plus;%20...%20&plus;%20a_%7Bj%7Dx_%7Bj%7D%20%29%7D%7D)



![logit 3](https://latex.codecogs.com/gif.latex?a_%7B0%7D%20&plus;%20a_%7B1%7D%20x_%7B1%7D%20&plus;%20a_%7B2%7Dx_%7B2%7D%20&plus;%20...%20&plus;%20a_%7Bj%7Dx_%7Bj%7D%20%3D%20-%5Cinfty%20%2C%20p%20%3D%200)




![logit 4](https://latex.codecogs.com/gif.latex?a_%7B0%7D%20&plus;%20a_%7B1%7D%20x_%7B1%7D%20&plus;%20a_%7B2%7Dx_%7B2%7D%20&plus;%20...%20&plus;%20a_%7Bj%7Dx_%7Bj%7D%20%3D%20&plus;%5Cinfty%20%2C%20p%20%3D1)

Pseudo R-squared is not really measuring fraction of variance. 

Receiver Operating Characteristic (ROC) Curve to specifiy a threshold probability. It is quicky way to determine quality of the model but does not provide cost of false negatives and false positives. 

- x-axis: 1 - Specificity = 1 - TN/(TN + FP) 
- y-axis: Sensitivity = TP/(TP + FN) 

**Confusion Matrix**

| Classification | Yes (Model) | No (Model) |
| --------------- | --------------- | --------------- |
| Yes (True)| Correct | Incorrect |
| No (True) | Incorrect| Correct |


**References**

1. The R Book, by Michael J.Crawley, Published by Wiley, 2007.
2. Introduction to Analytics Modeling, by Prof.Joel Sokol.





