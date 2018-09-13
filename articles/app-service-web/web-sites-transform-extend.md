---
title: Azure App Service web app advanced config and extensions
description: Use XML Document Transformation(XDT) declarations to transform the ApplicationHost.config file in your Azure App Service web app and to add private extensions to enable custom administration actions.
author: cephalin
writer: cephalin
editor: mollybos
manager: erikre
services: app-service
documentationcenter: ''
ms.assetid: b441a286-ef38-4abc-b102-cdb249baf5bc
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: a749190d99a26bc2ff76e5f13a089d7a0a74ddc8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551640"
---
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a><span data-ttu-id="e37b7-103">Azure App Service web app advanced config and extensions</span><span class="sxs-lookup"><span data-stu-id="e37b7-103">Azure App Service web app advanced config and extensions</span></span>
<span data-ttu-id="e37b7-104">By using [XML Document Transformation](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) declarations, you can transform the [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) file in your web app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="e37b7-104">By using [XML Document Transformation](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) declarations, you can transform the [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) file in your web app in Azure App Service.</span></span> <span data-ttu-id="e37b7-105">You can also use XDT declarations to add private extensions to enable custom web app administration actions.</span><span class="sxs-lookup"><span data-stu-id="e37b7-105">You can also use XDT declarations to add private extensions to enable custom web app administration actions.</span></span> <span data-ttu-id="e37b7-106">This article includes a sample PHP Manager web app extension that enables management of PHP settings through a web interface.</span><span class="sxs-lookup"><span data-stu-id="e37b7-106">This article includes a sample PHP Manager web app extension that enables management of PHP settings through a web interface.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="transform"></a><span data-ttu-id="e37b7-107">Advanced configuration through ApplicationHost.config</span><span class="sxs-lookup"><span data-stu-id="e37b7-107">Advanced configuration through ApplicationHost.config</span></span>
<span data-ttu-id="e37b7-108">The App Service platform provides flexibility and control for web app configuration.</span><span class="sxs-lookup"><span data-stu-id="e37b7-108">The App Service platform provides flexibility and control for web app configuration.</span></span> <span data-ttu-id="e37b7-109">Although the standard IIS ApplicationHost.config configuration file is not available for direct editing in App Service, the platform supports a declarative ApplicationHost.config transform model based on XML Document Transformation (XDT).</span><span class="sxs-lookup"><span data-stu-id="e37b7-109">Although the standard IIS ApplicationHost.config configuration file is not available for direct editing in App Service, the platform supports a declarative ApplicationHost.config transform model based on XML Document Transformation (XDT).</span></span>

