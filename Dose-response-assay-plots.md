Dose response assay plots
================
Emily J Tallerday
2023-06-30

# Setup

## Load packages to be used

``` r
packages <- c("rmarkdown", "pandoc", "formatR", "tidyverse", "gridExtra", "ggpubr", "viridis", "ggthemes", "here", "gplots", "cowplot", "ggtext", "ggsignif", "ggokabeito")
pacman::p_load(char = packages, install = T, character.only = T)
```

## Set ggplot theme

My personal preference:

``` r
theme_set(theme_light())
```

## Define functions

This section may be empty if functions are not needed.

# Data

## Import

``` r
BA_response <- read.csv(here(r"(Data\06292023_Eva_BA response data.csv)"))
```

NOTE that this data was provided by Eva from a magenta box BA dose
response assay done in Summer 2023.

## Tidy data for easy working

``` r
BA_response$treatment[BA_response$treatment == "veh"] <- 0
```

``` r
BA_response$genotype <- as.factor(BA_response$genotype)
```

``` r
BA_response$treatment <- as.numeric(BA_response$treatment)
```

``` r
colnames(BA_response) <- c("Genotype", "Conc. BA (ng/uL)", "Shoot length (cm)", "Root length (cm)")
```

# Plot

## Linear regression

The code for the following plot was modified from [this tutorial by
datanovia](https://rpkgs.datanovia.com/ggpubr/reference/stat_regline_equation.html).

``` r
BA_response %>%
  ggplot(aes(x = `Conc. BA (ng/uL)`, y = `Root length (cm)`, color = Genotype, fill = Genotype)) +
  geom_point(shape = 21, size = 2, alpha = 0.5, color = "black") +
  geom_smooth(method = "lm", se = T, alpha = 0.2) +
  facet_wrap(~Genotype,
    ncol = 4,
    nrow = 1,
    scales = "free"
  ) +
  theme(strip.background = element_blank()) +
  stat_regline_equation(color = "black") +
  labs(
    color = "Genotype",
    fill = "Genotype"
  ) +
  scale_color_okabe_ito() +
  scale_fill_okabe_ito()
```

![](Dose-response-assay-plots_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

# Session info

``` r
sessionInfo()
```

    ## R version 4.2.2 (2022-10-31 ucrt)
    ## Platform: x86_64-w64-mingw32/x64 (64-bit)
    ## Running under: Windows 10 x64 (build 22621)
    ## 
    ## Matrix products: default
    ## 
    ## locale:
    ## [1] LC_COLLATE=English_United States.utf8 
    ## [2] LC_CTYPE=English_United States.utf8   
    ## [3] LC_MONETARY=English_United States.utf8
    ## [4] LC_NUMERIC=C                          
    ## [5] LC_TIME=English_United States.utf8    
    ## 
    ## attached base packages:
    ## [1] stats     graphics  grDevices utils     datasets  methods   base     
    ## 
    ## other attached packages:
    ##  [1] ggokabeito_0.1.0  ggsignif_0.6.4    ggtext_0.1.2      cowplot_1.1.1    
    ##  [5] gplots_3.1.3      here_1.0.1        ggthemes_4.2.4    viridis_0.6.3    
    ##  [9] viridisLite_0.4.2 ggpubr_0.6.0      gridExtra_2.3     lubridate_1.9.2  
    ## [13] forcats_1.0.0     stringr_1.5.0     dplyr_1.1.2       purrr_1.0.1      
    ## [17] readr_2.1.4       tidyr_1.3.0       tibble_3.2.1      ggplot2_3.4.2    
    ## [21] tidyverse_2.0.0   formatR_1.14      pandoc_0.1.0      rmarkdown_2.22   
    ## 
    ## loaded via a namespace (and not attached):
    ##  [1] Rcpp_1.0.10        lattice_0.20-45    gtools_3.9.4       rprojroot_2.0.3   
    ##  [5] digest_0.6.32      utf8_1.2.3         R6_2.5.1           backports_1.4.1   
    ##  [9] evaluate_0.21      highr_0.10         pillar_1.9.0       rlang_1.1.1       
    ## [13] rstudioapi_0.14    car_3.1-2          Matrix_1.5-4.1     labeling_0.4.2    
    ## [17] splines_4.2.2      polynom_1.4-1      munsell_0.5.0      gridtext_0.1.5    
    ## [21] broom_1.0.5        compiler_4.2.2     xfun_0.39          pkgconfig_2.0.3   
    ## [25] mgcv_1.8-41        htmltools_0.5.5    tidyselect_1.2.0   fansi_1.0.4       
    ## [29] tzdb_0.4.0         withr_2.5.0        bitops_1.0-7       rappdirs_0.3.3    
    ## [33] grid_4.2.2         nlme_3.1-160       gtable_0.3.3       lifecycle_1.0.3   
    ## [37] pacman_0.5.1       magrittr_2.0.3     scales_1.2.1       KernSmooth_2.23-20
    ## [41] cli_3.6.1          stringi_1.7.12     carData_3.0-5      farver_2.1.1      
    ## [45] fs_1.6.2           xml2_1.3.4         generics_0.1.3     vctrs_0.6.3       
    ## [49] tools_4.2.2        glue_1.6.2         hms_1.1.3          abind_1.4-5       
    ## [53] fastmap_1.1.1      yaml_2.3.7         timechange_0.2.0   colorspace_2.1-0  
    ## [57] caTools_1.18.2     rstatix_0.7.2      knitr_1.43
