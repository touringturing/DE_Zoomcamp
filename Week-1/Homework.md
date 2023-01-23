Question 1:  Knowing docker tags  ( Multiple choice)
----------------------------------------------------


docker build --help | grep "Write" 

      --iidfile string          Write the image ID to the file


Question 2:  Understanding docker first run  (Multiple choice)
How many python packages/modules are installed?
---------------------------------------------------------------

docker run -it python:3.9 bash

root@be8df199c251:/# python --version

Python 3.9.16

root@be8df199c251:/# python -m pip list

Package    Version
---------- -------
pip        22.0.4

setuptools 58.1.0

wheel      0.38.4

WARNING: You are using pip version 22.0.4; however, version 22.3.1 is available.

You should consider upgrading via the '/usr/local/bin/python -m pip install --upgrade pip' command.

Question 3: Count records  (Multiple choice)
How many taxi trips were totally made on January 15?
-----------------------------------------------------

root@localhost:ny_taxi> select count(*) from green_taxi_data where date(lpep_pickup_datetime)='2019-01-15' and date(lpep
 _dropoff_datetime)='2019-01-15';

+-------+
| count |
|-------|
| 20530 |
+-------+
SELECT 1
Time: 0.395s


Question 4: Largest trip for each day (Multiple choice)
Which was the day with the largest trip distance?
--------------------------------------------------------

root@localhost:ny_taxi> select date(lpep_pickup_datetime) from green_taxi_data order by trip_distance desc limit 1;
+------------+
| date       |
|------------|
| 2019-01-15 |
+------------+
SELECT 1
Time: 0.165s


Question 5: The number of passengers  (Multiple choice)
In 2019-01-01 how many trips had 2 and 3 passengers?
--------------------------------------------------------

root@localhost:ny_taxi> select count(*) from green_taxi_data where passenger_count = 2 and date(lpep_pickup_datetime) = 
 '2019-01-01';

+-------+
| count |
|-------|
| 1282  |
+-------+
SELECT 1
Time: 0.136s

root@localhost:ny_taxi> select count(*) from green_taxi_data where passenger_count = 3 and date(lpep_pickup_datetime) = 
 '2019-01-01';

+-------+
| count |
|-------|
| 254   |
+-------+
SELECT 1
Time: 0.130s

Question 6: Largest tip (Multiple choice)
For the passengers picked up in the Astoria Zone which was the drop up zone that had the largest tip?
-----------------------------------------------------------------------------------------------------

root@localhost:ny_taxi> select "Zone" from taxi_zones where "LocationID" = (select "DOLocationID" from green_taxi_data where "PULocationID" = (select taxi_zon
 es."LocationID" from taxi_zones where taxi_zones."Zone" = 'Astoria')  order by tip_amount desc limit 1);
 
+-------------------------------+
| Zone                          |
|-------------------------------|
| Long Island City/Queens Plaza |
+-------------------------------+
SELECT 1
Time: 0.130s

