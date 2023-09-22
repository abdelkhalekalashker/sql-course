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
        use three tables one for each entity, and the third will have two foriegn key from entities as primary key ===> using three tables

  2. one : many relationship


  3. many : many relationship
    
