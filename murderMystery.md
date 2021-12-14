Tasks from https://mystery.knightlab.com/walkthrough.html


![image](https://user-images.githubusercontent.com/32721917/146020484-337a73e6-d58c-42f6-a405-efa3cfe302a3.png)


SELECT * FROM crime_scene_report
where type = 'murder'
and city = 'SQL City'
and date = 20180115;


Security footage shows that there were 2 witnesses. 
The first witness lives at the last house on "Northwestern Dr". 
The second witness, named Annabel, lives somewhere on "Franklin Ave".


SELECT * FROM person
where address_street_name = 'Northwestern Dr' 
and address_street_name ='Franklin Ave';


SELECT person_id, name, transcript
FROM interview  
INNER JOIN person
ON interview.person_id = person.id
WHERE person_id = 16371 
or person_id = 14887

SELECT *
FROM get_fit_now_member
JOIN person
ON person.id = get_fit_now_member.person_id
JOIN drivers_license
ON person.license_id = drivers_license.id
WHERE membership_status = 'gold' and get_fit_now_member.id LIKE '48Z%';



SELECT person_id, name, transcript
2
FROM interview  
3
INNER JOIN person
4
ON interview.person_id = person.id
5
WHERE person_id = 67318 
6
​
7
​

person_id	name	transcript
67318	Jeremy Bowers	I was hired by a woman with a lot of money. I don't know her name but I know she's around 5'5" (65") or 5'7" (67"). She has red hair and she drives a Tesla Model S. I know that she attended the SQL Symphony Concert 3 times in December 2017.


SELECT *
FROM drivers_license dl
JOIN person p
ON p.license_id = dl.id
JOIN facebook_event_checkin fec
ON fec.person_id = person.id
WHERE car_make LIKE '%Tesla%' and car_model LIKE '%Model S%'
and gender = 'female' 
and hair_color = 'red' 
and event_name = 'SQL Symphony Concert';


SELECT *
FROM drivers_license
JOIN person
ON person.license_id = drivers_license.id
JOIN facebook_event_checkin
ON facebook_event_checkin.person_id = person.id
WHERE car_make LIKE '%Tesla%' and car_model LIKE '%Model S%'
and gender = 'female' and hair_color = 'red' and event_name = 'SQL Symphony Concert';
