---
layout: post
title: A descriptive look at Veteran unemployment
tags: veterans OpenData
---





On any given year, is the President really the one to praise (or blame) for the country's economic situation? I don't ask this in a partisan way, I simply don't understand the intricacies of [economics](https://www.npr.org/tags/146988256/u-s-economy). When employment statistics are released, they tend to vary by industry, location, and population. Not all Americans experience the same economy. Ultimately, the economy is a complex system, and statistics come with a certain level of uncertainty and manipulation.


Lets look at this statistic:

![<img src="https://iecastro.github.io/images/DOL_veterans2018.png" alt="VeteranUnempl" style="width: 400px;"/>](/images/DOL_veterans2018.png)


That is great, no doubt --but, it doesn't tell us everything. Let's look at the annual averages across the country in 2017. We can see that unemployment among Veterans differs by State. Is the economic environment in Rhode Island that much different from Vermont or Maine? Why?


```
## Error in eval(lhs, parent, parent): object 'bls_pct' not found
```

## New York Data

Let's focus on New York State. Open Data NY released numbers on the [*Employment Status of the Veteran Population*](https://data.ny.gov/Economic-Development/Employment-Status-of-the-Veteran-Population-18-Yea/xnam-chv6). This post will describe and summarize these estimates

### Veteran unemployment 

In NYS, the unemployment rate among Post-9/11 Veterans has had a downward trend
over the years. However, with the exception of 2015 & 2017, unemployment in this population is higher than in non-Veterans (and across all Veterans). 

 

```
## Error in eval(lhs, parent, parent): object 'vetdata' not found
```

*Unemployed* refers to people in the labor force who are not working but have been looking for work and are currently available to work. The labor force is comprised of all who are either employed or unemployed. The percentage of the labor force unemployed is the unemployment rate -- although, it is not really a [rate](http://sphweb.bumc.bu.edu/otlt/MPH-Modules/PH/BasicQuantitativeConcepts/BasicQuantitativeConcepts4.html), but, what do I know?

### Veteran participation rate

The labor force participation rate (again, not really a rate) of Post-9/11 Veterans hasn't dropped below 75% in almost a decade. You may have never heard of the participation rate (I hadn't until I started exploring this dataset),so to compare, in 2016 the NYS labor force participation rate was [62.8%](https://www.osc.state.ny.us/reports/economic/labor-force-trends-nys-2017.pdf) -- that is, one-third of the working age population (not in prison or active duty military) does not participate in the labor force.  The national participation rate is not any [higher](https://data.bls.gov/timeseries/LNS11300000). 



```
## Error in eval(lhs, parent, parent): object 'vetdata' not found
```

As more Veterans return home, they are still active participants in the labor force. Only one-fith of this population does not participate in the labor force; and that includes Veterans who have retired, are disabled and unable to work, or currently attending school.

### Odds of unemployment 

Although Post-911 Veterans are more active participants than non-Veterans, they have higher odds of being unemployed.



```
## Error in eval(lhs, parent, parent): object 'merged' not found
```

The odds ratio (OR) tells us the odds of being unemployed if you're a Post-9/11 Veteran compared to the odds of being unemployed if you're not a Veteran. 

In 2010, Post-9/11 Veterans were *twice as likely* as a non-Veteran to be unemployed. These odds have improved over the years, and in 2017, Post-9/11 Veterans were about 20% *less likely* to be unemployed than non-Veterans. Somthing happened in 2016, couldn't tell you what.

And interesting association in this dataset is that Gulf War Veterans have better odds than Post-9/11 Veterans.  They actually tend to have better odds than non-Veterans. 



```
## Error in ggplot(merged, aes(as.factor(Year), oddsratio, color = Group)): object 'merged' not found
```

### Limitations

These associations are limited to the data available, so it is not possible to assess if these odds are affected by other variables, such as demographics, educational level, or technical skills.

*It's important to note these data are not official BLS estimates, and have limitations regarding how they were sampled and calculated.*

The NYS Department of Labor derived annual averages from [Current Population Survey](https://www.bls.gov/cps/documentation.htm) (CPS) sample records. CPS is a national, monthly, household survey, with about 2,300 households interviewed in NYS each month.

To calculate odds ratios for 2015 and 2017, the number unemployed was imputed by subtracting the number employed from the labor force count.

