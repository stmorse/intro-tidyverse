# Data wrangling and Visualization in R

This tutorial introduces basic techniques in data wrangling and visualization in R.  Specifically, we will cover some basic tools using out-of-the-box R commands, then introduce the powerful framework of the "tidyverse" (both in wrangling and visualizing data), and finally gain some understanding of the philosophy of this framework to set up deeper exploration of our data.  Throughout, we will be using a publicly available dataset of AirBnB listings.

This was originally presented as part of a month-long course in **Software Tools for Optimization and Analytics** given by the Operations Research Center at MIT.  [Here is a link](http://philchodrow.github.io/cos_2017) to some of the other sessions and notes, if you're interested.


## Pre-assignment 1: Installation

1. Before beginning, ensure you have RStudio installed.  This provides a graphical user interface (GUI) or integrated development environment (IDE) for programming in R, and is free at the [RStudio site](http://www.rstudio.com).  This installation will come with an installation of the base libraries of R itself.

2. Next step, make sure you have the course materials.  The easiest way to ensure you have all the materials for this class is clone this repository.  On a Mac, you can open a Terminal, navigate to a directory of your choice, and run
```
$ git clone https://github.com/stmorse/intro-tidyverse.git
```
Another way is to simply download all the course material as a .zip file (in the "Clone or download" dropdown menu).

These materials are summarized in an easy-to-digest form in the [online session notes](https://stmorse.github.io/intro-tidyverse/master.html).

The materials consist of a script (`script.R`) and corresponding exercises for each section (`exercises.R`).  Maybe the best way to self-teach this material is to open the session notes above in a browser window, and the two R scripts in RStudio, and work your way through them, doing the code yourself, flipping back and forth as necessary.

The R scripts with all code filled in are also provided, in `script_full.R` and `exercises_solved.R`.

(The `master.Rmd` and `master.html` files creating the [online session notes](https://stmorse.github.io/intro-tidyverse/master.html) can be ignored.)

The data is publicly available at [Kaggle](http://kaggle.com) as the [Boston Airbnb dataset](http://kaggle.com/airbnb/boston), but we also provide it in this repository for convenience.


## Pre-assignment 2: Installing libraries

We will use three libraries for this session: `tidyr`, `dplyr`, and `ggplot2`.  Before beginning, ensure that you install them, and are able to load them into an R session in RStudio.  You can install them by executing the following commands in the RStudio console:
```
install.packages('dplyr')
install.packages('tidyr')
install.packages('ggplot2')
```

You should test that the libraries will load by then running
```
library(dplyr)
library(tidyr)
library(ggplot2)
```

Then test that dplyr/tidyr work by executing the command:
```
data.frame(name=c('Ann', 'Bob'), number=c(3.141, 2.718)) %>% gather(type, favorite, -name)
```
which should output something like this
```
      name   type favorite
    1  Ann number    3.141
    2  Bob number    2.718
```

Finally, test that ggplot works by executing the command
```
data.frame(x=rnorm(1000), y=rnorm(1000)) %>% ggplot(aes(x,y)) + geom_point()
```
which should produce a cloud of points centered around the origin.

**Now you're ready to begin!**


## Additional Resources

`dplyr` and `tidyr` are well-established packages within the `R` community, and there are many resources to use for reference and further learning. Some of our favorites are below. 

- Tutorials by Hadley Wickham for `dplyr` [basics](https://cran.rstudio.com/web/packages/dplyr/vignettes/introduction.html), [advanced grouped operations](https://cran.r-project.org/web/packages/dplyr/vignettes/window-functions.html), and [database interface](https://cran.r-project.org/web/packages/dplyr/vignettes/databases.html).
- Third-party [tutorial](http://www.dataschool.io/dplyr-tutorial-for-faster-data-manipulation-in-r/) (including docs and a video) for using `dplyr`
- [Principles](http://vita.had.co.nz/papers/tidy-data.pdf) and [practice](https://cran.r-project.org/web/packages/tidyr/vignettes/tidy-data.html) of tidy data using `tidyr`
- (Detailed) [cheatsheet](https://www.rstudio.com/wp-content/uploads/2015/02/data-wrangling-cheatsheet.pdf?version=0.99.687&mode=desktop) for `dplyr` and `tidyr` 
- A useful [cheatsheet](https://stat545-ubc.github.io/bit001_dplyr-cheatsheet.html) for `dplyr` joins
- [Comparative discussion](http://stackoverflow.com/questions/21435339/data-table-vs-dplyr-can-one-do-something-well-the-other-cant-or-does-poorly) of `dplyr` and `data.table`, an alternative package with higher performance but more challenging syntax.  

Some of the infinitude of visualization subjects we did not cover are: heatmaps and 2D histograms, statistical functions, plot insets, ...  And even within the Tidyverse, don't feel you need to limit yourself to `ggplot`.  Here's a good overview of some [2d histogram techniques](http://www.everydayanalytics.ca/2014/09/5-ways-to-do-2d-histograms-in-r.html), a discussion on [overlaying a normal curve over a histogram](http://stackoverflow.com/questions/5688082/ggplot2-overlay-histogram-with-density-curve), a workaround to fit multiple plots in [one giant chart](http://www.cookbook-r.com/Graphs/Multiple_graphs_on_one_page_(ggplot2)/). 

For other datasets and applications, one place to start is data hosting and competition websites like [Kaggle](http://www.kaggle.com), and there many areas like [sports analytics](http://www.footballoutsiders.com), [political forecasting](http://www.electoral-vote.com/evp2016/Info/data.html), [historical analysis](https://t.co/3WCaDxGnJR), and countless others that have [clean](http://http://www.pro-football-reference.com/), [open](http://www.kdnuggets.com/datasets/index.html), and [interesting](https://www.kaggle.com/kaggle/hillary-clinton-emails) data just waiting for you to `read.csv`. 

