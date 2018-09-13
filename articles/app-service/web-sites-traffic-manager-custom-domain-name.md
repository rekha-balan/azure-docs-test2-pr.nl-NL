---
title: Configure a custom domain name for a web app in Azure App Service that uses Traffic Manager for load balancing.
description: Use a custom domain name for an a web app in Azure App Service that includes Traffic Manager for load balancing.
services: app-service\web
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
ms.assetid: 0f96c0e7-0901-489b-a95a-e3b66ca0a1c2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: a83b5dada8afff455375ae1606ecaac4c9ebe8e7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858112"
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a><span data-ttu-id="a4325-103">Configuring a custom domain name for a web app in Azure App Service using Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="a4325-103">Configuring a custom domain name for a web app in Azure App Service using Traffic Manager</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

<span data-ttu-id="a4325-104">This article provides generic instructions for using a custom domain name with an [App Service](app-service-web-overview.md) app that is integrated with [Traffic Manager](../traffic-manager/traffic-manager-overview.md) for load balancing.</span><span class="sxs-lookup"><span data-stu-id="a4325-104">This article provides generic instructions for using a custom domain name with an [App Service](app-service-web-overview.md) app that is integrated with [Traffic Manager](../traffic-manager/traffic-manager-overview.md) for load balancing.</span></span>

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="a4325-105">Understanding DNS records</span><span class="sxs-lookup"><span data-stu-id="a4325-105">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a><span data-ttu-id="a4325-106">Configure your web apps for standard mode</span><span class="sxs-lookup"><span data-stu-id="a4325-106">Configure your web apps for standard mode</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="a4325-107">Add a DNS record for your custom domain</span><span class="sxs-lookup"><span data-stu-id="a4325-107">Add a DNS record for your custom domain</span></span>
> [!NOTE]
> <span data-ttu-id="a4325-108">If you have purchased domain through Azure App Service Web Apps then skip following steps and refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md) article.</span><span class="sxs-lookup"><span data-stu-id="a4325-108">If you have purchased domain through Azure App Service Web Apps then skip following steps and refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md) article.</span></span>
> 
> 

<span data-ttu-id="a4325-109">To associate your custom domain with a web app in Azure App Service, you must add a new entry in the DNS table for your custom domain.</span><span class="sxs-lookup"><span data-stu-id="a4325-109">To associate your custom domain with a web app in Azure App Service, you must add a new entry in the DNS table for your custom domain.</span></span> <span data-ttu-id="a4325-110">You do this by using the management tools from your domain provider.</span><span class="sxs-lookup"><span data-stu-id="a4325-110">You do this by using the management tools from your domain provider.</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records-no-h.md)]

<span data-ttu-id="a4325-111">While the specifics of each domain provider vary, you map *from* your custom domain name (such as **contoso.com**) *to* the Traffic Manager domain name (**contoso.trafficmanager.net**) that is integrated with your web app.</span><span class="sxs-lookup"><span data-stu-id="a4325-111">While the specifics of each domain provider vary, you map *from* your custom domain name (such as **contoso.com**) *to* the Traffic Manager domain name (**contoso.trafficmanager.net**) that is integrated with your web app.</span></span>
   
> [!NOTE]
> <span data-ttu-id="a4325-112">If a record is already in use and you need to preemptively bind your apps to it, you can create an additional CNAME record.</span><span class="sxs-lookup"><span data-stu-id="a4325-112">If a record is already in use and you need to preemptively bind your apps to it, you can create an additional CNAME record.</span></span> <span data-ttu-id="a4325-113">For example, to preemptively bind **www.contoso.com** to your web app, create a CNAME record from **awverify.www** to **contoso.trafficmanager.net**.</span><span class="sxs-lookup"><span data-stu-id="a4325-113">For example, to preemptively bind **www.contoso.com** to your web app, create a CNAME record from **awverify.www** to **contoso.trafficmanager.net**.</span></span> <span data-ttu-id="a4325-114">You can then add "www.contoso.com" to your Web App without changing the "www" CNAME record.</span><span class="sxs-lookup"><span data-stu-id="a4325-114">You can then add "www.contoso.com" to your Web App without changing the "www" CNAME record.</span></span> <span data-ttu-id="a4325-115">For more information, see [Create DNS records for a web app in a custom domain][CREATEDNS].</span><span class="sxs-lookup"><span data-stu-id="a4325-115">For more information, see [Create DNS records for a web app in a custom domain][CREATEDNS].</span></span>
> 
> 

<span data-ttu-id="a4325-116">Once you have finished adding or modifying DNS records at your domain provider, save the changes.</span><span class="sxs-lookup"><span data-stu-id="a4325-116">Once you have finished adding or modifying DNS records at your domain provider, save the changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a><span data-ttu-id="a4325-117">Enable Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="a4325-117">Enable Traffic Manager</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="a4325-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="a4325-118">Next steps</span></span>
<span data-ttu-id="a4325-119">For more information, see the [Node.js Developer Center](http://azure.microsoft.com/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="a4325-119">For more information, see the [Node.js Developer Center](http://azure.microsoft.com/develop/nodejs/).</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
