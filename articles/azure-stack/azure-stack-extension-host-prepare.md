---
title: Prepare for extension host for Azure Stack | Microsoft Docs
description: Learn to prepare for extension host, which is automatically enabled via a future Azure Stack Update package.
services: azure-stack
keywords: ''
author: mattbriggs
ms.author: mabrigg
ms.date: 09/05/2018
ms.topic: article
ms.service: azure-stack
ms.reviewer: thoroet
manager: femila
ms.openlocfilehash: 02ff83b41af47492a67bea94c5e5deecec42d15e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869675"
---
# <a name="prepare-for-extension-host-for-azure-stack"></a><span data-ttu-id="298eb-103">Prepare for extension host for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="298eb-103">Prepare for extension host for Azure Stack</span></span>

<span data-ttu-id="298eb-104">The Extension host secures Azure Stack by reducing the number of required TCP/IP ports.</span><span class="sxs-lookup"><span data-stu-id="298eb-104">The Extension host secures Azure Stack by reducing the number of required TCP/IP ports.</span></span> <span data-ttu-id="298eb-105">This article looks at preparing Azure Stack for the extension host, which is automatically enabled through an Azure Stack Update package after the 1808 update.</span><span class="sxs-lookup"><span data-stu-id="298eb-105">This article looks at preparing Azure Stack for the extension host, which is automatically enabled through an Azure Stack Update package after the 1808 update.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="298eb-106">Certificate requirements</span><span class="sxs-lookup"><span data-stu-id="298eb-106">Certificate requirements</span></span>

<span data-ttu-id="298eb-107">The extension host implements two new domains namespaces to guarantee unique host entries for each portal extension.</span><span class="sxs-lookup"><span data-stu-id="298eb-107">The extension host implements two new domains namespaces to guarantee unique host entries for each portal extension.</span></span> <span data-ttu-id="298eb-108">The new domain namespaces require two additional wild-card certificates to ensure secure communication.</span><span class="sxs-lookup"><span data-stu-id="298eb-108">The new domain namespaces require two additional wild-card certificates to ensure secure communication.</span></span>

<span data-ttu-id="298eb-109">The table shows the new namespaces and the associated certificates:</span><span class="sxs-lookup"><span data-stu-id="298eb-109">The table shows the new namespaces and the associated certificates:</span></span>

| <span data-ttu-id="298eb-110">Deployment Folder</span><span class="sxs-lookup"><span data-stu-id="298eb-110">Deployment Folder</span></span> | <span data-ttu-id="298eb-111">Required certificate subject and subject alternative names (SAN)</span><span class="sxs-lookup"><span data-stu-id="298eb-111">Required certificate subject and subject alternative names (SAN)</span></span> | <span data-ttu-id="298eb-112">Scope (per region)</span><span class="sxs-lookup"><span data-stu-id="298eb-112">Scope (per region)</span></span> | <span data-ttu-id="298eb-113">SubDomain namespace</span><span class="sxs-lookup"><span data-stu-id="298eb-113">SubDomain namespace</span></span> |
|-----------------------|------------------------------------------------------------------|-----------------------|------------------------------|
| <span data-ttu-id="298eb-114">Admin extension host</span><span class="sxs-lookup"><span data-stu-id="298eb-114">Admin extension host</span></span> | <span data-ttu-id="298eb-115">\*.adminhosting.\<region>.\<fqdn> (Wildcard SSL Certificates)</span><span class="sxs-lookup"><span data-stu-id="298eb-115">\*.adminhosting.\<region>.\<fqdn> (Wildcard SSL Certificates)</span></span> | <span data-ttu-id="298eb-116">Admin extension host</span><span class="sxs-lookup"><span data-stu-id="298eb-116">Admin extension host</span></span> | <span data-ttu-id="298eb-117">adminhosting.\<region>.\<fqdn></span><span class="sxs-lookup"><span data-stu-id="298eb-117">adminhosting.\<region>.\<fqdn></span></span> |
| <span data-ttu-id="298eb-118">Public extension host</span><span class="sxs-lookup"><span data-stu-id="298eb-118">Public extension host</span></span> | <span data-ttu-id="298eb-119">\*.hosting.\<region>.\<fqdn> (Wildcard SSL Certificates)</span><span class="sxs-lookup"><span data-stu-id="298eb-119">\*.hosting.\<region>.\<fqdn> (Wildcard SSL Certificates)</span></span> | <span data-ttu-id="298eb-120">Public extension host</span><span class="sxs-lookup"><span data-stu-id="298eb-120">Public extension host</span></span> | <span data-ttu-id="298eb-121">hosting.\<region>.\<fqdn></span><span class="sxs-lookup"><span data-stu-id="298eb-121">hosting.\<region>.\<fqdn></span></span> |

