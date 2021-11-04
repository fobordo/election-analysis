# Election Analysis

## Overview of Election Audit
  
The purpose of the Election Audit was to aid the Colorado Board of Elections Committee in analyzing the [tabulated election results](https://github.com/fobordo/election-analysis/blob/bbee13297e47ac142ab7102fc71465b9ae1a6401/Resources/election_results.csv) of the U.S. Congressional Precinct in Colorado. The goal of the Election Audit was to determine the total number of votes cast, total number of votes for each candidate, percentage of votes for each candidate, and the winner of the election based on the popular vote. The programming language, Python, was used to analyze and output the final election results.

## Election-Audit Results

* **A total of 369,711 votes were cast in this congressional election.**
  
  To determine the total number of votes cast in this election, first, the variable `total_votes` was initialized and set to equal zero.
    
    ```
    total_votes = 0
    ```
 
  ***Include text for opening election results csv***
    ```Python
    # Read the csv and convert it into a list of dictionaries
    with open(file_to_load) as election_data:
      reader = csv.reader(election_data)

      # Read the header
      header = next(reader)
    ```

  Then, a `for` loop was written to loop through each row in the election results CSV file and increment the total vote count in `total_votes` by 1 after each       loop.
  
    ```Python
    # For each row in the CSV file.
    for row in reader:
    
        # Add to the total vote count
        total_votes += 1
    ```

  Finally, the statement to print the "Election Results," "Total Votes," and "County Votes" headers, along with the `total_votes` was set equal to the variable `election_results`, and printed to both the terminal and the election analysis text file.
  
    ```Python
    with open(file_to_save, "w") as txt_file:

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
  
  As a result, the number of total votes was printed onto the election analysis text file, along with the "Election Results" title and "County Votes" header:
  
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
  
  To determimne the number of votes and the percentage of total votes for each county in the precint, first, the variable `county_list` was initialized as an empty list to later store county names, and `county_votes` was initialized as an empty dictionary to later store the total number of votes per county. 

    ```Python
    # Create a county list and county votes dictionary.
    county_list = []
    county_votes = {}
    ```
  
  Then, a `for` loop was written to loop through each row in the election results CSV file and extract the county name each row.
  
    ```Python
    # For each row in the CSV file.
    for row in reader:

        # Add to the total vote count
        total_votes += 1

        # Get the candidate name from each row.
        candidate_name = row[2]

        # Extract the county name from each row.
        county_name = row[1]
    ```
  
  An `if` statement was nested inside of the `for` loop to check if the county name was added to the `county_list` yet. If not, the county name would be added to `county_list`, and the number of county votes for that county would begin to be tracked within the `county_votes` dictionary.
  
    ```Python
    # If statement that checks that the county does not match any existing county in the county list.
    if county_name not in county_list:

            # Add the existing county to the list of counties.
            county_list.append(county_name)

            # Begin tracking the county's vote count.
            county_votes[county_name] = 0
    ```
  
  Outside of the `if` statement, the `county_votes` dictionary was set to increment the number of votes for the current `county_name` by 1 for each row in the `for` loop.
  
    ```Python
    # Add a vote to current county's vote count.
    county_votes[county_name] += 1
    ```
  
  Once the `for` loop finished looping through all the rows in the election results CSV file, a new `for` loop was written. The new `for` loop would loop through each `county_name` in the `county_votes` dictionary, and retrieve the corresponding total votes for that county, which was stored in the variable `county_vote_count`. Then, the percentage of total votes for that county was calculated and stored in the variable `county_percentage`.
  
    ```Python
    # For loop to get the county from the county dictionary.
    for county_name in county_votes:

          # Retrieve the county vote count.
          county_vote_count = county_votes.get(county_name)

          # Calculate the percentage of votes for the county.
          county_percentage = float(county_vote_count) / float(total_votes) * 100

    ```
    
    Finally, still within the `for` loop, the statement to print the `county_name`, `county_percentage`, and `county_vote_count` was set equal to the variable `county_results`. Upon each loop, the `county_results` were printed to both the terminal and the election analysis text file.
    
    ```Python
          county_results = (f"{county_name}: {county_percentage:.1f}% ({county_vote_count:,})\n")

          # Print the county results to the terminal.
          print(county_results)
          
          # Save the county votes to a text file.
          txt_file.write(county_results)
    ```
  
  The resulting election analysis text file now included the results for each county:
   
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
  
  To determine which county had the largest number of votes, first, the following three variables were initialized outside of the `for` loop:
  
    ```Python
    # Track the largest county and county voter turnout.
    largest_county_turnout = ""
    largest_county_votes = 0
    largest_county_percentage = 0
    ```
    - `largest_county_turnout` was initialized as an empty string to later represent the name of the county with the largest number of votes.
    - `largest_county_votes` was set to zero to later represent the total number of votes of the county with the largest voter turnout.
    - `largest_county_percentage` was set to zero to later represent the percentage of total votes of the county with the largest voter turnout.

    
  Back inside of the `for` loop to get each `county_name` from the `county_votes` dictionary, an `if` statement was added. Upon each loop, the `if` statement checked if `county_vote_count` was greater than the `largest_county_votes` *and* the `county_percentage` was greater than the `largest_county_percentage`. If both conditions were `true`, the `largest_county_votes` was set equal to the `county_vote_count`, `largest_county_turnout` equal to `county_name`, and `largest_county_percentage` equal to `county_percentage`.
  
    ```Python
    # If statement to determine the winning county and get its vote count.
    if (county_vote_count > largest_county_votes) and (county_percentage > largest_county_percentage):
      largest_county_votes = county_vote_count
      largest_county_turnout = county_name
      largest_county_percentage = county_percentage
    ```

  Outside of the `for` loop, the statement to print the `largest_county_turnout` was set equal to the variable `largest_county_turnout_summary`, which was printed to both the terminal and the election analysis text file.
  
    ```Python
    # Print the county with the largest turnout to the terminal.
    largest_county_turnout_summary = (
        f"\n-------------------------\n"
        f"Largest County Turnout: {largest_county_turnout}\n"
        f"-------------------------\n")
    print(largest_county_turnout_summary)

    # Save the county with the largest turnout to a text file.
    txt_file.write(largest_county_turnout_summary)
    ```
  The resulting election analysis text file now included the county with the largest voter turnout:
    
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

* **Provide a breakdown of the number of votes and the percentage of the total votes each candidate received.**
* **Which candidate won the election, what was their vote count, and what was their percentage of the total votes?**

## Election-Audit Summary: 
  In a summary statement, provide a business proposal to the election commission on how this script can be used—with some modifications—for any election. Give at     least two examples of how this script can be modified to be used for other elections.
