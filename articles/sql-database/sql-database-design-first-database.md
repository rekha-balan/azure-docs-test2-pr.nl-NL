---
title: Design your first Azure SQL database | Microsoft Docs
description: Learn to design your first Azure SQL database.
services: sql-database
documentationcenter: ''
author: janeng
manager: jstrauss
editor: ''
tags: ''
ms.assetid: ''
ms.service: sql-database
ms.custom: tutorial-develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: ''
ms.date: 03/30/2017
ms.author: janeng
ms.openlocfilehash: ca51ee37801430d64581cbedfee4e3d612e40e48
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552146"
---
# <a name="design-your-first-azure-sql-database"></a>Design your first Azure SQL database

In this tutorial, you build a database for a university to track student grades and courses enrollment. This tutorial demonstrates how to use the [Azure portal](https://portal.azure.com/) and [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) to create an Azure SQL database on an Azure SQL Database logical server, add tables to the database, load data into the tables, and query the database. It also demonstrates how to use SQL Database [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore) capabilities to restore the database to an earlier point in time.

To complete this tutorial, make sure you have installed the newest version of [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS). 

## <a name="step-1-log-in-to-the-azure-portal"></a>Step 1: Log in to the Azure portal

Log in to the [Azure portal](https://portal.azure.com/).

## <a name="step-2-create-a-blank-sql-database-in-azure"></a>Step 2: Create a blank SQL database in Azure

An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md). The database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md). 

Follow these steps to create a blank SQL database. 

1. Click the **New** button found on the upper left-hand corner of the Azure portal.

2. Select **Databases** from the **New** page, and select **SQL Database** from the **Databases** page. 

    ![create empty-database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-design-first-database/create-empty-database.png)

3. Fill out the SQL Database form with the following information, as shown on the preceding image:     

   - Database name: **mySampleDatabase**
   - Resource group: **myResourceGroup**
   - Source: **Blank database**

4. Click **Server** to create and configure a new server for your new database. Fill out the **New server form** specifying a globally unique server name, provide a name for the Server admin login, and then specify the password of your choice. 

    ![create database-server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-design-first-database/create-database-server.png)
5. Click **Select**.

6. Click **Pricing tier** to specify the service tier and performance level for your new database. For this tutorial, select **20 DTUs** and **250** GB of storage.

    ![create database-s1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. Click **Apply**.  

8. Click **Create** to provision the database. Provisioning takes about a minute and a half to complete. 

9. On the toolbar, click **Notifications** to monitor the deployment process.

    ![notification](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-get-started-portal/notification.png)


## <a name="step-3-create-a-server-level-firewall-rule"></a>Step 3: Create a server-level firewall rule

Azure SQL Databases are protected by a firewall. By default, all connections to the server and the databases inside the server are rejected. Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your server to allow connections from your client's IP address. 

1. After the deployment completes, click **SQL databases** from the left-hand menu and click your new database, **mySampleDatabase**, on the **SQL databases** page. The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver-20170313.database.windows.net**) and provides options for further configuration.

      ![server firewall rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-design-first-database/server-firewall-rule.png) 

2. Click **Set server firewall** on the toolbar as shown in the previous image. The **Firewall settings** page for the SQL Database server opens. 

3. Click **Add client IP** on the toolbar and then click **Save**. A server-level firewall rule is created for your current IP address.

      ![set server firewall rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-design-first-database/server-firewall-rule-set.png) 

4. Click **OK** and then click the **X** to close the **Firewall settings** page.

You can now connect to the database and its server using SQL Server Management Studio or another tool of your choice.

> [!NOTE]
> SQL Database communicates over port 1433. If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall. If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.
>

## <a name="step-4---get-connection-information"></a>Step 4 - Get connection information

Get the fully qualified server name for your Azure SQL Database server in the Azure portal. You use the fully qualified server name to connect to your server using SQL Server Management Studio.

