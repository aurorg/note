~~~sql
# studio

```sql
mysql root@(none):TTMS> CREATE TABLE studio (  
                                                    studio_id INT PRIMARY KEY AUTO_INCREMENT,  
                                                    studio_name VARCHAR(100),  
                                                    studio_row_count INT,  
                                                    studio_col_count INT,  
                                                    studio_introduction VARCHAR(2000),  
                                                    studio_status SMALLINT DEFAULT 1  
                                                );              


```

# seat

 mysql root@(none):TTMS> CREATE TABLE seat ( 
                            seat_id INT PRIMARY KEY AUTO_INCREMENT, 
                            studio_id INT, 
                            seat_row INT, 
                            seat_column INT, 
                            seat_status SMALLINT DEFAULT 1 
                              );                                    

Query OK, 0 rows affected
Time: 0.051s

# play

 mysql root@(none):TTMS> CREATE TABLE play ( 
                            play_id INT PRIMARY KEY AUTO_INCREMENT, 
                            dict_type_id INT, 
                            dict_lang_id INT, 
                            play_name VARCHAR(200), 
                            play_introduction VARCHAR(2000), 
                            play_image VARCHAR(2000), 
                            play_video VARCHAR(2000), 
                            play_length INT, 
                            play_ticket_price NUMERIC(10, 2), 
                            play_status SMALLINT DEFAULT 0 
                        );                                                      
Query OK, 0 rows affected
Time: 0.062s

# schedule

 mysql root@(none):TTMS> CREATE TABLE schedule ( 
                            sched_id INT PRIMARY KEY AUTO_INCREMENT, 
                            studio_id INT, 
                            play_id INT, 
                            sched_time DATETIME, 
                            sched_ticket_price NUMERIC(10, 2), 
                            sched_status SMALLINT DEFAULT 0  
                        );                                                      
Query OK, 0 rows affected
Time: 0.053s

# ticket

 mysql root@(none):TTMS> CREATE TABLE ticket ( 
                            ticket_id BIGINT PRIMARY KEY AUTO_INCREMENT, 
                            seat_id INT, 
                            sched_id INT, 
                            ticket_price NUMERIC(10, 2), 
                            ticket_status SMALLINT DEFAULT 0, 
                            ticket_locktime TIMESTAMP 
                        );                                                      
Query OK, 0 rows affected
Time: 0.086s

# sale

 mysql root@(none):TTMS> CREATE TABLE sale ( 
                            sale_ID BIGINT PRIMARY KEY AUTO_INCREMENT, 
                            emp_id INT, 
                            cus_id INT, 
                            sale_time DATETIME, 
                            sale_payment DECIMAL(10, 2), 
                            sale_change NUMERIC(10, 2), 
                            sale_type SMALLINT, 
                            sale_status SMALLINT DEFAULT 0, 
                            sale_sort SMALLINT  
                        );                                                      
Query OK, 0 rows affected
Time: 0.056s

# sale_item

mysql root@(none):TTMS> CREATE TABLE sale_item ( 
                            sale_item_id BIGINT PRIMARY KEY AUTO_INCREMENT, 
                            ticket_id BIGINT, 
                            sale_ID BIGINT, 
                            sale_item_price NUMERIC(10, 2) 
                        );                                                      
Query OK, 0 rows affected
Time: 0.049s

# customer

mysql root@(none):TTMS> CREATE TABLE customer ( 
                            cus_id INT PRIMARY KEY AUTO_INCREMENT, 
                            cus_name VARCHAR(100), 
                            cus_gender SMALLINT, 
                            cus_telnum VARCHAR(30) NOT NULL UNIQUE, 
                            cus_email VARCHAR(100), 
                            cus_uid VARCHAR(20), 
                            cus_pwd VARCHAR(20), 
                            cus_payPwd VARCHAR(20), 
                            cus_balance DECIMAL(10, 0), 
                            cus_status SMALLINT 
                        );                                                      
Query OK, 0 rows affected
Time: 0.061s

#  data_dict

mysql root@(none):TTMS> CREATE TABLE data_dict ( 
                            dict_id INT PRIMARY KEY AUTO_INCREMENT, 
                            super_dict_id INT, 
                            dict_index INT, 
                            dict_name VARCHAR(200), 
                            dict_value VARCHAR(100)  
                        );                                                      
Query OK, 0 rows affected
Time: 0.048s

# employee 

mysql root@(none):TTMS> CREATE TABLE employee ( 
                            emp_id INT PRIMARY KEY AUTO_INCREMENT, 
                            emp_role int, 
                            emp_no VARCHAR(20), 
                            emp_name VARCHAR(100), 
                            emp_gender SMALLINT, 
                            emp_phone VARCHAR(30), 
                            emp_email VARCHAR(100), 
                            emp_pwd VARCHAR(20), 
                            emp_status SMALLINT );                              
Query OK, 0 rows affected
Time: 0.047s

# user_role

mysql root@(none):TTMS> CREATE TABLE user_role ( 
                            user_role_id INT PRIMARY KEY AUTO_INCREMENT, 
                            emp_id INT, 
                            role_id INT 
                        );                                                      
Query OK, 0 rows affected
Time: 0.054s

#  role

mysql root@(none):TTMS> CREATE TABLE role ( 
                            role_id INT PRIMARY KEY AUTO_INCREMENT, 
                            role_name VARCHAR(20) 
                        );                                                      
Query OK, 0 rows affected
Time: 0.050s



#  resource

mysql root@(none):TTMS> CREATE TABLE resource ( 
                            resource_id INT PRIMARY KEY, 
                            resource_type VARCHAR(20), 
                            resource_name VARCHAR(20), 
                            resource_url VARCHAR(200) 
                        );                                                      
Query OK, 0 rows affected
Time: 0.043s
mysql root@(none):TTMS> CREATE TABLE role_resource ( 
                            role_resource_id INT PRIMARY KEY AUTO_INCREMENT, 
                            role_id INT, 
                            resource_id INT 
                        );                                                      
Query OK, 0 rows affected
Time: 0.054s



# role_resource

mysql root@(none):TTMS> CREATE TABLE role_resource ( 
                            role_resource_id INT PRIMARY KEY AUTO_INCREMENT, 
                            role_id INT, 
                            resource_id INT 
                        );                                                      
Query OK, 0 rows affected
Time: 0.054s
~~~

