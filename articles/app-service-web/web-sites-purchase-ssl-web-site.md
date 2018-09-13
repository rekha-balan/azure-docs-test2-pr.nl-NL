---
title: Add an SSL certificate to your Azure App Service app | Microsoft Docs
description: Learn how to add an SSL certificate to your App Service app.
services: app-service
documentationcenter: .net
author: ahmedelnably
manager: stefsch
editor: cephalin
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2016
ms.author: apurvajo;aelnably
ms.openlocfilehash: eb12563923318110d80be859e85af25586e1a01a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564134"
---
# <a name="add-an-ssl-certificate-to-your-app-service-app"></a><span data-ttu-id="4bbe6-103">Add an SSL certificate to your App Service app</span><span class="sxs-lookup"><span data-stu-id="4bbe6-103">Add an SSL certificate to your App Service app</span></span>
> [!div class="op_single_selector"]
> * [Buy SSL certificate in Azure](web-sites-purchase-ssl-web-site.md)
> * [Use SSL certificate from elsewhere](web-sites-configure-ssl-certificate.md)
> 
> 

<span data-ttu-id="4bbe6-106">By default, [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) enables HTTPS for your web app with a wildcard certificate for the \*.azurewebsites.net domain.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-106">By default, [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) enables HTTPS for your web app with a wildcard certificate for the \*.azurewebsites.net domain.</span></span> <span data-ttu-id="4bbe6-107">If you don't plan to set up a custom domain, you can benefit from the default HTTPS certificate.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-107">If you don't plan to set up a custom domain, you can benefit from the default HTTPS certificate.</span></span> <span data-ttu-id="4bbe6-108">But, like all [wildcard domains](https://casecurity.org/2014/02/26/pros-and-cons-of-single-domain-multi-domain-and-wildcard-certificates), the Azure wildcard certificate is not as secure as using a custom domain with your own certificate.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-108">But, like all [wildcard domains](https://casecurity.org/2014/02/26/pros-and-cons-of-single-domain-multi-domain-and-wildcard-certificates), the Azure wildcard certificate is not as secure as using a custom domain with your own certificate.</span></span>

<span data-ttu-id="4bbe6-109">App Service gives you a simplified way to purchase and manage an SSL certificate in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-109">App Service gives you a simplified way to purchase and manage an SSL certificate in the Azure portal.</span></span> 

<span data-ttu-id="4bbe6-110">This article explains how to buy and set up an SSL certificate for your [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) app.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-110">This article explains how to buy and set up an SSL certificate for your [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) app.</span></span> 

> [!NOTE]
> You can't use SSL certificates for custom domain names for apps that are hosted in a Free or Shared App Service plan. To use SSL certificates, your web app must be hosted in a Basic, Standard, or Premium App Service plan. Changing your subscription type might change how much you are billed for your subscription. For more information, see [App Service pricing](https://azure.microsoft.com/pricing/details/web-sites/).
> 
> 

