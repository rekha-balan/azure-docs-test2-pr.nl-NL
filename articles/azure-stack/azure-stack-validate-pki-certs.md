---
title: Validate Azure Stack Public Key Infrastructure certificates for Azure Stack integrated systems deployment | Microsoft Docs
description: Describes how to validate the Azure Stack PKI certificates for Azure Stack integrated systems. Covers using the Azure Stack Certificate Checker tool.
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
ms.openlocfilehash: 1e7d3c4d5f91a74adb881840e3c5a5ac7e8f3763
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866242"
---
# <a name="validate-azure-stack-pki-certificates"></a><span data-ttu-id="a4b9d-104">Validate Azure Stack PKI certificates</span><span class="sxs-lookup"><span data-stu-id="a4b9d-104">Validate Azure Stack PKI certificates</span></span>

<span data-ttu-id="a4b9d-105">The Azure Stack Readiness Checker tool described in this article is available [from the PowerShell Gallery](https://aka.ms/AzsReadinessChecker).</span><span class="sxs-lookup"><span data-stu-id="a4b9d-105">The Azure Stack Readiness Checker tool described in this article is available [from the PowerShell Gallery](https://aka.ms/AzsReadinessChecker).</span></span> <span data-ttu-id="a4b9d-106">You can use the tool to validate that  the [generated PKI certificates](azure-stack-get-pki-certs.md) are suitable for pre-deployment.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-106">You can use the tool to validate that  the [generated PKI certificates](azure-stack-get-pki-certs.md) are suitable for pre-deployment.</span></span> <span data-ttu-id="a4b9d-107">You should validate certificates by leaving  enough time to test and reissue certificates if necessary.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-107">You should validate certificates by leaving  enough time to test and reissue certificates if necessary.</span></span>

<span data-ttu-id="a4b9d-108">The Readiness Checker tool performs the following certificate validations:</span><span class="sxs-lookup"><span data-stu-id="a4b9d-108">The Readiness Checker tool performs the following certificate validations:</span></span>

- <span data-ttu-id="a4b9d-109">**Read PFX**</span><span class="sxs-lookup"><span data-stu-id="a4b9d-109">**Read PFX**</span></span>  
    <span data-ttu-id="a4b9d-110">Checks for valid PFX file, correct password, and warns if public information is not protected by the password.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-110">Checks for valid PFX file, correct password, and warns if public information is not protected by the password.</span></span> 
- <span data-ttu-id="a4b9d-111">**Signature algorithm**</span><span class="sxs-lookup"><span data-stu-id="a4b9d-111">**Signature algorithm**</span></span>  
    <span data-ttu-id="a4b9d-112">Checks that the signature algorithm is not SHA1.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-112">Checks that the signature algorithm is not SHA1.</span></span>
- <span data-ttu-id="a4b9d-113">**Private Key**</span><span class="sxs-lookup"><span data-stu-id="a4b9d-113">**Private Key**</span></span>  
    <span data-ttu-id="a4b9d-114">Checks that the private key is present and is exported with the local machine attribute.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-114">Checks that the private key is present and is exported with the local machine attribute.</span></span> 
- <span data-ttu-id="a4b9d-115">**Cert chain**</span><span class="sxs-lookup"><span data-stu-id="a4b9d-115">**Cert chain**</span></span>  
    <span data-ttu-id="a4b9d-116">Checks certificate chain is intact including a check for self-signed certificates.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-116">Checks certificate chain is intact including a check for self-signed certificates.</span></span>
- <span data-ttu-id="a4b9d-117">**DNS names**</span><span class="sxs-lookup"><span data-stu-id="a4b9d-117">**DNS names**</span></span>  
    <span data-ttu-id="a4b9d-118">Checks the SAN contains relevant DNS names for each endpoint, or if a supporting wildcard is present.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-118">Checks the SAN contains relevant DNS names for each endpoint, or if a supporting wildcard is present.</span></span>
- <span data-ttu-id="a4b9d-119">**Key usage**</span><span class="sxs-lookup"><span data-stu-id="a4b9d-119">**Key usage**</span></span>  
    <span data-ttu-id="a4b9d-120">Checks if the key usage contains a digital signature and key encipherment and enhanced key usage contains server authentication and client authentication.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-120">Checks if the key usage contains a digital signature and key encipherment and enhanced key usage contains server authentication and client authentication.</span></span>
- <span data-ttu-id="a4b9d-121">**Key size**</span><span class="sxs-lookup"><span data-stu-id="a4b9d-121">**Key size**</span></span>  
    <span data-ttu-id="a4b9d-122">Checks if the key size is 2048 or larger.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-122">Checks if the key size is 2048 or larger.</span></span>
- <span data-ttu-id="a4b9d-123">**Chain order**</span><span class="sxs-lookup"><span data-stu-id="a4b9d-123">**Chain order**</span></span>  
    <span data-ttu-id="a4b9d-124">Checks the order of the other certificates validating that the order is correct.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-124">Checks the order of the other certificates validating that the order is correct.</span></span>
- <span data-ttu-id="a4b9d-125">**Other certificates**</span><span class="sxs-lookup"><span data-stu-id="a4b9d-125">**Other certificates**</span></span>  
    <span data-ttu-id="a4b9d-126">Ensure no other certificates have been packaged in PFX other than the relevant leaf certificate and its chain.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-126">Ensure no other certificates have been packaged in PFX other than the relevant leaf certificate and its chain.</span></span>
- <span data-ttu-id="a4b9d-127">**No profile**</span><span class="sxs-lookup"><span data-stu-id="a4b9d-127">**No profile**</span></span>  
    <span data-ttu-id="a4b9d-128">Checks that a new user can load the PFX data without a user profile loaded, mimicking the behavior of gMSA accounts during certificate servicing.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-128">Checks that a new user can load the PFX data without a user profile loaded, mimicking the behavior of gMSA accounts during certificate servicing.</span></span>

> [!IMPORTANT]  
> <span data-ttu-id="a4b9d-129">The PKI certificate is a PFX file and password should be treated as sensitive information.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-129">The PKI certificate is a PFX file and password should be treated as sensitive information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4b9d-130">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a4b9d-130">Prerequisites</span></span>

<span data-ttu-id="a4b9d-131">Your system should meet the following prerequisites before validating PKI certificates for an Azure Stack deployment:</span><span class="sxs-lookup"><span data-stu-id="a4b9d-131">Your system should meet the following prerequisites before validating PKI certificates for an Azure Stack deployment:</span></span>

- <span data-ttu-id="a4b9d-132">Microsoft Azure Stack Readiness Checker</span><span class="sxs-lookup"><span data-stu-id="a4b9d-132">Microsoft Azure Stack Readiness Checker</span></span>
- <span data-ttu-id="a4b9d-133">SSL Certificate(s) exported following the [preparation instructions](azure-stack-prepare-pki-certs.md)</span><span class="sxs-lookup"><span data-stu-id="a4b9d-133">SSL Certificate(s) exported following the [preparation instructions](azure-stack-prepare-pki-certs.md)</span></span>
- <span data-ttu-id="a4b9d-134">DeploymentData.json</span><span class="sxs-lookup"><span data-stu-id="a4b9d-134">DeploymentData.json</span></span>
- <span data-ttu-id="a4b9d-135">Windows 10 or Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="a4b9d-135">Windows 10 or Windows Server 2016</span></span>

## <a name="perform-core-services-certificate-validation"></a><span data-ttu-id="a4b9d-136">Perform core services certificate validation</span><span class="sxs-lookup"><span data-stu-id="a4b9d-136">Perform core services certificate validation</span></span>

<span data-ttu-id="a4b9d-137">Use these steps to prepare and to validate the Azure Stack PKI certificates for deployment and secret rotation:</span><span class="sxs-lookup"><span data-stu-id="a4b9d-137">Use these steps to prepare and to validate the Azure Stack PKI certificates for deployment and secret rotation:</span></span>

1. <span data-ttu-id="a4b9d-138">Install **AzsReadinessChecker** from a PowerShell prompt (5.1 or above), by running the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a4b9d-138">Install **AzsReadinessChecker** from a PowerShell prompt (5.1 or above), by running the following cmdlet:</span></span>

    ```PowerShell  
        Install-Module Microsoft.AzureStack.ReadinessChecker -force 
    ```

2. <span data-ttu-id="a4b9d-139">Create the certificate directory structure.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-139">Create the certificate directory structure.</span></span> <span data-ttu-id="a4b9d-140">In the example below, you can change `<c:\certificates>` to a new directory path of your choice.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-140">In the example below, you can change `<c:\certificates>` to a new directory path of your choice.</span></span>
    ```PowerShell  
    New-Item C:\Certificates -ItemType Directory
    
    $directories = 'ACSBlob','ACSQueue','ACSTable','ADFS','Admin Portal','ARM Admin','ARM Public','Graph','KeyVault','KeyVaultInternal','Public Portal','Admin Extension Host','Public Extension Host'
    
    $destination = 'c:\certificates'
    
    $directories | % { New-Item -Path (Join-Path $destination $PSITEM) -ItemType Directory -Force}
    ```
    
    > [!Note]  
    > <span data-ttu-id="a4b9d-141">AD FS and Graph are required if you are using AD FS as your identity system.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-141">AD FS and Graph are required if you are using AD FS as your identity system.</span></span>
    
     - <span data-ttu-id="a4b9d-142">Place your certificate(s) in the appropriate directories created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-142">Place your certificate(s) in the appropriate directories created in the previous step.</span></span> <span data-ttu-id="a4b9d-143">For example:</span><span class="sxs-lookup"><span data-stu-id="a4b9d-143">For example:</span></span>  
        - `c:\certificates\ACSBlob\CustomerCertificate.pfx`
        - `c:\certificates\Certs\Admin Portal\CustomerCertificate.pfx`
        - `c:\certificates\Certs\ARM Admin\CustomerCertificate.pfx`

3. <span data-ttu-id="a4b9d-144">In the PowerShell window, change the values of **RegionName** and **FQDN** appropriate to the Azure Stack environment and run the following:</span><span class="sxs-lookup"><span data-stu-id="a4b9d-144">In the PowerShell window, change the values of **RegionName** and **FQDN** appropriate to the Azure Stack environment and run the following:</span></span>

    ```PowerShell  
    $pfxPassword = Read-Host -Prompt "Enter PFX Password" -AsSecureString 

    Start-AzsReadinessChecker -CertificatePath c:\certificates -pfxPassword $pfxPassword -RegionName east -FQDN azurestack.contoso.com -IdentitySystem AAD 
    ```

4. <span data-ttu-id="a4b9d-145">Check the output and all certificates pass all tests.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-145">Check the output and all certificates pass all tests.</span></span> <span data-ttu-id="a4b9d-146">For example:</span><span class="sxs-lookup"><span data-stu-id="a4b9d-146">For example:</span></span>

    ```PowerShell  
    AzsReadinessChecker v1.1803.405.3 started
    Starting Certificate Validation

    Starting Azure Stack Certificate Validation 1.1803.405.3
    Testing: ARM Public\ssl.pfx
        Read PFX: OK
        Signature Algorithm: OK
        Private Key: OK
        Cert Chain: OK
        DNS Names: OK
        Key Usage: OK
        Key Size: OK
        Chain Order: OK
        Other Certificates: OK
    Testing: ACSBlob\ssl.pfx
        Read PFX: OK
        Signature Algorithm: OK
        Private Key: OK
        Cert Chain: OK
        DNS Names: OK
        Key Usage: OK
        Key Size: OK
        Chain Order: OK
        Other Certificates: OK
    Detailed log can be found C:\AzsReadinessChecker\CertificateValidation\CertChecker.log

    Finished Certificate Validation

    AzsReadinessChecker Log location: C:\AzsReadinessChecker\AzsReadinessChecker.log
    AzsReadinessChecker Report location: 
    C:\AzsReadinessChecker\AzsReadinessReport.json
    AzsReadinessChecker Completed
    ```

### <a name="known-issues"></a><span data-ttu-id="a4b9d-147">Known issues</span><span class="sxs-lookup"><span data-stu-id="a4b9d-147">Known issues</span></span>

<span data-ttu-id="a4b9d-148">**Symptom**: Tests are skipped</span><span class="sxs-lookup"><span data-stu-id="a4b9d-148">**Symptom**: Tests are skipped</span></span>

<span data-ttu-id="a4b9d-149">**Cause**: AzsReadinessChecker skips certain tests if a dependency isn’t met:</span><span class="sxs-lookup"><span data-stu-id="a4b9d-149">**Cause**: AzsReadinessChecker skips certain tests if a dependency isn’t met:</span></span>

 - <span data-ttu-id="a4b9d-150">Other certificates are skipped if certificate chain fails.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-150">Other certificates are skipped if certificate chain fails.</span></span>

    ```PowerShell  
    Testing: ACSBlob\singlewildcard.pfx
        Read PFX: OK
        Signature Algorithm: OK
        Private Key: OK
        Cert Chain: OK
        DNS Names: Fail
        Key Usage: OK
        Key Size: OK
        Chain Order: OK
        Other Certificates: Skipped
    Details:
    The certificate records '*.east.azurestack.contoso.com' do not contain a record that is valid for '*.blob.east.azurestack.contoso.com'. Please refer to the documentation for how to create the required certificate file.
    The Other Certificates check was skipped because Cert Chain and/or DNS Names failed. Follow the guidance to remediate those issues and recheck. 
    Detailed log can be found C:\AzsReadinessChecker\CertificateValidation\CertChecker.log

    Finished Certificate Validation

    AzsReadinessChecker Log location: C:\AzsReadinessChecker\AzsReadinessChecker.log
    AzsReadinessChecker Report location (for OEM): C:\AzsReadinessChecker\AzsReadinessChecker.log
    AzsReadinessChecker Completed
    ```

<span data-ttu-id="a4b9d-151">**Resolution**: Follow the tool's guidance in the details section under each set of tests for each certificate.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-151">**Resolution**: Follow the tool's guidance in the details section under each set of tests for each certificate.</span></span>

## <a name="perform-platform-as-a-service-certificate-validation"></a><span data-ttu-id="a4b9d-152">Perform platform as a service certificate validation</span><span class="sxs-lookup"><span data-stu-id="a4b9d-152">Perform platform as a service certificate validation</span></span>

<span data-ttu-id="a4b9d-153">Use these steps to prepare and validate the Azure Stack PKI certificates for platform as a service (PaaS) certificates, if SQL/MySQL or App Services deployments are planned.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-153">Use these steps to prepare and validate the Azure Stack PKI certificates for platform as a service (PaaS) certificates, if SQL/MySQL or App Services deployments are planned.</span></span>

1.  <span data-ttu-id="a4b9d-154">Install **AzsReadinessChecker** from a PowerShell prompt (5.1 or above), by running the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a4b9d-154">Install **AzsReadinessChecker** from a PowerShell prompt (5.1 or above), by running the following cmdlet:</span></span>

    ```PowerShell  
      Install-Module Microsoft.AzureStack.ReadinessChecker -force
    ```

2.  <span data-ttu-id="a4b9d-155">Create a nested hashtable containing paths and password to each PaaS certificate needing validation.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-155">Create a nested hashtable containing paths and password to each PaaS certificate needing validation.</span></span> <span data-ttu-id="a4b9d-156">In the PowerShell window run:</span><span class="sxs-lookup"><span data-stu-id="a4b9d-156">In the PowerShell window run:</span></span>

    ```PowerShell  
        $PaaSCertificates = @{
        'PaaSDBCert' = @{'pfxPath' = '<Path to DBAdapter PFX>';'pfxPassword' = (ConvertTo-SecureString -String '<Password for PFX>' -AsPlainText -Force)}
        'PaaSDefaultCert' = @{'pfxPath' = '<Path to Default PFX>';'pfxPassword' = (ConvertTo-SecureString -String '<Password for PFX>' -AsPlainText -Force)}
        'PaaSAPICert' = @{'pfxPath' = '<Path to API PFX>';'pfxPassword' = (ConvertTo-SecureString -String '<Password for PFX>' -AsPlainText -Force)}
        'PaaSFTPCert' = @{'pfxPath' = '<Path to FTP PFX>';'pfxPassword' = (ConvertTo-SecureString -String '<Password for PFX>' -AsPlainText -Force)}
        'PaaSSSOCert' = @{'pfxPath' = '<Path to SSO PFX>';'pfxPassword' = (ConvertTo-SecureString -String '<Password for PFX>' -AsPlainText -Force)}
        }
    ```

3.  <span data-ttu-id="a4b9d-157">Change the values of **RegionName** and **FQDN** to match your Azure Stack environment to start the validation.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-157">Change the values of **RegionName** and **FQDN** to match your Azure Stack environment to start the validation.</span></span> <span data-ttu-id="a4b9d-158">Then run:</span><span class="sxs-lookup"><span data-stu-id="a4b9d-158">Then run:</span></span>

    ```PowerShell  
    Start-AzsReadinessChecker -PaaSCertificates $PaaSCertificates -RegionName east -FQDN azurestack.contoso.com 
    ```
4.  <span data-ttu-id="a4b9d-159">Check that the output and that all certificates pass all tests.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-159">Check that the output and that all certificates pass all tests.</span></span>

    ```PowerShell
    AzsReadinessChecker v1.1805.425.2 started
    Starting PaaS Certificate Validation
    
    Starting Azure Stack Certificate Validation 1.0 
    Testing: PaaSCerts\wildcard.appservice.pfx
        Read PFX: OK
        Signature Algorithm: OK
        Private Key: OK
        Cert Chain: OK
        DNS Names: OK
        Key Usage: OK
        Key Size: OK
        Chain Order: OK
        Other Certificates: OK
    Testing: PaaSCerts\api.appservice.pfx
        Read PFX: OK
        Signature Algorithm: OK
        Private Key: OK
        Cert Chain: OK
        DNS Names: OK
        Key Usage: OK
        Key Size: OK
        Chain Order: OK
        Other Certificates: OK
    Testing: PaaSCerts\wildcard.dbadapter.pfx
        Read PFX: OK
        Signature Algorithm: OK
        Private Key: OK
        Cert Chain: OK
        DNS Names: OK
        Key Usage: OK
        Key Size: OK
        Chain Order: OK
        Other Certificates: OK
    Testing: PaaSCerts\sso.appservice.pfx
        Read PFX: OK
        Signature Algorithm: OK
        Private Key: OK
        Cert Chain: OK
        DNS Names: OK
        Key Usage: OK
        Key Size: OK
    ```

## <a name="using-validated-certificates"></a><span data-ttu-id="a4b9d-160">Using validated certificates</span><span class="sxs-lookup"><span data-stu-id="a4b9d-160">Using validated certificates</span></span>

<span data-ttu-id="a4b9d-161">Once your certificates have been validated by the AzsReadinessChecker, you are ready to use them in your Azure Stack deployment or for Azure Stack secret rotation.</span><span class="sxs-lookup"><span data-stu-id="a4b9d-161">Once your certificates have been validated by the AzsReadinessChecker, you are ready to use them in your Azure Stack deployment or for Azure Stack secret rotation.</span></span> 

 - <span data-ttu-id="a4b9d-162">For deployment, securely transfer your certificates to your deployment engineer so that they can copy them onto the deployment host as specified in the [Azure Stack PKI requirements documentation](azure-stack-pki-certs.md).</span><span class="sxs-lookup"><span data-stu-id="a4b9d-162">For deployment, securely transfer your certificates to your deployment engineer so that they can copy them onto the deployment host as specified in the [Azure Stack PKI requirements documentation](azure-stack-pki-certs.md).</span></span>
 - <span data-ttu-id="a4b9d-163">For secret rotation, you can use the certificates to update old certificates for your Azure Stack environment’s public infrastructure endpoints by following the [Azure Stack Secret Rotation documentation](azure-stack-rotate-secrets.md).</span><span class="sxs-lookup"><span data-stu-id="a4b9d-163">For secret rotation, you can use the certificates to update old certificates for your Azure Stack environment’s public infrastructure endpoints by following the [Azure Stack Secret Rotation documentation](azure-stack-rotate-secrets.md).</span></span>
 - <span data-ttu-id="a4b9d-164">For PaaS services, you can use the certificates to install SQL, MySQL, and App Services Resource Providers in Azure Stack by following the [Overview of offering services in Azure Stack documentation](azure-stack-offer-services-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4b9d-164">For PaaS services, you can use the certificates to install SQL, MySQL, and App Services Resource Providers in Azure Stack by following the [Overview of offering services in Azure Stack documentation](azure-stack-offer-services-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4b9d-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="a4b9d-165">Next steps</span></span>

[<span data-ttu-id="a4b9d-166">Datacenter identity integration</span><span class="sxs-lookup"><span data-stu-id="a4b9d-166">Datacenter identity integration</span></span>](azure-stack-integrate-identity.md)