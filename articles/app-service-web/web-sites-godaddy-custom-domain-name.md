---
title: Configure a custom domain name in Azure App Service (GoDaddy)
description: Learn how to use a domain name from GoDaddy with Azure Web Apps
services: app-service
documentationcenter: ''
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 33233e30-5846-488f-83f3-b32e5c114564
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 60713ce43418d34bbecbdeb7718678714530ed02
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662434"
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a><span data-ttu-id="f931a-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span><span class="sxs-lookup"><span data-stu-id="f931a-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

<span data-ttu-id="f931a-104">If you have purchased domain through Azure App Service Web Apps then refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="f931a-104">If you have purchased domain through Azure App Service Web Apps then refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span></span>

<span data-ttu-id="f931a-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="f931a-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="f931a-106">Understanding DNS records</span><span class="sxs-lookup"><span data-stu-id="f931a-106">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="f931a-107">Add a DNS record for your custom domain</span><span class="sxs-lookup"><span data-stu-id="f931a-107">Add a DNS record for your custom domain</span></span>
<span data-ttu-id="f931a-108">To associate your custom domain with a web app in App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by GoDaddy.</span><span class="sxs-lookup"><span data-stu-id="f931a-108">To associate your custom domain with a web app in App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by GoDaddy.</span></span> <span data-ttu-id="f931a-109">Use the following steps to locate the DNS tools for GoDaddy.com</span><span class="sxs-lookup"><span data-stu-id="f931a-109">Use the following steps to locate the DNS tools for GoDaddy.com</span></span>

1. <span data-ttu-id="f931a-110">Log on to your account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span><span class="sxs-lookup"><span data-stu-id="f931a-110">Log on to your account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span></span> <span data-ttu-id="f931a-111">Finally, select the drop-down menu for the domain name that you wish to use with your Azure web app and select **Manage DNS**.</span><span class="sxs-lookup"><span data-stu-id="f931a-111">Finally, select the drop-down menu for the domain name that you wish to use with your Azure web app and select **Manage DNS**.</span></span>
   
    ![custom domain page for GoDaddy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. <span data-ttu-id="f931a-113">From the **Domain details** page, scroll to the **DNS Zone File** tab. This is the section used for adding and modifying DNS records for your domain name.</span><span class="sxs-lookup"><span data-stu-id="f931a-113">From the **Domain details** page, scroll to the **DNS Zone File** tab. This is the section used for adding and modifying DNS records for your domain name.</span></span>
   
    ![DNS Zone File tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    <span data-ttu-id="f931a-115">Select **Add Record** to add an existing record.</span><span class="sxs-lookup"><span data-stu-id="f931a-115">Select **Add Record** to add an existing record.</span></span>
   
    <span data-ttu-id="f931a-116">To **edit** an existing record, select the pen & paper icon beside the record.</span><span class="sxs-lookup"><span data-stu-id="f931a-116">To **edit** an existing record, select the pen & paper icon beside the record.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f931a-117">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span><span class="sxs-lookup"><span data-stu-id="f931a-117">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span></span> <span data-ttu-id="f931a-118">If the name you wish to use already exists, modify the existing record instead of creating a new one.</span><span class="sxs-lookup"><span data-stu-id="f931a-118">If the name you wish to use already exists, modify the existing record instead of creating a new one.</span></span>
   > 
   > 
3. <span data-ttu-id="f931a-119">When adding a record, you must first select the record type.</span><span class="sxs-lookup"><span data-stu-id="f931a-119">When adding a record, you must first select the record type.</span></span>
   
    ![select record type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    <span data-ttu-id="f931a-121">Next, you must provide the **Host** (the custom domain or sub-domain) and what it **Points to**.</span><span class="sxs-lookup"><span data-stu-id="f931a-121">Next, you must provide the **Host** (the custom domain or sub-domain) and what it **Points to**.</span></span>
   
    ![add zone record](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * <span data-ttu-id="f931a-123">When adding an **A (host) record** - you must set the **Host** field to either **@** (this represents root domain name, such as **contoso.com**,) \* (a wildcard for matching multiple sub-domains,) or the sub-domain you wish to use (for example, **www**.) You must set the **Points to** field to the IP address of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="f931a-123">When adding an **A (host) record** - you must set the **Host** field to either **@** (this represents root domain name, such as **contoso.com**,) \* (a wildcard for matching multiple sub-domains,) or the sub-domain you wish to use (for example, **www**.) You must set the **Points to** field to the IP address of your Azure web app.</span></span>
   * <span data-ttu-id="f931a-124">When adding a **CNAME (alias) record** - you must set the **Host** field to the sub-domain you wish to use.</span><span class="sxs-lookup"><span data-stu-id="f931a-124">When adding a **CNAME (alias) record** - you must set the **Host** field to the sub-domain you wish to use.</span></span> <span data-ttu-id="f931a-125">For example, **www**.</span><span class="sxs-lookup"><span data-stu-id="f931a-125">For example, **www**.</span></span> <span data-ttu-id="f931a-126">You must set the **Points to** field to the **.azurewebsites.net** domain name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="f931a-126">You must set the **Points to** field to the **.azurewebsites.net** domain name of your Azure web app.</span></span> <span data-ttu-id="f931a-127">For example, **contoso.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="f931a-127">For example, **contoso.azurewebsites.net**.</span></span>
4. <span data-ttu-id="f931a-128">Click **Add Another**.</span><span class="sxs-lookup"><span data-stu-id="f931a-128">Click **Add Another**.</span></span>
5. <span data-ttu-id="f931a-129">Select **TXT** as the record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="f931a-129">Select **TXT** as the record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f931a-130">This TXT record is used by Azure to validate that you own the domain described by the A record or the first TXT record.</span><span class="sxs-lookup"><span data-stu-id="f931a-130">This TXT record is used by Azure to validate that you own the domain described by the A record or the first TXT record.</span></span> <span data-ttu-id="f931a-131">Once the domain has been mapped to the web app in the Azure Portal, this TXT record entry can be removed.</span><span class="sxs-lookup"><span data-stu-id="f931a-131">Once the domain has been mapped to the web app in the Azure Portal, this TXT record entry can be removed.</span></span>
   > 
   > 
6. <span data-ttu-id="f931a-132">When you have finished adding or modifying records, click **Finish** to save changes.</span><span class="sxs-lookup"><span data-stu-id="f931a-132">When you have finished adding or modifying records, click **Finish** to save changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-the-domain-name-on-your-web-app"></a><span data-ttu-id="f931a-133">Enable the domain name on your web app</span><span class="sxs-lookup"><span data-stu-id="f931a-133">Enable the domain name on your web app</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> <span data-ttu-id="f931a-134">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="f931a-134">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f931a-135">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="f931a-135">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="f931a-136">What's changed</span><span class="sxs-lookup"><span data-stu-id="f931a-136">What's changed</span></span>
* <span data-ttu-id="f931a-137">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="f931a-137">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>





