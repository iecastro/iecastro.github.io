---
layout: post
title: Exploring diabetes indicators across the US
tags: sf rspatial
---


### First Post

This material is from a learning project. I wanted to learn some rmarkdown and how to work with the [sf package](https://github.com/r-spatial/sf) and ggplot2's geom_sf().  It is not a polished write up (or analysis) but it's a good first post to help me set up a workflow for posting to this site. All the R code can be found on [GitHub](https://github.com/iecastro/ND-and-Diabetes).



## County level deprivation index

Details about the index can be found [here](https://github.com/iecastro/deprivation-index). In short, estimates are collected from the American Community Survey and a principal component analysis extracts a deprivation score for each observation. Higher index scores represent higher area deprivation relative to all other counties in the US. 

For this project, the index was calculated using 5-year ACS estimates from 2013, at the county-level, to link to the available diabetes dataset.   






![plot of chunk unnamed-chunk-3](https://iecastro.github.io/figures/2018-9-13-first-post-unnamed-chunk-3-1.png)

## Diabetes Indicators

National data on diabetes indciators are available from the [CDC](https://www.cdc.gov/diabetes/data/countydata/countydataindicators.html). Indicator estimates are the most up to date as of 2013 and available at the county-level only. Indicators (age-adjusted) are: 1. prevalence of diagnosed diabetes, 2. prevalence of obesity, and 3. prevalence of leisure-time physical inactivity, hereafter just inactivity.

The spatial distribution of diabetes prevalence in 2013 (below) parallels that of 2007, which led to the recognition of a ["diabetes belt"](https://www.scientificamerican.com/article/diabetes-belt/,https://www.ncbi.nlm.nih.gov/pubmed/21406277) in the southern United States.   




![plot of chunk unnamed-chunk-5](https://iecastro.github.io/figures/2018-9-13-first-post-unnamed-chunk-5-1.png)

## Data Analysis

Obesity and physical inactivity are well-known risk factors for developing diabetes.  Therefore, in order to assess whether area deprivation is associated with diabetes prevalence, independent of obesity and inactivity, a blocked multiple regression was fitted.  First we estimated the effects of obesity and inactivity; then, the deprivation variable was introduced.



### Regression results



```r
library(stargazer, quietly = TRUE)

stargazer(lm1,lm2, type ="html")
```


<table style="text-align:center"><tr><td colspan="3" style="border-bottom: 1px solid black"></td></tr><tr><td style="text-align:left"></td><td colspan="2"><em>Dependent variable:</em></td></tr>
<tr><td></td><td colspan="2" style="border-bottom: 1px solid black"></td></tr>
<tr><td style="text-align:left"></td><td colspan="2">DiabPrev</td></tr>
<tr><td style="text-align:left"></td><td>(1)</td><td>(2)</td></tr>
<tr><td colspan="3" style="border-bottom: 1px solid black"></td></tr><tr><td style="text-align:left">ObPrev</td><td>0.188<sup>***</sup></td><td>0.165<sup>***</sup></td></tr>
<tr><td style="text-align:left"></td><td>(0.008)</td><td>(0.007)</td></tr>
<tr><td style="text-align:left"></td><td></td><td></td></tr>
<tr><td style="text-align:left">InactPrev</td><td>0.192<sup>***</sup></td><td>0.132<sup>***</sup></td></tr>
<tr><td style="text-align:left"></td><td>(0.007)</td><td>(0.007)</td></tr>
<tr><td style="text-align:left"></td><td></td><td></td></tr>
<tr><td style="text-align:left">PC1</td><td></td><td>0.740<sup>***</sup></td></tr>
<tr><td style="text-align:left"></td><td></td><td>(0.031)</td></tr>
<tr><td style="text-align:left"></td><td></td><td></td></tr>
<tr><td style="text-align:left">Constant</td><td>-0.912<sup>***</sup></td><td>1.311<sup>***</sup></td></tr>
<tr><td style="text-align:left"></td><td>(0.166)</td><td>(0.180)</td></tr>
<tr><td style="text-align:left"></td><td></td><td></td></tr>
<tr><td colspan="3" style="border-bottom: 1px solid black"></td></tr><tr><td style="text-align:left">Observations</td><td>3,142</td><td>3,142</td></tr>
<tr><td style="text-align:left">R<sup>2</sup></td><td>0.601</td><td>0.661</td></tr>
<tr><td style="text-align:left">Adjusted R<sup>2</sup></td><td>0.600</td><td>0.660</td></tr>
<tr><td style="text-align:left">Residual Std. Error</td><td>1.383 (df = 3139)</td><td>1.275 (df = 3138)</td></tr>
<tr><td style="text-align:left">F Statistic</td><td>2,361.260<sup>***</sup> (df = 2; 3139)</td><td>2,035.008<sup>***</sup> (df = 3; 3138)</td></tr>
<tr><td colspan="3" style="border-bottom: 1px solid black"></td></tr><tr><td style="text-align:left"><em>Note:</em></td><td colspan="2" style="text-align:right"><sup>*</sup>p<0.1; <sup>**</sup>p<0.05; <sup>***</sup>p<0.01</td></tr>
</table>


### Increases in county-level deprivation predict increases in diabetes prevalence.

![plot of chunk unnamed-chunk-7](https://iecastro.github.io/figures/2018-9-13-first-post-unnamed-chunk-7-1.png)



![plot of chunk unnamed-chunk-8](https://iecastro.github.io/figures/2018-9-13-first-post-unnamed-chunk-8-1.png)

### Interaction Term

Results summary 


```
## MODEL INFO:
## Observations: 3142 (79 missing obs. deleted)
## Dependent Variable: DiabPrev
## Type: OLS linear regression 
## 
## MODEL FIT:
## F(4,3137) = 1668.00, p = 0.00
## R² = 0.68
## Adj. R² = 0.68 
## 
## Standard errors: OLS
##             Est. S.E. t val.    p    
## (Intercept) 9.50 0.02 400.02 0.00 ***
## InactPrev   0.14 0.01  19.71 0.00 ***
## ObPrev      0.16 0.01  22.99 0.00 ***
## PC1         0.68 0.03  22.08 0.00 ***
## ObPrev:PC1  0.06 0.00  13.90 0.00 ***
## 
## Continuous predictors are mean-centered.
```


![plot of chunk unnamed-chunk-10](https://iecastro.github.io/figures/2018-9-13-first-post-unnamed-chunk-10-1.png)


## Spatial Auto-correlation of county prevalence


```
## 
## 	Moran I test under randomisation
## 
## data:  MapSP$diabetes  
## weights: nb2listw(neighbors) 
## omitted: 1543, 3118   
## 
## Moran I statistic standard deviate = 67.205, p-value < 2.2e-16
## alternative hypothesis: greater
## sample estimates:
## Moran I statistic       Expectation          Variance 
##      0.6962110037     -0.0003185728      0.0001074177
```


```r
MapSP$diabetes <- ifelse(is.na(MapSP$diabetes), 0, MapSP$diabetes)
moran.plot(MapSP$diabetes,nb2listw(neighbors), zero.policy = FALSE, 
           labels = FALSE,main=c(" "),
           xlab="Diabetes Prevalence",ylab = "Spatially Lagged Diabetes Prevalence")
```

![plot of chunk unnamed-chunk-12](https://iecastro.github.io/figures/2018-9-13-first-post-unnamed-chunk-12-1.png)


