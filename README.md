# Phillies-Internship-Task
This repository includes the html output for computing the Qualified Offer named mlb_salaries.html, along with this README file which includes step-by-step instructions to completing the data science portion of the task, and my responses to the open ended questions.
 

The full response to the Two-Part Question Option 2 Part B can be found at the mlb_salaries.html file.This task was completed entriely in RStudio. All packages used are free and readily available for use.  

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



REQUIRED RESPONSE:
As a member of the Research and Development team, I would consider sabermetrics on the pitcher such as Adjusted Earned Run Average, Innings per Start, Strikeout-to-Walk ratio, and more to decide if a pitcher was ready for the show. Adjusted Earned Run Average normalizes a player’s earned run average across the entirety of the league. This statistic accounts for external factors like ballpark and opposing team. Once adjusted, a pitcher is compared to the rest of the league with a score of 100 being the league average. Being able to compare and rank a pitcher against his peers on a level playing field is an exciting concept and one with a lot of value. Statistics like Innings per Start and Pitches per Start help quantify the durability and consistency of a pitcher, two essential characteristics of a quality starter. The higher the Innings per Start and Pitches per Start means that the pitcher is durable and makes it deep into games, a valuable asset for a 162-game season. Raw strikeout and walk numbers can be misleading because a power pitcher can record many strikeouts while being wild and ineffective and a finesse pitcher can be successful while recording few strikeouts. The Strikeout-to-Walk ratio is a valuable replacement since it tells a more complete story. Sabermetrics alone are powerful tools but factors including work ethic, character, and injury-history are also pivotal to a player’s major league success. A conversation with the prospects minor-league coaches could provide additional insight about the player.

Source: 'http://m.mlb.com/glossary/advanced-stats'

Two-Part Question:

2. Part a response:

  Open source software is a computer software that allows users to modify its source code and change the software to fix bugs, make improvements or adapt the software for the user’s own needs. Open source software or OSS, encourages collaborative efforts which has both advantages and disadvantages. Since becoming a data science major about a year ago, my experiences with open-source software aren’t overly expansive however I have used OSS’s such as R, Python, MySQL, Atom, and Redis in varying degrees. Of the open source software that I have been exposed to, the worst is Redis for a variety of reasons. The first being that Redis requires three Masters each with two slaves to set up the architecture. Each Master has hash-slots assigned to them which shard the data. An issue with this is that when a Master who is holding slots fails, the data which was to be written to those slots will be lost. Additionally, your dataset must fit comfortably in the memory provided.  The whole dataset is stored in RAM which can be costly for the client as well. Yet another issue I have with Redis is that it supports no query language or joins which makes key management much more difficult than it has to be. New to the tech community, the fact that Redis uses a command line interface was off-putting to me. There are no user-friendly shell’s or applications to help work with the data as is the case with many other software including Python and R. 

	While Redis itself has some issues, there are also issues with open source software as a whole. OSS is meant to provide flexibility, freedom and cutting-edge technology to its users through collaborative work however this isn’t always the case. An issue many users have encountered is that their opinion or their feedback doesn’t actually matter. Reported bugs or suggested solutions are all too often ignored. The attitude seems to be if you can’t create the fix yourself the issue won’t be fixed. Even in situations where a functional patch was provided, users are often belittled and their work is disparaged leaving many users to stop contributing altogether. 

	Although OSS has issues, I find them more useful than harmful. Programming languages like Python and R which are often used for computer and data science applications and are both open source. These software are popular because they are free, generally simple to install, and have a plethora of documentation and support. In fact, R is my preferred software because of the sheer number of packages that are readily available. Packages are updated and added frequently giving the user access to many powerful tools. This is only possible because of the software’s large and active community. Open source software isn’t perfect. I could nitpick about every nuance I find slightly inconvenient but the fact of the matter is, with active community members all working collaboratively towards a common goal, amazing things can be accomplished for the benefit of the people.  


Source = 'https://betanews.com/2015/04/20/why-the-open-source-software-model-is-fundamentally-broken/ '