1. Log in to the [Azure portal](https://portal.azure.com/).
2. Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page. 
3. In the **Essentials** pane in the Azure portal page for your database, locate and then copy the **Server name**.

    ![connection information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-ssms/connection-information.png) 

## <a name="step-5---connect-to-your-database-using-sql-server-management-studio"></a>Step 5 - Connect to your database using SQL Server Management Studio

Use [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) to establish a connection to your Azure SQL Database server.

1. Open SQL Server Management Studio.

2. In the **Connect to Server** dialog box, enter the following information:
   - **Server type**: Specify Database engine
   - **Server name**: Enter your fully qualified server name, such as **mynewserver20170313.database.windows.net**
   - **Authentication**: Specify SQL Server Authentication
   - **Login**: Enter your server admin account
   - **Password**: Enter the password for your server admin account


   <img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-ssms/connect.png" alt="connect to server" style="width: 780px;" />

3. Click **Options** in the **Connect to server** dialog box. In the **Connect to database** section, enter **mySampleDatabase** to connect to this database.

   ![connect to db on server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. Click **Connect**. The Object Explorer window opens in SSMS. 

5. In Object Explorer, expand **Databases** and then expand **mySampleDatabase** to view the objects in the sample database.

   ![database objects](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-connect-query-ssms/connected.png)  

## <a name="step-6---create-tables-in-the-database"></a>Step 6 - Create tables in the database 

Create a database schema with four tables that model a student management system for universities using [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference):

- Person
- Course
- Student
- Credit that model a student management system for universities

The following diagram shows how these tables are related to each other. Some of these tables reference columns in other tables. For example, the Student table references the **PersonId** column of the **Person** table. Study the diagram to understand how the tables in this tutorial are related to one another. For an in-depth look at how to create effective database tables, see [Create effective database tables](https://msdn.microsoft.com/library/cc505842.aspx). For information about choosing data types, see [Data types](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).

> [!NOTE]
> You can also use the [table designer in SQL Server Management Studio](https://msdn.microsoft.com/library/hh272695.aspx) to create and design your tables. 

![Table relationships](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-design-first-database/tutorial-database-tables.png)

1. In Object Explorer, right-click **mySampleDatabase** and click **New Query**. A blank query window opens that is connected to your database.

2. In the query window, execute the following query to create four tables in your database: 

   ```sql 
   -- Create Person table

    CREATE TABLE Person
    (
      PersonId      INT IDENTITY PRIMARY KEY,
      FirstName     NVARCHAR(128) NOT NULL,
      MiddelInitial NVARCHAR(10),
      LastName      NVARCHAR(128) NOT NULL,
      DateOfBirth   DATE NOT NULL
    )
   
   -- Create Student table
 
    CREATE TABLE Student
    (
      StudentId INT IDENTITY PRIMARY KEY,
      PersonId  INT REFERENCES Person (PersonId),
      Email     NVARCHAR(256)
    )
    
   -- Create Course table
 
    CREATE TABLE Course
    (
      CourseId  INT IDENTITY PRIMARY KEY,
      Name      NVARCHAR(50) NOT NULL,
      Teacher   NVARCHAR(256) NOT NULL
    ) 

   -- Create Credit table
 
    CREATE TABLE Credit
    (
      StudentId   INT REFERENCES Student (StudentId),
      CourseId    INT REFERENCES Course (CourseId),
      Grade       DECIMAL(5,2) CHECK (Grade <= 100.00),
      Attempt     TINYINT,
      CONSTRAINT  [UQ_studentgrades] UNIQUE CLUSTERED
      (
        StudentId, CourseId, Grade, Attempt
      )
    )
   ```

![Create tables](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-design-first-database/create-tables.png)

3. Expand the 'tables' node in the SQL Server Management Studio Object explorer to see the tables you created.

   ![ssms tables-created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-design-first-database/ssms-tables-created.png)

## <a name="step-7---load-data-into-the-tables"></a>Step 7 - Load data into the tables

1. Create a folder called **SampleTableData** in your Downloads folder to store sample data for your database. 

2. Right-click the following links and save them into the **SampleTableData** folder. 

   - [SampleCourseData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCourseData)
   - [SamplePersonData](https://sqldbtutorial.blob.core.windows.net/tutorials/SamplePersonData)
   - [SampleStudentData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleStudentData)
   - [SampleCreditData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCreditData)

3. Open a command prompt window and navigate to the SampleTableData folder.

4. Execute the following commands to insert sample data into the tables replacing the values for **ServerName**, **DatabaseName**, **UserName**, and **Password** with the values for your environment.
  
   ```bcp
   bcp Course in SampleCourseData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Person in SamplePersonData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Student in SampleStudentData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Credit in SampleCreditData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   ```

You have now loaded sample data into the tables you created earlier.

## <a name="step-8---query-the-tables"></a>Step 8 - Query the tables

Execute the following queries to retrieve information from the database tables. See [Writing SQL Queries](https://technet.microsoft.com/library/bb264565.aspx) to learn more about writing SQL queries. The first query joins all four tables to find all the students taught by 'Dominick Pope' who have a grade higher than 75% in his class. The second query joins all four tables and finds all courses in which 'Noe Coleman' has ever enrolled.

1. In a SQL Server Management Studio query window, execute the following query:

   ```sql 
   -- Find the students taught by Dominick Pope who have a grade higher than 75%

    SELECT  person.FirstName,
        person.LastName,
        course.Name,
        credit.Grade
    FROM  Person AS person
        INNER JOIN Student AS student ON person.PersonId = student.PersonId
        INNER JOIN Credit AS credit ON student.StudentId = credit.StudentId
        INNER JOIN Course AS course ON credit.CourseId = course.courseId
    WHERE course.Teacher = 'Dominick Pope' 
        AND Grade > 75
   ```

2. In a SQL Server Management Studio query window, execute following query:

   ```sql
   -- Find all the courses in which Noe Coleman has ever enrolled

    SELECT  course.Name,
        course.Teacher,
        credit.Grade
    FROM  Course AS course
        INNER JOIN Credit AS credit ON credit.CourseId = course.CourseId
        INNER JOIN Student AS student ON student.StudentId = credit.StudentId
        INNER JOIN Person AS person ON person.PersonId = student.PersonId
    WHERE person.FirstName = 'Noe'
        AND person.LastName = 'Coleman'
   ```

## <a name="step-9---restore-a-database-to-a-previous-point-in-time"></a>Step 9 - Restore a database to a previous point in time 

Imagine you have accidentally deleted a table. This is something you cannot easily recover from. Azure SQL Database allows you to go back to any point in time in the last up to 35 days and restore this point in time to a new database. You can you this database to recover your deleted data. The following steps restore the sample database to a point before the tables were added.

1. On the SQL Database page for your database, click **Restore** on the toolbar. The **Restore** page opens.

   ![restore](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-design-first-database/restore.png)

2. Fill out the **Restore** form with the required information:
    * Database name: Provide a database name 
    * Point-in-time: Select the **Point-in-time** tab on the Restore form 
    * Restore point: Select a time that occurs before the database was changed
    * Target server: You cannot change this value when restoring a database 
    * Elastic database pool: Select **None**  
    * Pricing tier: Select **20 DTUs** and **250 GB** of storage.

   ![restore-point](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-design-first-database/restore-point.png)

3. Click **OK** to restore the database to [restore to a point in time](sql-database-recovery-using-backups.md#point-in-time-restore) before the tables were added. Restoring a database to a different point in time creates a duplicate database in the same server as the original database as of the point in time you specify, provided that it is within the retention period for your [service tier](sql-database-service-tiers.md).

## <a name="next-steps"></a>Next Steps 

For PowerShell samples for common tasks, see [SQL Database PowerShell samples](sql-database-powershell-samples.md)















