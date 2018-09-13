---
title: Map an existing custom DNS name to Azure Web Apps | Microsoft Docs
description: Learn how to add an existing custom DNS domain name (vanity domain) to a web app, mobile app backend, or API app in Azure App Service.
keywords: app service, azure app service, domain mapping, domain name, existing domain, hostname
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: ''
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/18/2018
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 30199005db93f9a43a37d2c72bb34dd772265419
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868168"
---
# <a name="tutorial-map-an-existing-custom-dns-name-to-azure-web-apps"></a><span data-ttu-id="b4c12-104">Tutorial: Map an existing custom DNS name to Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="b4c12-104">Tutorial: Map an existing custom DNS name to Azure Web Apps</span></span>

<span data-ttu-id="b4c12-105">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span><span class="sxs-lookup"><span data-stu-id="b4c12-105">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="b4c12-106">This tutorial shows you how to map an existing custom DNS name to Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="b4c12-106">This tutorial shows you how to map an existing custom DNS name to Azure Web Apps.</span></span>

![Portal navigation to Azure app](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

<span data-ttu-id="b4c12-108">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="b4c12-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b4c12-109">Map a subdomain (for example, `www.contoso.com`) by using a CNAME record</span><span class="sxs-lookup"><span data-stu-id="b4c12-109">Map a subdomain (for example, `www.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="b4c12-110">Map a root domain (for example, `contoso.com`) by using an A record</span><span class="sxs-lookup"><span data-stu-id="b4c12-110">Map a root domain (for example, `contoso.com`) by using an A record</span></span>
> * <span data-ttu-id="b4c12-111">Map a wildcard domain (for example, `*.contoso.com`) by using a CNAME record</span><span class="sxs-lookup"><span data-stu-id="b4c12-111">Map a wildcard domain (for example, `*.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="b4c12-112">Redirect the default URL to a custom directory</span><span class="sxs-lookup"><span data-stu-id="b4c12-112">Redirect the default URL to a custom directory</span></span>
> * <span data-ttu-id="b4c12-113">Automate domain mapping with scripts</span><span class="sxs-lookup"><span data-stu-id="b4c12-113">Automate domain mapping with scripts</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4c12-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b4c12-114">Prerequisites</span></span>

<span data-ttu-id="b4c12-115">To complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="b4c12-115">To complete this tutorial:</span></span>

* <span data-ttu-id="b4c12-116">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span><span class="sxs-lookup"><span data-stu-id="b4c12-116">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>
* <span data-ttu-id="b4c12-117">Purchase a domain name and make sure you have access to the DNS registry for your domain provider (such as GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="b4c12-117">Purchase a domain name and make sure you have access to the DNS registry for your domain provider (such as GoDaddy).</span></span>

  <span data-ttu-id="b4c12-118">For example, to add DNS entries for `contoso.com` and `www.contoso.com`, you must be able to configure the DNS settings for the `contoso.com` root domain.</span><span class="sxs-lookup"><span data-stu-id="b4c12-118">For example, to add DNS entries for `contoso.com` and `www.contoso.com`, you must be able to configure the DNS settings for the `contoso.com` root domain.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b4c12-119">If you don't have an existing domain name, consider [purchasing a domain using the Azure portal](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="b4c12-119">If you don't have an existing domain name, consider [purchasing a domain using the Azure portal](custom-dns-web-site-buydomains-web-app.md).</span></span> 

## <a name="prepare-the-app"></a><span data-ttu-id="b4c12-120">Prepare the app</span><span class="sxs-lookup"><span data-stu-id="b4c12-120">Prepare the app</span></span>

<span data-ttu-id="b4c12-121">To map a custom DNS name to a web app, the web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span><span class="sxs-lookup"><span data-stu-id="b4c12-121">To map a custom DNS name to a web app, the web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="b4c12-122">In this step, you make sure that the App Service app is in the supported pricing tier.</span><span class="sxs-lookup"><span data-stu-id="b4c12-122">In this step, you make sure that the App Service app is in the supported pricing tier.</span></span>

[!INCLUDE [app-service-dev-test-note](../../includes/app-service-dev-test-note.md)]

### <a name="sign-in-to-azure"></a><span data-ttu-id="b4c12-123">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="b4c12-123">Sign in to Azure</span></span>

<span data-ttu-id="b4c12-124">Open the [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="b4c12-124">Open the [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-to-the-app-in-the-azure-portal"></a><span data-ttu-id="b4c12-125">Navigate to the app in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b4c12-125">Navigate to the app in the Azure portal</span></span>

<span data-ttu-id="b4c12-126">From the left menu, select **App Services**, and then select the name of the app.</span><span class="sxs-lookup"><span data-stu-id="b4c12-126">From the left menu, select **App Services**, and then select the name of the app.</span></span>

![Portal navigation to Azure app](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="b4c12-128">You see the management page of the App Service app.</span><span class="sxs-lookup"><span data-stu-id="b4c12-128">You see the management page of the App Service app.</span></span>  

<a name="checkpricing"></a>

### <a name="check-the-pricing-tier"></a><span data-ttu-id="b4c12-129">Check the pricing tier</span><span class="sxs-lookup"><span data-stu-id="b4c12-129">Check the pricing tier</span></span>

<span data-ttu-id="b4c12-130">In the left navigation of the app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span><span class="sxs-lookup"><span data-stu-id="b4c12-130">In the left navigation of the app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Scale-up menu](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="b4c12-132">The app's current tier is highlighted by a blue border.</span><span class="sxs-lookup"><span data-stu-id="b4c12-132">The app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="b4c12-133">Check to make sure that the app is not in the **F1** tier.</span><span class="sxs-lookup"><span data-stu-id="b4c12-133">Check to make sure that the app is not in the **F1** tier.</span></span> <span data-ttu-id="b4c12-134">Custom DNS is not supported in the **F1** tier.</span><span class="sxs-lookup"><span data-stu-id="b4c12-134">Custom DNS is not supported in the **F1** tier.</span></span> 

![Check pricing tier](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="b4c12-136">If the App Service plan is not in the **F1** tier, close the **Scale up** page and skip to [Map a CNAME record](#cname).</span><span class="sxs-lookup"><span data-stu-id="b4c12-136">If the App Service plan is not in the **F1** tier, close the **Scale up** page and skip to [Map a CNAME record](#cname).</span></span>

<a name="scaleup"></a>

### <a name="scale-up-the-app-service-plan"></a><span data-ttu-id="b4c12-137">Scale up the App Service plan</span><span class="sxs-lookup"><span data-stu-id="b4c12-137">Scale up the App Service plan</span></span>

<span data-ttu-id="b4c12-138">Select any of the non-free tiers (**D1**, **B1**, **B2**, **B3**, or any tier in the **Production** category).</span><span class="sxs-lookup"><span data-stu-id="b4c12-138">Select any of the non-free tiers (**D1**, **B1**, **B2**, **B3**, or any tier in the **Production** category).</span></span> <span data-ttu-id="b4c12-139">For additional options, click **See additional options**.</span><span class="sxs-lookup"><span data-stu-id="b4c12-139">For additional options, click **See additional options**.</span></span>

<span data-ttu-id="b4c12-140">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="b4c12-140">Click **Apply**.</span></span>

![Check pricing tier](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="b4c12-142">When you see the following notification, the scale operation is complete.</span><span class="sxs-lookup"><span data-stu-id="b4c12-142">When you see the following notification, the scale operation is complete.</span></span>

![Scale operation confirmation](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-your-domain"></a><span data-ttu-id="b4c12-144">Map your domain</span><span class="sxs-lookup"><span data-stu-id="b4c12-144">Map your domain</span></span>

<span data-ttu-id="b4c12-145">You can use either a **CNAME record** or an **A record** to map a custom DNS name to App Service.</span><span class="sxs-lookup"><span data-stu-id="b4c12-145">You can use either a **CNAME record** or an **A record** to map a custom DNS name to App Service.</span></span> <span data-ttu-id="b4c12-146">Follow the respective steps:</span><span class="sxs-lookup"><span data-stu-id="b4c12-146">Follow the respective steps:</span></span>

- [<span data-ttu-id="b4c12-147">Map a CNAME record</span><span class="sxs-lookup"><span data-stu-id="b4c12-147">Map a CNAME record</span></span>](#map-a-cname-record)
- [<span data-ttu-id="b4c12-148">Map an A record</span><span class="sxs-lookup"><span data-stu-id="b4c12-148">Map an A record</span></span>](#map-an-a-record)
- [<span data-ttu-id="b4c12-149">Map a wildcard domain (with a CNAME record)</span><span class="sxs-lookup"><span data-stu-id="b4c12-149">Map a wildcard domain (with a CNAME record)</span></span>](#map-a-wildcard-domain)

> [!NOTE]
> <span data-ttu-id="b4c12-150">You should use CNAME records for all custom DNS names except root domains (for example, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="b4c12-150">You should use CNAME records for all custom DNS names except root domains (for example, `contoso.com`).</span></span> <span data-ttu-id="b4c12-151">For root domains, use A records.</span><span class="sxs-lookup"><span data-stu-id="b4c12-151">For root domains, use A records.</span></span>

### <a name="map-a-cname-record"></a><span data-ttu-id="b4c12-152">Map a CNAME record</span><span class="sxs-lookup"><span data-stu-id="b4c12-152">Map a CNAME record</span></span>

<span data-ttu-id="b4c12-153">In the tutorial example, you add a CNAME record for the `www` subdomain (for example, `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="b4c12-153">In the tutorial example, you add a CNAME record for the `www` subdomain (for example, `www.contoso.com`).</span></span>

#### <a name="access-dns-records-with-domain-provider"></a><span data-ttu-id="b4c12-154">Access DNS records with domain provider</span><span class="sxs-lookup"><span data-stu-id="b4c12-154">Access DNS records with domain provider</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records-no-h.md)]

#### <a name="create-the-cname-record"></a><span data-ttu-id="b4c12-155">Create the CNAME record</span><span class="sxs-lookup"><span data-stu-id="b4c12-155">Create the CNAME record</span></span>

<span data-ttu-id="b4c12-156">Add a CNAME record to map a subdomain to the app's default hostname (`<app_name>.azurewebsites.net`, where `<app_name>` is the name of your app).</span><span class="sxs-lookup"><span data-stu-id="b4c12-156">Add a CNAME record to map a subdomain to the app's default hostname (`<app_name>.azurewebsites.net`, where `<app_name>` is the name of your app).</span></span>

<span data-ttu-id="b4c12-157">For the `www.contoso.com` domain example, add a CNAME record that maps the name `www` to `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="b4c12-157">For the `www.contoso.com` domain example, add a CNAME record that maps the name `www` to `<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="b4c12-158">After you add the CNAME, the DNS records page looks like the following example:</span><span class="sxs-lookup"><span data-stu-id="b4c12-158">After you add the CNAME, the DNS records page looks like the following example:</span></span>

![Portal navigation to Azure app](./media/app-service-web-tutorial-custom-domain/cname-record.png)

#### <a name="enable-the-cname-record-mapping-in-azure"></a><span data-ttu-id="b4c12-160">Enable the CNAME record mapping in Azure</span><span class="sxs-lookup"><span data-stu-id="b4c12-160">Enable the CNAME record mapping in Azure</span></span>

<span data-ttu-id="b4c12-161">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span><span class="sxs-lookup"><span data-stu-id="b4c12-161">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Custom domain menu](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="b4c12-163">In the **Custom domains** page of the app, add the fully qualified custom DNS name (`www.contoso.com`) to the list.</span><span class="sxs-lookup"><span data-stu-id="b4c12-163">In the **Custom domains** page of the app, add the fully qualified custom DNS name (`www.contoso.com`) to the list.</span></span>

<span data-ttu-id="b4c12-164">Select the **+** icon next to **Add hostname**.</span><span class="sxs-lookup"><span data-stu-id="b4c12-164">Select the **+** icon next to **Add hostname**.</span></span>

![Add host name](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="b4c12-166">Type the fully qualified domain name that you added a CNAME record for, such as `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="b4c12-166">Type the fully qualified domain name that you added a CNAME record for, such as `www.contoso.com`.</span></span> 

<span data-ttu-id="b4c12-167">Select **Validate**.</span><span class="sxs-lookup"><span data-stu-id="b4c12-167">Select **Validate**.</span></span>

<span data-ttu-id="b4c12-168">The **Add hostname** page is shown.</span><span class="sxs-lookup"><span data-stu-id="b4c12-168">The **Add hostname** page is shown.</span></span> 

<span data-ttu-id="b4c12-169">Make sure that **Hostname record type** is set to **CNAME (www.example.com or any subdomain)**.</span><span class="sxs-lookup"><span data-stu-id="b4c12-169">Make sure that **Hostname record type** is set to **CNAME (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="b4c12-170">Select **Add hostname**.</span><span class="sxs-lookup"><span data-stu-id="b4c12-170">Select **Add hostname**.</span></span>

![Add DNS name to the app](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="b4c12-172">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span><span class="sxs-lookup"><span data-stu-id="b4c12-172">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="b4c12-173">Try refreshing the browser to update the data.</span><span class="sxs-lookup"><span data-stu-id="b4c12-173">Try refreshing the browser to update the data.</span></span>

![CNAME record added](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

> [!NOTE]
> <span data-ttu-id="b4c12-175">To add an SSL binding, see [Bind an existing custom SSL certificate to Azure Web Apps](app-service-web-tutorial-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="b4c12-175">To add an SSL binding, see [Bind an existing custom SSL certificate to Azure Web Apps](app-service-web-tutorial-custom-ssl.md).</span></span>

<span data-ttu-id="b4c12-176">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="b4c12-176">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span></span>

![Verification error](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

### <a name="map-an-a-record"></a><span data-ttu-id="b4c12-178">Map an A record</span><span class="sxs-lookup"><span data-stu-id="b4c12-178">Map an A record</span></span>

<span data-ttu-id="b4c12-179">In the tutorial example, you add an A record for the root domain (for example, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="b4c12-179">In the tutorial example, you add an A record for the root domain (for example, `contoso.com`).</span></span> 

<a name="info"></a>

#### <a name="copy-the-apps-ip-address"></a><span data-ttu-id="b4c12-180">Copy the app's IP address</span><span class="sxs-lookup"><span data-stu-id="b4c12-180">Copy the app's IP address</span></span>

<span data-ttu-id="b4c12-181">To map an A record, you need the app's external IP address.</span><span class="sxs-lookup"><span data-stu-id="b4c12-181">To map an A record, you need the app's external IP address.</span></span> <span data-ttu-id="b4c12-182">You can find this IP address in the app's **Custom domains** page in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b4c12-182">You can find this IP address in the app's **Custom domains** page in the Azure portal.</span></span>

<span data-ttu-id="b4c12-183">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span><span class="sxs-lookup"><span data-stu-id="b4c12-183">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Custom domain menu](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="b4c12-185">In the **Custom domains** page, copy the app's IP address.</span><span class="sxs-lookup"><span data-stu-id="b4c12-185">In the **Custom domains** page, copy the app's IP address.</span></span>

![Portal navigation to Azure app](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

#### <a name="access-dns-records-with-domain-provider"></a><span data-ttu-id="b4c12-187">Access DNS records with domain provider</span><span class="sxs-lookup"><span data-stu-id="b4c12-187">Access DNS records with domain provider</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records-no-h.md)]

#### <a name="create-the-a-record"></a><span data-ttu-id="b4c12-188">Create the A record</span><span class="sxs-lookup"><span data-stu-id="b4c12-188">Create the A record</span></span>

<span data-ttu-id="b4c12-189">To map an A record to an app, App Service requires **two** DNS records:</span><span class="sxs-lookup"><span data-stu-id="b4c12-189">To map an A record to an app, App Service requires **two** DNS records:</span></span>

- <span data-ttu-id="b4c12-190">An **A** record to map to the app's IP address.</span><span class="sxs-lookup"><span data-stu-id="b4c12-190">An **A** record to map to the app's IP address.</span></span>
- <span data-ttu-id="b4c12-191">A **TXT** record to map to the app's default hostname `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="b4c12-191">A **TXT** record to map to the app's default hostname `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="b4c12-192">App Service uses this record only at configuration time, to verify that you own the custom domain.</span><span class="sxs-lookup"><span data-stu-id="b4c12-192">App Service uses this record only at configuration time, to verify that you own the custom domain.</span></span> <span data-ttu-id="b4c12-193">After your custom domain is validated and configured in App Service, you can delete this TXT record.</span><span class="sxs-lookup"><span data-stu-id="b4c12-193">After your custom domain is validated and configured in App Service, you can delete this TXT record.</span></span> 

<span data-ttu-id="b4c12-194">For the `contoso.com` domain example, create the A and TXT records according to the following table (`@` typically represents the root domain).</span><span class="sxs-lookup"><span data-stu-id="b4c12-194">For the `contoso.com` domain example, create the A and TXT records according to the following table (`@` typically represents the root domain).</span></span> 

| <span data-ttu-id="b4c12-195">Record type</span><span class="sxs-lookup"><span data-stu-id="b4c12-195">Record type</span></span> | <span data-ttu-id="b4c12-196">Host</span><span class="sxs-lookup"><span data-stu-id="b4c12-196">Host</span></span> | <span data-ttu-id="b4c12-197">Value</span><span class="sxs-lookup"><span data-stu-id="b4c12-197">Value</span></span> |
| - | - | - |
| <span data-ttu-id="b4c12-198">A</span><span class="sxs-lookup"><span data-stu-id="b4c12-198">A</span></span> | `@` | <span data-ttu-id="b4c12-199">IP address from [Copy the app's IP address](#info)</span><span class="sxs-lookup"><span data-stu-id="b4c12-199">IP address from [Copy the app's IP address](#info)</span></span> |
| <span data-ttu-id="b4c12-200">TXT</span><span class="sxs-lookup"><span data-stu-id="b4c12-200">TXT</span></span> | `@` | `<app_name>.azurewebsites.net` |

<span data-ttu-id="b4c12-201">When the records are added, the DNS records page looks like the following example:</span><span class="sxs-lookup"><span data-stu-id="b4c12-201">When the records are added, the DNS records page looks like the following example:</span></span>

![DNS records page](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

#### <a name="enable-the-a-record-mapping-in-the-app"></a><span data-ttu-id="b4c12-203">Enable the A record mapping in the app</span><span class="sxs-lookup"><span data-stu-id="b4c12-203">Enable the A record mapping in the app</span></span>

<span data-ttu-id="b4c12-204">Back in the app's **Custom domains** page in the Azure portal, add the fully qualified custom DNS name (for example, `contoso.com`) to the list.</span><span class="sxs-lookup"><span data-stu-id="b4c12-204">Back in the app's **Custom domains** page in the Azure portal, add the fully qualified custom DNS name (for example, `contoso.com`) to the list.</span></span>

<span data-ttu-id="b4c12-205">Select the **+** icon next to **Add hostname**.</span><span class="sxs-lookup"><span data-stu-id="b4c12-205">Select the **+** icon next to **Add hostname**.</span></span>

![Add host name](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

<span data-ttu-id="b4c12-207">Type the fully qualified domain name that you configured the A record for, such as `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="b4c12-207">Type the fully qualified domain name that you configured the A record for, such as `contoso.com`.</span></span>

<span data-ttu-id="b4c12-208">Select **Validate**.</span><span class="sxs-lookup"><span data-stu-id="b4c12-208">Select **Validate**.</span></span>

<span data-ttu-id="b4c12-209">The **Add hostname** page is shown.</span><span class="sxs-lookup"><span data-stu-id="b4c12-209">The **Add hostname** page is shown.</span></span> 

<span data-ttu-id="b4c12-210">Make sure that **Hostname record type** is set to **A record (example.com)**.</span><span class="sxs-lookup"><span data-stu-id="b4c12-210">Make sure that **Hostname record type** is set to **A record (example.com)**.</span></span>

<span data-ttu-id="b4c12-211">Select **Add hostname**.</span><span class="sxs-lookup"><span data-stu-id="b4c12-211">Select **Add hostname**.</span></span>

![Add DNS name to the app](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

<span data-ttu-id="b4c12-213">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span><span class="sxs-lookup"><span data-stu-id="b4c12-213">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="b4c12-214">Try refreshing the browser to update the data.</span><span class="sxs-lookup"><span data-stu-id="b4c12-214">Try refreshing the browser to update the data.</span></span>

![A record added](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

> [!NOTE]
> <span data-ttu-id="b4c12-216">To add an SSL binding, see [Bind an existing custom SSL certificate to Azure Web Apps](app-service-web-tutorial-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="b4c12-216">To add an SSL binding, see [Bind an existing custom SSL certificate to Azure Web Apps](app-service-web-tutorial-custom-ssl.md).</span></span>

<span data-ttu-id="b4c12-217">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="b4c12-217">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span></span>

![Verification error](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

### <a name="map-a-wildcard-domain"></a><span data-ttu-id="b4c12-219">Map a wildcard domain</span><span class="sxs-lookup"><span data-stu-id="b4c12-219">Map a wildcard domain</span></span>

<span data-ttu-id="b4c12-220">In the tutorial example, you map a [wildcard DNS name](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (for example, `*.contoso.com`) to the App Service app by adding a CNAME record.</span><span class="sxs-lookup"><span data-stu-id="b4c12-220">In the tutorial example, you map a [wildcard DNS name](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (for example, `*.contoso.com`) to the App Service app by adding a CNAME record.</span></span> 

#### <a name="access-dns-records-with-domain-provider"></a><span data-ttu-id="b4c12-221">Access DNS records with domain provider</span><span class="sxs-lookup"><span data-stu-id="b4c12-221">Access DNS records with domain provider</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records-no-h.md)]

#### <a name="create-the-cname-record"></a><span data-ttu-id="b4c12-222">Create the CNAME record</span><span class="sxs-lookup"><span data-stu-id="b4c12-222">Create the CNAME record</span></span>

<span data-ttu-id="b4c12-223">Add a CNAME record to map a wildcard name to the app's default hostname (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="b4c12-223">Add a CNAME record to map a wildcard name to the app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="b4c12-224">For the `*.contoso.com` domain example, the CNAME record will map the name `*` to `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="b4c12-224">For the `*.contoso.com` domain example, the CNAME record will map the name `*` to `<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="b4c12-225">When the CNAME is added, the DNS records page looks like the following example:</span><span class="sxs-lookup"><span data-stu-id="b4c12-225">When the CNAME is added, the DNS records page looks like the following example:</span></span>

![Portal navigation to Azure app](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

#### <a name="enable-the-cname-record-mapping-in-the-app"></a><span data-ttu-id="b4c12-227">Enable the CNAME record mapping in the app</span><span class="sxs-lookup"><span data-stu-id="b4c12-227">Enable the CNAME record mapping in the app</span></span>

<span data-ttu-id="b4c12-228">You can now add any subdomain that matches the wildcard name to the app (for example, `sub1.contoso.com` and `sub2.contoso.com` match `*.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="b4c12-228">You can now add any subdomain that matches the wildcard name to the app (for example, `sub1.contoso.com` and `sub2.contoso.com` match `*.contoso.com`).</span></span> 

<span data-ttu-id="b4c12-229">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span><span class="sxs-lookup"><span data-stu-id="b4c12-229">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Custom domain menu](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="b4c12-231">Select the **+** icon next to **Add hostname**.</span><span class="sxs-lookup"><span data-stu-id="b4c12-231">Select the **+** icon next to **Add hostname**.</span></span>

![Add host name](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="b4c12-233">Type a fully qualified domain name that matches the wildcard domain (for example, `sub1.contoso.com`), and then select **Validate**.</span><span class="sxs-lookup"><span data-stu-id="b4c12-233">Type a fully qualified domain name that matches the wildcard domain (for example, `sub1.contoso.com`), and then select **Validate**.</span></span>

<span data-ttu-id="b4c12-234">The **Add hostname** button is activated.</span><span class="sxs-lookup"><span data-stu-id="b4c12-234">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="b4c12-235">Make sure that **Hostname record type** is set to **CNAME record (www.example.com or any subdomain)**.</span><span class="sxs-lookup"><span data-stu-id="b4c12-235">Make sure that **Hostname record type** is set to **CNAME record (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="b4c12-236">Select **Add hostname**.</span><span class="sxs-lookup"><span data-stu-id="b4c12-236">Select **Add hostname**.</span></span>

![Add DNS name to the app](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

<span data-ttu-id="b4c12-238">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span><span class="sxs-lookup"><span data-stu-id="b4c12-238">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="b4c12-239">Try refreshing the browser to update the data.</span><span class="sxs-lookup"><span data-stu-id="b4c12-239">Try refreshing the browser to update the data.</span></span>

<span data-ttu-id="b4c12-240">Select the **+** icon again to add another hostname that matches the wildcard domain.</span><span class="sxs-lookup"><span data-stu-id="b4c12-240">Select the **+** icon again to add another hostname that matches the wildcard domain.</span></span> <span data-ttu-id="b4c12-241">For example, add `sub2.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="b4c12-241">For example, add `sub2.contoso.com`.</span></span>

![CNAME record added](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

> [!NOTE]
> <span data-ttu-id="b4c12-243">To add an SSL binding, see [Bind an existing custom SSL certificate to Azure Web Apps](app-service-web-tutorial-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="b4c12-243">To add an SSL binding, see [Bind an existing custom SSL certificate to Azure Web Apps](app-service-web-tutorial-custom-ssl.md).</span></span>

## <a name="test-in-browser"></a><span data-ttu-id="b4c12-244">Test in browser</span><span class="sxs-lookup"><span data-stu-id="b4c12-244">Test in browser</span></span>

<span data-ttu-id="b4c12-245">Browse to the DNS name(s) that you configured earlier (for example, `contoso.com`,  `www.contoso.com`, `sub1.contoso.com`, and `sub2.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="b4c12-245">Browse to the DNS name(s) that you configured earlier (for example, `contoso.com`,  `www.contoso.com`, `sub1.contoso.com`, and `sub2.contoso.com`).</span></span>

![Portal navigation to Azure app](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="resolve-404-not-found"></a><span data-ttu-id="b4c12-247">Resolve 404 “Not Found”</span><span class="sxs-lookup"><span data-stu-id="b4c12-247">Resolve 404 “Not Found”</span></span>

<span data-ttu-id="b4c12-248">If you receive an HTTP 404 (Not Found) error when browsing to the URL of your custom domain, verify that your domain resolves to your app's IP address using <a href="https://www.whatsmydns.net/" target="_blank">WhatsmyDNS.net</a>.</span><span class="sxs-lookup"><span data-stu-id="b4c12-248">If you receive an HTTP 404 (Not Found) error when browsing to the URL of your custom domain, verify that your domain resolves to your app's IP address using <a href="https://www.whatsmydns.net/" target="_blank">WhatsmyDNS.net</a>.</span></span> <span data-ttu-id="b4c12-249">If not, it may be due to one of the following reasons:</span><span class="sxs-lookup"><span data-stu-id="b4c12-249">If not, it may be due to one of the following reasons:</span></span>

- <span data-ttu-id="b4c12-250">The custom domain configured is missing an A record and/or a CNAME record.</span><span class="sxs-lookup"><span data-stu-id="b4c12-250">The custom domain configured is missing an A record and/or a CNAME record.</span></span>
- <span data-ttu-id="b4c12-251">The browser client has cached the old IP address of your domain.</span><span class="sxs-lookup"><span data-stu-id="b4c12-251">The browser client has cached the old IP address of your domain.</span></span> <span data-ttu-id="b4c12-252">Clear the cache and test DNS resolution again.</span><span class="sxs-lookup"><span data-stu-id="b4c12-252">Clear the cache and test DNS resolution again.</span></span> <span data-ttu-id="b4c12-253">On a Windows machine, you clear the cache with `ipconfig /flushdns`.</span><span class="sxs-lookup"><span data-stu-id="b4c12-253">On a Windows machine, you clear the cache with `ipconfig /flushdns`.</span></span>

<a name="virtualdir"></a>

## <a name="migrate-an-active-domain"></a><span data-ttu-id="b4c12-254">Migrate an active domain</span><span class="sxs-lookup"><span data-stu-id="b4c12-254">Migrate an active domain</span></span>

<span data-ttu-id="b4c12-255">To migrate a live site and its DNS domain name to App Service with no downtime, see [Migrate an active DNS name to Azure App Service](app-service-custom-domain-name-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="b4c12-255">To migrate a live site and its DNS domain name to App Service with no downtime, see [Migrate an active DNS name to Azure App Service](app-service-custom-domain-name-migrate.md).</span></span>

## <a name="redirect-to-a-custom-directory"></a><span data-ttu-id="b4c12-256">Redirect to a custom directory</span><span class="sxs-lookup"><span data-stu-id="b4c12-256">Redirect to a custom directory</span></span>

<span data-ttu-id="b4c12-257">By default, App Service directs web requests to the root directory of your app code.</span><span class="sxs-lookup"><span data-stu-id="b4c12-257">By default, App Service directs web requests to the root directory of your app code.</span></span> <span data-ttu-id="b4c12-258">However, certain web frameworks don't start in the root directory.</span><span class="sxs-lookup"><span data-stu-id="b4c12-258">However, certain web frameworks don't start in the root directory.</span></span> <span data-ttu-id="b4c12-259">For example, [Laravel](https://laravel.com/) starts in the `public` subdirectory.</span><span class="sxs-lookup"><span data-stu-id="b4c12-259">For example, [Laravel](https://laravel.com/) starts in the `public` subdirectory.</span></span> <span data-ttu-id="b4c12-260">To continue the `contoso.com` DNS example, such an app would be accessible at `http://contoso.com/public`, but you would really want to direct `http://contoso.com` to the `public` directory instead.</span><span class="sxs-lookup"><span data-stu-id="b4c12-260">To continue the `contoso.com` DNS example, such an app would be accessible at `http://contoso.com/public`, but you would really want to direct `http://contoso.com` to the `public` directory instead.</span></span> <span data-ttu-id="b4c12-261">This step doesn't involve DNS resolution, but customizing the virtual directory.</span><span class="sxs-lookup"><span data-stu-id="b4c12-261">This step doesn't involve DNS resolution, but customizing the virtual directory.</span></span>

<span data-ttu-id="b4c12-262">To do this, select **Application settings** in the left-hand navigation of your web app page.</span><span class="sxs-lookup"><span data-stu-id="b4c12-262">To do this, select **Application settings** in the left-hand navigation of your web app page.</span></span> 

<span data-ttu-id="b4c12-263">At the bottom of the page, the root virtual directory `/` points to `site\wwwroot` by default, which is the root directory of your app code.</span><span class="sxs-lookup"><span data-stu-id="b4c12-263">At the bottom of the page, the root virtual directory `/` points to `site\wwwroot` by default, which is the root directory of your app code.</span></span> <span data-ttu-id="b4c12-264">Change it to point to the `site\wwwroot\public` instead, for example, and save your changes.</span><span class="sxs-lookup"><span data-stu-id="b4c12-264">Change it to point to the `site\wwwroot\public` instead, for example, and save your changes.</span></span> 

![Customize virtual directory](./media/app-service-web-tutorial-custom-domain/customize-virtual-directory.png)

<span data-ttu-id="b4c12-266">Once the operation completes, your app should return the right page at the root path (for example, http://contoso.com).</span><span class="sxs-lookup"><span data-stu-id="b4c12-266">Once the operation completes, your app should return the right page at the root path (for example, http://contoso.com).</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="b4c12-267">Automate with scripts</span><span class="sxs-lookup"><span data-stu-id="b4c12-267">Automate with scripts</span></span>

<span data-ttu-id="b4c12-268">You can automate management of custom domains with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b4c12-268">You can automate management of custom domains with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="azure-cli"></a><span data-ttu-id="b4c12-269">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b4c12-269">Azure CLI</span></span> 

<span data-ttu-id="b4c12-270">The following command adds a configured custom DNS name to an App Service app.</span><span class="sxs-lookup"><span data-stu-id="b4c12-270">The following command adds a configured custom DNS name to an App Service app.</span></span> 

```bash 
az webapp config hostname add \
    --webapp-name <app_name> \
    --resource-group <resource_group_name> \ 
    --hostname <fully_qualified_domain_name> 
``` 

<span data-ttu-id="b4c12-271">For more information, see [Map a custom domain to a web app](scripts/app-service-cli-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="b4c12-271">For more information, see [Map a custom domain to a web app](scripts/app-service-cli-configure-custom-domain.md).</span></span> 

### <a name="azure-powershell"></a><span data-ttu-id="b4c12-272">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4c12-272">Azure PowerShell</span></span> 

<span data-ttu-id="b4c12-273">The following command adds a configured custom DNS name to an App Service app.</span><span class="sxs-lookup"><span data-stu-id="b4c12-273">The following command adds a configured custom DNS name to an App Service app.</span></span> 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

<span data-ttu-id="b4c12-274">For more information, see [Assign a custom domain to a web app](scripts/app-service-powershell-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="b4c12-274">For more information, see [Assign a custom domain to a web app](scripts/app-service-powershell-configure-custom-domain.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4c12-275">Next steps</span><span class="sxs-lookup"><span data-stu-id="b4c12-275">Next steps</span></span>

<span data-ttu-id="b4c12-276">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="b4c12-276">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b4c12-277">Map a subdomain by using a CNAME record</span><span class="sxs-lookup"><span data-stu-id="b4c12-277">Map a subdomain by using a CNAME record</span></span>
> * <span data-ttu-id="b4c12-278">Map a root domain by using an A record</span><span class="sxs-lookup"><span data-stu-id="b4c12-278">Map a root domain by using an A record</span></span>
> * <span data-ttu-id="b4c12-279">Map a wildcard domain by using a CNAME record</span><span class="sxs-lookup"><span data-stu-id="b4c12-279">Map a wildcard domain by using a CNAME record</span></span>
> * <span data-ttu-id="b4c12-280">Redirect the default URL to a custom directory</span><span class="sxs-lookup"><span data-stu-id="b4c12-280">Redirect the default URL to a custom directory</span></span>
> * <span data-ttu-id="b4c12-281">Automate domain mapping with scripts</span><span class="sxs-lookup"><span data-stu-id="b4c12-281">Automate domain mapping with scripts</span></span>

<span data-ttu-id="b4c12-282">Advance to the next tutorial to learn how to bind a custom SSL certificate to a web app.</span><span class="sxs-lookup"><span data-stu-id="b4c12-282">Advance to the next tutorial to learn how to bind a custom SSL certificate to a web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b4c12-283">Bind an existing custom SSL certificate to Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="b4c12-283">Bind an existing custom SSL certificate to Azure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
