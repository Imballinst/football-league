# football-league (Status: brainstorming)
## Raw Data
### tabel liga (mutable)
```
id | nama liga
---|----------
1  | liga inggris 2016/2017
2  | liga champions 2016/2017
```
### tabel tim (mutable)
```
id | nama tim
---|---------
1  | arsenal
2  | manchester united
3  | manchester city
4  | liverpool
```
### tabel match (mutable)
```
id  | id liga | is neutral | home team | away team | home team score | away team score | match date
----|---------|------------|-----------|-----------|-----------------|-----------------|--------------
1   | 1       | 0          | 1         | 3         | 3               | 0               | isostringdate
2   | 1       | 0          | 2         | 4         | 3               | 0               | isostringdate
----|---------|------------|-----------|-----------|-----------------|-----------------|--------------
3   | 1       | 0          | 1         | 2         | 3               | 0               | isostringdate
4   | 1       | 0          | 3         | 4         | 1               | 1               | isostringdate
----|---------|------------|-----------|-----------|-----------------|-----------------|--------------
5   | 1       | 0          | 1         | 4         | 2               | 0               | isostringdate
6   | 1       | 0          | 2         | 3         | 1               | 2               | isostringdate
----|---------|------------|-----------|-----------|-----------------|-----------------|--------------
7   | 1       | 0          | 2         | 1         | 1               | 1               | isostringdate
8   | 1       | 0          | 4         | 3         | 2               | 0               | isostringdate
----|---------|------------|-----------|-----------|-----------------|-----------------|--------------
9   | 1       | 0          | 3         | 1         | 4               | 2               | isostringdate
10  | 1       | 0          | 4         | 2         | 1               | 2               | isostringdate
----|---------|------------|-----------|-----------|-----------------|-----------------|--------------
11  | 1       | 0          | 3         | 2         | 2               | 3               | isostringdate
12  | 1       | 0          | 4         | 1         | 3               | 3               | isostringdate
```
## Processed Data
### Stats and Pts
```
arsenal: 3w 2d 1l = 11pts
manchester united: 3w 1d 2l = 10pts
manchester city: 2w 1d 3l = 7pts
liverpool: 1w 2d 3l = 5pts
```
### Table Representation
```
# | nama tim          | p | w | d | l | gf | gd | ga | pts | last 3 matches
--|-------------------|---|---|---|---|----|----|----|-----|---------------
1 | arsenal           | 6 | 3 | 2 | 1 | 14 | 9  | 5  | 11  | d l d
2 | manchester united | 6 | 3 | 1 | 2 | 10 | 9  | 1  | 10  | d w w
3 | manchester city   | 6 | 2 | 1 | 3 | 8  | 12 | -4 | 7   | l w l
4 | liverpool         | 6 | 1 | 2 | 3 | 7  | 11 | -4 | 5   | w l d
```
## Algorithm
### Display Table
```
1. select (*) from (table match) where id liga=1 [AND date>=isostringdate1 AND date<=isostringdate2]
2. foreach select from (1)
2.1. if home team score > away team score: add 1W, 3 pts to home team; add 1L, 0 pts to away team
2.2. else if home team score < away team score: add 1W, 3 pts to away team; add 1L, 0 pts to home team
2.3. else: add 1D, 1 pts to home and away team
2.4. either way: add GF/GD/GA to both in table; add W/L/D to both in temp array
3. slice the temp array to last 3
4. show the table
```
