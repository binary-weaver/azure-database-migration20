# azure-database-migration20

## Milestone 2: Set up a production environment
- Created a Windows Virtual Machine on Azure with the following instance details:
  - Virtual Machine name: my-vm
  - Region: UK
  - Image: Windows 10/11 Pro
  - Size: Standard_B2ms
  - Set a username and password for authentication
  - Ensure the Remote Desktop Protocol (RDP) port - port 3389 - is allowed in the Network Security Group (NSG) inbound rules for the virtual machine
- Downloaded the RDP file and connected to the virtual machine using an RDP client with the username and password created previously.
- Installed SQL Server and SQL Server Management Studio (SSMS) on the virtual machine.
- Created the production database by restoring it from this [backup file](https://aicore-portal-public-prod-307050600709.s3.eu-west-1.amazonaws.com/project-files/93dd5a0c-212d-48eb-ad51-df521a9b4e9c/AdventureWorks2022.bak).

## Milestone 3: Migrate to SQL 
- Created an Azure SQL Database in the Azure Portal using SQL login as the authentication method.
    -- This involved ensuring a firewall exception was created to allow a connection between the local and remote servers.
- Established a connection between the local SQL database and the remote SQL database using Azure Data Studio, serving as a conduit for schema and data migration.
- Installed the SQL Server Schema Compare extension within Azure Data Studio, and leveraged the extension to compare and subsequently migrate the schema from the on-premise database to the Azure SQL database.
- Installed the Azure SQL Migration extension within Azure Data Studio , and leveraged the extension to transfer the data from the on-premise database to the Azure SQL Database.

## Milestone 4:  Data Backup and Restore

-  Generated a full backup of the on-premise database within SQL Server Management Studio.
-  Configured an Azure Blob Storage account to serve as a secure online repository for database backups.
-  Uploaded the database backup (.bak) file to the Blob Storage container.
-  Provisioned a new Windows Virtual Machine to replicate the production environment and subsequently restored the database backup into this new "sandbox".
-  Automated weekly backups by utilising SQL Server Management Studio to establish a Management Plan, ensuring consisten protection for evolving work and simple recovery of the development environment if required.

## Milestone 5: Disaster Recovery Simulation

- Replicated a scenario where data integrity is compromised by deliberately removing data from the production database using Azure Data Studio on the production virtual machine.
- Restored production database utilizing Azure SQL Database Backup.
- Verified database was brought to a state just prior to the simulated disaster using Azure Data Studio to ensure all critical data was intact and functional.
- Deleted the database that suffered data loss through the Azure portal.

## Milestone 6: Geo Replication and Failover

- Created a synchronised replica of my primary production database that resides on a separate SQL server located in a distant secondary geographical region.
- Created a failover group on the primary SQL server within the Azure SQL Dashboard.
- Orchestrated a planned failover to the secondary region.
- Connected to the failover database in Azure Data Studio to verify its availability and data consistency.
- Performed failback to the original primary region.
