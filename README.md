## Determining adherence and persistence

How to determine adherence and persistence to a certain drug, while taking into account stockpiling :pill:? This repository contains code that you can use to easily determine the proportion of days covered and the time until discontinuation, whilst taking into account stockpiling on dispensation-to-dispensation basis. 

The code creates two functions:

```
adh(drug, drug_df, yr)
per(drug, drug_df, yr, gp)
```

In these functions, you can specify your drug of interest, the dataframe from which they should be pulled, the amount of years you are interested in for follow-up, and for persistence the grace period you decided on. Note that the code is data-specific, but variable names can easily be changed to your own data.
