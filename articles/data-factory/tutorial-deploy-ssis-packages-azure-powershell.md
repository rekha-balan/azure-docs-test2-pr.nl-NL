---
title: Provision the Azure-SSIS Integration Runtime with PowerShell | Microsoft Docs
description: Learn how to provision the Azure-SSIS integration runtime in Azure Data Factory with PowerShell so you can deploy and run SSIS packages in Azure.
services: data-factory
documentationcenter: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: ''
ms.devlang: powershell
ms.topic: tutorial
ms.date: 06/27/2018
author: swinarko
ms.author: sawinark
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 30e02f0b852ef0af8105a69575ea2c88e1265639
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967081"
---
# <a name="provision-the-azure-ssis-integration-runtime-in-azure-data-factory-with-powershell"></a><span data-ttu-id="a81a7-103">Provision the Azure-SSIS Integration Runtime in Azure Data Factory with PowerShell</span><span class="sxs-lookup"><span data-stu-id="a81a7-103">Provision the Azure-SSIS Integration Runtime in Azure Data Factory with PowerShell</span></span>
<span data-ttu-id="a81a7-104">This tutorial provides steps for provisioning an Azure-SSIS integration runtime (IR) in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a81a7-104">This tutorial provides steps for provisioning an Azure-SSIS integration runtime (IR) in Azure Data Factory.</span></span> <span data-ttu-id="a81a7-105">Then, you can use SQL Server Data Tools (SSDT) or SQL Server Management Studio (SSMS) to deploy and run SQL Server Integration Services (SSIS) packages in this runtime in Azure.</span><span class="sxs-lookup"><span data-stu-id="a81a7-105">Then, you can use SQL Server Data Tools (SSDT) or SQL Server Management Studio (SSMS) to deploy and run SQL Server Integration Services (SSIS) packages in this runtime in Azure.</span></span> <span data-ttu-id="a81a7-106">In this tutorial, you do the following steps:</span><span class="sxs-lookup"><span data-stu-id="a81a7-106">In this tutorial, you do the following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="a81a7-107">This article uses Azure PowerShell to provision an Azure SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="a81a7-107">This article uses Azure PowerShell to provision an Azure SSIS IR.</span></span> <span data-ttu-id="a81a7-108">To use the Data Factory user interface (UI) to provision an Azure SSIS IR, see [Tutorial: Create an Azure SSIS integration runtime](tutorial-create-azure-ssis-runtime-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a81a7-108">To use the Data Factory user interface (UI) to provision an Azure SSIS IR, see [Tutorial: Create an Azure SSIS integration runtime](tutorial-create-azure-ssis-runtime-portal.md).</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="a81a7-109">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="a81a7-109">Create a data factory.</span></span>
> * <span data-ttu-id="a81a7-110">Create an Azure-SSIS integration runtime</span><span class="sxs-lookup"><span data-stu-id="a81a7-110">Create an Azure-SSIS integration runtime</span></span>
> * <span data-ttu-id="a81a7-111">Start the Azure-SSIS integration runtime</span><span class="sxs-lookup"><span data-stu-id="a81a7-111">Start the Azure-SSIS integration runtime</span></span>
> * <span data-ttu-id="a81a7-112">Deploy SSIS packages</span><span class="sxs-lookup"><span data-stu-id="a81a7-112">Deploy SSIS packages</span></span>
> * <span data-ttu-id="a81a7-113">Review the complete script</span><span class="sxs-lookup"><span data-stu-id="a81a7-113">Review the complete script</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a81a7-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a81a7-114">Prerequisites</span></span>
- <span data-ttu-id="a81a7-115">**Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="a81a7-115">**Azure subscription**.</span></span> <span data-ttu-id="a81a7-116">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="a81a7-116">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span> <span data-ttu-id="a81a7-117">For conceptual information on Azure-SSIS IR, see [Azure-SSIS integration runtime overview](concepts-integration-runtime.md#azure-ssis-integration-runtime).</span><span class="sxs-lookup"><span data-stu-id="a81a7-117">For conceptual information on Azure-SSIS IR, see [Azure-SSIS integration runtime overview](concepts-integration-runtime.md#azure-ssis-integration-runtime).</span></span> 
- <span data-ttu-id="a81a7-118">**Azure SQL Database server**.</span><span class="sxs-lookup"><span data-stu-id="a81a7-118">**Azure SQL Database server**.</span></span> <span data-ttu-id="a81a7-119">If you don't already have a database server, create one in the Azure portal before you get started.</span><span class="sxs-lookup"><span data-stu-id="a81a7-119">If you don't already have a database server, create one in the Azure portal before you get started.</span></span> <span data-ttu-id="a81a7-120">This server hosts the SSIS Catalog database (SSISDB).</span><span class="sxs-lookup"><span data-stu-id="a81a7-120">This server hosts the SSIS Catalog database (SSISDB).</span></span> <span data-ttu-id="a81a7-121">We recommend that you create the database server in the same Azure region as the integration runtime.</span><span class="sxs-lookup"><span data-stu-id="a81a7-121">We recommend that you create the database server in the same Azure region as the integration runtime.</span></span> <span data-ttu-id="a81a7-122">This configuration lets the integration runtime write execution logs to SSISDB without crossing Azure regions.</span><span class="sxs-lookup"><span data-stu-id="a81a7-122">This configuration lets the integration runtime write execution logs to SSISDB without crossing Azure regions.</span></span> 
    - <span data-ttu-id="a81a7-123">Based on the selected database server, SSISDB can be created on your behalf as a single database, part of an Elastic Pool, or in a Managed Instance (Preview) and accessible in public network or by joining a virtual network.</span><span class="sxs-lookup"><span data-stu-id="a81a7-123">Based on the selected database server, SSISDB can be created on your behalf as a single database, part of an Elastic Pool, or in a Managed Instance (Preview) and accessible in public network or by joining a virtual network.</span></span> <span data-ttu-id="a81a7-124">For guidance in choosing the type of database server to host SSISDB, see [Compare SQL Database and Managed Instance (Preview)](create-azure-ssis-integration-runtime.md#compare-sql-database-and-managed-instance-preview).</span><span class="sxs-lookup"><span data-stu-id="a81a7-124">For guidance in choosing the type of database server to host SSISDB, see [Compare SQL Database and Managed Instance (Preview)](create-azure-ssis-integration-runtime.md#compare-sql-database-and-managed-instance-preview).</span></span> <span data-ttu-id="a81a7-125">If you use Azure SQL Database with virtual network service endpoints/Managed Instance (Preview) to host SSISDB or require access to on-premises data, you need to join your Azure-SSIS IR to a virtual network, see [Create Azure-SSIS IR in a virtual network](https://docs.microsoft.com/en-us/azure/data-factory/create-azure-ssis-integration-runtime).</span><span class="sxs-lookup"><span data-stu-id="a81a7-125">If you use Azure SQL Database with virtual network service endpoints/Managed Instance (Preview) to host SSISDB or require access to on-premises data, you need to join your Azure-SSIS IR to a virtual network, see [Create Azure-SSIS IR in a virtual network](https://docs.microsoft.com/en-us/azure/data-factory/create-azure-ssis-integration-runtime).</span></span> 
    - <span data-ttu-id="a81a7-126">Confirm that the "**Allow access to Azure services**" setting is **ON** for the database server.</span><span class="sxs-lookup"><span data-stu-id="a81a7-126">Confirm that the "**Allow access to Azure services**" setting is **ON** for the database server.</span></span> <span data-ttu-id="a81a7-127">This setting is not applicable when you use Azure SQL Database with virtual network service endpoints/Managed Instance (Preview) to host SSISDB.</span><span class="sxs-lookup"><span data-stu-id="a81a7-127">This setting is not applicable when you use Azure SQL Database with virtual network service endpoints/Managed Instance (Preview) to host SSISDB.</span></span> <span data-ttu-id="a81a7-128">For more information, see [Secure your Azure SQL database](../sql-database/sql-database-security-tutorial.md#create-a-server-level-firewall-rule-in-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="a81a7-128">For more information, see [Secure your Azure SQL database](../sql-database/sql-database-security-tutorial.md#create-a-server-level-firewall-rule-in-the-azure-portal).</span></span> <span data-ttu-id="a81a7-129">To enable this setting by using PowerShell, see [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule?view=azurermps-4.4.1).</span><span class="sxs-lookup"><span data-stu-id="a81a7-129">To enable this setting by using PowerShell, see [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule?view=azurermps-4.4.1).</span></span> 
    - <span data-ttu-id="a81a7-130">Add the IP address of the client machine or a range of IP addresses that includes the IP address of client machine to the client IP address list in the firewall settings for the database server.</span><span class="sxs-lookup"><span data-stu-id="a81a7-130">Add the IP address of the client machine or a range of IP addresses that includes the IP address of client machine to the client IP address list in the firewall settings for the database server.</span></span> <span data-ttu-id="a81a7-131">For more information, see [Azure SQL Database server-level and database-level firewall rules](../sql-database/sql-database-firewall-configure.md).</span><span class="sxs-lookup"><span data-stu-id="a81a7-131">For more information, see [Azure SQL Database server-level and database-level firewall rules](../sql-database/sql-database-firewall-configure.md).</span></span> 
    - <span data-ttu-id="a81a7-132">You can connect to the database server using SQL authentication with your server admin credentials or Azure Active Directory (AAD) authentication with your Azure Data Factory Managed Service Identity (MSI).</span><span class="sxs-lookup"><span data-stu-id="a81a7-132">You can connect to the database server using SQL authentication with your server admin credentials or Azure Active Directory (AAD) authentication with your Azure Data Factory Managed Service Identity (MSI).</span></span>  <span data-ttu-id="a81a7-133">For the latter, you need to add your Data Factory MSI into an AAD group with access permissions to the database server, see [Create Azure-SSIS IR with AAD authentication](https://docs.microsoft.com/en-us/azure/data-factory/create-azure-ssis-integration-runtime).</span><span class="sxs-lookup"><span data-stu-id="a81a7-133">For the latter, you need to add your Data Factory MSI into an AAD group with access permissions to the database server, see [Create Azure-SSIS IR with AAD authentication](https://docs.microsoft.com/en-us/azure/data-factory/create-azure-ssis-integration-runtime).</span></span> 
    - <span data-ttu-id="a81a7-134">Confirm that your Azure SQL Database server does not have an SSIS Catalog (SSISDB database).</span><span class="sxs-lookup"><span data-stu-id="a81a7-134">Confirm that your Azure SQL Database server does not have an SSIS Catalog (SSISDB database).</span></span> <span data-ttu-id="a81a7-135">The provisioning of Azure-SSIS IR does not support using an existing SSIS Catalog.</span><span class="sxs-lookup"><span data-stu-id="a81a7-135">The provisioning of Azure-SSIS IR does not support using an existing SSIS Catalog.</span></span> 
- <span data-ttu-id="a81a7-136">**Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="a81a7-136">**Azure PowerShell**.</span></span> <span data-ttu-id="a81a7-137">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="a81a7-137">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="a81a7-138">You use PowerShell to run a script to provision an Azure-SSIS integration runtime that runs SSIS packages in the cloud.</span><span class="sxs-lookup"><span data-stu-id="a81a7-138">You use PowerShell to run a script to provision an Azure-SSIS integration runtime that runs SSIS packages in the cloud.</span></span> 

> [!NOTE]
> - <span data-ttu-id="a81a7-139">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="a81a7-139">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span></span> 
> - <span data-ttu-id="a81a7-140">For a list of Azure regions in which the Azure-SSIS Integration Runtime is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **SSIS Integration Runtime**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="a81a7-140">For a list of Azure regions in which the Azure-SSIS Integration Runtime is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **SSIS Integration Runtime**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span></span>

## <a name="launch-windows-powershell-ise"></a><span data-ttu-id="a81a7-141">Launch Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="a81a7-141">Launch Windows PowerShell ISE</span></span>
<span data-ttu-id="a81a7-142">Start **Windows PowerShell ISE** with administrative privileges.</span><span class="sxs-lookup"><span data-stu-id="a81a7-142">Start **Windows PowerShell ISE** with administrative privileges.</span></span> 

## <a name="create-variables"></a><span data-ttu-id="a81a7-143">Create variables</span><span class="sxs-lookup"><span data-stu-id="a81a7-143">Create variables</span></span>
<span data-ttu-id="a81a7-144">Copy and paste the following script: Specify values for the variables.</span><span class="sxs-lookup"><span data-stu-id="a81a7-144">Copy and paste the following script: Specify values for the variables.</span></span> <span data-ttu-id="a81a7-145">For a list of supported **pricing tiers** for Azure SQL Database, see [SQL Database resource limits](../sql-database/sql-database-resource-limits.md).</span><span class="sxs-lookup"><span data-stu-id="a81a7-145">For a list of supported **pricing tiers** for Azure SQL Database, see [SQL Database resource limits](../sql-database/sql-database-resource-limits.md).</span></span>

```powershell
# Azure Data Factory information 
# If your input contains a PSH special character, e.g. "$", precede it with the escape character "`" like "`$". 
$SubscriptionName = "[Azure subscription name]"
$ResourceGroupName = "[Azure resource group name]"
# Data factory name. Must be globally unique
$DataFactoryName = "[Data factory name]"
$DataFactoryLocation = "EastUS"

# Azure-SSIS integration runtime information. This is a Data Factory compute resource for running SSIS packages
$AzureSSISName = "[Specify a name for your Azure-SSIS IR]"
$AzureSSISDescription = "[Specify a description for your Azure-SSIS IR]"
$AzureSSISLocation = "EastUS"
# In public preview, only Standard_A4_v2, Standard_A8_v2, Standard_D1_v2, Standard_D2_v2, Standard_D3_v2, Standard_D4_v2 are supported
$AzureSSISNodeSize = "Standard_D4_v2"
# In public preview, only 1-10 nodes are supported.
$AzureSSISNodeNumber = 2 
# Azure-SSIS IR edition/license info: Standard or Enterprise 
$AzureSSISEdition = "" # Standard by default, while Enterprise lets you use advanced/premium features on your Azure-SSIS IR
# Azure-SSIS IR hybrid usage info: LicenseIncluded or BasePrice
$AzureSSISLicenseType = "" # LicenseIncluded by default, while BasePrice lets you bring your own on-premises SQL Server license to earn cost savings from Azure Hybrid Benefit (AHB) option
# For a Standard_D1_v2 node, 1-4 parallel executions per node are supported. For other nodes, it's 1-8.
$AzureSSISMaxParallelExecutionsPerNode = 8
# Custom setup info
$SetupScriptContainerSasUri = "" # OPTIONAL to provide SAS URI of blob container where your custom setup script and its associated files are stored

# SSISDB info
$SSISDBServerEndpoint = "[your Azure SQL Database server name].database.windows.net" # WARNING: Please ensure that there is no existing SSISDB, so we can prepare and manage one on your behalf    
$SSISDBServerAdminUserName = "[your server admin username for SQL authentication]"
$SSISDBServerAdminPassword = "[your server admin password for SQL authentication]"
# For the basic pricing tier, specify "Basic", not "B". For standard/premium/Elastic Pool tiers, specify "S0", "S1", "S2", "S3", etc.
$SSISDBPricingTier = "[Basic|S0|S1|S2|S3|S4|S6|S7|S9|S12|P1|P2|P4|P6|P11|P15|…|ELASTIC_POOL(name = <elastic_pool_name>)]"
```

## <a name="validate-the-connection-to-database"></a><span data-ttu-id="a81a7-146">Validate the connection to database</span><span class="sxs-lookup"><span data-stu-id="a81a7-146">Validate the connection to database</span></span>
<span data-ttu-id="a81a7-147">Add the following script to validate your Azure SQL Database server, `<servername>.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="a81a7-147">Add the following script to validate your Azure SQL Database server, `<servername>.database.windows.net`.</span></span> 

```powershell
$SSISDBConnectionString = "Data Source=" + $SSISDBServerEndpoint + ";User ID=" + $SSISDBServerAdminUserName + ";Password=" + $SSISDBServerAdminPassword    
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $SSISDBConnectionString;
Try
{
    $sqlConnection.Open();
}
Catch [System.Data.SqlClient.SqlException]
{
    Write-Warning "Cannot connect to your Azure SQL Database server, exception: $_";
    Write-Warning "Please make sure the server you specified has already been created. Do you want to proceed? [Y/N]"
    $yn = Read-Host
    if(!($yn -ieq "Y"))
    {
        Return;
    } 
}
```

<span data-ttu-id="a81a7-148">To create an Azure SQL database as part of the script, see the following example:</span><span class="sxs-lookup"><span data-stu-id="a81a7-148">To create an Azure SQL database as part of the script, see the following example:</span></span> 

<span data-ttu-id="a81a7-149">Set values for the variables that haven't been defined already.</span><span class="sxs-lookup"><span data-stu-id="a81a7-149">Set values for the variables that haven't been defined already.</span></span> <span data-ttu-id="a81a7-150">For example: SSISDBServerName, FirewallIPAddress.</span><span class="sxs-lookup"><span data-stu-id="a81a7-150">For example: SSISDBServerName, FirewallIPAddress.</span></span> 

```powershell
New-AzureRmSqlServer -ResourceGroupName $ResourceGroupName `
    -ServerName $SSISDBServerName `
    -Location $DataFactoryLocation `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $SSISDBServerAdminUserName, $(ConvertTo-SecureString -String $SSISDBServerAdminPassword -AsPlainText -Force))    

New-AzureRmSqlServerFirewallRule -ResourceGroupName $ResourceGroupName `
    -ServerName $SSISDBServerName `
    -FirewallRuleName "ClientIPAddress_$today" -StartIpAddress $FirewallIPAddress -EndIpAddress $FirewallIPAddress

New-AzureRmSqlServerFirewallRule -ResourceGroupName $ResourceGroupName -ServerName $SSISDBServerName -AllowAllAzureIPs
```

## <a name="log-in-and-select-subscription"></a><span data-ttu-id="a81a7-151">Log in and select subscription</span><span class="sxs-lookup"><span data-stu-id="a81a7-151">Log in and select subscription</span></span>
<span data-ttu-id="a81a7-152">Add the following code to the script to log in and select your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="a81a7-152">Add the following code to the script to log in and select your Azure subscription:</span></span> 

```powershell
Connect-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $SubscriptionName
```

## <a name="create-a-resource-group"></a><span data-ttu-id="a81a7-153">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="a81a7-153">Create a resource group</span></span>
<span data-ttu-id="a81a7-154">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span><span class="sxs-lookup"><span data-stu-id="a81a7-154">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="a81a7-155">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span><span class="sxs-lookup"><span data-stu-id="a81a7-155">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="a81a7-156">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span><span class="sxs-lookup"><span data-stu-id="a81a7-156">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span></span>

<span data-ttu-id="a81a7-157">If your resource group already exists, don't copy this code to your script.</span><span class="sxs-lookup"><span data-stu-id="a81a7-157">If your resource group already exists, don't copy this code to your script.</span></span> 

```powershell
New-AzureRmResourceGroup -Location $DataFactoryLocation -Name $ResourceGroupName
```

## <a name="create-a-data-factory"></a><span data-ttu-id="a81a7-158">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="a81a7-158">Create a data factory</span></span>
<span data-ttu-id="a81a7-159">Run the following command to create a data factory:</span><span class="sxs-lookup"><span data-stu-id="a81a7-159">Run the following command to create a data factory:</span></span>

```powershell
Set-AzureRmDataFactoryV2 -ResourceGroupName $ResourceGroupName `
                         -Location $DataFactoryLocation `
                         -Name $DataFactoryName
```

## <a name="create-an-integration-runtime"></a><span data-ttu-id="a81a7-160">Create an integration runtime</span><span class="sxs-lookup"><span data-stu-id="a81a7-160">Create an integration runtime</span></span>
<span data-ttu-id="a81a7-161">Run the following command to create an Azure-SSIS integration runtime that runs SSIS packages in Azure:</span><span class="sxs-lookup"><span data-stu-id="a81a7-161">Run the following command to create an Azure-SSIS integration runtime that runs SSIS packages in Azure:</span></span> 

```powershell
$secpasswd = ConvertTo-SecureString $SSISDBServerAdminPassword -AsPlainText -Force
$serverCreds = New-Object System.Management.Automation.PSCredential($SSISDBServerAdminUserName, $secpasswd)
  
Set-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName $ResourceGroupName `
                                           -DataFactoryName $DataFactoryName `
                                           -Name $AzureSSISName `
                                           -Description $AzureSSISDescription `
                                           -Type Managed `
                                           -Location $AzureSSISLocation `
                                           -NodeSize $AzureSSISNodeSize `
                                           -NodeCount $AzureSSISNodeNumber `
                                           -Edition $AzureSSISEdition `
                                           -LicenseType $AzureSSISLicenseType `
                                           -MaxParallelExecutionsPerNode $AzureSSISMaxParallelExecutionsPerNode `
                                           -SetupScriptContainerSasUri $SetupScriptContainerSasUri `
                                           -CatalogServerEndpoint $SSISDBServerEndpoint `
                                           -CatalogAdminCredential $serverCreds `
                                           -CatalogPricingTier $SSISDBPricingTier
```

## <a name="start-integration-runtime"></a><span data-ttu-id="a81a7-162">Start integration runtime</span><span class="sxs-lookup"><span data-stu-id="a81a7-162">Start integration runtime</span></span>
<span data-ttu-id="a81a7-163">Run the following command to start the Azure-SSIS integration runtime:</span><span class="sxs-lookup"><span data-stu-id="a81a7-163">Run the following command to start the Azure-SSIS integration runtime:</span></span> 

```powershell
write-host("##### Starting your Azure-SSIS integration runtime. This command takes 20 to 30 minutes to complete. #####")
Start-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName $ResourceGroupName `
                                             -DataFactoryName $DataFactoryName `
                                             -Name $AzureSSISName `
                                             -Force

write-host("##### Completed #####")
write-host("If any cmdlet is unsuccessful, please consider using -Debug option for diagnostics.")                                  
```
<span data-ttu-id="a81a7-164">This command takes from **20 to 30 minutes** to complete.</span><span class="sxs-lookup"><span data-stu-id="a81a7-164">This command takes from **20 to 30 minutes** to complete.</span></span> 

## <a name="deploy-ssis-packages"></a><span data-ttu-id="a81a7-165">Deploy SSIS packages</span><span class="sxs-lookup"><span data-stu-id="a81a7-165">Deploy SSIS packages</span></span>
<span data-ttu-id="a81a7-166">Now, use SQL Server Data Tools (SSDT) or SQL Server Management Studio (SSMS) to deploy your SSIS packages to Azure.</span><span class="sxs-lookup"><span data-stu-id="a81a7-166">Now, use SQL Server Data Tools (SSDT) or SQL Server Management Studio (SSMS) to deploy your SSIS packages to Azure.</span></span> <span data-ttu-id="a81a7-167">Connect to your Azure SQL server that hosts the SSIS catalog (SSISDB).</span><span class="sxs-lookup"><span data-stu-id="a81a7-167">Connect to your Azure SQL server that hosts the SSIS catalog (SSISDB).</span></span> <span data-ttu-id="a81a7-168">The name of the Azure SQL Database server is in the format: `<servername>.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="a81a7-168">The name of the Azure SQL Database server is in the format: `<servername>.database.windows.net`.</span></span> 

<span data-ttu-id="a81a7-169">See the following articles from SSIS documentation:</span><span class="sxs-lookup"><span data-stu-id="a81a7-169">See the following articles from SSIS documentation:</span></span> 

- [<span data-ttu-id="a81a7-170">Deploy, run, and monitor an SSIS package on Azure</span><span class="sxs-lookup"><span data-stu-id="a81a7-170">Deploy, run, and monitor an SSIS package on Azure</span></span>](/sql/integration-services/lift-shift/ssis-azure-deploy-run-monitor-tutorial)   
- [<span data-ttu-id="a81a7-171">Connect to SSIS catalog on Azure</span><span class="sxs-lookup"><span data-stu-id="a81a7-171">Connect to SSIS catalog on Azure</span></span>](/sql/integration-services/lift-shift/ssis-azure-connect-to-catalog-database)
- [<span data-ttu-id="a81a7-172">Schedule package execution on Azure</span><span class="sxs-lookup"><span data-stu-id="a81a7-172">Schedule package execution on Azure</span></span>](/sql/integration-services/lift-shift/ssis-azure-schedule-packages)
- [<span data-ttu-id="a81a7-173">Connect to on-premises data sources with Windows authentication</span><span class="sxs-lookup"><span data-stu-id="a81a7-173">Connect to on-premises data sources with Windows authentication</span></span>](/sql/integration-services/lift-shift/ssis-azure-connect-with-windows-auth) 

## <a name="full-script"></a><span data-ttu-id="a81a7-174">Full script</span><span class="sxs-lookup"><span data-stu-id="a81a7-174">Full script</span></span>
<span data-ttu-id="a81a7-175">The PowerShell script in this section configures an instance of Azure-SSIS integration runtime in the cloud that runs SSIS packages.</span><span class="sxs-lookup"><span data-stu-id="a81a7-175">The PowerShell script in this section configures an instance of Azure-SSIS integration runtime in the cloud that runs SSIS packages.</span></span> <span data-ttu-id="a81a7-176">After you run this script successfully, you can deploy and run SSIS packages in the Microsoft Azure cloud with SSISDB hosted in Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="a81a7-176">After you run this script successfully, you can deploy and run SSIS packages in the Microsoft Azure cloud with SSISDB hosted in Azure SQL Database.</span></span>

1. <span data-ttu-id="a81a7-177">Launch the Windows PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="a81a7-177">Launch the Windows PowerShell Integrated Scripting Environment (ISE).</span></span>
2. <span data-ttu-id="a81a7-178">In the ISE, run the following command from the command prompt.</span><span class="sxs-lookup"><span data-stu-id="a81a7-178">In the ISE, run the following command from the command prompt.</span></span>    
    ```powershell
    Set-ExecutionPolicy Unrestricted -Scope CurrentUser
    ```
3. <span data-ttu-id="a81a7-179">Copy the PowerShell script in this section and paste it into the ISE.</span><span class="sxs-lookup"><span data-stu-id="a81a7-179">Copy the PowerShell script in this section and paste it into the ISE.</span></span>
4. <span data-ttu-id="a81a7-180">Provide appropriate values for all parameters at the beginning of the script.</span><span class="sxs-lookup"><span data-stu-id="a81a7-180">Provide appropriate values for all parameters at the beginning of the script.</span></span>
5. <span data-ttu-id="a81a7-181">Run the script.</span><span class="sxs-lookup"><span data-stu-id="a81a7-181">Run the script.</span></span> <span data-ttu-id="a81a7-182">The `Start-AzureRmDataFactoryV2IntegrationRuntime` command near the end of the script runs for **20 to 30 minutes**.</span><span class="sxs-lookup"><span data-stu-id="a81a7-182">The `Start-AzureRmDataFactoryV2IntegrationRuntime` command near the end of the script runs for **20 to 30 minutes**.</span></span>

> [!NOTE]
> - <span data-ttu-id="a81a7-183">The script connects to your Azure SQL Database server to prepare the SSIS Catalog database (SSISDB).</span><span class="sxs-lookup"><span data-stu-id="a81a7-183">The script connects to your Azure SQL Database server to prepare the SSIS Catalog database (SSISDB).</span></span>

> - <span data-ttu-id="a81a7-184">When you provision an instance of Azure-SSIS IR, the Azure Feature Pack for SSIS and the Access Redistributable are also installed.</span><span class="sxs-lookup"><span data-stu-id="a81a7-184">When you provision an instance of Azure-SSIS IR, the Azure Feature Pack for SSIS and the Access Redistributable are also installed.</span></span> <span data-ttu-id="a81a7-185">These components provide connectivity to Excel and Access files and to various Azure data sources, in addition to the data sources supported by the built-in components.</span><span class="sxs-lookup"><span data-stu-id="a81a7-185">These components provide connectivity to Excel and Access files and to various Azure data sources, in addition to the data sources supported by the built-in components.</span></span> <span data-ttu-id="a81a7-186">You can also install additional components.</span><span class="sxs-lookup"><span data-stu-id="a81a7-186">You can also install additional components.</span></span> <span data-ttu-id="a81a7-187">For more info, see [Custom setup for the Azure-SSIS integration runtime](how-to-configure-azure-ssis-ir-custom-setup.md).</span><span class="sxs-lookup"><span data-stu-id="a81a7-187">For more info, see [Custom setup for the Azure-SSIS integration runtime](how-to-configure-azure-ssis-ir-custom-setup.md).</span></span>

<span data-ttu-id="a81a7-188">For a list of supported **pricing tiers** for Azure SQL Database, see [SQL Database resource limits](../sql-database/sql-database-resource-limits.md).</span><span class="sxs-lookup"><span data-stu-id="a81a7-188">For a list of supported **pricing tiers** for Azure SQL Database, see [SQL Database resource limits](../sql-database/sql-database-resource-limits.md).</span></span> 

<span data-ttu-id="a81a7-189">For a list of regions supported by Azure Data Factory V2 and Azure-SSIS Integration Runtime, see [Products available by region](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="a81a7-189">For a list of regions supported by Azure Data Factory V2 and Azure-SSIS Integration Runtime, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="a81a7-190">Expand **Data + Analytics** to see **Data Factory V2** and **SSIS Integration Runtime**.</span><span class="sxs-lookup"><span data-stu-id="a81a7-190">Expand **Data + Analytics** to see **Data Factory V2** and **SSIS Integration Runtime**.</span></span>

```powershell
# Azure Data Factory information 
# If your input contains a PSH special character, e.g. "$", precede it with the escape character "`" like "`$". 
$SubscriptionName = "[Azure subscription name]"
$ResourceGroupName = "[Azure resource group name]"
# Data factory name. Must be globally unique
$DataFactoryName = "[Data factory name]"
$DataFactoryLocation = "EastUS"

# Azure-SSIS integration runtime information. This is a Data Factory compute resource for running SSIS packages
$AzureSSISName = "[Specify a name for your Azure-SSIS IR]"
$AzureSSISDescription = "[Specify a description for your Azure-SSIS IR]"
$AzureSSISLocation = "EastUS"
# In public preview, only Standard_A4_v2, Standard_A8_v2, Standard_D1_v2, Standard_D2_v2, Standard_D3_v2, Standard_D4_v2 are supported
$AzureSSISNodeSize = "Standard_D4_v2"
# In public preview, only 1-10 nodes are supported.
$AzureSSISNodeNumber = 2 
# Azure-SSIS IR edition/license info: Standard or Enterprise 
$AzureSSISEdition = "" # Standard by default, while Enterprise lets you use advanced/premium features on your Azure-SSIS IR
# Azure-SSIS IR hybrid usage info: LicenseIncluded or BasePrice
$AzureSSISLicenseType = "" # LicenseIncluded by default, while BasePrice lets you bring your own on-premises SQL Server license to earn cost savings from Azure Hybrid Benefit (AHB) option
# For a Standard_D1_v2 node, 1-4 parallel executions per node are supported. For other nodes, it's 1-8.
$AzureSSISMaxParallelExecutionsPerNode = 8
# Custom setup info
$SetupScriptContainerSasUri = "" # OPTIONAL to provide SAS URI of blob container where your custom setup script and its associated files are stored

# SSISDB info
$SSISDBServerEndpoint = "[your Azure SQL Database server name].database.windows.net" # WARNING: Please ensure that there is no existing SSISDB, so we can prepare and manage one on your behalf    
$SSISDBServerAdminUserName = "[your server admin username for SQL authentication]"
$SSISDBServerAdminPassword = "[your server admin password for SQL authentication]"
# For the basic pricing tier, specify "Basic", not "B". For standard/premium/Elastic Pool tiers, specify "S0", "S1", "S2", "S3", etc.
$SSISDBPricingTier = "[Basic|S0|S1|S2|S3|S4|S6|S7|S9|S12|P1|P2|P4|P6|P11|P15|…|ELASTIC_POOL(name = <elastic_pool_name>)]"

$SSISDBConnectionString = "Data Source=" + $SSISDBServerEndpoint + ";User ID=" + $SSISDBServerAdminUserName + ";Password=" + $SSISDBServerAdminPassword    
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $SSISDBConnectionString;
Try
{
    $sqlConnection.Open();
}
Catch [System.Data.SqlClient.SqlException]
{
    Write-Warning "Cannot connect to your Azure SQL Database server, exception: $_";
    Write-Warning "Please make sure the server you specified has already been created. Do you want to proceed? [Y/N]"
    $yn = Read-Host
    if(!($yn -ieq "Y"))
    {
        Return;
    } 
}

Connect-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

Set-AzureRmDataFactoryV2 -ResourceGroupName $ResourceGroupName `
                         -Location $DataFactoryLocation `
                         -Name $DataFactoryName
    
$secpasswd = ConvertTo-SecureString $SSISDBServerAdminPassword -AsPlainText -Force
$serverCreds = New-Object System.Management.Automation.PSCredential($SSISDBServerAdminUserName, $secpasswd)
    
Set-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName $ResourceGroupName `
                                           -DataFactoryName $DataFactoryName `
                                           -Name $AzureSSISName `
                                           -Description $AzureSSISDescription `
                                           -Type Managed `
                                           -Location $AzureSSISLocation `
                                           -NodeSize $AzureSSISNodeSize `
                                           -NodeCount $AzureSSISNodeNumber `
                                           -Edition $AzureSSISEdition `
                                           -LicenseType $AzureSSISLicenseType `
                                           -MaxParallelExecutionsPerNode $AzureSSISMaxParallelExecutionsPerNode `
                                           -SetupScriptContainerSasUri $SetupScriptContainerSasUri `
                                           -CatalogServerEndpoint $SSISDBServerEndpoint `
                                           -CatalogAdminCredential $serverCreds `
                                           -CatalogPricingTier $SSISDBPricingTier

write-host("##### Starting your Azure-SSIS integration runtime. This command takes 20 to 30 minutes to complete. #####")
Start-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName $ResourceGroupName `
                                             -DataFactoryName $DataFactoryName `
                                             -Name $AzureSSISName `
                                             -Force

write-host("##### Completed #####")
write-host("If any cmdlet is unsuccessful, please consider using -Debug option for diagnostics.")
```

## <a name="join-azure-ssis-ir-to-a-virtual-network"></a><span data-ttu-id="a81a7-191">Join Azure-SSIS IR to a virtual network</span><span class="sxs-lookup"><span data-stu-id="a81a7-191">Join Azure-SSIS IR to a virtual network</span></span>
<span data-ttu-id="a81a7-192">If you use Azure SQL Database with virtual network service endpoints/Managed Instance (Preview) that joins a virtual network to host SSISDB, you must also join your Azure-SSIS integration runtime to the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="a81a7-192">If you use Azure SQL Database with virtual network service endpoints/Managed Instance (Preview) that joins a virtual network to host SSISDB, you must also join your Azure-SSIS integration runtime to the same virtual network.</span></span> <span data-ttu-id="a81a7-193">Azure Data Factory lets you join your Azure-SSIS integration runtime to a virtual network.</span><span class="sxs-lookup"><span data-stu-id="a81a7-193">Azure Data Factory lets you join your Azure-SSIS integration runtime to a virtual network.</span></span> <span data-ttu-id="a81a7-194">For more information, see [Join Azure-SSIS integration runtime to a virtual network](join-azure-ssis-integration-runtime-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="a81a7-194">For more information, see [Join Azure-SSIS integration runtime to a virtual network](join-azure-ssis-integration-runtime-virtual-network.md).</span></span>

<span data-ttu-id="a81a7-195">For a full script to create an Azure-SSIS integration runtime that joins a virtual network, see [Create an Azure-SSIS integration runtime](create-azure-ssis-integration-runtime.md).</span><span class="sxs-lookup"><span data-stu-id="a81a7-195">For a full script to create an Azure-SSIS integration runtime that joins a virtual network, see [Create an Azure-SSIS integration runtime](create-azure-ssis-integration-runtime.md).</span></span>

## <a name="monitor-and-manage-azure-ssis-ir"></a><span data-ttu-id="a81a7-196">Monitor and manage Azure-SSIS IR</span><span class="sxs-lookup"><span data-stu-id="a81a7-196">Monitor and manage Azure-SSIS IR</span></span>
<span data-ttu-id="a81a7-197">See the following articles for details about monitoring and managing an Azure-SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="a81a7-197">See the following articles for details about monitoring and managing an Azure-SSIS IR.</span></span> 

- [<span data-ttu-id="a81a7-198">Monitor an Azure-SSIS integration runtime</span><span class="sxs-lookup"><span data-stu-id="a81a7-198">Monitor an Azure-SSIS integration runtime</span></span>](monitor-integration-runtime.md#azure-ssis-integration-runtime)
- [<span data-ttu-id="a81a7-199">Manage an Azure-SSIS integration runtime</span><span class="sxs-lookup"><span data-stu-id="a81a7-199">Manage an Azure-SSIS integration runtime</span></span>](manage-azure-ssis-integration-runtime.md)

## <a name="next-steps"></a><span data-ttu-id="a81a7-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="a81a7-200">Next steps</span></span>
<span data-ttu-id="a81a7-201">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="a81a7-201">In this tutorial, you learned how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="a81a7-202">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="a81a7-202">Create a data factory.</span></span>
> * <span data-ttu-id="a81a7-203">Create an Azure-SSIS integration runtime</span><span class="sxs-lookup"><span data-stu-id="a81a7-203">Create an Azure-SSIS integration runtime</span></span>
> * <span data-ttu-id="a81a7-204">Start the Azure-SSIS integration runtime</span><span class="sxs-lookup"><span data-stu-id="a81a7-204">Start the Azure-SSIS integration runtime</span></span>
> * <span data-ttu-id="a81a7-205">Deploy SSIS packages</span><span class="sxs-lookup"><span data-stu-id="a81a7-205">Deploy SSIS packages</span></span>
> * <span data-ttu-id="a81a7-206">Review the complete script</span><span class="sxs-lookup"><span data-stu-id="a81a7-206">Review the complete script</span></span>

<span data-ttu-id="a81a7-207">Advance to the following tutorial to learn about coping data from on-premises to cloud:</span><span class="sxs-lookup"><span data-stu-id="a81a7-207">Advance to the following tutorial to learn about coping data from on-premises to cloud:</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="a81a7-208">Copy data in cloud</span><span class="sxs-lookup"><span data-stu-id="a81a7-208">Copy data in cloud</span></span>](tutorial-copy-data-dot-net.md)
