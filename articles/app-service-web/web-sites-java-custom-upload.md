---
title: Upload a custom Java web app to Azure
description: This tutorial shows you how to upload a custom Java web app to Azure App Service Web Apps.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: eb2ccd83-e5c6-444e-a0fc-08fd5cc8326c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: 2114b22bf4c5ad7dad524dfb0b64c92ebb6dee9f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563888"
---
# <a name="upload-a-custom-java-web-app-to-azure"></a><span data-ttu-id="41776-103">Upload a custom Java web app to Azure</span><span class="sxs-lookup"><span data-stu-id="41776-103">Upload a custom Java web app to Azure</span></span>
<span data-ttu-id="41776-104">This topic explains how to upload a custom Java web app to [Azure App Service] Web Apps.</span><span class="sxs-lookup"><span data-stu-id="41776-104">This topic explains how to upload a custom Java web app to [Azure App Service] Web Apps.</span></span> <span data-ttu-id="41776-105">Included is information that applies to any Java website or web app, and also some examples for specific applications.</span><span class="sxs-lookup"><span data-stu-id="41776-105">Included is information that applies to any Java website or web app, and also some examples for specific applications.</span></span>

<span data-ttu-id="41776-106">Note that Azure provides a means for creating Java web apps using the Azure Portal's configuration UI, and the Azure Marketplace, as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="41776-106">Note that Azure provides a means for creating Java web apps using the Azure Portal's configuration UI, and the Azure Marketplace, as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md).</span></span> <span data-ttu-id="41776-107">This tutorial is for scenarios in which you do not want to use the Azure Portal configuration UI or the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="41776-107">This tutorial is for scenarios in which you do not want to use the Azure Portal configuration UI or the Azure Marketplace.</span></span>  

## <a name="configuration-guidelines"></a><span data-ttu-id="41776-108">Configuration guidelines</span><span class="sxs-lookup"><span data-stu-id="41776-108">Configuration guidelines</span></span>
<span data-ttu-id="41776-109">The following describes the settings expected for custom Java web apps on Azure.</span><span class="sxs-lookup"><span data-stu-id="41776-109">The following describes the settings expected for custom Java web apps on Azure.</span></span>

* <span data-ttu-id="41776-110">The HTTP port used by the Java process is dynamically assigned.</span><span class="sxs-lookup"><span data-stu-id="41776-110">The HTTP port used by the Java process is dynamically assigned.</span></span>  <span data-ttu-id="41776-111">The process must use the port from the environment variable `HTTP_PLATFORM_PORT`.</span><span class="sxs-lookup"><span data-stu-id="41776-111">The process must use the port from the environment variable `HTTP_PLATFORM_PORT`.</span></span>
* <span data-ttu-id="41776-112">All listen ports other than the single HTTP listener should be disabled.</span><span class="sxs-lookup"><span data-stu-id="41776-112">All listen ports other than the single HTTP listener should be disabled.</span></span>  <span data-ttu-id="41776-113">In Tomcat, that includes the shutdown, HTTPS, and AJP ports.</span><span class="sxs-lookup"><span data-stu-id="41776-113">In Tomcat, that includes the shutdown, HTTPS, and AJP ports.</span></span>
* <span data-ttu-id="41776-114">The container needs to be configured for IPv4 traffic only.</span><span class="sxs-lookup"><span data-stu-id="41776-114">The container needs to be configured for IPv4 traffic only.</span></span>
* <span data-ttu-id="41776-115">The **startup** command for the application needs to be set in the configuration.</span><span class="sxs-lookup"><span data-stu-id="41776-115">The **startup** command for the application needs to be set in the configuration.</span></span>
* <span data-ttu-id="41776-116">Applications that require directories with write permission need to be located in the Azure web app's content directory,  which is **D:\home**.</span><span class="sxs-lookup"><span data-stu-id="41776-116">Applications that require directories with write permission need to be located in the Azure web app's content directory,  which is **D:\home**.</span></span>  <span data-ttu-id="41776-117">The environmental variable `HOME` refers to D:\home.</span><span class="sxs-lookup"><span data-stu-id="41776-117">The environmental variable `HOME` refers to D:\home.</span></span>  

