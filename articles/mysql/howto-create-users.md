---
title: Create users in Azure Database for MySQL server
description: This article describes how you can create new user accounts to interact with an Azure Database for MySQL server.
services: mysql
author: jasonwhowell
ms.author: jasonh
editor: jasonwhowell
manager: kfile
ms.service: mysql
ms.topic: article
ms.date: 02/28/2018
ms.openlocfilehash: ee74ea9e114f6401bfcafe44ca3caedfcd0005c5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966348"
---
# <a name="create-users-in-azure-database-for-mysql-server"></a><span data-ttu-id="81212-103">Create users in Azure Database for MySQL server</span><span class="sxs-lookup"><span data-stu-id="81212-103">Create users in Azure Database for MySQL server</span></span> 
<span data-ttu-id="81212-104">This article describes how you can create users in an Azure Database for MySQL server.</span><span class="sxs-lookup"><span data-stu-id="81212-104">This article describes how you can create users in an Azure Database for MySQL server.</span></span>

<span data-ttu-id="81212-105">When you first created your Azure Database for MySQL, you provided a server admin login user name and password.</span><span class="sxs-lookup"><span data-stu-id="81212-105">When you first created your Azure Database for MySQL, you provided a server admin login user name and password.</span></span> <span data-ttu-id="81212-106">For more information, you can follow the [Quickstart](quickstart-create-mysql-server-database-using-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="81212-106">For more information, you can follow the [Quickstart](quickstart-create-mysql-server-database-using-azure-portal.md).</span></span> <span data-ttu-id="81212-107">You can locate your server admin login user name from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="81212-107">You can locate your server admin login user name from the Azure portal.</span></span>

<span data-ttu-id="81212-108">The server admin user gets certain privileges for your server as listed: SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, RELOAD, PROCESS, REFERENCES, INDEX, ALTER, SHOW DATABASES, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, REPLICATION SLAVE, REPLICATION CLIENT, CREATE VIEW, SHOW VIEW, CREATE ROUTINE, ALTER ROUTINE, CREATE USER, EVENT, TRIGGER</span><span class="sxs-lookup"><span data-stu-id="81212-108">The server admin user gets certain privileges for your server as listed: SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, RELOAD, PROCESS, REFERENCES, INDEX, ALTER, SHOW DATABASES, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, REPLICATION SLAVE, REPLICATION CLIENT, CREATE VIEW, SHOW VIEW, CREATE ROUTINE, ALTER ROUTINE, CREATE USER, EVENT, TRIGGER</span></span>

<span data-ttu-id="81212-109">Once the Azure Database for MySQL server is created, you can use the first server admin user account to create additional users and grant admin access to them.</span><span class="sxs-lookup"><span data-stu-id="81212-109">Once the Azure Database for MySQL server is created, you can use the first server admin user account to create additional users and grant admin access to them.</span></span> <span data-ttu-id="81212-110">Also, the server admin account can be used to create less privileged users that have access to individual database schemas.</span><span class="sxs-lookup"><span data-stu-id="81212-110">Also, the server admin account can be used to create less privileged users that have access to individual database schemas.</span></span>

## <a name="how-to-create-additional-admin-users-in-azure-database-for-mysql"></a><span data-ttu-id="81212-111">How to create additional admin users in Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="81212-111">How to create additional admin users in Azure Database for MySQL</span></span>
1. <span data-ttu-id="81212-112">Get the connection information and admin user name.</span><span class="sxs-lookup"><span data-stu-id="81212-112">Get the connection information and admin user name.</span></span>
   <span data-ttu-id="81212-113">To connect to your database server, you need the full server name and admin sign-in credentials.</span><span class="sxs-lookup"><span data-stu-id="81212-113">To connect to your database server, you need the full server name and admin sign-in credentials.</span></span> <span data-ttu-id="81212-114">You can easily find the server name and sign-in information from the server **Overview** page or the **Properties** page in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="81212-114">You can easily find the server name and sign-in information from the server **Overview** page or the **Properties** page in the Azure portal.</span></span> 

2. <span data-ttu-id="81212-115">Use the admin account and password to connect to your database server.</span><span class="sxs-lookup"><span data-stu-id="81212-115">Use the admin account and password to connect to your database server.</span></span> <span data-ttu-id="81212-116">Use your preferred client tool, such as MySQL Workbench, mysql.exe, HeidiSQL, or others.</span><span class="sxs-lookup"><span data-stu-id="81212-116">Use your preferred client tool, such as MySQL Workbench, mysql.exe, HeidiSQL, or others.</span></span> 
   <span data-ttu-id="81212-117">If you are unsure of how to connect, see [Use MySQL Workbench to connect and query data](./connect-workbench.md)</span><span class="sxs-lookup"><span data-stu-id="81212-117">If you are unsure of how to connect, see [Use MySQL Workbench to connect and query data](./connect-workbench.md)</span></span>

3. <span data-ttu-id="81212-118">Edit and run the following SQL code.</span><span class="sxs-lookup"><span data-stu-id="81212-118">Edit and run the following SQL code.</span></span> <span data-ttu-id="81212-119">Replace your new user name for the placeholder value `new_master_user`.</span><span class="sxs-lookup"><span data-stu-id="81212-119">Replace your new user name for the placeholder value `new_master_user`.</span></span> <span data-ttu-id="81212-120">This syntax grants the listed privileges on all the database schemas (*.*) to the user name (new_master_user in this example).</span><span class="sxs-lookup"><span data-stu-id="81212-120">This syntax grants the listed privileges on all the database schemas (*.*) to the user name (new_master_user in this example).</span></span> 

   ```sql
   CREATE USER 'new_master_user'@'%' IDENTIFIED BY 'StrongPassword!';
   
   GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, RELOAD, PROCESS, REFERENCES, INDEX, ALTER, SHOW DATABASES, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, REPLICATION SLAVE, REPLICATION CLIENT, CREATE VIEW, SHOW VIEW, CREATE ROUTINE, ALTER ROUTINE, CREATE USER, EVENT, TRIGGER ON *.* TO 'new_master_user'@'%' WITH GRANT OPTION; 
   
   FLUSH PRIVILEGES;
   ```

4. <span data-ttu-id="81212-121">Verify the grants</span><span class="sxs-lookup"><span data-stu-id="81212-121">Verify the grants</span></span> 
   ```sql
   USE sys;
   
   SHOW GRANTS FOR 'new_master_user'@'%';
   ```

## <a name="how-to-create-database-users-in-azure-database-for-mysql"></a><span data-ttu-id="81212-122">How to create database users in Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="81212-122">How to create database users in Azure Database for MySQL</span></span>

1. <span data-ttu-id="81212-123">Get the connection information and admin user name.</span><span class="sxs-lookup"><span data-stu-id="81212-123">Get the connection information and admin user name.</span></span>
   <span data-ttu-id="81212-124">To connect to your database server, you need the full server name and admin sign-in credentials.</span><span class="sxs-lookup"><span data-stu-id="81212-124">To connect to your database server, you need the full server name and admin sign-in credentials.</span></span> <span data-ttu-id="81212-125">You can easily find the server name and sign-in information from the server **Overview** page or the **Properties** page in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="81212-125">You can easily find the server name and sign-in information from the server **Overview** page or the **Properties** page in the Azure portal.</span></span> 

2. <span data-ttu-id="81212-126">Use the admin account and password to connect to your database server.</span><span class="sxs-lookup"><span data-stu-id="81212-126">Use the admin account and password to connect to your database server.</span></span> <span data-ttu-id="81212-127">Use your preferred client tool, such as MySQL Workbench, mysql.exe, HeidiSQL, or others.</span><span class="sxs-lookup"><span data-stu-id="81212-127">Use your preferred client tool, such as MySQL Workbench, mysql.exe, HeidiSQL, or others.</span></span> 
   <span data-ttu-id="81212-128">If you are unsure of how to connect, see [Use MySQL Workbench to connect and query data](./connect-workbench.md)</span><span class="sxs-lookup"><span data-stu-id="81212-128">If you are unsure of how to connect, see [Use MySQL Workbench to connect and query data](./connect-workbench.md)</span></span>

3. <span data-ttu-id="81212-129">Edit and run the following SQL code.</span><span class="sxs-lookup"><span data-stu-id="81212-129">Edit and run the following SQL code.</span></span> <span data-ttu-id="81212-130">Replace the placeholder value `db_user` with your intended new user name, and placeholder value `testdb` with your own database name.</span><span class="sxs-lookup"><span data-stu-id="81212-130">Replace the placeholder value `db_user` with your intended new user name, and placeholder value `testdb` with your own database name.</span></span>

   <span data-ttu-id="81212-131">This sql code syntax creates a new database named testdb for example purposes.</span><span class="sxs-lookup"><span data-stu-id="81212-131">This sql code syntax creates a new database named testdb for example purposes.</span></span> <span data-ttu-id="81212-132">Then it creates a new user in the MySQL service, and grants all privileges to the new database schema (testdb.\*) for that user.</span><span class="sxs-lookup"><span data-stu-id="81212-132">Then it creates a new user in the MySQL service, and grants all privileges to the new database schema (testdb.\*) for that user.</span></span> 

   ```sql
   CREATE DATABASE testdb;
   
   CREATE USER 'db_user'@'%' IDENTIFIED BY 'StrongPassword!';
   
   GRANT ALL PRIVILEGES ON testdb . * TO 'db_user'@'%';
   
   FLUSH PRIVILEGES;
   ```

4. <span data-ttu-id="81212-133">Verify the grants within the database.</span><span class="sxs-lookup"><span data-stu-id="81212-133">Verify the grants within the database.</span></span>
   ```sql
   USE testdb;
   
   SHOW GRANTS FOR 'db_user'@'%';
   ```

5. <span data-ttu-id="81212-134">Log in to the server, specifying the designated database, using the new user name and password.</span><span class="sxs-lookup"><span data-stu-id="81212-134">Log in to the server, specifying the designated database, using the new user name and password.</span></span> <span data-ttu-id="81212-135">This example shows the mysql command line.</span><span class="sxs-lookup"><span data-stu-id="81212-135">This example shows the mysql command line.</span></span> <span data-ttu-id="81212-136">With this command, you are prompted for the password for the user name.</span><span class="sxs-lookup"><span data-stu-id="81212-136">With this command, you are prompted for the password for the user name.</span></span> <span data-ttu-id="81212-137">Replace your own server name, database name, and user name.</span><span class="sxs-lookup"><span data-stu-id="81212-137">Replace your own server name, database name, and user name.</span></span>

   ```azurecli-interactive
   mysql --host mydemoserver.mysql.database.azure.com --database testdb --user db_user@mydemoserver -p
   ```

## <a name="next-steps"></a><span data-ttu-id="81212-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="81212-138">Next steps</span></span>
<span data-ttu-id="81212-139">Open the firewall for the IP addresses of the new users' machines to enable them to connect: [Create and manage Azure Database for MySQL firewall rules by using the Azure portal](howto-manage-firewall-using-portal.md) or [Azure CLI](howto-manage-firewall-using-cli.md).</span><span class="sxs-lookup"><span data-stu-id="81212-139">Open the firewall for the IP addresses of the new users' machines to enable them to connect: [Create and manage Azure Database for MySQL firewall rules by using the Azure portal](howto-manage-firewall-using-portal.md) or [Azure CLI](howto-manage-firewall-using-cli.md).</span></span>

<span data-ttu-id="81212-140">For more information regarding user account management, see MySQL product documentation for [User account management](https://dev.mysql.com/doc/refman/5.7/en/user-account-management.html), [GRANT Syntax](https://dev.mysql.com/doc/refman/5.7/en/grant.html), and [Privileges](https://dev.mysql.com/doc/refman/5.7/en/privileges-provided.html).</span><span class="sxs-lookup"><span data-stu-id="81212-140">For more information regarding user account management, see MySQL product documentation for [User account management](https://dev.mysql.com/doc/refman/5.7/en/user-account-management.html), [GRANT Syntax](https://dev.mysql.com/doc/refman/5.7/en/grant.html), and [Privileges](https://dev.mysql.com/doc/refman/5.7/en/privileges-provided.html).</span></span>