<span data-ttu-id="298eb-122">The detailed certificate requirements can be found in the [Azure Stack public key infrastructure certificate requirements](azure-stack-pki-certs.md) article.</span><span class="sxs-lookup"><span data-stu-id="298eb-122">The detailed certificate requirements can be found in the [Azure Stack public key infrastructure certificate requirements](azure-stack-pki-certs.md) article.</span></span>

## <a name="create-certificate-signing-request"></a><span data-ttu-id="298eb-123">Create certificate signing request</span><span class="sxs-lookup"><span data-stu-id="298eb-123">Create certificate signing request</span></span>

<span data-ttu-id="298eb-124">The Azure Stack Readiness Checker Tool provides the ability to create a certificate signing request for the two new, required SSL certificates.</span><span class="sxs-lookup"><span data-stu-id="298eb-124">The Azure Stack Readiness Checker Tool provides the ability to create a certificate signing request for the two new, required SSL certificates.</span></span> <span data-ttu-id="298eb-125">Follow the steps in the article [Azure Stack certificates signing request generation](azure-stack-get-pki-certs.md).</span><span class="sxs-lookup"><span data-stu-id="298eb-125">Follow the steps in the article [Azure Stack certificates signing request generation](azure-stack-get-pki-certs.md).</span></span>

> [!Note]  
> <span data-ttu-id="298eb-126">You may skip this step depending on how you requested your SSL certificates.</span><span class="sxs-lookup"><span data-stu-id="298eb-126">You may skip this step depending on how you requested your SSL certificates.</span></span>

## <a name="validate-new-certificates"></a><span data-ttu-id="298eb-127">Validate new certificates</span><span class="sxs-lookup"><span data-stu-id="298eb-127">Validate new certificates</span></span>

1. <span data-ttu-id="298eb-128">Open PowerShell with elevated permission on the hardware lifecycle host or the Azure Stack management workstation.</span><span class="sxs-lookup"><span data-stu-id="298eb-128">Open PowerShell with elevated permission on the hardware lifecycle host or the Azure Stack management workstation.</span></span>
2. <span data-ttu-id="298eb-129">Run the following cmdlet to install the Azure Stack Readiness Checker tool.</span><span class="sxs-lookup"><span data-stu-id="298eb-129">Run the following cmdlet to install the Azure Stack Readiness Checker tool.</span></span>

    ```PowerShell  
    Install-Module -Name Microsoft.AzureStack.ReadinessChecker
    ```

3. <span data-ttu-id="298eb-130">Run the following script to create the required folder structure:</span><span class="sxs-lookup"><span data-stu-id="298eb-130">Run the following script to create the required folder structure:</span></span>

    ```PowerShell  
    New-Item C:\Certificates -ItemType Directory

    $directories = 'ACSBlob','ACSQueue','ACSTable','Admin Portal','ARM Admin','ARM Public','KeyVault','KeyVaultInternal','Public Portal', 'Admin extension host', 'Public extension host'

    $destination = 'c:\certificates'

    $directories | % { New-Item -Path (Join-Path $destination $PSITEM) -ItemType Directory -Force}
    ```

    > [!Note]  
    > <span data-ttu-id="298eb-131">If you deploy with Azure Active Directory Federated Services (AD FS) the following directories must be added to **$directories** in the script: `ADFS`, `Graph`.</span><span class="sxs-lookup"><span data-stu-id="298eb-131">If you deploy with Azure Active Directory Federated Services (AD FS) the following directories must be added to **$directories** in the script: `ADFS`, `Graph`.</span></span>

4. <span data-ttu-id="298eb-132">Run the following cmdlets to start the certificate check:</span><span class="sxs-lookup"><span data-stu-id="298eb-132">Run the following cmdlets to start the certificate check:</span></span>

    ```PowerShell  
    $pfxPassword = Read-Host -Prompt "Enter PFX Password" -AsSecureString 

    Start-AzsReadinessChecker -CertificatePath c:\certificates -pfxPassword $pfxPassword -RegionName east -FQDN azurestack.contoso.com -IdentitySystem AAD -ExtensionHostFeature $true
    ```

5. <span data-ttu-id="298eb-133">Place your certificate(s) in the appropriate directories.</span><span class="sxs-lookup"><span data-stu-id="298eb-133">Place your certificate(s) in the appropriate directories.</span></span>

