# Run a randomization analysis for one or more biodiversity metrics

The observed value of the biodiversity metric(s) will be calculated for
the input community data, then compared against a set of random
communities. Various statistics are calculated from the comparison (see
**Value** below).

## Usage

``` r
cpr_rand_test(
  comm,
  phy,
  null_model,
  n_reps = 100,
  n_iterations = 10000,
  thin = 1,
  metrics = c("pd", "rpd", "pe", "rpe"),
  site_col = "site",
  tbl_out = tibble::is_tibble(comm),
  quiet = FALSE
)
```

## Arguments

- comm:

  Dataframe, tibble, or matrix; input community data with sites
  (communities) as rows and species as columns. Either presence-absence
  data (values only 0s or 1s) or abundance data (values \>= 0) accepted,
  but calculations do not use abundance-weighting, so results from
  abundance data will be the same as if converted to presence-absence
  before analysis.

- phy:

  List of class `phylo`; input phylogeny.

- null_model:

  Character vector of length 1 or object of class `commsim`; either the
  name of the model to use for generating random communities (null
  model), or a custom null model. For full list of available predefined
  null models, see the help file of
  [`vegan::commsim()`](https://vegandevs.github.io/vegan/reference/commsim.html),
  or run
  [`vegan::make.commsim()`](https://vegandevs.github.io/vegan/reference/commsim.html).
  An object of class `commsim` can be generated with
  [`vegan::commsim()`](https://vegandevs.github.io/vegan/reference/commsim.html)
  (see **Examples** in
  [`cpr_rand_comm()`](https://docs.ropensci.org/canaper/reference/cpr_rand_comm.md)).

- n_reps:

  Numeric vector of length 1; number of random communities to replicate.

- n_iterations:

  Numeric vector of length 1; number of iterations to use for sequential
  null models; ignored for non-sequential models.

- thin:

  Numeric vector of length 1; thinning parameter used by some null
  models in `vegan` (e.g., `quasiswap`); ignored for other models.

- metrics:

  Character vector; names of biodiversity metrics to calculate. May
  include one or more of: `pd`, `rpd`, `pe`, `rpe` (case-sensitive).

- site_col:

  Character vector of length 1; name of column in `comm` that contains
  the site names; only used if `comm` is a tibble (object of class
  `tbl_df`).

- tbl_out:

  Logical vector of length 1; should the output be returned as a tibble?
  If `FALSE`, will return a dataframe. Defaults to `TRUE` if `comm` is a
  tibble.

- quiet:

  Logical vector of length 1; if `TRUE`, suppress all warnings and
  messages that would be emitted by this function.

## Value

Dataframe. For each of the biodiversity metrics, the following 9 columns
will be produced:

- `*_obs`: Observed value

- `*_obs_c_lower`: Count of times observed value was lower than random
  values

- `*_obs_c_upper`: Count of times observed value was higher than random
  values

- `*_obs_p_lower`: Percentage of times observed value was lower than
  random values

- `*_obs_p_upper`: Percentage of times observed value was higher than
  random values

- `*_obs_q`: Count of the non-NA random values used for comparison

- `*_obs_z`: Standard effect size (z-score)

- `*_rand_mean`: Mean of the random values

- `*_rand_sd`: Standard deviation of the random values

So if you included `pd` in `metrics`, the output columns would include
`pd_obs`, `pd_obs_c_lower`, etc...

## Details

The biodiversity metrics (`metrics`) available for analysis include:

- `pd`: Phylogenetic diversity (Faith 1992)

- `rpd`: Relative phylogenetic diversity (Mishler et al 2014)

- `pe`: Phylogenetic endemism (Rosauer et al 2009)

- `rpe`: Relative phylogenetic endemism (Mishler et al 2014)

(`pe` and `rpe` are needed for CANAPE with
[`cpr_classify_endem()`](https://docs.ropensci.org/canaper/reference/cpr_classify_endem.md))

The choice of a randomization algorithm (`null_model`) is not trivial,
and may strongly affect results. `cpr_rand_test()` uses null models
provided by `vegan`; for a complete list, see the help file of
[`vegan::commsim()`](https://vegandevs.github.io/vegan/reference/commsim.html)
or run
[`vegan::make.commsim()`](https://vegandevs.github.io/vegan/reference/commsim.html).
One frequently used null model is `swap` (Gotelli & Entsminger 2003),
which randomizes the community matrix while preserving column and row
sums (marginal sums). For a review of various null models, see Strona et
al. (2018); `swap` is an "FF" model in the sense of Strona et al.
(2018).

Instead of using one of the predefined null models in
[`vegan::commsim()`](https://vegandevs.github.io/vegan/reference/commsim.html),
it is also possible to define a custom null model; see **Examples** in
[`cpr_rand_comm()`](https://docs.ropensci.org/canaper/reference/cpr_rand_comm.md)

Note that the pre-defined models in `vegan` include binary models
(designed for presence-absence data) and quantitative models (designed
for abundance data). Although the binary models will accept abundance
data, they treat it as binary and always return a binary
(presence-absence) matrix. The PD and PE calculations in `canaper` are
not abundance-weighted, so they return the same result regardless of
whether the input is presence-absence or abundance. In that sense,
binary null models are appropriate for `cpr_rand_test()`. The
quantitative models could also be used for abundance data, but the
output will be treated as binary anyways when calculating PD and PE. The
effects of using binary vs. quantitative null models for
`cpr_rand_test()` have not been investigated.

A minimum of 5 species and sites are required as input; fewer than that
is likely cause the some randomization algorithms (e.g., `swap`) to
enter an infinite loop. Besides, inferences on very small numbers of
species and/or sites is not recommended generally.

The following rules apply to `comm` input:

- If dataframe or matrix, must include row names (site names) and column
  names (species names).

- If tibble, a single column (default, `site`) must be included with
  site names, and other columns must correspond to species names.

- Column names cannot start with a number and must be unique.

- Row names (site names) must be unique.

- Values (other than site names) should only include integers \>= 0;
  non-integer input will be converted to integer.

The results are identical regardless of whether the input for `comm` is
abundance or presence-absence data (i.e., abundance weighting is not
used).

## References

Faith DP (1992) Conservation evaluation and phylogenetic diversity.
Biological Conservation, 61:1–10.
[doi:10.1016/0006-3207(92)91201-3](https://doi.org/10.1016/0006-3207%2892%2991201-3)

Gotelli, N.J. and Entsminger, N.J. (2003). Swap algorithms in null model
analysis. Ecology 84, 532–535.

Mishler, B., Knerr, N., González-Orozco, C. et al. (2014) Phylogenetic
measures of biodiversity and neo- and paleo-endemism in Australian
Acacia. Nat Commun, 5: 4473.
[doi:10.1038/ncomms5473](https://doi.org/10.1038/ncomms5473)

Rosauer, D., Laffan, S.W., Crisp, M.D., Donnellan, S.C. and Cook, L.G.
(2009) Phylogenetic endemism: a new approach for identifying
geographical concentrations of evolutionary history. Molecular Ecology,
18: 4061-4072.
[doi:10.1111/j.1365-294X.2009.04311.x](https://doi.org/10.1111/j.1365-294X.2009.04311.x)

Strona, G., Ulrich, W. and Gotelli, N.J. (2018), Bi-dimensional null
model analysis of presence-absence binary matrices. Ecology, 99:
103-115. [doi:10.1002/ecy.2043](https://doi.org/10.1002/ecy.2043)

## Examples

``` r
# \donttest{
set.seed(12345)
data(phylocom)
# Returns a dataframe by defualt
cpr_rand_test(
  phylocom$comm, phylocom$phy,
  null_model = "curveball", metrics = "pd", n_reps = 10
)
#> Warning: Abundance data detected. Results will be the same as if using presence/absence data (no abundance weighting is used).
#> Warning: Dropping tips from the tree because they are not present in the community data: 
#>  sp16, sp23, sp27, sp28, sp30, sp31, sp32
#>            pd_obs pd_rand_mean pd_rand_sd  pd_obs_z pd_obs_c_upper
#> clump1  0.3018868    0.4622642 0.03799700 -4.220790              0
#> clump2a 0.3207547    0.4679245 0.03182166 -4.624831              0
#> clump2b 0.3396226    0.4698113 0.03009682 -4.325662              0
#> clump4  0.4150943    0.4698113 0.03138358 -1.743490              0
#> even    0.5660377    0.4773585 0.02819687  3.145003             10
#> random  0.5094340    0.4622642 0.02223606  2.121320             10
#>         pd_obs_c_lower pd_obs_q pd_obs_p_upper pd_obs_p_lower
#> clump1              10       10              0              1
#> clump2a             10       10              0              1
#> clump2b             10       10              0              1
#> clump4              10       10              0              1
#> even                 0       10              1              0
#> random               0       10              1              0

# Tibbles may be preferable because of the large number of columns
cpr_rand_test(
  phylocom$comm, phylocom$phy,
  null_model = "curveball", tbl_out = TRUE, n_reps = 10
)
#> Warning: Abundance data detected. Results will be the same as if using presence/absence data (no abundance weighting is used).
#> Warning: Dropping tips from the tree because they are not present in the community data: 
#>  sp16, sp23, sp27, sp28, sp30, sp31, sp32
#> # A tibble: 6 × 55
#>   site    pd_obs pd_rand_mean pd_rand_sd pd_obs_z pd_obs_c_upper pd_obs_c_lower
#>   <chr>    <dbl>        <dbl>      <dbl>    <dbl>          <dbl>          <dbl>
#> 1 clump1   0.302        0.472     0.0308   -5.51               0             10
#> 2 clump2a  0.321        0.464     0.0270   -5.32               0             10
#> 3 clump2b  0.340        0.458     0.0418   -2.85               0             10
#> 4 clump4   0.415        0.475     0.0425   -1.42               0              8
#> 5 even     0.566        0.474     0.0288    3.22              10              0
#> 6 random   0.509        0.472     0.0436    0.866              7              1
#> # ℹ 48 more variables: pd_obs_q <dbl>, pd_obs_p_upper <dbl>,
#> #   pd_obs_p_lower <dbl>, pd_alt_obs <dbl>, pd_alt_rand_mean <dbl>,
#> #   pd_alt_rand_sd <dbl>, pd_alt_obs_z <dbl>, pd_alt_obs_c_upper <dbl>,
#> #   pd_alt_obs_c_lower <dbl>, pd_alt_obs_q <dbl>, pd_alt_obs_p_upper <dbl>,
#> #   pd_alt_obs_p_lower <dbl>, rpd_obs <dbl>, rpd_rand_mean <dbl>,
#> #   rpd_rand_sd <dbl>, rpd_obs_z <dbl>, rpd_obs_c_upper <dbl>,
#> #   rpd_obs_c_lower <dbl>, rpd_obs_q <dbl>, rpd_obs_p_upper <dbl>, …
# }
```
