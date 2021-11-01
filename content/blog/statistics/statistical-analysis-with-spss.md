---
title: "Statistical Analysis With SPSS"
date: 2021-10-30T17:06:57+06:00
featureImage: images/blog/tutorials/statistics/spss/feature-small.png
postImage: images/blog/tutorials/statistics/spss/feature-large.png
---

[SPSS](https://www.ibm.com/products/spss-statistics) is one of the leading tools for statistical analysis. Here we shall learn some of the methods of doing common statistical analysis with SPSS.

### How To Do Fisher Exact Test in SPSS
[//]: # (#### Use cases)
<!-- #### Use cases -->
#### Data type
- Two categorical variables.

#### Steps
- Click `Analyze` -> `Descriptive Statistics` ->  `Crosstabs...`
- Drag and drop (at least) one variable into the `Row(s)` and one in `Column(s)` box.
- Click on `Exact`, and then select `Exact` bullet option. Leave the `Time limit per test` as it is, and then click `Continue`.
- Click `Statistics`, then select `Chi-square`, and then click `Continue`.
- To run the test, click `OK`.
- The result will be displayed in the SPSS output viewer.

#### Result
- The value of **Fisher's Exact Test** and **Exact Sig. (2-sided)** (***p value***) will be displayed in the **Chi-Square Tests** table.


### How To Do Poisson Regression Analysis Using SPSS
#### Steps
- Click `Analyze` > `Generalized Linear Models` > `Generalized Linear Models...`.
- In the **Type of Model** tab, select `Poisson loglinear` radio option.

<img src="/images/blog/tutorials/statistics/spss/poisson-regression-analysis-window.png" alt="Poisson Regression Analysis" caption="Poisson Regression Analysis" width="100%">

- In the **Response** tab, give your `Dependant Variable`.
- In the **Predictors** tab, give your `Factors` and `Covariates`.
- In the **Model** tab, add your items in the `Model`.
- In the **Statistics** tab, select `Include exponential parameter estimates`.
- Then click `OK`.