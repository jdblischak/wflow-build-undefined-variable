# undefined

This repository reproduces a strange observation with the function `wflow_build()` of the [workflowr][] R package.

## Description

If a function in a package has an undefined variable, and that variable is
defined in one of the enclosing environments, it will used that variable. In
general this is probably a bad idea, but if the purpose of the function is to
react to the current environment in some way, this may be desired behavior.

This works when using the "Knit" button in RStudio, `rmarkdown::render_site`,
and `rmarkdown::render`. However, `wflow_build`, which calls
`rmarkdown::render_site` via `callr::r_safe` does not allow this.

## Instructions

1. Clone this repo
1. Install workflowr
1. Build and install the package `undefined` with `devtools::install` (or Ctrl-Shift-B in RStudio)
1. Open `analysis/undefined.Rmd` and run with RStudio "Knit" button (or `rmarkdown::render_site("analysis/undefined.Rmd")`)
1. Run `workflowr::wflow_build("analysis/undefined.Rmd")`

To clean up, remove the fake package with `remove.packages("undefined")`

[workflowr]: https://github.com/jdblischak/workflowr
