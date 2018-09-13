---
title: Buid a Django app on an Azure VM | Microsoft Docs
description: This tutorial teaches you how to host a Django-based website on Azure using a Windows Server 2012 R2 Datacenter virtual machine using the classic deployment model.
services: virtual-machines-windows
documentationcenter: python
author: huguesv
manager: wpickett
editor: ''
tags: azure-service-management
ms.assetid: e36484d1-afbf-47f5-b755-5e65397dc1c3
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: python
ms.topic: article
ms.date: 08/04/2015
ms.author: huvalo
ms.openlocfilehash: a7ed3e2650cdc878f19b25888ac6522ece17c0b9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550980"
---
# <a name="django-hello-world-web-application-on-a-windows-server-vm"></a><span data-ttu-id="f48ea-103">Django Hello World web application on a Windows Server VM</span><span class="sxs-lookup"><span data-stu-id="f48ea-103">Django Hello World web application on a Windows Server VM</span></span>
> [!div class="op_single_selector"]
> * [Windows](python-django-web-app.md)
> * [Mac/Linux](../../linux/python-django-web-app.md)
> 
> 

<br>

> [!IMPORTANT] 
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model. For a Resource Manager template to deploy Django, see [here](https://azure.microsoft.com/documentation/templates/django-app/).

<span data-ttu-id="f48ea-110">This tutorial describes how to host a Django-based website on Microsoft Azure using a Windows Server virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f48ea-110">This tutorial describes how to host a Django-based website on Microsoft Azure using a Windows Server virtual machine.</span></span> <span data-ttu-id="f48ea-111">This tutorial assumes you have no prior experience using Azure.</span><span class="sxs-lookup"><span data-stu-id="f48ea-111">This tutorial assumes you have no prior experience using Azure.</span></span> <span data-ttu-id="f48ea-112">After completing this tutorial, you will have a Django-based application up and running in the cloud.</span><span class="sxs-lookup"><span data-stu-id="f48ea-112">After completing this tutorial, you will have a Django-based application up and running in the cloud.</span></span>

<span data-ttu-id="f48ea-113">You will learn how to:</span><span class="sxs-lookup"><span data-stu-id="f48ea-113">You will learn how to:</span></span>

* <span data-ttu-id="f48ea-114">Set up an Azure virtual machine to host Django.</span><span class="sxs-lookup"><span data-stu-id="f48ea-114">Set up an Azure virtual machine to host Django.</span></span> <span data-ttu-id="f48ea-115">While this tutorial explains how to accomplish this under Windows Server, the same could also be done with a Linux VM hosted in Azure.</span><span class="sxs-lookup"><span data-stu-id="f48ea-115">While this tutorial explains how to accomplish this under Windows Server, the same could also be done with a Linux VM hosted in Azure.</span></span>
* <span data-ttu-id="f48ea-116">Create a new Django application from Windows.</span><span class="sxs-lookup"><span data-stu-id="f48ea-116">Create a new Django application from Windows.</span></span>

<span data-ttu-id="f48ea-117">By following this tutorial, you will build a simple Hello World web application.</span><span class="sxs-lookup"><span data-stu-id="f48ea-117">By following this tutorial, you will build a simple Hello World web application.</span></span> <span data-ttu-id="f48ea-118">The application will be hosted in an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f48ea-118">The application will be hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="f48ea-119">A screenshot of the completed application appears next.</span><span class="sxs-lookup"><span data-stu-id="f48ea-119">A screenshot of the completed application appears next.</span></span>

![A browser window displaying the hello world page on Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="creating-and-configuring-an-azure-virtual-machine-to-host-django"></a><span data-ttu-id="f48ea-121">Creating and configuring an Azure virtual machine to host Django</span><span class="sxs-lookup"><span data-stu-id="f48ea-121">Creating and configuring an Azure virtual machine to host Django</span></span>
1. <span data-ttu-id="f48ea-122">Follow the instructions given [here](tutorial.md) to create an Azure virtual machine of the Windows Server 2012 R2 Datacenter distribution.</span><span class="sxs-lookup"><span data-stu-id="f48ea-122">Follow the instructions given [here](tutorial.md) to create an Azure virtual machine of the Windows Server 2012 R2 Datacenter distribution.</span></span>
2. <span data-ttu-id="f48ea-123">Instruct Azure to direct port 80 traffic from the web to port 80 on the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="f48ea-123">Instruct Azure to direct port 80 traffic from the web to port 80 on the virtual machine:</span></span>
   
   * <span data-ttu-id="f48ea-124">Navigate to your newly created virtual machine in the Azure classic portal and click the **ENDPOINTS** tab.</span><span class="sxs-lookup"><span data-stu-id="f48ea-124">Navigate to your newly created virtual machine in the Azure classic portal and click the **ENDPOINTS** tab.</span></span>
   * <span data-ttu-id="f48ea-125">Click the **ADD** button at the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="f48ea-125">Click the **ADD** button at the bottom of the screen.</span></span>
     <span data-ttu-id="f48ea-126">![add endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/python-django-web-app/django-helloworld-addendpoint.png)</span><span class="sxs-lookup"><span data-stu-id="f48ea-126">![add endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/python-django-web-app/django-helloworld-addendpoint.png)</span></span>
   * <span data-ttu-id="f48ea-127">Open up the **TCP** protocol's **PUBLIC PORT 80** as **PRIVATE PORT 80**.</span><span class="sxs-lookup"><span data-stu-id="f48ea-127">Open up the **TCP** protocol's **PUBLIC PORT 80** as **PRIVATE PORT 80**.</span></span>
     ![][port80]
3. <span data-ttu-id="f48ea-128">From the **DASHBOARD** tab, click **CONNECT** to use **Remote Desktop** to remotely log into the newly created Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f48ea-128">From the **DASHBOARD** tab, click **CONNECT** to use **Remote Desktop** to remotely log into the newly created Azure virtual machine.</span></span>  

<span data-ttu-id="f48ea-129">**Important Note:** All instructions below assume you logged into the virtual machine correctly and are issuing commands there rather than your local machine.</span><span class="sxs-lookup"><span data-stu-id="f48ea-129">**Important Note:** All instructions below assume you logged into the virtual machine correctly and are issuing commands there rather than your local machine.</span></span>

## <span data-ttu-id="f48ea-130"><a id="setup"> </a>Installing Python, Django, WFastCGI</span><span class="sxs-lookup"><span data-stu-id="f48ea-130"><a id="setup"> </a>Installing Python, Django, WFastCGI</span></span>
<span data-ttu-id="f48ea-131">**Note:** In order to download using Internet Explorer you may have to configure IE ESC settings (Start/Administrative Tools/Server Manager/Local Server, then click  **IE Enhanced Security Configuration**, set to Off).</span><span class="sxs-lookup"><span data-stu-id="f48ea-131">**Note:** In order to download using Internet Explorer you may have to configure IE ESC settings (Start/Administrative Tools/Server Manager/Local Server, then click  **IE Enhanced Security Configuration**, set to Off).</span></span>

1. <span data-ttu-id="f48ea-132">Install the latest Python 2.7 or 3.4 from [python.org][python.org].</span><span class="sxs-lookup"><span data-stu-id="f48ea-132">Install the latest Python 2.7 or 3.4 from [python.org][python.org].</span></span>
2. <span data-ttu-id="f48ea-133">Install the wfastcgi and django packages using pip.</span><span class="sxs-lookup"><span data-stu-id="f48ea-133">Install the wfastcgi and django packages using pip.</span></span>
   
    <span data-ttu-id="f48ea-134">For Python 2.7, use the following command.</span><span class="sxs-lookup"><span data-stu-id="f48ea-134">For Python 2.7, use the following command.</span></span>
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    <span data-ttu-id="f48ea-135">For Python 3.4, use the following command.</span><span class="sxs-lookup"><span data-stu-id="f48ea-135">For Python 3.4, use the following command.</span></span>
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="installing-iis-with-fastcgi"></a><span data-ttu-id="f48ea-136">Installing IIS with FastCGI</span><span class="sxs-lookup"><span data-stu-id="f48ea-136">Installing IIS with FastCGI</span></span>
1. <span data-ttu-id="f48ea-137">Install IIS with FastCGI support.</span><span class="sxs-lookup"><span data-stu-id="f48ea-137">Install IIS with FastCGI support.</span></span>  <span data-ttu-id="f48ea-138">This may take several minutes to execute.</span><span class="sxs-lookup"><span data-stu-id="f48ea-138">This may take several minutes to execute.</span></span>
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="creating-a-new-django-application"></a><span data-ttu-id="f48ea-139">Creating a new Django application</span><span class="sxs-lookup"><span data-stu-id="f48ea-139">Creating a new Django application</span></span>
1. <span data-ttu-id="f48ea-140">From *C:\inetpub\wwwroot*, enter the following command to create a new Django project:</span><span class="sxs-lookup"><span data-stu-id="f48ea-140">From *C:\inetpub\wwwroot*, enter the following command to create a new Django project:</span></span>
   
   <span data-ttu-id="f48ea-141">For Python 2.7, use the following command.</span><span class="sxs-lookup"><span data-stu-id="f48ea-141">For Python 2.7, use the following command.</span></span>
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   <span data-ttu-id="f48ea-142">For Python 3.4, use the following command.</span><span class="sxs-lookup"><span data-stu-id="f48ea-142">For Python 3.4, use the following command.</span></span>
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![The result of the New-AzureService command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. <span data-ttu-id="f48ea-144">The **django-admin** command generates a basic structure for Django-based websites:</span><span class="sxs-lookup"><span data-stu-id="f48ea-144">The **django-admin** command generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="f48ea-145">**helloworld\manage.py** helps you to start hosting and stop hosting your Django-based website</span><span class="sxs-lookup"><span data-stu-id="f48ea-145">**helloworld\manage.py** helps you to start hosting and stop hosting your Django-based website</span></span>
   * <span data-ttu-id="f48ea-146">**helloworld\helloworld\settings.py** contains Django settings for your application.</span><span class="sxs-lookup"><span data-stu-id="f48ea-146">**helloworld\helloworld\settings.py** contains Django settings for your application.</span></span>
   * <span data-ttu-id="f48ea-147">**helloworld\helloworld\urls.py** contains the mapping code between each url and its view.</span><span class="sxs-lookup"><span data-stu-id="f48ea-147">**helloworld\helloworld\urls.py** contains the mapping code between each url and its view.</span></span>
3. <span data-ttu-id="f48ea-148">Create a new file named **views.py** in the *C:\inetpub\wwwroot\helloworld\helloworld* directory.</span><span class="sxs-lookup"><span data-stu-id="f48ea-148">Create a new file named **views.py** in the *C:\inetpub\wwwroot\helloworld\helloworld* directory.</span></span> <span data-ttu-id="f48ea-149">This will contain the view that renders the "hello world" page.</span><span class="sxs-lookup"><span data-stu-id="f48ea-149">This will contain the view that renders the "hello world" page.</span></span> <span data-ttu-id="f48ea-150">Start your editor and enter the following:</span><span class="sxs-lookup"><span data-stu-id="f48ea-150">Start your editor and enter the following:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="f48ea-151">Replace the contents of the urls.py file with the following.</span><span class="sxs-lookup"><span data-stu-id="f48ea-151">Replace the contents of the urls.py file with the following.</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="configuring-iis"></a><span data-ttu-id="f48ea-152">Configuring IIS</span><span class="sxs-lookup"><span data-stu-id="f48ea-152">Configuring IIS</span></span>
1. <span data-ttu-id="f48ea-153">Unlock the handlers section in the global applicationhost.config.  This will enable the use of the python handler in your web.config.</span><span class="sxs-lookup"><span data-stu-id="f48ea-153">Unlock the handlers section in the global applicationhost.config.  This will enable the use of the python handler in your web.config.</span></span>
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. <span data-ttu-id="f48ea-154">Enable WFastCGI.</span><span class="sxs-lookup"><span data-stu-id="f48ea-154">Enable WFastCGI.</span></span>  <span data-ttu-id="f48ea-155">This will add an application to the global applicationhost.config that refers to your Python interpreter executable and the wfastcgi.py script.</span><span class="sxs-lookup"><span data-stu-id="f48ea-155">This will add an application to the global applicationhost.config that refers to your Python interpreter executable and the wfastcgi.py script.</span></span>
   
    <span data-ttu-id="f48ea-156">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="f48ea-156">Python 2.7:</span></span>
   
        c:\python27\scripts\wfastcgi-enable
   
    <span data-ttu-id="f48ea-157">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="f48ea-157">Python 3.4:</span></span>
   
        c:\python34\scripts\wfastcgi-enable
3. <span data-ttu-id="f48ea-158">Create a web.config file in *C:\inetpub\wwwroot\helloworld*.</span><span class="sxs-lookup"><span data-stu-id="f48ea-158">Create a web.config file in *C:\inetpub\wwwroot\helloworld*.</span></span>  <span data-ttu-id="f48ea-159">The value of the `scriptProcessor` attribute should match the output of the previous step.</span><span class="sxs-lookup"><span data-stu-id="f48ea-159">The value of the `scriptProcessor` attribute should match the output of the previous step.</span></span>  <span data-ttu-id="f48ea-160">See the page for [wfastcgi][wfastcgi] on pypi for more on wfastcgi settings.</span><span class="sxs-lookup"><span data-stu-id="f48ea-160">See the page for [wfastcgi][wfastcgi] on pypi for more on wfastcgi settings.</span></span>
   
    <span data-ttu-id="f48ea-161">Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="f48ea-161">Python 2.7:</span></span>
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python27\python.exe|C:\Python27\Lib\site-packages\wfastcgi.pyc" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
   
    <span data-ttu-id="f48ea-162">Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="f48ea-162">Python 3.4:</span></span>
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python34\python.exe|C:\Python34\Lib\site-packages\wfastcgi.py" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
4. <span data-ttu-id="f48ea-163">Update the location of the IIS Default Web Site to point to the django project folder.</span><span class="sxs-lookup"><span data-stu-id="f48ea-163">Update the location of the IIS Default Web Site to point to the django project folder.</span></span>
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. <span data-ttu-id="f48ea-164">Finally, load the web page in your browser.</span><span class="sxs-lookup"><span data-stu-id="f48ea-164">Finally, load the web page in your browser.</span></span>

![A browser window displaying the hello world page on Azure][1]

## <a name="shutting-down-your-azure-virtual-machine"></a><span data-ttu-id="f48ea-166">Shutting down your Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="f48ea-166">Shutting down your Azure virtual machine</span></span>
<span data-ttu-id="f48ea-167">When you're done with this tutorial, shut down and/or remove your newly created Azure virtual machine to free up resources for other tutorials and avoid incurring Azure usage charges.</span><span class="sxs-lookup"><span data-stu-id="f48ea-167">When you're done with this tutorial, shut down and/or remove your newly created Azure virtual machine to free up resources for other tutorials and avoid incurring Azure usage charges.</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi




