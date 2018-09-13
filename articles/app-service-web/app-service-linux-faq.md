---
title: Azure App Service web apps on Linux FAQ | Microsoft Docs
description: Azure App Service web apps on Linux FAQ.
keywords: azure app service, web app, faq, linux, oss
services: app-service
documentationCenter: ''
authors: ahmedelnably
manager: erikre
editor: ''
ms.assetid: ''
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: aelnably
ms.openlocfilehash: 148bc76b7f3e09745cbecfa41710a5e949704948
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552618"
---
# <a name="azure-app-service-web-apps-on-linux-faq"></a><span data-ttu-id="86a7b-104">Azure App Service web apps on Linux FAQ</span><span class="sxs-lookup"><span data-stu-id="86a7b-104">Azure App Service web apps on Linux FAQ</span></span>

<span data-ttu-id="86a7b-105">With the release of Azure App Service on Linux (currently in preview), we're working on adding features and making improvements to our platform.</span><span class="sxs-lookup"><span data-stu-id="86a7b-105">With the release of Azure App Service on Linux (currently in preview), we're working on adding features and making improvements to our platform.</span></span> <span data-ttu-id="86a7b-106">Here are some frequently asked questions (FAQ) that our customers have been asking us over the last months.</span><span class="sxs-lookup"><span data-stu-id="86a7b-106">Here are some frequently asked questions (FAQ) that our customers have been asking us over the last months.</span></span>
<span data-ttu-id="86a7b-107">If you have a question, please comment on the article and we'll answer it as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="86a7b-107">If you have a question, please comment on the article and we'll answer it as soon as possible.</span></span>

## <a name="built-in-images"></a><span data-ttu-id="86a7b-108">Built-in images</span><span class="sxs-lookup"><span data-stu-id="86a7b-108">Built-in images</span></span>

<span data-ttu-id="86a7b-109">**Q:** I want to fork the built-in Docker containers that the platform provides.</span><span class="sxs-lookup"><span data-stu-id="86a7b-109">**Q:** I want to fork the built-in Docker containers that the platform provides.</span></span> <span data-ttu-id="86a7b-110">Where can I find those files?</span><span class="sxs-lookup"><span data-stu-id="86a7b-110">Where can I find those files?</span></span>

