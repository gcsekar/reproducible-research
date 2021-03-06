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

> Summary: Checklist

* Are we doing good science?

* Was any part of the analysis done by hand

 - If so, are those precisely documented?
 
 - Does the documentation match reality?
 
* Have we taught the computer to do as much as possible (i.e. coded) ?

* Are we using version control system?

* Have we documented our software environment?

* Have we saved any output that we cannot reconstruct from original data + code ?

* How far back in the analysis pipeline can we go before our results are no longer (automatically) reproducible ?


## Evidence Based Data Analysis

### Replication and Reproducibility

> Replication

* Focuses on the validity of the scientific claim

* "Is this claim true"?

* The ultimate standard of strengthening scientific evidence

* New investigators, data analytical methods, laboratories, instruments, etc

* Particularly important in studies that can impact broad policy or regulatory decisions

> Reproducibility

* Focuses on validity of the data analysis

* "Can we trust this analysis"?

* Arguably a minimum standard for any scientific study

* New investigators, same data, same methods

* Important when replication is impossible

### Background and Underlying Trends

* Some studies cannot be replicated: No time, No money, Unique / Opportunistic

* Technology is increasing data collection throughput; data are more complex and high-dimensional

* Existing database can be merged to become bigger databases (but data are used off-label)

* Computing power allows more sophisticated analysis, even on "small" data

* For every fied "X" there is a "Computational X"

### The Result ?

* Even the basic analyses are difficult to describe

* Heavy computational requirements are thrust upon people without adequate training in statistics and computing

* Errors are more easily introduced in the long analysis pipelines

* Knowledge trasfer is inhibited

* Results are difficult to replicate or reproduce

* Complicated analyses cannot be trusted


### What is Reproducible Research ?

Scientific Question -> Protocol -> Nature -> Measured Data -> (Processing Code) -> Analytic Data -> (Analytic Code) -> Computational Results

Computational Results -> Tables or Figures or Numerical Summaries -> (Text) -> Published Article 

### What Problem Does Reproducibility Solve ?

> What we get

* Transparency

* Data Availability

* Software / Methods Availability

* Improved Knowledge Transfer

> What we do  NOT get

* Validity / Correctness of the analysis

An analyses can be reproducible and still be wrong

We want to know "Can we trust this analysis?"

Does requiring reproducibility deter bad analysis?

## Problems with Reproducibility

The promise of reproducible research is that with data/code available, people can check each other and the whole system is self-correcting

* Address the most "downstream" aspect of the research process - post-publication

* Assumes everyone plays by the same rules and want to achieve the same goals (i.e., scientific discovery)

## Who Reproduces Research?

* For reproducibility to be effective as a means to check validity, someone needs to do something

 - Re-run the analysis; check results match
 
 - Check the code for bugs/errors
 
 - Try alternate approaches; check sensitivity
 
* The need for someone to do something is inherited from traditional notion of replication

* Who is "someone" and what are their goals?

## The Story So Far

* Reproducibility brings transparency (wrt code+data) and increased transfer of knowledge

* A lot of discussion about how to get people to share data

* Key question of "can we trust this analysis?" is not addressed by reproducibility

* Reproducibility addresses potential problems long after they've occurred ("downstream")

* Secondary analyses are inevitably coloured by the interests / motivations of others

## Evidence-based Data Analysis

* Most data analyses involve stringing together many different tools and methods

* Some methods may be standard for a given field, but others are often applied ad hoc

* We should apply thoroughly studied (via statistical research), mutually agreed upon methods to analyze data whenever possible

* There should be evidence to justify the application of a given method

***

* Create analytic pipelines from evidence-based component - standarize it

* A Deterministic Statistical Machine - http://goo.gl/Qvlhuv

* Once an evidence-based analytic pipeline is establised, we shouldn't mess with it

* Analysis with a "transparent box"

* Reduce the "researcher degrees of freedom"

* Analogous to pre-specified clinical trial protocol

> Deterministic Statistical Model

**Dataset and Input Metadata -> Preprocessing -> Model Selection -> Sensitivity Analysis -> Report and Output parameters**

* Benchmark Dataset -> Preprocessing
* Benchmark Dataset -> Model Selection
* Benchmark Dataset -> Sensitivity Analysis

* Report -> Method Section or Public Repository



