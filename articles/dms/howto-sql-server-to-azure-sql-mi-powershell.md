---
title: Use Azure Database Migration Service module in Microsoft Azure PowerShell to migrate SQL Server on-premises to Azure SQL DB MI | Microsoft Docs
description: Learn to migrate from on-premises SQL Server to Azure SQL DB MI by using Azure PowerShell.
services: database-migration
author: HJToland3
ms.author: jtoland
manager: ''
ms.reviewer: ''
ms.service: database-migration
ms.workload: data-services
ms.custom: mvc
ms.topic: article
ms.date: 08/13/2018
ms.openlocfilehash: 7bd7e7a4cb78cf8a9f818936c980b47a2e7865e7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870290"
---
# <a name="migrate-sql-server-on-premises-to-azure-sql-db-using-azure-powershell"></a><span data-ttu-id="5b478-103">Migrate SQL Server on-premises to Azure SQL DB using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b478-103">Migrate SQL Server on-premises to Azure SQL DB using Azure PowerShell</span></span>
<span data-ttu-id="5b478-104">In this article, you migrate the **Adventureworks2012** database restored to an on-premises instance of SQL Server 2005 or above to an Azure SQL Database by using Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b478-104">In this article, you migrate the **Adventureworks2012** database restored to an on-premises instance of SQL Server 2005 or above to an Azure SQL Database by using Microsoft Azure PowerShell.</span></span> <span data-ttu-id="5b478-105">You can migrate databases from an on-premises SQL Server instance to Azure SQL Database by using the `AzureRM.DataMigration` module in Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b478-105">You can migrate databases from an on-premises SQL Server instance to Azure SQL Database by using the `AzureRM.DataMigration` module in Microsoft Azure PowerShell.</span></span>

<span data-ttu-id="5b478-106">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="5b478-106">In this article, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="5b478-107">Create a resource group.</span><span class="sxs-lookup"><span data-stu-id="5b478-107">Create a resource group.</span></span>
> * <span data-ttu-id="5b478-108">Create an instance of the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="5b478-108">Create an instance of the Azure Database Migration Service.</span></span>
> * <span data-ttu-id="5b478-109">Create a migration project in an Azure Database Migration Service instance.</span><span class="sxs-lookup"><span data-stu-id="5b478-109">Create a migration project in an Azure Database Migration Service instance.</span></span>
> * <span data-ttu-id="5b478-110">Run the migration.</span><span class="sxs-lookup"><span data-stu-id="5b478-110">Run the migration.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b478-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5b478-111">Prerequisites</span></span>
<span data-ttu-id="5b478-112">To complete these steps, you need:</span><span class="sxs-lookup"><span data-stu-id="5b478-112">To complete these steps, you need:</span></span>

