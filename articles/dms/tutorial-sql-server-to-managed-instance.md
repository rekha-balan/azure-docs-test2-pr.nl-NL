---
title: Use DMS to migrate to Azure SQL Database Managed Instance | Microsoft Docs
description: Learn to migrate from SQL Server on-premises to Azure SQL Database Managed Instance by using the Azure Database Migration Service.
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
ms.openlocfilehash: dbf71b1fcc15743f4670c4072921f1a167a90e97
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867717"
---
# <a name="migrate-sql-server-to-azure-sql-database-managed-instance-offline-using-dms"></a><span data-ttu-id="f4fa3-103">Migrate SQL Server to Azure SQL Database Managed Instance offline using DMS</span><span class="sxs-lookup"><span data-stu-id="f4fa3-103">Migrate SQL Server to Azure SQL Database Managed Instance offline using DMS</span></span>
<span data-ttu-id="f4fa3-104">You can use the Azure Database Migration Service to migrate the databases from an on-premises SQL Server instance to an [Azure SQL Database Managed Instance](../sql-database/sql-database-managed-instance.md).</span><span class="sxs-lookup"><span data-stu-id="f4fa3-104">You can use the Azure Database Migration Service to migrate the databases from an on-premises SQL Server instance to an [Azure SQL Database Managed Instance](../sql-database/sql-database-managed-instance.md).</span></span> <span data-ttu-id="f4fa3-105">For additional methods that may require some manual effort, see the article [SQL Server instance migration to Azure SQL Database Managed Instance](../sql-database/sql-database-managed-instance-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="f4fa3-105">For additional methods that may require some manual effort, see the article [SQL Server instance migration to Azure SQL Database Managed Instance](../sql-database/sql-database-managed-instance-migrate.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4fa3-106">Migration projects from SQL Server to Azure SQL Database Managed Instance are in preview and subject to the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="f4fa3-106">Migration projects from SQL Server to Azure SQL Database Managed Instance are in preview and subject to the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>

<span data-ttu-id="f4fa3-107">In this tutorial, you migrate the **Adventureworks2012** database from an on-premises instance of SQL Server to an Azure SQL Database Managed Instance by using the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-107">In this tutorial, you migrate the **Adventureworks2012** database from an on-premises instance of SQL Server to an Azure SQL Database Managed Instance by using the Azure Database Migration Service.</span></span>

<span data-ttu-id="f4fa3-108">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="f4fa3-108">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="f4fa3-109">Create an instance of the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-109">Create an instance of the Azure Database Migration Service.</span></span>
> * <span data-ttu-id="f4fa3-110">Create a migration project by using the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-110">Create a migration project by using the Azure Database Migration Service.</span></span>
> * <span data-ttu-id="f4fa3-111">Run the migration.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-111">Run the migration.</span></span>
> * <span data-ttu-id="f4fa3-112">Monitor the migration.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-112">Monitor the migration.</span></span>
> * <span data-ttu-id="f4fa3-113">Download a migration report.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-113">Download a migration report.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4fa3-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f4fa3-114">Prerequisites</span></span>
<span data-ttu-id="f4fa3-115">To complete this tutorial, you need to:</span><span class="sxs-lookup"><span data-stu-id="f4fa3-115">To complete this tutorial, you need to:</span></span>

- <span data-ttu-id="f4fa3-116">Create a VNET for the Azure Database Migration Service by using the Azure Resource Manager deployment model, which provides site-to-site connectivity to your on-premises source servers by using either [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) or [VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).</span><span class="sxs-lookup"><span data-stu-id="f4fa3-116">Create a VNET for the Azure Database Migration Service by using the Azure Resource Manager deployment model, which provides site-to-site connectivity to your on-premises source servers by using either [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) or [VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).</span></span> <span data-ttu-id="f4fa3-117">[Learn network topologies for Azure SQL DB Managed Instance migrations using the Azure Database Migration Service](https://aka.ms/dmsnetworkformi).</span><span class="sxs-lookup"><span data-stu-id="f4fa3-117">[Learn network topologies for Azure SQL DB Managed Instance migrations using the Azure Database Migration Service](https://aka.ms/dmsnetworkformi).</span></span>
- <span data-ttu-id="f4fa3-118">Ensure that your Azure Virtual Network (VNET) Network Security Group rules don't block the following communication ports 443, 53, 9354, 445, 12000.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-118">Ensure that your Azure Virtual Network (VNET) Network Security Group rules don't block the following communication ports 443, 53, 9354, 445, 12000.</span></span> <span data-ttu-id="f4fa3-119">For more detail on Azure VNET NSG traffic filtering, see the article [Filter network traffic with network security groups](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg).</span><span class="sxs-lookup"><span data-stu-id="f4fa3-119">For more detail on Azure VNET NSG traffic filtering, see the article [Filter network traffic with network security groups](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg).</span></span>
- <span data-ttu-id="f4fa3-120">Configure your [Windows Firewall for source database engine access](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access).</span><span class="sxs-lookup"><span data-stu-id="f4fa3-120">Configure your [Windows Firewall for source database engine access](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access).</span></span>
- <span data-ttu-id="f4fa3-121">Open your Windows Firewall to allow the Azure Database Migration Service to access the source SQL Server, which by default is TCP port 1433.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-121">Open your Windows Firewall to allow the Azure Database Migration Service to access the source SQL Server, which by default is TCP port 1433.</span></span>
- <span data-ttu-id="f4fa3-122">If you're running multiple named SQL Server instances using dynamic ports, you may wish to enable the SQL Browser Service and allow access to UDP port 1434 through your firewalls so that the Azure Database Migration Service can connect to a named instance on your source server.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-122">If you're running multiple named SQL Server instances using dynamic ports, you may wish to enable the SQL Browser Service and allow access to UDP port 1434 through your firewalls so that the Azure Database Migration Service can connect to a named instance on your source server.</span></span>
- <span data-ttu-id="f4fa3-123">If you're using a firewall appliance in front of your source databases, you may need to add firewall rules to allow the Azure Database Migration Service to access the source database(s) for migration, as well as files via SMB port 445.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-123">If you're using a firewall appliance in front of your source databases, you may need to add firewall rules to allow the Azure Database Migration Service to access the source database(s) for migration, as well as files via SMB port 445.</span></span>
- <span data-ttu-id="f4fa3-124">Create an Azure SQL Database Managed Instance by following the detail in the article [Create an Azure SQL Database Managed Instance in the Azure portal](https://aka.ms/sqldbmi).</span><span class="sxs-lookup"><span data-stu-id="f4fa3-124">Create an Azure SQL Database Managed Instance by following the detail in the article [Create an Azure SQL Database Managed Instance in the Azure portal](https://aka.ms/sqldbmi).</span></span>
- <span data-ttu-id="f4fa3-125">Ensure that the logins used to connect the source SQL Server and target Managed Instance are members of the sysadmin server role.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-125">Ensure that the logins used to connect the source SQL Server and target Managed Instance are members of the sysadmin server role.</span></span>
- <span data-ttu-id="f4fa3-126">Create a network share that the Azure Database Migration Service can use to back up the source database.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-126">Create a network share that the Azure Database Migration Service can use to back up the source database.</span></span>
- <span data-ttu-id="f4fa3-127">Ensure that the service account running the source SQL Server instance has write privileges on the network share that you created and that the computer account for the source server has read/write access to the same share.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-127">Ensure that the service account running the source SQL Server instance has write privileges on the network share that you created and that the computer account for the source server has read/write access to the same share.</span></span>
- <span data-ttu-id="f4fa3-128">Make a note of a Windows user (and password) that has full control privilege on the network share that you previously created.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-128">Make a note of a Windows user (and password) that has full control privilege on the network share that you previously created.</span></span> <span data-ttu-id="f4fa3-129">The Azure Database Migration Service impersonates the user credential to upload the backup files to Azure storage container for restore operation.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-129">The Azure Database Migration Service impersonates the user credential to upload the backup files to Azure storage container for restore operation.</span></span>
- <span data-ttu-id="f4fa3-130">Create a blob container and retrieve its SAS URI by using the steps in the article [Manage Azure Blob Storage resources with Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs#get-the-sas-for-a-blob-container), be sure to select all permissions (Read, Write, Delete, List) on the policy window while creating the SAS URI.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-130">Create a blob container and retrieve its SAS URI by using the steps in the article [Manage Azure Blob Storage resources with Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs#get-the-sas-for-a-blob-container), be sure to select all permissions (Read, Write, Delete, List) on the policy window while creating the SAS URI.</span></span> <span data-ttu-id="f4fa3-131">This detail provides the Azure Database Migration Service with access to your storage account container for uploading the backup files used for migrating databases to Azure SQL Database Managed Instance.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-131">This detail provides the Azure Database Migration Service with access to your storage account container for uploading the backup files used for migrating databases to Azure SQL Database Managed Instance.</span></span>

## <a name="register-the-microsoftdatamigration-resource-provider"></a><span data-ttu-id="f4fa3-132">Register the Microsoft.DataMigration resource provider</span><span class="sxs-lookup"><span data-stu-id="f4fa3-132">Register the Microsoft.DataMigration resource provider</span></span>

1. <span data-ttu-id="f4fa3-133">Sign in to the Azure portal, select **All services**, and then select **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-133">Sign in to the Azure portal, select **All services**, and then select **Subscriptions**.</span></span>

    ![Show portal subscriptions](media\tutorial-sql-server-to-managed-instance\portal-select-subscriptions.png)        

2. <span data-ttu-id="f4fa3-135">Select the subscription in which you want to create the instance of the Azure Database Migration Service, and then select **Resource providers**.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-135">Select the subscription in which you want to create the instance of the Azure Database Migration Service, and then select **Resource providers**.</span></span>

    ![Show resource providers](media\tutorial-sql-server-to-managed-instance\portal-select-resource-provider.png)

3. <span data-ttu-id="f4fa3-137">Search for migration, and then to the right of **Microsoft.DataMigration**, select **Register**.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-137">Search for migration, and then to the right of **Microsoft.DataMigration**, select **Register**.</span></span>

    ![Register resource provider](media\tutorial-sql-server-to-managed-instance\portal-register-resource-provider.png)   

## <a name="create-an-azure-database-migration-service-instance"></a><span data-ttu-id="f4fa3-139">Create an Azure Database Migration Service instance</span><span class="sxs-lookup"><span data-stu-id="f4fa3-139">Create an Azure Database Migration Service instance</span></span>

1. <span data-ttu-id="f4fa3-140">In the Azure portal, select + **Create a resource**, search for **Azure Database Migration Service**, and then select **Azure Database Migration Service** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-140">In the Azure portal, select + **Create a resource**, search for **Azure Database Migration Service**, and then select **Azure Database Migration Service** from the drop-down list.</span></span>

     ![Azure Marketplace](media\tutorial-sql-server-to-managed-instance\portal-marketplace.png)

2. <span data-ttu-id="f4fa3-142">On the **Azure Database Migration Service** screen, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-142">On the **Azure Database Migration Service** screen, select **Create**.</span></span>

    ![Create Azure Database Migration Service instance](media\tutorial-sql-server-to-managed-instance\dms-create1.png)

3. <span data-ttu-id="f4fa3-144">On the **Create Migration Service** screen, specify a name for the service, the subscription, and a new or existing resource group.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-144">On the **Create Migration Service** screen, specify a name for the service, the subscription, and a new or existing resource group.</span></span>

4.  <span data-ttu-id="f4fa3-145">Select the location in which you want to create the instance of DMS.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-145">Select the location in which you want to create the instance of DMS.</span></span>

5. <span data-ttu-id="f4fa3-146">Select an existing virtual network (VNET) or create one.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-146">Select an existing virtual network (VNET) or create one.</span></span>
 
    <span data-ttu-id="f4fa3-147">The VNET provides the Azure Database Migration Service with access to the source SQL Server and target Azure SQL Database Managed Instance.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-147">The VNET provides the Azure Database Migration Service with access to the source SQL Server and target Azure SQL Database Managed Instance.</span></span>

    <span data-ttu-id="f4fa3-148">For more information on how to create a VNET in Azure portal, see the article [Create a virtual network using the Azure portal](https://aka.ms/DMSVnet).</span><span class="sxs-lookup"><span data-stu-id="f4fa3-148">For more information on how to create a VNET in Azure portal, see the article [Create a virtual network using the Azure portal](https://aka.ms/DMSVnet).</span></span>

    <span data-ttu-id="f4fa3-149">For additional detail, see the article [Network topologies for Azure SQL DB Managed Instance migrations using the Azure Database Migration Service](https://aka.ms/dmsnetworkformi).</span><span class="sxs-lookup"><span data-stu-id="f4fa3-149">For additional detail, see the article [Network topologies for Azure SQL DB Managed Instance migrations using the Azure Database Migration Service](https://aka.ms/dmsnetworkformi).</span></span>

6. <span data-ttu-id="f4fa3-150">Select a pricing tier.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-150">Select a pricing tier.</span></span>

    <span data-ttu-id="f4fa3-151">For more information on costs and pricing tiers, see the [pricing page](https://aka.ms/dms-pricing).</span><span class="sxs-lookup"><span data-stu-id="f4fa3-151">For more information on costs and pricing tiers, see the [pricing page](https://aka.ms/dms-pricing).</span></span>
   
    ![Create DMS Service](media\tutorial-sql-server-to-managed-instance\dms-create-service2.png)

7.  <span data-ttu-id="f4fa3-153">Select **Create** to create the service.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-153">Select **Create** to create the service.</span></span>

## <a name="create-a-migration-project"></a><span data-ttu-id="f4fa3-154">Create a migration project</span><span class="sxs-lookup"><span data-stu-id="f4fa3-154">Create a migration project</span></span>

<span data-ttu-id="f4fa3-155">After an instance of the service is created, locate it within the Azure portal, open it, and then create a new migration project.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-155">After an instance of the service is created, locate it within the Azure portal, open it, and then create a new migration project.</span></span>

1. <span data-ttu-id="f4fa3-156">In the Azure portal, select **All services**, search for Azure Database Migration Service, and then select **Azure Database Migration Services**.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-156">In the Azure portal, select **All services**, search for Azure Database Migration Service, and then select **Azure Database Migration Services**.</span></span>

    ![Locate all instances of the Azure Database Migration Service](media\tutorial-sql-server-to-managed-instance\dms-search.png)

2. <span data-ttu-id="f4fa3-158">On the **Azure Database Migration Service screen**, search for the name of the instance that you created, and then select the instance.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-158">On the **Azure Database Migration Service screen**, search for the name of the instance that you created, and then select the instance.</span></span>
 
3. <span data-ttu-id="f4fa3-159">Select + **New Migration Project**.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-159">Select + **New Migration Project**.</span></span>

4. <span data-ttu-id="f4fa3-160">On the **New migration project** screen, specify a name for the project, in the **Source server type** text box, select **SQL Server**, in the **Target server type** text box, select **Azure SQL Database Managed Instance**, and then for **Choose type of activity**, select **Offline data migration**.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-160">On the **New migration project** screen, specify a name for the project, in the **Source server type** text box, select **SQL Server**, in the **Target server type** text box, select **Azure SQL Database Managed Instance**, and then for **Choose type of activity**, select **Offline data migration**.</span></span>

   ![Create DMS Project](media\tutorial-sql-server-to-managed-instance\dms-create-project2.png)

5. <span data-ttu-id="f4fa3-162">Select **Create** to create the project.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-162">Select **Create** to create the project.</span></span>

## <a name="specify-source-details"></a><span data-ttu-id="f4fa3-163">Specify source details</span><span class="sxs-lookup"><span data-stu-id="f4fa3-163">Specify source details</span></span>

1. <span data-ttu-id="f4fa3-164">On the **Migration source detail** screen, specify the connection details for the source SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-164">On the **Migration source detail** screen, specify the connection details for the source SQL Server.</span></span>

2. <span data-ttu-id="f4fa3-165">If you haven't installed a trusted certificate on your server, select the **Trust server certificate** check box.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-165">If you haven't installed a trusted certificate on your server, select the **Trust server certificate** check box.</span></span>

    <span data-ttu-id="f4fa3-166">When a trusted certificate isn't installed, SQL Server generates a self-signed certificate when the instance is started.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-166">When a trusted certificate isn't installed, SQL Server generates a self-signed certificate when the instance is started.</span></span> <span data-ttu-id="f4fa3-167">This certificate is used to encrypt the credentials for client connections.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-167">This certificate is used to encrypt the credentials for client connections.</span></span>

    > [!CAUTION]
    > <span data-ttu-id="f4fa3-168">SSL connections that are encrypted using a self-signed certificate does not provide strong security.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-168">SSL connections that are encrypted using a self-signed certificate does not provide strong security.</span></span> <span data-ttu-id="f4fa3-169">They are susceptible to man-in-the-middle attacks.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-169">They are susceptible to man-in-the-middle attacks.</span></span> <span data-ttu-id="f4fa3-170">You should not rely on SSL using self-signed certificates in a production environment or on servers that are connected to the internet.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-170">You should not rely on SSL using self-signed certificates in a production environment or on servers that are connected to the internet.</span></span>

   ![Source Details](media\tutorial-sql-server-to-managed-instance\dms-source-details1.png)

3. <span data-ttu-id="f4fa3-172">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-172">Select **Save**.</span></span>

4. <span data-ttu-id="f4fa3-173">On the **Select source databases** screen, select the **Adventureworks2012** database for migration.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-173">On the **Select source databases** screen, select the **Adventureworks2012** database for migration.</span></span>

   ![Select Source Databases](media\tutorial-sql-server-to-managed-instance\dms-source-database1.png)

5. <span data-ttu-id="f4fa3-175">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-175">Select **Save**.</span></span>

## <a name="specify-target-details"></a><span data-ttu-id="f4fa3-176">Specify target details</span><span class="sxs-lookup"><span data-stu-id="f4fa3-176">Specify target details</span></span>

1.  <span data-ttu-id="f4fa3-177">On the **Migration target details** screen, specify the connection details for the target, which is the pre-provisioned Azure SQL Database Managed Instance to which you are migrating the **AdventureWorks2012** database.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-177">On the **Migration target details** screen, specify the connection details for the target, which is the pre-provisioned Azure SQL Database Managed Instance to which you are migrating the **AdventureWorks2012** database.</span></span>

    <span data-ttu-id="f4fa3-178">If you have not already provisioned the Azure SQL Database Managed Instance, select **No** for a link to help you provision the instance.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-178">If you have not already provisioned the Azure SQL Database Managed Instance, select **No** for a link to help you provision the instance.</span></span> <span data-ttu-id="f4fa3-179">You can still proceed with project creation and then, when the Azure SQL Database Managed Instance is ready, return to this specific project to execute the migration.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-179">You can still proceed with project creation and then, when the Azure SQL Database Managed Instance is ready, return to this specific project to execute the migration.</span></span>   
 
       ![Select Target](media\tutorial-sql-server-to-managed-instance\dms-target-details2.png)

2.  <span data-ttu-id="f4fa3-181">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-181">Select **Save**.</span></span>

## <a name="select-source-databases"></a><span data-ttu-id="f4fa3-182">Select source databases</span><span class="sxs-lookup"><span data-stu-id="f4fa3-182">Select source databases</span></span>

1. <span data-ttu-id="f4fa3-183">On the **Select source databases** screen, select the source database that you want to migrate.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-183">On the **Select source databases** screen, select the source database that you want to migrate.</span></span>

    ![Select source databases](media\tutorial-sql-server-to-managed-instance\select-source-databases.png)

2. <span data-ttu-id="f4fa3-185">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-185">Select **Save**.</span></span>

## <a name="select-logins"></a><span data-ttu-id="f4fa3-186">Select logins</span><span class="sxs-lookup"><span data-stu-id="f4fa3-186">Select logins</span></span>
 
1. <span data-ttu-id="f4fa3-187">On the **Select logins** screen, select the logins that you want to migrate.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-187">On the **Select logins** screen, select the logins that you want to migrate.</span></span>

    >[!NOTE]
    ><span data-ttu-id="f4fa3-188">This release only supports migrating the SQL logins.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-188">This release only supports migrating the SQL logins.</span></span>

    ![Select logins](media\tutorial-sql-server-to-managed-instance\select-logins.png)

2. <span data-ttu-id="f4fa3-190">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-190">Select **Save**.</span></span>
 
## <a name="configure-migration-settings"></a><span data-ttu-id="f4fa3-191">Configure migration settings</span><span class="sxs-lookup"><span data-stu-id="f4fa3-191">Configure migration settings</span></span>
 
1. <span data-ttu-id="f4fa3-192">On the **Configure migration settings** screen, provide the following detail:</span><span class="sxs-lookup"><span data-stu-id="f4fa3-192">On the **Configure migration settings** screen, provide the following detail:</span></span>

    | | |
    |--------|---------|
    |<span data-ttu-id="f4fa3-193">**Choose source backup option**</span><span class="sxs-lookup"><span data-stu-id="f4fa3-193">**Choose source backup option**</span></span> | <span data-ttu-id="f4fa3-194">Choose the option **I will provide latest backup files** when you already have a full backup files available for DMS to use for database migration.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-194">Choose the option **I will provide latest backup files** when you already have a full backup files available for DMS to use for database migration.</span></span> <span data-ttu-id="f4fa3-195">Choose the option **I will let Azure Database Migration Service create backup files** when you want DMS to take the source database full backup at first and use it for migration.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-195">Choose the option **I will let Azure Database Migration Service create backup files** when you want DMS to take the source database full backup at first and use it for migration.</span></span> |
    |<span data-ttu-id="f4fa3-196">**Network location share**</span><span class="sxs-lookup"><span data-stu-id="f4fa3-196">**Network location share**</span></span> | <span data-ttu-id="f4fa3-197">The local SMB network share that the Azure Database Migration Service can take the source database backups to.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-197">The local SMB network share that the Azure Database Migration Service can take the source database backups to.</span></span> <span data-ttu-id="f4fa3-198">The service account running source SQL Server instance must have write privileges on this network share.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-198">The service account running source SQL Server instance must have write privileges on this network share.</span></span> <span data-ttu-id="f4fa3-199">Provide an FQDN or IP addresses of the server in the network share, for example, '\\\servername.domainname.com\backupfolder' or '\\\IP address\backupfolder'.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-199">Provide an FQDN or IP addresses of the server in the network share, for example, '\\\servername.domainname.com\backupfolder' or '\\\IP address\backupfolder'.</span></span>|
    |<span data-ttu-id="f4fa3-200">**User name**</span><span class="sxs-lookup"><span data-stu-id="f4fa3-200">**User name**</span></span> | <span data-ttu-id="f4fa3-201">Make sure that the Windows user has full control privilege on the network share that you provided above.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-201">Make sure that the Windows user has full control privilege on the network share that you provided above.</span></span> <span data-ttu-id="f4fa3-202">The Azure Database Migration Service will impersonate the user credential to upload the backup files to Azure storage container for restore operation.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-202">The Azure Database Migration Service will impersonate the user credential to upload the backup files to Azure storage container for restore operation.</span></span> <span data-ttu-id="f4fa3-203">If TDE-enabled databases are selected for migration, the above windows user must be the built-in administrator account and [User Account Control](https://docs.microsoft.com/windows/security/identity-protection/user-account-control/user-account-control-overview) must be disabled for Azure Database Migration Service to upload and delete the certificates files.)</span><span class="sxs-lookup"><span data-stu-id="f4fa3-203">If TDE-enabled databases are selected for migration, the above windows user must be the built-in administrator account and [User Account Control](https://docs.microsoft.com/windows/security/identity-protection/user-account-control/user-account-control-overview) must be disabled for Azure Database Migration Service to upload and delete the certificates files.)</span></span> |
    |<span data-ttu-id="f4fa3-204">**Password**</span><span class="sxs-lookup"><span data-stu-id="f4fa3-204">**Password**</span></span> | <span data-ttu-id="f4fa3-205">Password for the user.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-205">Password for the user.</span></span> |
    |<span data-ttu-id="f4fa3-206">**Storage account settings**</span><span class="sxs-lookup"><span data-stu-id="f4fa3-206">**Storage account settings**</span></span> | <span data-ttu-id="f4fa3-207">The SAS URI that provides the Azure Database Migration Service with access to your storage account container to which the service uploads the back-up files and that is used for migrating databases to Azure SQL Database Managed Instance.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-207">The SAS URI that provides the Azure Database Migration Service with access to your storage account container to which the service uploads the back-up files and that is used for migrating databases to Azure SQL Database Managed Instance.</span></span> <span data-ttu-id="f4fa3-208">[Learn how to get the SAS URI for blob container](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs#get-the-sas-for-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="f4fa3-208">[Learn how to get the SAS URI for blob container](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs#get-the-sas-for-a-blob-container).</span></span>|
    |<span data-ttu-id="f4fa3-209">**TDE Settings**</span><span class="sxs-lookup"><span data-stu-id="f4fa3-209">**TDE Settings**</span></span> | <span data-ttu-id="f4fa3-210">If you are migrating the source databases with Transparent Data Encryption (TDE) enabled, you need to have write privileges on the target Azure SQL DB Managed Instance.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-210">If you are migrating the source databases with Transparent Data Encryption (TDE) enabled, you need to have write privileges on the target Azure SQL DB Managed Instance.</span></span>  <span data-ttu-id="f4fa3-211">Select the subscription in which the Azure SQL DB Managed Instance provisioned from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-211">Select the subscription in which the Azure SQL DB Managed Instance provisioned from the drop-down menu.</span></span>  <span data-ttu-id="f4fa3-212">Select the target Azure SQL DB Managed Instance in the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-212">Select the target Azure SQL DB Managed Instance in the drop-down menu.</span></span> |
    
    ![Configure Migration Settings](media\tutorial-sql-server-to-managed-instance\dms-configure-migration-settings3.png)

2. <span data-ttu-id="f4fa3-214">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-214">Select **Save**.</span></span>
 
## <a name="review-the-migration-summary"></a><span data-ttu-id="f4fa3-215">Review the migration summary</span><span class="sxs-lookup"><span data-stu-id="f4fa3-215">Review the migration summary</span></span>

1. <span data-ttu-id="f4fa3-216">On the **Migration summary** screen, in the **Activity name** text box, specify a name for the migration activity.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-216">On the **Migration summary** screen, in the **Activity name** text box, specify a name for the migration activity.</span></span>

2. <span data-ttu-id="f4fa3-217">Expand the **Validation option** section to display the **Choose validation option** screen, specify whether to validate the migrated database for query correctness, and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-217">Expand the **Validation option** section to display the **Choose validation option** screen, specify whether to validate the migrated database for query correctness, and then select **Save**.</span></span>

3. <span data-ttu-id="f4fa3-218">Review and verify the details associated with the migration project.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-218">Review and verify the details associated with the migration project.</span></span>
 
    ![Migration project summary](media\tutorial-sql-server-to-managed-instance\dms-project-summary2.png)

4.  <span data-ttu-id="f4fa3-220">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-220">Select **Save**.</span></span>   

## <a name="run-the-migration"></a><span data-ttu-id="f4fa3-221">Run the migration</span><span class="sxs-lookup"><span data-stu-id="f4fa3-221">Run the migration</span></span>

- <span data-ttu-id="f4fa3-222">Select **Run migration**.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-222">Select **Run migration**.</span></span>

  <span data-ttu-id="f4fa3-223">The migration activity window appears, and the status of the activity is **Pending**.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-223">The migration activity window appears, and the status of the activity is **Pending**.</span></span>

## <a name="monitor-the-migration"></a><span data-ttu-id="f4fa3-224">Monitor the migration</span><span class="sxs-lookup"><span data-stu-id="f4fa3-224">Monitor the migration</span></span>

1. <span data-ttu-id="f4fa3-225">In the migration activity screen, select **Refresh** to update the display.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-225">In the migration activity screen, select **Refresh** to update the display.</span></span>
 
   ![Migration activity in progress](media\tutorial-sql-server-to-managed-instance\dms-monitor-migration1.png)

    <span data-ttu-id="f4fa3-227">You can further expand the databases and logins categories to monitor the migration status of the respective server objects.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-227">You can further expand the databases and logins categories to monitor the migration status of the respective server objects.</span></span>

   ![Migration activity in progress](media\tutorial-sql-server-to-managed-instance\dms-monitor-migration-extend.png)

2. <span data-ttu-id="f4fa3-229">After the migration completes, select **Download report** to get a report listing the details associated with the migration process.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-229">After the migration completes, select **Download report** to get a report listing the details associated with the migration process.</span></span>
 
3. <span data-ttu-id="f4fa3-230">Verify that the target database on the target Azure SQL Database Managed Instance environment.</span><span class="sxs-lookup"><span data-stu-id="f4fa3-230">Verify that the target database on the target Azure SQL Database Managed Instance environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4fa3-231">Next steps</span><span class="sxs-lookup"><span data-stu-id="f4fa3-231">Next steps</span></span>

- <span data-ttu-id="f4fa3-232">For a tutorial showing you how to migrate a database to a Managed Instance using the T-SQL RESTORE command, see [Restore a backup to a Managed Instance using the restore command](../sql-database/sql-database-managed-instance-restore-from-backup-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="f4fa3-232">For a tutorial showing you how to migrate a database to a Managed Instance using the T-SQL RESTORE command, see [Restore a backup to a Managed Instance using the restore command](../sql-database/sql-database-managed-instance-restore-from-backup-tutorial.md).</span></span>
- <span data-ttu-id="f4fa3-233">For information about Managed Instance, see [What is a Managed Instance](../sql-database/sql-database-managed-instance.md).</span><span class="sxs-lookup"><span data-stu-id="f4fa3-233">For information about Managed Instance, see [What is a Managed Instance](../sql-database/sql-database-managed-instance.md).</span></span>
- <span data-ttu-id="f4fa3-234">For information about connecting apps to a Managed Instance, see [Connect applications](../sql-database/sql-database-managed-instance-connect-app.md).</span><span class="sxs-lookup"><span data-stu-id="f4fa3-234">For information about connecting apps to a Managed Instance, see [Connect applications](../sql-database/sql-database-managed-instance-connect-app.md).</span></span>