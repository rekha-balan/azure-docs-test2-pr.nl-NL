---
title: Configure Azure Function App Settings | Microsoft Docs
description: Learn how to configure Azure function app settings.
services: ''
documentationcenter: .net
author: rachelappel
manager: erikre
editor: ''
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: rachelap
ms.openlocfilehash: a54d298132d47e9ecf83e9e263a92d088ffc2e9d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553390"
---
# <a name="how-to-configure-azure-function-app-settings"></a><span data-ttu-id="6551e-103">How to configure Azure Function app settings</span><span class="sxs-lookup"><span data-stu-id="6551e-103">How to configure Azure Function app settings</span></span>
## <a name="settings-overview"></a><span data-ttu-id="6551e-104">Settings overview</span><span class="sxs-lookup"><span data-stu-id="6551e-104">Settings overview</span></span>
<span data-ttu-id="6551e-105">You can manage Azure Function Apps settings by clicking the **Function App Settings** link in the bottom-left corner of the portal.</span><span class="sxs-lookup"><span data-stu-id="6551e-105">You can manage Azure Function Apps settings by clicking the **Function App Settings** link in the bottom-left corner of the portal.</span></span> <span data-ttu-id="6551e-106">Azure function app settings apply to all functions in the app.</span><span class="sxs-lookup"><span data-stu-id="6551e-106">Azure function app settings apply to all functions in the app.</span></span>

