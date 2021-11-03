# Election Analysis

## Overview of Election Audit
  Explain the purpose of this election audit analysis.

## Election-Audit Results
 Using a bulleted list, address the following election outcomes. Use images or examples of your code as support where necessary.

* How many votes were cast in this congressional election?
  * A total of 369,711 votes were cast in this congressional election.
  
  To determine the total number of votes cast in this congression election, first, a total_votes variable was initialized and set to equal zero.
  ![Initialize Total Votes Variable](/Screenshots/TotalVotes_Initialize.png)
  
  Then, a for loop was written to loop through each row in the election results CSV file and increment the number of total_votes by 1 after each loop.
  ![Total Votes For Loop](/Screenshots/TotalVotes_ForLoop.png)

  Finally, script was written to print the number of total votes to the election analysis text file.
  ![Total Votes Results Script](/Screenshots/TotalVotes_Results.png)
  
  As a result, the number of total votes was printed onto the election analysis text file, along with the "Election Results" title and "County Votes" header:
  ![Total Votes Text File](/Screenshots/TotalVotes_TextFile.png)
  
* Provide a breakdown of the number of votes and the percentage of total votes for each county in the precinct.
  * The number of votes and the percentage of total votes for each county in the precinct were as follows:
    * Jefferson: 10.5% (38,855)
    * Denver: 82.8% (306,055)
    * Arapahoe: 6.7% (24,801)
 
* Which county had the largest number of votes?
* Provide a breakdown of the number of votes and the percentage of the total votes each candidate received.
* Which candidate won the election, what was their vote count, and what was their percentage of the total votes?

## Election-Audit Summary: 
  In a summary statement, provide a business proposal to the election commission on how this script can be used—with some modifications—for any election. Give at     least two examples of how this script can be modified to be used for other elections.