> [!WARNING]
> Do not attempt to purchase an SSL certificate by using a subscription for which you have not attached a valid credit card. This might cause your subscription to be disabled. 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="4bbe6-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4bbe6-117">Prerequisites</span></span>
<span data-ttu-id="4bbe6-118">To enable HTTPS for a custom domain, start by [mapping a custom domain name to your Azure app](web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="4bbe6-118">To enable HTTPS for a custom domain, start by [mapping a custom domain name to your Azure app](web-sites-custom-domain-name.md).</span></span>

<span data-ttu-id="4bbe6-119">Before you request an SSL certificate, first determine which domain names you will secure with the certificate.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-119">Before you request an SSL certificate, first determine which domain names you will secure with the certificate.</span></span> <span data-ttu-id="4bbe6-120">This determines the type of certificate you need.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-120">This determines the type of certificate you need.</span></span> <span data-ttu-id="4bbe6-121">If you want to secure a single domain name, like contoso.com *or* www.contoso.com, you can use a Standard (basic) certificate.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-121">If you want to secure a single domain name, like contoso.com *or* www.contoso.com, you can use a Standard (basic) certificate.</span></span> <span data-ttu-id="4bbe6-122">If you need to secure multiple domain names, like contoso.com, www.contoso.com, *and* mail.contoso.com, you can get a [wildcard certificate](http://en.wikipedia.org/wiki/Wildcard_certificate).</span><span class="sxs-lookup"><span data-stu-id="4bbe6-122">If you need to secure multiple domain names, like contoso.com, www.contoso.com, *and* mail.contoso.com, you can get a [wildcard certificate](http://en.wikipedia.org/wiki/Wildcard_certificate).</span></span>

## <a name="bkmk_purchasecert"></a><span data-ttu-id="4bbe6-123">Purchase an SSL certificate</span><span class="sxs-lookup"><span data-stu-id="4bbe6-123">Purchase an SSL certificate</span></span>

1. <span data-ttu-id="4bbe6-124">In the [Azure portal](https://portal.azure.com/), in the menu, select **Browse**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-124">In the [Azure portal](https://portal.azure.com/), in the menu, select **Browse**.</span></span> <span data-ttu-id="4bbe6-125">In the **Search** box, type **App Service Certificate**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-125">In the **Search** box, type **App Service Certificate**.</span></span> <span data-ttu-id="4bbe6-126">In the search results, select **App Service Certificates**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-126">In the search results, select **App Service Certificates**.</span></span> 

   ![Create using browse](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-purchase-ssl-web-site/browse.jpg)
   
2. <span data-ttu-id="4bbe6-128">On the **App Service Certificates** page, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-128">On the **App Service Certificates** page, select **Add**.</span></span> 

   ![Add a certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-purchase-ssl-web-site/add.jpg)

3. <span data-ttu-id="4bbe6-130">Enter a **name** for your SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-130">Enter a **name** for your SSL certificate.</span></span>
4. <span data-ttu-id="4bbe6-131">Enter the **host name**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-131">Enter the **host name**.</span></span>
   
   > [!WARNING]
   > This is one of the most critical parts of the purchase process. Be sure that you enter the correct host name (custom domain name) that you want this certificate to secure. *Do not* add "www" to the beginning of your host name. For example, if your custom domain name is www.contoso.com, enter **contoso.com** in the **Host Name** box. The certificate will protect www and root domains. 
   > 

5. <span data-ttu-id="4bbe6-137">Select your **subscription**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-137">Select your **subscription**.</span></span> 
   
   <span data-ttu-id="4bbe6-138">If you have multiple subscriptions, create your SSL certificate in the same subscription that you use for your custom domain or web app.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-138">If you have multiple subscriptions, create your SSL certificate in the same subscription that you use for your custom domain or web app.</span></span>

6. <span data-ttu-id="4bbe6-139">Select or create a **resource group**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-139">Select or create a **resource group**.</span></span>
   
   <span data-ttu-id="4bbe6-140">You can use resource groups to manage related Azure resources as a unit.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-140">You can use resource groups to manage related Azure resources as a unit.</span></span> <span data-ttu-id="4bbe6-141">Resource groups are useful when you want to establish role-based access control (RBAC) rules for your apps.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-141">Resource groups are useful when you want to establish role-based access control (RBAC) rules for your apps.</span></span> <span data-ttu-id="4bbe6-142">For more information, see Managing your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-142">For more information, see Managing your Azure resources.</span></span>

7. <span data-ttu-id="4bbe6-143">Select the **certificate SKU**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-143">Select the **certificate SKU**.</span></span> 
   
   <span data-ttu-id="4bbe6-144">Select the certificate SKU that fits your need, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-144">Select the certificate SKU that fits your need, and then select **Create**.</span></span> 
   
   <span data-ttu-id="4bbe6-145">You can choose from two SKUS in App Service:</span><span class="sxs-lookup"><span data-stu-id="4bbe6-145">You can choose from two SKUS in App Service:</span></span>
   * <span data-ttu-id="4bbe6-146">**S1**: Standard certificate with one-year validity and auto renewal</span><span class="sxs-lookup"><span data-stu-id="4bbe6-146">**S1**: Standard certificate with one-year validity and auto renewal</span></span>  
   * <span data-ttu-id="4bbe6-147">**W1**: Wildcard certificate with one-year validity and auto renewal</span><span class="sxs-lookup"><span data-stu-id="4bbe6-147">**W1**: Wildcard certificate with one-year validity and auto renewal</span></span>       
  
    ![Certificate SKU](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-purchase-ssl-web-site/SKU.jpg)

    <span data-ttu-id="4bbe6-149">For more information, see [App Service pricing](https://azure.microsoft.com/pricing/details/web-sites/).</span><span class="sxs-lookup"><span data-stu-id="4bbe6-149">For more information, see [App Service pricing](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>

> [!NOTE]
> Creating an SSL certificate can take up to 10 minutes. The process involves multiple steps that take place in the background.  
> 
> 

## <a name="bkmk_StoreKeyVault"></a><span data-ttu-id="4bbe6-152">Store the certificate in Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="4bbe6-152">Store the certificate in Azure Key Vault</span></span>

1. <span data-ttu-id="4bbe6-153">When you've completed the SSL certificate purchase, in the Azure portal, go to the **App Service Certificates** blade.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-153">When you've completed the SSL certificate purchase, in the Azure portal, go to the **App Service Certificates** blade.</span></span>

   ![Certificate ready to store in Key Vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-purchase-ssl-web-site/ReadyKV.jpg)
   
   <span data-ttu-id="4bbe6-155">Note that the certificate status is **Pending Issuance**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-155">Note that the certificate status is **Pending Issuance**.</span></span> <span data-ttu-id="4bbe6-156">You need to complete a few steps before you can start using this certificate.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-156">You need to complete a few steps before you can start using this certificate.</span></span>

2. <span data-ttu-id="4bbe6-157">On the **Certificate Properties** blade, select **Certificate Configuration**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-157">On the **Certificate Properties** blade, select **Certificate Configuration**.</span></span> <span data-ttu-id="4bbe6-158">To store this certificate in Key Vault, select **Step 1: Store**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-158">To store this certificate in Key Vault, select **Step 1: Store**.</span></span>
3. <span data-ttu-id="4bbe6-159">On the **Key Vault Status** blade, to select an existing key vault to store this certificate, select **Key Vault Repository**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-159">On the **Key Vault Status** blade, to select an existing key vault to store this certificate, select **Key Vault Repository**.</span></span>  <span data-ttu-id="4bbe6-160">To create a new key vault in the same subscription and resource group, select **Create New Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-160">To create a new key vault in the same subscription and resource group, select **Create New Key Vault**.</span></span>

   ![Create new key vault](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-purchase-ssl-web-site/NewKV.jpg)
   
   > [!NOTE]
   > Azure Key Vault offers minimal charges for storing the certificate. For more information, see [Azure Key Vault pricing](https://azure.microsoft.com/pricing/details/key-vault/).
   > 
   > 

4. <span data-ttu-id="4bbe6-164">After you have selected the Key Vault repository to store the certificate in, at the top of **Key Vault Status** blade, select the **Store** button.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-164">After you have selected the Key Vault repository to store the certificate in, at the top of **Key Vault Status** blade, select the **Store** button.</span></span>  
   
<span data-ttu-id="4bbe6-165">To verify your selection, you can click your browser's refresh button.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-165">To verify your selection, you can click your browser's refresh button.</span></span> <span data-ttu-id="4bbe6-166">A green check mark shows that this step is finished.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-166">A green check mark shows that this step is finished.</span></span>

## <a name="bkmk_VerifyOwnership"></a><span data-ttu-id="4bbe6-167">Verify the domain ownership</span><span class="sxs-lookup"><span data-stu-id="4bbe6-167">Verify the domain ownership</span></span>

1. <span data-ttu-id="4bbe6-168">On the **Certificate Configuration** blade, select **Step 2: Verify**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-168">On the **Certificate Configuration** blade, select **Step 2: Verify**.</span></span>
2. <span data-ttu-id="4bbe6-169">Select verification options by using the following information.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-169">Select verification options by using the following information.</span></span> 

<span data-ttu-id="4bbe6-170">App Service certificates support three types of domain verification:</span><span class="sxs-lookup"><span data-stu-id="4bbe6-170">App Service certificates support three types of domain verification:</span></span>

   * <span data-ttu-id="4bbe6-171">Domain verification</span><span class="sxs-lookup"><span data-stu-id="4bbe6-171">Domain verification</span></span>
   * <span data-ttu-id="4bbe6-172">Mail verification</span><span class="sxs-lookup"><span data-stu-id="4bbe6-172">Mail verification</span></span>
   * <span data-ttu-id="4bbe6-173">Manual verification</span><span class="sxs-lookup"><span data-stu-id="4bbe6-173">Manual verification</span></span>

### <a name="domain-verification"></a><span data-ttu-id="4bbe6-174">Domain verification</span><span class="sxs-lookup"><span data-stu-id="4bbe6-174">Domain verification</span></span> 
     
<span data-ttu-id="4bbe6-175">Domain verification is the most convenient process, but *only* if you have [purchased your custom domain from Azure App Service](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="4bbe6-175">Domain verification is the most convenient process, but *only* if you have [purchased your custom domain from Azure App Service](custom-dns-web-site-buydomains-web-app.md).</span></span>

1. <span data-ttu-id="4bbe6-176">To complete this step, select **Verify**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-176">To complete this step, select **Verify**.</span></span>
2. <span data-ttu-id="4bbe6-177">To update the certificate status after verification is complete, select **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-177">To update the certificate status after verification is complete, select **Refresh**.</span></span> <span data-ttu-id="4bbe6-178">It might take a few minutes for verification to complete.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-178">It might take a few minutes for verification to complete.</span></span>

### <a name="mail-verification"></a><span data-ttu-id="4bbe6-179">Mail verification</span><span class="sxs-lookup"><span data-stu-id="4bbe6-179">Mail verification</span></span>
     
<span data-ttu-id="4bbe6-180">With a custom domain, a verification email is sent to the email address associated with the domain.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-180">With a custom domain, a verification email is sent to the email address associated with the domain.</span></span> 

1. <span data-ttu-id="4bbe6-181">To complete the email verification step, open the email and click the verification link.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-181">To complete the email verification step, open the email and click the verification link.</span></span> 
2. <span data-ttu-id="4bbe6-182">If you need to resend the verification email, click the **Resend Email** button.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-182">If you need to resend the verification email, click the **Resend Email** button.</span></span>

### <a name="manual-verification"></a><span data-ttu-id="4bbe6-183">Manual verification</span><span class="sxs-lookup"><span data-stu-id="4bbe6-183">Manual verification</span></span>    
     
<span data-ttu-id="4bbe6-184">**HTML web page verification (works only with a Standard certificate SKU)**</span><span class="sxs-lookup"><span data-stu-id="4bbe6-184">**HTML web page verification (works only with a Standard certificate SKU)**</span></span>

1. <span data-ttu-id="4bbe6-185">Create an HTML file named starfield.html.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-185">Create an HTML file named starfield.html.</span></span> <span data-ttu-id="4bbe6-186">The contents of this file should be the precise name of the domain verification token.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-186">The contents of this file should be the precise name of the domain verification token.</span></span> <span data-ttu-id="4bbe6-187">(You can copy the token from the **Domain Verification Status** blade.)</span><span class="sxs-lookup"><span data-stu-id="4bbe6-187">(You can copy the token from the **Domain Verification Status** blade.)</span></span>
2. <span data-ttu-id="4bbe6-188">Upload this file to the root of the web server where you host your domain.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-188">Upload this file to the root of the web server where you host your domain.</span></span> <span data-ttu-id="4bbe6-189">For example, /.well-known/pki-validation/starfield.html.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-189">For example, /.well-known/pki-validation/starfield.html.</span></span>
3.  <span data-ttu-id="4bbe6-190">When verification is finished, to update the certificate status, select **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-190">When verification is finished, to update the certificate status, select **Refresh**.</span></span> <span data-ttu-id="4bbe6-191">It might take a few minutes for verification to finish.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-191">It might take a few minutes for verification to finish.</span></span>

    <span data-ttu-id="4bbe6-192">For example, if you are buying a standard certificate for **contosocertdemo.com**, with a domain verification token **tgjgthq8d11ttaeah97s3fr2sh**, a web request made to **http://contosocertdemo.com/.well-known/pki-validation/starfield.html** should return **tgjgthq8d11ttaeah97s3fr2sh**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-192">For example, if you are buying a standard certificate for **contosocertdemo.com**, with a domain verification token **tgjgthq8d11ttaeah97s3fr2sh**, a web request made to **http://contosocertdemo.com/.well-known/pki-validation/starfield.html** should return **tgjgthq8d11ttaeah97s3fr2sh**.</span></span>

<span data-ttu-id="4bbe6-193">**DNS TXT record verification**</span><span class="sxs-lookup"><span data-stu-id="4bbe6-193">**DNS TXT record verification**</span></span>
        
1. <span data-ttu-id="4bbe6-194">Using your DNS manager, create a TXT record on the **@** subdomain with a value equal to the **domain verification token.**</span><span class="sxs-lookup"><span data-stu-id="4bbe6-194">Using your DNS manager, create a TXT record on the **@** subdomain with a value equal to the **domain verification token.**</span></span>
2. <span data-ttu-id="4bbe6-195">To update the certificate status when verification is finished, select **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-195">To update the certificate status when verification is finished, select **Refresh**.</span></span> <span data-ttu-id="4bbe6-196">It might take few minutes for verification to finish.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-196">It might take few minutes for verification to finish.</span></span>
 
   <span data-ttu-id="4bbe6-197">For example, to perform validation for a wildcard certificate with host name **\*.contosocertdemo.com** or **\*.subdomain.contosocertdemo.com**, and domain verification token **tgjgthq8d11ttaeah97s3fr2sh**, create a TXT record on **contosocertdemo.com** that has the value **tgjgthq8d11ttaeah97s3fr2sh**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-197">For example, to perform validation for a wildcard certificate with host name **\*.contosocertdemo.com** or **\*.subdomain.contosocertdemo.com**, and domain verification token **tgjgthq8d11ttaeah97s3fr2sh**, create a TXT record on **contosocertdemo.com** that has the value **tgjgthq8d11ttaeah97s3fr2sh**.</span></span>     

## <a name="bkmk_AssignCertificate"></a><span data-ttu-id="4bbe6-198">Assign the certificate to an App Service app</span><span class="sxs-lookup"><span data-stu-id="4bbe6-198">Assign the certificate to an App Service app</span></span>

> [!NOTE]
> Before you complete the steps in this section, you must associate a custom domain name with your app. For more information, see [Configure a custom domain name for a web app](web-sites-custom-domain-name.md).
> 
> 

1. <span data-ttu-id="4bbe6-201">In the [Azure portal](https://portal.azure.com/), in the menu, select **App Service**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-201">In the [Azure portal](https://portal.azure.com/), in the menu, select **App Service**.</span></span>
2. <span data-ttu-id="4bbe6-202">Select the name of the app that you want to assign this certificate to.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-202">Select the name of the app that you want to assign this certificate to.</span></span> 
3. <span data-ttu-id="4bbe6-203">Go to **Settings** > **SSL certificates** > **Import App Service Certificate**, and then select the certificate.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-203">Go to **Settings** > **SSL certificates** > **Import App Service Certificate**, and then select the certificate.</span></span>

   ![Import certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

4. <span data-ttu-id="4bbe6-205">In the **SSL bindings** section, select **Add bindings**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-205">In the **SSL bindings** section, select **Add bindings**.</span></span>
5. <span data-ttu-id="4bbe6-206">On the **Add SSL Binding** blade, select the domain name that you want to secure with the SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-206">On the **Add SSL Binding** blade, select the domain name that you want to secure with the SSL certificate.</span></span> <span data-ttu-id="4bbe6-207">Select the certificate that you want to use.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-207">Select the certificate that you want to use.</span></span> <span data-ttu-id="4bbe6-208">You might also want to select whether to use [Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication) or IP-based SSL.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-208">You might also want to select whether to use [Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication) or IP-based SSL.</span></span>

   ![SSL bindings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-purchase-ssl-web-site/SSLBindings.png)
   
    * <span data-ttu-id="4bbe6-210">To associate a certificate with a domain name, IP-based SSL maps the dedicated public IP address of the server to the domain name.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-210">To associate a certificate with a domain name, IP-based SSL maps the dedicated public IP address of the server to the domain name.</span></span> <span data-ttu-id="4bbe6-211">When you use IP-based SSL, each domain name (for example, contoso.com or fabricam.com) associated with your service must have a dedicated IP address.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-211">When you use IP-based SSL, each domain name (for example, contoso.com or fabricam.com) associated with your service must have a dedicated IP address.</span></span> <span data-ttu-id="4bbe6-212">This is the traditional method for associating an SSL certificate with a web server.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-212">This is the traditional method for associating an SSL certificate with a web server.</span></span>
    * <span data-ttu-id="4bbe6-213">SNI-based SSL is an extension to SSL and [Transport Layer Security](http://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS).</span><span class="sxs-lookup"><span data-stu-id="4bbe6-213">SNI-based SSL is an extension to SSL and [Transport Layer Security](http://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS).</span></span> <span data-ttu-id="4bbe6-214">When you use SNI-based SSL, multiple domains can share the same IP address.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-214">When you use SNI-based SSL, multiple domains can share the same IP address.</span></span> <span data-ttu-id="4bbe6-215">Each domain has a separate security certificate.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-215">Each domain has a separate security certificate.</span></span> <span data-ttu-id="4bbe6-216">Most modern browsers, including Internet Explorer, Chrome, Firefox, and Opera, support SNI.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-216">Most modern browsers, including Internet Explorer, Chrome, Firefox, and Opera, support SNI.</span></span> <span data-ttu-id="4bbe6-217">Older browsers might not support SNI.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-217">Older browsers might not support SNI.</span></span> <span data-ttu-id="4bbe6-218">For more information about SNI, see [Server Name Indication](http://en.wikipedia.org/wiki/Server_Name_Indication) in Wikipedia.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-218">For more information about SNI, see [Server Name Indication](http://en.wikipedia.org/wiki/Server_Name_Indication) in Wikipedia.</span></span>

6. <span data-ttu-id="4bbe6-219">To save your changes and enable SSL, select **Add Binding**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-219">To save your changes and enable SSL, select **Add Binding**.</span></span>

<span data-ttu-id="4bbe6-220">If you select **IP-based SSL** and your custom domain is configured using an A record, you must complete the following additional steps.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-220">If you select **IP-based SSL** and your custom domain is configured using an A record, you must complete the following additional steps.</span></span>

1.  <span data-ttu-id="4bbe6-221">After you set up an IP-based SSL binding, a dedicated IP address is assigned to your app.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-221">After you set up an IP-based SSL binding, a dedicated IP address is assigned to your app.</span></span> <span data-ttu-id="4bbe6-222">To find the IP address, go to **Settings** > **Custom domain**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-222">To find the IP address, go to **Settings** > **Custom domain**.</span></span> <span data-ttu-id="4bbe6-223">Right above the **Hostnames** section, your IP address is listed as **External IP Address**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-223">Right above the **Hostnames** section, your IP address is listed as **External IP Address**.</span></span>

   ![IP-based SSL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)
    
  <span data-ttu-id="4bbe6-225">Note that this IP address is different from the virtual IP address you previously used to configure the A record for your domain.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-225">Note that this IP address is different from the virtual IP address you previously used to configure the A record for your domain.</span></span> <span data-ttu-id="4bbe6-226">If your app is set up to use SNI-based SSL, or if it's not set up to use SSL, no IP address is listed here.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-226">If your app is set up to use SNI-based SSL, or if it's not set up to use SSL, no IP address is listed here.</span></span>

2.  <span data-ttu-id="4bbe6-227">Using the tools provided by your domain name registrar, modify the A record for your custom domain name so that it points to the IP address you used in the preceding step.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-227">Using the tools provided by your domain name registrar, modify the A record for your custom domain name so that it points to the IP address you used in the preceding step.</span></span>

3.  <span data-ttu-id="4bbe6-228">To verify that the certificate has been configured correctly, go to your app by using HTTPS:// instead of HTTP://.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-228">To verify that the certificate has been configured correctly, go to your app by using HTTPS:// instead of HTTP://.</span></span>

## <a name="bkmk_Export"></a><span data-ttu-id="4bbe6-229">Export your App Service certificate</span><span class="sxs-lookup"><span data-stu-id="4bbe6-229">Export your App Service certificate</span></span>
<span data-ttu-id="4bbe6-230">You can create a local PFX copy of an App Service certificate.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-230">You can create a local PFX copy of an App Service certificate.</span></span> <span data-ttu-id="4bbe6-231">When you have a local copy, you can use the certificate with other Azure services.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-231">When you have a local copy, you can use the certificate with other Azure services.</span></span> <span data-ttu-id="4bbe6-232">For more information, see our blog post [Create a local PFX copy of your App Service certificate](https://blogs.msdn.microsoft.com/appserviceteam/2017/02/24/creating-a-local-pfx-copy-of-app-service-certificate/).</span><span class="sxs-lookup"><span data-stu-id="4bbe6-232">For more information, see our blog post [Create a local PFX copy of your App Service certificate](https://blogs.msdn.microsoft.com/appserviceteam/2017/02/24/creating-a-local-pfx-copy-of-app-service-certificate/).</span></span>

## <a name="bkmk_Renew"></a><span data-ttu-id="4bbe6-233">Auto renew your App Service certificate</span><span class="sxs-lookup"><span data-stu-id="4bbe6-233">Auto renew your App Service certificate</span></span>
<span data-ttu-id="4bbe6-234">To set auto renew settings for your certificate, or to manually renew your certificate, on the **Certificate Properties** blade, select **Auto Renew Settings**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-234">To set auto renew settings for your certificate, or to manually renew your certificate, on the **Certificate Properties** blade, select **Auto Renew Settings**.</span></span> 

![Auto renew settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-purchase-ssl-web-site/autorenew.png)

<span data-ttu-id="4bbe6-236">To automatically renew your certificate before it expires, set **Auto Renew** to **On**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-236">To automatically renew your certificate before it expires, set **Auto Renew** to **On**.</span></span> <span data-ttu-id="4bbe6-237">This is the default option.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-237">This is the default option.</span></span> <span data-ttu-id="4bbe6-238">If auto renewal is turned on, we attempt to renew your certificate starting on the 90th day before the certificate expires.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-238">If auto renewal is turned on, we attempt to renew your certificate starting on the 90th day before the certificate expires.</span></span> <span data-ttu-id="4bbe6-239">If you created SSL bindings on your App Service apps in the Azure portal, the bindings also are updated when the new certificate is ready (like in rekey and sync scenarios).</span><span class="sxs-lookup"><span data-stu-id="4bbe6-239">If you created SSL bindings on your App Service apps in the Azure portal, the bindings also are updated when the new certificate is ready (like in rekey and sync scenarios).</span></span> 

<span data-ttu-id="4bbe6-240">If you want to handle renewals manually, set **Auto Renew** to **Off**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-240">If you want to handle renewals manually, set **Auto Renew** to **Off**.</span></span> <span data-ttu-id="4bbe6-241">You can manually renew an App Service certificate only when its expiration date is within 90 days.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-241">You can manually renew an App Service certificate only when its expiration date is within 90 days.</span></span>

## <a name="bkmk_Rekey"></a><span data-ttu-id="4bbe6-242">Rekey and sync your certificate</span><span class="sxs-lookup"><span data-stu-id="4bbe6-242">Rekey and sync your certificate</span></span>

1. <span data-ttu-id="4bbe6-243">If you ever need to rekey your certificate (for security reasons), on the **Certificate Properties** blade, select **Rekey and Sync**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-243">If you ever need to rekey your certificate (for security reasons), on the **Certificate Properties** blade, select **Rekey and Sync**.</span></span> 
2. <span data-ttu-id="4bbe6-244">Select **Rekey**.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-244">Select **Rekey**.</span></span> <span data-ttu-id="4bbe6-245">The process might take up to 10 minutes to finish.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-245">The process might take up to 10 minutes to finish.</span></span> 

   ![Rekey SSL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-purchase-ssl-web-site/Rekey.jpg)

<span data-ttu-id="4bbe6-247">Here's some additional information about rekeying:</span><span class="sxs-lookup"><span data-stu-id="4bbe6-247">Here's some additional information about rekeying:</span></span>

* <span data-ttu-id="4bbe6-248">Rekeying your certificate rolls the certificate with a new certificate.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-248">Rekeying your certificate rolls the certificate with a new certificate.</span></span> <span data-ttu-id="4bbe6-249">The new certificate is issued from the certificate authority.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-249">The new certificate is issued from the certificate authority.</span></span>
* <span data-ttu-id="4bbe6-250">You are not charged for rekeying for the lifetime of the certificate.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-250">You are not charged for rekeying for the lifetime of the certificate.</span></span> 
* <span data-ttu-id="4bbe6-251">Rekeying your certificate gives the certificate a **Pending Issuance** status.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-251">Rekeying your certificate gives the certificate a **Pending Issuance** status.</span></span> 
* <span data-ttu-id="4bbe6-252">When the certificate is ready, to prevent disruption to the service, be sure that you sync your resources by using the certificate.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-252">When the certificate is ready, to prevent disruption to the service, be sure that you sync your resources by using the certificate.</span></span>
* <span data-ttu-id="4bbe6-253">The sync option is not available for certificates that are not yet assigned to a web app.</span><span class="sxs-lookup"><span data-stu-id="4bbe6-253">The sync option is not available for certificates that are not yet assigned to a web app.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4bbe6-254">Next steps</span><span class="sxs-lookup"><span data-stu-id="4bbe6-254">Next steps</span></span>

* [<span data-ttu-id="4bbe6-255">Secure your app's custom domain with HTTPS</span><span class="sxs-lookup"><span data-stu-id="4bbe6-255">Secure your app's custom domain with HTTPS</span></span>](web-sites-configure-ssl-certificate.md)
* [<span data-ttu-id="4bbe6-256">Buy and configure a custom domain name in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4bbe6-256">Buy and configure a custom domain name in Azure App Service</span></span>](custom-dns-web-site-buydomains-web-app.md)
* [<span data-ttu-id="4bbe6-257">Microsoft Azure Trust Center</span><span class="sxs-lookup"><span data-stu-id="4bbe6-257">Microsoft Azure Trust Center</span></span>](https://azure.microsoft.com/en-us/support/trust-center/)

> [!NOTE]
> To get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/). You can create a short-lived, starter web app in App Service. A credit card is not required, and no commitments are required.
> 
> 