- <span data-ttu-id="5b478-113">[SQL Server 2016 or above](https://www.microsoft.com/sql-server/sql-server-downloads) (any edition)</span><span class="sxs-lookup"><span data-stu-id="5b478-113">[SQL Server 2016 or above](https://www.microsoft.com/sql-server/sql-server-downloads) (any edition)</span></span>
- <span data-ttu-id="5b478-114">To enable the TCP/IP protocol, which is disabled by default with SQL Server Express installation.</span><span class="sxs-lookup"><span data-stu-id="5b478-114">To enable the TCP/IP protocol, which is disabled by default with SQL Server Express installation.</span></span> <span data-ttu-id="5b478-115">Enable the TCP/IP protocol by following the article [Enable or Disable a Server Network Protocol](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-or-disable-a-server-network-protocol#SSMSProcedure).</span><span class="sxs-lookup"><span data-stu-id="5b478-115">Enable the TCP/IP protocol by following the article [Enable or Disable a Server Network Protocol](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-or-disable-a-server-network-protocol#SSMSProcedure).</span></span>
- <span data-ttu-id="5b478-116">To configure your [Windows Firewall for database engine access](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access).</span><span class="sxs-lookup"><span data-stu-id="5b478-116">To configure your [Windows Firewall for database engine access](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access).</span></span>
- <span data-ttu-id="5b478-117">An Azure SQL Database instance.</span><span class="sxs-lookup"><span data-stu-id="5b478-117">An Azure SQL Database instance.</span></span> <span data-ttu-id="5b478-118">You can create an Azure SQL Database instance by following the detail in the article [Create an Azure SQL database in the Azure portal](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="5b478-118">You can create an Azure SQL Database instance by following the detail in the article [Create an Azure SQL database in the Azure portal](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal).</span></span>
- <span data-ttu-id="5b478-119">[Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) v3.3 or later.</span><span class="sxs-lookup"><span data-stu-id="5b478-119">[Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) v3.3 or later.</span></span>
- <span data-ttu-id="5b478-120">To have created a VNET by using the Azure Resource Manager deployment model, which provides the Azure Database Migration Service with site-to-site connectivity to your on-premises source servers by using either [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) or [VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).</span><span class="sxs-lookup"><span data-stu-id="5b478-120">To have created a VNET by using the Azure Resource Manager deployment model, which provides the Azure Database Migration Service with site-to-site connectivity to your on-premises source servers by using either [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) or [VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).</span></span>
- <span data-ttu-id="5b478-121">To have completed assessment of your on-premises database and schema migration using Data Migration Assistant as described in the article [ Performing a SQL Server migration assessment](https://docs.microsoft.com/sql/dma/dma-assesssqlonprem)</span><span class="sxs-lookup"><span data-stu-id="5b478-121">To have completed assessment of your on-premises database and schema migration using Data Migration Assistant as described in the article [ Performing a SQL Server migration assessment](https://docs.microsoft.com/sql/dma/dma-assesssqlonprem)</span></span>
- <span data-ttu-id="5b478-122">To download and install the AzureRM.DataMigration module from the PowerShell Gallery by using [Install-Module PowerShell cmdlet](https://docs.microsoft.com/powershell/module/powershellget/Install-Module?view=powershell-5.1)</span><span class="sxs-lookup"><span data-stu-id="5b478-122">To download and install the AzureRM.DataMigration module from the PowerShell Gallery by using [Install-Module PowerShell cmdlet](https://docs.microsoft.com/powershell/module/powershellget/Install-Module?view=powershell-5.1)</span></span>
- <span data-ttu-id="5b478-123">To ensure that the credentials used to connect to source SQL Server instance has the [CONTROL SERVER](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql) permission.</span><span class="sxs-lookup"><span data-stu-id="5b478-123">To ensure that the credentials used to connect to source SQL Server instance has the [CONTROL SERVER](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql) permission.</span></span>
- <span data-ttu-id="5b478-124">To ensure that the credentials used to connect to target Azure SQL DB instance has the CONTROL DATABASE permission on the target Azure SQL Database databases.</span><span class="sxs-lookup"><span data-stu-id="5b478-124">To ensure that the credentials used to connect to target Azure SQL DB instance has the CONTROL DATABASE permission on the target Azure SQL Database databases.</span></span>
- <span data-ttu-id="5b478-125">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5b478-125">An Azure subscription.</span></span> <span data-ttu-id="5b478-126">If you don't have one, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="5b478-126">If you don't have one, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-to-your-microsoft-azure-subscription"></a><span data-ttu-id="5b478-127">Log in to your Microsoft Azure subscription</span><span class="sxs-lookup"><span data-stu-id="5b478-127">Log in to your Microsoft Azure subscription</span></span>
<span data-ttu-id="5b478-128">Use the directions in the article [Log in with Azure PowerShell](https://docs.microsoft.com/powershell/azure/authenticate-azureps?view=azurermps-4.4.1) to log in to your Azure subscription by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b478-128">Use the directions in the article [Log in with Azure PowerShell](https://docs.microsoft.com/powershell/azure/authenticate-azureps?view=azurermps-4.4.1) to log in to your Azure subscription by using PowerShell.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="5b478-129">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="5b478-129">Create a resource group</span></span>
<span data-ttu-id="5b478-130">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="5b478-130">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="5b478-131">Create a resource group before you can create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5b478-131">Create a resource group before you can create a virtual machine.</span></span>

<span data-ttu-id="5b478-132">Create a resource group by using the [New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup?view=azurermps-4.4.1) command.</span><span class="sxs-lookup"><span data-stu-id="5b478-132">Create a resource group by using the [New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup?view=azurermps-4.4.1) command.</span></span> 

<span data-ttu-id="5b478-133">The following example creates a resource group named *myResourceGroup* in the *EastUS* region.</span><span class="sxs-lookup"><span data-stu-id="5b478-133">The following example creates a resource group named *myResourceGroup* in the *EastUS* region.</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location EastUS
```
## <a name="create-an-instance-of-the-azure-database-migration-service"></a><span data-ttu-id="5b478-134">Create an instance of the Azure Database Migration Service</span><span class="sxs-lookup"><span data-stu-id="5b478-134">Create an instance of the Azure Database Migration Service</span></span> 
<span data-ttu-id="5b478-135">You can create new instance of Azure Database Migration Service by using the `New-AzureRmDataMigrationService` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b478-135">You can create new instance of Azure Database Migration Service by using the `New-AzureRmDataMigrationService` cmdlet.</span></span> <span data-ttu-id="5b478-136">This cmdlet expects the following required parameters:</span><span class="sxs-lookup"><span data-stu-id="5b478-136">This cmdlet expects the following required parameters:</span></span>
- <span data-ttu-id="5b478-137">*Azure Resource Group name*.</span><span class="sxs-lookup"><span data-stu-id="5b478-137">*Azure Resource Group name*.</span></span> <span data-ttu-id="5b478-138">You can use [New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup?view=azurermps-4.4.1) command to create Azure Resource group as previously shown and provide its name as a parameter.</span><span class="sxs-lookup"><span data-stu-id="5b478-138">You can use [New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup?view=azurermps-4.4.1) command to create Azure Resource group as previously shown and provide its name as a parameter.</span></span>
- <span data-ttu-id="5b478-139">*Service name*.</span><span class="sxs-lookup"><span data-stu-id="5b478-139">*Service name*.</span></span> <span data-ttu-id="5b478-140">String that corresponds to the desired unique service name for Azure Database Migration Service</span><span class="sxs-lookup"><span data-stu-id="5b478-140">String that corresponds to the desired unique service name for Azure Database Migration Service</span></span> 
- <span data-ttu-id="5b478-141">*Location*.</span><span class="sxs-lookup"><span data-stu-id="5b478-141">*Location*.</span></span> <span data-ttu-id="5b478-142">Specifies the location of the service.</span><span class="sxs-lookup"><span data-stu-id="5b478-142">Specifies the location of the service.</span></span> <span data-ttu-id="5b478-143">Specify an Azure data center location, such as West US or Southeast Asia</span><span class="sxs-lookup"><span data-stu-id="5b478-143">Specify an Azure data center location, such as West US or Southeast Asia</span></span>
- <span data-ttu-id="5b478-144">*Sku*.</span><span class="sxs-lookup"><span data-stu-id="5b478-144">*Sku*.</span></span> <span data-ttu-id="5b478-145">This parameter corresponds to DMS Sku name.</span><span class="sxs-lookup"><span data-stu-id="5b478-145">This parameter corresponds to DMS Sku name.</span></span> <span data-ttu-id="5b478-146">Currently supported Sku names are *Basic_1vCore*, *Basic_2vCores*, *GeneralPurpose_4vCores*</span><span class="sxs-lookup"><span data-stu-id="5b478-146">Currently supported Sku names are *Basic_1vCore*, *Basic_2vCores*, *GeneralPurpose_4vCores*</span></span>
- <span data-ttu-id="5b478-147">*Virtual Subnet Identifier*.</span><span class="sxs-lookup"><span data-stu-id="5b478-147">*Virtual Subnet Identifier*.</span></span> <span data-ttu-id="5b478-148">You can use cmdlet [New-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig?view=azurermps-4.4.1) to create a subnet.</span><span class="sxs-lookup"><span data-stu-id="5b478-148">You can use cmdlet [New-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig?view=azurermps-4.4.1) to create a subnet.</span></span> 

<span data-ttu-id="5b478-149">The following example creates a service named *MyDMS* in the resource group *MyDMSResourceGroup* located in the *East US* region using a virtual network named *MyVNET* and  subnet called *MySubnet*.</span><span class="sxs-lookup"><span data-stu-id="5b478-149">The following example creates a service named *MyDMS* in the resource group *MyDMSResourceGroup* located in the *East US* region using a virtual network named *MyVNET* and  subnet called *MySubnet*.</span></span>

```powershell
 $vNet = Get-AzureRmVirtualNetwork -ResourceGroupName MyDMSResourceGroup -Name MyVNET

$vSubNet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vNet -Name MySubnet

$service = New-AzureRmDms -ResourceGroupName myResourceGroup `
  -ServiceName MyDMS `
  -Location EastUS `
  -Sku Basic_2vCores `  
  -VirtualSubnetId $vSubNet.Id`
```

## <a name="create-a-migration-project"></a><span data-ttu-id="5b478-150">Create a migration project</span><span class="sxs-lookup"><span data-stu-id="5b478-150">Create a migration project</span></span>
<span data-ttu-id="5b478-151">After creating an Azure Database Migration Service instance, create a migration project.</span><span class="sxs-lookup"><span data-stu-id="5b478-151">After creating an Azure Database Migration Service instance, create a migration project.</span></span> <span data-ttu-id="5b478-152">An Azure Database Migration Service project requires connection information for both the source and target instances, as well as a list of databases that you want to migrate as part of the project.</span><span class="sxs-lookup"><span data-stu-id="5b478-152">An Azure Database Migration Service project requires connection information for both the source and target instances, as well as a list of databases that you want to migrate as part of the project.</span></span>

### <a name="create-a-database-connection-info-object-for-the-source-and-target-connections"></a><span data-ttu-id="5b478-153">Create a Database Connection Info object for the source and target connections</span><span class="sxs-lookup"><span data-stu-id="5b478-153">Create a Database Connection Info object for the source and target connections</span></span>
<span data-ttu-id="5b478-154">You can create a Database Connection Info object by using the `New-AzureRmDmsConnInfo` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b478-154">You can create a Database Connection Info object by using the `New-AzureRmDmsConnInfo` cmdlet.</span></span> <span data-ttu-id="5b478-155">This cmdlet expects the following parameters:</span><span class="sxs-lookup"><span data-stu-id="5b478-155">This cmdlet expects the following parameters:</span></span>
- <span data-ttu-id="5b478-156">*ServerType*.</span><span class="sxs-lookup"><span data-stu-id="5b478-156">*ServerType*.</span></span> <span data-ttu-id="5b478-157">The type of database connection requested, for example, SQL, Oracle, or MySQL.</span><span class="sxs-lookup"><span data-stu-id="5b478-157">The type of database connection requested, for example, SQL, Oracle, or MySQL.</span></span> <span data-ttu-id="5b478-158">Use SQL for SQL Server and Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="5b478-158">Use SQL for SQL Server and Azure SQL.</span></span>
- <span data-ttu-id="5b478-159">*DataSource*.</span><span class="sxs-lookup"><span data-stu-id="5b478-159">*DataSource*.</span></span> <span data-ttu-id="5b478-160">The name or IP of a SQL Server instance or Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="5b478-160">The name or IP of a SQL Server instance or Azure SQL database.</span></span>
- <span data-ttu-id="5b478-161">*AuthType*.</span><span class="sxs-lookup"><span data-stu-id="5b478-161">*AuthType*.</span></span> <span data-ttu-id="5b478-162">The authentication type for connection, which can be either SqlAuthentication or WindowsAuthentication.</span><span class="sxs-lookup"><span data-stu-id="5b478-162">The authentication type for connection, which can be either SqlAuthentication or WindowsAuthentication.</span></span>
- <span data-ttu-id="5b478-163">*TrustServerCertificate* parameter sets a value that indicates whether the channel is encrypted while bypassing walking the certificate chain to validate trust.</span><span class="sxs-lookup"><span data-stu-id="5b478-163">*TrustServerCertificate* parameter sets a value that indicates whether the channel is encrypted while bypassing walking the certificate chain to validate trust.</span></span> <span data-ttu-id="5b478-164">Value can be true or false.</span><span class="sxs-lookup"><span data-stu-id="5b478-164">Value can be true or false.</span></span>

<span data-ttu-id="5b478-165">The following example creates Connection Info object for source SQL Server called MySourceSQLServer using sql authentication:</span><span class="sxs-lookup"><span data-stu-id="5b478-165">The following example creates Connection Info object for source SQL Server called MySourceSQLServer using sql authentication:</span></span> 

```powershell
$sourceConnInfo = New-AzureRmDmsConnInfo -ServerType SQL `
  -DataSource MySourceSQLServer `
  -AuthType SqlAuthentication `
  -TrustServerCertificate:$true
```

<span data-ttu-id="5b478-166">The next example shows creation of Connection Info for an Azure SQL Database Managed Instance server called ‘targetmanagedinstance.database.windows.net’ using sql authentication:</span><span class="sxs-lookup"><span data-stu-id="5b478-166">The next example shows creation of Connection Info for an Azure SQL Database Managed Instance server called ‘targetmanagedinstance.database.windows.net’ using sql authentication:</span></span>

```powershell
$targetConnInfo = New-AzureRmDmsConnInfo -ServerType SQL `
  -DataSource "targetmanagedinstance.database.windows.net" `
  -AuthType SqlAuthentication `
  -TrustServerCertificate:$false
```

### <a name="provide-databases-for-the-migration-project"></a><span data-ttu-id="5b478-167">Provide databases for the migration project</span><span class="sxs-lookup"><span data-stu-id="5b478-167">Provide databases for the migration project</span></span>
<span data-ttu-id="5b478-168">Create a list of `AzureRmDataMigrationDatabaseInfo` objects that specifies databases as part of the Azure Database Migration project that can be provided  as parameter for creation of the project.</span><span class="sxs-lookup"><span data-stu-id="5b478-168">Create a list of `AzureRmDataMigrationDatabaseInfo` objects that specifies databases as part of the Azure Database Migration project that can be provided  as parameter for creation of the project.</span></span> <span data-ttu-id="5b478-169">The Cmdlet `New-AzureRmDataMigrationDatabaseInfo` can be used to create AzureRmDataMigrationDatabaseInfo.</span><span class="sxs-lookup"><span data-stu-id="5b478-169">The Cmdlet `New-AzureRmDataMigrationDatabaseInfo` can be used to create AzureRmDataMigrationDatabaseInfo.</span></span> 

<span data-ttu-id="5b478-170">The following example creates `AzureRmDataMigrationDatabaseInfo` project for the **AdventureWorks** database and adds it to the list to be provided as parameter for project creation.</span><span class="sxs-lookup"><span data-stu-id="5b478-170">The following example creates `AzureRmDataMigrationDatabaseInfo` project for the **AdventureWorks** database and adds it to the list to be provided as parameter for project creation.</span></span>

```powershell
$dbInfo1 = New-AzureRmDataMigrationDatabaseInfo -SourceDatabaseName AdventureWorks
$dbList = @($dbInfo1)
```

### <a name="create-a-project-object"></a><span data-ttu-id="5b478-171">Create a project object</span><span class="sxs-lookup"><span data-stu-id="5b478-171">Create a project object</span></span>
<span data-ttu-id="5b478-172">Finally you can create Azure Database Migration project called *MyDMSProject* located in *East US* using `New-AzureRmDataMigrationProject` and adding the previously created source and target connections and the list of databases to migrate.</span><span class="sxs-lookup"><span data-stu-id="5b478-172">Finally you can create Azure Database Migration project called *MyDMSProject* located in *East US* using `New-AzureRmDataMigrationProject` and adding the previously created source and target connections and the list of databases to migrate.</span></span>

```powershell
$project = New-AzureRmDataMigrationProject -ResourceGroupName myResourceGroup `
  -ServiceName $service.Name `
  -ProjectName MyDMSProject `
  -Location EastUS `
  -SourceType SQL `
  -TargetType SQLMI `
  -SourceConnection $sourceConnInfo `
  -TargetConnection $targetConnInfo `
  -DatabaseInfo $dbList
```

## <a name="create-and-start-a-migration-task"></a><span data-ttu-id="5b478-173">Create and start a migration task</span><span class="sxs-lookup"><span data-stu-id="5b478-173">Create and start a migration task</span></span>
<span data-ttu-id="5b478-174">Finally, create and start Azure Database Migration task.</span><span class="sxs-lookup"><span data-stu-id="5b478-174">Finally, create and start Azure Database Migration task.</span></span> <span data-ttu-id="5b478-175">Azure Database Migration task requires connection credential information for both source and target and list of database tables to be migrated in addition to the information already provided with the project created as a prerequisite.</span><span class="sxs-lookup"><span data-stu-id="5b478-175">Azure Database Migration task requires connection credential information for both source and target and list of database tables to be migrated in addition to the information already provided with the project created as a prerequisite.</span></span> 

### <a name="create-credential-parameters-for-source-and-target"></a><span data-ttu-id="5b478-176">Create credential parameters for source and target</span><span class="sxs-lookup"><span data-stu-id="5b478-176">Create credential parameters for source and target</span></span>
<span data-ttu-id="5b478-177">Connection security credentials can be created as a [PSCredential](https://docs.microsoft.com/dotnet/api/system.management.automation.pscredential?redirectedfrom=MSDN&view=powershellsdk-1.1.0) object.</span><span class="sxs-lookup"><span data-stu-id="5b478-177">Connection security credentials can be created as a [PSCredential](https://docs.microsoft.com/dotnet/api/system.management.automation.pscredential?redirectedfrom=MSDN&view=powershellsdk-1.1.0) object.</span></span> 

<span data-ttu-id="5b478-178">The following example shows the creation of *PSCredential* objects for both source and target connections providing passwords as string variables *$sourcePassword* and *$targetPassword*.</span><span class="sxs-lookup"><span data-stu-id="5b478-178">The following example shows the creation of *PSCredential* objects for both source and target connections providing passwords as string variables *$sourcePassword* and *$targetPassword*.</span></span> 

```powershell
$secpasswd = ConvertTo-SecureString -String $sourcePassword -AsPlainText -Force
$sourceCred = New-Object System.Management.Automation.PSCredential ($sourceUserName, $secpasswd)
$secpasswd = ConvertTo-SecureString -String $targetPassword -AsPlainText -Force
$targetCred = New-Object System.Management.Automation.PSCredential ($targetUserName, $secpasswd)
```

### <a name="create-backup-fileshare-object"></a><span data-ttu-id="5b478-179">Create backup fileshare object</span><span class="sxs-lookup"><span data-stu-id="5b478-179">Create backup fileshare object</span></span>
<span data-ttu-id="5b478-180">Now create FileShare object representing the local SMB network share that the Azure Database Migration Service can take the source database backups to using the New-AzureRmDmsFileShare cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b478-180">Now create FileShare object representing the local SMB network share that the Azure Database Migration Service can take the source database backups to using the New-AzureRmDmsFileShare cmdlet.</span></span>

```powershell
$backupPassword = ConvertTo-SecureString -String $password -AsPlainText -Force
$backupCred = New-Object System.Management.Automation.PSCredential ($backupUserName, $backupPassword)

$backupFileSharePath="\\10.0.0.76\SharedBackup"
$backupFileShare = New-AzureRmDmsFileShare -Path $backupFileSharePath -Credential $backupCred
```

### <a name="create-selected-database-object"></a><span data-ttu-id="5b478-181">Create selected database object</span><span class="sxs-lookup"><span data-stu-id="5b478-181">Create selected database object</span></span>
<span data-ttu-id="5b478-182">The next step is to select the source and target databases by using the New-AzureRmDmsSelectedDB cmdlet, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="5b478-182">The next step is to select the source and target databases by using the New-AzureRmDmsSelectedDB cmdlet, as shown in the following example:</span></span>

```powershell
$selectedDbs = @()
$selectedDbs += New-AzureRmDmsSelectedDB -MigrateSqlServerSqlDbMi `
  -Name AdventureWorks2016 `
  -TargetDatabaseName AdventureWorks2016 `
  -BackupFileShare $backupFileShare `
```

### <a name="sas-uri-for-azure-storage-container"></a><span data-ttu-id="5b478-183">SAS URI for Azure Storage Container</span><span class="sxs-lookup"><span data-stu-id="5b478-183">SAS URI for Azure Storage Container</span></span>
<span data-ttu-id="5b478-184">Create variable containing the SAS URI that provides the Azure Database Migration Service with access to the storage account container to which the service uploads the backup files.</span><span class="sxs-lookup"><span data-stu-id="5b478-184">Create variable containing the SAS URI that provides the Azure Database Migration Service with access to the storage account container to which the service uploads the backup files.</span></span>

```powershell
$blobSasUri="https://mystorage.blob.core.windows.net/test?st=2018-07-13T18%3A10%3A33Z&se=2019-07-14T18%3A10%3A00Z&sp=rwdl&sv=2018-03-28&sr=c&sig=qKlSA512EVtest3xYjvUg139tYSDrasbftY%3D"
```

### <a name="select-logins"></a><span data-ttu-id="5b478-185">Select logins</span><span class="sxs-lookup"><span data-stu-id="5b478-185">Select logins</span></span>
<span data-ttu-id="5b478-186">Create list of logins to be migrated as shown in below example:  Note, currently DMS supports migrating SQL logins only.</span><span class="sxs-lookup"><span data-stu-id="5b478-186">Create list of logins to be migrated as shown in below example:  Note, currently DMS supports migrating SQL logins only.</span></span> 

```powershell
$selectedLogins = @("user1", "user2")
```

### <a name="select-agent-jobs"></a><span data-ttu-id="5b478-187">Select agent jobs</span><span class="sxs-lookup"><span data-stu-id="5b478-187">Select agent jobs</span></span>
<span data-ttu-id="5b478-188">Create list of agent jobs to be migrated as shown in below example:</span><span class="sxs-lookup"><span data-stu-id="5b478-188">Create list of agent jobs to be migrated as shown in below example:</span></span>

>[!NOTE]
><span data-ttu-id="5b478-189">Currently DMS supports the jobs with T-SQL subsystem job steps only.</span><span class="sxs-lookup"><span data-stu-id="5b478-189">Currently DMS supports the jobs with T-SQL subsystem job steps only.</span></span>

```powershell
$selectedAgentJobs = @("agentJob1", "agentJob2")
```

### <a name="create-and-start-a-migration-task"></a><span data-ttu-id="5b478-190">Create and start a migration task</span><span class="sxs-lookup"><span data-stu-id="5b478-190">Create and start a migration task</span></span>

<span data-ttu-id="5b478-191">Use the `New-AzureRmDataMigrationTask` cmdlet to create and start a migration task.</span><span class="sxs-lookup"><span data-stu-id="5b478-191">Use the `New-AzureRmDataMigrationTask` cmdlet to create and start a migration task.</span></span> <span data-ttu-id="5b478-192">This cmdlet expects the following parameters:</span><span class="sxs-lookup"><span data-stu-id="5b478-192">This cmdlet expects the following parameters:</span></span>
- <span data-ttu-id="5b478-193">*TaskType*.</span><span class="sxs-lookup"><span data-stu-id="5b478-193">*TaskType*.</span></span> <span data-ttu-id="5b478-194">Type of migration task to create for SQL Server to Azure SQL Database Managaged Instance migration type *MigrateSqlServerSqlDbMi* is expected.</span><span class="sxs-lookup"><span data-stu-id="5b478-194">Type of migration task to create for SQL Server to Azure SQL Database Managaged Instance migration type *MigrateSqlServerSqlDbMi* is expected.</span></span> 
- <span data-ttu-id="5b478-195">*Resource Group Name*.</span><span class="sxs-lookup"><span data-stu-id="5b478-195">*Resource Group Name*.</span></span> <span data-ttu-id="5b478-196">Name of Azure resource group in which to create the task.</span><span class="sxs-lookup"><span data-stu-id="5b478-196">Name of Azure resource group in which to create the task.</span></span>
- <span data-ttu-id="5b478-197">*ServiceName*.</span><span class="sxs-lookup"><span data-stu-id="5b478-197">*ServiceName*.</span></span> <span data-ttu-id="5b478-198">Azure Database Migration Service instance in which to create the task.</span><span class="sxs-lookup"><span data-stu-id="5b478-198">Azure Database Migration Service instance in which to create the task.</span></span>
- <span data-ttu-id="5b478-199">*ProjectName*.</span><span class="sxs-lookup"><span data-stu-id="5b478-199">*ProjectName*.</span></span> <span data-ttu-id="5b478-200">Name of Azure Database Migration Service project in which to create the task.</span><span class="sxs-lookup"><span data-stu-id="5b478-200">Name of Azure Database Migration Service project in which to create the task.</span></span> 
- <span data-ttu-id="5b478-201">*TaskName*.</span><span class="sxs-lookup"><span data-stu-id="5b478-201">*TaskName*.</span></span> <span data-ttu-id="5b478-202">Name of task to be created.</span><span class="sxs-lookup"><span data-stu-id="5b478-202">Name of task to be created.</span></span> 
- <span data-ttu-id="5b478-203">*SourceConnection*.</span><span class="sxs-lookup"><span data-stu-id="5b478-203">*SourceConnection*.</span></span> <span data-ttu-id="5b478-204">AzureRmDmsConnInfo object representing source SQL Server connection.</span><span class="sxs-lookup"><span data-stu-id="5b478-204">AzureRmDmsConnInfo object representing source SQL Server connection.</span></span>
- <span data-ttu-id="5b478-205">*TargetConnection*.</span><span class="sxs-lookup"><span data-stu-id="5b478-205">*TargetConnection*.</span></span> <span data-ttu-id="5b478-206">AzureRmDmsConnInfo object representing target Azure SQL Database Managed Instance connection.</span><span class="sxs-lookup"><span data-stu-id="5b478-206">AzureRmDmsConnInfo object representing target Azure SQL Database Managed Instance connection.</span></span>
- <span data-ttu-id="5b478-207">*SourceCred*.</span><span class="sxs-lookup"><span data-stu-id="5b478-207">*SourceCred*.</span></span> <span data-ttu-id="5b478-208">[PSCredential](https://docs.microsoft.com/dotnet/api/system.management.automation.pscredential?redirectedfrom=MSDN&view=powershellsdk-1.1.0) object for connecting to source server.</span><span class="sxs-lookup"><span data-stu-id="5b478-208">[PSCredential](https://docs.microsoft.com/dotnet/api/system.management.automation.pscredential?redirectedfrom=MSDN&view=powershellsdk-1.1.0) object for connecting to source server.</span></span>
- <span data-ttu-id="5b478-209">*TargetCred*.</span><span class="sxs-lookup"><span data-stu-id="5b478-209">*TargetCred*.</span></span> <span data-ttu-id="5b478-210">[PSCredential](https://docs.microsoft.com/dotnet/api/system.management.automation.pscredential?redirectedfrom=MSDN&view=powershellsdk-1.1.0) object for connecting to target server.</span><span class="sxs-lookup"><span data-stu-id="5b478-210">[PSCredential](https://docs.microsoft.com/dotnet/api/system.management.automation.pscredential?redirectedfrom=MSDN&view=powershellsdk-1.1.0) object for connecting to target server.</span></span>
- <span data-ttu-id="5b478-211">*SelectedDatabase*.</span><span class="sxs-lookup"><span data-stu-id="5b478-211">*SelectedDatabase*.</span></span> <span data-ttu-id="5b478-212">AzureRmDataMigrationSelectedDB object representing the source and target database mapping.</span><span class="sxs-lookup"><span data-stu-id="5b478-212">AzureRmDataMigrationSelectedDB object representing the source and target database mapping.</span></span>
- <span data-ttu-id="5b478-213">*BackupFileShare*.</span><span class="sxs-lookup"><span data-stu-id="5b478-213">*BackupFileShare*.</span></span> <span data-ttu-id="5b478-214">FileShare object representing the local network share that the Azure Database Migration Service can take the source database backups to.</span><span class="sxs-lookup"><span data-stu-id="5b478-214">FileShare object representing the local network share that the Azure Database Migration Service can take the source database backups to.</span></span>
- <span data-ttu-id="5b478-215">*BackupBlobSasUri*.</span><span class="sxs-lookup"><span data-stu-id="5b478-215">*BackupBlobSasUri*.</span></span> <span data-ttu-id="5b478-216">The SAS URI that provides the Azure Database Migration Service with access to the storage account container to which the service uploads the backup files.</span><span class="sxs-lookup"><span data-stu-id="5b478-216">The SAS URI that provides the Azure Database Migration Service with access to the storage account container to which the service uploads the backup files.</span></span> <span data-ttu-id="5b478-217">Learn how to get the SAS URI for blob container.</span><span class="sxs-lookup"><span data-stu-id="5b478-217">Learn how to get the SAS URI for blob container.</span></span>
- <span data-ttu-id="5b478-218">*SelectedLogins*.</span><span class="sxs-lookup"><span data-stu-id="5b478-218">*SelectedLogins*.</span></span> <span data-ttu-id="5b478-219">List of selected logins to migrate.</span><span class="sxs-lookup"><span data-stu-id="5b478-219">List of selected logins to migrate.</span></span>
- <span data-ttu-id="5b478-220">*SelectedAgentJobs*.</span><span class="sxs-lookup"><span data-stu-id="5b478-220">*SelectedAgentJobs*.</span></span> <span data-ttu-id="5b478-221">List of selected agent jobs to migrate.</span><span class="sxs-lookup"><span data-stu-id="5b478-221">List of selected agent jobs to migrate.</span></span>

<span data-ttu-id="5b478-222">The following example creates and starts a migration task named myDMSTask:</span><span class="sxs-lookup"><span data-stu-id="5b478-222">The following example creates and starts a migration task named myDMSTask:</span></span>

```powershell
$migTask = New-AzureRmDataMigrationTask -TaskType MigrateSqlServerSqlDbMi `
  -ResourceGroupName myResourceGroup `
  -ServiceName $service.Name `
  -ProjectName $project.Name `
  -TaskName myDMSTask `
  -SourceConnection $sourceConnInfo `
  -SourceCred $sourceCred `
  -TargetConnection $targetConnInfo `
  -TargetCred $targetCred `
  -SelectedDatabase  $selectedDbs`
  -BackupFileShare $backupFileShare `
  -BackupBlobSasUri $blobSasUri `
  -SelectedLogins $selectedLogins `
  -SelectedAgentJobs $selectedJobs `
```

## <a name="monitor-the-migration"></a><span data-ttu-id="5b478-223">Monitor the migration</span><span class="sxs-lookup"><span data-stu-id="5b478-223">Monitor the migration</span></span>
<span data-ttu-id="5b478-224">You can monitor the migration task running by querying the state property of the task as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="5b478-224">You can monitor the migration task running by querying the state property of the task as shown in the following example:</span></span>

```powershell
if (($mytask.ProjectTask.Properties.State -eq "Running") -or ($mytask.ProjectTask.Properties.State -eq "Queued"))
{
  write-host "migration task running"
}
```

## <a name="next-steps"></a><span data-ttu-id="5b478-225">Next steps</span><span class="sxs-lookup"><span data-stu-id="5b478-225">Next steps</span></span>
- <span data-ttu-id="5b478-226">Review the migration guidance in the Microsoft [Database Migration Guide](https://datamigration.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="5b478-226">Review the migration guidance in the Microsoft [Database Migration Guide](https://datamigration.microsoft.com/).</span></span>