6. <span data-ttu-id="298eb-134">Check the output and all certificates pass all tests.</span><span class="sxs-lookup"><span data-stu-id="298eb-134">Check the output and all certificates pass all tests.</span></span>


## <a name="import-extension-host-certificates"></a><span data-ttu-id="298eb-135">Import extension host certificates</span><span class="sxs-lookup"><span data-stu-id="298eb-135">Import extension host certificates</span></span>

<span data-ttu-id="298eb-136">Use a computer that can connect to the Azure Stack privileged endpoint for the next steps.</span><span class="sxs-lookup"><span data-stu-id="298eb-136">Use a computer that can connect to the Azure Stack privileged endpoint for the next steps.</span></span> <span data-ttu-id="298eb-137">Make sure you have access to the new certificate files from that computer.</span><span class="sxs-lookup"><span data-stu-id="298eb-137">Make sure you have access to the new certificate files from that computer.</span></span>

1. <span data-ttu-id="298eb-138">Use a computer that can connect to the Azure Stack privileged endpoint for the next steps.</span><span class="sxs-lookup"><span data-stu-id="298eb-138">Use a computer that can connect to the Azure Stack privileged endpoint for the next steps.</span></span> <span data-ttu-id="298eb-139">Make sure you access to the new certificate files from that computer.</span><span class="sxs-lookup"><span data-stu-id="298eb-139">Make sure you access to the new certificate files from that computer.</span></span>
2. <span data-ttu-id="298eb-140">Open PowerShell ISE to execute the next script blocks</span><span class="sxs-lookup"><span data-stu-id="298eb-140">Open PowerShell ISE to execute the next script blocks</span></span>
3. <span data-ttu-id="298eb-141">Import the certificate for hosting endpoint.</span><span class="sxs-lookup"><span data-stu-id="298eb-141">Import the certificate for hosting endpoint.</span></span> <span data-ttu-id="298eb-142">Adjust the script to match your environment.</span><span class="sxs-lookup"><span data-stu-id="298eb-142">Adjust the script to match your environment.</span></span>
4. <span data-ttu-id="298eb-143">Import the certificate for the Admin hosting endpoint.</span><span class="sxs-lookup"><span data-stu-id="298eb-143">Import the certificate for the Admin hosting endpoint.</span></span>

    ```PowerShell  

    $CertPassword = read-host -AsSecureString -prompt "Certificate Password"

    $CloudAdminCred = Get-Credential -UserName <Privileged endpoint credentials> -Message "Enter the cloud domain credentials to access the privileged endpoint."

    [Byte[]] $AdminHostingCertContent = [Byte[]](Get-Content c:\certificate\myadminhostingcertificate.pfx -Encoding Byte)

    Invoke-Command -ComputeName <PrivilegedEndpoint computer name> `
    -Credential $CloudAdminCred `
    -ConfigurationName "PrivilegedEndpoint" `
    -ArgumentList @($AdminHostingCertContent, $CertPassword) `
    -ScriptBlock {
            param($AdminHostingCertContent, $CertPassword)
            Import-AdminHostingServiceCert $AdminHostingCertContent $certPassword
    }
    ```
5. <span data-ttu-id="298eb-144">Import the certificate for the hosting endpoint.</span><span class="sxs-lookup"><span data-stu-id="298eb-144">Import the certificate for the hosting endpoint.</span></span>
    ```PowerShell  
    $CertPassword = read-host -AsSecureString -prompt "Certificate Password"

    $CloudAdminCred = Get-Credential -UserName <Privileged endpoint credentials> -Message "Enter the cloud domain credentials to access the privileged endpoint."

    [Byte[]] $HostingCertContent = [Byte[]](Get-Content c:\certificate\myhostingcertificate.pfx  -Encoding Byte)

    Invoke-Command -ComputeName <PrivilegedEndpoint computer name> `
    -Credential $CloudAdminCred `
    -ConfigurationName "PrivilegedEndpoint" `
    -ArgumentList @($HostingCertContent, $CertPassword) `
    -ScriptBlock {
            param($HostingCertContent, $CertPassword)
            Import-UserHostingServiceCert $HostingCertContent $certPassword
    }
    ```



### <a name="update-dns-configuration"></a><span data-ttu-id="298eb-145">Update DNS configuration</span><span class="sxs-lookup"><span data-stu-id="298eb-145">Update DNS configuration</span></span>

