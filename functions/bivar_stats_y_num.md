# Bivariate Statistics for numerical outcomes

## Purpose
This function will produce a summary of how each variable varies with a _numerical_ outcome variable. This will help the user to flag associations between the independent variables and outcome variable that may not be compatible with the subsequent modelling approach.

## Internal Dependancies
`read_transform`

## Name
`bivar_stats_y_num`

## Parameters
* `input`
  * R data frame output by `read_transform`
* `var_config`
  * Full path and name of the CSV containing the variable configuration.
  * Example file is [here](../example_metadata_files/var_config.csv)
* `prefix`
  * Name of the output file(s). This might need to be postfixed with function specific names, see Output section.
* `output_dir`
  * The directory into which all outputs will be written to.
* `outcome_var`
  * The variable to use as an outcome.

## Function
* Output a warning if the outcome variable has less than 5 unique values.
  * This is because the statistics in this function will not be meaningful and it would be better to run `bivar_stats_y_cat`.
* For categorical variables (variable definition located in `var_config`), produce `prefix`bivar_stats_y_num_x_cat.csv where the statistics for each categorical variable spans a group of rows and each row within the group represents a level of the categorical variable. The statistics will be calculated ignoring missing values. The results should be round to two decimal places. The output file will have the following columns:
  * _Variable_: Name of the categorical variable.
  * _Level_: The value of the level in that variable.
  * _Mean outcome_: mean of the outcome variable when the categorical variable is level X.
  * _SD outcome_: the standard deviation of the outcome variable when the categorical variable is level X.
  * _Min outcome_: Minimum value of the variable when outcome level is X.
  * _P1 outcome_: Value at the percentile 1 of the outcome variable when categorical variable level is X.
  * _P5 outcome_: Value at the percentile 5 of the outcome variable when categorical variable level is X.
  * _P10 outcome_: Value at the percentile 10 of the outcome variable when categorical variable level is X.
  * _P25 outcome_: Value at the percentile 25 of the outcome variable when categorical variable level is X.
  * _P50 outcome_: Value at the percentile 50 of the outcome variable when categorical variable level is X.
  * _P75 outcome_: Value at the percentile 75 of the outcome variable when categorical variable level is X.
  * _P90 outcome_: Value at the percentile 90 of the outcome variable when categorical variable level is X.
  * _P95 outcome_: Value at the percentile 95 of the outcome variable when categorical variable level is X.
  * _P99 outcome_: Value at the percentile 99 of the outcome variable when categorical variable level is X.
  * _Max outcome_ : Maximum value of the outcome variable when categorical variable level is X.

* For categorical variables produce `prefix`RR_stats_y_num_x_cat.csv which contains stats on the relative risk where the statistics for each categorical variable spans a group of rows and each row within the group represents a level of the categorical variable. The results should be rounded to two decimal places. The output should have the following columns:
  * _Variable_: Name of the categorical variable.
  * _Level_: The value of the level in that variable.
  * _Relative risk_: This is the mean of the outcome variable when the categorical variable is equal to this level, divided by the mean of the outcome variable for when the categorical variable is equal to the _1st_ level.
    * The _1st_ level is defined as the first one when all level values are sorted alphabetically, or numerically by the first word in the level value. The first word in the following level value: "20 - 40", is "20".
    * The _1st_ level will be assumed to the baseline level and all other levels (including the first level) will be considered relative to this baseline.

