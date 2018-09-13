---
title: Deploy your app to Azure App Service using FTP/S | Microsoft Docs
description: Learn how to deploy your app to Azure App Service using FTP or FTPS.
services: app-service
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2018
ms.author: cephalin;dariac
ms.openlocfilehash: 66d375022d200cc916c77c059fa64eb6dbbc17e2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869599"
---
# <a name="deploy-your-app-to-azure-app-service-using-ftps"></a><span data-ttu-id="1369d-103">Deploy your app to Azure App Service using FTP/S</span><span class="sxs-lookup"><span data-stu-id="1369d-103">Deploy your app to Azure App Service using FTP/S</span></span>

<span data-ttu-id="1369d-104">This article shows you how to use FTP or FTPS to deploy your web app, mobile app backend, or API app to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="1369d-104">This article shows you how to use FTP or FTPS to deploy your web app, mobile app backend, or API app to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="1369d-105">The FTP/S endpoint for your app is already active.</span><span class="sxs-lookup"><span data-stu-id="1369d-105">The FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="1369d-106">No configuration is necessary to enable FTP/S deployment.</span><span class="sxs-lookup"><span data-stu-id="1369d-106">No configuration is necessary to enable FTP/S deployment.</span></span>

## <a name="open-ftp-dashboard"></a><span data-ttu-id="1369d-107">Open FTP dashboard</span><span class="sxs-lookup"><span data-stu-id="1369d-107">Open FTP dashboard</span></span>