> [!Note]  
> <span data-ttu-id="298eb-146">This step is not required if you used DNS Zone delegation for DNS Integration.</span><span class="sxs-lookup"><span data-stu-id="298eb-146">This step is not required if you used DNS Zone delegation for DNS Integration.</span></span>
<span data-ttu-id="298eb-147">If individual host A records have been configured to publish Azure Stack endpoints, you need to create two additional host A records:</span><span class="sxs-lookup"><span data-stu-id="298eb-147">If individual host A records have been configured to publish Azure Stack endpoints, you need to create two additional host A records:</span></span>

| <span data-ttu-id="298eb-148">IP</span><span class="sxs-lookup"><span data-stu-id="298eb-148">IP</span></span> | <span data-ttu-id="298eb-149">Hostname</span><span class="sxs-lookup"><span data-stu-id="298eb-149">Hostname</span></span> | <span data-ttu-id="298eb-150">Type</span><span class="sxs-lookup"><span data-stu-id="298eb-150">Type</span></span> |
|----|------------------------------|------|
| <span data-ttu-id="298eb-151">\<IP></span><span class="sxs-lookup"><span data-stu-id="298eb-151">\<IP></span></span> | <span data-ttu-id="298eb-152">Adminhosting.<Region>.<FQDN></span><span class="sxs-lookup"><span data-stu-id="298eb-152">Adminhosting.<Region>.<FQDN></span></span> | <span data-ttu-id="298eb-153">A</span><span class="sxs-lookup"><span data-stu-id="298eb-153">A</span></span> |
| <span data-ttu-id="298eb-154">\<IP></span><span class="sxs-lookup"><span data-stu-id="298eb-154">\<IP></span></span> | <span data-ttu-id="298eb-155">Hosting.<Region>.<FQDN></span><span class="sxs-lookup"><span data-stu-id="298eb-155">Hosting.<Region>.<FQDN></span></span> | <span data-ttu-id="298eb-156">A</span><span class="sxs-lookup"><span data-stu-id="298eb-156">A</span></span> |

<span data-ttu-id="298eb-157">Allocated IPs can be retrieved using privileged endpoint by running the cmdlet **Get-AzureStackStampInformation**.</span><span class="sxs-lookup"><span data-stu-id="298eb-157">Allocated IPs can be retrieved using privileged endpoint by running the cmdlet **Get-AzureStackStampInformation**.</span></span>

### <a name="ports-and-protocols"></a><span data-ttu-id="298eb-158">Ports and protocols</span><span class="sxs-lookup"><span data-stu-id="298eb-158">Ports and protocols</span></span>

<span data-ttu-id="298eb-159">The article, [Azure Stack datacenter integration - Publish endpoints](azure-stack-integrate-endpoints.md), covers the ports and protocols that require inbound communication to publish Azure Stack before the extension host rollout.</span><span class="sxs-lookup"><span data-stu-id="298eb-159">The article, [Azure Stack datacenter integration - Publish endpoints](azure-stack-integrate-endpoints.md), covers the ports and protocols that require inbound communication to publish Azure Stack before the extension host rollout.</span></span>

### <a name="publish-new-endpoints"></a><span data-ttu-id="298eb-160">Publish new endpoints</span><span class="sxs-lookup"><span data-stu-id="298eb-160">Publish new endpoints</span></span>

<span data-ttu-id="298eb-161">There are two new endpoints required to be published through your firewall.</span><span class="sxs-lookup"><span data-stu-id="298eb-161">There are two new endpoints required to be published through your firewall.</span></span> <span data-ttu-id="298eb-162">The allocated IPs from the public VIP pool can be retrieved using the cmdlet **Get-AzureStackStampInformation**.</span><span class="sxs-lookup"><span data-stu-id="298eb-162">The allocated IPs from the public VIP pool can be retrieved using the cmdlet **Get-AzureStackStampInformation**.</span></span>

> [!Note]  
> <span data-ttu-id="298eb-163">Make this change before enabling the extension host.</span><span class="sxs-lookup"><span data-stu-id="298eb-163">Make this change before enabling the extension host.</span></span> <span data-ttu-id="298eb-164">This allows the Azure Stack portals to be continuously accessible.</span><span class="sxs-lookup"><span data-stu-id="298eb-164">This allows the Azure Stack portals to be continuously accessible.</span></span>