* For numerical variables produce the following statistics where deciles are computed by mass (as opposed to by range) in `prefix`bivar_stats_y_num_x_num.csv where each row represents a single numerical variable.  The statistics will be calculated ignoring missing values. The output file will have the following columns:
  * _Variable_: Name of the numerical variable.
  * _Pearson's correlation coefficient_: Pearson's correlation coefficient measuring the association between the numerical variable and the outcome variable. The result should be rounded to two decimal places.
  * _P-value of Pearson's correlation coefficient_: The p-value for Pearson's correlation coefficient measuring the association between the numerical variable and the outcome variable. The result should be rounded to five decimal places.
  * _Spearman's correlation coefficient_: Spearman's correlation coefficient measuring the association between the numerical variable and the outcome variable. The result should be rounded to two decimal places.
  * _P-value of Spearman's correlation coefficient_: The p-value for Spearman's correlation coefficient measuring the association between the numerical variable and the outcome variable. The result should be rounded to five decimal places.
  * _Mean outcome in 1st decile_: the mean of the outcome variable for the observations where the numerical variable is >= minimum value of the numerical variable and < the value of the 1st decile of the numerical variable. The result should be rounded to two decimal places.
  * _Mean outcome in 2nd decile_: the mean of the outcome variable for the observations where the numerical variable is >= the value of the 1st decile of the numerical variable  and < the value of the 2nd decile of the numerical variable. The result should be rounded to two decimal places.
  * _Mean outcome in 3rd decile_: the mean of the outcome variable for the observations where the numerical variable is >= the value of the 2nd decile of the numerical variable  and < the value of the 3rd decile of the numerical variable. The result should be rounded to two decimal places.
  * _Mean outcome in 4th decile_: the mean of the outcome variable for the observations where the numerical variable is >= the value of the 3rd decile of the numerical variable  and < the value of the 4th decile of the numerical variable. The result should be rounded to two decimal places.
  * _Mean outcome in 5th decile_: the mean of the outcome variable for the observations where the numerical variable is >= the value of the 4th decile of the numerical variable  and < the value of the 5th decile of the numerical variable. The result should be rounded to two decimal places.
  * _Mean outcome in 6th decile_: the mean of the outcome variable for the observations where the numerical variable is >= the value of the 5th decile of the numerical variable  and < the value of the 6th decile of the numerical variable. The result should be rounded to two decimal places.
  * _Mean outcome in 7th decile_: the mean of the outcome variable for the observations where the numerical variable is >= the value of the 6th decile of the numerical variable  and < the value of the 7th decile of the numerical variable. The result should be rounded to two decimal places.
  * _Mean outcome in 8th decile_: the mean of the outcome variable for the observations where the numerical variable is >= the value of the 7th decile of the numerical variable  and < the value of the 8th decile of the numerical variable. The result should be rounded to two decimal places.
  * _Mean outcome in 9th decile_: the mean of the outcome variable for the observations where the numerical variable is >= the value of the 8th decile of the numerical variable  and < the value of the 9th decile of the numerical variable. The result should be rounded to two decimal places.
  * _Mean outcome in 10th decile_:  the mean of the outcome variable for the observations where the numerical variable is >= the value of the 9th decile of the numerical variable  and <= the maximum value numerical variable. The result should be rounded to two decimal places.

## Output
All CSVs below should be output to the `output_dir`, overwriting a previous version if necessary.
* `prefix`bivar_stats_y_num_x_cat.csv
* `prefix`RR_stats_y_num_x_cat.csv
* `prefix`bivar_stats_y_num_x_num.csv

## Return
List containing these data frames:
* bivar_stats_y_num_x_cat
* bivar_stats_y_num_x_num
* RR_stats_y_num_x_cat

## Defaults
```
bivar_stats_y_num(
  input=,
  var_config=,
  prefix='',
  output_dir=,
  outcome=
  )  
```

## Example call
```
cars_bivar_num <- bivar_stats_y_cat(
  input=cars$data,
  var_config=var_config,
  output="cars",
  output_dir="D:/data/cars1/",
  outcome = "gear"
  )
```

## Tests
* All outputs should have the correct format and structure as specified.
* Using the provided toy example for [input](./example_data/mtcars.csv): all outputs should exactly match the provided examples for the results [bivar_stats_y_num_x_cat](./example_output_csvs/bivar_stats_y_num_x_cat.csv);
[bivar_stats_y_num_x_num](./example_output_csvs/bivar_stats_y_num_x_num.csv);
[rr_stats_y_num_x_cat](./example_output_csvs/rr_stats_y_num_x_cat.csv).
