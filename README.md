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