<span data-ttu-id="41776-118">You can set environment variables as required in the web.config file.</span><span class="sxs-lookup"><span data-stu-id="41776-118">You can set environment variables as required in the web.config file.</span></span>

## <a name="webconfig-httpplatform-configuration"></a><span data-ttu-id="41776-119">web.config httpPlatform configuration</span><span class="sxs-lookup"><span data-stu-id="41776-119">web.config httpPlatform configuration</span></span>
<span data-ttu-id="41776-120">The following information describes the **httpPlatform** format within web.config.</span><span class="sxs-lookup"><span data-stu-id="41776-120">The following information describes the **httpPlatform** format within web.config.</span></span>

<span data-ttu-id="41776-121">**arguments** (Default="").</span><span class="sxs-lookup"><span data-stu-id="41776-121">**arguments** (Default="").</span></span> <span data-ttu-id="41776-122">Arguments to the executable or script specified in the **processPath** setting.</span><span class="sxs-lookup"><span data-stu-id="41776-122">Arguments to the executable or script specified in the **processPath** setting.</span></span>

<span data-ttu-id="41776-123">Examples (shown with **processPath** included):</span><span class="sxs-lookup"><span data-stu-id="41776-123">Examples (shown with **processPath** included):</span></span>

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


<span data-ttu-id="41776-124">**processPath** - Path to the executable or script that will launch a process listening for HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="41776-124">**processPath** - Path to the executable or script that will launch a process listening for HTTP requests.</span></span>

<span data-ttu-id="41776-125">Examples:</span><span class="sxs-lookup"><span data-stu-id="41776-125">Examples:</span></span>

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

<span data-ttu-id="41776-126">**rapidFailsPerMinute** (Default=10.) Number of times the process specified in **processPath** is allowed to crash per minute.</span><span class="sxs-lookup"><span data-stu-id="41776-126">**rapidFailsPerMinute** (Default=10.) Number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="41776-127">If this limit is exceeded, **HttpPlatformHandler** will stop launching the process for the remainder of the minute.</span><span class="sxs-lookup"><span data-stu-id="41776-127">If this limit is exceeded, **HttpPlatformHandler** will stop launching the process for the remainder of the minute.</span></span>

<span data-ttu-id="41776-128">**requestTimeout** (Default="00:02:00".) Duration for which **HttpPlatformHandler** will wait for a response from the process listening on `%HTTP_PLATFORM_PORT%`.</span><span class="sxs-lookup"><span data-stu-id="41776-128">**requestTimeout** (Default="00:02:00".) Duration for which **HttpPlatformHandler** will wait for a response from the process listening on `%HTTP_PLATFORM_PORT%`.</span></span>

<span data-ttu-id="41776-129">**startupRetryCount** (Default=10.) Number of times **HttpPlatformHandler** will try to launch the process specified in **processPath**.</span><span class="sxs-lookup"><span data-stu-id="41776-129">**startupRetryCount** (Default=10.) Number of times **HttpPlatformHandler** will try to launch the process specified in **processPath**.</span></span> <span data-ttu-id="41776-130">See **startupTimeLimit** for more details.</span><span class="sxs-lookup"><span data-stu-id="41776-130">See **startupTimeLimit** for more details.</span></span>

<span data-ttu-id="41776-131">**startupTimeLimit** (Default=10 seconds.) Duration for which **HttpPlatformHandler** will wait for the executable/script to start a process listening on the port.</span><span class="sxs-lookup"><span data-stu-id="41776-131">**startupTimeLimit** (Default=10 seconds.) Duration for which **HttpPlatformHandler** will wait for the executable/script to start a process listening on the port.</span></span>  <span data-ttu-id="41776-132">If this time limit is exceeded, **HttpPlatformHandler** will kill the process and try to launch it again **startupRetryCount** times.</span><span class="sxs-lookup"><span data-stu-id="41776-132">If this time limit is exceeded, **HttpPlatformHandler** will kill the process and try to launch it again **startupRetryCount** times.</span></span>