<span data-ttu-id="1369d-108">In the [Azure portal](https://portal.azure.com), open your app's [resource page](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="1369d-108">In the [Azure portal](https://portal.azure.com), open your app's [resource page](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>

<span data-ttu-id="1369d-109">To open the FTP dashboard, click **Continuous Delivery (Preview)** > **FTP** > **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="1369d-109">To open the FTP dashboard, click **Continuous Delivery (Preview)** > **FTP** > **Dashboard**.</span></span>

![Open FTP dashboard](./media/app-service-deploy-ftp/open-dashboard.png)

## <a name="get-ftp-connection-information"></a><span data-ttu-id="1369d-111">Get FTP connection information</span><span class="sxs-lookup"><span data-stu-id="1369d-111">Get FTP connection information</span></span>

<span data-ttu-id="1369d-112">In the FTP dashboard, click **Copy** to copy the FTPS endpoint and app credentials.</span><span class="sxs-lookup"><span data-stu-id="1369d-112">In the FTP dashboard, click **Copy** to copy the FTPS endpoint and app credentials.</span></span>

![Copy FTP information](./media/app-service-deploy-ftp/ftp-dashboard.png)

<span data-ttu-id="1369d-114">It's recommended that you use **App Credentials** to deploy to your app because it's unique to each app.</span><span class="sxs-lookup"><span data-stu-id="1369d-114">It's recommended that you use **App Credentials** to deploy to your app because it's unique to each app.</span></span> <span data-ttu-id="1369d-115">However, if you click **User Credentials**, you can set user-level credentials that you can use for FTP/S login to all App Service apps in your subscription.</span><span class="sxs-lookup"><span data-stu-id="1369d-115">However, if you click **User Credentials**, you can set user-level credentials that you can use for FTP/S login to all App Service apps in your subscription.</span></span>

## <a name="deploy-files-to-azure"></a><span data-ttu-id="1369d-116">Deploy files to Azure</span><span class="sxs-lookup"><span data-stu-id="1369d-116">Deploy files to Azure</span></span>

1. <span data-ttu-id="1369d-117">From your FTP client (for example, [Visual Studio](https://www.visualstudio.com/vs/community/) or [FileZilla](https://filezilla-project.org/download.php?type=client)), use the connection information you gathered to connect to your app.</span><span class="sxs-lookup"><span data-stu-id="1369d-117">From your FTP client (for example, [Visual Studio](https://www.visualstudio.com/vs/community/) or [FileZilla](https://filezilla-project.org/download.php?type=client)), use the connection information you gathered to connect to your app.</span></span>
3. <span data-ttu-id="1369d-118">Copy your files and their respective directory structure to the [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or the **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span><span class="sxs-lookup"><span data-stu-id="1369d-118">Copy your files and their respective directory structure to the [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or the **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="1369d-119">Browse to your app's URL to verify the app is running properly.</span><span class="sxs-lookup"><span data-stu-id="1369d-119">Browse to your app's URL to verify the app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="1369d-120">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support the following deployment automations:</span><span class="sxs-lookup"><span data-stu-id="1369d-120">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support the following deployment automations:</span></span> 
>
> - <span data-ttu-id="1369d-121">dependency restores (such as NuGet, NPM, PIP, and Composer automations)</span><span class="sxs-lookup"><span data-stu-id="1369d-121">dependency restores (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="1369d-122">compilation of .NET binaries</span><span class="sxs-lookup"><span data-stu-id="1369d-122">compilation of .NET binaries</span></span>
> - <span data-ttu-id="1369d-123">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span><span class="sxs-lookup"><span data-stu-id="1369d-123">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="1369d-124">Generate these necessary files manually on your local machine, and then deploy them together with your app.</span><span class="sxs-lookup"><span data-stu-id="1369d-124">Generate these necessary files manually on your local machine, and then deploy them together with your app.</span></span>
>
>

## <a name="enforce-ftps"></a><span data-ttu-id="1369d-125">Enforce FTPS</span><span class="sxs-lookup"><span data-stu-id="1369d-125">Enforce FTPS</span></span>

<span data-ttu-id="1369d-126">For enhanced security, you should allow FTP over SSL only.</span><span class="sxs-lookup"><span data-stu-id="1369d-126">For enhanced security, you should allow FTP over SSL only.</span></span> <span data-ttu-id="1369d-127">You can also disable both FTP and FTPS if you don't use FTP deployment.</span><span class="sxs-lookup"><span data-stu-id="1369d-127">You can also disable both FTP and FTPS if you don't use FTP deployment.</span></span>

<span data-ttu-id="1369d-128">In your app's resource page in [Azure portal](https://portal.azure.com), select **App settings** in the left navigation.</span><span class="sxs-lookup"><span data-stu-id="1369d-128">In your app's resource page in [Azure portal](https://portal.azure.com), select **App settings** in the left navigation.</span></span>

<span data-ttu-id="1369d-129">To disable unencrypted FTP, select **FTPS Only**.</span><span class="sxs-lookup"><span data-stu-id="1369d-129">To disable unencrypted FTP, select **FTPS Only**.</span></span> <span data-ttu-id="1369d-130">To disable both FTP and FTPS entirely, select **Disable**.</span><span class="sxs-lookup"><span data-stu-id="1369d-130">To disable both FTP and FTPS entirely, select **Disable**.</span></span> <span data-ttu-id="1369d-131">When finished, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1369d-131">When finished, click **Save**.</span></span> <span data-ttu-id="1369d-132">If using **FTPS Only** you must enforce TLS 1.1 or higher by navigating to the **SSL settings** blade of your web app.</span><span class="sxs-lookup"><span data-stu-id="1369d-132">If using **FTPS Only** you must enforce TLS 1.1 or higher by navigating to the **SSL settings** blade of your web app.</span></span> <span data-ttu-id="1369d-133">TLS 1.0 is not supported with **FTPS Only**.</span><span class="sxs-lookup"><span data-stu-id="1369d-133">TLS 1.0 is not supported with **FTPS Only**.</span></span>

![Disable FTP/S](./media/app-service-deploy-ftp/disable-ftp.png)

## <a name="automate-with-scripts"></a><span data-ttu-id="1369d-135">Automate with scripts</span><span class="sxs-lookup"><span data-stu-id="1369d-135">Automate with scripts</span></span>

<span data-ttu-id="1369d-136">For FTP deployment using [Azure CLI](/cli/azure), see [Create a web app and deploy files with FTP (Azure CLI)](./scripts/app-service-cli-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="1369d-136">For FTP deployment using [Azure CLI](/cli/azure), see [Create a web app and deploy files with FTP (Azure CLI)](./scripts/app-service-cli-deploy-ftp.md).</span></span>

<span data-ttu-id="1369d-137">For FTP deployment using [Azure PowerShell](/cli/azure), see [Upload files to a web app using FTP (PowerShell)](./scripts/app-service-powershell-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="1369d-137">For FTP deployment using [Azure PowerShell](/cli/azure), see [Upload files to a web app using FTP (PowerShell)](./scripts/app-service-powershell-deploy-ftp.md).</span></span>

[!INCLUDE [What happens to my app during deployment?](../../includes/app-service-deploy-atomicity.md)]

## <a name="troubleshoot-ftp-deployment"></a><span data-ttu-id="1369d-138">Troubleshoot FTP deployment</span><span class="sxs-lookup"><span data-stu-id="1369d-138">Troubleshoot FTP deployment</span></span>

- [<span data-ttu-id="1369d-139">How can I troubleshoot FTP deployment?</span><span class="sxs-lookup"><span data-stu-id="1369d-139">How can I troubleshoot FTP deployment?</span></span>](#how-can-i-troubleshoot-ftp-deployment)
- [<span data-ttu-id="1369d-140">I'm not able to FTP and publish my code. How can I resolve the issue?</span><span class="sxs-lookup"><span data-stu-id="1369d-140">I'm not able to FTP and publish my code. How can I resolve the issue?</span></span>](#im-not-able-to-ftp-and-publish-my-code-how-can-i-resolve-the-issue)
- [<span data-ttu-id="1369d-141">How can I connect to FTP in Azure App Service via passive mode?</span><span class="sxs-lookup"><span data-stu-id="1369d-141">How can I connect to FTP in Azure App Service via passive mode?</span></span>](#how-can-i-connect-to-ftp-in-azure-app-service-via-passive-mode)

### <a name="how-can-i-troubleshoot-ftp-deployment"></a><span data-ttu-id="1369d-142">How can I troubleshoot FTP deployment?</span><span class="sxs-lookup"><span data-stu-id="1369d-142">How can I troubleshoot FTP deployment?</span></span>

<span data-ttu-id="1369d-143">The first step for troubleshooting FTP deployment is isolating a deployment issue from a runtime application issue.</span><span class="sxs-lookup"><span data-stu-id="1369d-143">The first step for troubleshooting FTP deployment is isolating a deployment issue from a runtime application issue.</span></span>

<span data-ttu-id="1369d-144">A deployment issue typically results in no files or wrong files deployed to your app.</span><span class="sxs-lookup"><span data-stu-id="1369d-144">A deployment issue typically results in no files or wrong files deployed to your app.</span></span> <span data-ttu-id="1369d-145">You can troubleshoot by investigating your FTP deployment or selecting an alternate deployment path (such as source control).</span><span class="sxs-lookup"><span data-stu-id="1369d-145">You can troubleshoot by investigating your FTP deployment or selecting an alternate deployment path (such as source control).</span></span>

<span data-ttu-id="1369d-146">A runtime application issue typically results in the right set of files deployed to your app but incorrect app behavior.</span><span class="sxs-lookup"><span data-stu-id="1369d-146">A runtime application issue typically results in the right set of files deployed to your app but incorrect app behavior.</span></span> <span data-ttu-id="1369d-147">You can troubleshoot by focusing on code behavior at runtime and investigating specific failure paths.</span><span class="sxs-lookup"><span data-stu-id="1369d-147">You can troubleshoot by focusing on code behavior at runtime and investigating specific failure paths.</span></span>

<span data-ttu-id="1369d-148">To determine a deployment or runtime issue, see [Deployment vs. runtime issues](https://github.com/projectkudu/kudu/wiki/Deployment-vs-runtime-issues).</span><span class="sxs-lookup"><span data-stu-id="1369d-148">To determine a deployment or runtime issue, see [Deployment vs. runtime issues](https://github.com/projectkudu/kudu/wiki/Deployment-vs-runtime-issues).</span></span>

### <a name="im-not-able-to-ftp-and-publish-my-code-how-can-i-resolve-the-issue"></a><span data-ttu-id="1369d-149">I'm not able to FTP and publish my code.</span><span class="sxs-lookup"><span data-stu-id="1369d-149">I'm not able to FTP and publish my code.</span></span> <span data-ttu-id="1369d-150">How can I resolve the issue?</span><span class="sxs-lookup"><span data-stu-id="1369d-150">How can I resolve the issue?</span></span>
<span data-ttu-id="1369d-151">Check that you've entered the correct hostname and [credentials](#step-1--set-deployment-credentials).</span><span class="sxs-lookup"><span data-stu-id="1369d-151">Check that you've entered the correct hostname and [credentials](#step-1--set-deployment-credentials).</span></span> <span data-ttu-id="1369d-152">Check also that the following FTP ports on your machine are not blocked by a firewall:</span><span class="sxs-lookup"><span data-stu-id="1369d-152">Check also that the following FTP ports on your machine are not blocked by a firewall:</span></span>

- <span data-ttu-id="1369d-153">FTP control connection port: 21</span><span class="sxs-lookup"><span data-stu-id="1369d-153">FTP control connection port: 21</span></span>
- <span data-ttu-id="1369d-154">FTP data connection port: 989, 10001-10300</span><span class="sxs-lookup"><span data-stu-id="1369d-154">FTP data connection port: 989, 10001-10300</span></span>
 
### <a name="how-can-i-connect-to-ftp-in-azure-app-service-via-passive-mode"></a><span data-ttu-id="1369d-155">How can I connect to FTP in Azure App Service via passive mode?</span><span class="sxs-lookup"><span data-stu-id="1369d-155">How can I connect to FTP in Azure App Service via passive mode?</span></span>
<span data-ttu-id="1369d-156">Azure App Service supports connecting via both Active and Passive mode.</span><span class="sxs-lookup"><span data-stu-id="1369d-156">Azure App Service supports connecting via both Active and Passive mode.</span></span> <span data-ttu-id="1369d-157">Passive mode is preferred because your deployment machines are usually behind a firewall (in the operating system or as part of a home or business network).</span><span class="sxs-lookup"><span data-stu-id="1369d-157">Passive mode is preferred because your deployment machines are usually behind a firewall (in the operating system or as part of a home or business network).</span></span> <span data-ttu-id="1369d-158">See an [example from the WinSCP documentation](https://winscp.net/docs/ui_login_connection).</span><span class="sxs-lookup"><span data-stu-id="1369d-158">See an [example from the WinSCP documentation](https://winscp.net/docs/ui_login_connection).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1369d-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="1369d-159">Next steps</span></span>

<span data-ttu-id="1369d-160">For more advanced deployment scenarios, try [deploying to Azure with Git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="1369d-160">For more advanced deployment scenarios, try [deploying to Azure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="1369d-161">Git-based deployment to Azure enables version control, package restore, MSBuild, and more.</span><span class="sxs-lookup"><span data-stu-id="1369d-161">Git-based deployment to Azure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="1369d-162">More Resources</span><span class="sxs-lookup"><span data-stu-id="1369d-162">More Resources</span></span>

* [<span data-ttu-id="1369d-163">Azure App Service Deployment Credentials</span><span class="sxs-lookup"><span data-stu-id="1369d-163">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
