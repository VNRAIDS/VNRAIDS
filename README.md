- 👋 Hi, I’m @VNRAIDS
- 👀 I’m interested in helping students of AIDS for creating exciting repositories
- 📫 Contact me at:vnraids@gmail.com
 

<!---
VNRAIDS/VNRAIDS is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
sorry please dont feel bad

Prompt:
We have a table 'user data' that contains the following fields:
- data_date: string
- user_id: string
- properties: string

The properties field is formatted as a series of attribute=value pairs.
Ex: Age=21; state=CA; gender=M;

Ans:

I. Create the table in HIVE using Hive NoSQL-based query.

Step-by-Step Instructions:

1. Prepare Sample Data File
---------------------------
Open a terminal and run:
gedit usermap.txt

Paste the following into the file (using custom delimiters):
2025-05-01,u001,Age@21#state@CA#gender@M
2025-05-01,u002,Age@25#state@NY#gender@F
2025-05-02,u003,Age@22#state@TX#gender@M
2025-05-02,u004,Age@30#state@CA#gender@F

Save and close the file.

2. Open Hive Shell
-------------------
hive

3. Create Hive Table with Map Data Type
---------------------------------------
CREATE TABLE IF NOT EXISTS user_data1 (
  data_date STRING,
  user_id STRING,
  properties MAP<STRING,STRING>
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
COLLECTION ITEMS TERMINATED BY '#'
MAP KEYS TERMINATED BY '@'
STORED AS TEXTFILE;

4. Load Data into Hive Table
----------------------------
LOAD DATA LOCAL INPATH '/home/cloudera/usermap.txt' INTO TABLE user_data1;

5. View Raw Data
----------------
SELECT * FROM user_data1;

6. Query Specific Map Fields
----------------------------

a. Select specific attributes:
SELECT
  data_date,
  user_id,
  properties['Age'] AS age,
  properties['state'] AS state,
  properties['gender'] AS gender
FROM user_data1;

b. Find users from California:
SELECT user_id
FROM user_data1
WHERE properties['state'] = 'CA';

c. Users older than 25:
SELECT user_id
FROM user_data1
WHERE CAST(properties['Age'] AS INT) > 25;

d. Count users by gender:
SELECT properties['gender'] AS gender, COUNT(*) AS total
FROM user_data1
GROUP BY properties['gender'];

This method uses Hive's MAP data type to store and query structured key-value pairs efficiently.


Additional Hive Queries:

e. List all users along with their ages and genders:
SELECT user_id, properties['Age'] AS age, properties['gender'] AS gender
FROM user_data1;

f. Count users by state:
SELECT properties['state'] AS state, COUNT(*) AS count
FROM user_data1
GROUP BY properties['state'];

g. Maximum age of users:
SELECT MAX(CAST(properties['Age'] AS INT)) AS max_age
FROM user_data1;

h. Minimum age of users:
SELECT MIN(CAST(properties['Age'] AS INT)) AS min_age
FROM user_data1;

i. List female users:
SELECT user_id
FROM user_data1
WHERE properties['gender'] = 'F';

j. Group users by age:
SELECT properties['Age'] AS age, COUNT(*) AS count
FROM user_data1
GROUP BY properties['Age'];

k. Show users sorted by age descending:
SELECT user_id, properties['Age'] AS age
FROM user_data1
ORDER BY CAST(properties['Age'] AS INT) DESC;

l. Users with age between 22 and 28:
SELECT user_id
FROM user_data1
WHERE CAST(properties['Age'] AS INT) BETWEEN 22 AND 28;

m. Count users grouped by state and gender:
SELECT properties['state'] AS state, properties['gender'] AS gender, COUNT(*) AS count
FROM user_data1
GROUP BY properties['state'], properties['gender'];

n. Users with 'TX' or 'NY' as state:
SELECT user_id
FROM user_data1
WHERE properties['state'] IN ('TX', 'NY');

o. Number of users for each data_date:
SELECT data_date, COUNT(*) AS user_count
FROM user_data1
GROUP BY data_date;

p. Get distinct states:
SELECT DISTINCT properties['state'] AS state
FROM user_data1;

q. Get all users whose user_id starts with 'u00':
SELECT user_id
FROM user_data1
WHERE user_id LIKE 'u00%';
