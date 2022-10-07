mysql> use student;
Database changed
mysql> create table employees(id int, Name varchar(100), email varchar(100));
Query OK, 0 rows affected (0.11 sec)

mysql> insert into employees(id, Name, email) values(1, "Harry Potter", "pharry@warnerbros.com");
Query OK, 1 row affected (0.04 sec)

mysql> insert into employees(id, Name, email) values(2, "Clark Kent", "kclark@dccomics.com");
Query OK, 1 row affected (0.01 sec)

mysql> insert into employees(id, Name, email) values(3, "Tony Stark", "stony@marvel.com");
Query OK, 1 row affected (0.06 sec)

mysql> DELIMITER $$
mysql> CREATE PROCEDURE build_email_list (INOUT email_list varchar(4000))
    -> BEGIN
    ->  DECLARE v_finished INTEGER DEFAULT 0;
    ->  DECLARE v_email varchar(100) DEFAULT "";
    ->       DEClARE email_cursor CURSOR FOR SELECT email FROM employees;
    -> DECLARE CONTINUE HANDLER FOR NOT FOUND SET v_finished = 1;
    -> OPEN email_cursor;
    ->  get_email: LOOP
    ->
    ->          FETCH email_cursor INTO v_email;
    ->          IF v_finished = 1 THEN
    ->                  LEAVE get_email;
    ->          END IF;
    -> SET email_list = CONCAT(v_email,";",email_list);
    ->
    -> END LOOP get_email;
    -> CLOSE email_cursor;
    ->
    -> END$$
Query OK, 0 rows affected (0.02 sec)

mysql> DELIMITER ;
mysql> SET @email_list = "";
Query OK, 0 rows affected (0.00 sec)

mysql> CALL build_email_list(@email_list);
Query OK, 0 rows affected (0.04 sec)

mysql> SELECT @email_list;
+-------------------------------------------------------------+
| @email_list                                                 |
+-------------------------------------------------------------+
| stony@marvel.com;kclark@dccomics.com;pharry@warnerbros.com; |
+-------------------------------------------------------------+
1 row in set (0.00 sec)

