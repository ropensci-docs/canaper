# Original color palette for plotting results of CANAPE

Character vector with names corresponding to endemism types and values
corresponding to color codes. Original palette used by Mishler et al.
(2014). May not be distinguishable to people with color vision
deficiency (CVD).

## Usage

``` r
mishler_endem_cols
```

## Format

An object of class `character` of length 5.

## Details

Color scheme:

- paleo: blue

- neo: red

- not significant: beige

- mixed: light purple

- super: dark purple

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
[`mishler_signif_cols`](https://docs.ropensci.org/canaper/reference/mishler_signif_cols.md)

## Examples

``` r
mishler_endem_cols
#>             neo           paleo not significant           mixed           super 
#>       "#E73323"       "#5577F7"       "#FAFAD6"       "#BF84F8"       "#8E25F6" 
scales::show_col(mishler_endem_cols)
```
