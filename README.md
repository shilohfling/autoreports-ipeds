# Automating Peer Reports Using IPEDS Data

 	
  This is a brief tutorial on how to get set-up to run custom IPEDS peer reports using the IPEDS Access databases. Due to the size restrictions, the data could not be uploaded to GitHub. The databases are free and open to the public. They can be downloaded [here](https://nces.ed.gov/ipeds/use-the-data/download-access-database). 


## Getting up and running

### Prerequisites 
#### The following should be installed before running reports:
* [ODBC]() 
* [MiKTeX](https://miktex.org/2.9/setup) 
* [R](http://cran.cnr.berkeley.edu/)
* [RStudio](https://www.rstudio.com/products/rstudio/download/)

### Customizations
#### [main.Rmd](https://github.com/shilohbradley/autoreports-ipeds/blob/master/main.Rmd) 
  - **Lines 2-5**
    - Rename the report and the author to match your institution and department.

```
title: "IPEDS Peer Report 2016-2017" ## Put your title here
author: 
 - "Office of Decision Support" ## Put your name or office
 - "University of Nevada, Las Vegas" ## Another line for author, can change this also
```


  - **Line 36**
    - Replace the hexadecimal colors to fit your institution’s brand image
    - Replace #B10202 with the color that you want your institution to be. Currently, #B10202 codes for scarlet. 
    - Replace #666666 with the color that you want your peer institutions to be. Currently, #666666 codes for grey.
```
## Aesthetics
cols <- c("#B10202", rep("#666666", length(id_vec)-1))
```


#### [queries.R](https://github.com/shilohbradley/autoreports-ipeds/blob/master/queries.R) 

  - **Line 8**
     - Set the working directory to the path for where your Access database is stored.

```
## Set working directory
setwd("C:/Users/iadsshared/Desktop/autoreports/")
```
  - **Line 36**
    - Change “IPEDS201617.accdb” to the name of the Access database that you are using.
    - This should be in the same folder as your working directory.
```
## Load Access file
ipeds <- odbcConnectAccess2007("IPEDS201617.accdb")
```

#### [report_peers.csv](https://github.com/shilohbradley/autoreports-ipeds/blob/master/report_peers.csv)
- Change 182281 to your IPEDS UnitID. Make sure that you always keep yours as the first.
- Change the rest of the UnitID’s in rows 3-10
- You can add as many or as few peers as you want. More than eight might become cumbersome, but you can do it.

#### [report_metrics.csv](https://github.com/shilohbradley/autoreports-ipeds/blob/master/report_metrics.csv)
  - *Report_Name* is what you want the name of your graphs will be.
  - *Metric* is the variable that you want to use for comparison.
  - *Table* is which table the variable comes from.
  - Make sure to check the table names when changing which Access database you are using. HD2016 could become HD2017 for the next year of data. 
  - You can add as many “Metrics” as you want to make the peer report as complex as you want
  - **CRITICAL:** The first row after the header must always be "Institution Names", "INSTNM", and "HD2016" (where 2016 can change to various years depending on the year of the report you want to use).
