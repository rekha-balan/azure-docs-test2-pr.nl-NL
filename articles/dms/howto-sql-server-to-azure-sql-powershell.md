---
title: Use Azure Database Migration Service module in Microsoft Azure PowerShell to migrate SQL Server on-premises to Azure SQL DB | Microsoft Docs
description: Learn to migrate from on-premises SQL Server to Azure SQL by using Azure PowerShell.
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
ms.openlocfilehash: d6c2503a95fe6b1072848c047280a293a49c147a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867567"
---
# <a name="migrate-sql-server-on-premises-to-azure-sql-db-using-azure-powershell"></a><span data-ttu-id="0819f-103">Migrate SQL Server on-premises to Azure SQL DB using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0819f-103">Migrate SQL Server on-premises to Azure SQL DB using Azure PowerShell</span></span>
<span data-ttu-id="0819f-104">In this article, you migrate the **Adventureworks2012** database restored to an on-premises instance of SQL Server 2016 or above to an Azure SQL Database by using Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0819f-104">In this article, you migrate the **Adventureworks2012** database restored to an on-premises instance of SQL Server 2016 or above to an Azure SQL Database by using Microsoft Azure PowerShell.</span></span> <span data-ttu-id="0819f-105">You can migrate databases from an on-premises SQL Server instance to Azure SQL Database by using the `AzureRM.DataMigration` module in Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0819f-105">You can migrate databases from an on-premises SQL Server instance to Azure SQL Database by using the `AzureRM.DataMigration` module in Microsoft Azure PowerShell.</span></span>

<span data-ttu-id="0819f-106">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="0819f-106">In this article, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="0819f-107">Create a resource group.</span><span class="sxs-lookup"><span data-stu-id="0819f-107">Create a resource group.</span></span>
> * <span data-ttu-id="0819f-108">Create an instance of the Azure Database Migration Service.</span><span class="sxs-lookup"><span data-stu-id="0819f-108">Create an instance of the Azure Database Migration Service.</span></span>
> * <span data-ttu-id="0819f-109">Create a migration project in an Azure Database Migration Service instance.</span><span class="sxs-lookup"><span data-stu-id="0819f-109">Create a migration project in an Azure Database Migration Service instance.</span></span>
> * <span data-ttu-id="0819f-110">Run the migration.</span><span class="sxs-lookup"><span data-stu-id="0819f-110">Run the migration.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0819f-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0819f-111">Prerequisites</span></span>
<span data-ttu-id="0819f-112">To complete these steps, you need:</span><span class="sxs-lookup"><span data-stu-id="0819f-112">To complete these steps, you need:</span></span>

