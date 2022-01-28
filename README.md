# Determining adherence and persistence

How to determine adherence and persistence to a certain drug, while taking into account stockpiling :pill:? This repository contains [code](./adhper.R) that you can use to easily determine the proportion of days covered and the time until discontinuation, whilst taking into account stockpiling on dispensation-to-dispensation basis. 

The code creates two functions:

```
adh(df, drug_df, yr)
per(df, drug_df, yr, gp)
```

In these functions, you can specify your drug of interest, the dataframe from which they should be pulled, the amount of years you are interested in for follow-up, and for persistence the grace period you decided on. Note that the code is data-specific, but variable names can easily be changed to your own variable names.

## Explanation of code
The two diagrams shown below give an explanation of how the code works, with on the left a text-based explanation and on the right a visual example.

### Adherence
![Adherence function](https://user-images.githubusercontent.com/98459937/151542077-05bb2359-f661-470a-b5b1-330181156503.png)

### Persistence
![Persistence function](https://user-images.githubusercontent.com/98459937/151542115-3e4e59f5-243c-4094-a7eb-8ce6ac6db084.png)

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
