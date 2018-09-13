---
title: Generate Azure Stack Public Key Infrastructure certificates for Azure Stack integrated systems deployment | Microsoft Docs
description: Describes the Azure Stack PKI certificate deployment process for Azure Stack integrated systems.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/05/2018
ms.author: mabrigg
ms.reviewer: ppacent
ms.openlocfilehash: 698e044aea6bbd78847cb209160c1fa6b2edcdbf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870116"
---
# <a name="azure-stack-certificates-signing-request-generation"></a><span data-ttu-id="b1b6e-103">Azure Stack certificates signing request generation</span><span class="sxs-lookup"><span data-stu-id="b1b6e-103">Azure Stack certificates signing request generation</span></span>

<span data-ttu-id="b1b6e-104">The Azure Stack Readiness Checker tool described in this article is available [from the PowerShell Gallery](https://aka.ms/AzsReadinessChecker).</span><span class="sxs-lookup"><span data-stu-id="b1b6e-104">The Azure Stack Readiness Checker tool described in this article is available [from the PowerShell Gallery](https://aka.ms/AzsReadinessChecker).</span></span> <span data-ttu-id="b1b6e-105">The tool creates Certificate Signing Requests (CSRs) suitable for an Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="b1b6e-105">The tool creates Certificate Signing Requests (CSRs) suitable for an Azure Stack deployment.</span></span> <span data-ttu-id="b1b6e-106">Certificates should be requested, generated, and validated with enough time to test before deployment.</span><span class="sxs-lookup"><span data-stu-id="b1b6e-106">Certificates should be requested, generated, and validated with enough time to test before deployment.</span></span>

<span data-ttu-id="b1b6e-107">The Azure Stack Readiness Checker tool (AzsReadinessChecker) performs the following certificate requests:</span><span class="sxs-lookup"><span data-stu-id="b1b6e-107">The Azure Stack Readiness Checker tool (AzsReadinessChecker) performs the following certificate requests:</span></span>

 - <span data-ttu-id="b1b6e-108">**Standard Certificate Requests**</span><span class="sxs-lookup"><span data-stu-id="b1b6e-108">**Standard Certificate Requests**</span></span>  
    <span data-ttu-id="b1b6e-109">Request according to [Generate PKI Certificates for Azure Stack Deployment](azure-stack-get-pki-certs.md).</span><span class="sxs-lookup"><span data-stu-id="b1b6e-109">Request according to [Generate PKI Certificates for Azure Stack Deployment](azure-stack-get-pki-certs.md).</span></span>
 - <span data-ttu-id="b1b6e-110">**Platform-as-a-Service**</span><span class="sxs-lookup"><span data-stu-id="b1b6e-110">**Platform-as-a-Service**</span></span>  
    <span data-ttu-id="b1b6e-111">Optionally request platform-as-a-service (PaaS) names to certificates as specified in [Azure Stack Public Key Infrastructure certificate requirements - Optional PaaS Certificates](azure-stack-pki-certs.md#optional-paas-certificates).</span><span class="sxs-lookup"><span data-stu-id="b1b6e-111">Optionally request platform-as-a-service (PaaS) names to certificates as specified in [Azure Stack Public Key Infrastructure certificate requirements - Optional PaaS Certificates](azure-stack-pki-certs.md#optional-paas-certificates).</span></span>



## <a name="prerequisites"></a><span data-ttu-id="b1b6e-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b1b6e-112">Prerequisites</span></span>

<span data-ttu-id="b1b6e-113">Your system should meet the following prerequisites before generating the CSR(s) for PKI certificates for an Azure Stack deployment:</span><span class="sxs-lookup"><span data-stu-id="b1b6e-113">Your system should meet the following prerequisites before generating the CSR(s) for PKI certificates for an Azure Stack deployment:</span></span>

 - <span data-ttu-id="b1b6e-114">Microsoft Azure Stack Readiness Checker</span><span class="sxs-lookup"><span data-stu-id="b1b6e-114">Microsoft Azure Stack Readiness Checker</span></span>
 - <span data-ttu-id="b1b6e-115">Certificate attributes:</span><span class="sxs-lookup"><span data-stu-id="b1b6e-115">Certificate attributes:</span></span>
    - <span data-ttu-id="b1b6e-116">Region name</span><span class="sxs-lookup"><span data-stu-id="b1b6e-116">Region name</span></span>
    - <span data-ttu-id="b1b6e-117">External fully qualified domain name (FQDN)</span><span class="sxs-lookup"><span data-stu-id="b1b6e-117">External fully qualified domain name (FQDN)</span></span>
    - <span data-ttu-id="b1b6e-118">Subject</span><span class="sxs-lookup"><span data-stu-id="b1b6e-118">Subject</span></span>
 - <span data-ttu-id="b1b6e-119">Windows 10 or Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="b1b6e-119">Windows 10 or Windows Server 2016</span></span>
 
  > [!NOTE]
  > <span data-ttu-id="b1b6e-120">When you receive your certificates back from your certificate authority the steps in [Prepare Azure Stack PKI certificates](azure-stack-prepare-pki-certs.md) will need to be completed on the same system!</span><span class="sxs-lookup"><span data-stu-id="b1b6e-120">When you receive your certificates back from your certificate authority the steps in [Prepare Azure Stack PKI certificates](azure-stack-prepare-pki-certs.md) will need to be completed on the same system!</span></span>

## <a name="generate-certificate-signing-requests"></a><span data-ttu-id="b1b6e-121">Generate certificate signing request(s)</span><span class="sxs-lookup"><span data-stu-id="b1b6e-121">Generate certificate signing request(s)</span></span>

<span data-ttu-id="b1b6e-122">Use these steps to prepare and validate the Azure Stack PKI certificates:</span><span class="sxs-lookup"><span data-stu-id="b1b6e-122">Use these steps to prepare and validate the Azure Stack PKI certificates:</span></span> 

1.  <span data-ttu-id="b1b6e-123">Install AzsReadinessChecker from a PowerShell prompt (5.1 or above), by running the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b1b6e-123">Install AzsReadinessChecker from a PowerShell prompt (5.1 or above), by running the following cmdlet:</span></span>

    ````PowerShell  
        Install-Module Microsoft.AzureStack.ReadinessChecker
    ````

2.  <span data-ttu-id="b1b6e-124">Declare the **subject** as an ordered dictionary.</span><span class="sxs-lookup"><span data-stu-id="b1b6e-124">Declare the **subject** as an ordered dictionary.</span></span> <span data-ttu-id="b1b6e-125">For example:</span><span class="sxs-lookup"><span data-stu-id="b1b6e-125">For example:</span></span> 

    ````PowerShell  
    $subjectHash = [ordered]@{"OU"="AzureStack";"O"="Microsoft";"L"="Redmond";"ST"="Washington";"C"="US"} 
    ````
    > [!note]  
    > <span data-ttu-id="b1b6e-126">If a common name (CN) is supplied this will be overwritten by the first DNS name of the certificate request.</span><span class="sxs-lookup"><span data-stu-id="b1b6e-126">If a common name (CN) is supplied this will be overwritten by the first DNS name of the certificate request.</span></span>

3.  <span data-ttu-id="b1b6e-127">Declare an output directory that already exists.</span><span class="sxs-lookup"><span data-stu-id="b1b6e-127">Declare an output directory that already exists.</span></span> <span data-ttu-id="b1b6e-128">For example:</span><span class="sxs-lookup"><span data-stu-id="b1b6e-128">For example:</span></span>

    ````PowerShell  
    $outputDirectory = "$ENV:USERPROFILE\Documents\AzureStackCSR"
    ````
4.  <span data-ttu-id="b1b6e-129">Declare identify system</span><span class="sxs-lookup"><span data-stu-id="b1b6e-129">Declare identify system</span></span>

    <span data-ttu-id="b1b6e-130">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b1b6e-130">Azure Active Directory</span></span>

    ```PowerShell
    $IdentitySystem = "AAD"
    ````

    <span data-ttu-id="b1b6e-131">Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="b1b6e-131">Active Directory Federation Services</span></span>

    ```PowerShell
    $IdentitySystem = "ADFS"
    ````

5. <span data-ttu-id="b1b6e-132">Declare **region name** and an **external FQDN** intended for the Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="b1b6e-132">Declare **region name** and an **external FQDN** intended for the Azure Stack deployment.</span></span>

    ```PowerShell
    $regionName = 'east'
    $externalFQDN = 'azurestack.contoso.com'
    ````

    > [!note]  
    > <span data-ttu-id="b1b6e-133">`<regionName>.<externalFQDN>` forms the basis on which all external DNS names in Azure Stack are created, in this example, the portal would be `portal.east.azurestack.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="b1b6e-133">`<regionName>.<externalFQDN>` forms the basis on which all external DNS names in Azure Stack are created, in this example, the portal would be `portal.east.azurestack.contoso.com`.</span></span>  

6. <span data-ttu-id="b1b6e-134">To generate certificate signing requests for each DNS name:</span><span class="sxs-lookup"><span data-stu-id="b1b6e-134">To generate certificate signing requests for each DNS name:</span></span>

    ```PowerShell  
    Start-AzsReadinessChecker -RegionName $regionName -FQDN $externalFQDN -subject $subjectHash -OutputRequestPath $OutputDirectory -IdentitySystem $IdentitySystem
    ````

    <span data-ttu-id="b1b6e-135">To include PaaS Services specify the switch ```-IncludePaaS```</span><span class="sxs-lookup"><span data-stu-id="b1b6e-135">To include PaaS Services specify the switch ```-IncludePaaS```</span></span>

7. <span data-ttu-id="b1b6e-136">Alternatively, for Dev/Test environments.</span><span class="sxs-lookup"><span data-stu-id="b1b6e-136">Alternatively, for Dev/Test environments.</span></span> <span data-ttu-id="b1b6e-137">To generate a single certificate request with multiple Subject Alternative Names add **-RequestType SingleCSR** parameter and value (**not** recommended for production environments):</span><span class="sxs-lookup"><span data-stu-id="b1b6e-137">To generate a single certificate request with multiple Subject Alternative Names add **-RequestType SingleCSR** parameter and value (**not** recommended for production environments):</span></span>

    ```PowerShell  
    Start-AzsReadinessChecker -RegionName $regionName -FQDN $externalFQDN -subject $subjectHash -RequestType SingleCSR -OutputRequestPath $OutputDirectory -IdentitySystem $IdentitySystem
    ````

    <span data-ttu-id="b1b6e-138">To include PaaS Services specify the switch ```-IncludePaaS```</span><span class="sxs-lookup"><span data-stu-id="b1b6e-138">To include PaaS Services specify the switch ```-IncludePaaS```</span></span>
    
8. <span data-ttu-id="b1b6e-139">Review the output:</span><span class="sxs-lookup"><span data-stu-id="b1b6e-139">Review the output:</span></span>

    ````PowerShell  
    AzsReadinessChecker v1.1803.405.3 started
    Starting Certificate Request Generation

    CSR generating for following SAN(s): dns=*.east.azurestack.contoso.com&dns=*.blob.east.azurestack.contoso.com&dns=*.queue.east.azurestack.contoso.com&dns=*.table.east.azurestack.cont
    oso.com&dns=*.vault.east.azurestack.contoso.com&dns=*.adminvault.east.azurestack.contoso.com&dns=portal.east.azurestack.contoso.com&dns=adminportal.east.azurestack.contoso.com&dns=ma
    nagement.east.azurestack.contoso.com&dns=adminmanagement.east.azurestack.contoso.com*dn2=*.adminhosting.east.azurestack.contoso.com@dns=*.hosting.east.azurestack.contoso.com
    Present this CSR to your Certificate Authority for Certificate Generation: C:\Users\username\Documents\AzureStackCSR\wildcard_east_azurestack_contoso_com_CertRequest_20180405233530.req
    Certreq.exe output: CertReq: Request Created

    Finished Certificate Request Generation

    AzsReadinessChecker Log location: C:\Program Files\WindowsPowerShell\Modules\Microsoft.AzureStack.ReadinessChecker\1.1803.405.3\AzsReadinessChecker.log
    AzsReadinessChecker Completed
    ````

9.  <span data-ttu-id="b1b6e-140">Submit the **.REQ** file generated to your CA (either internal or public).</span><span class="sxs-lookup"><span data-stu-id="b1b6e-140">Submit the **.REQ** file generated to your CA (either internal or public).</span></span>  <span data-ttu-id="b1b6e-141">The output directory of **Start-AzsReadinessChecker** contains the CSR(s) necessary to submit to a Certificate Authority.</span><span class="sxs-lookup"><span data-stu-id="b1b6e-141">The output directory of **Start-AzsReadinessChecker** contains the CSR(s) necessary to submit to a Certificate Authority.</span></span>  <span data-ttu-id="b1b6e-142">It also contains a child directory containing the INF file(s) used during certificate request generation, as a reference.</span><span class="sxs-lookup"><span data-stu-id="b1b6e-142">It also contains a child directory containing the INF file(s) used during certificate request generation, as a reference.</span></span> <span data-ttu-id="b1b6e-143">Be sure that your CA generates certificates using your generated request that meet the [Azure Stack PKI Requirements](azure-stack-pki-certs.md).</span><span class="sxs-lookup"><span data-stu-id="b1b6e-143">Be sure that your CA generates certificates using your generated request that meet the [Azure Stack PKI Requirements](azure-stack-pki-certs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1b6e-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="b1b6e-144">Next steps</span></span>

[<span data-ttu-id="b1b6e-145">Prepare Azure Stack PKI certificates</span><span class="sxs-lookup"><span data-stu-id="b1b6e-145">Prepare Azure Stack PKI certificates</span></span>](azure-stack-prepare-pki-certs.md)
