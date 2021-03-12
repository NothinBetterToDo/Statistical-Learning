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



![Y_3step]()





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







### References:

1. [The R Book](https://learning.oreilly.com/library/view/the-r-book/9780470510247/ch009-sec016.html)
2. Statistics for Machine Learning, by Pratap Dangeti, Published by Packt Publishing, 2017
3. Introduction to Analytics Modeling by Prof.Joel Sokol









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

