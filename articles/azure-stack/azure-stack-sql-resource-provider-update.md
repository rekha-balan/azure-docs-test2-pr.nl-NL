---
title: Updating the Azure Stack SQL resource provider | Microsoft Docs
description: Learn how you can update the Azure Stack SQL resource provider.
services: azure-stack
documentationCenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/04/2018
ms.author: jeffgilb
ms.reviewer: jeffgo
ms.openlocfilehash: 3517114d5bc267aa32cea49161d0d34156a2ed1e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969379"
---
# <a name="update-the-sql-resource-provider"></a><span data-ttu-id="87bf1-103">Update the SQL resource provider</span><span class="sxs-lookup"><span data-stu-id="87bf1-103">Update the SQL resource provider</span></span>

<span data-ttu-id="87bf1-104">*Applies to: Azure Stack integrated systems.*</span><span class="sxs-lookup"><span data-stu-id="87bf1-104">*Applies to: Azure Stack integrated systems.*</span></span>

<span data-ttu-id="87bf1-105">A new SQL resource provider might be released when Azure Stack is updated to a new build.</span><span class="sxs-lookup"><span data-stu-id="87bf1-105">A new SQL resource provider might be released when Azure Stack is updated to a new build.</span></span> <span data-ttu-id="87bf1-106">Although the existing adapter continues to work, we recommend updating to the latest build as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="87bf1-106">Although the existing adapter continues to work, we recommend updating to the latest build as soon as possible.</span></span>

