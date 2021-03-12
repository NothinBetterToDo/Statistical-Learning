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

It can be used to determine how do systems work, and what will happen in the future. 

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




**AIC** 

Aikaike's information criterion (AIC) is known as a penalized log-likelihood. Adding extra parameters can lead to overfitting to fit random effects. Smallest AIC is preferred - encourages fewer parameters k, and higher likelihood.

- L*: maximum likelihood value
- k: number of parameters being estimated



![AIC](https://latex.codecogs.com/gif.latex?AIC%20%3D%202k%20-%202%20ln%20%28L%5E%7B*%7D%29)




![AIC Substitute](https://latex.codecogs.com/gif.latex?AIC%20%3D%202%28m&plus;1%29%20-%202%20ln%5Cleft%20%28%20%5Cfrac%7B1%7D%7B%5Csigma%20%5Csqrt%7B2%5Cpi%20%7D%5E%7Bn%7D%7D%20e%5E%7B-%5Cfrac%7B1%7D%7B2%5Csigma%20%5E%7B2%7D%7D%7D%20%5Csum_%7Bn%7D%5E%7Bi%3D1%7D%20%28z%7B_%7Bi%7D%7D%20-%20%28a%5E%7B_%7B0%7D%7D%20&plus;%20%5Csum_%7Bm%7D%5E%7Bj%3D1%7D%20a_%7Bj%7D%20x_%7Bij%7D%29%29%5E%7B2%7D%20%5Cright%20%29)





**Corrected AIC***

AIC has nice properties if there are infinitely manay data points to fit the model. There's a correction term we can add to AIC to deal with data where data set is not infinite.


![Corrected AIC]()







### References:

1. The R Book, by Michael J.Crawley, Published by Wiley, 2007.
2. Statistics for Machine Learning, by Pratap Dangeti, Published by Packt Publishing, 2017.
3. Introduction to Analytics Modeling by Prof.Joel Sokol.









## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/NothinBetterToDo/Analytics-Modeling/edit/main/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/NothinBetterToDo/Analytics-Modeling/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.

