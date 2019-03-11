1. 

1) Account Table 내용 조회

sqoop eval --connect jdbc:mysql://localhost/loudacre --username training --password training --query "describe accounts"

19/03/10 22:12:03 INFO sqoop.Sqoop: Running Sqoop version: 1.4.6-cdh5.7.0
19/03/10 22:12:03 WARN tool.BaseSqoopTool: Setting your password on the command-line is insecure. Consider using -P instead.
19/03/10 22:12:03 INFO manager.MySQLManager: Preparing to use a MySQL streaming resultset.
---------------------------------------------------------------------------------------------------------
| Field                | Type                 | Null | Key | Default              | Extra                | 
---------------------------------------------------------------------------------------------------------
| acct_num             | int(11)              | NO  | PRI | (null)               |                      | 
| acct_create_dt       | datetime             | NO  |     | (null)               |                      | 
| acct_close_dt        | datetime             | YES |     | (null)               |                      | 
| first_name           | varchar(255)         | NO  |     | (null)               |                      | 
| last_name            | varchar(255)         | NO  |     | (null)               |                      | 
| address              | varchar(255)         | NO  |     | (null)               |                      | 
| city                 | varchar(255)         | NO  |     | (null)               |                      | 
| state                | varchar(255)         | NO  |     | (null)               |                      | 
| zipcode              | varchar(255)         | NO  |     | (null)               |                      | 
| phone_number         | varchar(255)         | NO  |     | (null)               |                      | 
| created              | datetime             | NO  |     | (null)               |                      | 
| modified             | datetime             | NO  |     | (null)               |                      | 
---------------------------------------------------------------------------------------------------------

1.From the accounts table, import only the primary key, along with the first name, last name to
HDFS directory
=> sqoop import --table accounts --connect jdbc:mysql://localhost/loudacre --username training --password training --columns "acct_num,first_name,last_name" --target-dir /loudacre/accounts/user_info --fields-terminated-by "\t"


2.This time save the same in parquet format with snappy compression. Save it in
/loudacre/accounts/user_compressed. Provide.a screenshot of HUE with the new directory
created.
=>sqoop import --table accounts --connect jdbc:mysql://localhost/loudacre --username training --password training --columns "acct_num,first_name,last_name" --target-dir /loudacre/accounts/user_compressed --fields-terminated-by "\t" --as-parquetfile

