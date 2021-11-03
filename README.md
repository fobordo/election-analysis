# Election Analysis

## Overview of Election Audit
  Explain the purpose of this election audit analysis.

## Election-Audit Results

* A total of 369,711 votes were cast in this congressional election.
  
  To determine the total number of votes cast in this congression election, first, a total_votes variable was initialized and set to equal zero.
  
  ![Initialize Total Votes Variable](/Screenshots/TotalVotes_Initialize.png)
  
  Then, a for loop was written to loop through each row in the election results CSV file and increment the number of total_votes by 1 after each loop.
  
  ![Total Votes For Loop](/Screenshots/TotalVotes_ForLoop.png)

  Finally, script was written to print the number of total votes to the election analysis text file.
  
  ![Total Votes Results Script](/Screenshots/TotalVotes_Results.png)
  
  As a result, the number of total votes was printed onto the election analysis text file, along with the "Election Results" title and "County Votes" header:
  
  ![Total Votes Text File](/Screenshots/TotalVotes_TextFile.png)
  
* A breakdown of the number of votes and the percentage of total votes for each county in the precinct were as follows:
  * Jefferson: 10.5% (38,855 votes)
  * Denver: 82.8% (306,055 votes)
  * Arapahoe: 6.7% (24,801 votes)
  
  To determimne the number of votes and the percentage of total votes for each county in the precint, first, a variable called "county_list" was initialized as an     empty list to later store county names, and "county_votes" was initialized as an empty dictionary to later store the total number of votes per county name. 
  
  ![County Name List and County Votes Dictionary](/Screenshots/County_Initialize.png)
  
  Then, a for loop was written to loop through each row in the election results CSV file and extract the county name for each row.
  
  ![County Name Extraction](/Screenshots/County_NameExtraction.png)
  
  An if statement was nested inside of the for loop to check if the county name was added to the county_list yet. If not, the county name would be added to           county_list, and the number of county votes for that county would begin to be tracked within the county_votes dictionary.
  
  ![County List Creation and Begin Vote Tracking](/Screenshots/County_List.png)
  
  Outside of the if statement, the county_votes dictionary was set to increment the number of votes for the current county name by 1 for each row in the for loop.
  
  ![County Vote Counting](/Screenshots/County_Votes.png)
  
  Once the for loop finished looping through all the rows in the election results CSV file, a new for loop was written. The new for loop would loop through each county name in the county_votes dictionary, and retrieve the corresponding total votes for that county name. Then, the percentage of total votes for that county name was calculated. Finally, the county name, percentage of total votes, and total number of county votes are printed to the election analysis text file.
  
  ![County Results Script](/Screenshots/County_Results.png)
  
  The resulting election analysis text file now included the results for each county:
  
  ![County Results Text File](/Screenshots/County_TextFile.png)
  
* Which county had the largest number of votes?
* Provide a breakdown of the number of votes and the percentage of the total votes each candidate received.
* Which candidate won the election, what was their vote count, and what was their percentage of the total votes?

## Election-Audit Summary: 
  In a summary statement, provide a business proposal to the election commission on how this script can be used—with some modifications—for any election. Give at     least two examples of how this script can be modified to be used for other elections.
