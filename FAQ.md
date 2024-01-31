# FAQ

These are Frequently Asked Questions about tools in the
[AttieLab-Systems-Genetics](https://github/AttieLab-Systems-Genetics)
GitHub Organization.

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
  + See function `half()` in [foundr/area_under_curve.R](https://github.com/AttieLab-Systems-Genetics/foundr/blob/main/R/area_under_curve.R)
  + Take `log2()` of `value`
  + Fit a regression line to `log2(value)`
  + Find time when line drops `2` units from time `0`, which is at `-1/slope`
- How is `Slope` calculated?
  + Fit a regression line to `value`
  + Report the `slope`
  
