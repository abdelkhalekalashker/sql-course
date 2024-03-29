# sql-course
database relationship types
 1. cardinality
   * one : one
   * one : many
   * many : many
 2. degree
   * unary
   * binary
   * ternary
 3.  participation
   * total participation
   * partial participation

## mapping 
  1. one : one relationship
     the more partial needed the more tables will be created 
      * when two are total participation :-
        use one table and primary is any one of two entities primary key and the other one is foriegn-key ===> using one table 
      * when one of entities is partial and other is total :-
        use two tables, one for each, total participation entity has partial entity's primary-key as forign key ====> using two tables
      * when two entity are partial participation :-
        use three tables one for each entity, and the third will have two foriegn key from entities with anyone of them as primary key for third table ===> using three tables

  2. one : many relationship
      * we just look at many
      * if many is total participation then we have two tables one for each, and primary key of one table is forighn key in many table
      * if many is partial participation then we have three tables, one for each, and third table contains primary keys of two tables but the primary key of third table will be primary key of many table

  3. many : many relationship
     * if relationship is many to many, then it will be three tables one for each and third hvae primary keys of two tables as compossed primary key of third table.
    
## Join types 
1- cross join (cartissian join)
this join is used to joins two tables restaurantes table and customers table  number of records in new table becomes number of restaurantes table multiplied with number of records in customers table, customer can visit multiple restaurants, and restaurant can be visited by multiple customers, the output table will have number of records equal restaurants * customers table.

2- inner join (equai join)
this join type will use the common between two tables, this means that Table will have records with foreign keys null free. let tables be students and departments if i want to list students that belongs to department (this means that list department that have students in too), there are no records with null values in d_id or s_id.
query to do this join
SELECT s.name, d.name
FROM students s inner join departments d
ON d.id = a.d_id;

3- outer join
we can explain it on two tables students and departments tables.
i- LEFT OUTER JOIN
if I want to list all students in stidents table and it's department if exist and null if not, I will use left outer join 
query to do that
SELECT s.name, d.name
FROM students s LEFT OUTER JOIN departments d
ON s.d_id = d.id

ii- RIGHT OUTER JOIN
 this join used to list all departments in departments table with student if exist and null if not, and students without department won't appear in new table.
 query to do this join
 
 SELECT s.name, d.name
FROM students s RIGHT OUTER JOIN departments d
ON s.d_id = d.id

iii- FULL OUTER JOIN
 is used to list two tables each for its appropriate from second table, the output of this join may have many nulls in foreign keys.



 ### functions in sql 
 1- isnull(first_name, "no data")
   is null is function that take column and if the name is null the output should be "no data"
 2- coalesce(first_name, second_name, "this user has not first or second name")
   if first name is null it displays scond_name, but if second_name is null it displays "this user has not first or second name"
 3- convert(varchar(3), age)
   to convert age (int) into varchar
 4- concat(name , "has" , age, "years")
    convert all data in it to string
 5- like
   like is using to seach with different patterns
    "a%" starts with a
    "%a%" contains a 
    "_a%" second char is a
    "[alk]%"  starts with a or l or k
    "[^alk]%" does not start with a or k or l
    '[a-h]' range from a to h
    '[^a-h]' does not start with any of that range
    '[_]%' starts with _ char
     '%[%]' ends with % char


   `query 
   select name , age 
   from students
   order by 1` 

   this query will order the rows using first column in selected columns

   `select name , age 
   from students
   order by department`

   this query is valid even if the department is not selected in this query



 ## Normalization

 ### types of functional dependancy

 #### full functional dependancy
   if the whole PK is used to retrive all attributes of row 
    

 #### partial functional dependancy
   if the pk is composite and only one field of that PK used to retrieve one or more of row's attributes (partial of PK is unique).


   #### Transitive functional dependency
   if non key column is used to retrive one or more of row's attributes 
    i.e zip code is unique for each city so i can use zip code to know name of city  if zip or city_name not keys 
    i.e if user is has full name (not key but unique), I could retrieve it's age.


   simple primary key can not be partial dependency, but can be full or transitive functional dependency 

   composite primary key can be full or partial or transitive
    

steps to achieve Normalization
1- remove multivalued primary key
  build table with multivalued attributes and put it in table with PK 
2- remove partial dependencies
   build table with that key with attributes that depends on that column and put it in table with FK of original table 
3- remove transitive dependencies
   build table with that non key with attributes that depends on that column and put it in table with FK of original table 

