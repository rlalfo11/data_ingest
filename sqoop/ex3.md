3.
1) 명령어
sqoop import --table accounts --connect jdbc:mysql://localhost/loudacre --username training --password training --columns "acct_num,first_name,last_name" --target-dir /loudacre/accounts/CA --fields-terminated-by "\t" --as-parquetfile -z --where " state='CA'"

2) 명령 수행 결과
19/03/10 22:39:50 INFO sqoop.Sqoop: Running Sqoop version: 1.4.6-cdh5.7.0
19/03/10 22:39:50 WARN tool.BaseSqoopTool: Setting your password on the command-line is insecure. Consider using -P instead.
19/03/10 22:39:50 INFO manager.MySQLManager: Preparing to use a MySQL streaming resultset.
19/03/10 22:39:50 INFO tool.CodeGenTool: Beginning code generation
19/03/10 22:39:50 INFO tool.CodeGenTool: Will generate java class as codegen_accounts
19/03/10 22:39:51 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `accounts` AS t LIMIT 1
19/03/10 22:39:51 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `accounts` AS t LIMIT 1
19/03/10 22:39:51 INFO orm.CompilationManager: HADOOP_MAPRED_HOME is /usr/lib/hadoop-mapreduce
Note: /tmp/sqoop-training/compile/a6c1317d12d4fdc5b2aca6b75027bcb8/codegen_accounts.java uses or overrides a deprecated API.
Note: Recompile with -Xlint:deprecation for details.
19/03/10 22:39:54 INFO orm.CompilationManager: Writing jar file: /tmp/sqoop-training/compile/a6c1317d12d4fdc5b2aca6b75027bcb8/codegen_accounts.jar
19/03/10 22:39:54 WARN manager.MySQLManager: It looks like you are importing from mysql.
19/03/10 22:39:54 WARN manager.MySQLManager: This transfer can be faster! Use the --direct
19/03/10 22:39:54 WARN manager.MySQLManager: option to exercise a MySQL-specific fast path.
19/03/10 22:39:54 INFO manager.MySQLManager: Setting zero DATETIME behavior to convertToNull (mysql)
19/03/10 22:39:54 INFO mapreduce.ImportJobBase: Beginning import of accounts
19/03/10 22:39:54 INFO Configuration.deprecation: mapred.job.tracker is deprecated. Instead, use mapreduce.jobtracker.address
19/03/10 22:39:54 INFO Configuration.deprecation: mapred.jar is deprecated. Instead, use mapreduce.job.jar
19/03/10 22:39:55 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `accounts` AS t LIMIT 1
19/03/10 22:39:55 INFO manager.SqlManager: Executing SQL statement: SELECT t.* FROM `accounts` AS t LIMIT 1
19/03/10 22:39:57 INFO Configuration.deprecation: mapred.map.tasks is deprecated. Instead, use mapreduce.job.maps
19/03/10 22:39:57 INFO client.RMProxy: Connecting to ResourceManager at /0.0.0.0:8032
19/03/10 22:39:59 INFO db.DBInputFormat: Using read commited transaction isolation
19/03/10 22:39:59 INFO db.DataDrivenDBInputFormat: BoundingValsQuery: SELECT MIN(`acct_num`), MAX(`acct_num`) FROM `accounts` WHERE (  state='CA' )
19/03/10 22:39:59 INFO db.IntegerSplitter: Split size: 32439; Num splits: 4 from: 1 to: 129760
19/03/10 22:39:59 INFO mapreduce.JobSubmitter: number of splits:4
19/03/10 22:39:59 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1552277671618_0005
19/03/10 22:40:00 INFO impl.YarnClientImpl: Submitted application application_1552277671618_0005
19/03/10 22:40:00 INFO mapreduce.Job: The url to track the job: http://localhost:8088/proxy/application_1552277671618_0005/
19/03/10 22:40:00 INFO mapreduce.Job: Running job: job_1552277671618_0005
19/03/10 22:40:10 INFO mapreduce.Job: Job job_1552277671618_0005 running in uber mode : false
19/03/10 22:40:10 INFO mapreduce.Job:  map 0% reduce 0%
19/03/10 22:40:19 INFO mapreduce.Job:  map 25% reduce 0%
19/03/10 22:40:27 INFO mapreduce.Job:  map 50% reduce 0%
19/03/10 22:40:35 INFO mapreduce.Job:  map 75% reduce 0%
19/03/10 22:40:43 INFO mapreduce.Job:  map 100% reduce 0%
19/03/10 22:40:43 INFO mapreduce.Job: Job job_1552277671618_0005 completed successfully
19/03/10 22:40:43 INFO mapreduce.Job: Counters: 30
	File System Counters
		FILE: Number of bytes read=0
		FILE: Number of bytes written=565612
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
		HDFS: Number of bytes read=24714
		HDFS: Number of bytes written=969169
		HDFS: Number of read operations=272
		HDFS: Number of large read operations=0
		HDFS: Number of write operations=40
	Job Counters
		Launched map tasks=4
		Other local map tasks=4
		Total time spent by all maps in occupied slots (ms)=0
		Total time spent by all reduces in occupied slots (ms)=0
		Total time spent by all map tasks (ms)=26757
		Total vcore-seconds taken by all map tasks=26757
		Total megabyte-seconds taken by all map tasks=6849792
	Map-Reduce Framework
		Map input records=92416
		Map output records=92416
		Input split bytes=470
		Spilled Records=0
		Failed Shuffles=0
		Merged Map outputs=0
		GC time elapsed (ms)=542
		CPU time spent (ms)=9170
		Physical memory (bytes) snapshot=638009344
		Virtual memory (bytes) snapshot=8296513536
		Total committed heap usage (bytes)=251920384
	File Input Format Counters
		Bytes Read=0
	File Output Format Counters
		Bytes Written=0
19/03/10 22:40:43 INFO mapreduce.ImportJobBase: Transferred 946.4541 KB in 46.506 seconds (20.3512 KB/sec)
19/03/10 22:40:43 INFO mapreduce.ImportJobBase: Retrieved 92416 records.


2. CA DATA 조회
1) 명령어 parquet-tools head hdfs://localhost/loudacre/accounts/CA

2) 명령 결과
acct_num = 97323
first_name = Myra
last_name = Stiver

acct_num = 97324
first_name = Maria
last_name = Choe

acct_num = 97325
first_name = Sarah
last_name = Blumberg

acct_num = 97326
first_name = Pricilla
last_name = Webb

acct_num = 97327
first_name = Patricia
last_name = Dellinger