<span data-ttu-id="41776-133">**stdoutLogEnabled** (Default="true".) If true, **stdout** and **stderr** for the process specified in the **processPath** setting will be redirected to the file specified in **stdoutLogFile** (see **stdoutLogFile** section).</span><span class="sxs-lookup"><span data-stu-id="41776-133">**stdoutLogEnabled** (Default="true".) If true, **stdout** and **stderr** for the process specified in the **processPath** setting will be redirected to the file specified in **stdoutLogFile** (see **stdoutLogFile** section).</span></span>

<span data-ttu-id="41776-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Absolute file path for which **stdout** and **stderr** from the process specified in **processPath** will be logged.</span><span class="sxs-lookup"><span data-stu-id="41776-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Absolute file path for which **stdout** and **stderr** from the process specified in **processPath** will be logged.</span></span>

> [!NOTE]
> <span data-ttu-id="41776-135">`%HTTP_PLATFORM_PORT%` is a special placeholder which needs to specified either as part of **arguments** or as part of the **httpPlatform** **environmentVariables** list.</span><span class="sxs-lookup"><span data-stu-id="41776-135">`%HTTP_PLATFORM_PORT%` is a special placeholder which needs to specified either as part of **arguments** or as part of the **httpPlatform** **environmentVariables** list.</span></span> <span data-ttu-id="41776-136">This will be replaced by an internally generated port by **HttpPlatformHandler** so that the process specified by **processPath** can listen on this port.</span><span class="sxs-lookup"><span data-stu-id="41776-136">This will be replaced by an internally generated port by **HttpPlatformHandler** so that the process specified by **processPath** can listen on this port.</span></span>
> 
> 

## <a name="deployment"></a><span data-ttu-id="41776-137">Deployment</span><span class="sxs-lookup"><span data-stu-id="41776-137">Deployment</span></span>
<span data-ttu-id="41776-138">Java based web apps can be deployed easily through most of the same means that are used with the Internet Information Services (IIS) based web applications.</span><span class="sxs-lookup"><span data-stu-id="41776-138">Java based web apps can be deployed easily through most of the same means that are used with the Internet Information Services (IIS) based web applications.</span></span>  <span data-ttu-id="41776-139">FTP, Git and Kudu are all supported as deployment mechanisms, as is the integrated SCM capability for web apps.</span><span class="sxs-lookup"><span data-stu-id="41776-139">FTP, Git and Kudu are all supported as deployment mechanisms, as is the integrated SCM capability for web apps.</span></span> <span data-ttu-id="41776-140">WebDeploy works as a protocol, however, as Java is not developed in Visual Studio, WebDeploy does not fit with Java web app deployment use cases.</span><span class="sxs-lookup"><span data-stu-id="41776-140">WebDeploy works as a protocol, however, as Java is not developed in Visual Studio, WebDeploy does not fit with Java web app deployment use cases.</span></span>

## <a name="application-configuration-examples"></a><span data-ttu-id="41776-141">Application configuration Examples</span><span class="sxs-lookup"><span data-stu-id="41776-141">Application configuration Examples</span></span>
<span data-ttu-id="41776-142">For the following applications, a web.config file and the application configuration is provided as examples to show how to enable your Java application on App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="41776-142">For the following applications, a web.config file and the application configuration is provided as examples to show how to enable your Java application on App Service Web Apps.</span></span>

