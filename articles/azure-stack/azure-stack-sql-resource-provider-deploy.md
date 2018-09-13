---
title: Using SQL databases on Azure Stack | Microsoft Docs
description: Learn how you can deploy SQL databases as a service on Azure Stack and the quick steps to deploy the SQL Server resource provider adapter
services: azure-stack
documentationCenter: ''
author: JeffGoldner
manager: byronr
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: JeffGo
ms.openlocfilehash: 164280ac7cb19f4e3356bb959d97f7c4fe864927
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555514"
---
# <a name="use-sql-databases-on-azure-stack"></a><span data-ttu-id="f59e5-103">Use SQL databases on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="f59e5-103">Use SQL databases on Azure Stack</span></span>

> [!NOTE]
> <span data-ttu-id="f59e5-104">The following information only applies to Azure Stack TP3 Refresh deployments.</span><span class="sxs-lookup"><span data-stu-id="f59e5-104">The following information only applies to Azure Stack TP3 Refresh deployments.</span></span>
>
>

<span data-ttu-id="f59e5-105">Use the SQL Server resource provider adapter to expose SQL databases as a service of Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="f59e5-105">Use the SQL Server resource provider adapter to expose SQL databases as a service of Azure Stack.</span></span> <span data-ttu-id="f59e5-106">After you install the resource provider and connect it to a SQL Server instance, you and your users can create databases for cloud-native apps, websites that are based on SQL, and workloads that are based on SQL without having to provision a virtual machine (VM) that hosts SQL Server each time.</span><span class="sxs-lookup"><span data-stu-id="f59e5-106">After you install the resource provider and connect it to a SQL Server instance, you and your users can create databases for cloud-native apps, websites that are based on SQL, and workloads that are based on SQL without having to provision a virtual machine (VM) that hosts SQL Server each time.</span></span>

## <a name="sql-server-resource-provider-adapter-architecture"></a><span data-ttu-id="f59e5-107">SQL Server resource provider adapter architecture</span><span class="sxs-lookup"><span data-stu-id="f59e5-107">SQL Server resource provider adapter architecture</span></span>
<span data-ttu-id="f59e5-108">The resource provider is not based on, nor does it offer all the database management capabilities of Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="f59e5-108">The resource provider is not based on, nor does it offer all the database management capabilities of Azure SQL Database.</span></span> <span data-ttu-id="f59e5-109">For example, elastic database pools and the ability to dial database performance up and down automatically aren't available.</span><span class="sxs-lookup"><span data-stu-id="f59e5-109">For example, elastic database pools and the ability to dial database performance up and down automatically aren't available.</span></span> <span data-ttu-id="f59e5-110">However, the resource provider does support similar create, read, update, and delete (CRUD) operations.</span><span class="sxs-lookup"><span data-stu-id="f59e5-110">However, the resource provider does support similar create, read, update, and delete (CRUD) operations.</span></span>

<span data-ttu-id="f59e5-111">The resource provider is made up of three components:</span><span class="sxs-lookup"><span data-stu-id="f59e5-111">The resource provider is made up of three components:</span></span>

- <span data-ttu-id="f59e5-112">**The SQL resource provider adapter VM**, which encompasses the resource provider process and the servers that host a small SQL Server used for RP state and as a sample Hosting Server.</span><span class="sxs-lookup"><span data-stu-id="f59e5-112">**The SQL resource provider adapter VM**, which encompasses the resource provider process and the servers that host a small SQL Server used for RP state and as a sample Hosting Server.</span></span>
- <span data-ttu-id="f59e5-113">**The resource provider itself**, which processes provisioning requests and exposes database resources.</span><span class="sxs-lookup"><span data-stu-id="f59e5-113">**The resource provider itself**, which processes provisioning requests and exposes database resources.</span></span>
- <span data-ttu-id="f59e5-114">**Servers that host SQL Server**, which provide capacity for databases, called Hosting Servers</span><span class="sxs-lookup"><span data-stu-id="f59e5-114">**Servers that host SQL Server**, which provide capacity for databases, called Hosting Servers</span></span>

> [!NOTE]
> <span data-ttu-id="f59e5-115">The SQL Server Resource Provider Adapter requires an Azure Stack TP3 Refresh deployment.</span><span class="sxs-lookup"><span data-stu-id="f59e5-115">The SQL Server Resource Provider Adapter requires an Azure Stack TP3 Refresh deployment.</span></span>
>
>

<span data-ttu-id="f59e5-116">You can offer SQL Server databases as a service to your Azure Stack users.</span><span class="sxs-lookup"><span data-stu-id="f59e5-116">You can offer SQL Server databases as a service to your Azure Stack users.</span></span> <span data-ttu-id="f59e5-117">To do so, you must deploy the SQL Server resource provider, connect it to a SQL Server instance, and then create plans and offers that users can subscribe to.</span><span class="sxs-lookup"><span data-stu-id="f59e5-117">To do so, you must deploy the SQL Server resource provider, connect it to a SQL Server instance, and then create plans and offers that users can subscribe to.</span></span> <span data-ttu-id="f59e5-118">Users who subscribe can then create databases for cloud native apps and SQL-based websites and workloads without having to provision a SQL Server virtual machine each time.</span><span class="sxs-lookup"><span data-stu-id="f59e5-118">Users who subscribe can then create databases for cloud native apps and SQL-based websites and workloads without having to provision a SQL Server virtual machine each time.</span></span>

