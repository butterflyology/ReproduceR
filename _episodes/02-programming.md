---
title: "Programming and Organization"
teaching: 120
exercises: 20
questions:
- "How should we organize a project for reproducibility?"
objectives:
- ""
- ""
keypoints:
- "Keep raw data read only."
- "Manipulate data in a reproducible manner"
---
## Literate Programming

This section is broken down into three sections:
1. **Data manipulation**
1. **Literate programming**
1. **Project organization**


> ## 1. Documenting data modifications
> - Distinguish between a spreadsheet formatted properly for later analysis in R and one formatted improperly.
> - Be able to recognize common data entry errors and how to handle them.
> - Be able to describe the concept of 'raw data' and why it is important.
> - Differentiate between manual and programmatic file manipulation and know the pros and cons of each.
{: .objectives}

## Activity 1
Please download the Excel file called `oceania_uk.xlsx` and open it.

Depending on what type of science you do, data may come from instruments, online databases, or transcribed from field or lab notebooks into spreadsheets. Thinking about how to format your data in those spreadsheets to ensure that it is machine readable (that is, easily parseable by an algorithm or script) and well documented for humans is important.

In R, the primary data type used most often is called a data frame. Although there are many similarities to the ways datasets are represented in spreadsheet programs, there are a few key differences and formatting concerns. This exercise works through "fixing" a poorly-formatted spreadsheet in Excel and preparing it for use in R. Along the way, we will also work to create supplementary documentation and move everything to plain text formats.

**Instructions**

Assume for the moment that this is your only copy of the data. it's important NEVER to modify by hand or by script your only copy of a dataset, since you may need to start over at some point in the future. Therefore, before making any corrections to the dataset, remember to create a copy of the file.

Next, once you've duplicated that file, open the copy and start going though the spreadsheet and correct any errors you observe. Every time you find an error and correct it, document exactly what you did, step by step, in a text file. Imagine that you are writing these instructions to yourself or to a colleague to document exactly what you did to this file, so that you could read the file and easily repeat the changes on the original copy if you needed to.

**Textual documentation to executable documentation**

Eventually, all modifications to data files would be done programmatically -- that is, completely through a scripted approach instead of by hand in a graphical user interface (GUI) such as Excel. This skill takes time to learn and to get efficient with. Initially, it may take much longer than doing it by hand, but if the modifications need to be not only recounted later but re-executed, the scripted approach will start to pay off. Importantly, it is natural to extend the script approach to include automatic tests to verify that the dataset (which may changed since last time you inspected it) meets the basic integrity constraints that are assumed. AND you now have a fully documented and reproducible set of instructions for cleaning your data.

> ## 2. Literate programming
> - Organize your work
> - make work more pleasant for yourself? (less tedium, less manual, less ...)
> - reduce friction for collaboration?
> - reduce friction for communication?
> - make your work navigable, interpretable, and repeatable by others?
{: .objectives}

#### Getting the analysis right is only one link

Process, packaging, and presentation are often the weak links in the chain.

## Markdown

