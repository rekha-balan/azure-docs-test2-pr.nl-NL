---
title: Azure App Service IP Restrictions | Microsoft Docs
description: How to use IP restrictions with Azure App Service
author: ccompy
manager: stefsch
editor: ''
services: app-service\web
documentationcenter: ''
ms.assetid: 3be1f4bd-8a81-4565-8a56-528c037b24bd
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 7/30/2018
ms.author: ccompy
ms.openlocfilehash: fb26d91ae772c4da1055da80366d6e8c6b80a6ac
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869520"
---
# <a name="azure-app-service-static-ip-restrictions"></a><span data-ttu-id="529e9-103">Azure App Service Static IP Restrictions</span><span class="sxs-lookup"><span data-stu-id="529e9-103">Azure App Service Static IP Restrictions</span></span> #

<span data-ttu-id="529e9-104">IP Restrictions allow you to define a priority ordered allow/deny list of IP addresses that are allowed to access your app.</span><span class="sxs-lookup"><span data-stu-id="529e9-104">IP Restrictions allow you to define a priority ordered allow/deny list of IP addresses that are allowed to access your app.</span></span> <span data-ttu-id="529e9-105">The allow list can include IPv4 and IPv6 addresses.</span><span class="sxs-lookup"><span data-stu-id="529e9-105">The allow list can include IPv4 and IPv6 addresses.</span></span> <span data-ttu-id="529e9-106">When there are one or more entries, there is then an implicit deny all that exists at the end of the list.</span><span class="sxs-lookup"><span data-stu-id="529e9-106">When there are one or more entries, there is then an implicit deny all that exists at the end of the list.</span></span> 

<span data-ttu-id="529e9-107">The IP Restrictions capability works with all App Service hosted work loads, which include; web apps, api apps, linux apps, linux container apps, and Functions.</span><span class="sxs-lookup"><span data-stu-id="529e9-107">The IP Restrictions capability works with all App Service hosted work loads, which include; web apps, api apps, linux apps, linux container apps, and Functions.</span></span> 

