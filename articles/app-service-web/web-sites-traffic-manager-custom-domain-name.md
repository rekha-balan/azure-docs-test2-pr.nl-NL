---
title: Configure a custom domain name for a web app in Azure App Service that uses Traffic Manager for load balancing.
description: Use a custom domain name for an a web app in Azure App Service that includes Traffic Manager for load balancing.
services: app-service\web
documentationcenter: ''
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: 0f96c0e7-0901-489b-a95a-e3b66ca0a1c2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: d422731fd45b21844549774b520283985f25e1d7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549626"
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a><span data-ttu-id="bdcdc-103">Configuring a custom domain name for a web app in Azure App Service using Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="bdcdc-103">Configuring a custom domain name for a web app in Azure App Service using Traffic Manager</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

<span data-ttu-id="bdcdc-104">This article provides generic instructions for using a custom domain name with Azure App Service that use Traffic Manager for load balancing.</span><span class="sxs-lookup"><span data-stu-id="bdcdc-104">This article provides generic instructions for using a custom domain name with Azure App Service that use Traffic Manager for load balancing.</span></span>

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="bdcdc-105">Understanding DNS records</span><span class="sxs-lookup"><span data-stu-id="bdcdc-105">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a><span data-ttu-id="bdcdc-106">Configure your web apps for standard mode</span><span class="sxs-lookup"><span data-stu-id="bdcdc-106">Configure your web apps for standard mode</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="bdcdc-107">Add a DNS record for your custom domain</span><span class="sxs-lookup"><span data-stu-id="bdcdc-107">Add a DNS record for your custom domain</span></span>
> [!NOTE]
> <span data-ttu-id="bdcdc-108">If you have purchased domain through Azure App Service Web Apps then skip following steps and refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md) article.</span><span class="sxs-lookup"><span data-stu-id="bdcdc-108">If you have purchased domain through Azure App Service Web Apps then skip following steps and refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md) article.</span></span>
> 
> 

<span data-ttu-id="bdcdc-109">To associate your custom domain with a web app in Azure App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by the domain registrar that you purchased your domain name from.</span><span class="sxs-lookup"><span data-stu-id="bdcdc-109">To associate your custom domain with a web app in Azure App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by the domain registrar that you purchased your domain name from.</span></span> <span data-ttu-id="bdcdc-110">Use the following steps to locate and use the DNS tools.</span><span class="sxs-lookup"><span data-stu-id="bdcdc-110">Use the following steps to locate and use the DNS tools.</span></span>

