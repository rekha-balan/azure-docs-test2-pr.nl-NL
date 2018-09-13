---
title: Use the Azure Database Migration Service to perform an online migration of MySQL to Azure Database for MySQL | Microsoft Docs
description: Learn to perform an online migration from MySQL on-premises to Azure Database for MySQL by using the Azure Database Migration Service.
services: dms
author: HJToland3
ms.author: jtoland
manager: craigg
ms.reviewer: ''
ms.service: dms
ms.workload: data-services
ms.custom: mvc, tutorial
ms.topic: article
ms.date: 08/31/2018
ms.openlocfilehash: c36a771266f595f6d8dc8575d100fa5bb9496584
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867806"
---
# <a name="migrate-mysql-to-azure-database-for-mysql-online-using-dms"></a><span data-ttu-id="8c0ab-103">Migrate MySQL to Azure Database for MySQL online using DMS</span><span class="sxs-lookup"><span data-stu-id="8c0ab-103">Migrate MySQL to Azure Database for MySQL online using DMS</span></span>
<span data-ttu-id="8c0ab-104">You can use the Azure Database Migration Service to migrate the databases from an on-premises MySQL instance to [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/) with minimal downtime.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-104">You can use the Azure Database Migration Service to migrate the databases from an on-premises MySQL instance to [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/) with minimal downtime.</span></span> <span data-ttu-id="8c0ab-105">In other words, migration can be achieved with minimum downtime to the application.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-105">In other words, migration can be achieved with minimum downtime to the application.</span></span> <span data-ttu-id="8c0ab-106">In this tutorial, you migrate the **Employees** sample database from an on-premises instance of MySQL 5.7 to Azure Database for MySQL by using an online migration activity in the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-106">In this tutorial, you migrate the **Employees** sample database from an on-premises instance of MySQL 5.7 to Azure Database for MySQL by using an online migration activity in the Azure Database Migration Service.</span></span>

<span data-ttu-id="8c0ab-107">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="8c0ab-107">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="8c0ab-108">Migrate the sample schema using mysqldump utility.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-108">Migrate the sample schema using mysqldump utility.</span></span>
> * <span data-ttu-id="8c0ab-109">Create an instance of the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-109">Create an instance of the Azure Database Migration Service.</span></span>
> * <span data-ttu-id="8c0ab-110">Create a migration project by using the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-110">Create a migration project by using the Azure Database Migration Service.</span></span>
> * <span data-ttu-id="8c0ab-111">Run the migration.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-111">Run the migration.</span></span>
> * <span data-ttu-id="8c0ab-112">Monitor the migration.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-112">Monitor the migration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8c0ab-113">For an optimal migration experience, Microsoft recommends creating an instance of the Azure Database Migration Service in the same Azure region as the target database.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-113">For an optimal migration experience, Microsoft recommends creating an instance of the Azure Database Migration Service in the same Azure region as the target database.</span></span> <span data-ttu-id="8c0ab-114">Moving data across regions or geographies can slow down the migration process and introduce errors.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-114">Moving data across regions or geographies can slow down the migration process and introduce errors.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c0ab-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8c0ab-115">Prerequisites</span></span>
<span data-ttu-id="8c0ab-116">To complete this tutorial, you need to:</span><span class="sxs-lookup"><span data-stu-id="8c0ab-116">To complete this tutorial, you need to:</span></span>

