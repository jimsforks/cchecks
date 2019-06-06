cchecks
=======



[![Build Status](https://travis-ci.com/ropenscilabs/cchecks.svg?branch=master)](https://travis-ci.com/ropenscilabs/cchecks)
[![codecov.io](https://codecov.io/github/ropenscilabs/cchecks/coverage.svg?branch=master)](https://codecov.io/github/ropenscilabs/cchecks?branch=master)

R client for the cran checks API at <https://cranchecks.info>

[Cran checks API docs][docs]

there's no authentication needed

## Install

Development version


```r
devtools::install_github("ropenscilabs/cchecks")
```


```r
library("cchecks")
```

## heartbeat


```r
cch_heartbeat()
#> $routes
#> [1] "/docs (GET)"                    "/heartbeat (GET)"              
#> [3] "/pkgs (GET)"                    "/pkgs/:pkg_name: (GET)"        
#> [5] "/pkgs/:pkg_name:/history (GET)" "/maintainers (GET)"            
#> [7] "/maintainers/:email: (GET)"     "/badges/:type/:package (GET)"  
#> [9] "/badges/:flavor/:package (GET)"
```

## packages

all


```r
cch_pkgs(limit = 1)
#> $found
#> [1] 14463
#> 
#> $count
#> [1] 1
#> 
#> $offset
#> [1] 0
#> 
#> $error
#> NULL
#> 
#> $data
#>       _id package
#> 1 localIV localIV
#>                                                                 url
#> 1 https://cloud.r-project.org/web/checks/check_results_localIV.html
#>   summary.any summary.ok summary.note summary.warn summary.error
#> 1       FALSE         12            0            0             0
#>   summary.fail
#> 1            0
#>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          checks
#> 1 r-devel-linux-x86_64-debian-clang, r-devel-linux-x86_64-debian-gcc, r-devel-linux-x86_64-fedora-clang, r-devel-linux-x86_64-fedora-gcc, r-devel-windows-ix86+x86_64, r-patched-linux-x86_64, r-patched-solaris-x86, r-release-linux-x86_64, r-release-windows-ix86+x86_64, r-release-osx-x86_64, r-oldrel-windows-ix86+x86_64, r-oldrel-osx-x86_64, 0.2.1, 0.2.1, 0.2.1, 0.2.1, 0.2.1, 0.2.1, 0.2.1, 0.2.1, 0.2.1, 0.2.1, 0.2.1, 0.2.1, 2.11, 1.72, 0, 0, 7, 1.88, 0, 2.07, 9, 0, 3, 0, 41.42, 27.66, 0, 0, 74, 40.4, 0, 40.86, 70, 0, 71, 0, 43.53, 29.38, 51.02, 50.2, 81, 42.28, 80.2, 42.93, 79, 0, 74, 0, OK, OK, OK, OK, OK, OK, OK, OK, OK, OK, OK, OK, https://www.R-project.org/nosvn/R.check/r-devel-linux-x86_64-debian-clang/localIV-00check.html, https://www.R-project.org/nosvn/R.check/r-devel-linux-x86_64-debian-gcc/localIV-00check.html, https://www.R-project.org/nosvn/R.check/r-devel-linux-x86_64-fedora-clang/localIV-00check.html, https://www.R-project.org/nosvn/R.check/r-devel-linux-x86_64-fedora-gcc/localIV-00check.html, https://www.R-project.org/nosvn/R.check/r-devel-windows-ix86+x86_64/localIV-00check.html, https://www.R-project.org/nosvn/R.check/r-patched-linux-x86_64/localIV-00check.html, https://www.R-project.org/nosvn/R.check/r-patched-solaris-x86/localIV-00check.html, https://www.R-project.org/nosvn/R.check/r-release-linux-x86_64/localIV-00check.html, https://www.R-project.org/nosvn/R.check/r-release-windows-ix86+x86_64/localIV-00check.html, https://www.R-project.org/nosvn/R.check/r-release-osx-x86_64/localIV-00check.html, https://www.R-project.org/nosvn/R.check/r-oldrel-windows-ix86+x86_64/localIV-00check.html, https://www.R-project.org/nosvn/R.check/r-oldrel-osx-x86_64/localIV-00check.html
#>   check_details             date_updated
#> 1            NA 2019-06-06T15:02:28.681Z
```

by name


```r
x <- cch_pkgs(c("geojsonio", "leaflet", "MASS"))
lapply(x, "[[", c("data", "summary"))
#> [[1]]
#> [[1]]$any
#> [1] TRUE
#> 
#> [[1]]$ok
#> [1] 8
#> 
#> [[1]]$note
#> [1] 4
#> 
#> [[1]]$warn
#> [1] 0
#> 
#> [[1]]$error
#> [1] 0
#> 
#> [[1]]$fail
#> [1] 0
#> 
#> 
#> [[2]]
#> [[2]]$any
#> [1] TRUE
#> 
#> [[2]]$ok
#> [1] 11
#> 
#> [[2]]$note
#> [1] 1
#> 
#> [[2]]$warn
#> [1] 0
#> 
#> [[2]]$error
#> [1] 0
#> 
#> [[2]]$fail
#> [1] 0
#> 
#> 
#> [[3]]
#> [[3]]$any
#> [1] FALSE
#> 
#> [[3]]$ok
#> [1] 12
#> 
#> [[3]]$note
#> [1] 0
#> 
#> [[3]]$warn
#> [1] 0
#> 
#> [[3]]$error
#> [1] 0
#> 
#> [[3]]$fail
#> [1] 0
```

## maintainers

all


```r
cch_maintainers(limit = 1)
#> $found
#> [1] 7916
#> 
#> $count
#> [1] 1
#> 
#> $offset
#> [1] 0
#> 
#> $error
#> NULL
#> 
#> $data
#>                      _id                  email             name
#> 1 f.briatte_at_gmail.com f.briatte_at_gmail.com Francois Briatte
#>                                                                                url
#> 1 https://cloud.r-project.org/web/checks/check_results_f.briatte_at_gmail.com.html
#>                           table
#> 1 ggnetwork, FALSE, 12, 0, 0, 0
#>                                                                             packages
#> 1 ggnetwork, https://cloud.r-project.org/web/checks/check_results_ggnetwork.html, NA
#>               date_updated
#> 1 2019-04-03T12:01:43.690Z
```

by name


```r
cch_maintainers(c("maelle.salmon_at_yahoo.se", "13268259225_at_163.com"))
#> [[1]]
#> [[1]]$error
#> NULL
#> 
#> [[1]]$data
#> [[1]]$data$`_id`
#> [1] "maelle.salmon_at_yahoo.se"
#> 
#> [[1]]$data$email
#> [1] "maelle.salmon_at_yahoo.se"
#> 
#> [[1]]$data$name
#> [1] "Maëlle Salmon"
#> 
#> [[1]]$data$url
#> [1] "https://cloud.r-project.org/web/checks/check_results_maelle.salmon_at_yahoo.se.html"
#> 
#> [[1]]$data$table
#>       package   any ok note warn error
#> 1   geoparser FALSE 12    0    0     0
#> 2 monkeylearn  TRUE  7    5    0     0
#> 3    opencage FALSE 12    0    0     0
#> 4        riem FALSE 12    0    0     0
#> 5     ropenaq FALSE 12    0    0     0
#> 6 rtimicropem  TRUE  6    6    0     0
#> 
#> [[1]]$data$packages
#>       package
#> 1   geoparser
#> 2 monkeylearn
#> 3    opencage
#> 4        riem
#> 5     ropenaq
#> 6 rtimicropem
#>                                                                     url
#> 1   https://cloud.r-project.org/web/checks/check_results_geoparser.html
#> 2 https://cloud.r-project.org/web/checks/check_results_monkeylearn.html
#> 3    https://cloud.r-project.org/web/checks/check_results_opencage.html
#> 4        https://cloud.r-project.org/web/checks/check_results_riem.html
#> 5     https://cloud.r-project.org/web/checks/check_results_ropenaq.html
#> 6 https://cloud.r-project.org/web/checks/check_results_rtimicropem.html
#>     check_result version
#> 1         OK, 12      NA
#> 2 NOTE, OK, 5, 7      NA
#> 3         OK, 12      NA
#> 4         OK, 12      NA
#> 5         OK, 12      NA
#> 6 NOTE, OK, 6, 6      NA
#> 
#> [[1]]$data$date_updated
#> [1] "2019-04-03T12:01:43.725Z"
#> 
#> 
#> 
#> [[2]]
#> [[2]]$error
#> NULL
#> 
#> [[2]]$data
#> [[2]]$data$`_id`
#> [1] "13268259225_at_163.com"
#> 
#> [[2]]$data$email
#> [1] "13268259225_at_163.com"
#> 
#> [[2]]$data$name
#> [1] "Xiao-Ping You"
#> 
#> [[2]]$data$url
#> [1] "https://cloud.r-project.org/web/checks/check_results_13268259225_at_163.com.html"
#> 
#> [[2]]$data$table
#>   package  any ok note warn error
#> 1    XHWE TRUE  0   12    0     0
#> 
#> [[2]]$data$packages
#>   package                                                            url
#> 1    XHWE https://cloud.r-project.org/web/checks/check_results_XHWE.html
#>   check_result version
#> 1         NULL      NA
#> 
#> [[2]]$data$date_updated
#> [1] "2019-04-03T12:01:43.983Z"
```

## Meta

* Please [report any issues or bugs](https://github.com/ropenscilabs/cchecks/issues).
* License: MIT
* Get citation information for `cchecks` in R doing `citation(package = 'cchecks')`
* Please note that this project is released with a [Contributor Code of Conduct](CODE_OF_CONDUCT.md). By participating in this project you agree to abide by its terms.

[docs]: https://cranchecks.info/docs
