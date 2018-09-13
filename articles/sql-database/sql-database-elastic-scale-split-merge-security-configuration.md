---
title: Split-merge security configuration | Microsoft Docs
description: Set up x409 certificates for encryption
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: ''
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: multiple databases
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: f96cc52b060434de5f257724e2b975410c4fb761
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563607"
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="47004-103">Split-merge security configuration</span><span class="sxs-lookup"><span data-stu-id="47004-103">Split-merge security configuration</span></span>
<span data-ttu-id="47004-104">To use the Split/Merge service, you must correctly configure security.</span><span class="sxs-lookup"><span data-stu-id="47004-104">To use the Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="47004-105">The service is part of the Elastic Scale feature of Microsoft Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="47004-105">The service is part of the Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="47004-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="47004-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="47004-107">Configuring certificates</span><span class="sxs-lookup"><span data-stu-id="47004-107">Configuring certificates</span></span>
<span data-ttu-id="47004-108">Certificates are configured in two ways.</span><span class="sxs-lookup"><span data-stu-id="47004-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="47004-109">To Configure the SSL Certificate</span><span class="sxs-lookup"><span data-stu-id="47004-109">To Configure the SSL Certificate</span></span>](#To-Configure-the-SSL#Certificate)
2. [<span data-ttu-id="47004-110">To Configure Client Certificates</span><span class="sxs-lookup"><span data-stu-id="47004-110">To Configure Client Certificates</span></span>](#To-Configure-Client-Certificates) 

## <a name="to-obtain-certificates"></a><span data-ttu-id="47004-111">To obtain certificates</span><span class="sxs-lookup"><span data-stu-id="47004-111">To obtain certificates</span></span>
<span data-ttu-id="47004-112">Certificates can be obtained from public Certificate Authorities (CAs) or from the [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span><span class="sxs-lookup"><span data-stu-id="47004-112">Certificates can be obtained from public Certificate Authorities (CAs) or from the [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="47004-113">These are the preferred methods to obtain certificates.</span><span class="sxs-lookup"><span data-stu-id="47004-113">These are the preferred methods to obtain certificates.</span></span>

<span data-ttu-id="47004-114">If those options are not available, you can generate **self-signed certificates**.</span><span class="sxs-lookup"><span data-stu-id="47004-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-to-generate-certificates"></a><span data-ttu-id="47004-115">Tools to generate certificates</span><span class="sxs-lookup"><span data-stu-id="47004-115">Tools to generate certificates</span></span>
* [<span data-ttu-id="47004-116">makecert.exe</span><span class="sxs-lookup"><span data-stu-id="47004-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="47004-117">pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="47004-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="to-run-the-tools"></a><span data-ttu-id="47004-118">To run the tools</span><span class="sxs-lookup"><span data-stu-id="47004-118">To run the tools</span></span>
* <span data-ttu-id="47004-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span><span class="sxs-lookup"><span data-stu-id="47004-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="47004-120">If installed, go to:</span><span class="sxs-lookup"><span data-stu-id="47004-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="47004-121">Get the WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="47004-121">Get the WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="to-configure-the-ssl-certificate"></a><span data-ttu-id="47004-122">To configure the SSL certificate</span><span class="sxs-lookup"><span data-stu-id="47004-122">To configure the SSL certificate</span></span>
<span data-ttu-id="47004-123">A SSL certificate is required to encrypt the communication and authenticate the server.</span><span class="sxs-lookup"><span data-stu-id="47004-123">A SSL certificate is required to encrypt the communication and authenticate the server.</span></span> <span data-ttu-id="47004-124">Choose the most applicable of the three scenarios below, and execute all its steps:</span><span class="sxs-lookup"><span data-stu-id="47004-124">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="47004-125">Create a new self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="47004-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="47004-126">Create a Self-Signed Certificate</span><span class="sxs-lookup"><span data-stu-id="47004-126">Create a Self-Signed Certificate</span></span>](#Create-a-Self-Signed-Certificate)
2. [<span data-ttu-id="47004-127">Create PFX file for Self-Signed SSL Certificate</span><span class="sxs-lookup"><span data-stu-id="47004-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#Create-PFX-file-for-Self-Signed-SSL-Certificate)
3. [<span data-ttu-id="47004-128">Upload SSL Certificate to Cloud Service</span><span class="sxs-lookup"><span data-stu-id="47004-128">Upload SSL Certificate to Cloud Service</span></span>](#Upload-SSL-Certificate-to-Cloud-Service)
4. [<span data-ttu-id="47004-129">Update SSL Certificate in Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="47004-129">Update SSL Certificate in Service Configuration File</span></span>](#Update-SSL-Certificate-in-Service-Configuration-File)
5. [<span data-ttu-id="47004-130">Import SSL Certification Authority</span><span class="sxs-lookup"><span data-stu-id="47004-130">Import SSL Certification Authority</span></span>](#Import-SSL-Certification-Authority)

### <a name="to-use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="47004-131">To use an existing certificate from the certificate store</span><span class="sxs-lookup"><span data-stu-id="47004-131">To use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="47004-132">Export SSL Certificate From Certificate Store</span><span class="sxs-lookup"><span data-stu-id="47004-132">Export SSL Certificate From Certificate Store</span></span>](#Export-SSL-Certificate-From-Certificate-Store)
2. [<span data-ttu-id="47004-133">Upload SSL Certificate to Cloud Service</span><span class="sxs-lookup"><span data-stu-id="47004-133">Upload SSL Certificate to Cloud Service</span></span>](#Upload-SSL-Certificate-to-Cloud-Service)
3. [<span data-ttu-id="47004-134">Update SSL Certificate in Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="47004-134">Update SSL Certificate in Service Configuration File</span></span>](#Update-SSL-Certificate-in-Service-Configuration-File)

### <a name="to-use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="47004-135">To use an existing certificate in a PFX file</span><span class="sxs-lookup"><span data-stu-id="47004-135">To use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="47004-136">Upload SSL Certificate to Cloud Service</span><span class="sxs-lookup"><span data-stu-id="47004-136">Upload SSL Certificate to Cloud Service</span></span>](#Upload-SSL-Certificate-to-Cloud-Service)
2. [<span data-ttu-id="47004-137">Update SSL Certificate in Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="47004-137">Update SSL Certificate in Service Configuration File</span></span>](#Update-SSL-Certificate-in-Service-Configuration-File)

## <a name="to-configure-client-certificates"></a><span data-ttu-id="47004-138">To configure client certificates</span><span class="sxs-lookup"><span data-stu-id="47004-138">To configure client certificates</span></span>
<span data-ttu-id="47004-139">Client certificates are required in order to authenticate requests to the service.</span><span class="sxs-lookup"><span data-stu-id="47004-139">Client certificates are required in order to authenticate requests to the service.</span></span> <span data-ttu-id="47004-140">Choose the most applicable of the three scenarios below, and execute all its steps:</span><span class="sxs-lookup"><span data-stu-id="47004-140">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="47004-141">Turn off client certificates</span><span class="sxs-lookup"><span data-stu-id="47004-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="47004-142">Turn Off Client Certificate-Based Authentication</span><span class="sxs-lookup"><span data-stu-id="47004-142">Turn Off Client Certificate-Based Authentication</span></span>](#Turn-Off-Client-Certificate-Based-Authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="47004-143">Issue new self-signed client certificates</span><span class="sxs-lookup"><span data-stu-id="47004-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="47004-144">Create a Self-Signed Certification Authority</span><span class="sxs-lookup"><span data-stu-id="47004-144">Create a Self-Signed Certification Authority</span></span>](#Create-a-Self-Signed-Certification-Authority)
2. [<span data-ttu-id="47004-145">Upload CA Certificate to Cloud Service</span><span class="sxs-lookup"><span data-stu-id="47004-145">Upload CA Certificate to Cloud Service</span></span>](#Upload-CA-Certificate-to-Cloud-Service)
3. [<span data-ttu-id="47004-146">Update CA Certificate in Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="47004-146">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="47004-147">Issue Client Certificates</span><span class="sxs-lookup"><span data-stu-id="47004-147">Issue Client Certificates</span></span>](#Issue-Client-Certificates)
5. [<span data-ttu-id="47004-148">Create PFX files for Client Certificates</span><span class="sxs-lookup"><span data-stu-id="47004-148">Create PFX files for Client Certificates</span></span>](#Create-PFX-files-for-Client-Certificates)
6. [<span data-ttu-id="47004-149">Import Client Certificate</span><span class="sxs-lookup"><span data-stu-id="47004-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="47004-150">Copy Client Certificate Thumbprints</span><span class="sxs-lookup"><span data-stu-id="47004-150">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
8. [<span data-ttu-id="47004-151">Configure Allowed Clients in the Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="47004-151">Configure Allowed Clients in the Service Configuration File</span></span>](#Configure-Allowed-Clients-in-the-Service-Configuration-File)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="47004-152">Use existing client certificates</span><span class="sxs-lookup"><span data-stu-id="47004-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="47004-153">Find CA Public Key</span><span class="sxs-lookup"><span data-stu-id="47004-153">Find CA Public Key</span></span>](#Find-CA-Public Key)
2. [<span data-ttu-id="47004-154">Upload CA Certificate to Cloud Service</span><span class="sxs-lookup"><span data-stu-id="47004-154">Upload CA Certificate to Cloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="47004-155">Update CA Certificate in Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="47004-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="47004-156">Copy Client Certificate Thumbprints</span><span class="sxs-lookup"><span data-stu-id="47004-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="47004-157">Configure Allowed Clients in the Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="47004-157">Configure Allowed Clients in the Service Configuration File</span></span>](#Configure-Allowed-Clients-in-the-Service-Configuration File)
6. [<span data-ttu-id="47004-158">Configure Client Certificate Revocation Check</span><span class="sxs-lookup"><span data-stu-id="47004-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="47004-159">Allowed IP addresses</span><span class="sxs-lookup"><span data-stu-id="47004-159">Allowed IP addresses</span></span>
<span data-ttu-id="47004-160">Access to the service endpoints can be restricted to specific ranges of IP addresses.</span><span class="sxs-lookup"><span data-stu-id="47004-160">Access to the service endpoints can be restricted to specific ranges of IP addresses.</span></span>

## <a name="to-configure-encryption-for-the-store"></a><span data-ttu-id="47004-161">To configure encryption for the store</span><span class="sxs-lookup"><span data-stu-id="47004-161">To configure encryption for the store</span></span>
<span data-ttu-id="47004-162">A certificate is required to encrypt the credentials that are stored in the metadata store.</span><span class="sxs-lookup"><span data-stu-id="47004-162">A certificate is required to encrypt the credentials that are stored in the metadata store.</span></span> <span data-ttu-id="47004-163">Choose the most applicable of the three scenarios below, and execute all its steps:</span><span class="sxs-lookup"><span data-stu-id="47004-163">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="47004-164">Use a new self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="47004-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="47004-165">Create a Self-Signed Certificate</span><span class="sxs-lookup"><span data-stu-id="47004-165">Create a Self-Signed Certificate</span></span>](#Create-a-Self-Signed-Certificate)
2. [<span data-ttu-id="47004-166">Create PFX file for Self-Signed Encryption Certificate</span><span class="sxs-lookup"><span data-stu-id="47004-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#Create-PFX-file-for-Self-Signed-Encryption-Certificate)
3. [<span data-ttu-id="47004-167">Upload Encryption Certificate to Cloud Service</span><span class="sxs-lookup"><span data-stu-id="47004-167">Upload Encryption Certificate to Cloud Service</span></span>](#Upload-Encryption-Certificate-to-Cloud-Service)
4. [<span data-ttu-id="47004-168">Update Encryption Certificate in Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="47004-168">Update Encryption Certificate in Service Configuration File</span></span>](#Update-Encryption-Certificate-in-Service-Configuration-File)

### <a name="use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="47004-169">Use an existing certificate from the certificate store</span><span class="sxs-lookup"><span data-stu-id="47004-169">Use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="47004-170">Export Encryption Certificate From Certificate Store</span><span class="sxs-lookup"><span data-stu-id="47004-170">Export Encryption Certificate From Certificate Store</span></span>](#Export-Encryption-Certificate-From-Certificate-Store)
2. [<span data-ttu-id="47004-171">Upload Encryption Certificate to Cloud Service</span><span class="sxs-lookup"><span data-stu-id="47004-171">Upload Encryption Certificate to Cloud Service</span></span>](#Upload-Encryption-Certificate-to-Cloud-Service)
3. [<span data-ttu-id="47004-172">Update Encryption Certificate in Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="47004-172">Update Encryption Certificate in Service Configuration File</span></span>](#Update-Encryption-Certificate-in-Service-Configuration-File)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="47004-173">Use an existing certificate in a PFX file</span><span class="sxs-lookup"><span data-stu-id="47004-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="47004-174">Upload Encryption Certificate to Cloud Service</span><span class="sxs-lookup"><span data-stu-id="47004-174">Upload Encryption Certificate to Cloud Service</span></span>](#Upload-Encryption-Certificate-to-Cloud-Service)
2. [<span data-ttu-id="47004-175">Update Encryption Certificate in Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="47004-175">Update Encryption Certificate in Service Configuration File</span></span>](#Update-Encryption-Certificate-in-Service-Configuration-File)

## <a name="the-default-configuration"></a><span data-ttu-id="47004-176">The default configuration</span><span class="sxs-lookup"><span data-stu-id="47004-176">The default configuration</span></span>
<span data-ttu-id="47004-177">The default configuration denies all access to the HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="47004-177">The default configuration denies all access to the HTTP endpoint.</span></span> <span data-ttu-id="47004-178">This is the recommended setting, since the requests to these endpoints may carry sensitive information like database credentials.</span><span class="sxs-lookup"><span data-stu-id="47004-178">This is the recommended setting, since the requests to these endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="47004-179">The default configuration allows all access to the HTTPS endpoint.</span><span class="sxs-lookup"><span data-stu-id="47004-179">The default configuration allows all access to the HTTPS endpoint.</span></span> <span data-ttu-id="47004-180">This setting may be restricted further.</span><span class="sxs-lookup"><span data-stu-id="47004-180">This setting may be restricted further.</span></span>

### <a name="changing-the-configuration"></a><span data-ttu-id="47004-181">Changing the Configuration</span><span class="sxs-lookup"><span data-stu-id="47004-181">Changing the Configuration</span></span>
<span data-ttu-id="47004-182">The group of access control rules that apply to and endpoint are configured in the **<EndpointAcls>** section in the **service configuration file**.</span><span class="sxs-lookup"><span data-stu-id="47004-182">The group of access control rules that apply to and endpoint are configured in the **<EndpointAcls>** section in the **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="47004-183">The rules in an access control group are configured in a <AccessControl name=""> section of the service configuration file.</span><span class="sxs-lookup"><span data-stu-id="47004-183">The rules in an access control group are configured in a <AccessControl name=""> section of the service configuration file.</span></span> 

<span data-ttu-id="47004-184">The format is explained in Network Access Control Lists documentation.</span><span class="sxs-lookup"><span data-stu-id="47004-184">The format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="47004-185">For example, to allow only IPs in the range 100.100.0.0 to 100.100.255.255 to access the HTTPS endpoint, the rules would look like this:</span><span class="sxs-lookup"><span data-stu-id="47004-185">For example, to allow only IPs in the range 100.100.0.0 to 100.100.255.255 to access the HTTPS endpoint, the rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="47004-186">Denial of service prevention</span><span class="sxs-lookup"><span data-stu-id="47004-186">Denial of service prevention</span></span>
<span data-ttu-id="47004-187">There are two different mechanisms supported to detect and prevent Denial of Service attacks:</span><span class="sxs-lookup"><span data-stu-id="47004-187">There are two different mechanisms supported to detect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="47004-188">Restrict number of concurrent requests per remote host (off by default)</span><span class="sxs-lookup"><span data-stu-id="47004-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="47004-189">Restrict rate of access per remote host (on by default)</span><span class="sxs-lookup"><span data-stu-id="47004-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="47004-190">These are based on the features further documented in Dynamic IP Security in IIS.</span><span class="sxs-lookup"><span data-stu-id="47004-190">These are based on the features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="47004-191">When changing this configuration beware of the following factors:</span><span class="sxs-lookup"><span data-stu-id="47004-191">When changing this configuration beware of the following factors:</span></span>

* <span data-ttu-id="47004-192">The behavior of proxies and Network Address Translation devices over the remote host information</span><span class="sxs-lookup"><span data-stu-id="47004-192">The behavior of proxies and Network Address Translation devices over the remote host information</span></span>
* <span data-ttu-id="47004-193">Each request to any resource in the web role is considered (e.g. loading scripts, images, etc)</span><span class="sxs-lookup"><span data-stu-id="47004-193">Each request to any resource in the web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="47004-194">Restricting number of concurrent accesses</span><span class="sxs-lookup"><span data-stu-id="47004-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="47004-195">The settings that configure this behavior are:</span><span class="sxs-lookup"><span data-stu-id="47004-195">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="47004-196">Change DynamicIpRestrictionDenyByConcurrentRequests to true to enable this protection.</span><span class="sxs-lookup"><span data-stu-id="47004-196">Change DynamicIpRestrictionDenyByConcurrentRequests to true to enable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="47004-197">Restricting rate of access</span><span class="sxs-lookup"><span data-stu-id="47004-197">Restricting rate of access</span></span>
<span data-ttu-id="47004-198">The settings that configure this behavior are:</span><span class="sxs-lookup"><span data-stu-id="47004-198">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-the-response-to-a-denied-request"></a><span data-ttu-id="47004-199">Configuring the response to a denied request</span><span class="sxs-lookup"><span data-stu-id="47004-199">Configuring the response to a denied request</span></span>
<span data-ttu-id="47004-200">The following setting configures the response to a denied request:</span><span class="sxs-lookup"><span data-stu-id="47004-200">The following setting configures the response to a denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="47004-201">Refer to the documentation for Dynamic IP Security in IIS for other supported values.</span><span class="sxs-lookup"><span data-stu-id="47004-201">Refer to the documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="47004-202">Operations for configuring service certificates</span><span class="sxs-lookup"><span data-stu-id="47004-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="47004-203">This topic is for reference only.</span><span class="sxs-lookup"><span data-stu-id="47004-203">This topic is for reference only.</span></span> <span data-ttu-id="47004-204">Please follow the configuration steps outlined in:</span><span class="sxs-lookup"><span data-stu-id="47004-204">Please follow the configuration steps outlined in:</span></span>

* <span data-ttu-id="47004-205">Configure the SSL certificate</span><span class="sxs-lookup"><span data-stu-id="47004-205">Configure the SSL certificate</span></span>
* <span data-ttu-id="47004-206">Configure client certificates</span><span class="sxs-lookup"><span data-stu-id="47004-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="47004-207">Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="47004-207">Create a self-signed certificate</span></span>
<span data-ttu-id="47004-208">Execute:</span><span class="sxs-lookup"><span data-stu-id="47004-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="47004-209">To customize:</span><span class="sxs-lookup"><span data-stu-id="47004-209">To customize:</span></span>

* <span data-ttu-id="47004-210">-n with the service URL.</span><span class="sxs-lookup"><span data-stu-id="47004-210">-n with the service URL.</span></span> <span data-ttu-id="47004-211">Wildcards ("CN=\*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span><span class="sxs-lookup"><span data-stu-id="47004-211">Wildcards ("CN=\*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="47004-212">-e with the certificate expiration date Create a strong password and specify it when prompted.</span><span class="sxs-lookup"><span data-stu-id="47004-212">-e with the certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="47004-213">Create PFX file for self-signed SSL certificate</span><span class="sxs-lookup"><span data-stu-id="47004-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="47004-214">Execute:</span><span class="sxs-lookup"><span data-stu-id="47004-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="47004-215">Enter password and then export certificate with these options:</span><span class="sxs-lookup"><span data-stu-id="47004-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="47004-216">Yes, export the private key</span><span class="sxs-lookup"><span data-stu-id="47004-216">Yes, export the private key</span></span>
* <span data-ttu-id="47004-217">Export all extended properties</span><span class="sxs-lookup"><span data-stu-id="47004-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="47004-218">Export SSL certificate from certificate store</span><span class="sxs-lookup"><span data-stu-id="47004-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="47004-219">Find certificate</span><span class="sxs-lookup"><span data-stu-id="47004-219">Find certificate</span></span>
* <span data-ttu-id="47004-220">Click Actions -> All tasks -> Export…</span><span class="sxs-lookup"><span data-stu-id="47004-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="47004-221">Export certificate into a .PFX file with these options:</span><span class="sxs-lookup"><span data-stu-id="47004-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="47004-222">Yes, export the private key</span><span class="sxs-lookup"><span data-stu-id="47004-222">Yes, export the private key</span></span>
  * <span data-ttu-id="47004-223">Include all certificates in the certification path if possible \*Export all extended properties</span><span class="sxs-lookup"><span data-stu-id="47004-223">Include all certificates in the certification path if possible \*Export all extended properties</span></span>

## <a name="upload-ssl-certificate-to-cloud-service"></a><span data-ttu-id="47004-224">Upload SSL certificate to cloud service</span><span class="sxs-lookup"><span data-stu-id="47004-224">Upload SSL certificate to cloud service</span></span>
<span data-ttu-id="47004-225">Upload certificate with the existing or generated .PFX file with the SSL key pair:</span><span class="sxs-lookup"><span data-stu-id="47004-225">Upload certificate with the existing or generated .PFX file with the SSL key pair:</span></span>

* <span data-ttu-id="47004-226">Enter the password protecting the private key information</span><span class="sxs-lookup"><span data-stu-id="47004-226">Enter the password protecting the private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="47004-227">Update SSL certificate in service configuration file</span><span class="sxs-lookup"><span data-stu-id="47004-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="47004-228">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span><span class="sxs-lookup"><span data-stu-id="47004-228">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="47004-229">Import SSL certification authority</span><span class="sxs-lookup"><span data-stu-id="47004-229">Import SSL certification authority</span></span>
<span data-ttu-id="47004-230">Follow these steps in all account/machine that will communicate with the service:</span><span class="sxs-lookup"><span data-stu-id="47004-230">Follow these steps in all account/machine that will communicate with the service:</span></span>

* <span data-ttu-id="47004-231">Double-click the .CER file in Windows Explorer</span><span class="sxs-lookup"><span data-stu-id="47004-231">Double-click the .CER file in Windows Explorer</span></span>
* <span data-ttu-id="47004-232">In the Certificate dialog, click Install Certificate…</span><span class="sxs-lookup"><span data-stu-id="47004-232">In the Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="47004-233">Import certificate into the Trusted Root Certification Authorities store</span><span class="sxs-lookup"><span data-stu-id="47004-233">Import certificate into the Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="47004-234">Turn off client certificate-based authentication</span><span class="sxs-lookup"><span data-stu-id="47004-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="47004-235">Only client certificate-based authentication is supported and disabling it will allow for public access to the service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span><span class="sxs-lookup"><span data-stu-id="47004-235">Only client certificate-based authentication is supported and disabling it will allow for public access to the service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="47004-236">Change these settings to false in the service configuration file to turn the feature off:</span><span class="sxs-lookup"><span data-stu-id="47004-236">Change these settings to false in the service configuration file to turn the feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="47004-237">Then, copy the same thumbprint as the SSL certificate in the CA certificate setting:</span><span class="sxs-lookup"><span data-stu-id="47004-237">Then, copy the same thumbprint as the SSL certificate in the CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="47004-238">Create a self-signed certification authority</span><span class="sxs-lookup"><span data-stu-id="47004-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="47004-239">Execute the following steps to create a self-signed certificate to act as a Certification Authority:</span><span class="sxs-lookup"><span data-stu-id="47004-239">Execute the following steps to create a self-signed certificate to act as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="47004-240">To customize it</span><span class="sxs-lookup"><span data-stu-id="47004-240">To customize it</span></span>

* <span data-ttu-id="47004-241">-e with the certification expiration date</span><span class="sxs-lookup"><span data-stu-id="47004-241">-e with the certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="47004-242">Find CA public key</span><span class="sxs-lookup"><span data-stu-id="47004-242">Find CA public key</span></span>
<span data-ttu-id="47004-243">All client certificates must have been issued by a Certification Authority trusted by the service.</span><span class="sxs-lookup"><span data-stu-id="47004-243">All client certificates must have been issued by a Certification Authority trusted by the service.</span></span> <span data-ttu-id="47004-244">Find the public key to the Certification Authority that issued the client certificates that are going to be used for authentication in order to upload it to the cloud service.</span><span class="sxs-lookup"><span data-stu-id="47004-244">Find the public key to the Certification Authority that issued the client certificates that are going to be used for authentication in order to upload it to the cloud service.</span></span>

<span data-ttu-id="47004-245">If the file with the public key is not available, export it from the certificate store:</span><span class="sxs-lookup"><span data-stu-id="47004-245">If the file with the public key is not available, export it from the certificate store:</span></span>

* <span data-ttu-id="47004-246">Find certificate</span><span class="sxs-lookup"><span data-stu-id="47004-246">Find certificate</span></span>
  * <span data-ttu-id="47004-247">Search for a client certificate issued by the same Certification Authority</span><span class="sxs-lookup"><span data-stu-id="47004-247">Search for a client certificate issued by the same Certification Authority</span></span>
* <span data-ttu-id="47004-248">Double-click the certificate.</span><span class="sxs-lookup"><span data-stu-id="47004-248">Double-click the certificate.</span></span>
* <span data-ttu-id="47004-249">Select the Certification Path tab in the Certificate dialog.</span><span class="sxs-lookup"><span data-stu-id="47004-249">Select the Certification Path tab in the Certificate dialog.</span></span>
* <span data-ttu-id="47004-250">Double-click the CA entry in the path.</span><span class="sxs-lookup"><span data-stu-id="47004-250">Double-click the CA entry in the path.</span></span>
* <span data-ttu-id="47004-251">Take notes of the certificate properties.</span><span class="sxs-lookup"><span data-stu-id="47004-251">Take notes of the certificate properties.</span></span>
* <span data-ttu-id="47004-252">Close the **Certificate** dialog.</span><span class="sxs-lookup"><span data-stu-id="47004-252">Close the **Certificate** dialog.</span></span>
* <span data-ttu-id="47004-253">Find certificate</span><span class="sxs-lookup"><span data-stu-id="47004-253">Find certificate</span></span>
  * <span data-ttu-id="47004-254">Search for the CA noted above.</span><span class="sxs-lookup"><span data-stu-id="47004-254">Search for the CA noted above.</span></span>
* <span data-ttu-id="47004-255">Click Actions -> All tasks -> Export…</span><span class="sxs-lookup"><span data-stu-id="47004-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="47004-256">Export certificate into a .CER with these options:</span><span class="sxs-lookup"><span data-stu-id="47004-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="47004-257">**No, do not export the private key**</span><span class="sxs-lookup"><span data-stu-id="47004-257">**No, do not export the private key**</span></span>
  * <span data-ttu-id="47004-258">Include all certificates in the certification path if possible.</span><span class="sxs-lookup"><span data-stu-id="47004-258">Include all certificates in the certification path if possible.</span></span>
  * <span data-ttu-id="47004-259">Export all extended properties.</span><span class="sxs-lookup"><span data-stu-id="47004-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-to-cloud-service"></a><span data-ttu-id="47004-260">Upload CA certificate to cloud service</span><span class="sxs-lookup"><span data-stu-id="47004-260">Upload CA certificate to cloud service</span></span>
<span data-ttu-id="47004-261">Upload certificate with the existing or generated .CER file with the CA public key.</span><span class="sxs-lookup"><span data-stu-id="47004-261">Upload certificate with the existing or generated .CER file with the CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="47004-262">Update CA certificate in service configuration file</span><span class="sxs-lookup"><span data-stu-id="47004-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="47004-263">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span><span class="sxs-lookup"><span data-stu-id="47004-263">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="47004-264">Update the value of the following setting with the same thumbprint:</span><span class="sxs-lookup"><span data-stu-id="47004-264">Update the value of the following setting with the same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="47004-265">Issue client certificates</span><span class="sxs-lookup"><span data-stu-id="47004-265">Issue client certificates</span></span>
<span data-ttu-id="47004-266">Each individual authorized to access the service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password to protect its private key.</span><span class="sxs-lookup"><span data-stu-id="47004-266">Each individual authorized to access the service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password to protect its private key.</span></span> 

<span data-ttu-id="47004-267">The following steps must be executed in the same machine where the self-signed CA certificate was generated and stored:</span><span class="sxs-lookup"><span data-stu-id="47004-267">The following steps must be executed in the same machine where the self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="47004-268">Customizing:</span><span class="sxs-lookup"><span data-stu-id="47004-268">Customizing:</span></span>

* <span data-ttu-id="47004-269">-n with an ID for to the client that will be authenticated with this certificate</span><span class="sxs-lookup"><span data-stu-id="47004-269">-n with an ID for to the client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="47004-270">-e with the certificate expiration date</span><span class="sxs-lookup"><span data-stu-id="47004-270">-e with the certificate expiration date</span></span>
* <span data-ttu-id="47004-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span><span class="sxs-lookup"><span data-stu-id="47004-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="47004-272">This command will prompt for a password to be created and then used once.</span><span class="sxs-lookup"><span data-stu-id="47004-272">This command will prompt for a password to be created and then used once.</span></span> <span data-ttu-id="47004-273">Use a strong password.</span><span class="sxs-lookup"><span data-stu-id="47004-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="47004-274">Create PFX files for client certificates</span><span class="sxs-lookup"><span data-stu-id="47004-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="47004-275">For each generated client certificate, execute:</span><span class="sxs-lookup"><span data-stu-id="47004-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="47004-276">Customizing:</span><span class="sxs-lookup"><span data-stu-id="47004-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the client certificate

<span data-ttu-id="47004-277">Enter password and then export certificate with these options:</span><span class="sxs-lookup"><span data-stu-id="47004-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="47004-278">Yes, export the private key</span><span class="sxs-lookup"><span data-stu-id="47004-278">Yes, export the private key</span></span>
* <span data-ttu-id="47004-279">Export all extended properties</span><span class="sxs-lookup"><span data-stu-id="47004-279">Export all extended properties</span></span>
* <span data-ttu-id="47004-280">The individual to whom this certificate is being issued should choose the export password</span><span class="sxs-lookup"><span data-stu-id="47004-280">The individual to whom this certificate is being issued should choose the export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="47004-281">Import client certificate</span><span class="sxs-lookup"><span data-stu-id="47004-281">Import client certificate</span></span>
<span data-ttu-id="47004-282">Each individual for whom a client certificate has been issued should import the key pair in the machines he/she will use to communicate with the service:</span><span class="sxs-lookup"><span data-stu-id="47004-282">Each individual for whom a client certificate has been issued should import the key pair in the machines he/she will use to communicate with the service:</span></span>

* <span data-ttu-id="47004-283">Double-click the .PFX file in Windows Explorer</span><span class="sxs-lookup"><span data-stu-id="47004-283">Double-click the .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="47004-284">Import certificate into the Personal store with at least this option:</span><span class="sxs-lookup"><span data-stu-id="47004-284">Import certificate into the Personal store with at least this option:</span></span>
  * <span data-ttu-id="47004-285">Include all extended properties checked</span><span class="sxs-lookup"><span data-stu-id="47004-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="47004-286">Copy client certificate thumbprints</span><span class="sxs-lookup"><span data-stu-id="47004-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="47004-287">Each individual for whom a client certificate has been issued must follow these steps in order to obtain the thumbprint of his/hers certificate which will be added to the service configuration file:</span><span class="sxs-lookup"><span data-stu-id="47004-287">Each individual for whom a client certificate has been issued must follow these steps in order to obtain the thumbprint of his/hers certificate which will be added to the service configuration file:</span></span>

* <span data-ttu-id="47004-288">Run certmgr.exe</span><span class="sxs-lookup"><span data-stu-id="47004-288">Run certmgr.exe</span></span>
* <span data-ttu-id="47004-289">Select the Personal tab</span><span class="sxs-lookup"><span data-stu-id="47004-289">Select the Personal tab</span></span>
* <span data-ttu-id="47004-290">Double-click the client certificate to be used for authentication</span><span class="sxs-lookup"><span data-stu-id="47004-290">Double-click the client certificate to be used for authentication</span></span>
* <span data-ttu-id="47004-291">In the Certificate dialog that opens, select the Details tab</span><span class="sxs-lookup"><span data-stu-id="47004-291">In the Certificate dialog that opens, select the Details tab</span></span>
* <span data-ttu-id="47004-292">Make sure Show is displaying All</span><span class="sxs-lookup"><span data-stu-id="47004-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="47004-293">Select the field named Thumbprint in the list</span><span class="sxs-lookup"><span data-stu-id="47004-293">Select the field named Thumbprint in the list</span></span>
* <span data-ttu-id="47004-294">Copy the value of the thumbprint \*\* Delete non-visible Unicode characters in front of the first digit \*\* Delete all spaces</span><span class="sxs-lookup"><span data-stu-id="47004-294">Copy the value of the thumbprint \*\* Delete non-visible Unicode characters in front of the first digit \*\* Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-the-service-configuration-file"></a><span data-ttu-id="47004-295">Configure Allowed clients in the service configuration file</span><span class="sxs-lookup"><span data-stu-id="47004-295">Configure Allowed clients in the service configuration file</span></span>
<span data-ttu-id="47004-296">Update the value of the following setting in the service configuration file with a comma-separated list of the thumbprints of the client certificates allowed access to the service:</span><span class="sxs-lookup"><span data-stu-id="47004-296">Update the value of the following setting in the service configuration file with a comma-separated list of the thumbprints of the client certificates allowed access to the service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="47004-297">Configure client certificate revocation check</span><span class="sxs-lookup"><span data-stu-id="47004-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="47004-298">The default setting does not check with the Certification Authority for client certificate revocation status.</span><span class="sxs-lookup"><span data-stu-id="47004-298">The default setting does not check with the Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="47004-299">To turn on the checks, if the Certification Authority which issued the client certificates supports such checks, change the following setting with one of the values defined in the X509RevocationMode Enumeration:</span><span class="sxs-lookup"><span data-stu-id="47004-299">To turn on the checks, if the Certification Authority which issued the client certificates supports such checks, change the following setting with one of the values defined in the X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="47004-300">Create PFX file for self-signed encryption certificates</span><span class="sxs-lookup"><span data-stu-id="47004-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="47004-301">For an encryption certificate, execute:</span><span class="sxs-lookup"><span data-stu-id="47004-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="47004-302">Customizing:</span><span class="sxs-lookup"><span data-stu-id="47004-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the encryption certificate

<span data-ttu-id="47004-303">Enter password and then export certificate with these options:</span><span class="sxs-lookup"><span data-stu-id="47004-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="47004-304">Yes, export the private key</span><span class="sxs-lookup"><span data-stu-id="47004-304">Yes, export the private key</span></span>
* <span data-ttu-id="47004-305">Export all extended properties</span><span class="sxs-lookup"><span data-stu-id="47004-305">Export all extended properties</span></span>
* <span data-ttu-id="47004-306">You will need the password when uploading the certificate to the cloud service.</span><span class="sxs-lookup"><span data-stu-id="47004-306">You will need the password when uploading the certificate to the cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="47004-307">Export encryption certificate from certificate store</span><span class="sxs-lookup"><span data-stu-id="47004-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="47004-308">Find certificate</span><span class="sxs-lookup"><span data-stu-id="47004-308">Find certificate</span></span>
* <span data-ttu-id="47004-309">Click Actions -> All tasks -> Export…</span><span class="sxs-lookup"><span data-stu-id="47004-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="47004-310">Export certificate into a .PFX file with these options:</span><span class="sxs-lookup"><span data-stu-id="47004-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="47004-311">Yes, export the private key</span><span class="sxs-lookup"><span data-stu-id="47004-311">Yes, export the private key</span></span>
  * <span data-ttu-id="47004-312">Include all certificates in the certification path if possible</span><span class="sxs-lookup"><span data-stu-id="47004-312">Include all certificates in the certification path if possible</span></span> 
* <span data-ttu-id="47004-313">Export all extended properties</span><span class="sxs-lookup"><span data-stu-id="47004-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-to-cloud-service"></a><span data-ttu-id="47004-314">Upload encryption certificate to cloud service</span><span class="sxs-lookup"><span data-stu-id="47004-314">Upload encryption certificate to cloud service</span></span>
<span data-ttu-id="47004-315">Upload certificate with the existing or generated .PFX file with the encryption key pair:</span><span class="sxs-lookup"><span data-stu-id="47004-315">Upload certificate with the existing or generated .PFX file with the encryption key pair:</span></span>

* <span data-ttu-id="47004-316">Enter the password protecting the private key information</span><span class="sxs-lookup"><span data-stu-id="47004-316">Enter the password protecting the private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="47004-317">Update encryption certificate in service configuration file</span><span class="sxs-lookup"><span data-stu-id="47004-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="47004-318">Update the thumbprint value of the following settings in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span><span class="sxs-lookup"><span data-stu-id="47004-318">Update the thumbprint value of the following settings in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="47004-319">Common certificate operations</span><span class="sxs-lookup"><span data-stu-id="47004-319">Common certificate operations</span></span>
* <span data-ttu-id="47004-320">Configure the SSL certificate</span><span class="sxs-lookup"><span data-stu-id="47004-320">Configure the SSL certificate</span></span>
* <span data-ttu-id="47004-321">Configure client certificates</span><span class="sxs-lookup"><span data-stu-id="47004-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="47004-322">Find certificate</span><span class="sxs-lookup"><span data-stu-id="47004-322">Find certificate</span></span>
<span data-ttu-id="47004-323">Follow these steps:</span><span class="sxs-lookup"><span data-stu-id="47004-323">Follow these steps:</span></span>

1. <span data-ttu-id="47004-324">Run mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="47004-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="47004-325">File -> Add/Remove Snap-in…</span><span class="sxs-lookup"><span data-stu-id="47004-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="47004-326">Select **Certificates**.</span><span class="sxs-lookup"><span data-stu-id="47004-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="47004-327">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="47004-327">Click **Add**.</span></span>
5. <span data-ttu-id="47004-328">Choose the certificate store location.</span><span class="sxs-lookup"><span data-stu-id="47004-328">Choose the certificate store location.</span></span>
6. <span data-ttu-id="47004-329">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="47004-329">Click **Finish**.</span></span>
7. <span data-ttu-id="47004-330">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="47004-330">Click **OK**.</span></span>
8. <span data-ttu-id="47004-331">Expand **Certificates**.</span><span class="sxs-lookup"><span data-stu-id="47004-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="47004-332">Expand the certificate store node.</span><span class="sxs-lookup"><span data-stu-id="47004-332">Expand the certificate store node.</span></span>
10. <span data-ttu-id="47004-333">Expand the Certificate child node.</span><span class="sxs-lookup"><span data-stu-id="47004-333">Expand the Certificate child node.</span></span>
11. <span data-ttu-id="47004-334">Select a certificate in the list.</span><span class="sxs-lookup"><span data-stu-id="47004-334">Select a certificate in the list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="47004-335">Export certificate</span><span class="sxs-lookup"><span data-stu-id="47004-335">Export certificate</span></span>
<span data-ttu-id="47004-336">In the **Certificate Export Wizard**:</span><span class="sxs-lookup"><span data-stu-id="47004-336">In the **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="47004-337">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="47004-337">Click **Next**.</span></span>
2. <span data-ttu-id="47004-338">Select **Yes**, then **Export the private key**.</span><span class="sxs-lookup"><span data-stu-id="47004-338">Select **Yes**, then **Export the private key**.</span></span>
3. <span data-ttu-id="47004-339">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="47004-339">Click **Next**.</span></span>
4. <span data-ttu-id="47004-340">Select the desired output file format.</span><span class="sxs-lookup"><span data-stu-id="47004-340">Select the desired output file format.</span></span>
5. <span data-ttu-id="47004-341">Check the desired options.</span><span class="sxs-lookup"><span data-stu-id="47004-341">Check the desired options.</span></span>
6. <span data-ttu-id="47004-342">Check **Password**.</span><span class="sxs-lookup"><span data-stu-id="47004-342">Check **Password**.</span></span>
7. <span data-ttu-id="47004-343">Enter a strong password and confirm it.</span><span class="sxs-lookup"><span data-stu-id="47004-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="47004-344">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="47004-344">Click **Next**.</span></span>
9. <span data-ttu-id="47004-345">Type or browse a filename where to store the certificate (use a .PFX extension).</span><span class="sxs-lookup"><span data-stu-id="47004-345">Type or browse a filename where to store the certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="47004-346">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="47004-346">Click **Next**.</span></span>
11. <span data-ttu-id="47004-347">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="47004-347">Click **Finish**.</span></span>
12. <span data-ttu-id="47004-348">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="47004-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="47004-349">Import certificate</span><span class="sxs-lookup"><span data-stu-id="47004-349">Import certificate</span></span>
<span data-ttu-id="47004-350">In the Certificate Import Wizard:</span><span class="sxs-lookup"><span data-stu-id="47004-350">In the Certificate Import Wizard:</span></span>

1. <span data-ttu-id="47004-351">Select the store location.</span><span class="sxs-lookup"><span data-stu-id="47004-351">Select the store location.</span></span>
   
   * <span data-ttu-id="47004-352">Select **Current User** if only processes running under current user will access the service</span><span class="sxs-lookup"><span data-stu-id="47004-352">Select **Current User** if only processes running under current user will access the service</span></span>
   * <span data-ttu-id="47004-353">Select **Local Machine** if other processes in this computer will access the service</span><span class="sxs-lookup"><span data-stu-id="47004-353">Select **Local Machine** if other processes in this computer will access the service</span></span>
2. <span data-ttu-id="47004-354">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="47004-354">Click **Next**.</span></span>
3. <span data-ttu-id="47004-355">If importing from a file, confirm the file path.</span><span class="sxs-lookup"><span data-stu-id="47004-355">If importing from a file, confirm the file path.</span></span>
4. <span data-ttu-id="47004-356">If importing a .PFX file:</span><span class="sxs-lookup"><span data-stu-id="47004-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="47004-357">Enter the password protecting the private key</span><span class="sxs-lookup"><span data-stu-id="47004-357">Enter the password protecting the private key</span></span>
   2. <span data-ttu-id="47004-358">Select import options</span><span class="sxs-lookup"><span data-stu-id="47004-358">Select import options</span></span>
5. <span data-ttu-id="47004-359">Select "Place" certificates in the following store</span><span class="sxs-lookup"><span data-stu-id="47004-359">Select "Place" certificates in the following store</span></span>
6. <span data-ttu-id="47004-360">Click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="47004-360">Click **Browse**.</span></span>
7. <span data-ttu-id="47004-361">Select the desired store.</span><span class="sxs-lookup"><span data-stu-id="47004-361">Select the desired store.</span></span>
8. <span data-ttu-id="47004-362">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="47004-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="47004-363">If the Trusted Root Certification Authority store was chosen, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="47004-363">If the Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="47004-364">Click **OK** on all dialog windows.</span><span class="sxs-lookup"><span data-stu-id="47004-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="47004-365">Upload certificate</span><span class="sxs-lookup"><span data-stu-id="47004-365">Upload certificate</span></span>
<span data-ttu-id="47004-366">In the [Azure Portal](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="47004-366">In the [Azure Portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="47004-367">Select **Cloud Services**.</span><span class="sxs-lookup"><span data-stu-id="47004-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="47004-368">Select the cloud service.</span><span class="sxs-lookup"><span data-stu-id="47004-368">Select the cloud service.</span></span>
3. <span data-ttu-id="47004-369">On the top menu, click **Certificates**.</span><span class="sxs-lookup"><span data-stu-id="47004-369">On the top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="47004-370">On the bottom bar, click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="47004-370">On the bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="47004-371">Select the certificate file.</span><span class="sxs-lookup"><span data-stu-id="47004-371">Select the certificate file.</span></span>
6. <span data-ttu-id="47004-372">If it is a .PFX file, enter the password for the private key.</span><span class="sxs-lookup"><span data-stu-id="47004-372">If it is a .PFX file, enter the password for the private key.</span></span>
7. <span data-ttu-id="47004-373">Once completed, copy the certificate thumbprint from the new entry in the list.</span><span class="sxs-lookup"><span data-stu-id="47004-373">Once completed, copy the certificate thumbprint from the new entry in the list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="47004-374">Other security considerations</span><span class="sxs-lookup"><span data-stu-id="47004-374">Other security considerations</span></span>
<span data-ttu-id="47004-375">The SSL settings described in this document encrypt communication between the service and its clients when the HTTPS endpoint is used.</span><span class="sxs-lookup"><span data-stu-id="47004-375">The SSL settings described in this document encrypt communication between the service and its clients when the HTTPS endpoint is used.</span></span> <span data-ttu-id="47004-376">This is important since credentials for database access and potentially other sensitive information are contained in the communication.</span><span class="sxs-lookup"><span data-stu-id="47004-376">This is important since credentials for database access and potentially other sensitive information are contained in the communication.</span></span> <span data-ttu-id="47004-377">Note, however, that the service persists internal status, including credentials, in its internal tables in the Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="47004-377">Note, however, that the service persists internal status, including credentials, in its internal tables in the Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="47004-378">That database was defined as part of the following setting in your service configuration file (.CSCFG file):</span><span class="sxs-lookup"><span data-stu-id="47004-378">That database was defined as part of the following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="47004-379">Credentials stored in this database are encrypted.</span><span class="sxs-lookup"><span data-stu-id="47004-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="47004-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up to date and secure as they both have access to the metadata database and the certificate used for encryption and decryption of stored credentials.</span><span class="sxs-lookup"><span data-stu-id="47004-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up to date and secure as they both have access to the metadata database and the certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

