# Original color palette for plotting results of CANAPE

Character vector with names corresponding to endemism types and values
corresponding to color codes. Original palette used by Mishler et al.
(2014). May not be distinguishable to people with color vision
deficiency (CVD).

## Usage

``` r
mishler_signif_cols
```

## Format

An object of class `character` of length 5.

## References

Mishler, B., Knerr, N., González-Orozco, C. et al. (2014) Phylogenetic
measures of biodiversity and neo- and paleo-endemism in Australian
Acacia. Nat Commun, 5: 4473.
[doi:10.1038/ncomms5473](https://doi.org/10.1038/ncomms5473)

## See also

Other colors:
[`cpr_endem_cols_2`](https://docs.ropensci.org/canaper/reference/cpr_endem_cols_2.md),
[`cpr_endem_cols_3`](https://docs.ropensci.org/canaper/reference/cpr_endem_cols_3.md),
[`cpr_endem_cols_4`](https://docs.ropensci.org/canaper/reference/cpr_endem_cols_4.md),
[`cpr_endem_cols`](https://docs.ropensci.org/canaper/reference/cpr_endem_cols.md),
[`cpr_make_pal()`](https://docs.ropensci.org/canaper/reference/cpr_make_pal.md),
[`cpr_signif_cols_2`](https://docs.ropensci.org/canaper/reference/cpr_signif_cols_2.md),
[`cpr_signif_cols`](https://docs.ropensci.org/canaper/reference/cpr_signif_cols.md),
[`mishler_endem_cols`](https://docs.ropensci.org/canaper/reference/mishler_endem_cols.md)

## Examples

``` r
mishler_signif_cols
#>          < 0.01         < 0.025 not significant         > 0.975          > 0.99 
#>       "#7D170E"       "#E73323"       "#FAFAD6"       "#5577F7"       "#2E4086" 
scales::show_col(mishler_signif_cols)
```
