# azure-database-migration20

## Milestone 2: Set up a production environment
- Create a Windows Virtual Machine on Azure with the following instance details:
  -- Virtual Machine name: my-vm
  -- Region: Pick the region geographically closest to you
  -- Image: Windows 10/11 Pro
  -- Size: Standard_B2ms
  -- Set a username and password for authentication
  --Ensure the Remote Desktop Protocol (RDP) port - port 3389 - is allowed in the Network Security Group (NSG) inbound rules for the virtual machine
- Download the RDP file and connect to the virtual machine using an RDP client, logging in with the username and password created previously.
- Install SQL Server and SQL Server Management Studio (SSMS) on the virtual machine.
- Create the production database by restoring it from this [backup file](https://aicore-portal-public-prod-307050600709.s3.eu-west-1.amazonaws.com/project-files/93dd5a0c-212d-48eb-ad51-df521a9b4e9c/AdventureWorks2022.bak).

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


  
