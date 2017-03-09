# Reproducible Research - Week 4 Notes
Chandrasekar Ganesan  
March 9, 2017  


## The Cacher package for R

* Add-on package for R

* Evaluates code writtenin files and stores intermediate results ina  key-value database

* R expressions are given SHA-1 hash value so that changes can be tracked and code reevaluated if necessary

* "Cacher Packages" can be built for distribution

* Others can "clone" an analysis and evaluate susbets of code or inspect data objects

## Using cacher as an Author

* Parse the R source file; Create the necessary cache  directories and subdirectories

* Cycle through each expression in the source file:

  - If an expression has never been evaluated, evaluate it and store any resulting R objects in the cache database
  
  - If a cached resut exists, lazy-load the results from the cache database and dmove to the next expression
  
  - If an expression does not create any R onjects (i.e., there is nothing to cache), add the expression to the list of expressions where evaluation needs to be forced
  
  - Write out metadata for this expression to the metadata file
  
* The cachepackage function creates a cacher package storing

  - Source file
  
  - Cached data objects
  
  - Metadata

* Package file zipped and can be distributed

* Readers can unzip the file and immediately investigate its contents via cacher package

## Using cacher as a Reader

A journal article says

> *"..the code and data for this analysis can be found in the cachcel package 092dcc7dda4b93e42f23e038a60e1d44dbec7b3f"*


```r
library(cacher)
clonecache(id = "092dcc7dda4b93e42f23e038a60e1d44dbec7b3f")
clonecache(id = "092d")   ## Same as above

showFiles()
[1] "top20.R"

soourceFile("top20.R")
```

## Cloning an Analysis

* Local directories are created

* Source code files and metadata are downloaded

* Data objects are not downloaded by default

* References to data objects are loaded and corresponding data can be lazy-loaded on demand

## Examining Code

> >code()
> source file: top20.R


```r
cities <- readLines("citylist.txt")
classes <- readLines("colClasses.txt")
vars <- c("date","dow","death")
data <- lapply(cities, function(city){
  names(data) <- cities
  estimates <- sapply(data, function(city){
    effect <- weighted.mean(estimates[,1])
    stderr <- sqrt(1/sum(1/estimates[,2]))
  })
})

graphCode()
```

## Training Code  Backwards

> objectcode("data")


```r
cities <- readLines("citylist.txt")
classes <- readLines("colClasses.txt")
vars <- c("date","dow","death")
data <- lapply(cities, function(city){
  names(data) <- cities
  estimates <- sapply(data, function(city){
    effect <- weighted.mean(estimates[,1])
    stderr <- sqrt(1/sum(1/estimates[,2]))
  })
})

graphCode()
```

## Running Code

* The * runcode * function executed code in the source file

* By default, expressions that results in an object being created are *not* run and the results objects is lazy-loaded into the workspace

* Expressions not resulting in objects are evaluated.

## Check Code and Objects

* The *checkcode* function evaluates all expressions from scratch (no lazy-loading)

* Results of evaluation are checked against stored results to see if the results are the same as what the author calculated

  - Settinig random number generated (RNG) seeds is critical for this to work

* The integrity of data objects can be verified with the checkobjects function to check for possible corruption fo data (i.e., in transit)

## Inspecting Data Objects

* loadcache()

Loads all the objects in cache

* ls()

lists alll the objects in cache

user can then print and evaluate objects as appropriate




