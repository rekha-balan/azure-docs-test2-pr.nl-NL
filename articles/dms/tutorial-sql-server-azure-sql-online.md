---
title: Use the Azure Database Migration Service to perform an online migration of SQL Server to Azure SQL Database | Microsoft Docs
description: Learn to perform an online migration from SQL Server on-premises to Azure SQL Database by using the Azure Database Migration Service.
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
ms.openlocfilehash: b4cbc7fc7e031fcbd25229792488dbb4002ea23e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866843"
---
# <a name="migrate-sql-server-to-azure-sql-database-online-using-dms"></a><span data-ttu-id="5ce71-103">Migrate SQL Server to Azure SQL Database online using DMS</span><span class="sxs-lookup"><span data-stu-id="5ce71-103">Migrate SQL Server to Azure SQL Database online using DMS</span></span>
<span data-ttu-id="5ce71-104">You can use the Azure Database Migration Service to migrate the databases from an on-premises SQL Server instance to [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/) with minimal downtime.</span><span class="sxs-lookup"><span data-stu-id="5ce71-104">You can use the Azure Database Migration Service to migrate the databases from an on-premises SQL Server instance to [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/) with minimal downtime.</span></span> <span data-ttu-id="5ce71-105">In this tutorial, you migrate the **Adventureworks2012** database restored to an on-premises instance of SQL Server 2016 (or later) to an Azure SQL Database by using the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="5ce71-105">In this tutorial, you migrate the **Adventureworks2012** database restored to an on-premises instance of SQL Server 2016 (or later) to an Azure SQL Database by using the Azure Database Migration Service.</span></span>

<span data-ttu-id="5ce71-106">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="5ce71-106">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="5ce71-107">Assess your on-premises database by using the Data Migration Assistant.</span><span class="sxs-lookup"><span data-stu-id="5ce71-107">Assess your on-premises database by using the Data Migration Assistant.</span></span>
> * <span data-ttu-id="5ce71-108">Migrate the sample schema by using the Data Migration Assistant.</span><span class="sxs-lookup"><span data-stu-id="5ce71-108">Migrate the sample schema by using the Data Migration Assistant.</span></span>
> * <span data-ttu-id="5ce71-109">Create an instance of the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="5ce71-109">Create an instance of the Azure Database Migration Service.</span></span>
> * <span data-ttu-id="5ce71-110">Create a migration project by using the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="5ce71-110">Create a migration project by using the Azure Database Migration Service.</span></span>
> * <span data-ttu-id="5ce71-111">Run the migration.</span><span class="sxs-lookup"><span data-stu-id="5ce71-111">Run the migration.</span></span>
> * <span data-ttu-id="5ce71-112">Monitor the migration.</span><span class="sxs-lookup"><span data-stu-id="5ce71-112">Monitor the migration.</span></span>
> * <span data-ttu-id="5ce71-113">Download a migration report.</span><span class="sxs-lookup"><span data-stu-id="5ce71-113">Download a migration report.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ce71-114">For an optimal migration experience, Microsoft recommends creating an instance of the Azure Database Migration Service in the same Azure region as the target database.</span><span class="sxs-lookup"><span data-stu-id="5ce71-114">For an optimal migration experience, Microsoft recommends creating an instance of the Azure Database Migration Service in the same Azure region as the target database.</span></span> <span data-ttu-id="5ce71-115">Moving data across regions or geographies can slow down the migration process and introduce errors.</span><span class="sxs-lookup"><span data-stu-id="5ce71-115">Moving data across regions or geographies can slow down the migration process and introduce errors.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ce71-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5ce71-116">Prerequisites</span></span>
<span data-ttu-id="5ce71-117">To complete this tutorial, you need to:</span><span class="sxs-lookup"><span data-stu-id="5ce71-117">To complete this tutorial, you need to:</span></span>

