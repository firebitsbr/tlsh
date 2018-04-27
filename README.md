
# tlsh

Local Sensitivity Hashing Using the ‘Trend Micro’ ‘TLSH’ Implementation

## Description

‘Trend Micro’ provides an open source library
<https://github.com/trendmicro/tlsh/> for local sensitivity hashing.
Methods are provided to compute and compare hashes from character/byte
streams.

## TODO

  - \[ \] File input
  - \[ \] Docs
  - \[ \] Tests

## What’s Inside The Tin

The following functions are implemented:

## Installation

``` r
devtools::install_github("hrbrmstr/tlsh")
```

## Usage

``` r
library(tlsh)

# current verison
packageVersion("tlsh")
```

    ## [1] '0.1.0'

## Example

  - `index.html` is a static copy of a blog main page with a bunch of
    `<div>`s with article snippets
  - `index1.html` is the same file as `index.htmnl` with a changed cache
    timestamp at the end
  - `index2.html` is the same file as `index.html` with one article
    snippet removed
  - `RMacOSX-FAQ.html` is the CRAN ‘R for Mac OS X
FAQ’

<!-- end list -->

``` r
doc1 <- as.character(xml2::read_html(system.file("extdat", "index.html", package="tlsh")))
doc2 <- as.character(xml2::read_html(system.file("extdat", "index1.html", package="tlsh")))
doc3 <- as.character(xml2::read_html(system.file("extdat", "index2.html", package="tlsh")))
doc4 <- as.character(xml2::read_html(system.file("extdat", "RMacOSX-FAQ.html", package="tlsh")))

# generate hashes
 
(h1 <- tlsh_simple_hash(doc1))
```

    ## [1] "B253F9F3168DC8354B2363E2A585771CD25A803BCEA099C1FBED54ACA790EB5B137346"

``` r
(h2 <- tlsh_simple_hash(doc2))
```

    ## [1] "6153E8F3168DC8355B2363E2A585771CD26A803BCEA099C1FBED44AC9790EB5B137346"

``` r
(h3 <- tlsh_simple_hash(doc3))
```

    ## [1] "6443E8F3168DC8355B6262F2A9C5771CD25A802BCEA099C1FBED54AC9780FF4A137346"

``` r
(h4 <- tlsh_simple_hash(doc4))
```

    ## [1] "B8B3A52F93C0233E0F1216576F192FA812FD5C7EA3802188B557C67F8712D9A47666BB"

``` r
# compute distance

tlsh_simple_diff(h1, h2)
```

    ## [1] 7

``` r
tlsh_simple_diff(h1, h3)
```

    ## [1] 18

``` r
tlsh_simple_diff(h1, h4)
```

    ## [1] 334

## Code of Conduct

Please note that this project is released with a [Contributor Code of
Conduct](CONDUCT.md). By participating in this project you agree to
abide by its terms.
