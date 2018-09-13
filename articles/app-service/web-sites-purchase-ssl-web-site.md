---
title: Buy and Configure an SSL Certificate for your Azure App Service | Microsoft Docs
description: Learn how to buy an App Service certificate and bind it to your App Service app
services: app-service
documentationcenter: .net
author: cephalin
manager: cfowler
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2017
ms.author: apurvajo;cephalin
ms.openlocfilehash: c223e8fb000686aedefa1c02e93c1c8cbb30ec73
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855645"
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a><span data-ttu-id="6718e-103">Buy and Configure an SSL Certificate for your Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6718e-103">Buy and Configure an SSL Certificate for your Azure App Service</span></span>

<span data-ttu-id="6718e-104">This tutorial shows you how to secure your web app by purchasing an SSL certificate for your **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, securely storing it in [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-whatis), and associating it with a custom domain.</span><span class="sxs-lookup"><span data-stu-id="6718e-104">This tutorial shows you how to secure your web app by purchasing an SSL certificate for your **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, securely storing it in [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-whatis), and associating it with a custom domain.</span></span>

## <a name="step-1---sign-in-to-azure"></a><span data-ttu-id="6718e-105">Step 1 - Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="6718e-105">Step 1 - Sign in to Azure</span></span>

<span data-ttu-id="6718e-106">Sign in to the Azure portal at http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="6718e-106">Sign in to the Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---place-an-ssl-certificate-order"></a><span data-ttu-id="6718e-107">Step 2 - Place an SSL Certificate order</span><span class="sxs-lookup"><span data-stu-id="6718e-107">Step 2 - Place an SSL Certificate order</span></span>

<span data-ttu-id="6718e-108">You can place an SSL Certificate order by creating a new [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL) In the **Azure portal**.</span><span class="sxs-lookup"><span data-stu-id="6718e-108">You can place an SSL Certificate order by creating a new [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL) In the **Azure portal**.</span></span>

![Certificate Creation](./media/app-service-web-purchase-ssl-web-site/createssl.png)

<span data-ttu-id="6718e-110">Enter a friendly **Name** for your SSL certificate and enter the **Domain Name**</span><span class="sxs-lookup"><span data-stu-id="6718e-110">Enter a friendly **Name** for your SSL certificate and enter the **Domain Name**</span></span>

> [!NOTE]
> <span data-ttu-id="6718e-111">This step is one of the most critical parts of the purchase process.</span><span class="sxs-lookup"><span data-stu-id="6718e-111">This step is one of the most critical parts of the purchase process.</span></span> <span data-ttu-id="6718e-112">Make sure to enter correct host name (custom domain) that you want to protect with this certificate.</span><span class="sxs-lookup"><span data-stu-id="6718e-112">Make sure to enter correct host name (custom domain) that you want to protect with this certificate.</span></span> <span data-ttu-id="6718e-113">**DO NOT** prepend the Host name with WWW.</span><span class="sxs-lookup"><span data-stu-id="6718e-113">**DO NOT** prepend the Host name with WWW.</span></span> 
>

<span data-ttu-id="6718e-114">Select your **Subscription**, **Resource Group**, and **Certificate SKU**</span><span class="sxs-lookup"><span data-stu-id="6718e-114">Select your **Subscription**, **Resource Group**, and **Certificate SKU**</span></span>

