# Preview

[![CV](previews/DataDrivenResume-Page1.png)](https://github.com/sidechained/DataDrivenResume/blob/master/DataDrivenResume.pdf)

[![CV](previews/DataDrivenResume-Page2.png)](https://github.com/sidechained/DataDrivenResume/blob/master/DataDrivenResume.pdf)

# Aim
The basic aim of this project was to create a two-page resume with a geographical overview on the first page and selected highlights from my CV on the second, with layout/code separated from content as much as possible. The project also proved useful to learn Rmarkdown and deepen my knowledge of R and Latex.

# Project Structure
The resume itself is written as a RMarkdown document which knits together R and Latex code to produce a PDF. All the data shown in the Resume is contained with the Rmarkdown file header and four comma-separated values files. R does the heavy lifting when it comes to pulling the resume data from .csv files and sorting it chronologically, creating date range etc. R is also used to create custom figures as seen in the Interests and Skills sections. Latex on the other hand is used to format the final document in a clear, structured and visually-appealing way. Much of the R code programatically generates Latex.

## Resume: Overview Page
The overview page includes:

- a header of biographical information alongside a simple written introduction
- a map section entitled 'My Journey' which displays four geographically locations
(Acknowledgements)
- a written summary giving an overview of what was achieved in each location
- an 'Interests' section which uses a word-cloud to display categories of interest organised by colour, with deeper interests shown as smaller text
- a 'Skills' section which uses a circular packing diagram to place skills into categories and to compare experience by circle size

## Resume: Career Highlights Page(s)
The idea here was to forgo the traditional idea of separating the CV into sections and instead opt for an approach where all elements run-together but are given labels (such as Experience, Education etc). The Career Highlights page(s) include:

- a timeline-style summary of the candidates working/employment/life history
- two-types of entries: either 'short' or 'detailed', where:
  - 'short' consists of title, category and date range and description (i.e. bullet points)
  - 'detailed' adds an institution and a location

# Modifying the Resume
To modify the basic template, simply edit the header data in the Rmarkdown file and the four comma-separated values files to reflect your own experience. The .csv files are described as follows:

# Generating the Resume
I created the project using RStudio on MacOS, but the process should be similar regardless of OS e.g.:

- Clone the repo using `git clone https://github.com/sidechained/DataDrivenResume.git`
- Cpen the DataDrivenResume.Rmd file in RStudio
- Ensure the working directory is set to the directory where you cloned the repo (getwd and setwd)
- From the File menu in RStudio choose "Knit Document"
- Knitting will begin and after some time a PDF file will be output with the same name as the .Rmd file

# Description of comma-separated values files

## geo_data.csv

- CITYNAME      - i.e. Hanoi
- COUNTRYNAME   - i.e. Vietnam
- COUNTRYCODE   - i.e. VT
- LAT           - Lattitude i.e. 21.0278
- LONG          - Longitude i.e. 105.8342
- ICONNAME      - i.e. fa-map-pin
- LATEXICONNAME - i.e. faMapPin
- DESC          - bullet-point summary descriptions, with each point separated by a semicolon i.e. "married Anne Hewlett;developed the Stockade Building System". Note there is no semicolon at the end.

uses font awesome icons within both R and Latex.

Latex package:  fontawesome5 http://www.ipgp.fr/~moguilny/LaTeX/fontawesome5Icons.pdf
R package: library(fontawesome)

? where does library(emojifont) fit in?

## resume_data.csv

- CATEGORY      - EDUCATION, EXPERIENCE, EXTRACURRICULAR, SKILL, PUBLICATION
- TITLE         - "Chief Executive Officer" or "Master's Degree in Architecture"
- INSTITUTION   - "Black Mountain College" or "Geodesics Inc."
- STARTDATE     - DD/MM/YYYY
- ENDDATE       - DD/MM/YYYY
- CITYNAME      - NOTE: This should match with CITYNAMEs in geo_data.csv
- DESCRIPTION   - bullet-point summary descriptions, with each point separated by a semicolon i.e. "built huge geodesic domes; lectured in Raleigh in 1949". Note there is no semicolon at the end.

## interests_data.csv

The idea of the interests word-cloud is to display interests which move from generic one-word categories through to longer examples. To do this data is organised into 'categories', 'subcategories' and 'deepdives'. 'Categories' are shown in large text, each in a different colour. 'Subcategories' of interests appear in smaller text, in colours that correspond to the initial categories. 'Deepdives' do the same again but smaller still. Typically there are 4 'subcats' and 6 'deepdives' for each 'category'. An example for one category would be:

- CATS          - "Domes"
- SUBCATS       - "Geodesic;Monolithic;Crossed-arch;Rotational"
- DEEPDIVES     - "Dome Of The Rock, Jerusalem; Taj Mahal, Agra;Saint Basil’s Cathedral, Moscow;Seagaia Ocean Dome, Miyazaki; Round Valley Ensphere, Arizona; Jeddah Super Dome, Saudi Arabia"

## skills_data.csv

- name          -
- category      -
- size          -

# Acknowledgements

The initial inspiration and template for this project comes from Lorena Abad, who developed a great looking [geographical CV](https://github.com/loreabad6/R-CV) on which this resume is based. Her work uses the [vitae](https://github.com/mitchelloharawild/vitae) package in R by Mitchell O’Hara-Wild and also modifies the Awesome CV template created by Claud D. Park (https://github.com/posquit0/Awesome-CV). [Awesome CV](https://www.overleaf.com/latex/templates/awesome-cv/dfnvtnhzhhbm) and a [matching covering letter](https://www.overleaf.com/latex/templates/awesome-cv-cover-letter/hzvvsbxccjhz) can also be found on Overleaf.
