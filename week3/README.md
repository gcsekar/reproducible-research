# Reproducible Research - Week 3 Notes
Chandrasekar Ganesan  
March 6, 2017  



## Communicating Results

**tl;dr**

* People are busy, especially managers and leaders

* Results of data analyzes are sometimes presented in oral form, but often the first cut is presented via email

* It is often useful to breakdown the results of an analysis into different levels of granularity / detail
  
* Getting responses from busy people: http://goo.gl/sJDb9V

## Hierarchy of Information: Research Paper

* Title/Author

* Abstract

* Body/Results

* Supplementary Materials / the gory details

* Code / Data / really gory details

## Hierarchy of Information: Email Presentation

> Subject Line / Sender Info

* At a minimum; include one

* Can you summarize findings in one sentence ?

> Email body

* A brief description of the problem / context; recall what was proposed and executed; summarize findings / results; 1-2 paragraphs

* If action needs to be taken as a result of this presentation, suggest some options and make them as concrete as possible

* If questions need to be addressed, try to not make them yes / no

> Attachment(s)

* R Markdown file

* knitr report

* Stay concise; don't spit out pages of code (because you used knitr we know it's available)

> Links to Supplementary Materials

* Code / Software / Data

* Github repository / Project web site

## RPubs

Refer - http://rpubs.com 

Create a free account and you can publish the R Markdown files.

## Reproducible Research Checklist

> Do: Start with Good Science

* Garbage in, garbage out

* Coherant, focused questions simplifies many problems

* Working with good collaborators reinforces good practices

* Something that's interesting to you will (hopefully) motivate good habits

> DON'T: Do Things By Hand

* Editing spreadsheets to data to "clean it up" 

* - Removing outlines

* - QA / QC

* - Validating

* Editing tables or Figures (e.g. rounding, formatting)

* Downloading data from a web site (cliking links in a web browser)

* Moving data around your computer; splitting / reformatting data files

* "We're just doing this once ..."

Things done by hand to be precisely documented (this is harder than it sounds)

> Don't: Point and Click

* Many data processing / statistical analysis package have graphical user interface (GUIs)

* GUIs are convenient / intutive but the actions you take with a GUI can be difficult for others to reproduce

* Some GUIs produce a log file or script which includes equivalent commands; these can be saved for later examination

* In general, be careful with data analysis software that is highly *interactive*; ease of use can sometime lead to non-reproducible analysis

* Other interactive software, such as text editors, are usually fine

> DO: Teach a Computer

* If something needs to be done as part of analysis / investigation, try to teach you computer to do it (even if you only need to do it once)

* In order to give your computer instuctions, you eed to write down exactly what you mean to do and how it should be done

* Teaching a computer almost guarantees reproducibility

For example, by hand you can:

1) Go to the UCI Machine Learning Repository at http://archive.ics.uci.edu/ml

2) Download the Bike Sharing Datasheet by clicking on the link to the Data Folder, then clicking on the link to the zip file of dataset, and choosing "Save Linked File As ..." and then saving it to a folder on your computer.

**OR**

You can teach your computer to do the same thing using R:


```r
download.file("http://archive.ics.uci.edu/ml/machine-learning-databases/00275/Bike-Sharing-Dataset.zip", "ProjectData/Bike-Sharing-Dataset.zip")
```

Notice here that:

* The full URL to the dataset file is specified (no clicking through  a series of links)

* The name of the file saved to your local computer is specified

* The directory in which file was saved is specified ("ProjectData")

* Code can always be executed in R (as long as the link is available)

> DO: Use Some Version Control

* Slow things down

* Add changes in small chunks (don't just do one massie commit)

* Track / tag snapshots; revert to old versions

* Software like Github / Bitbucket / SourceForge make it easy to publish results

> DO: Keep track of Your Software Environment

* If you work on a complex project involving many tools / datasets, the software and computing environment can be critical for reproducing your analysis.

* **Computer architecture** - CPU (Intel, AMD, ARM), GPUs

* **Operating System** - Windows, Linus / Unix, Mac OS

* **Software toolchain** - Compilers, interpreters, command shell, programming languages (C, Perl, Python, etc.), database backends,, data analysis software

* **Supporting software / infrastructure** - Libraries, R Packages, dependencies

* **External dependencies** - Web sites, data repositories, remote database, software repositories

* **Version numbers** - Ideally for everything (if available)


```r
sessionInfo()
```

```
## R version 3.3.2 (2016-10-31)
## Platform: x86_64-w64-mingw32/x64 (64-bit)
## Running under: Windows 10 x64 (build 14393)
## 
## locale:
## [1] LC_COLLATE=English_United States.1252 
## [2] LC_CTYPE=English_United States.1252   
## [3] LC_MONETARY=English_United States.1252
## [4] LC_NUMERIC=C                          
## [5] LC_TIME=English_United States.1252    
## 
## attached base packages:
## [1] stats     graphics  grDevices utils     datasets  methods   base     
## 
## loaded via a namespace (and not attached):
##  [1] backports_1.0.5 magrittr_1.5    rprojroot_1.2   tools_3.3.2    
##  [5] htmltools_0.3.5 yaml_2.1.14     Rcpp_0.12.9     stringi_1.1.2  
##  [9] rmarkdown_1.3   knitr_1.15.1    stringr_1.2.0   digest_0.6.12  
## [13] evaluate_0.10
```

> DON'T: Save Output

* Avoid saving data analysis output (tables, figures, summaries, processed data, etc.), except perhaps temporarily for efficiency purposes

* If a stray output file cannot be easily connected with the means by which it was created, then it is not reproducible

* Save the data + code that generated the output, rather than the output itself

* Intermediate files are okay as long as there is clear documentation of how they were created

> DO: Set Your Seed

* Random number generators generate pseudo-random numbers based on an initial seed (usually a number of set of numbers)

* - In R you can use the **set.seed()** function to set the seed and to specify the random number generator to use

* Setting the seed allows for the stream of random numbers to be exactly reproducible

* Whenever you generate random numbers for a non-trivial purpose, **always set the seed**
