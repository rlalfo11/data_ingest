미디어플랫폼 성장전략 UNIT _ 07628 _ 김일해 수석

1.Account Table 조회 명령 수행

1) 명령어
sqoop eval --connect jdbc:mysql://localhost/loudacre --username training --password training --query "describe accounts"

2) 명령 수행 결과
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

1. accounts 테이블에서 acct_num,first_name,last_name 컬럼 값만 추출하여 /loudacre/accounts/user_info 경로에 저장 ( 필드 종료는 \t으로 )
1) 명령어
=> sqoop import --table accounts --connect jdbc:mysql://localhost/loudacre --username training --password training --columns "acct_num,first_name,last_name" --target-dir /loudacre/accounts/user_info --fields-terminated-by "\t"

2) 명령 수행 결과
19/03/10 22:19:55 INFO sqoop.Sqoop: Running Sqoop version: 1.4.6-cdh5.7.0
19/03/10 22:19:55 WARN tool.BaseSqoopTool: Setting your password on the command-line is insecure. Consider using -P instead.
19/03/10 22:19:55 INFO manager.MySQLManager: Preparing to use a MySQL streaming resultset.
19/03/10 22:19:55 INFO tool.CodeGenTool: Beginning code generation
19/03/10 22:19:56 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `accounts` AS t LIMIT 1
19/03/10 22:19:56 ERROR util.SqlTypeMap: It seems like you are looking up a column that does not
19/03/10 22:19:56 ERROR util.SqlTypeMap: exist in the table. Please ensure that you've specified
19/03/10 22:19:56 ERROR util.SqlTypeMap: correct column names in Sqoop options.
19/03/10 22:19:56 ERROR tool.ImportTool: Imported Failed: column not found: lastname
[training@localhost ~]$ sqoop import --table accounts --connect jdbc:mysql://localhost/loudacre --username training --password training --columns "acct_num,first_name,last_name" --target-dir /loudacre/accounts/user_info --fields-terminated-by "\t"
19/03/10 22:20:09 INFO sqoop.Sqoop: Running Sqoop version: 1.4.6-cdh5.7.0
19/03/10 22:20:09 WARN tool.BaseSqoopTool: Setting your password on the command-line is insecure. Consider using -P instead.
19/03/10 22:20:09 INFO manager.MySQLManager: Preparing to use a MySQL streaming resultset.
19/03/10 22:20:09 INFO tool.CodeGenTool: Beginning code generation
19/03/10 22:20:10 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `accounts` AS t LIMIT 1
19/03/10 22:20:10 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `accounts` AS t LIMIT 1
19/03/10 22:20:10 INFO orm.CompilationManager: HADOOP_MAPRED_HOME is /usr/lib/hadoop-mapreduce
Note: /tmp/sqoop-training/compile/1a114b64c313ade3a749e0f18ea20e16/accounts.java uses or overrides a deprecated API.
Note: Recompile with -Xlint:deprecation for details.
19/03/10 22:20:12 INFO orm.CompilationManager: Writing jar file: /tmp/sqoop-training/compile/1a114b64c313ade3a749e0f18ea20e16/accounts.jar
19/03/10 22:20:12 WARN manager.MySQLManager: It looks like you are importing from mysql.
19/03/10 22:20:12 WARN manager.MySQLManager: This transfer can be faster! Use the --direct
19/03/10 22:20:12 WARN manager.MySQLManager: option to exercise a MySQL-specific fast path.
19/03/10 22:20:12 INFO manager.MySQLManager: Setting zero DATETIME behavior to convertToNull (mysql)
19/03/10 22:20:12 INFO mapreduce.ImportJobBase: Beginning import of accounts
19/03/10 22:20:12 INFO Configuration.deprecation: mapred.job.tracker is deprecated. Instead, use mapreduce.jobtracker.address
19/03/10 22:20:13 INFO Configuration.deprecation: mapred.jar is deprecated. Instead, use mapreduce.job.jar
19/03/10 22:20:14 INFO Configuration.deprecation: mapred.map.tasks is deprecated. Instead, use mapreduce.job.maps
19/03/10 22:20:14 INFO client.RMProxy: Connecting to ResourceManager at /0.0.0.0:8032
19/03/10 22:20:16 INFO db.DBInputFormat: Using read commited transaction isolation
19/03/10 22:20:16 INFO db.DataDrivenDBInputFormat: BoundingValsQuery: SELECT MIN(`acct_num`), MAX(`acct_num`) FROM `accounts`
19/03/10 22:20:16 INFO db.IntegerSplitter: Split size: 32440; Num splits: 4 from: 1 to: 129761
19/03/10 22:20:16 INFO mapreduce.JobSubmitter: number of splits:4
19/03/10 22:20:16 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1552277671618_0003
19/03/10 22:20:16 INFO impl.YarnClientImpl: Submitted application application_1552277671618_0003
19/03/10 22:20:17 INFO mapreduce.Job: The url to track the job: http://localhost:8088/proxy/application_1552277671618_0003/
19/03/10 22:20:17 INFO mapreduce.Job: Running job: job_1552277671618_0003
19/03/10 22:20:26 INFO mapreduce.Job: Job job_1552277671618_0003 running in uber mode : false
19/03/10 22:20:26 INFO mapreduce.Job:  map 0% reduce 0%
19/03/10 22:20:33 INFO mapreduce.Job:  map 25% reduce 0%
19/03/10 22:20:39 INFO mapreduce.Job:  map 50% reduce 0%
19/03/10 22:20:44 INFO mapreduce.Job:  map 75% reduce 0%
19/03/10 22:20:49 INFO mapreduce.Job:  map 100% reduce 0%
19/03/10 22:20:49 INFO mapreduce.Job: Job job_1552277671618_0003 completed successfully
19/03/10 22:20:49 INFO mapreduce.Job: Counters: 30
	File System Counters
		FILE: Number of bytes read=0
		FILE: Number of bytes written=560464
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=470
		HDFS: Number of bytes written=2615920
		HDFS: Number of read operations=16
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=8
	Job Counters
		Launched map tasks=4
		Other local map tasks=4
		Total time spent by all maps in occupied slots (ms)=0
		Total time spent by all reduces in occupied slots (ms)=0
		Total time spent by all map tasks (ms)=17476
		Total vcore-seconds taken by all map tasks=17476
		Total megabyte-seconds taken by all map tasks=4473856
	Map-Reduce Framework
		Map input records=129761
		Map output records=129761
		Input split bytes=470
		Spilled Records=0
		Failed Shuffles=0
		Merged Map outputs=0
		GC time elapsed (ms)=232
		CPU time spent (ms)=4080
		Physical memory (bytes) snapshot=494190592
		Virtual memory (bytes) snapshot=8262049792
		Total committed heap usage (bytes)=251920384
	File Input Format Counters
		Bytes Read=0
	File Output Format Counters
		Bytes Written=2615920
19/03/10 22:20:49 INFO mapreduce.ImportJobBase: Transferred 2.4947 MB in 35.9364 seconds (71.0869 KB/sec)
19/03/10 22:20:49 INFO mapreduce.ImportJobBase: Retrieved 129761 records.
