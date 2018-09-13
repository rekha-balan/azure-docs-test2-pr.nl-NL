---
title: Configure Data-in Replication to replicate data into Azure Database for MySQL.
description: This article describes how to set up Data-in Replication for Azure Database for MySQL.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.topic: article
ms.date: 08/31/2018
ms.openlocfilehash: 83d970cf41dde4141fcba84c39b9b750783e54e0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869816"
---
# <a name="how-to-configure-azure-database-for-mysql-data-in-replication"></a><span data-ttu-id="aa8cb-103">How to configure Azure Database for MySQL Data-in Replication</span><span class="sxs-lookup"><span data-stu-id="aa8cb-103">How to configure Azure Database for MySQL Data-in Replication</span></span>

<span data-ttu-id="aa8cb-104">In this article, you will learn how to set up Data-in Replication in the Azure Database for MySQL service by configuring the master and replica servers.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-104">In this article, you will learn how to set up Data-in Replication in the Azure Database for MySQL service by configuring the master and replica servers.</span></span> <span data-ttu-id="aa8cb-105">Data-in Replication allows you to synchronize data from a master MySQL server running on-premises, in virtual machines, or database services hosted by other cloud providers into a replica in the Azure Database for MySQL service.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-105">Data-in Replication allows you to synchronize data from a master MySQL server running on-premises, in virtual machines, or database services hosted by other cloud providers into a replica in the Azure Database for MySQL service.</span></span> 

<span data-ttu-id="aa8cb-106">This article assumes that you have at least some prior experience with MySQL servers and databases.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-106">This article assumes that you have at least some prior experience with MySQL servers and databases.</span></span>

## <a name="create-a-mysql-server-to-be-used-as-replica"></a><span data-ttu-id="aa8cb-107">Create a MySQL server to be used as replica</span><span class="sxs-lookup"><span data-stu-id="aa8cb-107">Create a MySQL server to be used as replica</span></span>

