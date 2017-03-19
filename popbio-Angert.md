Background
==========

This exercise consists of a reanalysis of the datasets from Angert (2006). The data is provided as part of the `popbio` package.

First load the library:

``` r
library(popbio)
```

The dataset `monkeyflower` contains the transition rates of 32 populations of two *Mimulus* species, measured over multiple years. For an explanation of the transition rates see Angert (2006).

Here are the first few lines of the data set:

``` r
#Because Rmarkdown knits from a different environment, you need so save the data set first and then read it here. This is not necessary if you are working from the console.
#save(monkeyflower,file="monkeyflower.RData")
load(file="monkeyflower.RData")
head(monkeyflower)
```

    ##      species         site   year    a11 a12  a13  a14      a21    a22
    ## 1 cardinalis Buck Meadows   2000 0.2128   0 2038 9624 2.49e-05 0.0000
    ## 2 cardinalis Buck Meadows   2001 0.1840 376  720 1340 2.14e-05 0.0345
    ## 3 cardinalis Buck Meadows   2002 0.1840   0  144  916 3.93e-06 0.0000
    ## 4 cardinalis Buck Meadows pooled 0.1900 441 1262 3636 2.25e-05 0.0139
    ## 5 cardinalis Rainbow Pool   2000 0.1858   0   77  668 5.76e-05 0.2606
    ## 6 cardinalis Rainbow Pool   2001 0.1859   8  280 1279 2.39e-05 0.1152
    ##      a23    a24      a31    a32    a33    a34      a41    a42    a43
    ## 1 0.0000 0.0000 3.74e-05 0.0000 0.3529 0.5000 8.31e-07 0.0000 0.0588
    ## 2 0.0104 0.0000 2.14e-05 0.2759 0.3229 0.2632 0.00e+00 0.1034 0.1979
    ## 3 0.0000 0.0000 2.23e-05 0.0303 0.3662 0.2069 0.00e+00 0.0000 0.0704
    ## 4 0.0043 0.0000 3.26e-05 0.1250 0.3447 0.3725 3.46e-07 0.0417 0.1191
    ## 5 0.0643 0.0076 1.57e-05 0.0904 0.4143 0.3106 1.16e-06 0.0000 0.0500
    ## 6 0.0051 0.0000 1.66e-05 0.1264 0.3299 0.3205 7.10e-07 0.0028 0.1066
    ##      a44
    ## 1 0.2778
    ## 2 0.3684
    ## 3 0.4483
    ## 4 0.3431
    ## 5 0.4318
    ## 6 0.4872

The first three columns are species, site, and year. The data starting in the fourth column contains the transition rates.

To read the data in matrix form you need to get columns 4 to 19 for a given row. For instance, the data for the first row (*M. cardinalis*, population Buckmeadows, year 2000):

``` r
m1<-matrix(as.numeric(monkeyflower[1,4:19]), byrow=T, nrow=4)
m1
```

    ##           [,1] [,2]      [,3]      [,4]
    ## [1,] 2.128e-01    0 2038.0000 9624.0000
    ## [2,] 2.490e-05    0    0.0000    0.0000
    ## [3,] 3.740e-05    0    0.3529    0.5000
    ## [4,] 8.310e-07    0    0.0588    0.2778

This produces a 4x4 matrix with 16 transition rates.

And from this you can easily conduct the population matrix analyses. For example to get `lambda`:

``` r
lambda(m1)
```

    ## [1] 0.6997406

Analysis over multiple matrices
-------------------------------

Now you can do loops to analyse the properties of the 31 matrices at once.

``` r
temp.res<-data.frame(lambda=rep(NA,32), gentime=rep(NA,32))
for(i in 1:32){
  mattemp<-matrix(as.numeric(monkeyflower[i,4:19]), byrow=T, nrow=4)
  temp.res[i,1]<-lambda(mattemp) 
  temp.res[i,2]<- generation.time(mattemp)
}
par(mfrow=c(1,2))
hist(temp.res$gentime, breaks=10, main="Generation time", xlab="Generation time")
hist(temp.res$lambda, breaks=10, main="lambda", xlab="lambda")
```

![](popbio-Angert_files/figure-markdown_github/loops-1.png)
