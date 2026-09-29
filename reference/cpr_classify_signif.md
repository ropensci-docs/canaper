# Classify statistical significance

Given the results of
[`cpr_rand_test()`](https://docs.ropensci.org/canaper/reference/cpr_rand_test.md),
classifies statistical significance of a biodiversity metric. The null
hypothesis is that observed value does not lie in the extreme of the
random values.

## Usage

``` r
cpr_classify_signif(df, metric, one_sided = FALSE, upper = FALSE)
```

## Arguments

- df:

  Input data frame.

- metric:

  Character vector of length 1; selected metric to classify
  significance. May choose from `pd` (phylogenetic diversity), `rpd`
  (relative phylogenetic diversity), `pe` (phylogenetic endemism), `rpe`
  (relative phylogenetic endemism) (case-sensitive).

- one_sided:

  Logical vector of length 1; is the null hypothesis one-sided? If
  `TRUE`, values will be classified as significant if they are in
  **either** the top 5% **or** bottom 5%. If `FALSE`, values will be
  classified as significant if they are in the top 2.5% or bottom 2.5%,
  combined.

- upper:

  Logical vector of length 1; only applies if `one_sided` is `TRUE`. If
  `TRUE`, values in the top 5% will be classified as significant. If
  `FALSE`, values in the bottom 5% will be classified as significant.

## Value

Object of class data.frame with column added for statistical
significance of the selected metric. The new column name is the name of
the metric with `_signif` appended. The new column is a character that
may contain the following values, depending on the null hypothesis:

- `< 0.01`, `< 0.025`, `> 0.975`, `> 0.99`, `not significant`
  (two-sided)

- `< 0.01`, `< 0.05`, `> 0.99`, `> 0.95`, `not significant` (one-sided)

## Details

For metrics like `pe`, you probably want to consider a one-sided
hypothesis testing values in the upper extreme (i.e., we are interested
in areas that have higher than expected endemism). For this, you would
set `one_sided = TRUE, upper = TRUE`. For metrics like `pd`, you
probably want to consider a two-sided hypothesis (i.e., we are
interested in areas that are either more diverse or less than diverse
than expected at random). For this, set `one_sided = FALSE`.

## Examples

``` r
# \donttest{
set.seed(12345)
data(phylocom)
rand_test <- cpr_rand_test(
  phylocom$comm, phylocom$phy,
  null_model = "curveball", metrics = "pd", n_reps = 50
)
#> Warning: Abundance data detected. Results will be the same as if using presence/absence data (no abundance weighting is used).
#> Warning: Dropping tips from the tree because they are not present in the community data: 
#>  sp16, sp23, sp27, sp28, sp30, sp31, sp32
cpr_classify_signif(rand_test, "pd")
#>            pd_obs pd_rand_mean pd_rand_sd  pd_obs_z pd_obs_c_upper
#> clump1  0.3018868    0.4649057 0.03446764 -4.729621              0
#> clump2a 0.3207547    0.4664151 0.03831667 -3.801488              0
#> clump2b 0.3396226    0.4686792 0.03542398 -3.643198              0
#> clump4  0.4150943    0.4645283 0.03364201 -1.469412              2
#> even    0.5660377    0.4656604 0.02987904  3.359457             50
#> random  0.5094340    0.4716981 0.03073249  1.227881             44
#>         pd_obs_c_lower pd_obs_q pd_obs_p_upper pd_obs_p_lower       pd_signif
#> clump1              50       50           0.00           1.00          < 0.01
#> clump2a             50       50           0.00           1.00          < 0.01
#> clump2b             50       50           0.00           1.00          < 0.01
#> clump4              44       50           0.04           0.88 not significant
#> even                 0       50           1.00           0.00          > 0.99
#> random               2       50           0.88           0.04 not significant
# }
```