1. <span data-ttu-id="aa8cb-108">Create a new Azure Database for MySQL server</span><span class="sxs-lookup"><span data-stu-id="aa8cb-108">Create a new Azure Database for MySQL server</span></span>

   <span data-ttu-id="aa8cb-109">Create a new MySQL server (ex.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-109">Create a new MySQL server (ex.</span></span> <span data-ttu-id="aa8cb-110">"replica.mysql.database.azure.com").</span><span class="sxs-lookup"><span data-stu-id="aa8cb-110">"replica.mysql.database.azure.com").</span></span> <span data-ttu-id="aa8cb-111">Refer to [Create an Azure Database for MySQL server by using the Azure portal](quickstart-create-mysql-server-database-using-azure-portal.md) for server creation.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-111">Refer to [Create an Azure Database for MySQL server by using the Azure portal](quickstart-create-mysql-server-database-using-azure-portal.md) for server creation.</span></span> <span data-ttu-id="aa8cb-112">This server is the "replica" server in Data-in Replication.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-112">This server is the "replica" server in Data-in Replication.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="aa8cb-113">The Azure Database for MySQL server must be created in the General Purpose or Memory Optimized pricing tiers.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-113">The Azure Database for MySQL server must be created in the General Purpose or Memory Optimized pricing tiers.</span></span>
   > 

2. <span data-ttu-id="aa8cb-114">Create same user accounts and corresponding privileges</span><span class="sxs-lookup"><span data-stu-id="aa8cb-114">Create same user accounts and corresponding privileges</span></span>

   <span data-ttu-id="aa8cb-115">User accounts are not replicated from the master server to the replica server.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-115">User accounts are not replicated from the master server to the replica server.</span></span> <span data-ttu-id="aa8cb-116">If you plan on providing users with access to the replica server, you need to manually create all accounts and corresponding privileges on this newly created Azure Database for MySQL server.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-116">If you plan on providing users with access to the replica server, you need to manually create all accounts and corresponding privileges on this newly created Azure Database for MySQL server.</span></span>

## <a name="configure-the-master-server"></a><span data-ttu-id="aa8cb-117">Configure the master server</span><span class="sxs-lookup"><span data-stu-id="aa8cb-117">Configure the master server</span></span>
<span data-ttu-id="aa8cb-118">The following steps prepare and configure the MySQL server hosted on-premises, in a virtual machine, or database service hosted by other cloud providers for Data-in Replication.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-118">The following steps prepare and configure the MySQL server hosted on-premises, in a virtual machine, or database service hosted by other cloud providers for Data-in Replication.</span></span> <span data-ttu-id="aa8cb-119">This server is the "master" in Data-in replication.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-119">This server is the "master" in Data-in replication.</span></span> 

1. <span data-ttu-id="aa8cb-120">Turn on binary logging</span><span class="sxs-lookup"><span data-stu-id="aa8cb-120">Turn on binary logging</span></span>

   <span data-ttu-id="aa8cb-121">Check to see if binary logging has been enabled on the master by running the following command:</span><span class="sxs-lookup"><span data-stu-id="aa8cb-121">Check to see if binary logging has been enabled on the master by running the following command:</span></span> 

   ```sql
   SHOW VARIABLES LIKE 'log_bin';
   ```

   <span data-ttu-id="aa8cb-122">If the variable [`log_bin`](https://dev.mysql.com/doc/refman/8.0/en/replication-options-binary-log.html#sysvar_log_bin) is returned with the value “ON", binary logging is enabled on your server.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-122">If the variable [`log_bin`](https://dev.mysql.com/doc/refman/8.0/en/replication-options-binary-log.html#sysvar_log_bin) is returned with the value “ON", binary logging is enabled on your server.</span></span> 

   <span data-ttu-id="aa8cb-123">If `log_bin` is returned with the value “OFF”, turn on binary logging by editing your my.cnf file so that `log_bin=ON` and restart your server for the change to take effect.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-123">If `log_bin` is returned with the value “OFF”, turn on binary logging by editing your my.cnf file so that `log_bin=ON` and restart your server for the change to take effect.</span></span>

2. <span data-ttu-id="aa8cb-124">Master server settings</span><span class="sxs-lookup"><span data-stu-id="aa8cb-124">Master server settings</span></span>

   <span data-ttu-id="aa8cb-125">Data-in Replication requires parameter `lower_case_table_names` to be consistent between the master and replica servers.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-125">Data-in Replication requires parameter `lower_case_table_names` to be consistent between the master and replica servers.</span></span> <span data-ttu-id="aa8cb-126">This parameter is 1 by default in Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-126">This parameter is 1 by default in Azure Database for MySQL.</span></span> 

   ```sql
   SET GLOBAL lower_case_table_names = 1;
   ```

3. <span data-ttu-id="aa8cb-127">Create a new replication role and set up permission</span><span class="sxs-lookup"><span data-stu-id="aa8cb-127">Create a new replication role and set up permission</span></span>

   <span data-ttu-id="aa8cb-128">Create a user account on the master server that is configured with replication privileges.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-128">Create a user account on the master server that is configured with replication privileges.</span></span> <span data-ttu-id="aa8cb-129">This can be done through SQL commands or a tool like MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-129">This can be done through SQL commands or a tool like MySQL Workbench.</span></span> <span data-ttu-id="aa8cb-130">Consider whether you plan on replicating with SSL as this will need to be specified when creating the user.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-130">Consider whether you plan on replicating with SSL as this will need to be specified when creating the user.</span></span> <span data-ttu-id="aa8cb-131">Refer to the MySQL documentation to understand how to [add user accounts](https://dev.mysql.com/doc/refman/5.7/en/adding-users.html) on your master server.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-131">Refer to the MySQL documentation to understand how to [add user accounts](https://dev.mysql.com/doc/refman/5.7/en/adding-users.html) on your master server.</span></span> 

   <span data-ttu-id="aa8cb-132">In the commands below, the new replication role created is able to access the master from any machine, not just the machine that hosts the master itself.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-132">In the commands below, the new replication role created is able to access the master from any machine, not just the machine that hosts the master itself.</span></span> <span data-ttu-id="aa8cb-133">This is done by specifying "syncuser@'%'" in the create user command.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-133">This is done by specifying "syncuser@'%'" in the create user command.</span></span> <span data-ttu-id="aa8cb-134">See the MySQL documentation to learn more about [specifying account names](https://dev.mysql.com/doc/refman/5.7/en/account-names.html).</span><span class="sxs-lookup"><span data-stu-id="aa8cb-134">See the MySQL documentation to learn more about [specifying account names](https://dev.mysql.com/doc/refman/5.7/en/account-names.html).</span></span>

   <span data-ttu-id="aa8cb-135">**SQL Command**</span><span class="sxs-lookup"><span data-stu-id="aa8cb-135">**SQL Command**</span></span>

   <span data-ttu-id="aa8cb-136">*Replication with SSL*</span><span class="sxs-lookup"><span data-stu-id="aa8cb-136">*Replication with SSL*</span></span>

   <span data-ttu-id="aa8cb-137">To require SSL for all user connections, use the following command to create a user:</span><span class="sxs-lookup"><span data-stu-id="aa8cb-137">To require SSL for all user connections, use the following command to create a user:</span></span> 

   ```sql
   CREATE USER 'syncuser'@'%' IDENTIFIED BY 'yourpassword';
   GRANT REPLICATION SLAVE ON *.* TO ' syncuser'@'%' REQUIRE SSL;
   ```

   <span data-ttu-id="aa8cb-138">*Replication without SSL*</span><span class="sxs-lookup"><span data-stu-id="aa8cb-138">*Replication without SSL*</span></span>

   <span data-ttu-id="aa8cb-139">If SSL is not required for all connections, use the following command to create a user:</span><span class="sxs-lookup"><span data-stu-id="aa8cb-139">If SSL is not required for all connections, use the following command to create a user:</span></span>

   ```sql
   CREATE USER 'syncuser'@'%' IDENTIFIED BY 'yourpassword';
   GRANT REPLICATION SLAVE ON *.* TO ' syncuser'@'%';
   ```

   <span data-ttu-id="aa8cb-140">**MySQL Workbench**</span><span class="sxs-lookup"><span data-stu-id="aa8cb-140">**MySQL Workbench**</span></span>

   <span data-ttu-id="aa8cb-141">To create the replication role in MySQL Workbench, open the **Users and Privileges** panel from the **Management** panel.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-141">To create the replication role in MySQL Workbench, open the **Users and Privileges** panel from the **Management** panel.</span></span> <span data-ttu-id="aa8cb-142">Then click on **Add Account**.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-142">Then click on **Add Account**.</span></span> 
 
   ![Users and Privileges](./media/howto-data-in-replication/users_privileges.png)

   <span data-ttu-id="aa8cb-144">Type in the username into the **Login Name** field.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-144">Type in the username into the **Login Name** field.</span></span> 

   ![Sync user](./media/howto-data-in-replication/syncuser.png)
 
   <span data-ttu-id="aa8cb-146">Click on the **Administrative Roles** panel and then select **Replication Slave** from the list of **Global Privileges**.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-146">Click on the **Administrative Roles** panel and then select **Replication Slave** from the list of **Global Privileges**.</span></span> <span data-ttu-id="aa8cb-147">Then click on **Apply** to create the replication role.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-147">Then click on **Apply** to create the replication role.</span></span>

   ![Replication Slave](./media/howto-data-in-replication/replicationslave.png)


4. <span data-ttu-id="aa8cb-149">Set the master server to read-only mode</span><span class="sxs-lookup"><span data-stu-id="aa8cb-149">Set the master server to read-only mode</span></span>

   <span data-ttu-id="aa8cb-150">Before starting to dump out the database, the server needs to be placed in read-only mode.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-150">Before starting to dump out the database, the server needs to be placed in read-only mode.</span></span> <span data-ttu-id="aa8cb-151">While in read-only mode, the master will be unable to process any write transactions.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-151">While in read-only mode, the master will be unable to process any write transactions.</span></span> <span data-ttu-id="aa8cb-152">Evaluate the impact to your business and schedule the read-only window in an off-peak time if necessary.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-152">Evaluate the impact to your business and schedule the read-only window in an off-peak time if necessary.</span></span>

   ```sql
   FLUSH TABLES WITH READ LOCK;
   SET GLOBAL read_only = ON;
   ```

5. <span data-ttu-id="aa8cb-153">Get binary log file name and offset</span><span class="sxs-lookup"><span data-stu-id="aa8cb-153">Get binary log file name and offset</span></span>

   <span data-ttu-id="aa8cb-154">Run the [`show master status`](https://dev.mysql.com/doc/refman/5.7/en/show-master-status.html) command to determine the current binary log file name and offset.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-154">Run the [`show master status`](https://dev.mysql.com/doc/refman/5.7/en/show-master-status.html) command to determine the current binary log file name and offset.</span></span>
    
   ```sql
   show master status;
   ```
   <span data-ttu-id="aa8cb-155">The results should be like following.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-155">The results should be like following.</span></span> <span data-ttu-id="aa8cb-156">Make sure to note the binary file name as it will be used in later steps.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-156">Make sure to note the binary file name as it will be used in later steps.</span></span>

   ![Master Status Results](./media/howto-data-in-replication/masterstatus.png)
 
## <a name="dump-and-restore-master-server"></a><span data-ttu-id="aa8cb-158">Dump and restore master server</span><span class="sxs-lookup"><span data-stu-id="aa8cb-158">Dump and restore master server</span></span>

1. <span data-ttu-id="aa8cb-159">Dump all databases from master server</span><span class="sxs-lookup"><span data-stu-id="aa8cb-159">Dump all databases from master server</span></span>

   <span data-ttu-id="aa8cb-160">You can use mysqldump to dump databases from your master.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-160">You can use mysqldump to dump databases from your master.</span></span> <span data-ttu-id="aa8cb-161">For details, refer to [Dump & Restore](concepts-migrate-dump-restore.md).</span><span class="sxs-lookup"><span data-stu-id="aa8cb-161">For details, refer to [Dump & Restore](concepts-migrate-dump-restore.md).</span></span> <span data-ttu-id="aa8cb-162">It is unnecessary to dump MySQL library and test library.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-162">It is unnecessary to dump MySQL library and test library.</span></span>

2. <span data-ttu-id="aa8cb-163">Set master server to read/write mode</span><span class="sxs-lookup"><span data-stu-id="aa8cb-163">Set master server to read/write mode</span></span>

   <span data-ttu-id="aa8cb-164">Once the database has been dumped, change the master MySQL server back to read/write mode.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-164">Once the database has been dumped, change the master MySQL server back to read/write mode.</span></span>

   ```sql
   SET GLOBAL read_only = OFF;
   UNLOCK TABLES;
   ```

3. <span data-ttu-id="aa8cb-165">Restore dump file to new server</span><span class="sxs-lookup"><span data-stu-id="aa8cb-165">Restore dump file to new server</span></span>

   <span data-ttu-id="aa8cb-166">Restore the dump file to the server created in the Azure Database for MySQL service.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-166">Restore the dump file to the server created in the Azure Database for MySQL service.</span></span> <span data-ttu-id="aa8cb-167">Refer to [Dump & Restore](concepts-migrate-dump-restore.md) for how to restore a dump file to a MySQL server.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-167">Refer to [Dump & Restore](concepts-migrate-dump-restore.md) for how to restore a dump file to a MySQL server.</span></span> <span data-ttu-id="aa8cb-168">If the dump file is large, upload it to a virtual machine in Azure within the same region as your replica server.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-168">If the dump file is large, upload it to a virtual machine in Azure within the same region as your replica server.</span></span> <span data-ttu-id="aa8cb-169">Restore it to the Azure Database for MySQL server from the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-169">Restore it to the Azure Database for MySQL server from the virtual machine.</span></span>

## <a name="link-master-and-replica-servers-to-start-data-in-replication"></a><span data-ttu-id="aa8cb-170">Link master and replica servers to start Data-in Replication</span><span class="sxs-lookup"><span data-stu-id="aa8cb-170">Link master and replica servers to start Data-in Replication</span></span>

1. <span data-ttu-id="aa8cb-171">Set master server</span><span class="sxs-lookup"><span data-stu-id="aa8cb-171">Set master server</span></span>

   <span data-ttu-id="aa8cb-172">All Data-in Replication functions are done by stored procedures.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-172">All Data-in Replication functions are done by stored procedures.</span></span> <span data-ttu-id="aa8cb-173">You can find all procedures at [Data-in Replication Stored Procedures](reference-data-in-stored-procedures.md).</span><span class="sxs-lookup"><span data-stu-id="aa8cb-173">You can find all procedures at [Data-in Replication Stored Procedures](reference-data-in-stored-procedures.md).</span></span> <span data-ttu-id="aa8cb-174">The stored procedures can be run in the MySQL shell or MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-174">The stored procedures can be run in the MySQL shell or MySQL Workbench.</span></span> 

   <span data-ttu-id="aa8cb-175">To link two servers and start replication, login to the target replica server in the Azure DB for MySQL service and set the external instance as the master server.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-175">To link two servers and start replication, login to the target replica server in the Azure DB for MySQL service and set the external instance as the master server.</span></span> <span data-ttu-id="aa8cb-176">This is done by using the `mysql.az_replication_change_master` stored procedure on the Azure DB for MySQL server.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-176">This is done by using the `mysql.az_replication_change_master` stored procedure on the Azure DB for MySQL server.</span></span>

   ```sql
   CALL mysql.az_replication_change_master('<master_host>', '<master_user>', '<master_password>', 3306, '<master_log_file>', <master_log_pos>, '<master_ssl_ca>');
   ```

   - <span data-ttu-id="aa8cb-177">master_host: hostname of the master server</span><span class="sxs-lookup"><span data-stu-id="aa8cb-177">master_host: hostname of the master server</span></span>
   - <span data-ttu-id="aa8cb-178">master_user: username for the master server</span><span class="sxs-lookup"><span data-stu-id="aa8cb-178">master_user: username for the master server</span></span>
   - <span data-ttu-id="aa8cb-179">master_password: password for the master server</span><span class="sxs-lookup"><span data-stu-id="aa8cb-179">master_password: password for the master server</span></span>
   - <span data-ttu-id="aa8cb-180">master_log_file: binary log file name from running `show master status`</span><span class="sxs-lookup"><span data-stu-id="aa8cb-180">master_log_file: binary log file name from running `show master status`</span></span>
   - <span data-ttu-id="aa8cb-181">master_log_pos: binary log position from running `show master status`</span><span class="sxs-lookup"><span data-stu-id="aa8cb-181">master_log_pos: binary log position from running `show master status`</span></span>
   - <span data-ttu-id="aa8cb-182">master_ssl_ca: CA certificate’s context.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-182">master_ssl_ca: CA certificate’s context.</span></span> <span data-ttu-id="aa8cb-183">If not using SSL, pass in empty string.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-183">If not using SSL, pass in empty string.</span></span>
       - <span data-ttu-id="aa8cb-184">It is recommended to pass this parameter in as a variable.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-184">It is recommended to pass this parameter in as a variable.</span></span> <span data-ttu-id="aa8cb-185">See the following examples for more information.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-185">See the following examples for more information.</span></span>

   <span data-ttu-id="aa8cb-186">**Examples**</span><span class="sxs-lookup"><span data-stu-id="aa8cb-186">**Examples**</span></span>

   <span data-ttu-id="aa8cb-187">*Replication with SSL*</span><span class="sxs-lookup"><span data-stu-id="aa8cb-187">*Replication with SSL*</span></span>

   <span data-ttu-id="aa8cb-188">The variable `@cert` is created by running the following MySQL commands:</span><span class="sxs-lookup"><span data-stu-id="aa8cb-188">The variable `@cert` is created by running the following MySQL commands:</span></span> 

   ```sql
   SET @cert = '-----BEGIN CERTIFICATE-----
   PLACE YOUR PUBLIC KEY CERTIFICATE’S CONTEXT HERE
   -----END CERTIFICATE-----'
   ```

   <span data-ttu-id="aa8cb-189">Replication with SSL is set up between a master server hosted in the domain “companya.com” and a replica server hosted in Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-189">Replication with SSL is set up between a master server hosted in the domain “companya.com” and a replica server hosted in Azure Database for MySQL.</span></span> <span data-ttu-id="aa8cb-190">This stored procedure is run on the replica.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-190">This stored procedure is run on the replica.</span></span> 

   ```sql
   CALL mysql.az_replication_change_master('master.companya.com', 'syncuser', 'P@ssword!', 3306, 'mysql-bin.000002', 120, @cert);
   ```
   <span data-ttu-id="aa8cb-191">*Replication without SSL*</span><span class="sxs-lookup"><span data-stu-id="aa8cb-191">*Replication without SSL*</span></span>

   <span data-ttu-id="aa8cb-192">Replication without SSL is set up between a master server hosted in the domain “companya.com” and a replica server hosted in Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-192">Replication without SSL is set up between a master server hosted in the domain “companya.com” and a replica server hosted in Azure Database for MySQL.</span></span> <span data-ttu-id="aa8cb-193">This stored procedure is run on the replica.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-193">This stored procedure is run on the replica.</span></span>

   ```sql
   CALL mysql.az_replication_change_master('master.companya.com', 'syncuser', 'P@ssword!', 3306, 'mysql-bin.000002', 120, '');
   ```

2. <span data-ttu-id="aa8cb-194">Start replication</span><span class="sxs-lookup"><span data-stu-id="aa8cb-194">Start replication</span></span>

   <span data-ttu-id="aa8cb-195">Call the `mysql.az_replication_start` stored procedure to initiate replication.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-195">Call the `mysql.az_replication_start` stored procedure to initiate replication.</span></span>

   ```sql
   CALL mysql.az_replication_start;
   ```

3. <span data-ttu-id="aa8cb-196">Check replication status</span><span class="sxs-lookup"><span data-stu-id="aa8cb-196">Check replication status</span></span>

   <span data-ttu-id="aa8cb-197">Call the [`show slave status`](https://dev.mysql.com/doc/refman/5.7/en/show-slave-status.html) command on the replica server to view the replication status.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-197">Call the [`show slave status`](https://dev.mysql.com/doc/refman/5.7/en/show-slave-status.html) command on the replica server to view the replication status.</span></span>
    
   ```sql
   show slave status;
   ```

   <span data-ttu-id="aa8cb-198">If the state of `Slave_IO_Running` and `Slave_SQL_Running` are "yes" and the value of `Seconds_Behind_Master` is “0”, replication is working well.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-198">If the state of `Slave_IO_Running` and `Slave_SQL_Running` are "yes" and the value of `Seconds_Behind_Master` is “0”, replication is working well.</span></span> <span data-ttu-id="aa8cb-199">`Seconds_Behind_Master` indicates how late the replica is.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-199">`Seconds_Behind_Master` indicates how late the replica is.</span></span> <span data-ttu-id="aa8cb-200">If the value is not "0", it means that the replica is processing updates.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-200">If the value is not "0", it means that the replica is processing updates.</span></span> 

## <a name="other-stored-procedures"></a><span data-ttu-id="aa8cb-201">Other stored procedures</span><span class="sxs-lookup"><span data-stu-id="aa8cb-201">Other stored procedures</span></span>

### <a name="stop-replication"></a><span data-ttu-id="aa8cb-202">Stop replication</span><span class="sxs-lookup"><span data-stu-id="aa8cb-202">Stop replication</span></span>

<span data-ttu-id="aa8cb-203">To stop replication between the master and replica server, use the following stored procedure:</span><span class="sxs-lookup"><span data-stu-id="aa8cb-203">To stop replication between the master and replica server, use the following stored procedure:</span></span>

```sql
CALL mysql.az_replication_stop;
```

### <a name="remove-replication-relationship"></a><span data-ttu-id="aa8cb-204">Remove replication relationship</span><span class="sxs-lookup"><span data-stu-id="aa8cb-204">Remove replication relationship</span></span>

<span data-ttu-id="aa8cb-205">To remove the relationship between master and replica server, use the following stored procedure:</span><span class="sxs-lookup"><span data-stu-id="aa8cb-205">To remove the relationship between master and replica server, use the following stored procedure:</span></span>

```sql
CALL mysql.az_replication_remove_master;
```

### <a name="skip-replication-error"></a><span data-ttu-id="aa8cb-206">Skip replication error</span><span class="sxs-lookup"><span data-stu-id="aa8cb-206">Skip replication error</span></span>

<span data-ttu-id="aa8cb-207">To skip a replication error and allow replication to proceed, use the following stored procedure:</span><span class="sxs-lookup"><span data-stu-id="aa8cb-207">To skip a replication error and allow replication to proceed, use the following stored procedure:</span></span>
    
```sql
CALL mysql.az_replication_skip_counter;
```

## <a name="next-steps"></a><span data-ttu-id="aa8cb-208">Next steps</span><span class="sxs-lookup"><span data-stu-id="aa8cb-208">Next steps</span></span>
- <span data-ttu-id="aa8cb-209">Learn more about [Data-in Replication](concepts-data-in-replication.md) for Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="aa8cb-209">Learn more about [Data-in Replication](concepts-data-in-replication.md) for Azure Database for MySQL.</span></span> 
