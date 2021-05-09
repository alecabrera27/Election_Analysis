# Election_Analysis
Analyzing results for U.S. congressional precinct in Colorado using Python.

## Overview of Election Audit: 
In this analysis we will be reporting the total number of votes cast, the total number of votes for each candidate, the percentage of votes for each candidate, and the winner of the election based on the popular vote, as well as the voter turnout for each county, percentage of votes from each county out of the total count and the county with the highest turnout.
There were three primary voting methods that will be taken into account:

- Mail-in ballots
- Punch Cards
- DRE Counting Machines (Direct Recording Electronic)

Altogether the votes cast by these three methods will determine the final election results. 
After the votes are counted, we have to generate a vote count report to certify this U.S. congressional race.

---

## Election Audit Results 

### How many votes were cast in this congressional election? 

To find the total number of votes, we used the code;
```
# Initialize a total vote counter.
total_votes = 0
# Candidate Options and candidate votes.
candidate_options = []
# For each row in the CSV file.
    for row in reader:
        # Add to the total vote count
        total_votes = total_votes + 1
        # Get the candidate name from each row.
        candidate_name = row[2]
        # If the candidate does not match any existing candidate add it to
        # the candidate list
        if candidate_name not in candidate_options:
            # Add the candidate name to the candidate list.
            candidate_options.append(candidate_name)
            # And begin tracking that candidate's voter count.
            candidate_votes[candidate_name] = 0
        # Add a vote to that candidate's count
        candidate_votes[candidate_name] += 1
```
Having a total number of votes of *369,711*

+ Percentages per Candidate and County 

Once we have the total number of votes, we can find the number of votes for each candidate and each county. 

-For the total votes for each candidate and percentage:
```
for candidate_name in candidate_votes:

        # Retrieve vote count and percentage
        votes = candidate_votes.get(candidate_name)
        vote_percentage = float(votes) / float(total_votes) * 100
        candidate_results = (
            f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")
```

- For the total votes in each county and percentage: 
```  for county_name in county_votes:
        #  Retrieve the county vote count.
        total_county_votes = county_votes[county_name]
        # Calculate the percentage of votes for the county.
        county_vote_percentage = float(total_county_votes) / float(total_votes) * 100   
        county_results = (
            f"{county_name}: {county_vote_percentage:.1f}% ({total_county_votes:,})\n")    
            
```

### Which county had the largest number of votes?
Using the code: 
```
# Write an if statement to determine the winning county and get its vote count.
        if (total_county_votes > county_winning_count) and (total_county_votes > winning_county_percentage):
            county_winning_count=total_county_votes
            winning_county=county_name
```
we were able to find that the county with largest number of votes was *Denver*

### Which candidate won the election, what was their vote count, and what was their percentage of the total votes?
Here are the results of the analysis.

![Election Analysis](https://user-images.githubusercontent.com/78781719/117556437-a9e0d380-b02e-11eb-8c60-14d0d791ce70.PNG)

The winner was *Diana DeGette*
with a total of *272,892* votes
and a percentage of *73.8%*

---
# Election-Audit Summary

With this code we were able to count votes, find the winner candidate and county with most votes, and their percentages.
For upcoming elections, whether congressional or state, we could modify the code so we could input the name of the file to count votes, to facilitate the count of votes on different elections.
It could seem something like: 
```
#Insert the name of the file we want to analyze 
file_to_open = input("What is the name of the file to analyze?")
# Add a variable to load a file from a path.
file_to_load = os.path.join("Resources", file_to_open)
```
Also, if the information is given, we could have the percentage of total voters vs the total of registered voters, to make futher analysis on the elections and have more votes on each county. 