<span data-ttu-id="86a7b-111">**A:** You can find all Docker files on [GitHub](https://github.com/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="86a7b-111">**A:** You can find all Docker files on [GitHub](https://github.com/azure-app-service).</span></span> <span data-ttu-id="86a7b-112">You can find all Docker containers on [Docker Hub](https://hub.docker.com/u/appsvc/).</span><span class="sxs-lookup"><span data-stu-id="86a7b-112">You can find all Docker containers on [Docker Hub](https://hub.docker.com/u/appsvc/).</span></span>

<span data-ttu-id="86a7b-113">**Q:** What are the expected values for the Startup File section when I configure the runtime stack?</span><span class="sxs-lookup"><span data-stu-id="86a7b-113">**Q:** What are the expected values for the Startup File section when I configure the runtime stack?</span></span>

<span data-ttu-id="86a7b-114">**A:** For Node.Js, you specify the PM2 configuration file or your script file.</span><span class="sxs-lookup"><span data-stu-id="86a7b-114">**A:** For Node.Js, you specify the PM2 configuration file or your script file.</span></span> <span data-ttu-id="86a7b-115">For .NET Core, specify your compiled DLL name.</span><span class="sxs-lookup"><span data-stu-id="86a7b-115">For .NET Core, specify your compiled DLL name.</span></span> <span data-ttu-id="86a7b-116">For Ruby, you can specify the Ruby script that you want to initialize your app with.</span><span class="sxs-lookup"><span data-stu-id="86a7b-116">For Ruby, you can specify the Ruby script that you want to initialize your app with.</span></span>

## <a name="management"></a><span data-ttu-id="86a7b-117">Management</span><span class="sxs-lookup"><span data-stu-id="86a7b-117">Management</span></span>

<span data-ttu-id="86a7b-118">**Q:** I pressed the restart button in the Azure portal, but my web app didn't restart.</span><span class="sxs-lookup"><span data-stu-id="86a7b-118">**Q:** I pressed the restart button in the Azure portal, but my web app didn't restart.</span></span> <span data-ttu-id="86a7b-119">How come?</span><span class="sxs-lookup"><span data-stu-id="86a7b-119">How come?</span></span>

<span data-ttu-id="86a7b-120">**A:** We're working on enabling the restart button in the near future.</span><span class="sxs-lookup"><span data-stu-id="86a7b-120">**A:** We're working on enabling the restart button in the near future.</span></span> <span data-ttu-id="86a7b-121">Right now, you have two options:</span><span class="sxs-lookup"><span data-stu-id="86a7b-121">Right now, you have two options:</span></span>
- <span data-ttu-id="86a7b-122">Add or change a dummy application setting.</span><span class="sxs-lookup"><span data-stu-id="86a7b-122">Add or change a dummy application setting.</span></span> <span data-ttu-id="86a7b-123">This will force your web app to restart.</span><span class="sxs-lookup"><span data-stu-id="86a7b-123">This will force your web app to restart.</span></span>
- <span data-ttu-id="86a7b-124">Stop and then start your web app.</span><span class="sxs-lookup"><span data-stu-id="86a7b-124">Stop and then start your web app.</span></span>

<span data-ttu-id="86a7b-125">**Q:** Can I use Secure Shell (SSH) to connect to the app container virtual machine (VM)?</span><span class="sxs-lookup"><span data-stu-id="86a7b-125">**Q:** Can I use Secure Shell (SSH) to connect to the app container virtual machine (VM)?</span></span>

<span data-ttu-id="86a7b-126">**A:** No.</span><span class="sxs-lookup"><span data-stu-id="86a7b-126">**A:** No.</span></span> <span data-ttu-id="86a7b-127">We'll be providing a way to use SSH to connect to your app container in a future release.</span><span class="sxs-lookup"><span data-stu-id="86a7b-127">We'll be providing a way to use SSH to connect to your app container in a future release.</span></span>

## <a name="continuous-integrationdeployment"></a><span data-ttu-id="86a7b-128">Continuous integration/deployment</span><span class="sxs-lookup"><span data-stu-id="86a7b-128">Continuous integration/deployment</span></span>

<span data-ttu-id="86a7b-129">**Q:** My web app still uses an old Docker container image after I've updated the image on Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="86a7b-129">**Q:** My web app still uses an old Docker container image after I've updated the image on Docker Hub.</span></span> <span data-ttu-id="86a7b-130">Do you support continuous integration/deployment of custom containers?</span><span class="sxs-lookup"><span data-stu-id="86a7b-130">Do you support continuous integration/deployment of custom containers?</span></span>

<span data-ttu-id="86a7b-131">**A:** You can refresh the container by stopping and then starting your web app.</span><span class="sxs-lookup"><span data-stu-id="86a7b-131">**A:** You can refresh the container by stopping and then starting your web app.</span></span> <span data-ttu-id="86a7b-132">Or you can change or add a dummy application setting to force a refresh of your container.</span><span class="sxs-lookup"><span data-stu-id="86a7b-132">Or you can change or add a dummy application setting to force a refresh of your container.</span></span> <span data-ttu-id="86a7b-133">We're planning to have a continuous integration/deployment feature for custom containers in a future release.</span><span class="sxs-lookup"><span data-stu-id="86a7b-133">We're planning to have a continuous integration/deployment feature for custom containers in a future release.</span></span>

## <a name="language-support"></a><span data-ttu-id="86a7b-134">Language support</span><span class="sxs-lookup"><span data-stu-id="86a7b-134">Language support</span></span>

<span data-ttu-id="86a7b-135">**Q:** Do you support uncompiled .NET Core apps?</span><span class="sxs-lookup"><span data-stu-id="86a7b-135">**Q:** Do you support uncompiled .NET Core apps?</span></span>

<span data-ttu-id="86a7b-136">**A:** No.</span><span class="sxs-lookup"><span data-stu-id="86a7b-136">**A:** No.</span></span> <span data-ttu-id="86a7b-137">You need to deploy compiled .NET Core apps with all the dependencies.</span><span class="sxs-lookup"><span data-stu-id="86a7b-137">You need to deploy compiled .NET Core apps with all the dependencies.</span></span> <span data-ttu-id="86a7b-138">We're planning a full deployment and build experience in a future release.</span><span class="sxs-lookup"><span data-stu-id="86a7b-138">We're planning a full deployment and build experience in a future release.</span></span>

<span data-ttu-id="86a7b-139">**Q:** Do you support Composer as a dependency manager for PHP apps?</span><span class="sxs-lookup"><span data-stu-id="86a7b-139">**Q:** Do you support Composer as a dependency manager for PHP apps?</span></span>

<span data-ttu-id="86a7b-140">**A:** No.</span><span class="sxs-lookup"><span data-stu-id="86a7b-140">**A:** No.</span></span> <span data-ttu-id="86a7b-141">You need to deploy your PHP apps with all the dependencies.</span><span class="sxs-lookup"><span data-stu-id="86a7b-141">You need to deploy your PHP apps with all the dependencies.</span></span> <span data-ttu-id="86a7b-142">We're planning a full deployment experience in a future release.</span><span class="sxs-lookup"><span data-stu-id="86a7b-142">We're planning a full deployment experience in a future release.</span></span>

## <a name="custom-containers"></a><span data-ttu-id="86a7b-143">Custom containers</span><span class="sxs-lookup"><span data-stu-id="86a7b-143">Custom containers</span></span>

<span data-ttu-id="86a7b-144">**Q:** I'm using my own custom container.</span><span class="sxs-lookup"><span data-stu-id="86a7b-144">**Q:** I'm using my own custom container.</span></span> <span data-ttu-id="86a7b-145">My app resides in the \home\ directory, but I can't find my files when I browse the content by using the [SCM site](https://github.com/projectkudu/kudu) or an FTP client.</span><span class="sxs-lookup"><span data-stu-id="86a7b-145">My app resides in the \home\ directory, but I can't find my files when I browse the content by using the [SCM site](https://github.com/projectkudu/kudu) or an FTP client.</span></span> <span data-ttu-id="86a7b-146">Where are my files?</span><span class="sxs-lookup"><span data-stu-id="86a7b-146">Where are my files?</span></span>

<span data-ttu-id="86a7b-147">**A:** We mount an SMB share to the \home\ directory.</span><span class="sxs-lookup"><span data-stu-id="86a7b-147">**A:** We mount an SMB share to the \home\ directory.</span></span> <span data-ttu-id="86a7b-148">This overrides any content that's there.</span><span class="sxs-lookup"><span data-stu-id="86a7b-148">This overrides any content that's there.</span></span>

<span data-ttu-id="86a7b-149">**Q:** I want to expose more than one port on my custom container image.</span><span class="sxs-lookup"><span data-stu-id="86a7b-149">**Q:** I want to expose more than one port on my custom container image.</span></span> <span data-ttu-id="86a7b-150">Is that possible?</span><span class="sxs-lookup"><span data-stu-id="86a7b-150">Is that possible?</span></span>

<span data-ttu-id="86a7b-151">**A:** Currently, that isn't supported.</span><span class="sxs-lookup"><span data-stu-id="86a7b-151">**A:** Currently, that isn't supported.</span></span>

<span data-ttu-id="86a7b-152">**Q:** Can I bring my own storage?</span><span class="sxs-lookup"><span data-stu-id="86a7b-152">**Q:** Can I bring my own storage?</span></span>

<span data-ttu-id="86a7b-153">**A:** Currently that isn't supported.</span><span class="sxs-lookup"><span data-stu-id="86a7b-153">**A:** Currently that isn't supported.</span></span>

<span data-ttu-id="86a7b-154">**Q:** I can't browse my custom container's file system or running processes from the SCM site.</span><span class="sxs-lookup"><span data-stu-id="86a7b-154">**Q:** I can't browse my custom container's file system or running processes from the SCM site.</span></span> <span data-ttu-id="86a7b-155">Why is that?</span><span class="sxs-lookup"><span data-stu-id="86a7b-155">Why is that?</span></span>

<span data-ttu-id="86a7b-156">**A:** The SCM site runs in a separate container.</span><span class="sxs-lookup"><span data-stu-id="86a7b-156">**A:** The SCM site runs in a separate container.</span></span> <span data-ttu-id="86a7b-157">You can't check the file system or running processes of the app container.</span><span class="sxs-lookup"><span data-stu-id="86a7b-157">You can't check the file system or running processes of the app container.</span></span>

<span data-ttu-id="86a7b-158">**Q:** My custom container listens to a port other than port 80.</span><span class="sxs-lookup"><span data-stu-id="86a7b-158">**Q:** My custom container listens to a port other than port 80.</span></span> <span data-ttu-id="86a7b-159">How can I configure my app to route the requests to that port?</span><span class="sxs-lookup"><span data-stu-id="86a7b-159">How can I configure my app to route the requests to that port?</span></span>

<span data-ttu-id="86a7b-160">**A:** You can specify an application setting called **PORT**, and give it the value of the expected port number.</span><span class="sxs-lookup"><span data-stu-id="86a7b-160">**A:** You can specify an application setting called **PORT**, and give it the value of the expected port number.</span></span>

## <a name="pricing-and-sla"></a><span data-ttu-id="86a7b-161">Pricing and SLA</span><span class="sxs-lookup"><span data-stu-id="86a7b-161">Pricing and SLA</span></span>

<span data-ttu-id="86a7b-162">**Q:** What's the pricing while you're using the public preview?</span><span class="sxs-lookup"><span data-stu-id="86a7b-162">**Q:** What's the pricing while you're using the public preview?</span></span>

<span data-ttu-id="86a7b-163">**A:** You'll be charged half the number of hours that your app runs, with the normal Azure App Service pricing.</span><span class="sxs-lookup"><span data-stu-id="86a7b-163">**A:** You'll be charged half the number of hours that your app runs, with the normal Azure App Service pricing.</span></span> <span data-ttu-id="86a7b-164">This means that you get a 50 percent discount on normal Azure App Service pricing.</span><span class="sxs-lookup"><span data-stu-id="86a7b-164">This means that you get a 50 percent discount on normal Azure App Service pricing.</span></span>

## <a name="other"></a><span data-ttu-id="86a7b-165">Other</span><span class="sxs-lookup"><span data-stu-id="86a7b-165">Other</span></span>

<span data-ttu-id="86a7b-166">**Q:** What are the supported characters in application settings names?</span><span class="sxs-lookup"><span data-stu-id="86a7b-166">**Q:** What are the supported characters in application settings names?</span></span>

<span data-ttu-id="86a7b-167">**A:** You can only use A-Z, a-z, 0-9, and the underscore for application settings.</span><span class="sxs-lookup"><span data-stu-id="86a7b-167">**A:** You can only use A-Z, a-z, 0-9, and the underscore for application settings.</span></span>

<span data-ttu-id="86a7b-168">**Q:** Where can I request new features?</span><span class="sxs-lookup"><span data-stu-id="86a7b-168">**Q:** Where can I request new features?</span></span>

<span data-ttu-id="86a7b-169">**A:** You can submit your idea at the [Web Apps feedback forum](https://aka.ms/webapps-uservoice).</span><span class="sxs-lookup"><span data-stu-id="86a7b-169">**A:** You can submit your idea at the [Web Apps feedback forum](https://aka.ms/webapps-uservoice).</span></span> <span data-ttu-id="86a7b-170">Please add "[Linux]" to the title of your idea.</span><span class="sxs-lookup"><span data-stu-id="86a7b-170">Please add "[Linux]" to the title of your idea.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86a7b-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="86a7b-171">Next steps</span></span>
* [<span data-ttu-id="86a7b-172">What is App Service on Linux?</span><span class="sxs-lookup"><span data-stu-id="86a7b-172">What is App Service on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="86a7b-173">Creating web apps in App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="86a7b-173">Creating web apps in App Service on Linux</span></span>](app-service-linux-how-to-create-a-web-app.md)
