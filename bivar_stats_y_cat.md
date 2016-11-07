# Bivariate Statistics for categerical outcomes

## Purpose
This function will produce a summary of how each variable varies with a _categorical_ outcome variable. This will help the user to flag associations between the independent variables and outcome variable that may not be compatible with the subsequent modelling approach.

## Dependancies
`read_and_transform`

## Name
`bivar_stats_y_cat`

## Inputs
* `transformed_data`
  * R dataset output by `read_and_transform`
* `output_dir`
  * The directory into which all outputs will be output to.
* `outcome`
  * The variable to use as an outcome.

## Function
* Output a warning if the outcome variable has more than 5 levels.
  * More than 5 levels will make the resulting spreadsheets very difficult to digest, so the user needs to be warned about this.
* For columns prefixed with "o_", no stats should be calculated.
* Each statistic mentioned below ends in "_\__X_". This means that it should be calculated for each level of the outcome variable, and the name of the stat should be suffixed with that level value. E.g. if the outcome variable has 2 levels, "1" and "0", the stat _Count__X_ should have 2 columns in the output CSV, "Count_1" and "Count_0", calculated for all observations where the outcome variable has level 1 and 0 respectively.
* For categorical variables (except the outcome variable itself), produce `bivar_stats_y_cat_x_cat.csv`. This is a full frequency table containing all levels for all variables with the following columns:
  * _Variable_: Name of the categorical variable.
  * _Level_: The value of the level in that variable.
    * Each variable should the following 2 special levels:
      * First is a level called "non_missing". This row will contain aggregated stats on all the non-missing levels in that variable.
      * Second is a level called "missing". This row will contains stats on all the missing observations for that variable.
  * _Count__X_: Count of observations which have this variable equal to this level when outcome level is X.
  * _Percentage__X_: Percentage of observations which have this variable equal to this level when outcome level is X.
    * _Percentage__X_ = _Count__X_ / all observations where level is X.
* For numerical variables, produce `bivar_stats_y_cat_x_num.csv` with following columns:
  * _Variable_: Name of the categorical variable.
  * _NonMissing__X_: Number of non-missing obsservations when outcome level is X.
  * _NonMissingPerc__X_: Percentage of non-missing observations when outcome level is X.
  * _Missing__X_: Number of missing observations when outcome level is X.
  * _MissingPerc__X_: Percentage of missing observations when outcome level is X.
  * _Mean__X_: Mean of the variable when outcome level is X.
  * _SD__X_: Standard deviation of the variable when outcome level is X.
  * _Min__X_: Minimum value of the variable when outcome level is X.
  * _Max__X_: Maximum value of the variable when outcome level is X.
  * _P1__X_: Value at the percentile 1 of the variable when outcome level is X.
  * _P5__X_: Value at the percentile 5 of the variable when outcome level is X.
  * _P10__X_: Value at the percentile 10 of the variable when outcome level is X.
  * _P25__X_: Value at the percentile 25 of the variable when outcome level is X.
  * _P50__X_: Value at the percentile 50 of the variable when outcome level is X.
  * _P75__X_: Value at the percentile 75 of the variable when outcome level is X.
  * _P90__X_: Value at the percentile 90 of the variable when outcome level is X.
  * _P95__X_: Value at the percentile 95 of the variable when outcome level is X.
  * _P99__X_: Value at the percentile 99 of the variable when outcome level is X.

## Output
All CSVs below should be output to the `output_dir`, overwriting a previous version if necessary.
* bivar_stats_y_cat_x_cat.csv
* bivar_stats_y_cat_x_num.csv

## Defaults
```
bivariate_stats(
  transformed_data = transformed_data,
  output_dir = <test output directory>,
  outcome = gear
  )  
```
## Tests