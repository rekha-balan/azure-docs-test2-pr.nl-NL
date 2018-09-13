---
title: Rotate secrets in Azure Stack | Microsoft Docs
description: Learn how to rotate your secrets in Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2018
ms.author: mabrigg
ms.reviewer: ppacent
ms.openlocfilehash: dacfa738a99eb2d580d825957d09b2b1a3111e93
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857405"
---
# <a name="rotate-secrets-in-azure-stack"></a><span data-ttu-id="6d351-103">Rotate secrets in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="6d351-103">Rotate secrets in Azure Stack</span></span>

<span data-ttu-id="6d351-104">*These instructions apply only to Azure Stack Integrated Systems Version 1803 and Later. Do not attempt secret rotation on pre-1802 Azure Stack Versions*</span><span class="sxs-lookup"><span data-stu-id="6d351-104">*These instructions apply only to Azure Stack Integrated Systems Version 1803 and Later. Do not attempt secret rotation on pre-1802 Azure Stack Versions*</span></span>

<span data-ttu-id="6d351-105">Azure Stack uses various secrets to maintain secure communication between the Azure Stack infrastructure resources and services.</span><span class="sxs-lookup"><span data-stu-id="6d351-105">Azure Stack uses various secrets to maintain secure communication between the Azure Stack infrastructure resources and services.</span></span>

- <span data-ttu-id="6d351-106">**Internal secrets**</span><span class="sxs-lookup"><span data-stu-id="6d351-106">**Internal secrets**</span></span>  
<span data-ttu-id="6d351-107">All the certificates, passwords, secure strings, and keys used by the Azure Stack infrastructure without intervention of the Azure Stack Operator.</span><span class="sxs-lookup"><span data-stu-id="6d351-107">All the certificates, passwords, secure strings, and keys used by the Azure Stack infrastructure without intervention of the Azure Stack Operator.</span></span> 

- <span data-ttu-id="6d351-108">**External secrets**</span><span class="sxs-lookup"><span data-stu-id="6d351-108">**External secrets**</span></span>  
<span data-ttu-id="6d351-109">Infrastructure service certificates for external-facing services that are provided by the Azure Stack Operator.</span><span class="sxs-lookup"><span data-stu-id="6d351-109">Infrastructure service certificates for external-facing services that are provided by the Azure Stack Operator.</span></span> <span data-ttu-id="6d351-110">This includes the certificates for the following services:</span><span class="sxs-lookup"><span data-stu-id="6d351-110">This includes the certificates for the following services:</span></span> 
    - <span data-ttu-id="6d351-111">Administrator Portal</span><span class="sxs-lookup"><span data-stu-id="6d351-111">Administrator Portal</span></span> 
    - <span data-ttu-id="6d351-112">Public Portal</span><span class="sxs-lookup"><span data-stu-id="6d351-112">Public Portal</span></span> 
    - <span data-ttu-id="6d351-113">Administrator Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6d351-113">Administrator Azure Resource Manager</span></span> 
    - <span data-ttu-id="6d351-114">Global Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6d351-114">Global Azure Resource Manager</span></span> 
    - <span data-ttu-id="6d351-115">Administrator Keyvault</span><span class="sxs-lookup"><span data-stu-id="6d351-115">Administrator Keyvault</span></span> 
    - <span data-ttu-id="6d351-116">Keyvault</span><span class="sxs-lookup"><span data-stu-id="6d351-116">Keyvault</span></span> 
    - <span data-ttu-id="6d351-117">ACS (including blob, table, and queue storage)</span><span class="sxs-lookup"><span data-stu-id="6d351-117">ACS (including blob, table, and queue storage)</span></span> 
    - <span data-ttu-id="6d351-118">ADFS<sup>\*</sup></span><span class="sxs-lookup"><span data-stu-id="6d351-118">ADFS<sup>\*</sup></span></span>
    - <span data-ttu-id="6d351-119">Graph<sup>\*</sup></span><span class="sxs-lookup"><span data-stu-id="6d351-119">Graph<sup>\*</sup></span></span>

   <span data-ttu-id="6d351-120"><sup>\*</sup> Only applicable if the environment’s identity provider is Active Directory Federated Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="6d351-120"><sup>\*</sup> Only applicable if the environment’s identity provider is Active Directory Federated Services (AD FS).</span></span>

> [!NOTE]
> <span data-ttu-id="6d351-121">All other secure keys and strings, including BMC and switch passwords, user and administrator account passwords are still manually updated by the administrator.</span><span class="sxs-lookup"><span data-stu-id="6d351-121">All other secure keys and strings, including BMC and switch passwords, user and administrator account passwords are still manually updated by the administrator.</span></span> 

<span data-ttu-id="6d351-122">In order to maintain the integrity of the Azure Stack infrastructure, operators need the ability to periodically rotate their infrastructure’s secrets at frequencies that are consistent with their organization’s security requirements.</span><span class="sxs-lookup"><span data-stu-id="6d351-122">In order to maintain the integrity of the Azure Stack infrastructure, operators need the ability to periodically rotate their infrastructure’s secrets at frequencies that are consistent with their organization’s security requirements.</span></span>

