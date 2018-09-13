---
title: Updating the Azure Stack MySQL resource provider | Microsoft Docs
description: Learn how you can update the Azure Stack MySQL resource provider.
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
ms.openlocfilehash: 056906e1bcaea3a442616a933886aac6b317b595
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871481"
---
# <a name="update-the-mysql-resource-provider"></a><span data-ttu-id="dbb4b-103">Update the MySQL resource provider</span><span class="sxs-lookup"><span data-stu-id="dbb4b-103">Update the MySQL resource provider</span></span> 

<span data-ttu-id="dbb4b-104">*Applies to: Azure Stack integrated systems.*</span><span class="sxs-lookup"><span data-stu-id="dbb4b-104">*Applies to: Azure Stack integrated systems.*</span></span>

<span data-ttu-id="dbb4b-105">A new SQL resource provider adapter might be released when Azure Stack builds are updated.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-105">A new SQL resource provider adapter might be released when Azure Stack builds are updated.</span></span> <span data-ttu-id="dbb4b-106">While the existing adapter continues to work, we recommend updating to the latest build as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-106">While the existing adapter continues to work, we recommend updating to the latest build as soon as possible.</span></span> 

>[!IMPORTANT]
><span data-ttu-id="dbb4b-107">You must install updates in the order they're released.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-107">You must install updates in the order they're released.</span></span> <span data-ttu-id="dbb4b-108">You can't skip versions.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-108">You can't skip versions.</span></span> <span data-ttu-id="dbb4b-109">Refer to the versions list in [Deploy the resource provider prerequisites](.\azure-stack-mysql-resource-provider-deploy.md#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="dbb4b-109">Refer to the versions list in [Deploy the resource provider prerequisites](.\azure-stack-mysql-resource-provider-deploy.md#prerequisites).</span></span>

## <a name="update-the-mysql-resource-provider-adapter-integrated-systems-only"></a><span data-ttu-id="dbb4b-110">Update the MySQL resource provider adapter (integrated systems only)</span><span class="sxs-lookup"><span data-stu-id="dbb4b-110">Update the MySQL resource provider adapter (integrated systems only)</span></span>

<span data-ttu-id="dbb4b-111">A new SQL resource provider adapter might be released when Azure Stack builds are updated.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-111">A new SQL resource provider adapter might be released when Azure Stack builds are updated.</span></span> <span data-ttu-id="dbb4b-112">While the existing adapter continues to work, we recommend updating to the latest build as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-112">While the existing adapter continues to work, we recommend updating to the latest build as soon as possible.</span></span>  
 
<span data-ttu-id="dbb4b-113">To update of the resource provider you use the **UpdateMySQLProvider.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-113">To update of the resource provider you use the **UpdateMySQLProvider.ps1** script.</span></span> <span data-ttu-id="dbb4b-114">The process is similar to the process used to install a resource provider, as described in the [Deploy the resource provider](#deploy-the-resource-provider) section of this article.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-114">The process is similar to the process used to install a resource provider, as described in the [Deploy the resource provider](#deploy-the-resource-provider) section of this article.</span></span> <span data-ttu-id="dbb4b-115">The script is included with the download of the resource provider.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-115">The script is included with the download of the resource provider.</span></span> 

<span data-ttu-id="dbb4b-116">The **UpdateMySQLProvider.ps1** script creates a new VM with the latest resource provider code and migrates the settings from the old VM to the new VM.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-116">The **UpdateMySQLProvider.ps1** script creates a new VM with the latest resource provider code and migrates the settings from the old VM to the new VM.</span></span> <span data-ttu-id="dbb4b-117">The settings that migrate include database and hosting server information, and the necessary DNS record.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-117">The settings that migrate include database and hosting server information, and the necessary DNS record.</span></span> 

>[!NOTE]
><span data-ttu-id="dbb4b-118">We recommend that you download the latest Windows Server 2016 Core image from Marketplace Management.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-118">We recommend that you download the latest Windows Server 2016 Core image from Marketplace Management.</span></span> <span data-ttu-id="dbb4b-119">If you need to install an update, you can place a **single** MSU package in the local dependency path.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-119">If you need to install an update, you can place a **single** MSU package in the local dependency path.</span></span> <span data-ttu-id="dbb4b-120">The script will fail if there's more than one MSU file in this location.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-120">The script will fail if there's more than one MSU file in this location.</span></span>

>[!NOTE]  
> 

<span data-ttu-id="dbb4b-121">The script requires use of the same arguments that are described for the DeployMySqlProvider.ps1 script.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-121">The script requires use of the same arguments that are described for the DeployMySqlProvider.ps1 script.</span></span> <span data-ttu-id="dbb4b-122">Provide the certificate here as well.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-122">Provide the certificate here as well.</span></span>  

<span data-ttu-id="dbb4b-123">Following is an example of the *UpdateMySQLProvider.ps1* script that you can run from the PowerShell prompt.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-123">Following is an example of the *UpdateMySQLProvider.ps1* script that you can run from the PowerShell prompt.</span></span> <span data-ttu-id="dbb4b-124">Be sure to change the account information and passwords as needed:</span><span class="sxs-lookup"><span data-stu-id="dbb4b-124">Be sure to change the account information and passwords as needed:</span></span>  

> [!NOTE] 
> <span data-ttu-id="dbb4b-125">The update process only applies to integrated systems.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-125">The update process only applies to integrated systems.</span></span> 

```powershell 
# Install the AzureRM.Bootstrapper module and set the profile. 
Install-Module -Name AzureRm.BootStrapper -Force 
Use-AzureRmProfile -Profile 2017-03-09-profile 

# Use the NetBIOS name for the Azure Stack domain. On the Azure Stack SDK, the default is AzureStack but could have been changed at install time. 
$domain = "AzureStack" 

# For integrated systems, use the IP address of one of the ERCS virtual machines 
$privilegedEndpoint = "AzS-ERCS01" 

# Point to the directory where the resource provider installation files were extracted. 
$tempDir = 'C:\TEMP\MYSQLRP' 

# The service admin account (can be Azure Active Directory or Active Directory Federation Services). 
$serviceAdmin = "admin@mydomain.onmicrosoft.com" 
$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force 
$AdminCreds = New-Object System.Management.Automation.PSCredential ($serviceAdmin, $AdminPass) 
 
# Set credentials for the new resource provider VM. 
$vmLocalAdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force 
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("sqlrpadmin", $vmLocalAdminPass) 
 
# And the cloudadmin credential required for privileged endpoint access. 
$CloudAdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force 
$CloudAdminCreds = New-Object System.Management.Automation.PSCredential ("$domain\cloudadmin", $CloudAdminPass) 

# Change the following as appropriate. 
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force 
 
# Change directory to the folder where you extracted the installation files. 
# Then adjust the endpoints. 
$tempDir\UpdateMySQLProvider.ps1 -AzCredential $AdminCreds ` 
-VMLocalCredential $vmLocalAdminCreds ` 
-CloudAdminCredential $cloudAdminCreds ` 
-PrivilegedEndpoint $privilegedEndpoint ` 
-DefaultSSLCertificatePassword $PfxPass ` 
-DependencyFilesLocalPath $tempDir\cert ` 
-AcceptLicense 
``` 
 
### <a name="updatemysqlproviderps1-parameters"></a><span data-ttu-id="dbb4b-126">UpdateMySQLProvider.ps1 parameters</span><span class="sxs-lookup"><span data-stu-id="dbb4b-126">UpdateMySQLProvider.ps1 parameters</span></span> 
<span data-ttu-id="dbb4b-127">You can specify these parameters in the command line.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-127">You can specify these parameters in the command line.</span></span> <span data-ttu-id="dbb4b-128">If you don't, or if any parameter validation fails, you are prompted to provide the required parameters.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-128">If you don't, or if any parameter validation fails, you are prompted to provide the required parameters.</span></span> 

| <span data-ttu-id="dbb4b-129">Parameter Name</span><span class="sxs-lookup"><span data-stu-id="dbb4b-129">Parameter Name</span></span> | <span data-ttu-id="dbb4b-130">Description</span><span class="sxs-lookup"><span data-stu-id="dbb4b-130">Description</span></span> | <span data-ttu-id="dbb4b-131">Comment or default value</span><span class="sxs-lookup"><span data-stu-id="dbb4b-131">Comment or default value</span></span> | 
| --- | --- | --- | 
| <span data-ttu-id="dbb4b-132">**CloudAdminCredential**</span><span class="sxs-lookup"><span data-stu-id="dbb4b-132">**CloudAdminCredential**</span></span> | <span data-ttu-id="dbb4b-133">The credential for the cloud administrator, necessary for accessing the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-133">The credential for the cloud administrator, necessary for accessing the privileged endpoint.</span></span> | <span data-ttu-id="dbb4b-134">_Required_</span><span class="sxs-lookup"><span data-stu-id="dbb4b-134">_Required_</span></span> | 
| <span data-ttu-id="dbb4b-135">**AzCredential**</span><span class="sxs-lookup"><span data-stu-id="dbb4b-135">**AzCredential**</span></span> | <span data-ttu-id="dbb4b-136">The credentials for the Azure Stack service admin account.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-136">The credentials for the Azure Stack service admin account.</span></span> <span data-ttu-id="dbb4b-137">Use the same credentials as you used for deploying Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-137">Use the same credentials as you used for deploying Azure Stack.</span></span> | <span data-ttu-id="dbb4b-138">_Required_</span><span class="sxs-lookup"><span data-stu-id="dbb4b-138">_Required_</span></span> | 
| <span data-ttu-id="dbb4b-139">**VMLocalCredential**</span><span class="sxs-lookup"><span data-stu-id="dbb4b-139">**VMLocalCredential**</span></span> |<span data-ttu-id="dbb4b-140">The credentials for the local administrator account of the SQL resource provider VM.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-140">The credentials for the local administrator account of the SQL resource provider VM.</span></span> | <span data-ttu-id="dbb4b-141">_Required_</span><span class="sxs-lookup"><span data-stu-id="dbb4b-141">_Required_</span></span> | 
| <span data-ttu-id="dbb4b-142">**PrivilegedEndpoint**</span><span class="sxs-lookup"><span data-stu-id="dbb4b-142">**PrivilegedEndpoint**</span></span> | <span data-ttu-id="dbb4b-143">The IP address or DNS name of the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-143">The IP address or DNS name of the privileged endpoint.</span></span> |  <span data-ttu-id="dbb4b-144">_Required_</span><span class="sxs-lookup"><span data-stu-id="dbb4b-144">_Required_</span></span> | 
| <span data-ttu-id="dbb4b-145">**AzureEnvironment**</span><span class="sxs-lookup"><span data-stu-id="dbb4b-145">**AzureEnvironment**</span></span> | <span data-ttu-id="dbb4b-146">The azure environment of the service admin account which you used for deploying Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-146">The azure environment of the service admin account which you used for deploying Azure Stack.</span></span> <span data-ttu-id="dbb4b-147">Required only if it’s NOT ADFS.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-147">Required only if it’s NOT ADFS.</span></span> <span data-ttu-id="dbb4b-148">Supported environment names are **AzureCloud**, **AzureUSGovernment**, or if using a China Azure Active Directory, **AzureChinaCloud**.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-148">Supported environment names are **AzureCloud**, **AzureUSGovernment**, or if using a China Azure Active Directory, **AzureChinaCloud**.</span></span> | <span data-ttu-id="dbb4b-149">AzureCloud</span><span class="sxs-lookup"><span data-stu-id="dbb4b-149">AzureCloud</span></span> |
| <span data-ttu-id="dbb4b-150">**DependencyFilesLocalPath**</span><span class="sxs-lookup"><span data-stu-id="dbb4b-150">**DependencyFilesLocalPath**</span></span> | <span data-ttu-id="dbb4b-151">Your certificate .pfx file must be placed in this directory as well.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-151">Your certificate .pfx file must be placed in this directory as well.</span></span> | <span data-ttu-id="dbb4b-152">_Optional_ (_mandatory_ for multi-node)</span><span class="sxs-lookup"><span data-stu-id="dbb4b-152">_Optional_ (_mandatory_ for multi-node)</span></span> | 
| <span data-ttu-id="dbb4b-153">**DefaultSSLCertificatePassword**</span><span class="sxs-lookup"><span data-stu-id="dbb4b-153">**DefaultSSLCertificatePassword**</span></span> | <span data-ttu-id="dbb4b-154">The password for the .pfx certificate.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-154">The password for the .pfx certificate.</span></span> | <span data-ttu-id="dbb4b-155">_Required_</span><span class="sxs-lookup"><span data-stu-id="dbb4b-155">_Required_</span></span> | 
| <span data-ttu-id="dbb4b-156">**MaxRetryCount**</span><span class="sxs-lookup"><span data-stu-id="dbb4b-156">**MaxRetryCount**</span></span> | <span data-ttu-id="dbb4b-157">The number of times you want to retry each operation if there is a failure.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-157">The number of times you want to retry each operation if there is a failure.</span></span>| <span data-ttu-id="dbb4b-158">2</span><span class="sxs-lookup"><span data-stu-id="dbb4b-158">2</span></span> | 
| <span data-ttu-id="dbb4b-159">**RetryDuration**</span><span class="sxs-lookup"><span data-stu-id="dbb4b-159">**RetryDuration**</span></span> | <span data-ttu-id="dbb4b-160">The timeout interval between retries, in seconds.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-160">The timeout interval between retries, in seconds.</span></span> | <span data-ttu-id="dbb4b-161">120</span><span class="sxs-lookup"><span data-stu-id="dbb4b-161">120</span></span> | 
| <span data-ttu-id="dbb4b-162">**Uninstall**</span><span class="sxs-lookup"><span data-stu-id="dbb4b-162">**Uninstall**</span></span> | <span data-ttu-id="dbb4b-163">Remove the resource provider and all associated resources (see the following notes).</span><span class="sxs-lookup"><span data-stu-id="dbb4b-163">Remove the resource provider and all associated resources (see the following notes).</span></span> | <span data-ttu-id="dbb4b-164">No</span><span class="sxs-lookup"><span data-stu-id="dbb4b-164">No</span></span> | 
| <span data-ttu-id="dbb4b-165">**DebugMode**</span><span class="sxs-lookup"><span data-stu-id="dbb4b-165">**DebugMode**</span></span> | <span data-ttu-id="dbb4b-166">Prevents automatic cleanup on failure.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-166">Prevents automatic cleanup on failure.</span></span> | <span data-ttu-id="dbb4b-167">No</span><span class="sxs-lookup"><span data-stu-id="dbb4b-167">No</span></span> | 
| <span data-ttu-id="dbb4b-168">**AcceptLicense**</span><span class="sxs-lookup"><span data-stu-id="dbb4b-168">**AcceptLicense**</span></span> | <span data-ttu-id="dbb4b-169">Skips the prompt to accept the GPL license.</span><span class="sxs-lookup"><span data-stu-id="dbb4b-169">Skips the prompt to accept the GPL license.</span></span>  <span data-ttu-id="dbb4b-170">(http://www.gnu.org/licenses/old-licenses/gpl-2.0.html)</span><span class="sxs-lookup"><span data-stu-id="dbb4b-170">(http://www.gnu.org/licenses/old-licenses/gpl-2.0.html)</span></span> | | 
 

## <a name="next-steps"></a><span data-ttu-id="dbb4b-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="dbb4b-171">Next steps</span></span>
[<span data-ttu-id="dbb4b-172">Maintain MySQL resource provider</span><span class="sxs-lookup"><span data-stu-id="dbb4b-172">Maintain MySQL resource provider</span></span>](azure-stack-mysql-resource-provider-maintain.md)
