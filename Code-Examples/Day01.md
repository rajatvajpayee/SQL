[[SQL Concepts]]

## Create Table : CREATE TABLE
```
CREATE TABLE employee
(
    Employee_id Integer , /* Integer Data type assigned to the variable */
    Employee_Name   TEXT, /* TEXT Data type assigned to the variable */
    Department  TEXT /* TEXT Data type assigned to the variable */
);
```

- Table name : Employee
- parameter names and their data types

## Data Insert : INSERT
```
INSERT INTO employee (employee_id, employee_name, department)
VALUES  (4, 'Marcus Garcia', 'Product'),
        (5, 'Samantha Park', 'Hr');


┌─────────────┬────────────────┬────────────┐
│ Employee_id │ Employee_Name  │ Department │
├─────────────┼────────────────┼────────────┤
│ 1           │ Kayla Thompson │ Sales      │
│ 2           │ Ethan Chen     │ Operations │
│ 3           │ Julia Lee      │ Hr         │
│ 4           │ Marcus Garcia  │ Product    │
│ 5           │ Samantha Park  │ Hr         │
└─────────────┴────────────────┴────────────┘
```

## Alter Table
```
ALTER TABLE employee 
ADD column Designation TEXT default NULL;

SELECT * FROM employee;

┌─────────────┬────────────────┬────────────┬─────────────┐
│ Employee_id │ Employee_Name  │ Department │ Designation │
├─────────────┼────────────────┼────────────┼─────────────┤
│ 1           │ Kayla Thompson │ Sales      │ NULL        │
│ 2           │ Ethan Chen     │ Operations │ NULL        │
│ 3           │ Julia Lee      │ Hr         │ NULL        │
└─────────────┴────────────────┴────────────┴─────────────┘
```
1. Only one column can be updated at one time. No multiple columns @ 1 time

#### Update
```
UPDATE employee 
SET Department = 'HR', Employee_Name = 'John Doe'
WHERE Employee_id = 2 OR Employee_Name = 'Kayla Thompson'; 

SELECT * FROM employee;

## Change default values
UPDATE employee
SET hourly_pay = 150
WHERE hourly_pay != NULL;

select * from employee;
```
#### Delete
```
┌─────────────┬────────────────┬────────────┐
│ Employee_id │ Employee_Name  │ Department │
├─────────────┼────────────────┼────────────┤
│ 1           │ Kayla Thompson │ Sales      │
│ 2           │ Ethan Chen     │ Operations │
│ 3           │ Julia Lee      │ Hr         │
│ 4           │ Marcus Garcia  │ Product    │
└─────────────┴────────────────┴────────────┘

DELETE from employee
where Department = 'Hr';

select * from employee;

┌─────────────┬────────────────┬────────────┐
│ Employee_id │ Employee_Name  │ Department │
├─────────────┼────────────────┼────────────┤
│ 1           │ Kayla Thompson │ Sales      │
│ 2           │ Ethan Chen     │ Operations │
│ 4           │ Marcus Garcia  │ Product    │
└─────────────┴────────────────┴────────────┘
```

