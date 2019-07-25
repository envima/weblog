---
title: Using Python modues in R
layout: post
tags: R python marvin
categories: tutorial
---

Integration of Python modules in a R workflow.

## Import Python modules in R

With the `reticulate` package you can import python modules in R. The
variable np stores the python functions that come with the numpy
library. We can access these functions like np is a list with `$`.

``` r
# install.packages("reticulate")
library(reticulate)

np <- import("numpy")
np$absolute(-60)
```


## Facet Flow Networks

Facet flow networks performs a water accumulation algorithm directly on
a pointcloud. The package and details can be found on Github:
<https://github.com/Rheinwalt/FacetFlowNetwork>. Once the module is
installed we can use reticulate in R to incorporate it into a workflow
with other R Packages like lidR.

The package has only one function called `ffn`. So if we create an import
of the package in the variable ffn, we can use the function with
`ffn$ffn`.

``` r
library(lidR)
ffn <- import("FacetFlowNetwork")
np <- import("numpy")

pointcloud <- readLAS("~/proj_phenology/data/clouds_cropped/2019_05_03_tiepoints_default.las")

# make use of numpy to get the pointcloud in the correct format for ffn
x <- np$array(pointcloud@data$X)
y <- np$array(pointcloud@data$Y)
z <- np$array(pointcloud@data$Z)

flow <- ffn$ffn(x,y,z)
```

Flow now behaves as a python object with different attributes and
functions which you can call with `$`.

``` r
# get the specific catchment area
flow$sca() %>%
  head()
```

>	 [1] 0.109471080 7.832941793 0.068346767 0.011949873 0.003979073 0.105501005

``` r
# get the centroids of the facet
flow$facet_centroids() %>%
  head()
```

>              [,1]    [,2]     [,3]
>     [1,] 477798.6 5632226 330.2560
>     [2,] 477800.1 5632226 331.1307
>     [3,] 477893.5 5632169 337.3837
>     [4,] 477894.0 5632171 338.3153
>     [5,] 477798.4 5632226 331.0437
>     [6,] 477798.4 5632226 330.5493

You can use `ggplot2` now to visualize in familiar R grammar.

``` r
library(ggplot2)
library(viridis)

fc <- as.data.frame(flow$facet_centroids())
colnames(fc) <- c("x", "y", "z")

fc$sca <- as.vector(flow$sca())


ggplot(fc, aes(x, y, color = sca))+
  geom_point(size = 1)+
  scale_color_gradientn(colors = viridis(50), trans = "log")
```

![]({{site.url}}{{site.baseurl}}/assets/img/facetFlow.png)
