---
title: How to debug a Node.js web app in Azure App Service
description: Learn how to debug a Node.js web app in Azure App Service.
tags: azure-portal
services: app-service\web
documentationcenter: nodejs
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: a48f906c-1a3e-43bc-ae84-7d2dde175b15
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: 587037e30aa7a2005ebcadd30e6e4c0c54de6373
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555154"
---
# <a name="how-to-debug-a-nodejs-web-app-in-azure-app-service"></a><span data-ttu-id="67b63-103">How to debug a Node.js web app in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="67b63-103">How to debug a Node.js web app in Azure App Service</span></span>
<span data-ttu-id="67b63-104">Azure provides built-in diagnostics to assist with debugging Node.js applications hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span><span class="sxs-lookup"><span data-stu-id="67b63-104">Azure provides built-in diagnostics to assist with debugging Node.js applications hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="67b63-105">In this article, you will learn how to enable logging of stdout and stderr, display error information in the browser, and how to download and view log files.</span><span class="sxs-lookup"><span data-stu-id="67b63-105">In this article, you will learn how to enable logging of stdout and stderr, display error information in the browser, and how to download and view log files.</span></span>

<span data-ttu-id="67b63-106">Diagnostics for Node.js applications hosted on Azure is provided by [IISNode].</span><span class="sxs-lookup"><span data-stu-id="67b63-106">Diagnostics for Node.js applications hosted on Azure is provided by [IISNode].</span></span> <span data-ttu-id="67b63-107">While this article discusses the most common settings for gathering diagnostics information, it does not provide a complete reference for working with IISNode.</span><span class="sxs-lookup"><span data-stu-id="67b63-107">While this article discusses the most common settings for gathering diagnostics information, it does not provide a complete reference for working with IISNode.</span></span> <span data-ttu-id="67b63-108">For more information on working with IISNode, see the [IISNode Readme] on GitHub.</span><span class="sxs-lookup"><span data-stu-id="67b63-108">For more information on working with IISNode, see the [IISNode Readme] on GitHub.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="67b63-109">Enable logging</span><span class="sxs-lookup"><span data-stu-id="67b63-109">Enable logging</span></span>
<span data-ttu-id="67b63-110">By default, an App Service web app only captures diagnostic information about deployments, such as when you deploy a web app using Git.</span><span class="sxs-lookup"><span data-stu-id="67b63-110">By default, an App Service web app only captures diagnostic information about deployments, such as when you deploy a web app using Git.</span></span> <span data-ttu-id="67b63-111">This information is useful if you are having problems during deployment, such as a failure when installing a module referenced in **package.json**, or if you are using a custom deployment script.</span><span class="sxs-lookup"><span data-stu-id="67b63-111">This information is useful if you are having problems during deployment, such as a failure when installing a module referenced in **package.json**, or if you are using a custom deployment script.</span></span>

<span data-ttu-id="67b63-112">To enable the logging of stdout and stderr streams, you must create an **IISNode.yml** file at the root of your Node.js application and add the following:</span><span class="sxs-lookup"><span data-stu-id="67b63-112">To enable the logging of stdout and stderr streams, you must create an **IISNode.yml** file at the root of your Node.js application and add the following:</span></span>

    loggingEnabled: true

<span data-ttu-id="67b63-113">This enables the logging of stderr and stdout from your Node.js application.</span><span class="sxs-lookup"><span data-stu-id="67b63-113">This enables the logging of stderr and stdout from your Node.js application.</span></span>

<span data-ttu-id="67b63-114">The **IISNode.yml** file can also be used to control whether friendly errors or developer errors are returned to the browser when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="67b63-114">The **IISNode.yml** file can also be used to control whether friendly errors or developer errors are returned to the browser when a failure occurs.</span></span> <span data-ttu-id="67b63-115">To enable developer errors, add the following line to the **IISNode.yml** file:</span><span class="sxs-lookup"><span data-stu-id="67b63-115">To enable developer errors, add the following line to the **IISNode.yml** file:</span></span>

    devErrorsEnabled: true

