## [Outliers](#Outliers)

There are few different types of outliers:

1. Point Outliers - values are far from the rest of the data.
2. Contextual Outliers - relies on the context provided by other points. For instance, when a value is not too far from the rest overall, but far from points nearby in time.
3. Collective Outliers - when data points collectively look like outlier

It can be detected using:

1. Automated methods e.g. box-and-whisker
2. Modeling error e.g. fit exponential smoothing model, and points with very large error might be outlier

## [Change Detection](#Change-Detection)

xt = observed value at time t
mu = mean of x, if no change

If running total > 0, add to the previous metric 

Else, set to 0 because it is irrelevant to detect changes 

Include constant C to pull the running total down a bit. The bigger C, harder for St to get large & less sensitive

![cusum](https://latex.codecogs.com/gif.latex?S_%7Bt%7D%20%3D%20max%20%5Cleft%20%5C%7B%200%2C%20S_%7Bt-1%7D%20&plus;%20%5Cleft%20%28%20x_%7Bt%7D%20-%20%5Cmu%20-%20C%20%5Cright%20%29%20%5Cright%20%5C%7D)



Is St more or equal to T, threshold? 

## [Box-Cox Transformation](#Box-Cox-Transformation)

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

<br />

How can we measure model quality?
<br />
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

<br />

**Akaike Information Criterion(AIC)** 

Aikaike's information criterion (AIC) is known as a penalized log-likelihood. Adding extra parameters can lead to overfitting to fit random effects. Smallest AIC is preferred - encourages fewer parameters k, and higher likelihood.
```
- L*: maximum likelihood value
- k: number of parameters being estimated
```


![AIC](https://latex.codecogs.com/gif.latex?AIC%20%3D%202k%20-%202%20ln%20%28L%5E%7B*%7D%29)




![AIC Substitute](https://latex.codecogs.com/gif.latex?AIC%20%3D%202%28m&plus;1%29%20-%202%20ln%5Cleft%20%28%20%5Cfrac%7B1%7D%7B%5Csigma%20%5Csqrt%7B2%5Cpi%20%7D%5E%7Bn%7D%7D%20e%5E%7B-%5Cfrac%7B1%7D%7B2%5Csigma%20%5E%7B2%7D%7D%7D%20%5Csum_%7Bn%7D%5E%7Bi%3D1%7D%20%28z%7B_%7Bi%7D%7D%20-%20%28a%5E%7B_%7B0%7D%7D%20&plus;%20%5Csum_%7Bm%7D%5E%7Bj%3D1%7D%20a_%7Bj%7D%20x_%7Bij%7D%29%29%5E%7B2%7D%20%5Cright%20%29)



<br />

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

<br />

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

<br />

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


## [Advanced Regression](#Advanced-Regression)

We can use trees to divide data set, and specify different models for each subset of the data. 

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
- Sensitivity is also known as True Positive Rate, and Specificity = True Negative Rate

**Confusion Matrix**

| Classification | Yes (Model) | No (Model) |
| --------------- | --------------- | --------------- |
| Yes (True)| Correct | Incorrect |
| No (True) | Incorrect| Correct |

<br />

Meaning:

| Classification | Yes (Model) | No (Model) |
| --------------- | --------------- | --------------- |
| Yes (True)| True Positive | False Negative |
| No (True) | False Positive | True Negative |

<br />

Example of an email spam filter using SVM:

| Classification | Yes (Model) | No (Model) |
| --------------- | --------------- | --------------- |
| Yes (True)| 490 (TP) | 10 (FN) |
| No (True) | 100 (FP) | 400 (TN) |

<br />

Question: 
- fraction of email expect to be spam = FP / (TP+FP) 
- fraction of real email lost = FN / (TP+FN)

We can also calculate cost of lost productivity: 
- assume: $0 for correct, $0.04 to read spam, $1 to miss a real email
- if 50% of email is spam, total cost = 490 x $0 + 400 x $0 + 10 x $1 + 100 x $0.04 = $14, or $1.4 per email
- if 40% of email is spam, total cost = 490 x (60%/50%) x $0 + 400 x (40%/50%) x $0 + 10 x (60%/50%) x $1 + 100 x (40%/50%) x $0.04 = $15.2, or $1.52 per email

<br />

**Regression**

1. Poisson Regression: 
    - use when response follows a Poisson distribution ![Poisson Dist](https://latex.codecogs.com/gif.latex?f%28z%29%20%3D%20%5Cfrac%7B%5Clambda%20%5E%7Bz%7D%20e%5E%7B-%5Clambda%20%7D%7D%7Bz%21%7D)




    - example: to count arrivals at an airport security line
    - estimate lambda (x) 


2. Regression splines:
    - function of polynomials that connect to each other
    - allow fit to different functions to different parts of the data set, which smooth connections between the parts 
    - order k regression spline: the polynomials are all order k   

3. Bayesian regression:
   - also start with some estimate of how regression coefficients & random error is distributed
   - then use Bayes' theorem to update estimate
   - most helpful when not much data

4. K-Nearest-Neighbor (KNN) regression:
   - no trying to guess function of the attributes which might be a good predictor
   - plot all the data, and predict a response by taking average response of k closest data points 
   
## [Exponential Smoothing](#Exponential-Smoothing)

Time series data can be affected by:
- trends over time e.g. stock prices
- cyclical variations e.g. annual temperature cycles, weekly sales
- randomness e.g. stock prices, blood pressure

St = expected baseline response at time period t 

xt = observed response at t 

- alpha -> 0: a lot of randomness (e.g. yesterday's baseliness is a good indicator for today, willing to trust previous estimate, St-1)
- alpha -> 1: not much randomness (e.g. today's baseliness is close to the observed data, willing to trust xt)

![Exp Smooth Eq1](https://latex.codecogs.com/gif.latex?S_%7Bt%7D%20%3D%20%5Calpha%20x_%7Bt%7D%20&plus;%20%281-%5Calpha%20%29%28S_%7Bt-1%7D%29)




Include trends at time period t (starting conditions T1= 0, shows no initial trend): 

![trend1](https://latex.codecogs.com/gif.latex?S_%7Bt%7D%20%3D%20%5Calpha%20x_%7Bt%7D%20&plus;%20%281-%5Calpha%20%29%28S_%7Bt-1%7D%20&plus;%20T_%7Bt-1%7D%29)



![trend2](https://latex.codecogs.com/gif.latex?T_%7Bt%7D%20%3D%20%5Cbeta%20%28S_%7Bt%7D%20-%20S_%7Bt-1%7D%29%20&plus;%20%281-%5Cbeta%20%29T_%7Bt-1%7D)




Include cyclic patterns:

It can be like trend, additive component OR

Seasonalities in a multiplicative way (starting condition, 1 = no initial cyclic effect)
- L: length of a cycle
- Ct: multiplicative seasonality factor for time t, inflate/deflate the observation (we use cyclic factor from L time periods ago, because that is the most recent cyclic factor from the same part of the cycle)

![cyclic1](https://latex.codecogs.com/gif.latex?S_%7Bt%7D%20%3D%20%5Cfrac%7B%20%5Calpha%20x_%7Bt%7D%7D%7BC_%7Bt-L%7D%20&plus;%20%281-%5Calpha%29%28S_%7Bt-1%7D%20&plus;%20T_%7Bt-1%7D%29%7D)
 
 

If C = 1.1 on weekend, just means sales were 10% higher because of weekend


![cyclic2](https://latex.codecogs.com/gif.latex?C_%7Bt%7D%20%3D%20%5Cgamma%20%28x_%7Bt%7D%20/%20S_%7Bt%7D%29%20&plus;%20%281-%5Cgamma%20%29C_%7Bt-L%7D)





This time series model is also known as single / double / triple exponential smoothing (depending on how many trends and seasonality include). 

Triple exponential smoothing is also called Winter's Method or Holt-Winters.

Exponential smoothing smoothes out randomness (peaks/valleys), and can also be used for forecasting. It is primarily used on the most recent data points, so it is better for short-term forecasting. 

Our guess for next time period is the same as latest baseline estimate

![forecast1](https://latex.codecogs.com/gif.latex?S_%7Bt&plus;1%7D%20%3D%20%5Calpha%20x_%7Bt&plus;1%7D%20&plus;%20%281-%5Calpha%20%29S_%7Bt%7D%20%2C%20x_%7Bt&plus;1%7D%20%5Crightarrow%20unknown%20%5Crightarrow%20S_%7Bt%7D)



When trends included, best estimate of trend = most current trend estimate

When multiplicative seasonality is included, 
![forecast2](https://latex.codecogs.com/gif.latex?F_%7Bt&plus;1%7D%20&plus;%20%28S_%7Bt%7D%20&plus;%20T_%7Bt%7D%29%20C_%7B%28t&plus;1%29-L%7D)




To optimize alpha, beta, gamma: use optimization = min(Ft - xt)^2

## [ARIMA](#ARIMA)

AutoRegressive Integrated Moving Average has 3 key parts:
1. Differences (d)
    - exponential smoothing estimates that St based on xt, xt-1 and it works well if data is stationary 
    - often data is NOT stationary, but the difference might be stationary 
2. Autoregression (p)
    - predicting current value based on previous time periods' values 
3. Moving Average (q)
    - use previous errors as predictors 

Specific values of p, d, q:
- ARIMA (0,0,0) = white noise
- ARIMA (0,1,0) = random walk
- ARIMA (p,0,0) = autoregressive model
- ARIMA (0,0,q) = moving average model
- ARIMA (0,1,1) = basic exponential smoothing model 

ARIMA works better than exponential smoothing when data is more stable with fewer peaks, valleys and outliers. We also need at least 40 data points for ARIMA to work well. 

## [GARCH](#GARCH)

Generalized Autoregressive Conditional Heteroscedasticity (GARCH) is used to estimate or forecast the variance. We need to do variance estimation because it can tell us how much the forecast might be different than the true value. 

It is important in investment e.g. traditional portfolio optimization model, where it balances the expected return of investments based on amount of volatility. 

| GARCH | ARIMA | 
| --------------- | --------------- | 
| Variances, squared errors | Observations, linear errors | 
| Raw variances | Differences in variances |

<br />



<br />
**References**

1. The R Book, by Michael J.Crawley, Published by Wiley, 2007.
2. Introduction to Analytics Modeling, by Prof.Joel Sokol.