### <a name="tomcat"></a><span data-ttu-id="41776-143">Tomcat</span><span class="sxs-lookup"><span data-stu-id="41776-143">Tomcat</span></span>
<span data-ttu-id="41776-144">While there are two variations on Tomcat that are supplied with App Service Web Apps, it is still quite possible to upload customer specific instances.</span><span class="sxs-lookup"><span data-stu-id="41776-144">While there are two variations on Tomcat that are supplied with App Service Web Apps, it is still quite possible to upload customer specific instances.</span></span> <span data-ttu-id="41776-145">Below is an example of an install of Tomcat with a different Java Virtual Machine (JVM).</span><span class="sxs-lookup"><span data-stu-id="41776-145">Below is an example of an install of Tomcat with a different Java Virtual Machine (JVM).</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat" 
            arguments="">
          <environmentVariables>
            <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
            <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\bin\tomcat" />
            <environmentVariable name="JRE_HOME" value="%HOME%\site\wwwroot\bin\java" /> <!-- optional, if not specified, this will default to %programfiles%\Java -->
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="41776-146">On the Tomcat side, there are a few configuration changes that need to be made.</span><span class="sxs-lookup"><span data-stu-id="41776-146">On the Tomcat side, there are a few configuration changes that need to be made.</span></span> <span data-ttu-id="41776-147">The server.xml needs to be edited to set:</span><span class="sxs-lookup"><span data-stu-id="41776-147">The server.xml needs to be edited to set:</span></span>

* <span data-ttu-id="41776-148">Shutdown port = -1</span><span class="sxs-lookup"><span data-stu-id="41776-148">Shutdown port = -1</span></span>
* <span data-ttu-id="41776-149">HTTP connector port = ${port.http}</span><span class="sxs-lookup"><span data-stu-id="41776-149">HTTP connector port = ${port.http}</span></span>
* <span data-ttu-id="41776-150">HTTP connector address = "127.0.0.1"</span><span class="sxs-lookup"><span data-stu-id="41776-150">HTTP connector address = "127.0.0.1"</span></span>
* <span data-ttu-id="41776-151">Comment out HTTPS and AJP connectors</span><span class="sxs-lookup"><span data-stu-id="41776-151">Comment out HTTPS and AJP connectors</span></span>
* <span data-ttu-id="41776-152">The IPv4 setting can also be set in the catalina.properties file where you can add     `java.net.preferIPv4Stack=true`</span><span class="sxs-lookup"><span data-stu-id="41776-152">The IPv4 setting can also be set in the catalina.properties file where you can add     `java.net.preferIPv4Stack=true`</span></span>

<span data-ttu-id="41776-153">Direct3d calls are not supported on App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="41776-153">Direct3d calls are not supported on App Service Web Apps.</span></span> <span data-ttu-id="41776-154">To disable those, add the following Java option should your application make such calls: `-Dsun.java2d.d3d=false`</span><span class="sxs-lookup"><span data-stu-id="41776-154">To disable those, add the following Java option should your application make such calls: `-Dsun.java2d.d3d=false`</span></span>

### <a name="jetty"></a><span data-ttu-id="41776-155">Jetty</span><span class="sxs-lookup"><span data-stu-id="41776-155">Jetty</span></span>
<span data-ttu-id="41776-156">As is the case for Tomcat, customers can upload their own instances for Jetty.</span><span class="sxs-lookup"><span data-stu-id="41776-156">As is the case for Tomcat, customers can upload their own instances for Jetty.</span></span> <span data-ttu-id="41776-157">In the case of running the full install of Jetty, the configuration would look like this:</span><span class="sxs-lookup"><span data-stu-id="41776-157">In the case of running the full install of Jetty, the configuration would look like this:</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httppPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe" 
             arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP_PLATFORM_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"
            startupTimeLimit="20"
          startupRetryCount="10"
          stdoutLogEnabled="true">
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="41776-158">The Jetty configuration needs to be changed in the start.ini to set `java.net.preferIPv4Stack=true`.</span><span class="sxs-lookup"><span data-stu-id="41776-158">The Jetty configuration needs to be changed in the start.ini to set `java.net.preferIPv4Stack=true`.</span></span>