<span data-ttu-id="67b63-116">Once this option is enabled, IISNode will return the last 64K of information sent to stderr instead of a friendly error such as "an internal server error occurred".</span><span class="sxs-lookup"><span data-stu-id="67b63-116">Once this option is enabled, IISNode will return the last 64K of information sent to stderr instead of a friendly error such as "an internal server error occurred".</span></span>

> [!NOTE]
> <span data-ttu-id="67b63-117">While devErrorsEnabled is useful when diagnosing problems during development, enabling it in a production environment may result in development errors being sent to end users.</span><span class="sxs-lookup"><span data-stu-id="67b63-117">While devErrorsEnabled is useful when diagnosing problems during development, enabling it in a production environment may result in development errors being sent to end users.</span></span>
> 
> 

<span data-ttu-id="67b63-118">If the **IISNode.yml** file did not already exist within your application, you must restart your web app after publishing the updated application.</span><span class="sxs-lookup"><span data-stu-id="67b63-118">If the **IISNode.yml** file did not already exist within your application, you must restart your web app after publishing the updated application.</span></span> <span data-ttu-id="67b63-119">If you are simply changing settings in an existing **IISNode.yml** file that has previously been published, no restart is required.</span><span class="sxs-lookup"><span data-stu-id="67b63-119">If you are simply changing settings in an existing **IISNode.yml** file that has previously been published, no restart is required.</span></span>

> [!NOTE]
> <span data-ttu-id="67b63-120">If your web app was created using the Azure Command-Line Tools or Azure PowerShell Cmdlets, a default **IISNode.yml** file is automatically created.</span><span class="sxs-lookup"><span data-stu-id="67b63-120">If your web app was created using the Azure Command-Line Tools or Azure PowerShell Cmdlets, a default **IISNode.yml** file is automatically created.</span></span>
> 
> 

