1. Read/Write Grace Period in Azure SQL Server (Serverless Tier)

When you use Azure SQL Database (Serverless compute tier), the database can auto-pause to save costs if idle.

Auto-pause: Happens when there are no connections and no CPU activity for a set duration.

Resume: When a new connection/query comes in, the DB wakes up (cold start, takes a few seconds).

Grace Period (default: 1 hour):

After the DB resumes, it will remain online for at least the grace period even if idle.

Prevents frequent pauses/resumes when there are intermittent queries.

Example:

DB is paused. You connect at 2:00 PM → DB resumes.

You disconnect at 2:05 PM.

DB stays running until at least 3:00 PM (grace period).

If still no activity, it auto-pauses after 3:00 PM.

👉 Useful for dev/test databases or workloads with intermittent usage.

🔹 2. Read/Write Listener & Read-Only Listener (Failover Groups)

Failover Groups in Azure SQL help with HA/DR (High Availability / Disaster Recovery) across regions.

Read-Write Listener Endpoint

DNS always points to the current primary.

Applications doing INSERT, UPDATE, DELETE, SELECT connect here.

Example: myapp-fog.database.windows.net.

Read-Only Listener Endpoint

DNS always points to the secondary replica.

Used for read-only queries (reporting, dashboards).

Example: myapp-fog.secondary.database.windows.net.

Prevents analytics/reporting load from affecting OLTP operations.

During failover → endpoints auto-switch.

🔹 3. Azure SQL Security Features

Auditing

Logs database activity for compliance.

Destinations: Azure Storage, Log Analytics, Event Hub.

Firewall & VNET Rules

Restrict traffic to specific IP ranges or VNets.

Transparent Data Encryption (TDE)

Encrypts DB files, backups, and logs at rest.

No code changes needed.

Advanced Data Security (optional)

Threat detection (alerts on suspicious logins, SQL injection).

Data classification & vulnerability assessment.

🔹 4. Intelligent Performance Features

Automatic Tuning:

Create Index: Adds missing indexes.

Drop Index: Removes unused/duplicate indexes.

Force Last Good Plan: Uses last stable plan if new plan causes regression.

Query Performance Insights: Visualize query duration & DTU/CPU usage.

🔹 5. Automation Examples

Automation Tasks in Azure SQL or via Logic Apps / Functions.
Example:

Monthly: Send cost report via email to admin.

Use Azure Automation Runbooks or Logic Apps.

🔹 6. Creating SQL Users

Ways to create a new SQL user:

Azure Data Studio

SSMS (SQL Server Management Studio)

Query Editor (Azure Portal)

SQL Script:

CREATE LOGIN user1 WITH PASSWORD = 'StrongPass@123';
CREATE USER user1 FOR LOGIN user1 WITH DEFAULT_SCHEMA = dbo;
ALTER ROLE db_owner ADD MEMBER user1;

🔹 7. SQL Server on Azure VM (IaaS)

Full Windows VM with SQL Server installed.

You manage:

Patching

Backups

HA/DR setup

SQL Agent jobs

Connect via RDP:

Open Remmina (Linux) or RDP client.

Enter VM’s Public IP and credentials.

Inside VM:

Open SSMS, connect to localhost SQL instance.

Use SQL logins (e.g., SA / custom user).

🔹 8. Stretch Database (⚠ Deprecated)

Normal setup: All data (hot + cold) stored on VM.

With Stretch DB:

Hot data → stays on-prem SQL Server.

Cold data → transparently moved to Azure SQL Database.

Queries span both, but cold data is remote (slower).

❌ Already retired/deprecated by Microsoft.

🔹 9. Migration (On-Prem SQL → Azure)

Data Migration Assistant (DMA):

Runs assessments (compatibility, issues).

Guides migration.

Azure Database Migration Service (DMS):

Online/offline migration at scale.

Target Options:

Azure SQL Database

Azure SQL Managed Instance

SQL Server on Azure VM

🔹 10. Azure Synapse Analytics

Combines Data Integration + Data Warehouse + Big Data Analytics.

Run analytics queries at scale over structured/unstructured data.

Azure Synapse Link for SQL Server:

Automatically captures row-level changes from SQL Server.

Streams them into Azure Synapse Lake Database.

Enables near real-time analytics without ETL.

✅ So in summary:

Grace Period → Keeps serverless DB running after resume.

Listener Endpoints → Simplify connectivity during failover.

Security → Auditing, TDE, Firewalls.

Performance → Auto-tuning, query insights.

VM vs PaaS → VM gives full control, PaaS (Azure SQL DB) is managed.

Migration → DMA & DMS help move from on-prem SQL.

Synapse → Analytics + real-time integration with SQL.
