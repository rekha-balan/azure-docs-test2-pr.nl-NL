---
title: Cloud Services and management certificates | Microsoft Docs
description: Learn how to create and use certificates with Microsoft Azure
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: ''
ms.assetid: fc70d00d-899b-4771-855f-44574dc4bfc6
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 7e68a738feff2eb2330b74d942b0a7f42d07df78
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550708"
---
# <a name="certificates-overview-for-azure-cloud-services"></a><span data-ttu-id="2af2d-103">Certificates overview for Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="2af2d-103">Certificates overview for Azure Cloud Services</span></span>
<span data-ttu-id="2af2d-104">Certificates are used in Azure for cloud services ([service certificates](#what-are-service-certificates)) and for authenticating with the management API ([management certificates](#what-are-management-certificates) when using the Azure classic portal and not the non-classic Azure portal).</span><span class="sxs-lookup"><span data-stu-id="2af2d-104">Certificates are used in Azure for cloud services ([service certificates](#what-are-service-certificates)) and for authenticating with the management API ([management certificates](#what-are-management-certificates) when using the Azure classic portal and not the non-classic Azure portal).</span></span> <span data-ttu-id="2af2d-105">This topic gives a general overview of both certificate types, how to [create](#create) and [deploy](#deploy) them to Azure.</span><span class="sxs-lookup"><span data-stu-id="2af2d-105">This topic gives a general overview of both certificate types, how to [create](#create) and [deploy](#deploy) them to Azure.</span></span>

<span data-ttu-id="2af2d-106">Certificates used in Azure are x.509 v3 certificates and can be signed by another trusted certificate or they can be self-signed.</span><span class="sxs-lookup"><span data-stu-id="2af2d-106">Certificates used in Azure are x.509 v3 certificates and can be signed by another trusted certificate or they can be self-signed.</span></span> <span data-ttu-id="2af2d-107">A self-signed certificate is signed by its own creator, therefore it is not trusted by default.</span><span class="sxs-lookup"><span data-stu-id="2af2d-107">A self-signed certificate is signed by its own creator, therefore it is not trusted by default.</span></span> <span data-ttu-id="2af2d-108">Most browsers can ignore this problem.</span><span class="sxs-lookup"><span data-stu-id="2af2d-108">Most browsers can ignore this problem.</span></span> <span data-ttu-id="2af2d-109">You should only use self-signed certificates when developing and testing your cloud services.</span><span class="sxs-lookup"><span data-stu-id="2af2d-109">You should only use self-signed certificates when developing and testing your cloud services.</span></span> 

<span data-ttu-id="2af2d-110">Certificates used by Azure can contain a private or a public key.</span><span class="sxs-lookup"><span data-stu-id="2af2d-110">Certificates used by Azure can contain a private or a public key.</span></span> <span data-ttu-id="2af2d-111">Certificates have a thumbprint that provides a means to identify them in an unambiguous way.</span><span class="sxs-lookup"><span data-stu-id="2af2d-111">Certificates have a thumbprint that provides a means to identify them in an unambiguous way.</span></span> <span data-ttu-id="2af2d-112">This thumbprint is used in the Azure [configuration file](cloud-services-configure-ssl-certificate.md) to identify which certificate a cloud service should use.</span><span class="sxs-lookup"><span data-stu-id="2af2d-112">This thumbprint is used in the Azure [configuration file](cloud-services-configure-ssl-certificate.md) to identify which certificate a cloud service should use.</span></span> 

## <a name="what-are-service-certificates"></a><span data-ttu-id="2af2d-113">What are service certificates?</span><span class="sxs-lookup"><span data-stu-id="2af2d-113">What are service certificates?</span></span>
<span data-ttu-id="2af2d-114">Service certificates are attached to cloud services and enable secure communication to and from the service.</span><span class="sxs-lookup"><span data-stu-id="2af2d-114">Service certificates are attached to cloud services and enable secure communication to and from the service.</span></span> <span data-ttu-id="2af2d-115">For example, if you deployed a web role, you would want to supply a certificate that can authenticate an exposed HTTPS endpoint.</span><span class="sxs-lookup"><span data-stu-id="2af2d-115">For example, if you deployed a web role, you would want to supply a certificate that can authenticate an exposed HTTPS endpoint.</span></span> <span data-ttu-id="2af2d-116">Service certificates, defined in your service definition, are automatically deployed to the virtual machine that is running an instance of your role.</span><span class="sxs-lookup"><span data-stu-id="2af2d-116">Service certificates, defined in your service definition, are automatically deployed to the virtual machine that is running an instance of your role.</span></span> 

<span data-ttu-id="2af2d-117">You can upload service certificates to Azure classic portal either using the Azure classic portal or by using the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="2af2d-117">You can upload service certificates to Azure classic portal either using the Azure classic portal or by using the classic deployment model.</span></span> <span data-ttu-id="2af2d-118">Service certificates are associated with a specific cloud service.</span><span class="sxs-lookup"><span data-stu-id="2af2d-118">Service certificates are associated with a specific cloud service.</span></span> <span data-ttu-id="2af2d-119">They are assigned to a deployment in the service definition file.</span><span class="sxs-lookup"><span data-stu-id="2af2d-119">They are assigned to a deployment in the service definition file.</span></span>

<span data-ttu-id="2af2d-120">Service certificates can be managed separately from your services, and may be managed by different individuals.</span><span class="sxs-lookup"><span data-stu-id="2af2d-120">Service certificates can be managed separately from your services, and may be managed by different individuals.</span></span> <span data-ttu-id="2af2d-121">For example, a developer may upload a service package that refers to a certificate that an IT manager has previously uploaded to Azure.</span><span class="sxs-lookup"><span data-stu-id="2af2d-121">For example, a developer may upload a service package that refers to a certificate that an IT manager has previously uploaded to Azure.</span></span> <span data-ttu-id="2af2d-122">An IT manager can manage and renew that certificate (changing the configuration of the service) without needing to upload a new service package.</span><span class="sxs-lookup"><span data-stu-id="2af2d-122">An IT manager can manage and renew that certificate (changing the configuration of the service) without needing to upload a new service package.</span></span> <span data-ttu-id="2af2d-123">Updating without a new service package is possible because the logical name, store name, and location of the certificate is in the service definition file and while the certificate thumbprint is specified in the service configuration file.</span><span class="sxs-lookup"><span data-stu-id="2af2d-123">Updating without a new service package is possible because the logical name, store name, and location of the certificate is in the service definition file and while the certificate thumbprint is specified in the service configuration file.</span></span> <span data-ttu-id="2af2d-124">To update the certificate, it's only necessary to upload a new certificate and change the thumbprint value in the service configuration file.</span><span class="sxs-lookup"><span data-stu-id="2af2d-124">To update the certificate, it's only necessary to upload a new certificate and change the thumbprint value in the service configuration file.</span></span>

>[!Note]
><span data-ttu-id="2af2d-125">The [Cloud Services FAQ](cloud-services-faq.md#certificates) article has some helpful information about certificates.</span><span class="sxs-lookup"><span data-stu-id="2af2d-125">The [Cloud Services FAQ](cloud-services-faq.md#certificates) article has some helpful information about certificates.</span></span>

## <a name="what-are-management-certificates"></a><span data-ttu-id="2af2d-126">What are management certificates?</span><span class="sxs-lookup"><span data-stu-id="2af2d-126">What are management certificates?</span></span>
<span data-ttu-id="2af2d-127">Management certificates allow you to authenticate with the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="2af2d-127">Management certificates allow you to authenticate with the classic deployment model.</span></span> <span data-ttu-id="2af2d-128">Many programs and tools (such as Visual Studio or the Azure SDK) use these certificates to automate configuration and deployment of various Azure services.</span><span class="sxs-lookup"><span data-stu-id="2af2d-128">Many programs and tools (such as Visual Studio or the Azure SDK) use these certificates to automate configuration and deployment of various Azure services.</span></span> <span data-ttu-id="2af2d-129">These are not really related to cloud services.</span><span class="sxs-lookup"><span data-stu-id="2af2d-129">These are not really related to cloud services.</span></span> 

> [!WARNING]
> <span data-ttu-id="2af2d-130">Be careful!</span><span class="sxs-lookup"><span data-stu-id="2af2d-130">Be careful!</span></span> <span data-ttu-id="2af2d-131">These types of certificates allow anyone who authenticates with them to manage the subscription they are associated with.</span><span class="sxs-lookup"><span data-stu-id="2af2d-131">These types of certificates allow anyone who authenticates with them to manage the subscription they are associated with.</span></span> 
> 
> 

### <a name="limitations"></a><span data-ttu-id="2af2d-132">Limitations</span><span class="sxs-lookup"><span data-stu-id="2af2d-132">Limitations</span></span>
<span data-ttu-id="2af2d-133">There is a limit of 100 management certificates per subscription.</span><span class="sxs-lookup"><span data-stu-id="2af2d-133">There is a limit of 100 management certificates per subscription.</span></span> <span data-ttu-id="2af2d-134">There is also a limit of 100 management certificates for all subscriptions under a specific service administrator’s user ID.</span><span class="sxs-lookup"><span data-stu-id="2af2d-134">There is also a limit of 100 management certificates for all subscriptions under a specific service administrator’s user ID.</span></span> <span data-ttu-id="2af2d-135">If the user ID for the account administrator has already been used to add 100 management certificates and there is a need for more certificates, you can add a co-administrator to add the additional certificates.</span><span class="sxs-lookup"><span data-stu-id="2af2d-135">If the user ID for the account administrator has already been used to add 100 management certificates and there is a need for more certificates, you can add a co-administrator to add the additional certificates.</span></span> 

<span data-ttu-id="2af2d-136">Before adding more than 100 certificates, see if you can reuse an existing certificate.</span><span class="sxs-lookup"><span data-stu-id="2af2d-136">Before adding more than 100 certificates, see if you can reuse an existing certificate.</span></span> <span data-ttu-id="2af2d-137">Using co-administrators adds potentially unneeded complexity to your certificate management process.</span><span class="sxs-lookup"><span data-stu-id="2af2d-137">Using co-administrators adds potentially unneeded complexity to your certificate management process.</span></span>

<a name="create"></a>
## <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="2af2d-138">Create a new self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="2af2d-138">Create a new self-signed certificate</span></span>
<span data-ttu-id="2af2d-139">You can use any tool available to create a self-signed certificate as long as they adhere to these settings:</span><span class="sxs-lookup"><span data-stu-id="2af2d-139">You can use any tool available to create a self-signed certificate as long as they adhere to these settings:</span></span>

* <span data-ttu-id="2af2d-140">An X.509 certificate.</span><span class="sxs-lookup"><span data-stu-id="2af2d-140">An X.509 certificate.</span></span>
* <span data-ttu-id="2af2d-141">Contains a private key.</span><span class="sxs-lookup"><span data-stu-id="2af2d-141">Contains a private key.</span></span>
* <span data-ttu-id="2af2d-142">Created for key exchange (.pfx file).</span><span class="sxs-lookup"><span data-stu-id="2af2d-142">Created for key exchange (.pfx file).</span></span>
* <span data-ttu-id="2af2d-143">Subject name must match the domain used to access the cloud service.</span><span class="sxs-lookup"><span data-stu-id="2af2d-143">Subject name must match the domain used to access the cloud service.</span></span>

    > <span data-ttu-id="2af2d-144">You cannot acquire an SSL certificate for the cloudapp.net (or for any Azure-related) domain; the certificate's subject name must match the custom domain name used to access your application.</span><span class="sxs-lookup"><span data-stu-id="2af2d-144">You cannot acquire an SSL certificate for the cloudapp.net (or for any Azure-related) domain; the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="2af2d-145">For example, **contoso.net**, not **contoso.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="2af2d-145">For example, **contoso.net**, not **contoso.cloudapp.net**.</span></span>

* <span data-ttu-id="2af2d-146">Minimum of 2048-bit encryption.</span><span class="sxs-lookup"><span data-stu-id="2af2d-146">Minimum of 2048-bit encryption.</span></span>
* <span data-ttu-id="2af2d-147">**Service Certificate Only**: Client-side certificate must reside in the *Personal* certificate store.</span><span class="sxs-lookup"><span data-stu-id="2af2d-147">**Service Certificate Only**: Client-side certificate must reside in the *Personal* certificate store.</span></span>

<span data-ttu-id="2af2d-148">There are two easy ways to create a certificate on Windows, with the `makecert.exe` utility, or IIS.</span><span class="sxs-lookup"><span data-stu-id="2af2d-148">There are two easy ways to create a certificate on Windows, with the `makecert.exe` utility, or IIS.</span></span>

### <a name="makecertexe"></a><span data-ttu-id="2af2d-149">Makecert.exe</span><span class="sxs-lookup"><span data-stu-id="2af2d-149">Makecert.exe</span></span>
<span data-ttu-id="2af2d-150">This utility has been deprecated and is no longer documented here.</span><span class="sxs-lookup"><span data-stu-id="2af2d-150">This utility has been deprecated and is no longer documented here.</span></span> <span data-ttu-id="2af2d-151">For more information, see [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa386968).</span><span class="sxs-lookup"><span data-stu-id="2af2d-151">For more information, see [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa386968).</span></span>

### <a name="powershell"></a><span data-ttu-id="2af2d-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2af2d-152">PowerShell</span></span>
```powershell
$cert = New-SelfSignedCertificate -DnsName yourdomain.cloudapp.net -CertStoreLocation "cert:\LocalMachine\My"
$password = ConvertTo-SecureString -String "your-password" -Force -AsPlainText
Export-PfxCertificate -Cert $cert -FilePath ".\my-cert-file.pfx" -Password $password
```

> [!NOTE]
> <span data-ttu-id="2af2d-153">If you want to use the certificate with an IP address instead of a domain, use the IP address in the -DnsName parameter.</span><span class="sxs-lookup"><span data-stu-id="2af2d-153">If you want to use the certificate with an IP address instead of a domain, use the IP address in the -DnsName parameter.</span></span>


<span data-ttu-id="2af2d-154">If you want to use this [certificate with the management portal](../azure-api-management-certs.md), export it to a **.cer** file:</span><span class="sxs-lookup"><span data-stu-id="2af2d-154">If you want to use this [certificate with the management portal](../azure-api-management-certs.md), export it to a **.cer** file:</span></span>

```powershell
Export-Certificate -Type CERT -Cert $cert -FilePath .\my-cert-file.cer
```

### <a name="internet-information-services-iis"></a><span data-ttu-id="2af2d-155">Internet Information Services (IIS)</span><span class="sxs-lookup"><span data-stu-id="2af2d-155">Internet Information Services (IIS)</span></span>
<span data-ttu-id="2af2d-156">There are many pages on the internet that cover how to do this with IIS.</span><span class="sxs-lookup"><span data-stu-id="2af2d-156">There are many pages on the internet that cover how to do this with IIS.</span></span> <span data-ttu-id="2af2d-157">[Here](https://www.sslshopper.com/article-how-to-create-a-self-signed-certificate-in-iis-7.html) is a great one I found that I think explains it well.</span><span class="sxs-lookup"><span data-stu-id="2af2d-157">[Here](https://www.sslshopper.com/article-how-to-create-a-self-signed-certificate-in-iis-7.html) is a great one I found that I think explains it well.</span></span> 

### <a name="java"></a><span data-ttu-id="2af2d-158">Java</span><span class="sxs-lookup"><span data-stu-id="2af2d-158">Java</span></span>
<span data-ttu-id="2af2d-159">You can use Java to [create a certificate](../app-service-web/java-create-azure-website-using-java-sdk.md#create-a-certificate).</span><span class="sxs-lookup"><span data-stu-id="2af2d-159">You can use Java to [create a certificate](../app-service-web/java-create-azure-website-using-java-sdk.md#create-a-certificate).</span></span>

### <a name="linux"></a><span data-ttu-id="2af2d-160">Linux</span><span class="sxs-lookup"><span data-stu-id="2af2d-160">Linux</span></span>
<span data-ttu-id="2af2d-161">[This](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article describes how to create certificates with SSH.</span><span class="sxs-lookup"><span data-stu-id="2af2d-161">[This](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article describes how to create certificates with SSH.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2af2d-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="2af2d-162">Next steps</span></span>
<span data-ttu-id="2af2d-163">[Upload your service certificate to the Azure classic portal](cloud-services-configure-ssl-certificate.md) (or the [Azure portal](cloud-services-configure-ssl-certificate-portal.md)).</span><span class="sxs-lookup"><span data-stu-id="2af2d-163">[Upload your service certificate to the Azure classic portal](cloud-services-configure-ssl-certificate.md) (or the [Azure portal](cloud-services-configure-ssl-certificate-portal.md)).</span></span>

<span data-ttu-id="2af2d-164">Upload a [management API certificate](../azure-api-management-certs.md) to the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="2af2d-164">Upload a [management API certificate](../azure-api-management-certs.md) to the Azure classic portal.</span></span> <span data-ttu-id="2af2d-165">The Azure portal does not use management certificates for authentication.</span><span class="sxs-lookup"><span data-stu-id="2af2d-165">The Azure portal does not use management certificates for authentication.</span></span>

