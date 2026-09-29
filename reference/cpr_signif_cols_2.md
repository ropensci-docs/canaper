# CVD-friendly color palette for plotting results of randomization test, version 2

Character vector with names corresponding to significance levels and
values corresponding to color codes, with "not significant" colored
grey.

## Usage

``` r
cpr_signif_cols_2
```

## Format

An object of class `character` of length 5.

## See also

Other colors:
[`cpr_endem_cols_2`](https://docs.ropensci.org/canaper/reference/cpr_endem_cols_2.md),
[`cpr_endem_cols_3`](https://docs.ropensci.org/canaper/reference/cpr_endem_cols_3.md),
[`cpr_endem_cols_4`](https://docs.ropensci.org/canaper/reference/cpr_endem_cols_4.md),
[`cpr_endem_cols`](https://docs.ropensci.org/canaper/reference/cpr_endem_cols.md),
[`cpr_make_pal()`](https://docs.ropensci.org/canaper/reference/cpr_make_pal.md),
[`cpr_signif_cols`](https://docs.ropensci.org/canaper/reference/cpr_signif_cols.md),
[`mishler_endem_cols`](https://docs.ropensci.org/canaper/reference/mishler_endem_cols.md),
[`mishler_signif_cols`](https://docs.ropensci.org/canaper/reference/mishler_signif_cols.md)

## Examples

``` r
cpr_signif_cols_2
#>          < 0.01         < 0.025 not significant         > 0.975          > 0.99 
#>       "#E31A1C"       "#FB9A99"        "grey90"       "#A6CEE3"       "#1F78B4" 
scales::show_col(cpr_signif_cols_2)
```
