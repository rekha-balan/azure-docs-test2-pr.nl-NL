---
title: Use the Azure Database Migration Service to migrate SQL Server to Azure SQL Database offline | Microsoft Docs
description: Learn to migrate from SQL Server on-premises to Azure SQL Database offline by using the Azure Database Migration Service.
services: dms
author: edmacauley
ms.author: jtoland
manager: craigg
ms.reviewer: ''
ms.service: dms
ms.workload: data-services
ms.custom: mvc, tutorial
ms.topic: article
ms.date: 08/24/2018
ms.openlocfilehash: 028dc14773bb7287fb143c940867b2c94d4d3c8e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867132"
---
# <a name="migrate-sql-server-to-azure-sql-database-offline-using-dms"></a><span data-ttu-id="26455-103">Migrate SQL Server to Azure SQL Database offline using DMS</span><span class="sxs-lookup"><span data-stu-id="26455-103">Migrate SQL Server to Azure SQL Database offline using DMS</span></span>
<span data-ttu-id="26455-104">You can use the Azure Database Migration Service to migrate the databases from an on-premises SQL Server instance to [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="26455-104">You can use the Azure Database Migration Service to migrate the databases from an on-premises SQL Server instance to [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/).</span></span> <span data-ttu-id="26455-105">In this tutorial, you migrate the **Adventureworks2012** database restored to an on-premises instance of SQL Server 2016 (or later) to an Azure SQL Database by using the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="26455-105">In this tutorial, you migrate the **Adventureworks2012** database restored to an on-premises instance of SQL Server 2016 (or later) to an Azure SQL Database by using the Azure Database Migration Service.</span></span>

<span data-ttu-id="26455-106">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="26455-106">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="26455-107">Assess your on-premises database by using the Data Migration Assistant.</span><span class="sxs-lookup"><span data-stu-id="26455-107">Assess your on-premises database by using the Data Migration Assistant.</span></span>
> * <span data-ttu-id="26455-108">Migrate the sample schema by using the Data Migration Assistant.</span><span class="sxs-lookup"><span data-stu-id="26455-108">Migrate the sample schema by using the Data Migration Assistant.</span></span>
> * <span data-ttu-id="26455-109">Create an instance of the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="26455-109">Create an instance of the Azure Database Migration Service.</span></span>
> * <span data-ttu-id="26455-110">Create a migration project by using the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="26455-110">Create a migration project by using the Azure Database Migration Service.</span></span>
> * <span data-ttu-id="26455-111">Run the migration.</span><span class="sxs-lookup"><span data-stu-id="26455-111">Run the migration.</span></span>
> * <span data-ttu-id="26455-112">Monitor the migration.</span><span class="sxs-lookup"><span data-stu-id="26455-112">Monitor the migration.</span></span>
> * <span data-ttu-id="26455-113">Download a migration report.</span><span class="sxs-lookup"><span data-stu-id="26455-113">Download a migration report.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26455-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="26455-114">Prerequisites</span></span>
<span data-ttu-id="26455-115">To complete this tutorial, you need to:</span><span class="sxs-lookup"><span data-stu-id="26455-115">To complete this tutorial, you need to:</span></span>

- <span data-ttu-id="26455-116">Download and install [SQL Server 2016 or later](https://www.microsoft.com/sql-server/sql-server-downloads) (any edition).</span><span class="sxs-lookup"><span data-stu-id="26455-116">Download and install [SQL Server 2016 or later](https://www.microsoft.com/sql-server/sql-server-downloads) (any edition).</span></span>
- <span data-ttu-id="26455-117">Enable the TCP/IP protocol, which is disabled by default during SQL Server Express installation, by following the instructions in the article [Enable or Disable a Server Network Protocol](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-or-disable-a-server-network-protocol#SSMSProcedure).</span><span class="sxs-lookup"><span data-stu-id="26455-117">Enable the TCP/IP protocol, which is disabled by default during SQL Server Express installation, by following the instructions in the article [Enable or Disable a Server Network Protocol](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-or-disable-a-server-network-protocol#SSMSProcedure).</span></span>
- <span data-ttu-id="26455-118">Create an instance of Azure SQL Database instance, which you do by following the detail in the article [Create an Azure SQL database in the Azure portal](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="26455-118">Create an instance of Azure SQL Database instance, which you do by following the detail in the article [Create an Azure SQL database in the Azure portal](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal).</span></span>
- <span data-ttu-id="26455-119">Download and install the [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) v3.3 or later.</span><span class="sxs-lookup"><span data-stu-id="26455-119">Download and install the [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) v3.3 or later.</span></span>
- <span data-ttu-id="26455-120">Create a VNET for the Azure Database Migration Service by using the Azure Resource Manager deployment model, which provides site-to-site connectivity to your on-premises source servers by using either [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) or [VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).</span><span class="sxs-lookup"><span data-stu-id="26455-120">Create a VNET for the Azure Database Migration Service by using the Azure Resource Manager deployment model, which provides site-to-site connectivity to your on-premises source servers by using either [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) or [VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).</span></span>
- <span data-ttu-id="26455-121">Ensure that your Azure Virtual Network (VNET) Network Security Group rules do not block the following communication ports 443, 53, 9354, 445, 12000.</span><span class="sxs-lookup"><span data-stu-id="26455-121">Ensure that your Azure Virtual Network (VNET) Network Security Group rules do not block the following communication ports 443, 53, 9354, 445, 12000.</span></span> <span data-ttu-id="26455-122">For more detail on Azure VNET NSG traffic filtering, see the article [Filter network traffic with network security groups](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg).</span><span class="sxs-lookup"><span data-stu-id="26455-122">For more detail on Azure VNET NSG traffic filtering, see the article [Filter network traffic with network security groups](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg).</span></span>
- <span data-ttu-id="26455-123">Configure your [Windows Firewall for database engine access](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access).</span><span class="sxs-lookup"><span data-stu-id="26455-123">Configure your [Windows Firewall for database engine access](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access).</span></span>
- <span data-ttu-id="26455-124">Open your Windows firewall to allow the Azure Database Migration Service to access the source SQL Server, which by default is TCP port 1433.</span><span class="sxs-lookup"><span data-stu-id="26455-124">Open your Windows firewall to allow the Azure Database Migration Service to access the source SQL Server, which by default is TCP port 1433.</span></span>
- <span data-ttu-id="26455-125">If you are running multiple named SQL Server instances using dynamic ports, you may wish to enable the SQL Browser Service and allow access to UDP port 1434 through your firewalls so that the Azure Database Migration Service can connect to a named instance on your source server.</span><span class="sxs-lookup"><span data-stu-id="26455-125">If you are running multiple named SQL Server instances using dynamic ports, you may wish to enable the SQL Browser Service and allow access to UDP port 1434 through your firewalls so that the Azure Database Migration Service can connect to a named instance on your source server.</span></span>
- <span data-ttu-id="26455-126">When using a firewall appliance in front of your source database(s), you may need to add firewall rules to allow the Azure Database Migration Service to access the source database(s) for migration.</span><span class="sxs-lookup"><span data-stu-id="26455-126">When using a firewall appliance in front of your source database(s), you may need to add firewall rules to allow the Azure Database Migration Service to access the source database(s) for migration.</span></span>
- <span data-ttu-id="26455-127">Create a server-level [firewall rule](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) for the Azure SQL Database server to allow the Azure Database Migration Service access to the target databases.</span><span class="sxs-lookup"><span data-stu-id="26455-127">Create a server-level [firewall rule](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) for the Azure SQL Database server to allow the Azure Database Migration Service access to the target databases.</span></span> <span data-ttu-id="26455-128">Provide the subnet range of the VNET used for the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="26455-128">Provide the subnet range of the VNET used for the Azure Database Migration Service.</span></span>
- <span data-ttu-id="26455-129">Ensure that the credentials used to connect to source SQL Server instance have [CONTROL SERVER](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql) permissions.</span><span class="sxs-lookup"><span data-stu-id="26455-129">Ensure that the credentials used to connect to source SQL Server instance have [CONTROL SERVER](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql) permissions.</span></span>
- <span data-ttu-id="26455-130">Ensure that the credentials used to connect to target Azure SQL Database instance have CONTROL DATABASE permission on the target Azure SQL databases.</span><span class="sxs-lookup"><span data-stu-id="26455-130">Ensure that the credentials used to connect to target Azure SQL Database instance have CONTROL DATABASE permission on the target Azure SQL databases.</span></span>

## <a name="assess-your-on-premises-database"></a><span data-ttu-id="26455-131">Assess your on-premises database</span><span class="sxs-lookup"><span data-stu-id="26455-131">Assess your on-premises database</span></span>
<span data-ttu-id="26455-132">Before you can migrate data from an on-premises SQL Server instance to Azure SQL Database, you need to assess the SQL Server database for any blocking issues that might prevent migration.</span><span class="sxs-lookup"><span data-stu-id="26455-132">Before you can migrate data from an on-premises SQL Server instance to Azure SQL Database, you need to assess the SQL Server database for any blocking issues that might prevent migration.</span></span> <span data-ttu-id="26455-133">Using the Data Migration Assistant v3.3 or later, follow the steps described in the article [Performing a SQL Server migration assessment](https://docs.microsoft.com/sql/dma/dma-assesssqlonprem) to complete the on-premises database assessment.</span><span class="sxs-lookup"><span data-stu-id="26455-133">Using the Data Migration Assistant v3.3 or later, follow the steps described in the article [Performing a SQL Server migration assessment](https://docs.microsoft.com/sql/dma/dma-assesssqlonprem) to complete the on-premises database assessment.</span></span> <span data-ttu-id="26455-134">A summary of the required steps follows:</span><span class="sxs-lookup"><span data-stu-id="26455-134">A summary of the required steps follows:</span></span>
1.  <span data-ttu-id="26455-135">In the Data Migration Assistant, select the New (+) icon, and then select the **Assessment**  project type.</span><span class="sxs-lookup"><span data-stu-id="26455-135">In the Data Migration Assistant, select the New (+) icon, and then select the **Assessment**  project type.</span></span>
2.  <span data-ttu-id="26455-136">Specify a project name, in the **Source server type** text box, select **SQL Server**, in the **Target server type** text box, select **Azure SQL Database**, and then select **Create** to create the project.</span><span class="sxs-lookup"><span data-stu-id="26455-136">Specify a project name, in the **Source server type** text box, select **SQL Server**, in the **Target server type** text box, select **Azure SQL Database**, and then select **Create** to create the project.</span></span>

    <span data-ttu-id="26455-137">When you are assessing the source SQL Server database migrating to Azure SQL Database, you can choose one or both of the following assessment report types:</span><span class="sxs-lookup"><span data-stu-id="26455-137">When you are assessing the source SQL Server database migrating to Azure SQL Database, you can choose one or both of the following assessment report types:</span></span>
    - <span data-ttu-id="26455-138">Check database compatibility</span><span class="sxs-lookup"><span data-stu-id="26455-138">Check database compatibility</span></span>
    - <span data-ttu-id="26455-139">Check feature parity</span><span class="sxs-lookup"><span data-stu-id="26455-139">Check feature parity</span></span>

    <span data-ttu-id="26455-140">Both report types are selected by default.</span><span class="sxs-lookup"><span data-stu-id="26455-140">Both report types are selected by default.</span></span>

3.  <span data-ttu-id="26455-141">In the Data Migration Assistant, on the **Options** screen, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="26455-141">In the Data Migration Assistant, on the **Options** screen, select **Next**.</span></span>
4.  <span data-ttu-id="26455-142">On the **Select sources** screen, in the **Connect to a server** dialog box, provide the connection details to your SQL Server, and then select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="26455-142">On the **Select sources** screen, in the **Connect to a server** dialog box, provide the connection details to your SQL Server, and then select **Connect**.</span></span>
5.  <span data-ttu-id="26455-143">In the **Add sources** dialog box, select **AdventureWorks2012**, select **Add**, and then select **Start Assessment**.</span><span class="sxs-lookup"><span data-stu-id="26455-143">In the **Add sources** dialog box, select **AdventureWorks2012**, select **Add**, and then select **Start Assessment**.</span></span>

    <span data-ttu-id="26455-144">When the assessment is complete, the results display as shown in the following graphic:</span><span class="sxs-lookup"><span data-stu-id="26455-144">When the assessment is complete, the results display as shown in the following graphic:</span></span>

    ![Assess data migration](media\tutorial-sql-server-to-azure-sql\dma-assessments.png)

    <span data-ttu-id="26455-146">For Azure SQL Database, the assessments identify feature parity issues and migration blocking issues.</span><span class="sxs-lookup"><span data-stu-id="26455-146">For Azure SQL Database, the assessments identify feature parity issues and migration blocking issues.</span></span>

    - <span data-ttu-id="26455-147">The **SQL Server feature parity** category provides a comprehensive set of recommendations, alternative approaches available in Azure, and mitigating steps to help you plan the effort into your migration projects.</span><span class="sxs-lookup"><span data-stu-id="26455-147">The **SQL Server feature parity** category provides a comprehensive set of recommendations, alternative approaches available in Azure, and mitigating steps to help you plan the effort into your migration projects.</span></span>
    - <span data-ttu-id="26455-148">The **Compatibility issues** category identifies partially supported or unsupported features that reflect compatibility issues that might block migrating on-premises SQL Server database(s) to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="26455-148">The **Compatibility issues** category identifies partially supported or unsupported features that reflect compatibility issues that might block migrating on-premises SQL Server database(s) to Azure SQL Database.</span></span> <span data-ttu-id="26455-149">Recommendations are also provided to help you address those issues.</span><span class="sxs-lookup"><span data-stu-id="26455-149">Recommendations are also provided to help you address those issues.</span></span>

6.  <span data-ttu-id="26455-150">Review the assessment results for migration blocking issues and feature parity issues by selecting the specific options.</span><span class="sxs-lookup"><span data-stu-id="26455-150">Review the assessment results for migration blocking issues and feature parity issues by selecting the specific options.</span></span>

## <a name="migrate-the-sample-schema"></a><span data-ttu-id="26455-151">Migrate the sample schema</span><span class="sxs-lookup"><span data-stu-id="26455-151">Migrate the sample schema</span></span>
<span data-ttu-id="26455-152">After you are comfortable with the assessment and satisfied that the selected database is a viable candidate for migration to Azure SQL Database, use the Data Migration Assistant to migrate the schema to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="26455-152">After you are comfortable with the assessment and satisfied that the selected database is a viable candidate for migration to Azure SQL Database, use the Data Migration Assistant to migrate the schema to Azure SQL Database.</span></span>

> [!NOTE]
> <span data-ttu-id="26455-153">Before you create a migration project in Data Migration Assistant, be sure that you have already provisioned an Azure SQL database as mentioned in the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="26455-153">Before you create a migration project in Data Migration Assistant, be sure that you have already provisioned an Azure SQL database as mentioned in the prerequisites.</span></span> <span data-ttu-id="26455-154">For purposes of this tutorial, the name of the Azure SQL Database is assumed to be **AdventureWorksAzure**, but you can provide whatever name you wish.</span><span class="sxs-lookup"><span data-stu-id="26455-154">For purposes of this tutorial, the name of the Azure SQL Database is assumed to be **AdventureWorksAzure**, but you can provide whatever name you wish.</span></span>

<span data-ttu-id="26455-155">To migrate the **AdventureWorks2012** schema to Azure SQL Database, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="26455-155">To migrate the **AdventureWorks2012** schema to Azure SQL Database, perform the following steps:</span></span>

1.  <span data-ttu-id="26455-156">In the Data Migration Assistant, select the New (+) icon, and then under **Project type**, select **Migration**.</span><span class="sxs-lookup"><span data-stu-id="26455-156">In the Data Migration Assistant, select the New (+) icon, and then under **Project type**, select **Migration**.</span></span>
2.  <span data-ttu-id="26455-157">Specify a project name, in the **Source server type** text box, select **SQL Server**, and then in the **Target server type** text box, select **Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="26455-157">Specify a project name, in the **Source server type** text box, select **SQL Server**, and then in the **Target server type** text box, select **Azure SQL Database**.</span></span>
3.  <span data-ttu-id="26455-158">Under **Migration Scope**, select **Schema only**.</span><span class="sxs-lookup"><span data-stu-id="26455-158">Under **Migration Scope**, select **Schema only**.</span></span>

    <span data-ttu-id="26455-159">After performing the previous steps, the Data Migration Assistant interface should appear as shown in the following graphic:</span><span class="sxs-lookup"><span data-stu-id="26455-159">After performing the previous steps, the Data Migration Assistant interface should appear as shown in the following graphic:</span></span>
    
    ![Create Data Migration Assistant Project](media\tutorial-sql-server-to-azure-sql\dma-create-project.png)

4.  <span data-ttu-id="26455-161">Select **Create** to create the project.</span><span class="sxs-lookup"><span data-stu-id="26455-161">Select **Create** to create the project.</span></span>
5.  <span data-ttu-id="26455-162">In the Data Migration Assistant, specify the source connection details for your SQL Server, select **Connect**, and then select the **AdventureWorks2012** database.</span><span class="sxs-lookup"><span data-stu-id="26455-162">In the Data Migration Assistant, specify the source connection details for your SQL Server, select **Connect**, and then select the **AdventureWorks2012** database.</span></span>

    ![Data Migration Assistant Source Connection Details](media\tutorial-sql-server-to-azure-sql\dma-source-connect.png)

6.  <span data-ttu-id="26455-164">Select **Next**, under **Connect to target server**, specify the target connection details for the Azure SQL database, select **Connect**, and then select the **AdventureWorksAzure** database you had pre-provisioned in Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="26455-164">Select **Next**, under **Connect to target server**, specify the target connection details for the Azure SQL database, select **Connect**, and then select the **AdventureWorksAzure** database you had pre-provisioned in Azure SQL database.</span></span>

    ![Data Migration Assistant Target Connection Details](media\tutorial-sql-server-to-azure-sql\dma-target-connect.png)

7.  <span data-ttu-id="26455-166">Select **Next** to advance to the **Select objects** screen, on which you can specify the schema objects in the **AdventureWorks2012** database that need to be deployed to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="26455-166">Select **Next** to advance to the **Select objects** screen, on which you can specify the schema objects in the **AdventureWorks2012** database that need to be deployed to Azure SQL Database.</span></span>

    <span data-ttu-id="26455-167">By default, all objects are selected.</span><span class="sxs-lookup"><span data-stu-id="26455-167">By default, all objects are selected.</span></span>

    ![Generate SQL Scripts](media\tutorial-sql-server-to-azure-sql\dma-assessment-source.png)

8.  <span data-ttu-id="26455-169">Select **Generate SQL script** to create the SQL scripts, and then review the scripts for any errors.</span><span class="sxs-lookup"><span data-stu-id="26455-169">Select **Generate SQL script** to create the SQL scripts, and then review the scripts for any errors.</span></span>

    ![Schema Script](media\tutorial-sql-server-to-azure-sql\dma-schema-script.png)

9.  <span data-ttu-id="26455-171">Select **Deploy schema** to deploy the schema to Azure SQL Database, and then after the schema is deployed, check the target server for any anomalies.</span><span class="sxs-lookup"><span data-stu-id="26455-171">Select **Deploy schema** to deploy the schema to Azure SQL Database, and then after the schema is deployed, check the target server for any anomalies.</span></span>

    ![Deploy Schema](media\tutorial-sql-server-to-azure-sql\dma-schema-deploy.png)

## <a name="register-the-microsoftdatamigration-resource-provider"></a><span data-ttu-id="26455-173">Register the Microsoft.DataMigration resource provider</span><span class="sxs-lookup"><span data-stu-id="26455-173">Register the Microsoft.DataMigration resource provider</span></span>
1. <span data-ttu-id="26455-174">Log in to the Azure portal, select **All services**, and then select **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="26455-174">Log in to the Azure portal, select **All services**, and then select **Subscriptions**.</span></span>
 
   ![Show portal subscriptions](media\tutorial-sql-server-to-azure-sql\portal-select-subscription1.png)
       
2. <span data-ttu-id="26455-176">Select the subscription in which you want to create the instance of the Azure Database Migration Service, and then select **Resource providers**.</span><span class="sxs-lookup"><span data-stu-id="26455-176">Select the subscription in which you want to create the instance of the Azure Database Migration Service, and then select **Resource providers**.</span></span>
 
    ![Show resource providers](media\tutorial-sql-server-to-azure-sql\portal-select-resource-provider.png)
    
3.  <span data-ttu-id="26455-178">Search for migration, and then to the right of **Microsoft.DataMigration**, select **Register**.</span><span class="sxs-lookup"><span data-stu-id="26455-178">Search for migration, and then to the right of **Microsoft.DataMigration**, select **Register**.</span></span>
 
    ![Register resource provider](media\tutorial-sql-server-to-azure-sql\portal-register-resource-provider.png)    

## <a name="create-an-instance"></a><span data-ttu-id="26455-180">Create an instance</span><span class="sxs-lookup"><span data-stu-id="26455-180">Create an instance</span></span>
1.  <span data-ttu-id="26455-181">In the Azure portal, select + **Create a resource**, search for Azure Database Migration Service, and then select **Azure Database Migration Service** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="26455-181">In the Azure portal, select + **Create a resource**, search for Azure Database Migration Service, and then select **Azure Database Migration Service** from the drop-down list.</span></span>

    ![Azure Marketplace](media\tutorial-sql-server-to-azure-sql\portal-marketplace.png)

2.  <span data-ttu-id="26455-183">On the **Azure Database Migration Service** screen, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="26455-183">On the **Azure Database Migration Service** screen, select **Create**.</span></span>
 
    ![Create Azure Database Migration Service instance](media\tutorial-sql-server-to-azure-sql\dms-create1.png)
  
3.  <span data-ttu-id="26455-185">On the **Create Migration Service** screen, specify a name for the service, the subscription, and a new or existing resource group.</span><span class="sxs-lookup"><span data-stu-id="26455-185">On the **Create Migration Service** screen, specify a name for the service, the subscription, and a new or existing resource group.</span></span>

4. <span data-ttu-id="26455-186">Select the location in which you want to create the instance of the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="26455-186">Select the location in which you want to create the instance of the Azure Database Migration Service.</span></span> 

5. <span data-ttu-id="26455-187">Select an existing virtual network (VNET) or create a new one.</span><span class="sxs-lookup"><span data-stu-id="26455-187">Select an existing virtual network (VNET) or create a new one.</span></span>

    <span data-ttu-id="26455-188">The VNET provides the Azure Database Migration Service with access to the source SQL Server and the target Azure SQL Database instance.</span><span class="sxs-lookup"><span data-stu-id="26455-188">The VNET provides the Azure Database Migration Service with access to the source SQL Server and the target Azure SQL Database instance.</span></span>

    <span data-ttu-id="26455-189">For more information about how to create a VNET in the Azure portal, see the article [Create a virtual network using the Azure portal](https://aka.ms/DMSVnet).</span><span class="sxs-lookup"><span data-stu-id="26455-189">For more information about how to create a VNET in the Azure portal, see the article [Create a virtual network using the Azure portal](https://aka.ms/DMSVnet).</span></span>

6. <span data-ttu-id="26455-190">Select a pricing tier.</span><span class="sxs-lookup"><span data-stu-id="26455-190">Select a pricing tier.</span></span>

    <span data-ttu-id="26455-191">For more information on costs and pricing tiers, see the [pricing page](https://aka.ms/dms-pricing).</span><span class="sxs-lookup"><span data-stu-id="26455-191">For more information on costs and pricing tiers, see the [pricing page](https://aka.ms/dms-pricing).</span></span>

    <span data-ttu-id="26455-192">If you need help in choosing the right Azure Database Migration Service tier, refer to the recommendations in the posting [here](https://go.microsoft.com/fwlink/?linkid=861067).</span><span class="sxs-lookup"><span data-stu-id="26455-192">If you need help in choosing the right Azure Database Migration Service tier, refer to the recommendations in the posting [here](https://go.microsoft.com/fwlink/?linkid=861067).</span></span>  

     ![Configure Azure Database Migration Service instance settings](media\tutorial-sql-server-to-azure-sql\dms-settings2.png)

7.  <span data-ttu-id="26455-194">Select **Create** to create the service.</span><span class="sxs-lookup"><span data-stu-id="26455-194">Select **Create** to create the service.</span></span>

## <a name="create-a-migration-project"></a><span data-ttu-id="26455-195">Create a migration project</span><span class="sxs-lookup"><span data-stu-id="26455-195">Create a migration project</span></span>
<span data-ttu-id="26455-196">After the service is created, locate it within the Azure portal, open it, and then create a new migration project.</span><span class="sxs-lookup"><span data-stu-id="26455-196">After the service is created, locate it within the Azure portal, open it, and then create a new migration project.</span></span>

1. <span data-ttu-id="26455-197">In the Azure portal, select **All services**, search for Azure Database Migration Service, and then select **Azure Database Migration Services**.</span><span class="sxs-lookup"><span data-stu-id="26455-197">In the Azure portal, select **All services**, search for Azure Database Migration Service, and then select **Azure Database Migration Services**.</span></span>
 
      ![Locate all instances of the Azure Database Migration Service](media\tutorial-sql-server-to-azure-sql\dms-search.png)

2. <span data-ttu-id="26455-199">On the **Azure Database Migration Services** screen, search for the name of the Azure Database Migration Service instance that you created, and then select the instance.</span><span class="sxs-lookup"><span data-stu-id="26455-199">On the **Azure Database Migration Services** screen, search for the name of the Azure Database Migration Service instance that you created, and then select the instance.</span></span>
 
     ![Locate your instance of the Azure Database Migration Service](media\tutorial-sql-server-to-azure-sql\dms-instance-search.png)
 
3. <span data-ttu-id="26455-201">Select + **New Migration Project**.</span><span class="sxs-lookup"><span data-stu-id="26455-201">Select + **New Migration Project**.</span></span>
4. <span data-ttu-id="26455-202">On the **New migration project** screen, specify a name for the project, in the **Source server type** text box, select **SQL Server**, in the **Target server type** text box, select **Azure SQL Database**, and then for **Choose type of activity**, select **Offline data migration**.</span><span class="sxs-lookup"><span data-stu-id="26455-202">On the **New migration project** screen, specify a name for the project, in the **Source server type** text box, select **SQL Server**, in the **Target server type** text box, select **Azure SQL Database**, and then for **Choose type of activity**, select **Offline data migration**.</span></span> 

    ![Create Database Migration Service Project](media\tutorial-sql-server-to-azure-sql\dms-create-project2.png)

5.  <span data-ttu-id="26455-204">Select **Create and run activity** to create the project and run the migration activity.</span><span class="sxs-lookup"><span data-stu-id="26455-204">Select **Create and run activity** to create the project and run the migration activity.</span></span>

## <a name="specify-source-details"></a><span data-ttu-id="26455-205">Specify source details</span><span class="sxs-lookup"><span data-stu-id="26455-205">Specify source details</span></span>
1. <span data-ttu-id="26455-206">On the **Migration source detail** screen, specify the connection details for the source SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="26455-206">On the **Migration source detail** screen, specify the connection details for the source SQL Server instance.</span></span>
 
    <span data-ttu-id="26455-207">Make sure to use a Fully Qualified Domain Name (FQDN) for the source SQL Server instance name.</span><span class="sxs-lookup"><span data-stu-id="26455-207">Make sure to use a Fully Qualified Domain Name (FQDN) for the source SQL Server instance name.</span></span> <span data-ttu-id="26455-208">You can also use the IP Address for situations in which DNS name resolution is not possible.</span><span class="sxs-lookup"><span data-stu-id="26455-208">You can also use the IP Address for situations in which DNS name resolution is not possible.</span></span>

2. <span data-ttu-id="26455-209">If you have not installed a trusted certificate on your source server, select the **Trust server certificate** check box.</span><span class="sxs-lookup"><span data-stu-id="26455-209">If you have not installed a trusted certificate on your source server, select the **Trust server certificate** check box.</span></span>

    <span data-ttu-id="26455-210">When a trusted certificate is not installed, SQL Server generates a self-signed certificate when the instance is started.</span><span class="sxs-lookup"><span data-stu-id="26455-210">When a trusted certificate is not installed, SQL Server generates a self-signed certificate when the instance is started.</span></span> <span data-ttu-id="26455-211">This certificate is used to encrypt the credentials for client connections.</span><span class="sxs-lookup"><span data-stu-id="26455-211">This certificate is used to encrypt the credentials for client connections.</span></span>

    > [!CAUTION]
    > <span data-ttu-id="26455-212">SSL connections that are encrypted using a self-signed certificate do not provide strong security.</span><span class="sxs-lookup"><span data-stu-id="26455-212">SSL connections that are encrypted using a self-signed certificate do not provide strong security.</span></span> <span data-ttu-id="26455-213">They are susceptible to man-in-the-middle attacks.</span><span class="sxs-lookup"><span data-stu-id="26455-213">They are susceptible to man-in-the-middle attacks.</span></span> <span data-ttu-id="26455-214">You should not rely on SSL using self-signed certificates in a production environment or on servers that are connected to the internet.</span><span class="sxs-lookup"><span data-stu-id="26455-214">You should not rely on SSL using self-signed certificates in a production environment or on servers that are connected to the internet.</span></span>

   ![Source Details](media\tutorial-sql-server-to-azure-sql\dms-source-details2.png)

## <a name="specify-target-details"></a><span data-ttu-id="26455-216">Specify target details</span><span class="sxs-lookup"><span data-stu-id="26455-216">Specify target details</span></span>
1. <span data-ttu-id="26455-217">Select **Save**, and then on the **Migration target details** screen, specify the connection details for the target Azure SQL Database Server, which is the pre-provisioned Azure SQL Database to which the **AdventureWorks2012** schema was deployed by using the Data Migration Assistant.</span><span class="sxs-lookup"><span data-stu-id="26455-217">Select **Save**, and then on the **Migration target details** screen, specify the connection details for the target Azure SQL Database Server, which is the pre-provisioned Azure SQL Database to which the **AdventureWorks2012** schema was deployed by using the Data Migration Assistant.</span></span>

    ![Select Target](media\tutorial-sql-server-to-azure-sql\dms-select-target2.png)

2. <span data-ttu-id="26455-219">Select **Save**, and then on the **Map to target databases** screen, map the source and the target database for migration.</span><span class="sxs-lookup"><span data-stu-id="26455-219">Select **Save**, and then on the **Map to target databases** screen, map the source and the target database for migration.</span></span>

    <span data-ttu-id="26455-220">If the target database contains the same database name as the source database, the Azure Database Migration Service selects the target database by default.</span><span class="sxs-lookup"><span data-stu-id="26455-220">If the target database contains the same database name as the source database, the Azure Database Migration Service selects the target database by default.</span></span>

    ![Map to target databases](media\tutorial-sql-server-to-azure-sql\dms-map-targets-activity2.png)

3. <span data-ttu-id="26455-222">Select **Save**, on the **Select tables** screen, expand the table listing, and then review the list of affected fields.</span><span class="sxs-lookup"><span data-stu-id="26455-222">Select **Save**, on the **Select tables** screen, expand the table listing, and then review the list of affected fields.</span></span>

    <span data-ttu-id="26455-223">Note that the Azure Database Migration Service auto selects all the empty source tables that exist on the target Azure SQL Database instance.</span><span class="sxs-lookup"><span data-stu-id="26455-223">Note that the Azure Database Migration Service auto selects all the empty source tables that exist on the target Azure SQL Database instance.</span></span> <span data-ttu-id="26455-224">If you want to remigrate tables that already include data, you need to explicitly select the tables on this blade.</span><span class="sxs-lookup"><span data-stu-id="26455-224">If you want to remigrate tables that already include data, you need to explicitly select the tables on this blade.</span></span>

    ![Select tables](media\tutorial-sql-server-to-azure-sql\dms-configure-setting-activity2.png)

4.  <span data-ttu-id="26455-226">Select **Save**, on the **Migration summary** screen, in the **Activity name** text box, specify a name for the migration activity.</span><span class="sxs-lookup"><span data-stu-id="26455-226">Select **Save**, on the **Migration summary** screen, in the **Activity name** text box, specify a name for the migration activity.</span></span>

5. <span data-ttu-id="26455-227">Expand the **Validation option** section to display the **Choose validation option** screen, and then specify whether to validate the migrated databases for **Schema comparison**, **Data consistency**, and **Query correctness**.</span><span class="sxs-lookup"><span data-stu-id="26455-227">Expand the **Validation option** section to display the **Choose validation option** screen, and then specify whether to validate the migrated databases for **Schema comparison**, **Data consistency**, and **Query correctness**.</span></span>
    
    ![Choose validation option](media\tutorial-sql-server-to-azure-sql\dms-configuration2.png)

6.  <span data-ttu-id="26455-229">Select **Save**, review the summary to ensure that the source and target details match what you previously specified.</span><span class="sxs-lookup"><span data-stu-id="26455-229">Select **Save**, review the summary to ensure that the source and target details match what you previously specified.</span></span>

    ![Migration Summary](media\tutorial-sql-server-to-azure-sql\dms-run-migration2.png)

## <a name="run-the-migration"></a><span data-ttu-id="26455-231">Run the migration</span><span class="sxs-lookup"><span data-stu-id="26455-231">Run the migration</span></span>
- <span data-ttu-id="26455-232">Select **Run migration**.</span><span class="sxs-lookup"><span data-stu-id="26455-232">Select **Run migration**.</span></span>

    <span data-ttu-id="26455-233">The migration activity window appears, and the **Status** of the activity is **Pending**.</span><span class="sxs-lookup"><span data-stu-id="26455-233">The migration activity window appears, and the **Status** of the activity is **Pending**.</span></span>

    ![Activity Status](media\tutorial-sql-server-to-azure-sql\dms-activity-status1.png)

## <a name="monitor-the-migration"></a><span data-ttu-id="26455-235">Monitor the migration</span><span class="sxs-lookup"><span data-stu-id="26455-235">Monitor the migration</span></span>
1. <span data-ttu-id="26455-236">On the migration activity screen, select **Refresh** to update the display until the **Status** of the migration shows as **Completed**.</span><span class="sxs-lookup"><span data-stu-id="26455-236">On the migration activity screen, select **Refresh** to update the display until the **Status** of the migration shows as **Completed**.</span></span>

    ![Activity Status Completed](media\tutorial-sql-server-to-azure-sql\dms-completed-activity1.png)

2. <span data-ttu-id="26455-238">After the migration completes, select **Download report** to get a report listing the details associated with the migration process.</span><span class="sxs-lookup"><span data-stu-id="26455-238">After the migration completes, select **Download report** to get a report listing the details associated with the migration process.</span></span>

3. <span data-ttu-id="26455-239">Verify the target database(s) on the target Azure SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="26455-239">Verify the target database(s) on the target Azure SQL Database server.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="26455-240">Additional resources</span><span class="sxs-lookup"><span data-stu-id="26455-240">Additional resources</span></span>

 * <span data-ttu-id="26455-241">[SQL migration using Azure Data Migration Service (DMS)](https://www.microsoft.com/handsonlabs/SelfPacedLabs/?storyGuid=3b671509-c3cd-4495-8e8f-354acfa09587) hands-on lab.</span><span class="sxs-lookup"><span data-stu-id="26455-241">[SQL migration using Azure Data Migration Service (DMS)](https://www.microsoft.com/handsonlabs/SelfPacedLabs/?storyGuid=3b671509-c3cd-4495-8e8f-354acfa09587) hands-on lab.</span></span>