# Randomize a single community matrix

Note that binary null models return a binary matrix, even if an
abundance matrix was used as input.

## Usage

``` r
cpr_rand_comm(comm, null_model, n_iterations = 1, thin = 1, seed = NULL)
```

## Arguments

- comm:

  Dataframe or matrix; input community data with sites (communities) as
  rows and species as columns. Values of each cell are the
  presence/absence (0 or 1) or number of individuals (abundance) of each
  species in each site.

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
  (see Examples).

- n_iterations:

  Numeric vector of length 1; number of iterations for sequential null
  models. Ignored by non-sequential null models.

- thin:

  Numeric vector of length 1; thinning parameter used by some null
  models in `vegan` (e.g., `quasiswap`); ignored for other models.

- seed:

  Integer vector of length 1 or NULL; random seed that will be used in a
  call to [`set.seed()`](https://rdrr.io/r/base/Random.html) before
  randomizing the matrix. Default (`NULL`) will not change the random
  generator state.

## Value

Matrix

## Examples

``` r
set.seed(12345)

# Check list of available pre-defined null models in vegan
vegan::make.commsim()
#>  [1] "r00"             "c0"              "r0"              "r1"             
#>  [5] "r2"              "quasiswap"       "greedyqswap"     "swap"           
#>  [9] "tswap"           "curveball"       "backtrack"       "r2dtable"       
#> [13] "swap_count"      "quasiswap_count" "swsh_samp"       "swsh_both"      
#> [17] "swsh_samp_r"     "swsh_samp_c"     "swsh_both_r"     "swsh_both_c"    
#> [21] "abuswap_r"       "abuswap_c"       "r00_samp"        "c0_samp"        
#> [25] "r0_samp"         "r00_ind"         "c0_ind"          "r0_ind"         
#> [29] "r00_both"        "c0_both"         "r0_both"        

# Binary null model produces binary output
data(phylocom)
cpr_rand_comm(phylocom$comm, "swap", 100)
#>         sp1 sp10 sp11 sp12 sp13 sp14 sp15 sp17 sp18 sp19 sp2 sp20 sp21 sp22
#> clump1    1    0    0    0    0    0    0    1    1    0   1    0    0    0
#> clump2a   0    1    0    0    0    0    0    1    0    0   1    0    0    1
#> clump2b   1    1    0    1    0    1    0    0    0    0   1    0    0    0
#> clump4    1    0    1    0    0    0    0    1    0    1   1    0    1    0
#> even      1    0    0    0    0    0    0    1    1    0   0    1    0    0
#> random    1    0    0    1    1    0    1    0    0    0   1    0    0    0
#>         sp24 sp25 sp26 sp29 sp3 sp4 sp5 sp6 sp7 sp8 sp9
#> clump1     0    0    0    1   1   0   0   1   0   0   1
#> clump2a    0    1    0    0   1   1   1   0   0   0   0
#> clump2b    0    0    0    0   1   1   0   0   0   0   1
#> clump4     0    0    0    0   0   0   1   0   0   1   0
#> even       1    0    1    0   0   0   0   0   1   0   1
#> random     0    1    0    0   0   1   1   0   0   0   0

# Quantitative null model produces quantitative output
cpr_rand_comm(phylocom$comm, "swap_count", 100)
#>         sp1 sp10 sp11 sp12 sp13 sp14 sp15 sp17 sp18 sp19 sp2 sp20 sp21 sp22
#> clump1    1    0    0    2    1    0    0    0    1    0   0    0    0    0
#> clump2a   1    2    2    0    0    1    0    0    2    0   2    0    0    0
#> clump2b   1    0    0    0    0    0    1    0    0    2   2    1    0    0
#> clump4    0    0    0    0    0    0    0    5    1    0   0    0    0    0
#> even      1    0    0    1    0    0    0    0    0    0   0    1    0    1
#> random    1    1    0    0    0    3    1    3    0    0   1    0    1    0
#>         sp24 sp25 sp26 sp29 sp3 sp4 sp5 sp6 sp7 sp8 sp9
#> clump1     0    0    0    0   1   0   2   0   0   0   0
#> clump2a    0    0    2    0   0   0   0   0   0   0   0
#> clump2b    0    2    0    0   0   1   1   0   0   0   1
#> clump4     1    0    0    0   1   2   0   0   0   1   1
#> even       0    0    0    0   0   0   0   1   1   0   2
#> random     1    1    0    1   1   0   1   0   0   0   0

# How to use a custom null model
# 1. Define a randomizing function, e.g. re-sample the matrix while
# preserving total number of presences (same as the "r00" model)
randomizer <- function(x, n, ...) {
  array(replicate(n, sample(x)), c(dim(x), n))
}

# 2. Generate a commsim object
cs_object <- vegan::commsim(
  "r00_model",
  fun = randomizer, binary = TRUE,
  isSeq = FALSE, mode = "integer"
)

# 3. Generate the null community
cpr_rand_comm(phylocom$comm, cs_object, 100)
#>         sp1 sp10 sp11 sp12 sp13 sp14 sp15 sp17 sp18 sp19 sp2 sp20 sp21 sp22
#> clump1    0    1    0    0    1    0    1    0    0    0   0    1    0    1
#> clump2a   0    0    0    0    1    0    0    1    1    0   0    0    0    1
#> clump2b   0    0    0    0    0    0    0    0    0    0   1    0    0    0
#> clump4    0    1    1    0    1    1    0    0    0    1   1    1    0    1
#> even      0    0    1    0    1    0    0    1    1    1   1    0    0    1
#> random    1    1    0    0    1    0    0    0    0    0   0    0    0    0
#>         sp24 sp25 sp26 sp29 sp3 sp4 sp5 sp6 sp7 sp8 sp9
#> clump1     1    0    0    1   0   0   0   0   0   0   0
#> clump2a    1    0    0    0   0   0   1   0   1   0   0
#> clump2b    0    0    1    0   1   0   1   1   0   0   0
#> clump4     1    0    0    0   1   0   0   0   0   1   1
#> even       0    0    0    1   0   0   0   0   0   0   1
#> random     0    0    1    1   1   1   0   1   0   0   0
```
