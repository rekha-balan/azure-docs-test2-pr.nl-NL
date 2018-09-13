---
title: How to use io.js with Azure App Service Web Apps
description: Learn how to use a web app in Azure App Service with io.js.
services: app-service\web
documentationcenter: nodejs
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: 5c14bd2ae2effd554f52662961c2e219433f8cd8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551481"
---
# <a name="how-to-use-iojs-with-azure-app-service-web-apps"></a><span data-ttu-id="64a0b-103">How to use io.js with Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="64a0b-103">How to use io.js with Azure App Service Web Apps</span></span>
<span data-ttu-id="64a0b-104">The popular Node fork [io.js] features various differences to Joyent's Node.js project, including a more open governance model, a faster release cycle and a faster adoption of new and experimental JavaScript features.</span><span class="sxs-lookup"><span data-stu-id="64a0b-104">The popular Node fork [io.js] features various differences to Joyent's Node.js project, including a more open governance model, a faster release cycle and a faster adoption of new and experimental JavaScript features.</span></span>

<span data-ttu-id="64a0b-105">While [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps has many Node.js versions preinstalled, it also allows for an user-provided Node.js binary.</span><span class="sxs-lookup"><span data-stu-id="64a0b-105">While [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps has many Node.js versions preinstalled, it also allows for an user-provided Node.js binary.</span></span> <span data-ttu-id="64a0b-106">This article discusses two methods enabling the use of io.js on App Service Web Apps: The use of an extended deployment script, which automatically configures Azure to use the latest available io.js version, as well as the manual upload of a io.js binary.</span><span class="sxs-lookup"><span data-stu-id="64a0b-106">This article discusses two methods enabling the use of io.js on App Service Web Apps: The use of an extended deployment script, which automatically configures Azure to use the latest available io.js version, as well as the manual upload of a io.js binary.</span></span> 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a><span data-ttu-id="64a0b-107">Using a Deployment Script</span><span class="sxs-lookup"><span data-stu-id="64a0b-107">Using a Deployment Script</span></span>
<span data-ttu-id="64a0b-108">Upon deployment of a Node.js app, App Service Web Apps runs a number of small commands to ensure that the environment is configured properly.</span><span class="sxs-lookup"><span data-stu-id="64a0b-108">Upon deployment of a Node.js app, App Service Web Apps runs a number of small commands to ensure that the environment is configured properly.</span></span> <span data-ttu-id="64a0b-109">Using a deployment script, this process can be customized to include the download and configuration of io.js.</span><span class="sxs-lookup"><span data-stu-id="64a0b-109">Using a deployment script, this process can be customized to include the download and configuration of io.js.</span></span>

<span data-ttu-id="64a0b-110">The [io.js Deployment Script](https://github.com/felixrieseberg/iojs-azure) is available on GitHub.</span><span class="sxs-lookup"><span data-stu-id="64a0b-110">The [io.js Deployment Script](https://github.com/felixrieseberg/iojs-azure) is available on GitHub.</span></span> <span data-ttu-id="64a0b-111">To enable io.js on your web app, simply copy **.deployment**, **deploy.cmd** and **IISNode.yml** to the root of your application folder and deploy to Web Apps.</span><span class="sxs-lookup"><span data-stu-id="64a0b-111">To enable io.js on your web app, simply copy **.deployment**, **deploy.cmd** and **IISNode.yml** to the root of your application folder and deploy to Web Apps.</span></span>  

<span data-ttu-id="64a0b-112">The first file, **.deployment**, instructs Web Apps to run **deploy.cmd** upon deployment.</span><span class="sxs-lookup"><span data-stu-id="64a0b-112">The first file, **.deployment**, instructs Web Apps to run **deploy.cmd** upon deployment.</span></span> <span data-ttu-id="64a0b-113">This script runs all the usual steps for a Node.js application, but also downloads the latest version of io.js.</span><span class="sxs-lookup"><span data-stu-id="64a0b-113">This script runs all the usual steps for a Node.js application, but also downloads the latest version of io.js.</span></span> <span data-ttu-id="64a0b-114">Finally, **IISNode.yml** configures Web Apps to use just the downloaded io.js binary instead of a pre-installed Node.js binary.</span><span class="sxs-lookup"><span data-stu-id="64a0b-114">Finally, **IISNode.yml** configures Web Apps to use just the downloaded io.js binary instead of a pre-installed Node.js binary.</span></span>

> [!NOTE]
> <span data-ttu-id="64a0b-115">To update the used io.js binary, just redeploy your application - the script will download a new version of io.js every single time the application is deployed.</span><span class="sxs-lookup"><span data-stu-id="64a0b-115">To update the used io.js binary, just redeploy your application - the script will download a new version of io.js every single time the application is deployed.</span></span>
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a><span data-ttu-id="64a0b-116">Using Manual Installation</span><span class="sxs-lookup"><span data-stu-id="64a0b-116">Using Manual Installation</span></span>
<span data-ttu-id="64a0b-117">The manual installation of a custom io.js version includes only two steps.</span><span class="sxs-lookup"><span data-stu-id="64a0b-117">The manual installation of a custom io.js version includes only two steps.</span></span> <span data-ttu-id="64a0b-118">First, download the **win-x64** binary directly from the [io.js distribution].</span><span class="sxs-lookup"><span data-stu-id="64a0b-118">First, download the **win-x64** binary directly from the [io.js distribution].</span></span> <span data-ttu-id="64a0b-119">Required are two files - **iojs.exe** and **iojs.lib**.</span><span class="sxs-lookup"><span data-stu-id="64a0b-119">Required are two files - **iojs.exe** and **iojs.lib**.</span></span> <span data-ttu-id="64a0b-120">Save both files to a folder inside your web app, for example in **bin/iojs**.</span><span class="sxs-lookup"><span data-stu-id="64a0b-120">Save both files to a folder inside your web app, for example in **bin/iojs**.</span></span>

<span data-ttu-id="64a0b-121">To configure Web Apps to use **iojs.exe** instead of a pre-installed Node version, create a **IISNode.yml** file at the root of your application and add the following line.</span><span class="sxs-lookup"><span data-stu-id="64a0b-121">To configure Web Apps to use **iojs.exe** instead of a pre-installed Node version, create a **IISNode.yml** file at the root of your application and add the following line.</span></span>

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="64a0b-122">Next Steps</span><span class="sxs-lookup"><span data-stu-id="64a0b-122">Next Steps</span></span>
<span data-ttu-id="64a0b-123">In this article you learned how to use io.js with App Service Web Apps, using both provided deployment scripts as well as manual installation.</span><span class="sxs-lookup"><span data-stu-id="64a0b-123">In this article you learned how to use io.js with App Service Web Apps, using both provided deployment scripts as well as manual installation.</span></span> 

> [!NOTE]
> <span data-ttu-id="64a0b-124">io.js is in heavy development and updated more frequently than Node.js.</span><span class="sxs-lookup"><span data-stu-id="64a0b-124">io.js is in heavy development and updated more frequently than Node.js.</span></span> <span data-ttu-id="64a0b-125">A number of Node.js modules might not work with io.js - please consult [io.js on GitHub] for troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="64a0b-125">A number of Node.js modules might not work with io.js - please consult [io.js on GitHub] for troubleshooting.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="64a0b-126">What's changed</span><span class="sxs-lookup"><span data-stu-id="64a0b-126">What's changed</span></span>
* <span data-ttu-id="64a0b-127">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="64a0b-127">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="64a0b-128">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="64a0b-128">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="64a0b-129">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="64a0b-129">No credit cards required; no commitments.</span></span>
> 
> 

[io.js]: https://iojs.org
[io.js distribution]: https://iojs.org/dist/
[io.js on GitHub]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
