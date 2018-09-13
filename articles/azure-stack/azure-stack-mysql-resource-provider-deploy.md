---
title: Use MySQL databases as PaaS on Azure Stack | Microsoft Docs
description: Learn how you can deploy the MySQL Resource Provider and provide MySQL databases as a service on Azure Stack
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
ms.openlocfilehash: 327b78c35f42ec55570b263f1dbbe0dffed4b47a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562799"
---
# <a name="use-mysql-databases-as-paas-on-azure-stack"></a><span data-ttu-id="d4116-103">Use MySQL databases as PaaS on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d4116-103">Use MySQL databases as PaaS on Azure Stack</span></span>

> [!NOTE]
> <span data-ttu-id="d4116-104">The following information only applies to Azure Stack TP3 Refresh deployments.</span><span class="sxs-lookup"><span data-stu-id="d4116-104">The following information only applies to Azure Stack TP3 Refresh deployments.</span></span> <span data-ttu-id="d4116-105">TP3 Refresh now uses the current release of MySQL 5.7.</span><span class="sxs-lookup"><span data-stu-id="d4116-105">TP3 Refresh now uses the current release of MySQL 5.7.</span></span>
>
>

<span data-ttu-id="d4116-106">You can deploy a MySQL resource provider on Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="d4116-106">You can deploy a MySQL resource provider on Azure Stack.</span></span> <span data-ttu-id="d4116-107">After you deploy the resource provider, you can create MySQL servers and databases through Azure Resource Manager deployment templates and provide MySQL databases as a service.</span><span class="sxs-lookup"><span data-stu-id="d4116-107">After you deploy the resource provider, you can create MySQL servers and databases through Azure Resource Manager deployment templates and provide MySQL databases as a service.</span></span> <span data-ttu-id="d4116-108">MySQL databases, which are common on web sites, support many website platforms.</span><span class="sxs-lookup"><span data-stu-id="d4116-108">MySQL databases, which are common on web sites, support many website platforms.</span></span> <span data-ttu-id="d4116-109">As an example, after you deploy the resource provider, you can create WordPress websites from the Azure Web Apps platform as a service (PaaS) add-on for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="d4116-109">As an example, after you deploy the resource provider, you can create WordPress websites from the Azure Web Apps platform as a service (PaaS) add-on for Azure Stack.</span></span>

<span data-ttu-id="d4116-110">To deploy the MySQL provider on a system that does not have internet access, you can copy the files  [mysql-5.7.17-winx64.zip](https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.17-winx64.zip) and [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi) to a local share and provide that share name when prompted (see below).</span><span class="sxs-lookup"><span data-stu-id="d4116-110">To deploy the MySQL provider on a system that does not have internet access, you can copy the files  [mysql-5.7.17-winx64.zip](https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.17-winx64.zip) and [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi) to a local share and provide that share name when prompted (see below).</span></span>

> [!NOTE]
> <span data-ttu-id="d4116-111">The deployment script will perform retries, if necessary, to accommodate less reliable network connections or if an operation exceeds a timeout.</span><span class="sxs-lookup"><span data-stu-id="d4116-111">The deployment script will perform retries, if necessary, to accommodate less reliable network connections or if an operation exceeds a timeout.</span></span>
>
>

## <a name="steps-to-deploy-the-resource-provider"></a><span data-ttu-id="d4116-112">Steps to deploy the resource provider</span><span class="sxs-lookup"><span data-stu-id="d4116-112">Steps to deploy the resource provider</span></span>

1. <span data-ttu-id="d4116-113">If you have not already done so, create a [Windows Server 2016 image with the .NET 3.5 runtime](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image) installed.</span><span class="sxs-lookup"><span data-stu-id="d4116-113">If you have not already done so, create a [Windows Server 2016 image with the .NET 3.5 runtime](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image) installed.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d4116-114">The .NET 3.5 runtime is not required for this RP, but will be used for the SQL Resource Provider, so you can save space by using the same image.</span><span class="sxs-lookup"><span data-stu-id="d4116-114">The .NET 3.5 runtime is not required for this RP, but will be used for the SQL Resource Provider, so you can save space by using the same image.</span></span>
    >
    >

2. <span data-ttu-id="d4116-115">If you have installed any version of the AzureRm PowerShell module other than 1.2.9, you will need to remove it or the install will block.</span><span class="sxs-lookup"><span data-stu-id="d4116-115">If you have installed any version of the AzureRm PowerShell module other than 1.2.9, you will need to remove it or the install will block.</span></span>

