---
title: Secure your app's custom domain with HTTPS | Microsoft Docs
description: Learn how secure the custom domain name for your app in Azure App Service by configuring an SSL certificate binding. You will also learn how to get an SSL certificate from multiple tools.
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 613d7932-73aa-4318-867c-1ce1416224dc
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2016
ms.author: cephalin
ms.openlocfilehash: 24a038dccf37ac4fd234c7b8150cd3007318dcfa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671495"
---
# <a name="secure-your-apps-custom-domain-with-https"></a><span data-ttu-id="62f53-104">Secure your app's custom domain with HTTPS</span><span class="sxs-lookup"><span data-stu-id="62f53-104">Secure your app's custom domain with HTTPS</span></span>
> [!div class="op_single_selector"]
> * [Buy SSL cert in Azure](web-sites-purchase-ssl-web-site.md)
> * [Use SSL cert from elsewhere](web-sites-configure-ssl-certificate.md)
> 
> 

<span data-ttu-id="62f53-107">This article shows you how to enable HTTPS for a web app, a mobile app backend, or an API app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that uses a custom domain name.</span><span class="sxs-lookup"><span data-stu-id="62f53-107">This article shows you how to enable HTTPS for a web app, a mobile app backend, or an API app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that uses a custom domain name.</span></span> <span data-ttu-id="62f53-108">It covers server-only authentication.</span><span class="sxs-lookup"><span data-stu-id="62f53-108">It covers server-only authentication.</span></span> <span data-ttu-id="62f53-109">If you need mutual authentication (including client authentication), see [How To Configure TLS Mutual Authentication for App Service](app-service-web-configure-tls-mutual-auth.md).</span><span class="sxs-lookup"><span data-stu-id="62f53-109">If you need mutual authentication (including client authentication), see [How To Configure TLS Mutual Authentication for App Service](app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="62f53-110">To secure with HTTPS an app that has a custom domain name, you add a certificate for that domain name.</span><span class="sxs-lookup"><span data-stu-id="62f53-110">To secure with HTTPS an app that has a custom domain name, you add a certificate for that domain name.</span></span> <span data-ttu-id="62f53-111">By default, Azure secures the **\*.azurewebsites.net** wildcard domain with a single SSL certificate, so your clients can already access your app at **https://*&lt;appname>*.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="62f53-111">By default, Azure secures the **\*.azurewebsites.net** wildcard domain with a single SSL certificate, so your clients can already access your app at **https://*&lt;appname>*.azurewebsites.net**.</span></span> <span data-ttu-id="62f53-112">But if you want to use a custom domain, like **contoso.com**, **www.contoso.com**, and **\*.contoso.com**, the default certificate can't secure that.</span><span class="sxs-lookup"><span data-stu-id="62f53-112">But if you want to use a custom domain, like **contoso.com**, **www.contoso.com**, and **\*.contoso.com**, the default certificate can't secure that.</span></span> <span data-ttu-id="62f53-113">Furthermore, like all [wildcard certificates](https://casecurity.org/2014/02/26/pros-and-cons-of-single-domain-multi-domain-and-wildcard-certificates/), the default certificate is not as secure as using a custom domain and a certificate for that custom domain.</span><span class="sxs-lookup"><span data-stu-id="62f53-113">Furthermore, like all [wildcard certificates](https://casecurity.org/2014/02/26/pros-and-cons-of-single-domain-multi-domain-and-wildcard-certificates/), the default certificate is not as secure as using a custom domain and a certificate for that custom domain.</span></span>   

> [!NOTE]
> You can get help from Azure experts anytime on the [Azure forums](https://azure.microsoft.com/support/forums/). For more personalized support, go to [Azure Support](https://azure.microsoft.com/support/options/) and click **Get Support**.
> 
> 

<a name="bkmk_domainname"></a>

## <a name="what-you-need"></a><span data-ttu-id="62f53-116">What you need</span><span class="sxs-lookup"><span data-stu-id="62f53-116">What you need</span></span>
<span data-ttu-id="62f53-117">To secure your custom domain name with HTTPS, you bind a custom SSL certificate to that custom domain in Azure.</span><span class="sxs-lookup"><span data-stu-id="62f53-117">To secure your custom domain name with HTTPS, you bind a custom SSL certificate to that custom domain in Azure.</span></span> <span data-ttu-id="62f53-118">Before binding a custom certificate, you need to do the following:</span><span class="sxs-lookup"><span data-stu-id="62f53-118">Before binding a custom certificate, you need to do the following:</span></span>

* <span data-ttu-id="62f53-119">**Configure the custom domain** - App Service only allows adding a certificate for a domain name that's already configured in your app.</span><span class="sxs-lookup"><span data-stu-id="62f53-119">**Configure the custom domain** - App Service only allows adding a certificate for a domain name that's already configured in your app.</span></span> <span data-ttu-id="62f53-120">For instructions, see [Map a custom domain name to an Azure app](web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="62f53-120">For instructions, see [Map a custom domain name to an Azure app](web-sites-custom-domain-name.md).</span></span> 
* <span data-ttu-id="62f53-121">**Scale up to Basic tier or higher** App Service plans in lower pricing tiers don't support custom SSL certificates.</span><span class="sxs-lookup"><span data-stu-id="62f53-121">**Scale up to Basic tier or higher** App Service plans in lower pricing tiers don't support custom SSL certificates.</span></span> <span data-ttu-id="62f53-122">For instructions, see [Scale up an app in Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="62f53-122">For instructions, see [Scale up an app in Azure](web-sites-scale.md).</span></span> 
* <span data-ttu-id="62f53-123">**Get an SSL certificate** - If you do not already have one, you need to get one from a trusted [certificate authority](http://en.wikipedia.org/wiki/Certificate_authority) (CA).</span><span class="sxs-lookup"><span data-stu-id="62f53-123">**Get an SSL certificate** - If you do not already have one, you need to get one from a trusted [certificate authority](http://en.wikipedia.org/wiki/Certificate_authority) (CA).</span></span> <span data-ttu-id="62f53-124">The certificate must meet all the following requirements:</span><span class="sxs-lookup"><span data-stu-id="62f53-124">The certificate must meet all the following requirements:</span></span>
  
  * <span data-ttu-id="62f53-125">It is signed by a trusted CA (no private CA servers).</span><span class="sxs-lookup"><span data-stu-id="62f53-125">It is signed by a trusted CA (no private CA servers).</span></span>
  * <span data-ttu-id="62f53-126">It contains a private key.</span><span class="sxs-lookup"><span data-stu-id="62f53-126">It contains a private key.</span></span>
  * <span data-ttu-id="62f53-127">It is created for key exchange, and exported to a .PFX file.</span><span class="sxs-lookup"><span data-stu-id="62f53-127">It is created for key exchange, and exported to a .PFX file.</span></span>
  * <span data-ttu-id="62f53-128">It uses a minimum of 2048-bit encryption.</span><span class="sxs-lookup"><span data-stu-id="62f53-128">It uses a minimum of 2048-bit encryption.</span></span>
  * <span data-ttu-id="62f53-129">Its subject name matches the custom domain it needs to secure.</span><span class="sxs-lookup"><span data-stu-id="62f53-129">Its subject name matches the custom domain it needs to secure.</span></span> <span data-ttu-id="62f53-130">To secure multiple domains with one certificate, you need to use a wildcard name (e.g. **\*.contoso.com**) or specify subjectAltName values.</span><span class="sxs-lookup"><span data-stu-id="62f53-130">To secure multiple domains with one certificate, you need to use a wildcard name (e.g. **\*.contoso.com**) or specify subjectAltName values.</span></span>
  * <span data-ttu-id="62f53-131">It is merged with all **[intermediate certificates](http://en.wikipedia.org/wiki/Intermediate_certificate_authorities)** used by your CA.</span><span class="sxs-lookup"><span data-stu-id="62f53-131">It is merged with all **[intermediate certificates](http://en.wikipedia.org/wiki/Intermediate_certificate_authorities)** used by your CA.</span></span> <span data-ttu-id="62f53-132">Otherwise, you may run into irreproducible interoperability problems on some clients.</span><span class="sxs-lookup"><span data-stu-id="62f53-132">Otherwise, you may run into irreproducible interoperability problems on some clients.</span></span>
    
    > [!NOTE]
    > The easiest way to get an SSL certificate that meets all the requirements is to [buy one in the Azure portal directly](web-sites-purchase-ssl-web-site.md). This article shows you how to do it manually and then bind it to your custom domain in App Service.
    > 
    > **Elliptic Curve Cryptography (ECC) certificates** can work with App Service, but outside the scope of this article. Work with your CA on the exact steps to create ECC certificates.
    > 
    > 

<a name="bkmk_getcert"></a>

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="62f53-137">Step 1.</span><span class="sxs-lookup"><span data-stu-id="62f53-137">Step 1.</span></span> <span data-ttu-id="62f53-138">Get an SSL certificate</span><span class="sxs-lookup"><span data-stu-id="62f53-138">Get an SSL certificate</span></span>
<span data-ttu-id="62f53-139">Because CAs provide the various SSL certificate types at different price points, you should start by deciding what type of SSL certificate to buy.</span><span class="sxs-lookup"><span data-stu-id="62f53-139">Because CAs provide the various SSL certificate types at different price points, you should start by deciding what type of SSL certificate to buy.</span></span> <span data-ttu-id="62f53-140">To secure a single domain name (**www.contoso.com**), you just need a basic certificate.</span><span class="sxs-lookup"><span data-stu-id="62f53-140">To secure a single domain name (**www.contoso.com**), you just need a basic certificate.</span></span> <span data-ttu-id="62f53-141">To secure multiple domain names (**contoso.com** *and* **www.contoso.com** 
*and* **mail.contoso.com**), you need either a [wildcard certificate](http://en.wikipedia.org/wiki/Wildcard_certificate) or a certificate with [Subject Alternate Name](http://en.wikipedia.org/wiki/SubjectAltName) (`subjectAltName`).</span><span class="sxs-lookup"><span data-stu-id="62f53-141">To secure multiple domain names (**contoso.com** *and* **www.contoso.com** 
*and* **mail.contoso.com**), you need either a [wildcard certificate](http://en.wikipedia.org/wiki/Wildcard_certificate) or a certificate with [Subject Alternate Name](http://en.wikipedia.org/wiki/SubjectAltName) (`subjectAltName`).</span></span>

<span data-ttu-id="62f53-142">Once you know which SSL certificate to buy, you submit a Certificate Signing Request (CSR) to a CA.</span><span class="sxs-lookup"><span data-stu-id="62f53-142">Once you know which SSL certificate to buy, you submit a Certificate Signing Request (CSR) to a CA.</span></span> <span data-ttu-id="62f53-143">When you get requested certificate back from the CA, you then generate a .pfx file from the certificate.</span><span class="sxs-lookup"><span data-stu-id="62f53-143">When you get requested certificate back from the CA, you then generate a .pfx file from the certificate.</span></span> <span data-ttu-id="62f53-144">You can perform these steps using the tool of your choice.</span><span class="sxs-lookup"><span data-stu-id="62f53-144">You can perform these steps using the tool of your choice.</span></span> <span data-ttu-id="62f53-145">Here are instructions for the common tools:</span><span class="sxs-lookup"><span data-stu-id="62f53-145">Here are instructions for the common tools:</span></span>

* <span data-ttu-id="62f53-146">[Certreq.exe steps](#bkmk_certreq) - the Windows utility for creating certificate requests.</span><span class="sxs-lookup"><span data-stu-id="62f53-146">[Certreq.exe steps](#bkmk_certreq) - the Windows utility for creating certificate requests.</span></span> 
  <span data-ttu-id="62f53-147">It has been part of Windows since Windows XP/Windows Server 2000.</span><span class="sxs-lookup"><span data-stu-id="62f53-147">It has been part of Windows since Windows XP/Windows Server 2000.</span></span>
* <span data-ttu-id="62f53-148">[IIS Manager steps](#bkmk_iismgr) - The tool of choice if you're already familiar with it.</span><span class="sxs-lookup"><span data-stu-id="62f53-148">[IIS Manager steps](#bkmk_iismgr) - The tool of choice if you're already familiar with it.</span></span>
* <span data-ttu-id="62f53-149">[OpenSSL steps](#bkmk_openssl) - an [open-source, cross-platform tool](https://www.openssl.org).</span><span class="sxs-lookup"><span data-stu-id="62f53-149">[OpenSSL steps](#bkmk_openssl) - an [open-source, cross-platform tool](https://www.openssl.org).</span></span> <span data-ttu-id="62f53-150">Use it to help you get an SSL certificate from any platform.</span><span class="sxs-lookup"><span data-stu-id="62f53-150">Use it to help you get an SSL certificate from any platform.</span></span>
* <span data-ttu-id="62f53-151">[subjectAltName steps using OpenSSL](#bkmk_subjectaltname) - steps for getting `subjectAltName` certificates.</span><span class="sxs-lookup"><span data-stu-id="62f53-151">[subjectAltName steps using OpenSSL](#bkmk_subjectaltname) - steps for getting `subjectAltName` certificates.</span></span>

<span data-ttu-id="62f53-152">If you want to test the setup in App Service before buying a certificate, you can generate a [self-signed certificate](https://en.wikipedia.org/wiki/Self-signed_certificate).</span><span class="sxs-lookup"><span data-stu-id="62f53-152">If you want to test the setup in App Service before buying a certificate, you can generate a [self-signed certificate](https://en.wikipedia.org/wiki/Self-signed_certificate).</span></span> <span data-ttu-id="62f53-153">This tutorial gives you two ways to generate it:</span><span class="sxs-lookup"><span data-stu-id="62f53-153">This tutorial gives you two ways to generate it:</span></span>

* [<span data-ttu-id="62f53-154">Self-signed certificate, Certreq.exe steps</span><span class="sxs-lookup"><span data-stu-id="62f53-154">Self-signed certificate, Certreq.exe steps</span></span>](#bkmk_sscertreq)
* [<span data-ttu-id="62f53-155">Self-signed certificate, OpenSSL steps</span><span class="sxs-lookup"><span data-stu-id="62f53-155">Self-signed certificate, OpenSSL steps</span></span>](#bkmk_ssopenssl)

<a name="bkmk_certreq"></a>

### <a name="get-a-certificate-using-certreqexe"></a><span data-ttu-id="62f53-156">Get a certificate using Certreq.exe</span><span class="sxs-lookup"><span data-stu-id="62f53-156">Get a certificate using Certreq.exe</span></span>
1. <span data-ttu-id="62f53-157">Create a file (e.g. **myrequest.txt**), and copy into it the following text, and save it in a working directory.</span><span class="sxs-lookup"><span data-stu-id="62f53-157">Create a file (e.g. **myrequest.txt**), and copy into it the following text, and save it in a working directory.</span></span> 
   <span data-ttu-id="62f53-158">Replace the `<your-domain>` placeholder with the custom domain name of your app.</span><span class="sxs-lookup"><span data-stu-id="62f53-158">Replace the `<your-domain>` placeholder with the custom domain name of your app.</span></span>
   
        [NewRequest]
        Subject = "CN=<your-domain>"  ; E.g. "CN=www.contoso.com", or "CN=*.contoso.com" for a wildcard certificate
        Exportable = TRUE
        KeyLength = 2048              ; Required minimum is 2048
        KeySpec = 1
        KeyUsage = 0xA0
        MachineKeySet = FALSE
        ProviderName = "Microsoft RSA SChannel Cryptographic Provider"
        ProviderType = 12
        HashAlgorithm = SHA256
   
        [EnhancedKeyUsageExtension]
        OID=1.3.6.1.5.5.7.3.1         ; Server Authentication
   
    <span data-ttu-id="62f53-159">For more information on the options in the CSR, and other available options, see the [Certreq reference documentation](https://technet.microsoft.com/library/dn296456.aspx).</span><span class="sxs-lookup"><span data-stu-id="62f53-159">For more information on the options in the CSR, and other available options, see the [Certreq reference documentation](https://technet.microsoft.com/library/dn296456.aspx).</span></span>
2. <span data-ttu-id="62f53-160">In a command prompt, `CD` into your working directory and run the following command to create the CSR:</span><span class="sxs-lookup"><span data-stu-id="62f53-160">In a command prompt, `CD` into your working directory and run the following command to create the CSR:</span></span>
   
        certreq -new myrequest.txt myrequest.csr
   
    <span data-ttu-id="62f53-161">**myrequest.csr** is now created in your current working directory.</span><span class="sxs-lookup"><span data-stu-id="62f53-161">**myrequest.csr** is now created in your current working directory.</span></span>
3. <span data-ttu-id="62f53-162">Submit **myrequest.csr** to a CA to obtain an SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="62f53-162">Submit **myrequest.csr** to a CA to obtain an SSL certificate.</span></span> <span data-ttu-id="62f53-163">You either upload the file, or copy its content from a text editor into a web form.</span><span class="sxs-lookup"><span data-stu-id="62f53-163">You either upload the file, or copy its content from a text editor into a web form.</span></span>
   
    <span data-ttu-id="62f53-164">For a list of CAs trusted by Microsoft, see [Microsoft Trusted Root Certificate Program: Participants][cas].</span><span class="sxs-lookup"><span data-stu-id="62f53-164">For a list of CAs trusted by Microsoft, see [Microsoft Trusted Root Certificate Program: Participants][cas].</span></span>
4. <span data-ttu-id="62f53-165">Once the CA has responded to you with a certificate (.CER) file, save it in your working directory.</span><span class="sxs-lookup"><span data-stu-id="62f53-165">Once the CA has responded to you with a certificate (.CER) file, save it in your working directory.</span></span> <span data-ttu-id="62f53-166">Then, run the following command to complete the pending CSR.</span><span class="sxs-lookup"><span data-stu-id="62f53-166">Then, run the following command to complete the pending CSR.</span></span>
   
        certreq -accept -user <certificate-name>.cer
   
    <span data-ttu-id="62f53-167">This command stores the finished certificate in the Windows certificate store.</span><span class="sxs-lookup"><span data-stu-id="62f53-167">This command stores the finished certificate in the Windows certificate store.</span></span>
5. <span data-ttu-id="62f53-168">If your CA uses intermediate certificates, install them before you proceed.</span><span class="sxs-lookup"><span data-stu-id="62f53-168">If your CA uses intermediate certificates, install them before you proceed.</span></span> <span data-ttu-id="62f53-169">They usually come as a separate download from your CA, and in several formats for different web server types.</span><span class="sxs-lookup"><span data-stu-id="62f53-169">They usually come as a separate download from your CA, and in several formats for different web server types.</span></span> <span data-ttu-id="62f53-170">Select the version for Microsoft IIS.</span><span class="sxs-lookup"><span data-stu-id="62f53-170">Select the version for Microsoft IIS.</span></span>
   
    <span data-ttu-id="62f53-171">Once you have downloaded the certificates, right-click each of them in Windows Explorer and select **Install certificate**.</span><span class="sxs-lookup"><span data-stu-id="62f53-171">Once you have downloaded the certificates, right-click each of them in Windows Explorer and select **Install certificate**.</span></span> <span data-ttu-id="62f53-172">Use the default values in the **Certificate Import Wizard**, and continue selecting **Next** until the import has completed.</span><span class="sxs-lookup"><span data-stu-id="62f53-172">Use the default values in the **Certificate Import Wizard**, and continue selecting **Next** until the import has completed.</span></span>
6. <span data-ttu-id="62f53-173">To export your SSL certificate from the certificate store, press `Win`+`R` and run **certmgr.msc** to launch Certificate Manager.</span><span class="sxs-lookup"><span data-stu-id="62f53-173">To export your SSL certificate from the certificate store, press `Win`+`R` and run **certmgr.msc** to launch Certificate Manager.</span></span> 
   <span data-ttu-id="62f53-174">Select **Personal** > **Certificates**.</span><span class="sxs-lookup"><span data-stu-id="62f53-174">Select **Personal** > **Certificates**.</span></span> <span data-ttu-id="62f53-175">In the **Issued To** column, you should see an entry with your custom domain name, and the CA you used to generate the certificate in the **Issued By** column.</span><span class="sxs-lookup"><span data-stu-id="62f53-175">In the **Issued To** column, you should see an entry with your custom domain name, and the CA you used to generate the certificate in the **Issued By** column.</span></span>
   
    ![insert image of cert manager here][certmgr]
7. <span data-ttu-id="62f53-177">Right-click the certificate and select **All Tasks** > **Export**.</span><span class="sxs-lookup"><span data-stu-id="62f53-177">Right-click the certificate and select **All Tasks** > **Export**.</span></span> <span data-ttu-id="62f53-178">In the **Certificate Export Wizard**, click **Next**, then select **Yes, export the private key**, and then click **Next** again.</span><span class="sxs-lookup"><span data-stu-id="62f53-178">In the **Certificate Export Wizard**, click **Next**, then select **Yes, export the private key**, and then click **Next** again.</span></span>
   
    ![Export the private key][certwiz1]
8. <span data-ttu-id="62f53-180">Select **Personal Information Exchange - PKCS #12**, **Include all certificates in the certificate path if possible**, and **Export all extended properties**.</span><span class="sxs-lookup"><span data-stu-id="62f53-180">Select **Personal Information Exchange - PKCS #12**, **Include all certificates in the certificate path if possible**, and **Export all extended properties**.</span></span> <span data-ttu-id="62f53-181">Then, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="62f53-181">Then, click **Next**.</span></span>
   
   ![include all certs and extended properties][certwiz2]
9. <span data-ttu-id="62f53-183">Select **Password**, and then enter and confirm the password.</span><span class="sxs-lookup"><span data-stu-id="62f53-183">Select **Password**, and then enter and confirm the password.</span></span> <span data-ttu-id="62f53-184">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="62f53-184">Click **Next**.</span></span>
   
   ![specify a password][certwiz3]
10. <span data-ttu-id="62f53-186">Provide a path and filename for the exported certificate, with the extension **.pfx**.</span><span class="sxs-lookup"><span data-stu-id="62f53-186">Provide a path and filename for the exported certificate, with the extension **.pfx**.</span></span> <span data-ttu-id="62f53-187">Click **Next** to finish.</span><span class="sxs-lookup"><span data-stu-id="62f53-187">Click **Next** to finish.</span></span>
    
    ![provide a file path][certwiz4]

<span data-ttu-id="62f53-189">You are now ready to upload the exported PFX file to App Service.</span><span class="sxs-lookup"><span data-stu-id="62f53-189">You are now ready to upload the exported PFX file to App Service.</span></span> <span data-ttu-id="62f53-190">See [Step 2. Upload and bind the custom SSL certificate](#bkmk_configuressl).</span><span class="sxs-lookup"><span data-stu-id="62f53-190">See [Step 2. Upload and bind the custom SSL certificate](#bkmk_configuressl).</span></span>

<a name="bkmk_iismgr"></a>

### <a name="get-a-certificate-using-the-iis-manager"></a><span data-ttu-id="62f53-191">Get a certificate using the IIS Manager</span><span class="sxs-lookup"><span data-stu-id="62f53-191">Get a certificate using the IIS Manager</span></span>
1. <span data-ttu-id="62f53-192">Generate a CSR with IIS Manager to send to the CA.</span><span class="sxs-lookup"><span data-stu-id="62f53-192">Generate a CSR with IIS Manager to send to the CA.</span></span> <span data-ttu-id="62f53-193">For more information on generating a CSR, see [Request an Internet Server Certificate (IIS 7)][iiscsr].</span><span class="sxs-lookup"><span data-stu-id="62f53-193">For more information on generating a CSR, see [Request an Internet Server Certificate (IIS 7)][iiscsr].</span></span>
2. <span data-ttu-id="62f53-194">Submit your CSR to a CA to get an SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="62f53-194">Submit your CSR to a CA to get an SSL certificate.</span></span> <span data-ttu-id="62f53-195">For a list of CAs trusted by Microsoft, see [Microsoft Trusted Root Certificate Program: Participants][cas].</span><span class="sxs-lookup"><span data-stu-id="62f53-195">For a list of CAs trusted by Microsoft, see [Microsoft Trusted Root Certificate Program: Participants][cas].</span></span>
3. <span data-ttu-id="62f53-196">Complete the CSR with the certificate that the CA sends back to you.</span><span class="sxs-lookup"><span data-stu-id="62f53-196">Complete the CSR with the certificate that the CA sends back to you.</span></span> <span data-ttu-id="62f53-197">For more information on completing the CSR, see [Install an Internet Server Certificate (IIS 7)][installcertiis].</span><span class="sxs-lookup"><span data-stu-id="62f53-197">For more information on completing the CSR, see [Install an Internet Server Certificate (IIS 7)][installcertiis].</span></span>
4. <span data-ttu-id="62f53-198">If your CA uses intermediate certificates, install them before you proceed.</span><span class="sxs-lookup"><span data-stu-id="62f53-198">If your CA uses intermediate certificates, install them before you proceed.</span></span> <span data-ttu-id="62f53-199">They usually come as a separate download from your CA, and in several formats for different web server types.</span><span class="sxs-lookup"><span data-stu-id="62f53-199">They usually come as a separate download from your CA, and in several formats for different web server types.</span></span> <span data-ttu-id="62f53-200">Select the version for Microsoft IIS.</span><span class="sxs-lookup"><span data-stu-id="62f53-200">Select the version for Microsoft IIS.</span></span>
   
    <span data-ttu-id="62f53-201">Once you have downloaded the certificates, right-click each of them in Windows Explorer and select **Install certificate**.</span><span class="sxs-lookup"><span data-stu-id="62f53-201">Once you have downloaded the certificates, right-click each of them in Windows Explorer and select **Install certificate**.</span></span> 
    <span data-ttu-id="62f53-202">Use the default values in the **Certificate Import Wizard**, and continue selecting **Next** until the import has completed.</span><span class="sxs-lookup"><span data-stu-id="62f53-202">Use the default values in the **Certificate Import Wizard**, and continue selecting **Next** until the import has completed.</span></span>
5. <span data-ttu-id="62f53-203">Export the SSL certificate from IIS Manager.</span><span class="sxs-lookup"><span data-stu-id="62f53-203">Export the SSL certificate from IIS Manager.</span></span> <span data-ttu-id="62f53-204">For more information on exporting the certificate, see [Export a Server Certificate (IIS 7)][exportcertiis].</span><span class="sxs-lookup"><span data-stu-id="62f53-204">For more information on exporting the certificate, see [Export a Server Certificate (IIS 7)][exportcertiis].</span></span> 
   
   > [!IMPORTANT]
   > In the **Certificate Export Wizard**, make sure that you select **Yes, export the private key**  
   > 
   > ![Export the private key][certwiz1]  
   > 
   > and also select **Personal Information Exchange - PKCS #12**, **Include all certificates in the certificate path if possible**, and **Export all extended properties**.
   > 
   > ![include all certs and extended properties][certwiz2]
   > 
   > 

<span data-ttu-id="62f53-209">You are now ready to upload the exported PFX file to App Service.</span><span class="sxs-lookup"><span data-stu-id="62f53-209">You are now ready to upload the exported PFX file to App Service.</span></span> <span data-ttu-id="62f53-210">See [Step 2. Upload and bind the custom SSL certificate](#bkmk_configuressl).</span><span class="sxs-lookup"><span data-stu-id="62f53-210">See [Step 2. Upload and bind the custom SSL certificate](#bkmk_configuressl).</span></span>

<a name="bkmk_openssl"></a>

### <a name="get-a-certificate-using-openssl"></a><span data-ttu-id="62f53-211">Get a certificate using OpenSSL</span><span class="sxs-lookup"><span data-stu-id="62f53-211">Get a certificate using OpenSSL</span></span>
1. <span data-ttu-id="62f53-212">In a command-line terminal, `CD` into a working directory generate a private key and CSR by running the following command:</span><span class="sxs-lookup"><span data-stu-id="62f53-212">In a command-line terminal, `CD` into a working directory generate a private key and CSR by running the following command:</span></span>
   
        openssl req -sha256 -new -nodes -keyout myserver.key -out server.csr -newkey rsa:2048
2. <span data-ttu-id="62f53-213">When prompted, enter the appropriate information.</span><span class="sxs-lookup"><span data-stu-id="62f53-213">When prompted, enter the appropriate information.</span></span> <span data-ttu-id="62f53-214">For example:</span><span class="sxs-lookup"><span data-stu-id="62f53-214">For example:</span></span>
   
         Country Name (2 letter code)
        State or Province Name (full name) []: Washington
        Locality Name (eg, city) []: Redmond
        Organization Name (eg, company) []: Microsoft
        Organizational Unit Name (eg, section) []: Azure
        Common Name (eg, YOUR name) []: www.microsoft.com
        Email Address []:
   
        Please enter the following 'extra' attributes to be sent with your certificate request
   
           A challenge password []:
   
    <span data-ttu-id="62f53-215">When finished, you should have two files in your working directory: **myserver.key** and **server.csr**.</span><span class="sxs-lookup"><span data-stu-id="62f53-215">When finished, you should have two files in your working directory: **myserver.key** and **server.csr**.</span></span> 
    <span data-ttu-id="62f53-216">The **server.csr** contains the CSR, and you need **myserver.key** later.</span><span class="sxs-lookup"><span data-stu-id="62f53-216">The **server.csr** contains the CSR, and you need **myserver.key** later.</span></span>
3. <span data-ttu-id="62f53-217">Submit your CSR to a CA to get an SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="62f53-217">Submit your CSR to a CA to get an SSL certificate.</span></span> <span data-ttu-id="62f53-218">For a list of CAs trusted by Microsoft, see [Microsoft Trusted Root Certificate Program: Participants][cas].</span><span class="sxs-lookup"><span data-stu-id="62f53-218">For a list of CAs trusted by Microsoft, see [Microsoft Trusted Root Certificate Program: Participants][cas].</span></span>
4. <span data-ttu-id="62f53-219">Once the CA sends you the requested certificate, save it to a file named **myserver.crt** in your working directory.</span><span class="sxs-lookup"><span data-stu-id="62f53-219">Once the CA sends you the requested certificate, save it to a file named **myserver.crt** in your working directory.</span></span> <span data-ttu-id="62f53-220">If your CA provides it in a text format, simply copy the content into **myserver.crt** in a text editor and save it.</span><span class="sxs-lookup"><span data-stu-id="62f53-220">If your CA provides it in a text format, simply copy the content into **myserver.crt** in a text editor and save it.</span></span> <span data-ttu-id="62f53-221">Your file should look like the following:</span><span class="sxs-lookup"><span data-stu-id="62f53-221">Your file should look like the following:</span></span>
   
        -----BEGIN CERTIFICATE-----
        MIIDJDCCAgwCCQCpCY4o1LBQuzANBgkqhkiG9w0BAQUFADBUMQswCQYDVQQGEwJV
        UzELMAkGA1UECBMCV0ExEDAOBgNVBAcTB1JlZG1vbmQxEDAOBgNVBAsTB0NvbnRv
        c28xFDASBgNVBAMTC2NvbnRvc28uY29tMB4XDTE0MDExNjE1MzIyM1oXDTE1MDEx
        NjE1MzIyM1owVDELMAkGA1UEBhMCVVMxCzAJBgNVBAgTAldBMRAwDgYDVQQHEwdS
        ZWRtb25kMRAwDgYDVQQLEwdDb250b3NvMRQwEgYDVQQDEwtjb250b3NvLmNvbTCC
        ASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAN96hBX5EDgULtWkCRK7DMM3
        enae1LT9fXqGlbA7ScFvFivGvOLEqEPD//eLGsf15OYHFOQHK1hwgyfXa9sEDPMT
        3AsF3iWyF7FiEoR/qV6LdKjeQicJ2cXjGwf3G5vPoIaYifI5r0lhgOUqBxzaBDZ4
        xMgCh2yv7NavI17BHlWyQo90gS2X5glYGRhzY/fGp10BeUEgIs3Se0kQfBQOFUYb
        ktA6802lod5K0OxlQy4Oc8kfxTDf8AF2SPQ6BL7xxWrNl/Q2DuEEemjuMnLNxmeA
        Ik2+6Z6+WdvJoRxqHhleoL8ftOpWR20ToiZXCPo+fcmLod4ejsG5qjBlztVY4qsC
        AwEAATANBgkqhkiG9w0BAQUFAAOCAQEAVcM9AeeNFv2li69qBZLGDuK0NDHD3zhK
        Y0nDkqucgjE2QKUuvVSPodz8qwHnKoPwnSrTn8CRjW1gFq5qWEO50dGWgyLR8Wy1
        F69DYsEzodG+shv/G+vHJZg9QzutsJTB/Q8OoUCSnQS1PSPZP7RbvDV9b7Gx+gtg
        7kQ55j3A5vOrpI8N9CwdPuimtu6X8Ylw9ejWZsnyy0FMeOPpK3WTkDMxwwGxkU3Y
        lCRTzkv6vnHrlYQxyBLOSafCB1RWinN/slcWSLHADB6R+HeMiVKkFpooT+ghtii1
        A9PdUQIhK9bdaFicXPBYZ6AgNVuGtfwyuS5V6ucm7RE6+qf+QjXNFg==
        -----END CERTIFICATE-----
5. <span data-ttu-id="62f53-222">In the command-line terminal, run the following command to export **myserver.pfx** from **myserver.key** and **myserver.crt**:</span><span class="sxs-lookup"><span data-stu-id="62f53-222">In the command-line terminal, run the following command to export **myserver.pfx** from **myserver.key** and **myserver.crt**:</span></span>
   
        openssl pkcs12 -export -out myserver.pfx -inkey myserver.key -in myserver.crt
   
    <span data-ttu-id="62f53-223">When prompted, define a password to secure the .pfx file.</span><span class="sxs-lookup"><span data-stu-id="62f53-223">When prompted, define a password to secure the .pfx file.</span></span>
   
   > [!NOTE]
   > If your CA uses intermediate certificates, you must include them with the `-certfile` parameter. They usually come as a separate download from your CA, and in several formats for different web server types. Select the version with the `.pem` extension.
   > 
   > Your `openssl -export` command should look like the following example, which creates a .pfx file that includes the intermediate certificates from the **intermediate-cets.pem** file:
   > 
   > `openssl pkcs12 -chain -export -out myserver.pfx -inkey myserver.key -in myserver.crt -certfile intermediate-cets.pem`
   > 
   > 

<span data-ttu-id="62f53-228">You are now ready to upload the exported PFX file to App Service.</span><span class="sxs-lookup"><span data-stu-id="62f53-228">You are now ready to upload the exported PFX file to App Service.</span></span> <span data-ttu-id="62f53-229">See [Step 2. Upload and bind the custom SSL certificate](#bkmk_configuressl).</span><span class="sxs-lookup"><span data-stu-id="62f53-229">See [Step 2. Upload and bind the custom SSL certificate](#bkmk_configuressl).</span></span>

<a name="bkmk_subjectaltname"></a>

### <a name="get-a-subjectaltname-certificate-using-openssl"></a><span data-ttu-id="62f53-230">Get a SubjectAltName certificate using OpenSSL</span><span class="sxs-lookup"><span data-stu-id="62f53-230">Get a SubjectAltName certificate using OpenSSL</span></span>
1. <span data-ttu-id="62f53-231">Create a file named **sancert.cnf**, copy the following text into it, and save it in a working directory:</span><span class="sxs-lookup"><span data-stu-id="62f53-231">Create a file named **sancert.cnf**, copy the following text into it, and save it in a working directory:</span></span>
   
        # -------------- BEGIN custom sancert.cnf -----
        HOME = .
        oid_section = new_oids
        [ new_oids ]
        [ req ]
        default_days = 730
        distinguished_name = req_distinguished_name
        encrypt_key = no
        string_mask = nombstr
        req_extensions = v3_req # Extensions to add to certificate request
        [ req_distinguished_name ]
        countryName = Country Name (2 letter code)
        countryName_default =
        stateOrProvinceName = State or Province Name (full name)
        stateOrProvinceName_default =
        localityName = Locality Name (eg, city)
        localityName_default =
        organizationalUnitName  = Organizational Unit Name (eg, section)
        organizationalUnitName_default  =
        commonName              = Your common name (eg, domain name)
        commonName_default      = www.mydomain.com
        commonName_max = 64
        [ v3_req ]
        subjectAltName=DNS:ftp.mydomain.com,DNS:blog.mydomain.com,DNS:*.mydomain.com
        # -------------- END custom sancert.cnf -----
   
    <span data-ttu-id="62f53-232">In the line that begins with `subjectAltName`, replace the value with all domain names you want to secure (in addition to `commonName`).</span><span class="sxs-lookup"><span data-stu-id="62f53-232">In the line that begins with `subjectAltName`, replace the value with all domain names you want to secure (in addition to `commonName`).</span></span> <span data-ttu-id="62f53-233">For example:</span><span class="sxs-lookup"><span data-stu-id="62f53-233">For example:</span></span>
   
        subjectAltName=DNS:sales.contoso.com,DNS:support.contoso.com,DNS:fabrikam.com
   
    <span data-ttu-id="62f53-234">You do not need to change any other field, including `commonName`.</span><span class="sxs-lookup"><span data-stu-id="62f53-234">You do not need to change any other field, including `commonName`.</span></span> <span data-ttu-id="62f53-235">You will be prompted to specify them in the next few steps.</span><span class="sxs-lookup"><span data-stu-id="62f53-235">You will be prompted to specify them in the next few steps.</span></span>
2. <span data-ttu-id="62f53-236">In a command-line terminal, `CD` into your working directory and run the following command:</span><span class="sxs-lookup"><span data-stu-id="62f53-236">In a command-line terminal, `CD` into your working directory and run the following command:</span></span>
   
        openssl req -sha256 -new -nodes -keyout myserver.key -out server.csr -newkey rsa:2048 -config sancert.cnf
3. <span data-ttu-id="62f53-237">When prompted, enter the appropriate information.</span><span class="sxs-lookup"><span data-stu-id="62f53-237">When prompted, enter the appropriate information.</span></span> <span data-ttu-id="62f53-238">For example:</span><span class="sxs-lookup"><span data-stu-id="62f53-238">For example:</span></span>
   
         Country Name (2 letter code) []: US
        State or Province Name (full name) []: Washington
        Locality Name (eg, city) []: Redmond
        Organizational Unit Name (eg, section) []: Azure
        Your common name (eg, domain name) []: www.microsoft.com
   
    <span data-ttu-id="62f53-239">Once finished, you should have two files in your working directory: **myserver.key** and **server.csr**.</span><span class="sxs-lookup"><span data-stu-id="62f53-239">Once finished, you should have two files in your working directory: **myserver.key** and **server.csr**.</span></span> 
    <span data-ttu-id="62f53-240">The **server.csr** contains the CSR, and you need **myserver.key** later.</span><span class="sxs-lookup"><span data-stu-id="62f53-240">The **server.csr** contains the CSR, and you need **myserver.key** later.</span></span>
4. <span data-ttu-id="62f53-241">Submit your CSR to a CA to get an SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="62f53-241">Submit your CSR to a CA to get an SSL certificate.</span></span> <span data-ttu-id="62f53-242">For a list of CAs trusted by Microsoft, see [Microsoft Trusted Root Certificate Program: Participants][cas].</span><span class="sxs-lookup"><span data-stu-id="62f53-242">For a list of CAs trusted by Microsoft, see [Microsoft Trusted Root Certificate Program: Participants][cas].</span></span>
5. <span data-ttu-id="62f53-243">Once the CA sends you the requested certificate, save it to a file named **myserver.crt**.</span><span class="sxs-lookup"><span data-stu-id="62f53-243">Once the CA sends you the requested certificate, save it to a file named **myserver.crt**.</span></span> <span data-ttu-id="62f53-244">If your CA provides it in a text format, simply copy the content into **myserver.crt** in a text editor and save it.</span><span class="sxs-lookup"><span data-stu-id="62f53-244">If your CA provides it in a text format, simply copy the content into **myserver.crt** in a text editor and save it.</span></span> <span data-ttu-id="62f53-245">The file should look like the following:</span><span class="sxs-lookup"><span data-stu-id="62f53-245">The file should look like the following:</span></span>
   
        -----BEGIN CERTIFICATE-----
        MIIDJDCCAgwCCQCpCY4o1LBQuzANBgkqhkiG9w0BAQUFADBUMQswCQYDVQQGEwJV
        UzELMAkGA1UECBMCV0ExEDAOBgNVBAcTB1JlZG1vbmQxEDAOBgNVBAsTB0NvbnRv
        c28xFDASBgNVBAMTC2NvbnRvc28uY29tMB4XDTE0MDExNjE1MzIyM1oXDTE1MDEx
        NjE1MzIyM1owVDELMAkGA1UEBhMCVVMxCzAJBgNVBAgTAldBMRAwDgYDVQQHEwdS
        ZWRtb25kMRAwDgYDVQQLEwdDb250b3NvMRQwEgYDVQQDEwtjb250b3NvLmNvbTCC
        ASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAN96hBX5EDgULtWkCRK7DMM3
        enae1LT9fXqGlbA7ScFvFivGvOLEqEPD//eLGsf15OYHFOQHK1hwgyfXa9sEDPMT
        3AsF3iWyF7FiEoR/qV6LdKjeQicJ2cXjGwf3G5vPoIaYifI5r0lhgOUqBxzaBDZ4
        xMgCh2yv7NavI17BHlWyQo90gS2X5glYGRhzY/fGp10BeUEgIs3Se0kQfBQOFUYb
        ktA6802lod5K0OxlQy4Oc8kfxTDf8AF2SPQ6BL7xxWrNl/Q2DuEEemjuMnLNxmeA
        Ik2+6Z6+WdvJoRxqHhleoL8ftOpWR20ToiZXCPo+fcmLod4ejsG5qjBlztVY4qsC
        AwEAATANBgkqhkiG9w0BAQUFAAOCAQEAVcM9AeeNFv2li69qBZLGDuK0NDHD3zhK
        Y0nDkqucgjE2QKUuvVSPodz8qwHnKoPwnSrTn8CRjW1gFq5qWEO50dGWgyLR8Wy1
        F69DYsEzodG+shv/G+vHJZg9QzutsJTB/Q8OoUCSnQS1PSPZP7RbvDV9b7Gx+gtg
        7kQ55j3A5vOrpI8N9CwdPuimtu6X8Ylw9ejWZsnyy0FMeOPpK3WTkDMxwwGxkU3Y
        lCRTzkv6vnHrlYQxyBLOSafCB1RWinN/slcWSLHADB6R+HeMiVKkFpooT+ghtii1
        A9PdUQIhK9bdaFicXPBYZ6AgNVuGtfwyuS5V6ucm7RE6+qf+QjXNFg==
        -----END CERTIFICATE-----
6. <span data-ttu-id="62f53-246">In the command-line terminal, run the following command to export **myserver.pfx** from **myserver.key** and **myserver.crt**:</span><span class="sxs-lookup"><span data-stu-id="62f53-246">In the command-line terminal, run the following command to export **myserver.pfx** from **myserver.key** and **myserver.crt**:</span></span>
   
        openssl pkcs12 -export -out myserver.pfx -inkey myserver.key -in myserver.crt
   
    <span data-ttu-id="62f53-247">When prompted, define a password to secure the .pfx file.</span><span class="sxs-lookup"><span data-stu-id="62f53-247">When prompted, define a password to secure the .pfx file.</span></span>
   
   > [!NOTE]
   > If your CA uses intermediate certificates, you must include them with the `-certfile` parameter. They usually come as a separate download from your CA, and in several formats for different web server types. Select the version with the `.pem` extension).
   > 
   > Your `openssl -export` command should look like the following example, which creates a .pfx file that includes the intermediate certificates from the **intermediate-cets.pem** file:
   > 
   > `openssl pkcs12 -chain -export -out myserver.pfx -inkey myserver.key -in myserver.crt -certfile intermediate-cets.pem`
   > 
   > 

<span data-ttu-id="62f53-252">You are now ready to upload the exported PFX file to App Service.</span><span class="sxs-lookup"><span data-stu-id="62f53-252">You are now ready to upload the exported PFX file to App Service.</span></span> <span data-ttu-id="62f53-253">See [Step 2. Upload and bind the custom SSL certificate](#bkmk_configuressl).</span><span class="sxs-lookup"><span data-stu-id="62f53-253">See [Step 2. Upload and bind the custom SSL certificate](#bkmk_configuressl).</span></span>

<a name="bkmk_sscertreq"></a>

### <a name="generate-a-self-signed-certificate-using-certreqexe"></a><span data-ttu-id="62f53-254">Generate a self-signed certificate using Certreq.exe</span><span class="sxs-lookup"><span data-stu-id="62f53-254">Generate a self-signed certificate using Certreq.exe</span></span>
> [!IMPORTANT]
> Self-signed certificates are for test purposes only. Most browsers return errors when visiting a website that's secured by a self-signed certificate. Some browsers may even refuse to navigate to the site. 
> 
> 

1. <span data-ttu-id="62f53-258">Create a text file (e.g. **mycert.txt**), copy into it the following text, and save the file in a working directory.</span><span class="sxs-lookup"><span data-stu-id="62f53-258">Create a text file (e.g. **mycert.txt**), copy into it the following text, and save the file in a working directory.</span></span> 
   <span data-ttu-id="62f53-259">Replace the `<your-domain>` placeholder with the custom domain name of your app.</span><span class="sxs-lookup"><span data-stu-id="62f53-259">Replace the `<your-domain>` placeholder with the custom domain name of your app.</span></span>
   
        [NewRequest]
        Subject = "CN=<your-domain>"  ; E.g. "CN=www.contoso.com", or "CN=*.contoso.com" for a wildcard certificate
        Exportable = TRUE
        KeyLength = 2048              ; KeyLength can be 2048, 4096, 8192, or 16384 (required minimum is 2048)
        KeySpec = 1
        KeyUsage = 0xA0
        MachineKeySet = True
        ProviderName = "Microsoft RSA SChannel Cryptographic Provider"
        ProviderType = 12
        HashAlgorithm = SHA256
        RequestType = Cert            ; Self-signed certificate
        ValidityPeriod = Years
        ValidityPeriodUnits = 1
   
        [EnhancedKeyUsageExtension]
        OID=1.3.6.1.5.5.7.3.1         ; Server Authentication
   
    <span data-ttu-id="62f53-260">The important parameter is `RequestType = Cert`, which specifies a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="62f53-260">The important parameter is `RequestType = Cert`, which specifies a self-signed certificate.</span></span> 
    <span data-ttu-id="62f53-261">For more information on the options in the CSR, and other available options, see the [Certreq reference documentation](https://technet.microsoft.com/library/dn296456.aspx).</span><span class="sxs-lookup"><span data-stu-id="62f53-261">For more information on the options in the CSR, and other available options, see the [Certreq reference documentation](https://technet.microsoft.com/library/dn296456.aspx).</span></span>
2. <span data-ttu-id="62f53-262">In the command prompt, `CD` to your working directory and run the following command:</span><span class="sxs-lookup"><span data-stu-id="62f53-262">In the command prompt, `CD` to your working directory and run the following command:</span></span>
   
        certreq -new mycert.txt mycert.crt
   
    <span data-ttu-id="62f53-263">Your new self-signed certificate is now installed in the certificate store.</span><span class="sxs-lookup"><span data-stu-id="62f53-263">Your new self-signed certificate is now installed in the certificate store.</span></span>
3. <span data-ttu-id="62f53-264">To export the certificate from the certificate store, press `Win`+`R` and run **certmgr.msc** to launch Certificate Manager.</span><span class="sxs-lookup"><span data-stu-id="62f53-264">To export the certificate from the certificate store, press `Win`+`R` and run **certmgr.msc** to launch Certificate Manager.</span></span> 
   <span data-ttu-id="62f53-265">Select **Personal** > **Certificates**.</span><span class="sxs-lookup"><span data-stu-id="62f53-265">Select **Personal** > **Certificates**.</span></span> <span data-ttu-id="62f53-266">In the **Issued To** column, you should see an entry with your custom domain name, and the CA you used to generate the certificate in the **Issued By** column.</span><span class="sxs-lookup"><span data-stu-id="62f53-266">In the **Issued To** column, you should see an entry with your custom domain name, and the CA you used to generate the certificate in the **Issued By** column.</span></span>
   
    ![insert image of cert manager here][certmgr]
4. <span data-ttu-id="62f53-268">Right-click the certificate and select **All Tasks** > **Export**.</span><span class="sxs-lookup"><span data-stu-id="62f53-268">Right-click the certificate and select **All Tasks** > **Export**.</span></span> <span data-ttu-id="62f53-269">In the **Certificate Export Wizard**, click **Next**, then select **Yes, export the private key**, and then click **Next** again.</span><span class="sxs-lookup"><span data-stu-id="62f53-269">In the **Certificate Export Wizard**, click **Next**, then select **Yes, export the private key**, and then click **Next** again.</span></span>
   
    ![Export the private key][certwiz1]
5. <span data-ttu-id="62f53-271">Select **Personal Information Exchange - PKCS #12**, **Include all certificates in the certificate path if possible**, and **Export all extended properties**.</span><span class="sxs-lookup"><span data-stu-id="62f53-271">Select **Personal Information Exchange - PKCS #12**, **Include all certificates in the certificate path if possible**, and **Export all extended properties**.</span></span> <span data-ttu-id="62f53-272">Then, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="62f53-272">Then, click **Next**.</span></span>
   
   ![include all certs and extended properties][certwiz2]
6. <span data-ttu-id="62f53-274">Select **Password**, and then enter and confirm the password.</span><span class="sxs-lookup"><span data-stu-id="62f53-274">Select **Password**, and then enter and confirm the password.</span></span> <span data-ttu-id="62f53-275">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="62f53-275">Click **Next**.</span></span>
   
   ![specify a password][certwiz3]
7. <span data-ttu-id="62f53-277">Provide a path and filename for the exported certificate, with the extension **.pfx**.</span><span class="sxs-lookup"><span data-stu-id="62f53-277">Provide a path and filename for the exported certificate, with the extension **.pfx**.</span></span> <span data-ttu-id="62f53-278">Click **Next** to finish.</span><span class="sxs-lookup"><span data-stu-id="62f53-278">Click **Next** to finish.</span></span>
   
   ![provide a file path][certwiz4]

<span data-ttu-id="62f53-280">You are now ready to upload the exported PFX file to App Service.</span><span class="sxs-lookup"><span data-stu-id="62f53-280">You are now ready to upload the exported PFX file to App Service.</span></span> <span data-ttu-id="62f53-281">See [Step 2. Upload and bind the custom SSL certificate](#bkmk_configuressl).</span><span class="sxs-lookup"><span data-stu-id="62f53-281">See [Step 2. Upload and bind the custom SSL certificate](#bkmk_configuressl).</span></span>

<a name="bkmk_ssopenssl"></a>

### <a name="generate-a-self-signed-certificate-using-openssl"></a><span data-ttu-id="62f53-282">Generate a self-signed certificate using OpenSSL</span><span class="sxs-lookup"><span data-stu-id="62f53-282">Generate a self-signed certificate using OpenSSL</span></span>
> [!IMPORTANT]
> Self-signed certificates are for test purposes only. Most browsers return errors when visiting a website that's secured by a self-signed certificate. Some browsers may even refuse to navigate to the site. 
> 
> 

1. <span data-ttu-id="62f53-286">Create a text file named **serverauth.cnf**, then copy the following content into it, and then save it in a working directory:</span><span class="sxs-lookup"><span data-stu-id="62f53-286">Create a text file named **serverauth.cnf**, then copy the following content into it, and then save it in a working directory:</span></span>
   
        [ req ]
        default_bits           = 2048
        default_keyfile        = privkey.pem
        distinguished_name     = req_distinguished_name
        attributes             = req_attributes
        x509_extensions        = v3_ca
   
        [ req_distinguished_name ]
        countryName            = Country Name (2 letter code)
        countryName_min            = 2
        countryName_max            = 2
        stateOrProvinceName        = State or Province Name (full name)
        localityName            = Locality Name (eg, city)
        0.organizationName        = Organization Name (eg, company)
        organizationalUnitName        = Organizational Unit Name (eg, section)
        commonName            = Common Name (eg, your app's domain name)
        commonName_max            = 64
        emailAddress            = Email Address
        emailAddress_max        = 40
   
        [ req_attributes ]
        challengePassword        = A challenge password
        challengePassword_min        = 4
        challengePassword_max        = 20
   
        [ v3_ca ]
         subjectKeyIdentifier=hash
         authorityKeyIdentifier=keyid:always,issuer:always
         basicConstraints = CA:false
         keyUsage=nonRepudiation, digitalSignature, keyEncipherment
         extendedKeyUsage = serverAuth
2. <span data-ttu-id="62f53-287">In a command-line terminal, `CD` into your working directory and run the following command:</span><span class="sxs-lookup"><span data-stu-id="62f53-287">In a command-line terminal, `CD` into your working directory and run the following command:</span></span>
   
        openssl req -sha256 -x509 -nodes -days 365 -newkey rsa:2048 -keyout myserver.key -out myserver.crt -config serverauth.cnf
   
    <span data-ttu-id="62f53-288">This command creates two files: **myserver.crt** (the self-signed certificate) and **myserver.key** (the private key), based on the settings in **serverauth.cnf**.</span><span class="sxs-lookup"><span data-stu-id="62f53-288">This command creates two files: **myserver.crt** (the self-signed certificate) and **myserver.key** (the private key), based on the settings in **serverauth.cnf**.</span></span>
3. <span data-ttu-id="62f53-289">Export the certificate to a .pfx file by running the following command:</span><span class="sxs-lookup"><span data-stu-id="62f53-289">Export the certificate to a .pfx file by running the following command:</span></span>
   
        openssl pkcs12 -export -out myserver.pfx -inkey myserver.key -in myserver.crt
   
    <span data-ttu-id="62f53-290">When prompted, define a password to secure the .pfx file.</span><span class="sxs-lookup"><span data-stu-id="62f53-290">When prompted, define a password to secure the .pfx file.</span></span>

<span data-ttu-id="62f53-291">You are now ready to upload the exported PFX file to App Service.</span><span class="sxs-lookup"><span data-stu-id="62f53-291">You are now ready to upload the exported PFX file to App Service.</span></span> <span data-ttu-id="62f53-292">See [Step 2. Upload and bind the custom SSL certificate](#bkmk_configuressl).</span><span class="sxs-lookup"><span data-stu-id="62f53-292">See [Step 2. Upload and bind the custom SSL certificate](#bkmk_configuressl).</span></span>

<a name="bkmk_configuressl"></a>

## <a name="step-2-upload-and-bind-the-custom-ssl-certificate"></a><span data-ttu-id="62f53-293">Step 2.</span><span class="sxs-lookup"><span data-stu-id="62f53-293">Step 2.</span></span> <span data-ttu-id="62f53-294">Upload and bind the custom SSL certificate</span><span class="sxs-lookup"><span data-stu-id="62f53-294">Upload and bind the custom SSL certificate</span></span>
<span data-ttu-id="62f53-295">Before you move on, review the [What you need](#bkmk_domainname) section and verify that:</span><span class="sxs-lookup"><span data-stu-id="62f53-295">Before you move on, review the [What you need](#bkmk_domainname) section and verify that:</span></span>

* <span data-ttu-id="62f53-296">you have a custom domain that maps to your Azure app,</span><span class="sxs-lookup"><span data-stu-id="62f53-296">you have a custom domain that maps to your Azure app,</span></span>
* <span data-ttu-id="62f53-297">your app is running in **Basic** tier or higher, and</span><span class="sxs-lookup"><span data-stu-id="62f53-297">your app is running in **Basic** tier or higher, and</span></span>
* <span data-ttu-id="62f53-298">you have an SSL certificate for the custom domain from a CA.</span><span class="sxs-lookup"><span data-stu-id="62f53-298">you have an SSL certificate for the custom domain from a CA.</span></span>

1. <span data-ttu-id="62f53-299">In your browser, open the **[Azure Portal.](https://portal.azure.com/)**</span><span class="sxs-lookup"><span data-stu-id="62f53-299">In your browser, open the **[Azure Portal.](https://portal.azure.com/)**</span></span>
2. <span data-ttu-id="62f53-300">Click the **App Service** option on the left side of the page.</span><span class="sxs-lookup"><span data-stu-id="62f53-300">Click the **App Service** option on the left side of the page.</span></span>
3. <span data-ttu-id="62f53-301">Click the name of your app to which you want to assign this certificate.</span><span class="sxs-lookup"><span data-stu-id="62f53-301">Click the name of your app to which you want to assign this certificate.</span></span> 
4. <span data-ttu-id="62f53-302">In the **Settings**, Click **SSL certificates**</span><span class="sxs-lookup"><span data-stu-id="62f53-302">In the **Settings**, Click **SSL certificates**</span></span>
5. <span data-ttu-id="62f53-303">Click **Upload Certificate**</span><span class="sxs-lookup"><span data-stu-id="62f53-303">Click **Upload Certificate**</span></span>
6. <span data-ttu-id="62f53-304">Select the .pfx file that you exported in [Step 1](#bkmk_getcert) and specify the password that you create before.</span><span class="sxs-lookup"><span data-stu-id="62f53-304">Select the .pfx file that you exported in [Step 1](#bkmk_getcert) and specify the password that you create before.</span></span> 
   <span data-ttu-id="62f53-305">Then, click **Upload** to upload the certificate.</span><span class="sxs-lookup"><span data-stu-id="62f53-305">Then, click **Upload** to upload the certificate.</span></span> <span data-ttu-id="62f53-306">You should now see your uploaded certificate back in the **SSL certificate** blade.</span><span class="sxs-lookup"><span data-stu-id="62f53-306">You should now see your uploaded certificate back in the **SSL certificate** blade.</span></span>
7. <span data-ttu-id="62f53-307">In the **ssl bindings** section Click on **Add bindings**</span><span class="sxs-lookup"><span data-stu-id="62f53-307">In the **ssl bindings** section Click on **Add bindings**</span></span>
8. <span data-ttu-id="62f53-308">In the **Add SSL Binding** blade use the dropdowns to select the domain name to secure with SSL, and the certificate to use.</span><span class="sxs-lookup"><span data-stu-id="62f53-308">In the **Add SSL Binding** blade use the dropdowns to select the domain name to secure with SSL, and the certificate to use.</span></span> <span data-ttu-id="62f53-309">You may also select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span><span class="sxs-lookup"><span data-stu-id="62f53-309">You may also select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span></span>
   
    ![insert image of SSL Bindings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-configure-ssl-certificate/sslbindings.png)
   
    > [!NOTE] 
    > **IP based SSL** associates a certificate with a domain name by mapping the dedicated public IP address of the server to the domain name. This requires each domain name (contoso.com, fabricam.com, etc.) associated with your service to have a dedicated IP address. This is the traditional method of associating SSL certificates with a web server.  
    >
    > **SNI based SSL** is an extension to SSL and **[Transport Layer Security](http://en.wikipedia.org/wiki/Transport_Layer_Security)** (TLS) that allows multiple domains to share the same IP address, with separate security certificates for each domain. Most modern  browsers (including Internet Explorer, Chrome, Firefox and Opera) support SNI, however older browsers may not support SNI. For more information on SNI, see the **[Server Name Indication](http://en.wikipedia.org/wiki/Server_Name_Indication)** article on Wikipedia.
    > 

9. <span data-ttu-id="62f53-317">Click **Add Binding** to save the changes and enable SSL.</span><span class="sxs-lookup"><span data-stu-id="62f53-317">Click **Add Binding** to save the changes and enable SSL.</span></span>

## <a name="step-3-change-your-domain-name-mapping-ip-based-ssl-only"></a><span data-ttu-id="62f53-318">Step 3.</span><span class="sxs-lookup"><span data-stu-id="62f53-318">Step 3.</span></span> <span data-ttu-id="62f53-319">Change your domain name mapping (IP based SSL only)</span><span class="sxs-lookup"><span data-stu-id="62f53-319">Change your domain name mapping (IP based SSL only)</span></span>
<span data-ttu-id="62f53-320">If you use **SNI SSL** bindings only, skip this section.</span><span class="sxs-lookup"><span data-stu-id="62f53-320">If you use **SNI SSL** bindings only, skip this section.</span></span> <span data-ttu-id="62f53-321">Multiple **SNI SSL** bindings can work together on the existing shared IP address assigned to your app.</span><span class="sxs-lookup"><span data-stu-id="62f53-321">Multiple **SNI SSL** bindings can work together on the existing shared IP address assigned to your app.</span></span> <span data-ttu-id="62f53-322">However, if you create an **IP based SSL** binding, App Service creates a dedicated IP address for the binding because the **IP based SSL** requires one.</span><span class="sxs-lookup"><span data-stu-id="62f53-322">However, if you create an **IP based SSL** binding, App Service creates a dedicated IP address for the binding because the **IP based SSL** requires one.</span></span> <span data-ttu-id="62f53-323">Only one dedicated IP address can be created, therefore only one **IP based SSL** binding may be added.</span><span class="sxs-lookup"><span data-stu-id="62f53-323">Only one dedicated IP address can be created, therefore only one **IP based SSL** binding may be added.</span></span>

<span data-ttu-id="62f53-324">Because of this dedicated IP address, you will need to configure your app further if:</span><span class="sxs-lookup"><span data-stu-id="62f53-324">Because of this dedicated IP address, you will need to configure your app further if:</span></span>

* <span data-ttu-id="62f53-325">You [used an A record to map your custom domain](web-sites-custom-domain-name.md#a) to your Azure app, and you just added an **IP based SSL** binding.</span><span class="sxs-lookup"><span data-stu-id="62f53-325">You [used an A record to map your custom domain](web-sites-custom-domain-name.md#a) to your Azure app, and you just added an **IP based SSL** binding.</span></span> <span data-ttu-id="62f53-326">In this scenario, you need to remap the existing A record to point to the dedicated IP address by following these steps:</span><span class="sxs-lookup"><span data-stu-id="62f53-326">In this scenario, you need to remap the existing A record to point to the dedicated IP address by following these steps:</span></span>
  
  1. <span data-ttu-id="62f53-327">After you have configured an IP based SSL binding, a dedicated IP address is assigned to your app.</span><span class="sxs-lookup"><span data-stu-id="62f53-327">After you have configured an IP based SSL binding, a dedicated IP address is assigned to your app.</span></span> <span data-ttu-id="62f53-328">You can find this IP address on the **Custom domain** page under settings of your app, right above the **Hostnames** section.</span><span class="sxs-lookup"><span data-stu-id="62f53-328">You can find this IP address on the **Custom domain** page under settings of your app, right above the **Hostnames** section.</span></span> <span data-ttu-id="62f53-329">It will be listed as **External IP Address**</span><span class="sxs-lookup"><span data-stu-id="62f53-329">It will be listed as **External IP Address**</span></span>
     
      ![Virtual IP address](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-configure-ssl-certificate/virtual-ip-address.png)
  2. <span data-ttu-id="62f53-331">[Remap the A record for your custom domain name to this new IP address](web-sites-custom-domain-name.md#a).</span><span class="sxs-lookup"><span data-stu-id="62f53-331">[Remap the A record for your custom domain name to this new IP address](web-sites-custom-domain-name.md#a).</span></span>
* <span data-ttu-id="62f53-332">You already have one or more **SNI SSL** bindings in your app, and you just added an **IP based SSL** binding.</span><span class="sxs-lookup"><span data-stu-id="62f53-332">You already have one or more **SNI SSL** bindings in your app, and you just added an **IP based SSL** binding.</span></span> 
  <span data-ttu-id="62f53-333">Once the binding is complete, your *&lt;appname>*.azurewebsites.net domain name points to the new IP address.</span><span class="sxs-lookup"><span data-stu-id="62f53-333">Once the binding is complete, your *&lt;appname>*.azurewebsites.net domain name points to the new IP address.</span></span> 
  <span data-ttu-id="62f53-334">Therefore, any existing [CNAME mapping from the custom domain](web-sites-custom-domain-name.md#cname) to *&lt;appname>*.azurewebsites.net, including the ones that the **SNI SSL** secure, also receives traffic on the new address, which is created for the **IP based SSL** only.</span><span class="sxs-lookup"><span data-stu-id="62f53-334">Therefore, any existing [CNAME mapping from the custom domain](web-sites-custom-domain-name.md#cname) to *&lt;appname>*.azurewebsites.net, including the ones that the **SNI SSL** secure, also receives traffic on the new address, which is created for the **IP based SSL** only.</span></span> <span data-ttu-id="62f53-335">In this scenario, you need to send the **SNI SSL** traffic back to the original shared IP address by following these steps:</span><span class="sxs-lookup"><span data-stu-id="62f53-335">In this scenario, you need to send the **SNI SSL** traffic back to the original shared IP address by following these steps:</span></span>
  
  1. <span data-ttu-id="62f53-336">Identify all [CNAME mappings of custom domains](web-sites-custom-domain-name.md#cname) to your app that has an **SNI SSL** binding.</span><span class="sxs-lookup"><span data-stu-id="62f53-336">Identify all [CNAME mappings of custom domains](web-sites-custom-domain-name.md#cname) to your app that has an **SNI SSL** binding.</span></span>
  2. <span data-ttu-id="62f53-337">Remap each CNAME record to **sni.**&lt;appname>.azurewebsites.net instead of &lt;appname>.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="62f53-337">Remap each CNAME record to **sni.**&lt;appname>.azurewebsites.net instead of &lt;appname>.azurewebsites.net.</span></span>

## <a name="step-4-test-https-for-your-custom-domain"></a><span data-ttu-id="62f53-338">Step 4.</span><span class="sxs-lookup"><span data-stu-id="62f53-338">Step 4.</span></span> <span data-ttu-id="62f53-339">Test HTTPS for your custom domain</span><span class="sxs-lookup"><span data-stu-id="62f53-339">Test HTTPS for your custom domain</span></span>
<span data-ttu-id="62f53-340">All that's left to do now is to make sure that HTTPS works for your custom domain.</span><span class="sxs-lookup"><span data-stu-id="62f53-340">All that's left to do now is to make sure that HTTPS works for your custom domain.</span></span> <span data-ttu-id="62f53-341">In various browsers, browse to `https://<your.custom.domain>` to see that it serves up your app.</span><span class="sxs-lookup"><span data-stu-id="62f53-341">In various browsers, browse to `https://<your.custom.domain>` to see that it serves up your app.</span></span>

* <span data-ttu-id="62f53-342">If your app gives you certificate validation errors, you're probably using a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="62f53-342">If your app gives you certificate validation errors, you're probably using a self-signed certificate.</span></span>
* <span data-ttu-id="62f53-343">If that's not the case, you may have left out intermediate certificates when you export your .pfx certificate.</span><span class="sxs-lookup"><span data-stu-id="62f53-343">If that's not the case, you may have left out intermediate certificates when you export your .pfx certificate.</span></span> <span data-ttu-id="62f53-344">Go back to [What you need](#bkmk_domainname) to verify that your CSR meets all the requirements by App Service.</span><span class="sxs-lookup"><span data-stu-id="62f53-344">Go back to [What you need](#bkmk_domainname) to verify that your CSR meets all the requirements by App Service.</span></span>

<a name="bkmk_enforce"></a>

## <a name="enforce-https-on-your-app"></a><span data-ttu-id="62f53-345">Enforce HTTPS on your app</span><span class="sxs-lookup"><span data-stu-id="62f53-345">Enforce HTTPS on your app</span></span>
<span data-ttu-id="62f53-346">If you still want to allow HTTP access to your app, skip this step.</span><span class="sxs-lookup"><span data-stu-id="62f53-346">If you still want to allow HTTP access to your app, skip this step.</span></span> <span data-ttu-id="62f53-347">App Service does *not* enforce HTTPS, so visitors can still access your app using HTTP.</span><span class="sxs-lookup"><span data-stu-id="62f53-347">App Service does *not* enforce HTTPS, so visitors can still access your app using HTTP.</span></span> <span data-ttu-id="62f53-348">If you want to enforce HTTPS for your app, you can define a rewrite rule in the `web.config` file for your app.</span><span class="sxs-lookup"><span data-stu-id="62f53-348">If you want to enforce HTTPS for your app, you can define a rewrite rule in the `web.config` file for your app.</span></span> <span data-ttu-id="62f53-349">Every App Service app has this file, regardless of the language framework of your app.</span><span class="sxs-lookup"><span data-stu-id="62f53-349">Every App Service app has this file, regardless of the language framework of your app.</span></span>

> [!NOTE]
> There is language-specific redirection of requests. ASP.NET MVC can use the [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter instead of the rewrite rule in `web.config` (see [Deploy a secure ASP.NET MVC 5 app to a web app](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md)).
> 
> 

<span data-ttu-id="62f53-352">Follow these steps:</span><span class="sxs-lookup"><span data-stu-id="62f53-352">Follow these steps:</span></span>

1. <span data-ttu-id="62f53-353">Navigate to the Kudu debug console for your app.</span><span class="sxs-lookup"><span data-stu-id="62f53-353">Navigate to the Kudu debug console for your app.</span></span> <span data-ttu-id="62f53-354">Its address is `https://<appname>.scm.azurewebsites.net/DebugConsole`.</span><span class="sxs-lookup"><span data-stu-id="62f53-354">Its address is `https://<appname>.scm.azurewebsites.net/DebugConsole`.</span></span>
2. <span data-ttu-id="62f53-355">In the debug console, CD to `D:\home\site\wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="62f53-355">In the debug console, CD to `D:\home\site\wwwroot`.</span></span>
3. <span data-ttu-id="62f53-356">Open `web.config` by clicking the pencil button.</span><span class="sxs-lookup"><span data-stu-id="62f53-356">Open `web.config` by clicking the pencil button.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-configure-ssl-certificate/openwebconfig.png)
   
    <span data-ttu-id="62f53-357">If you deploy your app with Visual Studio or Git, App Service automatically generates the appropriate `web.config` for your .NET, PHP, Node.js, or Python app in the application root.</span><span class="sxs-lookup"><span data-stu-id="62f53-357">If you deploy your app with Visual Studio or Git, App Service automatically generates the appropriate `web.config` for your .NET, PHP, Node.js, or Python app in the application root.</span></span> 
    <span data-ttu-id="62f53-358">If `web.config` doesn't exist, run `touch web.config` in the web-based command prompt to create it.</span><span class="sxs-lookup"><span data-stu-id="62f53-358">If `web.config` doesn't exist, run `touch web.config` in the web-based command prompt to create it.</span></span> <span data-ttu-id="62f53-359">Or, you can create it in your local project and redeploy your code.</span><span class="sxs-lookup"><span data-stu-id="62f53-359">Or, you can create it in your local project and redeploy your code.</span></span>
4. <span data-ttu-id="62f53-360">If you had to create a `web.config`, copy the following code into it and save it.</span><span class="sxs-lookup"><span data-stu-id="62f53-360">If you had to create a `web.config`, copy the following code into it and save it.</span></span> <span data-ttu-id="62f53-361">If you opened an existing web.config, then you just need to copy the entire `<rule>` tag into your `web.config`'s `configuration/system.webServer/rewrite/rules` element.</span><span class="sxs-lookup"><span data-stu-id="62f53-361">If you opened an existing web.config, then you just need to copy the entire `<rule>` tag into your `web.config`'s `configuration/system.webServer/rewrite/rules` element.</span></span>
   
        <?xml version="1.0" encoding="UTF-8"?>
        <configuration>
          <system.webServer>
            <rewrite>
              <rules>
                <!-- BEGIN rule TAG FOR HTTPS REDIRECT -->
                <rule name="Force HTTPS" enabled="true">
                  <match url="(.*)" ignoreCase="false" />
                  <conditions>
                    <add input="{HTTPS}" pattern="off" />
                  </conditions>
                  <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
                </rule>
                <!-- END rule TAG FOR HTTPS REDIRECT -->
              </rules>
            </rewrite>
          </system.webServer>
        </configuration>
   
    <span data-ttu-id="62f53-362">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user requests a page using HTTP.</span><span class="sxs-lookup"><span data-stu-id="62f53-362">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user requests a page using HTTP.</span></span> <span data-ttu-id="62f53-363">It redirects from http://contoso.com to https://contoso.com.</span><span class="sxs-lookup"><span data-stu-id="62f53-363">It redirects from http://contoso.com to https://contoso.com.</span></span>
   
   > [!IMPORTANT]
   > If there are already other `<rule>` tags in your `web.config`, then place the copied `<rule>` tag before the other `<rule>` tags.
   > 
   > 
5. <span data-ttu-id="62f53-365">Save the file in the Kudu debug console.</span><span class="sxs-lookup"><span data-stu-id="62f53-365">Save the file in the Kudu debug console.</span></span> <span data-ttu-id="62f53-366">It should take effect immediately redirect all requests to HTTPS.</span><span class="sxs-lookup"><span data-stu-id="62f53-366">It should take effect immediately redirect all requests to HTTPS.</span></span>

<span data-ttu-id="62f53-367">For more information on the IIS URL Rewrite module, see the [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span><span class="sxs-lookup"><span data-stu-id="62f53-367">For more information on the IIS URL Rewrite module, see the [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span></span>

## <a name="more-resources"></a><span data-ttu-id="62f53-368">More Resources</span><span class="sxs-lookup"><span data-stu-id="62f53-368">More Resources</span></span>
* [<span data-ttu-id="62f53-369">Microsoft Azure Trust Center</span><span class="sxs-lookup"><span data-stu-id="62f53-369">Microsoft Azure Trust Center</span></span>](/support/trust-center/security/)
* [<span data-ttu-id="62f53-370">Configuration options unlocked in Azure Web Sites</span><span class="sxs-lookup"><span data-stu-id="62f53-370">Configuration options unlocked in Azure Web Sites</span></span>](https://azure.microsoft.com/blog/2014/01/28/more-to-explore-configuration-options-unlocked-in-windows-azure-web-sites/)
* [<span data-ttu-id="62f53-371">Enable diagnostic logging</span><span class="sxs-lookup"><span data-stu-id="62f53-371">Enable diagnostic logging</span></span>](web-sites-enable-diagnostic-log.md)
* [<span data-ttu-id="62f53-372">Configure web apps in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="62f53-372">Configure web apps in Azure App Service</span></span>](web-sites-configure.md)
* [<span data-ttu-id="62f53-373">Azure Management Portal</span><span class="sxs-lookup"><span data-stu-id="62f53-373">Azure Management Portal</span></span>](https://manage.windowsazure.com)

> [!NOTE]
> If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter app in App Service. No credit cards required; no commitments.
> 
> 

[customdomain]: web-sites-custom-domain-name.md
[iiscsr]: http://technet.microsoft.com/library/cc732906(WS.10).aspx
[cas]: http://social.technet.microsoft.com/wiki/contents/articles/31634.microsoft-trusted-root-certificate-program-participants-v-2016-april.aspx
[installcertiis]: http://technet.microsoft.com/library/cc771816(WS.10).aspx
[exportcertiis]: http://technet.microsoft.com/library/cc731386(WS.10).aspx
[openssl]: http://www.openssl.org/
[portal]: https://manage.windowsazure.com/
[tls]: http://en.wikipedia.org/wiki/Transport_Layer_Security
[staticip]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-configure-ssl-certificate/staticip.png
[website]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-configure-ssl-certificate/sslwebsite.png
[scale]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-configure-ssl-certificate/sslscale.png
[standard]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-configure-ssl-certificate/sslreserved.png
[pricing]: /pricing/details/
[configure]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-configure-ssl-certificate/sslconfig.png
[uploadcert]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-configure-ssl-certificate/ssluploadcert.png
[uploadcertdlg]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-configure-ssl-certificate/ssluploaddlg.png
[sslbindings]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-configure-ssl-certificate/sslbindings.png
[sni]: http://en.wikipedia.org/wiki/Server_Name_Indication
[certmgr]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-configure-ssl-certificate/waws-certmgr.png
[certwiz1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-configure-ssl-certificate/waws-certwiz1.png
[certwiz2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-configure-ssl-certificate/waws-certwiz2.png
[certwiz3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-configure-ssl-certificate/waws-certwiz3.png
[certwiz4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-configure-ssl-certificate/waws-certwiz4.png


















