---
title: Using Ruby in Azure App Service Web Apps on Linux | Microsoft Docs
description: Using Ruby in Azure App Service Web Apps on Linux.
keywords: azure app service, web app, faq, linux, oss, ruby
services: app-service
documentationCenter: ''
authors: aelnably
manager: erikre
editor: ''
ms.assetid: ''
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: e77b5abe10582262dd50000a605843eebe00ac4b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661459"
---
# <a name="using-ruby-in-web-apps-on-linux"></a><span data-ttu-id="a79e7-104">Using Ruby in Web Apps on Linux</span><span class="sxs-lookup"><span data-stu-id="a79e7-104">Using Ruby in Web Apps on Linux</span></span> #

<span data-ttu-id="a79e7-105">With the latest update to our backend, we introduced support for Ruby v.2.3.</span><span class="sxs-lookup"><span data-stu-id="a79e7-105">With the latest update to our backend, we introduced support for Ruby v.2.3.</span></span> <span data-ttu-id="a79e7-106">By setting the configuration of your Linux web app, you can change the application stack.</span><span class="sxs-lookup"><span data-stu-id="a79e7-106">By setting the configuration of your Linux web app, you can change the application stack.</span></span>

## <a name="using-the-azure-portal"></a><span data-ttu-id="a79e7-107">Using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a79e7-107">Using the Azure portal</span></span> ##

<span data-ttu-id="a79e7-108">From the new menu in the [Azure portal](https://portal.azure.com), you can choose to create a Web App on Linux from the Web + Mobile option as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="a79e7-108">From the new menu in the [Azure portal](https://portal.azure.com), you can choose to create a Web App on Linux from the Web + Mobile option as shown in the following image:</span></span>

![Start creating a web app on the Azure portal][1]

<span data-ttu-id="a79e7-110">Next, the **Create blade** opens as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="a79e7-110">Next, the **Create blade** opens as shown in the following image:</span></span>

![The Create blade][2]

1. <span data-ttu-id="a79e7-112">Give your web app a name.</span><span class="sxs-lookup"><span data-stu-id="a79e7-112">Give your web app a name.</span></span>
2. <span data-ttu-id="a79e7-113">Choose an existing resource group or create a new one.</span><span class="sxs-lookup"><span data-stu-id="a79e7-113">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="a79e7-114">(See available regions in the [limitations section](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="a79e7-114">(See available regions in the [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="a79e7-115">Choose an existing Azure App Service plan or create a new one.</span><span class="sxs-lookup"><span data-stu-id="a79e7-115">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="a79e7-116">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="a79e7-116">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="a79e7-117">Choose the Ruby from the Built-in Runtime stacks.</span><span class="sxs-lookup"><span data-stu-id="a79e7-117">Choose the Ruby from the Built-in Runtime stacks.</span></span>

<span data-ttu-id="a79e7-118">After your Ruby web app gets created, you can deploy to it using Git or FTP.</span><span class="sxs-lookup"><span data-stu-id="a79e7-118">After your Ruby web app gets created, you can deploy to it using Git or FTP.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a79e7-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="a79e7-119">Next steps</span></span>
* [<span data-ttu-id="a79e7-120">What is App Service on Linux?</span><span class="sxs-lookup"><span data-stu-id="a79e7-120">What is App Service on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="a79e7-121">Creating Web Apps in App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="a79e7-121">Creating Web Apps in App Service on Linux</span></span>](app-service-linux-how-to-create-a-web-app.md)
* [<span data-ttu-id="a79e7-122">Local Git Deployment to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a79e7-122">Local Git Deployment to Azure App Service</span></span>](app-service-deploy-local-git.md)
* [<span data-ttu-id="a79e7-123">Azure App Service Web Apps on Linux FAQ</span><span class="sxs-lookup"><span data-stu-id="a79e7-123">Azure App Service Web Apps on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-linux-using-ruby/New-Linux.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-linux-using-ruby/Ruby-UX.png

