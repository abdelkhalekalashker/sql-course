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
    