<span data-ttu-id="67b63-121">To restart the web app, select the web app in the [Azure Portal](https://portal.azure.com), and then click **RESTART** button:</span><span class="sxs-lookup"><span data-stu-id="67b63-121">To restart the web app, select the web app in the [Azure Portal](https://portal.azure.com), and then click **RESTART** button:</span></span>

![restart button][restart-button]

<span data-ttu-id="67b63-123">If the Azure Command-Line Tools are installed in your development environment, you can use the following command to restart the web app:</span><span class="sxs-lookup"><span data-stu-id="67b63-123">If the Azure Command-Line Tools are installed in your development environment, you can use the following command to restart the web app:</span></span>

    azure site restart [sitename]

> [!NOTE]
> <span data-ttu-id="67b63-124">While loggingEnabled and devErrorsEnabled are the most commonly used IISNode.yml configuration options for capturing diagnostic information, IISNode.yml can be used to configure a variety of options for your hosting environment.</span><span class="sxs-lookup"><span data-stu-id="67b63-124">While loggingEnabled and devErrorsEnabled are the most commonly used IISNode.yml configuration options for capturing diagnostic information, IISNode.yml can be used to configure a variety of options for your hosting environment.</span></span> <span data-ttu-id="67b63-125">For a full list of the configuration options, see the [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span><span class="sxs-lookup"><span data-stu-id="67b63-125">For a full list of the configuration options, see the [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span></span>
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a><span data-ttu-id="67b63-126">Accessing logs</span><span class="sxs-lookup"><span data-stu-id="67b63-126">Accessing logs</span></span>
<span data-ttu-id="67b63-127">Diagnostic logs can be accessed in three ways; Using the File Transfer Protocol (FTP), downloading a Zip archive, or as a live updated stream of the log (also known as a tail).</span><span class="sxs-lookup"><span data-stu-id="67b63-127">Diagnostic logs can be accessed in three ways; Using the File Transfer Protocol (FTP), downloading a Zip archive, or as a live updated stream of the log (also known as a tail).</span></span> <span data-ttu-id="67b63-128">Downloading the Zip archive of the log files or viewing the live stream require the Azure Command-Line Tools.</span><span class="sxs-lookup"><span data-stu-id="67b63-128">Downloading the Zip archive of the log files or viewing the live stream require the Azure Command-Line Tools.</span></span> <span data-ttu-id="67b63-129">These can be installed by using the following command:</span><span class="sxs-lookup"><span data-stu-id="67b63-129">These can be installed by using the following command:</span></span>

    npm install azure-cli -g

<span data-ttu-id="67b63-130">Once installed, the tools can be accessed using the 'azure' command.</span><span class="sxs-lookup"><span data-stu-id="67b63-130">Once installed, the tools can be accessed using the 'azure' command.</span></span> <span data-ttu-id="67b63-131">The command-line tools must first be configured to use your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="67b63-131">The command-line tools must first be configured to use your Azure subscription.</span></span> <span data-ttu-id="67b63-132">For information on how to accomplish this task, see the **How to download and import publish settings** section of the [How to Use The Azure Command-Line Tools](../xplat-cli-connect.md) article.</span><span class="sxs-lookup"><span data-stu-id="67b63-132">For information on how to accomplish this task, see the **How to download and import publish settings** section of the [How to Use The Azure Command-Line Tools](../xplat-cli-connect.md) article.</span></span>

### <a name="ftp"></a><span data-ttu-id="67b63-133">FTP</span><span class="sxs-lookup"><span data-stu-id="67b63-133">FTP</span></span>
<span data-ttu-id="67b63-134">To access the diagnostic information through FTP, visit the [Azure Portal](https://portal.azure.com), select your web app, and then select the **DASHBOARD**.</span><span class="sxs-lookup"><span data-stu-id="67b63-134">To access the diagnostic information through FTP, visit the [Azure Portal](https://portal.azure.com), select your web app, and then select the **DASHBOARD**.</span></span> <span data-ttu-id="67b63-135">In the **quick links** section, the **FTP DIAGNOSTIC LOGS** and **FTPS DIAGNOSTIC LOGS** links provide access to the logs using the FTP protocol.</span><span class="sxs-lookup"><span data-stu-id="67b63-135">In the **quick links** section, the **FTP DIAGNOSTIC LOGS** and **FTPS DIAGNOSTIC LOGS** links provide access to the logs using the FTP protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="67b63-136">If you have not previously configured user name and password for FTP or deployment, you can do so from the **Quickstart** management page by selecting **Set up deployment credentials**.</span><span class="sxs-lookup"><span data-stu-id="67b63-136">If you have not previously configured user name and password for FTP or deployment, you can do so from the **Quickstart** management page by selecting **Set up deployment credentials**.</span></span>
> 
> 

<span data-ttu-id="67b63-137">The FTP URL returned in the dashboard is for the **LogFiles** directory, which will contain the following sub-directories:</span><span class="sxs-lookup"><span data-stu-id="67b63-137">The FTP URL returned in the dashboard is for the **LogFiles** directory, which will contain the following sub-directories:</span></span>

* <span data-ttu-id="67b63-138">[Deployment Method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span><span class="sxs-lookup"><span data-stu-id="67b63-138">[Deployment Method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span></span>
* <span data-ttu-id="67b63-139">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span><span class="sxs-lookup"><span data-stu-id="67b63-139">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="zip-archive"></a><span data-ttu-id="67b63-140">Zip archive</span><span class="sxs-lookup"><span data-stu-id="67b63-140">Zip archive</span></span>
<span data-ttu-id="67b63-141">To download a Zip archive of the diagnostic logs, use the following command from the Azure Command-Line Tools:</span><span class="sxs-lookup"><span data-stu-id="67b63-141">To download a Zip archive of the diagnostic logs, use the following command from the Azure Command-Line Tools:</span></span>

    azure site log download [sitename]

<span data-ttu-id="67b63-142">This will download a **diagnostics.zip** in the current directory.</span><span class="sxs-lookup"><span data-stu-id="67b63-142">This will download a **diagnostics.zip** in the current directory.</span></span> <span data-ttu-id="67b63-143">This archive contains the following directory structure:</span><span class="sxs-lookup"><span data-stu-id="67b63-143">This archive contains the following directory structure:</span></span>

* <span data-ttu-id="67b63-144">deployments - A log of information about deployments of your application</span><span class="sxs-lookup"><span data-stu-id="67b63-144">deployments - A log of information about deployments of your application</span></span>
* <span data-ttu-id="67b63-145">LogFiles</span><span class="sxs-lookup"><span data-stu-id="67b63-145">LogFiles</span></span>
  
  * <span data-ttu-id="67b63-146">[Deployment method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span><span class="sxs-lookup"><span data-stu-id="67b63-146">[Deployment method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span></span>
  * <span data-ttu-id="67b63-147">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span><span class="sxs-lookup"><span data-stu-id="67b63-147">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="live-stream-tail"></a><span data-ttu-id="67b63-148">Live stream (tail)</span><span class="sxs-lookup"><span data-stu-id="67b63-148">Live stream (tail)</span></span>
<span data-ttu-id="67b63-149">To view a live stream of diagnostic log information, use the following command from the Azure Command-Line Tools:</span><span class="sxs-lookup"><span data-stu-id="67b63-149">To view a live stream of diagnostic log information, use the following command from the Azure Command-Line Tools:</span></span>

    azure site log tail [sitename]

<span data-ttu-id="67b63-150">This will return a stream of log events that are updated as they occur on the server.</span><span class="sxs-lookup"><span data-stu-id="67b63-150">This will return a stream of log events that are updated as they occur on the server.</span></span> <span data-ttu-id="67b63-151">This stream will return deployment information as well as stdout and stderr information (when loggingEnabled is true.)</span><span class="sxs-lookup"><span data-stu-id="67b63-151">This stream will return deployment information as well as stdout and stderr information (when loggingEnabled is true.)</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="67b63-152">Next Steps</span><span class="sxs-lookup"><span data-stu-id="67b63-152">Next Steps</span></span>
<span data-ttu-id="67b63-153">In this article you learned how to enable and access diagnostics information for Azure.</span><span class="sxs-lookup"><span data-stu-id="67b63-153">In this article you learned how to enable and access diagnostics information for Azure.</span></span> <span data-ttu-id="67b63-154">While this information is useful in understanding problems that occur with your application, it may point to a problem with a module you are using or that the version of Node.js used by App Service Web Apps is different than the one used in your deployment environment.</span><span class="sxs-lookup"><span data-stu-id="67b63-154">While this information is useful in understanding problems that occur with your application, it may point to a problem with a module you are using or that the version of Node.js used by App Service Web Apps is different than the one used in your deployment environment.</span></span>

<span data-ttu-id="67b63-155">For information in working with modules on Azure, see [Using Node.js Modules with Azure Applications](../nodejs-use-node-modules-azure-apps.md).</span><span class="sxs-lookup"><span data-stu-id="67b63-155">For information in working with modules on Azure, see [Using Node.js Modules with Azure Applications](../nodejs-use-node-modules-azure-apps.md).</span></span>

<span data-ttu-id="67b63-156">For information on specifying a Node.js version for your application, see [Specifying a Node.js version in an Azure application].</span><span class="sxs-lookup"><span data-stu-id="67b63-156">For information on specifying a Node.js version for your application, see [Specifying a Node.js version in an Azure application].</span></span>

<span data-ttu-id="67b63-157">For more information, see also the [Node.js Developer Center](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="67b63-157">For more information, see also the [Node.js Developer Center](/develop/nodejs/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="67b63-158">What's changed</span><span class="sxs-lookup"><span data-stu-id="67b63-158">What's changed</span></span>
* <span data-ttu-id="67b63-159">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="67b63-159">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="67b63-160">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="67b63-160">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="67b63-161">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="67b63-161">No credit cards required; no commitments.</span></span>
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme
[How to Use The Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[Specifying a Node.js version in an Azure application]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-nodejs-debug/restartbutton.png


