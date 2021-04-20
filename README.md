# Intro to SQL - Part 1
_April 2021_

For this workshop, we'll be using [DB Browser fo SQLite](https://sqlitebrowser.org/dl/). It's availaible on Mac, Windows and Linunx, it is open source and self-contained without the need for a server. It's great for getting started with SQL.

The database we will be using for our exercises is New York City's Department of Health and Mental Hygiene (DOHMH) [Restaurant Inspection Results](https://data.cityofnewyork.us/Health/DOHMH-New-York-City-Restaurant-Inspection-Results/43nn-pn8j).

You can download the files here:

Data (ZIP CSV) _(Last updated: April 19, 2021)_: 
[nyc_grades.csv.zip](https://github.com/jonkeegan/intro-to-sql/raw/master/nyc_grades.csv.zip)

Data dictionary (XLSX): 
[RestaurantInspectionDataDictionary_09242018.xlsx](https://github.com/jonkeegan/intro-to-sql/raw/master/RestaurantInspectionDataDictionary_09242018.xlsx)

Here are the [slides](https://docs.google.com/presentation/d/1wKlNn9b-B5RgN6dBMMvhNVIGliIj4GCpoZlkdxMkS8M/edit?usp=sharing) for this workshop.

---
### Queries used in the workshop

#### Simple queries
**Show everything:**
```sql
SELECT * FROM nyc_grades
```
---
**Show everything, but sort the business name A-Z:**
```sql
SELECT * FROM nyc_grades ORDER BY DBA asc
```
---
**Just showing a subset of columns:**
```sql
SELECT DBA, BUILDING, STREET, BORO FROM nyc_grades
```
---
**A list of all restaurants in Queens:**
```sql
SELECT * FROM nyc_grades WHERE BORO = "Queens"
```
---
**A list of all KFCs in Queens:**
```sql
SELECT * FROM nyc_grades WHERE BORO = "Queens" and DBA = "KFC"
```
---
**A list of all KFCs with an A grade:**
```sql
SELECT * FROM nyc_grades WHERE DBA = "KFC" and GRADE = “A”
```
---
**A list of all distinct grades:**
```sql
SELECT DISTINCT GRADE FROM nyc_grades
```
---
**A list of all distinct values for `CUISINEDESCRIPTION`:**
```sql
SELECT DISTINCT CUISINEDESCRIPTION FROM nyc_grades ORDER BY CUISINEDESCRIPTION ASC 
```
---
**All restaurants with Frank or Johnny anywhere in the name:**
```sql
SELECT * FROM nyc_grades WHERE DBA LIKE "%frank%" OR DBA LIKE "%johnny%"
```
---
**All restaurants with a score less than 10 and a 'Y' value for `CRITICALFLAG`:**
```sql
SELECT * FROM nyc_grades WHERE SCORE < 10 AND CRITICALFLAG = "Y"
```
**Count all records in `nyc_grades`:**

```sql
SELECT COUNT(*) AS count from nyc_grades
```
**Count all records and group by `BORO`. This gives a total count of restaurants broken down by borough:**
```sql
SELECT BORO, COUNT(*) AS count from nyc_grades GROUP BY BORO
```
**Find all records where "live mice" appeared in the `VIOLATIONDESCRIPTION` field, then group them by the unique restaurant ID (CAMIS):**
```sql
SELECT *, COUNT( * ) AS count from nyc_grades where VIOLATIONDESCRIPTION LIKE "%live mice%" group by `CAMIS` order by count desc
```
**Find all Chinese food restaurants with "gold" in the `DBA`:**
```sql
SELECT * from nyc_grades WHERE `CUISINEDESCRIPTION` LIKE "Chinese" AND `DBA` LIKE "%gold%" AND `BORO`= "Manhattan"
```
### BONUS CHALLENGES

- 1. What pizza restaurant in Queens had the most "A" grades?
- 2. What is the total number of "establishment closed" actions per borough?
- 3. What is the restaurant with the most number of violations overall?
