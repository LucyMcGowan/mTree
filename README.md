
<!-- README.md is generated from README.Rmd. Please edit that file -->

# mTree

<!-- badges: start -->
<!-- badges: end -->

The goal of mTree is to discover heterogeneous treatment effect
subgroups in clinical trials and observational studies that are balanced
on important variables.

## Installation

You can install the development version of mTree from
[GitHub](https://github.com/) with:

``` r
# install.packages("pak")
pak::pak("joerigdon/mTree")
```

## Example

Here is an example of simulated data from Rigdon, J., Baiocchi, M. &
Basu, S. Preventing false discovery of heterogeneous treatment effect
subgroups in randomized trials. Trials 19, 382 (2018).
<https://doi.org/10.1186/s13063-018-2774-5>.

``` r
library(mTree)

covariates <- c("age", "black", "sbp", "dbp", "scr", "eGFR", "statin",
                 "aspirin", "fram", "smok")
# get filtered matches (performs pair matching and removes any matches that 
# don't exactly match on categorical variables)
matched_data <- get_filtered_matches(
  data = example_trial_hte_data,
  treatment = "Z",
  covariates = covariates,
  id = "UNIQID"
)

# get average covariates 
avg_matched_data <- get_averaged_matches(
  matched_data,
  treatment = "Z",
  outcome = "Y",
  covariates = covariates
)

# get tree
tree <- get_mtree(avg_matched_data, covariates)

plot(tree)
```

<img src="man/figures/README-example-1.png" width="100%" />