- <span data-ttu-id="0819f-113">[SQL Server 2016 or above](https://www.microsoft.com/sql-server/sql-server-downloads) (any edition)</span><span class="sxs-lookup"><span data-stu-id="0819f-113">[SQL Server 2016 or above](https://www.microsoft.com/sql-server/sql-server-downloads) (any edition)</span></span>
- <span data-ttu-id="0819f-114">To enable the TCP/IP protocol, which is disabled by default with SQL Server Express installation.</span><span class="sxs-lookup"><span data-stu-id="0819f-114">To enable the TCP/IP protocol, which is disabled by default with SQL Server Express installation.</span></span> <span data-ttu-id="0819f-115">Enable the TCP/IP protocol by following the article [Enable or Disable a Server Network Protocol](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-or-disable-a-server-network-protocol#SSMSProcedure).</span><span class="sxs-lookup"><span data-stu-id="0819f-115">Enable the TCP/IP protocol by following the article [Enable or Disable a Server Network Protocol](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-or-disable-a-server-network-protocol#SSMSProcedure).</span></span>
- <span data-ttu-id="0819f-116">To configure your [Windows Firewall for database engine access](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access).</span><span class="sxs-lookup"><span data-stu-id="0819f-116">To configure your [Windows Firewall for database engine access](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access).</span></span>
- <span data-ttu-id="0819f-117">An Azure SQL Database instance.</span><span class="sxs-lookup"><span data-stu-id="0819f-117">An Azure SQL Database instance.</span></span> <span data-ttu-id="0819f-118">You can create an Azure SQL Database instance by following the detail in the article [Create an Azure SQL database in the Azure portal](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="0819f-118">You can create an Azure SQL Database instance by following the detail in the article [Create an Azure SQL database in the Azure portal](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal).</span></span>
- <span data-ttu-id="0819f-119">[Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) v3.3 or later.</span><span class="sxs-lookup"><span data-stu-id="0819f-119">[Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) v3.3 or later.</span></span>
- <span data-ttu-id="0819f-120">To have created a VNET by using the Azure Resource Manager deployment model, which provides the Azure Database Migration Service with site-to-site connectivity to your on-premises source servers by using either [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) or [VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).</span><span class="sxs-lookup"><span data-stu-id="0819f-120">To have created a VNET by using the Azure Resource Manager deployment model, which provides the Azure Database Migration Service with site-to-site connectivity to your on-premises source servers by using either [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) or [VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways).</span></span>
- <span data-ttu-id="0819f-121">To have completed assessment of your on-premises database and schema migration using Data Migration Assistant as described in the article [ Performing a SQL Server migration assessment](https://docs.microsoft.com/sql/dma/dma-assesssqlonprem)</span><span class="sxs-lookup"><span data-stu-id="0819f-121">To have completed assessment of your on-premises database and schema migration using Data Migration Assistant as described in the article [ Performing a SQL Server migration assessment](https://docs.microsoft.com/sql/dma/dma-assesssqlonprem)</span></span>
- <span data-ttu-id="0819f-122">To download and install the AzureRM.DataMigration module from the PowerShell Gallery by using [Install-Module PowerShell cmdlet](https://docs.microsoft.com/powershell/module/powershellget/Install-Module?view=powershell-5.1); be sure to open the powershell command window using run as an Administrator.</span><span class="sxs-lookup"><span data-stu-id="0819f-122">To download and install the AzureRM.DataMigration module from the PowerShell Gallery by using [Install-Module PowerShell cmdlet](https://docs.microsoft.com/powershell/module/powershellget/Install-Module?view=powershell-5.1); be sure to open the powershell command window using run as an Administrator.</span></span>
- <span data-ttu-id="0819f-123">To ensure that the credentials used to connect to source SQL Server instance has the [CONTROL SERVER](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql) permission.</span><span class="sxs-lookup"><span data-stu-id="0819f-123">To ensure that the credentials used to connect to source SQL Server instance has the [CONTROL SERVER](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql) permission.</span></span>
- <span data-ttu-id="0819f-124">To ensure that the credentials used to connect to target Azure SQL DB instance has the CONTROL DATABASE permission on the target Azure SQL Database databases.</span><span class="sxs-lookup"><span data-stu-id="0819f-124">To ensure that the credentials used to connect to target Azure SQL DB instance has the CONTROL DATABASE permission on the target Azure SQL Database databases.</span></span>
- <span data-ttu-id="0819f-125">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0819f-125">An Azure subscription.</span></span> <span data-ttu-id="0819f-126">If you don't have one, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="0819f-126">If you don't have one, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-to-your-microsoft-azure-subscription"></a><span data-ttu-id="0819f-127">Log in to your Microsoft Azure subscription</span><span class="sxs-lookup"><span data-stu-id="0819f-127">Log in to your Microsoft Azure subscription</span></span>
<span data-ttu-id="0819f-128">Use the directions in the article [Log in with Azure PowerShell](https://docs.microsoft.com/powershell/azure/authenticate-azureps?view=azurermps-4.4.1) to sign in to your Azure subscription by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0819f-128">Use the directions in the article [Log in with Azure PowerShell](https://docs.microsoft.com/powershell/azure/authenticate-azureps?view=azurermps-4.4.1) to sign in to your Azure subscription by using PowerShell.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="0819f-129">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="0819f-129">Create a resource group</span></span>
<span data-ttu-id="0819f-130">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="0819f-130">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="0819f-131">Create a resource group before you can create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="0819f-131">Create a resource group before you can create a virtual machine.</span></span>

<span data-ttu-id="0819f-132">Create a resource group by using the [New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup?view=azurermps-4.4.1) command.</span><span class="sxs-lookup"><span data-stu-id="0819f-132">Create a resource group by using the [New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup?view=azurermps-4.4.1) command.</span></span> 

<span data-ttu-id="0819f-133">The following example creates a resource group named *myResourceGroup* in the *EastUS* region.</span><span class="sxs-lookup"><span data-stu-id="0819f-133">The following example creates a resource group named *myResourceGroup* in the *EastUS* region.</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location EastUS
```
## <a name="create-an-instance-of-the-azure-database-migration-service"></a><span data-ttu-id="0819f-134">Create an instance of the Azure Database Migration Service</span><span class="sxs-lookup"><span data-stu-id="0819f-134">Create an instance of the Azure Database Migration Service</span></span> 
<span data-ttu-id="0819f-135">You can create new instance of Azure Database Migration Service by using the `New-AzureRmDataMigrationService` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0819f-135">You can create new instance of Azure Database Migration Service by using the `New-AzureRmDataMigrationService` cmdlet.</span></span> <span data-ttu-id="0819f-136">This cmdlet expects the following required parameters:</span><span class="sxs-lookup"><span data-stu-id="0819f-136">This cmdlet expects the following required parameters:</span></span>
- <span data-ttu-id="0819f-137">*Azure Resource Group name*.</span><span class="sxs-lookup"><span data-stu-id="0819f-137">*Azure Resource Group name*.</span></span> <span data-ttu-id="0819f-138">You can use [New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup?view=azurermps-4.4.1) command to create Azure Resource group as previously shown and provide its name as a parameter.</span><span class="sxs-lookup"><span data-stu-id="0819f-138">You can use [New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup?view=azurermps-4.4.1) command to create Azure Resource group as previously shown and provide its name as a parameter.</span></span>
- <span data-ttu-id="0819f-139">*Service name*.</span><span class="sxs-lookup"><span data-stu-id="0819f-139">*Service name*.</span></span> <span data-ttu-id="0819f-140">String that corresponds to the desired unique service name for Azure Database Migration Service</span><span class="sxs-lookup"><span data-stu-id="0819f-140">String that corresponds to the desired unique service name for Azure Database Migration Service</span></span> 
- <span data-ttu-id="0819f-141">*Location*.</span><span class="sxs-lookup"><span data-stu-id="0819f-141">*Location*.</span></span> <span data-ttu-id="0819f-142">Specifies the location of the service.</span><span class="sxs-lookup"><span data-stu-id="0819f-142">Specifies the location of the service.</span></span> <span data-ttu-id="0819f-143">Specify an Azure data center location, such as West US or Southeast Asia</span><span class="sxs-lookup"><span data-stu-id="0819f-143">Specify an Azure data center location, such as West US or Southeast Asia</span></span>
- <span data-ttu-id="0819f-144">*Sku*.</span><span class="sxs-lookup"><span data-stu-id="0819f-144">*Sku*.</span></span> <span data-ttu-id="0819f-145">This parameter corresponds to DMS Sku name.</span><span class="sxs-lookup"><span data-stu-id="0819f-145">This parameter corresponds to DMS Sku name.</span></span> <span data-ttu-id="0819f-146">Currently supported Sku names are *Basic_1vCore*, *Basic_2vCores*, *GeneralPurpose_4vCores*</span><span class="sxs-lookup"><span data-stu-id="0819f-146">Currently supported Sku names are *Basic_1vCore*, *Basic_2vCores*, *GeneralPurpose_4vCores*</span></span>
- <span data-ttu-id="0819f-147">*Virtual Subnet Identifier*.</span><span class="sxs-lookup"><span data-stu-id="0819f-147">*Virtual Subnet Identifier*.</span></span> <span data-ttu-id="0819f-148">You can use cmdlet [New-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig?view=azurermps-4.4.1) to create a subnet.</span><span class="sxs-lookup"><span data-stu-id="0819f-148">You can use cmdlet [New-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig?view=azurermps-4.4.1) to create a subnet.</span></span> 

<span data-ttu-id="0819f-149">The following example creates a service named *MyDMS* in the resource group *MyDMSResourceGroup* located in the *East US* region using a virtual network named *MyVNET* and  subnet called *MySubnet*.</span><span class="sxs-lookup"><span data-stu-id="0819f-149">The following example creates a service named *MyDMS* in the resource group *MyDMSResourceGroup* located in the *East US* region using a virtual network named *MyVNET* and  subnet called *MySubnet*.</span></span>

```powershell
 $vNet = Get-AzureRmVirtualNetwork -ResourceGroupName MyDMSResourceGroup -Name MyVNET

$vSubNet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vNet -Name MySubnet

$service = New-AzureRmDms -ResourceGroupName myResourceGroup `
  -ServiceName MyDMS `
  -Location EastUS `
  -Sku Basic_2vCores `  
  -VirtualSubnetId $vSubNet.Id`
```

## <a name="create-a-migration-project"></a><span data-ttu-id="0819f-150">Create a migration project</span><span class="sxs-lookup"><span data-stu-id="0819f-150">Create a migration project</span></span>
<span data-ttu-id="0819f-151">After creating an Azure Database Migration Service instance, create a migration project.</span><span class="sxs-lookup"><span data-stu-id="0819f-151">After creating an Azure Database Migration Service instance, create a migration project.</span></span> <span data-ttu-id="0819f-152">An Azure Database Migration Service project requires connection information for both the source and target instances, as well as a list of databases that you want to migrate as part of the project.</span><span class="sxs-lookup"><span data-stu-id="0819f-152">An Azure Database Migration Service project requires connection information for both the source and target instances, as well as a list of databases that you want to migrate as part of the project.</span></span>

### <a name="create-a-database-connection-info-object-for-the-source-and-target-connections"></a><span data-ttu-id="0819f-153">Create a Database Connection Info object for the source and target connections</span><span class="sxs-lookup"><span data-stu-id="0819f-153">Create a Database Connection Info object for the source and target connections</span></span>
<span data-ttu-id="0819f-154">You can create a Database Connection Info object by using the `New-AzureRmDmsConnInfo` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0819f-154">You can create a Database Connection Info object by using the `New-AzureRmDmsConnInfo` cmdlet.</span></span> <span data-ttu-id="0819f-155">This cmdlet expects the following parameters:</span><span class="sxs-lookup"><span data-stu-id="0819f-155">This cmdlet expects the following parameters:</span></span>
- <span data-ttu-id="0819f-156">*ServerType*.</span><span class="sxs-lookup"><span data-stu-id="0819f-156">*ServerType*.</span></span> <span data-ttu-id="0819f-157">The type of database connection requested, for example, SQL, Oracle, or MySQL.</span><span class="sxs-lookup"><span data-stu-id="0819f-157">The type of database connection requested, for example, SQL, Oracle, or MySQL.</span></span> <span data-ttu-id="0819f-158">Use SQL for SQL Server and Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="0819f-158">Use SQL for SQL Server and Azure SQL.</span></span>
- <span data-ttu-id="0819f-159">*DataSource*.</span><span class="sxs-lookup"><span data-stu-id="0819f-159">*DataSource*.</span></span> <span data-ttu-id="0819f-160">The name or IP of a SQL Server instance or Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="0819f-160">The name or IP of a SQL Server instance or Azure SQL database.</span></span>
- <span data-ttu-id="0819f-161">*AuthType*.</span><span class="sxs-lookup"><span data-stu-id="0819f-161">*AuthType*.</span></span> <span data-ttu-id="0819f-162">The authentication type for connection, which can be either SqlAuthentication or WindowsAuthentication.</span><span class="sxs-lookup"><span data-stu-id="0819f-162">The authentication type for connection, which can be either SqlAuthentication or WindowsAuthentication.</span></span>
- <span data-ttu-id="0819f-163">*TrustServerCertificate* parameter sets a value that indicates whether the channel is encrypted while bypassing walking the certificate chain to validate trust.</span><span class="sxs-lookup"><span data-stu-id="0819f-163">*TrustServerCertificate* parameter sets a value that indicates whether the channel is encrypted while bypassing walking the certificate chain to validate trust.</span></span> <span data-ttu-id="0819f-164">Value can be true or false.</span><span class="sxs-lookup"><span data-stu-id="0819f-164">Value can be true or false.</span></span>

<span data-ttu-id="0819f-165">The following example creates Connection Info object for source SQL Server called MySourceSQLServer using sql authentication:</span><span class="sxs-lookup"><span data-stu-id="0819f-165">The following example creates Connection Info object for source SQL Server called MySourceSQLServer using sql authentication:</span></span> 

```powershell
$sourceConnInfo = New-AzureRmDmsConnInfo -ServerType SQL `
  -DataSource MySourceSQLServer `
  -AuthType SqlAuthentication `
  -TrustServerCertificate:$true
```

<span data-ttu-id="0819f-166">The next example shows creation of Connection Info for an Azure SQL database server called SQLAzureTarget using sql authentication:</span><span class="sxs-lookup"><span data-stu-id="0819f-166">The next example shows creation of Connection Info for an Azure SQL database server called SQLAzureTarget using sql authentication:</span></span>

```powershell
$targetConnInfo = New-AzureRmDmsConnInfo -ServerType SQL `
  -DataSource "sqlazuretarget.database.windows.net" `
  -AuthType SqlAuthentication `
  -TrustServerCertificate:$false
```

### <a name="provide-databases-for-the-migration-project"></a><span data-ttu-id="0819f-167">Provide databases for the migration project</span><span class="sxs-lookup"><span data-stu-id="0819f-167">Provide databases for the migration project</span></span>
<span data-ttu-id="0819f-168">Create a list of `AzureRmDataMigrationDatabaseInfo` objects that specifies databases as part of the Azure Database Migration project that can be provided  as parameter for creation of the project.</span><span class="sxs-lookup"><span data-stu-id="0819f-168">Create a list of `AzureRmDataMigrationDatabaseInfo` objects that specifies databases as part of the Azure Database Migration project that can be provided  as parameter for creation of the project.</span></span> <span data-ttu-id="0819f-169">The Cmdlet `New-AzureRmDataMigrationDatabaseInfo` can be used to create AzureRmDataMigrationDatabaseInfo.</span><span class="sxs-lookup"><span data-stu-id="0819f-169">The Cmdlet `New-AzureRmDataMigrationDatabaseInfo` can be used to create AzureRmDataMigrationDatabaseInfo.</span></span> 

<span data-ttu-id="0819f-170">The following example creates `AzureRmDataMigrationDatabaseInfo` project for the **AdventureWorks2016** database and adds it to the list to be provided as parameter for project creation.</span><span class="sxs-lookup"><span data-stu-id="0819f-170">The following example creates `AzureRmDataMigrationDatabaseInfo` project for the **AdventureWorks2016** database and adds it to the list to be provided as parameter for project creation.</span></span>

```powershell
$dbInfo1 = New-AzureRmDataMigrationDatabaseInfo -SourceDatabaseName AdventureWorks2016
$dbList = @($dbInfo1)
```

### <a name="create-a-project-object"></a><span data-ttu-id="0819f-171">Create a project object</span><span class="sxs-lookup"><span data-stu-id="0819f-171">Create a project object</span></span>
<span data-ttu-id="0819f-172">Finally you can create Azure Database Migration project called *MyDMSProject* located in *East US* using `New-AzureRmDataMigrationProject` and adding the previously created source and target connections and the list of databases to migrate.</span><span class="sxs-lookup"><span data-stu-id="0819f-172">Finally you can create Azure Database Migration project called *MyDMSProject* located in *East US* using `New-AzureRmDataMigrationProject` and adding the previously created source and target connections and the list of databases to migrate.</span></span>

```powershell
$project = New-AzureRmDataMigrationProject -ResourceGroupName myResourceGroup `
  -ServiceName $service.Name `
  -ProjectName MyDMSProject `
  -Location EastUS `
  -SourceType SQL `
  -TargetType SQLDB `
  -SourceConnection $sourceConnInfo `
  -TargetConnection $targetConnInfo `
  -DatabaseInfo $dbList
```

## <a name="create-and-start-a-migration-task"></a><span data-ttu-id="0819f-173">Create and start a migration task</span><span class="sxs-lookup"><span data-stu-id="0819f-173">Create and start a migration task</span></span>
<span data-ttu-id="0819f-174">Finally, create and start Azure Database Migration task.</span><span class="sxs-lookup"><span data-stu-id="0819f-174">Finally, create and start Azure Database Migration task.</span></span> <span data-ttu-id="0819f-175">Azure Database Migration task requires connection credential information for both source and target and list of database tables to be migrated in addition to the information already provided with the project created as a prerequisite.</span><span class="sxs-lookup"><span data-stu-id="0819f-175">Azure Database Migration task requires connection credential information for both source and target and list of database tables to be migrated in addition to the information already provided with the project created as a prerequisite.</span></span> 

### <a name="create-credential-parameters-for-source-and-target"></a><span data-ttu-id="0819f-176">Create credential parameters for source and target</span><span class="sxs-lookup"><span data-stu-id="0819f-176">Create credential parameters for source and target</span></span>
<span data-ttu-id="0819f-177">Connection security credentials can be created as a [PSCredential](https://docs.microsoft.com/dotnet/api/system.management.automation.pscredential?redirectedfrom=MSDN&view=powershellsdk-1.1.0) object.</span><span class="sxs-lookup"><span data-stu-id="0819f-177">Connection security credentials can be created as a [PSCredential](https://docs.microsoft.com/dotnet/api/system.management.automation.pscredential?redirectedfrom=MSDN&view=powershellsdk-1.1.0) object.</span></span> 

<span data-ttu-id="0819f-178">The following example shows the creation of *PSCredential* objects for both source and target connections providing passwords as string variables *$sourcePassword* and *$targetPassword*.</span><span class="sxs-lookup"><span data-stu-id="0819f-178">The following example shows the creation of *PSCredential* objects for both source and target connections providing passwords as string variables *$sourcePassword* and *$targetPassword*.</span></span> 

```powershell
$secpasswd = ConvertTo-SecureString -String $sourcePassword -AsPlainText -Force
$sourceCred = New-Object System.Management.Automation.PSCredential ($sourceUserName, $secpasswd)
$secpasswd = ConvertTo-SecureString -String $targetPassword -AsPlainText -Force
$targetCred = New-Object System.Management.Automation.PSCredential ($targetUserName, $secpasswd)
```

### <a name="create-a-table-map-and-select-source-and-target-parameters-for-migration"></a><span data-ttu-id="0819f-179">Create a table map and select source and target parameters for migration</span><span class="sxs-lookup"><span data-stu-id="0819f-179">Create a table map and select source and target parameters for migration</span></span>
<span data-ttu-id="0819f-180">Another parameter needed for migration is mapping of tables from source to target to be migrated.</span><span class="sxs-lookup"><span data-stu-id="0819f-180">Another parameter needed for migration is mapping of tables from source to target to be migrated.</span></span> <span data-ttu-id="0819f-181">Create dictionary of tables that provides a mapping between source and target tables for migration.</span><span class="sxs-lookup"><span data-stu-id="0819f-181">Create dictionary of tables that provides a mapping between source and target tables for migration.</span></span> <span data-ttu-id="0819f-182">The following example illustrates mapping between source and target tables Human Resources schema for the AdventureWorks 2016 database.</span><span class="sxs-lookup"><span data-stu-id="0819f-182">The following example illustrates mapping between source and target tables Human Resources schema for the AdventureWorks 2016 database.</span></span>

```powershell
$tableMap = New-Object 'system.collections.generic.dictionary[string,string]'
$tableMap.Add("HumanResources.Department", "HumanResources.Department")
$tableMap.Add("HumanResources.Employee","HumanResources.Employee")
$tableMap.Add("HumanResources.EmployeeDepartmentHistory","HumanResources.EmployeeDepartmentHistory")
$tableMap.Add("HumanResources.EmployeePayHistory","HumanResources.EmployeePayHistory")
$tableMap.Add("HumanResources.JobCandidate","HumanResources.JobCandidate")
$tableMap.Add("HumanResources.Shift","HumanResources.Shift")
```

<span data-ttu-id="0819f-183">The next step is to select the source and target databases and provide table mapping to migrate as a parameter by using the `New-AzureRmDmsSelectedDB` cmdlet, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="0819f-183">The next step is to select the source and target databases and provide table mapping to migrate as a parameter by using the `New-AzureRmDmsSelectedDB` cmdlet, as shown in the following example:</span></span>

```powershell
$selectedDbs = New-AzureRmDmsSelectedDB -MigrateSqlServerSqlDb -Name AdventureWorks2016 `
  -TargetDatabaseName AdventureWorks2016 `
  -TableMap $tableMap
```

### <a name="create-and-start-a-migration-task"></a><span data-ttu-id="0819f-184">Create and start a migration task</span><span class="sxs-lookup"><span data-stu-id="0819f-184">Create and start a migration task</span></span>

<span data-ttu-id="0819f-185">Use the `New-AzureRmDataMigrationTask` cmdlet to create and start a migration task.</span><span class="sxs-lookup"><span data-stu-id="0819f-185">Use the `New-AzureRmDataMigrationTask` cmdlet to create and start a migration task.</span></span> <span data-ttu-id="0819f-186">This cmdlet expects the following parameters:</span><span class="sxs-lookup"><span data-stu-id="0819f-186">This cmdlet expects the following parameters:</span></span>
- <span data-ttu-id="0819f-187">*TaskType*.</span><span class="sxs-lookup"><span data-stu-id="0819f-187">*TaskType*.</span></span> <span data-ttu-id="0819f-188">Type of migration task to create for SQL Server to Azure SQL Database migration type *MigrateSqlServerSqlDb* is expected.</span><span class="sxs-lookup"><span data-stu-id="0819f-188">Type of migration task to create for SQL Server to Azure SQL Database migration type *MigrateSqlServerSqlDb* is expected.</span></span> 
- <span data-ttu-id="0819f-189">*Resource Group Name*.</span><span class="sxs-lookup"><span data-stu-id="0819f-189">*Resource Group Name*.</span></span> <span data-ttu-id="0819f-190">Name of Azure resource group in which to create the task.</span><span class="sxs-lookup"><span data-stu-id="0819f-190">Name of Azure resource group in which to create the task.</span></span>
- <span data-ttu-id="0819f-191">*ServiceName*.</span><span class="sxs-lookup"><span data-stu-id="0819f-191">*ServiceName*.</span></span> <span data-ttu-id="0819f-192">Azure Database Migration Service instance in which to create the task.</span><span class="sxs-lookup"><span data-stu-id="0819f-192">Azure Database Migration Service instance in which to create the task.</span></span>
- <span data-ttu-id="0819f-193">*ProjectName*.</span><span class="sxs-lookup"><span data-stu-id="0819f-193">*ProjectName*.</span></span> <span data-ttu-id="0819f-194">Name of Azure Database Migration Service project in which to create the task.</span><span class="sxs-lookup"><span data-stu-id="0819f-194">Name of Azure Database Migration Service project in which to create the task.</span></span> 
- <span data-ttu-id="0819f-195">*TaskName*.</span><span class="sxs-lookup"><span data-stu-id="0819f-195">*TaskName*.</span></span> <span data-ttu-id="0819f-196">Name of task to be created.</span><span class="sxs-lookup"><span data-stu-id="0819f-196">Name of task to be created.</span></span> 
- <span data-ttu-id="0819f-197">*SourceConnection*.</span><span class="sxs-lookup"><span data-stu-id="0819f-197">*SourceConnection*.</span></span> <span data-ttu-id="0819f-198">AzureRmDmsConnInfo object representing source SQL Server connection.</span><span class="sxs-lookup"><span data-stu-id="0819f-198">AzureRmDmsConnInfo object representing source SQL Server connection.</span></span>
- <span data-ttu-id="0819f-199">*TargetConnection*.</span><span class="sxs-lookup"><span data-stu-id="0819f-199">*TargetConnection*.</span></span> <span data-ttu-id="0819f-200">AzureRmDmsConnInfo object representing target Azure SQL Database connection.</span><span class="sxs-lookup"><span data-stu-id="0819f-200">AzureRmDmsConnInfo object representing target Azure SQL Database connection.</span></span>
- <span data-ttu-id="0819f-201">*SourceCred*.</span><span class="sxs-lookup"><span data-stu-id="0819f-201">*SourceCred*.</span></span> <span data-ttu-id="0819f-202">[PSCredential](https://docs.microsoft.com/dotnet/api/system.management.automation.pscredential?redirectedfrom=MSDN&view=powershellsdk-1.1.0) object for connecting to source server.</span><span class="sxs-lookup"><span data-stu-id="0819f-202">[PSCredential](https://docs.microsoft.com/dotnet/api/system.management.automation.pscredential?redirectedfrom=MSDN&view=powershellsdk-1.1.0) object for connecting to source server.</span></span>
- <span data-ttu-id="0819f-203">*TargetCred*.</span><span class="sxs-lookup"><span data-stu-id="0819f-203">*TargetCred*.</span></span> <span data-ttu-id="0819f-204">[PSCredential](https://docs.microsoft.com/dotnet/api/system.management.automation.pscredential?redirectedfrom=MSDN&view=powershellsdk-1.1.0) object for connecting to target server.</span><span class="sxs-lookup"><span data-stu-id="0819f-204">[PSCredential](https://docs.microsoft.com/dotnet/api/system.management.automation.pscredential?redirectedfrom=MSDN&view=powershellsdk-1.1.0) object for connecting to target server.</span></span>
- <span data-ttu-id="0819f-205">*SelectedDatabase*.</span><span class="sxs-lookup"><span data-stu-id="0819f-205">*SelectedDatabase*.</span></span> <span data-ttu-id="0819f-206">AzureRmDataMigrationSelectedDB object representing the source and target database mapping.</span><span class="sxs-lookup"><span data-stu-id="0819f-206">AzureRmDataMigrationSelectedDB object representing the source and target database mapping.</span></span>

<span data-ttu-id="0819f-207">The following example creates and starts a migration task named myDMSTask:</span><span class="sxs-lookup"><span data-stu-id="0819f-207">The following example creates and starts a migration task named myDMSTask:</span></span>

```powershell
$migTask = New-AzureRmDataMigrationTask -TaskType MigrateSqlServerSqlDb `
  -ResourceGroupName myResourceGroup `
  -ServiceName $service.Name `
  -ProjectName $project.Name `
  -TaskName myDMSTask `
  -SourceConnection $sourceConnInfo `
  -SourceCred $sourceCred `
  -TargetConnection $targetConnInfo `
  -TargetCred $targetCred `
  -SelectedDatabase  $selectedDbs`
```

## <a name="monitor-the-migration"></a><span data-ttu-id="0819f-208">Monitor the migration</span><span class="sxs-lookup"><span data-stu-id="0819f-208">Monitor the migration</span></span>
<span data-ttu-id="0819f-209">You can monitor the migration task running by querying the state property of the task as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="0819f-209">You can monitor the migration task running by querying the state property of the task as shown in the following example:</span></span>

```powershell
if (($mytask.ProjectTask.Properties.State -eq "Running") -or ($mytask.ProjectTask.Properties.State -eq "Queued"))
{
  write-host "migration task running"
}
```

## <a name="next-steps"></a><span data-ttu-id="0819f-210">Next steps</span><span class="sxs-lookup"><span data-stu-id="0819f-210">Next steps</span></span>
- <span data-ttu-id="0819f-211">Review the migration guidance in the Microsoft [Database Migration Guide](https://datamigration.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="0819f-211">Review the migration guidance in the Microsoft [Database Migration Guide](https://datamigration.microsoft.com/).</span></span>