| <span data-ttu-id="298eb-165">Endpoint (VIP)</span><span class="sxs-lookup"><span data-stu-id="298eb-165">Endpoint (VIP)</span></span> | <span data-ttu-id="298eb-166">Protocol</span><span class="sxs-lookup"><span data-stu-id="298eb-166">Protocol</span></span> | <span data-ttu-id="298eb-167">Ports</span><span class="sxs-lookup"><span data-stu-id="298eb-167">Ports</span></span> |
|----------------|----------|-------|
| <span data-ttu-id="298eb-168">AdminHosting</span><span class="sxs-lookup"><span data-stu-id="298eb-168">AdminHosting</span></span> | <span data-ttu-id="298eb-169">HTTPS</span><span class="sxs-lookup"><span data-stu-id="298eb-169">HTTPS</span></span> | <span data-ttu-id="298eb-170">443</span><span class="sxs-lookup"><span data-stu-id="298eb-170">443</span></span> |
| <span data-ttu-id="298eb-171">Hosting</span><span class="sxs-lookup"><span data-stu-id="298eb-171">Hosting</span></span> | <span data-ttu-id="298eb-172">HTTPS</span><span class="sxs-lookup"><span data-stu-id="298eb-172">HTTPS</span></span> | <span data-ttu-id="298eb-173">443</span><span class="sxs-lookup"><span data-stu-id="298eb-173">443</span></span> |

### <a name="update-existing-publishing-rules-post-enablement-of-extension-host"></a><span data-ttu-id="298eb-174">Update existing publishing Rules (Post enablement of extension host)</span><span class="sxs-lookup"><span data-stu-id="298eb-174">Update existing publishing Rules (Post enablement of extension host)</span></span>

> [!Note]  
> <span data-ttu-id="298eb-175">The 1808 Azure Stack Update Package does **not** enable extension host yet.</span><span class="sxs-lookup"><span data-stu-id="298eb-175">The 1808 Azure Stack Update Package does **not** enable extension host yet.</span></span> <span data-ttu-id="298eb-176">It allows to prepare for extension host by importing the required certificates.</span><span class="sxs-lookup"><span data-stu-id="298eb-176">It allows to prepare for extension host by importing the required certificates.</span></span> <span data-ttu-id="298eb-177">Do not close any ports before extension host is automatically enabled through an Azure Stack Update package after the 1808 update.</span><span class="sxs-lookup"><span data-stu-id="298eb-177">Do not close any ports before extension host is automatically enabled through an Azure Stack Update package after the 1808 update.</span></span>

<span data-ttu-id="298eb-178">The following existing endpoint ports must be closed in your existing firewall rules.</span><span class="sxs-lookup"><span data-stu-id="298eb-178">The following existing endpoint ports must be closed in your existing firewall rules.</span></span>

> [!Note]  
> <span data-ttu-id="298eb-179">It is recommended to close those ports after successful validation.</span><span class="sxs-lookup"><span data-stu-id="298eb-179">It is recommended to close those ports after successful validation.</span></span>

