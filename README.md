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



  
