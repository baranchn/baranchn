# min_to_max
min_to_max aggregate function returns to text like '1->7' first number(1) is min and the second number(7) is the max result.
This function work in between the **-99999999999999** and  **99999999999999** range.

## 1-installation:
  All below codes run with sudo users.
  * upload min_to_max.tar.gz 
  * cd --Path_uploaded_tar/
  * tar -xvf min_to_max.tar.gz
  * cd min_to_max
  * make install
## 2- Testin:
If you want to test, run the below code.
  * su - postgres
  * cd -Path/min_to_max
  *  make installcheck
## 3- In Postgres
  * psql -d your_database -c "create extension min_to_max;"

## 4- Test on the database
  * psql -d your_database
    ```
    create table vals as select val from (values(5),(3),(6),(7),(9),(10),(7)) t(val);
    select min_to_max(val) from vals;
    ```
     **min_to_max**<br />
    **3 -> 10**
  * on a table test
     ```
     create table test_minmax(col1 int, col2 float, col3 float8, col4 numeric,col5 bigint) ;
     insert into test_minmax values (2,2.2, 3.54634, 10.343546, 1344565475)
      ,(-1,-5,-5.55, -555, -10)
      ,(null,7,2.19, null, -10)
      ,(7.7,-5.8, 4.55, 6, null);
     ```
     
    ```
    select
      min_to_max(col1) as num_int,
      min_to_max(col2::numeric) as num_float,
      min_to_max(col3::numeric) as nume_float8,
      min_to_max(col4) as num_numeric,
      min_to_max(col5) as num_bigint
    from test_minmax;
    ```
    **num_int | num_float |  nume_float8  |    num_numeric    |    num_bigint<br />
    -1 -> 8 | -5.8 -> 7 | -5.55 -> 4.55 | -555 -> 10.343546 | -10 -> 1344565475<br />
    (1 row)**

   * ```
     select min_to_max(null);
     ```
     **min_to_max<br />
      (1 row)**


Links: http://big-elephants.com/2015-10/writing-postgres-extensions-part-i/

