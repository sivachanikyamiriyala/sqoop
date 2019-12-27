# sqoop  

sqoop list-databases \ 
  --connect "jdbc:mysql://localhost:3306" \ 
  --username root \
  --password hadoop  
#to list the all databases

sqoop list-databases --connect "jdbc:mysql://localhost:3306"  --username root --password hadoop

#to see the all tables in a particular database kalyan 

sqoop list-tables --connect "jdbc:mysql://localhost:3306/kalyan"  --username root --password hadoop

#to evaluate an quey in a rdbms using sqoop 

sqoop eval --connect "jdbc:mysql://localhost:3306/kalyan"  --username root --password hadoop --query "select count(*) from orders " 

#to evaluate an query with otions-file

sqoop eval --options-file /home/siva/connect --query "show tables " 

#storage options
--as-textfile
--as-sequencefile
--as-avrodatafile
--as-parquetfile 

#import all the tables from kalyandatabase 

sqoop import-all-tables --connect "jdbc:mysql://localhost:3306/kalyan"  --username root --password hadoop --warehouse-dir /sqoop/import-all-data/kalyan.db/ --exclude-tables orders  

#to import a particular table from rdbms to hdfs sqoopdb pet table with number of mappers1 because table not having pk 
sqoop import --connect "jdbc:mysql://localhost:3306/sqoop" --username root --password hadoop --table pet --target-dir /sqoop/import-data/sqoop.db/pet -m 1 --as-textfile  
#to import a particular sqoopdb pet table with split-by 

sqoop import --connect "jdbc:mysql://localhost:3306/sqoop --username root --password hadoop --table pet --target-dir /sqoop/import-data/sqoop.db/pet-split --as-textfile --split-by name 


#to import data using boundary-query columns delete-target-dir 

sqoop import --connect "jdbc:mysql://localhost:3306/sqoop" --username root --password hadoop --table student --target-dir /sqoop/boundary-query/sqoop.db/student --delete-target-dir --boundary-query "select 1,10 from student limit 1" --columns id,name,class -m 1

#to import data using boundary-query append fields lines terminated 

sqoop import --connect "jdbc:mysql://localhost:3306/sqoop" --username root --password hadoop --table student --target-dir /sqoop/boundary-query/sqoop.db/student --append --boundary-query "select 11,20 from student limit 1" --fields-terminated-by ',' --lines-terminated-by '\n' --num-mappers 1




























