
Exercise from https://sqlbolt.com/lesson/select_queries_with_constraints
Using the right constraints, find the information we need from the Movies table for each task below.

Table: Movies
Title	Year
Toy Story	1995
A Bug's Life	1998
Toy Story 2	1999
Cars 2	2011
Brave	2012
Monsters University	2013


SELECT title,
year FROM movies
WHERE year NOT BETWEEN 2000 AND 2010;



Questions from 
https://pgexercises.com/questions/joins/simplejoin.html

Question 1
How can you produce a list of the start times for bookings by members named 'David Farrell'?
![image](https://user-images.githubusercontent.com/32721917/146003904-e699d935-a4ea-4c99-b045-b204ff1c419f.png)

SELECT starttime
FROM cd.members
LEFT JOIN cd.bookings
ON cd.members.memid = cd.bookings.memid
WHERE firstname = 'David' and surname = 'Farrell';



Question 2
How can you produce a list of the start times for bookings for tennis courts, 
for the date '2012-09-21'? Return a list of start time and facility name pairings, ordered by the time.

![image](https://user-images.githubusercontent.com/32721917/145997969-b74a0a73-c1a5-41c8-ad5f-ee73d2f1dd89.png)

SELECT starttime,name
FROM cd.bookings 


LEFT JOIN cd.facilities 
ON cd.bookings.facid = cd.facilities.facid
where cd.facilities.name LIKE 'Tennis Court%' and 
cd.bookings.starttime >= TIMESTAMP '2012-09-21 08:00:00' and
cd.bookings.starttime <= TIMESTAMP '2012-09-21 18:00:00'


another resourse to exercise:
https://www.w3resource.com/postgresql-exercises/
