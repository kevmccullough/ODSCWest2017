<!-- README.md is generated from README.Rmd. Please edit that file -->
Materials for:

#### [Modeling big data with R, sparklyr, and Apache Spark](https://conferences.oreilly.com/strata/strata-ca/public/schedule/detail/55791)

    Thursday Nov 2 2017,
    2:00 PM,
    Room T2,
    "Modeling big data with R, Sparklyr, and Apache Spark""
    Workshop/Training intermediate, 4 hours,
    by Dr. John Mount ( [link](https://odsc.com/training/portfolio/succeeding-big-data-real-world) ).

We have a short video showing how to install [Spark](http://spark.apache.org) using [R](https://cran.r-project.org) and [RStudio](https://www.rstudio.com) [here](https://youtu.be/qnINvPqcRvE).

Also please click through for slides from Edgar Ruiz's excellent [Strata Sparklyr presentation](https://conferences.oreilly.com/strata/strata-ca/public/schedule/detail/55800) and [cheat-sheet](http://spark.rstudio.com/images/sparklyr-cheatsheet.pdf).

#### Who is this presentation for?

Data scientists, data analysts, modelers, R users, Spark users, statisticians, and those in IT

#### Prerequisite knowledge

##### Basic familiarity with R

Experience using the [dplyr](https://CRAN.R-project.org/package=dplyr) R package (If you have not used dplyr before, please read this chapter before coming to class.) Materials or downloads needed in advance.

A WiFi-enabled laptop (You'll be provided an [RStudio Server Pro](https://www.rstudio.com/products/rstudio-server-pro/) login for students to use on the day of the workshop.)

##### What you'll learn

Learn how to quickly set up a local Spark instance, store big data in Spark and then connect to the data with R, use R to apply machine-learning algorithms to big data stored in Spark, and filter and aggregate big data stored in Spark and then import the results into R for analysis and visualization Understand how to extend R and use [sparkly](http://spark.rstudio.com)) to access the entire Spark API

### Description

Sparklyr, developed by RStudio in conjunction with IBM, Cloudera, and [H2O](http://www.h2o.ai), provides an R interface to Spark’s distributed machine-learning algorithms and much more. Sparklyr makes practical machine learning scalable and easy. With sparklyr, you can interactively manipulate Spark data using both dplyr and SQL (via DBI); filter and aggregate Spark datasets then bring them into R for analysis and visualization; orchestrate distributed machine learning from R using either Spark MLlib or H2O SparkingWater; create extensions that call the full Spark API and provide interfaces to Spark packages; and establish Spark connections and browse Spark data frames within the RStudio IDE.

John Mount demonstrates how to use sparklyr to analyze big data in Spark, covering filtering and manipulating Spark data to import into R and using R to run machine-learning algorithms on data in Spark. John also also explores the sparklyr integration built into the RStudio IDE.

Derived from ["Modeling big data with R, sparklyr, and Apache Spark" Strata Hadoop 2017]().

Public repository is: [https://github.com/WinVector/BigDataRStrata2017](https://github.com/WinVector/ODSCWest2017/tree/master/SparklyRMachineLearning).

###### config

``` r
update.packages(ask = FALSE, checkBuilt = TRUE)
```

Current list of CRAN packages used:

``` r
# often a good idea, though try "n" to build source
# may interfere with us pinning h2o to a specific version
# update.packages(ask=FALSE) 
cranpkgs <- c(
  'DBI', 'RCurl', 'RSQLite', 'WVPlots', 'babynames', 'caret', 'cdata',
  'dbplyr', 'devtools', 'dplyr', 'dygraphs', 'e1071', 'formatR',
  'ggplot2', 'h2o', 'jsonlite', 'lubridate', 
  'nycflights13', 'plotly', 'rbokeh', 'replyr', 'rsparkling', 'sigr',
  'sparklyr', 'statmod', 'tidyr', 'tidyverse', 'titanic',
  'xtable' )
install.packages(cranpkgs)
sparklyr::spark_install(version = "2.2.0", hadoop_version = "2.7")
```

``` r
devpkgs <- c(
  'RStudio/EDAWR',
  'WinVector/replyr')
for(pkgi in devpkgs) {
  devtools::install_github(pkgi)
}
```

Also it is critical to look at [Exercises/solutions/RsparklingExample.Rmd](Exercises/solutions/RsparklingExample.Rmd) as it installs and configures some packages. A refresh of all packages will break the matching version numbers required by `h2o` and `rsparkling`. So please work through the details in `RsparklingExample.Rmd` after updating and installing all the above packages.

A copy of those note are below (but it is better to look at `RsparklingExample.Rmd`).

TODO: check if we can get away without the following re-install (will sparkling just work off the CRAN version).

``` r
# updated from https://gist.github.com/edgararuiz/6453d44a91c85a87998cfeb0dfed9fa9
# The following two commands remove any previously installed H2O packages for R.
if ("package:h2o" %in% search()) { detach("package:h2o", unload=TRUE) }
if ("h2o" %in% rownames(installed.packages())) { remove.packages("h2o") }

# Now we download, install and initialize the H2O package for R.
install.packages("h2o", type = "source", repos = "http://h2o-release.s3.amazonaws.com/h2o/rel-turnbull/2/R")

# Installing 'rsparkling' from CRAN
install.packages("rsparkling")
options(rsparkling.sparklingwater.version = "2.0.3")
# Reinstalling 'sparklyr' 
install.packages("sparklyr")
sparklyr::spark_install(version = "2.0.0")
```

Note: please note using `dplyr::compute()` (or `sparklyr::sdf_checkpoint()`) with `sparklyr` can have issues (see [sparklyr issue 721](https://github.com/rstudio/sparklyr/issues/721)).