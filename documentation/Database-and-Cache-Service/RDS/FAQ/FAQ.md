# FAQ
## Current Types Supported by Cloud Database
The following engines and versions are supported by RDS which will support more database engine types and versions

- MySQL
    - 5.6
    - 5.7
    - 8.0
  
- Percona:
    - 5.7
  
- MariaDB
    - 10.2
  
- SQL Sever
    - 2008 R2: Enterprise Version
    - 2012: Enterprise Version and Standard Version
    - 2014: Enterprise Version and Standard Version
    - 2016: Enterprise Version, Standard Version and Web Version

## VM's Failure to Access RDS
Following conditions shall be met for the VM accessing RDS:
  - The VM shall be in one VPC with RDS.
  - VM may fail to access database due to wrong rules of the security group configured in the VM. The correct configuration of the VM security group is given in the VM settings.

## Software License
- The JCS for SQL server service already contains the Microsoft SQL Server software license, and will be authorized by Microsoft SQL Server license after the instance is created. You don't have to purchase JCS for SQL Server license separately.
- When a SQL Server instance is expired and deleted, the corresponding software license will fail accordingly, and you cannot use the original license for other authorization.
- The JCS for SQL Server Service does not support users' own SQL Server license temporarily.

## The historical data in JCS for SQL Server performance analysis cannot be seen after the JCS for SQL Server service instance is rebooted.
The data in the performance analysis is saved in the instance memory. The performance analysis data will be lost after the instance is rebooted. You can use following two OpenAPIs to export the data if demanding the historical data analysis.
- describeIndexPerformance
- describeQueryPerformance

## Users still cannot connect to the RDS instance via internet after the instance access is opened.
In default, the RDS White List is only available to the VPC where this instance resides to ensure data security. Thus, you need to add your new IP address in the White List to access the database instance.

## Why not enter a username and password when creating a database based on backup or time point.
The username and password of the backup source database may be used for the new database created based on the backup or time point, which temporarily does not support the manual input during creation.

## Why does only a part of optional configuration can be displayed during backup creation?
Users can only select configurations not less than the actual size of the backup when creating a backup according to a backup.

## How many days are the automatic backup available now?
Automatic backup is currently available for 7 days at least.

## How to solve the problem that JD Cloud RDS instance is under creation for a long time and finally gets into an error state?
If a network ACL is set for the subnet selected when the JD Cloud RDS is created, please ensure that DNS (UDP) rules are added into the outbound rules and accepted. Since the network ACL is stateless, please ensure that the inbound rules also allow the ALL UDP configurations. If the problem remains unresolved, please contact the customer service in work order form.

## How to modify parameters of JCS for MySQL service instance?
At present, user are not allowed to modify JCS for MySQL instance parameters in JD Cloud. Therefore, users can feed back the demands through open ticket to the engineers of JD Cloud, and the engineers will help give assistance in the modification.

## Some data is deleted for a large table in JCS for MySQL, but the data space disk usage has not changed through the monitoring graph
This is a data file fragment hole problem. When InnoDB performs data deletion, the deleted space will not be recovered, and it will cause a lot of file holes, leading to that the data space usage in the monitoring graph will not change. Optimization method: `OPTIMIZE TABLE <table>` or `ALTER TABLE <table> ENGINE=Innodb` to rebuild the table space.

## I want to modify the character set of a created database. But my account does not have such permission and the console does not provide corresponding interface. What shall I do?
You can modify the character set of a database via DMS; Click **Console** to log in the database, select the name of the database containing the character set intended to be modified from the left after logging in DMS and click the operation tab on the top bar behind to refresh the current page; then, the ranking rule option will be shown in the current page; and choose the character set intended to be modified and click **Execute**.