## grouping
```
SELECT count(id), dept_id
FROM students
WHERE name like 'a%'
group by dept_id
having count > 5;

```
- this query is listing every department id besides xount of students in that department with condition that student name of these students have name starts with 'a' using 'where' clause, and group these students by department id, and condition on groups with 'having'
- we can not use aggregate finction without group by.
- where is used to filter rows
- having is used to filter groups
- use aggregate functions when selecting whole rows, but can be used if you want to select just column that aggregated using aggregation function.
- where executes first then having.


   ## sub queries
```
 SELECT name, age
 FROM students
 where age > avg(age);

```
previous query raises syntact error
because
- avg can't be used in this query unless using group.
- some times you have to use sub query, like this case.

the correct of previous query is
```
 SELECT name, age
 FROM students
 where age > (SELECT  avg(age) FROM students;) as avg_age;
```
this query is error free because I used inner query to select avg_age and use aggregate function in it to be comapred with outer query.
     


note: where clause does not work with alias names because where is performed before select clause, but we can use it if we make this query sub query in another one
## Union 

union is used to union two xolumn values to be in one column, output column will
- be whole values of two columns listed to be one column with both columns values.
- column name will take the first column name of selected column.
- can ise alias to give output value
- two columns should be with same data type
- if union between two tables you, tables should having same number, data types of columns.

### Union all

```
SELECT name
FROM students
union all
SELECT first_name
FROM instructos
```
this query output will be one column listing names of students then under these names will be instructors first name.

### union

same as union all conditions unless union is listing distinct values only(unique and ordered values).
## Distinct 
in sql, three clauses will list uniqe and ordered values
1- distinct 
2- intersect (return all values in first that equal second table values)
3- except (return all values in first table but not equal second table values)


## super and sub entities
sub entity should be part of system, but if there are more than one table that shared in some columns, then we invented super entity, generic table

#### Inheritance
if I have Employees with different types like customer_service, drvelopers and designers, but every table have different logic and columns but are shared in some,
I could make employees table that have all employees in all roles, and make developers and designers as sub tables inherite feom employee which is super table
# constrains in super type
## completness constraints 
this constarains is two rules
### total specialization rule
if all rows in super table  are existed in developers table and designers table, then this is total, and represented with two lines under super table.
if relation is total, then super table's rows should be equal rows in two tables inheriting from super, because super table can not contain any rows that not exist in any of inherting tables(all rows in super should be in one of two inheriting tables, and vise versa)
### partial specialization rule
if i add service providors to be type of super table (employees), but not a table from employees, then this relatiob is partial, and represented by one line under super table.
if relation is partial, then super table's rows should be bigger than or equal rows in two tables that inherted from super, because super table may contains some rows that not exist in any of inherting tables 

## Disjointedness rule
### total disjoin 
if employee should belongs to only table of two inheriting tables, then this rule is disjoin, row can not be part of two different tables, and represented with 'd' in the circle

### overlap rule 
If employee may be developer and designer at same time then this rule is overlap, and represented with 'o' in circle 