### <a name="springboot"></a><span data-ttu-id="41776-159">Springboot</span><span class="sxs-lookup"><span data-stu-id="41776-159">Springboot</span></span>
<span data-ttu-id="41776-160">In order to get a Springboot application running you need to upload your JAR or WAR file and add the following web.config file.</span><span class="sxs-lookup"><span data-stu-id="41776-160">In order to get a Springboot application running you need to upload your JAR or WAR file and add the following web.config file.</span></span> <span data-ttu-id="41776-161">The web.config file goes into the wwwroot folder.</span><span class="sxs-lookup"><span data-stu-id="41776-161">The web.config file goes into the wwwroot folder.</span></span> <span data-ttu-id="41776-162">In the web.config adjust the arguments to point to your JAR file, in the following example the JAR file is located in the wwwroot folder as well.</span><span class="sxs-lookup"><span data-stu-id="41776-162">In the web.config adjust the arguments to point to your JAR file, in the following example the JAR file is located in the wwwroot folder as well.</span></span>  

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
            arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\my-web-project.jar&quot;">
        </httpPlatform>
      </system.webServer>
    </configuration>


### <a name="hudson"></a><span data-ttu-id="41776-163">Hudson</span><span class="sxs-lookup"><span data-stu-id="41776-163">Hudson</span></span>
<span data-ttu-id="41776-164">Our test used the Hudson 3.1.2 war and the default Tomcat 7.0.50 instance but without using the UI to set things up.</span><span class="sxs-lookup"><span data-stu-id="41776-164">Our test used the Hudson 3.1.2 war and the default Tomcat 7.0.50 instance but without using the UI to set things up.</span></span>  <span data-ttu-id="41776-165">Because Hudson is a software build tool, it is advised to install it on dedicated instances where the **AlwaysOn** flag can be set on the web app.</span><span class="sxs-lookup"><span data-stu-id="41776-165">Because Hudson is a software build tool, it is advised to install it on dedicated instances where the **AlwaysOn** flag can be set on the web app.</span></span>

1. <span data-ttu-id="41776-166">In your web app’s root directory, i.e., **d:\home\site\wwwroot**, create a **webapps** directory (if not already present), and place Hudson.war in **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="41776-166">In your web app’s root directory, i.e., **d:\home\site\wwwroot**, create a **webapps** directory (if not already present), and place Hudson.war in **d:\home\site\wwwroot\webapps**.</span></span>
2. <span data-ttu-id="41776-167">Download apache maven 3.0.5 (compatible with Hudson) and place it in **d:\home\site\wwwroot**.</span><span class="sxs-lookup"><span data-stu-id="41776-167">Download apache maven 3.0.5 (compatible with Hudson) and place it in **d:\home\site\wwwroot**.</span></span>
3. <span data-ttu-id="41776-168">Create web.config in **d:\home\site\wwwroot** and paste the following contents in it:</span><span class="sxs-lookup"><span data-stu-id="41776-168">Create web.config in **d:\home\site\wwwroot** and paste the following contents in it:</span></span>
   
        <?xml version="1.0" encoding="UTF-8"?>
        <configuration>
          <system.webServer>
            <handlers>
              <add name="httppPlatformHandler" path="*" verb="*" 
        modules="httpPlatformHandler" resourceType="Unspecified" />
            </handlers>
            <httpPlatform processPath="%AZURE_TOMCAT7_HOME%\bin\startup.bat"
        startupTimeLimit="20"
        startupRetryCount="10">
        <environmentVariables>
          <environmentVariable name="HUDSON_HOME" 
        value="%HOME%\site\wwwroot\hudson_home" />
          <environmentVariable name="JAVA_OPTS" 
        value="-Djava.net.preferIPv4Stack=true -Duser.home=%HOME%/site/wwwroot/user_home -Dhudson.DNSMultiCast.disabled=true" />
        </environmentVariables>            
            </httpPlatform>
          </system.webServer>
        </configuration>
   
    <span data-ttu-id="41776-169">At this point the web app can be restarted to take the changes.</span><span class="sxs-lookup"><span data-stu-id="41776-169">At this point the web app can be restarted to take the changes.</span></span>  <span data-ttu-id="41776-170">Connect to http://yourwebapp/hudson to start Hudson.</span><span class="sxs-lookup"><span data-stu-id="41776-170">Connect to http://yourwebapp/hudson to start Hudson.</span></span>