### <a name="rotating-secrets-with-external-certificates-from-a-new-certificate-authority"></a><span data-ttu-id="6d351-123">Rotating Secrets with External Certificates from a new Certificate Authority</span><span class="sxs-lookup"><span data-stu-id="6d351-123">Rotating Secrets with External Certificates from a new Certificate Authority</span></span>

<span data-ttu-id="6d351-124">Azure Stack supports secret rotation with external certificates from a new Certificate Authority (CA) in the following contexts:</span><span class="sxs-lookup"><span data-stu-id="6d351-124">Azure Stack supports secret rotation with external certificates from a new Certificate Authority (CA) in the following contexts:</span></span>

|<span data-ttu-id="6d351-125">Installed Certificate CA</span><span class="sxs-lookup"><span data-stu-id="6d351-125">Installed Certificate CA</span></span>|<span data-ttu-id="6d351-126">CA to Rotate To</span><span class="sxs-lookup"><span data-stu-id="6d351-126">CA to Rotate To</span></span>|<span data-ttu-id="6d351-127">Supported</span><span class="sxs-lookup"><span data-stu-id="6d351-127">Supported</span></span>|<span data-ttu-id="6d351-128">Azure Stack Versions Supported</span><span class="sxs-lookup"><span data-stu-id="6d351-128">Azure Stack Versions Supported</span></span>|
|-----|-----|-----|-----|
|<span data-ttu-id="6d351-129">From Self-Signed</span><span class="sxs-lookup"><span data-stu-id="6d351-129">From Self-Signed</span></span>|<span data-ttu-id="6d351-130">To Enterprise</span><span class="sxs-lookup"><span data-stu-id="6d351-130">To Enterprise</span></span>|<span data-ttu-id="6d351-131">Not Supported</span><span class="sxs-lookup"><span data-stu-id="6d351-131">Not Supported</span></span>||
|<span data-ttu-id="6d351-132">From Self-Signed</span><span class="sxs-lookup"><span data-stu-id="6d351-132">From Self-Signed</span></span>|<span data-ttu-id="6d351-133">To Self-Signed</span><span class="sxs-lookup"><span data-stu-id="6d351-133">To Self-Signed</span></span>|<span data-ttu-id="6d351-134">Not Supported</span><span class="sxs-lookup"><span data-stu-id="6d351-134">Not Supported</span></span>||
|<span data-ttu-id="6d351-135">From Self-Signed</span><span class="sxs-lookup"><span data-stu-id="6d351-135">From Self-Signed</span></span>|<span data-ttu-id="6d351-136">To Public<sup>\*</sup></span><span class="sxs-lookup"><span data-stu-id="6d351-136">To Public<sup>\*</sup></span></span>|<span data-ttu-id="6d351-137">Supported</span><span class="sxs-lookup"><span data-stu-id="6d351-137">Supported</span></span>|<span data-ttu-id="6d351-138">1803 & Later</span><span class="sxs-lookup"><span data-stu-id="6d351-138">1803 & Later</span></span>|
|<span data-ttu-id="6d351-139">From Enterprise</span><span class="sxs-lookup"><span data-stu-id="6d351-139">From Enterprise</span></span>|<span data-ttu-id="6d351-140">To Enterprise</span><span class="sxs-lookup"><span data-stu-id="6d351-140">To Enterprise</span></span>|<span data-ttu-id="6d351-141">Supported so long as customers use the SAME enterprise CA as used at deployment</span><span class="sxs-lookup"><span data-stu-id="6d351-141">Supported so long as customers use the SAME enterprise CA as used at deployment</span></span>|<span data-ttu-id="6d351-142">1803 & Later</span><span class="sxs-lookup"><span data-stu-id="6d351-142">1803 & Later</span></span>|
|<span data-ttu-id="6d351-143">From Enterprise</span><span class="sxs-lookup"><span data-stu-id="6d351-143">From Enterprise</span></span>|<span data-ttu-id="6d351-144">To Self-Signed</span><span class="sxs-lookup"><span data-stu-id="6d351-144">To Self-Signed</span></span>|<span data-ttu-id="6d351-145">Not Supported</span><span class="sxs-lookup"><span data-stu-id="6d351-145">Not Supported</span></span>||
|<span data-ttu-id="6d351-146">From Enterprise</span><span class="sxs-lookup"><span data-stu-id="6d351-146">From Enterprise</span></span>|<span data-ttu-id="6d351-147">To Public<sup>\*</sup></span><span class="sxs-lookup"><span data-stu-id="6d351-147">To Public<sup>\*</sup></span></span>|<span data-ttu-id="6d351-148">Supported</span><span class="sxs-lookup"><span data-stu-id="6d351-148">Supported</span></span>|<span data-ttu-id="6d351-149">1803 & Later</span><span class="sxs-lookup"><span data-stu-id="6d351-149">1803 & Later</span></span>|
|<span data-ttu-id="6d351-150">From Public<sup>\*</sup></span><span class="sxs-lookup"><span data-stu-id="6d351-150">From Public<sup>\*</sup></span></span>|<span data-ttu-id="6d351-151">To Enterprise</span><span class="sxs-lookup"><span data-stu-id="6d351-151">To Enterprise</span></span>|<span data-ttu-id="6d351-152">Not Supported</span><span class="sxs-lookup"><span data-stu-id="6d351-152">Not Supported</span></span>|<span data-ttu-id="6d351-153">1803 & Later</span><span class="sxs-lookup"><span data-stu-id="6d351-153">1803 & Later</span></span>|
|<span data-ttu-id="6d351-154">From Public<sup>\*</sup></span><span class="sxs-lookup"><span data-stu-id="6d351-154">From Public<sup>\*</sup></span></span>|<span data-ttu-id="6d351-155">To Self-Signed</span><span class="sxs-lookup"><span data-stu-id="6d351-155">To Self-Signed</span></span>|<span data-ttu-id="6d351-156">Not Supported</span><span class="sxs-lookup"><span data-stu-id="6d351-156">Not Supported</span></span>||
|<span data-ttu-id="6d351-157">From Public<sup>\*</sup></span><span class="sxs-lookup"><span data-stu-id="6d351-157">From Public<sup>\*</sup></span></span>|<span data-ttu-id="6d351-158">To Public<sup>\*</sup></span><span class="sxs-lookup"><span data-stu-id="6d351-158">To Public<sup>\*</sup></span></span>|<span data-ttu-id="6d351-159">Supported</span><span class="sxs-lookup"><span data-stu-id="6d351-159">Supported</span></span>|<span data-ttu-id="6d351-160">1803 & Later</span><span class="sxs-lookup"><span data-stu-id="6d351-160">1803 & Later</span></span>|

