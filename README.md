# Phillies-Internship-Task
This repository includes the source code for a html output for computing the Qualified Offer named mlb_salaries.html, as well as the rmarkdown file called mlb_salaries.rmd, along with this README file which includes step-by-step instructions to completing the data science portion of the task, and my responses to the open ended questions which is named Responses.
 

The full response to the Two-Part Question Option 2 Part B can be found at the Calculating_Qualified_Offer.docz file.This task was completed entriely in RStudio. All packages used are free and readily available for use.  

Step-by-step instructions:

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




