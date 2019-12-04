import os
import csv

election_csv_path = os.path.join('..', 'Resources', 'election_data.csv')  # how to use direct path to open csv?


voter_ID = []
# county = []
candidate_list = []
candidate = []

with open(election_csv_path, newline="") as csvfile:
    csv_reader = csv.reader(csvfile, delimiter=",")
    csv_header = next(csv_reader)   
    election_list = list(csv_reader)

    for each_row in election_list[1:]:

        voter_ID.append(each_row[0])
        # county.append(each_row[1])
        candidate_list.append(each_row[2])  
        total_votes = len(voter_ID)

print('Election results')
print('-------------------------')
print(f'Total votes: {total_votes}')
print('-------------------------')

for i in candidate_list:
    if not i in candidate:
        candidate.append(i) # store all the unique candidate in list "candidate"

count_times = []
for i in candidate:
    count_times.append(candidate_list.count(i))
    vote_percentage = round((candidate_list.count(i)/total_votes)*100, 3) # I dont know why the "round" function was not working...
    print(f'{i} : {vote_percentage}% ({candidate_list.count(i)})')

max_count = max(count_times)
count_location = count_times.index(max_count)

print('-------------------------')
print(f'Winner : {candidate[count_location]}')
print('-------------------------')