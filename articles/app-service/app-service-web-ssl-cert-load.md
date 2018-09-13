---
title: Use an uploaded SSL certificate in your application code in Azure App Service | Microsoft Docs
description: ''
services: app-service\web
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2017
ms.author: cephalin
ms.openlocfilehash: 87c9cd5955dda1a379733e5ad48d58f8361f0e6b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871000"
---
# <a name="use-an-ssl-certificate-in-your-application-code-in-azure-app-service"></a><span data-ttu-id="97bba-102">Use an SSL certificate in your application code in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="97bba-102">Use an SSL certificate in your application code in Azure App Service</span></span>

<span data-ttu-id="97bba-103">This how-to guide shows how to use one of SSL certificates you have uploaded or imported into your App Service app in your application code.</span><span class="sxs-lookup"><span data-stu-id="97bba-103">This how-to guide shows how to use one of SSL certificates you have uploaded or imported into your App Service app in your application code.</span></span> <span data-ttu-id="97bba-104">An example of the use case is that your app accesses an external service that requires certificate authentication.</span><span class="sxs-lookup"><span data-stu-id="97bba-104">An example of the use case is that your app accesses an external service that requires certificate authentication.</span></span> 

<span data-ttu-id="97bba-105">This approach to using SSL certificates in your code makes use of the SSL functionality in App Service, which requires your app to be in **Basic** tier or above.</span><span class="sxs-lookup"><span data-stu-id="97bba-105">This approach to using SSL certificates in your code makes use of the SSL functionality in App Service, which requires your app to be in **Basic** tier or above.</span></span> <span data-ttu-id="97bba-106">An alternative is to include the certificate file in your application directory and load it directly (see [Alternative: load certificate as a file](#file)).</span><span class="sxs-lookup"><span data-stu-id="97bba-106">An alternative is to include the certificate file in your application directory and load it directly (see [Alternative: load certificate as a file](#file)).</span></span> <span data-ttu-id="97bba-107">However, this alternative does not let you hide the private key in the certificate from the application code or the developer.</span><span class="sxs-lookup"><span data-stu-id="97bba-107">However, this alternative does not let you hide the private key in the certificate from the application code or the developer.</span></span> <span data-ttu-id="97bba-108">Furthermore, if your application code is in an open source repository, keeping a certificate with a private key in the repository is not an option.</span><span class="sxs-lookup"><span data-stu-id="97bba-108">Furthermore, if your application code is in an open source repository, keeping a certificate with a private key in the repository is not an option.</span></span>

<span data-ttu-id="97bba-109">When you let App Service manage your SSL certificates, you can maintain the certificates and your application code separately and safeguard your sensitive data.</span><span class="sxs-lookup"><span data-stu-id="97bba-109">When you let App Service manage your SSL certificates, you can maintain the certificates and your application code separately and safeguard your sensitive data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97bba-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="97bba-110">Prerequisites</span></span>

<span data-ttu-id="97bba-111">To complete this how-to guide:</span><span class="sxs-lookup"><span data-stu-id="97bba-111">To complete this how-to guide:</span></span>

- [<span data-ttu-id="97bba-112">Create an App Service app</span><span class="sxs-lookup"><span data-stu-id="97bba-112">Create an App Service app</span></span>](/azure/app-service/)
- [<span data-ttu-id="97bba-113">Map a custom DNS name to your web app</span><span class="sxs-lookup"><span data-stu-id="97bba-113">Map a custom DNS name to your web app</span></span>](app-service-web-tutorial-custom-domain.md)
- <span data-ttu-id="97bba-114">[Upload an SSL certificate](app-service-web-tutorial-custom-ssl.md) or [import an App Service Certificate](web-sites-purchase-ssl-web-site.md) to your web app</span><span class="sxs-lookup"><span data-stu-id="97bba-114">[Upload an SSL certificate](app-service-web-tutorial-custom-ssl.md) or [import an App Service Certificate](web-sites-purchase-ssl-web-site.md) to your web app</span></span>


## <a name="load-your-certificates"></a><span data-ttu-id="97bba-115">Load your certificates</span><span class="sxs-lookup"><span data-stu-id="97bba-115">Load your certificates</span></span>

<span data-ttu-id="97bba-116">To use a certificate that is uploaded to or imported into App Service, first make it accessible to your application code.</span><span class="sxs-lookup"><span data-stu-id="97bba-116">To use a certificate that is uploaded to or imported into App Service, first make it accessible to your application code.</span></span> <span data-ttu-id="97bba-117">You do this with the `WEBSITE_LOAD_CERTIFICATES` app setting.</span><span class="sxs-lookup"><span data-stu-id="97bba-117">You do this with the `WEBSITE_LOAD_CERTIFICATES` app setting.</span></span>

<span data-ttu-id="97bba-118">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, open your web app page.</span><span class="sxs-lookup"><span data-stu-id="97bba-118">In the <a href="https://portal.azure.com" target="_blank">Azure portal</a>, open your web app page.</span></span>

<span data-ttu-id="97bba-119">In the left navigation, click **SSL certificates**.</span><span class="sxs-lookup"><span data-stu-id="97bba-119">In the left navigation, click **SSL certificates**.</span></span>

![Certificate uploaded](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

<span data-ttu-id="97bba-121">All your uploaded and imported SSL certificates for this web app are shown here with their thumbprints.</span><span class="sxs-lookup"><span data-stu-id="97bba-121">All your uploaded and imported SSL certificates for this web app are shown here with their thumbprints.</span></span> <span data-ttu-id="97bba-122">Copy the thumbprint of the certificate you want to use.</span><span class="sxs-lookup"><span data-stu-id="97bba-122">Copy the thumbprint of the certificate you want to use.</span></span>

<span data-ttu-id="97bba-123">In the left navigation, click **Application settings**.</span><span class="sxs-lookup"><span data-stu-id="97bba-123">In the left navigation, click **Application settings**.</span></span>

<span data-ttu-id="97bba-124">Add an app setting called `WEBSITE_LOAD_CERTIFICATES` and set its value to the thumbprint of the certificate.</span><span class="sxs-lookup"><span data-stu-id="97bba-124">Add an app setting called `WEBSITE_LOAD_CERTIFICATES` and set its value to the thumbprint of the certificate.</span></span> <span data-ttu-id="97bba-125">To make multiple certificates accessible, use comma-separated thumbprint values.</span><span class="sxs-lookup"><span data-stu-id="97bba-125">To make multiple certificates accessible, use comma-separated thumbprint values.</span></span> <span data-ttu-id="97bba-126">To make all certificates accessible, set the value to `*`.</span><span class="sxs-lookup"><span data-stu-id="97bba-126">To make all certificates accessible, set the value to `*`.</span></span> <span data-ttu-id="97bba-127">Take note that this will place the certificate into the `CurrentUser\My` store.</span><span class="sxs-lookup"><span data-stu-id="97bba-127">Take note that this will place the certificate into the `CurrentUser\My` store.</span></span>

![Configure app setting](./media/app-service-web-ssl-cert-load/configure-app-setting.png)

<span data-ttu-id="97bba-129">When finished, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="97bba-129">When finished, click **Save**.</span></span>

<span data-ttu-id="97bba-130">The configured certificate is now ready to be used by your code.</span><span class="sxs-lookup"><span data-stu-id="97bba-130">The configured certificate is now ready to be used by your code.</span></span>

## <a name="use-certificate-in-c-code"></a><span data-ttu-id="97bba-131">Use certificate in C# code</span><span class="sxs-lookup"><span data-stu-id="97bba-131">Use certificate in C# code</span></span>

<span data-ttu-id="97bba-132">Once your certificate is accessible, you access it in C# code by the certificate thumbprint.</span><span class="sxs-lookup"><span data-stu-id="97bba-132">Once your certificate is accessible, you access it in C# code by the certificate thumbprint.</span></span> <span data-ttu-id="97bba-133">The following code loads a certificate with the thumbprint `E661583E8FABEF4C0BEF694CBC41C28FB81CD870`.</span><span class="sxs-lookup"><span data-stu-id="97bba-133">The following code loads a certificate with the thumbprint `E661583E8FABEF4C0BEF694CBC41C28FB81CD870`.</span></span>

```csharp
using System;
using System.Security.Cryptography.X509Certificates;

...
X509Store certStore = new X509Store(StoreName.My, StoreLocation.CurrentUser);
certStore.Open(OpenFlags.ReadOnly);
X509Certificate2Collection certCollection = certStore.Certificates.Find(
                            X509FindType.FindByThumbprint,
                            // Replace below with your certificate's thumbprint
                            "E661583E8FABEF4C0BEF694CBC41C28FB81CD870",
                            false);
// Get the first cert with the thumbprint
if (certCollection.Count > 0)
{
    X509Certificate2 cert = certCollection[0];
    // Use certificate
    Console.WriteLine(cert.FriendlyName);
}
certStore.Close();
...
```

<a name="file"></a>
## <a name="alternative-load-certificate-as-a-file"></a><span data-ttu-id="97bba-134">Alternative: load certificate as a file</span><span class="sxs-lookup"><span data-stu-id="97bba-134">Alternative: load certificate as a file</span></span>

<span data-ttu-id="97bba-135">This section shows how to and load a certificate file that is in your application directory.</span><span class="sxs-lookup"><span data-stu-id="97bba-135">This section shows how to and load a certificate file that is in your application directory.</span></span> 

<span data-ttu-id="97bba-136">The following C# example loads a certificate called `mycert.pfx` from the `certs` directory of your app's repository.</span><span class="sxs-lookup"><span data-stu-id="97bba-136">The following C# example loads a certificate called `mycert.pfx` from the `certs` directory of your app's repository.</span></span>

```csharp
using System;
using System.Security.Cryptography.X509Certificates;

...
// Replace the parameter with "~/<relative-path-to-cert-file>".
string certPath = Server.MapPath("~/certs/mycert.pfx");

X509Certificate2 cert = GetCertificate(certPath, signatureBlob.Thumbprint);
...
```

