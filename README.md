- 👋 Hi, I’m @VNRAIDS
- 👀 I’m interested in helping students of AIDS for creating exciting repositories
- 📫 Contact me at:vnraids@gmail.com
 

<!---
VNRAIDS/VNRAIDS is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
Minimum values:
hive> select t.my_key, min(t.my_key_value) as min_value
> from (
> select explode(properties) as (my_key,my_key_value)
> from user_data1
> ) t
> group by t.my_key;
...
... OK
Age 21
Gender F
State CA
Time taken: 26.099 seconds, Fetched: 3 row(s)
Maximum values:
hive> select t.my_key, max(t.my_key_value) as max_value
> from (
> select explode(properties) as (my_key,my_key_value)
> from user_data1
> ) t
> group by t.my_key;
...
...

VNR VJIET Name of the experiment : ___________________
Name of the Laboratory Exp.No.: _____________ Date : ____________

OK
Age 23
Gender M
State TX
Time taken: 22.254 seconds, Fetched: 3 row(s)
Unique Count:
hive> select t.my_key, count(distinct t.my_key_value) as unique_count
> from (
> select explode(properties) as (my_key,my_key_value)
> from user_data1
> ) t
> group by t.my_key;
...
... OK
Age 3
Gender 2
State 5
Time taken: 19.956 seconds, Fetched: 3 row(s)
iv.Generate a count per state.
hive> select my_value, count(*) as state_count
> from (
> select explode(properties) as (my_state, my_value)
> from user_data1
> ) t
> where t.my_state = 'State'

VNR VJIET Name of the experiment : ___________________
Name of the Laboratory Exp.No.: _____________ Date : ____________

> group by t.my_value;
