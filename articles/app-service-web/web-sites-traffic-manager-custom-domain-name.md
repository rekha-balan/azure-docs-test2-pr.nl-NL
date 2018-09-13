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
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a>Configuring a custom domain name for a web app in Azure App Service using Traffic Manager
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

This article provides generic instructions for using a custom domain name with Azure App Service that use Traffic Manager for load balancing.

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>Understanding DNS records
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a>Configure your web apps for standard mode
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>Add a DNS record for your custom domain
> [!NOTE]
> If you have purchased domain through Azure App Service Web Apps then skip following steps and refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md) article.
> 
> 

To associate your custom domain with a web app in Azure App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by the domain registrar that you purchased your domain name from. Use the following steps to locate and use the DNS tools.

1. Sign in to your account at your domain registrar, and look for a page for managing DNS records. Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**. Often a link to this page can be found be viewing your account information, and then looking for a link such as **My domains**.
2. Once you have found the management page for your domain name, look for a link that allows you to edit the DNS records. This might be listed as a **Zone file**, **DNS Records**, or as an **Advanced** configuration link.
   
   * The page will most likely have a few records already created, such as an entry associating '**@**' or '\*' with a 'domain parking' page. It may also contain records for common sub-domains such as **www**.
   * The page will mention **CNAME records**, or provide a drop-down to select a record type. It may also mention other records such as **A records** and **MX records**. In some cases, CNAME records will be called by other names such as an **Alias Record**.
   * The page will also have fields that allow you to **map** from a **Host name** or **Domain name** to another domain name.
3. While the specifics of each registrar vary, in general you map *from* your custom domain name (such as **contoso.com**,) *to* the Traffic Manager domain name (**contoso.trafficmanager.net**) that is used for your web app.
   
   > [!NOTE]
   > Alternatively, if a record is already in use and you need to preemptively bind your apps to it, you can create an additional CNAME record. For example, to preemptively bind **www.contoso.com** to your web app, create a CNAME record from **awverify.www** to **contoso.trafficmanager.net**. You can then add "www.contoso.com" to your Web App without changing the "www" CNAME record. For more information, see [Create DNS records for a web app in a custom domain][CREATEDNS].
   > 
   > 
4. Once you have finished adding or modifying DNS records at your registrar, save the changes.

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a>Enable Traffic Manager
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a>Next steps
For more information, see the [Node.js Developer Center](/develop/nodejs/).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