<span data-ttu-id="6d351-161"><sup>\*</sup> Here Public Certificate Authorities are those that are part of the Windows Trusted Root Program.</span><span class="sxs-lookup"><span data-stu-id="6d351-161"><sup>\*</sup> Here Public Certificate Authorities are those that are part of the Windows Trusted Root Program.</span></span> <span data-ttu-id="6d351-162">You can find the full list [Microsoft Trusted Root Certificate Program: Participants (as of June 27, 2017)](https://gallery.technet.microsoft.com/Trusted-Root-Certificate-123665ca).</span><span class="sxs-lookup"><span data-stu-id="6d351-162">You can find the full list [Microsoft Trusted Root Certificate Program: Participants (as of June 27, 2017)](https://gallery.technet.microsoft.com/Trusted-Root-Certificate-123665ca).</span></span>

## <a name="alert-remediation"></a><span data-ttu-id="6d351-163">Alert remediation</span><span class="sxs-lookup"><span data-stu-id="6d351-163">Alert remediation</span></span>

<span data-ttu-id="6d351-164">When secrets are within 30 days of expiration, the following alerts are generated in the Administrator Portal:</span><span class="sxs-lookup"><span data-stu-id="6d351-164">When secrets are within 30 days of expiration, the following alerts are generated in the Administrator Portal:</span></span> 

- <span data-ttu-id="6d351-165">Pending service account password expiration</span><span class="sxs-lookup"><span data-stu-id="6d351-165">Pending service account password expiration</span></span> 
- <span data-ttu-id="6d351-166">Pending internal certificate expiration</span><span class="sxs-lookup"><span data-stu-id="6d351-166">Pending internal certificate expiration</span></span> 
- <span data-ttu-id="6d351-167">Pending external certificate expiration</span><span class="sxs-lookup"><span data-stu-id="6d351-167">Pending external certificate expiration</span></span> 

<span data-ttu-id="6d351-168">Running secret rotation using the instructions below will remediate these alerts.</span><span class="sxs-lookup"><span data-stu-id="6d351-168">Running secret rotation using the instructions below will remediate these alerts.</span></span>

## <a name="pre-steps-for-secret-rotation"></a><span data-ttu-id="6d351-169">Pre-steps for secret rotation</span><span class="sxs-lookup"><span data-stu-id="6d351-169">Pre-steps for secret rotation</span></span>

   > [!IMPORTANT]  
   > <span data-ttu-id="6d351-170">Ensure secret rotation hasn't been successfully executed on your environment.</span><span class="sxs-lookup"><span data-stu-id="6d351-170">Ensure secret rotation hasn't been successfully executed on your environment.</span></span> <span data-ttu-id="6d351-171">If secret rotation has already been performed, update Azure Stack to version 1807 or later before you execute secret rotation.</span><span class="sxs-lookup"><span data-stu-id="6d351-171">If secret rotation has already been performed, update Azure Stack to version 1807 or later before you execute secret rotation.</span></span> 
1.  <span data-ttu-id="6d351-172">Notify your users of any maintenance operations.</span><span class="sxs-lookup"><span data-stu-id="6d351-172">Notify your users of any maintenance operations.</span></span> <span data-ttu-id="6d351-173">Schedule normal maintenance windows, as much as possible,  during non-business hours.</span><span class="sxs-lookup"><span data-stu-id="6d351-173">Schedule normal maintenance windows, as much as possible,  during non-business hours.</span></span> <span data-ttu-id="6d351-174">Maintenance operations may affect both user workloads and portal operations.</span><span class="sxs-lookup"><span data-stu-id="6d351-174">Maintenance operations may affect both user workloads and portal operations.</span></span>
    > [!note]  
    > <span data-ttu-id="6d351-175">The next steps only apply when rotating Azure Stack external secrets.</span><span class="sxs-lookup"><span data-stu-id="6d351-175">The next steps only apply when rotating Azure Stack external secrets.</span></span>
3. <span data-ttu-id="6d351-176">Prepare a new set of replacement external certificates.</span><span class="sxs-lookup"><span data-stu-id="6d351-176">Prepare a new set of replacement external certificates.</span></span> <span data-ttu-id="6d351-177">The new set matches the certificate specifications outlined in the [Azure Stack PKI certificate requirements](https://docs.microsoft.com/azure/azure-stack/azure-stack-pki-certs).</span><span class="sxs-lookup"><span data-stu-id="6d351-177">The new set matches the certificate specifications outlined in the [Azure Stack PKI certificate requirements](https://docs.microsoft.com/azure/azure-stack/azure-stack-pki-certs).</span></span>
4.  <span data-ttu-id="6d351-178">Store a back up to the certificates used for rotation in a secure backup location.</span><span class="sxs-lookup"><span data-stu-id="6d351-178">Store a back up to the certificates used for rotation in a secure backup location.</span></span> <span data-ttu-id="6d351-179">If your rotation runs and then fails, replace the certificates in the file share with the backup copies before you rerun the rotation.</span><span class="sxs-lookup"><span data-stu-id="6d351-179">If your rotation runs and then fails, replace the certificates in the file share with the backup copies before you rerun the rotation.</span></span> <span data-ttu-id="6d351-180">Note, keep backup copies in the secure backup location.</span><span class="sxs-lookup"><span data-stu-id="6d351-180">Note, keep backup copies in the secure backup location.</span></span>
5.  <span data-ttu-id="6d351-181">Create a fileshare you can access from the ERCS VMs.</span><span class="sxs-lookup"><span data-stu-id="6d351-181">Create a fileshare you can access from the ERCS VMs.</span></span> <span data-ttu-id="6d351-182">The file share must be  readable and writable for the **CloudAdmin** identity.</span><span class="sxs-lookup"><span data-stu-id="6d351-182">The file share must be  readable and writable for the **CloudAdmin** identity.</span></span>
6.  <span data-ttu-id="6d351-183">Open a PowerShell ISE console from a computer where you have access to the fileshare.</span><span class="sxs-lookup"><span data-stu-id="6d351-183">Open a PowerShell ISE console from a computer where you have access to the fileshare.</span></span> <span data-ttu-id="6d351-184">Navigate to your fileshare.</span><span class="sxs-lookup"><span data-stu-id="6d351-184">Navigate to your fileshare.</span></span> 
7.  <span data-ttu-id="6d351-185">Run **[CertDirectoryMaker.ps1](http://www.aka.ms/azssecretrotationhelper)** to create the required directories for your external certificates.</span><span class="sxs-lookup"><span data-stu-id="6d351-185">Run **[CertDirectoryMaker.ps1](http://www.aka.ms/azssecretrotationhelper)** to create the required directories for your external certificates.</span></span>

## <a name="rotating-external-and-internal-secrets"></a><span data-ttu-id="6d351-186">Rotating external and internal secrets</span><span class="sxs-lookup"><span data-stu-id="6d351-186">Rotating external and internal secrets</span></span>

<span data-ttu-id="6d351-187">To rotate both external an internal secret:</span><span class="sxs-lookup"><span data-stu-id="6d351-187">To rotate both external an internal secret:</span></span>

1. <span data-ttu-id="6d351-188">Within the newly created **/Certificates** directory created in the Pre-steps, place the new set of replacement external certificates in the directory structure according to the format outlined in the Mandatory Certificates section of the [Azure Stack PKI certificate requirements](https://docs.microsoft.com/azure/azure-stack/azure-stack-pki-certs#mandatory-certificates).</span><span class="sxs-lookup"><span data-stu-id="6d351-188">Within the newly created **/Certificates** directory created in the Pre-steps, place the new set of replacement external certificates in the directory structure according to the format outlined in the Mandatory Certificates section of the [Azure Stack PKI certificate requirements](https://docs.microsoft.com/azure/azure-stack/azure-stack-pki-certs#mandatory-certificates).</span></span>
2. <span data-ttu-id="6d351-189">Create a PowerShell Session with the [Privileged Endpoint](https://docs.microsoft.com/azure/azure-stack/azure-stack-privileged-endpoint) using the **CloudAdmin** account and store the sessions as a variable.</span><span class="sxs-lookup"><span data-stu-id="6d351-189">Create a PowerShell Session with the [Privileged Endpoint](https://docs.microsoft.com/azure/azure-stack/azure-stack-privileged-endpoint) using the **CloudAdmin** account and store the sessions as a variable.</span></span> <span data-ttu-id="6d351-190">You will use this variable as the parameter in the next step.</span><span class="sxs-lookup"><span data-stu-id="6d351-190">You will use this variable as the parameter in the next step.</span></span>

    > [!IMPORTANT]  
    > <span data-ttu-id="6d351-191">Do not enter the session, store the session as a variable.</span><span class="sxs-lookup"><span data-stu-id="6d351-191">Do not enter the session, store the session as a variable.</span></span>
    
3. <span data-ttu-id="6d351-192">Run **[invoke-command](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/invoke-command?view=powershell-5.1)**.</span><span class="sxs-lookup"><span data-stu-id="6d351-192">Run **[invoke-command](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/invoke-command?view=powershell-5.1)**.</span></span> <span data-ttu-id="6d351-193">Pass your Privileged Endpoint PowerShell session variable as the **Session** parameter.</span><span class="sxs-lookup"><span data-stu-id="6d351-193">Pass your Privileged Endpoint PowerShell session variable as the **Session** parameter.</span></span> 
4. <span data-ttu-id="6d351-194">Run **Start-SecretRotation** with the following parameters:</span><span class="sxs-lookup"><span data-stu-id="6d351-194">Run **Start-SecretRotation** with the following parameters:</span></span>
    - <span data-ttu-id="6d351-195">**PfxFilesPath**</span><span class="sxs-lookup"><span data-stu-id="6d351-195">**PfxFilesPath**</span></span>  
    <span data-ttu-id="6d351-196">Specify the network path to your Certificates directory created earlier.</span><span class="sxs-lookup"><span data-stu-id="6d351-196">Specify the network path to your Certificates directory created earlier.</span></span>  
    - <span data-ttu-id="6d351-197">**PathAccessCredential**</span><span class="sxs-lookup"><span data-stu-id="6d351-197">**PathAccessCredential**</span></span>  
    <span data-ttu-id="6d351-198">A PSCredential object for credentials to the share.</span><span class="sxs-lookup"><span data-stu-id="6d351-198">A PSCredential object for credentials to the share.</span></span> 
    - <span data-ttu-id="6d351-199">**CertificatePassword**</span><span class="sxs-lookup"><span data-stu-id="6d351-199">**CertificatePassword**</span></span>  
    <span data-ttu-id="6d351-200">A secure string of the password used for all of the pfx certificate files created.</span><span class="sxs-lookup"><span data-stu-id="6d351-200">A secure string of the password used for all of the pfx certificate files created.</span></span>
4. <span data-ttu-id="6d351-201">Wait while your secrets rotate.</span><span class="sxs-lookup"><span data-stu-id="6d351-201">Wait while your secrets rotate.</span></span>  
<span data-ttu-id="6d351-202">When secret rotation successfully completes, your console will display **Overall action status: Success**.</span><span class="sxs-lookup"><span data-stu-id="6d351-202">When secret rotation successfully completes, your console will display **Overall action status: Success**.</span></span> 
5. <span data-ttu-id="6d351-203">After successful completion of secret rotation, remove your certificates from the share created in the pre-step and store them in their secure backup location.</span><span class="sxs-lookup"><span data-stu-id="6d351-203">After successful completion of secret rotation, remove your certificates from the share created in the pre-step and store them in their secure backup location.</span></span> 

## <a name="walkthrough-of-secret-rotation"></a><span data-ttu-id="6d351-204">Walkthrough of secret rotation</span><span class="sxs-lookup"><span data-stu-id="6d351-204">Walkthrough of secret rotation</span></span>

<span data-ttu-id="6d351-205">The following PowerShell example demonstrates the cmdlets and parameters to run in order to rotate your secrets.</span><span class="sxs-lookup"><span data-stu-id="6d351-205">The following PowerShell example demonstrates the cmdlets and parameters to run in order to rotate your secrets.</span></span>

```powershell
#Create a PEP Session
winrm s winrm/config/client '@{TrustedHosts= "<IPofERCSMachine>"}'
$PEPCreds = Get-Credential 
$PEPsession = New-PSSession -computername <IPofERCSMachine> -Credential $PEPCreds -ConfigurationName PrivilegedEndpoint 

#Run Secret Rotation
$CertPassword = ConvertTo-SecureString "Certpasswordhere" -AsPlainText -Force
$CertShareCred = Get-Credential 
$CertSharePath = "<NetworkPathofCertShare>"
Invoke-Command -session $PEPsession -ScriptBlock { 
Start-SecretRotation -PfxFilesPath $using:CertSharePath -PathAccessCredential $using:CertShareCred -CertificatePassword $using:CertPassword }
Remove-PSSession -Session $PEPSession
```
## <a name="rotating-only-internal-secrets"></a><span data-ttu-id="6d351-206">Rotating only internal secrets</span><span class="sxs-lookup"><span data-stu-id="6d351-206">Rotating only internal secrets</span></span>

<span data-ttu-id="6d351-207">To rotate only Azure Stack’s internal secrets:</span><span class="sxs-lookup"><span data-stu-id="6d351-207">To rotate only Azure Stack’s internal secrets:</span></span>

1. <span data-ttu-id="6d351-208">Create a PowerShell session with the [Privileged Endpoint](https://docs.microsoft.com/azure/azure-stack/azure-stack-privileged-endpoint).</span><span class="sxs-lookup"><span data-stu-id="6d351-208">Create a PowerShell session with the [Privileged Endpoint](https://docs.microsoft.com/azure/azure-stack/azure-stack-privileged-endpoint).</span></span>
2. <span data-ttu-id="6d351-209">In the Privileged Endpoint session, run **Start-SecretRotation** with no arguments.</span><span class="sxs-lookup"><span data-stu-id="6d351-209">In the Privileged Endpoint session, run **Start-SecretRotation** with no arguments.</span></span>

## <a name="start-secretrotation-reference"></a><span data-ttu-id="6d351-210">Start-SecretRotation reference</span><span class="sxs-lookup"><span data-stu-id="6d351-210">Start-SecretRotation reference</span></span>

<span data-ttu-id="6d351-211">Rotates the secrets of an Azure Stack System.</span><span class="sxs-lookup"><span data-stu-id="6d351-211">Rotates the secrets of an Azure Stack System.</span></span> <span data-ttu-id="6d351-212">Only executed against the Azure Stack Privileged Endpoint.</span><span class="sxs-lookup"><span data-stu-id="6d351-212">Only executed against the Azure Stack Privileged Endpoint.</span></span>

### <a name="syntax"></a><span data-ttu-id="6d351-213">Syntax</span><span class="sxs-lookup"><span data-stu-id="6d351-213">Syntax</span></span>

<span data-ttu-id="6d351-214">Path (Default)</span><span class="sxs-lookup"><span data-stu-id="6d351-214">Path (Default)</span></span>

```powershell
Start-SecretRotation [-PfxFilesPath <string>] [-PathAccessCredential] <PSCredential> [-CertificatePassword <SecureString>]  
```

### <a name="description"></a><span data-ttu-id="6d351-215">Description</span><span class="sxs-lookup"><span data-stu-id="6d351-215">Description</span></span>

<span data-ttu-id="6d351-216">The Start-SecretRotation cmdlet rotates the infrastructure secrets of an Azure Stack system.</span><span class="sxs-lookup"><span data-stu-id="6d351-216">The Start-SecretRotation cmdlet rotates the infrastructure secrets of an Azure Stack system.</span></span> <span data-ttu-id="6d351-217">By default it rotates all secrets exposed to the internal infrastructure network, with user-input it also rotates the certificates of all external network infrastructure endpoints.</span><span class="sxs-lookup"><span data-stu-id="6d351-217">By default it rotates all secrets exposed to the internal infrastructure network, with user-input it also rotates the certificates of all external network infrastructure endpoints.</span></span><span data-ttu-id="6d351-218"> When rotating external network infrastructure endpoints, Start-SecretRotation should be executed via an Invoke-Command script block with the Azure Stack environment's privileged endpoint session passed in as the session parameter.</span><span class="sxs-lookup"><span data-stu-id="6d351-218"> When rotating external network infrastructure endpoints, Start-SecretRotation should be executed via an Invoke-Command script block with the Azure Stack environment's privileged endpoint session passed in as the session parameter.</span></span>
 
### <a name="parameters"></a><span data-ttu-id="6d351-219">Parameters</span><span class="sxs-lookup"><span data-stu-id="6d351-219">Parameters</span></span>

| <span data-ttu-id="6d351-220">Parameter</span><span class="sxs-lookup"><span data-stu-id="6d351-220">Parameter</span></span> | <span data-ttu-id="6d351-221">Type</span><span class="sxs-lookup"><span data-stu-id="6d351-221">Type</span></span> | <span data-ttu-id="6d351-222">Required</span><span class="sxs-lookup"><span data-stu-id="6d351-222">Required</span></span> | <span data-ttu-id="6d351-223">Position</span><span class="sxs-lookup"><span data-stu-id="6d351-223">Position</span></span> | <span data-ttu-id="6d351-224">Default</span><span class="sxs-lookup"><span data-stu-id="6d351-224">Default</span></span> | <span data-ttu-id="6d351-225">Description</span><span class="sxs-lookup"><span data-stu-id="6d351-225">Description</span></span> |
| -- | -- | -- | -- | -- | -- |
| <span data-ttu-id="6d351-226">PfxFilesPath</span><span class="sxs-lookup"><span data-stu-id="6d351-226">PfxFilesPath</span></span> | <span data-ttu-id="6d351-227">String</span><span class="sxs-lookup"><span data-stu-id="6d351-227">String</span></span>  | <span data-ttu-id="6d351-228">False</span><span class="sxs-lookup"><span data-stu-id="6d351-228">False</span></span>  | <span data-ttu-id="6d351-229">Named</span><span class="sxs-lookup"><span data-stu-id="6d351-229">Named</span></span>  | <span data-ttu-id="6d351-230">None</span><span class="sxs-lookup"><span data-stu-id="6d351-230">None</span></span>  | <span data-ttu-id="6d351-231">The fileshare path to the **\Certificates** directory containing all external network endpoint certificates.</span><span class="sxs-lookup"><span data-stu-id="6d351-231">The fileshare path to the **\Certificates** directory containing all external network endpoint certificates.</span></span> <span data-ttu-id="6d351-232">Only required when rotating external secrets or all secrets.</span><span class="sxs-lookup"><span data-stu-id="6d351-232">Only required when rotating external secrets or all secrets.</span></span> <span data-ttu-id="6d351-233">End directory must be **\Certificates**.</span><span class="sxs-lookup"><span data-stu-id="6d351-233">End directory must be **\Certificates**.</span></span> |
| <span data-ttu-id="6d351-234">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="6d351-234">CertificatePassword</span></span> | <span data-ttu-id="6d351-235">SecureString</span><span class="sxs-lookup"><span data-stu-id="6d351-235">SecureString</span></span> | <span data-ttu-id="6d351-236">False</span><span class="sxs-lookup"><span data-stu-id="6d351-236">False</span></span>  | <span data-ttu-id="6d351-237">Named</span><span class="sxs-lookup"><span data-stu-id="6d351-237">Named</span></span>  | <span data-ttu-id="6d351-238">None</span><span class="sxs-lookup"><span data-stu-id="6d351-238">None</span></span>  | <span data-ttu-id="6d351-239">The password for all certificates provided in the -PfXFilesPath.</span><span class="sxs-lookup"><span data-stu-id="6d351-239">The password for all certificates provided in the -PfXFilesPath.</span></span> <span data-ttu-id="6d351-240">Required value if PfxFilesPath is provided when both internal and external secrets are rotated.</span><span class="sxs-lookup"><span data-stu-id="6d351-240">Required value if PfxFilesPath is provided when both internal and external secrets are rotated.</span></span> |
| <span data-ttu-id="6d351-241">PathAccessCredential</span><span class="sxs-lookup"><span data-stu-id="6d351-241">PathAccessCredential</span></span> | <span data-ttu-id="6d351-242">PSCredential</span><span class="sxs-lookup"><span data-stu-id="6d351-242">PSCredential</span></span> | <span data-ttu-id="6d351-243">False</span><span class="sxs-lookup"><span data-stu-id="6d351-243">False</span></span>  | <span data-ttu-id="6d351-244">Named</span><span class="sxs-lookup"><span data-stu-id="6d351-244">Named</span></span>  | <span data-ttu-id="6d351-245">None</span><span class="sxs-lookup"><span data-stu-id="6d351-245">None</span></span>  | <span data-ttu-id="6d351-246">The PowerShell credential for the fileshare of the **\Certificates** directory containing all external network endpoint certificates.</span><span class="sxs-lookup"><span data-stu-id="6d351-246">The PowerShell credential for the fileshare of the **\Certificates** directory containing all external network endpoint certificates.</span></span> <span data-ttu-id="6d351-247">Only required when rotating external secrets or all secrets.</span><span class="sxs-lookup"><span data-stu-id="6d351-247">Only required when rotating external secrets or all secrets.</span></span>  |
| <span data-ttu-id="6d351-248">Rerun</span><span class="sxs-lookup"><span data-stu-id="6d351-248">Rerun</span></span> | <span data-ttu-id="6d351-249">SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="6d351-249">SwitchParameter</span></span> | <span data-ttu-id="6d351-250">False</span><span class="sxs-lookup"><span data-stu-id="6d351-250">False</span></span>  | <span data-ttu-id="6d351-251">Named</span><span class="sxs-lookup"><span data-stu-id="6d351-251">Named</span></span>  | <span data-ttu-id="6d351-252">None</span><span class="sxs-lookup"><span data-stu-id="6d351-252">None</span></span>  | <span data-ttu-id="6d351-253">Rerun must be used anytime secret rotation is re-attempted after a failed attempt.</span><span class="sxs-lookup"><span data-stu-id="6d351-253">Rerun must be used anytime secret rotation is re-attempted after a failed attempt.</span></span> |

### <a name="examples"></a><span data-ttu-id="6d351-254">Examples</span><span class="sxs-lookup"><span data-stu-id="6d351-254">Examples</span></span>
 
<span data-ttu-id="6d351-255">**Rotate only internal infrastructure secrets**</span><span class="sxs-lookup"><span data-stu-id="6d351-255">**Rotate only internal infrastructure secrets**</span></span>

```powershell  
PS C:\> Start-SecretRotation  
```

<span data-ttu-id="6d351-256">This command rotates all of the infrastructure secrets exposed to Azure Stack internal network.</span><span class="sxs-lookup"><span data-stu-id="6d351-256">This command rotates all of the infrastructure secrets exposed to Azure Stack internal network.</span></span> <span data-ttu-id="6d351-257">Start-SecretRotation rotates all stack-generated secrets, but because there are no provided certificates, external endpoint certificates will not be rotated.</span><span class="sxs-lookup"><span data-stu-id="6d351-257">Start-SecretRotation rotates all stack-generated secrets, but because there are no provided certificates, external endpoint certificates will not be rotated.</span></span>  

<span data-ttu-id="6d351-258">**Rotate internal and external infrastructure secrets**</span><span class="sxs-lookup"><span data-stu-id="6d351-258">**Rotate internal and external infrastructure secrets**</span></span>
  
```powershell
PS C:\> Invoke-Command -session $PEPSession -ScriptBlock { 
Start-SecretRotation -PfxFilesPath $using:CertSharePath -PathAccessCredential $using:CertShareCred -CertificatePassword $using:CertPassword } 
Remove-PSSession -Session $PEPSession
```

<span data-ttu-id="6d351-259">This command rotates all of the infrastructure secrets exposed to Azure Stack internal network as well as the TLS certificates used for Azure Stack’s external network infrastructure endpoints.</span><span class="sxs-lookup"><span data-stu-id="6d351-259">This command rotates all of the infrastructure secrets exposed to Azure Stack internal network as well as the TLS certificates used for Azure Stack’s external network infrastructure endpoints.</span></span> <span data-ttu-id="6d351-260">Start-SecretRotation rotates all stack-generated secrets, and because there are provided certificates, external endpoint certificates will also be rotated.</span><span class="sxs-lookup"><span data-stu-id="6d351-260">Start-SecretRotation rotates all stack-generated secrets, and because there are provided certificates, external endpoint certificates will also be rotated.</span></span>  


## <a name="update-the-baseboard-management-controller-bmc-password"></a><span data-ttu-id="6d351-261">Update the baseboard management controller (BMC) password</span><span class="sxs-lookup"><span data-stu-id="6d351-261">Update the baseboard management controller (BMC) password</span></span>

<span data-ttu-id="6d351-262">The baseboard management controller (BMC) monitors the physical state of your servers.</span><span class="sxs-lookup"><span data-stu-id="6d351-262">The baseboard management controller (BMC) monitors the physical state of your servers.</span></span> <span data-ttu-id="6d351-263">The specifications and instructions on updating the password of the BMC vary based on your original equipment manufacturer (OEM) hardware vendor.</span><span class="sxs-lookup"><span data-stu-id="6d351-263">The specifications and instructions on updating the password of the BMC vary based on your original equipment manufacturer (OEM) hardware vendor.</span></span> <span data-ttu-id="6d351-264">You should update your passwords for Azure Stack components at a regular cadence.</span><span class="sxs-lookup"><span data-stu-id="6d351-264">You should update your passwords for Azure Stack components at a regular cadence.</span></span>

1. <span data-ttu-id="6d351-265">Update the BMC on the Azure Stack’s physical servers by following your OEM instructions.</span><span class="sxs-lookup"><span data-stu-id="6d351-265">Update the BMC on the Azure Stack’s physical servers by following your OEM instructions.</span></span> <span data-ttu-id="6d351-266">The password for each BMC in your environment must be the same.</span><span class="sxs-lookup"><span data-stu-id="6d351-266">The password for each BMC in your environment must be the same.</span></span>
2. <span data-ttu-id="6d351-267">Open a privileged endpoint in Azure Stack Sessions.</span><span class="sxs-lookup"><span data-stu-id="6d351-267">Open a privileged endpoint in Azure Stack Sessions.</span></span> <span data-ttu-id="6d351-268">For instruction, see [Using the privileged endpoint in Azure Stack](azure-stack-privileged-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="6d351-268">For instruction, see [Using the privileged endpoint in Azure Stack](azure-stack-privileged-endpoint.md).</span></span>
3. <span data-ttu-id="6d351-269">After your PowerShell prompt has changed to **[IP address or ERCS VM name]: PS>** or to **[azs-ercs01]: PS>**, depending on the environment, run `Set-BmcPassword` by running `invoke-command`.</span><span class="sxs-lookup"><span data-stu-id="6d351-269">After your PowerShell prompt has changed to **[IP address or ERCS VM name]: PS>** or to **[azs-ercs01]: PS>**, depending on the environment, run `Set-BmcPassword` by running `invoke-command`.</span></span> <span data-ttu-id="6d351-270">Pass your privileged endpoint session variable as a parameter.</span><span class="sxs-lookup"><span data-stu-id="6d351-270">Pass your privileged endpoint session variable as a parameter.</span></span> <span data-ttu-id="6d351-271">For example:</span><span class="sxs-lookup"><span data-stu-id="6d351-271">For example:</span></span>

    ```powershell
    # Interactive Version
    $PEip = "<Privileged Endpoint IP or Name>" # You can also use the machine name instead of IP here.
    $PECred = Get-Credential "<Domain>\CloudAdmin" -Message "PE Credentials" 
    $NewBMCpwd = Read-Host -Prompt "Enter New BMC password" -AsSecureString 

    $PEPSession = New-PSSession -ComputerName $PEip -Credential $PECred -ConfigurationName "PrivilegedEndpoint" 

    Invoke-Command -Session $PEPSession -ScriptBlock {
        Set-Bmcpassword -bmcpassword $using:NewBMCpwd
    }
    Remove-PSSession -Session $PEPSession
    ```
    
    <span data-ttu-id="6d351-272">You can also use the static PowerShell version with the Passwords as code lines:</span><span class="sxs-lookup"><span data-stu-id="6d351-272">You can also use the static PowerShell version with the Passwords as code lines:</span></span>
    
    ```powershell
    # Static Version
    $PEip = "<Privileged Endpoint IP or Name>" # You can also use the machine name instead of IP here.
    $PEUser = "<Privileged Endpoint user for exmaple Domain\CloudAdmin>"
    $PEpwd = ConvertTo-SecureString "<Privileged Endpoint Password>" -AsPlainText -Force
    $PECred = New-Object System.Management.Automation.PSCredential ($PEUser, $PEpwd) 
    $NewBMCpwd = ConvertTo-SecureString "<New BMC Password>" -AsPlainText -Force 

    $PEPSession = New-PSSession -ComputerName $PEip -Credential $PECred -ConfigurationName "PrivilegedEndpoint" 

    Invoke-Command -Session $PEPSession -ScriptBlock {
        Set-Bmcpassword -bmcpassword $using:NewBMCpwd
    }
    Remove-PSSession -Session $PEPSession
    ```

## <a name="next-steps"></a><span data-ttu-id="6d351-273">Next steps</span><span class="sxs-lookup"><span data-stu-id="6d351-273">Next steps</span></span>

[<span data-ttu-id="6d351-274">Learn more about Azure Stack security</span><span class="sxs-lookup"><span data-stu-id="6d351-274">Learn more about Azure Stack security</span></span>](azure-stack-security-foundations.md)