<span data-ttu-id="e37b7-110">To leverage this transform functionality, you create an ApplicationHost.xdt file with XDT content and place under the site root (d:\home\site) in the [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span><span class="sxs-lookup"><span data-stu-id="e37b7-110">To leverage this transform functionality, you create an ApplicationHost.xdt file with XDT content and place under the site root (d:\home\site) in the [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span></span> <span data-ttu-id="e37b7-111">You may need to restart the Web App for changes to take effect.</span><span class="sxs-lookup"><span data-stu-id="e37b7-111">You may need to restart the Web App for changes to take effect.</span></span>

<span data-ttu-id="e37b7-112">The following applicationHost.xdt sample shows how to add a new custom environment variable to a web app that uses PHP 5.4.</span><span class="sxs-lookup"><span data-stu-id="e37b7-112">The following applicationHost.xdt sample shows how to add a new custom environment variable to a web app that uses PHP 5.4.</span></span>

    <?xml version="1.0"?>
    <configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
          <system.webServer>
                <fastCgi>
                      <application>
                         <environmentVariables>
                                <environmentVariable name="CONFIGTEST" value="TEST" xdt:Transform="Insert" xdt:Locator="XPath(/configuration/system.webServer/fastCgi/application[contains(@fullPath,'5.4')]/environmentVariables)" />
                         </environmentVariables>
                      </application>
                </fastCgi>
          </system.webServer>
    </configuration>


<span data-ttu-id="e37b7-113">A log file with transform status and details is available from the FTP root under LogFiles\Transform.</span><span class="sxs-lookup"><span data-stu-id="e37b7-113">A log file with transform status and details is available from the FTP root under LogFiles\Transform.</span></span>

<span data-ttu-id="e37b7-114">For additional samples, see [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span><span class="sxs-lookup"><span data-stu-id="e37b7-114">For additional samples, see [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span></span>

<span data-ttu-id="e37b7-115">**Note**</span><span class="sxs-lookup"><span data-stu-id="e37b7-115">**Note**</span></span><br />
<span data-ttu-id="e37b7-116">Elements from the list of modules under `system.webServer` cannot be removed or reordered, but additions to the list are possible.</span><span class="sxs-lookup"><span data-stu-id="e37b7-116">Elements from the list of modules under `system.webServer` cannot be removed or reordered, but additions to the list are possible.</span></span>

## <a id="extend"></a> <span data-ttu-id="e37b7-117">Extend your web app</span><span class="sxs-lookup"><span data-stu-id="e37b7-117">Extend your web app</span></span>
### <a id="overview"></a> <span data-ttu-id="e37b7-118">Overview of private web app extensions</span><span class="sxs-lookup"><span data-stu-id="e37b7-118">Overview of private web app extensions</span></span>
<span data-ttu-id="e37b7-119">App Service supports web app extensions as an extensibility point for administrative actions.</span><span class="sxs-lookup"><span data-stu-id="e37b7-119">App Service supports web app extensions as an extensibility point for administrative actions.</span></span> <span data-ttu-id="e37b7-120">In fact, some App Service platform features are implemented as pre-installed extensions.</span><span class="sxs-lookup"><span data-stu-id="e37b7-120">In fact, some App Service platform features are implemented as pre-installed extensions.</span></span> <span data-ttu-id="e37b7-121">While the pre-installed platform extensions cannot be modified, you can create and configure private extensions for your own web app.</span><span class="sxs-lookup"><span data-stu-id="e37b7-121">While the pre-installed platform extensions cannot be modified, you can create and configure private extensions for your own web app.</span></span> <span data-ttu-id="e37b7-122">This functionality also relies on XDT declarations.</span><span class="sxs-lookup"><span data-stu-id="e37b7-122">This functionality also relies on XDT declarations.</span></span> <span data-ttu-id="e37b7-123">The key steps for creating a private web app extension are the following:</span><span class="sxs-lookup"><span data-stu-id="e37b7-123">The key steps for creating a private web app extension are the following:</span></span>

1. <span data-ttu-id="e37b7-124">Web app extension **content**: create any web application supported by App Service</span><span class="sxs-lookup"><span data-stu-id="e37b7-124">Web app extension **content**: create any web application supported by App Service</span></span>
2. <span data-ttu-id="e37b7-125">Web app extension **declaration**: create an ApplicationHost.xdt file</span><span class="sxs-lookup"><span data-stu-id="e37b7-125">Web app extension **declaration**: create an ApplicationHost.xdt file</span></span>
3. <span data-ttu-id="e37b7-126">Web app extension **deployment**: place content in the SiteExtensions folder under `root`</span><span class="sxs-lookup"><span data-stu-id="e37b7-126">Web app extension **deployment**: place content in the SiteExtensions folder under `root`</span></span>

<span data-ttu-id="e37b7-127">Internal links for the web app should point to a path relative to the application path specified in the ApplicationHost.xdt file.</span><span class="sxs-lookup"><span data-stu-id="e37b7-127">Internal links for the web app should point to a path relative to the application path specified in the ApplicationHost.xdt file.</span></span> <span data-ttu-id="e37b7-128">Any change to the ApplicationHost.xdt file requires a web app recycle.</span><span class="sxs-lookup"><span data-stu-id="e37b7-128">Any change to the ApplicationHost.xdt file requires a web app recycle.</span></span>

<span data-ttu-id="e37b7-129">**Note**: Additional information for these key elements is available at [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span><span class="sxs-lookup"><span data-stu-id="e37b7-129">**Note**: Additional information for these key elements is available at [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span></span>

<span data-ttu-id="e37b7-130">A detailed example is included to illustrate the steps for creating and enabling a private web app extension.</span><span class="sxs-lookup"><span data-stu-id="e37b7-130">A detailed example is included to illustrate the steps for creating and enabling a private web app extension.</span></span> <span data-ttu-id="e37b7-131">The source code for the PHP Manager example that follows can be downloaded from [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span><span class="sxs-lookup"><span data-stu-id="e37b7-131">The source code for the PHP Manager example that follows can be downloaded from [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span></span>

### <a id="SiteSample"></a> <span data-ttu-id="e37b7-132">Web app extension example: PHP Manager</span><span class="sxs-lookup"><span data-stu-id="e37b7-132">Web app extension example: PHP Manager</span></span>
<span data-ttu-id="e37b7-133">PHP Manager is a web app extension that allows web app administrators to easily view and configure their PHP settings using a web interface instead of having to modify PHP .ini files directly.</span><span class="sxs-lookup"><span data-stu-id="e37b7-133">PHP Manager is a web app extension that allows web app administrators to easily view and configure their PHP settings using a web interface instead of having to modify PHP .ini files directly.</span></span> <span data-ttu-id="e37b7-134">Common configuration files for PHP include the php.ini file located under Program Files and the .user.ini file located in the root folder of your web app.</span><span class="sxs-lookup"><span data-stu-id="e37b7-134">Common configuration files for PHP include the php.ini file located under Program Files and the .user.ini file located in the root folder of your web app.</span></span> <span data-ttu-id="e37b7-135">Since the php.ini file is not directly editable on the App Service platform, the PHP Manager extension uses the .user.ini file to apply setting changes.</span><span class="sxs-lookup"><span data-stu-id="e37b7-135">Since the php.ini file is not directly editable on the App Service platform, the PHP Manager extension uses the .user.ini file to apply setting changes.</span></span>

#### <a id="PHPwebapp"></a> <span data-ttu-id="e37b7-136">The PHP Manager web application</span><span class="sxs-lookup"><span data-stu-id="e37b7-136">The PHP Manager web application</span></span>
<span data-ttu-id="e37b7-137">The following is the home page of the PHP Manager deployment:</span><span class="sxs-lookup"><span data-stu-id="e37b7-137">The following is the home page of the PHP Manager deployment:</span></span>

![TransformSitePHPUI][TransformSitePHPUI]

<span data-ttu-id="e37b7-139">As you can see, a web app extension is just like a regular web application, but with an additional ApplicationHost.xdt file placed in the root folder of the web app (more details about the ApplicationHost.xdt file are available in the next section of this article).</span><span class="sxs-lookup"><span data-stu-id="e37b7-139">As you can see, a web app extension is just like a regular web application, but with an additional ApplicationHost.xdt file placed in the root folder of the web app (more details about the ApplicationHost.xdt file are available in the next section of this article).</span></span>

<span data-ttu-id="e37b7-140">The PHP Manager extension was created using the Visual Studio ASP.NET MVC 4 Web Application template.</span><span class="sxs-lookup"><span data-stu-id="e37b7-140">The PHP Manager extension was created using the Visual Studio ASP.NET MVC 4 Web Application template.</span></span> <span data-ttu-id="e37b7-141">The following view from Solution Explorer shows the structure of the PHP Manager extension.</span><span class="sxs-lookup"><span data-stu-id="e37b7-141">The following view from Solution Explorer shows the structure of the PHP Manager extension.</span></span>

![TransformSiteSolEx][TransformSiteSolEx]

<span data-ttu-id="e37b7-143">The only special logic needed for file I/O is to indicate where the wwwroot directory of the web app is located.</span><span class="sxs-lookup"><span data-stu-id="e37b7-143">The only special logic needed for file I/O is to indicate where the wwwroot directory of the web app is located.</span></span> <span data-ttu-id="e37b7-144">As the following code example shows, the environment variable "HOME" indicates the web app's root path, and the wwwroot path can be constructed by appending "site\wwwroot":</span><span class="sxs-lookup"><span data-stu-id="e37b7-144">As the following code example shows, the environment variable "HOME" indicates the web app's root path, and the wwwroot path can be constructed by appending "site\wwwroot":</span></span>

    /// <summary>
    /// Gives the location of the .user.ini file, even if one doesn't exist yet
    /// </summary>
    private static string GetUserSettingsFilePath()
    {
            var rootPath = Environment.GetEnvironmentVariable("HOME"); // For use on Azure Websites
            if (rootPath == null)
            {
                rootPath = System.IO.Path.GetTempPath(); // For testing purposes
            };
            var userSettingsFile = Path.Combine(rootPath, @"site\wwwroot\.user.ini");
            return userSettingsFile;
    }


<span data-ttu-id="e37b7-145">After you have the directory path, you can use regular file I/O operations to read and write to files.</span><span class="sxs-lookup"><span data-stu-id="e37b7-145">After you have the directory path, you can use regular file I/O operations to read and write to files.</span></span>

<span data-ttu-id="e37b7-146">One point of caution with web app extensions regards the handling of internal links.</span><span class="sxs-lookup"><span data-stu-id="e37b7-146">One point of caution with web app extensions regards the handling of internal links.</span></span>  <span data-ttu-id="e37b7-147">If you have any links in your HTML files that give absolute paths to internal links on your web app, you must ensure those links are prepended with your extension name as your root.</span><span class="sxs-lookup"><span data-stu-id="e37b7-147">If you have any links in your HTML files that give absolute paths to internal links on your web app, you must ensure those links are prepended with your extension name as your root.</span></span> <span data-ttu-id="e37b7-148">This is needed because the root for your extension is now "/`[your-extension-name]`/" rather than being just "/", so any internal links must be updated accordingly.</span><span class="sxs-lookup"><span data-stu-id="e37b7-148">This is needed because the root for your extension is now "/`[your-extension-name]`/" rather than being just "/", so any internal links must be updated accordingly.</span></span> <span data-ttu-id="e37b7-149">For example, suppose your code includes a link to the following:</span><span class="sxs-lookup"><span data-stu-id="e37b7-149">For example, suppose your code includes a link to the following:</span></span>

`"<a href="/Home/Settings">PHP Settings</a>"`

<span data-ttu-id="e37b7-150">When the link is part of a web app extension, the link must be in the following form:</span><span class="sxs-lookup"><span data-stu-id="e37b7-150">When the link is part of a web app extension, the link must be in the following form:</span></span>

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

<span data-ttu-id="e37b7-151">You can work around this requirement by either using only relative paths within your web application, or in the case of ASP.NET applications, by using the `@Html.ActionLink` method which creates the appropriate links for you.</span><span class="sxs-lookup"><span data-stu-id="e37b7-151">You can work around this requirement by either using only relative paths within your web application, or in the case of ASP.NET applications, by using the `@Html.ActionLink` method which creates the appropriate links for you.</span></span>

#### <a id="XDT"></a> <span data-ttu-id="e37b7-152">The applicationHost.xdt file</span><span class="sxs-lookup"><span data-stu-id="e37b7-152">The applicationHost.xdt file</span></span>
<span data-ttu-id="e37b7-153">The code for your web app extension goes under %HOME%\SiteExtensions\[your-extension-name].</span><span class="sxs-lookup"><span data-stu-id="e37b7-153">The code for your web app extension goes under %HOME%\SiteExtensions\[your-extension-name].</span></span> <span data-ttu-id="e37b7-154">We'll call this the extension root.</span><span class="sxs-lookup"><span data-stu-id="e37b7-154">We'll call this the extension root.</span></span>  

<span data-ttu-id="e37b7-155">To register your web app extension with the applicationHost.config file, you need to place a file called ApplicationHost.xdt in the extension root.</span><span class="sxs-lookup"><span data-stu-id="e37b7-155">To register your web app extension with the applicationHost.config file, you need to place a file called ApplicationHost.xdt in the extension root.</span></span> <span data-ttu-id="e37b7-156">The content of the ApplicationHost.xdt file should be as follows:</span><span class="sxs-lookup"><span data-stu-id="e37b7-156">The content of the ApplicationHost.xdt file should be as follows:</span></span>

    <?xml version="1.0"?>
    <configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
          <system.applicationHost>
                <sites>
                      <site name="%XDT_SCMSITENAME%" xdt:Locator="Match(name)">
                        <!-- NOTE: Add your extension name in the application paths below -->
                        <application path="/[your-extension-name]" xdt:Locator="Match(path)" xdt:Transform="Remove" />
                        <application path="/[your-extension-name]" applicationPool="%XDT_APPPOOLNAME%" xdt:Transform="Insert">
                              <virtualDirectory path="/" physicalPath="%XDT_EXTENSIONPATH%" />
                        </application>
                      </site>
                </sites>
          </system.applicationHost>
    </configuration>

<span data-ttu-id="e37b7-157">The name you select as your extension name should have the same name as your extension root folder.</span><span class="sxs-lookup"><span data-stu-id="e37b7-157">The name you select as your extension name should have the same name as your extension root folder.</span></span>

<span data-ttu-id="e37b7-158">This has the effect of adding a new application path to the `system.applicationHost` sites list under the SCM site.</span><span class="sxs-lookup"><span data-stu-id="e37b7-158">This has the effect of adding a new application path to the `system.applicationHost` sites list under the SCM site.</span></span> <span data-ttu-id="e37b7-159">The SCM site is a site administration end point with specific access credentials.</span><span class="sxs-lookup"><span data-stu-id="e37b7-159">The SCM site is a site administration end point with specific access credentials.</span></span> <span data-ttu-id="e37b7-160">It has the URL `https://[your-site-name].scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="e37b7-160">It has the URL `https://[your-site-name].scm.azurewebsites.net`.</span></span>  

    <system.applicationHost>
          ...
          <site name="~1[your-website]" id="1716402716">
                  <bindings>
                    <binding protocol="http" bindingInformation="*:80: [your-website].scm.azurewebsites.net" />
                    <binding protocol="https" bindingInformation="*:443: [your-website].scm.azurewebsites.net" />
                  </bindings>
                  <traceFailedRequestsLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles" />
                  <detailedErrorLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles\DetailedErrors" />
                  <logFile logSiteId="false" />
                  <application path="/" applicationPool="[your-website]">
                    <virtualDirectory path="/" physicalPath="D:\Program Files (x86)\SiteExtensions\Kudu\1.24.20926.5" />
                  </application>
                <!-- Note the custom changes that go here -->
                  <application path="/[your-extension-name]" applicationPool="[your-website]">
                    <virtualDirectory path="/" physicalPath="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\SiteExtensions\[your-extension-name]" />
                  </application>
            </site>
      </sites>
      ...
    </system.applicationHost>

### <a id="deploy"></a> <span data-ttu-id="e37b7-161">Web app extension deployment</span><span class="sxs-lookup"><span data-stu-id="e37b7-161">Web app extension deployment</span></span>
<span data-ttu-id="e37b7-162">To install your web app extension, you can use FTP to copy all the files of your web application to the `\SiteExtensions\[your-extension-name]` folder of the web app on which you want to install the extension.</span><span class="sxs-lookup"><span data-stu-id="e37b7-162">To install your web app extension, you can use FTP to copy all the files of your web application to the `\SiteExtensions\[your-extension-name]` folder of the web app on which you want to install the extension.</span></span>  <span data-ttu-id="e37b7-163">Be sure to copy the ApplicationHost.xdt file to this location as well.</span><span class="sxs-lookup"><span data-stu-id="e37b7-163">Be sure to copy the ApplicationHost.xdt file to this location as well.</span></span> <span data-ttu-id="e37b7-164">Restart your web app to enable the extension.</span><span class="sxs-lookup"><span data-stu-id="e37b7-164">Restart your web app to enable the extension.</span></span>

<span data-ttu-id="e37b7-165">You should be able to see your web app extension at:</span><span class="sxs-lookup"><span data-stu-id="e37b7-165">You should be able to see your web app extension at:</span></span>

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

<span data-ttu-id="e37b7-166">Note that the URL looks just like the URL for your web app, except that it uses HTTPS and contains ".scm".</span><span class="sxs-lookup"><span data-stu-id="e37b7-166">Note that the URL looks just like the URL for your web app, except that it uses HTTPS and contains ".scm".</span></span>

<span data-ttu-id="e37b7-167">It is possible to disable all private (not pre-installed) extensions for your web app during development and investigations by adding an app settings with the key `WEBSITE_PRIVATE_EXTENSIONS` and a value of `0`.</span><span class="sxs-lookup"><span data-stu-id="e37b7-167">It is possible to disable all private (not pre-installed) extensions for your web app during development and investigations by adding an app settings with the key `WEBSITE_PRIVATE_EXTENSIONS` and a value of `0`.</span></span>

> [!NOTE]
> <span data-ttu-id="e37b7-168">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="e37b7-168">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e37b7-169">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="e37b7-169">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="e37b7-170">What's changed</span><span class="sxs-lookup"><span data-stu-id="e37b7-170">What's changed</span></span>
* <span data-ttu-id="e37b7-171">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="e37b7-171">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[TransformSitePHPUI]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-transform-extend/TransformSiteSolEx.png



