---
title: Split-merge security configuration | Microsoft Docs
description: Set up x409 certificates for encryption with the split/merge service for elastic scale.
metakeywords: Elastic Database certificates security
services: sql-database
manager: craigg
author: stevestein
ms.service: sql-database
ms.custom: scale out apps
ms.topic: conceptual
ms.date: 04/01/2018
ms.author: sstein
ms.openlocfilehash: bb2090aba61f32e79fe3a9fd950e6e3688193d7d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44775053"
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="ef9f6-103">Split-merge security configuration</span><span class="sxs-lookup"><span data-stu-id="ef9f6-103">Split-merge security configuration</span></span>
<span data-ttu-id="ef9f6-104">To use the Split/Merge service, you must correctly configure security.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-104">To use the Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="ef9f6-105">The service is part of the Elastic Scale feature of Microsoft Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-105">The service is part of the Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="ef9f6-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="ef9f6-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="ef9f6-107">Configuring certificates</span><span class="sxs-lookup"><span data-stu-id="ef9f6-107">Configuring certificates</span></span>
<span data-ttu-id="ef9f6-108">Certificates are configured in two ways.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="ef9f6-109">To Configure the SSL Certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-109">To Configure the SSL Certificate</span></span>](#to-configure-the-ssl-certificate)
2. [<span data-ttu-id="ef9f6-110">To Configure Client Certificates</span><span class="sxs-lookup"><span data-stu-id="ef9f6-110">To Configure Client Certificates</span></span>](#to-configure-client-certificates) 

## <a name="to-obtain-certificates"></a><span data-ttu-id="ef9f6-111">To obtain certificates</span><span class="sxs-lookup"><span data-stu-id="ef9f6-111">To obtain certificates</span></span>
<span data-ttu-id="ef9f6-112">Certificates can be obtained from public Certificate Authorities (CAs) or from the [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span><span class="sxs-lookup"><span data-stu-id="ef9f6-112">Certificates can be obtained from public Certificate Authorities (CAs) or from the [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="ef9f6-113">These are the preferred methods to obtain certificates.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-113">These are the preferred methods to obtain certificates.</span></span>

<span data-ttu-id="ef9f6-114">If those options are not available, you can generate **self-signed certificates**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-to-generate-certificates"></a><span data-ttu-id="ef9f6-115">Tools to generate certificates</span><span class="sxs-lookup"><span data-stu-id="ef9f6-115">Tools to generate certificates</span></span>
* [<span data-ttu-id="ef9f6-116">makecert.exe</span><span class="sxs-lookup"><span data-stu-id="ef9f6-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="ef9f6-117">pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="ef9f6-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="to-run-the-tools"></a><span data-ttu-id="ef9f6-118">To run the tools</span><span class="sxs-lookup"><span data-stu-id="ef9f6-118">To run the tools</span></span>
* <span data-ttu-id="ef9f6-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span><span class="sxs-lookup"><span data-stu-id="ef9f6-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="ef9f6-120">If installed, go to:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="ef9f6-121">Get the WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="ef9f6-121">Get the WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="to-configure-the-ssl-certificate"></a><span data-ttu-id="ef9f6-122">To configure the SSL certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-122">To configure the SSL certificate</span></span>
<span data-ttu-id="ef9f6-123">A SSL certificate is required to encrypt the communication and authenticate the server.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-123">A SSL certificate is required to encrypt the communication and authenticate the server.</span></span> <span data-ttu-id="ef9f6-124">Choose the most applicable of the three scenarios below, and execute all its steps:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-124">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="ef9f6-125">Create a new self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="ef9f6-126">Create a Self-Signed Certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-126">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="ef9f6-127">Create PFX file for Self-Signed SSL Certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="ef9f6-128">Upload SSL Certificate to Cloud Service</span><span class="sxs-lookup"><span data-stu-id="ef9f6-128">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
4. [<span data-ttu-id="ef9f6-129">Update SSL Certificate in Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="ef9f6-129">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)
5. [<span data-ttu-id="ef9f6-130">Import SSL Certification Authority</span><span class="sxs-lookup"><span data-stu-id="ef9f6-130">Import SSL Certification Authority</span></span>](#import-ssl-certification-authority)

### <a name="to-use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="ef9f6-131">To use an existing certificate from the certificate store</span><span class="sxs-lookup"><span data-stu-id="ef9f6-131">To use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="ef9f6-132">Export SSL Certificate From Certificate Store</span><span class="sxs-lookup"><span data-stu-id="ef9f6-132">Export SSL Certificate From Certificate Store</span></span>](#export-ssl-certificate-from-certificate-store)
2. [<span data-ttu-id="ef9f6-133">Upload SSL Certificate to Cloud Service</span><span class="sxs-lookup"><span data-stu-id="ef9f6-133">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
3. [<span data-ttu-id="ef9f6-134">Update SSL Certificate in Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="ef9f6-134">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

### <a name="to-use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="ef9f6-135">To use an existing certificate in a PFX file</span><span class="sxs-lookup"><span data-stu-id="ef9f6-135">To use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="ef9f6-136">Upload SSL Certificate to Cloud Service</span><span class="sxs-lookup"><span data-stu-id="ef9f6-136">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
2. [<span data-ttu-id="ef9f6-137">Update SSL Certificate in Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="ef9f6-137">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

## <a name="to-configure-client-certificates"></a><span data-ttu-id="ef9f6-138">To configure client certificates</span><span class="sxs-lookup"><span data-stu-id="ef9f6-138">To configure client certificates</span></span>
<span data-ttu-id="ef9f6-139">Client certificates are required in order to authenticate requests to the service.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-139">Client certificates are required in order to authenticate requests to the service.</span></span> <span data-ttu-id="ef9f6-140">Choose the most applicable of the three scenarios below, and execute all its steps:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-140">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="ef9f6-141">Turn off client certificates</span><span class="sxs-lookup"><span data-stu-id="ef9f6-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="ef9f6-142">Turn Off Client Certificate-Based Authentication</span><span class="sxs-lookup"><span data-stu-id="ef9f6-142">Turn Off Client Certificate-Based Authentication</span></span>](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="ef9f6-143">Issue new self-signed client certificates</span><span class="sxs-lookup"><span data-stu-id="ef9f6-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="ef9f6-144">Create a Self-Signed Certification Authority</span><span class="sxs-lookup"><span data-stu-id="ef9f6-144">Create a Self-Signed Certification Authority</span></span>](#create-a-self-signed-certification-authority)
2. [<span data-ttu-id="ef9f6-145">Upload CA Certificate to Cloud Service</span><span class="sxs-lookup"><span data-stu-id="ef9f6-145">Upload CA Certificate to Cloud Service</span></span>](#upload-ca-certificate-to-cloud-service)
3. [<span data-ttu-id="ef9f6-146">Update CA Certificate in Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="ef9f6-146">Update CA Certificate in Service Configuration File</span></span>](#update-ca-certificate-in-service-configuration-file)
4. [<span data-ttu-id="ef9f6-147">Issue Client Certificates</span><span class="sxs-lookup"><span data-stu-id="ef9f6-147">Issue Client Certificates</span></span>](#issue-client-certificates)
5. [<span data-ttu-id="ef9f6-148">Create PFX files for Client Certificates</span><span class="sxs-lookup"><span data-stu-id="ef9f6-148">Create PFX files for Client Certificates</span></span>](#create-pfx-files-for-client-certificates)
6. [<span data-ttu-id="ef9f6-149">Import Client Certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="ef9f6-150">Copy Client Certificate Thumbprints</span><span class="sxs-lookup"><span data-stu-id="ef9f6-150">Copy Client Certificate Thumbprints</span></span>](#copy-client-certificate-thumbprints)
8. [<span data-ttu-id="ef9f6-151">Configure Allowed Clients in the Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="ef9f6-151">Configure Allowed Clients in the Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="ef9f6-152">Use existing client certificates</span><span class="sxs-lookup"><span data-stu-id="ef9f6-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="ef9f6-153">Find CA Public Key</span><span class="sxs-lookup"><span data-stu-id="ef9f6-153">Find CA Public Key</span></span>](#find-ca-public-key)
2. [<span data-ttu-id="ef9f6-154">Upload CA Certificate to Cloud Service</span><span class="sxs-lookup"><span data-stu-id="ef9f6-154">Upload CA Certificate to Cloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="ef9f6-155">Update CA Certificate in Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="ef9f6-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="ef9f6-156">Copy Client Certificate Thumbprints</span><span class="sxs-lookup"><span data-stu-id="ef9f6-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="ef9f6-157">Configure Allowed Clients in the Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="ef9f6-157">Configure Allowed Clients in the Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)
6. [<span data-ttu-id="ef9f6-158">Configure Client Certificate Revocation Check</span><span class="sxs-lookup"><span data-stu-id="ef9f6-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="ef9f6-159">Allowed IP addresses</span><span class="sxs-lookup"><span data-stu-id="ef9f6-159">Allowed IP addresses</span></span>
<span data-ttu-id="ef9f6-160">Access to the service endpoints can be restricted to specific ranges of IP addresses.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-160">Access to the service endpoints can be restricted to specific ranges of IP addresses.</span></span>

## <a name="to-configure-encryption-for-the-store"></a><span data-ttu-id="ef9f6-161">To configure encryption for the store</span><span class="sxs-lookup"><span data-stu-id="ef9f6-161">To configure encryption for the store</span></span>
<span data-ttu-id="ef9f6-162">A certificate is required to encrypt the credentials that are stored in the metadata store.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-162">A certificate is required to encrypt the credentials that are stored in the metadata store.</span></span> <span data-ttu-id="ef9f6-163">Choose the most applicable of the three scenarios below, and execute all its steps:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-163">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="ef9f6-164">Use a new self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="ef9f6-165">Create a Self-Signed Certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-165">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="ef9f6-166">Create PFX file for Self-Signed Encryption Certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="ef9f6-167">Upload Encryption Certificate to Cloud Service</span><span class="sxs-lookup"><span data-stu-id="ef9f6-167">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
4. [<span data-ttu-id="ef9f6-168">Update Encryption Certificate in Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="ef9f6-168">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="ef9f6-169">Use an existing certificate from the certificate store</span><span class="sxs-lookup"><span data-stu-id="ef9f6-169">Use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="ef9f6-170">Export Encryption Certificate From Certificate Store</span><span class="sxs-lookup"><span data-stu-id="ef9f6-170">Export Encryption Certificate From Certificate Store</span></span>](#export-encryption-certificate-from-certificate-store)
2. [<span data-ttu-id="ef9f6-171">Upload Encryption Certificate to Cloud Service</span><span class="sxs-lookup"><span data-stu-id="ef9f6-171">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
3. [<span data-ttu-id="ef9f6-172">Update Encryption Certificate in Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="ef9f6-172">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="ef9f6-173">Use an existing certificate in a PFX file</span><span class="sxs-lookup"><span data-stu-id="ef9f6-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="ef9f6-174">Upload Encryption Certificate to Cloud Service</span><span class="sxs-lookup"><span data-stu-id="ef9f6-174">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
2. [<span data-ttu-id="ef9f6-175">Update Encryption Certificate in Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="ef9f6-175">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

## <a name="the-default-configuration"></a><span data-ttu-id="ef9f6-176">The default configuration</span><span class="sxs-lookup"><span data-stu-id="ef9f6-176">The default configuration</span></span>
<span data-ttu-id="ef9f6-177">The default configuration denies all access to the HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-177">The default configuration denies all access to the HTTP endpoint.</span></span> <span data-ttu-id="ef9f6-178">This is the recommended setting, since the requests to these endpoints may carry sensitive information like database credentials.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-178">This is the recommended setting, since the requests to these endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="ef9f6-179">The default configuration allows all access to the HTTPS endpoint.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-179">The default configuration allows all access to the HTTPS endpoint.</span></span> <span data-ttu-id="ef9f6-180">This setting may be restricted further.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-180">This setting may be restricted further.</span></span>

### <a name="changing-the-configuration"></a><span data-ttu-id="ef9f6-181">Changing the Configuration</span><span class="sxs-lookup"><span data-stu-id="ef9f6-181">Changing the Configuration</span></span>
<span data-ttu-id="ef9f6-182">The group of access control rules that apply to and endpoint are configured in the **<EndpointAcls>** section in the **service configuration file**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-182">The group of access control rules that apply to and endpoint are configured in the **<EndpointAcls>** section in the **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="ef9f6-183">The rules in an access control group are configured in a <AccessControl name=""> section of the service configuration file.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-183">The rules in an access control group are configured in a <AccessControl name=""> section of the service configuration file.</span></span> 

<span data-ttu-id="ef9f6-184">The format is explained in Network Access Control Lists documentation.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-184">The format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="ef9f6-185">For example, to allow only IPs in the range 100.100.0.0 to 100.100.255.255 to access the HTTPS endpoint, the rules would look like this:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-185">For example, to allow only IPs in the range 100.100.0.0 to 100.100.255.255 to access the HTTPS endpoint, the rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="ef9f6-186">Denial of service prevention</span><span class="sxs-lookup"><span data-stu-id="ef9f6-186">Denial of service prevention</span></span>
<span data-ttu-id="ef9f6-187">There are two different mechanisms supported to detect and prevent Denial of Service attacks:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-187">There are two different mechanisms supported to detect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="ef9f6-188">Restrict number of concurrent requests per remote host (off by default)</span><span class="sxs-lookup"><span data-stu-id="ef9f6-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="ef9f6-189">Restrict rate of access per remote host (on by default)</span><span class="sxs-lookup"><span data-stu-id="ef9f6-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="ef9f6-190">These are based on the features further documented in Dynamic IP Security in IIS.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-190">These are based on the features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="ef9f6-191">When changing this configuration beware of the following factors:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-191">When changing this configuration beware of the following factors:</span></span>

* <span data-ttu-id="ef9f6-192">The behavior of proxies and Network Address Translation devices over the remote host information</span><span class="sxs-lookup"><span data-stu-id="ef9f6-192">The behavior of proxies and Network Address Translation devices over the remote host information</span></span>
* <span data-ttu-id="ef9f6-193">Each request to any resource in the web role is considered (e.g. loading scripts, images, etc)</span><span class="sxs-lookup"><span data-stu-id="ef9f6-193">Each request to any resource in the web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="ef9f6-194">Restricting number of concurrent accesses</span><span class="sxs-lookup"><span data-stu-id="ef9f6-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="ef9f6-195">The settings that configure this behavior are:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-195">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="ef9f6-196">Change DynamicIpRestrictionDenyByConcurrentRequests to true to enable this protection.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-196">Change DynamicIpRestrictionDenyByConcurrentRequests to true to enable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="ef9f6-197">Restricting rate of access</span><span class="sxs-lookup"><span data-stu-id="ef9f6-197">Restricting rate of access</span></span>
<span data-ttu-id="ef9f6-198">The settings that configure this behavior are:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-198">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-the-response-to-a-denied-request"></a><span data-ttu-id="ef9f6-199">Configuring the response to a denied request</span><span class="sxs-lookup"><span data-stu-id="ef9f6-199">Configuring the response to a denied request</span></span>
<span data-ttu-id="ef9f6-200">The following setting configures the response to a denied request:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-200">The following setting configures the response to a denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="ef9f6-201">Refer to the documentation for Dynamic IP Security in IIS for other supported values.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-201">Refer to the documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="ef9f6-202">Operations for configuring service certificates</span><span class="sxs-lookup"><span data-stu-id="ef9f6-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="ef9f6-203">This topic is for reference only.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-203">This topic is for reference only.</span></span> <span data-ttu-id="ef9f6-204">Please follow the configuration steps outlined in:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-204">Please follow the configuration steps outlined in:</span></span>

* <span data-ttu-id="ef9f6-205">Configure the SSL certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-205">Configure the SSL certificate</span></span>
* <span data-ttu-id="ef9f6-206">Configure client certificates</span><span class="sxs-lookup"><span data-stu-id="ef9f6-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="ef9f6-207">Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-207">Create a self-signed certificate</span></span>
<span data-ttu-id="ef9f6-208">Execute:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="ef9f6-209">To customize:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-209">To customize:</span></span>

* <span data-ttu-id="ef9f6-210">-n with the service URL.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-210">-n with the service URL.</span></span> <span data-ttu-id="ef9f6-211">Wildcards ("CN=\*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-211">Wildcards ("CN=\*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="ef9f6-212">-e with the certificate expiration date Create a strong password and specify it when prompted.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-212">-e with the certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="ef9f6-213">Create PFX file for self-signed SSL certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="ef9f6-214">Execute:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="ef9f6-215">Enter password and then export certificate with these options:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="ef9f6-216">Yes, export the private key</span><span class="sxs-lookup"><span data-stu-id="ef9f6-216">Yes, export the private key</span></span>
* <span data-ttu-id="ef9f6-217">Export all extended properties</span><span class="sxs-lookup"><span data-stu-id="ef9f6-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="ef9f6-218">Export SSL certificate from certificate store</span><span class="sxs-lookup"><span data-stu-id="ef9f6-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="ef9f6-219">Find certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-219">Find certificate</span></span>
* <span data-ttu-id="ef9f6-220">Click Actions -> All tasks -> Export…</span><span class="sxs-lookup"><span data-stu-id="ef9f6-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="ef9f6-221">Export certificate into a .PFX file with these options:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="ef9f6-222">Yes, export the private key</span><span class="sxs-lookup"><span data-stu-id="ef9f6-222">Yes, export the private key</span></span>
  * <span data-ttu-id="ef9f6-223">Include all certificates in the certification path if possible \*Export all extended properties</span><span class="sxs-lookup"><span data-stu-id="ef9f6-223">Include all certificates in the certification path if possible \*Export all extended properties</span></span>

## <a name="upload-ssl-certificate-to-cloud-service"></a><span data-ttu-id="ef9f6-224">Upload SSL certificate to cloud service</span><span class="sxs-lookup"><span data-stu-id="ef9f6-224">Upload SSL certificate to cloud service</span></span>
<span data-ttu-id="ef9f6-225">Upload certificate with the existing or generated .PFX file with the SSL key pair:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-225">Upload certificate with the existing or generated .PFX file with the SSL key pair:</span></span>

* <span data-ttu-id="ef9f6-226">Enter the password protecting the private key information</span><span class="sxs-lookup"><span data-stu-id="ef9f6-226">Enter the password protecting the private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="ef9f6-227">Update SSL certificate in service configuration file</span><span class="sxs-lookup"><span data-stu-id="ef9f6-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="ef9f6-228">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-228">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="ef9f6-229">Import SSL certification authority</span><span class="sxs-lookup"><span data-stu-id="ef9f6-229">Import SSL certification authority</span></span>
<span data-ttu-id="ef9f6-230">Follow these steps in all account/machine that will communicate with the service:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-230">Follow these steps in all account/machine that will communicate with the service:</span></span>

* <span data-ttu-id="ef9f6-231">Double-click the .CER file in Windows Explorer</span><span class="sxs-lookup"><span data-stu-id="ef9f6-231">Double-click the .CER file in Windows Explorer</span></span>
* <span data-ttu-id="ef9f6-232">In the Certificate dialog, click Install Certificate…</span><span class="sxs-lookup"><span data-stu-id="ef9f6-232">In the Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="ef9f6-233">Import certificate into the Trusted Root Certification Authorities store</span><span class="sxs-lookup"><span data-stu-id="ef9f6-233">Import certificate into the Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="ef9f6-234">Turn off client certificate-based authentication</span><span class="sxs-lookup"><span data-stu-id="ef9f6-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="ef9f6-235">Only client certificate-based authentication is supported and disabling it will allow for public access to the service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span><span class="sxs-lookup"><span data-stu-id="ef9f6-235">Only client certificate-based authentication is supported and disabling it will allow for public access to the service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="ef9f6-236">Change these settings to false in the service configuration file to turn the feature off:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-236">Change these settings to false in the service configuration file to turn the feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="ef9f6-237">Then, copy the same thumbprint as the SSL certificate in the CA certificate setting:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-237">Then, copy the same thumbprint as the SSL certificate in the CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="ef9f6-238">Create a self-signed certification authority</span><span class="sxs-lookup"><span data-stu-id="ef9f6-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="ef9f6-239">Execute the following steps to create a self-signed certificate to act as a Certification Authority:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-239">Execute the following steps to create a self-signed certificate to act as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="ef9f6-240">To customize it</span><span class="sxs-lookup"><span data-stu-id="ef9f6-240">To customize it</span></span>

* <span data-ttu-id="ef9f6-241">-e with the certification expiration date</span><span class="sxs-lookup"><span data-stu-id="ef9f6-241">-e with the certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="ef9f6-242">Find CA public key</span><span class="sxs-lookup"><span data-stu-id="ef9f6-242">Find CA public key</span></span>
<span data-ttu-id="ef9f6-243">All client certificates must have been issued by a Certification Authority trusted by the service.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-243">All client certificates must have been issued by a Certification Authority trusted by the service.</span></span> <span data-ttu-id="ef9f6-244">Find the public key to the Certification Authority that issued the client certificates that are going to be used for authentication in order to upload it to the cloud service.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-244">Find the public key to the Certification Authority that issued the client certificates that are going to be used for authentication in order to upload it to the cloud service.</span></span>

<span data-ttu-id="ef9f6-245">If the file with the public key is not available, export it from the certificate store:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-245">If the file with the public key is not available, export it from the certificate store:</span></span>

* <span data-ttu-id="ef9f6-246">Find certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-246">Find certificate</span></span>
  * <span data-ttu-id="ef9f6-247">Search for a client certificate issued by the same Certification Authority</span><span class="sxs-lookup"><span data-stu-id="ef9f6-247">Search for a client certificate issued by the same Certification Authority</span></span>
* <span data-ttu-id="ef9f6-248">Double-click the certificate.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-248">Double-click the certificate.</span></span>
* <span data-ttu-id="ef9f6-249">Select the Certification Path tab in the Certificate dialog.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-249">Select the Certification Path tab in the Certificate dialog.</span></span>
* <span data-ttu-id="ef9f6-250">Double-click the CA entry in the path.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-250">Double-click the CA entry in the path.</span></span>
* <span data-ttu-id="ef9f6-251">Take notes of the certificate properties.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-251">Take notes of the certificate properties.</span></span>
* <span data-ttu-id="ef9f6-252">Close the **Certificate** dialog.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-252">Close the **Certificate** dialog.</span></span>
* <span data-ttu-id="ef9f6-253">Find certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-253">Find certificate</span></span>
  * <span data-ttu-id="ef9f6-254">Search for the CA noted above.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-254">Search for the CA noted above.</span></span>
* <span data-ttu-id="ef9f6-255">Click Actions -> All tasks -> Export…</span><span class="sxs-lookup"><span data-stu-id="ef9f6-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="ef9f6-256">Export certificate into a .CER with these options:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="ef9f6-257">**No, do not export the private key**</span><span class="sxs-lookup"><span data-stu-id="ef9f6-257">**No, do not export the private key**</span></span>
  * <span data-ttu-id="ef9f6-258">Include all certificates in the certification path if possible.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-258">Include all certificates in the certification path if possible.</span></span>
  * <span data-ttu-id="ef9f6-259">Export all extended properties.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-to-cloud-service"></a><span data-ttu-id="ef9f6-260">Upload CA certificate to cloud service</span><span class="sxs-lookup"><span data-stu-id="ef9f6-260">Upload CA certificate to cloud service</span></span>
<span data-ttu-id="ef9f6-261">Upload certificate with the existing or generated .CER file with the CA public key.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-261">Upload certificate with the existing or generated .CER file with the CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="ef9f6-262">Update CA certificate in service configuration file</span><span class="sxs-lookup"><span data-stu-id="ef9f6-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="ef9f6-263">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-263">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="ef9f6-264">Update the value of the following setting with the same thumbprint:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-264">Update the value of the following setting with the same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="ef9f6-265">Issue client certificates</span><span class="sxs-lookup"><span data-stu-id="ef9f6-265">Issue client certificates</span></span>
<span data-ttu-id="ef9f6-266">Each individual authorized to access the service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password to protect its private key.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-266">Each individual authorized to access the service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password to protect its private key.</span></span> 

<span data-ttu-id="ef9f6-267">The following steps must be executed in the same machine where the self-signed CA certificate was generated and stored:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-267">The following steps must be executed in the same machine where the self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="ef9f6-268">Customizing:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-268">Customizing:</span></span>

* <span data-ttu-id="ef9f6-269">-n with an ID for to the client that will be authenticated with this certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-269">-n with an ID for to the client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="ef9f6-270">-e with the certificate expiration date</span><span class="sxs-lookup"><span data-stu-id="ef9f6-270">-e with the certificate expiration date</span></span>
* <span data-ttu-id="ef9f6-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="ef9f6-272">This command will prompt for a password to be created and then used once.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-272">This command will prompt for a password to be created and then used once.</span></span> <span data-ttu-id="ef9f6-273">Use a strong password.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="ef9f6-274">Create PFX files for client certificates</span><span class="sxs-lookup"><span data-stu-id="ef9f6-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="ef9f6-275">For each generated client certificate, execute:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="ef9f6-276">Customizing:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the client certificate

<span data-ttu-id="ef9f6-277">Enter password and then export certificate with these options:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="ef9f6-278">Yes, export the private key</span><span class="sxs-lookup"><span data-stu-id="ef9f6-278">Yes, export the private key</span></span>
* <span data-ttu-id="ef9f6-279">Export all extended properties</span><span class="sxs-lookup"><span data-stu-id="ef9f6-279">Export all extended properties</span></span>
* <span data-ttu-id="ef9f6-280">The individual to whom this certificate is being issued should choose the export password</span><span class="sxs-lookup"><span data-stu-id="ef9f6-280">The individual to whom this certificate is being issued should choose the export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="ef9f6-281">Import client certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-281">Import client certificate</span></span>
<span data-ttu-id="ef9f6-282">Each individual for whom a client certificate has been issued should import the key pair in the machines he/she will use to communicate with the service:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-282">Each individual for whom a client certificate has been issued should import the key pair in the machines he/she will use to communicate with the service:</span></span>

* <span data-ttu-id="ef9f6-283">Double-click the .PFX file in Windows Explorer</span><span class="sxs-lookup"><span data-stu-id="ef9f6-283">Double-click the .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="ef9f6-284">Import certificate into the Personal store with at least this option:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-284">Import certificate into the Personal store with at least this option:</span></span>
  * <span data-ttu-id="ef9f6-285">Include all extended properties checked</span><span class="sxs-lookup"><span data-stu-id="ef9f6-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="ef9f6-286">Copy client certificate thumbprints</span><span class="sxs-lookup"><span data-stu-id="ef9f6-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="ef9f6-287">Each individual for whom a client certificate has been issued must follow these steps in order to obtain the thumbprint of his/hers certificate which will be added to the service configuration file:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-287">Each individual for whom a client certificate has been issued must follow these steps in order to obtain the thumbprint of his/hers certificate which will be added to the service configuration file:</span></span>

* <span data-ttu-id="ef9f6-288">Run certmgr.exe</span><span class="sxs-lookup"><span data-stu-id="ef9f6-288">Run certmgr.exe</span></span>
* <span data-ttu-id="ef9f6-289">Select the Personal tab</span><span class="sxs-lookup"><span data-stu-id="ef9f6-289">Select the Personal tab</span></span>
* <span data-ttu-id="ef9f6-290">Double-click the client certificate to be used for authentication</span><span class="sxs-lookup"><span data-stu-id="ef9f6-290">Double-click the client certificate to be used for authentication</span></span>
* <span data-ttu-id="ef9f6-291">In the Certificate dialog that opens, select the Details tab</span><span class="sxs-lookup"><span data-stu-id="ef9f6-291">In the Certificate dialog that opens, select the Details tab</span></span>
* <span data-ttu-id="ef9f6-292">Make sure Show is displaying All</span><span class="sxs-lookup"><span data-stu-id="ef9f6-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="ef9f6-293">Select the field named Thumbprint in the list</span><span class="sxs-lookup"><span data-stu-id="ef9f6-293">Select the field named Thumbprint in the list</span></span>
* <span data-ttu-id="ef9f6-294">Copy the value of the thumbprint \*\* Delete non-visible Unicode characters in front of the first digit \*\* Delete all spaces</span><span class="sxs-lookup"><span data-stu-id="ef9f6-294">Copy the value of the thumbprint \*\* Delete non-visible Unicode characters in front of the first digit \*\* Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-the-service-configuration-file"></a><span data-ttu-id="ef9f6-295">Configure Allowed clients in the service configuration file</span><span class="sxs-lookup"><span data-stu-id="ef9f6-295">Configure Allowed clients in the service configuration file</span></span>
<span data-ttu-id="ef9f6-296">Update the value of the following setting in the service configuration file with a comma-separated list of the thumbprints of the client certificates allowed access to the service:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-296">Update the value of the following setting in the service configuration file with a comma-separated list of the thumbprints of the client certificates allowed access to the service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="ef9f6-297">Configure client certificate revocation check</span><span class="sxs-lookup"><span data-stu-id="ef9f6-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="ef9f6-298">The default setting does not check with the Certification Authority for client certificate revocation status.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-298">The default setting does not check with the Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="ef9f6-299">To turn on the checks, if the Certification Authority which issued the client certificates supports such checks, change the following setting with one of the values defined in the X509RevocationMode Enumeration:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-299">To turn on the checks, if the Certification Authority which issued the client certificates supports such checks, change the following setting with one of the values defined in the X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="ef9f6-300">Create PFX file for self-signed encryption certificates</span><span class="sxs-lookup"><span data-stu-id="ef9f6-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="ef9f6-301">For an encryption certificate, execute:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="ef9f6-302">Customizing:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the encryption certificate

<span data-ttu-id="ef9f6-303">Enter password and then export certificate with these options:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="ef9f6-304">Yes, export the private key</span><span class="sxs-lookup"><span data-stu-id="ef9f6-304">Yes, export the private key</span></span>
* <span data-ttu-id="ef9f6-305">Export all extended properties</span><span class="sxs-lookup"><span data-stu-id="ef9f6-305">Export all extended properties</span></span>
* <span data-ttu-id="ef9f6-306">You will need the password when uploading the certificate to the cloud service.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-306">You will need the password when uploading the certificate to the cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="ef9f6-307">Export encryption certificate from certificate store</span><span class="sxs-lookup"><span data-stu-id="ef9f6-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="ef9f6-308">Find certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-308">Find certificate</span></span>
* <span data-ttu-id="ef9f6-309">Click Actions -> All tasks -> Export…</span><span class="sxs-lookup"><span data-stu-id="ef9f6-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="ef9f6-310">Export certificate into a .PFX file with these options:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="ef9f6-311">Yes, export the private key</span><span class="sxs-lookup"><span data-stu-id="ef9f6-311">Yes, export the private key</span></span>
  * <span data-ttu-id="ef9f6-312">Include all certificates in the certification path if possible</span><span class="sxs-lookup"><span data-stu-id="ef9f6-312">Include all certificates in the certification path if possible</span></span> 
* <span data-ttu-id="ef9f6-313">Export all extended properties</span><span class="sxs-lookup"><span data-stu-id="ef9f6-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-to-cloud-service"></a><span data-ttu-id="ef9f6-314">Upload encryption certificate to cloud service</span><span class="sxs-lookup"><span data-stu-id="ef9f6-314">Upload encryption certificate to cloud service</span></span>
<span data-ttu-id="ef9f6-315">Upload certificate with the existing or generated .PFX file with the encryption key pair:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-315">Upload certificate with the existing or generated .PFX file with the encryption key pair:</span></span>

* <span data-ttu-id="ef9f6-316">Enter the password protecting the private key information</span><span class="sxs-lookup"><span data-stu-id="ef9f6-316">Enter the password protecting the private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="ef9f6-317">Update encryption certificate in service configuration file</span><span class="sxs-lookup"><span data-stu-id="ef9f6-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="ef9f6-318">Update the thumbprint value of the following settings in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-318">Update the thumbprint value of the following settings in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="ef9f6-319">Common certificate operations</span><span class="sxs-lookup"><span data-stu-id="ef9f6-319">Common certificate operations</span></span>
* <span data-ttu-id="ef9f6-320">Configure the SSL certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-320">Configure the SSL certificate</span></span>
* <span data-ttu-id="ef9f6-321">Configure client certificates</span><span class="sxs-lookup"><span data-stu-id="ef9f6-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="ef9f6-322">Find certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-322">Find certificate</span></span>
<span data-ttu-id="ef9f6-323">Follow these steps:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-323">Follow these steps:</span></span>

1. <span data-ttu-id="ef9f6-324">Run mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="ef9f6-325">File -> Add/Remove Snap-in…</span><span class="sxs-lookup"><span data-stu-id="ef9f6-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="ef9f6-326">Select **Certificates**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="ef9f6-327">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-327">Click **Add**.</span></span>
5. <span data-ttu-id="ef9f6-328">Choose the certificate store location.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-328">Choose the certificate store location.</span></span>
6. <span data-ttu-id="ef9f6-329">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-329">Click **Finish**.</span></span>
7. <span data-ttu-id="ef9f6-330">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-330">Click **OK**.</span></span>
8. <span data-ttu-id="ef9f6-331">Expand **Certificates**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="ef9f6-332">Expand the certificate store node.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-332">Expand the certificate store node.</span></span>
10. <span data-ttu-id="ef9f6-333">Expand the Certificate child node.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-333">Expand the Certificate child node.</span></span>
11. <span data-ttu-id="ef9f6-334">Select a certificate in the list.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-334">Select a certificate in the list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="ef9f6-335">Export certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-335">Export certificate</span></span>
<span data-ttu-id="ef9f6-336">In the **Certificate Export Wizard**:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-336">In the **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="ef9f6-337">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-337">Click **Next**.</span></span>
2. <span data-ttu-id="ef9f6-338">Select **Yes**, then **Export the private key**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-338">Select **Yes**, then **Export the private key**.</span></span>
3. <span data-ttu-id="ef9f6-339">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-339">Click **Next**.</span></span>
4. <span data-ttu-id="ef9f6-340">Select the desired output file format.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-340">Select the desired output file format.</span></span>
5. <span data-ttu-id="ef9f6-341">Check the desired options.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-341">Check the desired options.</span></span>
6. <span data-ttu-id="ef9f6-342">Check **Password**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-342">Check **Password**.</span></span>
7. <span data-ttu-id="ef9f6-343">Enter a strong password and confirm it.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="ef9f6-344">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-344">Click **Next**.</span></span>
9. <span data-ttu-id="ef9f6-345">Type or browse a filename where to store the certificate (use a .PFX extension).</span><span class="sxs-lookup"><span data-stu-id="ef9f6-345">Type or browse a filename where to store the certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="ef9f6-346">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-346">Click **Next**.</span></span>
11. <span data-ttu-id="ef9f6-347">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-347">Click **Finish**.</span></span>
12. <span data-ttu-id="ef9f6-348">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="ef9f6-349">Import certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-349">Import certificate</span></span>
<span data-ttu-id="ef9f6-350">In the Certificate Import Wizard:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-350">In the Certificate Import Wizard:</span></span>

1. <span data-ttu-id="ef9f6-351">Select the store location.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-351">Select the store location.</span></span>
   
   * <span data-ttu-id="ef9f6-352">Select **Current User** if only processes running under current user will access the service</span><span class="sxs-lookup"><span data-stu-id="ef9f6-352">Select **Current User** if only processes running under current user will access the service</span></span>
   * <span data-ttu-id="ef9f6-353">Select **Local Machine** if other processes in this computer will access the service</span><span class="sxs-lookup"><span data-stu-id="ef9f6-353">Select **Local Machine** if other processes in this computer will access the service</span></span>
2. <span data-ttu-id="ef9f6-354">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-354">Click **Next**.</span></span>
3. <span data-ttu-id="ef9f6-355">If importing from a file, confirm the file path.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-355">If importing from a file, confirm the file path.</span></span>
4. <span data-ttu-id="ef9f6-356">If importing a .PFX file:</span><span class="sxs-lookup"><span data-stu-id="ef9f6-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="ef9f6-357">Enter the password protecting the private key</span><span class="sxs-lookup"><span data-stu-id="ef9f6-357">Enter the password protecting the private key</span></span>
   2. <span data-ttu-id="ef9f6-358">Select import options</span><span class="sxs-lookup"><span data-stu-id="ef9f6-358">Select import options</span></span>
5. <span data-ttu-id="ef9f6-359">Select "Place" certificates in the following store</span><span class="sxs-lookup"><span data-stu-id="ef9f6-359">Select "Place" certificates in the following store</span></span>
6. <span data-ttu-id="ef9f6-360">Click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-360">Click **Browse**.</span></span>
7. <span data-ttu-id="ef9f6-361">Select the desired store.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-361">Select the desired store.</span></span>
8. <span data-ttu-id="ef9f6-362">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="ef9f6-363">If the Trusted Root Certification Authority store was chosen, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-363">If the Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="ef9f6-364">Click **OK** on all dialog windows.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="ef9f6-365">Upload certificate</span><span class="sxs-lookup"><span data-stu-id="ef9f6-365">Upload certificate</span></span>
<span data-ttu-id="ef9f6-366">In the [Azure portal](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="ef9f6-366">In the [Azure portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="ef9f6-367">Select **Cloud Services**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="ef9f6-368">Select the cloud service.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-368">Select the cloud service.</span></span>
3. <span data-ttu-id="ef9f6-369">On the top menu, click **Certificates**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-369">On the top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="ef9f6-370">On the bottom bar, click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-370">On the bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="ef9f6-371">Select the certificate file.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-371">Select the certificate file.</span></span>
6. <span data-ttu-id="ef9f6-372">If it is a .PFX file, enter the password for the private key.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-372">If it is a .PFX file, enter the password for the private key.</span></span>
7. <span data-ttu-id="ef9f6-373">Once completed, copy the certificate thumbprint from the new entry in the list.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-373">Once completed, copy the certificate thumbprint from the new entry in the list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="ef9f6-374">Other security considerations</span><span class="sxs-lookup"><span data-stu-id="ef9f6-374">Other security considerations</span></span>
<span data-ttu-id="ef9f6-375">The SSL settings described in this document encrypt communication between the service and its clients when the HTTPS endpoint is used.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-375">The SSL settings described in this document encrypt communication between the service and its clients when the HTTPS endpoint is used.</span></span> <span data-ttu-id="ef9f6-376">This is important since credentials for database access and potentially other sensitive information are contained in the communication.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-376">This is important since credentials for database access and potentially other sensitive information are contained in the communication.</span></span> <span data-ttu-id="ef9f6-377">Note, however, that the service persists internal status, including credentials, in its internal tables in the Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-377">Note, however, that the service persists internal status, including credentials, in its internal tables in the Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="ef9f6-378">That database was defined as part of the following setting in your service configuration file (.CSCFG file):</span><span class="sxs-lookup"><span data-stu-id="ef9f6-378">That database was defined as part of the following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="ef9f6-379">Credentials stored in this database are encrypted.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="ef9f6-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up to date and secure as they both have access to the metadata database and the certificate used for encryption and decryption of stored credentials.</span><span class="sxs-lookup"><span data-stu-id="ef9f6-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up to date and secure as they both have access to the metadata database and the certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

