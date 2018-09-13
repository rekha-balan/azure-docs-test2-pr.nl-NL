---
title: Introduction to App Service on Linux | Microsoft Docs
description: Learn about Azure App Service on Linux.
keywords: azure app service, linux, oss
services: app-service
documentationcenter: ''
author: naziml
manager: cfowler
editor: ''
ms.assetid: bc85eff6-bbdf-410a-93dc-0f1222796676
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 02/16/2017
ms.author: wesmc
ms.custom: mvc
ms.openlocfilehash: 5ab5452aec5b0371caaf437b6e364ed7b922db3a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857293"
---
# <a name="introduction-to-azure-app-service-on-linux"></a><span data-ttu-id="c5ecd-104">Introduction to Azure App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="c5ecd-104">Introduction to Azure App Service on Linux</span></span>

<span data-ttu-id="c5ecd-105">[Web App](../app-service-web-overview.md) is a fully managed compute platform that is optimized for hosting websites and web applications.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-105">[Web App](../app-service-web-overview.md) is a fully managed compute platform that is optimized for hosting websites and web applications.</span></span> <span data-ttu-id="c5ecd-106">Customers can use App Service on Linux to host web apps natively on Linux for supported application stacks.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-106">Customers can use App Service on Linux to host web apps natively on Linux for supported application stacks.</span></span> <span data-ttu-id="c5ecd-107">The following sections lists the application stacks that are currently supported.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-107">The following sections lists the application stacks that are currently supported.</span></span>

## <a name="languages"></a><span data-ttu-id="c5ecd-108">Languages</span><span class="sxs-lookup"><span data-stu-id="c5ecd-108">Languages</span></span>

<span data-ttu-id="c5ecd-109">App Service on Linux supports a number of Built-in images in order to increase developer productivity.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-109">App Service on Linux supports a number of Built-in images in order to increase developer productivity.</span></span> <span data-ttu-id="c5ecd-110">If the runtime your application requires is not supported in the built-in images, there are instructions on how to [build your own Docker image](tutorial-custom-docker-image.md) to deploy to Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-110">If the runtime your application requires is not supported in the built-in images, there are instructions on how to [build your own Docker image](tutorial-custom-docker-image.md) to deploy to Web App for Containers.</span></span>

| <span data-ttu-id="c5ecd-111">Language</span><span class="sxs-lookup"><span data-stu-id="c5ecd-111">Language</span></span> | <span data-ttu-id="c5ecd-112">Supported Versions</span><span class="sxs-lookup"><span data-stu-id="c5ecd-112">Supported Versions</span></span> |
|---|---|
| <span data-ttu-id="c5ecd-113">Node.js</span><span class="sxs-lookup"><span data-stu-id="c5ecd-113">Node.js</span></span> | <span data-ttu-id="c5ecd-114">4.4, 4.5, 4.8, 6.2, 6.6, 6.9, 6.10, 6.11, 8.0, 8.1, 8.2, 8.8, 8.9, 9.4</span><span class="sxs-lookup"><span data-stu-id="c5ecd-114">4.4, 4.5, 4.8, 6.2, 6.6, 6.9, 6.10, 6.11, 8.0, 8.1, 8.2, 8.8, 8.9, 9.4</span></span> |
| <span data-ttu-id="c5ecd-115">Java \*</span><span class="sxs-lookup"><span data-stu-id="c5ecd-115">Java \*</span></span> | <span data-ttu-id="c5ecd-116">8.0</span><span class="sxs-lookup"><span data-stu-id="c5ecd-116">8.0</span></span> |
| <span data-ttu-id="c5ecd-117">PHP</span><span class="sxs-lookup"><span data-stu-id="c5ecd-117">PHP</span></span> | <span data-ttu-id="c5ecd-118">5.6, 7.0, 7.2</span><span class="sxs-lookup"><span data-stu-id="c5ecd-118">5.6, 7.0, 7.2</span></span> |
| <span data-ttu-id="c5ecd-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="c5ecd-119">.NET Core</span></span> | <span data-ttu-id="c5ecd-120">1.0, 1.1, 2.0</span><span class="sxs-lookup"><span data-stu-id="c5ecd-120">1.0, 1.1, 2.0</span></span> |
| <span data-ttu-id="c5ecd-121">Ruby</span><span class="sxs-lookup"><span data-stu-id="c5ecd-121">Ruby</span></span> | <span data-ttu-id="c5ecd-122">2.3</span><span class="sxs-lookup"><span data-stu-id="c5ecd-122">2.3</span></span> |
| <span data-ttu-id="c5ecd-123">Go</span><span class="sxs-lookup"><span data-stu-id="c5ecd-123">Go</span></span> | <span data-ttu-id="c5ecd-124">1.0</span><span class="sxs-lookup"><span data-stu-id="c5ecd-124">1.0</span></span> |
| <span data-ttu-id="c5ecd-125">Apache Tomcat</span><span class="sxs-lookup"><span data-stu-id="c5ecd-125">Apache Tomcat</span></span> | <span data-ttu-id="c5ecd-126">8.5, 9.0</span><span class="sxs-lookup"><span data-stu-id="c5ecd-126">8.5, 9.0</span></span> |