1. <span data-ttu-id="bdcdc-111">Sign in to your account at your domain registrar, and look for a page for managing DNS records.</span><span class="sxs-lookup"><span data-stu-id="bdcdc-111">Sign in to your account at your domain registrar, and look for a page for managing DNS records.</span></span> <span data-ttu-id="bdcdc-112">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span><span class="sxs-lookup"><span data-stu-id="bdcdc-112">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="bdcdc-113">Often a link to this page can be found be viewing your account information, and then looking for a link such as **My domains**.</span><span class="sxs-lookup"><span data-stu-id="bdcdc-113">Often a link to this page can be found be viewing your account information, and then looking for a link such as **My domains**.</span></span>
2. <span data-ttu-id="bdcdc-114">Once you have found the management page for your domain name, look for a link that allows you to edit the DNS records.</span><span class="sxs-lookup"><span data-stu-id="bdcdc-114">Once you have found the management page for your domain name, look for a link that allows you to edit the DNS records.</span></span> <span data-ttu-id="bdcdc-115">This might be listed as a **Zone file**, **DNS Records**, or as an **Advanced** configuration link.</span><span class="sxs-lookup"><span data-stu-id="bdcdc-115">This might be listed as a **Zone file**, **DNS Records**, or as an **Advanced** configuration link.</span></span>
   
   * <span data-ttu-id="bdcdc-116">The page will most likely have a few records already created, such as an entry associating '**@**' or '\*' with a 'domain parking' page.</span><span class="sxs-lookup"><span data-stu-id="bdcdc-116">The page will most likely have a few records already created, such as an entry associating '**@**' or '\*' with a 'domain parking' page.</span></span> <span data-ttu-id="bdcdc-117">It may also contain records for common sub-domains such as **www**.</span><span class="sxs-lookup"><span data-stu-id="bdcdc-117">It may also contain records for common sub-domains such as **www**.</span></span>
   * <span data-ttu-id="bdcdc-118">The page will mention **CNAME records**, or provide a drop-down to select a record type.</span><span class="sxs-lookup"><span data-stu-id="bdcdc-118">The page will mention **CNAME records**, or provide a drop-down to select a record type.</span></span> <span data-ttu-id="bdcdc-119">It may also mention other records such as **A records** and **MX records**.</span><span class="sxs-lookup"><span data-stu-id="bdcdc-119">It may also mention other records such as **A records** and **MX records**.</span></span> <span data-ttu-id="bdcdc-120">In some cases, CNAME records will be called by other names such as an **Alias Record**.</span><span class="sxs-lookup"><span data-stu-id="bdcdc-120">In some cases, CNAME records will be called by other names such as an **Alias Record**.</span></span>
   * <span data-ttu-id="bdcdc-121">The page will also have fields that allow you to **map** from a **Host name** or **Domain name** to another domain name.</span><span class="sxs-lookup"><span data-stu-id="bdcdc-121">The page will also have fields that allow you to **map** from a **Host name** or **Domain name** to another domain name.</span></span>
3. <span data-ttu-id="bdcdc-122">While the specifics of each registrar vary, in general you map *from* your custom domain name (such as **contoso.com**,) *to* the Traffic Manager domain name (**contoso.trafficmanager.net**) that is used for your web app.</span><span class="sxs-lookup"><span data-stu-id="bdcdc-122">While the specifics of each registrar vary, in general you map *from* your custom domain name (such as **contoso.com**,) *to* the Traffic Manager domain name (**contoso.trafficmanager.net**) that is used for your web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bdcdc-123">Alternatively, if a record is already in use and you need to preemptively bind your apps to it, you can create an additional CNAME record.</span><span class="sxs-lookup"><span data-stu-id="bdcdc-123">Alternatively, if a record is already in use and you need to preemptively bind your apps to it, you can create an additional CNAME record.</span></span> <span data-ttu-id="bdcdc-124">For example, to preemptively bind **www.contoso.com** to your web app, create a CNAME record from **awverify.www** to **contoso.trafficmanager.net**.</span><span class="sxs-lookup"><span data-stu-id="bdcdc-124">For example, to preemptively bind **www.contoso.com** to your web app, create a CNAME record from **awverify.www** to **contoso.trafficmanager.net**.</span></span> <span data-ttu-id="bdcdc-125">You can then add "www.contoso.com" to your Web App without changing the "www" CNAME record.</span><span class="sxs-lookup"><span data-stu-id="bdcdc-125">You can then add "www.contoso.com" to your Web App without changing the "www" CNAME record.</span></span> <span data-ttu-id="bdcdc-126">For more information, see [Create DNS records for a web app in a custom domain][CREATEDNS].</span><span class="sxs-lookup"><span data-stu-id="bdcdc-126">For more information, see [Create DNS records for a web app in a custom domain][CREATEDNS].</span></span>
   > 
   > 
4. <span data-ttu-id="bdcdc-127">Once you have finished adding or modifying DNS records at your registrar, save the changes.</span><span class="sxs-lookup"><span data-stu-id="bdcdc-127">Once you have finished adding or modifying DNS records at your registrar, save the changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a><span data-ttu-id="bdcdc-128">Enable Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="bdcdc-128">Enable Traffic Manager</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="bdcdc-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="bdcdc-129">Next steps</span></span>
<span data-ttu-id="bdcdc-130">For more information, see the [Node.js Developer Center](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="bdcdc-130">For more information, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
