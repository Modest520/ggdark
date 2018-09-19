
<!-- README.md is generated from README.Rmd. Please edit that file -->
ggdark
======

Activate dark mode on your favorite ggplot2 theme with `ggdark::darken`.

Installation
------------

You can install ggdark from github with:

``` r
# install.packages("devtools")
devtools::install_github("nsgrantham/ggdark")
```

Dark mode
---------

`ggdark::darken` is not a ggplot2 theme. Rather, it acts on a ggplot2 theme and inverts its colors.

``` r
library(ggplot2)
library(ggdark)

p <- ggplot(iris, aes(Sepal.Width, Sepal.Length)) + 
  geom_point(aes(color = Species))

p  # theme_gray()
```

![](man/figures/gray-1.png)

``` r
p + darken()  # activate dark mode on theme_gray()
```

![](man/figures/darken-gray-1.png)

``` r
p + darken(theme_minimal())  # darken a different ggplot2 theme
```

![](man/figures/darken-minimal-1.png)

``` r
p + darken(theme_minimal(), background = "grey20")  # lighten black background
```

![](man/figures/grey-background-1.png)

In addition to inverting colors of theme elements, `darken` redefines the default values of geom fill and geom color from `"black"` to `"white"`. This makes the geoms visible against the dark background.

``` r
p <- ggplot(iris, aes(Sepal.Width, Sepal.Length)) +
  geom_point() +
  facet_wrap(~ Species)

p + darken()  # geom color is now white
```

![](man/figures/white-geom-color-1.png)

``` r
p + darken(geom_color = "grey77")  # or perhaps a light grey 
```

![](man/figures/grey-geom-color-1.png)

Restore the geom colors to their ggplot2 defaults with

    restore_geom_colors()  # fill = "black", color = "black"

Beware
------

`darken` must act directly on the theme it is modifying, layering does not work.

``` r
# darken is not aware of theme_minimal() and will darken the theme returned by theme_get()
p + theme_minimal() + darken()  # darkens theme_gray()
```

Set the theme to avoid this problem.

``` r
# this will darken theme_minimal(), as it is now returned by theme_get()
theme_set(theme_minimal())
p + darken()  

# why not turn on dark mode for all plots? :)
theme_set(darken(theme_minimal()))
p  # dark
```
