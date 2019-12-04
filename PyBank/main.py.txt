import os
import csv

budget_csv_path = os.path.join('..', 'Resources', 'budget_data.csv')  # how to use direct path to open csv?

with open(budget_csv_path, newline="") as csvfile:
    csv_reader = csv.reader(csvfile, delimiter=",")

    budget_list = list(csv_reader)
    csv_header = budget_list[0]

    new_list_M = []  # creat a list for month
    new_list_B = []  # list for profit/losses
    new_list_A = []  # list for total changes
    
    # get rid of header
    for each_row in budget_list[1:]:

        new_list_M.append(each_row[0])
        total_months = len(new_list_M)
        # actually we could use the length of new_list_B (or budget_list) to calculate the total months,
        # thus, this step is not necessarily needed

        new_list_B.append(int(each_row[-1]))
        total = sum(new_list_B)

        new_list_A = [new_list_B[i+1] - new_list_B[i] for i in range(len(new_list_B) - 1)]
        #it actually equals the last digit minus the first one (new_list_B[last one] - new_list_B[o])

    average_changes = sum(new_list_A) / (len(new_list_B) - 1)

    for i in range(len(new_list_A)):
        # noted that the lengh of list new_list_A is 85 while that of new_list_B/new_list_M is 86
        # since the first value in new_list_B is considered as control, so new_list_A starts from the second number in new_list_B
        # thus we will need to add "1" more row when we need to locate the corresponding month 

        if new_list_A[i] == max(new_list_A):
            a = new_list_M[i+1]

        if new_list_A[i] == min(new_list_A):
            b = new_list_M[i+1]

#print(len(new_list_A))
#print(len(new_list_B))
#print(len(new_list_M))

print('Financial Analysis')
print('----------------------------')
print("Total Months" + ":" + str(total_months))
print(f'Total : ${total}')
print(f'Average Changes: {round(average_changes, 2)}')
print(f'Greatest Increase in Profits: {a} (${max(new_list_A)})')
print(f'Greatest Decrease in Profits: {b} (${min(new_list_A)})')