- <span data-ttu-id="5ce71-118">Download and install [SQL Server 2012 or later](https://www.microsoft.com/sql-server/sql-server-downloads) (any edition).</span><span class="sxs-lookup"><span data-stu-id="5ce71-118">Download and install [SQL Server 2012 or later](https://www.microsoft.com/sql-server/sql-server-downloads) (any edition).</span></span>
- <span data-ttu-id="5ce71-119">Enable the TCP/IP protocol, which is disabled by default during SQL Server Express installation, by following the instructions in the article [Enable or Disable a Server Network Protocol](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-or-disable-a-server-network-protocol#SSMSProcedure).</span><span class="sxs-lookup"><span data-stu-id="5ce71-119">Enable the TCP/IP protocol, which is disabled by default during SQL Server Express installation, by following the instructions in the article [Enable or Disable a Server Network Protocol](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-or-disable-a-server-network-protocol#SSMSProcedure).</span></span>
- <span data-ttu-id="5ce71-120">Create an instance of Azure SQL Database instance, which you do by following the detail in the article [Create an Azure SQL database in the Azure portal](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="5ce71-120">Create an instance of Azure SQL Database instance, which you do by following the detail in the article [Create an Azure SQL database in the Azure portal](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal).</span></span>
- <span data-ttu-id="5ce71-121">Download and install the [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA) v3.3 or later.</span><span class="sxs-lookup"><span data-stu-id="5ce71-121">Download and install the [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA) v3.3 or later.</span></span>
- <span data-ttu-id="5ce71-122">Create a VNET for the Azure Database Migration Service by using the Azure Resource Manager deployment model, which provides site-to-site connectivity to your on-premises source servers by using either [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) or [VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).</span><span class="sxs-lookup"><span data-stu-id="5ce71-122">Create a VNET for the Azure Database Migration Service by using the Azure Resource Manager deployment model, which provides site-to-site connectivity to your on-premises source servers by using either [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) or [VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).</span></span>
- <span data-ttu-id="5ce71-123">Ensure that your Azure Virtual Network (VNET) Network Security Group rules don't block the following communication ports 443, 53, 9354, 445, 12000.</span><span class="sxs-lookup"><span data-stu-id="5ce71-123">Ensure that your Azure Virtual Network (VNET) Network Security Group rules don't block the following communication ports 443, 53, 9354, 445, 12000.</span></span> <span data-ttu-id="5ce71-124">For more detail on Azure VNET NSG traffic filtering, see the article [Filter network traffic with network security groups](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg).</span><span class="sxs-lookup"><span data-stu-id="5ce71-124">For more detail on Azure VNET NSG traffic filtering, see the article [Filter network traffic with network security groups](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg).</span></span>
- <span data-ttu-id="5ce71-125">Configure your [Windows Firewall for database engine access](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access).</span><span class="sxs-lookup"><span data-stu-id="5ce71-125">Configure your [Windows Firewall for database engine access](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access).</span></span>
- <span data-ttu-id="5ce71-126">Open your Windows firewall to allow the Azure Database Migration Service to access the source SQL Server, which by default is TCP port 1433.</span><span class="sxs-lookup"><span data-stu-id="5ce71-126">Open your Windows firewall to allow the Azure Database Migration Service to access the source SQL Server, which by default is TCP port 1433.</span></span>
- <span data-ttu-id="5ce71-127">If you're running multiple named SQL Server instances using dynamic ports, you may wish to enable the SQL Browser Service and allow access to UDP port 1434 through your firewalls so that the Azure Database Migration Service can connect to a named instance on your source server.</span><span class="sxs-lookup"><span data-stu-id="5ce71-127">If you're running multiple named SQL Server instances using dynamic ports, you may wish to enable the SQL Browser Service and allow access to UDP port 1434 through your firewalls so that the Azure Database Migration Service can connect to a named instance on your source server.</span></span>
- <span data-ttu-id="5ce71-128">When using a firewall appliance in front of your source database(s), you may need to add firewall rules to allow the Azure Database Migration Service to access the source database(s) for migration.</span><span class="sxs-lookup"><span data-stu-id="5ce71-128">When using a firewall appliance in front of your source database(s), you may need to add firewall rules to allow the Azure Database Migration Service to access the source database(s) for migration.</span></span>
- <span data-ttu-id="5ce71-129">Create a server-level [firewall rule](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) for the Azure SQL Database server to allow the Azure Database Migration Service access to the target databases.</span><span class="sxs-lookup"><span data-stu-id="5ce71-129">Create a server-level [firewall rule](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) for the Azure SQL Database server to allow the Azure Database Migration Service access to the target databases.</span></span> <span data-ttu-id="5ce71-130">Provide the subnet range of the VNET used for the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="5ce71-130">Provide the subnet range of the VNET used for the Azure Database Migration Service.</span></span>
- <span data-ttu-id="5ce71-131">Ensure that the credentials used to connect to source SQL Server instance have [CONTROL SERVER](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql) permissions.</span><span class="sxs-lookup"><span data-stu-id="5ce71-131">Ensure that the credentials used to connect to source SQL Server instance have [CONTROL SERVER](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql) permissions.</span></span>
- <span data-ttu-id="5ce71-132">Ensure that the credentials used to connect to target Azure SQL Database instance have CONTROL DATABASE permission on the target Azure SQL databases.</span><span class="sxs-lookup"><span data-stu-id="5ce71-132">Ensure that the credentials used to connect to target Azure SQL Database instance have CONTROL DATABASE permission on the target Azure SQL databases.</span></span>
- <span data-ttu-id="5ce71-133">The source SQL Server version must be SQL Server 2005 and above.</span><span class="sxs-lookup"><span data-stu-id="5ce71-133">The source SQL Server version must be SQL Server 2005 and above.</span></span> <span data-ttu-id="5ce71-134">To determine the version that you SQL Server instance is running, see the article [How to determine the version, edition, and update level of SQL Server and its components](https://support.microsoft.com/help/321185/how-to-determine-the-version-edition-and-update-level-of-sql-server-an).</span><span class="sxs-lookup"><span data-stu-id="5ce71-134">To determine the version that you SQL Server instance is running, see the article [How to determine the version, edition, and update level of SQL Server and its components](https://support.microsoft.com/help/321185/how-to-determine-the-version-edition-and-update-level-of-sql-server-an).</span></span>
- <span data-ttu-id="5ce71-135">Database(s) must be in either Bulk-logged or Full recovery mode.</span><span class="sxs-lookup"><span data-stu-id="5ce71-135">Database(s) must be in either Bulk-logged or Full recovery mode.</span></span> <span data-ttu-id="5ce71-136">To determine the recovery model configured for your SQL Server instance, see the article [View or Change the Recovery Model of a Database (SQL Server)](https://docs.microsoft.com/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server?view=sql-server-2017).</span><span class="sxs-lookup"><span data-stu-id="5ce71-136">To determine the recovery model configured for your SQL Server instance, see the article [View or Change the Recovery Model of a Database (SQL Server)](https://docs.microsoft.com/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server?view=sql-server-2017).</span></span>
- <span data-ttu-id="5ce71-137">Make sure to take the Full database backups for the databases.</span><span class="sxs-lookup"><span data-stu-id="5ce71-137">Make sure to take the Full database backups for the databases.</span></span> <span data-ttu-id="5ce71-138">To create a Full database backup, see the article [How to: Create a Full Database Backup (Transact-SQL)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms191304(v=sql.105)).</span><span class="sxs-lookup"><span data-stu-id="5ce71-138">To create a Full database backup, see the article [How to: Create a Full Database Backup (Transact-SQL)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms191304(v=sql.105)).</span></span>
- <span data-ttu-id="5ce71-139">If any of the tables don't have a primary key, enable Change Data Capture (CDC) on the database and specific table(s).</span><span class="sxs-lookup"><span data-stu-id="5ce71-139">If any of the tables don't have a primary key, enable Change Data Capture (CDC) on the database and specific table(s).</span></span>
    > [!NOTE]
    > <span data-ttu-id="5ce71-140">You can use the script below to find any tables that do not have primary keys.</span><span class="sxs-lookup"><span data-stu-id="5ce71-140">You can use the script below to find any tables that do not have primary keys.</span></span>
    ```
    USE <DBName>;
    go
    SELECT is_tracked_by_cdc, name AS TableName
    FROM sys.tables WHERE type = 'U' and is_ms_shipped = 0 AND
    OBJECTPROPERTY(OBJECT_ID, 'TableHasPrimaryKey') = 0;
     ```
    ><span data-ttu-id="5ce71-141">If the results show one or more tables with 'is_tracked_by_cdc' as '0', enable change capture for the database and for the specific tables by using the process described in the article [Enable and Disable Change Data Capture (SQL Server)](https://docs.microsoft.com/sql/relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server?view=sql-server-2017).</span><span class="sxs-lookup"><span data-stu-id="5ce71-141">If the results show one or more tables with 'is_tracked_by_cdc' as '0', enable change capture for the database and for the specific tables by using the process described in the article [Enable and Disable Change Data Capture (SQL Server)](https://docs.microsoft.com/sql/relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server?view=sql-server-2017).</span></span>

- <span data-ttu-id="5ce71-142">Configure the distributor role for source SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5ce71-142">Configure the distributor role for source SQL Server.</span></span>

    >[!NOTE]
    > <span data-ttu-id="5ce71-143">You can determine if replication components are installed by using the query below.</span><span class="sxs-lookup"><span data-stu-id="5ce71-143">You can determine if replication components are installed by using the query below.</span></span>
    ```
    USE master;
    DECLARE @installed int;
    EXEC @installed = sys.sp_MS_replication_installed;
    SELECT @installed as installed;
    ```
    <span data-ttu-id="5ce71-144">If the result returns an error message suggesting to install replication components, install SQL Server replication components by using the process in the article [Install SQL Server replication](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-replication?view=sql-server-2017).</span><span class="sxs-lookup"><span data-stu-id="5ce71-144">If the result returns an error message suggesting to install replication components, install SQL Server replication components by using the process in the article [Install SQL Server replication](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-replication?view=sql-server-2017).</span></span>

    <span data-ttu-id="5ce71-145">If the replication is already installed, check if the distribution role is configured on the source SQL Server using the T-SQL command below.</span><span class="sxs-lookup"><span data-stu-id="5ce71-145">If the replication is already installed, check if the distribution role is configured on the source SQL Server using the T-SQL command below.</span></span>
    ```
    EXEC sp_get_distributor;
    ```

    <span data-ttu-id="5ce71-146">If the distribution isn't set up, where the distribution server shows NULL for above command output, configure the distribution using the guidance provided in the article [Configure Distribution](https://docs.microsoft.com/sql/relational-databases/replication/configure-publishing-and-distribution?view=sql-server-2017).</span><span class="sxs-lookup"><span data-stu-id="5ce71-146">If the distribution isn't set up, where the distribution server shows NULL for above command output, configure the distribution using the guidance provided in the article [Configure Distribution](https://docs.microsoft.com/sql/relational-databases/replication/configure-publishing-and-distribution?view=sql-server-2017).</span></span>

- <span data-ttu-id="5ce71-147">Disable database triggers on the target Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="5ce71-147">Disable database triggers on the target Azure SQL Database.</span></span>
    >[!NOTE]
    > <span data-ttu-id="5ce71-148">You can find the database triggers on the target Azure SQL Database by using the following query:</span><span class="sxs-lookup"><span data-stu-id="5ce71-148">You can find the database triggers on the target Azure SQL Database by using the following query:</span></span>
    ```
    Use <Database name>
    select * from sys.triggers
    DISABLE TRIGGER (Transact-SQL)
    ```
    <span data-ttu-id="5ce71-149">For more information, see the article [DISABLE TRIGGER (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/disable-trigger-transact-sql?view=sql-server-2017).</span><span class="sxs-lookup"><span data-stu-id="5ce71-149">For more information, see the article [DISABLE TRIGGER (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/disable-trigger-transact-sql?view=sql-server-2017).</span></span> 

## <a name="assess-your-on-premises-database"></a><span data-ttu-id="5ce71-150">Assess your on-premises database</span><span class="sxs-lookup"><span data-stu-id="5ce71-150">Assess your on-premises database</span></span>
<span data-ttu-id="5ce71-151">Before you can migrate data from an on-premises SQL Server instance to Azure SQL Database, you need to assess the SQL Server database for any blocking issues that might prevent migration.</span><span class="sxs-lookup"><span data-stu-id="5ce71-151">Before you can migrate data from an on-premises SQL Server instance to Azure SQL Database, you need to assess the SQL Server database for any blocking issues that might prevent migration.</span></span> <span data-ttu-id="5ce71-152">Using the Data Migration Assistant v3.3 or later, follow the steps described in the article [Performing a SQL Server migration assessment](https://docs.microsoft.com/sql/dma/dma-assesssqlonprem) to complete the on-premises database assessment.</span><span class="sxs-lookup"><span data-stu-id="5ce71-152">Using the Data Migration Assistant v3.3 or later, follow the steps described in the article [Performing a SQL Server migration assessment](https://docs.microsoft.com/sql/dma/dma-assesssqlonprem) to complete the on-premises database assessment.</span></span>

<span data-ttu-id="5ce71-153">To assess am on-premises database, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5ce71-153">To assess am on-premises database, perform the following steps:</span></span>
1.  <span data-ttu-id="5ce71-154">In DMA, select the New (+) icon, and then select the **Assessment**  project type.</span><span class="sxs-lookup"><span data-stu-id="5ce71-154">In DMA, select the New (+) icon, and then select the **Assessment**  project type.</span></span>
2.  <span data-ttu-id="5ce71-155">Specify a project name, in the **Source server type** text box, select **SQL Server**, in the **Target server type** text box, select **Azure SQL Database**, and then select **Create** to create the project.</span><span class="sxs-lookup"><span data-stu-id="5ce71-155">Specify a project name, in the **Source server type** text box, select **SQL Server**, in the **Target server type** text box, select **Azure SQL Database**, and then select **Create** to create the project.</span></span>

    <span data-ttu-id="5ce71-156">When you're assessing the source SQL Server database migrating to Azure SQL Database, you can choose one or both of the following assessment report types:</span><span class="sxs-lookup"><span data-stu-id="5ce71-156">When you're assessing the source SQL Server database migrating to Azure SQL Database, you can choose one or both of the following assessment report types:</span></span>
    - <span data-ttu-id="5ce71-157">Check database compatibility</span><span class="sxs-lookup"><span data-stu-id="5ce71-157">Check database compatibility</span></span>
    - <span data-ttu-id="5ce71-158">Check feature parity</span><span class="sxs-lookup"><span data-stu-id="5ce71-158">Check feature parity</span></span>

    <span data-ttu-id="5ce71-159">Both report types are selected by default.</span><span class="sxs-lookup"><span data-stu-id="5ce71-159">Both report types are selected by default.</span></span>

3.  <span data-ttu-id="5ce71-160">In DMA, on the **Options** screen, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="5ce71-160">In DMA, on the **Options** screen, select **Next**.</span></span>
4.  <span data-ttu-id="5ce71-161">On the **Select sources** screen, in the **Connect to a server** dialog box, provide the connection details to your SQL Server, and then select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="5ce71-161">On the **Select sources** screen, in the **Connect to a server** dialog box, provide the connection details to your SQL Server, and then select **Connect**.</span></span>
5.  <span data-ttu-id="5ce71-162">In the **Add sources** dialog box, select **AdventureWorks2012**, select **Add**, and then select **Start Assessment**.</span><span class="sxs-lookup"><span data-stu-id="5ce71-162">In the **Add sources** dialog box, select **AdventureWorks2012**, select **Add**, and then select **Start Assessment**.</span></span>

    <span data-ttu-id="5ce71-163">When the assessment is complete, the results display as shown in the following graphic:</span><span class="sxs-lookup"><span data-stu-id="5ce71-163">When the assessment is complete, the results display as shown in the following graphic:</span></span>

    ![Assess data migration](media\tutorial-sql-server-to-azure-sql-online\dma-assessments.png)

    <span data-ttu-id="5ce71-165">For Azure SQL Database, the assessments identify feature parity issues and migration blocking issues.</span><span class="sxs-lookup"><span data-stu-id="5ce71-165">For Azure SQL Database, the assessments identify feature parity issues and migration blocking issues.</span></span>

    - <span data-ttu-id="5ce71-166">The **SQL Server feature parity** category provides a comprehensive set of recommendations, alternative approaches available in Azure, and mitigating steps to help you plan the effort into your migration projects.</span><span class="sxs-lookup"><span data-stu-id="5ce71-166">The **SQL Server feature parity** category provides a comprehensive set of recommendations, alternative approaches available in Azure, and mitigating steps to help you plan the effort into your migration projects.</span></span>
    - <span data-ttu-id="5ce71-167">The **Compatibility issues** category identifies partially supported or unsupported features that reflect compatibility issues that might block migrating on-premises SQL Server database(s) to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="5ce71-167">The **Compatibility issues** category identifies partially supported or unsupported features that reflect compatibility issues that might block migrating on-premises SQL Server database(s) to Azure SQL Database.</span></span> <span data-ttu-id="5ce71-168">Recommendations are also provided to help you address those issues.</span><span class="sxs-lookup"><span data-stu-id="5ce71-168">Recommendations are also provided to help you address those issues.</span></span>

6.  <span data-ttu-id="5ce71-169">Review the assessment results for migration blocking issues and feature parity issues by selecting the specific options.</span><span class="sxs-lookup"><span data-stu-id="5ce71-169">Review the assessment results for migration blocking issues and feature parity issues by selecting the specific options.</span></span>

## <a name="migrate-the-sample-schema"></a><span data-ttu-id="5ce71-170">Migrate the sample schema</span><span class="sxs-lookup"><span data-stu-id="5ce71-170">Migrate the sample schema</span></span>
<span data-ttu-id="5ce71-171">After you're comfortable with the assessment and satisfied that the selected database is a viable candidate for migration to Azure SQL Database, use DMA to migrate the schema to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="5ce71-171">After you're comfortable with the assessment and satisfied that the selected database is a viable candidate for migration to Azure SQL Database, use DMA to migrate the schema to Azure SQL Database.</span></span>

> [!NOTE]
> <span data-ttu-id="5ce71-172">Before you create a migration project in DMA, be sure that you have already provisioned an Azure SQL database as mentioned in the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="5ce71-172">Before you create a migration project in DMA, be sure that you have already provisioned an Azure SQL database as mentioned in the prerequisites.</span></span> <span data-ttu-id="5ce71-173">For purposes of this tutorial, the name of the Azure SQL Database is assumed to be **AdventureWorksAzure**, but you can provide whatever name you wish.</span><span class="sxs-lookup"><span data-stu-id="5ce71-173">For purposes of this tutorial, the name of the Azure SQL Database is assumed to be **AdventureWorksAzure**, but you can provide whatever name you wish.</span></span>

<span data-ttu-id="5ce71-174">To migrate the **AdventureWorks2012** schema to Azure SQL Database, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5ce71-174">To migrate the **AdventureWorks2012** schema to Azure SQL Database, perform the following steps:</span></span>

1.  <span data-ttu-id="5ce71-175">In the Data Migration Assistant, select the New (+) icon, and then under **Project type**, select **Migration**.</span><span class="sxs-lookup"><span data-stu-id="5ce71-175">In the Data Migration Assistant, select the New (+) icon, and then under **Project type**, select **Migration**.</span></span>
2.  <span data-ttu-id="5ce71-176">Specify a project name, in the **Source server type** text box, select **SQL Server**, and then in the **Target server type** text box, select **Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="5ce71-176">Specify a project name, in the **Source server type** text box, select **SQL Server**, and then in the **Target server type** text box, select **Azure SQL Database**.</span></span>
3.  <span data-ttu-id="5ce71-177">Under **Migration Scope**, select **Schema only**.</span><span class="sxs-lookup"><span data-stu-id="5ce71-177">Under **Migration Scope**, select **Schema only**.</span></span>

    <span data-ttu-id="5ce71-178">After performing the previous steps, the DMA interface should appear as shown in the following graphic:</span><span class="sxs-lookup"><span data-stu-id="5ce71-178">After performing the previous steps, the DMA interface should appear as shown in the following graphic:</span></span>
    
    ![Create Data Migration Assistant Project](media\tutorial-sql-server-to-azure-sql-online\dma-create-project.png)

4.  <span data-ttu-id="5ce71-180">Select **Create** to create the project.</span><span class="sxs-lookup"><span data-stu-id="5ce71-180">Select **Create** to create the project.</span></span>
5.  <span data-ttu-id="5ce71-181">In DMA, specify the source connection details for your SQL Server, select **Connect**, and then select the **AdventureWorks2012** database.</span><span class="sxs-lookup"><span data-stu-id="5ce71-181">In DMA, specify the source connection details for your SQL Server, select **Connect**, and then select the **AdventureWorks2012** database.</span></span>

    ![Data Migration Assistant Source Connection Details](media\tutorial-sql-server-to-azure-sql-online\dma-source-connect.png)

6.  <span data-ttu-id="5ce71-183">Select **Next**, under **Connect to target server**, specify the target connection details for the Azure SQL database, select **Connect**, and then select the **AdventureWorksAzure** database you had pre-provisioned in Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="5ce71-183">Select **Next**, under **Connect to target server**, specify the target connection details for the Azure SQL database, select **Connect**, and then select the **AdventureWorksAzure** database you had pre-provisioned in Azure SQL Database.</span></span>

    ![Data Migration Assistant Target Connection Details](media\tutorial-sql-server-to-azure-sql-online\dma-target-connect.png)

7.  <span data-ttu-id="5ce71-185">Select **Next** to advance to the **Select objects** screen, on which you can specify the schema objects in the **AdventureWorks2012** database that need to be deployed to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="5ce71-185">Select **Next** to advance to the **Select objects** screen, on which you can specify the schema objects in the **AdventureWorks2012** database that need to be deployed to Azure SQL Database.</span></span>

    <span data-ttu-id="5ce71-186">By default, all objects are selected.</span><span class="sxs-lookup"><span data-stu-id="5ce71-186">By default, all objects are selected.</span></span>

    ![Generate SQL Scripts](media\tutorial-sql-server-to-azure-sql-online\dma-assessment-source.png)

8.  <span data-ttu-id="5ce71-188">Select **Generate SQL script** to create the SQL scripts, and then review the scripts for any errors.</span><span class="sxs-lookup"><span data-stu-id="5ce71-188">Select **Generate SQL script** to create the SQL scripts, and then review the scripts for any errors.</span></span>

    ![Schema Script](media\tutorial-sql-server-to-azure-sql-online\dma-schema-script.png)

9.  <span data-ttu-id="5ce71-190">Select **Deploy schema** to deploy the schema to Azure SQL Database, and then after the schema is deployed, check the target server for any anomalies.</span><span class="sxs-lookup"><span data-stu-id="5ce71-190">Select **Deploy schema** to deploy the schema to Azure SQL Database, and then after the schema is deployed, check the target server for any anomalies.</span></span>

    ![Deploy Schema](media\tutorial-sql-server-to-azure-sql-online\dma-schema-deploy.png)

## <a name="register-the-microsoftdatamigration-resource-provider"></a><span data-ttu-id="5ce71-192">Register the Microsoft.DataMigration resource provider</span><span class="sxs-lookup"><span data-stu-id="5ce71-192">Register the Microsoft.DataMigration resource provider</span></span>
1. <span data-ttu-id="5ce71-193">Sign in to the Azure portal, select **All services**, and then select **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="5ce71-193">Sign in to the Azure portal, select **All services**, and then select **Subscriptions**.</span></span>
 
   ![Show portal subscriptions](media\tutorial-sql-server-to-azure-sql-online\portal-select-subscription1.png)
       
2. <span data-ttu-id="5ce71-195">Select the subscription in which you want to create the instance of the Azure Database Migration Service, and then select **Resource providers**.</span><span class="sxs-lookup"><span data-stu-id="5ce71-195">Select the subscription in which you want to create the instance of the Azure Database Migration Service, and then select **Resource providers**.</span></span>
 
    ![Show resource providers](media\tutorial-sql-server-to-azure-sql-online\portal-select-resource-provider.png)
    
3.  <span data-ttu-id="5ce71-197">Search for migration, and then to the right of **Microsoft.DataMigration**, select **Register**.</span><span class="sxs-lookup"><span data-stu-id="5ce71-197">Search for migration, and then to the right of **Microsoft.DataMigration**, select **Register**.</span></span>
 
    ![Register resource provider](media\tutorial-sql-server-to-azure-sql-online\portal-register-resource-provider.png)    

## <a name="create-an-instance"></a><span data-ttu-id="5ce71-199">Create an instance</span><span class="sxs-lookup"><span data-stu-id="5ce71-199">Create an instance</span></span>
1.  <span data-ttu-id="5ce71-200">In the Azure portal, select + **Create a resource**, search for Azure Database Migration Service, and then select **Azure Database Migration Service** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="5ce71-200">In the Azure portal, select + **Create a resource**, search for Azure Database Migration Service, and then select **Azure Database Migration Service** from the drop-down list.</span></span>

    ![Azure Marketplace](media\tutorial-sql-server-to-azure-sql-online\portal-marketplace.png)

2.  <span data-ttu-id="5ce71-202">On the **Azure Database Migration Service** screen, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="5ce71-202">On the **Azure Database Migration Service** screen, select **Create**.</span></span>
 
    ![Create Azure Database Migration Service instance](media\tutorial-sql-server-to-azure-sql-online\dms-create1.png)
  
3.  <span data-ttu-id="5ce71-204">On the **Create Migration Service** screen, specify a name for the service, the subscription, and a new or existing resource group.</span><span class="sxs-lookup"><span data-stu-id="5ce71-204">On the **Create Migration Service** screen, specify a name for the service, the subscription, and a new or existing resource group.</span></span>

4. <span data-ttu-id="5ce71-205">Select the location in which you want to create the instance of the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="5ce71-205">Select the location in which you want to create the instance of the Azure Database Migration Service.</span></span> 

5. <span data-ttu-id="5ce71-206">Select an existing virtual network (VNET) or create a new one.</span><span class="sxs-lookup"><span data-stu-id="5ce71-206">Select an existing virtual network (VNET) or create a new one.</span></span>

    <span data-ttu-id="5ce71-207">The VNET provides the Azure Database Migration Service with access to the source SQL Server and the target Azure SQL Database instance.</span><span class="sxs-lookup"><span data-stu-id="5ce71-207">The VNET provides the Azure Database Migration Service with access to the source SQL Server and the target Azure SQL Database instance.</span></span>

    <span data-ttu-id="5ce71-208">For more information about how to create a VNET in the Azure portal, see the article [Create a virtual network using the Azure portal](https://aka.ms/DMSVnet).</span><span class="sxs-lookup"><span data-stu-id="5ce71-208">For more information about how to create a VNET in the Azure portal, see the article [Create a virtual network using the Azure portal](https://aka.ms/DMSVnet).</span></span>

6. <span data-ttu-id="5ce71-209">Select a pricing tier.</span><span class="sxs-lookup"><span data-stu-id="5ce71-209">Select a pricing tier.</span></span>

    <span data-ttu-id="5ce71-210">For more information on costs and pricing tiers, see the [pricing page](https://aka.ms/dms-pricing).</span><span class="sxs-lookup"><span data-stu-id="5ce71-210">For more information on costs and pricing tiers, see the [pricing page](https://aka.ms/dms-pricing).</span></span>

    <span data-ttu-id="5ce71-211">If you need help in choosing the right Azure Database Migration Service tier, refer to the recommendations in the posting [here](https://go.microsoft.com/fwlink/?linkid=861067).</span><span class="sxs-lookup"><span data-stu-id="5ce71-211">If you need help in choosing the right Azure Database Migration Service tier, refer to the recommendations in the posting [here](https://go.microsoft.com/fwlink/?linkid=861067).</span></span>  

     ![Configure Azure Database Migration Service instance settings](media\tutorial-sql-server-to-azure-sql-online\dms-settings2.png)

7.  <span data-ttu-id="5ce71-213">Select **Create** to create the service.</span><span class="sxs-lookup"><span data-stu-id="5ce71-213">Select **Create** to create the service.</span></span>

## <a name="create-a-migration-project"></a><span data-ttu-id="5ce71-214">Create a migration project</span><span class="sxs-lookup"><span data-stu-id="5ce71-214">Create a migration project</span></span>
<span data-ttu-id="5ce71-215">After the service is created, locate it within the Azure portal, open it, and then create a new migration project.</span><span class="sxs-lookup"><span data-stu-id="5ce71-215">After the service is created, locate it within the Azure portal, open it, and then create a new migration project.</span></span>

1. <span data-ttu-id="5ce71-216">In the Azure portal, select **All services**, search for Azure Database Migration Service, and then select **Azure Database Migration Services**.</span><span class="sxs-lookup"><span data-stu-id="5ce71-216">In the Azure portal, select **All services**, search for Azure Database Migration Service, and then select **Azure Database Migration Services**.</span></span>
 
      ![Locate all instances of the Azure Database Migration Service](media\tutorial-sql-server-to-azure-sql-online\dms-search.png)

2. <span data-ttu-id="5ce71-218">On the **Azure Database Migration Services** screen, search for the name of the Azure Database Migration Service instance that you created, and then select the instance.</span><span class="sxs-lookup"><span data-stu-id="5ce71-218">On the **Azure Database Migration Services** screen, search for the name of the Azure Database Migration Service instance that you created, and then select the instance.</span></span>
 
     ![Locate your instance of the Azure Database Migration Service](media\tutorial-sql-server-to-azure-sql-online\dms-instance-search.png)
 
3. <span data-ttu-id="5ce71-220">Select + **New Migration Project**.</span><span class="sxs-lookup"><span data-stu-id="5ce71-220">Select + **New Migration Project**.</span></span>
4. <span data-ttu-id="5ce71-221">On the **New migration project** screen, specify a name for the project, in the **Source server type** text box, select **SQL Server**, in the **Target server type** text box, select **Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="5ce71-221">On the **New migration project** screen, specify a name for the project, in the **Source server type** text box, select **SQL Server**, in the **Target server type** text box, select **Azure SQL Database**.</span></span>
5. <span data-ttu-id="5ce71-222">In the **Choose type of activity** section, select **Online data migration**</span><span class="sxs-lookup"><span data-stu-id="5ce71-222">In the **Choose type of activity** section, select **Online data migration**</span></span>

    ![Create Database Migration Service Project](media\tutorial-sql-server-to-azure-sql-online\dms-create-project3.png)

    > [!NOTE]
    > <span data-ttu-id="5ce71-224">Alternately, you can chose **Create project only** to create the migration project now and execute the migration later.</span><span class="sxs-lookup"><span data-stu-id="5ce71-224">Alternately, you can chose **Create project only** to create the migration project now and execute the migration later.</span></span>

6. <span data-ttu-id="5ce71-225">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="5ce71-225">Select **Save**.</span></span>

7. <span data-ttu-id="5ce71-226">Select **Create and run activity** to create the project and run the migration activity.</span><span class="sxs-lookup"><span data-stu-id="5ce71-226">Select **Create and run activity** to create the project and run the migration activity.</span></span>

    ![Create and Run Database Migration Service Activity](media\tutorial-sql-server-to-azure-sql-online\dms-create-and-run-activity.png)
 
## <a name="specify-source-details"></a><span data-ttu-id="5ce71-228">Specify source details</span><span class="sxs-lookup"><span data-stu-id="5ce71-228">Specify source details</span></span>
1. <span data-ttu-id="5ce71-229">On the **Migration source detail** screen, specify the connection details for the source SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="5ce71-229">On the **Migration source detail** screen, specify the connection details for the source SQL Server instance.</span></span>
 
    <span data-ttu-id="5ce71-230">Make sure to use a Fully Qualified Domain Name (FQDN) for the source SQL Server instance name.</span><span class="sxs-lookup"><span data-stu-id="5ce71-230">Make sure to use a Fully Qualified Domain Name (FQDN) for the source SQL Server instance name.</span></span> <span data-ttu-id="5ce71-231">You can also use the IP Address for situations in which DNS name resolution isn't possible.</span><span class="sxs-lookup"><span data-stu-id="5ce71-231">You can also use the IP Address for situations in which DNS name resolution isn't possible.</span></span>

2. <span data-ttu-id="5ce71-232">If you haven't installed a trusted certificate on your source server, select the **Trust server certificate** check box.</span><span class="sxs-lookup"><span data-stu-id="5ce71-232">If you haven't installed a trusted certificate on your source server, select the **Trust server certificate** check box.</span></span>

    <span data-ttu-id="5ce71-233">When a trusted certificate isn't installed, SQL Server generates a self-signed certificate when the instance is started.</span><span class="sxs-lookup"><span data-stu-id="5ce71-233">When a trusted certificate isn't installed, SQL Server generates a self-signed certificate when the instance is started.</span></span> <span data-ttu-id="5ce71-234">This certificate is used to encrypt the credentials for client connections.</span><span class="sxs-lookup"><span data-stu-id="5ce71-234">This certificate is used to encrypt the credentials for client connections.</span></span>

    > [!CAUTION]
    > <span data-ttu-id="5ce71-235">SSL connections that are encrypted using a self-signed certificate do not provide strong security.</span><span class="sxs-lookup"><span data-stu-id="5ce71-235">SSL connections that are encrypted using a self-signed certificate do not provide strong security.</span></span> <span data-ttu-id="5ce71-236">They are susceptible to man-in-the-middle attacks.</span><span class="sxs-lookup"><span data-stu-id="5ce71-236">They are susceptible to man-in-the-middle attacks.</span></span> <span data-ttu-id="5ce71-237">You should not rely on SSL using self-signed certificates in a production environment or on servers that are connected to the internet.</span><span class="sxs-lookup"><span data-stu-id="5ce71-237">You should not rely on SSL using self-signed certificates in a production environment or on servers that are connected to the internet.</span></span>

   ![Source Details](media\tutorial-sql-server-to-azure-sql-online\dms-source-details3.png)

## <a name="specify-target-details"></a><span data-ttu-id="5ce71-239">Specify target details</span><span class="sxs-lookup"><span data-stu-id="5ce71-239">Specify target details</span></span>
1. <span data-ttu-id="5ce71-240">Select **Save**, and then on the **Migration target details** screen, specify the connection details for the target Azure SQL Database server, which is the pre-provisioned Azure SQL Database to which the **AdventureWorks2012** schema was deployed by using the DMA.</span><span class="sxs-lookup"><span data-stu-id="5ce71-240">Select **Save**, and then on the **Migration target details** screen, specify the connection details for the target Azure SQL Database server, which is the pre-provisioned Azure SQL Database to which the **AdventureWorks2012** schema was deployed by using the DMA.</span></span>

    ![Select Target](media\tutorial-sql-server-to-azure-sql-online\dms-select-target3.png)

2. <span data-ttu-id="5ce71-242">Select **Save**, and then on the **Map to target databases** screen, map the source and the target database for migration.</span><span class="sxs-lookup"><span data-stu-id="5ce71-242">Select **Save**, and then on the **Map to target databases** screen, map the source and the target database for migration.</span></span>

    <span data-ttu-id="5ce71-243">If the target database contains the same database name as the source database, the Azure Database Migration Service selects the target database by default.</span><span class="sxs-lookup"><span data-stu-id="5ce71-243">If the target database contains the same database name as the source database, the Azure Database Migration Service selects the target database by default.</span></span>

    ![Map to target databases](media\tutorial-sql-server-to-azure-sql-online\dms-map-targets-activity3.png)

3. <span data-ttu-id="5ce71-245">Select **Save**, on the **Select tables** screen, expand the table listing, and then review the list of affected fields.</span><span class="sxs-lookup"><span data-stu-id="5ce71-245">Select **Save**, on the **Select tables** screen, expand the table listing, and then review the list of affected fields.</span></span>

    <span data-ttu-id="5ce71-246">The Azure Database Migration Service auto selects all the empty source tables that exist on the target Azure SQL Database instance.</span><span class="sxs-lookup"><span data-stu-id="5ce71-246">The Azure Database Migration Service auto selects all the empty source tables that exist on the target Azure SQL Database instance.</span></span> <span data-ttu-id="5ce71-247">If you want to remigrate tables that already include data, you need to explicitly select the tables on this blade.</span><span class="sxs-lookup"><span data-stu-id="5ce71-247">If you want to remigrate tables that already include data, you need to explicitly select the tables on this blade.</span></span>

    ![Select tables](media\tutorial-sql-server-to-azure-sql-online\dms-configure-setting-activity3.png)

4.  <span data-ttu-id="5ce71-249">Select **Save**, on the **Migration summary** screen, in the **Activity name** text box, specify a name for the migration activity, and then review the summary to ensure that the source and target details match what you previously specified.</span><span class="sxs-lookup"><span data-stu-id="5ce71-249">Select **Save**, on the **Migration summary** screen, in the **Activity name** text box, specify a name for the migration activity, and then review the summary to ensure that the source and target details match what you previously specified.</span></span>

    ![Migration Summary](media\tutorial-sql-server-to-azure-sql-online\dms-migration-summary.png)

## <a name="run-the-migration"></a><span data-ttu-id="5ce71-251">Run the migration</span><span class="sxs-lookup"><span data-stu-id="5ce71-251">Run the migration</span></span>
- <span data-ttu-id="5ce71-252">Select **Run migration**.</span><span class="sxs-lookup"><span data-stu-id="5ce71-252">Select **Run migration**.</span></span>

    <span data-ttu-id="5ce71-253">The migration activity window appears, and the **Status** of the activity is **Initializing**.</span><span class="sxs-lookup"><span data-stu-id="5ce71-253">The migration activity window appears, and the **Status** of the activity is **Initializing**.</span></span>

    ![Activity Status - initializing](media\tutorial-sql-server-to-azure-sql-online\dms-activity-status2.png)

## <a name="monitor-the-migration"></a><span data-ttu-id="5ce71-255">Monitor the migration</span><span class="sxs-lookup"><span data-stu-id="5ce71-255">Monitor the migration</span></span>
1. <span data-ttu-id="5ce71-256">On the migration activity screen, select **Refresh** to update the display until the **Status** of the migration shows as **Running**.</span><span class="sxs-lookup"><span data-stu-id="5ce71-256">On the migration activity screen, select **Refresh** to update the display until the **Status** of the migration shows as **Running**.</span></span>

2. <span data-ttu-id="5ce71-257">Click on a specific database to get to the migration status for **Full data load** and **Incremental data sync** operations.</span><span class="sxs-lookup"><span data-stu-id="5ce71-257">Click on a specific database to get to the migration status for **Full data load** and **Incremental data sync** operations.</span></span>

    ![Activity Status - in progress](media\tutorial-sql-server-to-azure-sql-online\dms-activity-in-progress.png)

## <a name="perform-migration-cutover"></a><span data-ttu-id="5ce71-259">Perform migration cutover</span><span class="sxs-lookup"><span data-stu-id="5ce71-259">Perform migration cutover</span></span>
<span data-ttu-id="5ce71-260">After the initial Full load is completed, the databases are marked **Ready to cutover**.</span><span class="sxs-lookup"><span data-stu-id="5ce71-260">After the initial Full load is completed, the databases are marked **Ready to cutover**.</span></span>

1. <span data-ttu-id="5ce71-261">When you're ready to complete the database migration, select **Start Cutover**.</span><span class="sxs-lookup"><span data-stu-id="5ce71-261">When you're ready to complete the database migration, select **Start Cutover**.</span></span>

    ![Start cutover](media\tutorial-sql-server-to-azure-sql-online\dms-start-cutover.png)
 
2.  <span data-ttu-id="5ce71-263">Make sure to stop all the incoming transactions to the source database; wait until the **Pending changes** counter shows **0**.</span><span class="sxs-lookup"><span data-stu-id="5ce71-263">Make sure to stop all the incoming transactions to the source database; wait until the **Pending changes** counter shows **0**.</span></span>
3.  <span data-ttu-id="5ce71-264">Select **Confirm**, and the select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="5ce71-264">Select **Confirm**, and the select **Apply**.</span></span>
4. <span data-ttu-id="5ce71-265">When the database migration status shows **Completed**, connect your applications to the new target Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="5ce71-265">When the database migration status shows **Completed**, connect your applications to the new target Azure SQL Database.</span></span>
 
    ![Activity Status - completed](media\tutorial-sql-server-to-azure-sql-online\dms-activity-completed.png)

## <a name="next-steps"></a><span data-ttu-id="5ce71-267">Next steps</span><span class="sxs-lookup"><span data-stu-id="5ce71-267">Next steps</span></span>
- <span data-ttu-id="5ce71-268">For information about known issues and limitations when performing online migrations to Azure Database for MySQL, see the article [Known issues and workarounds with Azure SQL Database online migrations](known-issues-azure-sql-online.md).</span><span class="sxs-lookup"><span data-stu-id="5ce71-268">For information about known issues and limitations when performing online migrations to Azure Database for MySQL, see the article [Known issues and workarounds with Azure SQL Database online migrations](known-issues-azure-sql-online.md).</span></span>
- <span data-ttu-id="5ce71-269">For information about the Azure Database Migration Service, see the article [What is the Azure Database Migration Service?](https://docs.microsoft.com/azure/dms/dms-overview).</span><span class="sxs-lookup"><span data-stu-id="5ce71-269">For information about the Azure Database Migration Service, see the article [What is the Azure Database Migration Service?](https://docs.microsoft.com/azure/dms/dms-overview).</span></span>
- <span data-ttu-id="5ce71-270">For information about the Azure SQL Database, see the article [What is the Azure SQL Database service?](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview).</span><span class="sxs-lookup"><span data-stu-id="5ce71-270">For information about the Azure SQL Database, see the article [What is the Azure SQL Database service?](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview).</span></span>
