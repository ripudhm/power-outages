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


### Bivariate Analysis


### Interesting Aggregates