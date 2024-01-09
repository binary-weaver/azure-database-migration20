#  Azure Database Migration

## Overview

This project involves migrating a production database to Azure SQL Database using Azure Database Migration Service. The migration process includes setting up a production environment, migrating the database schema and data, implementing disaster recovery simulations, enabling geo-replication with failover, and integrating Microsoft Entra Directory for authentication.

## Table of Contents

1. [Set up a Production Environment](#step-1-set-up-a-production-environment)
2. [Migrate to SQL](#step-2-migrate-to-sql)
3. [Data Backup and Restore](#step-3-data-backup-and-restore)
4. [Disaster Recovery Simulation](#step-4-disaster-recovery-simulation)
5. [Geo Replication and Failover](#step-5-geo-replication-and-failover)
6. [Microsoft Entra Directory Integration](#step-6-microsoft-entra-directory-integration)
7. [UML Diagram of Cloud Architecture](#uml-diagram-of-cloud-architecture)


## Step 1: Set Up a Production Environment
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

## Step 2: Migrate to SQL 
- Created an Azure SQL Database in the Azure Portal using SQL login as the authentication method.
    - Ensured a firewall exception was created to allow a connection between the local and remote servers.
- Established a connection between the local SQL database and the remote SQL database using Azure Data Studio, serving as a conduit for schema and data migration.
- Installed the SQL Server Schema Compare extension within Azure Data Studio, and leveraged the extension to compare and subsequently migrate the schema from the on-premise database to the Azure SQL database.
- Installed the Azure SQL Migration extension within Azure Data Studio , and leveraged the extension to transfer the data from the on-premise database to the Azure SQL Database.

## Step 3: Data Backup and Restore

-  Generated a full backup of the on-premise database within SQL Server Management Studio.
-  Configured an Azure Blob Storage account to serve as a secure online repository for database backups.
-  Uploaded the database backup (.bak) file to the Blob Storage container.
-  Provisioned a new Windows Virtual Machine to replicate the production environment and subsequently restored the database backup into this new "sandbox".
-  Automated weekly backups by utilising SQL Server Management Studio to establish a Management Plan, ensuring consisten protection for evolving work and simple recovery of the development environment if required.

## Step 4: Disaster Recovery Simulation

- Replicated a scenario where data integrity is compromised by deliberately removing data from the production database using Azure Data Studio on the production virtual machine.
- Restored production database utilizing Azure SQL Database Backup.
- Verified database was brought to a state just prior to the simulated disaster using Azure Data Studio to ensure all critical data was intact and functional.
- Deleted the database that suffered data loss through the Azure portal.

## Step 5: Geo Replication and Failover

- Created a synchronised replica of my primary production database that resides on a separate SQL server located in a distant secondary geographical region.
- Created a failover group on the primary SQL server within the Azure SQL Dashboard.
- Orchestrated a planned failover to the secondary region.
- Connected to the failover database in Azure Data Studio to verify its availability and data consistency.
- Performed failback to the original primary region.

## Step 6: Microsoft Entra Directory Integration

- Configured Microsoft Entra ID authentication for primary server hosting the production database.
- Subsequently allocated myself admin privileges to grant me the ability to create and manage users, assign roles, and control access to the database.
- Reconnected to the database using Microsoft Entra Admin details and verified privileges.
- Created a new user within the Microsoft Entra ID page of the Azure portal.
- Granted the "db_datareader" role to this user, allowing them to view but not modify the data, using  SQL query.
- Reconnected to the database using the db_datareader credentials.
- Verified user's read-only priveleges; select queries succeeded, delete queries failed.

## UML Diagram of Cloud Architecture
![Azure Project Diagram](https://github.com/binary-weaver/azure-database-migration20/assets/146210029/c54f907e-ee07-4585-97d0-bd636224be32)