### What is Markdown?
- Markdown is a particular type of markup language. Markup languages are designed to produce documents from plain text.
- You may be familiar with `LaTeX`, another (though less human friendly) text markup language.
- Tools render markdown to different formats (for example, HTML/pdf/Word).
  - The main tool for rendering Markdown is [pandoc](http://pandoc.org/).

Adapted from [Carson Sievert's markdown slides](http://cpsievert.github.io/slides/markdown/#/1)

### Markdown enables fast publication to the web
- **Markdown** Easy to write and read in an editor.
- **HTML** Easy to publish and read on web.

### Markdown versus HTML code {.code-columns}
This is a Markdown document.

## Medium header <!-- header 2, actually -->

It's easy to do *italics* or __make things bold__.

> All models are wrong, but some are useful. An approximate answer to the right problem is worth a good deal more than an exact answer to an approximate problem.

Code block below. Just affects formatting here.

```
x <- 3 * 4
```
I can haz equations. Inline equations, such as the average is computed as $\frac{1}{n} \sum_{i=1}^{n} x_{i}$. Or display equations like this:

$$
\begin{equation*}
|x|=
\begin{cases} x & \text{if $x\ge 0$,} \\\\
-x &\text{if $x\lt 0$.}
\end{cases}
\end{equation*}
$$

<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
<title>Title</title>
<!-- MathJax scripts -->
<script type="text/javascript" src="..."></script>
<style type="text/css">
body {
   font-family: Helvetica, arial, sans-serif;
   font-size: 14px;
...
</style>
</head>
<body>
<p>This is a Markdown document.</p>

<h2>Medium header</h2>

<p>It's easy to do <em>italics</em> or <strong>make things bold</strong>.</p>

<blockquote><p>All models are wrong, but some are...</p></blockquote>
<p>Code block below. Just affects formatting here.</p>

<pre><code>x <- 3 * 4
</code></pre>


### Markdown versus rendered HTML {.code-columns}

This is a Markdown document.

## Medium header <!-- header 2, actually -->

It's easy to do *italics* or __make things bold__.

> All models are wrong, but some are useful. An approximate answer to the right problem is worth a good deal more than an exact answer to an approximate problem.

Code block below. Just affects formatting here.

```
x <- 3 * 4
```

I can haz equations. Inline equations, such as the average is computed as $\frac{1}{n} \sum_{i=1}^{n} x_{i}$. Or display equations like this:

$$
\begin{equation*}
|x|=
\begin{cases} x & \text{if $x\ge 0$,} \\
-x &\text{if $x\lt 0$.}
\end{cases}
\end{equation*}
$$
This is a Markdown document.

## Medium header

It's easy to do *italics* or __make things bold__. > All models are wrong, but some are useful. An approximate answer to the right problem is worth a good deal more than an exact answer to an approximate problem. Code block below. Just affects formatting here. ``` x <- 3 * 4 ``` I can haz equations. Inline equations, such as the average is computed as $\frac{1}{n} \sum_{i=1}^{n} x_{i}$. Or display equations like this: $$ \begin{equation*} |x|= \begin{cases} x & \text{if $x\ge 0$,} \\\\ -x &\text{if $x\lt 0$.} \end{cases} \end{equation*} $$

## Markdown can be rendered to multiple formats
- `pandoc` is a swiss-army knife tool for conversion`

## R Markdown

R Markdown is rendered to Markdown {.code-columns}

This is an R Markdown document.

```{r}
x <- rnorm(1000)
head(x)
```

`knitr` offers a lot of control over representing different types of output. We can also have inline R expressions computed on the fly. The mean $\bar{x} = \frac{1}{n} \sum_{i=1}^{n} x_{i}$ of the `r length(x)` random variates we generated is `r round(mean(x), 3)`. This figure is computed on-the-fly as well. No more copy-paste, including for figures:

```{r}
plot(density(x))
```
This is an R Markdown document.

```{r}
x <- rnorm(1000)
head(x)
```

`knitr` offers a lot of control over representing different types of output. We can also have inline R expressions computed on the fly. The mean $\bar{x} = \frac{1}{n} \sum_{i=1}^{n} x_{i}$ of the `r length(x)` random variates we generated is `r round(mean(x), 3)`. This figure is computed on-the-fly as well. No more copy-paste, including for figures:

```r
plot(density(x))
```
![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2.png)

### Ideas, code, and generated results tied together {.code-columns}

This is an R Markdown document.

```{r}
x <- rnorm(1000)
head(x)
```

`knitr` offers a lot of control over representing different types of output. We can also have inline R expressions computed on the fly. The mean $\bar{x} = \frac{1}{n} \sum_{i=1}^{n} x_{i}$ of the `r length(x)` random variates we generated is `r round(mean(x), 3)`. This figure is computed on-the-fly as well. No more copy-paste, including for figures:

```{r}
plot(density(x))
```


This is an R Markdown document. ```{r} x <- rnorm(1000) head(x) ``` `knitr` offers a lot of control over representing different types of output. We can also have inline R expressions computed on the fly. The mean $\bar{x} = \frac{1}{n} \sum_{i=1}^{n} x_{i}$ of the `r length(x)` random variates we generated is `r round(mean(x), 3)`. No more copy-paste, including for figures: ```{r} plot(density(x)) ```


## Rendering can be automated is thus repeatable

From within R:

`rmarkdown::render("filename.Rmd")`

From the command line:

`$ Rscript -e "rmarkdown::render('filename.Rmd')"`


## Summary
- R Markdown enables ideas and questions, the code that implements them, and the results generated by the implementation, to all stay together.
- R Markdown toolchain allows automated, repeatable rendering
  - for publishing to the web and viewing through a browser
  - and (through `LaTeX`) to obtain a submittable manuscript (in PDF or Word).
- `knitr` is not limited to executing R code. See the book Dynamic documents with R and knitr by Yihui Xie, part of the CRC Press / Chapman & Hall R Series (2013). [ISBN](http://www.isbnsearch.org/isbn/9781482203530)
