---
title: Configure web apps in Azure App Service
description: How to configure a web app in Azure App Services
services: app-service\web
documentationcenter: ''
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: 9af8a367-7d39-4399-9941-b80cbc5f39a0
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: 27db8f0e7062f9f49206f33e8e7853794f3eb6c9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551506"
---
# <a name="configure-web-apps-in-azure-app-service"></a><span data-ttu-id="cf66e-103">Configure web apps in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="cf66e-103">Configure web apps in Azure App Service</span></span>
<span data-ttu-id="cf66e-104">This topic explains how to configure a web app using the [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="cf66e-104">This topic explains how to configure a web app using the [Azure Portal].</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a><span data-ttu-id="cf66e-105">Application settings</span><span class="sxs-lookup"><span data-stu-id="cf66e-105">Application settings</span></span>
1. <span data-ttu-id="cf66e-106">In the [Azure Portal], open the blade for the web app.</span><span class="sxs-lookup"><span data-stu-id="cf66e-106">In the [Azure Portal], open the blade for the web app.</span></span>
2. <span data-ttu-id="cf66e-107">Click **All Settings**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-107">Click **All Settings**.</span></span>
3. <span data-ttu-id="cf66e-108">Click **Application Settings**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-108">Click **Application Settings**.</span></span>

![Application Settings][configure01]

<span data-ttu-id="cf66e-110">The **Application settings** blade has settings grouped under several categories.</span><span class="sxs-lookup"><span data-stu-id="cf66e-110">The **Application settings** blade has settings grouped under several categories.</span></span>

### <a name="general-settings"></a><span data-ttu-id="cf66e-111">General settings</span><span class="sxs-lookup"><span data-stu-id="cf66e-111">General settings</span></span>
<span data-ttu-id="cf66e-112">**Framework versions**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-112">**Framework versions**.</span></span> <span data-ttu-id="cf66e-113">Set these options if your app uses any these frameworks:</span><span class="sxs-lookup"><span data-stu-id="cf66e-113">Set these options if your app uses any these frameworks:</span></span> 

* <span data-ttu-id="cf66e-114">**.NET Framework**: Set the .NET framework version.</span><span class="sxs-lookup"><span data-stu-id="cf66e-114">**.NET Framework**: Set the .NET framework version.</span></span> 
* <span data-ttu-id="cf66e-115">**PHP**: Set the PHP version, or **OFF** to disable PHP.</span><span class="sxs-lookup"><span data-stu-id="cf66e-115">**PHP**: Set the PHP version, or **OFF** to disable PHP.</span></span> 
* <span data-ttu-id="cf66e-116">**Java**: Select the Java version or **OFF** to disable Java.</span><span class="sxs-lookup"><span data-stu-id="cf66e-116">**Java**: Select the Java version or **OFF** to disable Java.</span></span> <span data-ttu-id="cf66e-117">Use the **Web Container** option to choose between Tomcat and Jetty versions.</span><span class="sxs-lookup"><span data-stu-id="cf66e-117">Use the **Web Container** option to choose between Tomcat and Jetty versions.</span></span>
* <span data-ttu-id="cf66e-118">**Python**: Select the Python version, or **OFF** to disable Python.</span><span class="sxs-lookup"><span data-stu-id="cf66e-118">**Python**: Select the Python version, or **OFF** to disable Python.</span></span>

<span data-ttu-id="cf66e-119">For technical reasons, enabling Java for your app disables the .NET, PHP, and Python options.</span><span class="sxs-lookup"><span data-stu-id="cf66e-119">For technical reasons, enabling Java for your app disables the .NET, PHP, and Python options.</span></span>

<a name="platform"></a>
<span data-ttu-id="cf66e-120">**Platform**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-120">**Platform**.</span></span> <span data-ttu-id="cf66e-121">Selects whether your web app runs in a 32-bit or 64-bit environment.</span><span class="sxs-lookup"><span data-stu-id="cf66e-121">Selects whether your web app runs in a 32-bit or 64-bit environment.</span></span> <span data-ttu-id="cf66e-122">The 64-bit environment requires Basic or Standard mode.</span><span class="sxs-lookup"><span data-stu-id="cf66e-122">The 64-bit environment requires Basic or Standard mode.</span></span> <span data-ttu-id="cf66e-123">Free and Shared modes always run in a 32-bit environment.</span><span class="sxs-lookup"><span data-stu-id="cf66e-123">Free and Shared modes always run in a 32-bit environment.</span></span>

<span data-ttu-id="cf66e-124">**Web Sockets**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-124">**Web Sockets**.</span></span> <span data-ttu-id="cf66e-125">Set **ON** to enable the WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io].</span><span class="sxs-lookup"><span data-stu-id="cf66e-125">Set **ON** to enable the WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io].</span></span>

<a name="alwayson"></a>
<span data-ttu-id="cf66e-126">**Always On**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-126">**Always On**.</span></span> <span data-ttu-id="cf66e-127">By default, web apps are unloaded if they are idle for some period of time.</span><span class="sxs-lookup"><span data-stu-id="cf66e-127">By default, web apps are unloaded if they are idle for some period of time.</span></span> <span data-ttu-id="cf66e-128">This lets the system conserve resources.</span><span class="sxs-lookup"><span data-stu-id="cf66e-128">This lets the system conserve resources.</span></span> <span data-ttu-id="cf66e-129">In Basic or Standard mode, you can enable **Always On** to keep the app loaded all the time.</span><span class="sxs-lookup"><span data-stu-id="cf66e-129">In Basic or Standard mode, you can enable **Always On** to keep the app loaded all the time.</span></span> <span data-ttu-id="cf66e-130">If your app runs continuous web jobs, you should enable **Always On**, or the web jobs may not run reliably.</span><span class="sxs-lookup"><span data-stu-id="cf66e-130">If your app runs continuous web jobs, you should enable **Always On**, or the web jobs may not run reliably.</span></span>

<span data-ttu-id="cf66e-131">**Managed Pipeline Version**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-131">**Managed Pipeline Version**.</span></span> <span data-ttu-id="cf66e-132">Sets the IIS [pipeline mode].</span><span class="sxs-lookup"><span data-stu-id="cf66e-132">Sets the IIS [pipeline mode].</span></span> <span data-ttu-id="cf66e-133">Leave this set to Integrated (the default) unless you have a legacy app that requires an older version of IIS.</span><span class="sxs-lookup"><span data-stu-id="cf66e-133">Leave this set to Integrated (the default) unless you have a legacy app that requires an older version of IIS.</span></span>

<span data-ttu-id="cf66e-134">**Auto Swap**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-134">**Auto Swap**.</span></span> <span data-ttu-id="cf66e-135">If you enable Auto Swap for a deployment slot, App Service will automatically swap the web app into production when you push an update to that slot.</span><span class="sxs-lookup"><span data-stu-id="cf66e-135">If you enable Auto Swap for a deployment slot, App Service will automatically swap the web app into production when you push an update to that slot.</span></span> <span data-ttu-id="cf66e-136">For more information, see [Deploy to staging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="cf66e-136">For more information, see [Deploy to staging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span>

### <a name="debugging"></a><span data-ttu-id="cf66e-137">Debugging</span><span class="sxs-lookup"><span data-stu-id="cf66e-137">Debugging</span></span>
<span data-ttu-id="cf66e-138">**Remote Debugging**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-138">**Remote Debugging**.</span></span> <span data-ttu-id="cf66e-139">Enables remote debugging.</span><span class="sxs-lookup"><span data-stu-id="cf66e-139">Enables remote debugging.</span></span> <span data-ttu-id="cf66e-140">When enabled, you can use the remote debugger in Visual Studio to connect directly to your web app.</span><span class="sxs-lookup"><span data-stu-id="cf66e-140">When enabled, you can use the remote debugger in Visual Studio to connect directly to your web app.</span></span> <span data-ttu-id="cf66e-141">Remote debugging will remain enabled for 48 hours.</span><span class="sxs-lookup"><span data-stu-id="cf66e-141">Remote debugging will remain enabled for 48 hours.</span></span> 

### <a name="app-settings"></a><span data-ttu-id="cf66e-142">App settings</span><span class="sxs-lookup"><span data-stu-id="cf66e-142">App settings</span></span>
<span data-ttu-id="cf66e-143">This section contains name/value pairs that you web app will load on start up.</span><span class="sxs-lookup"><span data-stu-id="cf66e-143">This section contains name/value pairs that you web app will load on start up.</span></span> 

* <span data-ttu-id="cf66e-144">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span><span class="sxs-lookup"><span data-stu-id="cf66e-144">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span></span> 
* <span data-ttu-id="cf66e-145">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span><span class="sxs-lookup"><span data-stu-id="cf66e-145">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span></span> <span data-ttu-id="cf66e-146">For each app setting, two environment variables are created; one with the name specified by the app setting entry, and another with a prefix of APPSETTING_.</span><span class="sxs-lookup"><span data-stu-id="cf66e-146">For each app setting, two environment variables are created; one with the name specified by the app setting entry, and another with a prefix of APPSETTING_.</span></span> <span data-ttu-id="cf66e-147">Both contain the same value.</span><span class="sxs-lookup"><span data-stu-id="cf66e-147">Both contain the same value.</span></span>

### <a name="connection-strings"></a><span data-ttu-id="cf66e-148">Connection strings</span><span class="sxs-lookup"><span data-stu-id="cf66e-148">Connection strings</span></span>
<span data-ttu-id="cf66e-149">Connection strings for linked resources.</span><span class="sxs-lookup"><span data-stu-id="cf66e-149">Connection strings for linked resources.</span></span> 

<span data-ttu-id="cf66e-150">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where the key equals the linked database name.</span><span class="sxs-lookup"><span data-stu-id="cf66e-150">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where the key equals the linked database name.</span></span> 

<span data-ttu-id="cf66e-151">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with the connection type.</span><span class="sxs-lookup"><span data-stu-id="cf66e-151">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with the connection type.</span></span> <span data-ttu-id="cf66e-152">The environment variable prefixes are as follows:</span><span class="sxs-lookup"><span data-stu-id="cf66e-152">The environment variable prefixes are as follows:</span></span> 

* <span data-ttu-id="cf66e-153">SQL Server: `SQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="cf66e-153">SQL Server: `SQLCONNSTR_`</span></span>
* <span data-ttu-id="cf66e-154">MySQL: `MYSQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="cf66e-154">MySQL: `MYSQLCONNSTR_`</span></span>
* <span data-ttu-id="cf66e-155">SQL Database: `SQLAZURECONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="cf66e-155">SQL Database: `SQLAZURECONNSTR_`</span></span>
* <span data-ttu-id="cf66e-156">Custom: `CUSTOMCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="cf66e-156">Custom: `CUSTOMCONNSTR_`</span></span>

<span data-ttu-id="cf66e-157">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through the environment variable `MYSQLCONNSTR_connectionString1`.</span><span class="sxs-lookup"><span data-stu-id="cf66e-157">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through the environment variable `MYSQLCONNSTR_connectionString1`.</span></span>

### <a name="default-documents"></a><span data-ttu-id="cf66e-158">Default documents</span><span class="sxs-lookup"><span data-stu-id="cf66e-158">Default documents</span></span>
<span data-ttu-id="cf66e-159">The default document is the web page that is displayed at the root URL for a website.</span><span class="sxs-lookup"><span data-stu-id="cf66e-159">The default document is the web page that is displayed at the root URL for a website.</span></span>  <span data-ttu-id="cf66e-160">The first matching file in the list is used.</span><span class="sxs-lookup"><span data-stu-id="cf66e-160">The first matching file in the list is used.</span></span> 

<span data-ttu-id="cf66e-161">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span><span class="sxs-lookup"><span data-stu-id="cf66e-161">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span></span>    

### <a name="handler-mappings"></a><span data-ttu-id="cf66e-162">Handler mappings</span><span class="sxs-lookup"><span data-stu-id="cf66e-162">Handler mappings</span></span>
<span data-ttu-id="cf66e-163">Use this area to add custom script processors to handle requests for specific file extensions.</span><span class="sxs-lookup"><span data-stu-id="cf66e-163">Use this area to add custom script processors to handle requests for specific file extensions.</span></span> 

* <span data-ttu-id="cf66e-164">**Extension**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-164">**Extension**.</span></span> <span data-ttu-id="cf66e-165">The file extension to be handled, such as \*.php or handler.fcgi.</span><span class="sxs-lookup"><span data-stu-id="cf66e-165">The file extension to be handled, such as \*.php or handler.fcgi.</span></span> 
* <span data-ttu-id="cf66e-166">**Script Processor Path**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-166">**Script Processor Path**.</span></span> <span data-ttu-id="cf66e-167">The absolute path of the script processor.</span><span class="sxs-lookup"><span data-stu-id="cf66e-167">The absolute path of the script processor.</span></span> <span data-ttu-id="cf66e-168">Requests to files that match the file extension will be processed by the script processor.</span><span class="sxs-lookup"><span data-stu-id="cf66e-168">Requests to files that match the file extension will be processed by the script processor.</span></span> <span data-ttu-id="cf66e-169">Use the path `D:\home\site\wwwroot` to refer to your app's root directory.</span><span class="sxs-lookup"><span data-stu-id="cf66e-169">Use the path `D:\home\site\wwwroot` to refer to your app's root directory.</span></span>
* <span data-ttu-id="cf66e-170">**Additional Arguments**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-170">**Additional Arguments**.</span></span> <span data-ttu-id="cf66e-171">Optional command-line arguments for the script processor</span><span class="sxs-lookup"><span data-stu-id="cf66e-171">Optional command-line arguments for the script processor</span></span> 

### <a name="virtual-applications-and-directories"></a><span data-ttu-id="cf66e-172">Virtual applications and directories</span><span class="sxs-lookup"><span data-stu-id="cf66e-172">Virtual applications and directories</span></span>
<span data-ttu-id="cf66e-173">To configure virtual applications and directories, specify each virtual directory and its corresponding physical path relative to the website root.</span><span class="sxs-lookup"><span data-stu-id="cf66e-173">To configure virtual applications and directories, specify each virtual directory and its corresponding physical path relative to the website root.</span></span> <span data-ttu-id="cf66e-174">Optionally, you can select the **Application** checkbox to mark a virtual directory as an application.</span><span class="sxs-lookup"><span data-stu-id="cf66e-174">Optionally, you can select the **Application** checkbox to mark a virtual directory as an application.</span></span>

## <a name="enabling-diagnostic-logs"></a><span data-ttu-id="cf66e-175">Enabling diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="cf66e-175">Enabling diagnostic logs</span></span>
<span data-ttu-id="cf66e-176">To enable diagnostic logs:</span><span class="sxs-lookup"><span data-stu-id="cf66e-176">To enable diagnostic logs:</span></span>

1. <span data-ttu-id="cf66e-177">In the blade for your web app, click **All settings**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-177">In the blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="cf66e-178">Click **Diagnostic logs**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-178">Click **Diagnostic logs**.</span></span> 

<span data-ttu-id="cf66e-179">Options for writing diagnostic logs from a web application that supports logging:</span><span class="sxs-lookup"><span data-stu-id="cf66e-179">Options for writing diagnostic logs from a web application that supports logging:</span></span> 

* <span data-ttu-id="cf66e-180">**Application Logging**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-180">**Application Logging**.</span></span> <span data-ttu-id="cf66e-181">Writes application logs to the file system.</span><span class="sxs-lookup"><span data-stu-id="cf66e-181">Writes application logs to the file system.</span></span> <span data-ttu-id="cf66e-182">Logging lasts for a period of 12 hours.</span><span class="sxs-lookup"><span data-stu-id="cf66e-182">Logging lasts for a period of 12 hours.</span></span> 

<span data-ttu-id="cf66e-183">**Level**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-183">**Level**.</span></span> <span data-ttu-id="cf66e-184">When application logging is enabled, this option specifies the amount of information that will be recorded (Error, Warning, Information, or Verbose).</span><span class="sxs-lookup"><span data-stu-id="cf66e-184">When application logging is enabled, this option specifies the amount of information that will be recorded (Error, Warning, Information, or Verbose).</span></span>

<span data-ttu-id="cf66e-185">**Web server logging**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-185">**Web server logging**.</span></span> <span data-ttu-id="cf66e-186">Logs are saved in the W3C extended log file format.</span><span class="sxs-lookup"><span data-stu-id="cf66e-186">Logs are saved in the W3C extended log file format.</span></span> 

<span data-ttu-id="cf66e-187">**Detailed error messages**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-187">**Detailed error messages**.</span></span> <span data-ttu-id="cf66e-188">Saves detailed error messages .htm files.</span><span class="sxs-lookup"><span data-stu-id="cf66e-188">Saves detailed error messages .htm files.</span></span> <span data-ttu-id="cf66e-189">The files are saved under /LogFiles/DetailedErrors.</span><span class="sxs-lookup"><span data-stu-id="cf66e-189">The files are saved under /LogFiles/DetailedErrors.</span></span> 

<span data-ttu-id="cf66e-190">**Failed request tracing**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-190">**Failed request tracing**.</span></span> <span data-ttu-id="cf66e-191">Logs failed requests to XML files.</span><span class="sxs-lookup"><span data-stu-id="cf66e-191">Logs failed requests to XML files.</span></span> <span data-ttu-id="cf66e-192">The files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span><span class="sxs-lookup"><span data-stu-id="cf66e-192">The files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span></span> <span data-ttu-id="cf66e-193">This folder contains an XSL file and one or more XML files.</span><span class="sxs-lookup"><span data-stu-id="cf66e-193">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="cf66e-194">Make sure to download the XSL file, because it provides functionality for formatting and filtering the contents of the XML files.</span><span class="sxs-lookup"><span data-stu-id="cf66e-194">Make sure to download the XSL file, because it provides functionality for formatting and filtering the contents of the XML files.</span></span>

<span data-ttu-id="cf66e-195">To view the log files, you must create FTP credentials, as follows:</span><span class="sxs-lookup"><span data-stu-id="cf66e-195">To view the log files, you must create FTP credentials, as follows:</span></span>

1. <span data-ttu-id="cf66e-196">In the blade for your web app, click **All settings**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-196">In the blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="cf66e-197">Click **Deployment credentials**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-197">Click **Deployment credentials**.</span></span>
3. <span data-ttu-id="cf66e-198">Enter a user name and password.</span><span class="sxs-lookup"><span data-stu-id="cf66e-198">Enter a user name and password.</span></span>
4. <span data-ttu-id="cf66e-199">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-199">Click **Save**.</span></span>

![Set deployment credentials][configure03]

<span data-ttu-id="cf66e-201">The full FTP user name is “app\username” where *app* is the name of your web app.</span><span class="sxs-lookup"><span data-stu-id="cf66e-201">The full FTP user name is “app\username” where *app* is the name of your web app.</span></span> <span data-ttu-id="cf66e-202">The username is listed in the web app blade, under **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-202">The username is listed in the web app blade, under **Essentials**.</span></span>  

![FTP deployment credentials][configure02]

## <a name="other-configuration-tasks"></a><span data-ttu-id="cf66e-204">Other configuration tasks</span><span class="sxs-lookup"><span data-stu-id="cf66e-204">Other configuration tasks</span></span>
### <a name="ssl"></a><span data-ttu-id="cf66e-205">SSL</span><span class="sxs-lookup"><span data-stu-id="cf66e-205">SSL</span></span>
<span data-ttu-id="cf66e-206">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span><span class="sxs-lookup"><span data-stu-id="cf66e-206">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span></span> <span data-ttu-id="cf66e-207">For more information, see [Enable HTTPS for a web app].</span><span class="sxs-lookup"><span data-stu-id="cf66e-207">For more information, see [Enable HTTPS for a web app].</span></span> 

<span data-ttu-id="cf66e-208">To view your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-208">To view your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="domain-names"></a><span data-ttu-id="cf66e-209">Domain names</span><span class="sxs-lookup"><span data-stu-id="cf66e-209">Domain names</span></span>
<span data-ttu-id="cf66e-210">Add custom domain names for your web app.</span><span class="sxs-lookup"><span data-stu-id="cf66e-210">Add custom domain names for your web app.</span></span> <span data-ttu-id="cf66e-211">For more information, see [Configure a custom domain name for a web app in Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="cf66e-211">For more information, see [Configure a custom domain name for a web app in Azure App Service].</span></span>

<span data-ttu-id="cf66e-212">To view your domain names, click **All Settings** > **Custom domains and SSL**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-212">To view your domain names, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="deployments"></a><span data-ttu-id="cf66e-213">Deployments</span><span class="sxs-lookup"><span data-stu-id="cf66e-213">Deployments</span></span>
* <span data-ttu-id="cf66e-214">Set up continuous deployment.</span><span class="sxs-lookup"><span data-stu-id="cf66e-214">Set up continuous deployment.</span></span> <span data-ttu-id="cf66e-215">See [Using Git to deploy Web Apps in Azure App Service](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="cf66e-215">See [Using Git to deploy Web Apps in Azure App Service](web-sites-deploy.md).</span></span>
* <span data-ttu-id="cf66e-216">Deployment slots.</span><span class="sxs-lookup"><span data-stu-id="cf66e-216">Deployment slots.</span></span> <span data-ttu-id="cf66e-217">See [Deploy to Staging Environments for Web Apps in Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="cf66e-217">See [Deploy to Staging Environments for Web Apps in Azure App Service].</span></span>

<span data-ttu-id="cf66e-218">To view your deployment slots, click **All Settings** > **Deployment slots**.</span><span class="sxs-lookup"><span data-stu-id="cf66e-218">To view your deployment slots, click **All Settings** > **Deployment slots**.</span></span>

### <a name="monitoring"></a><span data-ttu-id="cf66e-219">Monitoring</span><span class="sxs-lookup"><span data-stu-id="cf66e-219">Monitoring</span></span>
<span data-ttu-id="cf66e-220">In Basic or Standard mode, you can  test the availability of HTTP or HTTPS endpoints, from up to three geo-distributed locations.</span><span class="sxs-lookup"><span data-stu-id="cf66e-220">In Basic or Standard mode, you can  test the availability of HTTP or HTTPS endpoints, from up to three geo-distributed locations.</span></span> <span data-ttu-id="cf66e-221">A monitoring test fails if the HTTP response code is an error (4xx or 5xx) or the response takes more than 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="cf66e-221">A monitoring test fails if the HTTP response code is an error (4xx or 5xx) or the response takes more than 30 seconds.</span></span> <span data-ttu-id="cf66e-222">An endpoint is considered available if the monitoring tests succeed from all the specified locations.</span><span class="sxs-lookup"><span data-stu-id="cf66e-222">An endpoint is considered available if the monitoring tests succeed from all the specified locations.</span></span> 

<span data-ttu-id="cf66e-223">For more information, see [How to: Monitor web endpoint status].</span><span class="sxs-lookup"><span data-stu-id="cf66e-223">For more information, see [How to: Monitor web endpoint status].</span></span>

> [!NOTE]
> <span data-ttu-id="cf66e-224">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="cf66e-224">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="cf66e-225">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="cf66e-225">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="cf66e-226">Next steps</span><span class="sxs-lookup"><span data-stu-id="cf66e-226">Next steps</span></span>
* <span data-ttu-id="cf66e-227">[Configure a custom domain name in Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="cf66e-227">[Configure a custom domain name in Azure App Service]</span></span>
* <span data-ttu-id="cf66e-228">[Enable HTTPS for an app in Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="cf66e-228">[Enable HTTPS for an app in Azure App Service]</span></span>
* <span data-ttu-id="cf66e-229">[Scale a web app in Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="cf66e-229">[Scale a web app in Azure App Service]</span></span>
* <span data-ttu-id="cf66e-230">[Monitoring basics for Web Apps in Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="cf66e-230">[Monitoring basics for Web Apps in Azure App Service]</span></span>

<!-- URL List -->

[ASP.NET SignalR]: http://www.asp.net/signalr
[Azure Portal]: https://portal.azure.com/
[Configure a custom domain name in Azure App Service]: ./web-sites-custom-domain-name.md
[Deploy to Staging Environments for Web Apps in Azure App Service]: ./web-sites-staged-publishing.md
[Enable HTTPS for an app in Azure App Service]: ./web-sites-configure-ssl-certificate.md
[How to: Monitor web endpoint status]: http://go.microsoft.com/fwLink/?LinkID=279906
[Monitoring basics for Web Apps in Azure App Service]: ./web-sites-monitor.md
[pipeline mode]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application
[Scale a web app in Azure App Service]: ./web-sites-scale.md
[socket.io]: ./web-sites-nodejs-chat-app-socketio.md
[Try App Service]: https://azure.microsoft.com/try/app-service/

<!-- IMG List -->

[configure01]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-configure/configure01.png
[configure02]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-configure/configure02.png
[configure03]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-configure/configure03.png



