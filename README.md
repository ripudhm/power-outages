# Is climate an important characteristic of major power outages in the United States?

## Ripudh Mylapur

This website goes over the analysis of major power outages in the United States. The data set used in the analysis that follows can be found *[here.](https://engineering.purdue.edu/LASCI/research-data/outages/outagerisks)*
This data set not only has data anout the major outages but also electricity consumption and price data, demogrpahic data, land and water use data and also climate data. This data is important because it can be used to find out about the salient characteristicxs of power outages and hence make educated predictions on where and when they could occur. This report will focus on answering the question "Is climate an important characteristic of major power outages in the United States?". This question focuses down on one important characteristic that might affect power outages. If climate turns out to be a an important characteristic that affects power outages this could have widespread effects in the future due to global warming. The dataset has 1534 rows and 57 columns in total. However, in this analysis only some of the columns will be of importance. Those are: 
- YEAR: Indicates the year when the outage event occurred
- MONTH: Indicates the month when the outage event occurred
- U.S._STATE: Represents all the states in the continental U.S.
- POSTAL.CODE: Represents the postal code of the U.S. states
- CLIMATE.REGION: U.S. Climate regions as specified by National Centers for Environmental Information (nine climatically consistent regions in continental U.S.A.)
- CLIMATE.CATEGORY: This represents the climate episodes corresponding to the years. The categories "Warm", "Cold" or "Normal" episodes of the climate are based on a threshold of *$\text{\plusminus}$* 0.5 *^O^* C for the Oceanic Nino Index (ONI)
- PC.REALGSP.STATE: Per capita real gross state product (GSP) in the U.S. state (measured in 2009 chained U.S. dollars)
- PC.REALGSP.REL: Relative per capita real GSP as compared to the total per capita real GDP of the U.S. (expressed as fraction of per capita State real GDP & per capita US real GDP)
- POPULATION: Population in the U.S. state in a year
- CUSTOMERS.AFFECTED: Number of customers affected by the power outage event
- OUTAGE.START: Indicates when the outage event started
- OUTAGE.RESTORATION: Indicates when power was restored to all the customers
- 'OUTAGE.DURATION: Duration of outage events (in minutes)
- CAUSE.CATEGORY: Categories of all the events causing the major power outages


There are 3 parts to this report: 
1. Exploratory Data Analysis
2. Assessment of Missingness
3. Permutation Testing

## Exploratory Data Analysis

### Data Cleaning
After looking at the data extensively there was no data that I had to replace with NaN values since all of the missing values were already NaN. However, I still had to do some other data cleaning. The original dataset had the OUTAGE.START.DATE and OUTAGE.START.TIME as two distinct columns which is unnecessary and hard to work with since they were object dtypes in pandas. There being two columns for this data in some ways makes sense since it is likely that the Data Generating Process probably had 2 field for collecting information, one field for the date and another for the time. To make it easier to work with I combined the two columns into one OUTAGE.START column whose dtype is pd.datetime. OUTAGE.RESTORATION was also made in the same way since that was also in two columns. Using the start and end times for each outage it was now possible to cross check the OUTAGE.DURATION column in the original dataset. There were also missing values in the OUTAGE.DURATION column that could have been filled out using the start and end times, but it turns out that this was not possible due to OUTAGE.RESTORATION itself having missing values. At the end of the Data Cleaning process, this was what the data framce looked like: 

|   YEAR |   MONTH | U.S._STATE   | POSTAL.CODE   | CLIMATE.REGION     | CLIMATE.CATEGORY   |   PC.REALGSP.STATE |   PC.REALGSP.REL |   POPULATION | OUTAGE.START        | OUTAGE.RESTORATION   |   OUTAGE.DURATION | CAUSE.CATEGORY     |
|-------:|--------:|:-------------|:--------------|:-------------------|:-------------------|-------------------:|-----------------:|-------------:|:--------------------|:---------------------|------------------:|:-------------------|
|   2011 |       7 | Minnesota    | MN            | East North Central | normal             |              51268 |          1.07738 |  5.34812e+06 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00  |              3060 | severe weather     |
|   2014 |       5 | Minnesota    | MN            | East North Central | normal             |              53499 |          1.08979 |  5.45712e+06 | 2014-05-11 18:38:00 | 2014-05-11 18:39:00  |                 1 | intentional attack |
|   2010 |      10 | Minnesota    | MN            | East North Central | cold               |              50447 |          1.06683 |  5.3109e+06  | 2010-10-26 20:00:00 | 2010-10-28 22:00:00  |              3000 | severe weather     |
|   2012 |       6 | Minnesota    | MN            | East North Central | normal             |              51598 |          1.07148 |  5.38044e+06 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00  |              2550 | severe weather     |
|   2015 |       7 | Minnesota    | MN            | East North Central | warm               |              54431 |          1.09203 |  5.48959e+06 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00  |              1740 | severe weather     |



### Univariate Analysis

<iframe src="assets/folium_map.html" width=800 height=600 frameBorder=0></iframe>
The above map shows the number of major outages in the US by state. Notably, California seems to have a very high number of major power outages compared to other states. 

### Bivariate Analysis

<iframe src="assets/month_count.html" width=800 height=600 frameBorder=0></iframe>
This graph shows the number of major power outages by month in the US. There seems to be significant seasonal variation in the number of majoe power outages since there are a lot more in the June compared to December. 

<iframe src="assets/causes_by_month.html" width=800 height=600 frameBorder=0></iframe>
To investigate further into these seasonal variations the cause was added to the graph. This shows that the only cause to significantly vary across the months is severe weather. 

### Interesting Aggregates

| CLIMATE.CATEGORY   |    mean |   count |
|:-------------------|--------:|--------:|
| cold               | 2656.96 |     463 |
| normal             | 2530.98 |     730 |
| warm               | 2817.32 |     283 |

This was one of the most interesting aggregates fromt he data set, showing the mean outage duration for cold, normal and warm climate places. The average outage duration for warm places seems to be higher than that of cold and normal climate places. 

## Assessment of Missingness

### NMAR Analysis

The column for CUSTOMERS.AFFECTED could be NMAR (Not Missing At Random) in this dataset. While it could be the case that the company that had the major outage is not able to find the exact number of customers that were affected due to the incident, it is likely that they do not want such kind of information to be public even if they do have access to the data. If people found out that millions of customers lost power this could have a negative impact of the percieved brand of the company and their present and future customers might look for alternatives. Hence, if the number of customers affected is a very large number the company might be incentivised to not make such information public in order to protect its interests. 

### Missingness Dependency


The missingness dependency was tested using permutations tests. The OUTAGE.DURATION column was chosen to test on. 



| variable           |   p_value |   observed_statistic |\n|:-------------------|----------:|---------------------:|\n| YEAR               |     1     |             0.659477 |\n| U.S._STATE         |     1     |             0.470204 |\n| POSTAL.CODE        |     1     |             0.470204 |\n| CLIMATE.REGION     |     1     |             0.317388 |\n| CLIMATE.CATEGORY   |     1     |             0.31847  |\n| PC.REALGSP.STATE   |     0.982 |             0.781511 |\n| PC.REALGSP.REL     |     0.986 |             0.781511 |\n| POPULATION         |     0.966 |             0.771984 |\n| CUSTOMERS.AFFECTED |     0.988 |             0.656115 |\n| OUTAGE.START       |     0.218 |             0.509527 |\n| OUTAGE.RESTORATION |     0.043 |             0.5      |\n| CAUSE.CATEGORY     |     0.998 |             0.266799 |

The permutation test was run for all the variables in the dataset and the above table was the result for each of them. The missingness in the OUTAGE.DURATION columns is not dependent on most variables. For example, the YEAR column with a p-value of 1 seems to be independent of the missingness of the OUTAGE.DURATION column. The only column that is dependent seems to be the OUTAGE.RESTORATION column. This makes sense since the OUTAGE.DURATION column has missing values when the OUTAGE.RESTORATION column has missing values. 

<iframe src="assets/YEAR_missing.html" width=800 height=600 frameBorder=0></iframe>
The above plot shows the distribution of the YEAR variables when the OUTAGE.DURATION vales are missing and not missing. 

## Permutation Testing

As indicated in the title of the report, a permutation test will be conducted in order to answer the question **"Is climate an important characteristic of major power outages in the United States?"** 

- Null hypothesis: The climate and outage duration are not related - the high average outage duration of warm climate places is due to chance alone.

- Alternative hypothesis: The climate and outage duration are related - the high average outage duration of warm climate places is not due to chance alone. 

- Test statistic: The average outage duration was used as the test statistic here to keep the analysis straightforward and interpretable. 

- Significance level: A significance level of 5% was chosen.

- P-value: The p-value obtained from the permutation test was 0.72. 

- Conclusion: Since this p-value is greater than the significance level of 0.05, we fail to reject the null hypothesis and conclude that the average outage duration of warm places seems to have come from the same distribution as that of the outage duration of all major power outages in the dataset. 

<iframe src="assets/emp_dist_perm.html" width=800 height=600 frameBorder=0></iframe>
Finally, the above graph shows the empirical distribution of the average outaeg duration. The red line indicated the observed statistic and as can be seen in the graph the observed statistic appears to be a fairly common value in the distribution. 