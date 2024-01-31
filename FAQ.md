# FAQ

These are Frequently Asked Questions about tools in the
[AttieLab-Systems-Genetics](https://github/AttieLab-Systems-Genetics)
GitHub Organization.

- [Data Harmonization](#data-harmonization)
- [QTL Effects](#qtl-effects)

## Data Harmonization

- What is data harmonization?
  + [Data harmonization](https://www.icpsr.umich.edu/web/pages/DSDR/harmonization.html) is a widely used phrase for putting data in a machine-useable format.
  + In our case, this usually involves pivoting a "wide" file (many columns, few rows) to a "long" file (few columns, many rows).
  + The Founder apps want data with columns `dataset`, `trait`, `strain`, `sex`, `diet`, `animal`, and `value`.
  + Calculations are done currently in a script [FounderDietStudy/DataHarmony.Rmd](https://github.com/AttieLab-Systems-Genetics/FounderDietStudy/blob/main/DataHarmony.Rmd) using scripts that are tailored to specific wide format as supplied by collaborators.

- How are `area under the curve` and similar summaries calculated? What is `Vmax`, etc.?
  + See code in [foundr/area_under_curve.R](https://github.com/AttieLab-Systems-Genetics/foundr/blob/main/R/area_under_curve.R).
  + There are slightly different calculations for non-destructive measurements taken over `week`s and those at sacrifice over `minute`s for [glucose tolerance test (GTT)](https://www.ncbi.nlm.nih.gov/books/NBK279331/).
  + measurements over `week`s
    + Ave = mean(`value`)
    + Vmax = max(`value`)
    + Tmax = `week`[which.max(`value`)]
    + Slope = slope(`week`, `value`)
  + measurements over `minute`s
    + AUC = sum(diff(`minute`) * zoo::rollmean(`value`, 2))
    + Emax = max(`value`)
    + Tmax = `minute`[which.max(`value`)]
    + HalfLife = `half`(Tmax, `minute`, `value`)
- How is `HalfLife` calculated?
  + Take `log2()` of `value`
  + Fit a regression line to `log2(value)`
  + Find time when line drops `2` units from time `0`, which is at `-1/slope`
  + See function `half()` in [foundr/area_under_curve.R](https://github.com/AttieLab-Systems-Genetics/foundr/blob/main/R/area_under_curve.R)
- How is `Slope` calculated?
  + Fit a regression line to `value`
  + Report the `slope`
  + See function `slope()` in [foundr/area_under_curve.R](https://github.com/AttieLab-Systems-Genetics/foundr/blob/main/R/area_under_curve.R)
  
## QTL Effects

- How do I get QTL effects when there is an interaction?
  + See [DO_Diet/gene_trait.Rmd](https://github.com/AttieLab-Systems-Genetics/DO_Diet/blob/master/gene_trait.Rmd) for a scripted example.
  + This Rmarkdown script has user-modifiable parameters.
  
