---
title: Before you deploy App Service on Azure Stack | Microsoft Docs
description: Steps to complete before you deploy App Service on Azure Stack
services: azure-stack
documentationcenter: ''
author: apwestgarth
manager: stefsch
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/20/2018
ms.author: anwestg
ms.openlocfilehash: e5fc6b5d396a45d15548cfdd8f445158147ad12f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804835"
---
# <a name="before-you-get-started-with-app-service-on-azure-stack"></a><span data-ttu-id="f2915-103">Before you get started with App Service on Azure Stack</span><span class="sxs-lookup"><span data-stu-id="f2915-103">Before you get started with App Service on Azure Stack</span></span>

<span data-ttu-id="f2915-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="f2915-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="f2915-105">Before you deploy Azure App Service on Azure Stack, you must complete the prerequisite steps in this article.</span><span class="sxs-lookup"><span data-stu-id="f2915-105">Before you deploy Azure App Service on Azure Stack, you must complete the prerequisite steps in this article.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2915-106">Apply the 1807 update to your Azure Stack integrated system or deploy the latest Azure Stack Development Kit (ASDK) before you deploy Azure App Service 1.3.</span><span class="sxs-lookup"><span data-stu-id="f2915-106">Apply the 1807 update to your Azure Stack integrated system or deploy the latest Azure Stack Development Kit (ASDK) before you deploy Azure App Service 1.3.</span></span>

## <a name="download-the-installer-and-helper-scripts"></a><span data-ttu-id="f2915-107">Download the installer and helper scripts</span><span class="sxs-lookup"><span data-stu-id="f2915-107">Download the installer and helper scripts</span></span>

