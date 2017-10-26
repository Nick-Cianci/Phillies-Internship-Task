# Phillies-Internship-Task
This repository includes the source code for a html output for computing the Qualified Offer named mlb_salaries.html, as well as the rmarkdown file called mlb_salaries.rmd, along with this README file which includes step-by-step instructions on how I completed the data science portion of the task, and my responses to the open ended questions which is named Responses.
 

The output I produced for the Two-Part Question Option 2 Part B can be found in the word document called Calculating_Qualified_Offer.docz in this respository OR copy and paste the following link into a web browser to view the html output; file:///C:/Users/Nicholas/Documents/MLB%20salaries/mlb_salaries.html . This task was completed entriely in RStudio. All packages used are free and readily available to be installed and used.  

In order to access this application, r and rstudio must be installed.  Complete the following steps to install and run the application successfully. 

To Install R on Windows:

Go to the following website www.r-project.org
Click the "download R" link in the middle of the page under "Getting Started."
Select a CRAN location (pick the closest location) and click the corresponding link.  
Click on the "Download R for Windows" if you run Windows. The link is at the top of the page.  
Click on the "install R for the first time" link at the top of the page.
Click "Download R for Windows" and save the executable file somewhere on your computer.  Run the .exe file and follow the installation instructions.  
Now that R is installed, you need to download and install RStudio. 

To Install RStudio on Windows:

Go to www.rstudio.com and click on the "Download RStudio" button.
Click on "Download RStudio Desktop."
Click on the version recommended for your system, or the latest Windows version, and save the executable file.  Run the .exe file and follow the installation instructions. 


Install R, RStudio, and R Commander in Mac OS X:

Open this url in a web browser: http://cran.us.r-project.org/ 

click on “Download R for Mac OS X” > “R-2.x.x.pkg (latest version)” 

Follow the installation wizards instructions (the default settings are fine)

Download RStudio from the following url: http://rstudio.org/download/desktop.

Install RStudio by dragging the application icon to your Applications folder.

Download Tcl/Tk from http://cran.r-project.org/bin/macosx/tools/ (click on tcltk-8.x.x-x11.dmg; OS X needs this to run R Commander.)

Install Tcl/Tk.

Go to your Applications folder and find a folder named Utilities. Verify that you have a program named “X11” there. If not, go to http://xquartz.macosforge.org/ and download and install the latest version of XQuartz.

X11 in Applications/Utilities

Open RStudio.

Go to the “Packages” tab and click on “Install Packages”. The first time you’ll do this you’ll be prompted to choose a CRAN mirror. R will download all necessary files from the server you select here. Choose the location closest to you (probably “USA CA 1” or “USA CA 2”, which are housed at UC Berkeley and UCLA, respectively).

Install packages in OS X

Start typing “Rcmdr” until you see it appear in a list. Select the first option (or finish typing Rcmdr), ensure that “Install dependencies” is checked, and click “Install”.

Install Rcmdr in OS X

Wait while all the parts of the R Commander package are installed.

Once both Rstudio and R are installed, open the Rstudio shell. 
In order to open the mlb_salaries.rmd file, click on the clone or download button located at the top right hand corner of this github repository. 
Click "Download Zip". Once the Zip file is downloaded, go into the zip file and right click on the file called mlb_salaries.rmd and click open. 
This should open the file in the Rstudio environment. Finally hit the knit button in the upper left hand corner which should output my response as an html file.


Step-by-step instructions on creating the response:

The first step is installing all the necessary packages.
The packages used are as follows:
  'DataComputing'
  'rvest'
  'readr'
  'scales'
  'knitr'
  
1. To install all of these packages, use the command install.packages(). At the top of this code chunk, I set echo, eval, message, and warning equal to False because these packages were previously installed in my RStudio.To avoid receiving sloppy warnings and error messages in the knitted Html file, these commands tell R to not evaluate the code chunk but keeps the source code for others who will need to install the packages. 
Ex. install.packages('rvest')
    {r, eval = False}

2. Once the packages are installed, use the command library() to load in the packages from the previous step. From this point on, message and warning are set to FAlSE for every code chunk to ensure a clean Html output.
Ex. library('rvest')

3. Read the url into R by using the command read_html() from the rvest package. 
Ex. read_html('https://myurl.com')

4. Create the data table from data scraped from the provided url. This can be done using html_nodes() and html_table() both from the rvest package. Next name the columns of the table by using the command names() and assigning proper labels. Display the top 6 rows of the data table in order to visualize the data by using the head() command and the kable() command from the knitr package to make the display more visually appealling. 
Ex. html_nodes(webpage, 'table')
    names(plr_sal) <- c('Player Name', 'Salary ($)')
    
5. Start the Data cleaning process by removing all rows that are missing data. This can be done by using a pipeline from the DataComputing package. The filter() is used to keep all the rows that do not have missing salary data. 

Ex. table %>%
      filter(column != 'no salary data')

6. Continue the Data cleaning process by extracting just the number from the salary ($) column and sorting them in descending order. The commands parse_number() and sort() can be used to accomplish this. 
Ex. sort(data, descreasing = TRUE)

7. Compute the average of the top 125 Major League Salaries (The Qualified Offer) by using the slicing the sorted data and using the mean() function on it. Use the dollar_format() command to format the Qualified Offer as currency ($16,000,000 instead of 16000000)
Ex. sorted[0:124] returns the top 125 rows in the data table sorted
    dollar_format()(Qualified Offer)
    
8. Use the paste() command to output a sentence and show the upcoming Qualified Offer.
Ex. paste('Sentence',Qualified_Offer)

9. Using the sorted and parsed salary data, create a density plot of all the major league salaries and have the Qualified Offer represented as a vertical line overlayed on top of the density plot in order to compare the Qualified Offer against the rest of the league's salaries. This can be accomplished by using commands such as ggplot(), geom_density(), and geom_vline(). 

To take a look at the Qualified Offer in a smaller scope, the same density plot can be made but on a smaller portion of the data, as long as the Qualified Offer lies in that portion. To look at the Qualified Offer against the top half of the leagues salaries, just take subset the salary column by taking the length of the data divided by 2. 
Ex. clean_sal$`Salary ($)`<-clean_sal$`Salary ($)`[0:(length(clean_sal$`Salary ($)`)/2)]




