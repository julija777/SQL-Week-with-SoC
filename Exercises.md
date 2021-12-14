Question
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
