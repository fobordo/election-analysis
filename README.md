# Election Analysis

## Overview of Election Audit
  
The purpose of the Election Audit was to aid the Colorado Board of Elections Committee in analyzing the [tabulated election results](https://github.com/fobordo/election-analysis/blob/bbee13297e47ac142ab7102fc71465b9ae1a6401/Resources/election_results.csv) of the U.S. Congressional Precinct in Colorado. The goal of the Election Audit was to determine the total number of votes cast, total number of votes for each candidate, percentage of votes for each candidate, and the winner of the election based on the popular vote. The programming language, Python, was used to analyze and output the final election results. 

## Dependencies and File Paths

The Election Audit was analyzed by first adding dependencies to the script to increase the functional programming of the code. Using the `import` statement, the Python's built-in `csv` module was imported so the script could pull in data from the external election results CSV file and perform operations on it. The `import` statement was also used to import the `os` module, which was necessary to interact with the operating system. 
  
```Python
# Add our dependencies.
import csv
import os
```

To load `election_results.csv`, chaining was used to connect the `os.path` submodule, which allows the user to access files on different operating systems, like macOS and Windows, with the `join()` function, which joins the file path components together and returns a direct path. Within the parantheses of the `join()` function, the name of the folder that contained `election_results.csv`, "Resources", and the name of the election results CSV file, "election_results.csv", were added. The `os.path.join("Resources", "election_results.csv")` expression was stored in the `file_to_load` variable.

```Python
# Add a variable to load a file from a path.
file_to_load = os.path.join("Resources", "election_results.csv")
```

It was determined that the election analysis data would be written to the text file named "election_analysis.txt," which was located in the "analysis" folder. As such, the `os.path.join("analysis", "election_analysis.txt")` expression was stored in the variable `file_to_save`, which would later be used to indicate where to write the election analysis data.

```Python
# Add a variable to save the file to a path.
file_to_save = os.path.join("analysis", "election_analysis.txt")
```
  
Once these dependencies and variables were established, we obtained the results of the Election Audit. 

## Election-Audit Results

* **A total of 369,711 votes were cast in this congressional election.**
  
  To determine the total number of votes cast in this election, first, the variable `total_votes` was initialized and set to equal zero.
    
  ```
  total_votes = 0
  ```
 
  Using the `with` statement and `open()` function on `file_to_load`, `election_results.csv` was opened and stored in the variable `election_data`. Then, the `csv` module was used with the `reader` function to read `election_data`, and stored in the variable `reader`.
  
  ```Python
  # Read the csv and convert it into a list of dictionaries
  with open(file_to_load) as election_data:
    reader = csv.reader(election_data)
  ```
  
  The `next()` method was used on `reader` to skip the header/first row of the CSV file since the column headers were not needed, and stored in the variable `header`.
    
  ```Python
    # Read the header
    header = next(reader)
  ```
   
  Then, a `for` loop was written to loop through each row in `reader` and increment the total vote count in `total_votes` by 1 after each loop.
     
  ```Python
    # For each row in the CSV file.
    for row in reader:

      # Add to the total vote count
      total_votes += 1
  ```
    
  Outside of the `for` loop and `with` statement, another `with` statement was written to open and save the results to the text file `election_analysis.txt`. Using the `with` statement and `open()` function on `file_to_save`, `election_analysis.txt` was opened, and stored in the variable `txt_file`.
    
  ```Python
  with open(file_to_save, "w") as txt_file:
  ```
  
  Within the `with` statement, the statement to print the "Election Results," "Total Votes," and "County Votes" headers, along with the `total_votes` was stored in the variable `election_results`, and printed to both the terminal and `txt_file`.
  
    ```Python
      election_results = (
          f"\nElection Results\n"
          f"-------------------------\n"
          f"Total Votes: {total_votes:,}\n"
          f"-------------------------\n\n"
          f"County Votes:\n")
          
      # Print the final vote count to the terminal
      print(election_results, end="")
      
      # Save the results to the election analysis text file.
      txt_file.write(election_results)
    ```
  
  The election analysis text file, `election_analysis.txt`, now included the "Election Results," "Total Votes," and "County Votes" headers, and the `total_votes`:
  
  ```
  Election Results
  -------------------------
  Total Votes: 369,711
  -------------------------

  County Votes:
  ```
  
* **A breakdown of the number of votes and the percentage of total votes for each county in the precinct were as follows:**
  * **Jefferson: 10.5% (38,855 votes)**
  * **Denver: 82.8% (306,055 votes)**
  * **Arapahoe: 6.7% (24,801 votes)**
  
  To determine the number of votes and the percentage of total votes for each county in the precint, first, the variable `county_list` was initialized as an empty list to later store county names, and `county_votes` was initialized as an empty dictionary to later store the total number of votes per county. 

  ```Python
  # Create a county list and county votes dictionary.
  county_list = []
  county_votes = {}
  ```
  
  Then, within the `with` statement to open and read the `election_results.csv` file,
  
  ```Python
  with open(file_to_load) as election_data:
    reader = csv.reader(election_data)

    # Read the header
    header = next(reader)
    ```
  
  a `for` loop was written to loop through each row in `reader` and extract the county name from the appropriate index, which in this case was "1" because county names were located in Column 2 of the CSV file. The extracted county name was then stored in the variable `county_name`.
  
  ```Python
    # For each row in the CSV file.
    for row in reader:

      # Extract the county name from each row.
      county_name = row[1]
  ```
  
  An `if` statement was nested inside of the `for` loop to check if `county_name` was added to the `county_list` yet. If `county_name` was `not in` `county_list`, the `county_name` was added to `county_list` with the `append()` method, and the number of county votes for that county would begin to be tracked within the `county_votes` dictionary.
  
  ```Python
      # If statement that checks that the county does not match any existing county in the county list.
      if county_name not in county_list:

        # Add the existing county to the list of counties.
        county_list.append(county_name)

        # Begin tracking the county's vote count.
        county_votes[county_name] = 0
  ```
  
  Outside of the `if` statement but still within the `for` loop, the `county_votes` dictionary was set to increment the number of votes for the current `county_name` by 1 for each row in the loop.
  
  ```Python
    # Add a vote to current county's vote count.
    county_votes[county_name] += 1
  ```
  
  Then, within the `with` statement to open and save results to `election_analysis.txt`,
  
  ```Python
  # Save the results to our text file.
  with open(file_to_save, "w") as txt_file:
  ```
  
  a `for` loop was written to loop through each `county_name` in the `county_votes` dictionary, and `get` the corresponding total votes for that county, which was stored in the variable `county_vote_count`. Then, the percentage of total votes for that county was calculated and stored in the variable `county_percentage`.
  
  ```Python
    # For loop to get the county from the county dictionary.
    for county_name in county_votes:

      # Retrieve the county vote count.
      county_vote_count = county_votes.get(county_name)

      # Calculate the percentage of votes for the county.
      county_percentage = float(county_vote_count) / float(total_votes) * 100
  ```
    
  Finally, still within the `for` loop, the statement to print the `county_name`, `county_percentage`, and `county_vote_count` was stored in the variable `county_results`. Upon each loop, the `county_results` statement was printed to both the terminal and `txt_file`.
    
  ```Python
      county_results = (f"{county_name}: {county_percentage:.1f}% ({county_vote_count:,})\n")

      # Print the county results to the terminal.
      print(county_results)

      # Save the county votes to a text file.
      txt_file.write(county_results)
  ```
  
  The election analysis text file, `election_analysis.txt`, now included the results for each county:
   
  ```
  Election Results
  -------------------------
  Total Votes: 369,711
  -------------------------

  County Votes:
  Jefferson: 10.5% (38,855)
  Denver: 82.8% (306,055)
  Arapahoe: 6.7% (24,801)
  ```
  
* **The county with the largest number of votes was Denver.**
  
  To determine which county had the largest number of votes, first, the following three variables were initialized:
  
  ```Python
  # Track the largest county and county voter turnout.
  largest_county_turnout = ""
  largest_county_votes = 0
  largest_county_percentage = 0
  ```
  - `largest_county_turnout` was initialized as an empty string to later represent the name of the county with the largest number of votes.
  - `largest_county_votes` was set to zero to later represent the total number of votes of the county with the largest voter turnout.
  - `largest_county_percentage` was set to zero to later represent the percentage of total votes of the county with the largest voter turnout.

  Then, within the `with` statement to open and save results to `election_analysis.txt`,
  
  ```Python
  with open(file_to_save, "w") as txt_file:
  ```
   
  and inside of the `for` loop to get each `county_name` from the `county_votes` dictionary, 
  
  ```Python
    # For loop to get the county from the county dictionary.
    for county_name in county_votes:
  ```
  
   an `if` statement was added. Upon each loop, the `if` statement checked if the current county's votes, `county_vote_count`, was greater than `largest_county_votes` *and* if the current county's vote percentage, `county_percentage`, was greater than `largest_county_percentage`. If both conditions were `true`, `largest_county_votes` was set equal to `county_vote_count`, `largest_county_turnout` equal to `county_name`, and `largest_county_percentage` equal to `county_percentage`.
  
  ```Python
      # If statement to determine the winning county and get its vote count.
      if (county_vote_count > largest_county_votes) and (county_percentage > largest_county_percentage):
        largest_county_votes = county_vote_count
        largest_county_turnout = county_name
        largest_county_percentage = county_percentage
  ```

  Outside of the `for` loop, the statement to print the `largest_county_turnout` was stored in the variable `largest_county_turnout_summary`, which was printed to both the terminal and `txt_file`.
  
  ```Python
    largest_county_turnout_summary = (
        f"\n-------------------------\n"
        f"Largest County Turnout: {largest_county_turnout}\n"
        f"-------------------------\n")
        
    # Print the county with the largest turnout to the terminal.
    print(largest_county_turnout_summary)

    # Save the county with the largest turnout to a text file.
    txt_file.write(largest_county_turnout_summary)
  ```
    
  The election analysis text file, `election_analysis.txt`, now included the county with the largest voter turnout:
    
  ```
  Election Results
  -------------------------
  Total Votes: 369,711
  -------------------------

  County Votes:
  Jefferson: 10.5% (38,855)
  Denver: 82.8% (306,055)
  Arapahoe: 6.7% (24,801)

  -------------------------
  Largest County Turnout: Denver
  -------------------------
  ```

* **A breakdown of the number of votes and the percentage of the total votes each candidate received were as follows:**
  * Charles Casper Stockham: 23.0% (85,213 votes)
  * Diana DeGette: 73.8% (272,892 votes)
  * Raymon Anthony Doane: 3.1% (11,606 votes)

  To determine the number of votes and the percentage of the total votes each candidate received, first, the variable `candidate_options` was initialized as an empty list to later store candidate names, and `candidate_votes` was initialized as an empty dictionary to later store the total number of votes per candidate. 

  ```Python
  # Candidate Options and candidate votes.
  candidate_options = []
  candidate_votes = {}
  ```
  
  Then, within the `with` statement to open and read the `election_results.csv` file,
  
  ```Python
  # Read the csv and convert it into a list of dictionaries
  with open(file_to_load) as election_data:
    reader = csv.reader(election_data)

    # Read the header
    header = next(reader)
  ```

  a `for` loop was written to loop through each row in `reader` and extract the candidate name from the appropriate index, which in this case was "2" because candidate names were located in Column 3 of the CSV file. The extracted candidate name was then stored in the variable `candidate_name`.
  
  ```Python
    # For each row in the CSV file.
    for row in reader:
        
      # Get the candidate name from each row.
      candidate_name = row[2]
  ```
  
  An `if` statement was nested inside of the `for` loop to check if the `candidate_name` was added to the `candidate_options` list yet. If the `candidate_name` was `not in` `candidate_options`, the `candidate_name` was added to `candidate_options` with the `append()` method, and the number of votes for that candidate would begin to be tracked within the `candidate_votes` dictionary.
  
  ```Python
      # If the candidate does not match any existing candidate add it to the candidate list
      if candidate_name not in candidate_options:

        # Add the candidate name to the candidate list.
        candidate_options.append(candidate_name)

        # Begin tracking that candidate's voter count.
        candidate_votes[candidate_name] = 0
  ```
  
  Outside of the `if` statement but still within the `for` loop, the `candidate_votes` dictionary was set to increment the number of votes for the current `candidate_name` by 1 for each row in the loop.
  
  ```Python
      # Add a vote to that candidate's count
      candidate_votes[candidate_name] += 1
  ```
  
  Then, within the `with` statement to open and save results to `election_analysis.txt`,
  
  ```Python
  # Save the results to our text file.
  with open(file_to_save, "w") as txt_file:
  ```
  
  a `for` loop was written to loop through each `candidate_name` in the `candidate_votes` dictionary, and `get` the corresponding total votes for that candidate, which was stored in the variable `votes`. Then, the percentage of total votes for that candidate was calculated and stored in the variable `vote_percentage`.
  
  ```Python
    for candidate_name in candidate_votes:

      # Retrieve vote count and percentage
      votes = candidate_votes.get(candidate_name)
      vote_percentage = float(votes) / float(total_votes) * 100
  ```
    
    Finally, still within the `for` loop, the statement to print the `candidate_name`, `vote_percentage`, and `votes` was stored in the variable `candidate_results`. Upon each loop, the `candidate_results` statement was printed to both the terminal and `txt_file`.
    
  ```Python
      candidate_results = (f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")

      # Print each candidate's voter count and percentage to the terminal.
      print(candidate_results)
      
      #  Save the candidate results to our text file.
      txt_file.write(candidate_results)
  ```
  
  The election analysis text file, `election_analysis.txt`, now included the results for each candidate:
   
  ```
  Election Results
  -------------------------
  Total Votes: 369,711
  -------------------------

  County Votes:
  Jefferson: 10.5% (38,855)
  Denver: 82.8% (306,055)
  Arapahoe: 6.7% (24,801)

  -------------------------
  Largest County Turnout: Denver
  -------------------------
  Charles Casper Stockham: 23.0% (85,213)
  Diana DeGette: 73.8% (272,892)
  Raymon Anthony Doane: 3.1% (11,606)
  ```

* **Diana DeGette won the election with a vote count of 272,892 votes, which was 73.8% of the total votes.**
  
  To determine which candidate won the election, their vote count, and their percentage of the total votes, first, the following three variables were initialized:
  
  ```Python
  # Track the winning candidate, vote count and percentage
  winning_candidate = ""
  winning_count = 0
  winning_percentage = 0
  ```
    
  - `winning_candidate` was initialized as an empty string to later represent the name of the candidate with the largest number of votes.
  - `winning_count` was set to zero to later represent the total number of votes of the winning candidate.
  - `winning_percentage` was set to zero to later represent the percentage of total votes of the winning candidate.

  Then, within the `with` statement to open and save results to `election_analysis.txt`,
  
  ```Python
  with open(file_to_save, "w") as txt_file:
  ```
 
  and inside of the `for` loop to get each `county_name` from the `county_votes` dictionary,
  
  ```Python
    for candidate_name in candidate_votes:
  ```
  
  an `if` statement was added. Upon each loop, the `if` statement checked if the current candidate's total votes, `votes`, was greater than `winning_count` *and* if the current candidate's percentage of votes, `vote_percentage`, was greater than `winning_percentage`. If both conditions were `true`, `winning_count` was set equal to `votes`, `winning_candidate` equal to `candidate_name`, and `winning_percentage` equal to `vote_percentage`.
  
  ```Python
      # Determine winning vote count, winning percentage, and candidate.
      if (votes > winning_count) and (vote_percentage > winning_percentage):
        winning_count = votes
        winning_candidate = candidate_name
        winning_percentage = vote_percentage
  ```

  Outside of the `for` loop, the statement to print the `winning_candidate`, `winning_count`, and `winning_percentage` was stored in the variable `winning_candidate_summary`, which was printed to both the terminal and `txt_file`.
  
  ```Python
    winning_candidate_summary = (
        f"-------------------------\n"
        f"Winner: {winning_candidate}\n"
        f"Winning Vote Count: {winning_count:,}\n"
        f"Winning Percentage: {winning_percentage:.1f}%\n"
        f"-------------------------\n")
        
    # Print the winning candidate (to terminal)
    print(winning_candidate_summary)

    # Save the winning candidate's name to the text file
    txt_file.write(winning_candidate_summary)
  ```
  The election analysis text file, `election_analysis.txt`, now included the county with the winning candidate summary:
    
  ```
  Election Results
  -------------------------
  Total Votes: 369,711
  -------------------------

  County Votes:
  Jefferson: 10.5% (38,855)
  Denver: 82.8% (306,055)
  Arapahoe: 6.7% (24,801)

  -------------------------
  Largest County Turnout: Denver
  -------------------------
  Charles Casper Stockham: 23.0% (85,213)
  Diana DeGette: 73.8% (272,892)
  Raymon Anthony Doane: 3.1% (11,606)
  -------------------------
  Winner: Diana DeGette
  Winning Vote Count: 272,892
  Winning Percentage: 73.8%
  -------------------------
  ```

## Election-Audit Summary:
The Election Audit script can easily be used for any election, with a few modifications. Below are a few examples of modifications that can be made for the analysis of other elections:

1. If the file type of the election results file is not CSV, another built-in module can be imported in order to pull in data from external files and perform operations on them:

    ```Python
    import csv
    ```
  
    * `csv` can be replaced with the appropriate Python module corresponding to the new election result file's file type.


2. The folder and file names of other election results can be changed in the `file_to_load` variable so the new data can be read from the appropriate path:

    ```Python
    # Add a variable to load a file from a path.
    file_to_load = os.path.join("Resources", "election_results.csv")
    ```

    * `Resources` can be replaced with the folder name of the folder that contains the election results file.
    * `election_results.csv` can be replaced with the file name of the file that contains the election results data.


3. The folder and file name of the election analysis can be changed in the `file_to_save` variable so the analysis results can be written to the appropriate file:
  
    ```Python
    file_to_save = os.path.join("analysis", "election_analysis.txt")
    ```

    * `analysis` can be replaced with the folder name of the folder that contains the file that the analysis results will be written to.
    * `election_analysis.txt` can be replaced with the file name of the file that the analysis results will be written to.


4. The index numbers that are used to retrieve data (i.e. candidate name and county name) from the election results file can be changed to reference the appropriate columns to obtain the desired data:

    ```Python
    # For each row in the CSV file.
    for row in reader:

        # Get the candidate name from each row.
        candidate_name = row[2]

        # Get the county name from each row.
        county_name = row[1]
    ```

    * In the `candidate_name = row[2]` expression, the number `2` can be changed to the index of the appropriate column in the election results file that contains the candidate names.
    * In the `county_name = row[1]` expression, the number `1` can be changed to the index of the appropriate column in the election results file that contains the county names.

The rest of the script may remain the same to return the same election analysis results as those that were returned from this project.