<span data-ttu-id="f59e5-119">The resource provider is made up of three components:</span><span class="sxs-lookup"><span data-stu-id="f59e5-119">The resource provider is made up of three components:</span></span>

- <span data-ttu-id="f59e5-120">**The SQL resource provider adapter VM**: the VM on which the resource provider and servers hosting SQL server reside.</span><span class="sxs-lookup"><span data-stu-id="f59e5-120">**The SQL resource provider adapter VM**: the VM on which the resource provider and servers hosting SQL server reside.</span></span>
- <span data-ttu-id="f59e5-121">**The resource provider**: processes provisioning requests and provides database resources.</span><span class="sxs-lookup"><span data-stu-id="f59e5-121">**The resource provider**: processes provisioning requests and provides database resources.</span></span>
- <span data-ttu-id="f59e5-122">**Servers that host SQL Server**: provides capacity for databases.</span><span class="sxs-lookup"><span data-stu-id="f59e5-122">**Servers that host SQL Server**: provides capacity for databases.</span></span>

<span data-ttu-id="f59e5-123">The resource provider does not support all of the database management capabilities of [Azure SQL Database](https://azure.microsoft.com/en-us/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="f59e5-123">The resource provider does not support all of the database management capabilities of [Azure SQL Database](https://azure.microsoft.com/en-us/services/sql-database/).</span></span> <span data-ttu-id="f59e5-124">For example, elastic database pools and the ability to dial database performance up and down automatically aren't supported.</span><span class="sxs-lookup"><span data-stu-id="f59e5-124">For example, elastic database pools and the ability to dial database performance up and down automatically aren't supported.</span></span>

### <a name="deploy-without-internet-access"></a><span data-ttu-id="f59e5-125">Deploy without internet access</span><span class="sxs-lookup"><span data-stu-id="f59e5-125">Deploy without internet access</span></span>

<span data-ttu-id="f59e5-126">To deploy the SQL provider on a system that does not have internet access, you can copy the file [SQL 2014 SP1 Enterprise Evaluation ISO](http://care.dlservice.microsoft.com/dl/download/2/F/8/2F8F7165-BB21-4D1E-B5D8-3BD3CE73C77D/SQLServer2014SP1-FullSlipstream-x64-ENU.iso) to a local file share and provide that share name when prompted (see below).</span><span class="sxs-lookup"><span data-stu-id="f59e5-126">To deploy the SQL provider on a system that does not have internet access, you can copy the file [SQL 2014 SP1 Enterprise Evaluation ISO](http://care.dlservice.microsoft.com/dl/download/2/F/8/2F8F7165-BB21-4D1E-B5D8-3BD3CE73C77D/SQLServer2014SP1-FullSlipstream-x64-ENU.iso) to a local file share and provide that share name when prompted (see below).</span></span> <span data-ttu-id="f59e5-127">You will also need to provision the Windows Server 2016 VM image and install the PowerShell module using the offline procedure.</span><span class="sxs-lookup"><span data-stu-id="f59e5-127">You will also need to provision the Windows Server 2016 VM image and install the PowerShell module using the offline procedure.</span></span>

> [!NOTE]
> <span data-ttu-id="f59e5-128">The deployment script will perform retries, if necessary, to accommodate less reliable network connections or if an operation exceeds a timeout.</span><span class="sxs-lookup"><span data-stu-id="f59e5-128">The deployment script will perform retries, if necessary, to accommodate less reliable network connections or if an operation exceeds a timeout.</span></span>
>
>

## <a name="deploy-the-resource-provider"></a><span data-ttu-id="f59e5-129">Deploy the resource provider</span><span class="sxs-lookup"><span data-stu-id="f59e5-129">Deploy the resource provider</span></span>

1. <span data-ttu-id="f59e5-130">If you have not already done so, create a [Windows Server 2016 image with the .NET 3.5 runtime](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-add-default-image) installed.</span><span class="sxs-lookup"><span data-stu-id="f59e5-130">If you have not already done so, create a [Windows Server 2016 image with the .NET 3.5 runtime](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-add-default-image) installed.</span></span>

  > [!NOTE]
  > <span data-ttu-id="f59e5-131">The current RP uses SQL Server 2014 SP1, which requires the .NET 3.5 runtime - if your image does not contain this optional component, the deployment will fail.</span><span class="sxs-lookup"><span data-stu-id="f59e5-131">The current RP uses SQL Server 2014 SP1, which requires the .NET 3.5 runtime - if your image does not contain this optional component, the deployment will fail.</span></span>
  >
  >

2. <span data-ttu-id="f59e5-132">Sign in to the POC host, [download the SQL Server RP installer executable file](https://aka.ms/azurestacksqlrptp3), and extract the files to a temporary directory.</span><span class="sxs-lookup"><span data-stu-id="f59e5-132">Sign in to the POC host, [download the SQL Server RP installer executable file](https://aka.ms/azurestacksqlrptp3), and extract the files to a temporary directory.</span></span> <span data-ttu-id="f59e5-133">If your POC host has limited hard disk space, you can instead download the executable to another computer and then copy the extracted files to the POC host.</span><span class="sxs-lookup"><span data-stu-id="f59e5-133">If your POC host has limited hard disk space, you can instead download the executable to another computer and then copy the extracted files to the POC host.</span></span>

3. <span data-ttu-id="f59e5-134">If you have installed any versions of the AzureRm PowerShell module other than 1.2.9, you will need to remove them or the install will not proceed.</span><span class="sxs-lookup"><span data-stu-id="f59e5-134">If you have installed any versions of the AzureRm PowerShell module other than 1.2.9, you will need to remove them or the install will not proceed.</span></span>

4. <span data-ttu-id="f59e5-135">Open a **new** elevated PowerShell console and change to the directory where you extracted the files.</span><span class="sxs-lookup"><span data-stu-id="f59e5-135">Open a **new** elevated PowerShell console and change to the directory where you extracted the files.</span></span> <span data-ttu-id="f59e5-136">Use a new window to avoid problems that may arise from incorrect PowerShell modules already loaded on the system.</span><span class="sxs-lookup"><span data-stu-id="f59e5-136">Use a new window to avoid problems that may arise from incorrect PowerShell modules already loaded on the system.</span></span>

5. <span data-ttu-id="f59e5-137">Run the DeploySqlProvider.ps1 script with the parameters listed below.</span><span class="sxs-lookup"><span data-stu-id="f59e5-137">Run the DeploySqlProvider.ps1 script with the parameters listed below.</span></span> <span data-ttu-id="f59e5-138">Depending on your hardware and download speed, it may take up to 60 minutes for the resource provider to get up and running, and another 60 minutes for the configuration of the virtual machines to complete.</span><span class="sxs-lookup"><span data-stu-id="f59e5-138">Depending on your hardware and download speed, it may take up to 60 minutes for the resource provider to get up and running, and another 60 minutes for the configuration of the virtual machines to complete.</span></span>

* <span data-ttu-id="f59e5-139">If necessary, download a compatible version of Azure PowerShell (only AzureRm version 1.2.9 is supported).</span><span class="sxs-lookup"><span data-stu-id="f59e5-139">If necessary, download a compatible version of Azure PowerShell (only AzureRm version 1.2.9 is supported).</span></span>
* <span data-ttu-id="f59e5-140">Create a wildcard certificate to secure communication between the resource provider and Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f59e5-140">Create a wildcard certificate to secure communication between the resource provider and Azure Resource Manager.</span></span>
* <span data-ttu-id="f59e5-141">Download an evaluation build of SQL Server SP1 from the internet or from a local file share.</span><span class="sxs-lookup"><span data-stu-id="f59e5-141">Download an evaluation build of SQL Server SP1 from the internet or from a local file share.</span></span>
* <span data-ttu-id="f59e5-142">Upload the certificate and all other artifacts to a storage account on your Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="f59e5-142">Upload the certificate and all other artifacts to a storage account on your Azure Stack.</span></span>
* <span data-ttu-id="f59e5-143">Publish gallery package so that you can deploy SQL database through the gallery.</span><span class="sxs-lookup"><span data-stu-id="f59e5-143">Publish gallery package so that you can deploy SQL database through the gallery.</span></span>
* <span data-ttu-id="f59e5-144">Deploy a VM using the Windows Server image create in step 1.</span><span class="sxs-lookup"><span data-stu-id="f59e5-144">Deploy a VM using the Windows Server image create in step 1.</span></span>
* <span data-ttu-id="f59e5-145">Register a local DNS record that maps to your resource provider VM.</span><span class="sxs-lookup"><span data-stu-id="f59e5-145">Register a local DNS record that maps to your resource provider VM.</span></span>
* <span data-ttu-id="f59e5-146">Register your resource provider with the local Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f59e5-146">Register your resource provider with the local Azure Resource Manager.</span></span>

> <span data-ttu-id="f59e5-147">If the installation takes more than 90 minutes, it may fail and you will see a failure message on the screen and in the log file, but the deployment will be retried from the failing step.</span><span class="sxs-lookup"><span data-stu-id="f59e5-147">If the installation takes more than 90 minutes, it may fail and you will see a failure message on the screen and in the log file, but the deployment will be retried from the failing step.</span></span> <span data-ttu-id="f59e5-148">Systems that do not meet the minimum required memory and core specifications may not be able to deploy the SQL RP.</span><span class="sxs-lookup"><span data-stu-id="f59e5-148">Systems that do not meet the minimum required memory and core specifications may not be able to deploy the SQL RP.</span></span>
>

### <a name="deploysqlproviderps1-parameters"></a><span data-ttu-id="f59e5-149">DeploySqlProvider.ps1 Parameters</span><span class="sxs-lookup"><span data-stu-id="f59e5-149">DeploySqlProvider.ps1 Parameters</span></span>

| <span data-ttu-id="f59e5-150">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="f59e5-150">Parameter Name</span></span> | <span data-ttu-id="f59e5-151">Description</span><span class="sxs-lookup"><span data-stu-id="f59e5-151">Description</span></span> | <span data-ttu-id="f59e5-152">Comment or Default Value</span><span class="sxs-lookup"><span data-stu-id="f59e5-152">Comment or Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f59e5-153">**DirectoryTenantID**</span><span class="sxs-lookup"><span data-stu-id="f59e5-153">**DirectoryTenantID**</span></span> | <span data-ttu-id="f59e5-154">Provide the GUID of the Azure Active Directory used for the Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="f59e5-154">Provide the GUID of the Azure Active Directory used for the Azure Stack deployment.</span></span> <span data-ttu-id="f59e5-155">This can be obtained using the Get-AADTenantGUID command.</span><span class="sxs-lookup"><span data-stu-id="f59e5-155">This can be obtained using the Get-AADTenantGUID command.</span></span> <span data-ttu-id="f59e5-156">For example, Get-AADTenantGUID - AADTenantName "mydomain.onmicrosoft.com"</span><span class="sxs-lookup"><span data-stu-id="f59e5-156">For example, Get-AADTenantGUID - AADTenantName "mydomain.onmicrosoft.com"</span></span> | <span data-ttu-id="f59e5-157">_required_</span><span class="sxs-lookup"><span data-stu-id="f59e5-157">_required_</span></span> |
| <span data-ttu-id="f59e5-158">**AzCredential**</span><span class="sxs-lookup"><span data-stu-id="f59e5-158">**AzCredential**</span></span> | <span data-ttu-id="f59e5-159">Provide the credentails for the Azure Stack Service Admin account.</span><span class="sxs-lookup"><span data-stu-id="f59e5-159">Provide the credentails for the Azure Stack Service Admin account.</span></span> <span data-ttu-id="f59e5-160">You must use the same credentials as you used for deploying Azure Stack).</span><span class="sxs-lookup"><span data-stu-id="f59e5-160">You must use the same credentials as you used for deploying Azure Stack).</span></span> <span data-ttu-id="f59e5-161">You can use the **New-Object** command to define this info, such as: `New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AADAdminPass)`.</span><span class="sxs-lookup"><span data-stu-id="f59e5-161">You can use the **New-Object** command to define this info, such as: `New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AADAdminPass)`.</span></span> | <span data-ttu-id="f59e5-162">_required_</span><span class="sxs-lookup"><span data-stu-id="f59e5-162">_required_</span></span> |
| <span data-ttu-id="f59e5-163">**VMLocalCredential**</span><span class="sxs-lookup"><span data-stu-id="f59e5-163">**VMLocalCredential**</span></span> | <span data-ttu-id="f59e5-164">Define the credentials for the local administrator account of the SQL resource provider VM.</span><span class="sxs-lookup"><span data-stu-id="f59e5-164">Define the credentials for the local administrator account of the SQL resource provider VM.</span></span> <span data-ttu-id="f59e5-165">This password will also be used for the SQL **sa** account.</span><span class="sxs-lookup"><span data-stu-id="f59e5-165">This password will also be used for the SQL **sa** account.</span></span> <span data-ttu-id="f59e5-166">You can use the **New-Object** command to provide this info, such as: `New-Object System.Management.Automation.PSCredential ("sqlrpadmin", $vmLocalAdminPass)`.</span><span class="sxs-lookup"><span data-stu-id="f59e5-166">You can use the **New-Object** command to provide this info, such as: `New-Object System.Management.Automation.PSCredential ("sqlrpadmin", $vmLocalAdminPass)`.</span></span> | <span data-ttu-id="f59e5-167">_required_</span><span class="sxs-lookup"><span data-stu-id="f59e5-167">_required_</span></span> |
| <span data-ttu-id="f59e5-168">**ResourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="f59e5-168">**ResourceGroupName**</span></span> | <span data-ttu-id="f59e5-169">Define a name for a Resource Group in which items created by this script will be stored.</span><span class="sxs-lookup"><span data-stu-id="f59e5-169">Define a name for a Resource Group in which items created by this script will be stored.</span></span> <span data-ttu-id="f59e5-170">For example, *System.Sql*.</span><span class="sxs-lookup"><span data-stu-id="f59e5-170">For example, *System.Sql*.</span></span> | <span data-ttu-id="f59e5-171">Microsoft-SQL-RP1</span><span class="sxs-lookup"><span data-stu-id="f59e5-171">Microsoft-SQL-RP1</span></span> |
| <span data-ttu-id="f59e5-172">**VmName**</span><span class="sxs-lookup"><span data-stu-id="f59e5-172">**VmName**</span></span> | <span data-ttu-id="f59e5-173">Define the name of the virtual machine on which to install the resource provider.</span><span class="sxs-lookup"><span data-stu-id="f59e5-173">Define the name of the virtual machine on which to install the resource provider.</span></span> <span data-ttu-id="f59e5-174">For example, *SystemSqlRP*.</span><span class="sxs-lookup"><span data-stu-id="f59e5-174">For example, *SystemSqlRP*.</span></span> | <span data-ttu-id="f59e5-175">sqlvm</span><span class="sxs-lookup"><span data-stu-id="f59e5-175">sqlvm</span></span> |
| <span data-ttu-id="f59e5-176">**DependencyFilesLocalPath**</span><span class="sxs-lookup"><span data-stu-id="f59e5-176">**DependencyFilesLocalPath**</span></span> | <span data-ttu-id="f59e5-177">If you're doing an offline deployment, this is path to a local share containing the SQL ISO.</span><span class="sxs-lookup"><span data-stu-id="f59e5-177">If you're doing an offline deployment, this is path to a local share containing the SQL ISO.</span></span> <span data-ttu-id="f59e5-178">You can download [SQL 2014 SP1 Enterprise Evaluation ISO](http://care.dlservice.microsoft.com/dl/download/2/F/8/2F8F7165-BB21-4D1E-B5D8-3BD3CE73C77D/SQLServer2014SP1-FullSlipstream-x64-ENU.iso) from the Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="f59e5-178">You can download [SQL 2014 SP1 Enterprise Evaluation ISO](http://care.dlservice.microsoft.com/dl/download/2/F/8/2F8F7165-BB21-4D1E-B5D8-3BD3CE73C77D/SQLServer2014SP1-FullSlipstream-x64-ENU.iso) from the Microsoft Download Center.</span></span> | <span data-ttu-id="f59e5-179">_leave blank to download from the internet_</span><span class="sxs-lookup"><span data-stu-id="f59e5-179">_leave blank to download from the internet_</span></span> |
| <span data-ttu-id="f59e5-180">**MaxRetryCount**</span><span class="sxs-lookup"><span data-stu-id="f59e5-180">**MaxRetryCount**</span></span> | <span data-ttu-id="f59e5-181">Define how many times you want to retry each operation if there is a failure.</span><span class="sxs-lookup"><span data-stu-id="f59e5-181">Define how many times you want to retry each operation if there is a failure.</span></span>| <span data-ttu-id="f59e5-182">2</span><span class="sxs-lookup"><span data-stu-id="f59e5-182">2</span></span> |
| <span data-ttu-id="f59e5-183">**RetryDuration**</span><span class="sxs-lookup"><span data-stu-id="f59e5-183">**RetryDuration**</span></span> | <span data-ttu-id="f59e5-184">Define the timeout between retries, in seconds.</span><span class="sxs-lookup"><span data-stu-id="f59e5-184">Define the timeout between retries, in seconds.</span></span> | <span data-ttu-id="f59e5-185">120</span><span class="sxs-lookup"><span data-stu-id="f59e5-185">120</span></span> |
| <span data-ttu-id="f59e5-186">**Uninstall**</span><span class="sxs-lookup"><span data-stu-id="f59e5-186">**Uninstall**</span></span> | <span data-ttu-id="f59e5-187">Clean up the resource provider and remove all resources (see notes below)</span><span class="sxs-lookup"><span data-stu-id="f59e5-187">Clean up the resource provider and remove all resources (see notes below)</span></span> | <span data-ttu-id="f59e5-188">No</span><span class="sxs-lookup"><span data-stu-id="f59e5-188">No</span></span> |
| <span data-ttu-id="f59e5-189">**DebugMode**</span><span class="sxs-lookup"><span data-stu-id="f59e5-189">**DebugMode**</span></span> | <span data-ttu-id="f59e5-190">Prevents automatic clean up on failure</span><span class="sxs-lookup"><span data-stu-id="f59e5-190">Prevents automatic clean up on failure</span></span> | <span data-ttu-id="f59e5-191">No</span><span class="sxs-lookup"><span data-stu-id="f59e5-191">No</span></span> |

<span data-ttu-id="f59e5-192">You can specify these parameters in the command line.</span><span class="sxs-lookup"><span data-stu-id="f59e5-192">You can specify these parameters in the command line.</span></span> <span data-ttu-id="f59e5-193">If you do not, or parameter validation failes, you will be prompted to provide them.</span><span class="sxs-lookup"><span data-stu-id="f59e5-193">If you do not, or parameter validation failes, you will be prompted to provide them.</span></span>

<span data-ttu-id="f59e5-194">Here's an example you can run from the PowerShell prompt (but change the account information and portal endpoints as needed):</span><span class="sxs-lookup"><span data-stu-id="f59e5-194">Here's an example you can run from the PowerShell prompt (but change the account information and portal endpoints as needed):</span></span>

```
$vmLocalAdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("sqlrpadmin", $vmLocalAdminPass)

$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)

$DirectoryTenantID = Get-AADTenantGUID -AADTenantName "mydomain.onmicrosoft.com"

.\DeploySQLProvider.ps1 -DirectoryTenantID $DirectoryTenantID -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "System.Sql" -VmName "SQLVM" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external"
 ```

## <a name="verify-the-deployment-using-the-azure-stack-portal"></a><span data-ttu-id="f59e5-195">Verify the deployment using the Azure Stack Portal</span><span class="sxs-lookup"><span data-stu-id="f59e5-195">Verify the deployment using the Azure Stack Portal</span></span>

> [!NOTE]
>  <span data-ttu-id="f59e5-196">After the installation script completes, it can take up to 60 minutes for all of the virtual machines to finish configuration.</span><span class="sxs-lookup"><span data-stu-id="f59e5-196">After the installation script completes, it can take up to 60 minutes for all of the virtual machines to finish configuration.</span></span> <span data-ttu-id="f59e5-197">If you attempt the next steps before this completes, you will see failures.</span><span class="sxs-lookup"><span data-stu-id="f59e5-197">If you attempt the next steps before this completes, you will see failures.</span></span>
>
>

1. <span data-ttu-id="f59e5-198">On the Console VM desktop, click **Microsoft Azure Stack Portal** and sign in to the portal as the service administrator.</span><span class="sxs-lookup"><span data-stu-id="f59e5-198">On the Console VM desktop, click **Microsoft Azure Stack Portal** and sign in to the portal as the service administrator.</span></span>

2. <span data-ttu-id="f59e5-199">Verify that the deployment succeeded.</span><span class="sxs-lookup"><span data-stu-id="f59e5-199">Verify that the deployment succeeded.</span></span> <span data-ttu-id="f59e5-200">Click **Resource Groups** &gt; click the resource group you used (default is **Microsoft-SQL-RP1**), and then make sure that the essentials part of the blade (upper half) reads **_date_ (Succeeded)**.</span><span class="sxs-lookup"><span data-stu-id="f59e5-200">Click **Resource Groups** &gt; click the resource group you used (default is **Microsoft-SQL-RP1**), and then make sure that the essentials part of the blade (upper half) reads **_date_ (Succeeded)**.</span></span>

      ![Verify Deployment of the SQL RP](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-sql-rp-deploy/5.png)

3. <span data-ttu-id="f59e5-202">Verify that the registration succeeded.</span><span class="sxs-lookup"><span data-stu-id="f59e5-202">Verify that the registration succeeded.</span></span> <span data-ttu-id="f59e5-203">Click **Resource providers**, and then look for **SQLAdapter**:</span><span class="sxs-lookup"><span data-stu-id="f59e5-203">Click **Resource providers**, and then look for **SQLAdapter**:</span></span>

      ![Verify the SQL RP was registered](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-sql-rp-deploy/6.png)


## <a name="provide-capacity-by-connecting-it-to-a-hosting-sql-server"></a><span data-ttu-id="f59e5-205">Provide capacity by connecting it to a hosting SQL server</span><span class="sxs-lookup"><span data-stu-id="f59e5-205">Provide capacity by connecting it to a hosting SQL server</span></span>

1. <span data-ttu-id="f59e5-206">Sign in to the Azure Stack admin portal as a service admin</span><span class="sxs-lookup"><span data-stu-id="f59e5-206">Sign in to the Azure Stack admin portal as a service admin</span></span>

2. <span data-ttu-id="f59e5-207">Click **Resource Providers** &gt; **SQLAdapter** &gt; **Hosting Servers** &gt; **+Add**.</span><span class="sxs-lookup"><span data-stu-id="f59e5-207">Click **Resource Providers** &gt; **SQLAdapter** &gt; **Hosting Servers** &gt; **+Add**.</span></span>

    <span data-ttu-id="f59e5-208">The **SQL Hosting Servers** blade is where you can connect the SQL Server Resource Provider to actual instances of SQL Server that serve as the resource provider’s backend.</span><span class="sxs-lookup"><span data-stu-id="f59e5-208">The **SQL Hosting Servers** blade is where you can connect the SQL Server Resource Provider to actual instances of SQL Server that serve as the resource provider’s backend.</span></span>

    ![Hosting Servers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-sql-rp-deploy/multiplehostingservers.PNG)

3. <span data-ttu-id="f59e5-210">Fill the form with the connection details of your SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="f59e5-210">Fill the form with the connection details of your SQL Server instance.</span></span> <span data-ttu-id="f59e5-211">By default, a preconfigured SQL Server called “SQLVM” with the administrator username “sa” and the password you called out in the "LocalCredential" parameter is running on the VM.</span><span class="sxs-lookup"><span data-stu-id="f59e5-211">By default, a preconfigured SQL Server called “SQLVM” with the administrator username “sa” and the password you called out in the "LocalCredential" parameter is running on the VM.</span></span> <span data-ttu-id="f59e5-212">You will need to specify the fully-qualified domain name (FQDN) or IPv4 address of each hosting server you add.</span><span class="sxs-lookup"><span data-stu-id="f59e5-212">You will need to specify the fully-qualified domain name (FQDN) or IPv4 address of each hosting server you add.</span></span> <span data-ttu-id="f59e5-213">Specify the maximum size of the server (for all databases).</span><span class="sxs-lookup"><span data-stu-id="f59e5-213">Specify the maximum size of the server (for all databases).</span></span>

    ![New Hosting Server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-sql-rp-deploy/sqlrp-newhostingserver.PNG)

4.  <span data-ttu-id="f59e5-215">As you add servers, you will need to assign a SKU or create a new one.</span><span class="sxs-lookup"><span data-stu-id="f59e5-215">As you add servers, you will need to assign a SKU or create a new one.</span></span> <span data-ttu-id="f59e5-216">This allows differentiation of service offerings.</span><span class="sxs-lookup"><span data-stu-id="f59e5-216">This allows differentiation of service offerings.</span></span> <span data-ttu-id="f59e5-217">For example, you could have a SQL Enterprise instance providing database capacity and automatic backup, reserve high performance servers for individual departments, etc. The SKU name should reflect the properties so that tenants can place their databases appropriately.</span><span class="sxs-lookup"><span data-stu-id="f59e5-217">For example, you could have a SQL Enterprise instance providing database capacity and automatic backup, reserve high performance servers for individual departments, etc. The SKU name should reflect the properties so that tenants can place their databases appropriately.</span></span>

    <span data-ttu-id="f59e5-218">An example:</span><span class="sxs-lookup"><span data-stu-id="f59e5-218">An example:</span></span>

    ![SKUs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-sql-rp-deploy/sqlrp-newsku.PNG)


## <a name="create-your-first-sql-database-to-test-your-deployment"></a><span data-ttu-id="f59e5-220">Create your first SQL Database to test your deployment</span><span class="sxs-lookup"><span data-stu-id="f59e5-220">Create your first SQL Database to test your deployment</span></span>

1. <span data-ttu-id="f59e5-221">Sign in to the Azure Stack admin portal as service admin.</span><span class="sxs-lookup"><span data-stu-id="f59e5-221">Sign in to the Azure Stack admin portal as service admin.</span></span>

2. <span data-ttu-id="f59e5-222">Click **+ New** &gt;**Data + Storage"** &gt; **SQL Server Database (preview)** &gt; **Add**</span><span class="sxs-lookup"><span data-stu-id="f59e5-222">Click **+ New** &gt;**Data + Storage"** &gt; **SQL Server Database (preview)** &gt; **Add**</span></span>

3. <span data-ttu-id="f59e5-223">Fill in the form with database details, including a **Database Name**, **Maximum Size**, and change the other parameters as necessary.</span><span class="sxs-lookup"><span data-stu-id="f59e5-223">Fill in the form with database details, including a **Database Name**, **Maximum Size**, and change the other parameters as necessary.</span></span>

    ![New database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-sql-rp-deploy/sqlrp-newdb.PNG)


4. <span data-ttu-id="f59e5-225">Fill in the Login Settings: **Database login**, and **Password**.</span><span class="sxs-lookup"><span data-stu-id="f59e5-225">Fill in the Login Settings: **Database login**, and **Password**.</span></span> <span data-ttu-id="f59e5-226">These is a SQL Authentication credential that will be created for your access to this database only.</span><span class="sxs-lookup"><span data-stu-id="f59e5-226">These is a SQL Authentication credential that will be created for your access to this database only.</span></span> <span data-ttu-id="f59e5-227">The login user name must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="f59e5-227">The login user name must be globally unique.</span></span>

    ![SQL Database Login Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-sql-rp-deploy/sqlrp-db-loginsettings.png)

4. <span data-ttu-id="f59e5-229">You are asked to pick a SKU for your database.</span><span class="sxs-lookup"><span data-stu-id="f59e5-229">You are asked to pick a SKU for your database.</span></span> <span data-ttu-id="f59e5-230">As hosting servers are added, they are assigned a SKU and databases are created in that pool of hosting servers that make up the SKU.</span><span class="sxs-lookup"><span data-stu-id="f59e5-230">As hosting servers are added, they are assigned a SKU and databases are created in that pool of hosting servers that make up the SKU.</span></span>

    ![Pick a SKU](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-sql-rp-deploy/sqlrp-select-sku.png)


5. <span data-ttu-id="f59e5-232">Submit the form and wait for the deployment to complete.</span><span class="sxs-lookup"><span data-stu-id="f59e5-232">Submit the form and wait for the deployment to complete.</span></span>

6. <span data-ttu-id="f59e5-233">In the resulting blade, notice the “Connection string” field.</span><span class="sxs-lookup"><span data-stu-id="f59e5-233">In the resulting blade, notice the “Connection string” field.</span></span> <span data-ttu-id="f59e5-234">You can use that string in any application that requires SQL Server access (for example, a web app) in your Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="f59e5-234">You can use that string in any application that requires SQL Server access (for example, a web app) in your Azure Stack.</span></span>

    ![Retrieve the connection string](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-sql-rp-deploy/11.png)

## <a name="add-capacity"></a><span data-ttu-id="f59e5-236">Add Capacity</span><span class="sxs-lookup"><span data-stu-id="f59e5-236">Add Capacity</span></span>

<span data-ttu-id="f59e5-237">Add Capacity by adding additional SQL hosts in the Azure Stack portal.</span><span class="sxs-lookup"><span data-stu-id="f59e5-237">Add Capacity by adding additional SQL hosts in the Azure Stack portal.</span></span> <span data-ttu-id="f59e5-238">If you wish to use another instance of SQL instead of the one installed on the provider VM, click **Resource Providers** &gt; **SQLAdapter** &gt; **SQL Hosting Servers** &gt; **+Add**.</span><span class="sxs-lookup"><span data-stu-id="f59e5-238">If you wish to use another instance of SQL instead of the one installed on the provider VM, click **Resource Providers** &gt; **SQLAdapter** &gt; **SQL Hosting Servers** &gt; **+Add**.</span></span>

## <a name="making-sql-databases-available-to-tenants"></a><span data-ttu-id="f59e5-239">Making SQL databases available to tenants</span><span class="sxs-lookup"><span data-stu-id="f59e5-239">Making SQL databases available to tenants</span></span>

<span data-ttu-id="f59e5-240">Create plans and offers to make SQL databases available for tenants.</span><span class="sxs-lookup"><span data-stu-id="f59e5-240">Create plans and offers to make SQL databases available for tenants.</span></span> <span data-ttu-id="f59e5-241">You will need to create a plan, add the Microsoft.SqlAdapter service to the plan, and add an existing Quota, or create a new one.</span><span class="sxs-lookup"><span data-stu-id="f59e5-241">You will need to create a plan, add the Microsoft.SqlAdapter service to the plan, and add an existing Quota, or create a new one.</span></span> <span data-ttu-id="f59e5-242">If you create a quota, you can specify the capacity to allow the tenant.</span><span class="sxs-lookup"><span data-stu-id="f59e5-242">If you create a quota, you can specify the capacity to allow the tenant.</span></span>
    <span data-ttu-id="f59e5-243">![Create plans and offers to include databases](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-sql-rp-deploy/12.PNG)</span><span class="sxs-lookup"><span data-stu-id="f59e5-243">![Create plans and offers to include databases](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-sql-rp-deploy/12.PNG)</span></span>

## <a name="tenant-usage-of-the-resource-provider"></a><span data-ttu-id="f59e5-244">Tenant Usage of the Resource Provider</span><span class="sxs-lookup"><span data-stu-id="f59e5-244">Tenant Usage of the Resource Provider</span></span>

<span data-ttu-id="f59e5-245">Self-service databases are provided through the tenant portal experience.</span><span class="sxs-lookup"><span data-stu-id="f59e5-245">Self-service databases are provided through the tenant portal experience.</span></span> <span data-ttu-id="f59e5-246">Once the administrator has performed the above steps, a tenant will need to register the resource provider before they will be able to create databases.</span><span class="sxs-lookup"><span data-stu-id="f59e5-246">Once the administrator has performed the above steps, a tenant will need to register the resource provider before they will be able to create databases.</span></span>

<span data-ttu-id="f59e5-247">To do so, the following command must be executed in a PowerShell window:</span><span class="sxs-lookup"><span data-stu-id="f59e5-247">To do so, the following command must be executed in a PowerShell window:</span></span>

```
Register-AzureRMResourceProvider –ProviderNamespace Microsoft.SQLAdapter
```


## <a name="next-steps"></a><span data-ttu-id="f59e5-248">Next steps</span><span class="sxs-lookup"><span data-stu-id="f59e5-248">Next steps</span></span>


<span data-ttu-id="f59e5-249">Try other [PaaS services](azure-stack-tools-paas-services.md) like the [MySQL Server resource provider](azure-stack-mysql-resource-provider-deploy.md) and the [App Services resource provider](azure-stack-app-service-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f59e5-249">Try other [PaaS services](azure-stack-tools-paas-services.md) like the [MySQL Server resource provider](azure-stack-mysql-resource-provider-deploy.md) and the [App Services resource provider](azure-stack-app-service-overview.md).</span></span>