4. <span data-ttu-id="41776-171">After Hudson configures itself, you should see the following screen:</span><span class="sxs-lookup"><span data-stu-id="41776-171">After Hudson configures itself, you should see the following screen:</span></span>
   
    ![Hudson](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-java-custom-upload/hudson1.png)
5. <span data-ttu-id="41776-173">Access the Hudson configuration page: Click **Manage Hudson**, and then click **Configure System**.</span><span class="sxs-lookup"><span data-stu-id="41776-173">Access the Hudson configuration page: Click **Manage Hudson**, and then click **Configure System**.</span></span>
6. <span data-ttu-id="41776-174">Configure the JDK as shown below:</span><span class="sxs-lookup"><span data-stu-id="41776-174">Configure the JDK as shown below:</span></span>
   
    ![Hudson configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-java-custom-upload/hudson2.png)
7. <span data-ttu-id="41776-176">Configure Maven as shown below:</span><span class="sxs-lookup"><span data-stu-id="41776-176">Configure Maven as shown below:</span></span>
   
    ![Maven configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-java-custom-upload/maven.png)
8. <span data-ttu-id="41776-178">Save the settings.</span><span class="sxs-lookup"><span data-stu-id="41776-178">Save the settings.</span></span> <span data-ttu-id="41776-179">Hudson should now be configured and ready for use.</span><span class="sxs-lookup"><span data-stu-id="41776-179">Hudson should now be configured and ready for use.</span></span>

