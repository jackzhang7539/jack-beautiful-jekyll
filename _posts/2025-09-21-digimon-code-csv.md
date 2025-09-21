---
layout: post
title:  Exploring csv files with digimon
subtitle: Lab 1.4
gh-repo: jack-beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [Lab]
comments: true
mathjax: true
author: Jack Zhang
---

For our first lab we were tasked with using python to take infomation from a csv file
[Digimon CSV](https://drive.google.com/file/d/1YGVROpS7pg_0ZP3zk31e3bG2ghwz4Snw/view)
The first part of the lab was to find the average speed (spd) of all the digimon. 
```python
import csv
with open("datasets/digimon.csv", "r") as f:
    data = csv.DictReader(f)
    spdTotal = 0
    DigiTotal = 0
    for row in data:
        spd = row['Spd']
        spdTotal += int(spd)
        DigiTotal += 1
    print("\nAverage Speed of all digimon", spdTotal/DigiTotal)
```
Result: 120

This was really simple to code and I didn't have any issues with it. One way I could have improved it was to use the command input() so that instead of speed I could put any of the stats and find the average.

The second part of the lab was to write a function that can count the number of Digimon with a specific attribute. 
```python
import csv
def count_digimon(category, stat):
    counter = 0
    with open("datasets/digimon.csv", "r") as f:
        data = csv.DictReader(f)
        for row in data:
            if row.get(category) == stat:
                counter += 1
    return counter
matches = count_digimon("Type", "Vaccine")
print("\nMatches found for types:", matches)
```
Result for "Type", "Vaccine": 70
The code runs by changin the two parameters inside of the function to whcihever the user wants and then the code searches through each digimon to see how many have the first match then, they sort through the ones firstly matched to see which ones match the second parameter.

The third part of the lab was to write a function that can create a random team of 3 Digimon that have max of 15 memory and a minimum of 300 attack.
```python
import csv
import random
list = []
with open("datasets/digimon.csv", "r") as f:
    data = csv.DictReader(f)
    MAX_MEMORY = 15
    MIN_ATTACK = 300
    found_team = False
    for row in data:
        list.append({
        "Name": row["Digimon"],
        "Attack": int(row["Atk"]),
        "Memory": int(row["Memory"])
    })

    for i in range(10000): 
        team = random.sample(list, 3)  
        total_attack = sum(digi["Attack"] for digi in team)
        total_memory = sum(digi["Memory"] for digi in team)
        if total_attack >= MIN_ATTACK and total_memory <= MAX_MEMORY:
            found_team = team
            break

    if found_team:
        print("\nTeam found:")
        for digi in found_team:
            print(f"{digi['Name']} (Atk: {digi['Attack']}, Mem: {digi['Memory']})")
        print(f"Total Attack: {total_attack}")
        print(f"Total Memory: {total_memory}/{MAX_MEMORY}")
        
    else:
        print("No teams found")
```
How the code works is that I created a list called list and then I added the name, attack, and memory of each Digimon onto the list. I then used random to find 3 random Digimon out of the list and see if they meet the requirements. If they don't, the code continues searching. It searches at most 10000 times meaning that I am basically garaunteed to find a match. One imrpovement I could do in the future is learn to make the code search until a match is found or break if there is no match. Lastly, I printed out the stats of each Digimon in the team of three. I learned to use 'f' inside of print lines which basicallt formats the print lines when I use {} so that I don't have to constantly use commas and quotation marks. 


