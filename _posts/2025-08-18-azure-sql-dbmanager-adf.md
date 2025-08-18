---
layout: post
title:  "Azure SQL, dbmanager and ADF pipeline with Managed Identity"
date:   2025-08-18 20:00:00 +0200
categories: Azure SQL dbmanager ADF
---
# Azure SQL, dbmanager and ADF pipeline with Managed Identity

If you have to create **Azure SQL** databases in your **ADF** (Azure Data Factory) pipeline script, you might have run into issues with SQL permissions. e.g. error might be `CREATE DATABASE permission denied in database master`. And you might have noticed that if you use your own Azure Entra identity, you can run same commands without issues. So why doesn't it work?

Issue happens because `CREATE DATABASE` T-SQL command needs some [extra permissions](https://learn.microsoft.com/en-us/azure/azure-sql/database/single-database-create-quickstart?view=azuresql&tabs=azure-portal#permissions) to work if user executing the commands does not belong to the Azure SQL admin group. Even if most permissions in Azure SQL are given per database, the [dbmanager permission](https://learn.microsoft.com/en-us/sql/relational-databases/security/authentication-access/database-level-roles?view=sql-server-ver17#special-roles-for-azure-sql-database-and-azure-synapse) must be given to **master** database.

Situation gets even more trickier if you want to use Managed Identity with ADF when you login into Azure SQL as you created linked service.

## Steps

In this example I use name **my-adf** for Azure ADF resource, **my-sql** for Azure SQL Server and **my-sqldb** for Azure SQL datase.

1. Create your **my-adf** ADF resource (e.g via Azure portal)
2. Enable system managed identity for **my-adf** (e.g via Azure portal)
3. Go to [ADF portal](http://adf.azure.com/) and choose the **my-adf**, then add linked service (sorry, no help for this part)
4. Create a pipeline in ADF and add a script to the pipeline with `CREATE DATABASE my-sqldb` T-SQL command
5. Open **SQL Server Management Studio** (SSMS) and connect to `my-sql.database.windows.net` with your own credentials (assuming you are an Azure SQL Server admin), open the **master** database and execute following commands (this will add required role to the managed identity)
```SQL
CREATE USER [my-adf] FROM EXTERNAL PROVIDER;
ALTER ROLE dbmanager ADD MEMBER [my-adf];
```
6. Run debug for the ADF pipeline and see if it works