# Preview
<p float="left">
  <a href="https://github.com/sidechained/DataDrivenResume/blob/master/DataDrivenResume.pdf"><img src="/previews/DataDrivenResume-Page1.png"></a>
  <a href="https://github.com/sidechained/DataDrivenResume/blob/master/DataDrivenResume.pdf"><img src="/previews/DataDrivenResume-Page2.png"></a>
</p>

# Introduction
The aim of this project was to create a 'data-driven' resume. In this case, data-driven simply means to separate code from content as much as possible, so that the content can easily be maintained or - in the case of this template - swapped out for your own.

The resume itself consists of two pages, with a geographical overview on the first page and selected career highlights on the second.

## Overview Page
This page includes:

- a _header of biographical information_. This can be modified to be as simple or as detailed as required, with options for a profile picture, 'about me' section, links to social media accounts etc.
- a _map section_ which displays icons for four geographical locations (created by Lorena Abad - see [Acknowledgements](#acknowledgements))
- a _written summary_ giving an overview of what was achieved in each location
- an _interests_ section which uses a [word-cloud](https://www.r-graph-gallery.com/wordcloud.html) to display categories-of-interest organised by colour (with deeper interests shown as smaller text in the same colour)
- a _skills_ section which uses a [circular-packing diagram](https://www.r-graph-gallery.com/circle-packing.html) to place skills into categories, with circle size showing relative levels of experience

## Career Highlights Page(s)
The idea of this page was to forgo the traditional idea of separating the CV into sections (such as Experience, Education etc) and instead have all elements run-together reverse-chronologically but tagged with icons/labels.

This page includes:
- a _timeline-style summary_ of the candidate's history, consisting of two-types of entries: either 'short' or 'detailed', where:
  - _short entries_ consist of a title, category, date range and bullet points description
  - _detailed entries_ consist of the above plus an institution and a location

# Editing the Template
The resume template contains uses data taken from the life of [Buckminster Fuller](https://en.wikipedia.org/wiki/Buckminster_Fuller). To modify it, simply edit:

1. The four comma-separated values files in the [`/data`](/data) folder
2. The header section in the [`DataDrivenResume.Rmd`](DataDrivenResume.Rmd) file

To knit the document yourself you will first need to install [RStudio](https://www.rstudio.com). I'm running RStudio on MacOS, but the process should be similar regardless of operating system, as follows:

1. Clone this repo using `git clone https://github.com/sidechained/DataDrivenResume.git`
2. Cpen the [`DataDrivenResume.Rmd`](DataDrivenResume.Rmd) file in RStudio
3. Install package dependencies in R by uncommenting and running the [following lines](DataDrivenResume.Rmd#L34-47) in `DataDrivenResume.Rmd`
4. Ensure the working directory is set to the directory where you cloned the repo. Use the command `getwd()` to check and `setwd()` to provide the correct path if it is incorrect
5. From the File menu in RStudio choose "Knit Document". Knitting will begin and after some time a PDF file will be output with the same name as the .Rmd file (i.e. `DataDrivenResume.pdf`). Note this will overwrite the existing template PDF.

# Under the Hood
The main code for generating the resume is contained within the [`DataDrivenResume.Rmd`](DataDrivenResume.Rmd) file. This uses R's Vitae package to knit together R and LaTex code, with the final output being a PDF.

R does the heavy lifting when it comes to pulling the resume data from .csv files and sorting it chronologically, automatically creating date ranges etc. Much of this R code programatically generates LaTex. R is also used to create custom figures as seen in the _Interests_ and _Skills_ sections.

LaTex itself is used to format the final document in a clear, structured and visually-appealing way. The final layout is based on a given LaTex class file (in this case [awesome-cv.cls](awesome-cv.cls) - see [Acknowledgements](#acknowledgements)).

To see the final LaTex code that R generates, change the `keep_tex: false` to `true` in the YAML header of [`DataDrivenResume.Rmd`](DataDrivenResume.Rmd), then watch for a `DataDrivenResume.tex` file being created when knitting the document.

# Description of comma-separated values files
The following describes the column names contained in the four .csv files in the `/data` folder. This should help when replacing the data with your own. The files are best viewed in Excel, Google Sheets or their open-source equivalents.

## cv_data.csv

- CATEGORY: Must match one of the following five types: EXPERIENCE, EDUCATION, EXTRACURRICULAR, SKILL, PUBLICATION.
- TITLE: Title of job/course/etc i.e. for EXPERIENCE "Master Dome Builder", for EDUCATION "PhD in Geodesic Domes".
- INSTITUTION: place worked or studied at e.g. "Geodesics Inc.", "North Carolina State University"
- STARTDATE: in format DD/MM/YYYY (single digit dates/months also acceptable)
- ENDDATE: as above
- CITYNAME: city where the entry took place. This must match the CITYNAME in geo_data.csv - see [below](#geo_data.csv)
- DESCRIPTION: Bullet-point description of experience. Each bullet-point is separated by a semicolon i.e. "erected a geodesic dome building that could sustain its own weight with no practical limits;suspended several students from the structure's framework". Note there is no semicolon at the end. Items may be separated by carriage returns for ease of reading.

## geo_data.csv

- CITYNAME: i.e. Hanoi
- COUNTRYNAME: i.e. Vietnam
- COUNTRYCODE: i.e. VT
- LAT: Lattitude i.e. 21.0278
- LONG: Longitude i.e. 105.8342
- ICONNAME: Name used by the R [fontawesome package](https://cran.r-project.org/web/packages/fontawesome/index.html) i.e. fa-map-pin
- LATEXICONNAME: Name used by the LaTex [fontawesome5 package](http://www.ipgp.fr/~moguilny/LaTex/fontawesome5Icons.pdf) i.e. faMapPin
- DESC: Bullet-point summary of what happened in the given location. Each bullet-point is separated by a semicolon i.e. "married Anne Hewlett;developed the Stockade Building System". Note there is no semicolon at the end. Items may be separated by carriage returns for ease of reading.

## interests_data.csv

The idea of the _interests_ word-cloud is to display interests which move from generic one-word categories through to specific examples.

To do this data is organised into 'categories', 'subcategories' and 'sub-subcategories'. 'Categories' are shown in large text, each in a different colour. 'Subcategories' of interests appear in smaller text, in colours that correspond to the initial categories. 'Sub-subcategories' do the same again but smaller still. Typically there are 4 'subcategories' and 6 'sub-subcategories' for each 'category'. An example for one category would be:

- CATEGORY: Typically a single word i.e. "domes"
- TYPE: Either _main_, _sub_ or _subsub_
- TEXT: The text that will appear in the wordcloud e.g.
  - "domes", "travel" for _main_
  - "Geodesic" or "Monolithic" for the _sub_ "domes"
  - "Dome Of The Rock, Jerusalem" or "Taj Mahal, Agra" for _subsub_

## skills_data.csv

Skill names are grouped into categories, with size showing relative levels of experience.

- NAME: The name of the particular skill i.e. Python
- CATEGORY: The category i.e. Programming Languages
- SIZE: The relative size of the bubble that will be plotted, where 1 is the smallest bubble and 3 the largest

# Acknowledgements

The initial inspiration and template for this project comes from Lorena Abad, who developed a great looking [geographical CV](https://github.com/loreabad6/R-CV) which this resume template builds on.

Her work uses the [vitae](https://github.com/mitchelloharawild/vitae) package in R by Mitchell O’Hara-Wild and also modifies the [Awesome CV template](https://github.com/posquit0/Awesome-CV) created by Claud D. Park .

[Awesome CV](https://www.overleaf.com/LaTex/templates/awesome-cv/dfnvtnhzhhbm) and a [matching covering letter](https://www.overleaf.com/LaTex/templates/awesome-cv-cover-letter/hzvvsbxccjhz) can also be found on Overleaf.
