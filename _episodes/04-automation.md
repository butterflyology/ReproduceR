---
title: "Automation"
teaching: 120
exercises: 30
questions:
- "What is code automation?"
- "How can automation help?"
objectives:
- "Learn the use of RStudio and functions for project automation."
keypoints:
- "Code automation is an important part of reproducible research"
---

> ## Prerequisites
> Installation of R and RStudio:
> - Download R from [CRAN](https://cran.r-project.org/)
> - Download [RStudio](https://www.rstudio.com/products/rstudio/download/)
> - Install the following R packages:
  - `tidyverse`
  - `testthat`
  - `rmarkdown` and `knitr` (in RStudio pushing the knit HTML button the first time will prompt to have these packages installed)
- Distribute a Zip file that only contains the content of the example-manuscript folder from this repository.
- Explain what the handout file contains
{: .prereq}

## Introduction to automation
> "Reproduciibilty is actually all about being as lazy as possible!"
>
> -- Hadley Wickham (via [Twitter](https://twitter.com/hadleywickham/status/598532170160873472), 2015-05-03)

## Disclaimer
Depending on your previous experience with knitr, this lesson might seem too advanced as it provides ways to deal with annoyances you can face when you try to use knitr with a large project. If you have never used knitr before this is a good opportunity to learn efficient practices right away.

The main goal of this lesson is to teach you some tips and tricks that will make your life easier with knitr if you are using it in the context of a research project that involves multiple sources of raw data that are combined to create multiple intermediate datasets that are themselves combined to generate figures and tables.

You certainly don't need to adopt all of these practices at once. Start small. Maybe with only one dataset, one figure first, and later learn how to use Make, and then Travis. None of these tools are exceedingly hard to learn or to grasp, but trying to learn everything at once might feel overwhelming. However, in the process of learning these tools, you will learn skills that you will be able to translate into other components of your research. For instance, if you are interested in learning how to write a package in R, many of the advice and tools included in this lecture will greatly help you to get started. If you start using Make and Travis, you will learn some basics of UNIX and Linux which are general useful skills to have if you are interested in analyzing large datasets (e.g., set up runs on an HPC cluster).

## The issue(s)
`knitr` allows you to mix code and prose, which is wonderful and very powerful, but can be difficult to manage if you don't have a good plan to get organized. The challenge with working in this reproducible framework is that you end up developing your analysis at the same time as you are writting your manuscript and refining your ideas, adjusting the aim of your paper, deciding on the data you are going to include, etc. It's therefore important that you have a modular framework in place where each section of your analysis can be self-contained so you don't depend on a linear script that will not reflect the complexity of your analysis.

## A solution
IMAGE

In this lesson, I will demonstrate how to write your own functions to generate the clean version of your data, your figures, your tables and your manuscript. Having all the content of your manuscript as a function will greatly facilitate the upkeep of your manuscript as it forces to be organized. It also comes with some benefits:

1. Modularity
1. Less variables
1. Better documentation
1. Testing

## Modularity

By breaking down your analysis into functions, you end up with blocks of code that can interact and depend on each others in explicit ways. It allows you to avoid repeating yourself, and you will be able to re-use the functions you create for other projects more easily than if your paper only contains scripts.

## Fewer variables to worry about to focus on the important stuff

If your manuscript only contains scripts, you are going to accumulate many variables in your document and you are going to have to worry about avoiding name conflicts among all these temporary variables that store intermediate versions of your datasets but won't need in your analysis. By putting everything into functions, these variables will be hidden from your global environment and you can focus on the important stuff: the inputs and the outputs of your workflow.

Functions that produce the variables, results, or figures you need in your manuscript allows you to track how your variables are related, which dataset depend on which one, etc.

## Documenting your code

Ideally, your code should be written so that it's easy to understand and your intentions are clear. However, what might seem clear to you now might be clear as mud 6 months from now or even 3 weeks from now. Other times, it might not seem very efficient to refactor a piece of code to make it clearer, and you end up with a piece of code that works but is klunky. If you thrive on geekiness and/or nerdiness you might endup over engineering a part of your code and make it more difficult to understand a few weeks later. In all of these situations, and even if you think your code is clear and simple, it's important that you document your code and your functions, for your collaborators, and your future self.

If all your analysis is made up of scripts, with pieces that are repeated in multiple parts of your document, things can get out of hand pretty quickly. Not only is it more difficult to maintain because you will have to find and replace the thing that you need to change in multiple places of your code, but managing documentation is also challenging. Do you also duplicate your comments where you duplicate parts of your scripts? How do you keep the duplicated comments in sync? Re-organizing your scripts into functions (or organizing your analysis in functions from the beginning) will allow you to explicitly document the dataset or the parameters on which your function, and therefore your results, depends on.

The easiest way to document your code, is to add comments around your functions to explicitly indicate the purpose of each function, what the arguments are supposed to be (class and format) and the kind of output you will get from it.

You may also want to take advantage of [roxygen](https://cran.r-project.org/web/packages/roxygen2/vignettes/roxygen2.html), it's a format that allows the documentation of functions, and it can easily be converted into the file formats used by R documentation. Writing for roxygen is not very different from simple comments, you just need to add some keywords to define what will end up in the different sections of the help files. This is not a strict requirement, and will it not make your analysis more reproducible, but it will be useful down the road if you think you will convert your manuscript into a package (see aside below). RStudio makes it easy to write roxygen. Once you have started writing a function, in the menu choose `Code > Insert Roxygen Skeleton or type Ctrl + Alt + Shift + R` on your keyboard.

When documenting your functions, it important to not only document the kind of input your function takes, but also the format and structure of the output.

## Testing

When you start writing a lot of code for your paper, it becomes easier to introduce bugs. If your analysis relies on data that gets updated often, you may want to make sure that all the columns are there, and that they don't include data they should not.

If these issues break something in your analysis, you might be able to find it easily, but more often than not, these issues might produce subtle differences in your results that you may not be able to detect.

If all your code is made up of functions, then you can control the input and test for the output. It is something that would be difficult if not impossible to do if all your analysis is in the form of a long script.

The package [`testthat`]() provides a powerful and easy-to-use framework to build tests for your functions.

> ## Should you make your manuscript and its functions into a package?
>
> If your manuscript uses functions (which are properly documented and have tests) not only have you done most of the work required to have a functional R package, but you could be in a better position than many R packages.
>
> **Pros**: common format, allows you to leverage the infrastructure for packages (tests, all functions are properly documented), can make sure it will work across platforms.
>
> **Cons**: no good place for the manuscript text, you may have to dissociate code for functions and code for analysis.
>
> **Bottom line**: it really depends on your type of paper, how much code there is in it, and whether others might end up re-using it. It's not because your manuscript follows the conventions of a package that you need to submit to CRAN. If you have written functions that could be useful to the community, consider making those into a package.

## Organizing your files
As you are writing the code for your manuscript, your life will be much easier if you spend time thinking about the organization of your files. File organization is a mix of conventions (e.g., you wouldn't want to put your data in a folder called `favorite_cat_pictures`), requirements by other tools (e.g., when we will write tests later, the package we will use expects the tests to be in a folder named `tests`), and minimizing the impact of the quirks of your project/data on the time you spent writing code. You also need to be mindful, that during the life of your project you will probably go through several iterations of data exploration, and that your analysis will generate intermediate datasets (e.g., summaries by continent/year in our case) that might be computationally expensive to recreate, and that you don't want to have to recreate everytime to build your manuscript. Additionally, it might also be useful to have the intermediate datasets, figures, and result tables, available independently from the manuscript so you can share them with your collaborators.

Thinking about these issues beforehand (and communicating about them with your collaborators) will save you time and headaches.

In this lesson, we are going to functionalize a knitr document that is more complex than what we have seen so far but not quite as complex as a "real" research document could look like. For this project, we will use of the following folders in our working directory:

IMAGE - Replace with ProjectTemplate
- `data-raw`: the original data, you shouldn't edit or otherwise alter any of the files in this folder. In this directory, there is one file for each country. The data is already "clean" (all files have the same columns, in the same order, the data use the same unit).
- `data-output`: intermediate datasets that will be generated by the analysis. We write them to `.csv` (comma eperated values) files so we could share them with collaborators. If it took a long time to generate these data files, we may want to also use them for our analysis, but for this example, they are relatively small and can be recreated every time.
- `fig`: the folder where we can store the figures used in the manuscript. In our example, the figures are generated directly during the rendering of the `Rmardown` file for the manuscript, but having the figures as standalone files may facilitate getting feedback from your collaborators, or save time if you just work on tweaking its appearance without having to recompile the full manuscript.
- `R`: our `R` code (the functions that will generate the intermediate datasets, the analyses, and the figures), it's often easier to keep the prose separated from the code. If you have a lot of code (and/or if the manuscript is long), it's easier to navigate.
- `tests`: the code to test that our functions are behaving properly and that all our data is included in the analysis.

WILL WANT TO REDO THE ABOVE WITH `ProjectTemplate` and integrate those changes into organization.

> ## Overview
> What is a function?
{: .objectives}

```
input --> function does something --> output
```
{: .r}

One of the main benefits of writing functions is to avoid repetition of your code. When you write code you should aim for laziness. If you are about to copy a piece of code 5 times and just change a variable in each instance, you are better off converting it into a function. In general, you should never repeat yourself when you write code, it's called the DRY (Don't Repeat Yourself) principle.

Another advantage is that your code is self contained and any variable that you create inside a function will not be exported into your global environment.

## How to write functions in R?
```
# Fahrenheit to Celsius
(70 - 32) * 5/9
(65 - 32) * 5/9
(85 - 32) * 5/9
```
{: .r}
Let's convert this into a `function`:
```
fahr_to_celsius <- function(temp) {
    (temp - 32) * 5/9
}
```
{: .r}
Don't forget to re-evaluate your function, after modifying it.

A little better:
```
convert_fahr <- function(temp, to) {
    res <- (temp - 32) * 5/9
    if (to == "kelvin") {
        res <- res + 273.15
    }
    res
}
```
{: .r}
With functions you can easily control the format of the input and avoid the chances for typos or other small mistakes.
```
convert_fahr <- function(temp, to = c("celsius", "kelvin")) {
    to <- tolower(to)
    to <- match.arg(to)
    res <- (temp - 32) * 5/9
    if (to == "kelvin") {
        res <- res + 273.15
    }
    res
}
```
{: .r}
Let's refactor this function into something even better that will allow you to easily expend the convert_fahr function to other units:
```
fahr_to_celsius <- function(temp) {
    (temp - 32) * 5/9
}

celsius_to_kelvin <- function(temp) {
    temp + 273.15
}

convert_fahr <- function(temp, to = c("celsius", "kelvin")) {
    to <- tolower(to)
    to <- match.arg(to)
    res <- fahr_to_celsius(temp)
    if (to == "kelvin") {
        res <- celsius_to_kelvin(res)
    }
    res
}
```
{: .r}
Your intentions are clear, everything is self contained, you can easily debug, test and document each of the steps involved.

> ## Challenge
> - Write a function that converts pounds in kilograms (divides by 2.2).
> - _Stretch goal_: and in grams.
{: .challenge}

## Functions for data

Now that we know how to write functions, we can use this concept for preparing our data sets for analysis, generating the intermediary data files, and exporting them to CSV so that we can, for instance, share them with our collaborators.

Let's start with the chunk from the manuscript:
```
## Gathering all the data files
split_gdp_files <- list.files(path = "data-raw", pattern = "gdp-percapita\\.csv$", full.names = TRUE)
split_gdp_list <- lapply(split_gdp_files, read.csv)
gdp <- do.call("rbind", split_gdp_list)
```
{: .r}
The simplest function we can write from this chunk is simply to enclose these lines of code inside curly brackets and not forgetting to return the gdp variable on the last line:
```
gather_gdp_data <- function() {
    split_gdp_files <- list.files(path = "data-raw", pattern = "gdp-percapita\\.csv$", full.names = TRUE)
    split_gdp_list <- lapply(split_gdp_files, read.csv)
    gdp <- do.call("rbind", split_gdp_list)
    gdp
}
```
{: .r}
We can make this function more general by using the folder where the files are stored and the pattern we use as arguments (path and pattern respectively). This way, we could re-use this function for another project where a similar operation (combining many CSV files into a single `data.frame`) would be needed.
```
gather_data <- function(path = "data-raw", pattern = "gdp-percapita\\.csv$") {
    split_files <- list.files(path = path, pattern = pattern, full.names = TRUE)
    split_list <- lapply(split_gdp_files, read.csv)
    gdp <- do.call("rbind", split_gdp_list)
    gdp
}
```
{: .r}
> ## A word of warning
>
> - the code here is pretty simple because we know that all datasets have exactly the same column, but in a real life example, we might way to add additional checks to ensure that we won't be introducing any issues.
> - this also illustrates how general you need to be when writing your functions. We could spend a lot of time optimizing and writing a function that would work on all cases. Sometimes it's worth your time, sometimes it might distract from your primary goal: writing the manuscript.

## Towards automation
We can create a `make_csv` function to automatically generate CSV files from our data sets. This might come handy if you want to send your intermediate datasets to your collaborators or if you want to inspect more closely that everything is working as it should.

This function takes a data frame and make a CSV file out of it.
```
make_csv <- function(obj, file, ...,  verbose = TRUE) {
    if (verbose) {
        message("Creating csv file: ", file)
    }
    write.csv(obj, file = file, row.names = FALSE, ...)
}
```
{: .r}
Now, we can combine the two functions we just wrote (make_csv and gather_data) to generate a CSV file that contains the data from all countries:
```
gdp_data <- gather_data()
make_csv(gdp_data, file = "data-output/gdp.csv")
```
{: .r}
### Your turn
Transform into functions these two pieces of code.
```
## Turn this into a function called get_mean_lifeExp
mean_lifeExp_by_cont <- gdp %>%
    group_by(continent, year) %>%
    summarize(mean_lifeExp = mean(lifeExp)) %>%
    as.data.frame

## Turn this into a function called get_latest_lifeExp
latest_lifeExp <- gdp %>%
    filter(year == max(gdp$year)) %>%
    group_by(continent) %>%
    summarize(latest_lifeExp = mean(lifeExp)) %>%
    as.data.frame    
```
{: .r}

## Long computations
[aside: talk about it if time permits]

Caching is available in knitr but it can be pretty fragile. For instance, the caching is only based on whether the code in your chunk changes and doesn't check if your data on your hard drive is changing.

In other cases, the output of your R code can't be represented into a CSV files, so you need to save it directly into an R object.
```
## If you need to save an R object to avoid the repetition of long computations
make_rds <- function(obj, file, ..., verbose = TRUE) {
    if (verbose) {
        message("Creating rds file: ", file)
    }
    saveRDS(obj, file = file)
    invisible(file.exists(file))
}
```
{: .r}
Then in your knitr document, you can do:
```
gdp <- readRDS(file="data-output/gdp.rds")

or maybe even:

## An example of the kind of code you could use to work with time-consuming
## computations in R.
if ( !file.exists("data-output/gdp.rds")) {
    gdp <- gather_gdp_data() ## long computation...
    make_rds(gdp, file="data-output/gdp.rds")
}
gdp <- readRDS(file="data-output/gdp.rds")
```
{: .r}

## Writing functions to generate figures
Now that we have functions to generate the datasets we need for our paper, we can start using them to generate the figures.

To illustrate this concept, we are going to generate a figure before converting it into a function.
```
gdp <- read.csv(file = "data-output/gdp.csv")

gdp %>%
    filter(country %in% c("United States", "France", "Zimbabwe", "South Africa")) %>%
    ggplot(aes(x = year, y = lifeExp, color = country)) +
    geom_point(aes(size = gdpPercap)) +
    geom_line() +
    geom_vline(xintercept = year_break, color = "red", linetype = 2)
```
{: .r}

If we want to make a PDF file of this figure we could do:
```
pdf(file = "gdp_comparison.pdf", width = 8, height = 6, bg = "white")

gdp %>%
    filter(country %in% c("United States", "France", "Zimbabwe", "South Africa")) %>%
    ggplot(aes(x = year, y = lifeExp, color = country)) +
    geom_point(aes(size = gdpPercap)) +
    geom_line() +
    geom_vline(xintercept = 1985, color = "red", linetype = 2)

dev.off()
```
{: .r}
It's not very neat, we are hardcoding where the year break (the vertical dotted red line) should occur. This example is relatively simple but if you are building a more complex figure that relies on several variables, it means that they will be globally available in your knitr document, potentially causing conflicts down the road.

Let's convert this into a function:
```
fig_gdp_comparison <- function() {

    gdp %>%
      filter(country %in% c("United States", "France", "Zimbabwe", "South Africa")) %>%
      ggplot(aes(x = year, y = lifeExp, color = country)) +
      geom_point(aes(size = gdpPercap)) +
      geom_line() +
      geom_vline(xintercept = 1985, color = "red", linetype = 2)

}
```
{: .r}
so this part gets a little prettier:
```
pdf(file = "fig_gdp_comparison.pdf", width = 8, height = 6, bg = "white")
fig_gdp_comparison()
dev.off()
```
{: .r}
If you start making a lot of figures, it would be nice to have to repeat this first and third lines...

Let's create another function that will automate this process:
```
## An example of a function that generates a PDF file from a function
## that creates a plot
## See http://nicercode.github.io/blog/2013-07-09-figure-functions/
make_pdf <- function(expr, filename, ..., verbose = TRUE) {
    if (verbose) {
        message("Creating: ", filename)
    }
    pdf(file = filename, ...)
    on.exit(dev.off())
    eval.parent(substitute(expr))
}
make_pdf(fig_gdp_comparison(), "fig_gdp_comparison.pdf", width = 8, height = 6, bg = "white")
```
{: .r}
We can even improve our `fig_gdp_commparison` to make it a little more general. For instance, we can add arguments such that the vertical line isn't always at 1985 but can be specified by the user. We can use the same approach for the list of countries to be included in the plot:
```
fig_gdp_comparison <- function(year_break = 1985,
                               countries = c("United States", "France", "Zimbabwe", "South Africa")) {

    gdp %>%
      filter(country %in% countries) %>%
      ggplot(aes(x = year, y = lifeExp, color = country)) +
      geom_point(aes(size = gdpPercap)) +
      geom_line() +
      geom_vline(xintercept = year_break, color = "red", linetype = 2)

}
```
{: .r}
> ## Your turn
>
> Create your own function that generates a plot and use it with make_pdf.
> - If you are looking for some inspiration (or not too familiar with R syntax), the code below compares the relationship between GDP and life expectancy for Japan and Finland.
>
> ~~~
> finland <- read.csv(file = "data-raw/Finland-gdp-percapita.csv")
> japan <- read.csv(file = "data-raw/Japan-gdp-percapita.csv")
> comp_finland_japan <- rbind(finland, japan)
>
> mggplot(comp_finland_japan, aes(x = gdpPercap, y = lifeExp, color = country)) +
>    geom_point() +
>    stat_smooth(method = "lm", se = FALSE)
> ~~~
> {: .r}
>
> > ## Solution
> >
> > This is the body of the solution.
> >
> > ~~~
> > it may also include some code
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}


## Testing
### Using `testthat` to test your functions
One of the advantages of divvying up your entire manuscript into functions, is that you can test that they perform properly.

To do so, we are going to use the package `testthat` that has been designed to test functions written for packages, but it can be applied to any kind of functions.

Make sure you have `testthat` installed:
```
install.packages("testthat")
```
{: .r}
Let's start by writing a first test:
```
## Example of using testthat to check that a function generating a dataset works as expected.
test_that("my first test: correct number of countries",
          expect_equal(length(unique(gather_gdp_data()$country)),
                       length(list.files(path = "data-raw/", pattern="gdp-percapita\\.csv$")))
          )
```
{: .r}

The tests should be wrapped within the `test_that` function, you then provide a short sentence that explains the nature of the test. Keep it short and meaningful because it will be shown to you if the test fails, and having a clear message will help you figure out the problem.

I have also found that spending a little bit of time thinking about the message helps me refine the nature of the test and be more careful about what I test.

You can use one of the several functions that `testthat` provides that tells you what you should expect from your function. The most commonly used ones are `expect_equal()` and `expect_true()`. The functions `expect_warning()` and `expect_error()` are useful to make sure that your functions produce warnings and errors correctly.

### Your turn

Write a test for the `get_mean_lifeExp()` data, or write additional tests for the `gather_gdp_data()`.

## Putting it all together and getting organized
> ## Instructor notebooks
> The goal of this last part is to put together all the pieces started in the previous lesson to build a manuscript that is fully automated. Most of the files are already provided but they are missing the key pieces that make everything work. In this lesson, participants need to copy and paste the chunks of code listed in the appropriate files. At the end, their directory should look like the content of https://github.com/fmichonneau/teaching-automation

Will replace this with `ProjectTemplate`
```
|
`-- data-raw/
|   |
|   `-- Afghanistan-gdp-percapita.csv
|   `-- Albania-gdp-percapita.csv
|   `-- ....
|
`-- data-output/
|
`-- fig/
|
`-- R/
|   |
|    `-- figures.R
|    `-- data.R
|    `-- utils.R
|    `-- dependencies.R
|
`-- tests/
|
`-- manuscript.Rmd
`-- make.R
```

## Tests
`testthat` has a convenient function called `test_dir` that will run tests included in files in a given directory. We can use it to run all the tests in our `tests/` folder.
```
test_dir("tests/")
```
{: .r}

Let's turn it into a function, so we'll be able to add some additional functionalities to it a little later. We are also going to save it at the root of our working directory in the file called `make.R`:
```
## add this to make.R
make_tests <- function() {
    test_dir("tests/")
}
```
{: .r}

## Figures
This is the code to generate the two figures in the manuscript:
```
## add this to R/figure.R
plot_summary_lifeExp_by_continent <- function(mean_lifeExp) {
    ggplot(mean_lifeExp, aes(x = year, y = mean_lifeExp, colour = continent)) +
      geom_line() + facet_wrap(~ continent) + theme(legend.position = "top")
}

plot_change_trend <- function(mean_lifeExp, year_break) {
    tmp_data <- get_coef_before_after(mean_lifeExp, year_break)
    ggplot(tmp_data, aes(x = period, y = trend, colour = continent, group = continent)) +
      geom_point() + geom_path()
}
```
{: .r}

This is the code to generate PDF files from figures, and the two figures as PDF files:
```
## add this to make.R
make_figures <- function(path = "fig", ...) {
    make_summary_by_continent(path = path, ...)
    make_change_trend(path = path, ...)
}

make_summary_by_continent <- function(path = "fig", ...) {
    mean_lifeExp <- get_mean_lifeExp(gather_gdp_data())
    p <- plot_summary_lifeExp_by_continent(mean_lifeExp)
    make_pdf(print(p), file = file.path(path, "summary_by_continent.pdf"), ...)
}

make_change_trend <- function(path = "fig", year = 1980, ...) {
    mean_lifeExp <- get_mean_lifeExp(gather_gdp_data())
    p <- plot_change_trend(mean_lifeExp, year = year)
    make_pdf(print(p), file = file.path(path, "change_trend.pdf"), ...)
}
```
{: .r}

## Data

This is the code that generates the intermediate datasets:
```
## add this to R/data.R
gather_gdp_data <- function(path = "data-raw") {
    split_gdp_files <- list.files(path = path, pattern = "gdp-percapita\\.csv$", full.names = TRUE)

    split_gdp_list <- lapply(split_gdp_files, read.csv)
    gdp <- do.call("rbind", split_gdp_list)
    gdp
}

get_mean_lifeExp <- function(gdp) {
    mean_lifeExp_by_cont <- gdp %>% group_by(continent, year) %>%
      summarize(mean_lifeExp = mean(lifeExp)) %>% as.data.frame
    mean_lifeExp_by_cont
}

get_latest_lifeExp <- function(gdp) {
    latest_lifeExp <- gdp %>% filter(year == max(gdp$year)) %>%
      group_by(continent) %>%
      summarize(latest_lifeExp = mean(lifeExp)) %>%
      as.data.frame
    latest_lifeExp
}

get_coef_before_after <- function(mean_lifeExp, year_break) {
    coef_before_after <- lapply(unique(mean_lifeExp$continent), function(cont) {
                                    mdl_before <- lm(mean_lifeExp ~ year,
                                                     data = mean_lifeExp,
                                                     subset = (continent == cont & year <= year_break))
                                    mdl_after  <- lm(mean_lifeExp ~ year,
                                                     data = mean_lifeExp,
                                                     subset = (continent == cont & year > year_break))
                                    rbind(c(as.character(cont), "before", coef(mdl_before)[2]),
                                          c(as.character(cont), "after", coef(mdl_after)[2]))
                                }) %>%
      do.call("rbind", .) %>% as.data.frame %>%
      setNames(c("continent", "period", "trend"))
    coef_before_after$trend <- as.numeric(levels(coef_before_after$trend)[coef_before_after$trend])
    coef_before_after$period <- factor(coef_before_after$period, levels = c("before", "after"))
    coef_before_after
}
```
{: .r}

This is the code to generate the CSV files that contain the intermediate datasets that are needed to draw the figures. The function make_data generates both datasets at once.
```
## add this to make.R
make_data <- function(path = "data-output", verbose = TRUE) {
    make_gdp_data(path)
    make_mean_lifeExp_data()
}

make_gdp_data <- function(path = "data-output") {
    gdp <- gather_gdp_data()
    make_csv(gdp, file = file.path(path, "gdp.csv"))
}

make_mean_lifeExp_data <- function(path = "data-output") {
    gdp <- gather_gdp_data()
    make_csv(get_mean_lifeExp(gdp), file = file.path(path, "mean_lifeExp.csv"))
}
```
{: .r}

## Cleaning

The only way to ensure that your analysis is reproducible is to delete all the intermediate and final products to make sure your functions can recreate everything from the raw data and your code.

Having the figures and the intermediate data files isolated in their own folders in your working directory will allow you to make sure you only delete these generated figures, and none of the original data.

```
## add this to make.R
clean_data <- function(path = "data-output") {
    to_rm <- list.files(path = path, pattern = "csv$", full.names = TRUE)
    res <- file.remove(to_rm)
    invisible(res)
}

clean_figures <- function(path = "fig") {
    to_rm <- list.files(path = path, pattern = "pdf$", full.names = TRUE)
    res <- file.remove(to_rm)
    invisible(res)
}
```
{: .r}

## Make everything

These are wrapper functions to generate/delete everything:
```
## add this to make.R
make_ms <- function() {
    rmarkdown::render("manuscript.Rmd", "html_document")
    invisible(file.exists("manuscript.html"))
}

clean_ms <- function() {
    res <- file.remove("manuscript.html")
    invisible(res)
}

make_all <- function() {
    make_data()
    make_figures()
    make_tests()
    make_ms()
}

clean_all <- function() {
    clean_data()
    clean_figures()
    clean_ms()
}
```
{: .r}

and before we continue, we are going to replace the make_tests function with something a little more comprehensive:

```
## add this to make.R
make_tests <- function() {
    if (require(testthat)) {
        p <- test_dir("tests/")
        if (!interactive() && any(p$failed)) {
            q("no", status = 1, FALSE)
        }
    } else {
        message("skipped the tests, testthat not available.")
        return(NULL)
    }
}
```
{: .r}
