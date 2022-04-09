Relational Database Services(RDS)
--------------------------------------------------------------------------
    Tables store the information.
    Rows and Columns in Tables.
    Microsoft SQL Server , PostgreSQL , Oracle , MariaDB , Aurora ,MySQL

Advantages :
    Multiple Availability Zones.
    FailOver capabilities.
    Automated backups.
    Up and running in minutes.
Usecases :
    use in online transactions processing.

Online transaction processing vs Online Analytical processing
-------------------------------------------------------------------------
OLTP :1) Processes data from transactions in real time(eg customer orders,
banking transactions,payments and booking systems).

2)OLTP is all about processing and completing large numbers of small transactions
in real time.


OLAP :1) process complex queries to analyse historical data.(data analysis for the forecasting).

RDS is not suitable for analysing large amount of data.Use a datawarehouse like
Redshift which is optimized for OLAP.

What is Multi-AZ
--------------------------------------------------------------------------
With Multi-AZ , RDS creates an exact copy of yur production database in another 
Availability Zone.

RDS Types Can be configured Multi-AZ
-------------------------------------------------------------------------
SQL server ,MySQL ,MariaDB ,Oracle ,PostgreSQL(can be in Single AZ).
and Aurora is already configured for multi-AZ.(can't be in Single AZ).

Increase Read Performance using Read Replica
------------------------------------------------------------------------
1)Read Only Copy of your Primary Database.
2)Great for read heavy work loads.
3)Multi-AZ for disaster Recovery . Read recovery for performance boosting.
4)can be spread across multiple AZ.
5)Read Replicas can be promoted to their own databases.(breaks Replication).

Tips :
------------------------------------------------------------------------
    scaling read performance.
    you must have Automatic backups.
    Multiple Read Replicas are supported.


Amazon Aurora
-------------------------------------------------------------------------
its a MySQL and PostgreSQL compatible relational database engine that combines the speed and availability of high-end commercial database with the simplicity and cost-effw\ectiveness of open source database.

==>starts with 10GB to 128TB.
==>Compute Resources can scale up to 96 vCPUs and 768 GB of memory.
==>2 Copies of your data are contained in each availability Zone with minimum of 3 AZ.(6 copies).


Scaling Aurora
-------------------------------------------------------------------------
==>Aurora is designed to transparently handle the loss of 2 copies of data without affecting database and upto 3 copies without affecting read availability.

==>Aurora storage is also self healing.Data blocks and disks are continuously scanned for errors and repaired automatically.

3 Types of Replicas are supported==>Aurora ,Mysql,postgreSQl.

Backups on Aurora
------------------------------------------------------------------------
1) backups are enabled and do not impact database performance.
2) snapshots take and share with other aws accounts.

Amazon Aurora Serverless
------------------------------------------------------------------------
==>Ondemand , autoscale ,MySQL and postgreSQl Compatible.
==>An Aurora Serverless DB Cluster automatically starts up and shuts down and scales up and down on your applications need.

Usecases :
==>simple , cost-efficient option for infrequent or unpredictable workloads.

DynamoDB
--------------------------------------------------------------------------
1)Its a NOSQL database for all applications that nee consisitent , single-digit millisecond latency at any scale.
2)it is fully managed database and supports both document and key-value data models.
3)It is flexible data model and reliable performance make its great fit for mobile , web, gaming , ad-tech,IoT,and many other applications.


Facts about DynamoDB
--------------------------------------------------------------------------
1)Stored on SSD storage.
2)Spread across 3 geographically distinct data centers.
3)Eventually consistent reads(default)
4)Strongly consistent reads.

eventually consistent reads : 
---------------------------------------------------------------------------
1)consistency across all copies of data should be reached within 1 second. Repeating read after short time return updated data.
2)Gives Best Read performance.

Strongly Consistent Read :
---------------------------------------------------------------------------
A strongly consistent reads returns a result that reflects all writes that recieved successful prior to read.


DynamoDB Accelerator(DAX) : 
---------------------------------------------------------------------------
1)Fully Managed , highly available,in-memory cache.
2)10X performance
3)Compatible with DynamoDB API calls.

Caching with DAX : 
---------------------------------------------------------------------------
Application ===>DAX===>DynamoDB

Here we just need to connect to DAX no need worry about database.

Traditional:
---------------------------------------------------------------------------
Application====>Cache
Application====>DynamoDB

we need to separate connection for database and cache.


Security:
-------------------------------------------------------------------------
1)Encryption at rest using KMS.
2)Site to Site VPN.
3)Direct Connect(DX)
4)IAM policies and ROles 
5)Fine Grained Access.
6)VPC endpoints


When do we use DynamoDB Transactions
--------------------------------------------------------------------------
ACID ==>Atomic , Consistent , Isolated,Durable.

1)DynamoDB Transactions provides ACID properties.
2)ACID means all or nothing.


Usecases : 1)Financial Transactions .Fulfillling orders.

Reads: 1)Eventual consistency , Strong Consistency , amd Transactional Consistency.
Writes : Standard and transactional.


Saving Data with DynamoDB Backups
---------------------------------------------------------------------------
1)Full Backups at any time.
2)Zero impact on table performance or availability.
3)Consistent within seconds and retained until delated.
4)Operates within same regions.

Point in time recovery.
--------------------------------------------------------------------------
1)Accidental Recovery
2)Restore at any point within 30 days.
3)Incremental backups.
4)Not enabled by default.
5)Latest Restorable : 5 minutes in pasts.



DynamoDB Streams :
---------------------------------------------------------------------------1)Time - ordered - sequence of item level changes in a table
2)stored for 24 hours.
3)changes :insert /update/delete timesequence are in streams.
4)Combine with Lamda functions for functionality line stored procedures.


Manages Multi-Master,Multi-Region Replication.
---------------------------------------------------------------------------
1)Globally distributed Application.
2)Based on DynamoDB Streams.(Turn on DynamoDB Streams for Global Tables).
3)Multi-Region redundancy for disaster recovery of high availability.
4)No application rewrites.
5)Replication latency under 1s.



