# Output from Biodiverse

Output of analyzing test data with
[Biodiverse](https://github.com/shawnlaffan/biodiverse).

## Usage

``` r
biod_results
```

## Format

A tibble (dataframe) with 127 rows and 7 columns. Columns include:

- site:

  Site name; corresponds to row names of
  [`biod_example`](https://docs.ropensci.org/canaper/reference/biod_example.md)`$comm`

- pd_biodiv:

  Phylogenetic diversity (PD; `PD_P` in Biodiverse)

- pd_alt_biodiv:

  Alternative PD (PD measured on tree with all branchlengths equal;
  `PHYLO_RPD_NULL2` in Biodiverse)

- rpd_biodiv:

  Relative PD (PD divided by alternative PD; `PHYLO_RPD_NULL2` in
  Biodiverse)

- pe_biodiv:

  Phylogenetic endemism (PE; `PE_WE_P` in Biodiverse)

- pe_alt_biodiv:

  Alternative PE (PE measured on tree with all branchlengths equal;
  `PHYLO_RPE_NULL2` in Biodiverse)

- rpe_biodiv:

  Relative PE (PE divided by alternative PD; `PHYLO_RPE2` in Biodiverse)

## Details

The
[example_project.bps](https://github.com/shawnlaffan/biodiverse/raw/fbcad3c1df3667bac1235e822cb48ef6e5884e66/data/example_project.bps)
\# nolint example data set was used as input,which corresponds to the
[`biod_example`](https://docs.ropensci.org/canaper/reference/biod_example.md)
dataset in this package.

For a description of all Biodiverse metrics, [see the Biodiverse
wiki](https://github.com/shawnlaffan/biodiverse/wiki/Indices). \# nolint

## References

Laffan, S.W., Lubarsky, E. & Rosauer, D.F. (2010) Biodiverse, a tool for
the spatial analysis of biological and related diversity. Ecography. Vol
33, 643-647 (Version 3.1).
[doi:10.1111/j.1600-0587.2010.06237.x](https://doi.org/10.1111/j.1600-0587.2010.06237.x)

## Examples

``` r
biod_results
#> # A tibble: 127 × 7
#>    site    pd_biodiv pd_alt_biodiv rpd_biodiv pe_biodiv pe_alt_biodiv rpe_biodiv
#>    <chr>       <dbl>         <dbl>      <dbl>     <dbl>         <dbl>      <dbl>
#>  1 195000…    0.0469        0.0690      0.680   0.00661       0.00290      2.28 
#>  2 195000…    0.0469        0.0690      0.680   0.00661       0.00290      2.28 
#>  3 205000…    0.0931        0.172       0.540   0.00833       0.00504      1.65 
#>  4 205000…    0.0469        0.0690      0.680   0.00661       0.00290      2.28 
#>  5 215000…    0.0469        0.155       0.302   0.00146       0.00236      0.620
#>  6 215000…    0.0683        0.172       0.396   0.00259       0.00327      0.793
#>  7 215000…    0.0931        0.172       0.540   0.00833       0.00504      1.65 
#>  8 225000…    0.0469        0.155       0.302   0.00173       0.00258      0.673
#>  9 225000…    0.0931        0.172       0.540   0.00806       0.00482      1.67 
#> 10 225000…    0.182         0.276       0.659   0.0109        0.00755      1.45 
#> # ℹ 117 more rows
```
