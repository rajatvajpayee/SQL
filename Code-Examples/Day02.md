# Queries

###### EXAMPLE
```

┌──────────────┬────────────────┬────────┬──────────┬─────────────┐
│ Passenger_id │ Passenger_name │ Gender │  Origin  │ Destination │
├──────────────┼────────────────┼────────┼──────────┼─────────────┤
│ 10001        │ Jackson        │ Male   │ Mumbai   │ New York    │
│ 10002        │ Riya           │ Female │ Mumbai   │ Delhi       │
│ 10003        │ Roy            │ Male   │ London   │ Delhi       │
│ 10004        │ Anthony        │ Male   │ Mumbai   │ Cairo       │
│ 10005        │ Salim          │ Male   │ Ohio     │ New York    │
│ 10006        │ Dia            │ Female │ New York │ Cairo       │
│ 10007        │ Jackson        │ Male   │ New York │ London      │
│ 10008        │ Dia            │ Female │ Beijing  │ Mumbai      │
│ 10009        │ Riya           │ Female │ Damascus │ Mumbai      │
│ 10010        │ Betty          │ Female │ Beijing  │ Cairo       │
└──────────────┴────────────────┴────────┴──────────┴─────────────┘
```
### Distinct
```
select Distinct origin
from flights;

┌──────────┐
│  Origin  │
├──────────┤
│ Mumbai   │
│ London   │
│ Ohio     │
│ New York │
│ Beijing  │
│ Damascus │
└──────────┘
```

### BETWEEN

```
select * from Flights 
where passenger_name BETWEEN 'A' AND 'D';

┌──────────────┬────────────────┬────────┬─────────┬─────────────┐
│ Passenger_id │ Passenger_name │ Gender │ Origin  │ Destination │
├──────────────┼────────────────┼────────┼─────────┼─────────────┤
│ 10004        │ Anthony        │ Male   │ Mumbai  │ Cairo       │
│ 10010        │ Betty          │ Female │ Beijing │ Cairo       │
└──────────────┴────────────────┴────────┴─────────┴─────────────┘
```


###### NOTE 
```
select  passenger_name
from flights
where gender = 'Male'
and origin = 'Mumbai';

┌────────────────┐
│ Passenger_name │
├────────────────┤
│ Jackson        │
│ Anthony        │<< DOUBLE
│ Anthony        │
└────────────────┘
```

```
select DISTINCT passenger_name
from flights
where gender = 'Male'
and origin = 'Mumbai';

┌────────────────┐
│ Passenger_name │
├────────────────┤
│ Jackson        │
│ Anthony        │
└────────────────┘
```

# Functions 
|customer_id|first_name|last_name|age|country|
|---|---|---|---|---|
|1|John|Doe|31|USA|
|2|Robert|Luna|22|USA|
|3|David|Robinson|22|UK|
|4|John|Reinhardt|25|UK|
|5|Betty|Doe|28|UAE|
### As
```
SELECT first_name as FIRST, age as Umar
FROM Customers;
```

|FIRST|Umar|
|---|---|
|John|31|
|Robert|22|
|David|22|
|John|25|
|Betty|28|

### COUNT
```
SELECT COUNT(*)
FROM Customers;

Return 5
```

### MAX() & MIN()
```
SELECT MAX(age) , MIN(age)
FROM Customers;

SELECT MAX(age) as oldest, MIN(age) as youngest
FROM Customers;
```

|oldest|youngest|
|---|---|
|31|22|
### AVG and ROUND
```
SELECT ROUND(AVG(age),1) AS avg_age
FROM customers;

25.6
```

#### GROUP BY and HAVING
```
-- Number of customers in each country
SELECT country, COUNT(*) AS customer_count
FROM customers
GROUP BY country;
```

|country|customer_count|
|---|---|
|UAE|1|
|UK|2|
|USA|2|
```
SELECT country, COUNT(*) AS customer_count
FROM customers
GROUP BY country
HAVING customer_count>=2;
```

|country|customer_count|
|---|---|
|UK|2|
|USA|2|
