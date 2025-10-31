
<!-- README.md is generated from README.Rmd. Please edit that file -->

# niceday

<!-- badges: start -->

[![R-CMD-check](https://github.com/statdivlab/niceday/workflows/R-CMD-check/badge.svg)](https://github.com/statdivlab/niceday/actions)
<!-- badges: end -->

`niceday` is an `R` package for non-parametrically estimating
fold-differences in multivariate outcomes. `niceday` specifically
estimates log-fold differences in covariate-weighted conditional means
of an outcome *even when the desired outcome may not be directly
observed*. Instead, the observed outcome reflects the desired outcome
but with category- and sample-specific multiplicative distortions. One
of the key advantages of niceday is that no assumptions about the
distribution of outcomes or the structural relationship between the
outcome and adjustment covariates (e.g., linearity) need to be made.

We expect `niceday` to be especially useful for **microbiome
researchers**, because

1.  High-throughput sequencing of microbiomes displays variation in
    sequencing depth, and [unequal detection of
    taxa](https://elifesciences.org/articles/46923) (e.g., due to
    extraction bias, amongst other things). Therefore, `niceday` allows
    estimation of fold-differences on the true abundance scale, but just
    the observed sequencing scale.
2.  Researchers often want to adjust for additional covariates (either
    known confounders or simply to make more reasonable comparisons
    between groups), but don’t know what form the adjustment should take
    – e.g., linear vs nonlinear, etc.

We welcome your feedback and questions, and hope you find this package
useful!

## Installation

To install and load `niceday`, use the following code. You may get some
messages about the loaded packages, but these aren’t a problem.

``` r
# install.packages("remotes")
# remotes::install_github("statdivlab/niceday")
library(niceday)
```

## Use

Here’s an example of how to run `niceday`’s main fitting function,
`ndFit`. Check out the vignettes for more information! Here, we have an
observed data matrix `W`, metadata `data`, contrast of interest `A`, and
adjustment covariates `X`.

``` r
library(niceday)
data(EcoZUR_meta)
data(EcoZUR_count)
my_ndfit <- ndFit(W = EcoZUR_count[, 1:50], # consider only the first 50 taxa to run quickly
      data = EcoZUR_meta,
      A = ~ Diarrhea,
      X = ~ sex + age_months,
      num_crossval_folds = 2, # use more folds in practice
      num_crossfit_folds = 2, # for cross validation and cross fitting
      sl.lib.pi = c("SL.mean"), # choosing single learner for the example to run quickly,
      sl.lib.m = c("SL.mean"))  # in practice would use other options as well
```

If you want to go deep down the rabbit hole, you can look at how we ran
it for the data analysis in our paper
[here](https://github.com/statdivlab/niceday_supplementary/tree/main/data_application/R_scripts).

## Citation

If you use `niceday` for your analysis, please cite our manuscript.

Grant Hopkins, Sarah Teichman, Ellen Graham, and Amy Willis.
“Nonparametric Identification and Estimation of Ratios of Multi-Category
Means under Preferential Sampling.” <https://arxiv.org/abs/2510.23920>

## Bug reports and feature requests

If you identify a bug in `niceday` or have a feature request, please
post an issue [here](https://github.com/statdivlab/niceday/issues).

## Nomenclature

`niceday` stands for Nonparametrically Identified (de-Confounded)
Estimands for Difference Abundance, Yippee!
