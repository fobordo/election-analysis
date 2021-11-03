# Election Analysis

## Overview of Election Audit
  
The purpose of the Election Audit was to aid the Colorado Board of Elections Committee in analyzing the [tabulated election results](https://github.com/fobordo/election-analysis/blob/bbee13297e47ac142ab7102fc71465b9ae1a6401/Resources/election_results.csv) of the U.S. Congressional Precinct in Colorado. The goal of the Election Audit was to determine the total number of votes cast, total number of votes for each candidate, percentage of votes for each candidate, and the winner of the election based on the popular vote. The programming language, Python, was used to analyze and output the final election results.

## Election-Audit Results

* A total of 369,711 votes were cast in this congressional election.
  
  To determine the total number of votes cast in this election, first, the variable `total_votes` was initialized and set to equal zero.
    
    ```
    total_votes = 0
    ```
    
  Then, a `for` loop was written to loop through each row in the election results CSV file and increment the number of `total_votes` by 1 after each loop.
  
      ```Python
      # Read the csv and convert it into a list of dictionaries
      with open(file_to_load) as election_data:
      reader = csv.reader(election_data)

      # Read the header
      header = next(reader)

      # For each row in the CSV file.
      for row in reader:

          # Add to the total vote count
          total_votes += 1
      ```

  Finally, script was written to print the number of total votes to the election analysis text file.
  
    ```Python
    # Save the results to our text file.
    with open(file_to_save, "w") as txt_file:

      # Print the final vote count (to terminal)
      election_results = (
          f"\nElection Results\n"
          f"-------------------------\n"
          f"Total Votes: {total_votes:,}\n"
          f"-------------------------\n\n"
          f"County Votes:\n")
      print(election_results, end="")

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
  
* A breakdown of the number of votes and the percentage of total votes for each county in the precinct were as follows:
  * Jefferson: 10.5% (38,855 votes)
  * Denver: 82.8% (306,055 votes)
  * Arapahoe: 6.7% (24,801 votes)
  
  To determimne the number of votes and the percentage of total votes for each county in the precint, first, a variable called "county_list" was initialized as an   empty list to later store county names, and "county_votes" was initialized as an empty dictionary to later store the total number of votes per county name. 

    ```Python
    county_list = []
    county_votes = {}
    ```
  
  Then, a for loop was written to loop through each row in the election results CSV file and extract the county name for each row.
  
    ```Python
    for row in reader:

        # Add to the total vote count
        total_votes += 1

        # Get the candidate name from each row.
        candidate_name = row[2]

        # 3: Extract the county name from each row.
        county_name = row[1]
    ```
  
  An if statement was nested inside of the for loop to check if the county name was added to the county_list yet. If not, the county name would be added to           county_list, and the number of county votes for that county would begin to be tracked within the county_votes dictionary.
  
    ```Python
    if county_name not in county_list:

            # 4b: Add the existing county to the list of counties.
            county_list.append(county_name)

            # 4c: Begin tracking the county's vote count.
            county_votes[county_name] = 0
    ```
  
  Outside of the if statement, the county_votes dictionary was set to increment the number of votes for the current county name by 1 for each row in the for loop.
  
    ```Python
    county_votes[county_name] += 1
    ```
  
  Once the for loop finished looping through all the rows in the election results CSV file, a new for loop was written. The new for loop would loop through each     county name in the county_votes dictionary, and retrieve the corresponding total votes for that county name. Then, the percentage of total votes for that county   name was calculated. Finally, the county name, percentage of total votes, and total number of county votes are printed to the election analysis text file.
  
  ```Python
  for county_name in county_votes:

        # 6b: Retrieve the county vote count.
        county_vote_count = county_votes.get(county_name)

        # 6c: Calculate the percentage of votes for the county.
        county_percentage = float(county_vote_count) / float(total_votes) * 100
        county_results = (
            f"{county_name}: {county_percentage:.1f}% ({county_vote_count:,})\n")

        # 6d: Print the county results to the terminal.
        print(county_results)

        # 6e: Save the county votes to a text file.
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
  
* The county with the largest number of votes was Denver.
  
  To determine which county had the largest number of votes,...

* Provide a breakdown of the number of votes and the percentage of the total votes each candidate received.
* Which candidate won the election, what was their vote count, and what was their percentage of the total votes?

## Election-Audit Summary: 
  In a summary statement, provide a business proposal to the election commission on how this script can be used—with some modifications—for any election. Give at     least two examples of how this script can be modified to be used for other elections.
