# Classify phylogenetic endemism

Given the results of
[`cpr_rand_test()`](https://docs.ropensci.org/canaper/reference/cpr_rand_test.md),
classifies phylogenetic endemism according to CANAPE scheme of Mishler
et al. 2014.

## Usage

``` r
cpr_classify_endem(df)
```

## Arguments

- df:

  Input data frame. Must have the following columns:

  - `pe_obs_p_upper`: Upper *p*-value comparing observed phylogenetic
    endemism to random values

  - `pe_alt_obs_p_upper`: Upper *p*-value comparing observed
    phylogenetic endemism on alternate tree to random values

  - `rpe_obs_p_upper`: Upper *p*-value comparing observed relative
    phylogenetic endemism to random values

## Value

Object of class data.frame with column `endem_type` (character) added.
Values of `endem_type` type include `paleo` (paleoendemic), `neo`
(neoendemic), `not significant` (what it says), `mixed` (mixed
endemism), and `super` (super-endemic; both `pe_obs` and `pe_obs_alt`
are highly significant).

## Details

For a summary of the classification scheme, see:
[http://biodiverse-analysis-software.blogspot.com/2014/11/canape-categorical-analysis-of-palaeo.html](http://biodiverse-analysis-software.blogspot.com/2014/11/canape-categorical-analysis-of-palaeo.md)
\# nolint

## References

Mishler, B., Knerr, N., González-Orozco, C. et al. (2014) Phylogenetic
measures of biodiversity and neo- and paleo-endemism in Australian
Acacia. Nat Commun, 5: 4473.
[doi:10.1038/ncomms5473](https://doi.org/10.1038/ncomms5473)

## Examples

``` r
# \donttest{
set.seed(12345)
data(phylocom)
rand_test <- cpr_rand_test(
  phylocom$comm, phylocom$phy,
  null_model = "curveball", metrics = c("pe", "rpe"), n_reps = 10
)
#> Warning: Abundance data detected. Results will be the same as if using presence/absence data (no abundance weighting is used).
#> Warning: Dropping tips from the tree because they are not present in the community data: 
#>  sp16, sp23, sp27, sp28, sp30, sp31, sp32
cpr_classify_endem(rand_test)
#>            pe_obs pe_rand_mean pe_rand_sd   pe_obs_z pe_obs_c_upper
#> clump1  0.1333333    0.1622013 0.02479597 -1.1642182              1
#> clump2a 0.1081761    0.1563208 0.02319925 -2.0752680              1
#> clump2b 0.1286164    0.1727358 0.02557568 -1.7250565              0
#> clump4  0.1411950    0.1686164 0.02835495 -0.9670758              2
#> even    0.2506289    0.1752201 0.02225572  3.3882887             10
#> random  0.2380503    0.1649057 0.01987926  3.6794464             10
#>         pe_obs_c_lower pe_obs_q pe_obs_p_upper pe_obs_p_lower pe_alt_obs
#> clump1               9       10            0.1            0.9  0.1472222
#> clump2a              9       10            0.1            0.9  0.1194444
#> clump2b             10       10            0.0            1.0  0.1420139
#> clump4               8       10            0.2            0.8  0.1454861
#> even                 0       10            1.0            0.0  0.2246528
#> random               0       10            1.0            0.0  0.2211806
#>         pe_alt_rand_mean pe_alt_rand_sd pe_alt_obs_z pe_alt_obs_c_upper
#> clump1         0.1596528     0.01541291   -0.8065027                  2
#> clump2a        0.1583681     0.02159578   -1.8023714                  1
#> clump2b        0.1712847     0.01951462   -1.4999435                  0
#> clump4         0.1705556     0.01641871   -1.5268825                  0
#> even           0.1761111     0.01130450    4.2940129                 10
#> random         0.1640278     0.02422894    2.3588646                 10
#>         pe_alt_obs_c_lower pe_alt_obs_q pe_alt_obs_p_upper pe_alt_obs_p_lower
#> clump1                   8           10                0.2                0.8
#> clump2a                  9           10                0.1                0.9
#> clump2b                 10           10                0.0                1.0
#> clump4                  10           10                0.0                1.0
#> even                     0           10                1.0                0.0
#> random                   0           10                1.0                0.0
#>           rpe_obs rpe_rand_mean rpe_rand_sd  rpe_obs_z rpe_obs_c_upper
#> clump1  0.9056604     1.0167654  0.12496739 -0.8890724               0
#> clump2a 0.9056604     0.9881408  0.08895808 -0.9271831               0
#> clump2b 0.9056604     1.0064227  0.05648438 -1.7838966               0
#> clump4  0.9705048     0.9852723  0.09957128 -0.1483107               6
#> even    1.1156280     0.9946438  0.10702965  1.1303804               9
#> random  1.0762714     1.0140246  0.11480252  0.5422078               7
#>         rpe_obs_c_lower rpe_obs_q rpe_obs_p_upper rpe_obs_p_lower
#> clump1               10        10             0.0             1.0
#> clump2a              10        10             0.0             1.0
#> clump2b               9        10             0.0             0.9
#> clump4                4        10             0.6             0.4
#> even                  1        10             0.9             0.1
#> random                3        10             0.7             0.3
#>              endem_type
#> clump1  not significant
#> clump2a not significant
#> clump2b not significant
#> clump4  not significant
#> even              super
#> random            super
# }
```
