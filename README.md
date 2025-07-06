 CREATE PROCEDURE `new_procedure` ()
    -> BEGIN
    -> select username from users;
    -> END$$
Query OK, 0 rows affected (0.076 sec)
 call ecommerce_new.new_procedure();
+---------------+
| username      |
+---------------+
| nehaprakash   |
| nishasarang   |
| parvathygowri |
| rudradev      |
+---------------+
4 rows in set (0.009 sec)

function

 CREATE FUNCTION getamount(o_id int)
    ->    RETURNS int
    ->    DETERMINISTIC
    ->    BEGIN
    ->       declare t_amount int;
    ->       select total_amount into t_amount from orders where
    ->    order_id = o_id;
    ->          return t_amount;
    ->    END//

     SELECT getamount('1');
    -> //
+----------------+
| getamount('1') |
+----------------+
|            754 |
+----------------+
1 row in set (0.010 sec)

mysql> SELECT getamount('2');//
+----------------+
| getamount('2') |
+----------------+
|            450 |
+----------------+
1 row in set (0.007 sec)
Query OK, 0 rows affected (0.105 sec)

function with conditional logic

 DELIMITER //
mysql> CREATE FUNCTION getstatus1(o_id int)
    ->    RETURNS int
    ->    DETERMINISTIC
    ->    BEGIN
    ->       declare stats varchar(20);
    ->       select status into stats from orders where
    ->    order_id = o_id;
    ->  IF stats='paid' then
    ->         RETURN 1;
    ->     ELSE
    ->         RETURN 0;
    ->     END IF;
    ->    END//
Query OK, 0 rows affected (0.087 sec)

mysql> select getstatus1(1);//
+---------------+
| getstatus1(1) |
+---------------+
|             0 |
+---------------+
1 row in set (0.023 sec)

mysql> select getstatus1(2);//
+---------------+
| getstatus1(2) |
+---------------+
|             1 |
+---------------+
1 row in set (0.007 sec)

