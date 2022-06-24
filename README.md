# AB Testing - Project Overview
- 


## Code and Resources Used
**Python Version:** 3.9

**Packages Used:** pandas, numpy, matplotlib, random, statsmodels

## Table of Contents
- [Introduction](#intro)
- [Part I - Cleaning and Probability](#probability)
- [Part II - A/B Test](#ab_test)
- [Part III - Regression](#regression)
- [Conclusion](#should-the-new-page-replace-the-old-page)

<a id='intro'></a>
### Introduction

A/B tests are very commonly performed by data analysts and data scientists.  It is important to get some practice working with the difficulties of these.

For this project, I will be working to understand the results of an A/B test run by an e-commerce website. My goal is to work through this notebook to help the company understand if they should implement the new page, keep the old page, or perhaps run the experiment longer to make their decision.

<a id='probability'></a>
#### Part I - Cleaning and Probability

The dataset was relatively clean, but I ended up creating a new dataset to only show the rows where treatment matches with new_page and control matches with old_page for accurate results.

After simply statistical testing I would say that the new page does not lead to more conversions. The probability of an individual converted on the old page is higher than conversion rates on the new page, however the difference is small. The chance an individual recieves the new page is 50% meaning that individuals recieved an equal amount of the new page and old page. With the conversion rate being similar of 12% for the old page and 11.9% for the new page, it would seem that the different page has little to no effect on a viewer, however, this is all surface probability and I need to dig deeper to know the real answer.

<a id='ab_test'></a>
### Part II - A/B Test
**Hypothesis**:

$H_{0}$ : $p_{new}$ <= $p_{old}$

$H_{1}$ : $p_{new}$ > $p_{old}$

After stating my hypothesis, I performed a sampling distribution for the difference in **converted** between the two pages over 10,000 iterations of calculating an estimate from the null. I used Python libraries such as **pandas**, **numpy**, and **random**. The probability difference is as shown:
![image](https://user-images.githubusercontent.com/69525188/175644745-28e66b18-8569-4b57-8038-34c7779ccd20.png)

Next I calculated the p value. The p value is a number that describes the probability of obtaining test results at least as extreme as the results actually observed, under the assumption that the null hypothesis is correct. A p value below .05 usually indicates that the null hypothesis should be rejected in favore of the new hypothesis. Alternatively a p value above .05 usually idicates that the null hypothesis should be failed to reject and change nothing. Since my calculated p value is .9, it indicates that I should fail to reject my null hypothesis as the new page does not perform any better than the old page.

I also calculated the z score as 1.31. The z-score means that the difference between our test statistic (the difference between conversion rates) and the null hypothesis is 1.31 standard deviations above the mean. This is less than the critical 1.96 and suggests that the null hypothesis should be rejected. Therefore, the findings in this part coincide with the findings from calculated the p value.

<a id='regression'></a>
### Part III - A regression approach

In this section I will be looking to see if the result I achieved in the A/B test in Part II above can also be achieved by performing regression. Since I am exploring whether an event happens or not, the type of regression to be used is logistic regression. To fit my regression model I will be using **statsmodel**.

The summary of the regression model is as shown:

![image](https://user-images.githubusercontent.com/69525188/175642911-fc015fba-8010-4f1b-b376-87e772f25901.png)

**Hypothesis:**

$H_{0}$ : $p_{new}$ − $p_{old}$ = 0

$H_{1}$ : $p_{new}$ − $p_{old}$ ≠ 0

This test is two sided T-test unlike the one sided T test in part II. The p value of the ab_page is .190. Although more significant, this is still higher than the p value's level of significance of .05. Therefore, I am still inclined to fail to reject the null hypothesis as found with previous conclusions.

#### Adding in data countries' pages
To gain extra insight, I appending country data onto my original dataset to understand of webpages performed differently in other countries. After, I created another regression model where US was the intercept.

The model:

![image](https://user-images.githubusercontent.com/69525188/175644504-7347ee75-8396-4919-8e08-9b26bd51c1bc.png)

This summary statistic's conclusions are not much different than previous tests. The P value for Canada's page was .1947 which is not statistically significant as it is much higher that .05. The same is found for the UK page as the P value is .6349, a much larger number. To conclude my findings, I am still inclined to fail to reject the null hypothesis which coincide with my previous findings. I have not found substantial evidence to conclude that the new page performed better and therefore, I do not find purpose in the new page being launched.

### Should the new page replace the old page?
**No, the company should keep the old page for better performance. After statistically testing the data in several different ways, I was never able to reject the null in favor of the alternative.**