3. <span data-ttu-id="d4116-116">[Download the MySQL resource provider binaries file](https://aka.ms/azurestackmysqlrptp3) and extract it on the Console VM in your Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="d4116-116">[Download the MySQL resource provider binaries file](https://aka.ms/azurestackmysqlrptp3) and extract it on the Console VM in your Azure Stack.</span></span>

4. <span data-ttu-id="d4116-117">Open a **new** elevated PowerShell console and change to the directory where you extracted the files.</span><span class="sxs-lookup"><span data-stu-id="d4116-117">Open a **new** elevated PowerShell console and change to the directory where you extracted the files.</span></span> <span data-ttu-id="d4116-118">Use a new window to avoid problems that may arise from incorrect PowerShell modules already loaded on the system.</span><span class="sxs-lookup"><span data-stu-id="d4116-118">Use a new window to avoid problems that may arise from incorrect PowerShell modules already loaded on the system.</span></span>

5. <span data-ttu-id="d4116-119">Run DeployMySqlProvider.ps1.</span><span class="sxs-lookup"><span data-stu-id="d4116-119">Run DeployMySqlProvider.ps1.</span></span>

<span data-ttu-id="d4116-120">This script will do all of the following:</span><span class="sxs-lookup"><span data-stu-id="d4116-120">This script will do all of the following:</span></span>

* <span data-ttu-id="d4116-121">If necessary, download a compatible version of Azure PowerShell (only AzureRm version 1.2.9 is supported).</span><span class="sxs-lookup"><span data-stu-id="d4116-121">If necessary, download a compatible version of Azure PowerShell (only AzureRm version 1.2.9 is supported).</span></span>
* <span data-ttu-id="d4116-122">Create a wildcard certificate to secure communication between the resource provider and Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d4116-122">Create a wildcard certificate to secure communication between the resource provider and Azure Resource Manager.</span></span>
* <span data-ttu-id="d4116-123">Download the MySQL binaries.</span><span class="sxs-lookup"><span data-stu-id="d4116-123">Download the MySQL binaries.</span></span>
* <span data-ttu-id="d4116-124">Upload the certificate and all other artifacts to an Azure Stack storage account.</span><span class="sxs-lookup"><span data-stu-id="d4116-124">Upload the certificate and all other artifacts to an Azure Stack storage account.</span></span>
* <span data-ttu-id="d4116-125">Publish gallery packages so that you can deploy MySQL resources through the gallery.</span><span class="sxs-lookup"><span data-stu-id="d4116-125">Publish gallery packages so that you can deploy MySQL resources through the gallery.</span></span>
* <span data-ttu-id="d4116-126">Deploy a virtual machine (VM) that will host both your resource provider, and a MySQL 5.7 server.</span><span class="sxs-lookup"><span data-stu-id="d4116-126">Deploy a virtual machine (VM) that will host both your resource provider, and a MySQL 5.7 server.</span></span>
* <span data-ttu-id="d4116-127">Register a local DNS record that will map to your resource provider VM.</span><span class="sxs-lookup"><span data-stu-id="d4116-127">Register a local DNS record that will map to your resource provider VM.</span></span>
* <span data-ttu-id="d4116-128">Register your resource provider with the local Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d4116-128">Register your resource provider with the local Azure Resource Manager.</span></span>

<span data-ttu-id="d4116-129">Either specify at least the required parameters on the command line, or, if you run without any parameters, you will be prompted to enter them.</span><span class="sxs-lookup"><span data-stu-id="d4116-129">Either specify at least the required parameters on the command line, or, if you run without any parameters, you will be prompted to enter them.</span></span> 

<span data-ttu-id="d4116-130">Here's an example you can run from the PowerShell prompt (but change the account information and portal endpoints as needed):</span><span class="sxs-lookup"><span data-stu-id="d4116-130">Here's an example you can run from the PowerShell prompt (but change the account information and portal endpoints as needed):</span></span>

```
$vmLocalAdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("mysqlrpadmin", $vmLocalAdminPass)

$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)

.\DeployMySQLProvider.ps1 -DirectoryTenantID "51377b64-4a17-46b1-83ff-902d97c50b22" -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "System.MySql" -VmName "SystemMySqlRP" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external"
 ```

### <a name="parameters"></a><span data-ttu-id="d4116-131">Parameters</span><span class="sxs-lookup"><span data-stu-id="d4116-131">Parameters</span></span>


| <span data-ttu-id="d4116-132">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="d4116-132">Parameter Name</span></span> | <span data-ttu-id="d4116-133">Description</span><span class="sxs-lookup"><span data-stu-id="d4116-133">Description</span></span> | <span data-ttu-id="d4116-134">Comment or Default Value</span><span class="sxs-lookup"><span data-stu-id="d4116-134">Comment or Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d4116-135">**DirectoryTenantID**</span><span class="sxs-lookup"><span data-stu-id="d4116-135">**DirectoryTenantID**</span></span> | <span data-ttu-id="d4116-136">The Azure or ADFS Directory ID (guid)</span><span class="sxs-lookup"><span data-stu-id="d4116-136">The Azure or ADFS Directory ID (guid)</span></span> | <span data-ttu-id="d4116-137">_required_</span><span class="sxs-lookup"><span data-stu-id="d4116-137">_required_</span></span> |
| <span data-ttu-id="d4116-138">**ArmEndpoint**</span><span class="sxs-lookup"><span data-stu-id="d4116-138">**ArmEndpoint**</span></span> | <span data-ttu-id="d4116-139">The Azure Stack Administrative ARM Endpoint</span><span class="sxs-lookup"><span data-stu-id="d4116-139">The Azure Stack Administrative ARM Endpoint</span></span> | <span data-ttu-id="d4116-140">_required_</span><span class="sxs-lookup"><span data-stu-id="d4116-140">_required_</span></span> |
| <span data-ttu-id="d4116-141">**TenantArmEndpoint**</span><span class="sxs-lookup"><span data-stu-id="d4116-141">**TenantArmEndpoint**</span></span> | <span data-ttu-id="d4116-142">The Azure Stack Tenant ARM Endpoint</span><span class="sxs-lookup"><span data-stu-id="d4116-142">The Azure Stack Tenant ARM Endpoint</span></span> | <span data-ttu-id="d4116-143">_required_</span><span class="sxs-lookup"><span data-stu-id="d4116-143">_required_</span></span> |
| <span data-ttu-id="d4116-144">**AzCredential**</span><span class="sxs-lookup"><span data-stu-id="d4116-144">**AzCredential**</span></span> | <span data-ttu-id="d4116-145">Azure Stack Service Admin account credential (use the same account as you used for deploying Azure Stack)</span><span class="sxs-lookup"><span data-stu-id="d4116-145">Azure Stack Service Admin account credential (use the same account as you used for deploying Azure Stack)</span></span> | <span data-ttu-id="d4116-146">_required_</span><span class="sxs-lookup"><span data-stu-id="d4116-146">_required_</span></span> |
| <span data-ttu-id="d4116-147">**VMLocalCredential**</span><span class="sxs-lookup"><span data-stu-id="d4116-147">**VMLocalCredential**</span></span> | <span data-ttu-id="d4116-148">The local administrator account of the MySQL resource provider VM</span><span class="sxs-lookup"><span data-stu-id="d4116-148">The local administrator account of the MySQL resource provider VM</span></span> | <span data-ttu-id="d4116-149">_required_</span><span class="sxs-lookup"><span data-stu-id="d4116-149">_required_</span></span> |
| <span data-ttu-id="d4116-150">**ResourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="d4116-150">**ResourceGroupName**</span></span> | <span data-ttu-id="d4116-151">Resource Group for the items created by this script</span><span class="sxs-lookup"><span data-stu-id="d4116-151">Resource Group for the items created by this script</span></span> | <span data-ttu-id="d4116-152">Default: Microsoft-MySQL-RP1</span><span class="sxs-lookup"><span data-stu-id="d4116-152">Default: Microsoft-MySQL-RP1</span></span> |
| <span data-ttu-id="d4116-153">**VmName**</span><span class="sxs-lookup"><span data-stu-id="d4116-153">**VmName**</span></span> | <span data-ttu-id="d4116-154">Name of the VM holding the resource provider</span><span class="sxs-lookup"><span data-stu-id="d4116-154">Name of the VM holding the resource provider</span></span> | <span data-ttu-id="d4116-155">mysqlvm</span><span class="sxs-lookup"><span data-stu-id="d4116-155">mysqlvm</span></span> |
| <span data-ttu-id="d4116-156">**AcceptLicense**</span><span class="sxs-lookup"><span data-stu-id="d4116-156">**AcceptLicense**</span></span> | <span data-ttu-id="d4116-157">Prompts to accept the GPL License Accept the terms of the GPL License (http://www.gnu.org/licenses/old-licenses/gpl-2.0.html)</span><span class="sxs-lookup"><span data-stu-id="d4116-157">Prompts to accept the GPL License Accept the terms of the GPL License (http://www.gnu.org/licenses/old-licenses/gpl-2.0.html)</span></span> | <span data-ttu-id="d4116-158">Yes</span><span class="sxs-lookup"><span data-stu-id="d4116-158">Yes</span></span> |
| <span data-ttu-id="d4116-159">**DependencyFilesLocalPath**</span><span class="sxs-lookup"><span data-stu-id="d4116-159">**DependencyFilesLocalPath**</span></span> | <span data-ttu-id="d4116-160">Path to a local share containing the MySQL files [mysql-5.7.17-winx64.zip](https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.17-winx64.zip) and [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi)</span><span class="sxs-lookup"><span data-stu-id="d4116-160">Path to a local share containing the MySQL files [mysql-5.7.17-winx64.zip](https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.17-winx64.zip) and [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi)</span></span> | <span data-ttu-id="d4116-161">_leave blank to download from the internet_</span><span class="sxs-lookup"><span data-stu-id="d4116-161">_leave blank to download from the internet_</span></span> |
| <span data-ttu-id="d4116-162">**MaxRetryCount**</span><span class="sxs-lookup"><span data-stu-id="d4116-162">**MaxRetryCount**</span></span> | <span data-ttu-id="d4116-163">Each operation will be retried if there is a failure</span><span class="sxs-lookup"><span data-stu-id="d4116-163">Each operation will be retried if there is a failure</span></span> | <span data-ttu-id="d4116-164">2</span><span class="sxs-lookup"><span data-stu-id="d4116-164">2</span></span> |
| <span data-ttu-id="d4116-165">**RetryDuration**</span><span class="sxs-lookup"><span data-stu-id="d4116-165">**RetryDuration**</span></span> | <span data-ttu-id="d4116-166">Timeout between retries, in seconds</span><span class="sxs-lookup"><span data-stu-id="d4116-166">Timeout between retries, in seconds</span></span> | <span data-ttu-id="d4116-167">120</span><span class="sxs-lookup"><span data-stu-id="d4116-167">120</span></span> |
| <span data-ttu-id="d4116-168">**Uninstall**</span><span class="sxs-lookup"><span data-stu-id="d4116-168">**Uninstall**</span></span> | <span data-ttu-id="d4116-169">Clean up the resource provider</span><span class="sxs-lookup"><span data-stu-id="d4116-169">Clean up the resource provider</span></span> | <span data-ttu-id="d4116-170">No</span><span class="sxs-lookup"><span data-stu-id="d4116-170">No</span></span> |
| <span data-ttu-id="d4116-171">**DebugMode**</span><span class="sxs-lookup"><span data-stu-id="d4116-171">**DebugMode**</span></span> | <span data-ttu-id="d4116-172">Prevents automatic clean up on failure</span><span class="sxs-lookup"><span data-stu-id="d4116-172">Prevents automatic clean up on failure</span></span> | <span data-ttu-id="d4116-173">No</span><span class="sxs-lookup"><span data-stu-id="d4116-173">No</span></span> |


<span data-ttu-id="d4116-174">Depending on the system performance and download speeds, installation may take as little as 20 minutes or as long as several hours.</span><span class="sxs-lookup"><span data-stu-id="d4116-174">Depending on the system performance and download speeds, installation may take as little as 20 minutes or as long as several hours.</span></span> <span data-ttu-id="d4116-175">You may need to refresh the admin portal if the MySQLAdapter blade is not available.</span><span class="sxs-lookup"><span data-stu-id="d4116-175">You may need to refresh the admin portal if the MySQLAdapter blade is not available.</span></span>

> [!NOTE]
> <span data-ttu-id="d4116-176">If the installation takes more than 90 minutes, it may fail and you will see a failure message on the screen and in the log file, but the deployment will be retried from the failing step.</span><span class="sxs-lookup"><span data-stu-id="d4116-176">If the installation takes more than 90 minutes, it may fail and you will see a failure message on the screen and in the log file, but the deployment will be retried from the failing step.</span></span> <span data-ttu-id="d4116-177">Systems that do not meet the minimum required memory and core specifications may not be able to deploy the MySQL RP.</span><span class="sxs-lookup"><span data-stu-id="d4116-177">Systems that do not meet the minimum required memory and core specifications may not be able to deploy the MySQL RP.</span></span>
>
>

## <a name="provide-capacity-by-connecting-it-to-a-mysql-hosting-server"></a><span data-ttu-id="d4116-178">Provide capacity by connecting it to a MySQL hosting server</span><span class="sxs-lookup"><span data-stu-id="d4116-178">Provide capacity by connecting it to a MySQL hosting server</span></span>

1. <span data-ttu-id="d4116-179">Sign in to the Azure Stack POC portal as a service admin</span><span class="sxs-lookup"><span data-stu-id="d4116-179">Sign in to the Azure Stack POC portal as a service admin</span></span>

2. <span data-ttu-id="d4116-180">Click **Resource Providers** &gt; **MySQLAdapter** &gt; **Hosting Servers** &gt; **+Add**.</span><span class="sxs-lookup"><span data-stu-id="d4116-180">Click **Resource Providers** &gt; **MySQLAdapter** &gt; **Hosting Servers** &gt; **+Add**.</span></span>

    <span data-ttu-id="d4116-181">The **MySQL Hosting Servers** blade is where you can connect the MySQL Server Resource Provider to actual instances of MySQL Server that serve as the resource provider’s backend.</span><span class="sxs-lookup"><span data-stu-id="d4116-181">The **MySQL Hosting Servers** blade is where you can connect the MySQL Server Resource Provider to actual instances of MySQL Server that serve as the resource provider’s backend.</span></span>

    ![Hosting Servers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-mysql-rp-deploy/mysql-add-hosting-server-2.PNG)

3. <span data-ttu-id="d4116-183">Fill the form with the connection details of your MySQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="d4116-183">Fill the form with the connection details of your MySQL Server instance.</span></span> <span data-ttu-id="d4116-184">You must provide the fully-qualified domain name (FQDN) or a valid IPv4 address, and not the short VM name.</span><span class="sxs-lookup"><span data-stu-id="d4116-184">You must provide the fully-qualified domain name (FQDN) or a valid IPv4 address, and not the short VM name.</span></span> <span data-ttu-id="d4116-185">By default, a preconfigured MySQL 5.7 Server called “mysqlvm.local.cloudapp.azurestack.external” with the administrator user name and the password you provided in the "LocalCredential" parameter is running on the VM.</span><span class="sxs-lookup"><span data-stu-id="d4116-185">By default, a preconfigured MySQL 5.7 Server called “mysqlvm.local.cloudapp.azurestack.external” with the administrator user name and the password you provided in the "LocalCredential" parameter is running on the VM.</span></span>


<span data-ttu-id="d4116-186">The size provided helps the resource provider manage the database capacity.</span><span class="sxs-lookup"><span data-stu-id="d4116-186">The size provided helps the resource provider manage the database capacity.</span></span> <span data-ttu-id="d4116-187">It should be close to the physical capacity of the database server.</span><span class="sxs-lookup"><span data-stu-id="d4116-187">It should be close to the physical capacity of the database server.</span></span>


## <a name="create-your-first-mysql-database-to-test-your-deployment"></a><span data-ttu-id="d4116-188">Create your first MySQL database to test your deployment</span><span class="sxs-lookup"><span data-stu-id="d4116-188">Create your first MySQL database to test your deployment</span></span>

> [!NOTE]
> <span data-ttu-id="d4116-189">After the installation script completes, it can take up to 60 minutes for all of the virtual machines to finish configuration.</span><span class="sxs-lookup"><span data-stu-id="d4116-189">After the installation script completes, it can take up to 60 minutes for all of the virtual machines to finish configuration.</span></span> <span data-ttu-id="d4116-190">If you attempt the next steps before this completes, you will see failures.</span><span class="sxs-lookup"><span data-stu-id="d4116-190">If you attempt the next steps before this completes, you will see failures.</span></span>
>
>

1. <span data-ttu-id="d4116-191">Sign in to the Azure Stack POC portal as service admin.</span><span class="sxs-lookup"><span data-stu-id="d4116-191">Sign in to the Azure Stack POC portal as service admin.</span></span>

2. <span data-ttu-id="d4116-192">Click the **+ New** button &gt; **Data + Storage** &gt; **MySQL Database (preview)**.</span><span class="sxs-lookup"><span data-stu-id="d4116-192">Click the **+ New** button &gt; **Data + Storage** &gt; **MySQL Database (preview)**.</span></span>

3. <span data-ttu-id="d4116-193">Fill in the form with the database details.</span><span class="sxs-lookup"><span data-stu-id="d4116-193">Fill in the form with the database details.</span></span>

![Create a test MySQL database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-mysql-rp-deploy/mysql-create-db.PNG)


<span data-ttu-id="d4116-195">**New.**</span><span class="sxs-lookup"><span data-stu-id="d4116-195">**New.**</span></span> <span data-ttu-id="d4116-196">The connections string will include the real database server name.</span><span class="sxs-lookup"><span data-stu-id="d4116-196">The connections string will include the real database server name.</span></span> <span data-ttu-id="d4116-197">Copy it from the portal.</span><span class="sxs-lookup"><span data-stu-id="d4116-197">Copy it from the portal.</span></span>

![Get the connection string for the MySQL database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-mysql-rp-deploy/mysql-db-created.PNG)

> <span data-ttu-id="d4116-199">The combined length of the user and server names cannot exceed 31 characters with MySQL 5.7 or 15 characters in earlier editions, in addition to the '@' sign.</span><span class="sxs-lookup"><span data-stu-id="d4116-199">The combined length of the user and server names cannot exceed 31 characters with MySQL 5.7 or 15 characters in earlier editions, in addition to the '@' sign.</span></span> <span data-ttu-id="d4116-200">This is a limitation of the MySQL implementations.</span><span class="sxs-lookup"><span data-stu-id="d4116-200">This is a limitation of the MySQL implementations.</span></span>
>

## <a name="add-capacity"></a><span data-ttu-id="d4116-201">Add Capacity</span><span class="sxs-lookup"><span data-stu-id="d4116-201">Add Capacity</span></span>

<span data-ttu-id="d4116-202">Add Capacity by adding additional MySQL servers in the Azure Stack portal.</span><span class="sxs-lookup"><span data-stu-id="d4116-202">Add Capacity by adding additional MySQL servers in the Azure Stack portal.</span></span> <span data-ttu-id="d4116-203">If you wish to use another instance of MySQL, click **Resource Providers** &gt; **MySQLAdapter** &gt; **MySQL Hosting Servers** &gt; **+Add**.</span><span class="sxs-lookup"><span data-stu-id="d4116-203">If you wish to use another instance of MySQL, click **Resource Providers** &gt; **MySQLAdapter** &gt; **MySQL Hosting Servers** &gt; **+Add**.</span></span>


## <a name="making-sql-databases-available-to-tenants"></a><span data-ttu-id="d4116-204">Making SQL databases available to tenants</span><span class="sxs-lookup"><span data-stu-id="d4116-204">Making SQL databases available to tenants</span></span> ##
<span data-ttu-id="d4116-205">Create plans and offers to make MySQL databases available for tenants.</span><span class="sxs-lookup"><span data-stu-id="d4116-205">Create plans and offers to make MySQL databases available for tenants.</span></span> <span data-ttu-id="d4116-206">You will need to add the Microsoft.MySqlAdapter service, add a new quota, and accept the default values.</span><span class="sxs-lookup"><span data-stu-id="d4116-206">You will need to add the Microsoft.MySqlAdapter service, add a new quota, and accept the default values.</span></span>

![Create plans and offers to include databases](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-mysql-rp-deploy/mysql-new-plan.PNG)


## <a name="next-steps"></a><span data-ttu-id="d4116-208">Next steps</span><span class="sxs-lookup"><span data-stu-id="d4116-208">Next steps</span></span>


<span data-ttu-id="d4116-209">Try other [PaaS services](azure-stack-tools-paas-services.md) like the [SQL Server resource provider](azure-stack-sql-resource-provider-deploy.md) and the [App Services resource provider](azure-stack-app-service-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d4116-209">Try other [PaaS services](azure-stack-tools-paas-services.md) like the [SQL Server resource provider](azure-stack-sql-resource-provider-deploy.md) and the [App Services resource provider](azure-stack-app-service-overview.md).</span></span>




