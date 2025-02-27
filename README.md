# 🌲🌉 Species distribution models with BART 🌉 🌲

Colin J. Carlson (Georgetown University); February 2020

[![DOI](https://zenodo.org/badge/187687555.svg)](https://zenodo.org/badge/latestdoi/187687555)

__How do I install__?

```
# install.packages('devtools')
devtools::install_github('cjcarlson/embarcadero')
```

Before you do that, you need the "velox" package, which is currently not on CRAN (that should be fixed soon). You can do that one of a couple ways:

```
remotes::install_github("hunzikp/velox@master")
```

Or,

```
devtools::install_version("velox", version = "0.2.0")
```

**If you have additional issues with velox install on Mac**, it might be because of some underlying issues with your C compiler, the current version of Rcpp (which has a known issue), and/or GDAL. If you leave me an issue I can try to help you figure it out. [Here](https://community.rstudio.com/t/later-package-not-compiling-on-macos-unknown-type-name-uuid-t/57171/2) [are](https://github.com/hunzikp/velox/issues/30) [some](https://github.com/rstudio/httpuv/issues/120) [posts](https://stackoverflow.com/questions/12141422/error-gdal-config-not-found) that were helpful when we recently had some of these issues.

__What's BART?__ 

Bayesian additive regression trees (BARTs) are an exciting alternative to other popular classification tree methods being used in ecology, like random forests or boosted regression trees. Whereas boosted regression trees fit an ensemble of trees each explaining smaller fractions of variance, BART starts by fitting a sum-of-trees model and then uses Bayesian "backfitting" with an MCMC algorithm to create a posterior draw. 

__Why BART?__ 

BART does well with model-free variable selection and handles irrelevant predictors well; the Bayesian aspect also comes with perks, like posterior distributions on predictions (without having to bootstrap, like you do with BRTs) and automated confidence intervals on partial dependency plots. So far, it also seems to avoid the problem BRTs have for niche modeling: with no automated selection of tree depth or tree complexity, BRTs tend to overfit especially with randomly-generated pseudoabsences and ensembling over subsets. In previous "bake-offs," BART commonly outperforms other methods, including comparable classification tree methods like random forests and boosted regression trees.

__Are BARTs new to ecology?__

No, there is nothing new under the sun. [Yen et al.](https://onlinelibrary.wiley.com/doi/pdf/10.1111/j.1600-0587.2011.06651.x) used BARTs to examine habitat selection of birds back in 2011. But so far, no, no one is using them for species distribution modeling (as far as I can tell).

__What does embarcadero do?__

This package is basically a wrapper around 'dbarts'  with a few tools
- basic model summary statistics and diagnostics 
- spatial prediction with raster data
- credible interval draws from the posterior distribution
- visualization of how posterior draws learn over time 
- variable importance measures and plots
- stepwise variable elimination
- automatic Nice Plots for partials, including multiple ways to visualize posterior draws
- spatial projection of partials ("spartials")
- compatibility with random intercept BART models (riBART)
- plots for random intercepts 

In future versions I'd hope to include compatibility with:
- explicitly-spatial adaptations of BART (spatial priors)
- compatibility with smoothed BART models (softBART) and sparse BART models with Dirichlet priors (DART)

__How do I learn to use embarcadero__?

The paper at _Methods in Ecology and Evolution_ includes a bunch of code, and there's a new vignette included in the package that runs through all of the basic functionality using a virtual species. I've migrated the older, more advanced vignette - which is over 30 pages and takes a good 3 hours to run on an older machine - to another repo (cjcarlson/pier39) and am in the process of updating it to be much clearer.

__How do I cite embarcadero__?

The embarcadero package is published at [*Methods in Ecology and Evolution*](https://besjournals.onlinelibrary.wiley.com/doi/abs/10.1111/2041-210X.13389)!

__Can I help__?

Please! Reach out to colin.carlson@georgetown.edu if you want to help with development or otherwise are interested in being one of the first users.

__Why is it called embarcadero?__

Because of Embarcadero BART station, and because I'm homesick for Humphry Slocombe. 
