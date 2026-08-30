# CVD-friendly color palette for plotting results of CANAPE, version 4

Character vector with names corresponding to endemism types and values
corresponding to color codes. Should be distinguishable to people with
color vision deficiency (CVD).

## Usage

``` r
cpr_endem_cols_4
```

## Format

An object of class `character` of length 5.

## Details

Color scheme:

- paleo: light blue

- neo: red

- not significant: light grey

- mixed: green

- super: yellow

## See also

Other colors:
[`cpr_endem_cols_2`](https://docs.ropensci.org/canaper/reference/cpr_endem_cols_2.md),
[`cpr_endem_cols_3`](https://docs.ropensci.org/canaper/reference/cpr_endem_cols_3.md),
[`cpr_endem_cols`](https://docs.ropensci.org/canaper/reference/cpr_endem_cols.md),
[`cpr_make_pal()`](https://docs.ropensci.org/canaper/reference/cpr_make_pal.md),
[`cpr_signif_cols_2`](https://docs.ropensci.org/canaper/reference/cpr_signif_cols_2.md),
[`cpr_signif_cols`](https://docs.ropensci.org/canaper/reference/cpr_signif_cols.md),
[`mishler_endem_cols`](https://docs.ropensci.org/canaper/reference/mishler_endem_cols.md),
[`mishler_signif_cols`](https://docs.ropensci.org/canaper/reference/mishler_signif_cols.md)

## Examples

``` r
cpr_endem_cols_4
#>           paleo             neo not significant           mixed           super 
#>       "#56B4E9"       "#D55E00"        "grey90"       "#009E73"       "#E69F00" 
scales::show_col(cpr_endem_cols_4)
```
