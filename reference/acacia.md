# *Acacia* example data

Dataset of Australian *Acacia* from Mishler et al. 2014 (Nat. Comm.)

## Usage

``` r
acacia
```

## Format

A list with two elements:

- phy:

  Phylogeny of Australian *Acacia* (list of class "phylo"). Tip labels
  are specific epithet, except for the outgroup, which includes genus
  and specific epithet. Includes 508 ingroup taxa (genus *Acacia*) and
  two outgroup taxa.

- comm:

  Community matrix of Australian *Acacia* (dataframe). Column names are
  specific epithet of each species. Row names are centroids of 50km grid
  cells in Australian Albers equal area EPSG:3577 projection. 3037 rows
  (sites) x 506 columns (species). Data are counts, i.e., the number of
  times a species was observed in a grid cell.

## References

Mishler, B., Knerr, N., González-Orozco, C. et al. Phylogenetic measures
of biodiversity and neo- and paleo-endemism in Australian Acacia. Nat
Commun 5, 4473 (2014).
[doi:10.1038/ncomms5473](https://doi.org/10.1038/ncomms5473)

## Examples

``` r
# Example phylogeny
acacia$phy
#> 
#> Phylogenetic tree with 510 tips and 509 internal nodes.
#> 
#> Tip labels:
#>   Pararchidendron_pruinosum, Paraserianthes_lophantha, adinophylla, semicircinalis, aphanoclada, inaequilatera, ...
#> 
#> Rooted; includes branch length(s).
# Example community
acacia$comm[1:5, 1:5]
#>                   abbreviata acanthaster acanthoclada acinacea aciphylla
#> -1025000:-1825000          0           0            0        0         0
#> -1025000:-1875000          0           0            0        0         0
#> -1025000:-1925000          0           0            0        0         0
#> -1025000:-1975000          0           0            0        0         0
#> -1025000:-2025000          0           0            0        0         0
```