<span data-ttu-id="529e9-108">When a request is made to your app, the FROM IP address is evaluated against the IP Restrictions list.</span><span class="sxs-lookup"><span data-stu-id="529e9-108">When a request is made to your app, the FROM IP address is evaluated against the IP Restrictions list.</span></span> <span data-ttu-id="529e9-109">If the address is not allowed access based on the rules in the list, the service replies with an [HTTP 403](https://en.wikipedia.org/wiki/HTTP_403) status code.</span><span class="sxs-lookup"><span data-stu-id="529e9-109">If the address is not allowed access based on the rules in the list, the service replies with an [HTTP 403](https://en.wikipedia.org/wiki/HTTP_403) status code.</span></span>

<span data-ttu-id="529e9-110">The IP Restrictions capability is implemented in the App Service front-end roles, which are upstream of the worker hosts where your code runs.</span><span class="sxs-lookup"><span data-stu-id="529e9-110">The IP Restrictions capability is implemented in the App Service front-end roles, which are upstream of the worker hosts where your code runs.</span></span> <span data-ttu-id="529e9-111">IP Restrictions are therefor effectively network ACLs.</span><span class="sxs-lookup"><span data-stu-id="529e9-111">IP Restrictions are therefor effectively network ACLs.</span></span>  

![IP restrictions flow](media/app-service-ip-restrictions/ip-restrictions-flow.png)

<span data-ttu-id="529e9-113">For a time, the IP Restrictions capability in the portal was a layer on top of the ipSecurity capability in IIS.</span><span class="sxs-lookup"><span data-stu-id="529e9-113">For a time, the IP Restrictions capability in the portal was a layer on top of the ipSecurity capability in IIS.</span></span> <span data-ttu-id="529e9-114">The current IP Restrictions capability is different.</span><span class="sxs-lookup"><span data-stu-id="529e9-114">The current IP Restrictions capability is different.</span></span> <span data-ttu-id="529e9-115">You can still configure ipSecurity within your application web.config but the front-end based IP Restrictions rules will be applied before any traffic reaches IIS.</span><span class="sxs-lookup"><span data-stu-id="529e9-115">You can still configure ipSecurity within your application web.config but the front-end based IP Restrictions rules will be applied before any traffic reaches IIS.</span></span>

## <a name="adding-and-editing-ip-restriction-rules-in-the-portal"></a><span data-ttu-id="529e9-116">Adding and editing IP Restriction rules in the portal</span><span class="sxs-lookup"><span data-stu-id="529e9-116">Adding and editing IP Restriction rules in the portal</span></span> ##

<span data-ttu-id="529e9-117">To add an IP restriction rule to your app, use the menu to open **Network**>**IP Restrictions** and click on **Configure IP Restrictions**</span><span class="sxs-lookup"><span data-stu-id="529e9-117">To add an IP restriction rule to your app, use the menu to open **Network**>**IP Restrictions** and click on **Configure IP Restrictions**</span></span>

![App Service networking options](media/app-service-ip-restrictions/ip-restrictions.png)  

<span data-ttu-id="529e9-119">From the IP Restrictions UI, you can review the list of IP restriction rules defined for your app.</span><span class="sxs-lookup"><span data-stu-id="529e9-119">From the IP Restrictions UI, you can review the list of IP restriction rules defined for your app.</span></span>

![list IP restrictions](media/app-service-ip-restrictions/ip-restrictions-browse.png)

<span data-ttu-id="529e9-121">If your rules were configured as in this image, then your app would only accept traffic from 131.107.159.0/24 and would be denied from any other IP address.</span><span class="sxs-lookup"><span data-stu-id="529e9-121">If your rules were configured as in this image, then your app would only accept traffic from 131.107.159.0/24 and would be denied from any other IP address.</span></span>

<span data-ttu-id="529e9-122">You can click on **[+] Add** to add a new IP restriction rule.</span><span class="sxs-lookup"><span data-stu-id="529e9-122">You can click on **[+] Add** to add a new IP restriction rule.</span></span> <span data-ttu-id="529e9-123">Once you add a rule, it will become effective immediately.</span><span class="sxs-lookup"><span data-stu-id="529e9-123">Once you add a rule, it will become effective immediately.</span></span> <span data-ttu-id="529e9-124">Rules are enforced in priority order starting from the lowest number and going up.</span><span class="sxs-lookup"><span data-stu-id="529e9-124">Rules are enforced in priority order starting from the lowest number and going up.</span></span> <span data-ttu-id="529e9-125">There is an implicit deny all that is in effect once you add even a single rule.</span><span class="sxs-lookup"><span data-stu-id="529e9-125">There is an implicit deny all that is in effect once you add even a single rule.</span></span> 

![add an IP restriction rule](media/app-service-ip-restrictions/ip-restrictions-add.png)

<span data-ttu-id="529e9-127">IP Address notation must be specified in CIDR notation for both IPv4 and IPv6 addresses.</span><span class="sxs-lookup"><span data-stu-id="529e9-127">IP Address notation must be specified in CIDR notation for both IPv4 and IPv6 addresses.</span></span> <span data-ttu-id="529e9-128">To specify an exact address, you can use something like 1.2.3.4/32 where the first four octets represent your IP address and /32 is the mask.</span><span class="sxs-lookup"><span data-stu-id="529e9-128">To specify an exact address, you can use something like 1.2.3.4/32 where the first four octets represent your IP address and /32 is the mask.</span></span> <span data-ttu-id="529e9-129">The IPv4 CIDR notation for all addresses is 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="529e9-129">The IPv4 CIDR notation for all addresses is 0.0.0.0/0.</span></span> <span data-ttu-id="529e9-130">To learn more about CIDR notation, you can read [Classless Inter-Domain Routing](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing).</span><span class="sxs-lookup"><span data-stu-id="529e9-130">To learn more about CIDR notation, you can read [Classless Inter-Domain Routing](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing).</span></span>  

<span data-ttu-id="529e9-131">You can click on any row to edit an existing IP restriction rule.</span><span class="sxs-lookup"><span data-stu-id="529e9-131">You can click on any row to edit an existing IP restriction rule.</span></span> <span data-ttu-id="529e9-132">Edits are effective immediately including changes in priority ordering.</span><span class="sxs-lookup"><span data-stu-id="529e9-132">Edits are effective immediately including changes in priority ordering.</span></span>

![edit an IP restriction rule](media/app-service-ip-restrictions/ip-restrictions-edit.png)

<span data-ttu-id="529e9-134">To delete a rule, click the **...** on your rule and then click **remove**.</span><span class="sxs-lookup"><span data-stu-id="529e9-134">To delete a rule, click the **...** on your rule and then click **remove**.</span></span> 

![delete IP restriction rule](media/app-service-ip-restrictions/ip-restrictions-delete.png)

## <a name="programmatic-manipulation-of-ip-restriction-rules"></a><span data-ttu-id="529e9-136">Programmatic manipulation of IP restriction rules</span><span class="sxs-lookup"><span data-stu-id="529e9-136">Programmatic manipulation of IP restriction rules</span></span> ##

<span data-ttu-id="529e9-137">There currently is no CLI or PowerShell for the new IP Restrictions capability but the values can be set manually with a PUT operation on the app configuration in Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="529e9-137">There currently is no CLI or PowerShell for the new IP Restrictions capability but the values can be set manually with a PUT operation on the app configuration in Resource Manager.</span></span> <span data-ttu-id="529e9-138">As an example, you can use resources.azure.com and edit the ipSecurityRestrictions block to add the required JSON.</span><span class="sxs-lookup"><span data-stu-id="529e9-138">As an example, you can use resources.azure.com and edit the ipSecurityRestrictions block to add the required JSON.</span></span> 

<span data-ttu-id="529e9-139">The location for this information in Resource Manager is:</span><span class="sxs-lookup"><span data-stu-id="529e9-139">The location for this information in Resource Manager is:</span></span>

<span data-ttu-id="529e9-140">management.azure.com/subscriptions/**subscription ID**/resourceGroups/**resource groups**/providers/Microsoft.Web/sites/**web app name**/config/web?api-version=2018-02-01</span><span class="sxs-lookup"><span data-stu-id="529e9-140">management.azure.com/subscriptions/**subscription ID**/resourceGroups/**resource groups**/providers/Microsoft.Web/sites/**web app name**/config/web?api-version=2018-02-01</span></span>

<span data-ttu-id="529e9-141">The JSON syntax for the earlier example is:</span><span class="sxs-lookup"><span data-stu-id="529e9-141">The JSON syntax for the earlier example is:</span></span>

    "ipSecurityRestrictions": [
      {
        "ipAddress": "131.107.159.0/24",
        "action": "Allow",
        "tag": "Default",
        "priority": 100,
        "name": "allowed access"
      }
    ],
