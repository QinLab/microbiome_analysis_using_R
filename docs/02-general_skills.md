# General Skills

The completion of any project in R, microbiome focused or not, will benefit from some basic knowledge of a few tools developed by the R community to help document and expedite your work. This book is not meant to be a replacement for the tremendous number of R tutorials and Workshops currently available (see references for a few recommendations). The reality is that to become proficient at using R will likely take you much longer than you expect. R is a fully developed software language, and like human language, takes many years of immersion to fully develop proficiency.

That being said, with some limited focus on learning, and with the aid of useful tools and an active support community, even a novice can complete a large number of basic analysis and should not shy away from working with R if their project would benefit from the packages, statistics or plotting made available through R.

Below are several brief introductions to working efficiently and effectively with R. The topics have been selected to target the microbiome specific topics throughout this book, but are limited in scope. Links are provided for each topic if you wish to expand your knowledge further.

## Integrated Development Environment (IDE)

An [Integrated Development Environment](https://en.wikipedia.org/wiki/Integrated_development_environment) (IDE) is a term used by software developers to describe a comprehensive software toolbox for completing projects. An IDE it is single software package which pulls together all of the resources one needs to take a project from beginning to end. So imagine if Microsoft Office had a single software called the Microsoft IDE which combined Word, Excel and PowerPoint into a single software package. This would enable you to document, calculate and present your work all from one piece of software instead of working with them independently.

R has several IDE options. The material in this book will focus on one, [RStudio](https://www.rstudio.com) which is continually supported, updated and tightly integrated with a number of useful R tools. However, there are other several other options listed below. Of note, you do not need an IDE to work with R. In fact, R can be run entirely from the command line which is useful for scripting workflows.

### List of popular R IDEs

* [RStudio](https://www.rstudio.com)
* [Microsoft Visual Studio](https://www.rstudio.com)
* [IntelliJ Plug In](https://plugins.jetbrains.com/plugin/6632-r-language-support)
* [Rattle](http://rattle.togaware.com)
* [StatET Plug In for Eclipse](http://www.walware.de/goto/statet)

The value of using an IDE for R can not be overstated. A well-developed IDE, such as RStudio will enable you to work seamlessly with your data, manage your packages and document and publish your work either as a static document or to a web-site.

<div class="figure" style="text-align: center">
<img src="figures/ch02_rstudio.png" alt="R Studio in Action" width="1280" />
<p class="caption">(\#fig:Figure-1)R Studio in Action</p>
</div>

RStudio is a popular IDE for several reasons. First, it can be run as a server from a cloud based or local server ([RStudio Server](https://www.rstudio.com/products/rstudio-server/)). This is useful if you want to have a number of people in a group work with a single installation or if you need the computing resources available in server/cloud hardware. Second, it provides a friendly front-end to access the R language. Being able to visualize code, files and plots in a single window is incredibly useful for exploring data. Third, it is tightly integrated with a number of useful tools such as [RMarkdown](http://rmarkdown.rstudio.com) for documenting your work or [Shiny](https://shiny.rstudio.com) for making interactive analysis documents and [many more useful tools](https://www.rstudio.com/products/rpackages/).

This book was written in RStudio using [Bookdown](https://github.com/rstudio/bookdown). All of the analysis and figures were completed within RStudio as well. You can reproduce all of the analysis using RMarkdown documents. All of this was made much simpler due to the tight integration of these packages within RStudio.

## Packages

The concept of *packages* has been brought up throughout this book already. Put simply, a package can be thought of as an app for analysis. Packages are developed by people from various research communities and deposited either into the official R package repository [CRAN](https://cran.r-project.org) or in curated, discipline specific repositories such as [Bioconductor](http://bioconductor.org). More recently a large number of packages are being hosted on [Github](http://github.com).

Between CRAN, Bioconductor and Github you should be pretty well-covered in package discovery and installation. There are slightly different ways to install packages from each resource:

**CRAN:** There are two ways to install packages from CRAN in RStudio. The first way is from the *Packages* tab which you will see at the top of one of the panes in RStudio:

<div class="figure" style="text-align: center">
<img src="./figures/ch02_rstudio_install_packages.png" alt="Package Installation Tab" width="200" />
<p class="caption">(\#fig:Figure-2)Package Installation Tab</p>
</div>

The other way is to use the *install.packages* command from the console. For example, the following code will install the *ade4* package.


```r
install.packages("ade4")
```

**Bioconductor:** Installing packages from Bioconductor requires you to first install Bioconductor using the following commands:


```r
## try http:// if https:// URLs are not supported
source("https://bioconductor.org/biocLite.R")
biocLite()
```

Once bioconductor installs you can install specific libraries. The following command will install the *PhyloSeq* package which is used extensively in this book.


```r
## try http:// if https:// URLs are not supported
source("https://bioconductor.org/biocLite.R")
biocLite("phyloseq")
```

**Github:** To install packages from Github you first have to install *Developer Tools*. The following series of commands would install Developer Tools and then install *ggplot2* from it's Github repository:


```r
install.packages("devtools")
devtools::install_github("tidyverse/ggplot2")
```

If everything goes smoothly the package will be installed and is ready to use. There can be some package specific issues such as the requirement for a dependency which you may need to read further documentation on at the package web site or by contacting the package author.

Once you have a package installed you need to load it using the *library* function in R. Again, this can be done two ways. The first is by checking the box next to the library in the package tab shown in Figure 2. The second is using the *library* command in the console.


```r
library(ggplot2)
packageVersion("ggplot2")
```

```
## [1] '2.2.1.9000'
```

The above command will load the ggplot2 package into the current R session and is followed by a second command which will display the library version. Tracking library versions can be useful for reproducing and sharing code so it is a good habit to get into. Although it may seem tedious now, we will see how we can leverage RMarkdown documents to facilitate library loading and versioning.

## R Markdown

[RMarkdown](http://rmarkdown.rstudio.com) is a software package integrated into RStudio which facilitates documentation and reproducibility of your work. RMarkdown documents can be shared with colleageus or published on-line facilitating collaboration and open data sharing.

While there are some nuances to R Markdown documents there are three key principles you should understand before diving in. Once you understand the basics, you can extend your knowledge using the official [R Markdown](http://rmarkdown.rstudio.com/index.html) documentation.

**Principle 1: Formatting**

[R Markdown](http://rmarkdown.rstudio.com/index.html) is based on the original [Markdown](http://daringfireball.net/projects/markdown/) tool which was designed to provide a simple syntax for writing documents for the web. This simple, code based format makes for an unobstructive writing environment. Formatting is done with mark-up codes instead of using functions in a word processor which makes it easy for other software such as web-browsers or [knitr](https://yihui.name/knitr/) (disussed below) to dissect and recompile into html or PDF documents.

There are a lot of codes available to customize the format of your text (see: [The R Markdown Reference Guide](https://www.rstudio.com/wp-content/uploads/2015/03/rmarkdown-reference.pdf)), but you don't need to memorize all of them to get started. Some basics will be sufficient for getting started.

* *italics* are displayed by surrounding the word with single asterisks (\*word\*).

* **bold** a word with double asterisks (\*\*word\*\*)

Most importantly, any text you write **outside** of a chunk (described below) is just text. It doesnt do anything at all other than act as plain text. So the areas outside of chunks should be used for exposition and documentation of your analysis.

**Principle 2: The Chunk**

[R Code Chunks](http://rmarkdown.rstudio.com/authoring_rcodechunks.html) are the real heartbeat of R Markdown documents. Contrary to all of the text outside of an R chunk, text within a R code chunk is treated as code to process analysis, calculate statistics, or generate plots. The basis of a chunk are three backticks and an r in squigly brackets (\`\`\`\{r\}) to start the chunk and three backticks (```) to end it. For example:


```r
# This is an example R chunk
```

Everything in between the R chunk identifiers will be run when the entire chunk is run. It is useful to break each step of your analysis into individual chunks. For example, if you want to load a set of libraries at the start of your R analysis you may do something like the following:


```r
# Load libraries
library("ggplot2")
packageVersion("ggplot2")
library("phyloseq")
packageVersion("phyloseq")
library("magrittr")
packageVersion("magrittr")
library("RColorBrewer")
packageVersion("RColorBrewer")
library("vegan")
packageVersion("vegan")
library("gridExtra")
packageVersion("gridExtra")
library("knitr")
packageVersion("knitr")
library("dplyr")
packageVersion("dplyr")
library("DESeq2")
packageVersion("DeSeq2")
library("plotly")
packageVersion("plotly")
```

All of the commands in this chunk can be run by running the entire chunk. There are options for running the current chunk, all chunks, current line of the chunk and more available at the top of the menu under the *run* tab. It will be worth your time to learn the key bindings for running chunks as you will be regularly updating and rerunning chunks as you work.

You will notice that there are parts of the chunk that start with the # symbol. This is how you tell the R Markdown chunk **not** to run something. So while # Load libraries will be displayed when it is run, due to the # symbol R knows not to process this as a command. This is an additional way to document your code and should be used liberally throughout your R Markdown document creation.

**Principle 3: Publishing**

Once you know some basics about formatting text and creating R chunks you can combine these two skills to produce reports as either PDF, HTML or Word. Other document types are available as well through other packages, but these three formats are standard.

Report generation is completed by *knit*ing your R Markdown document. This is done using the *knit* button at the top of the R Markdown pane. The processing from R Markdown to another format is done by the [knitr](https://yihui.name/knitr/) package. Knitr provides a number of options for customizing how your reports appear. Many of these options are placed in the R chunk header. For example, the following header will tell knitr to exclude the R chunk from the final document, but to go ahead and run it as part of your analysis. This is useful for sharing reports with collaborators who may not be interested in some of the intermediate analysis that goes along with an analysis. You can also specify figure height and width amongst other things.

You should also name your R chunks to keep them straight. Naming a chunk is easy as it is just any text that appears after the r and before a comma. The name of the following R chunk is *Example R chunk*.



```r
# This R chunk will print a summary of the cars example data set
# It will also generate a scatterplot of the cars data.
summary(cars)
```

```
##      speed           dist       
##  Min.   : 4.0   Min.   :  2.00  
##  1st Qu.:12.0   1st Qu.: 26.00  
##  Median :15.0   Median : 36.00  
##  Mean   :15.4   Mean   : 42.98  
##  3rd Qu.:19.0   3rd Qu.: 56.00  
##  Max.   :25.0   Max.   :120.00
```

```r
plot(cars)
```

<img src="02-general_skills_files/figure-html/Example R chunk-1.png" width="288" />

There are a number of interesting ways to publish or share your work from R Studio including geneating web sites or interactive notebooks. This book will not detail them further, but more information can be found using the links below:

* [RPubs](https://rpubs.com): Free, simple R Markdown sharing service.
* [R Notebooks](http://rmarkdown.rstudio.com/r_notebooks.html#overview): Interactive, portable R Markdown documents.
* [Shiny](http://rmarkdown.rstudio.com/authoring_shiny.html). Publish interactive documents which accept user input.
* [R Markdown Web sites](http://rmarkdown.rstudio.com/rmarkdown_websites.html): HTML versions of your R Markdown documents with additional features.
* [bookdown](https://bookdown.org/yihui/bookdown/): Used to generate this book
* [R presentations](https://support.rstudio.com/hc/en-us/articles/200486468-Authoring-R-Presentations). Make slide decks directly in R Studio
