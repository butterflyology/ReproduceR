---
title: "Introduction"
teaching: 120
exercises: 30
questions:
- "What is reproducible research?"
- "What are the keys to reproducible research?"
objectives:
- "Learn the four facets of reproducibility."
keypoints:
- "There are four facets to reproducibility: Documentation, Organization, Automation, Dissemination"
---

## Motivating Reproducibility
- The sciences have with reproducibility problem. [Nature article](http://www.nature.com/news/1-500-scientists-lift-the-lid-on-reproducibility-1.19970)
- Many published studies cannot be reproduced
  - __Replication__ - when independent investigators use methods, protocols, data, and equipment to confirm scientific claims.
  - __Reproduction__ - when data sets and computer code are made available for researchers to verify results.
- Peng (2009) Reproducible research and Biostatistics. [*Biostatistics 10: 405-408*](http://biostatistics.oxfordjournals.org/content/10/3/405.full)


> ## *Science* retracts paper without agreement of lead author.
> - Journal retracted a study of how canvassers can sway people's opinions about gay marriage.
>
> -[Editor-in-Chief](http://news.sciencemag.org/policy/2015/05/science-retracts-gay-marriage-paper-without-lead-author-s-consent): Original survey data:
>    + not made available for independent reproduction of results
>    + Survey incentives misrepresented
>    + Sponsorship statement false
>
> - Two grad students attempted to reproduce the study and could not. Concluded the data must have been fabricated. [538 story](http://fivethirtyeight.com/features/how-two-grad-students-uncovered-michael-lacour-fraud-and-a-way-to-change-opinions-on-transgender-rights/)
>
> - Methods we'll discuss today can't prevent fraud, but they can make it easier to discover such issues.
{: .callout}

> ## Retracted, but not fraud
> - One researcher had seven papers retracted because of irreproducibility [Retraction Watch](http://retractionwatch.com/2014/11/14/univ-no-misconduct-but-poor-research-practice-in-mgt-profs-work-now-subject-to-7-retractions/#more-23666)
> - Couldn't find the data [Wiley](http://onlinelibrary.wiley.com/doi/10.1111/j.1468-1331.2011.03524.x/abstract)
> - "Extensive" errors force retraction of lymphoma paper [JRO](http://retractionwatch.com/2013/01/14/extensive-errors-force-retraction-of-lymphoma-radiation-paper/)
> - Many, many more [Hackathon](https://github.com/Reproducible-Science-Curriculum/Reproducible-Science-Hackathon-Dec-08-2014/wiki/Irreproducible-Examples)
{: .callout}

> ## Seizure study retracted after authors realized data were "Terribly mixed"
> From the authors of Low Dose Lidocaine for Refractory Seizures in Preterm Neonates:
> "The article has been retracted at the request of the authors. After carefully re-examining the data presented in the article, they identified that data of two different hospitals got terribly mixed. The published results cannot be reproduced in accordance with scientific and clinical correctness." [IJP](http://retractionwatch.com/2013/02/01/seizure-study-retracted-after-authors-realize-data-got-terribly-mixed/)
{: .callout}

> ## Bad spreadsheet merge kills depression paper, quick fix resurrects it
> - The authors informed the journal that the merge of lab results and other survey data used in the paper resulted in an error regarding the identification codes.
> - **Original conclusion** : Lower levels of CSF IL-6 were associated with current depression and with future depression.
> - **Revised conclusion**: Higher levels of CSF IL-6 and IL-8 were associated with current depression.
{: .callout}

## Exercise: Motivating reproducibility

This is a two-part exercise:

> ## Part 1: Analyze + document
>
> Complete the following tasks and write instructions / documentation for your collaborator to reproduce your work starting with the original dataset (data/gapminder-5060.csv).
>
> ~~~
> 1. Visualize life expectancy over time for Canada in the 1950s and 1960s using a line plot.
>
> 2. Something is clearly wrong with this plot! Turns out there's a data error in the data file: life expectancy for Canada in the year 1957 is coded as 999999, it should actually be 69.96. Make this correction.
>
> 3. Visualize life expectancy over time for Canada again, with the corrected data.
>
> Stretch goal: Add lines for Mexico and United States.
> ~~~
> {: .source}
> {: .output}
{: .challenge}


> ## Part 2: Swap + discuss
>
> Introduce yourself to your collaborator and tell them why you're here.
>
> ~~~
> 1. Swap instructions / documentation with your collaborator, and try to reproduce their work, first without talking to each other. If your collaborator does not have the software they need to reproduce your work, we encourage you to either help them install it or walk them through it on your computer in a way that would emulate the experience. (Remember, this could be part of the irreproducibility problem!)
>
> 2. Then, talk to each other about challenges you faced (or didn't face) or why you were or weren't able to reproduce their work.
>
> ~~~
> {: .source}
> {: .output}
{: .challenge}

## Reflection
  - What tools did you use (Excel / R / Python / Word / plain text etc.)?
  - Were you successful in reproducing each others' work?
  - What would happen if your collaborator is no longer available to walk you through their analysis?
  - What made it easy / hard for reproducing your partners' work?
  - What would have to happen if:
      - you had to swap out the dataset or extend the analysis further?
      - you caught further data errors and had to re-create the analysis with corrections?
      - you had to revert back to the original dataset?

## Summary
- Everyone struggles with reproducibility and it is a hindrance to moving science forward.
- Evan with a fairly simple analysis challenges were faced in four main areas: organization, documentation, automation, and dissemination
- Over the two day workshop, data analysis tasks will become more complex as we gather more data and ask more complicated questions, so we need better tools and workflows to combat issues arising in these areas


## Why we care
It is vital that scientific research be reproducible. This improves communication, openness, and transparency. We consider that there are four facets required to maximize reproducibility.


## Four facets of reproducibility:

1. **Documentation**: difference between binary files (e.g. docx) and text files and why text files are preferred for documentation.

1. **Organization**: tools to organize your projects so that you don't have a single folder with hundreds of files.

1. **Automation**: the power of scripting to create automated data analyses.

1. **Dissemination**: publishing is not the end of your analysis, rather it is a way station towards your future research and the future research of others.

## Our reproducibility toolkit
### R + RStudio

#### Why R?
- Programming language for data analysis:
  - Free!
  - Open source
  - Widely used and supported across all disciplines
  - Can be used on Windows, Mac OS X, or Linux!

#### Why not language X?
- There are a number of other great programming tools out there that can also be used to improve the reproducibility of your analysis

- The key is to use some type of language that will allow you to automate and document your analysis

- Once you master one language you'll probably find it easier to learn another

#### Once in R

You could just type into the command prompt...
 - ... but that doesn't help much with documentation.
 - ... but that doesn't help much with automation.

#### A better solution
- With RStudio you can combine your programming and your documentation.
- RStudio gives you a single environment to combine your documentation and your analysis - It runs on top of R - Gives you a bunch of really cool features that we'll explore throughout the workshop.

## R Packages

Packages are the fundamental units of reproducible R code. They include reusable R functions, the documentation that describes how to use them, and (often) sample data. (From: http://r-pkgs.had.co.nz)

- We will use the ggplot2 package for plots and dplyr for data wrangling in this session.

- If you have not yet done so, install these packages by running the following in the Console:

~~~
install.packages("ggplot2")
install.packages("dplyr")
~~~
{: .source}


## Demo

Goals of the demo:
- Demonstrate "good practice" for organizing data files and analysis documents (R Markdown)
- How to read data from a file
- How to manipulate the data, and document it in a reproducible way
  - How easy it would be to revert any changes if need be
- How to subset data
- How to make simple plots in ggplot
- **NOT** about understanding all the R commands, but  **rather** getting the big picture of how using R in this way facilitates reproducible analyses

### R Markdown demo

Open `intro-template.Rmd`

Click on `Knit HTML` to compile the document

Important features:
- YAML on top
- Code in chunks
- R Markdown syntax
    - Human readable!
    - Limited, so not too time consuming to master
- Self contained workspace

### Extending the analysis

Great news!? We just received some more data, in bits and pieces of course:
`gapminder-7080.csv`

`gapminder-90plus.csv`

Let's walk through generation of new plots for the 1970s and 1980s and 1990s plus (these new analyses are already in the `intro-tutorial.Rmd` document).

Note that all code required to accomplish these tasks is also in the template. You do not need to come up with the R code, **knit** the document to combine the datasets and you'll see that the code required for recreating the plots is the same as above. That's the beauty of R Markdown!

### Take aways
- The analysis is self-documenting
- It's easy to extend or refine analyses by copying and modifying code blocks
- The results of the analysis can be disseminated by sending R Markdown and providing data sources, or just simply providing the generated HTML of just a summary of the analysis is needed

> ## Reproducibility checklist
>
> - Serves as a tool to help you think about the reproducibility of your data analysis.
> - Many of the questions can be thought of as having a yes/no answer.
> - A better approach would be to see the questions as being open ended with the real question being, "What can I do to improve the status of my project on this bullet point?"
> - With that in mind, you'll never get 100% of the bullets right for your project, but you'll always be improving.
{: .checklist}