1. <span data-ttu-id="6551e-107">Go to the [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="6551e-107">Go to the [Azure portal](http://portal.azure.com) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="6551e-108">Click **Function App Settings** in the bottom-left corner of the portal.</span><span class="sxs-lookup"><span data-stu-id="6551e-108">Click **Function App Settings** in the bottom-left corner of the portal.</span></span> <span data-ttu-id="6551e-109">This action reveals several configuration options to choose from.</span><span class="sxs-lookup"><span data-stu-id="6551e-109">This action reveals several configuration options to choose from.</span></span> 

![Azure Function App settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <a name="develop"></a><span data-ttu-id="6551e-111">Develop</span><span class="sxs-lookup"><span data-stu-id="6551e-111">Develop</span></span>
### <a name="app-service-editor"></a><span data-ttu-id="6551e-112">App Service Editor</span><span class="sxs-lookup"><span data-stu-id="6551e-112">App Service Editor</span></span>
<span data-ttu-id="6551e-113">The App Service Editor is an advanced in-portal editor that you can use to modify Json configuration files and code files alike.</span><span class="sxs-lookup"><span data-stu-id="6551e-113">The App Service Editor is an advanced in-portal editor that you can use to modify Json configuration files and code files alike.</span></span> <span data-ttu-id="6551e-114">Choosing this option launches a separate browser tab with a basic editor.</span><span class="sxs-lookup"><span data-stu-id="6551e-114">Choosing this option launches a separate browser tab with a basic editor.</span></span> <span data-ttu-id="6551e-115">This enables you to integrate with GitHub, run and debug code, and modify function app settings.</span><span class="sxs-lookup"><span data-stu-id="6551e-115">This enables you to integrate with GitHub, run and debug code, and modify function app settings.</span></span>

![The App Service Editor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <a name="application-settings"></a><span data-ttu-id="6551e-117">Application settings</span><span class="sxs-lookup"><span data-stu-id="6551e-117">Application settings</span></span>
<span data-ttu-id="6551e-118">Manage environment variables, Framework versions, remote debugging, app settings, connection strings, default docs, etc. These settings are specific to your Function App.</span><span class="sxs-lookup"><span data-stu-id="6551e-118">Manage environment variables, Framework versions, remote debugging, app settings, connection strings, default docs, etc. These settings are specific to your Function App.</span></span> 

<span data-ttu-id="6551e-119">To configure app settings, click the **Configure App Settings** link.</span><span class="sxs-lookup"><span data-stu-id="6551e-119">To configure app settings, click the **Configure App Settings** link.</span></span> 

![Configure App Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <a name="dev-console"></a><span data-ttu-id="6551e-121">Dev console</span><span class="sxs-lookup"><span data-stu-id="6551e-121">Dev console</span></span>
<span data-ttu-id="6551e-122">You can execute DOS style commands with the Azure functions in-portal console.</span><span class="sxs-lookup"><span data-stu-id="6551e-122">You can execute DOS style commands with the Azure functions in-portal console.</span></span> <span data-ttu-id="6551e-123">Common commands include directory and file creation and navigation, as well as executing batch files and scripts.</span><span class="sxs-lookup"><span data-stu-id="6551e-123">Common commands include directory and file creation and navigation, as well as executing batch files and scripts.</span></span> 

> [!NOTE]
> <span data-ttu-id="6551e-124">You can upload scripts, but first you must configure an FTP client in the Azure Function's **Advanced Settings**.</span><span class="sxs-lookup"><span data-stu-id="6551e-124">You can upload scripts, but first you must configure an FTP client in the Azure Function's **Advanced Settings**.</span></span>
> 
> 

<span data-ttu-id="6551e-125">To open the In-portal console, click **Open dev console**.</span><span class="sxs-lookup"><span data-stu-id="6551e-125">To open the In-portal console, click **Open dev console**.</span></span>

![Configure function app memory size](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

> [!NOTE]
> <span data-ttu-id="6551e-127">Working in a console with ASCII art like that makes you look cool.</span><span class="sxs-lookup"><span data-stu-id="6551e-127">Working in a console with ASCII art like that makes you look cool.</span></span>
> 
> 

## <a name="deploy"></a><span data-ttu-id="6551e-128">Deploy</span><span class="sxs-lookup"><span data-stu-id="6551e-128">Deploy</span></span>
### <a name="continuous-integration"></a><span data-ttu-id="6551e-129">Continuous integration</span><span class="sxs-lookup"><span data-stu-id="6551e-129">Continuous integration</span></span>
<span data-ttu-id="6551e-130">You can integrate your Function App with GitHub, Visual Studio Team Services, and more.</span><span class="sxs-lookup"><span data-stu-id="6551e-130">You can integrate your Function App with GitHub, Visual Studio Team Services, and more.</span></span>

1. <span data-ttu-id="6551e-131">Click the  **Configure continuous integration** link.</span><span class="sxs-lookup"><span data-stu-id="6551e-131">Click the  **Configure continuous integration** link.</span></span> <span data-ttu-id="6551e-132">This  opens a **Deployments** pane with options.</span><span class="sxs-lookup"><span data-stu-id="6551e-132">This  opens a **Deployments** pane with options.</span></span>
2. <span data-ttu-id="6551e-133">Click **Setup** in the **Deployments** pane to reveal a **Deployment Source** pane with one option: Click **Choose Source** to show available sources.</span><span class="sxs-lookup"><span data-stu-id="6551e-133">Click **Setup** in the **Deployments** pane to reveal a **Deployment Source** pane with one option: Click **Choose Source** to show available sources.</span></span> 
3. <span data-ttu-id="6551e-134">Choose any of the deployment sources available: Visual Studio Team Services, OneDrive, Local Git Repository, GitHub, Bitbucket, DropBox, or an External Repository by clicking it.</span><span class="sxs-lookup"><span data-stu-id="6551e-134">Choose any of the deployment sources available: Visual Studio Team Services, OneDrive, Local Git Repository, GitHub, Bitbucket, DropBox, or an External Repository by clicking it.</span></span> 
   
    ![Configure Function App's CI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/configure-function-ci.png)
4. <span data-ttu-id="6551e-136">Enter your credentials and information as prompted by the various deployment sources.</span><span class="sxs-lookup"><span data-stu-id="6551e-136">Enter your credentials and information as prompted by the various deployment sources.</span></span> <span data-ttu-id="6551e-137">The credentials and information requested may be slightly different depending on what source you have chosen.</span><span class="sxs-lookup"><span data-stu-id="6551e-137">The credentials and information requested may be slightly different depending on what source you have chosen.</span></span> 

<span data-ttu-id="6551e-138">Once you have setup CI, connected code you push to the configured source is automatically deployed to this function app.</span><span class="sxs-lookup"><span data-stu-id="6551e-138">Once you have setup CI, connected code you push to the configured source is automatically deployed to this function app.</span></span>

### <a name="kudu"></a><span data-ttu-id="6551e-139">Kudu</span><span class="sxs-lookup"><span data-stu-id="6551e-139">Kudu</span></span>
<span data-ttu-id="6551e-140">Kudu allows you to access advanced administrative features of a Function App.</span><span class="sxs-lookup"><span data-stu-id="6551e-140">Kudu allows you to access advanced administrative features of a Function App.</span></span>

<span data-ttu-id="6551e-141">To open Kudu, click **Go to Kudu**.</span><span class="sxs-lookup"><span data-stu-id="6551e-141">To open Kudu, click **Go to Kudu**.</span></span> <span data-ttu-id="6551e-142">This action opens an entirely new browser window with the Kudu web admin.</span><span class="sxs-lookup"><span data-stu-id="6551e-142">This action opens an entirely new browser window with the Kudu web admin.</span></span>

> [!NOTE]
> <span data-ttu-id="6551e-143">You can alternatively launch **Kudu** by inserting "scm" into your function's URL, as shown here: ```https://<YourFunctionName>.scm.azurewebsites.net/```</span><span class="sxs-lookup"><span data-stu-id="6551e-143">You can alternatively launch **Kudu** by inserting "scm" into your function's URL, as shown here: ```https://<YourFunctionName>.scm.azurewebsites.net/```</span></span>
> 
> 

<span data-ttu-id="6551e-144">From the Kudu webpage, you can view and manage system information, app settings, environment variables, HTTP headers, server variables, and more.</span><span class="sxs-lookup"><span data-stu-id="6551e-144">From the Kudu webpage, you can view and manage system information, app settings, environment variables, HTTP headers, server variables, and more.</span></span>

![Configure Kudu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)

## <a name="manage-app-service-settings"></a><span data-ttu-id="6551e-146">Manage: App Service settings</span><span class="sxs-lookup"><span data-stu-id="6551e-146">Manage: App Service settings</span></span>
<span data-ttu-id="6551e-147">Manage your function app like any other App Service instance.</span><span class="sxs-lookup"><span data-stu-id="6551e-147">Manage your function app like any other App Service instance.</span></span> <span data-ttu-id="6551e-148">This option gives you access to all the previously discussed settings, plus several more.</span><span class="sxs-lookup"><span data-stu-id="6551e-148">This option gives you access to all the previously discussed settings, plus several more.</span></span>  

<span data-ttu-id="6551e-149">To open advanced settings, click the **Advanced Settings** link.</span><span class="sxs-lookup"><span data-stu-id="6551e-149">To open advanced settings, click the **Advanced Settings** link.</span></span> 

![Configure App Service Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-settings.png)

<span data-ttu-id="6551e-151">For details on how to configure each App Service setting, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="6551e-151">For details on how to configure each App Service setting, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).</span></span>

## <a name="manage-cors"></a><span data-ttu-id="6551e-152">Manage: CORS</span><span class="sxs-lookup"><span data-stu-id="6551e-152">Manage: CORS</span></span>
<span data-ttu-id="6551e-153">Normally, for security reasons, calls to your hosts (domains) from external sources, such as Ajax calls from a browser, are not allowed.</span><span class="sxs-lookup"><span data-stu-id="6551e-153">Normally, for security reasons, calls to your hosts (domains) from external sources, such as Ajax calls from a browser, are not allowed.</span></span> <span data-ttu-id="6551e-154">Otherwise, malicious code could be sent to and executed on the backend.</span><span class="sxs-lookup"><span data-stu-id="6551e-154">Otherwise, malicious code could be sent to and executed on the backend.</span></span> <span data-ttu-id="6551e-155">The safest route then is to blacklist all sources of code, except for a few of your own trusted ones.</span><span class="sxs-lookup"><span data-stu-id="6551e-155">The safest route then is to blacklist all sources of code, except for a few of your own trusted ones.</span></span> <span data-ttu-id="6551e-156">You can configure which sources you accept calls from in Azure functions by configuring Cross-Origin Resource Sharing (CORS).</span><span class="sxs-lookup"><span data-stu-id="6551e-156">You can configure which sources you accept calls from in Azure functions by configuring Cross-Origin Resource Sharing (CORS).</span></span> <span data-ttu-id="6551e-157">CORS allows you to list domains that are the source of JavaScript that can call functions in your Azure Function App.</span><span class="sxs-lookup"><span data-stu-id="6551e-157">CORS allows you to list domains that are the source of JavaScript that can call functions in your Azure Function App.</span></span> 

1. <span data-ttu-id="6551e-158">To configure CORS, click the **Configure CORS** link.</span><span class="sxs-lookup"><span data-stu-id="6551e-158">To configure CORS, click the **Configure CORS** link.</span></span> 
2. <span data-ttu-id="6551e-159">Enter the domains that you want to whitelist.</span><span class="sxs-lookup"><span data-stu-id="6551e-159">Enter the domains that you want to whitelist.</span></span>

![Configure Function App's CORS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

## <a name="manage-authenticationauthorization"></a><span data-ttu-id="6551e-161">Manage: Authentication/authorization</span><span class="sxs-lookup"><span data-stu-id="6551e-161">Manage: Authentication/authorization</span></span>
<span data-ttu-id="6551e-162">For functions that use an HTTP trigger, you can require calls to be authenticated.</span><span class="sxs-lookup"><span data-stu-id="6551e-162">For functions that use an HTTP trigger, you can require calls to be authenticated.</span></span>

1. <span data-ttu-id="6551e-163">To configure authentication click the **Configure authentication** link.</span><span class="sxs-lookup"><span data-stu-id="6551e-163">To configure authentication click the **Configure authentication** link.</span></span>
2. <span data-ttu-id="6551e-164">Toggle the **App Service Authentication** button to **On**.</span><span class="sxs-lookup"><span data-stu-id="6551e-164">Toggle the **App Service Authentication** button to **On**.</span></span>

![Configure Function App's CI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)

<span data-ttu-id="6551e-166">Most authentication providers ask for an API Key/Client ID and a Secret; however, both the Microsoft Account and Facebook options also allow you to define scopes (specific authorization credentials).</span><span class="sxs-lookup"><span data-stu-id="6551e-166">Most authentication providers ask for an API Key/Client ID and a Secret; however, both the Microsoft Account and Facebook options also allow you to define scopes (specific authorization credentials).</span></span> <span data-ttu-id="6551e-167">Active Directory has several express or advanced configuration settings you can set.</span><span class="sxs-lookup"><span data-stu-id="6551e-167">Active Directory has several express or advanced configuration settings you can set.</span></span>

<span data-ttu-id="6551e-168">For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6551e-168">For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span>

## <a name="manage-api-definition"></a><span data-ttu-id="6551e-169">Manage: API definition</span><span class="sxs-lookup"><span data-stu-id="6551e-169">Manage: API definition</span></span>
<span data-ttu-id="6551e-170">Allow clients to more easily consume your HTTP-triggered functions.</span><span class="sxs-lookup"><span data-stu-id="6551e-170">Allow clients to more easily consume your HTTP-triggered functions.</span></span>

1. <span data-ttu-id="6551e-171">To set up an API, click **Configure API metadata**.</span><span class="sxs-lookup"><span data-stu-id="6551e-171">To set up an API, click **Configure API metadata**.</span></span> 
2. <span data-ttu-id="6551e-172">Enter the URL that points to a Swagger json file.</span><span class="sxs-lookup"><span data-stu-id="6551e-172">Enter the URL that points to a Swagger json file.</span></span>

![Configure Function App's API](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)

<span data-ttu-id="6551e-174">For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6551e-174">For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span></span>

## <a name="daily-usage-quota"></a><span data-ttu-id="6551e-175">Daily Usage Quota</span><span class="sxs-lookup"><span data-stu-id="6551e-175">Daily Usage Quota</span></span>

<span data-ttu-id="6551e-176">Azure Functions enables you to predictably limit platform usage by setting a daily spending quota.</span><span class="sxs-lookup"><span data-stu-id="6551e-176">Azure Functions enables you to predictably limit platform usage by setting a daily spending quota.</span></span> <span data-ttu-id="6551e-177">Once the daily spending quota is reached the Function App is stopped.</span><span class="sxs-lookup"><span data-stu-id="6551e-177">Once the daily spending quota is reached the Function App is stopped.</span></span> <span data-ttu-id="6551e-178">A Function App stopped as a result of reaching the spending quota can be re-enabled from the same context as establishing the daily spending quota.</span><span class="sxs-lookup"><span data-stu-id="6551e-178">A Function App stopped as a result of reaching the spending quota can be re-enabled from the same context as establishing the daily spending quota.</span></span> <span data-ttu-id="6551e-179">The unit of the spending quota is the unit of billing: GB-s (gigabyte-seconds), please refer to the [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on the billing model.</span><span class="sxs-lookup"><span data-stu-id="6551e-179">The unit of the spending quota is the unit of billing: GB-s (gigabyte-seconds), please refer to the [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on the billing model.</span></span> 

![Configure function app memory size](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-how-to-use-azure-function-app-settings/configure-function-app-quota.png)

## <a name="next-steps"></a><span data-ttu-id="6551e-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="6551e-181">Next steps</span></span>
[!INCLUDE [Getting Started Note](../../includes/functions-get-help.md)]












