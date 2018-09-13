---
title: Run a custom Windows container in Azure (Preview) | Microsoft Docs
description: Learn how to deploy a custom Windows container into Azure App Service.
services: app-service\web
documentationcenter: ''
author: cephalin
manager: jeconnoc
editor: ''
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 08/07/2018
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: e8f357347e39c2e8ff071e8f4af8e69dcce3940e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866481"
---
# <a name="run-a-custom-windows-container-in-azure-preview"></a><span data-ttu-id="eeec9-103">Run a custom Windows container in Azure (Preview)</span><span class="sxs-lookup"><span data-stu-id="eeec9-103">Run a custom Windows container in Azure (Preview)</span></span>

<span data-ttu-id="eeec9-104">[Azure App Service](app-service-web-overview.md) provides pre-defined application stacks on Windows like ASP.NET or Node.js, running on IIS.</span><span class="sxs-lookup"><span data-stu-id="eeec9-104">[Azure App Service](app-service-web-overview.md) provides pre-defined application stacks on Windows like ASP.NET or Node.js, running on IIS.</span></span> <span data-ttu-id="eeec9-105">The preconfigured Windows environment locks down the operating system from administrative access, software installations, changes to the global assembly cache, and so on (see [Operating system functionality on Azure App Service](web-sites-available-operating-system-functionality.md)).</span><span class="sxs-lookup"><span data-stu-id="eeec9-105">The preconfigured Windows environment locks down the operating system from administrative access, software installations, changes to the global assembly cache, and so on (see [Operating system functionality on Azure App Service](web-sites-available-operating-system-functionality.md)).</span></span> <span data-ttu-id="eeec9-106">If your application requires more access than the preconfigured environment allows, you can deploy a custom Windows container instead.</span><span class="sxs-lookup"><span data-stu-id="eeec9-106">If your application requires more access than the preconfigured environment allows, you can deploy a custom Windows container instead.</span></span> <span data-ttu-id="eeec9-107">This quickstart shows how to deploy a custom IIS image to Azure App Service from [Docker Hub](https://hub.docker.com/).</span><span class="sxs-lookup"><span data-stu-id="eeec9-107">This quickstart shows how to deploy a custom IIS image to Azure App Service from [Docker Hub](https://hub.docker.com/).</span></span>

![](media/app-service-web-get-started-windows-container/app-running.png)

## <a name="sign-in-to-azure"></a><span data-ttu-id="eeec9-108">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="eeec9-108">Sign in to Azure</span></span>

<span data-ttu-id="eeec9-109">Sign in to the Azure portal at https://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="eeec9-109">Sign in to the Azure portal at https://portal.azure.com.</span></span>

## <a name="create-a-windows-container-app"></a><span data-ttu-id="eeec9-110">Create a Windows container app</span><span class="sxs-lookup"><span data-stu-id="eeec9-110">Create a Windows container app</span></span>

1. <span data-ttu-id="eeec9-111">Choose **Create a resource** in the upper left-hand corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="eeec9-111">Choose **Create a resource** in the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="eeec9-112">In the search box above the list of Azure Marketplace resources, search for and select **Web App for Containers**.</span><span class="sxs-lookup"><span data-stu-id="eeec9-112">In the search box above the list of Azure Marketplace resources, search for and select **Web App for Containers**.</span></span>

3. <span data-ttu-id="eeec9-113">Provide an app name, such as *mywebapp*, accept the defaults to create a new resource group, and click **Windows (Preview)** in the **OS** box.</span><span class="sxs-lookup"><span data-stu-id="eeec9-113">Provide an app name, such as *mywebapp*, accept the defaults to create a new resource group, and click **Windows (Preview)** in the **OS** box.</span></span>

    ![](media/app-service-web-get-started-windows-container/portal-create-page.png)

4. <span data-ttu-id="eeec9-114">Create an App Service plan by clicking **App Service plan/Location** > **Create new**.</span><span class="sxs-lookup"><span data-stu-id="eeec9-114">Create an App Service plan by clicking **App Service plan/Location** > **Create new**.</span></span> <span data-ttu-id="eeec9-115">Give the new plan a name, accept the defaults, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="eeec9-115">Give the new plan a name, accept the defaults, and click **OK**.</span></span>

    ![](media/app-service-web-get-started-windows-container/portal-create-plan.png)

5. <span data-ttu-id="eeec9-116">Click **Configure container**, type _microsoft/iis:latest_ in **Image and optional tag**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="eeec9-116">Click **Configure container**, type _microsoft/iis:latest_ in **Image and optional tag**, and click **OK**.</span></span>

    ![](media/app-service-web-get-started-windows-container/portal-configure-container.png)

    <span data-ttu-id="eeec9-117">In this article, you use the public [microsoft/iis:latest](https://hub.docker.com/r/microsoft/iis/) Docker Hub image.</span><span class="sxs-lookup"><span data-stu-id="eeec9-117">In this article, you use the public [microsoft/iis:latest](https://hub.docker.com/r/microsoft/iis/) Docker Hub image.</span></span> <span data-ttu-id="eeec9-118">If you have a custom image elsewhere for your web application, such as in [Azure Container Registry](/azure/container-registry/) or in any other private repository, you can configure it here.</span><span class="sxs-lookup"><span data-stu-id="eeec9-118">If you have a custom image elsewhere for your web application, such as in [Azure Container Registry](/azure/container-registry/) or in any other private repository, you can configure it here.</span></span>

6. <span data-ttu-id="eeec9-119">Click **Create** and wait for Azure to create the required resources.</span><span class="sxs-lookup"><span data-stu-id="eeec9-119">Click **Create** and wait for Azure to create the required resources.</span></span>

## <a name="browse-to-the-container-app"></a><span data-ttu-id="eeec9-120">Browse to the container app</span><span class="sxs-lookup"><span data-stu-id="eeec9-120">Browse to the container app</span></span>

<span data-ttu-id="eeec9-121">When the Azure operation is complete, a notification box is displayed.</span><span class="sxs-lookup"><span data-stu-id="eeec9-121">When the Azure operation is complete, a notification box is displayed.</span></span>

![](media/app-service-web-get-started-windows-container/portal-create-finished.png)

1. <span data-ttu-id="eeec9-122">Click **Go to resource**.</span><span class="sxs-lookup"><span data-stu-id="eeec9-122">Click **Go to resource**.</span></span>

2. <span data-ttu-id="eeec9-123">In the app page, click the link under **URL**.</span><span class="sxs-lookup"><span data-stu-id="eeec9-123">In the app page, click the link under **URL**.</span></span>

<span data-ttu-id="eeec9-124">A new browser page is opened to the following page:</span><span class="sxs-lookup"><span data-stu-id="eeec9-124">A new browser page is opened to the following page:</span></span>

![](media/app-service-web-get-started-windows-container/app-starting.png)

<span data-ttu-id="eeec9-125">Wait a few minutes and try again, until you get the IIS welcome page:</span><span class="sxs-lookup"><span data-stu-id="eeec9-125">Wait a few minutes and try again, until you get the IIS welcome page:</span></span>

![](media/app-service-web-get-started-windows-container/app-running.png)

<span data-ttu-id="eeec9-126">**Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="eeec9-126">**Congratulations!**</span></span> <span data-ttu-id="eeec9-127">You're running your first custom Windows container in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="eeec9-127">You're running your first custom Windows container in Azure App Service.</span></span>

## <a name="see-container-start-up-logs"></a><span data-ttu-id="eeec9-128">See container start-up logs</span><span class="sxs-lookup"><span data-stu-id="eeec9-128">See container start-up logs</span></span>

<span data-ttu-id="eeec9-129">It may take some time for the Windows container to load.</span><span class="sxs-lookup"><span data-stu-id="eeec9-129">It may take some time for the Windows container to load.</span></span> <span data-ttu-id="eeec9-130">To see the progress, navigate to the following URL by replacing *\<app_name>* with the name of your app.</span><span class="sxs-lookup"><span data-stu-id="eeec9-130">To see the progress, navigate to the following URL by replacing *\<app_name>* with the name of your app.</span></span>
```
https://<app_name>.scm.azurewebsites.net/api/logstream
```

<span data-ttu-id="eeec9-131">The streamed logs looks like this:</span><span class="sxs-lookup"><span data-stu-id="eeec9-131">The streamed logs looks like this:</span></span>

```
2018-07-27T12:03:11  Welcome, you are now connected to log-streaming service.
27/07/2018 12:04:10.978 INFO - Site: win-container-demo - Start container succeeded. Container: facbf6cb214de86e58557a6d073396f640bbe2fdec88f8368695c8d1331fc94b
27/07/2018 12:04:16.767 INFO - Site: win-container-demo - Container start complete
27/07/2018 12:05:05.017 INFO - Site: win-container-demo - Container start complete
27/07/2018 12:05:05.020 INFO - Site: win-container-demo - Container started successfully
```

## <a name="use-a-different-docker-image"></a><span data-ttu-id="eeec9-132">Use a different Docker image</span><span class="sxs-lookup"><span data-stu-id="eeec9-132">Use a different Docker image</span></span>

<span data-ttu-id="eeec9-133">You are free to use a different custom Docker image to run your app.</span><span class="sxs-lookup"><span data-stu-id="eeec9-133">You are free to use a different custom Docker image to run your app.</span></span> <span data-ttu-id="eeec9-134">However, you must choose the right [parent image](https://docs.docker.com/develop/develop-images/baseimages/) for the framework you want:</span><span class="sxs-lookup"><span data-stu-id="eeec9-134">However, you must choose the right [parent image](https://docs.docker.com/develop/develop-images/baseimages/) for the framework you want:</span></span> 

- <span data-ttu-id="eeec9-135">To deploy .NET Framework apps, use a parent image based on the Windows Server Core 2016 [Long-Term Servicing Channel (LTSC)](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#long-term-servicing-channel-ltsc) release.</span><span class="sxs-lookup"><span data-stu-id="eeec9-135">To deploy .NET Framework apps, use a parent image based on the Windows Server Core 2016 [Long-Term Servicing Channel (LTSC)](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#long-term-servicing-channel-ltsc) release.</span></span> 
- <span data-ttu-id="eeec9-136">To deploy .NET Core apps, use a parent image based on the Windows Server Nano 2016 [Long-Term Servicing Channel (LTSC)](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#long-term-servicing-channel-ltsc) release.</span><span class="sxs-lookup"><span data-stu-id="eeec9-136">To deploy .NET Core apps, use a parent image based on the Windows Server Nano 2016 [Long-Term Servicing Channel (LTSC)](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview#long-term-servicing-channel-ltsc) release.</span></span> 

<span data-ttu-id="eeec9-137">It takes some time to download a parent image during app start-up.</span><span class="sxs-lookup"><span data-stu-id="eeec9-137">It takes some time to download a parent image during app start-up.</span></span> <span data-ttu-id="eeec9-138">However, you can reduce start-up time by using one of the following parent images that are already cached in Azure App Service:</span><span class="sxs-lookup"><span data-stu-id="eeec9-138">However, you can reduce start-up time by using one of the following parent images that are already cached in Azure App Service:</span></span>

- <span data-ttu-id="eeec9-139">[microsoft/iis](https://hub.docker.com/r/microsoft/iis/):windowsservercore-ltsc2016, latest</span><span class="sxs-lookup"><span data-stu-id="eeec9-139">[microsoft/iis](https://hub.docker.com/r/microsoft/iis/):windowsservercore-ltsc2016, latest</span></span>
- <span data-ttu-id="eeec9-140">[microsoft/iis](https://hub.docker.com/r/microsoft/iis/):nanoserver-sac2016</span><span class="sxs-lookup"><span data-stu-id="eeec9-140">[microsoft/iis](https://hub.docker.com/r/microsoft/iis/):nanoserver-sac2016</span></span>
- <span data-ttu-id="eeec9-141">[microsoft/aspnet](https://hub.docker.com/r/microsoft/aspnet/):4.7.2-windowsservercore-ltsc2016, 4.7.2, latest</span><span class="sxs-lookup"><span data-stu-id="eeec9-141">[microsoft/aspnet](https://hub.docker.com/r/microsoft/aspnet/):4.7.2-windowsservercore-ltsc2016, 4.7.2, latest</span></span>
- <span data-ttu-id="eeec9-142">[microsoft/dotnet](https://hub.docker.com/r/microsoft/dotnet/):2.1-aspnetcore-runtime</span><span class="sxs-lookup"><span data-stu-id="eeec9-142">[microsoft/dotnet](https://hub.docker.com/r/microsoft/dotnet/):2.1-aspnetcore-runtime</span></span>
- <span data-ttu-id="eeec9-143">[microsoft/dotnet](https://hub.docker.com/r/microsoft/dotnet/):2.1-sdk</span><span class="sxs-lookup"><span data-stu-id="eeec9-143">[microsoft/dotnet](https://hub.docker.com/r/microsoft/dotnet/):2.1-sdk</span></span>
