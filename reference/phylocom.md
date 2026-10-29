# Phylocom example data

Fictional data for testing purposes from
[Phylocom](https://www.phylodiversity.net/phylocom/) (Webb et al. 2008)

## Usage

``` r
phylocom
```

## Format

A list with three elements:

- phylo:

  Phylogeny with 32 tips

- sample:

  Community matrix with 6 sites (rows) and 25 species (columns).

- traits:

  Trait data; a data.frame with 32 species (rows) and 4 traits (columns)

## Details

Obtained via the `picante` package (Kembel et al. 2010)

## References

Webb, C.O., Ackerly, D.D., and Kembel, S.W. 2008. Phylocom: software for
the analysis of phylogenetic community structure and trait evolution.
Version 4.0.1. http://www.phylodiversity.net/phylocom/.

Kembel, et al. Picante: R tools for integrating phylogenies and ecology,
Bioinformatics 26: 1463–1464
[doi:10.1093/bioinformatics/btq166](https://doi.org/10.1093/bioinformatics/btq166)

## Examples

``` r
# Example phylogeny
phylocom$phy
#> 
#> Phylogenetic tree with 32 tips and 31 internal nodes.
#> 
#> Tip labels:
#>   sp1, sp2, sp3, sp4, sp5, sp6, ...
#> Node labels:
#>   A, B, C, D, E, F, ...
#> 
#> Rooted; includes branch length(s).
# Example community
phylocom$comm
#>         sp1 sp10 sp11 sp12 sp13 sp14 sp15 sp17 sp18 sp19 sp2 sp20 sp21 sp22
#> clump1    1    0    0    0    0    0    0    0    0    0   1    0    0    0
#> clump2a   1    2    2    2    0    0    0    0    0    0   1    0    0    0
#> clump2b   1    0    0    0    0    0    0    2    2    2   1    2    0    0
#> clump4    1    1    0    0    0    0    0    2    2    0   1    0    0    0
#> even      1    0    0    0    1    0    0    1    0    0   0    0    1    0
#> random    0    0    0    1    0    4    2    3    0    0   1    0    0    1
#>         sp24 sp25 sp26 sp29 sp3 sp4 sp5 sp6 sp7 sp8 sp9
#> clump1     0    0    0    0   1   1   1   1   1   1   0
#> clump2a    0    0    0    0   1   1   0   0   0   0   2
#> clump2b    0    0    0    0   1   1   0   0   0   0   0
#> clump4     0    2    2    0   0   0   0   0   0   0   1
#> even       0    1    0    1   0   0   1   0   0   0   1
#> random     2    0    0    0   0   0   2   0   0   0   0
```