1. <span data-ttu-id="f2915-108">Download the [App Service on Azure Stack deployment helper scripts](https://aka.ms/appsvconmashelpers).</span><span class="sxs-lookup"><span data-stu-id="f2915-108">Download the [App Service on Azure Stack deployment helper scripts](https://aka.ms/appsvconmashelpers).</span></span>
2. <span data-ttu-id="f2915-109">Download the [App Service on Azure Stack installer](https://aka.ms/appsvconmasinstaller).</span><span class="sxs-lookup"><span data-stu-id="f2915-109">Download the [App Service on Azure Stack installer](https://aka.ms/appsvconmasinstaller).</span></span>
3. <span data-ttu-id="f2915-110">Extract the files from the helper scripts .zip file.</span><span class="sxs-lookup"><span data-stu-id="f2915-110">Extract the files from the helper scripts .zip file.</span></span> <span data-ttu-id="f2915-111">The following files and folders are extracted:</span><span class="sxs-lookup"><span data-stu-id="f2915-111">The following files and folders are extracted:</span></span>

   - <span data-ttu-id="f2915-112">Common.ps1</span><span class="sxs-lookup"><span data-stu-id="f2915-112">Common.ps1</span></span>
   - <span data-ttu-id="f2915-113">Create-AADIdentityApp.ps1</span><span class="sxs-lookup"><span data-stu-id="f2915-113">Create-AADIdentityApp.ps1</span></span>
   - <span data-ttu-id="f2915-114">Create-ADFSIdentityApp.ps1</span><span class="sxs-lookup"><span data-stu-id="f2915-114">Create-ADFSIdentityApp.ps1</span></span>
   - <span data-ttu-id="f2915-115">Create-AppServiceCerts.ps1</span><span class="sxs-lookup"><span data-stu-id="f2915-115">Create-AppServiceCerts.ps1</span></span>
   - <span data-ttu-id="f2915-116">Get-AzureStackRootCert.ps1</span><span class="sxs-lookup"><span data-stu-id="f2915-116">Get-AzureStackRootCert.ps1</span></span>
   - <span data-ttu-id="f2915-117">Remove-AppService.ps1</span><span class="sxs-lookup"><span data-stu-id="f2915-117">Remove-AppService.ps1</span></span>
   - <span data-ttu-id="f2915-118">Modules folder</span><span class="sxs-lookup"><span data-stu-id="f2915-118">Modules folder</span></span>
     - <span data-ttu-id="f2915-119">GraphAPI.psm1</span><span class="sxs-lookup"><span data-stu-id="f2915-119">GraphAPI.psm1</span></span>

## <a name="high-availability"></a><span data-ttu-id="f2915-120">High availability</span><span class="sxs-lookup"><span data-stu-id="f2915-120">High availability</span></span>

<span data-ttu-id="f2915-121">The Azure Stack 1802 update added support for fault domains.</span><span class="sxs-lookup"><span data-stu-id="f2915-121">The Azure Stack 1802 update added support for fault domains.</span></span> <span data-ttu-id="f2915-122">New deployments of Azure App Service on Azure Stack will be distributed across fault domains and provide fault tolerance.</span><span class="sxs-lookup"><span data-stu-id="f2915-122">New deployments of Azure App Service on Azure Stack will be distributed across fault domains and provide fault tolerance.</span></span>

<span data-ttu-id="f2915-123">For existing deployments of Azure App Service on Azure Stack, which were deployed before the 1802 update, see the [Rebalance an App Service resource provider across fault domains](azure-stack-app-service-fault-domain-update.md) article.</span><span class="sxs-lookup"><span data-stu-id="f2915-123">For existing deployments of Azure App Service on Azure Stack, which were deployed before the 1802 update, see the [Rebalance an App Service resource provider across fault domains](azure-stack-app-service-fault-domain-update.md) article.</span></span>

<span data-ttu-id="f2915-124">Additionally, deploy the required file server and SQL Server instances in a highly available configuration.</span><span class="sxs-lookup"><span data-stu-id="f2915-124">Additionally, deploy the required file server and SQL Server instances in a highly available configuration.</span></span>

## <a name="get-certificates"></a><span data-ttu-id="f2915-125">Get certificates</span><span class="sxs-lookup"><span data-stu-id="f2915-125">Get certificates</span></span>

### <a name="azure-resource-manager-root-certificate-for-azure-stack"></a><span data-ttu-id="f2915-126">Azure Resource Manager root certificate for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="f2915-126">Azure Resource Manager root certificate for Azure Stack</span></span>

<span data-ttu-id="f2915-127">Open an elevated PowerShell session on a computer that can reach the privileged endpoint on the Azure Stack Integrated System or Azure Stack Development Kit Host.</span><span class="sxs-lookup"><span data-stu-id="f2915-127">Open an elevated PowerShell session on a computer that can reach the privileged endpoint on the Azure Stack Integrated System or Azure Stack Development Kit Host.</span></span>

<span data-ttu-id="f2915-128">Run the *Get-AzureStackRootCert.ps1* script from the folder where you extracted the helper scripts.</span><span class="sxs-lookup"><span data-stu-id="f2915-128">Run the *Get-AzureStackRootCert.ps1* script from the folder where you extracted the helper scripts.</span></span> <span data-ttu-id="f2915-129">The script creates a root certificate in the same folder as the script that App Service needs for creating certificates.</span><span class="sxs-lookup"><span data-stu-id="f2915-129">The script creates a root certificate in the same folder as the script that App Service needs for creating certificates.</span></span>

<span data-ttu-id="f2915-130">When you run the following PowerShell command you'll have to provide the privileged endpoint and the credentials for the AzureStack\CloudAdmin.</span><span class="sxs-lookup"><span data-stu-id="f2915-130">When you run the following PowerShell command you'll have to provide the privileged endpoint and the credentials for the AzureStack\CloudAdmin.</span></span>

```PowerShell
    Get-AzureStackRootCert.ps1
```

#### <a name="get-azurestackrootcertps1-script-parameters"></a><span data-ttu-id="f2915-131">Get-AzureStackRootCert.ps1 script parameters</span><span class="sxs-lookup"><span data-stu-id="f2915-131">Get-AzureStackRootCert.ps1 script parameters</span></span>

| <span data-ttu-id="f2915-132">Parameter</span><span class="sxs-lookup"><span data-stu-id="f2915-132">Parameter</span></span> | <span data-ttu-id="f2915-133">Required or optional</span><span class="sxs-lookup"><span data-stu-id="f2915-133">Required or optional</span></span> | <span data-ttu-id="f2915-134">Default value</span><span class="sxs-lookup"><span data-stu-id="f2915-134">Default value</span></span> | <span data-ttu-id="f2915-135">Description</span><span class="sxs-lookup"><span data-stu-id="f2915-135">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f2915-136">PrivilegedEndpoint</span><span class="sxs-lookup"><span data-stu-id="f2915-136">PrivilegedEndpoint</span></span> | <span data-ttu-id="f2915-137">Required</span><span class="sxs-lookup"><span data-stu-id="f2915-137">Required</span></span> | <span data-ttu-id="f2915-138">AzS-ERCS01</span><span class="sxs-lookup"><span data-stu-id="f2915-138">AzS-ERCS01</span></span> | <span data-ttu-id="f2915-139">Privileged endpoint</span><span class="sxs-lookup"><span data-stu-id="f2915-139">Privileged endpoint</span></span> |
| <span data-ttu-id="f2915-140">CloudAdminCredential</span><span class="sxs-lookup"><span data-stu-id="f2915-140">CloudAdminCredential</span></span> | <span data-ttu-id="f2915-141">Required</span><span class="sxs-lookup"><span data-stu-id="f2915-141">Required</span></span> | <span data-ttu-id="f2915-142">AzureStack\CloudAdmin</span><span class="sxs-lookup"><span data-stu-id="f2915-142">AzureStack\CloudAdmin</span></span> | <span data-ttu-id="f2915-143">Domain account credential for Azure Stack cloud admins</span><span class="sxs-lookup"><span data-stu-id="f2915-143">Domain account credential for Azure Stack cloud admins</span></span> |

### <a name="certificates-required-for-asdk-deployment-of-azure-app-service"></a><span data-ttu-id="f2915-144">Certificates required for ASDK deployment of Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f2915-144">Certificates required for ASDK deployment of Azure App Service</span></span>

<span data-ttu-id="f2915-145">The *Create-AppServiceCerts.ps1* script works with the Azure Stack certificate authority to create the four certificates that App Service needs.</span><span class="sxs-lookup"><span data-stu-id="f2915-145">The *Create-AppServiceCerts.ps1* script works with the Azure Stack certificate authority to create the four certificates that App Service needs.</span></span>

| <span data-ttu-id="f2915-146">File name</span><span class="sxs-lookup"><span data-stu-id="f2915-146">File name</span></span> | <span data-ttu-id="f2915-147">Use</span><span class="sxs-lookup"><span data-stu-id="f2915-147">Use</span></span> |
| --- | --- |
| <span data-ttu-id="f2915-148">_.appservice.local.azurestack.external.pfx</span><span class="sxs-lookup"><span data-stu-id="f2915-148">_.appservice.local.azurestack.external.pfx</span></span> | <span data-ttu-id="f2915-149">App Service default SSL certificate</span><span class="sxs-lookup"><span data-stu-id="f2915-149">App Service default SSL certificate</span></span> |
| <span data-ttu-id="f2915-150">api.appservice.local.azurestack.external.pfx</span><span class="sxs-lookup"><span data-stu-id="f2915-150">api.appservice.local.azurestack.external.pfx</span></span> | <span data-ttu-id="f2915-151">App Service API SSL certificate</span><span class="sxs-lookup"><span data-stu-id="f2915-151">App Service API SSL certificate</span></span> |
| <span data-ttu-id="f2915-152">ftp.appservice.local.azurestack.external.pfx</span><span class="sxs-lookup"><span data-stu-id="f2915-152">ftp.appservice.local.azurestack.external.pfx</span></span> | <span data-ttu-id="f2915-153">App Service publisher SSL certificate</span><span class="sxs-lookup"><span data-stu-id="f2915-153">App Service publisher SSL certificate</span></span> |
| <span data-ttu-id="f2915-154">sso.appservice.local.azurestack.external.pfx</span><span class="sxs-lookup"><span data-stu-id="f2915-154">sso.appservice.local.azurestack.external.pfx</span></span> | <span data-ttu-id="f2915-155">App Service identity application certificate</span><span class="sxs-lookup"><span data-stu-id="f2915-155">App Service identity application certificate</span></span> |

<span data-ttu-id="f2915-156">To create the certificates, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="f2915-156">To create the certificates, follow these steps:</span></span>

1. <span data-ttu-id="f2915-157">Sign in to the Azure Stack Development Kit host using the AzureStack\AzureStackAdmin account.</span><span class="sxs-lookup"><span data-stu-id="f2915-157">Sign in to the Azure Stack Development Kit host using the AzureStack\AzureStackAdmin account.</span></span>
2. <span data-ttu-id="f2915-158">Open an elevated PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="f2915-158">Open an elevated PowerShell session.</span></span>
3. <span data-ttu-id="f2915-159">Run the *Create-AppServiceCerts.ps1* script from the folder where you extracted the helper scripts.</span><span class="sxs-lookup"><span data-stu-id="f2915-159">Run the *Create-AppServiceCerts.ps1* script from the folder where you extracted the helper scripts.</span></span> <span data-ttu-id="f2915-160">This script creates four certificates in the same folder as the script that App Service needs for creating certificates.</span><span class="sxs-lookup"><span data-stu-id="f2915-160">This script creates four certificates in the same folder as the script that App Service needs for creating certificates.</span></span>
4. <span data-ttu-id="f2915-161">Enter a password to secure the .pfx files, and make a note of it.</span><span class="sxs-lookup"><span data-stu-id="f2915-161">Enter a password to secure the .pfx files, and make a note of it.</span></span> <span data-ttu-id="f2915-162">You'll have to enter it in the App Service on Azure Stack installer.</span><span class="sxs-lookup"><span data-stu-id="f2915-162">You'll have to enter it in the App Service on Azure Stack installer.</span></span>

#### <a name="create-appservicecertsps1-script-parameters"></a><span data-ttu-id="f2915-163">Create-AppServiceCerts.ps1 script parameters</span><span class="sxs-lookup"><span data-stu-id="f2915-163">Create-AppServiceCerts.ps1 script parameters</span></span>

| <span data-ttu-id="f2915-164">Parameter</span><span class="sxs-lookup"><span data-stu-id="f2915-164">Parameter</span></span> | <span data-ttu-id="f2915-165">Required or optional</span><span class="sxs-lookup"><span data-stu-id="f2915-165">Required or optional</span></span> | <span data-ttu-id="f2915-166">Default value</span><span class="sxs-lookup"><span data-stu-id="f2915-166">Default value</span></span> | <span data-ttu-id="f2915-167">Description</span><span class="sxs-lookup"><span data-stu-id="f2915-167">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f2915-168">pfxPassword</span><span class="sxs-lookup"><span data-stu-id="f2915-168">pfxPassword</span></span> | <span data-ttu-id="f2915-169">Required</span><span class="sxs-lookup"><span data-stu-id="f2915-169">Required</span></span> | <span data-ttu-id="f2915-170">Null</span><span class="sxs-lookup"><span data-stu-id="f2915-170">Null</span></span> | <span data-ttu-id="f2915-171">Password that helps protect the certificate private key</span><span class="sxs-lookup"><span data-stu-id="f2915-171">Password that helps protect the certificate private key</span></span> |
| <span data-ttu-id="f2915-172">DomainName</span><span class="sxs-lookup"><span data-stu-id="f2915-172">DomainName</span></span> | <span data-ttu-id="f2915-173">Required</span><span class="sxs-lookup"><span data-stu-id="f2915-173">Required</span></span> | <span data-ttu-id="f2915-174">local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="f2915-174">local.azurestack.external</span></span> | <span data-ttu-id="f2915-175">Azure Stack region and domain suffix</span><span class="sxs-lookup"><span data-stu-id="f2915-175">Azure Stack region and domain suffix</span></span> |

### <a name="certificates-required-for-azure-stack-production-deployment-of-azure-app-service"></a><span data-ttu-id="f2915-176">Certificates required for Azure Stack production deployment of Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f2915-176">Certificates required for Azure Stack production deployment of Azure App Service</span></span>

<span data-ttu-id="f2915-177">To run the resource provider in production, you must provide the following certificates:</span><span class="sxs-lookup"><span data-stu-id="f2915-177">To run the resource provider in production, you must provide the following certificates:</span></span>

- <span data-ttu-id="f2915-178">Default domain certificate</span><span class="sxs-lookup"><span data-stu-id="f2915-178">Default domain certificate</span></span>
- <span data-ttu-id="f2915-179">API certificate</span><span class="sxs-lookup"><span data-stu-id="f2915-179">API certificate</span></span>
- <span data-ttu-id="f2915-180">Publishing certificate</span><span class="sxs-lookup"><span data-stu-id="f2915-180">Publishing certificate</span></span>
- <span data-ttu-id="f2915-181">Identity certificate</span><span class="sxs-lookup"><span data-stu-id="f2915-181">Identity certificate</span></span>

#### <a name="default-domain-certificate"></a><span data-ttu-id="f2915-182">Default domain certificate</span><span class="sxs-lookup"><span data-stu-id="f2915-182">Default domain certificate</span></span>

<span data-ttu-id="f2915-183">The default domain certificate is placed on the Front End role.</span><span class="sxs-lookup"><span data-stu-id="f2915-183">The default domain certificate is placed on the Front End role.</span></span> <span data-ttu-id="f2915-184">User applications for wildcard or default domain request to Azure App Service use this certificate.</span><span class="sxs-lookup"><span data-stu-id="f2915-184">User applications for wildcard or default domain request to Azure App Service use this certificate.</span></span> <span data-ttu-id="f2915-185">The certificate is also used for source control operations (Kudu).</span><span class="sxs-lookup"><span data-stu-id="f2915-185">The certificate is also used for source control operations (Kudu).</span></span>

<span data-ttu-id="f2915-186">The certificate must be in .pfx format and should be a three-subject wildcard certificate.</span><span class="sxs-lookup"><span data-stu-id="f2915-186">The certificate must be in .pfx format and should be a three-subject wildcard certificate.</span></span> <span data-ttu-id="f2915-187">This requirement allows one certificate to cover both the default domain and the SCM endpoint for source control operations.</span><span class="sxs-lookup"><span data-stu-id="f2915-187">This requirement allows one certificate to cover both the default domain and the SCM endpoint for source control operations.</span></span>

| <span data-ttu-id="f2915-188">Format</span><span class="sxs-lookup"><span data-stu-id="f2915-188">Format</span></span> | <span data-ttu-id="f2915-189">Example</span><span class="sxs-lookup"><span data-stu-id="f2915-189">Example</span></span> |
| --- | --- |
| <span data-ttu-id="f2915-190">\*.appservice.\<region\>.\<DomainName\>.\<extension\></span><span class="sxs-lookup"><span data-stu-id="f2915-190">\*.appservice.\<region\>.\<DomainName\>.\<extension\></span></span> | <span data-ttu-id="f2915-191">\*.appservice.redmond.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="f2915-191">\*.appservice.redmond.azurestack.external</span></span> |
| <span data-ttu-id="f2915-192">\*.scm.appservice.<region>.<DomainName>.<extension></span><span class="sxs-lookup"><span data-stu-id="f2915-192">\*.scm.appservice.<region>.<DomainName>.<extension></span></span> | <span data-ttu-id="f2915-193">\*.scm.appservice.redmond.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="f2915-193">\*.scm.appservice.redmond.azurestack.external</span></span> |
| <span data-ttu-id="f2915-194">\*.sso.appservice.<region>.<DomainName>.<extension></span><span class="sxs-lookup"><span data-stu-id="f2915-194">\*.sso.appservice.<region>.<DomainName>.<extension></span></span> | <span data-ttu-id="f2915-195">\*.sso.appservice.redmond.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="f2915-195">\*.sso.appservice.redmond.azurestack.external</span></span> |

#### <a name="api-certificate"></a><span data-ttu-id="f2915-196">API certificate</span><span class="sxs-lookup"><span data-stu-id="f2915-196">API certificate</span></span>

<span data-ttu-id="f2915-197">The API certificate is placed on the Management role.</span><span class="sxs-lookup"><span data-stu-id="f2915-197">The API certificate is placed on the Management role.</span></span> <span data-ttu-id="f2915-198">The resource provider uses it to help secure API calls.</span><span class="sxs-lookup"><span data-stu-id="f2915-198">The resource provider uses it to help secure API calls.</span></span> <span data-ttu-id="f2915-199">The certificate for publishing must contain a subject that matches the API DNS entry.</span><span class="sxs-lookup"><span data-stu-id="f2915-199">The certificate for publishing must contain a subject that matches the API DNS entry.</span></span>

| <span data-ttu-id="f2915-200">Format</span><span class="sxs-lookup"><span data-stu-id="f2915-200">Format</span></span> | <span data-ttu-id="f2915-201">Example</span><span class="sxs-lookup"><span data-stu-id="f2915-201">Example</span></span> |
| --- | --- |
| <span data-ttu-id="f2915-202">api.appservice.\<region\>.\<DomainName\>.\<extension\></span><span class="sxs-lookup"><span data-stu-id="f2915-202">api.appservice.\<region\>.\<DomainName\>.\<extension\></span></span> | <span data-ttu-id="f2915-203">api.appservice.redmond.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="f2915-203">api.appservice.redmond.azurestack.external</span></span> |

#### <a name="publishing-certificate"></a><span data-ttu-id="f2915-204">Publishing certificate</span><span class="sxs-lookup"><span data-stu-id="f2915-204">Publishing certificate</span></span>

<span data-ttu-id="f2915-205">The certificate for the Publisher role secures the FTPS traffic for application owners when they upload content.</span><span class="sxs-lookup"><span data-stu-id="f2915-205">The certificate for the Publisher role secures the FTPS traffic for application owners when they upload content.</span></span> <span data-ttu-id="f2915-206">The certificate for publishing must contain a subject that matches the FTPS DNS entry.</span><span class="sxs-lookup"><span data-stu-id="f2915-206">The certificate for publishing must contain a subject that matches the FTPS DNS entry.</span></span>

| <span data-ttu-id="f2915-207">Format</span><span class="sxs-lookup"><span data-stu-id="f2915-207">Format</span></span> | <span data-ttu-id="f2915-208">Example</span><span class="sxs-lookup"><span data-stu-id="f2915-208">Example</span></span> |
| --- | --- |
| <span data-ttu-id="f2915-209">ftp.appservice.\<region\>.\<DomainName\>.\<extension\></span><span class="sxs-lookup"><span data-stu-id="f2915-209">ftp.appservice.\<region\>.\<DomainName\>.\<extension\></span></span> | <span data-ttu-id="f2915-210">ftp.appservice.redmond.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="f2915-210">ftp.appservice.redmond.azurestack.external</span></span> |

#### <a name="identity-certificate"></a><span data-ttu-id="f2915-211">Identity certificate</span><span class="sxs-lookup"><span data-stu-id="f2915-211">Identity certificate</span></span>

<span data-ttu-id="f2915-212">The certificate for the identity application enables:</span><span class="sxs-lookup"><span data-stu-id="f2915-212">The certificate for the identity application enables:</span></span>

- <span data-ttu-id="f2915-213">Integration between the Azure Active Directory (Azure AD) or Active Directory Federation Services (AD FS) directory, Azure Stack, and App Service to support integration with the compute resource provider.</span><span class="sxs-lookup"><span data-stu-id="f2915-213">Integration between the Azure Active Directory (Azure AD) or Active Directory Federation Services (AD FS) directory, Azure Stack, and App Service to support integration with the compute resource provider.</span></span>
- <span data-ttu-id="f2915-214">Single sign-on scenarios for advanced developer tools within Azure App Service on Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="f2915-214">Single sign-on scenarios for advanced developer tools within Azure App Service on Azure Stack.</span></span>

<span data-ttu-id="f2915-215">The certificate for identity must contain a subject that matches the following format.</span><span class="sxs-lookup"><span data-stu-id="f2915-215">The certificate for identity must contain a subject that matches the following format.</span></span>

| <span data-ttu-id="f2915-216">Format</span><span class="sxs-lookup"><span data-stu-id="f2915-216">Format</span></span> | <span data-ttu-id="f2915-217">Example</span><span class="sxs-lookup"><span data-stu-id="f2915-217">Example</span></span> |
| --- | --- |
| <span data-ttu-id="f2915-218">sso.appservice.\<region\>.\<DomainName\>.\<extension\></span><span class="sxs-lookup"><span data-stu-id="f2915-218">sso.appservice.\<region\>.\<DomainName\>.\<extension\></span></span> | <span data-ttu-id="f2915-219">sso.appservice.redmond.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="f2915-219">sso.appservice.redmond.azurestack.external</span></span> |

## <a name="virtual-network"></a><span data-ttu-id="f2915-220">Virtual network</span><span class="sxs-lookup"><span data-stu-id="f2915-220">Virtual network</span></span>

<span data-ttu-id="f2915-221">Azure App Service on Azure Stack lets you deploy the resource provider to an existing virtual network or lets you create a virtual network as part of the deployment.</span><span class="sxs-lookup"><span data-stu-id="f2915-221">Azure App Service on Azure Stack lets you deploy the resource provider to an existing virtual network or lets you create a virtual network as part of the deployment.</span></span> <span data-ttu-id="f2915-222">Using an existing virtual network enables the use of internal IPs to connect to the file server and SQL server required by Azure App Service on Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="f2915-222">Using an existing virtual network enables the use of internal IPs to connect to the file server and SQL server required by Azure App Service on Azure Stack.</span></span> <span data-ttu-id="f2915-223">The virtual network must be configured with the following address range and subnets before installing Azure App Service on Azure Stack:</span><span class="sxs-lookup"><span data-stu-id="f2915-223">The virtual network must be configured with the following address range and subnets before installing Azure App Service on Azure Stack:</span></span>

<span data-ttu-id="f2915-224">Virtual Network - /16</span><span class="sxs-lookup"><span data-stu-id="f2915-224">Virtual Network - /16</span></span>

<span data-ttu-id="f2915-225">Subnets</span><span class="sxs-lookup"><span data-stu-id="f2915-225">Subnets</span></span>

- <span data-ttu-id="f2915-226">ControllersSubnet /24</span><span class="sxs-lookup"><span data-stu-id="f2915-226">ControllersSubnet /24</span></span>
- <span data-ttu-id="f2915-227">ManagementServersSubnet /24</span><span class="sxs-lookup"><span data-stu-id="f2915-227">ManagementServersSubnet /24</span></span>
- <span data-ttu-id="f2915-228">FrontEndsSubnet /24</span><span class="sxs-lookup"><span data-stu-id="f2915-228">FrontEndsSubnet /24</span></span>
- <span data-ttu-id="f2915-229">PublishersSubnet /24</span><span class="sxs-lookup"><span data-stu-id="f2915-229">PublishersSubnet /24</span></span>
- <span data-ttu-id="f2915-230">WorkersSubnet /21</span><span class="sxs-lookup"><span data-stu-id="f2915-230">WorkersSubnet /21</span></span>

## <a name="prepare-the-file-server"></a><span data-ttu-id="f2915-231">Prepare the file server</span><span class="sxs-lookup"><span data-stu-id="f2915-231">Prepare the file server</span></span>

<span data-ttu-id="f2915-232">Azure App Service requires the use of a file server.</span><span class="sxs-lookup"><span data-stu-id="f2915-232">Azure App Service requires the use of a file server.</span></span> <span data-ttu-id="f2915-233">For production deployments, the file server must be configured to be highly available and capable of handling failures.</span><span class="sxs-lookup"><span data-stu-id="f2915-233">For production deployments, the file server must be configured to be highly available and capable of handling failures.</span></span>

<span data-ttu-id="f2915-234">For Azure Stack Development Kit deployments only, you can use the [example Azure Resource Manager deployment template](https://aka.ms/appsvconmasdkfstemplate) to deploy a configured single-node file server.</span><span class="sxs-lookup"><span data-stu-id="f2915-234">For Azure Stack Development Kit deployments only, you can use the [example Azure Resource Manager deployment template](https://aka.ms/appsvconmasdkfstemplate) to deploy a configured single-node file server.</span></span> <span data-ttu-id="f2915-235">The single-node file server will be in a workgroup.</span><span class="sxs-lookup"><span data-stu-id="f2915-235">The single-node file server will be in a workgroup.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="f2915-236">If you choose to deploy App Service in an existing Virtual Network the File Server should be deployed into a separate Subnet from App Service.</span><span class="sxs-lookup"><span data-stu-id="f2915-236">If you choose to deploy App Service in an existing Virtual Network the File Server should be deployed into a separate Subnet from App Service.</span></span>

### <a name="provision-groups-and-accounts-in-active-directory"></a><span data-ttu-id="f2915-237">Provision groups and accounts in Active Directory</span><span class="sxs-lookup"><span data-stu-id="f2915-237">Provision groups and accounts in Active Directory</span></span>

1. <span data-ttu-id="f2915-238">Create the following Active Directory global security groups:</span><span class="sxs-lookup"><span data-stu-id="f2915-238">Create the following Active Directory global security groups:</span></span>

   - <span data-ttu-id="f2915-239">FileShareOwners</span><span class="sxs-lookup"><span data-stu-id="f2915-239">FileShareOwners</span></span>
   - <span data-ttu-id="f2915-240">FileShareUsers</span><span class="sxs-lookup"><span data-stu-id="f2915-240">FileShareUsers</span></span>

2. <span data-ttu-id="f2915-241">Create the following Active Directory accounts as service accounts:</span><span class="sxs-lookup"><span data-stu-id="f2915-241">Create the following Active Directory accounts as service accounts:</span></span>

   - <span data-ttu-id="f2915-242">FileShareOwner</span><span class="sxs-lookup"><span data-stu-id="f2915-242">FileShareOwner</span></span>
   - <span data-ttu-id="f2915-243">FileShareUser</span><span class="sxs-lookup"><span data-stu-id="f2915-243">FileShareUser</span></span>

   <span data-ttu-id="f2915-244">As a security best practice, the users for these accounts (and for all web roles) should be unique  and have strong usernames and passwords.</span><span class="sxs-lookup"><span data-stu-id="f2915-244">As a security best practice, the users for these accounts (and for all web roles) should be unique  and have strong usernames and passwords.</span></span> <span data-ttu-id="f2915-245">Set the passwords with the following conditions:</span><span class="sxs-lookup"><span data-stu-id="f2915-245">Set the passwords with the following conditions:</span></span>

   - <span data-ttu-id="f2915-246">Enable **Password never expires**.</span><span class="sxs-lookup"><span data-stu-id="f2915-246">Enable **Password never expires**.</span></span>
   - <span data-ttu-id="f2915-247">Enable **User cannot change password**.</span><span class="sxs-lookup"><span data-stu-id="f2915-247">Enable **User cannot change password**.</span></span>
   - <span data-ttu-id="f2915-248">Disable **User must change password at next logon**.</span><span class="sxs-lookup"><span data-stu-id="f2915-248">Disable **User must change password at next logon**.</span></span>

3. <span data-ttu-id="f2915-249">Add the accounts to the group memberships as follows:</span><span class="sxs-lookup"><span data-stu-id="f2915-249">Add the accounts to the group memberships as follows:</span></span>

   - <span data-ttu-id="f2915-250">Add **FileShareOwner** to the **FileShareOwners** group.</span><span class="sxs-lookup"><span data-stu-id="f2915-250">Add **FileShareOwner** to the **FileShareOwners** group.</span></span>
   - <span data-ttu-id="f2915-251">Add **FileShareUser** to the **FileShareUsers** group.</span><span class="sxs-lookup"><span data-stu-id="f2915-251">Add **FileShareUser** to the **FileShareUsers** group.</span></span>

### <a name="provision-groups-and-accounts-in-a-workgroup"></a><span data-ttu-id="f2915-252">Provision groups and accounts in a workgroup</span><span class="sxs-lookup"><span data-stu-id="f2915-252">Provision groups and accounts in a workgroup</span></span>

>[!NOTE]
> <span data-ttu-id="f2915-253">When you're configuring a file server, run all the following commands from an **Administrator Command Prompt**.</span><span class="sxs-lookup"><span data-stu-id="f2915-253">When you're configuring a file server, run all the following commands from an **Administrator Command Prompt**.</span></span> <br><span data-ttu-id="f2915-254">***Don't use PowerShell.***</span><span class="sxs-lookup"><span data-stu-id="f2915-254">***Don't use PowerShell.***</span></span>

<span data-ttu-id="f2915-255">When you use the Azure Resource Manager template, the users are already created.</span><span class="sxs-lookup"><span data-stu-id="f2915-255">When you use the Azure Resource Manager template, the users are already created.</span></span>

1. <span data-ttu-id="f2915-256">Run the following commands to create the FileShareOwner and FileShareUser accounts.</span><span class="sxs-lookup"><span data-stu-id="f2915-256">Run the following commands to create the FileShareOwner and FileShareUser accounts.</span></span> <span data-ttu-id="f2915-257">Replace `<password>` with your own values.</span><span class="sxs-lookup"><span data-stu-id="f2915-257">Replace `<password>` with your own values.</span></span>

   ``` DOS
   net user FileShareOwner <password> /add /expires:never /passwordchg:no
   net user FileShareUser <password> /add /expires:never /passwordchg:no
   ```

2. <span data-ttu-id="f2915-258">Set the passwords for the accounts to never expire by running the following WMIC commands:</span><span class="sxs-lookup"><span data-stu-id="f2915-258">Set the passwords for the accounts to never expire by running the following WMIC commands:</span></span>

   ``` DOS
   WMIC USERACCOUNT WHERE "Name='FileShareOwner'" SET PasswordExpires=FALSE
   WMIC USERACCOUNT WHERE "Name='FileShareUser'" SET PasswordExpires=FALSE
   ```

3. <span data-ttu-id="f2915-259">Create the local groups FileShareUsers and FileShareOwners, and add the accounts in the first step to them:</span><span class="sxs-lookup"><span data-stu-id="f2915-259">Create the local groups FileShareUsers and FileShareOwners, and add the accounts in the first step to them:</span></span>

   ``` DOS
   net localgroup FileShareUsers /add
   net localgroup FileShareUsers FileShareUser /add
   net localgroup FileShareOwners /add
   net localgroup FileShareOwners FileShareOwner /add
   ```

### <a name="provision-the-content-share"></a><span data-ttu-id="f2915-260">Provision the content share</span><span class="sxs-lookup"><span data-stu-id="f2915-260">Provision the content share</span></span>

<span data-ttu-id="f2915-261">The content share contains tenant website content.</span><span class="sxs-lookup"><span data-stu-id="f2915-261">The content share contains tenant website content.</span></span> <span data-ttu-id="f2915-262">The procedure to provision the content share on a single file server is the same for both Active Directory and Workgroup environments.</span><span class="sxs-lookup"><span data-stu-id="f2915-262">The procedure to provision the content share on a single file server is the same for both Active Directory and Workgroup environments.</span></span> <span data-ttu-id="f2915-263">But it's different for a failover cluster in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f2915-263">But it's different for a failover cluster in Active Directory.</span></span>

#### <a name="provision-the-content-share-on-a-single-file-server-active-directory-or-workgroup"></a><span data-ttu-id="f2915-264">Provision the content share on a single file server (Active Directory or workgroup)</span><span class="sxs-lookup"><span data-stu-id="f2915-264">Provision the content share on a single file server (Active Directory or workgroup)</span></span>

<span data-ttu-id="f2915-265">On a single file server, run the following commands at an elevated command prompt.</span><span class="sxs-lookup"><span data-stu-id="f2915-265">On a single file server, run the following commands at an elevated command prompt.</span></span> <span data-ttu-id="f2915-266">Replace the value for `C:\WebSites` with the corresponding paths in your environment.</span><span class="sxs-lookup"><span data-stu-id="f2915-266">Replace the value for `C:\WebSites` with the corresponding paths in your environment.</span></span>

```DOS
set WEBSITES_SHARE=WebSites
set WEBSITES_FOLDER=C:\WebSites
md %WEBSITES_FOLDER%
net share %WEBSITES_SHARE% /delete
net share %WEBSITES_SHARE%=%WEBSITES_FOLDER% /grant:Everyone,full
```

### <a name="configure-access-control-to-the-shares"></a><span data-ttu-id="f2915-267">Configure access control to the shares</span><span class="sxs-lookup"><span data-stu-id="f2915-267">Configure access control to the shares</span></span>

<span data-ttu-id="f2915-268">Run the following commands at an elevated command prompt on the file server or on the failover cluster node, which is the current cluster resource owner.</span><span class="sxs-lookup"><span data-stu-id="f2915-268">Run the following commands at an elevated command prompt on the file server or on the failover cluster node, which is the current cluster resource owner.</span></span> <span data-ttu-id="f2915-269">Replace values in italics with values that are specific to your environment.</span><span class="sxs-lookup"><span data-stu-id="f2915-269">Replace values in italics with values that are specific to your environment.</span></span>

#### <a name="active-directory"></a><span data-ttu-id="f2915-270">Active Directory</span><span class="sxs-lookup"><span data-stu-id="f2915-270">Active Directory</span></span>

```DOS
set DOMAIN=<DOMAIN>
set WEBSITES_FOLDER=C:\WebSites
icacls %WEBSITES_FOLDER% /reset
icacls %WEBSITES_FOLDER% /grant Administrators:(OI)(CI)(F)
icacls %WEBSITES_FOLDER% /grant %DOMAIN%\FileShareOwners:(OI)(CI)(M)
icacls %WEBSITES_FOLDER% /inheritance:r
icacls %WEBSITES_FOLDER% /grant %DOMAIN%\FileShareUsers:(CI)(S,X,RA)
icacls %WEBSITES_FOLDER% /grant *S-1-1-0:(OI)(CI)(IO)(RA,REA,RD)
```

#### <a name="workgroup"></a><span data-ttu-id="f2915-271">Workgroup</span><span class="sxs-lookup"><span data-stu-id="f2915-271">Workgroup</span></span>

```DOS
set WEBSITES_FOLDER=C:\WebSites
icacls %WEBSITES_FOLDER% /reset
icacls %WEBSITES_FOLDER% /grant Administrators:(OI)(CI)(F)
icacls %WEBSITES_FOLDER% /grant FileShareOwners:(OI)(CI)(M)
icacls %WEBSITES_FOLDER% /inheritance:r
icacls %WEBSITES_FOLDER% /grant FileShareUsers:(CI)(S,X,RA)
icacls %WEBSITES_FOLDER% /grant *S-1-1-0:(OI)(CI)(IO)(RA,REA,RD)
```

## <a name="prepare-the-sql-server-instance"></a><span data-ttu-id="f2915-272">Prepare the SQL Server instance</span><span class="sxs-lookup"><span data-stu-id="f2915-272">Prepare the SQL Server instance</span></span>

<span data-ttu-id="f2915-273">For the Azure App Service on Azure Stack hosting and metering databases, you must prepare a SQL Server instance to hold the App Service databases.</span><span class="sxs-lookup"><span data-stu-id="f2915-273">For the Azure App Service on Azure Stack hosting and metering databases, you must prepare a SQL Server instance to hold the App Service databases.</span></span>

<span data-ttu-id="f2915-274">For Azure Stack Development Kit deployments, you can use SQL Server Express 2014 SP2 or later.</span><span class="sxs-lookup"><span data-stu-id="f2915-274">For Azure Stack Development Kit deployments, you can use SQL Server Express 2014 SP2 or later.</span></span>

<span data-ttu-id="f2915-275">For production and high-availability purposes, you should use a full version of SQL Server 2014 SP2 or later, enable mixed-mode authentication, and deploy in a [highly available configuration](https://docs.microsoft.com/sql/sql-server/failover-clusters/high-availability-solutions-sql-server).</span><span class="sxs-lookup"><span data-stu-id="f2915-275">For production and high-availability purposes, you should use a full version of SQL Server 2014 SP2 or later, enable mixed-mode authentication, and deploy in a [highly available configuration](https://docs.microsoft.com/sql/sql-server/failover-clusters/high-availability-solutions-sql-server).</span></span>

<span data-ttu-id="f2915-276">The SQL Server instance for Azure App Service on Azure Stack must be accessible from all App Service roles.</span><span class="sxs-lookup"><span data-stu-id="f2915-276">The SQL Server instance for Azure App Service on Azure Stack must be accessible from all App Service roles.</span></span> <span data-ttu-id="f2915-277">You can deploy SQL Server within the Default Provider Subscription in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="f2915-277">You can deploy SQL Server within the Default Provider Subscription in Azure Stack.</span></span> <span data-ttu-id="f2915-278">Or you can make use of the existing infrastructure within your organization (as long as there is connectivity to Azure Stack).</span><span class="sxs-lookup"><span data-stu-id="f2915-278">Or you can make use of the existing infrastructure within your organization (as long as there is connectivity to Azure Stack).</span></span> <span data-ttu-id="f2915-279">If you're using an Azure Marketplace image, remember to configure the firewall accordingly.</span><span class="sxs-lookup"><span data-stu-id="f2915-279">If you're using an Azure Marketplace image, remember to configure the firewall accordingly.</span></span>

>[!NOTE]
> <span data-ttu-id="f2915-280">A number of SQL IaaS virtual machine images are available through the Marketplace Management feature.</span><span class="sxs-lookup"><span data-stu-id="f2915-280">A number of SQL IaaS virtual machine images are available through the Marketplace Management feature.</span></span> <span data-ttu-id="f2915-281">Make sure you always download the latest version of the SQL IaaS Extension before you deploy a VM using a Marketplace item.</span><span class="sxs-lookup"><span data-stu-id="f2915-281">Make sure you always download the latest version of the SQL IaaS Extension before you deploy a VM using a Marketplace item.</span></span> <span data-ttu-id="f2915-282">The SQL images are the same as the SQL VMs that are available in Azure.</span><span class="sxs-lookup"><span data-stu-id="f2915-282">The SQL images are the same as the SQL VMs that are available in Azure.</span></span> <span data-ttu-id="f2915-283">For SQL VMs created from these images, the IaaS extension and corresponding portal enhancements provide features such as automatic patching and backup capabilities.</span><span class="sxs-lookup"><span data-stu-id="f2915-283">For SQL VMs created from these images, the IaaS extension and corresponding portal enhancements provide features such as automatic patching and backup capabilities.</span></span>
>
<span data-ttu-id="f2915-284">For any of the SQL Server roles, you can use a default instance or a named instance.</span><span class="sxs-lookup"><span data-stu-id="f2915-284">For any of the SQL Server roles, you can use a default instance or a named instance.</span></span> <span data-ttu-id="f2915-285">If you use a named instance, be sure to manually start the SQL Server Browser service and open port 1434.</span><span class="sxs-lookup"><span data-stu-id="f2915-285">If you use a named instance, be sure to manually start the SQL Server Browser service and open port 1434.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="f2915-286">If you choose to deploy App Service in an existing Virtual Network the SQL Server should be deployed into a separate Subnet from App Service and the File Server.</span><span class="sxs-lookup"><span data-stu-id="f2915-286">If you choose to deploy App Service in an existing Virtual Network the SQL Server should be deployed into a separate Subnet from App Service and the File Server.</span></span>
>

## <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="f2915-287">Create an Azure Active Directory application</span><span class="sxs-lookup"><span data-stu-id="f2915-287">Create an Azure Active Directory application</span></span>

<span data-ttu-id="f2915-288">Configure an Azure AD service principal to support the following operations:</span><span class="sxs-lookup"><span data-stu-id="f2915-288">Configure an Azure AD service principal to support the following operations:</span></span>

- <span data-ttu-id="f2915-289">Virtual machine scale set integration on worker tiers.</span><span class="sxs-lookup"><span data-stu-id="f2915-289">Virtual machine scale set integration on worker tiers.</span></span>
- <span data-ttu-id="f2915-290">SSO for the Azure Functions portal and advanced developer tools.</span><span class="sxs-lookup"><span data-stu-id="f2915-290">SSO for the Azure Functions portal and advanced developer tools.</span></span>

<span data-ttu-id="f2915-291">These steps apply to Azure AD-secured Azure Stack environments only.</span><span class="sxs-lookup"><span data-stu-id="f2915-291">These steps apply to Azure AD-secured Azure Stack environments only.</span></span>

<span data-ttu-id="f2915-292">Administrators must configure SSO to:</span><span class="sxs-lookup"><span data-stu-id="f2915-292">Administrators must configure SSO to:</span></span>

- <span data-ttu-id="f2915-293">Enable the advanced developer tools within App Service (Kudu).</span><span class="sxs-lookup"><span data-stu-id="f2915-293">Enable the advanced developer tools within App Service (Kudu).</span></span>
- <span data-ttu-id="f2915-294">Enable the use of the Azure Functions portal experience.</span><span class="sxs-lookup"><span data-stu-id="f2915-294">Enable the use of the Azure Functions portal experience.</span></span>

<span data-ttu-id="f2915-295">Follow these steps:</span><span class="sxs-lookup"><span data-stu-id="f2915-295">Follow these steps:</span></span>

1. <span data-ttu-id="f2915-296">Open a PowerShell instance as azurestack\AzureStackAdmin.</span><span class="sxs-lookup"><span data-stu-id="f2915-296">Open a PowerShell instance as azurestack\AzureStackAdmin.</span></span>
2. <span data-ttu-id="f2915-297">Go to the location of the scripts that you downloaded and extracted in the [prerequisite step](https://docs.microsoft.com/azure/azure-stack/azure-stack-app-service-before-you-get-started#download-the-azure-app-service-on-azure-stack-installer-and-helper-scripts).</span><span class="sxs-lookup"><span data-stu-id="f2915-297">Go to the location of the scripts that you downloaded and extracted in the [prerequisite step](https://docs.microsoft.com/azure/azure-stack/azure-stack-app-service-before-you-get-started#download-the-azure-app-service-on-azure-stack-installer-and-helper-scripts).</span></span>
3. <span data-ttu-id="f2915-298">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="f2915-298">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span>
4. <span data-ttu-id="f2915-299">Run the **Create-AADIdentityApp.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="f2915-299">Run the **Create-AADIdentityApp.ps1** script.</span></span> <span data-ttu-id="f2915-300">When you're prompted, enter the Azure AD tenant ID that you're using for your Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="f2915-300">When you're prompted, enter the Azure AD tenant ID that you're using for your Azure Stack deployment.</span></span> <span data-ttu-id="f2915-301">For example, enter **myazurestack.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="f2915-301">For example, enter **myazurestack.onmicrosoft.com**.</span></span>
5. <span data-ttu-id="f2915-302">In the **Credential** window, enter your Azure AD service admin account and password.</span><span class="sxs-lookup"><span data-stu-id="f2915-302">In the **Credential** window, enter your Azure AD service admin account and password.</span></span> <span data-ttu-id="f2915-303">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="f2915-303">Select **OK**.</span></span>
6. <span data-ttu-id="f2915-304">Enter the certificate file path and certificate password for the [certificate created earlier](https://docs.microsoft.com/en-gb/azure/azure-stack/azure-stack-app-service-before-you-get-started#certificates-required-for-azure-app-service-on-azure-stack).</span><span class="sxs-lookup"><span data-stu-id="f2915-304">Enter the certificate file path and certificate password for the [certificate created earlier](https://docs.microsoft.com/en-gb/azure/azure-stack/azure-stack-app-service-before-you-get-started#certificates-required-for-azure-app-service-on-azure-stack).</span></span> <span data-ttu-id="f2915-305">The certificate created for this step by default is **sso.appservice.local.azurestack.external.pfx**.</span><span class="sxs-lookup"><span data-stu-id="f2915-305">The certificate created for this step by default is **sso.appservice.local.azurestack.external.pfx**.</span></span>
7. <span data-ttu-id="f2915-306">The script creates a new application in the tenant Azure AD instance.</span><span class="sxs-lookup"><span data-stu-id="f2915-306">The script creates a new application in the tenant Azure AD instance.</span></span> <span data-ttu-id="f2915-307">Make note of the application ID that's returned in the PowerShell output.</span><span class="sxs-lookup"><span data-stu-id="f2915-307">Make note of the application ID that's returned in the PowerShell output.</span></span> <span data-ttu-id="f2915-308">You need this information during installation.</span><span class="sxs-lookup"><span data-stu-id="f2915-308">You need this information during installation.</span></span>
8. <span data-ttu-id="f2915-309">Open a new browser window, and sign in to the [Azure portal](https://portal.azure.com) as the Azure Active Directory service admin.</span><span class="sxs-lookup"><span data-stu-id="f2915-309">Open a new browser window, and sign in to the [Azure portal](https://portal.azure.com) as the Azure Active Directory service admin.</span></span>
9. <span data-ttu-id="f2915-310">Open the Azure AD resource provider.</span><span class="sxs-lookup"><span data-stu-id="f2915-310">Open the Azure AD resource provider.</span></span>
10. <span data-ttu-id="f2915-311">Select **App Registrations**.</span><span class="sxs-lookup"><span data-stu-id="f2915-311">Select **App Registrations**.</span></span>
11. <span data-ttu-id="f2915-312">Search for the application ID returned as part of step 7.</span><span class="sxs-lookup"><span data-stu-id="f2915-312">Search for the application ID returned as part of step 7.</span></span> <span data-ttu-id="f2915-313">An App Service application is listed.</span><span class="sxs-lookup"><span data-stu-id="f2915-313">An App Service application is listed.</span></span>
12. <span data-ttu-id="f2915-314">Select **Application** in the list.</span><span class="sxs-lookup"><span data-stu-id="f2915-314">Select **Application** in the list.</span></span>
13. <span data-ttu-id="f2915-315">Select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="f2915-315">Select **Settings**.</span></span>
14. <span data-ttu-id="f2915-316">Select **Required Permissions** > **Grant Permissions** > **Yes**.</span><span class="sxs-lookup"><span data-stu-id="f2915-316">Select **Required Permissions** > **Grant Permissions** > **Yes**.</span></span>

```PowerShell
    Create-AADIdentityApp.ps1
```

| <span data-ttu-id="f2915-317">Parameter</span><span class="sxs-lookup"><span data-stu-id="f2915-317">Parameter</span></span> | <span data-ttu-id="f2915-318">Required or optional</span><span class="sxs-lookup"><span data-stu-id="f2915-318">Required or optional</span></span> | <span data-ttu-id="f2915-319">Default value</span><span class="sxs-lookup"><span data-stu-id="f2915-319">Default value</span></span> | <span data-ttu-id="f2915-320">Description</span><span class="sxs-lookup"><span data-stu-id="f2915-320">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f2915-321">DirectoryTenantName</span><span class="sxs-lookup"><span data-stu-id="f2915-321">DirectoryTenantName</span></span> | <span data-ttu-id="f2915-322">Required</span><span class="sxs-lookup"><span data-stu-id="f2915-322">Required</span></span> | <span data-ttu-id="f2915-323">Null</span><span class="sxs-lookup"><span data-stu-id="f2915-323">Null</span></span> | <span data-ttu-id="f2915-324">Azure AD tenant ID.</span><span class="sxs-lookup"><span data-stu-id="f2915-324">Azure AD tenant ID.</span></span> <span data-ttu-id="f2915-325">Provide the GUID or string.</span><span class="sxs-lookup"><span data-stu-id="f2915-325">Provide the GUID or string.</span></span> <span data-ttu-id="f2915-326">An example is myazureaaddirectory.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="f2915-326">An example is myazureaaddirectory.onmicrosoft.com.</span></span> |
| <span data-ttu-id="f2915-327">AdminArmEndpoint</span><span class="sxs-lookup"><span data-stu-id="f2915-327">AdminArmEndpoint</span></span> | <span data-ttu-id="f2915-328">Required</span><span class="sxs-lookup"><span data-stu-id="f2915-328">Required</span></span> | <span data-ttu-id="f2915-329">Null</span><span class="sxs-lookup"><span data-stu-id="f2915-329">Null</span></span> | <span data-ttu-id="f2915-330">Admin Azure Resource Manager endpoint.</span><span class="sxs-lookup"><span data-stu-id="f2915-330">Admin Azure Resource Manager endpoint.</span></span> <span data-ttu-id="f2915-331">An example is adminmanagement.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="f2915-331">An example is adminmanagement.local.azurestack.external.</span></span> |
| <span data-ttu-id="f2915-332">TenantARMEndpoint</span><span class="sxs-lookup"><span data-stu-id="f2915-332">TenantARMEndpoint</span></span> | <span data-ttu-id="f2915-333">Required</span><span class="sxs-lookup"><span data-stu-id="f2915-333">Required</span></span> | <span data-ttu-id="f2915-334">Null</span><span class="sxs-lookup"><span data-stu-id="f2915-334">Null</span></span> | <span data-ttu-id="f2915-335">Tenant Azure Resource Manager endpoint.</span><span class="sxs-lookup"><span data-stu-id="f2915-335">Tenant Azure Resource Manager endpoint.</span></span> <span data-ttu-id="f2915-336">An example is management.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="f2915-336">An example is management.local.azurestack.external.</span></span> |
| <span data-ttu-id="f2915-337">AzureStackAdminCredential</span><span class="sxs-lookup"><span data-stu-id="f2915-337">AzureStackAdminCredential</span></span> | <span data-ttu-id="f2915-338">Required</span><span class="sxs-lookup"><span data-stu-id="f2915-338">Required</span></span> | <span data-ttu-id="f2915-339">Null</span><span class="sxs-lookup"><span data-stu-id="f2915-339">Null</span></span> | <span data-ttu-id="f2915-340">Azure AD service admin credential.</span><span class="sxs-lookup"><span data-stu-id="f2915-340">Azure AD service admin credential.</span></span> |
| <span data-ttu-id="f2915-341">CertificateFilePath</span><span class="sxs-lookup"><span data-stu-id="f2915-341">CertificateFilePath</span></span> | <span data-ttu-id="f2915-342">Required</span><span class="sxs-lookup"><span data-stu-id="f2915-342">Required</span></span> | <span data-ttu-id="f2915-343">Null</span><span class="sxs-lookup"><span data-stu-id="f2915-343">Null</span></span> | <span data-ttu-id="f2915-344">**Full path** to the identity application certificate file generated earlier.</span><span class="sxs-lookup"><span data-stu-id="f2915-344">**Full path** to the identity application certificate file generated earlier.</span></span> |
| <span data-ttu-id="f2915-345">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="f2915-345">CertificatePassword</span></span> | <span data-ttu-id="f2915-346">Required</span><span class="sxs-lookup"><span data-stu-id="f2915-346">Required</span></span> | <span data-ttu-id="f2915-347">Null</span><span class="sxs-lookup"><span data-stu-id="f2915-347">Null</span></span> | <span data-ttu-id="f2915-348">Password that helps protect the certificate private key.</span><span class="sxs-lookup"><span data-stu-id="f2915-348">Password that helps protect the certificate private key.</span></span> |
| <span data-ttu-id="f2915-349">Environment</span><span class="sxs-lookup"><span data-stu-id="f2915-349">Environment</span></span> | <span data-ttu-id="f2915-350">Optional</span><span class="sxs-lookup"><span data-stu-id="f2915-350">Optional</span></span> | <span data-ttu-id="f2915-351">AzureCloud</span><span class="sxs-lookup"><span data-stu-id="f2915-351">AzureCloud</span></span> | <span data-ttu-id="f2915-352">The name of the supported Cloud Environment in which the target Azure Active Directory Graph Service is available.</span><span class="sxs-lookup"><span data-stu-id="f2915-352">The name of the supported Cloud Environment in which the target Azure Active Directory Graph Service is available.</span></span>  <span data-ttu-id="f2915-353">Allowed values: 'AzureCloud', 'AzureChinaCloud', 'AzureUSGovernment', 'AzureGermanCloud'.</span><span class="sxs-lookup"><span data-stu-id="f2915-353">Allowed values: 'AzureCloud', 'AzureChinaCloud', 'AzureUSGovernment', 'AzureGermanCloud'.</span></span>|

## <a name="create-an-active-directory-federation-services-application"></a><span data-ttu-id="f2915-354">Create an Active Directory Federation Services application</span><span class="sxs-lookup"><span data-stu-id="f2915-354">Create an Active Directory Federation Services application</span></span>

<span data-ttu-id="f2915-355">For Azure Stack environments secured by AD FS, you must configure an AD FS service principal to support the following operations:</span><span class="sxs-lookup"><span data-stu-id="f2915-355">For Azure Stack environments secured by AD FS, you must configure an AD FS service principal to support the following operations:</span></span>

- <span data-ttu-id="f2915-356">Virtual machine scale set integration on worker tiers.</span><span class="sxs-lookup"><span data-stu-id="f2915-356">Virtual machine scale set integration on worker tiers.</span></span>
- <span data-ttu-id="f2915-357">SSO for the Azure Functions portal and advanced developer tools.</span><span class="sxs-lookup"><span data-stu-id="f2915-357">SSO for the Azure Functions portal and advanced developer tools.</span></span>

<span data-ttu-id="f2915-358">Administrators must configure SSO to:</span><span class="sxs-lookup"><span data-stu-id="f2915-358">Administrators must configure SSO to:</span></span>

- <span data-ttu-id="f2915-359">Configure a service principal for virtual machine scale set integration on worker tiers.</span><span class="sxs-lookup"><span data-stu-id="f2915-359">Configure a service principal for virtual machine scale set integration on worker tiers.</span></span>
- <span data-ttu-id="f2915-360">Enable the advanced developer tools within App Service (Kudu).</span><span class="sxs-lookup"><span data-stu-id="f2915-360">Enable the advanced developer tools within App Service (Kudu).</span></span>
- <span data-ttu-id="f2915-361">Enable the use of the Azure Functions portal experience.</span><span class="sxs-lookup"><span data-stu-id="f2915-361">Enable the use of the Azure Functions portal experience.</span></span>

<span data-ttu-id="f2915-362">Follow these steps:</span><span class="sxs-lookup"><span data-stu-id="f2915-362">Follow these steps:</span></span>

1. <span data-ttu-id="f2915-363">Open a PowerShell instance as azurestack\AzureStackAdmin.</span><span class="sxs-lookup"><span data-stu-id="f2915-363">Open a PowerShell instance as azurestack\AzureStackAdmin.</span></span>
2. <span data-ttu-id="f2915-364">Go to the location of the scripts that you downloaded and extracted in the [prerequisite step](https://docs.microsoft.com/en-gb/azure/azure-stack/azure-stack-app-service-before-you-get-started#download-the-azure-app-service-on-azure-stack-installer-and-helper-scripts).</span><span class="sxs-lookup"><span data-stu-id="f2915-364">Go to the location of the scripts that you downloaded and extracted in the [prerequisite step](https://docs.microsoft.com/en-gb/azure/azure-stack/azure-stack-app-service-before-you-get-started#download-the-azure-app-service-on-azure-stack-installer-and-helper-scripts).</span></span>
3. <span data-ttu-id="f2915-365">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="f2915-365">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span>
4. <span data-ttu-id="f2915-366">Run the **Create-ADFSIdentityApp.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="f2915-366">Run the **Create-ADFSIdentityApp.ps1** script.</span></span>
5. <span data-ttu-id="f2915-367">In the **Credential** window, enter your AD FS cloud admin account and password.</span><span class="sxs-lookup"><span data-stu-id="f2915-367">In the **Credential** window, enter your AD FS cloud admin account and password.</span></span> <span data-ttu-id="f2915-368">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="f2915-368">Select **OK**.</span></span>
6. <span data-ttu-id="f2915-369">Provide the certificate file path and certificate password for the [certificate created earlier](https://docs.microsoft.com/en-gb/azure/azure-stack/azure-stack-app-service-before-you-get-started#certificates-required-for-azure-app-service-on-azure-stack).</span><span class="sxs-lookup"><span data-stu-id="f2915-369">Provide the certificate file path and certificate password for the [certificate created earlier](https://docs.microsoft.com/en-gb/azure/azure-stack/azure-stack-app-service-before-you-get-started#certificates-required-for-azure-app-service-on-azure-stack).</span></span> <span data-ttu-id="f2915-370">The certificate created for this step by default is **sso.appservice.local.azurestack.external.pfx**.</span><span class="sxs-lookup"><span data-stu-id="f2915-370">The certificate created for this step by default is **sso.appservice.local.azurestack.external.pfx**.</span></span>

```PowerShell
    Create-ADFSIdentityApp.ps1
```

| <span data-ttu-id="f2915-371">Parameter</span><span class="sxs-lookup"><span data-stu-id="f2915-371">Parameter</span></span> | <span data-ttu-id="f2915-372">Required or optional</span><span class="sxs-lookup"><span data-stu-id="f2915-372">Required or optional</span></span> | <span data-ttu-id="f2915-373">Default value</span><span class="sxs-lookup"><span data-stu-id="f2915-373">Default value</span></span> | <span data-ttu-id="f2915-374">Description</span><span class="sxs-lookup"><span data-stu-id="f2915-374">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f2915-375">AdminArmEndpoint</span><span class="sxs-lookup"><span data-stu-id="f2915-375">AdminArmEndpoint</span></span> | <span data-ttu-id="f2915-376">Required</span><span class="sxs-lookup"><span data-stu-id="f2915-376">Required</span></span> | <span data-ttu-id="f2915-377">Null</span><span class="sxs-lookup"><span data-stu-id="f2915-377">Null</span></span> | <span data-ttu-id="f2915-378">Admin Azure Resource Manager endpoint.</span><span class="sxs-lookup"><span data-stu-id="f2915-378">Admin Azure Resource Manager endpoint.</span></span> <span data-ttu-id="f2915-379">An example is adminmanagement.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="f2915-379">An example is adminmanagement.local.azurestack.external.</span></span> |
| <span data-ttu-id="f2915-380">PrivilegedEndpoint</span><span class="sxs-lookup"><span data-stu-id="f2915-380">PrivilegedEndpoint</span></span> | <span data-ttu-id="f2915-381">Required</span><span class="sxs-lookup"><span data-stu-id="f2915-381">Required</span></span> | <span data-ttu-id="f2915-382">Null</span><span class="sxs-lookup"><span data-stu-id="f2915-382">Null</span></span> | <span data-ttu-id="f2915-383">Privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="f2915-383">Privileged endpoint.</span></span> <span data-ttu-id="f2915-384">An example is AzS-ERCS01.</span><span class="sxs-lookup"><span data-stu-id="f2915-384">An example is AzS-ERCS01.</span></span> |
| <span data-ttu-id="f2915-385">CloudAdminCredential</span><span class="sxs-lookup"><span data-stu-id="f2915-385">CloudAdminCredential</span></span> | <span data-ttu-id="f2915-386">Required</span><span class="sxs-lookup"><span data-stu-id="f2915-386">Required</span></span> | <span data-ttu-id="f2915-387">Null</span><span class="sxs-lookup"><span data-stu-id="f2915-387">Null</span></span> | <span data-ttu-id="f2915-388">Domain account credential for Azure Stack cloud admins.</span><span class="sxs-lookup"><span data-stu-id="f2915-388">Domain account credential for Azure Stack cloud admins.</span></span> <span data-ttu-id="f2915-389">An example is Azurestack\CloudAdmin.</span><span class="sxs-lookup"><span data-stu-id="f2915-389">An example is Azurestack\CloudAdmin.</span></span> |
| <span data-ttu-id="f2915-390">CertificateFilePath</span><span class="sxs-lookup"><span data-stu-id="f2915-390">CertificateFilePath</span></span> | <span data-ttu-id="f2915-391">Required</span><span class="sxs-lookup"><span data-stu-id="f2915-391">Required</span></span> | <span data-ttu-id="f2915-392">Null</span><span class="sxs-lookup"><span data-stu-id="f2915-392">Null</span></span> | <span data-ttu-id="f2915-393">**Full path** to the identity application's certificate PFX file.</span><span class="sxs-lookup"><span data-stu-id="f2915-393">**Full path** to the identity application's certificate PFX file.</span></span> |
| <span data-ttu-id="f2915-394">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="f2915-394">CertificatePassword</span></span> | <span data-ttu-id="f2915-395">Required</span><span class="sxs-lookup"><span data-stu-id="f2915-395">Required</span></span> | <span data-ttu-id="f2915-396">Null</span><span class="sxs-lookup"><span data-stu-id="f2915-396">Null</span></span> | <span data-ttu-id="f2915-397">Password that helps protect the certificate private key.</span><span class="sxs-lookup"><span data-stu-id="f2915-397">Password that helps protect the certificate private key.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f2915-398">Next steps</span><span class="sxs-lookup"><span data-stu-id="f2915-398">Next steps</span></span>

[<span data-ttu-id="f2915-399">Install the App Service resource provider</span><span class="sxs-lookup"><span data-stu-id="f2915-399">Install the App Service resource provider</span></span>](azure-stack-app-service-deploy.md)