>[!IMPORTANT]
><span data-ttu-id="87bf1-107">You must install updates in the order they're released.</span><span class="sxs-lookup"><span data-stu-id="87bf1-107">You must install updates in the order they're released.</span></span> <span data-ttu-id="87bf1-108">You can't skip versions.</span><span class="sxs-lookup"><span data-stu-id="87bf1-108">You can't skip versions.</span></span> <span data-ttu-id="87bf1-109">Refer to the versions list in [Deploy the resource provider prerequisites](.\azure-stack-sql-resource-provider-deploy.md#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="87bf1-109">Refer to the versions list in [Deploy the resource provider prerequisites](.\azure-stack-sql-resource-provider-deploy.md#prerequisites).</span></span>

## <a name="overview"></a><span data-ttu-id="87bf1-110">Overview</span><span class="sxs-lookup"><span data-stu-id="87bf1-110">Overview</span></span>

<span data-ttu-id="87bf1-111">To update the resource provider, use the *UpdateSQLProvider.ps1* script.</span><span class="sxs-lookup"><span data-stu-id="87bf1-111">To update the resource provider, use the *UpdateSQLProvider.ps1* script.</span></span> <span data-ttu-id="87bf1-112">This script is included with the download of the new SQL resource provider.</span><span class="sxs-lookup"><span data-stu-id="87bf1-112">This script is included with the download of the new SQL resource provider.</span></span> <span data-ttu-id="87bf1-113">The update process is similar to the process used to [Deploy the resource provider](.\azure-stack-sql-resource-provider-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="87bf1-113">The update process is similar to the process used to [Deploy the resource provider](.\azure-stack-sql-resource-provider-deploy.md).</span></span> <span data-ttu-id="87bf1-114">The update script uses the same arguments as the DeploySqlProvider.ps1 script, and you'll need to provide certificate information.</span><span class="sxs-lookup"><span data-stu-id="87bf1-114">The update script uses the same arguments as the DeploySqlProvider.ps1 script, and you'll need to provide certificate information.</span></span>

### <a name="update-script-processes"></a><span data-ttu-id="87bf1-115">Update script processes</span><span class="sxs-lookup"><span data-stu-id="87bf1-115">Update script processes</span></span>

<span data-ttu-id="87bf1-116">The *UpdateSQLProvider.ps1* script creates a new virtual machine (VM) with the latest resource provider code.</span><span class="sxs-lookup"><span data-stu-id="87bf1-116">The *UpdateSQLProvider.ps1* script creates a new virtual machine (VM) with the latest resource provider code.</span></span>

>[!NOTE]
><span data-ttu-id="87bf1-117">We recommend that you download the latest Windows Server 2016 Core image from Marketplace Management.</span><span class="sxs-lookup"><span data-stu-id="87bf1-117">We recommend that you download the latest Windows Server 2016 Core image from Marketplace Management.</span></span> <span data-ttu-id="87bf1-118">If you need to install an update, you can place a **single** MSU package in the local dependency path.</span><span class="sxs-lookup"><span data-stu-id="87bf1-118">If you need to install an update, you can place a **single** MSU package in the local dependency path.</span></span> <span data-ttu-id="87bf1-119">The script will fail if there's more than one MSU file in this location.</span><span class="sxs-lookup"><span data-stu-id="87bf1-119">The script will fail if there's more than one MSU file in this location.</span></span>

<span data-ttu-id="87bf1-120">After the *UpdateSQLProvider.ps1* script creates a new VM, the script migrates the following settings from the old provider VM:</span><span class="sxs-lookup"><span data-stu-id="87bf1-120">After the *UpdateSQLProvider.ps1* script creates a new VM, the script migrates the following settings from the old provider VM:</span></span>

* <span data-ttu-id="87bf1-121">database information</span><span class="sxs-lookup"><span data-stu-id="87bf1-121">database information</span></span>
* <span data-ttu-id="87bf1-122">hosting server information</span><span class="sxs-lookup"><span data-stu-id="87bf1-122">hosting server information</span></span>
* <span data-ttu-id="87bf1-123">required DNS record</span><span class="sxs-lookup"><span data-stu-id="87bf1-123">required DNS record</span></span>

### <a name="update-script-powershell-example"></a><span data-ttu-id="87bf1-124">Update script PowerShell example</span><span class="sxs-lookup"><span data-stu-id="87bf1-124">Update script PowerShell example</span></span>

<a name="you-can-edit-and-run-the-following-script-from-an-elevated-powershell-ise"></a><span data-ttu-id="87bf1-125">You can edit and run the following script from an elevated PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="87bf1-125">You can edit and run the following script from an elevated PowerShell ISE.</span></span> 
-  
- <span data-ttu-id="87bf1-126">Remember to change the account information and passwords as needed for your environment.</span><span class="sxs-lookup"><span data-stu-id="87bf1-126">Remember to change the account information and passwords as needed for your environment.</span></span>

> [!NOTE]
> <span data-ttu-id="87bf1-127">This update process only applies to Azure Stack integrated systems.</span><span class="sxs-lookup"><span data-stu-id="87bf1-127">This update process only applies to Azure Stack integrated systems.</span></span>

```powershell
# Install the AzureRM.Bootstrapper module and set the profile.
Install-Module -Name AzureRm.BootStrapper -Force
Use-AzureRmProfile -Profile 2017-03-09-profile

# Use the NetBIOS name for the Azure Stack domain. On the Azure Stack SDK, the default is AzureStack but this might have been changed at installation.
$domain = "AzureStack"

# For integrated systems, use the IP address of one of the ERCS virtual machines.
$privilegedEndpoint = "AzS-ERCS01"

# Point to the directory where the resource provider installation files were extracted.
$tempDir = 'C:\TEMP\SQLRP'

# The service administrator account (this can be Azure AD or AD FS).
$serviceAdmin = "admin@mydomain.onmicrosoft.com"
$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ($serviceAdmin, $AdminPass)

# Set the credentials for the new resource provider VM.
$vmLocalAdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("sqlrpadmin", $vmLocalAdminPass)

# Add the cloudadmin credential required for privileged endpoint access.
$CloudAdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$CloudAdminCreds = New-Object System.Management.Automation.PSCredential ("$domain\cloudadmin", $CloudAdminPass)

# Change the following as appropriate.
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force

# Change directory to the folder where you extracted the installation files.
# Then adjust the endpoints.
. $tempDir\UpdateSQLProvider.ps1 -AzCredential $AdminCreds `
  -VMLocalCredential $vmLocalAdminCreds `
  -CloudAdminCredential $cloudAdminCreds `
  -PrivilegedEndpoint $privilegedEndpoint `
  -DefaultSSLCertificatePassword $PfxPass `
  -DependencyFilesLocalPath $tempDir\cert `

 ```

## <a name="updatesqlproviderps1-parameters"></a><span data-ttu-id="87bf1-128">UpdateSQLProvider.ps1 parameters</span><span class="sxs-lookup"><span data-stu-id="87bf1-128">UpdateSQLProvider.ps1 parameters</span></span>

<span data-ttu-id="87bf1-129">You can specify the following parameters from the command line when you run the script.</span><span class="sxs-lookup"><span data-stu-id="87bf1-129">You can specify the following parameters from the command line when you run the script.</span></span> <span data-ttu-id="87bf1-130">If you don't, or if any parameter validation fails, you're prompted to provide the required parameters.</span><span class="sxs-lookup"><span data-stu-id="87bf1-130">If you don't, or if any parameter validation fails, you're prompted to provide the required parameters.</span></span>

| <span data-ttu-id="87bf1-131">Parameter name</span><span class="sxs-lookup"><span data-stu-id="87bf1-131">Parameter name</span></span> | <span data-ttu-id="87bf1-132">Description</span><span class="sxs-lookup"><span data-stu-id="87bf1-132">Description</span></span> | <span data-ttu-id="87bf1-133">Comment or default value</span><span class="sxs-lookup"><span data-stu-id="87bf1-133">Comment or default value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="87bf1-134">**CloudAdminCredential**</span><span class="sxs-lookup"><span data-stu-id="87bf1-134">**CloudAdminCredential**</span></span> | <span data-ttu-id="87bf1-135">The credential for the cloud administrator, necessary for accessing the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="87bf1-135">The credential for the cloud administrator, necessary for accessing the privileged endpoint.</span></span> | <span data-ttu-id="87bf1-136">_Required_</span><span class="sxs-lookup"><span data-stu-id="87bf1-136">_Required_</span></span> |
| <span data-ttu-id="87bf1-137">**AzCredential**</span><span class="sxs-lookup"><span data-stu-id="87bf1-137">**AzCredential**</span></span> | <span data-ttu-id="87bf1-138">The credentials for the Azure Stack service administrator account.</span><span class="sxs-lookup"><span data-stu-id="87bf1-138">The credentials for the Azure Stack service administrator account.</span></span> <span data-ttu-id="87bf1-139">Use the same credentials that you used for deploying Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="87bf1-139">Use the same credentials that you used for deploying Azure Stack.</span></span> | <span data-ttu-id="87bf1-140">_Required_</span><span class="sxs-lookup"><span data-stu-id="87bf1-140">_Required_</span></span> |
| <span data-ttu-id="87bf1-141">**VMLocalCredential**</span><span class="sxs-lookup"><span data-stu-id="87bf1-141">**VMLocalCredential**</span></span> | <span data-ttu-id="87bf1-142">The credentials for the local administrator account of the SQL resource provider VM.</span><span class="sxs-lookup"><span data-stu-id="87bf1-142">The credentials for the local administrator account of the SQL resource provider VM.</span></span> | <span data-ttu-id="87bf1-143">_Required_</span><span class="sxs-lookup"><span data-stu-id="87bf1-143">_Required_</span></span> |
| <span data-ttu-id="87bf1-144">**PrivilegedEndpoint**</span><span class="sxs-lookup"><span data-stu-id="87bf1-144">**PrivilegedEndpoint**</span></span> | <span data-ttu-id="87bf1-145">The IP address or DNS name of the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="87bf1-145">The IP address or DNS name of the privileged endpoint.</span></span> |  <span data-ttu-id="87bf1-146">_Required_</span><span class="sxs-lookup"><span data-stu-id="87bf1-146">_Required_</span></span> |
| <span data-ttu-id="87bf1-147">**AzureEnvironment**</span><span class="sxs-lookup"><span data-stu-id="87bf1-147">**AzureEnvironment**</span></span> | <span data-ttu-id="87bf1-148">The azure environment of the service admin account which you used for deploying Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="87bf1-148">The azure environment of the service admin account which you used for deploying Azure Stack.</span></span> <span data-ttu-id="87bf1-149">Required only if it’s NOT ADFS.</span><span class="sxs-lookup"><span data-stu-id="87bf1-149">Required only if it’s NOT ADFS.</span></span> <span data-ttu-id="87bf1-150">Supported environment names are **AzureCloud**, **AzureUSGovernment**, or if using a China Azure Active Directory, **AzureChinaCloud**.</span><span class="sxs-lookup"><span data-stu-id="87bf1-150">Supported environment names are **AzureCloud**, **AzureUSGovernment**, or if using a China Azure Active Directory, **AzureChinaCloud**.</span></span> | <span data-ttu-id="87bf1-151">AzureCloud</span><span class="sxs-lookup"><span data-stu-id="87bf1-151">AzureCloud</span></span> |
| <span data-ttu-id="87bf1-152">**DependencyFilesLocalPath**</span><span class="sxs-lookup"><span data-stu-id="87bf1-152">**DependencyFilesLocalPath**</span></span> | <span data-ttu-id="87bf1-153">You must also put your certificate .pfx file in this directory.</span><span class="sxs-lookup"><span data-stu-id="87bf1-153">You must also put your certificate .pfx file in this directory.</span></span> | <span data-ttu-id="87bf1-154">_Optional for single node, but mandatory for multi-node_</span><span class="sxs-lookup"><span data-stu-id="87bf1-154">_Optional for single node, but mandatory for multi-node_</span></span> |
| <span data-ttu-id="87bf1-155">**DefaultSSLCertificatePassword**</span><span class="sxs-lookup"><span data-stu-id="87bf1-155">**DefaultSSLCertificatePassword**</span></span> | <span data-ttu-id="87bf1-156">The password for the .pfx certificate.</span><span class="sxs-lookup"><span data-stu-id="87bf1-156">The password for the .pfx certificate.</span></span> | <span data-ttu-id="87bf1-157">_Required_</span><span class="sxs-lookup"><span data-stu-id="87bf1-157">_Required_</span></span> |
| <span data-ttu-id="87bf1-158">**MaxRetryCount**</span><span class="sxs-lookup"><span data-stu-id="87bf1-158">**MaxRetryCount**</span></span> | <span data-ttu-id="87bf1-159">The number of times you want to retry each operation if there's a failure.</span><span class="sxs-lookup"><span data-stu-id="87bf1-159">The number of times you want to retry each operation if there's a failure.</span></span>| <span data-ttu-id="87bf1-160">2</span><span class="sxs-lookup"><span data-stu-id="87bf1-160">2</span></span> |
| <span data-ttu-id="87bf1-161">**RetryDuration**</span><span class="sxs-lookup"><span data-stu-id="87bf1-161">**RetryDuration**</span></span> |<span data-ttu-id="87bf1-162">The timeout interval between retries, in seconds.</span><span class="sxs-lookup"><span data-stu-id="87bf1-162">The timeout interval between retries, in seconds.</span></span> | <span data-ttu-id="87bf1-163">120</span><span class="sxs-lookup"><span data-stu-id="87bf1-163">120</span></span> |
| <span data-ttu-id="87bf1-164">**Uninstall**</span><span class="sxs-lookup"><span data-stu-id="87bf1-164">**Uninstall**</span></span> | <span data-ttu-id="87bf1-165">Removes the resource provider and all associated resources.</span><span class="sxs-lookup"><span data-stu-id="87bf1-165">Removes the resource provider and all associated resources.</span></span> | <span data-ttu-id="87bf1-166">No</span><span class="sxs-lookup"><span data-stu-id="87bf1-166">No</span></span> |
| <span data-ttu-id="87bf1-167">**DebugMode**</span><span class="sxs-lookup"><span data-stu-id="87bf1-167">**DebugMode**</span></span> | <span data-ttu-id="87bf1-168">Prevents automatic cleanup on failure.</span><span class="sxs-lookup"><span data-stu-id="87bf1-168">Prevents automatic cleanup on failure.</span></span> | <span data-ttu-id="87bf1-169">No</span><span class="sxs-lookup"><span data-stu-id="87bf1-169">No</span></span> |

## <a name="next-steps"></a><span data-ttu-id="87bf1-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="87bf1-170">Next steps</span></span>

[<span data-ttu-id="87bf1-171">Maintain the SQL resource provider</span><span class="sxs-lookup"><span data-stu-id="87bf1-171">Maintain the SQL resource provider</span></span>](azure-stack-sql-resource-provider-maintain.md)
