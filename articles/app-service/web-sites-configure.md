---
title: Configure web apps in Azure App Service
description: How to configure a web app in Azure App Services
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
ms.assetid: 9af8a367-7d39-4399-9941-b80cbc5f39a0
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: cephalin
ms.openlocfilehash: 84bd2019e9586fa008560dba07119323ecb7f02e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870395"
---
# <a name="configure-web-apps-in-azure-app-service"></a><span data-ttu-id="41cc0-103">Configure web apps in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="41cc0-103">Configure web apps in Azure App Service</span></span>

<span data-ttu-id="41cc0-104">This topic explains how to configure a web app using the [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="41cc0-104">This topic explains how to configure a web app using the [Azure Portal].</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a><span data-ttu-id="41cc0-105">Application settings</span><span class="sxs-lookup"><span data-stu-id="41cc0-105">Application settings</span></span>
1. <span data-ttu-id="41cc0-106">In the [Azure Portal], open the blade for the web app.</span><span class="sxs-lookup"><span data-stu-id="41cc0-106">In the [Azure Portal], open the blade for the web app.</span></span>
3. <span data-ttu-id="41cc0-107">Click **Application settings**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-107">Click **Application settings**.</span></span>

![Application Settings][configure01]

<span data-ttu-id="41cc0-109">The **Application settings** blade has settings grouped under several categories.</span><span class="sxs-lookup"><span data-stu-id="41cc0-109">The **Application settings** blade has settings grouped under several categories.</span></span>

### <a name="general-settings"></a><span data-ttu-id="41cc0-110">General settings</span><span class="sxs-lookup"><span data-stu-id="41cc0-110">General settings</span></span>
<span data-ttu-id="41cc0-111">**Framework versions**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-111">**Framework versions**.</span></span> <span data-ttu-id="41cc0-112">Set these options if your app uses any these frameworks:</span><span class="sxs-lookup"><span data-stu-id="41cc0-112">Set these options if your app uses any these frameworks:</span></span> 

* <span data-ttu-id="41cc0-113">**.NET Framework**: Set the .NET framework version.</span><span class="sxs-lookup"><span data-stu-id="41cc0-113">**.NET Framework**: Set the .NET framework version.</span></span> 
* <span data-ttu-id="41cc0-114">**PHP**: Set the PHP version, or **OFF** to disable PHP.</span><span class="sxs-lookup"><span data-stu-id="41cc0-114">**PHP**: Set the PHP version, or **OFF** to disable PHP.</span></span> 
* <span data-ttu-id="41cc0-115">**Java**: Select the Java version or **OFF** to disable Java.</span><span class="sxs-lookup"><span data-stu-id="41cc0-115">**Java**: Select the Java version or **OFF** to disable Java.</span></span> <span data-ttu-id="41cc0-116">Use the **Web Container** option to choose between Tomcat and Jetty versions.</span><span class="sxs-lookup"><span data-stu-id="41cc0-116">Use the **Web Container** option to choose between Tomcat and Jetty versions.</span></span>
* <span data-ttu-id="41cc0-117">**Python**: Select the Python version, or **OFF** to disable Python.</span><span class="sxs-lookup"><span data-stu-id="41cc0-117">**Python**: Select the Python version, or **OFF** to disable Python.</span></span>

<span data-ttu-id="41cc0-118">For technical reasons, enabling Java for your app disables the .NET, PHP, and Python options.</span><span class="sxs-lookup"><span data-stu-id="41cc0-118">For technical reasons, enabling Java for your app disables the .NET, PHP, and Python options.</span></span>

<a name="platform"></a>
<span data-ttu-id="41cc0-119">**Platform**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-119">**Platform**.</span></span> <span data-ttu-id="41cc0-120">Selects whether your web app runs in a 32-bit or 64-bit environment.</span><span class="sxs-lookup"><span data-stu-id="41cc0-120">Selects whether your web app runs in a 32-bit or 64-bit environment.</span></span> <span data-ttu-id="41cc0-121">The 64-bit environment requires Basic or Standard tier.</span><span class="sxs-lookup"><span data-stu-id="41cc0-121">The 64-bit environment requires Basic or Standard tier.</span></span> <span data-ttu-id="41cc0-122">Free and Shared tier always run in a 32-bit environment.</span><span class="sxs-lookup"><span data-stu-id="41cc0-122">Free and Shared tier always run in a 32-bit environment.</span></span>

[!INCLUDE [app-service-dev-test-note](../../includes/app-service-dev-test-note.md)]

<span data-ttu-id="41cc0-123">**Web Sockets**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-123">**Web Sockets**.</span></span> <span data-ttu-id="41cc0-124">Set **ON** to enable the WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io](https://socket.io/).</span><span class="sxs-lookup"><span data-stu-id="41cc0-124">Set **ON** to enable the WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io](https://socket.io/).</span></span>

<a name="alwayson"></a>
<span data-ttu-id="41cc0-125">**Always On**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-125">**Always On**.</span></span> <span data-ttu-id="41cc0-126">By default, web apps are unloaded if they are idle for some period of time.</span><span class="sxs-lookup"><span data-stu-id="41cc0-126">By default, web apps are unloaded if they are idle for some period of time.</span></span> <span data-ttu-id="41cc0-127">This lets the system conserve resources.</span><span class="sxs-lookup"><span data-stu-id="41cc0-127">This lets the system conserve resources.</span></span> <span data-ttu-id="41cc0-128">In Basic or Standard mode, you can enable **Always On** to keep the app loaded all the time.</span><span class="sxs-lookup"><span data-stu-id="41cc0-128">In Basic or Standard mode, you can enable **Always On** to keep the app loaded all the time.</span></span> <span data-ttu-id="41cc0-129">If your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or the web jobs may not run reliably.</span><span class="sxs-lookup"><span data-stu-id="41cc0-129">If your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or the web jobs may not run reliably.</span></span>

<span data-ttu-id="41cc0-130">**Managed Pipeline Version**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-130">**Managed Pipeline Version**.</span></span> <span data-ttu-id="41cc0-131">Sets the IIS [pipeline mode].</span><span class="sxs-lookup"><span data-stu-id="41cc0-131">Sets the IIS [pipeline mode].</span></span> <span data-ttu-id="41cc0-132">Leave this set to Integrated (the default) unless you have a legacy app that requires an older version of IIS.</span><span class="sxs-lookup"><span data-stu-id="41cc0-132">Leave this set to Integrated (the default) unless you have a legacy app that requires an older version of IIS.</span></span>

<span data-ttu-id="41cc0-133">**HTTP Version**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-133">**HTTP Version**.</span></span> <span data-ttu-id="41cc0-134">Set to **2.0** to enable support for [HTTPS/2](https://wikipedia.org/wiki/HTTP/2) protocol.</span><span class="sxs-lookup"><span data-stu-id="41cc0-134">Set to **2.0** to enable support for [HTTPS/2](https://wikipedia.org/wiki/HTTP/2) protocol.</span></span> 

> [!NOTE]
> <span data-ttu-id="41cc0-135">Most modern browsers support HTTP/2 protocol over TLS only, while non-encrypted traffic continues to use HTTP/1.1.</span><span class="sxs-lookup"><span data-stu-id="41cc0-135">Most modern browsers support HTTP/2 protocol over TLS only, while non-encrypted traffic continues to use HTTP/1.1.</span></span> <span data-ttu-id="41cc0-136">To ensure that client browsers connect to your app with HTTP/2, either [buy an App Service Certificate](web-sites-purchase-ssl-web-site.md) for your app's custom domain or [bind a third party certificate](app-service-web-tutorial-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="41cc0-136">To ensure that client browsers connect to your app with HTTP/2, either [buy an App Service Certificate](web-sites-purchase-ssl-web-site.md) for your app's custom domain or [bind a third party certificate](app-service-web-tutorial-custom-ssl.md).</span></span>

<span data-ttu-id="41cc0-137">**ARR Affinity**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-137">**ARR Affinity**.</span></span> <span data-ttu-id="41cc0-138">In an app that's scaled out to multiple VM instances, ARR Affinity cookies guarantee that the client is routed to the same instance for the life of the session.</span><span class="sxs-lookup"><span data-stu-id="41cc0-138">In an app that's scaled out to multiple VM instances, ARR Affinity cookies guarantee that the client is routed to the same instance for the life of the session.</span></span> <span data-ttu-id="41cc0-139">To improve the performance of stateless applications, set this option to **Off**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-139">To improve the performance of stateless applications, set this option to **Off**.</span></span>   

<span data-ttu-id="41cc0-140">**Auto Swap**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-140">**Auto Swap**.</span></span> <span data-ttu-id="41cc0-141">If you enable Auto Swap for a deployment slot, App Service will automatically swap the web app into production when you push an update to that slot.</span><span class="sxs-lookup"><span data-stu-id="41cc0-141">If you enable Auto Swap for a deployment slot, App Service will automatically swap the web app into production when you push an update to that slot.</span></span> <span data-ttu-id="41cc0-142">For more information, see [Deploy to staging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="41cc0-142">For more information, see [Deploy to staging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span>

### <a name="debugging"></a><span data-ttu-id="41cc0-143">Debugging</span><span class="sxs-lookup"><span data-stu-id="41cc0-143">Debugging</span></span>
<span data-ttu-id="41cc0-144">**Remote Debugging**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-144">**Remote Debugging**.</span></span> <span data-ttu-id="41cc0-145">Enables remote debugging.</span><span class="sxs-lookup"><span data-stu-id="41cc0-145">Enables remote debugging.</span></span> <span data-ttu-id="41cc0-146">When enabled, you can use the remote debugger in Visual Studio to connect directly to your web app.</span><span class="sxs-lookup"><span data-stu-id="41cc0-146">When enabled, you can use the remote debugger in Visual Studio to connect directly to your web app.</span></span> <span data-ttu-id="41cc0-147">Remote debugging will remain enabled for 48 hours.</span><span class="sxs-lookup"><span data-stu-id="41cc0-147">Remote debugging will remain enabled for 48 hours.</span></span> 

### <a name="app-settings"></a><span data-ttu-id="41cc0-148">App settings</span><span class="sxs-lookup"><span data-stu-id="41cc0-148">App settings</span></span>
<span data-ttu-id="41cc0-149">This section contains name/value pairs that your web app will load on start up.</span><span class="sxs-lookup"><span data-stu-id="41cc0-149">This section contains name/value pairs that your web app will load on start up.</span></span> 

* <span data-ttu-id="41cc0-150">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span><span class="sxs-lookup"><span data-stu-id="41cc0-150">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span></span> 
* <span data-ttu-id="41cc0-151">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span><span class="sxs-lookup"><span data-stu-id="41cc0-151">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span></span> <span data-ttu-id="41cc0-152">For each app setting, two environment variables are created; one with the name specified by the app setting entry, and another with a prefix of APPSETTING_.</span><span class="sxs-lookup"><span data-stu-id="41cc0-152">For each app setting, two environment variables are created; one with the name specified by the app setting entry, and another with a prefix of APPSETTING_.</span></span> <span data-ttu-id="41cc0-153">Both contain the same value.</span><span class="sxs-lookup"><span data-stu-id="41cc0-153">Both contain the same value.</span></span>

<span data-ttu-id="41cc0-154">App settings are always encrypted when stored (encrypted-at-rest).</span><span class="sxs-lookup"><span data-stu-id="41cc0-154">App settings are always encrypted when stored (encrypted-at-rest).</span></span>

### <a name="connection-strings"></a><span data-ttu-id="41cc0-155">Connection strings</span><span class="sxs-lookup"><span data-stu-id="41cc0-155">Connection strings</span></span>
<span data-ttu-id="41cc0-156">Connection strings for linked resources.</span><span class="sxs-lookup"><span data-stu-id="41cc0-156">Connection strings for linked resources.</span></span> 

<span data-ttu-id="41cc0-157">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where the key equals the linked database name.</span><span class="sxs-lookup"><span data-stu-id="41cc0-157">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where the key equals the linked database name.</span></span> 

<span data-ttu-id="41cc0-158">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with the connection type.</span><span class="sxs-lookup"><span data-stu-id="41cc0-158">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with the connection type.</span></span> <span data-ttu-id="41cc0-159">The environment variable prefixes are as follows:</span><span class="sxs-lookup"><span data-stu-id="41cc0-159">The environment variable prefixes are as follows:</span></span> 

* <span data-ttu-id="41cc0-160">SQL Server: `SQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="41cc0-160">SQL Server: `SQLCONNSTR_`</span></span>
* <span data-ttu-id="41cc0-161">MySQL: `MYSQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="41cc0-161">MySQL: `MYSQLCONNSTR_`</span></span>
* <span data-ttu-id="41cc0-162">SQL Database: `SQLAZURECONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="41cc0-162">SQL Database: `SQLAZURECONNSTR_`</span></span>
* <span data-ttu-id="41cc0-163">Custom: `CUSTOMCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="41cc0-163">Custom: `CUSTOMCONNSTR_`</span></span>

<span data-ttu-id="41cc0-164">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through the environment variable `MYSQLCONNSTR_connectionString1`.</span><span class="sxs-lookup"><span data-stu-id="41cc0-164">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through the environment variable `MYSQLCONNSTR_connectionString1`.</span></span>

<span data-ttu-id="41cc0-165">Connection strings are always encrypted when stored (encrypted-at-rest).</span><span class="sxs-lookup"><span data-stu-id="41cc0-165">Connection strings are always encrypted when stored (encrypted-at-rest).</span></span>

### <a name="default-documents"></a><span data-ttu-id="41cc0-166">Default documents</span><span class="sxs-lookup"><span data-stu-id="41cc0-166">Default documents</span></span>
<span data-ttu-id="41cc0-167">The default document is the web page that is displayed at the root URL for a website.</span><span class="sxs-lookup"><span data-stu-id="41cc0-167">The default document is the web page that is displayed at the root URL for a website.</span></span>  <span data-ttu-id="41cc0-168">The first matching file in the list is used.</span><span class="sxs-lookup"><span data-stu-id="41cc0-168">The first matching file in the list is used.</span></span> 

<span data-ttu-id="41cc0-169">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span><span class="sxs-lookup"><span data-stu-id="41cc0-169">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span></span>    

### <a name="handler-mappings"></a><span data-ttu-id="41cc0-170">Handler mappings</span><span class="sxs-lookup"><span data-stu-id="41cc0-170">Handler mappings</span></span>
<span data-ttu-id="41cc0-171">Use this area to add custom script processors to handle requests for specific file extensions.</span><span class="sxs-lookup"><span data-stu-id="41cc0-171">Use this area to add custom script processors to handle requests for specific file extensions.</span></span> 

* <span data-ttu-id="41cc0-172">**Extension**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-172">**Extension**.</span></span> <span data-ttu-id="41cc0-173">The file extension to be handled, such as \*.php or handler.fcgi.</span><span class="sxs-lookup"><span data-stu-id="41cc0-173">The file extension to be handled, such as \*.php or handler.fcgi.</span></span> 
* <span data-ttu-id="41cc0-174">**Script Processor Path**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-174">**Script Processor Path**.</span></span> <span data-ttu-id="41cc0-175">The absolute path of the script processor.</span><span class="sxs-lookup"><span data-stu-id="41cc0-175">The absolute path of the script processor.</span></span> <span data-ttu-id="41cc0-176">Requests to files that match the file extension will be processed by the script processor.</span><span class="sxs-lookup"><span data-stu-id="41cc0-176">Requests to files that match the file extension will be processed by the script processor.</span></span> <span data-ttu-id="41cc0-177">Use the path `D:\home\site\wwwroot` to refer to your app's root directory.</span><span class="sxs-lookup"><span data-stu-id="41cc0-177">Use the path `D:\home\site\wwwroot` to refer to your app's root directory.</span></span>
* <span data-ttu-id="41cc0-178">**Additional Arguments**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-178">**Additional Arguments**.</span></span> <span data-ttu-id="41cc0-179">Optional command-line arguments for the script processor</span><span class="sxs-lookup"><span data-stu-id="41cc0-179">Optional command-line arguments for the script processor</span></span> 

### <a name="virtual-applications-and-directories"></a><span data-ttu-id="41cc0-180">Virtual applications and directories</span><span class="sxs-lookup"><span data-stu-id="41cc0-180">Virtual applications and directories</span></span>
<span data-ttu-id="41cc0-181">To configure virtual applications and directories, specify each virtual directory and its corresponding physical path relative to the website root.</span><span class="sxs-lookup"><span data-stu-id="41cc0-181">To configure virtual applications and directories, specify each virtual directory and its corresponding physical path relative to the website root.</span></span> <span data-ttu-id="41cc0-182">Optionally, you can select the **Application** checkbox to mark a virtual directory as an application.</span><span class="sxs-lookup"><span data-stu-id="41cc0-182">Optionally, you can select the **Application** checkbox to mark a virtual directory as an application.</span></span>

## <a name="enabling-diagnostic-logs"></a><span data-ttu-id="41cc0-183">Enabling diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="41cc0-183">Enabling diagnostic logs</span></span>
<span data-ttu-id="41cc0-184">To enable diagnostic logs:</span><span class="sxs-lookup"><span data-stu-id="41cc0-184">To enable diagnostic logs:</span></span>

1. <span data-ttu-id="41cc0-185">In the blade for your web app, click **All settings**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-185">In the blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="41cc0-186">Click **Diagnostic logs**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-186">Click **Diagnostic logs**.</span></span> 

<span data-ttu-id="41cc0-187">Options for writing diagnostic logs from a web application that supports logging:</span><span class="sxs-lookup"><span data-stu-id="41cc0-187">Options for writing diagnostic logs from a web application that supports logging:</span></span> 

* <span data-ttu-id="41cc0-188">**Application Logging**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-188">**Application Logging**.</span></span> <span data-ttu-id="41cc0-189">Writes application logs to the file system.</span><span class="sxs-lookup"><span data-stu-id="41cc0-189">Writes application logs to the file system.</span></span> <span data-ttu-id="41cc0-190">Logging lasts for a period of 12 hours.</span><span class="sxs-lookup"><span data-stu-id="41cc0-190">Logging lasts for a period of 12 hours.</span></span> 

<span data-ttu-id="41cc0-191">**Level**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-191">**Level**.</span></span> <span data-ttu-id="41cc0-192">When application logging is enabled, this option specifies the amount of information that will be recorded (Error, Warning, Information, or Verbose).</span><span class="sxs-lookup"><span data-stu-id="41cc0-192">When application logging is enabled, this option specifies the amount of information that will be recorded (Error, Warning, Information, or Verbose).</span></span>

<span data-ttu-id="41cc0-193">**Web server logging**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-193">**Web server logging**.</span></span> <span data-ttu-id="41cc0-194">Logs are saved in the W3C extended log file format.</span><span class="sxs-lookup"><span data-stu-id="41cc0-194">Logs are saved in the W3C extended log file format.</span></span> 

<span data-ttu-id="41cc0-195">**Detailed error messages**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-195">**Detailed error messages**.</span></span> <span data-ttu-id="41cc0-196">Saves detailed error messages .htm files.</span><span class="sxs-lookup"><span data-stu-id="41cc0-196">Saves detailed error messages .htm files.</span></span> <span data-ttu-id="41cc0-197">The files are saved under /LogFiles/DetailedErrors.</span><span class="sxs-lookup"><span data-stu-id="41cc0-197">The files are saved under /LogFiles/DetailedErrors.</span></span> 

<span data-ttu-id="41cc0-198">**Failed request tracing**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-198">**Failed request tracing**.</span></span> <span data-ttu-id="41cc0-199">Logs failed requests to XML files.</span><span class="sxs-lookup"><span data-stu-id="41cc0-199">Logs failed requests to XML files.</span></span> <span data-ttu-id="41cc0-200">The files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span><span class="sxs-lookup"><span data-stu-id="41cc0-200">The files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span></span> <span data-ttu-id="41cc0-201">This folder contains an XSL file and one or more XML files.</span><span class="sxs-lookup"><span data-stu-id="41cc0-201">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="41cc0-202">Make sure to download the XSL file, because it provides functionality for formatting and filtering the contents of the XML files.</span><span class="sxs-lookup"><span data-stu-id="41cc0-202">Make sure to download the XSL file, because it provides functionality for formatting and filtering the contents of the XML files.</span></span>

<span data-ttu-id="41cc0-203">To view the log files, you must create FTP credentials, as follows:</span><span class="sxs-lookup"><span data-stu-id="41cc0-203">To view the log files, you must create FTP credentials, as follows:</span></span>

1. <span data-ttu-id="41cc0-204">In the blade for your web app, click **All settings**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-204">In the blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="41cc0-205">Click **Deployment credentials**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-205">Click **Deployment credentials**.</span></span>
3. <span data-ttu-id="41cc0-206">Enter a user name and password.</span><span class="sxs-lookup"><span data-stu-id="41cc0-206">Enter a user name and password.</span></span>
4. <span data-ttu-id="41cc0-207">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-207">Click **Save**.</span></span>

![Set deployment credentials][configure03]

<span data-ttu-id="41cc0-209">The full FTP user name is “app\username” where *app* is the name of your web app.</span><span class="sxs-lookup"><span data-stu-id="41cc0-209">The full FTP user name is “app\username” where *app* is the name of your web app.</span></span> <span data-ttu-id="41cc0-210">The username is listed in the web app blade, under **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-210">The username is listed in the web app blade, under **Essentials**.</span></span>

![FTP deployment credentials][configure02]

## <a name="other-configuration-tasks"></a><span data-ttu-id="41cc0-212">Other configuration tasks</span><span class="sxs-lookup"><span data-stu-id="41cc0-212">Other configuration tasks</span></span>
### <a name="ssl"></a><span data-ttu-id="41cc0-213">SSL</span><span class="sxs-lookup"><span data-stu-id="41cc0-213">SSL</span></span>
<span data-ttu-id="41cc0-214">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span><span class="sxs-lookup"><span data-stu-id="41cc0-214">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span></span> <span data-ttu-id="41cc0-215">For more information, see [Enable HTTPS for a web app](app-service-web-tutorial-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="41cc0-215">For more information, see [Enable HTTPS for a web app](app-service-web-tutorial-custom-ssl.md).</span></span> 

<span data-ttu-id="41cc0-216">To view your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-216">To view your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="domain-names"></a><span data-ttu-id="41cc0-217">Domain names</span><span class="sxs-lookup"><span data-stu-id="41cc0-217">Domain names</span></span>
<span data-ttu-id="41cc0-218">Add custom domain names for your web app.</span><span class="sxs-lookup"><span data-stu-id="41cc0-218">Add custom domain names for your web app.</span></span> <span data-ttu-id="41cc0-219">For more information, see [Configure a custom domain name for a web app in Azure App Service](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="41cc0-219">For more information, see [Configure a custom domain name for a web app in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span>

<span data-ttu-id="41cc0-220">To view your domain names, click **All Settings** > **Custom domains and SSL**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-220">To view your domain names, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="deployments"></a><span data-ttu-id="41cc0-221">Deployments</span><span class="sxs-lookup"><span data-stu-id="41cc0-221">Deployments</span></span>
* <span data-ttu-id="41cc0-222">Set up continuous deployment.</span><span class="sxs-lookup"><span data-stu-id="41cc0-222">Set up continuous deployment.</span></span> <span data-ttu-id="41cc0-223">See [Using Git to deploy Web Apps in Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="41cc0-223">See [Using Git to deploy Web Apps in Azure App Service](app-service-deploy-local-git.md).</span></span>
* <span data-ttu-id="41cc0-224">Deployment slots.</span><span class="sxs-lookup"><span data-stu-id="41cc0-224">Deployment slots.</span></span> <span data-ttu-id="41cc0-225">See [Deploy to Staging Environments for Web Apps in Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="41cc0-225">See [Deploy to Staging Environments for Web Apps in Azure App Service].</span></span>

<span data-ttu-id="41cc0-226">To view your deployment slots, click **All Settings** > **Deployment slots**.</span><span class="sxs-lookup"><span data-stu-id="41cc0-226">To view your deployment slots, click **All Settings** > **Deployment slots**.</span></span>

### <a name="monitoring"></a><span data-ttu-id="41cc0-227">Monitoring</span><span class="sxs-lookup"><span data-stu-id="41cc0-227">Monitoring</span></span>
<span data-ttu-id="41cc0-228">In Basic or Standard mode, you can  test the availability of HTTP or HTTPS endpoints, from up to three geo-distributed locations.</span><span class="sxs-lookup"><span data-stu-id="41cc0-228">In Basic or Standard mode, you can  test the availability of HTTP or HTTPS endpoints, from up to three geo-distributed locations.</span></span> <span data-ttu-id="41cc0-229">A monitoring test fails if the HTTP response code is an error (4xx or 5xx) or the response takes more than 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="41cc0-229">A monitoring test fails if the HTTP response code is an error (4xx or 5xx) or the response takes more than 30 seconds.</span></span> <span data-ttu-id="41cc0-230">An endpoint is considered available if the monitoring tests succeed from all the specified locations.</span><span class="sxs-lookup"><span data-stu-id="41cc0-230">An endpoint is considered available if the monitoring tests succeed from all the specified locations.</span></span> 

<span data-ttu-id="41cc0-231">For more information, see [How to: Monitor web endpoint status].</span><span class="sxs-lookup"><span data-stu-id="41cc0-231">For more information, see [How to: Monitor web endpoint status].</span></span>

> [!NOTE]
> <span data-ttu-id="41cc0-232">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="41cc0-232">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="41cc0-233">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="41cc0-233">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="41cc0-234">Next steps</span><span class="sxs-lookup"><span data-stu-id="41cc0-234">Next steps</span></span>
* <span data-ttu-id="41cc0-235">[Configure a custom domain name in Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="41cc0-235">[Configure a custom domain name in Azure App Service]</span></span>
* <span data-ttu-id="41cc0-236">[Enable HTTPS for an app in Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="41cc0-236">[Enable HTTPS for an app in Azure App Service]</span></span>
* <span data-ttu-id="41cc0-237">[Scale a web app in Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="41cc0-237">[Scale a web app in Azure App Service]</span></span>
* <span data-ttu-id="41cc0-238">[Monitoring basics for Web Apps in Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="41cc0-238">[Monitoring basics for Web Apps in Azure App Service]</span></span>

<!-- URL List -->

[ASP.NET SignalR]: http://www.asp.net/signalr
[Azure Portal]: https://portal.azure.com/
[Configure a custom domain name in Azure App Service]: ./app-service-web-tutorial-custom-domain.md
[Deploy to Staging Environments for Web Apps in Azure App Service]: ./web-sites-staged-publishing.md
[Enable HTTPS for an app in Azure App Service]: ./app-service-web-tutorial-custom-ssl.md
[How to: Monitor web endpoint status]: http://go.microsoft.com/fwLink/?LinkID=279906
[Monitoring basics for Web Apps in Azure App Service]: ./web-sites-monitor.md
[pipeline mode]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application
[Scale a web app in Azure App Service]: ./web-sites-scale.md
[Try App Service]: https://azure.microsoft.com/try/app-service/

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
