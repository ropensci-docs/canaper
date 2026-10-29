# Biodiverse example data

Fictional data for testing purposes from
[Biodiverse](https://github.com/shawnlaffan/biodiverse/tree/master/data).

## Usage

``` r
biod_example
```

## Format

A list with two elements:

- phy:

  Phylogeny with 31 tips

- comm:

  Community matrix with 127 sites and 31 species. Data are counts, i.e.,
  the number of times a species was observed in a grid cell.

## Details

Corresponds to the the community matrix ("groups" object) and phylogeny
from the Biodiverse
[example_project.bps](https://github.com/shawnlaffan/biodiverse/raw/fbcad3c1df3667bac1235e822cb48ef6e5884e66/data/example_project.bps).
\# nolint

## References

Laffan, S.W., Lubarsky, E. & Rosauer, D.F. (2010) Biodiverse, a tool for
the spatial analysis of biological and related diversity. Ecography. Vol
33, 643-647 (Version 3.1).
[doi:10.1111/j.1600-0587.2010.06237.x](https://doi.org/10.1111/j.1600-0587.2010.06237.x)

## Examples

``` r
# Example phylogeny
biod_example$phy
#> 
#> Phylogenetic tree with 31 tips and 30 internal nodes.
#> 
#> Tip labels:
#>   sp19, sp5, sp15, sp1, sp10, sp26, ...
#> Node labels:
#>   29___, 28___, 22___, 20___, 19___, 15___, ...
#> 
#> Rooted; includes branch length(s).
# Example community
biod_example$comm[1:5, 1:5]
#>                 sp1 sp2 sp3 sp4 sp5
#> 1950000:1350000   0   0   0   0   0
#> 1950000:1450000   0   0   0   0   0
#> 2050000:1250000   0   0   0   0   0
#> 2050000:1350000   0   0   0   0   0
#> 2150000:1050000   0   0   0   0   0
```
