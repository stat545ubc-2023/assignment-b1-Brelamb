## Assignment B1 - *Making a function*

### **Repository goals:**

This repository contains assignment B1 completed for the course STAT545B at UBC. The goal of this project is to familiarize yourself with the process of making a function. This is done by creating, documenting, testing and showing examples of a function in R. 

### **Assignment B1** 
[click here for detailed instructions](https://stat545.stat.ubc.ca/assignments/assignment-b1/) 

Assignment B1 has four major parts to it. First, a function is created using in R using a set of criteria (found in the detailed instructions). This new function is then documented using roxygen2 tags, these include the functions title, description, parameter names and what the function returns. After that four different use examples for the function are demonstrated, along with a final example showing the error code. Finally, there are three non-redundant tests run on the function using the *testthat* package.

### Files in this Repository (b1-new-function): 

1.	**README.md File**:
The README.md file consists of a brief overview of the goals of this repository, a brief description of assignment B1, a list of the repository files and instructions for how to interact with the repository. 

2.	**Function_.Rmd File**:
The Function_.Rmd file contains all of the R code for assignment B1. This includes code for the new function *getNamesCount*. The code from this .Rmd file can be knit to a .md file using RStudio.
 
3.  **Function_.md File**:
The Function_.md file contains is the R markdown file for this project. It contains all of the the R code which has been knit into a .md file. The Function_.md file introduces the new *getNamesCount* function and documents it using roxygen2 tags. The file also contains examples uses for the *getNamesCount* function and tests preformed on the function using testthat.


### Interacting with this Repository: 

If you would like to interact with this repository you can use Git, R or R studio to run the files. To use RStudio to interact with repository files *(recommended)*, open RStudio and click the *'create a project'* button (top left hand corner). From the options that appear select *'version control'* and then *'git'*. There will be a space on the screen for you to paste github repository URL. Once you have successfully copy and pasted the URL into RStudio the all of the github repository files should appear in the files of your Rstudio. Click on a file to interact with it.

If you have made changes to a file in this repository and would like to upload them to github you will need to push the changes. In order to push the changes select the folder(s) you would like to upload under the *'git'* tab in R studio. After selecting your files commit them using the *'commit'* button. Once you have committed remember to hit the *'push'* button. Now you can check the github repository to see your changes.