| <span data-ttu-id="298eb-180">Endpoint (VIP)</span><span class="sxs-lookup"><span data-stu-id="298eb-180">Endpoint (VIP)</span></span> | <span data-ttu-id="298eb-181">Protocol</span><span class="sxs-lookup"><span data-stu-id="298eb-181">Protocol</span></span> | <span data-ttu-id="298eb-182">Ports</span><span class="sxs-lookup"><span data-stu-id="298eb-182">Ports</span></span> |
|----------------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="298eb-183">Portal (administrator)</span><span class="sxs-lookup"><span data-stu-id="298eb-183">Portal (administrator)</span></span> | <span data-ttu-id="298eb-184">HTTPS</span><span class="sxs-lookup"><span data-stu-id="298eb-184">HTTPS</span></span> | <span data-ttu-id="298eb-185">12495</span><span class="sxs-lookup"><span data-stu-id="298eb-185">12495</span></span><br><span data-ttu-id="298eb-186">12499</span><span class="sxs-lookup"><span data-stu-id="298eb-186">12499</span></span><br><span data-ttu-id="298eb-187">12646</span><span class="sxs-lookup"><span data-stu-id="298eb-187">12646</span></span><br><span data-ttu-id="298eb-188">12647</span><span class="sxs-lookup"><span data-stu-id="298eb-188">12647</span></span><br><span data-ttu-id="298eb-189">12648</span><span class="sxs-lookup"><span data-stu-id="298eb-189">12648</span></span><br><span data-ttu-id="298eb-190">12649</span><span class="sxs-lookup"><span data-stu-id="298eb-190">12649</span></span><br><span data-ttu-id="298eb-191">12650</span><span class="sxs-lookup"><span data-stu-id="298eb-191">12650</span></span><br><span data-ttu-id="298eb-192">13001</span><span class="sxs-lookup"><span data-stu-id="298eb-192">13001</span></span><br><span data-ttu-id="298eb-193">13003</span><span class="sxs-lookup"><span data-stu-id="298eb-193">13003</span></span><br><span data-ttu-id="298eb-194">13010</span><span class="sxs-lookup"><span data-stu-id="298eb-194">13010</span></span><br><span data-ttu-id="298eb-195">13011</span><span class="sxs-lookup"><span data-stu-id="298eb-195">13011</span></span><br><span data-ttu-id="298eb-196">13020</span><span class="sxs-lookup"><span data-stu-id="298eb-196">13020</span></span><br><span data-ttu-id="298eb-197">13021</span><span class="sxs-lookup"><span data-stu-id="298eb-197">13021</span></span><br><span data-ttu-id="298eb-198">13026</span><span class="sxs-lookup"><span data-stu-id="298eb-198">13026</span></span><br><span data-ttu-id="298eb-199">30015</span><span class="sxs-lookup"><span data-stu-id="298eb-199">30015</span></span> |
| <span data-ttu-id="298eb-200">Portal (user)</span><span class="sxs-lookup"><span data-stu-id="298eb-200">Portal (user)</span></span> | <span data-ttu-id="298eb-201">HTTPS</span><span class="sxs-lookup"><span data-stu-id="298eb-201">HTTPS</span></span> | <span data-ttu-id="298eb-202">12495</span><span class="sxs-lookup"><span data-stu-id="298eb-202">12495</span></span><br><span data-ttu-id="298eb-203">12649</span><span class="sxs-lookup"><span data-stu-id="298eb-203">12649</span></span><br><span data-ttu-id="298eb-204">13001</span><span class="sxs-lookup"><span data-stu-id="298eb-204">13001</span></span><br><span data-ttu-id="298eb-205">13010</span><span class="sxs-lookup"><span data-stu-id="298eb-205">13010</span></span><br><span data-ttu-id="298eb-206">13011</span><span class="sxs-lookup"><span data-stu-id="298eb-206">13011</span></span><br><span data-ttu-id="298eb-207">13020</span><span class="sxs-lookup"><span data-stu-id="298eb-207">13020</span></span><br><span data-ttu-id="298eb-208">13021</span><span class="sxs-lookup"><span data-stu-id="298eb-208">13021</span></span><br><span data-ttu-id="298eb-209">30015</span><span class="sxs-lookup"><span data-stu-id="298eb-209">30015</span></span><br><span data-ttu-id="298eb-210">13003</span><span class="sxs-lookup"><span data-stu-id="298eb-210">13003</span></span> |
| <span data-ttu-id="298eb-211">Azure Resource Manager (administrator)</span><span class="sxs-lookup"><span data-stu-id="298eb-211">Azure Resource Manager (administrator)</span></span> | <span data-ttu-id="298eb-212">HTTPS</span><span class="sxs-lookup"><span data-stu-id="298eb-212">HTTPS</span></span> | <span data-ttu-id="298eb-213">30024</span><span class="sxs-lookup"><span data-stu-id="298eb-213">30024</span></span> |
| <span data-ttu-id="298eb-214">Azure Resource Manager (user)</span><span class="sxs-lookup"><span data-stu-id="298eb-214">Azure Resource Manager (user)</span></span> | <span data-ttu-id="298eb-215">HTTPS</span><span class="sxs-lookup"><span data-stu-id="298eb-215">HTTPS</span></span> | <span data-ttu-id="298eb-216">30024</span><span class="sxs-lookup"><span data-stu-id="298eb-216">30024</span></span> |

## <a name="next-steps"></a><span data-ttu-id="298eb-217">Next steps</span><span class="sxs-lookup"><span data-stu-id="298eb-217">Next steps</span></span>

- <span data-ttu-id="298eb-218">Learn about [Firewall integration](azure-stack-firewall.md).</span><span class="sxs-lookup"><span data-stu-id="298eb-218">Learn about [Firewall integration](azure-stack-firewall.md).</span></span>
- <span data-ttu-id="298eb-219">Learn about [Azure Stack certificates signing request generation](azure-stack-get-pki-certs.md)</span><span class="sxs-lookup"><span data-stu-id="298eb-219">Learn about [Azure Stack certificates signing request generation](azure-stack-get-pki-certs.md)</span></span>
