---
title: Bind an existing custom SSL certificate to Azure Web Apps | Microsoft Docs
description: Learn how to bind a custom SSL certificate to your web app, mobile app backend, or API app in Azure App Service.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: ''
ms.assetid: 5d5bf588-b0bb-4c6d-8840-1b609cfb5750
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 08/24/2018
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2aca366e6a433e3e71cccb49a13638dedacc38d6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871377"
---
# <a name="tutorial-bind-an-existing-custom-ssl-certificate-to-azure-web-apps"></a><span data-ttu-id="f4ff4-103">Tutorial: Bind an existing custom SSL certificate to Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="f4ff4-103">Tutorial: Bind an existing custom SSL certificate to Azure Web Apps</span></span>

<span data-ttu-id="f4ff4-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="f4ff4-105">This tutorial shows you how to bind a custom SSL certificate that you purchased from a trusted certificate authority to [Azure Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f4ff4-105">This tutorial shows you how to bind a custom SSL certificate that you purchased from a trusted certificate authority to [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="f4ff4-106">When you're finished, you'll be able to access your web app at the HTTPS endpoint of your custom DNS domain.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-106">When you're finished, you'll be able to access your web app at the HTTPS endpoint of your custom DNS domain.</span></span>

![Web app with custom SSL certificate](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

<span data-ttu-id="f4ff4-108">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="f4ff4-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f4ff4-109">Upgrade your app's pricing tier</span><span class="sxs-lookup"><span data-stu-id="f4ff4-109">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="f4ff4-110">Bind your custom certificate to App Service</span><span class="sxs-lookup"><span data-stu-id="f4ff4-110">Bind your custom certificate to App Service</span></span>
> * <span data-ttu-id="f4ff4-111">Renew certificates</span><span class="sxs-lookup"><span data-stu-id="f4ff4-111">Renew certificates</span></span>
> * <span data-ttu-id="f4ff4-112">Enforce HTTPS</span><span class="sxs-lookup"><span data-stu-id="f4ff4-112">Enforce HTTPS</span></span>
> * <span data-ttu-id="f4ff4-113">Enforce TLS 1.1/1.2</span><span class="sxs-lookup"><span data-stu-id="f4ff4-113">Enforce TLS 1.1/1.2</span></span>
> * <span data-ttu-id="f4ff4-114">Automate TLS management with scripts</span><span class="sxs-lookup"><span data-stu-id="f4ff4-114">Automate TLS management with scripts</span></span>

> [!NOTE]
> <span data-ttu-id="f4ff4-115">If you need to get a custom SSL certificate, you can get one in the Azure portal directly and bind it to your web app.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-115">If you need to get a custom SSL certificate, you can get one in the Azure portal directly and bind it to your web app.</span></span> <span data-ttu-id="f4ff4-116">Follow the [App Service Certificates tutorial](web-sites-purchase-ssl-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="f4ff4-116">Follow the [App Service Certificates tutorial](web-sites-purchase-ssl-web-site.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4ff4-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f4ff4-117">Prerequisites</span></span>

<span data-ttu-id="f4ff4-118">To complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="f4ff4-118">To complete this tutorial:</span></span>

- [<span data-ttu-id="f4ff4-119">Create an App Service app</span><span class="sxs-lookup"><span data-stu-id="f4ff4-119">Create an App Service app</span></span>](/azure/app-service/)
- [<span data-ttu-id="f4ff4-120">Map a custom DNS name to your web app</span><span class="sxs-lookup"><span data-stu-id="f4ff4-120">Map a custom DNS name to your web app</span></span>](app-service-web-tutorial-custom-domain.md)
- <span data-ttu-id="f4ff4-121">Acquire an SSL certificate from a trusted certificate authority</span><span class="sxs-lookup"><span data-stu-id="f4ff4-121">Acquire an SSL certificate from a trusted certificate authority</span></span>
- <span data-ttu-id="f4ff4-122">Have the private key you used to sign the SSL certificate request</span><span class="sxs-lookup"><span data-stu-id="f4ff4-122">Have the private key you used to sign the SSL certificate request</span></span>

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a><span data-ttu-id="f4ff4-123">Requirements for your SSL certificate</span><span class="sxs-lookup"><span data-stu-id="f4ff4-123">Requirements for your SSL certificate</span></span>

<span data-ttu-id="f4ff4-124">To use a certificate in App Service, the certificate must meet all the following requirements:</span><span class="sxs-lookup"><span data-stu-id="f4ff4-124">To use a certificate in App Service, the certificate must meet all the following requirements:</span></span>

* <span data-ttu-id="f4ff4-125">Signed by a trusted certificate authority</span><span class="sxs-lookup"><span data-stu-id="f4ff4-125">Signed by a trusted certificate authority</span></span>
* <span data-ttu-id="f4ff4-126">Exported as a password-protected PFX file</span><span class="sxs-lookup"><span data-stu-id="f4ff4-126">Exported as a password-protected PFX file</span></span>
* <span data-ttu-id="f4ff4-127">Contains private key at least 2048 bits long</span><span class="sxs-lookup"><span data-stu-id="f4ff4-127">Contains private key at least 2048 bits long</span></span>
* <span data-ttu-id="f4ff4-128">Contains all intermediate certificates in the certificate chain</span><span class="sxs-lookup"><span data-stu-id="f4ff4-128">Contains all intermediate certificates in the certificate chain</span></span>

> [!NOTE]
> <span data-ttu-id="f4ff4-129">**Elliptic Curve Cryptography (ECC) certificates** can work with App Service but are not covered by this article.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-129">**Elliptic Curve Cryptography (ECC) certificates** can work with App Service but are not covered by this article.</span></span> <span data-ttu-id="f4ff4-130">Work with your certificate authority on the exact steps to create ECC certificates.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-130">Work with your certificate authority on the exact steps to create ECC certificates.</span></span>

## <a name="prepare-your-web-app"></a><span data-ttu-id="f4ff4-131">Prepare your web app</span><span class="sxs-lookup"><span data-stu-id="f4ff4-131">Prepare your web app</span></span>

<span data-ttu-id="f4ff4-132">To bind a custom SSL certificate to your web app, your [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in the **Basic**, **Standard**, or **Premium** tier.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-132">To bind a custom SSL certificate to your web app, your [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in the **Basic**, **Standard**, or **Premium** tier.</span></span> <span data-ttu-id="f4ff4-133">In this step, you make sure that your web app is in the supported pricing tier.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-133">In this step, you make sure that your web app is in the supported pricing tier.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="f4ff4-134">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="f4ff4-134">Log in to Azure</span></span>

<span data-ttu-id="f4ff4-135">Open the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f4ff4-135">Open the [Azure portal](https://portal.azure.com).</span></span>

### <a name="navigate-to-your-web-app"></a><span data-ttu-id="f4ff4-136">Navigate to your web app</span><span class="sxs-lookup"><span data-stu-id="f4ff4-136">Navigate to your web app</span></span>

<span data-ttu-id="f4ff4-137">From the left menu, click **App Services**, and then click the name of your web app.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-137">From the left menu, click **App Services**, and then click the name of your web app.</span></span>

![Select web app](./media/app-service-web-tutorial-custom-ssl/select-app.png)

<span data-ttu-id="f4ff4-139">You have landed in the management page of your web app.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-139">You have landed in the management page of your web app.</span></span>  

### <a name="check-the-pricing-tier"></a><span data-ttu-id="f4ff4-140">Check the pricing tier</span><span class="sxs-lookup"><span data-stu-id="f4ff4-140">Check the pricing tier</span></span>

<span data-ttu-id="f4ff4-141">In the left-hand navigation of your web app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-141">In the left-hand navigation of your web app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Scale-up menu](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

<span data-ttu-id="f4ff4-143">Check to make sure that your web app is not in the **F1** or **D1** tier.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-143">Check to make sure that your web app is not in the **F1** or **D1** tier.</span></span> <span data-ttu-id="f4ff4-144">Your web app's current tier is highlighted by a dark blue box.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-144">Your web app's current tier is highlighted by a dark blue box.</span></span>

![Check pricing tier](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

<span data-ttu-id="f4ff4-146">Custom SSL is not supported in the **F1** or **D1** tier.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-146">Custom SSL is not supported in the **F1** or **D1** tier.</span></span> <span data-ttu-id="f4ff4-147">If you need to scale up, follow the steps in the next section.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-147">If you need to scale up, follow the steps in the next section.</span></span> <span data-ttu-id="f4ff4-148">Otherwise, close the **Scale up** page and skip to [Upload and bind your SSL certificate](#upload).</span><span class="sxs-lookup"><span data-stu-id="f4ff4-148">Otherwise, close the **Scale up** page and skip to [Upload and bind your SSL certificate](#upload).</span></span>

### <a name="scale-up-your-app-service-plan"></a><span data-ttu-id="f4ff4-149">Scale up your App Service plan</span><span class="sxs-lookup"><span data-stu-id="f4ff4-149">Scale up your App Service plan</span></span>

<span data-ttu-id="f4ff4-150">Select any of the non-free tiers (**B1**, **B2**, **B3**, or any tier in the **Production** category).</span><span class="sxs-lookup"><span data-stu-id="f4ff4-150">Select any of the non-free tiers (**B1**, **B2**, **B3**, or any tier in the **Production** category).</span></span> <span data-ttu-id="f4ff4-151">For additional options, click **See additional options**.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-151">For additional options, click **See additional options**.</span></span>

<span data-ttu-id="f4ff4-152">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-152">Click **Apply**.</span></span>

![Choose pricing tier](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

<span data-ttu-id="f4ff4-154">When you see the following notification, the scale operation is complete.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-154">When you see the following notification, the scale operation is complete.</span></span>

![Scale up notification](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a><span data-ttu-id="f4ff4-156">Bind your SSL certificate</span><span class="sxs-lookup"><span data-stu-id="f4ff4-156">Bind your SSL certificate</span></span>

<span data-ttu-id="f4ff4-157">You are ready to upload your SSL certificate to your web app.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-157">You are ready to upload your SSL certificate to your web app.</span></span>

### <a name="merge-intermediate-certificates"></a><span data-ttu-id="f4ff4-158">Merge intermediate certificates</span><span class="sxs-lookup"><span data-stu-id="f4ff4-158">Merge intermediate certificates</span></span>

<span data-ttu-id="f4ff4-159">If your certificate authority gives you multiple certificates in the certificate chain, you need to merge the certificates in order.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-159">If your certificate authority gives you multiple certificates in the certificate chain, you need to merge the certificates in order.</span></span> 

<span data-ttu-id="f4ff4-160">To do this, open each certificate you received in a text editor.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-160">To do this, open each certificate you received in a text editor.</span></span> 

<span data-ttu-id="f4ff4-161">Create a file for the merged certificate, called _mergedcertificate.crt_.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-161">Create a file for the merged certificate, called _mergedcertificate.crt_.</span></span> <span data-ttu-id="f4ff4-162">In a text editor, copy the content of each certificate into this file.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-162">In a text editor, copy the content of each certificate into this file.</span></span> <span data-ttu-id="f4ff4-163">The order of your certificates should follow the order in the certificate chain, beginning with your certificate and ending with the root certificate.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-163">The order of your certificates should follow the order in the certificate chain, beginning with your certificate and ending with the root certificate.</span></span> <span data-ttu-id="f4ff4-164">It looks like the following example:</span><span class="sxs-lookup"><span data-stu-id="f4ff4-164">It looks like the following example:</span></span>

```
-----BEGIN CERTIFICATE-----
<your entire Base64 encoded SSL certificate>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<The entire Base64 encoded intermediate certificate 1>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<The entire Base64 encoded intermediate certificate 2>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<The entire Base64 encoded root certificate>
-----END CERTIFICATE-----
```

### <a name="export-certificate-to-pfx"></a><span data-ttu-id="f4ff4-165">Export certificate to PFX</span><span class="sxs-lookup"><span data-stu-id="f4ff4-165">Export certificate to PFX</span></span>

<span data-ttu-id="f4ff4-166">Export your merged SSL certificate with the private key that your certificate request was generated with.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-166">Export your merged SSL certificate with the private key that your certificate request was generated with.</span></span>

<span data-ttu-id="f4ff4-167">If you generated your certificate request using OpenSSL, then you have created a private key file.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-167">If you generated your certificate request using OpenSSL, then you have created a private key file.</span></span> <span data-ttu-id="f4ff4-168">To export your certificate to PFX, run the following command.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-168">To export your certificate to PFX, run the following command.</span></span> <span data-ttu-id="f4ff4-169">Replace the placeholders _&lt;private-key-file>_ and _&lt;merged-certificate-file>_ with the paths to your private key and your merged certificate file.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-169">Replace the placeholders _&lt;private-key-file>_ and _&lt;merged-certificate-file>_ with the paths to your private key and your merged certificate file.</span></span>

```bash
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

<span data-ttu-id="f4ff4-170">When prompted, define an export password.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-170">When prompted, define an export password.</span></span> <span data-ttu-id="f4ff4-171">You'll use this password when uploading your SSL certificate to App Service later.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-171">You'll use this password when uploading your SSL certificate to App Service later.</span></span>

<span data-ttu-id="f4ff4-172">If you used IIS or _Certreq.exe_ to generate your certificate request, install the certificate to your local machine, and then [export the certificate to PFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="f4ff4-172">If you used IIS or _Certreq.exe_ to generate your certificate request, install the certificate to your local machine, and then [export the certificate to PFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span></span>

### <a name="upload-your-ssl-certificate"></a><span data-ttu-id="f4ff4-173">Upload your SSL certificate</span><span class="sxs-lookup"><span data-stu-id="f4ff4-173">Upload your SSL certificate</span></span>

<span data-ttu-id="f4ff4-174">To upload your SSL certificate, click **SSL settings** in the left navigation of your web app.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-174">To upload your SSL certificate, click **SSL settings** in the left navigation of your web app.</span></span>

<span data-ttu-id="f4ff4-175">Click **Upload Certificate**.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-175">Click **Upload Certificate**.</span></span> 

<span data-ttu-id="f4ff4-176">In **PFX Certificate File**, select your PFX file.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-176">In **PFX Certificate File**, select your PFX file.</span></span> <span data-ttu-id="f4ff4-177">In **Certificate password**, type the password that you created when you exported the PFX file.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-177">In **Certificate password**, type the password that you created when you exported the PFX file.</span></span>

<span data-ttu-id="f4ff4-178">Click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-178">Click **Upload**.</span></span>

![Upload certificate](./media/app-service-web-tutorial-custom-ssl/upload-certificate-private1.png)

<span data-ttu-id="f4ff4-180">When App Service finishes uploading your certificate, it appears in the **SSL settings** page.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-180">When App Service finishes uploading your certificate, it appears in the **SSL settings** page.</span></span>

![Certificate uploaded](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a><span data-ttu-id="f4ff4-182">Bind your SSL certificate</span><span class="sxs-lookup"><span data-stu-id="f4ff4-182">Bind your SSL certificate</span></span>

<span data-ttu-id="f4ff4-183">In the **SSL bindings** section, click **Add binding**.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-183">In the **SSL bindings** section, click **Add binding**.</span></span>

<span data-ttu-id="f4ff4-184">In the **Add SSL Binding** page, use the dropdowns to select the domain name to secure, and the certificate to use.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-184">In the **Add SSL Binding** page, use the dropdowns to select the domain name to secure, and the certificate to use.</span></span>

> [!NOTE]
> <span data-ttu-id="f4ff4-185">If you have uploaded your certificate but don't see the domain name(s) in the **Hostname** dropdown, try refreshing the browser page.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-185">If you have uploaded your certificate but don't see the domain name(s) in the **Hostname** dropdown, try refreshing the browser page.</span></span>
>
>

<span data-ttu-id="f4ff4-186">In **SSL Type**, select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP-based SSL.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-186">In **SSL Type**, select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP-based SSL.</span></span>

- <span data-ttu-id="f4ff4-187">**SNI-based SSL** - Multiple SNI-based SSL bindings may be added.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-187">**SNI-based SSL** - Multiple SNI-based SSL bindings may be added.</span></span> <span data-ttu-id="f4ff4-188">This option allows multiple SSL certificates to secure multiple domains on the same IP address.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-188">This option allows multiple SSL certificates to secure multiple domains on the same IP address.</span></span> <span data-ttu-id="f4ff4-189">Most modern browsers (including Internet Explorer, Chrome, Firefox, and Opera) support SNI (find more comprehensive browser support information at [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)).</span><span class="sxs-lookup"><span data-stu-id="f4ff4-189">Most modern browsers (including Internet Explorer, Chrome, Firefox, and Opera) support SNI (find more comprehensive browser support information at [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)).</span></span>
- <span data-ttu-id="f4ff4-190">**IP-based SSL** - Only one IP-based SSL binding may be added.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-190">**IP-based SSL** - Only one IP-based SSL binding may be added.</span></span> <span data-ttu-id="f4ff4-191">This option allows only one SSL certificate to secure a dedicated public IP address.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-191">This option allows only one SSL certificate to secure a dedicated public IP address.</span></span> <span data-ttu-id="f4ff4-192">To secure multiple domains, you must secure them all using the same SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-192">To secure multiple domains, you must secure them all using the same SSL certificate.</span></span> <span data-ttu-id="f4ff4-193">This is the traditional option for SSL binding.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-193">This is the traditional option for SSL binding.</span></span>

<span data-ttu-id="f4ff4-194">Click **Add Binding**.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-194">Click **Add Binding**.</span></span>

![Bind SSL certificate](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

<span data-ttu-id="f4ff4-196">When App Service finishes uploading your certificate, it appears in the **SSL bindings** sections.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-196">When App Service finishes uploading your certificate, it appears in the **SSL bindings** sections.</span></span>

![Certificate bound to web app](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a><span data-ttu-id="f4ff4-198">Remap A record for IP SSL</span><span class="sxs-lookup"><span data-stu-id="f4ff4-198">Remap A record for IP SSL</span></span>

<span data-ttu-id="f4ff4-199">If you don't use IP-based SSL in your web app, skip to [Test HTTPS for your custom domain](#test).</span><span class="sxs-lookup"><span data-stu-id="f4ff4-199">If you don't use IP-based SSL in your web app, skip to [Test HTTPS for your custom domain](#test).</span></span>

<span data-ttu-id="f4ff4-200">By default, your web app uses a shared public IP address.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-200">By default, your web app uses a shared public IP address.</span></span> <span data-ttu-id="f4ff4-201">When you bind a certificate with IP-based SSL, App Service creates a new, dedicated IP address for your web app.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-201">When you bind a certificate with IP-based SSL, App Service creates a new, dedicated IP address for your web app.</span></span>

<span data-ttu-id="f4ff4-202">If you have mapped an A record to your web app, update your domain registry with this new, dedicated IP address.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-202">If you have mapped an A record to your web app, update your domain registry with this new, dedicated IP address.</span></span>

<span data-ttu-id="f4ff4-203">Your web app's **Custom domain** page is updated with the new, dedicated IP address.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-203">Your web app's **Custom domain** page is updated with the new, dedicated IP address.</span></span> <span data-ttu-id="f4ff4-204">[Copy this IP address](app-service-web-tutorial-custom-domain.md#info), then [remap the A record](app-service-web-tutorial-custom-domain.md#map-an-a-record) to this new IP address.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-204">[Copy this IP address](app-service-web-tutorial-custom-domain.md#info), then [remap the A record](app-service-web-tutorial-custom-domain.md#map-an-a-record) to this new IP address.</span></span>

<a name="test"></a>

## <a name="test-https"></a><span data-ttu-id="f4ff4-205">Test HTTPS</span><span class="sxs-lookup"><span data-stu-id="f4ff4-205">Test HTTPS</span></span>

<span data-ttu-id="f4ff4-206">All that's left to do now is to make sure that HTTPS works for your custom domain.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-206">All that's left to do now is to make sure that HTTPS works for your custom domain.</span></span> <span data-ttu-id="f4ff4-207">In various browsers, browse to `https://<your.custom.domain>` to see that it serves up your web app.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-207">In various browsers, browse to `https://<your.custom.domain>` to see that it serves up your web app.</span></span>

![Portal navigation to Azure app](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> <span data-ttu-id="f4ff4-209">If your web app gives you certificate validation errors, you're probably using a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-209">If your web app gives you certificate validation errors, you're probably using a self-signed certificate.</span></span>
>
> <span data-ttu-id="f4ff4-210">If that's not the case, you may have left out intermediate certificates when you export your certificate to the PFX file.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-210">If that's not the case, you may have left out intermediate certificates when you export your certificate to the PFX file.</span></span>

<a name="bkmk_enforce"></a>

## <a name="renew-certificates"></a><span data-ttu-id="f4ff4-211">Renew certificates</span><span class="sxs-lookup"><span data-stu-id="f4ff4-211">Renew certificates</span></span>

<span data-ttu-id="f4ff4-212">Your inbound IP address can change when you delete a binding, even if that binding is IP-based.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-212">Your inbound IP address can change when you delete a binding, even if that binding is IP-based.</span></span> <span data-ttu-id="f4ff4-213">This is especially important when you renew a certificate that's already in an IP-based binding.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-213">This is especially important when you renew a certificate that's already in an IP-based binding.</span></span> <span data-ttu-id="f4ff4-214">To avoid a change in your app's IP address, follow these steps in order:</span><span class="sxs-lookup"><span data-stu-id="f4ff4-214">To avoid a change in your app's IP address, follow these steps in order:</span></span>

1. <span data-ttu-id="f4ff4-215">Upload the new certificate.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-215">Upload the new certificate.</span></span>
2. <span data-ttu-id="f4ff4-216">Bind the new certificate to the custom domain you want without deleting the old one.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-216">Bind the new certificate to the custom domain you want without deleting the old one.</span></span> <span data-ttu-id="f4ff4-217">This action replaces the binding instead of removing the old one.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-217">This action replaces the binding instead of removing the old one.</span></span>
3. <span data-ttu-id="f4ff4-218">Delete the old certificate.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-218">Delete the old certificate.</span></span> 

## <a name="enforce-https"></a><span data-ttu-id="f4ff4-219">Enforce HTTPS</span><span class="sxs-lookup"><span data-stu-id="f4ff4-219">Enforce HTTPS</span></span>

<span data-ttu-id="f4ff4-220">By default, anyone can still access your web app using HTTP.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-220">By default, anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="f4ff4-221">You can redirect all HTTP requests to the HTTPS port.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-221">You can redirect all HTTP requests to the HTTPS port.</span></span>

<span data-ttu-id="f4ff4-222">In your web app page, in the left navigation, select **SSL settings**.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-222">In your web app page, in the left navigation, select **SSL settings**.</span></span> <span data-ttu-id="f4ff4-223">Then, in **HTTPS Only**, select **On**.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-223">Then, in **HTTPS Only**, select **On**.</span></span>

![Enforce HTTPS](./media/app-service-web-tutorial-custom-ssl/enforce-https.png)

<span data-ttu-id="f4ff4-225">When the operation is complete, navigate to any of the HTTP URLs that point to your app.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-225">When the operation is complete, navigate to any of the HTTP URLs that point to your app.</span></span> <span data-ttu-id="f4ff4-226">For example:</span><span class="sxs-lookup"><span data-stu-id="f4ff4-226">For example:</span></span>

- `http://<app_name>.azurewebsites.net`
- `http://contoso.com`
- `http://www.contoso.com`

## <a name="enforce-tls-versions"></a><span data-ttu-id="f4ff4-227">Enforce TLS versions</span><span class="sxs-lookup"><span data-stu-id="f4ff4-227">Enforce TLS versions</span></span>

<span data-ttu-id="f4ff4-228">Your app allows [TLS](https://wikipedia.org/wiki/Transport_Layer_Security) 1.2 by default, which is the recommended TLS level by industry standards, such as [PCI DSS](https://wikipedia.org/wiki/Payment_Card_Industry_Data_Security_Standard).</span><span class="sxs-lookup"><span data-stu-id="f4ff4-228">Your app allows [TLS](https://wikipedia.org/wiki/Transport_Layer_Security) 1.2 by default, which is the recommended TLS level by industry standards, such as [PCI DSS](https://wikipedia.org/wiki/Payment_Card_Industry_Data_Security_Standard).</span></span> <span data-ttu-id="f4ff4-229">To enforce different TLS versions, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="f4ff4-229">To enforce different TLS versions, follow these steps:</span></span>

<span data-ttu-id="f4ff4-230">In your web app page, in the left navigation, select **SSL settings**.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-230">In your web app page, in the left navigation, select **SSL settings**.</span></span> <span data-ttu-id="f4ff4-231">Then, in **TLS version**, select the minimum TLS version you want.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-231">Then, in **TLS version**, select the minimum TLS version you want.</span></span> <span data-ttu-id="f4ff4-232">This setting controls the inbound calls only.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-232">This setting controls the inbound calls only.</span></span> 

![Enforce TLS 1.1 or 1.2](./media/app-service-web-tutorial-custom-ssl/enforce-tls1.2.png)

<span data-ttu-id="f4ff4-234">When the operation is complete, your app rejects all connections with lower TLS versions.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-234">When the operation is complete, your app rejects all connections with lower TLS versions.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="f4ff4-235">Automate with scripts</span><span class="sxs-lookup"><span data-stu-id="f4ff4-235">Automate with scripts</span></span>

<span data-ttu-id="f4ff4-236">You can automate SSL bindings for your web app with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f4ff4-236">You can automate SSL bindings for your web app with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="azure-cli"></a><span data-ttu-id="f4ff4-237">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f4ff4-237">Azure CLI</span></span>

<span data-ttu-id="f4ff4-238">The following command uploads an exported PFX file and gets the thumbprint.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-238">The following command uploads an exported PFX file and gets the thumbprint.</span></span>

```bash
thumbprint=$(az webapp config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

<span data-ttu-id="f4ff4-239">The following command adds an SNI-based SSL binding, using the thumbprint from the previous command.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-239">The following command adds an SNI-based SSL binding, using the thumbprint from the previous command.</span></span>

```bash
az webapp config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

<span data-ttu-id="f4ff4-240">The following command enforces minimum TLS version of 1.2.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-240">The following command enforces minimum TLS version of 1.2.</span></span>

```bash
az webapp config set \
    --name <app_name> \
    --resource-group <resource_group_name>
    --min-tls-version 1.2
```

### <a name="azure-powershell"></a><span data-ttu-id="f4ff4-241">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4ff4-241">Azure PowerShell</span></span>

<span data-ttu-id="f4ff4-242">The following command uploads an exported PFX file and adds an SNI-based SSL binding.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-242">The following command uploads an exported PFX file and adds an SNI-based SSL binding.</span></span>

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```
## <a name="public-certificates-optional"></a><span data-ttu-id="f4ff4-243">Public certificates (optional)</span><span class="sxs-lookup"><span data-stu-id="f4ff4-243">Public certificates (optional)</span></span>
<span data-ttu-id="f4ff4-244">You can upload [public certificates](https://blogs.msdn.microsoft.com/appserviceteam/2017/11/01/app-service-certificates-now-supports-public-certificates-cer/) to your web app so the app can access an external service that requires certificate authentication.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-244">You can upload [public certificates](https://blogs.msdn.microsoft.com/appserviceteam/2017/11/01/app-service-certificates-now-supports-public-certificates-cer/) to your web app so the app can access an external service that requires certificate authentication.</span></span>  <span data-ttu-id="f4ff4-245">For more details on loading and using a public certificate in your app, see [Use an SSL certificate in your application code in Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-web-ssl-cert-load).</span><span class="sxs-lookup"><span data-stu-id="f4ff4-245">For more details on loading and using a public certificate in your app, see [Use an SSL certificate in your application code in Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-web-ssl-cert-load).</span></span>  <span data-ttu-id="f4ff4-246">You can use public certificates with apps in App Service Environments also.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-246">You can use public certificates with apps in App Service Environments also.</span></span> <span data-ttu-id="f4ff4-247">If you need to store the certificate in the LocalMachine certificate store, you need to use a web app on App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-247">If you need to store the certificate in the LocalMachine certificate store, you need to use a web app on App Service Environment.</span></span> <span data-ttu-id="f4ff4-248">For more information, see [How to configure public certificates to your Web App](https://blogs.msdn.microsoft.com/appserviceteam/2017/11/01/app-service-certificates-now-supports-public-certificates-cer).</span><span class="sxs-lookup"><span data-stu-id="f4ff4-248">For more information, see [How to configure public certificates to your Web App](https://blogs.msdn.microsoft.com/appserviceteam/2017/11/01/app-service-certificates-now-supports-public-certificates-cer).</span></span>

![Upload Public Certificate](./media/app-service-web-tutorial-custom-ssl/upload-certificate-public1.png)

## <a name="next-steps"></a><span data-ttu-id="f4ff4-250">Next steps</span><span class="sxs-lookup"><span data-stu-id="f4ff4-250">Next steps</span></span>

<span data-ttu-id="f4ff4-251">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="f4ff4-251">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f4ff4-252">Upgrade your app's pricing tier</span><span class="sxs-lookup"><span data-stu-id="f4ff4-252">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="f4ff4-253">Bind your custom certificate to App Service</span><span class="sxs-lookup"><span data-stu-id="f4ff4-253">Bind your custom certificate to App Service</span></span>
> * <span data-ttu-id="f4ff4-254">Renew certificates</span><span class="sxs-lookup"><span data-stu-id="f4ff4-254">Renew certificates</span></span>
> * <span data-ttu-id="f4ff4-255">Enforce HTTPS</span><span class="sxs-lookup"><span data-stu-id="f4ff4-255">Enforce HTTPS</span></span>
> * <span data-ttu-id="f4ff4-256">Enforce TLS 1.1/1.2</span><span class="sxs-lookup"><span data-stu-id="f4ff4-256">Enforce TLS 1.1/1.2</span></span>
> * <span data-ttu-id="f4ff4-257">Automate TLS management with scripts</span><span class="sxs-lookup"><span data-stu-id="f4ff4-257">Automate TLS management with scripts</span></span>

<span data-ttu-id="f4ff4-258">Advance to the next tutorial to learn how to use Azure Content Delivery Network.</span><span class="sxs-lookup"><span data-stu-id="f4ff4-258">Advance to the next tutorial to learn how to use Azure Content Delivery Network.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f4ff4-259">Add a Content Delivery Network (CDN) to an Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f4ff4-259">Add a Content Delivery Network (CDN) to an Azure App Service</span></span>](../cdn/cdn-add-to-web-app.md)

<span data-ttu-id="f4ff4-260">For more information, see [Use an SSL certificate in your application code in Azure App Service](app-service-web-ssl-cert-load.md).</span><span class="sxs-lookup"><span data-stu-id="f4ff4-260">For more information, see [Use an SSL certificate in your application code in Azure App Service](app-service-web-ssl-cert-load.md).</span></span>
