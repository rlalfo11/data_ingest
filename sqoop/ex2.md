미디어플랫폼 성장전략 UNIT _ 07628 _ 김일해 수석

1) 명령어
/loudacre/accounts/user_compressed. Provide.a screenshot of HUE with the new directory
created.
=>sqoop import --table accounts --connect jdbc:mysql://localhost/loudacre --username training --password training --columns "acct_num,first_name,last_name" --target-dir /loudacre/accounts/user_compressed --fields-terminated-by "\t" --as-parquetfile

2) 명령 수행 결과
sqoop import --table accounts --connect jdbc:mysql://localhost/loudacre --username training --password training --columns "acct_num, first_name, last_name" --target-dir /loudacre/accounts/user_compressed --as-parquetfile --compression-codec org.apache.hadoop.io.compress.SnappyCodec
