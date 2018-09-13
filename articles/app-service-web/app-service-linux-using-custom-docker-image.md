---
title: How to use a custom Docker image for Azure App Service on Linux | Microsoft Docs
description: How to use a custom Docker image for App Service on Linux.
keywords: azure app service, web app, linux, docker, container
services: app-service
documentationcenter: ''
author: naziml
manager: erikre
editor: ''
ms.assetid: b97bd4e6-dff0-4976-ac20-d5c109a559a8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 9788fcd31e1e31867badea1bee7f8fb99757475d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553758"
---
# <a name="using-a-custom-docker-image-for-app-service-on-linux"></a><span data-ttu-id="30e30-104">Using a custom Docker image for App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="30e30-104">Using a custom Docker image for App Service on Linux</span></span> #

<span data-ttu-id="30e30-105">App Service provides pre-defined application stacks on Linux with support for specific versions, such as PHP 7.0 and Node.js 4.5.</span><span class="sxs-lookup"><span data-stu-id="30e30-105">App Service provides pre-defined application stacks on Linux with support for specific versions, such as PHP 7.0 and Node.js 4.5.</span></span> <span data-ttu-id="30e30-106">App Service on Linux uses Docker containers to host these pre-built application stacks.</span><span class="sxs-lookup"><span data-stu-id="30e30-106">App Service on Linux uses Docker containers to host these pre-built application stacks.</span></span> <span data-ttu-id="30e30-107">You can also use a custom Docker image to deploy your web app to an application stack that is not already defined in Azure.</span><span class="sxs-lookup"><span data-stu-id="30e30-107">You can also use a custom Docker image to deploy your web app to an application stack that is not already defined in Azure.</span></span> <span data-ttu-id="30e30-108">Custom Docker images can be hosted on either a public or private Docker repository.</span><span class="sxs-lookup"><span data-stu-id="30e30-108">Custom Docker images can be hosted on either a public or private Docker repository.</span></span>


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a><span data-ttu-id="30e30-109">How to: set a custom Docker image for a web app</span><span class="sxs-lookup"><span data-stu-id="30e30-109">How to: set a custom Docker image for a web app</span></span>
<span data-ttu-id="30e30-110">You can set the custom Docker image for both new and existing webs apps.</span><span class="sxs-lookup"><span data-stu-id="30e30-110">You can set the custom Docker image for both new and existing webs apps.</span></span> <span data-ttu-id="30e30-111">When you create a web app on Linux in the [Azure portal](https://portal.azure.com), click **Configure container** to set a custom Docker image:</span><span class="sxs-lookup"><span data-stu-id="30e30-111">When you create a web app on Linux in the [Azure portal](https://portal.azure.com), click **Configure container** to set a custom Docker image:</span></span>

![Custom Docker Image for a new web app on Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a><span data-ttu-id="30e30-113">How to: use a custom Docker image from Docker Hub</span><span class="sxs-lookup"><span data-stu-id="30e30-113">How to: use a custom Docker image from Docker Hub</span></span> ##
<span data-ttu-id="30e30-114">To use a custom Docker image from Docker Hub:</span><span class="sxs-lookup"><span data-stu-id="30e30-114">To use a custom Docker image from Docker Hub:</span></span>

1. <span data-ttu-id="30e30-115">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span><span class="sxs-lookup"><span data-stu-id="30e30-115">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="30e30-116">Select **Docker Hub** as the **Image source**, then click either **Public** or **Private** and type the **Image and optional tag name**, such as `node:4.5`.</span><span class="sxs-lookup"><span data-stu-id="30e30-116">Select **Docker Hub** as the **Image source**, then click either **Public** or **Private** and type the **Image and optional tag name**, such as `node:4.5`.</span></span> <span data-ttu-id="30e30-117">The **Startup command** is set automatically based on what is defined in the Docker image file, but you can set your own commands.</span><span class="sxs-lookup"><span data-stu-id="30e30-117">The **Startup command** is set automatically based on what is defined in the Docker image file, but you can set your own commands.</span></span>  

    ![Configure Docker Hub public repository image][2]

    <span data-ttu-id="30e30-119">When your image is from a private repository, you also need to enter the Docker Hub credentials as (**Login username** and **Password**) for the private Docker Hub repository.</span><span class="sxs-lookup"><span data-stu-id="30e30-119">When your image is from a private repository, you also need to enter the Docker Hub credentials as (**Login username** and **Password**) for the private Docker Hub repository.</span></span>

    ![Configure Docker Hub private repository image][3]

3. <span data-ttu-id="30e30-121">After you have configured the container, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="30e30-121">After you have configured the container, click **Save**.</span></span>

## <a name="how-to-use-a-docker-image-from-a-private-image-registry"></a><span data-ttu-id="30e30-122">How to use a Docker image from a private image registry</span><span class="sxs-lookup"><span data-stu-id="30e30-122">How to use a Docker image from a private image registry</span></span> ##
<span data-ttu-id="30e30-123">To use a custom Docker image from a private image registry:</span><span class="sxs-lookup"><span data-stu-id="30e30-123">To use a custom Docker image from a private image registry:</span></span>

1. <span data-ttu-id="30e30-124">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span><span class="sxs-lookup"><span data-stu-id="30e30-124">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **Docker Container**.</span></span>

2.  <span data-ttu-id="30e30-125">Click **Private registry** as the **Image source**.</span><span class="sxs-lookup"><span data-stu-id="30e30-125">Click **Private registry** as the **Image source**.</span></span> <span data-ttu-id="30e30-126">Enter the **Image and optional tag name**, **Server URL** for the private registry, along with the credentials (**Login username** and **Password**).</span><span class="sxs-lookup"><span data-stu-id="30e30-126">Enter the **Image and optional tag name**, **Server URL** for the private registry, along with the credentials (**Login username** and **Password**).</span></span> <span data-ttu-id="30e30-127">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="30e30-127">Click **Save**.</span></span>

    ![Configure Docker image from private registry][4]


## <a name="how-to-set-the-port-used-by-your-docker-image"></a><span data-ttu-id="30e30-129">How to: set the port used by your Docker image</span><span class="sxs-lookup"><span data-stu-id="30e30-129">How to: set the port used by your Docker image</span></span> ##

<span data-ttu-id="30e30-130">When you use a custom Docker image for your web app, you can use the `PORT` environment variable in your Dockerfile, which gets added to the generated container.</span><span class="sxs-lookup"><span data-stu-id="30e30-130">When you use a custom Docker image for your web app, you can use the `PORT` environment variable in your Dockerfile, which gets added to the generated container.</span></span> <span data-ttu-id="30e30-131">Consider the following example of a docker file for a Ruby application:</span><span class="sxs-lookup"><span data-stu-id="30e30-131">Consider the following example of a docker file for a Ruby application:</span></span>

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p $PORT -e production

<span data-ttu-id="30e30-132">On last line of the command, you can see that the PORT environment variable is passed at runtime.</span><span class="sxs-lookup"><span data-stu-id="30e30-132">On last line of the command, you can see that the PORT environment variable is passed at runtime.</span></span> <span data-ttu-id="30e30-133">Remember that casing matters in commands.</span><span class="sxs-lookup"><span data-stu-id="30e30-133">Remember that casing matters in commands.</span></span>

<span data-ttu-id="30e30-134">When you use an existing Docker image built by someone else, you may need to specify a port other than port 80 for the application.</span><span class="sxs-lookup"><span data-stu-id="30e30-134">When you use an existing Docker image built by someone else, you may need to specify a port other than port 80 for the application.</span></span> <span data-ttu-id="30e30-135">To configure the port, add an application setting named `PORT` with the value as shown below:</span><span class="sxs-lookup"><span data-stu-id="30e30-135">To configure the port, add an application setting named `PORT` with the value as shown below:</span></span>

![Configure PORT app setting for custom Docker image][6]


## <a name="how-to-switch-back-to-using-a-built-in-image"></a><span data-ttu-id="30e30-137">How to: Switch back to using a built-in image</span><span class="sxs-lookup"><span data-stu-id="30e30-137">How to: Switch back to using a built-in image</span></span> ##

<span data-ttu-id="30e30-138">To switch from using a custom image to using a built-in image:</span><span class="sxs-lookup"><span data-stu-id="30e30-138">To switch from using a custom image to using a built-in image:</span></span>

1. <span data-ttu-id="30e30-139">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **App Service**.</span><span class="sxs-lookup"><span data-stu-id="30e30-139">In the [Azure portal](https://portal.azure.com), locate your web app on Linux, then in **Settings** click **App Service**.</span></span>

2. <span data-ttu-id="30e30-140">Select your **Runtime Stack** to use for the built-in image, then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="30e30-140">Select your **Runtime Stack** to use for the built-in image, then click **Save**.</span></span> 

![Configure Built-In Docker image][5]


## <a name="troubleshooting"></a><span data-ttu-id="30e30-142">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="30e30-142">Troubleshooting</span></span> ##

<span data-ttu-id="30e30-143">When your application fails to start with your custom Docker image, check the Docker logs in the LogFiles/docker directory.</span><span class="sxs-lookup"><span data-stu-id="30e30-143">When your application fails to start with your custom Docker image, check the Docker logs in the LogFiles/docker directory.</span></span> <span data-ttu-id="30e30-144">You can access this directory either through your SCM site or via FTP.</span><span class="sxs-lookup"><span data-stu-id="30e30-144">You can access this directory either through your SCM site or via FTP.</span></span> 

![Using Kudu to view Docker logs][7]

<span data-ttu-id="30e30-146">You can access the SCM site from **Advanced Tools** in the **Development Tools** menu.</span><span class="sxs-lookup"><span data-stu-id="30e30-146">You can access the SCM site from **Advanced Tools** in the **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30e30-147">Next Steps</span><span class="sxs-lookup"><span data-stu-id="30e30-147">Next Steps</span></span> ##

<span data-ttu-id="30e30-148">Follow the following links to get started with App Service on Linux.</span><span class="sxs-lookup"><span data-stu-id="30e30-148">Follow the following links to get started with App Service on Linux.</span></span>   

* [<span data-ttu-id="30e30-149">Introduction to App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="30e30-149">Introduction to App Service on Linux</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="30e30-150">Creating Web Apps in App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="30e30-150">Creating Web Apps in App Service on Linux</span></span>](./app-service-linux-how-to-create-a-web-app.md)
* [<span data-ttu-id="30e30-151">Using PM2 Configuration for Node.js in Web Apps on Linux</span><span class="sxs-lookup"><span data-stu-id="30e30-151">Using PM2 Configuration for Node.js in Web Apps on Linux</span></span>](./app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="30e30-152">Azure App Service Web Apps on Linux FAQ</span><span class="sxs-lookup"><span data-stu-id="30e30-152">Azure App Service Web Apps on Linux FAQ</span></span>](app-service-linux-faq.md)

<span data-ttu-id="30e30-153">Post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="30e30-153">Post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>


<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png