<span data-ttu-id="41776-180">For additional information on Hudson, see [http://hudson-ci.org](http://hudson-ci.org).</span><span class="sxs-lookup"><span data-stu-id="41776-180">For additional information on Hudson, see [http://hudson-ci.org](http://hudson-ci.org).</span></span>

### <a name="liferay"></a><span data-ttu-id="41776-181">Liferay</span><span class="sxs-lookup"><span data-stu-id="41776-181">Liferay</span></span>
<span data-ttu-id="41776-182">Liferay is supported on App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="41776-182">Liferay is supported on App Service Web Apps.</span></span> <span data-ttu-id="41776-183">Since Liferay can require significant memory, the web app needs to run on a medium or large dedicated worker, which can provide enough memory.</span><span class="sxs-lookup"><span data-stu-id="41776-183">Since Liferay can require significant memory, the web app needs to run on a medium or large dedicated worker, which can provide enough memory.</span></span> <span data-ttu-id="41776-184">Liferay also takes several minutes to start up.</span><span class="sxs-lookup"><span data-stu-id="41776-184">Liferay also takes several minutes to start up.</span></span> <span data-ttu-id="41776-185">For that reason, it is recommended that you set the web app to **Always On**.</span><span class="sxs-lookup"><span data-stu-id="41776-185">For that reason, it is recommended that you set the web app to **Always On**.</span></span>  

<span data-ttu-id="41776-186">Using Liferay 6.1.2 Community Edition GA3 bundled with Tomcat, the following files were edited after downloading Liferay:</span><span class="sxs-lookup"><span data-stu-id="41776-186">Using Liferay 6.1.2 Community Edition GA3 bundled with Tomcat, the following files were edited after downloading Liferay:</span></span>

<span data-ttu-id="41776-187">**Server.xml**</span><span class="sxs-lookup"><span data-stu-id="41776-187">**Server.xml**</span></span>

* <span data-ttu-id="41776-188">Change Shutdown port to -1.</span><span class="sxs-lookup"><span data-stu-id="41776-188">Change Shutdown port to -1.</span></span>
* <span data-ttu-id="41776-189">Change HTTP connector to       `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span><span class="sxs-lookup"><span data-stu-id="41776-189">Change HTTP connector to       `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span></span>
* <span data-ttu-id="41776-190">Comment out the AJP connector.</span><span class="sxs-lookup"><span data-stu-id="41776-190">Comment out the AJP connector.</span></span>

<span data-ttu-id="41776-191">In the **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** folder, create a file named **portal-ext.properties**.</span><span class="sxs-lookup"><span data-stu-id="41776-191">In the **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** folder, create a file named **portal-ext.properties**.</span></span> <span data-ttu-id="41776-192">This file needs to contain one line, as shown here:</span><span class="sxs-lookup"><span data-stu-id="41776-192">This file needs to contain one line, as shown here:</span></span>

    liferay.home=%HOME%/site/wwwroot/liferay

<span data-ttu-id="41776-193">At the same directory level as the tomcat-7.0.40 folder, create a file named **web.config** with the following content:</span><span class="sxs-lookup"><span data-stu-id="41776-193">At the same directory level as the tomcat-7.0.40 folder, create a file named **web.config** with the following content:</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
    <add name="httpPlatformHandler" path="*" verb="*"
         modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\tomcat-7.0.40\bin\catalina.bat" 
                      arguments="run" 
                      startupTimeLimit="10" 
                      requestTimeout="00:10:00" 
                      stdoutLogEnabled="true">
          <environmentVariables>
      <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
      <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\tomcat-7.0.40" />
            <environmentVariable name="JRE_HOME" value="D:\Program Files\Java\jdk1.7.0_51" /> 
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="41776-194">Under the **httpPlatform** block, the **requestTimeout** is set to “00:10:00”.</span><span class="sxs-lookup"><span data-stu-id="41776-194">Under the **httpPlatform** block, the **requestTimeout** is set to “00:10:00”.</span></span>  <span data-ttu-id="41776-195">It can be reduced but then you are likely to see some timeout errors while Liferay is bootstrapping.</span><span class="sxs-lookup"><span data-stu-id="41776-195">It can be reduced but then you are likely to see some timeout errors while Liferay is bootstrapping.</span></span>  <span data-ttu-id="41776-196">If this value is changed, then the **connectionTimeout** in the tomcat server.xml should also be modified.</span><span class="sxs-lookup"><span data-stu-id="41776-196">If this value is changed, then the **connectionTimeout** in the tomcat server.xml should also be modified.</span></span>  

<span data-ttu-id="41776-197">It is worth noting that the JRE_HOME environnment varariable is specified in the above web.config to point to the 64-bit JDK.</span><span class="sxs-lookup"><span data-stu-id="41776-197">It is worth noting that the JRE_HOME environnment varariable is specified in the above web.config to point to the 64-bit JDK.</span></span> <span data-ttu-id="41776-198">The default is 32-bit, but since Liferay may require high levels of memory, it is recommended to use the 64-bit JDK.</span><span class="sxs-lookup"><span data-stu-id="41776-198">The default is 32-bit, but since Liferay may require high levels of memory, it is recommended to use the 64-bit JDK.</span></span>

<span data-ttu-id="41776-199">Once you make these changes, restart your web app running Liferay, Then, open http://yourwebapp.</span><span class="sxs-lookup"><span data-stu-id="41776-199">Once you make these changes, restart your web app running Liferay, Then, open http://yourwebapp.</span></span> <span data-ttu-id="41776-200">The Liferay portal is available from the web app root.</span><span class="sxs-lookup"><span data-stu-id="41776-200">The Liferay portal is available from the web app root.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="41776-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="41776-201">Next steps</span></span>
<span data-ttu-id="41776-202">For more information about Liferay, see [http://www.liferay.com](http://www.liferay.com).</span><span class="sxs-lookup"><span data-stu-id="41776-202">For more information about Liferay, see [http://www.liferay.com](http://www.liferay.com).</span></span>

<span data-ttu-id="41776-203">For more information about Java, see the [Java Developer Center](/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="41776-203">For more information about Java, see the [Java Developer Center](/develop/java/).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714