<span data-ttu-id="c5ecd-127">See [Create a Java web app in App Service on Linux](https://docs.microsoft.com/azure/app-service/containers/quickstart-java) for more details.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-127">See [Create a Java web app in App Service on Linux](https://docs.microsoft.com/azure/app-service/containers/quickstart-java) for more details.</span></span>

## <a name="deployments"></a><span data-ttu-id="c5ecd-128">Deployments</span><span class="sxs-lookup"><span data-stu-id="c5ecd-128">Deployments</span></span>

* <span data-ttu-id="c5ecd-129">FTP</span><span class="sxs-lookup"><span data-stu-id="c5ecd-129">FTP</span></span>
* <span data-ttu-id="c5ecd-130">Local Git</span><span class="sxs-lookup"><span data-stu-id="c5ecd-130">Local Git</span></span>
* <span data-ttu-id="c5ecd-131">GitHub</span><span class="sxs-lookup"><span data-stu-id="c5ecd-131">GitHub</span></span>
* <span data-ttu-id="c5ecd-132">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="c5ecd-132">Bitbucket</span></span>

## <a name="devops"></a><span data-ttu-id="c5ecd-133">DevOps</span><span class="sxs-lookup"><span data-stu-id="c5ecd-133">DevOps</span></span>

* <span data-ttu-id="c5ecd-134">Staging environments</span><span class="sxs-lookup"><span data-stu-id="c5ecd-134">Staging environments</span></span>
* <span data-ttu-id="c5ecd-135">[Azure Container Registry](https://docs.microsoft.com/azure/container-registry/container-registry-intro) and DockerHub CI/CD</span><span class="sxs-lookup"><span data-stu-id="c5ecd-135">[Azure Container Registry](https://docs.microsoft.com/azure/container-registry/container-registry-intro) and DockerHub CI/CD</span></span>

## <a name="console-publishing-and-debugging"></a><span data-ttu-id="c5ecd-136">Console, Publishing, and Debugging</span><span class="sxs-lookup"><span data-stu-id="c5ecd-136">Console, Publishing, and Debugging</span></span>

* <span data-ttu-id="c5ecd-137">Environments</span><span class="sxs-lookup"><span data-stu-id="c5ecd-137">Environments</span></span>
* <span data-ttu-id="c5ecd-138">Deployments</span><span class="sxs-lookup"><span data-stu-id="c5ecd-138">Deployments</span></span>
* <span data-ttu-id="c5ecd-139">Basic console</span><span class="sxs-lookup"><span data-stu-id="c5ecd-139">Basic console</span></span>
* <span data-ttu-id="c5ecd-140">SSH</span><span class="sxs-lookup"><span data-stu-id="c5ecd-140">SSH</span></span>

## <a name="scaling"></a><span data-ttu-id="c5ecd-141">Scaling</span><span class="sxs-lookup"><span data-stu-id="c5ecd-141">Scaling</span></span>

* <span data-ttu-id="c5ecd-142">Customers can scale web apps up and down by changing the tier of their [App Service plan](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview?toc=%2fazure%2fapp-service-web%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="c5ecd-142">Customers can scale web apps up and down by changing the tier of their [App Service plan](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview?toc=%2fazure%2fapp-service-web%2ftoc.json)</span></span>

## <a name="locations"></a><span data-ttu-id="c5ecd-143">Locations</span><span class="sxs-lookup"><span data-stu-id="c5ecd-143">Locations</span></span>

<span data-ttu-id="c5ecd-144">Check the [Azure Status Dashboard](https://azure.microsoft.com/status).</span><span class="sxs-lookup"><span data-stu-id="c5ecd-144">Check the [Azure Status Dashboard](https://azure.microsoft.com/status).</span></span>

## <a name="limitations"></a><span data-ttu-id="c5ecd-145">Limitations</span><span class="sxs-lookup"><span data-stu-id="c5ecd-145">Limitations</span></span>

<span data-ttu-id="c5ecd-146">The Azure portal shows only features that currently work for Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-146">The Azure portal shows only features that currently work for Web App for Containers.</span></span> <span data-ttu-id="c5ecd-147">As we enable more features, they will become visible on the portal.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-147">As we enable more features, they will become visible on the portal.</span></span>

<span data-ttu-id="c5ecd-148">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not available yet.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-148">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not available yet.</span></span> <span data-ttu-id="c5ecd-149">Once these features are available, we will update our documentation and blog about the changes.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-149">Once these features are available, we will update our documentation and blog about the changes.</span></span>

<span data-ttu-id="c5ecd-150">App Service on Linux is only supported with [Basic, Standard, and Premium](https://azure.microsoft.com/pricing/details/app-service/plans/) app service plans and does not have a [Free or Shared](https://azure.microsoft.com/pricing/details/app-service/plans/) tier.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-150">App Service on Linux is only supported with [Basic, Standard, and Premium](https://azure.microsoft.com/pricing/details/app-service/plans/) app service plans and does not have a [Free or Shared](https://azure.microsoft.com/pricing/details/app-service/plans/) tier.</span></span> <span data-ttu-id="c5ecd-151">You cannot create Web App for Containers in an App Service plan already hosting non-Linux Web Apps.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-151">You cannot create Web App for Containers in an App Service plan already hosting non-Linux Web Apps.</span></span> <span data-ttu-id="c5ecd-152">There is a current limitation in regards to not mixing Windows and Linux apps in the same resource group as well.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-152">There is a current limitation in regards to not mixing Windows and Linux apps in the same resource group as well.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c5ecd-153">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="c5ecd-153">Troubleshooting</span></span>

<span data-ttu-id="c5ecd-154">When your application fails to start or you want to check the logging from your app, check the Docker logs in the LogFiles directory.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-154">When your application fails to start or you want to check the logging from your app, check the Docker logs in the LogFiles directory.</span></span> <span data-ttu-id="c5ecd-155">You can access this directory either through your SCM site or via FTP.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-155">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="c5ecd-156">To log the `stdout` and `stderr` from your container, you need to enable **Docker Container logging** under **Diagnostics Logs**.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-156">To log the `stdout` and `stderr` from your container, you need to enable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Enabling Logging][2]

![Using Kudu to view Docker logs][1]

<span data-ttu-id="c5ecd-159">You can access the SCM site from **Advanced Tools** in the **Development Tools** menu.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-159">You can access the SCM site from **Advanced Tools** in the **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5ecd-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="c5ecd-160">Next steps</span></span>

<span data-ttu-id="c5ecd-161">See the following links to get started with App Service on Linux.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-161">See the following links to get started with App Service on Linux.</span></span> <span data-ttu-id="c5ecd-162">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="c5ecd-162">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="c5ecd-163">How to use a custom Docker image for Web App for Containers</span><span class="sxs-lookup"><span data-stu-id="c5ecd-163">How to use a custom Docker image for Web App for Containers</span></span>](quickstart-docker-go.md)
* [<span data-ttu-id="c5ecd-164">Using .NET Core in Azure App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="c5ecd-164">Using .NET Core in Azure App Service on Linux</span></span>](quickstart-dotnetcore.md)
* [<span data-ttu-id="c5ecd-165">Using Ruby in Azure App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="c5ecd-165">Using Ruby in Azure App Service on Linux</span></span>](quickstart-ruby.md)
* [<span data-ttu-id="c5ecd-166">Azure App Service Web App for Containers FAQ</span><span class="sxs-lookup"><span data-stu-id="c5ecd-166">Azure App Service Web App for Containers FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="c5ecd-167">SSH support for Azure App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="c5ecd-167">SSH support for Azure App Service on Linux</span></span>](app-service-linux-ssh-support.md)
* [<span data-ttu-id="c5ecd-168">Set up staging environments in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c5ecd-168">Set up staging environments in Azure App Service</span></span>](../../app-service/web-sites-staged-publishing.md?toc=%2fazure%2fapp-service%2fcontainers%2ftoc.json)
* [<span data-ttu-id="c5ecd-169">Docker Hub Continuous Deployment with Web App for Containers</span><span class="sxs-lookup"><span data-stu-id="c5ecd-169">Docker Hub Continuous Deployment with Web App for Containers</span></span>](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png
