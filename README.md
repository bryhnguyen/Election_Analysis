# Overview of Election Audit: Explain the purpose of this election audit analysis.
The purpose of this election audit analysis was to count the votes for 3 candidates (Charles Casper Stockham, Diana DeGette, Raymon Anthony Doane) from 3 counties (Jefferson, Denver, Arapahoe) using data from a .csv file using a script written in Python 3.7 in Visual Code Studio. We auditted the election_results.csv with 369,711 rows (excluding the header row) to identify votes cast from each county for each candidate using for loops and wrote the results to a .txt file called election_results.txt.

# Election-Audit Results: Using a bulleted list, address the following election outcomes. Use images or examples of your code as support where necessary.

* How many votes were cast in this congressional election?
Using an if-statement, we iterated through each row to count the total amount of votes.
```
        if candidate_name not in candidate_options:
            candidate_options.append(candidate_name)
            candidate_votes[candidate_name] = 0

        candidate_votes[candidate_name] += 1
        if county_name not in county_list:
            county_list.append(county_name)
            county_votes[county_name] = 0
        county_votes[county_name] += 1
```
Once this is has been completed, we printed the results to the .txt file. 
```
with open(file_to_save, "w") as txt_file:

    election_results = (
        f"\nElection Results\n"
        f"-------------------------\n"
        f"Total Votes: {total_votes:,}\n"
        f"-------------------------\n\n"
        f"County Votes:\n")
    print(election_results, end="")

    txt_file.write(election_results)
```
The result of this snippet generated the results as:
```
Election Results
-------------------------
Total Votes: 369,711
-------------------------
```

* Number of votes and the percentage of total votes for each county in the precinct.
Then, we counted the number of votes and the percentage of total votes for each county using a for-loop.
```
    for county in county_list:
        county_vote = county_votes[county]
        county_vote_percentage = float(county_vote) / float(total_votes) * 100
        county_results = f"{county}: {county_vote_percentage:.1f}% ({county_vote:,})\n"
        print(county_results)
        txt_file.write(county_results)
```

Using the county_list list and the county_votes dictionary, we iterated through each row to count the votes from each county and converted the results from strings to floats and multiplied the quotient by 100 to find the percentage of votes per county / total votes. To simplify the percentages, we formatted the county_vote_percentage to a 1 decimal point to be read as ##.#%. 
The results were printed and written to the .txt file as:

```
County Votes:
Jefferson: 10.5% (38,855)
Denver: 82.8% (306,055)
Arapahoe: 6.7% (24,801)
```

An if-statement was then used to identify the largest county voter turnout. The if-statement checks for the winning county and the largest vote percentage.

```
        if (county_vote > largest_county_votes) and (county_vote_percentage > largest_county_percentage):
            largest_county_votes = county_vote
            largest_county_percentage = county_vote_percentage
            largest_county = county
```            

* Largest County Turnout
The results were printed and written to the txt file.
```
    largest_county_print = (
        f"-------------\n"
        f"Largest County Turnout: {largest_county}\n"
        f"-------------\n"
    )
    print(largest_county_print)
    # 8: Save the county with the largest turnout to a text file.
    txt_file.write(largest_county_print)
```
The result of this as seen in the election_results.txt is:
```
-------------
Largest County Turnout: Denver
-------------
```
* The winning candidate and the percentage of votes received
The count of votes and the percentage received for each vote was counted by creating variables for the candidate, their vote count, and dividing the count by the total votes using an if statement and a for-loop.
```
    for candidate_name in candidate_votes:
        votes = candidate_votes.get(candidate_name)
        vote_percentage = float(votes) / float(total_votes) * 100
        candidate_results = (
            f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")
```

Once the results were generated, they were printed to the .txt file.
```
        print(candidate_results)
        txt_file.write(candidate_results)
```
The outcome for candidate_results is displayed as:
```
Charles Casper Stockham: 23.0% (85,213)
Diana DeGette: 73.8% (272,892)
Raymon Anthony Doane: 3.1% (11,606)
```

Finally, we checked for the winning candidate using a for-loop for the greatest percentage of votes and vote count. 
```
        if (votes > winning_count) and (vote_percentage > winning_percentage):
            winning_count = votes
            winning_candidate = candidate_name
            winning_percentage = vote_percentage
```           
The winning candidate is printed and written with their name, count, and percentage.
```
    winning_candidate_summary = (
        f"-------------------------\n"
        f"Winner: {winning_candidate}\n"
        f"Winning Vote Count: {winning_count:,}\n"
        f"Winning Percentage: {winning_percentage:.1f}%\n"
        f"-------------------------\n")
    print(winning_candidate_summary)
    txt_file.write(winning_candidate_summary)
```   
We can see the result as:
```
-------------------------
Winner: Diana DeGette
Winning Vote Count: 272,892
Winning Percentage: 73.8%
-------------------------
```
Diana DeGette received the largest vote count and the highest percentage!

# Summary
This script can be used in future elections in the same method for different .csv files if the headers are kept the same. Changing the desired file to read in line 9:
```
file_to_load = os.path.join("Resources", "election_results.csv")
```
and writing the results to the desired file in line 11:
```
file_to_save = os.path.join("analysis", "election_analysis.txt")
```
The dictionaries and lists are already created to read the names of candidates and counties in the case that there are a higher number of different counties or candidates. 
The only considerable factors to change is what file is read and what file is written. 