- <span data-ttu-id="8c0ab-117">Download and install [MySQL community edition](https://dev.mysql.com/downloads/mysql/) 5.6 or 5.7.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-117">Download and install [MySQL community edition](https://dev.mysql.com/downloads/mysql/) 5.6 or 5.7.</span></span> <span data-ttu-id="8c0ab-118">The on-premises MySQL version must match with Azure Database for MySQL version.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-118">The on-premises MySQL version must match with Azure Database for MySQL version.</span></span> <span data-ttu-id="8c0ab-119">For example, MySQL 5.6 can only migrate to Azure Database for MySQL 5.6 and not upgraded to 5.7.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-119">For example, MySQL 5.6 can only migrate to Azure Database for MySQL 5.6 and not upgraded to 5.7.</span></span>
- <span data-ttu-id="8c0ab-120">[Create an instance in Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/quickstart-create-mysql-server-database-using-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="8c0ab-120">[Create an instance in Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/quickstart-create-mysql-server-database-using-azure-portal).</span></span> <span data-ttu-id="8c0ab-121">Refer to the article [Use MySQL Workbench to connect and query data](https://docs.microsoft.com/azure/mysql/connect-workbench) for details about how to connect and create a database using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-121">Refer to the article [Use MySQL Workbench to connect and query data](https://docs.microsoft.com/azure/mysql/connect-workbench) for details about how to connect and create a database using the Azure portal.</span></span>  
- <span data-ttu-id="8c0ab-122">Create a VNET for the Azure Database Migration Service by using the Azure Resource Manager deployment model, which provides site-to-site connectivity to your on-premises source servers by using either [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) or [VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).</span><span class="sxs-lookup"><span data-stu-id="8c0ab-122">Create a VNET for the Azure Database Migration Service by using the Azure Resource Manager deployment model, which provides site-to-site connectivity to your on-premises source servers by using either [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) or [VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).</span></span>
- <span data-ttu-id="8c0ab-123">Ensure that your Azure Virtual Network (VNET) Network Security Group rules do not block the following communication ports 443, 53, 9354, 445, 12000.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-123">Ensure that your Azure Virtual Network (VNET) Network Security Group rules do not block the following communication ports 443, 53, 9354, 445, 12000.</span></span> <span data-ttu-id="8c0ab-124">For more detail on Azure VNET NSG traffic filtering, see the article [Filter network traffic with network security groups](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm).</span><span class="sxs-lookup"><span data-stu-id="8c0ab-124">For more detail on Azure VNET NSG traffic filtering, see the article [Filter network traffic with network security groups](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm).</span></span>
- <span data-ttu-id="8c0ab-125">Configure your [Windows Firewall for database engine access](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access).</span><span class="sxs-lookup"><span data-stu-id="8c0ab-125">Configure your [Windows Firewall for database engine access](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access).</span></span>
- <span data-ttu-id="8c0ab-126">Open your Windows firewall to allow the Azure Database Migration Service to access the source MySQL Server, which by default is TCP port 3306.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-126">Open your Windows firewall to allow the Azure Database Migration Service to access the source MySQL Server, which by default is TCP port 3306.</span></span>
- <span data-ttu-id="8c0ab-127">When using a firewall appliance in front of your source database(s), you may need to add firewall rules to allow the Azure Database Migration Service to access the source database(s) for migration.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-127">When using a firewall appliance in front of your source database(s), you may need to add firewall rules to allow the Azure Database Migration Service to access the source database(s) for migration.</span></span>
- <span data-ttu-id="8c0ab-128">Create a server-level [firewall rule](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) for Azure Database for MySQL to allow the Azure Database Migration Service access to the target databases.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-128">Create a server-level [firewall rule](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) for Azure Database for MySQL to allow the Azure Database Migration Service access to the target databases.</span></span> <span data-ttu-id="8c0ab-129">Provide the subnet range of the VNET used for the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-129">Provide the subnet range of the VNET used for the Azure Database Migration Service.</span></span>
- <span data-ttu-id="8c0ab-130">The source MySQL must be on supported MySQL community edition.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-130">The source MySQL must be on supported MySQL community edition.</span></span> <span data-ttu-id="8c0ab-131">To determine the version of MySQL instance, in the MySQL utility or MySQL Workbench, run the following command:</span><span class="sxs-lookup"><span data-stu-id="8c0ab-131">To determine the version of MySQL instance, in the MySQL utility or MySQL Workbench, run the following command:</span></span>
    ```
    SELECT @@version;
    ```
- <span data-ttu-id="8c0ab-132">Azure Database for MySQL supports only InnoDB tables.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-132">Azure Database for MySQL supports only InnoDB tables.</span></span> <span data-ttu-id="8c0ab-133">To convert MyISAM tables to InnoDB, see the article [Converting Tables from MyISAM to InnoDB](https://dev.mysql.com/doc/refman/5.7/en/converting-tables-to-innodb.html)</span><span class="sxs-lookup"><span data-stu-id="8c0ab-133">To convert MyISAM tables to InnoDB, see the article [Converting Tables from MyISAM to InnoDB](https://dev.mysql.com/doc/refman/5.7/en/converting-tables-to-innodb.html)</span></span> 

- <span data-ttu-id="8c0ab-134">Enable binary logging in the my.ini (Windows) or my.cnf (Unix) file in source database by using the  following configuration:</span><span class="sxs-lookup"><span data-stu-id="8c0ab-134">Enable binary logging in the my.ini (Windows) or my.cnf (Unix) file in source database by using the  following configuration:</span></span>
- <span data-ttu-id="8c0ab-135">The user must have the ReplicationAdmin role with the following privileges:</span><span class="sxs-lookup"><span data-stu-id="8c0ab-135">The user must have the ReplicationAdmin role with the following privileges:</span></span>
    - <span data-ttu-id="8c0ab-136">**REPLICATION CLIENT** - Required for Change Processing tasks only.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-136">**REPLICATION CLIENT** - Required for Change Processing tasks only.</span></span> <span data-ttu-id="8c0ab-137">In other words, Full Load only tasks don't require this privilege.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-137">In other words, Full Load only tasks don't require this privilege.</span></span>
    - <span data-ttu-id="8c0ab-138">**REPLICATION REPLICA** - Required for Change Processing tasks only.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-138">**REPLICATION REPLICA** - Required for Change Processing tasks only.</span></span> <span data-ttu-id="8c0ab-139">In other words, Full Load only tasks don't require this privilege.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-139">In other words, Full Load only tasks don't require this privilege.</span></span>
    - <span data-ttu-id="8c0ab-140">**SUPER** - Only required in versions earlier than MySQL 5.6.6.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-140">**SUPER** - Only required in versions earlier than MySQL 5.6.6.</span></span>

## <a name="migrate-the-sample-schema"></a><span data-ttu-id="8c0ab-141">Migrate the sample schema</span><span class="sxs-lookup"><span data-stu-id="8c0ab-141">Migrate the sample schema</span></span>
<span data-ttu-id="8c0ab-142">To complete all the database objects like table schemas, indexes and stored procedures, we need to extract schema from the source database and apply to the database.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-142">To complete all the database objects like table schemas, indexes and stored procedures, we need to extract schema from the source database and apply to the database.</span></span> <span data-ttu-id="8c0ab-143">To extract schema, you can use mysqldump with - - no-data parameter.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-143">To extract schema, you can use mysqldump with - - no-data parameter.</span></span>
 
<span data-ttu-id="8c0ab-144">Assuming you have MySQL employees sample database in the on-premise system, the command to do schema migration using mysqldump is:</span><span class="sxs-lookup"><span data-stu-id="8c0ab-144">Assuming you have MySQL employees sample database in the on-premise system, the command to do schema migration using mysqldump is:</span></span>
```
mysqldump -h [servername] -u [username] -p[password] --databases [db name] --no-data > [schema file path]
```
<span data-ttu-id="8c0ab-145">For example:</span><span class="sxs-lookup"><span data-stu-id="8c0ab-145">For example:</span></span>
```
mysqldump -h 10.10.123.123 -u root -p --databases employees --no-data > d:\employees.sql
```

<span data-ttu-id="8c0ab-146">To import schema to Azure Database for MySQL target, run the following command:</span><span class="sxs-lookup"><span data-stu-id="8c0ab-146">To import schema to Azure Database for MySQL target, run the following command:</span></span>

```
mysql.exe -h [servername] -u [username] -p[password] [database]< [schema file path]
 ```

<span data-ttu-id="8c0ab-147">For example:</span><span class="sxs-lookup"><span data-stu-id="8c0ab-147">For example:</span></span>
```
mysql.exe -h shausample.mysql.database.azure.com -u dms@shausample -p employees < d:\employees.sql
 ```

<span data-ttu-id="8c0ab-148">If you have foreign keys in your schema, the initial load and continuous sync of the migration will fail.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-148">If you have foreign keys in your schema, the initial load and continuous sync of the migration will fail.</span></span>  <span data-ttu-id="8c0ab-149">Execute the following script in MySQL workbench to extract the drop foreign key script and add foreign key script.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-149">Execute the following script in MySQL workbench to extract the drop foreign key script and add foreign key script.</span></span>
```
SET group_concat_max_len = 8192;
    SELECT SchemaName, GROUP_CONCAT(DropQuery SEPARATOR ';\n') as DropQuery, GROUP_CONCAT(AddQuery SEPARATOR ';\n') as AddQuery
    FROM
    (SELECT 
    KCU.REFERENCED_TABLE_SCHEMA as SchemaName,    
    KCU.TABLE_NAME,
    KCU.COLUMN_NAME,
    CONCAT('ALTER TABLE ', KCU.TABLE_NAME, ' DROP FOREIGN KEY ', KCU.CONSTRAINT_NAME) AS DropQuery,
    CONCAT('ALTER TABLE ', KCU.TABLE_NAME, ' ADD CONSTRAINT ', KCU.CONSTRAINT_NAME, ' FOREIGN KEY (`', KCU.COLUMN_NAME, '`) REFERENCES `', KCU.REFERENCED_TABLE_NAME, '` (`', KCU.REFERENCED_COLUMN_NAME, '`) ON UPDATE ',RC.UPDATE_RULE, ' ON DELETE ',RC.DELETE_RULE) AS AddQuery
    FROM INFORMATION_SCHEMA.KEY_COLUMN_USAGE KCU, information_schema.REFERENTIAL_CONSTRAINTS RC
    WHERE
      KCU.CONSTRAINT_NAME = RC.CONSTRAINT_NAME
      AND KCU.REFERENCED_TABLE_SCHEMA = RC.UNIQUE_CONSTRAINT_SCHEMA
  AND KCU.REFERENCED_TABLE_SCHEMA = 'SchemaName') Queries
  GROUP BY SchemaName;
 ```
        
<span data-ttu-id="8c0ab-150">Run the drop foreign key (which is the second column) in the query result to drop foreign key.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-150">Run the drop foreign key (which is the second column) in the query result to drop foreign key.</span></span>

<span data-ttu-id="8c0ab-151">If you have trigger in the data (insert or update trigger), it will enforce data integrity in the target ahead of the replicated data from the source.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-151">If you have trigger in the data (insert or update trigger), it will enforce data integrity in the target ahead of the replicated data from the source.</span></span> <span data-ttu-id="8c0ab-152">The recommendation is to disable triggers in all the tables at the target during migration, and then enable the triggers after migration is done.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-152">The recommendation is to disable triggers in all the tables at the target during migration, and then enable the triggers after migration is done.</span></span>

<span data-ttu-id="8c0ab-153">To disable triggers in target database, use the following command:</span><span class="sxs-lookup"><span data-stu-id="8c0ab-153">To disable triggers in target database, use the following command:</span></span>
```
SELECT Concat('DROP TRIGGER ', Trigger_Name, ';') FROM  information_schema.TRIGGERS WHERE TRIGGER_SCHEMA = 'your_schema';
```
## <a name="register-the-microsoftdatamigration-resource-provider"></a><span data-ttu-id="8c0ab-154">Register the Microsoft.DataMigration resource provider</span><span class="sxs-lookup"><span data-stu-id="8c0ab-154">Register the Microsoft.DataMigration resource provider</span></span>
1. <span data-ttu-id="8c0ab-155">Sign in to the Azure portal, select **All services**, and then select **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-155">Sign in to the Azure portal, select **All services**, and then select **Subscriptions**.</span></span>
 
   ![Show portal subscriptions](media\tutorial-mysql-to-azure-mysql-online\portal-select-subscriptions.png)
       
2. <span data-ttu-id="8c0ab-157">Select the subscription in which you want to create the instance of the Azure Database Migration Service, and then select **Resource providers**.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-157">Select the subscription in which you want to create the instance of the Azure Database Migration Service, and then select **Resource providers**.</span></span>
 
    ![Show resource providers](media\tutorial-mysql-to-azure-mysql-online\portal-select-resource-provider.png)
    
3.  <span data-ttu-id="8c0ab-159">Search for migration, and then to the right of **Microsoft.DataMigration**, select **Register**.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-159">Search for migration, and then to the right of **Microsoft.DataMigration**, select **Register**.</span></span>
 
    ![Register resource provider](media\tutorial-mysql-to-azure-mysql-online\portal-register-resource-provider.png)    

## <a name="create-a-dms-instance"></a><span data-ttu-id="8c0ab-161">Create a DMS instance</span><span class="sxs-lookup"><span data-stu-id="8c0ab-161">Create a DMS instance</span></span>
1.  <span data-ttu-id="8c0ab-162">In the Azure portal, select + **Create a resource**, search for Azure Database Migration Service, and then select **Azure Database Migration Service** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-162">In the Azure portal, select + **Create a resource**, search for Azure Database Migration Service, and then select **Azure Database Migration Service** from the drop-down list.</span></span>

    ![Azure Marketplace](media\tutorial-mysql-to-azure-mysql-online\portal-marketplace.png)

2.  <span data-ttu-id="8c0ab-164">On the **Azure Database Migration Service** screen, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-164">On the **Azure Database Migration Service** screen, select **Create**.</span></span>
 
    ![Create Azure Database Migration Service instance](media\tutorial-mysql-to-azure-mysql-online\dms-create1.png)
  
3.  <span data-ttu-id="8c0ab-166">On the **Create Migration Service** screen, specify a name for the service, the subscription, and a new or existing resource group.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-166">On the **Create Migration Service** screen, specify a name for the service, the subscription, and a new or existing resource group.</span></span>

4. <span data-ttu-id="8c0ab-167">Select an existing virtual network (VNET) or create a new one.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-167">Select an existing virtual network (VNET) or create a new one.</span></span>

    <span data-ttu-id="8c0ab-168">The VNET provides the Azure Database Migration Service with access to the source SQL Server and the target Azure SQL Database instance.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-168">The VNET provides the Azure Database Migration Service with access to the source SQL Server and the target Azure SQL Database instance.</span></span>

    <span data-ttu-id="8c0ab-169">For more information about how to create a VNET in the Azure portal, see the article [Create a virtual network using the Azure portal](https://aka.ms/DMSVnet).</span><span class="sxs-lookup"><span data-stu-id="8c0ab-169">For more information about how to create a VNET in the Azure portal, see the article [Create a virtual network using the Azure portal](https://aka.ms/DMSVnet).</span></span>

5. <span data-ttu-id="8c0ab-170">Select a pricing tier.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-170">Select a pricing tier.</span></span>

    <span data-ttu-id="8c0ab-171">For more information on costs and pricing tiers, see the [pricing page](https://aka.ms/dms-pricing).</span><span class="sxs-lookup"><span data-stu-id="8c0ab-171">For more information on costs and pricing tiers, see the [pricing page](https://aka.ms/dms-pricing).</span></span>

    <span data-ttu-id="8c0ab-172">If you need help in choosing the right Azure Database Migration Service tier, refer to the recommendations in the blog posting [Choosing an Azure Database Migration Service (Azure DMS) tier](https://go.microsoft.com/fwlink/?linkid=861067).</span><span class="sxs-lookup"><span data-stu-id="8c0ab-172">If you need help in choosing the right Azure Database Migration Service tier, refer to the recommendations in the blog posting [Choosing an Azure Database Migration Service (Azure DMS) tier](https://go.microsoft.com/fwlink/?linkid=861067).</span></span> 

     ![Configure Azure Database Migration Service instance settings](media\tutorial-mysql-to-azure-mysql-online\dms-settings3.png)

7.  <span data-ttu-id="8c0ab-174">Select **Create** to create the service.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-174">Select **Create** to create the service.</span></span>

## <a name="create-a-migration-project"></a><span data-ttu-id="8c0ab-175">Create a migration project</span><span class="sxs-lookup"><span data-stu-id="8c0ab-175">Create a migration project</span></span>
<span data-ttu-id="8c0ab-176">After the service is created, locate it within the Azure portal, open it, and then create a new migration project.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-176">After the service is created, locate it within the Azure portal, open it, and then create a new migration project.</span></span>

1. <span data-ttu-id="8c0ab-177">In the Azure portal, select **All services**, search for Azure Database Migration Service, and then select **Azure Database Migration Services**.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-177">In the Azure portal, select **All services**, search for Azure Database Migration Service, and then select **Azure Database Migration Services**.</span></span>
 
      ![Locate all instances of the Azure Database Migration Service](media\tutorial-mysql-to-azure-mysql-online\dms-search.png)

2. <span data-ttu-id="8c0ab-179">On the **Azure Database Migration Services** screen, search for the name of the Azure Database Migration Service instance that you created, and then select the instance.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-179">On the **Azure Database Migration Services** screen, search for the name of the Azure Database Migration Service instance that you created, and then select the instance.</span></span>
 
     ![Locate your instance of the Azure Database Migration Service](media\tutorial-mysql-to-azure-mysql-online\dms-instance-search.png)
 
3. <span data-ttu-id="8c0ab-181">Select + **New Migration Project**.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-181">Select + **New Migration Project**.</span></span>
4. <span data-ttu-id="8c0ab-182">On the **New migration project** screen, specify a name for the project, in the **Source server type** text box, select **MySQL**, in the **Target server type** text box, select **AzureDbForMySQL**.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-182">On the **New migration project** screen, specify a name for the project, in the **Source server type** text box, select **MySQL**, in the **Target server type** text box, select **AzureDbForMySQL**.</span></span>
5. <span data-ttu-id="8c0ab-183">In the **Choose type of activity** section, select **Online data migration**</span><span class="sxs-lookup"><span data-stu-id="8c0ab-183">In the **Choose type of activity** section, select **Online data migration**</span></span>

    ![Create Database Migration Service Project](media\tutorial-mysql-to-azure-mysql-online\dms-create-project4.png)

    > [!NOTE]
    > <span data-ttu-id="8c0ab-185">Alternately, you can chose **Create project only** to create the migration project now and execute the migration later.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-185">Alternately, you can chose **Create project only** to create the migration project now and execute the migration later.</span></span>

6. <span data-ttu-id="8c0ab-186">Select **Save**, note the requirements to successfully use DMS to migrate data, and then select **Create and run activity**.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-186">Select **Save**, note the requirements to successfully use DMS to migrate data, and then select **Create and run activity**.</span></span>

## <a name="specify-source-details"></a><span data-ttu-id="8c0ab-187">Specify source details</span><span class="sxs-lookup"><span data-stu-id="8c0ab-187">Specify source details</span></span>
1. <span data-ttu-id="8c0ab-188">On the **Add Source Details** screen, specify the connection details for the source MySQL instance.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-188">On the **Add Source Details** screen, specify the connection details for the source MySQL instance.</span></span>
 
    ![Add Source Details screen](media\tutorial-mysql-to-azure-mysql-online\dms-add-source-details.png)   

## <a name="specify-target-details"></a><span data-ttu-id="8c0ab-190">Specify target details</span><span class="sxs-lookup"><span data-stu-id="8c0ab-190">Specify target details</span></span>
1. <span data-ttu-id="8c0ab-191">Select **Save**, and then on the **Target details** screen, specify the connection details for the target Azure Database for MySQL server, which is the pre-provisioned instance of Azure Database for MySQL to which the **Employees** schema was deployed by using mysqldump.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-191">Select **Save**, and then on the **Target details** screen, specify the connection details for the target Azure Database for MySQL server, which is the pre-provisioned instance of Azure Database for MySQL to which the **Employees** schema was deployed by using mysqldump.</span></span>

    ![Target details screen](media\tutorial-mysql-to-azure-mysql-online\dms-add-target-details.png)

2. <span data-ttu-id="8c0ab-193">Select **Save**, and then on the **Map to target databases** screen, map the source and the target database for migration.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-193">Select **Save**, and then on the **Map to target databases** screen, map the source and the target database for migration.</span></span>

    <span data-ttu-id="8c0ab-194">If the target database contains the same database name as the source database, the Azure Database Migration Service selects the target database by default.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-194">If the target database contains the same database name as the source database, the Azure Database Migration Service selects the target database by default.</span></span>

    ![Map to target databases](media\tutorial-mysql-to-azure-mysql-online\dms-map-target-details.png)

3.  <span data-ttu-id="8c0ab-196">Select **Save**, on the **Migration summary** screen, in the **Activity name** text box, specify a name for the migration activity, and then review the summary to ensure that the source and target details match what you previously specified.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-196">Select **Save**, on the **Migration summary** screen, in the **Activity name** text box, specify a name for the migration activity, and then review the summary to ensure that the source and target details match what you previously specified.</span></span>

    ![Migration Summary](media\tutorial-mysql-to-azure-mysql-online\dms-migration-summary.png)

## <a name="run-the-migration"></a><span data-ttu-id="8c0ab-198">Run the migration</span><span class="sxs-lookup"><span data-stu-id="8c0ab-198">Run the migration</span></span>
- <span data-ttu-id="8c0ab-199">Select **Run migration**.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-199">Select **Run migration**.</span></span>

    <span data-ttu-id="8c0ab-200">The migration activity window appears, and the **Status** of the activity is **initializing**.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-200">The migration activity window appears, and the **Status** of the activity is **initializing**.</span></span>

## <a name="monitor-the-migration"></a><span data-ttu-id="8c0ab-201">Monitor the migration</span><span class="sxs-lookup"><span data-stu-id="8c0ab-201">Monitor the migration</span></span>
1. <span data-ttu-id="8c0ab-202">On the migration activity screen, select **Refresh** to update the display until the **Status** of the migration shows as **Complete**.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-202">On the migration activity screen, select **Refresh** to update the display until the **Status** of the migration shows as **Complete**.</span></span>

     ![Activity Status - complete](media\tutorial-mysql-to-azure-mysql-online\dms-activity-completed.png)

2. <span data-ttu-id="8c0ab-204">Under **Database Name**, select specific database to get to the migration status for **Full data load** and **Incremental data sync** operations.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-204">Under **Database Name**, select specific database to get to the migration status for **Full data load** and **Incremental data sync** operations.</span></span>

    <span data-ttu-id="8c0ab-205">Full data load will show the initial load migration status while Incremental data sync will show change data capture (CDC) status.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-205">Full data load will show the initial load migration status while Incremental data sync will show change data capture (CDC) status.</span></span>
   
     ![Activity Status - Full load completed](media\tutorial-mysql-to-azure-mysql-online\dms-activity-full-load-completed.png)

     ![Activity Status - Incremental data sync](media\tutorial-mysql-to-azure-mysql-online\dms-activity-incremental-data-sync.png)

## <a name="perform-migration-cutover"></a><span data-ttu-id="8c0ab-208">Perform migration cutover</span><span class="sxs-lookup"><span data-stu-id="8c0ab-208">Perform migration cutover</span></span>
<span data-ttu-id="8c0ab-209">After the initial Full load is completed, the databases are marked **Ready to cutover**.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-209">After the initial Full load is completed, the databases are marked **Ready to cutover**.</span></span>

1. <span data-ttu-id="8c0ab-210">When you're ready to complete the database migration, select **Start Cutover**.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-210">When you're ready to complete the database migration, select **Start Cutover**.</span></span>

    ![Start cutover](media\tutorial-mysql-to-azure-mysql-online\dms-start-cutover.png)
 
2.  <span data-ttu-id="8c0ab-212">Make sure to stop all the incoming transactions to the source database; wait until the **Pending changes** counter shows **0**.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-212">Make sure to stop all the incoming transactions to the source database; wait until the **Pending changes** counter shows **0**.</span></span>
3.  <span data-ttu-id="8c0ab-213">Select **Confirm**, and the select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-213">Select **Confirm**, and the select **Apply**.</span></span>
4. <span data-ttu-id="8c0ab-214">When the database migration status shows **Completed**, connect your applications to the new target Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="8c0ab-214">When the database migration status shows **Completed**, connect your applications to the new target Azure SQL Database.</span></span>
 
## <a name="next-steps"></a><span data-ttu-id="8c0ab-215">Next steps</span><span class="sxs-lookup"><span data-stu-id="8c0ab-215">Next steps</span></span>
- <span data-ttu-id="8c0ab-216">For information about known issues and limitations when performing online migrations to Azure Database for MySQL, see the article [Known issues and workarounds with Azure Database for MySQL online migrations](known-issues-azure-mysql-online.md).</span><span class="sxs-lookup"><span data-stu-id="8c0ab-216">For information about known issues and limitations when performing online migrations to Azure Database for MySQL, see the article [Known issues and workarounds with Azure Database for MySQL online migrations](known-issues-azure-mysql-online.md).</span></span>
- <span data-ttu-id="8c0ab-217">For information about the Azure Database Migration Service, see the article [What is the Azure Database Migration Service?](https://docs.microsoft.com/azure/dms/dms-overview).</span><span class="sxs-lookup"><span data-stu-id="8c0ab-217">For information about the Azure Database Migration Service, see the article [What is the Azure Database Migration Service?](https://docs.microsoft.com/azure/dms/dms-overview).</span></span>
- <span data-ttu-id="8c0ab-218">For information about the Azure Database for MySQL, see the article [What is the Azure Database for MySQL?](https://docs.microsoft.com/azure/mysql/overview).</span><span class="sxs-lookup"><span data-stu-id="8c0ab-218">For information about the Azure Database for MySQL, see the article [What is the Azure Database for MySQL?](https://docs.microsoft.com/azure/mysql/overview).</span></span>