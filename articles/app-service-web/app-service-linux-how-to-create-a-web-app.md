---
title: Create an Azure web app running on Linux | Microsoft Docs
description: Web app creation workflow for App Service on Linux.
keywords: azure app service, web app, linux, oss
services: app-service
documentationcenter: ''
author: naziml
manager: erikre
editor: ''
ms.assetid: 3a71d10a-a0fe-4d28-af95-03b2860057d5
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 66abb1d3d71b7338868e7b0ef86da67d9f12534b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549409"
---
# <a name="create-an-azure-web-app-running-on-linux"></a><span data-ttu-id="41cb8-104">Create an Azure web app running on Linux</span><span class="sxs-lookup"><span data-stu-id="41cb8-104">Create an Azure web app running on Linux</span></span>
## <a name="use-the-azure-portal-to-create-your-web-app"></a><span data-ttu-id="41cb8-105">Use the Azure portal to create your web app</span><span class="sxs-lookup"><span data-stu-id="41cb8-105">Use the Azure portal to create your web app</span></span>
<span data-ttu-id="41cb8-106">You can start creating your web app on Linux from the [Azure portal](https://portal.azure.com) as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="41cb8-106">You can start creating your web app on Linux from the [Azure portal](https://portal.azure.com) as shown in the following image:</span></span>

![Start creating a web app on the Azure portal][1]

<span data-ttu-id="41cb8-108">Next, the **Create blade** opens as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="41cb8-108">Next, the **Create blade** opens as shown in the following image:</span></span>

![The Create blade][2]

1. <span data-ttu-id="41cb8-110">Give your web app a name.</span><span class="sxs-lookup"><span data-stu-id="41cb8-110">Give your web app a name.</span></span>
2. <span data-ttu-id="41cb8-111">Choose an existing resource group or create a new one.</span><span class="sxs-lookup"><span data-stu-id="41cb8-111">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="41cb8-112">(See available regions in the [limitations section](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="41cb8-112">(See available regions in the [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="41cb8-113">Choose an existing Azure App Service plan or create a new one.</span><span class="sxs-lookup"><span data-stu-id="41cb8-113">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="41cb8-114">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="41cb8-114">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="41cb8-115">Choose the application stack that you intend to use.</span><span class="sxs-lookup"><span data-stu-id="41cb8-115">Choose the application stack that you intend to use.</span></span> <span data-ttu-id="41cb8-116">You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.</span><span class="sxs-lookup"><span data-stu-id="41cb8-116">You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.</span></span>

<span data-ttu-id="41cb8-117">Once you have created the app, you can change the application stack from the application settings as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="41cb8-117">Once you have created the app, you can change the application stack from the application settings as shown in the following image:</span></span>

![Application settings][3]

## <a name="deploy-your-web-app"></a><span data-ttu-id="41cb8-119">Deploy your web app</span><span class="sxs-lookup"><span data-stu-id="41cb8-119">Deploy your web app</span></span>
<span data-ttu-id="41cb8-120">Choosing **deployment options** from the management portal gives you the option to use local a Git or GitHub repository to deploy your application.</span><span class="sxs-lookup"><span data-stu-id="41cb8-120">Choosing **deployment options** from the management portal gives you the option to use local a Git or GitHub repository to deploy your application.</span></span> <span data-ttu-id="41cb8-121">The rest of the instructions are similar to those for a non-Linux web app.</span><span class="sxs-lookup"><span data-stu-id="41cb8-121">The rest of the instructions are similar to those for a non-Linux web app.</span></span> <span data-ttu-id="41cb8-122">You can follow the instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) to deploy your app.</span><span class="sxs-lookup"><span data-stu-id="41cb8-122">You can follow the instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) to deploy your app.</span></span>

<span data-ttu-id="41cb8-123">You can also use FTP to upload your application to your site.</span><span class="sxs-lookup"><span data-stu-id="41cb8-123">You can also use FTP to upload your application to your site.</span></span> <span data-ttu-id="41cb8-124">You can get the FTP endpoint for your web app from the diagnostics logs section as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="41cb8-124">You can get the FTP endpoint for your web app from the diagnostics logs section as shown in the following image:</span></span>

![Diagnostics logs][4]

## <a name="next-steps"></a><span data-ttu-id="41cb8-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="41cb8-126">Next steps</span></span>
* [<span data-ttu-id="41cb8-127">What is App Service on Linux?</span><span class="sxs-lookup"><span data-stu-id="41cb8-127">What is App Service on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="41cb8-128">Using PM2 Configuration for Node.js in Web Apps on Linux</span><span class="sxs-lookup"><span data-stu-id="41cb8-128">Using PM2 Configuration for Node.js in Web Apps on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="41cb8-129">Using Ruby in Azure App Service Web Apps on Linux</span><span class="sxs-lookup"><span data-stu-id="41cb8-129">Using Ruby in Azure App Service Web Apps on Linux</span></span>](app-service-linux-using-ruby.md)
* [<span data-ttu-id="41cb8-130">Azure App Service Web Apps on Linux FAQ</span><span class="sxs-lookup"><span data-stu-id="41cb8-130">Azure App Service Web Apps on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png




