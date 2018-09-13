---
title: Azure Cloud Services roles FAQ | Microsoft Docs
description: Frequently asked questions about Azure Cloud Services. Answers some common questions about certificates, web roles, and worker roles.
services: cloud-services
documentationcenter: ''
author: Thraka
manager: timlt
editor: ''
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: d887f3b31693c414254dc01dac4dbdd6d9224b6d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563155"
---
# <a name="cloud-services-faq"></a><span data-ttu-id="25214-104">Cloud Services FAQ</span><span class="sxs-lookup"><span data-stu-id="25214-104">Cloud Services FAQ</span></span>
<span data-ttu-id="25214-105">This article answers some frequently asked questions about Microsoft Azure Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="25214-105">This article answers some frequently asked questions about Microsoft Azure Cloud Services.</span></span> <span data-ttu-id="25214-106">You can also visit the [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span><span class="sxs-lookup"><span data-stu-id="25214-106">You can also visit the [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span> <span data-ttu-id="25214-107">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span><span class="sxs-lookup"><span data-stu-id="25214-107">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

## <a name="certificates"></a><span data-ttu-id="25214-108">Certificates</span><span class="sxs-lookup"><span data-stu-id="25214-108">Certificates</span></span>
### <a name="where-should-i-install-my-certificate"></a><span data-ttu-id="25214-109">Where should I install my certificate?</span><span class="sxs-lookup"><span data-stu-id="25214-109">Where should I install my certificate?</span></span>
* <span data-ttu-id="25214-110">**My**</span><span class="sxs-lookup"><span data-stu-id="25214-110">**My**</span></span>  
  <span data-ttu-id="25214-111">Application Certificate with private key (\*.pfx, \*.p12).</span><span class="sxs-lookup"><span data-stu-id="25214-111">Application Certificate with private key (\*.pfx, \*.p12).</span></span>
* <span data-ttu-id="25214-112">**CA**</span><span class="sxs-lookup"><span data-stu-id="25214-112">**CA**</span></span>  
  <span data-ttu-id="25214-113">All your intermediate certificates go in this store (Policy and Sub CAs).</span><span class="sxs-lookup"><span data-stu-id="25214-113">All your intermediate certificates go in this store (Policy and Sub CAs).</span></span>
* <span data-ttu-id="25214-114">**ROOT**</span><span class="sxs-lookup"><span data-stu-id="25214-114">**ROOT**</span></span>  
  <span data-ttu-id="25214-115">The root CA store, so your main root CA cert should go here.</span><span class="sxs-lookup"><span data-stu-id="25214-115">The root CA store, so your main root CA cert should go here.</span></span>

### <a name="i-cant-remove-expired-certificate"></a><span data-ttu-id="25214-116">I can't remove expired certificate</span><span class="sxs-lookup"><span data-stu-id="25214-116">I can't remove expired certificate</span></span>
<span data-ttu-id="25214-117">Azure prevents you from removing a certificate while it is in use.</span><span class="sxs-lookup"><span data-stu-id="25214-117">Azure prevents you from removing a certificate while it is in use.</span></span> <span data-ttu-id="25214-118">You need to either delete the deployment that uses the certificate, or update the deployment with a different or renewed certificate.</span><span class="sxs-lookup"><span data-stu-id="25214-118">You need to either delete the deployment that uses the certificate, or update the deployment with a different or renewed certificate.</span></span>

### <a name="delete-an-expired-certificate"></a><span data-ttu-id="25214-119">Delete an expired certificate</span><span class="sxs-lookup"><span data-stu-id="25214-119">Delete an expired certificate</span></span>
<span data-ttu-id="25214-120">As long as the certificate is not in use, you can use the [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet to remove a certificate.</span><span class="sxs-lookup"><span data-stu-id="25214-120">As long as the certificate is not in use, you can use the [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet to remove a certificate.</span></span>

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a><span data-ttu-id="25214-121">I have expired certificates named Windows Azure Service Management for Extensions</span><span class="sxs-lookup"><span data-stu-id="25214-121">I have expired certificates named Windows Azure Service Management for Extensions</span></span>
<span data-ttu-id="25214-122">These certificates are created whenever an extension is added to the cloud service such as the Remote Desktop extension.</span><span class="sxs-lookup"><span data-stu-id="25214-122">These certificates are created whenever an extension is added to the cloud service such as the Remote Desktop extension.</span></span> <span data-ttu-id="25214-123">These certificates are only used for encrypting and decrypting the private configuration of the extension.</span><span class="sxs-lookup"><span data-stu-id="25214-123">These certificates are only used for encrypting and decrypting the private configuration of the extension.</span></span> <span data-ttu-id="25214-124">It does not matter if these certificates expire.</span><span class="sxs-lookup"><span data-stu-id="25214-124">It does not matter if these certificates expire.</span></span> <span data-ttu-id="25214-125">The expiration date is not checked.</span><span class="sxs-lookup"><span data-stu-id="25214-125">The expiration date is not checked.</span></span>

### <a name="certificates-i-have-deleted-keep-reappearing"></a><span data-ttu-id="25214-126">Certificates I have deleted keep reappearing</span><span class="sxs-lookup"><span data-stu-id="25214-126">Certificates I have deleted keep reappearing</span></span>
<span data-ttu-id="25214-127">These keep reappearing most likely because of a tool you're using, such as Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="25214-127">These keep reappearing most likely because of a tool you're using, such as Visual Studio.</span></span> <span data-ttu-id="25214-128">Whenever you reconnect with a tool that is using a certificate, it will again be uploaded to Azure.</span><span class="sxs-lookup"><span data-stu-id="25214-128">Whenever you reconnect with a tool that is using a certificate, it will again be uploaded to Azure.</span></span>

### <a name="my-certificates-keep-disappearing"></a><span data-ttu-id="25214-129">My certificates keep disappearing</span><span class="sxs-lookup"><span data-stu-id="25214-129">My certificates keep disappearing</span></span>
<span data-ttu-id="25214-130">When the virtual machine instance recycles, all local changes are lost.</span><span class="sxs-lookup"><span data-stu-id="25214-130">When the virtual machine instance recycles, all local changes are lost.</span></span> <span data-ttu-id="25214-131">Use a [startup task](cloud-services-startup-tasks.md) to install certificates to the virtual machine each time the role starts.</span><span class="sxs-lookup"><span data-stu-id="25214-131">Use a [startup task](cloud-services-startup-tasks.md) to install certificates to the virtual machine each time the role starts.</span></span>

### <a name="i-cannot-find-my-management-certificates-in-the-portal"></a><span data-ttu-id="25214-132">I cannot find my management certificates in the portal</span><span class="sxs-lookup"><span data-stu-id="25214-132">I cannot find my management certificates in the portal</span></span>
<span data-ttu-id="25214-133">[Management certificates](../azure-api-management-certs.md) are only available in the Azure Classic Portal.</span><span class="sxs-lookup"><span data-stu-id="25214-133">[Management certificates](../azure-api-management-certs.md) are only available in the Azure Classic Portal.</span></span> <span data-ttu-id="25214-134">The current Azure portal does not use management certificates.</span><span class="sxs-lookup"><span data-stu-id="25214-134">The current Azure portal does not use management certificates.</span></span> 

### <a name="how-can-i-disable-a-management-certificate"></a><span data-ttu-id="25214-135">How can I disable a management certificate?</span><span class="sxs-lookup"><span data-stu-id="25214-135">How can I disable a management certificate?</span></span>
<span data-ttu-id="25214-136">[Management certificates](../azure-api-management-certs.md) cannot be disabled.</span><span class="sxs-lookup"><span data-stu-id="25214-136">[Management certificates](../azure-api-management-certs.md) cannot be disabled.</span></span> <span data-ttu-id="25214-137">You delete them through the Azure Classic Portal when you do not want them to be used anymore.</span><span class="sxs-lookup"><span data-stu-id="25214-137">You delete them through the Azure Classic Portal when you do not want them to be used anymore.</span></span>

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a><span data-ttu-id="25214-138">How do I create an SSL certificate for a specific IP address?</span><span class="sxs-lookup"><span data-stu-id="25214-138">How do I create an SSL certificate for a specific IP address?</span></span>
<span data-ttu-id="25214-139">Follow the directions in the [create a certificate tutorial](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="25214-139">Follow the directions in the [create a certificate tutorial](cloud-services-certs-create.md).</span></span> <span data-ttu-id="25214-140">Use the IP address as the DNS Name.</span><span class="sxs-lookup"><span data-stu-id="25214-140">Use the IP address as the DNS Name.</span></span>

## <a name="security"></a><span data-ttu-id="25214-141">Security</span><span class="sxs-lookup"><span data-stu-id="25214-141">Security</span></span>
### <a name="disable-ssl-30"></a><span data-ttu-id="25214-142">Disable SSL 3.0</span><span class="sxs-lookup"><span data-stu-id="25214-142">Disable SSL 3.0</span></span>
<span data-ttu-id="25214-143">To disable SSL 3.0 and use TLS security, create a startup task which is documented on this blog post: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span><span class="sxs-lookup"><span data-stu-id="25214-143">To disable SSL 3.0 and use TLS security, create a startup task which is documented on this blog post: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span></span>

### <a name="add-nosniff-to-your-website"></a><span data-ttu-id="25214-144">Add **nosniff** to your website</span><span class="sxs-lookup"><span data-stu-id="25214-144">Add **nosniff** to your website</span></span>
<span data-ttu-id="25214-145">To prevent clients from sniffing the MIME types, add a setting in your *web.config* file.</span><span class="sxs-lookup"><span data-stu-id="25214-145">To prevent clients from sniffing the MIME types, add a setting in your *web.config* file.</span></span>

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

<span data-ttu-id="25214-146">You can also add this as a setting in IIS.</span><span class="sxs-lookup"><span data-stu-id="25214-146">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="25214-147">Use the following command with the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span><span class="sxs-lookup"><span data-stu-id="25214-147">Use the following command with the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a><span data-ttu-id="25214-148">Customize IIS for a web role</span><span class="sxs-lookup"><span data-stu-id="25214-148">Customize IIS for a web role</span></span>
<span data-ttu-id="25214-149">Use the IIS startup script from the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span><span class="sxs-lookup"><span data-stu-id="25214-149">Use the IIS startup script from the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="scaling"></a><span data-ttu-id="25214-150">Scaling</span><span class="sxs-lookup"><span data-stu-id="25214-150">Scaling</span></span>
### <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="25214-151">I cannot scale beyond X instances</span><span class="sxs-lookup"><span data-stu-id="25214-151">I cannot scale beyond X instances</span></span>
<span data-ttu-id="25214-152">Your Azure Subscription has a limit on the number of cores you can use.</span><span class="sxs-lookup"><span data-stu-id="25214-152">Your Azure Subscription has a limit on the number of cores you can use.</span></span> <span data-ttu-id="25214-153">Scaling will not work if you have used all the cores available.</span><span class="sxs-lookup"><span data-stu-id="25214-153">Scaling will not work if you have used all the cores available.</span></span> <span data-ttu-id="25214-154">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span><span class="sxs-lookup"><span data-stu-id="25214-154">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="networking"></a><span data-ttu-id="25214-155">Networking</span><span class="sxs-lookup"><span data-stu-id="25214-155">Networking</span></span>
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="25214-156">I can't reserve an IP in a multi-VIP cloud service</span><span class="sxs-lookup"><span data-stu-id="25214-156">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="25214-157">First, make sure that the virtual machine instance that you're trying to reserve the IP for is turned on.</span><span class="sxs-lookup"><span data-stu-id="25214-157">First, make sure that the virtual machine instance that you're trying to reserve the IP for is turned on.</span></span> <span data-ttu-id="25214-158">Second, make sure that you're using Reserved IPs for bother the staging and production deployments.</span><span class="sxs-lookup"><span data-stu-id="25214-158">Second, make sure that you're using Reserved IPs for bother the staging and production deployments.</span></span> <span data-ttu-id="25214-159">**Do not** change the settings while the deployment is upgrading.</span><span class="sxs-lookup"><span data-stu-id="25214-159">**Do not** change the settings while the deployment is upgrading.</span></span>

## <a name="remote-desktop"></a><span data-ttu-id="25214-160">Remote desktop</span><span class="sxs-lookup"><span data-stu-id="25214-160">Remote desktop</span></span>
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="25214-161">How do I remote desktop when I have an NSG?</span><span class="sxs-lookup"><span data-stu-id="25214-161">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="25214-162">Add rules to the NSG that allow traffic on ports **3389** and **20000**.</span><span class="sxs-lookup"><span data-stu-id="25214-162">Add rules to the NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="25214-163">Remote Desktop uses port **3389**.</span><span class="sxs-lookup"><span data-stu-id="25214-163">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="25214-164">Cloud Service instances are load balanced, so you can't directly control which instance to connect to.</span><span class="sxs-lookup"><span data-stu-id="25214-164">Cloud Service instances are load balanced, so you can't directly control which instance to connect to.</span></span>  <span data-ttu-id="25214-165">The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.</span><span class="sxs-lookup"><span data-stu-id="25214-165">The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.</span></span>  <span data-ttu-id="25214-166">The *RemoteForwarder* and *RemoteAccess* agents require that port **20000**\* be opened, which may be blocked if you have an NSG.</span><span class="sxs-lookup"><span data-stu-id="25214-166">The *RemoteForwarder* and *RemoteAccess* agents require that port **20000**\* be opened, which may be blocked if you have an NSG.</span></span>
