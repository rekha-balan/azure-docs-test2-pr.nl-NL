---
title: Connect a Web App to a Content Deliver Network | Microsoft Docs
description: Connect a Web App to a Content Deliver Network to deliver your static files from edge nodes.
services: app-service
author: syntaxc4
ms.author: cfowler
ms.date: 04/03/2017
ms.topic: hero-article
ms.service: app-service-web
manager: erikre
ms.openlocfilehash: 6c32371d9002c96ba62c4009f883aee3dcf85acd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556156"
---
# <a name="connect-a-web-app-to-a-content-delivery-network"></a>Connect a Web App to a Content Delivery Network

In this tutorial, you will create an Azure CDN Profile and an Azure CDN Endpoint to serve the static files from your Web App via the Azure CDN pop locations.

> [!TIP]
> Review the up to date list of [Azure CDN pop locations](https://docs.microsoft.com/en-us/azure/cdn/cdn-pop-locations).
>

## <a name="step-1---login-to-azure-portal"></a>Step 1 - Login to Azure Portal

First, open your favorite browser and browse to the Azure [Portal](https://portal.azure.com).

## <a name="step-2---create-a-cdn-profile"></a>Step 2 - Create a CDN Profile

Click the **+ New** button in the left hand navigation, Click on **Web + Mobile**. Under the Web + Mobile category, select **CDN**.

Specify the **Name**, **Location**, **Resource group**, **Pricing tier**, then click **Create**.

Open the resource groups hub from the left hand navigation, select **myResourceGroup**. From the resource listing, select **myCDNProfile**.

![azure-cdn-profile-created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-content-delivery-network/azure-cdn-profile-created.png)

## <a name="step-3---create-a-cdn-endpoint"></a>Step 3 - Create a CDN Endpoint

Click on **+ Endpoint** from the commands beside the search box, this will launch the Endpoint creation blade.

Specify the **Name**, **Origin type**, **Origin hostname**, then click **Add**.

The Endpoint will be created, once the Content Delivery Network endpoint is created the status will be updated to **running**.

![azure-cdn-endpoint-created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-content-delivery-network/azure-cdn-endpoint-created.png)

## <a name="step-4---leveraging-cdn"></a>Step 4 - Leveraging CDN

Now that the endpoint is running, let's validate that the content is available on the pop server by browsing to a static file on the web server, then changing the hostname from `http://<app_name>.azurewebsites.net/path/to-static-file` to `http://<endpoint_name>.azureedge.net/path/to-static-file`.

![app-service-web-url-to-cdn-endpoint-url](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-tutorial-content-delivery-network/app-service-web-url-to-cdn-endpoint-url.png)

## <a name="next-steps"></a>Next Steps




