# Determining adherence and persistence

How to determine adherence and persistence to a certain drug, while taking into account stockpiling :pill:? This repository contains [code](docs/adhper.R) that you can use to easily determine the proportion of days covered and the time until discontinuation, whilst taking into account stockpiling on dispensation-to-dispensation basis. 

The code creates two functions:

```
adh(df, drug_df, yr)
per(df, drug_df, yr, gp)
```

In these functions, you can specify your drug of interest, the dataframe from which they should be pulled, the amount of years you are interested in for follow-up, and for persistence the grace period you decided on. Note that the code is data-specific, but variable names can easily be changed to your own variable names.

## Explanation of code
The two diagrams shown below give an explanation of how the code works, with on the left a text-based explanation and on the right a visual example.

### Adherence
![Adherence function](https://user-images.githubusercontent.com/98459937/151541059-15e2506c-82e6-40b5-bb66-74a5126dabc9.png)

### Persistence
![Persistence function](https://user-images.githubusercontent.com/98459937/151541075-0157e179-05ae-4d0d-a105-f8d3d28bd9e4.png)

## How to use the function
Imagine I am interested in the adherence and persistence to angiotensin-converting-enzyme inhibitors (ACEis) after initiation. I have prepared a dataframe _cohort_ with my cohort of ACEi new-users and I have prepared a dataframe _drugs_ with all dispensations for ACEis. Then, to determine the adherence and persistence (with a grace period of 30 days) in the first 12 months, I can simply run the following code:

```
adh_acei <- adh(cohort, drugs, 1)
per_acei <- adh(cohort, drugs, 1, 30)

adhper <- adh_acei %>% dplyr::left_join(per_acei, "id")
```

### Variable names
The following data-specific variable names are used in the code and mean the following:
- lopnr           =   participant ID
- drug            =   drug of interest
- index_dt        =   participant's cohort entry date
- censor_dt_cod   =   participant's censor date
- edatum          =   dispensation date
- antal           =   amount of packages dispensed
- antnum          =   amount of units (e.g., pills) per package