# 5th Lecture
 when you want to insert data from table to another table( if columns types are same and selected columns <= tables's columns in table to insert to
 ex- create new table called students with column name and age 
   ```
    CREATE TABLE students (
      id SERIAL PRIMARY KEY,
      name VARCHAR(50)
    )
   ```
   
   ```
    insert into students 
    select name, age from users
   ```
 then name and age from all records in users table will be copied to students table

# Ranking Function
its four functions 
 1- Row_Number()
 2- Dense_Rank()
 3- NTiles(Group)
 4- Rank()

  -query to get maximum salary in employees 
  
  ```
  select max(salary) from employees;
```
  
  -max department salary in departments
  
  ```
  select sum(salary) as sum_salary from employees group by dept_id order by sum_salary desc limit 1;
```
  
  -second max salary in employees
  
  ```
  select salary from employees order by salary desc offset 1 limit 1;
```

  
  and what if i want to get third max salary from each department? its hell, so the ranking functions come.

   1- Row_Number()
  this function used to give number each column in ordered table this number is serial(every row has its own order number).
    retrieve row that has max third salary in employees table
    
    ``` 
              select * from (
                             select *, Row_Number() over(order by salary desc) as RN 
                             ) as ne_table
                where RN = 3
    ```
    
   2- Dense_Rank()
 same as Row_Number but it differs that dense give all equals values same rank number, then if there are two employees whose salary 7000 USD then both  of them will have same rank number
     -- retriev all rows that has salary eqaul to max third salary in employees table 
     
     ``` 
          select * from (
                         select *, Dense_Rank() over(order by salary desc) as DN 
                        ) as new_table 
                where DN = 1
     ```

  3- NTiles(Group)
this function is grouping the rows into number of groups, each group has same number of rows, and if they not equal then the last group should have one row less than other groups.  
      retriev rows in group number 2 when employees ordered by salary 
      
     ``` 
          select * from (
                         select *,  NTiles(3) over(order by salary desc) as NT 
                        ) as new_table 
                where NT = 1
     ```
     
 4- Rank()



 ### partition

 partition as same as group by but it differs than group by in use with rankinig functions, rank function is applied on each partition not on whole table's rows.
     
  -- select max 3rd row in each department (partition) (if i have three department then i will get three rows, (third from each partition).

     ``` 
          select * from (
                         select *,  Row_Number() over(partition by dept_id order by salary desc) as RN 
                        ) as new_table 
                where RN = 3
     ```

-- select max 3rd row and whatever equal to thired max value in employees's salary in each department (partition) (if i have three department then i will get all rows that have max third value), (third from each partition).

     ``` 
          select * from (
                         select *,  Dense_Rank() over(partition by dept_id order by salary desc) as DN 
                        ) as new_table 
                where DN = 3
     ```

  ### Indexing
  #### clustered_index
   - table's rows is sorted based on primary key of that table because primary is a clustered_index
   - clustered_index is an index that used for ordering table's rows
   - table can not include more than one clustered_index
   - clustered_index is using B+ tree
   - b+ tree is levels (root, node and leaf) node can have more than two children
   - leaf level is including pages that include the data
   - each node has begining of their child nodes
   - then engine can do page scan not table scan
   - clustered can be on any column
   - primary key constraint creates clustred_index on that column unless other column have clustered_index
  #### flow to search in database with clustered_index
   1- search in the root which range includeing the id and redirect to next node
   2- redirected node will search in its child nodes 
   3- that node will redirect to the page that include that id
   4- page will do page scan to get the record

  #### nonclustered_index
   - table can include nonclustered indices up to 999 indices
   - craete unique constraint on column creates non clustered index on that column
   -  in memory engine will create new data pages to store all values of non clustered index
  
  #### flow to search in database with non clustered_index
  1- search in the root and that have begging of ranges of all child nodes
  2- when get that value of non clustered index pointer to primary key and get the data from database

  which columns to set index on? columns that used in search in the database
  tooles to be used to suggest columns to be indexed based on database queries for a while:-
  in sql server 1- sql server profiler
                2- sql server tuning advisor
                
  
    
   

   
   ##### rollup, cube and grouping sets
   - rollup
    is used with group by to apply agg function on first column in group by columns
    if i want to sum salesries of specific name for example "Ahmed"
 ```
    select name, sum(sal) from employees
    group by rollup(name, dept_id);
```
this query will create three queries 

1- calculate sum salaries of name in specific department (sum salaries of all persons named "Ahmed" in marketing department) 
2- calculates sum salaries of specific name in all table (sum salaries of all persons named "Ahmed" in all database table regardless department) 
3- calculates sum salaries of all returned groups  (sum of all salaries in all table)

- cube
    is used with group by to apply agg function on all columns in group by columns
    if i want to sum salesries of specific name for example "Ahmed"
 ```
    select name, sum(sal) from employees
    group by cube(name, dept_id);
```
this query will create four queries 

1- calculate sum salaries of name in specific department (sum salaries of all persons named "Ahmed" in marketing department) 
2- calculates sum salaries of specific name in all table (sum salaries of all persons in marketing department regardless name)
2- calculates sum salaries of specific department in all table (sum salaries of all persons named "Ahmed" in all database table regardless the department) 
3- calculates sum salaries of all salaries in table (sum of all salaries in all table)

   
- grouping sets
    is used with group by to rollup all columns in group by columns and to cancel group by
    output will be

  1- calculates sum salaries of specific name in all table (sum salaries of all persons in marketing department regardless name)
  2- calculates sum salaries of specific department in all table (sum salaries of all persons named "Ahmed" in all database table regardless the department) 
  3- calculates sum salaries of all salaries in table (sum of all salaries in all table)
 ```
    select name, sum(sal) from employees
    group by grouping sets(name, dept_id);
```
    
