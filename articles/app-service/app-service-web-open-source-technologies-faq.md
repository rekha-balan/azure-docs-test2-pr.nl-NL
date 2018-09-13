---
title: Open-source technologies FAQs for Azure web apps | Microsoft Docs
description: Get answers to frequently asked questions about open-source technologies in the Web Apps feature of Azure App Service.
services: app-service\web
documentationcenter: ''
author: genlin
manager: cshepard
editor: ''
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/11/2018
ms.author: genli
ms.openlocfilehash: d65a33dc13d0b91a9ace04dab0be6c37bcd2188f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866745"
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a><span data-ttu-id="c91d2-103">Open-source technologies FAQs for Web Apps in Azure</span><span class="sxs-lookup"><span data-stu-id="c91d2-103">Open-source technologies FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="c91d2-104">This article has answers to frequently asked questions (FAQs) about issues with open-source technologies for the [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="c91d2-104">This article has answers to frequently asked questions (FAQs) about issues with open-source technologies for the [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="how-do-i-turn-on-php-logging-to-troubleshoot-php-issues"></a><span data-ttu-id="c91d2-105">How do I turn on PHP logging to troubleshoot PHP issues?</span><span class="sxs-lookup"><span data-stu-id="c91d2-105">How do I turn on PHP logging to troubleshoot PHP issues?</span></span>

<span data-ttu-id="c91d2-106">To turn on PHP logging:</span><span class="sxs-lookup"><span data-stu-id="c91d2-106">To turn on PHP logging:</span></span>

1. <span data-ttu-id="c91d2-107">Sign in to your [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="c91d2-107">Sign in to your [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="c91d2-108">In the top menu, select **Debug Console** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="c91d2-108">In the top menu, select **Debug Console** > **CMD**.</span></span>
3. <span data-ttu-id="c91d2-109">Select the **Site** folder.</span><span class="sxs-lookup"><span data-stu-id="c91d2-109">Select the **Site** folder.</span></span>
4. <span data-ttu-id="c91d2-110">Select the **wwwroot** folder.</span><span class="sxs-lookup"><span data-stu-id="c91d2-110">Select the **wwwroot** folder.</span></span>
5. <span data-ttu-id="c91d2-111">Select the **+** icon, and then select **New File**.</span><span class="sxs-lookup"><span data-stu-id="c91d2-111">Select the **+** icon, and then select **New File**.</span></span>
6. <span data-ttu-id="c91d2-112">Set the file name to **.user.ini**.</span><span class="sxs-lookup"><span data-stu-id="c91d2-112">Set the file name to **.user.ini**.</span></span>
7. <span data-ttu-id="c91d2-113">Select the pencil icon next to **.user.ini**.</span><span class="sxs-lookup"><span data-stu-id="c91d2-113">Select the pencil icon next to **.user.ini**.</span></span>
8. <span data-ttu-id="c91d2-114">In the file, add this code: `log_errors=on`</span><span class="sxs-lookup"><span data-stu-id="c91d2-114">In the file, add this code: `log_errors=on`</span></span>
9. <span data-ttu-id="c91d2-115">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="c91d2-115">Select **Save**.</span></span>
10. <span data-ttu-id="c91d2-116">Select the pencil icon next to **wp-config.php**.</span><span class="sxs-lookup"><span data-stu-id="c91d2-116">Select the pencil icon next to **wp-config.php**.</span></span>
11. <span data-ttu-id="c91d2-117">Change the text to the following code:</span><span class="sxs-lookup"><span data-stu-id="c91d2-117">Change the text to the following code:</span></span>
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging to /wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings to screendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors to screenini_set('display_errors', 0);
   ```
12. <span data-ttu-id="c91d2-118">In the Azure portal, in the web app menu, restart your web app.</span><span class="sxs-lookup"><span data-stu-id="c91d2-118">In the Azure portal, in the web app menu, restart your web app.</span></span>

<span data-ttu-id="c91d2-119">For more information, see [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span><span class="sxs-lookup"><span data-stu-id="c91d2-119">For more information, see [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a><span data-ttu-id="c91d2-120">How do I log Python application errors in apps that are hosted in App Service?</span><span class="sxs-lookup"><span data-stu-id="c91d2-120">How do I log Python application errors in apps that are hosted in App Service?</span></span>
[!INCLUDE [web-sites-python-troubleshooting-wsgi-error-log](../../includes/web-sites-python-troubleshooting-wsgi-error-log.md)]

## <a name="how-do-i-change-the-version-of-the-nodejs-application-that-is-hosted-in-app-service"></a><span data-ttu-id="c91d2-121">How do I change the version of the Node.js application that is hosted in App Service?</span><span class="sxs-lookup"><span data-stu-id="c91d2-121">How do I change the version of the Node.js application that is hosted in App Service?</span></span>

<span data-ttu-id="c91d2-122">To change the version of the Node.js application, you can use one of the following options:</span><span class="sxs-lookup"><span data-stu-id="c91d2-122">To change the version of the Node.js application, you can use one of the following options:</span></span>

*   <span data-ttu-id="c91d2-123">In the Azure portal, use **App settings**.</span><span class="sxs-lookup"><span data-stu-id="c91d2-123">In the Azure portal, use **App settings**.</span></span>
    1. <span data-ttu-id="c91d2-124">In the Azure portal, go to your web app.</span><span class="sxs-lookup"><span data-stu-id="c91d2-124">In the Azure portal, go to your web app.</span></span>
    2. <span data-ttu-id="c91d2-125">On the **Settings** blade, select **Application settings**.</span><span class="sxs-lookup"><span data-stu-id="c91d2-125">On the **Settings** blade, select **Application settings**.</span></span>
    3. <span data-ttu-id="c91d2-126">In **App settings**, you can include WEBSITE_NODE_DEFAULT_VERSION as the key, and the version of Node.js you want as the value.</span><span class="sxs-lookup"><span data-stu-id="c91d2-126">In **App settings**, you can include WEBSITE_NODE_DEFAULT_VERSION as the key, and the version of Node.js you want as the value.</span></span>
    4. <span data-ttu-id="c91d2-127">Go to your [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="c91d2-127">Go to your [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
    5. <span data-ttu-id="c91d2-128">To check the Node.js version, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="c91d2-128">To check the Node.js version, enter the following command:</span></span>  
   ```
   node -v
   ```
*   <span data-ttu-id="c91d2-129">Modify the iisnode.yml file.</span><span class="sxs-lookup"><span data-stu-id="c91d2-129">Modify the iisnode.yml file.</span></span> <span data-ttu-id="c91d2-130">Changing the Node.js version in the iisnode.yml file only sets the runtime environment that iisnode uses.</span><span class="sxs-lookup"><span data-stu-id="c91d2-130">Changing the Node.js version in the iisnode.yml file only sets the runtime environment that iisnode uses.</span></span> <span data-ttu-id="c91d2-131">Your Kudu cmd and others still use the Node.js version that is set in **App settings** in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c91d2-131">Your Kudu cmd and others still use the Node.js version that is set in **App settings** in the Azure portal.</span></span>

    <span data-ttu-id="c91d2-132">To set the iisnode.yml manually, create an iisnode.yml file in your app root folder.</span><span class="sxs-lookup"><span data-stu-id="c91d2-132">To set the iisnode.yml manually, create an iisnode.yml file in your app root folder.</span></span> <span data-ttu-id="c91d2-133">In the file, include the following line:</span><span class="sxs-lookup"><span data-stu-id="c91d2-133">In the file, include the following line:</span></span>
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   <span data-ttu-id="c91d2-134">Set the iisnode.yml file by using package.json during source control deployment.</span><span class="sxs-lookup"><span data-stu-id="c91d2-134">Set the iisnode.yml file by using package.json during source control deployment.</span></span>
    <span data-ttu-id="c91d2-135">The Azure source control deployment process involves the following steps:</span><span class="sxs-lookup"><span data-stu-id="c91d2-135">The Azure source control deployment process involves the following steps:</span></span>
    1. <span data-ttu-id="c91d2-136">Moves content to the Azure web app.</span><span class="sxs-lookup"><span data-stu-id="c91d2-136">Moves content to the Azure web app.</span></span>
    2. <span data-ttu-id="c91d2-137">Creates a default deployment script, if there isn’t one (deploy.cmd, .deployment files) in the web app root folder.</span><span class="sxs-lookup"><span data-stu-id="c91d2-137">Creates a default deployment script, if there isn’t one (deploy.cmd, .deployment files) in the web app root folder.</span></span>
    3. <span data-ttu-id="c91d2-138">Runs a deployment script in which it creates an iisnode.yml file if you mention the Node.js version in the package.json file > engine `"engines": {"node": "5.9.1","npm": "3.7.3"}`</span><span class="sxs-lookup"><span data-stu-id="c91d2-138">Runs a deployment script in which it creates an iisnode.yml file if you mention the Node.js version in the package.json file > engine `"engines": {"node": "5.9.1","npm": "3.7.3"}`</span></span>
    4. <span data-ttu-id="c91d2-139">The iisnode.yml file has the following line of code:</span><span class="sxs-lookup"><span data-stu-id="c91d2-139">The iisnode.yml file has the following line of code:</span></span>
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-the-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a><span data-ttu-id="c91d2-140">I see the message "Error establishing a database connection" in my WordPress app that's hosted in App Service.</span><span class="sxs-lookup"><span data-stu-id="c91d2-140">I see the message "Error establishing a database connection" in my WordPress app that's hosted in App Service.</span></span> <span data-ttu-id="c91d2-141">How do I troubleshoot this?</span><span class="sxs-lookup"><span data-stu-id="c91d2-141">How do I troubleshoot this?</span></span>

<span data-ttu-id="c91d2-142">If you see this error in your Azure WordPress app, to enable php_errors.log and debug.log, complete the steps detailed in [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span><span class="sxs-lookup"><span data-stu-id="c91d2-142">If you see this error in your Azure WordPress app, to enable php_errors.log and debug.log, complete the steps detailed in [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

<span data-ttu-id="c91d2-143">When the logs are enabled, reproduce the error, and then check the logs to see if you are running out of connections:</span><span class="sxs-lookup"><span data-stu-id="c91d2-143">When the logs are enabled, reproduce the error, and then check the logs to see if you are running out of connections:</span></span>
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded the ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

<span data-ttu-id="c91d2-144">If you see this error in your debug.log or php_errors.log files, your app is exceeding the number of connections.</span><span class="sxs-lookup"><span data-stu-id="c91d2-144">If you see this error in your debug.log or php_errors.log files, your app is exceeding the number of connections.</span></span> <span data-ttu-id="c91d2-145">If you’re hosting on ClearDB, verify the number of connections that are available in your [service plan](https://www.cleardb.com/pricing.view).</span><span class="sxs-lookup"><span data-stu-id="c91d2-145">If you’re hosting on ClearDB, verify the number of connections that are available in your [service plan](https://www.cleardb.com/pricing.view).</span></span>

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a><span data-ttu-id="c91d2-146">How do I debug a Node.js app that's hosted in App Service?</span><span class="sxs-lookup"><span data-stu-id="c91d2-146">How do I debug a Node.js app that's hosted in App Service?</span></span>

1.  <span data-ttu-id="c91d2-147">Go to your [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span><span class="sxs-lookup"><span data-stu-id="c91d2-147">Go to your [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span></span>
2.  <span data-ttu-id="c91d2-148">Go to your application logs folder (D:\home\LogFiles\Application).</span><span class="sxs-lookup"><span data-stu-id="c91d2-148">Go to your application logs folder (D:\home\LogFiles\Application).</span></span>
3.  <span data-ttu-id="c91d2-149">In the logging_errors.txt file, check for content.</span><span class="sxs-lookup"><span data-stu-id="c91d2-149">In the logging_errors.txt file, check for content.</span></span>

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a><span data-ttu-id="c91d2-150">How do I install native Python modules in an App Service web app or API app?</span><span class="sxs-lookup"><span data-stu-id="c91d2-150">How do I install native Python modules in an App Service web app or API app?</span></span>

<span data-ttu-id="c91d2-151">Some packages might not install by using pip in Azure.</span><span class="sxs-lookup"><span data-stu-id="c91d2-151">Some packages might not install by using pip in Azure.</span></span> <span data-ttu-id="c91d2-152">The package might not be available on the Python Package Index, or a compiler might be required (a compiler is not available on the computer that is running the web app in App Service).</span><span class="sxs-lookup"><span data-stu-id="c91d2-152">The package might not be available on the Python Package Index, or a compiler might be required (a compiler is not available on the computer that is running the web app in App Service).</span></span> <span data-ttu-id="c91d2-153">For information about installing native modules in App Service web apps and API apps, see [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span><span class="sxs-lookup"><span data-stu-id="c91d2-153">For information about installing native modules in App Service web apps and API apps, see [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span></span>

## <a name="how-do-i-deploy-a-django-app-to-app-service-by-using-git-and-the-new-version-of-python"></a><span data-ttu-id="c91d2-154">How do I deploy a Django app to App Service by using Git and the new version of Python?</span><span class="sxs-lookup"><span data-stu-id="c91d2-154">How do I deploy a Django app to App Service by using Git and the new version of Python?</span></span>

<span data-ttu-id="c91d2-155">For information about installing Django, see [Deploying a Django app to App Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span><span class="sxs-lookup"><span data-stu-id="c91d2-155">For information about installing Django, see [Deploying a Django app to App Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span></span>

## <a name="where-are-the-tomcat-log-files-located"></a><span data-ttu-id="c91d2-156">Where are the Tomcat log files located?</span><span class="sxs-lookup"><span data-stu-id="c91d2-156">Where are the Tomcat log files located?</span></span>

<span data-ttu-id="c91d2-157">For Azure Marketplace and custom deployments:</span><span class="sxs-lookup"><span data-stu-id="c91d2-157">For Azure Marketplace and custom deployments:</span></span>

* <span data-ttu-id="c91d2-158">Folder location: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span><span class="sxs-lookup"><span data-stu-id="c91d2-158">Folder location: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span></span>
* <span data-ttu-id="c91d2-159">Files of interest:</span><span class="sxs-lookup"><span data-stu-id="c91d2-159">Files of interest:</span></span>
    * <span data-ttu-id="c91d2-160">catalina.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="c91d2-160">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="c91d2-161">host-manager.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="c91d2-161">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="c91d2-162">localhost.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="c91d2-162">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="c91d2-163">manager.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="c91d2-163">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="c91d2-164">site_access_log.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="c91d2-164">site_access_log.*yyyy-mm-dd*.log</span></span>


<span data-ttu-id="c91d2-165">For portal **App settings** deployments:</span><span class="sxs-lookup"><span data-stu-id="c91d2-165">For portal **App settings** deployments:</span></span>

* <span data-ttu-id="c91d2-166">Folder location: D:\home\LogFiles</span><span class="sxs-lookup"><span data-stu-id="c91d2-166">Folder location: D:\home\LogFiles</span></span>
* <span data-ttu-id="c91d2-167">Files of interest:</span><span class="sxs-lookup"><span data-stu-id="c91d2-167">Files of interest:</span></span>
    * <span data-ttu-id="c91d2-168">catalina.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="c91d2-168">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="c91d2-169">host-manager.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="c91d2-169">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="c91d2-170">localhost.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="c91d2-170">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="c91d2-171">manager.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="c91d2-171">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="c91d2-172">site_access_log.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="c91d2-172">site_access_log.*yyyy-mm-dd*.log</span></span>

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a><span data-ttu-id="c91d2-173">How do I troubleshoot JDBC driver connection errors?</span><span class="sxs-lookup"><span data-stu-id="c91d2-173">How do I troubleshoot JDBC driver connection errors?</span></span>

<span data-ttu-id="c91d2-174">You might see the following message in your Tomcat logs:</span><span class="sxs-lookup"><span data-stu-id="c91d2-174">You might see the following message in your Tomcat logs:</span></span>

```
The web application[ROOT] registered the JDBC driver [com.mysql.jdbc.Driver] but failed to unregister it when the web application was stopped. To prevent a memory leak,the JDBC Driver has been forcibly unregistered
```

<span data-ttu-id="c91d2-175">To resolve the error:</span><span class="sxs-lookup"><span data-stu-id="c91d2-175">To resolve the error:</span></span>

1. <span data-ttu-id="c91d2-176">Remove the sqljdbc\*.jar file from your app/lib folder.</span><span class="sxs-lookup"><span data-stu-id="c91d2-176">Remove the sqljdbc\*.jar file from your app/lib folder.</span></span>
2. <span data-ttu-id="c91d2-177">If you are using the custom Tomcat or Azure Marketplace Tomcat web server, copy this .jar file to the Tomcat lib folder.</span><span class="sxs-lookup"><span data-stu-id="c91d2-177">If you are using the custom Tomcat or Azure Marketplace Tomcat web server, copy this .jar file to the Tomcat lib folder.</span></span>
3. <span data-ttu-id="c91d2-178">If you are enabling Java from the Azure portal (select **Java 1.8** > **Tomcat server**), copy the sqljdbc.\* jar file in the folder that's parallel to your app.</span><span class="sxs-lookup"><span data-stu-id="c91d2-178">If you are enabling Java from the Azure portal (select **Java 1.8** > **Tomcat server**), copy the sqljdbc.\* jar file in the folder that's parallel to your app.</span></span> <span data-ttu-id="c91d2-179">Then, add the following classpath setting to the web.config file:</span><span class="sxs-lookup"><span data-stu-id="c91d2-179">Then, add the following classpath setting to the web.config file:</span></span>

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path to the sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-to-copy-live-log-files"></a><span data-ttu-id="c91d2-180">Why do I see errors when I attempt to copy live log files?</span><span class="sxs-lookup"><span data-stu-id="c91d2-180">Why do I see errors when I attempt to copy live log files?</span></span>

<span data-ttu-id="c91d2-181">If you try to copy live log files for a Java app (for example, Tomcat), you might see this FTP error:</span><span class="sxs-lookup"><span data-stu-id="c91d2-181">If you try to copy live log files for a Java app (for example, Tomcat), you might see this FTP error:</span></span>

```
Error transferring file [filename] Copying files from remote side failed.
    
The process cannot access the file because it is being used by another process.
```

<span data-ttu-id="c91d2-182">The error message might vary, depending on the FTP client.</span><span class="sxs-lookup"><span data-stu-id="c91d2-182">The error message might vary, depending on the FTP client.</span></span>

<span data-ttu-id="c91d2-183">All Java apps have this locking issue.</span><span class="sxs-lookup"><span data-stu-id="c91d2-183">All Java apps have this locking issue.</span></span> <span data-ttu-id="c91d2-184">Only Kudu supports downloading this file while the app is running.</span><span class="sxs-lookup"><span data-stu-id="c91d2-184">Only Kudu supports downloading this file while the app is running.</span></span>

<span data-ttu-id="c91d2-185">Stopping the app allows FTP access to these files.</span><span class="sxs-lookup"><span data-stu-id="c91d2-185">Stopping the app allows FTP access to these files.</span></span>

<span data-ttu-id="c91d2-186">Another workaround is to write a WebJob that runs on a schedule and copies these files to a different directory.</span><span class="sxs-lookup"><span data-stu-id="c91d2-186">Another workaround is to write a WebJob that runs on a schedule and copies these files to a different directory.</span></span> <span data-ttu-id="c91d2-187">For a sample project, see the [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) project.</span><span class="sxs-lookup"><span data-stu-id="c91d2-187">For a sample project, see the [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) project.</span></span>

## <a name="where-do-i-find-the-log-files-for-jetty"></a><span data-ttu-id="c91d2-188">Where do I find the log files for Jetty?</span><span class="sxs-lookup"><span data-stu-id="c91d2-188">Where do I find the log files for Jetty?</span></span>

<span data-ttu-id="c91d2-189">For Marketplace and custom deployments, the log file is in the D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs folder.</span><span class="sxs-lookup"><span data-stu-id="c91d2-189">For Marketplace and custom deployments, the log file is in the D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs folder.</span></span> <span data-ttu-id="c91d2-190">Note that the folder location depends on the version of Jetty you are using.</span><span class="sxs-lookup"><span data-stu-id="c91d2-190">Note that the folder location depends on the version of Jetty you are using.</span></span> <span data-ttu-id="c91d2-191">For example, the path provided here is for Jetty 9.1.2.</span><span class="sxs-lookup"><span data-stu-id="c91d2-191">For example, the path provided here is for Jetty 9.1.2.</span></span> <span data-ttu-id="c91d2-192">Look for jetty_*YYYY_MM_DD*.stderrout.log.</span><span class="sxs-lookup"><span data-stu-id="c91d2-192">Look for jetty_*YYYY_MM_DD*.stderrout.log.</span></span>

<span data-ttu-id="c91d2-193">For portal App Setting deployments, the log file is in D:\home\LogFiles.</span><span class="sxs-lookup"><span data-stu-id="c91d2-193">For portal App Setting deployments, the log file is in D:\home\LogFiles.</span></span> <span data-ttu-id="c91d2-194">Look for jetty_*YYYY_MM_DD*.stderrout.log</span><span class="sxs-lookup"><span data-stu-id="c91d2-194">Look for jetty_*YYYY_MM_DD*.stderrout.log</span></span>

## <a name="can-i-send-email-from-my-azure-web-app"></a><span data-ttu-id="c91d2-195">Can I send email from my Azure web app?</span><span class="sxs-lookup"><span data-stu-id="c91d2-195">Can I send email from my Azure web app?</span></span>

<span data-ttu-id="c91d2-196">App Service doesn't have a built-in email feature.</span><span class="sxs-lookup"><span data-stu-id="c91d2-196">App Service doesn't have a built-in email feature.</span></span> <span data-ttu-id="c91d2-197">For some good alternatives for sending email from your app, see this [Stack Overflow discussion](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span><span class="sxs-lookup"><span data-stu-id="c91d2-197">For some good alternatives for sending email from your app, see this [Stack Overflow discussion](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span></span>

## <a name="why-does-my-wordpress-site-redirect-to-another-url"></a><span data-ttu-id="c91d2-198">Why does my WordPress site redirect to another URL?</span><span class="sxs-lookup"><span data-stu-id="c91d2-198">Why does my WordPress site redirect to another URL?</span></span>

<span data-ttu-id="c91d2-199">If you have recently migrated to Azure, WordPress might redirect to the old domain URL.</span><span class="sxs-lookup"><span data-stu-id="c91d2-199">If you have recently migrated to Azure, WordPress might redirect to the old domain URL.</span></span> <span data-ttu-id="c91d2-200">This is caused by a setting in the MySQL database.</span><span class="sxs-lookup"><span data-stu-id="c91d2-200">This is caused by a setting in the MySQL database.</span></span>

<span data-ttu-id="c91d2-201">WordPress Buddy+ is an Azure Site Extension that you can use to update the redirection URL directly in the database.</span><span class="sxs-lookup"><span data-stu-id="c91d2-201">WordPress Buddy+ is an Azure Site Extension that you can use to update the redirection URL directly in the database.</span></span> <span data-ttu-id="c91d2-202">For more information about using WordPress Buddy+, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="c91d2-202">For more information about using WordPress Buddy+, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

<span data-ttu-id="c91d2-203">Alternatively, if you prefer to manually update the redirection URL by using SQL queries or PHPMyAdmin, see [WordPress: Redirecting to wrong URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span><span class="sxs-lookup"><span data-stu-id="c91d2-203">Alternatively, if you prefer to manually update the redirection URL by using SQL queries or PHPMyAdmin, see [WordPress: Redirecting to wrong URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span></span>

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a><span data-ttu-id="c91d2-204">How do I change my WordPress sign-in password?</span><span class="sxs-lookup"><span data-stu-id="c91d2-204">How do I change my WordPress sign-in password?</span></span>

<span data-ttu-id="c91d2-205">If you have forgotten your WordPress sign-in password, you can use WordPress Buddy+ to update it.</span><span class="sxs-lookup"><span data-stu-id="c91d2-205">If you have forgotten your WordPress sign-in password, you can use WordPress Buddy+ to update it.</span></span> <span data-ttu-id="c91d2-206">To reset your password, install the WordPress Buddy+ Azure Site Extension, and then complete the steps described in [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="c91d2-206">To reset your password, install the WordPress Buddy+ Azure Site Extension, and then complete the steps described in [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="i-cant-sign-in-to-wordpress-how-do-i-resolve-this"></a><span data-ttu-id="c91d2-207">I can't sign in to WordPress.</span><span class="sxs-lookup"><span data-stu-id="c91d2-207">I can't sign in to WordPress.</span></span> <span data-ttu-id="c91d2-208">How do I resolve this?</span><span class="sxs-lookup"><span data-stu-id="c91d2-208">How do I resolve this?</span></span>

<span data-ttu-id="c91d2-209">If you find yourself locked out of WordPress after recently installing a plugin, you might have a faulty plugin.</span><span class="sxs-lookup"><span data-stu-id="c91d2-209">If you find yourself locked out of WordPress after recently installing a plugin, you might have a faulty plugin.</span></span> <span data-ttu-id="c91d2-210">WordPress Buddy+ is an Azure Site Extension that can help you disable plugins in WordPress.</span><span class="sxs-lookup"><span data-stu-id="c91d2-210">WordPress Buddy+ is an Azure Site Extension that can help you disable plugins in WordPress.</span></span> <span data-ttu-id="c91d2-211">For more information, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="c91d2-211">For more information, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="how-do-i-migrate-my-wordpress-database"></a><span data-ttu-id="c91d2-212">How do I migrate my WordPress database?</span><span class="sxs-lookup"><span data-stu-id="c91d2-212">How do I migrate my WordPress database?</span></span>

<span data-ttu-id="c91d2-213">You have multiple options for migrating the MySQL database that's connected to your WordPress website:</span><span class="sxs-lookup"><span data-stu-id="c91d2-213">You have multiple options for migrating the MySQL database that's connected to your WordPress website:</span></span>

* <span data-ttu-id="c91d2-214">Developers: Use the [command prompt or PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span><span class="sxs-lookup"><span data-stu-id="c91d2-214">Developers: Use the [command prompt or PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span></span>
* <span data-ttu-id="c91d2-215">Non-developers: Use [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span><span class="sxs-lookup"><span data-stu-id="c91d2-215">Non-developers: Use [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span></span>

## <a name="how-do-i-help-make-wordpress-more-secure"></a><span data-ttu-id="c91d2-216">How do I help make WordPress more secure?</span><span class="sxs-lookup"><span data-stu-id="c91d2-216">How do I help make WordPress more secure?</span></span>

<span data-ttu-id="c91d2-217">To learn about security best practices for WordPress, see [Best practices for WordPress security in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span><span class="sxs-lookup"><span data-stu-id="c91d2-217">To learn about security best practices for WordPress, see [Best practices for WordPress security in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span></span>

## <a name="i-am-trying-to-use-phpmyadmin-and-i-see-the-message-access-denied-how-do-i-resolve-this"></a><span data-ttu-id="c91d2-218">I am trying to use PHPMyAdmin, and I see the message “Access denied.”</span><span class="sxs-lookup"><span data-stu-id="c91d2-218">I am trying to use PHPMyAdmin, and I see the message “Access denied.”</span></span> <span data-ttu-id="c91d2-219">How do I resolve this?</span><span class="sxs-lookup"><span data-stu-id="c91d2-219">How do I resolve this?</span></span>

<span data-ttu-id="c91d2-220">You might experience this issue if the MySQL in-app feature isn't running yet in this App Service instance.</span><span class="sxs-lookup"><span data-stu-id="c91d2-220">You might experience this issue if the MySQL in-app feature isn't running yet in this App Service instance.</span></span> <span data-ttu-id="c91d2-221">To resolve the issue, try to access your website.</span><span class="sxs-lookup"><span data-stu-id="c91d2-221">To resolve the issue, try to access your website.</span></span> <span data-ttu-id="c91d2-222">This starts the required processes, including the MySQL in-app process.</span><span class="sxs-lookup"><span data-stu-id="c91d2-222">This starts the required processes, including the MySQL in-app process.</span></span> <span data-ttu-id="c91d2-223">To verify that MySQL in-app is running, in Process Explorer, ensure that mysqld.exe is listed in the processes.</span><span class="sxs-lookup"><span data-stu-id="c91d2-223">To verify that MySQL in-app is running, in Process Explorer, ensure that mysqld.exe is listed in the processes.</span></span>

<span data-ttu-id="c91d2-224">After you ensure that MySQL in-app is running, try to use PHPMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="c91d2-224">After you ensure that MySQL in-app is running, try to use PHPMyAdmin.</span></span>

## <a name="i-get-an-http-403-error-when-i-try-to-import-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a><span data-ttu-id="c91d2-225">I get an HTTP 403 error when I try to import or export my MySQL in-app database by using PHPMyadmin.</span><span class="sxs-lookup"><span data-stu-id="c91d2-225">I get an HTTP 403 error when I try to import or export my MySQL in-app database by using PHPMyadmin.</span></span> <span data-ttu-id="c91d2-226">How do I resolve this?</span><span class="sxs-lookup"><span data-stu-id="c91d2-226">How do I resolve this?</span></span>

<span data-ttu-id="c91d2-227">If you are using an older version of Chrome, you might be experiencing a known bug.</span><span class="sxs-lookup"><span data-stu-id="c91d2-227">If you are using an older version of Chrome, you might be experiencing a known bug.</span></span> <span data-ttu-id="c91d2-228">To resolve the issue, upgrade to a newer version of Chrome.</span><span class="sxs-lookup"><span data-stu-id="c91d2-228">To resolve the issue, upgrade to a newer version of Chrome.</span></span> <span data-ttu-id="c91d2-229">Also try using a different browser, like Internet Explorer or Edge, where the issue does not occur.</span><span class="sxs-lookup"><span data-stu-id="c91d2-229">Also try using a different browser, like Internet Explorer or Edge, where the issue does not occur.</span></span>
