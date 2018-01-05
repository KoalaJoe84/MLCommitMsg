# MLCommitMsg
# Command to extract commits into a string pair:
git log --format=oneline | awk '{print $1}' > list_of_shas

# Extracting sha pairs for commit message and diff
while read sha; do echo "\"" > strings/$sha.txt; git log --format=%B -n 1 $sha >> strings/$sha.txt; echo "\"" >> strings/$sha.txt; echo ",\"" >> strings/$sha.txt; git diff $sha^ $sha >> strings/$sha.txt; echo "\"" >> strings/$sha.txt; done < list_of_shas