> [!TIP]
> <span data-ttu-id="6718e-115">App Service Certificates can be used for any Azure or non-Azure Services and is not limited to App Services.</span><span class="sxs-lookup"><span data-stu-id="6718e-115">App Service Certificates can be used for any Azure or non-Azure Services and is not limited to App Services.</span></span> <span data-ttu-id="6718e-116">To do so , you need to create a local PFX copy of an App Service certificate that you can use it anywhere you want.</span><span class="sxs-lookup"><span data-stu-id="6718e-116">To do so , you need to create a local PFX copy of an App Service certificate that you can use it anywhere you want.</span></span> <span data-ttu-id="6718e-117">For more information, read [Creating a local PFX copy of an App Service Certificate](https://blogs.msdn.microsoft.com/appserviceteam/2017/02/24/creating-a-local-pfx-copy-of-app-service-certificate/).</span><span class="sxs-lookup"><span data-stu-id="6718e-117">For more information, read [Creating a local PFX copy of an App Service Certificate](https://blogs.msdn.microsoft.com/appserviceteam/2017/02/24/creating-a-local-pfx-copy-of-app-service-certificate/).</span></span>
>

## <a name="step-3---store-the-certificate-in-azure-key-vault"></a><span data-ttu-id="6718e-118">Step 3 - Store the certificate in Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="6718e-118">Step 3 - Store the certificate in Azure Key Vault</span></span>

> [!NOTE]
> <span data-ttu-id="6718e-119">[Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-whatis) is an Azure service that helps safeguard cryptographic keys and secrets used by cloud applications and services.</span><span class="sxs-lookup"><span data-stu-id="6718e-119">[Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-whatis) is an Azure service that helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>
>

<span data-ttu-id="6718e-120">Once the SSL Certificate purchase is complete, you need to open the [App Service Certificates](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) page.</span><span class="sxs-lookup"><span data-stu-id="6718e-120">Once the SSL Certificate purchase is complete, you need to open the [App Service Certificates](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) page.</span></span>

![insert image of ready to store in KV](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

<span data-ttu-id="6718e-122">The certificate status is **“Pending Issuance”** as there are few more steps you need to complete before you can start using this certificate.</span><span class="sxs-lookup"><span data-stu-id="6718e-122">The certificate status is **“Pending Issuance”** as there are few more steps you need to complete before you can start using this certificate.</span></span>

<span data-ttu-id="6718e-123">Click **Certificate Configuration** inside the Certificate Properties page and Click on **Step 1: Store** to store this certificate in Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="6718e-123">Click **Certificate Configuration** inside the Certificate Properties page and Click on **Step 1: Store** to store this certificate in Azure Key Vault.</span></span>

<span data-ttu-id="6718e-124">From the **Key Vault Status** page, click **Key Vault Repository** to choose an existing Key Vault to store this certificate **OR Create New Key Vault** to create new Key Vault inside same subscription and resource group.</span><span class="sxs-lookup"><span data-stu-id="6718e-124">From the **Key Vault Status** page, click **Key Vault Repository** to choose an existing Key Vault to store this certificate **OR Create New Key Vault** to create new Key Vault inside same subscription and resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="6718e-125">Azure Key Vault has minimal charges for storing this certificate.</span><span class="sxs-lookup"><span data-stu-id="6718e-125">Azure Key Vault has minimal charges for storing this certificate.</span></span>
> <span data-ttu-id="6718e-126">For more information, see **[Azure Key Vault Pricing Details](https://azure.microsoft.com/pricing/details/key-vault/)**.</span><span class="sxs-lookup"><span data-stu-id="6718e-126">For more information, see **[Azure Key Vault Pricing Details](https://azure.microsoft.com/pricing/details/key-vault/)**.</span></span>
>

<span data-ttu-id="6718e-127">Once you have selected the Key Vault Repository to store this certificate in, the **Store** option should show success.</span><span class="sxs-lookup"><span data-stu-id="6718e-127">Once you have selected the Key Vault Repository to store this certificate in, the **Store** option should show success.</span></span>

![insert image of store success in KV](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-the-domain-ownership"></a><span data-ttu-id="6718e-129">Step 4 - Verify the Domain Ownership</span><span class="sxs-lookup"><span data-stu-id="6718e-129">Step 4 - Verify the Domain Ownership</span></span>

<span data-ttu-id="6718e-130">From the same **Certificate Configuration** page you used in Step 3, click **Step 2: Verify**.</span><span class="sxs-lookup"><span data-stu-id="6718e-130">From the same **Certificate Configuration** page you used in Step 3, click **Step 2: Verify**.</span></span>

<span data-ttu-id="6718e-131">Choose the preferred domain verification method.</span><span class="sxs-lookup"><span data-stu-id="6718e-131">Choose the preferred domain verification method.</span></span> 

<span data-ttu-id="6718e-132">There are four types of domain verification supported by App Service Certificates: App Service, Domain, and Manual Verification.</span><span class="sxs-lookup"><span data-stu-id="6718e-132">There are four types of domain verification supported by App Service Certificates: App Service, Domain, and Manual Verification.</span></span> <span data-ttu-id="6718e-133">These verification types are explained in more details in the [Advanced section](#advanced).</span><span class="sxs-lookup"><span data-stu-id="6718e-133">These verification types are explained in more details in the [Advanced section](#advanced).</span></span>

> [!NOTE]
> <span data-ttu-id="6718e-134">**App Service Verification** is the most convenient option when the domain you want to verify is already mapped to an App Service app in the same subscription.</span><span class="sxs-lookup"><span data-stu-id="6718e-134">**App Service Verification** is the most convenient option when the domain you want to verify is already mapped to an App Service app in the same subscription.</span></span> <span data-ttu-id="6718e-135">It takes advantage of the fact that the App Service app has already verified the domain ownership.</span><span class="sxs-lookup"><span data-stu-id="6718e-135">It takes advantage of the fact that the App Service app has already verified the domain ownership.</span></span>
>

<span data-ttu-id="6718e-136">Click on **Verify** button to complete this step.</span><span class="sxs-lookup"><span data-stu-id="6718e-136">Click on **Verify** button to complete this step.</span></span>

![insert image of domain verification](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

<span data-ttu-id="6718e-138">After clicking **Verify**, use the **Refresh** button until the **Verify** option should show success.</span><span class="sxs-lookup"><span data-stu-id="6718e-138">After clicking **Verify**, use the **Refresh** button until the **Verify** option should show success.</span></span>

![insert image of verify success in KV](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-to-app-service-app"></a><span data-ttu-id="6718e-140">Step 5 - Assign Certificate to App Service App</span><span class="sxs-lookup"><span data-stu-id="6718e-140">Step 5 - Assign Certificate to App Service App</span></span>

> [!NOTE]
> <span data-ttu-id="6718e-141">Before performing the steps in this section, you must have associated a custom domain name with your app.</span><span class="sxs-lookup"><span data-stu-id="6718e-141">Before performing the steps in this section, you must have associated a custom domain name with your app.</span></span> <span data-ttu-id="6718e-142">For more information, see **[Configuring a custom domain name for a web app.](app-service-web-tutorial-custom-domain.md)**</span><span class="sxs-lookup"><span data-stu-id="6718e-142">For more information, see **[Configuring a custom domain name for a web app.](app-service-web-tutorial-custom-domain.md)**</span></span>
>

<span data-ttu-id="6718e-143">In the **[Azure portal](https://portal.azure.com/)**, click the **App Service** option on the left of the page.</span><span class="sxs-lookup"><span data-stu-id="6718e-143">In the **[Azure portal](https://portal.azure.com/)**, click the **App Service** option on the left of the page.</span></span>

<span data-ttu-id="6718e-144">Click the name of your app to which you want to assign this certificate.</span><span class="sxs-lookup"><span data-stu-id="6718e-144">Click the name of your app to which you want to assign this certificate.</span></span>

<span data-ttu-id="6718e-145">In the **Settings**, click **SSL settings**.</span><span class="sxs-lookup"><span data-stu-id="6718e-145">In the **Settings**, click **SSL settings**.</span></span>

<span data-ttu-id="6718e-146">Click **Import App Service Certificate** and select the certificate that you just purchased.</span><span class="sxs-lookup"><span data-stu-id="6718e-146">Click **Import App Service Certificate** and select the certificate that you just purchased.</span></span>

![insert image of Import Certificate](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

<span data-ttu-id="6718e-148">In the **ssl bindings** section Click on **Add bindings**, and use the dropdowns to select the domain name to secure with SSL, and the certificate to use.</span><span class="sxs-lookup"><span data-stu-id="6718e-148">In the **ssl bindings** section Click on **Add bindings**, and use the dropdowns to select the domain name to secure with SSL, and the certificate to use.</span></span> <span data-ttu-id="6718e-149">You may also select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span><span class="sxs-lookup"><span data-stu-id="6718e-149">You may also select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span></span>

![insert image of SSL Bindings](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

<span data-ttu-id="6718e-151">Click **Add Binding** to save the changes and enable SSL.</span><span class="sxs-lookup"><span data-stu-id="6718e-151">Click **Add Binding** to save the changes and enable SSL.</span></span>

> [!NOTE]
> <span data-ttu-id="6718e-152">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps.</span><span class="sxs-lookup"><span data-stu-id="6718e-152">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps.</span></span> <span data-ttu-id="6718e-153">These are explained in more details in the [Advanced section](#Advanced).</span><span class="sxs-lookup"><span data-stu-id="6718e-153">These are explained in more details in the [Advanced section](#Advanced).</span></span>

<span data-ttu-id="6718e-154">At this point, you should be able to visit your app using `HTTPS://` instead of `HTTP://` to verify that the certificate has been configured correctly.</span><span class="sxs-lookup"><span data-stu-id="6718e-154">At this point, you should be able to visit your app using `HTTPS://` instead of `HTTP://` to verify that the certificate has been configured correctly.</span></span>

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a><span data-ttu-id="6718e-155">Step 6 - Management tasks</span><span class="sxs-lookup"><span data-stu-id="6718e-155">Step 6 - Management tasks</span></span>

### <a name="azure-cli"></a><span data-ttu-id="6718e-156">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6718e-156">Azure CLI</span></span>

[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")] 

### <a name="powershell"></a><span data-ttu-id="6718e-157">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6718e-157">PowerShell</span></span>

[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="advanced"></a><span data-ttu-id="6718e-158">Advanced</span><span class="sxs-lookup"><span data-stu-id="6718e-158">Advanced</span></span>

### <a name="verifying-domain-ownership"></a><span data-ttu-id="6718e-159">Verifying Domain Ownership</span><span class="sxs-lookup"><span data-stu-id="6718e-159">Verifying Domain Ownership</span></span>

<span data-ttu-id="6718e-160">There are two other types of domain verification supported by App service Certificates: domain verification and manual verification.</span><span class="sxs-lookup"><span data-stu-id="6718e-160">There are two other types of domain verification supported by App service Certificates: domain verification and manual verification.</span></span>

#### <a name="domain-verification"></a><span data-ttu-id="6718e-161">Domain Verification</span><span class="sxs-lookup"><span data-stu-id="6718e-161">Domain Verification</span></span>

<span data-ttu-id="6718e-162">Choose this option only for [an App Service domain that you purchased from Azure.](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="6718e-162">Choose this option only for [an App Service domain that you purchased from Azure.](custom-dns-web-site-buydomains-web-app.md).</span></span> <span data-ttu-id="6718e-163">Azure automatically adds the verification TXT record for you and completes the process.</span><span class="sxs-lookup"><span data-stu-id="6718e-163">Azure automatically adds the verification TXT record for you and completes the process.</span></span>

#### <a name="manual-verification"></a><span data-ttu-id="6718e-164">Manual Verification</span><span class="sxs-lookup"><span data-stu-id="6718e-164">Manual Verification</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6718e-165">HTML Web Page Verification (only works with Standard Certificate SKU)</span><span class="sxs-lookup"><span data-stu-id="6718e-165">HTML Web Page Verification (only works with Standard Certificate SKU)</span></span>
>

1. <span data-ttu-id="6718e-166">Create an HTML file named **"starfield.html"**</span><span class="sxs-lookup"><span data-stu-id="6718e-166">Create an HTML file named **"starfield.html"**</span></span>

1. <span data-ttu-id="6718e-167">Content of this file should be the exact name of the Domain Verification Token.</span><span class="sxs-lookup"><span data-stu-id="6718e-167">Content of this file should be the exact name of the Domain Verification Token.</span></span> <span data-ttu-id="6718e-168">(You can copy the token from the Domain Verification Status page)</span><span class="sxs-lookup"><span data-stu-id="6718e-168">(You can copy the token from the Domain Verification Status page)</span></span>

1. <span data-ttu-id="6718e-169">Upload this file at the root of the web server hosting your domain `/.well-known/pki-validation/starfield.html`</span><span class="sxs-lookup"><span data-stu-id="6718e-169">Upload this file at the root of the web server hosting your domain `/.well-known/pki-validation/starfield.html`</span></span>

1. <span data-ttu-id="6718e-170">Click **Refresh** to update the certificate status after verification is completed.</span><span class="sxs-lookup"><span data-stu-id="6718e-170">Click **Refresh** to update the certificate status after verification is completed.</span></span> <span data-ttu-id="6718e-171">It might take few minutes for verification to complete.</span><span class="sxs-lookup"><span data-stu-id="6718e-171">It might take few minutes for verification to complete.</span></span>

> [!TIP]
> <span data-ttu-id="6718e-172">Verify in a terminal using `curl -G http://<domain>/.well-known/pki-validation/starfield.html` the response should contain the `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="6718e-172">Verify in a terminal using `curl -G http://<domain>/.well-known/pki-validation/starfield.html` the response should contain the `<verification-token>`.</span></span>

#### <a name="dns-txt-record-verification"></a><span data-ttu-id="6718e-173">DNS TXT Record Verification</span><span class="sxs-lookup"><span data-stu-id="6718e-173">DNS TXT Record Verification</span></span>

1. <span data-ttu-id="6718e-174">Using your DNS manager, Create a TXT record on the `@` subdomain with value equal to the Domain Verification Token.</span><span class="sxs-lookup"><span data-stu-id="6718e-174">Using your DNS manager, Create a TXT record on the `@` subdomain with value equal to the Domain Verification Token.</span></span>
1. <span data-ttu-id="6718e-175">Click **“Refresh”** to update the Certificate status after verification is completed.</span><span class="sxs-lookup"><span data-stu-id="6718e-175">Click **“Refresh”** to update the Certificate status after verification is completed.</span></span>

> [!TIP]
> <span data-ttu-id="6718e-176">You need to create a TXT record on `@.<domain>` with value `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="6718e-176">You need to create a TXT record on `@.<domain>` with value `<verification-token>`.</span></span>

### <a name="assign-certificate-to-app-service-app"></a><span data-ttu-id="6718e-177">Assign Certificate to App Service App</span><span class="sxs-lookup"><span data-stu-id="6718e-177">Assign Certificate to App Service App</span></span>

<span data-ttu-id="6718e-178">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps:</span><span class="sxs-lookup"><span data-stu-id="6718e-178">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps:</span></span>

<span data-ttu-id="6718e-179">After you have configured an IP based SSL binding, a dedicated IP address is assigned to your app.</span><span class="sxs-lookup"><span data-stu-id="6718e-179">After you have configured an IP based SSL binding, a dedicated IP address is assigned to your app.</span></span> <span data-ttu-id="6718e-180">You can find this IP address on the **Custom domain** page under settings of your app, right above the **Hostnames** section.</span><span class="sxs-lookup"><span data-stu-id="6718e-180">You can find this IP address on the **Custom domain** page under settings of your app, right above the **Hostnames** section.</span></span> <span data-ttu-id="6718e-181">It is listed as **External IP Address**</span><span class="sxs-lookup"><span data-stu-id="6718e-181">It is listed as **External IP Address**</span></span>

![insert image of IP SSL](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

<span data-ttu-id="6718e-183">This IP address is different than the virtual IP address used previously to configure the A record for your domain.</span><span class="sxs-lookup"><span data-stu-id="6718e-183">This IP address is different than the virtual IP address used previously to configure the A record for your domain.</span></span> <span data-ttu-id="6718e-184">If you are configured to use SNI based SSL, or are not configured to use SSL, no address is listed for this entry.</span><span class="sxs-lookup"><span data-stu-id="6718e-184">If you are configured to use SNI based SSL, or are not configured to use SSL, no address is listed for this entry.</span></span>

<span data-ttu-id="6718e-185">Using the tools provided by your domain name registrar, modify the A record for your custom domain name to point to the IP address from the previous step.</span><span class="sxs-lookup"><span data-stu-id="6718e-185">Using the tools provided by your domain name registrar, modify the A record for your custom domain name to point to the IP address from the previous step.</span></span>

## <a name="rekey-and-sync-the-certificate"></a><span data-ttu-id="6718e-186">Rekey and Sync the Certificate</span><span class="sxs-lookup"><span data-stu-id="6718e-186">Rekey and Sync the Certificate</span></span>

<span data-ttu-id="6718e-187">If you ever need to rekey your certificate, select the **Rekey and Sync** option from the **Certificate Properties** page.</span><span class="sxs-lookup"><span data-stu-id="6718e-187">If you ever need to rekey your certificate, select the **Rekey and Sync** option from the **Certificate Properties** page.</span></span>

<span data-ttu-id="6718e-188">Click **Rekey** Button to initiate the process.</span><span class="sxs-lookup"><span data-stu-id="6718e-188">Click **Rekey** Button to initiate the process.</span></span> <span data-ttu-id="6718e-189">This process can take 1-10 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="6718e-189">This process can take 1-10 minutes to complete.</span></span>

![insert image of Rekey SSL](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

<span data-ttu-id="6718e-191">Rekeying your certificate rolls the certificate with a new certificate issued from the certificate authority.</span><span class="sxs-lookup"><span data-stu-id="6718e-191">Rekeying your certificate rolls the certificate with a new certificate issued from the certificate authority.</span></span>

## <a name="renew-the-certificate"></a><span data-ttu-id="6718e-192">Renew the certificate</span><span class="sxs-lookup"><span data-stu-id="6718e-192">Renew the certificate</span></span>

<span data-ttu-id="6718e-193">To turn on automatic renewal of your certificate at anytime, click **Auto Renew Settings** in the certificate management page.</span><span class="sxs-lookup"><span data-stu-id="6718e-193">To turn on automatic renewal of your certificate at anytime, click **Auto Renew Settings** in the certificate management page.</span></span> <span data-ttu-id="6718e-194">Select **On** and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="6718e-194">Select **On** and click **Save**.</span></span> <span data-ttu-id="6718e-195">Certificates can start automatically renewing 90 days before expiration if you have automatic renewal turned on.</span><span class="sxs-lookup"><span data-stu-id="6718e-195">Certificates can start automatically renewing 90 days before expiration if you have automatic renewal turned on.</span></span>

![](./media/app-service-web-purchase-ssl-web-site/auto-renew.png)

<span data-ttu-id="6718e-196">To manually renew the certificate instead, click **Manual Renew** instead.</span><span class="sxs-lookup"><span data-stu-id="6718e-196">To manually renew the certificate instead, click **Manual Renew** instead.</span></span> <span data-ttu-id="6718e-197">You can request to manually renew your certificate 60 days before expiration.</span><span class="sxs-lookup"><span data-stu-id="6718e-197">You can request to manually renew your certificate 60 days before expiration.</span></span>

> [!NOTE]
> <span data-ttu-id="6718e-198">The renewed certificate is not automatically bound to your app, whether you renewed it manually or it renewed automatically.</span><span class="sxs-lookup"><span data-stu-id="6718e-198">The renewed certificate is not automatically bound to your app, whether you renewed it manually or it renewed automatically.</span></span> <span data-ttu-id="6718e-199">To bind it to your app, see [Renew certificates](./app-service-web-tutorial-custom-ssl.md#renew-certificates).</span><span class="sxs-lookup"><span data-stu-id="6718e-199">To bind it to your app, see [Renew certificates](./app-service-web-tutorial-custom-ssl.md#renew-certificates).</span></span> 

<a name="notrenewed"></a>
## <a name="why-is-my-certificate-not-auto-renewed"></a><span data-ttu-id="6718e-200">Why is my certificate not auto-renewed?</span><span class="sxs-lookup"><span data-stu-id="6718e-200">Why is my certificate not auto-renewed?</span></span>

<span data-ttu-id="6718e-201">If your SSL certificate is configured for auto-renewal, but it is not automatically renewed, you may have a pending domain verification.</span><span class="sxs-lookup"><span data-stu-id="6718e-201">If your SSL certificate is configured for auto-renewal, but it is not automatically renewed, you may have a pending domain verification.</span></span> <span data-ttu-id="6718e-202">Note that:</span><span class="sxs-lookup"><span data-stu-id="6718e-202">Note that:</span></span> 

- <span data-ttu-id="6718e-203">GoDaddy, which generates App Service certificates, requires domain verification once every two years.</span><span class="sxs-lookup"><span data-stu-id="6718e-203">GoDaddy, which generates App Service certificates, requires domain verification once every two years.</span></span> <span data-ttu-id="6718e-204">The domain administrator receives an email once every three years to verify the domain.</span><span class="sxs-lookup"><span data-stu-id="6718e-204">The domain administrator receives an email once every three years to verify the domain.</span></span> <span data-ttu-id="6718e-205">Failure to check the email or verify your domain prevents the App Service certificate from being automatically renewed.</span><span class="sxs-lookup"><span data-stu-id="6718e-205">Failure to check the email or verify your domain prevents the App Service certificate from being automatically renewed.</span></span> 
- <span data-ttu-id="6718e-206">Because of a change in GoDaddy policy, all App Service certificates issued prior to March 1, 2017 require reverification of domain at the time of next renewal (even if the auto-renewal is enabled for the certificate).</span><span class="sxs-lookup"><span data-stu-id="6718e-206">Because of a change in GoDaddy policy, all App Service certificates issued prior to March 1, 2017 require reverification of domain at the time of next renewal (even if the auto-renewal is enabled for the certificate).</span></span> <span data-ttu-id="6718e-207">Check your email and complete this one-time domain verification to continue the auto-renewal of the App Service certificate.</span><span class="sxs-lookup"><span data-stu-id="6718e-207">Check your email and complete this one-time domain verification to continue the auto-renewal of the App Service certificate.</span></span> 

## <a name="more-resources"></a><span data-ttu-id="6718e-208">More resources</span><span class="sxs-lookup"><span data-stu-id="6718e-208">More resources</span></span>

* [<span data-ttu-id="6718e-209">Enforce HTTPS</span><span class="sxs-lookup"><span data-stu-id="6718e-209">Enforce HTTPS</span></span>](app-service-web-tutorial-custom-ssl.md#enforce-https)
* [<span data-ttu-id="6718e-210">Enforce TLS 1.1/1.2</span><span class="sxs-lookup"><span data-stu-id="6718e-210">Enforce TLS 1.1/1.2</span></span>](app-service-web-tutorial-custom-ssl.md#enforce-tls-versions)
* [<span data-ttu-id="6718e-211">Use an SSL certificate in your application code in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6718e-211">Use an SSL certificate in your application code in Azure App Service</span></span>](app-service-web-ssl-cert-load.md)
* [<span data-ttu-id="6718e-212">FAQ : App Service Certificates</span><span class="sxs-lookup"><span data-stu-id="6718e-212">FAQ : App Service Certificates</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/24/faq-app-service-certificates/)
