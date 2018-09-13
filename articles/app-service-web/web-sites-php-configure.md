---
title: Configure PHP in Azure App Service Web Apps | Microsoft Docs
description: Learn how to configure the default PHP installation or add a custom PHP installation for Web Apps in Azure App Service.
services: app-service
documentationcenter: php
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: 95c4072b-8570-496b-9c48-ee21a223fb60
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/16/2016
ms.author: robmcm
ms.openlocfilehash: 4156a27f40641fe34658a8aaed0ba677fac8da17
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550748"
---
# <a name="configure-php-in-azure-app-service-web-apps"></a><span data-ttu-id="8c495-103">Configure PHP in Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="8c495-103">Configure PHP in Azure App Service Web Apps</span></span>
## <a name="introduction"></a><span data-ttu-id="8c495-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="8c495-104">Introduction</span></span>
<span data-ttu-id="8c495-105">This guide will show you how to configure the built-in PHP runtime for Web Apps in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), provide a custom PHP runtime, and enable extensions.</span><span class="sxs-lookup"><span data-stu-id="8c495-105">This guide will show you how to configure the built-in PHP runtime for Web Apps in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), provide a custom PHP runtime, and enable extensions.</span></span> <span data-ttu-id="8c495-106">To use App Service, sign up for the [free trial].</span><span class="sxs-lookup"><span data-stu-id="8c495-106">To use App Service, sign up for the [free trial].</span></span> <span data-ttu-id="8c495-107">To get the most from this guide, you should first create a PHP web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="8c495-107">To get the most from this guide, you should first create a PHP web app in App Service.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-the-built-in-php-version"></a><span data-ttu-id="8c495-108">How to: Change the built-in PHP version</span><span class="sxs-lookup"><span data-stu-id="8c495-108">How to: Change the built-in PHP version</span></span>
<span data-ttu-id="8c495-109">By default, PHP 5.5 is installed and immediately available for use when you create an App Service web app.</span><span class="sxs-lookup"><span data-stu-id="8c495-109">By default, PHP 5.5 is installed and immediately available for use when you create an App Service web app.</span></span> <span data-ttu-id="8c495-110">The best way to see the available release revision, its default configuration, and the enabled extensions is to deploy a script that calls the [phpinfo()] function.</span><span class="sxs-lookup"><span data-stu-id="8c495-110">The best way to see the available release revision, its default configuration, and the enabled extensions is to deploy a script that calls the [phpinfo()] function.</span></span>

<span data-ttu-id="8c495-111">PHP 5.6 and PHP 7.0 versions are also available, but not enabled by default.</span><span class="sxs-lookup"><span data-stu-id="8c495-111">PHP 5.6 and PHP 7.0 versions are also available, but not enabled by default.</span></span> <span data-ttu-id="8c495-112">To update the PHP version, follow one of these methods:</span><span class="sxs-lookup"><span data-stu-id="8c495-112">To update the PHP version, follow one of these methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="8c495-113">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8c495-113">Azure Portal</span></span>
1. <span data-ttu-id="8c495-114">Browse to your web app in the [Azure Portal](https://portal.azure.com) and click on the **Settings** button.</span><span class="sxs-lookup"><span data-stu-id="8c495-114">Browse to your web app in the [Azure Portal](https://portal.azure.com) and click on the **Settings** button.</span></span>
   
    ![Web App Settings][settings-button]
2. <span data-ttu-id="8c495-116">From the **Settings** blade select **Application Settings** and choose the new PHP version.</span><span class="sxs-lookup"><span data-stu-id="8c495-116">From the **Settings** blade select **Application Settings** and choose the new PHP version.</span></span>
   
    ![Application Settings][application-settings]
3. <span data-ttu-id="8c495-118">Click the **Save** button at the top of the **Web app settings** blade.</span><span class="sxs-lookup"><span data-stu-id="8c495-118">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![Save configuration settings][save-button]

### <a name="azure-powershell-windows"></a><span data-ttu-id="8c495-120">Azure PowerShell (Windows)</span><span class="sxs-lookup"><span data-stu-id="8c495-120">Azure PowerShell (Windows)</span></span>
1. <span data-ttu-id="8c495-121">Open Azure PowerShell, and login to your account:</span><span class="sxs-lookup"><span data-stu-id="8c495-121">Open Azure PowerShell, and login to your account:</span></span>
   
        PS C:\> Login-AzureRmAccount
2. <span data-ttu-id="8c495-122">Set the PHP version for the web app.</span><span class="sxs-lookup"><span data-stu-id="8c495-122">Set the PHP version for the web app.</span></span>
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. <span data-ttu-id="8c495-123">The PHP version is now set.</span><span class="sxs-lookup"><span data-stu-id="8c495-123">The PHP version is now set.</span></span> <span data-ttu-id="8c495-124">You can confirm these settings:</span><span class="sxs-lookup"><span data-stu-id="8c495-124">You can confirm these settings:</span></span>
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a><span data-ttu-id="8c495-125">Azure Command-Line Interface (Linux, Mac, Windows)</span><span class="sxs-lookup"><span data-stu-id="8c495-125">Azure Command-Line Interface (Linux, Mac, Windows)</span></span>
<span data-ttu-id="8c495-126">To use the Azure Command-Line Interface, you must have **Node.js** installed on your computer.</span><span class="sxs-lookup"><span data-stu-id="8c495-126">To use the Azure Command-Line Interface, you must have **Node.js** installed on your computer.</span></span>

1. <span data-ttu-id="8c495-127">Open Terminal, and login to your account.</span><span class="sxs-lookup"><span data-stu-id="8c495-127">Open Terminal, and login to your account.</span></span>
   
        azure login
2. <span data-ttu-id="8c495-128">Set the PHP version for the web app.</span><span class="sxs-lookup"><span data-stu-id="8c495-128">Set the PHP version for the web app.</span></span>
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. <span data-ttu-id="8c495-129">The PHP version is now set.</span><span class="sxs-lookup"><span data-stu-id="8c495-129">The PHP version is now set.</span></span> <span data-ttu-id="8c495-130">You can confirm these settings:</span><span class="sxs-lookup"><span data-stu-id="8c495-130">You can confirm these settings:</span></span>
   
        azure site show {app-name}

> [!NOTE] 
> <span data-ttu-id="8c495-131">The [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands that are equivalent to the above are:</span><span class="sxs-lookup"><span data-stu-id="8c495-131">The [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands that are equivalent to the above are:</span></span>
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-the-built-in-php-configurations"></a><span data-ttu-id="8c495-132">How to: Change the built-in PHP configurations</span><span class="sxs-lookup"><span data-stu-id="8c495-132">How to: Change the built-in PHP configurations</span></span>
<span data-ttu-id="8c495-133">For any built-in PHP runtime, you can change any of the configuration options by following the steps below.</span><span class="sxs-lookup"><span data-stu-id="8c495-133">For any built-in PHP runtime, you can change any of the configuration options by following the steps below.</span></span> <span data-ttu-id="8c495-134">(For information about php.ini directives, see [List of php.ini directives].)</span><span class="sxs-lookup"><span data-stu-id="8c495-134">(For information about php.ini directives, see [List of php.ini directives].)</span></span>

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a><span data-ttu-id="8c495-135">Changing PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL configuration settings</span><span class="sxs-lookup"><span data-stu-id="8c495-135">Changing PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL configuration settings</span></span>
1. <span data-ttu-id="8c495-136">Add a [.user.ini] file to your root directory.</span><span class="sxs-lookup"><span data-stu-id="8c495-136">Add a [.user.ini] file to your root directory.</span></span>
2. <span data-ttu-id="8c495-137">Add configuration settings to the `.user.ini` file using the same syntax you would use in a `php.ini` file.</span><span class="sxs-lookup"><span data-stu-id="8c495-137">Add configuration settings to the `.user.ini` file using the same syntax you would use in a `php.ini` file.</span></span> <span data-ttu-id="8c495-138">For example, if you wanted to turn the `display_errors` setting on and set `upload_max_filesize` setting to 10M, your `.user.ini` file would contain this text:</span><span class="sxs-lookup"><span data-stu-id="8c495-138">For example, if you wanted to turn the `display_errors` setting on and set `upload_max_filesize` setting to 10M, your `.user.ini` file would contain this text:</span></span>
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on to write errors to d:\home\LogFiles\php_errors.log
        ; log_errors=On
3. <span data-ttu-id="8c495-139">Deploy your web app.</span><span class="sxs-lookup"><span data-stu-id="8c495-139">Deploy your web app.</span></span>
4. <span data-ttu-id="8c495-140">Restart the web app.</span><span class="sxs-lookup"><span data-stu-id="8c495-140">Restart the web app.</span></span> <span data-ttu-id="8c495-141">(Restarting is necessary because the frequency with which PHP reads `.user.ini` files is governed by the `user_ini.cache_ttl` setting, which is a system level setting and is 300 seconds (5 minutes) by default.</span><span class="sxs-lookup"><span data-stu-id="8c495-141">(Restarting is necessary because the frequency with which PHP reads `.user.ini` files is governed by the `user_ini.cache_ttl` setting, which is a system level setting and is 300 seconds (5 minutes) by default.</span></span> <span data-ttu-id="8c495-142">Restarting the web app forces PHP to read the new settings in the `.user.ini` file.)</span><span class="sxs-lookup"><span data-stu-id="8c495-142">Restarting the web app forces PHP to read the new settings in the `.user.ini` file.)</span></span>

<span data-ttu-id="8c495-143">As an alternative to using a `.user.ini` file, you can use the [ini_set()] function in scripts to set configuration options that are not system-level directives.</span><span class="sxs-lookup"><span data-stu-id="8c495-143">As an alternative to using a `.user.ini` file, you can use the [ini_set()] function in scripts to set configuration options that are not system-level directives.</span></span>

### <a name="changing-phpinisystem-configuration-settings"></a><span data-ttu-id="8c495-144">Changing PHP\_INI\_SYSTEM configuration settings</span><span class="sxs-lookup"><span data-stu-id="8c495-144">Changing PHP\_INI\_SYSTEM configuration settings</span></span>
1. <span data-ttu-id="8c495-145">Add an App Setting to your Web App with the key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="8c495-145">Add an App Setting to your Web App with the key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
2. <span data-ttu-id="8c495-146">Create an `settings.ini` file using Kudu Console (http://&lt;site-name&gt;.scm.azurewebsite.net) in the `d:\home\site\ini` directory.</span><span class="sxs-lookup"><span data-stu-id="8c495-146">Create an `settings.ini` file using Kudu Console (http://&lt;site-name&gt;.scm.azurewebsite.net) in the `d:\home\site\ini` directory.</span></span>
3. <span data-ttu-id="8c495-147">Add configuration settings to the `settings.ini` file using the same syntax you would use in a php.ini file.</span><span class="sxs-lookup"><span data-stu-id="8c495-147">Add configuration settings to the `settings.ini` file using the same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="8c495-148">For example, if you wanted to point the `curl.cainfo` setting to a `*.crt` file and set 'wincache.maxfilesize' setting to 512K, your `settings.ini` file would contain this text:</span><span class="sxs-lookup"><span data-stu-id="8c495-148">For example, if you wanted to point the `curl.cainfo` setting to a `*.crt` file and set 'wincache.maxfilesize' setting to 512K, your `settings.ini` file would contain this text:</span></span>
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. <span data-ttu-id="8c495-149">Restart your Web App to load the changes.</span><span class="sxs-lookup"><span data-stu-id="8c495-149">Restart your Web App to load the changes.</span></span>

## <a name="how-to-enable-extensions-in-the-default-php-runtime"></a><span data-ttu-id="8c495-150">How to: Enable extensions in the default PHP runtime</span><span class="sxs-lookup"><span data-stu-id="8c495-150">How to: Enable extensions in the default PHP runtime</span></span>
<span data-ttu-id="8c495-151">As noted in the previous section, the best way to see the default PHP version, its default configuration, and the enabled extensions is to deploy a script that calls [phpinfo()].</span><span class="sxs-lookup"><span data-stu-id="8c495-151">As noted in the previous section, the best way to see the default PHP version, its default configuration, and the enabled extensions is to deploy a script that calls [phpinfo()].</span></span> <span data-ttu-id="8c495-152">To enable additional extensions, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="8c495-152">To enable additional extensions, follow the steps below:</span></span>

### <a name="configure-via-ini-settings"></a><span data-ttu-id="8c495-153">Configure via ini settings</span><span class="sxs-lookup"><span data-stu-id="8c495-153">Configure via ini settings</span></span>
1. <span data-ttu-id="8c495-154">Add a `ext` directory to the `d:\home\site` directory.</span><span class="sxs-lookup"><span data-stu-id="8c495-154">Add a `ext` directory to the `d:\home\site` directory.</span></span>
2. <span data-ttu-id="8c495-155">Put `.dll` extension files in the `ext` directory (for example, `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="8c495-155">Put `.dll` extension files in the `ext` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="8c495-156">Make sure that the extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span><span class="sxs-lookup"><span data-stu-id="8c495-156">Make sure that the extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="8c495-157">Add an App Setting to your Web App with the key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="8c495-157">Add an App Setting to your Web App with the key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
4. <span data-ttu-id="8c495-158">Create an `ini` file in `d:\home\site\ini` called `extensions.ini`.</span><span class="sxs-lookup"><span data-stu-id="8c495-158">Create an `ini` file in `d:\home\site\ini` called `extensions.ini`.</span></span>
5. <span data-ttu-id="8c495-159">Add configuration settings to the `extensions.ini` file using the same syntax you would use in a php.ini file.</span><span class="sxs-lookup"><span data-stu-id="8c495-159">Add configuration settings to the `extensions.ini` file using the same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="8c495-160">For example, if you wanted to enable the MongoDB and XDebug extensions, your `extensions.ini` file would contain this text:</span><span class="sxs-lookup"><span data-stu-id="8c495-160">For example, if you wanted to enable the MongoDB and XDebug extensions, your `extensions.ini` file would contain this text:</span></span>
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. <span data-ttu-id="8c495-161">Restart your Web App to load the changes.</span><span class="sxs-lookup"><span data-stu-id="8c495-161">Restart your Web App to load the changes.</span></span>

### <a name="configure-via-app-setting"></a><span data-ttu-id="8c495-162">Configure via App Setting</span><span class="sxs-lookup"><span data-stu-id="8c495-162">Configure via App Setting</span></span>
1. <span data-ttu-id="8c495-163">Add a `bin` directory to the root directory.</span><span class="sxs-lookup"><span data-stu-id="8c495-163">Add a `bin` directory to the root directory.</span></span>
2. <span data-ttu-id="8c495-164">Put `.dll` extension files in the `bin` directory (for example, `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="8c495-164">Put `.dll` extension files in the `bin` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="8c495-165">Make sure that the extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span><span class="sxs-lookup"><span data-stu-id="8c495-165">Make sure that the extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="8c495-166">Deploy your web app.</span><span class="sxs-lookup"><span data-stu-id="8c495-166">Deploy your web app.</span></span>
4. <span data-ttu-id="8c495-167">Browse to your web app in the Azure Portal and click on the **Settings** button.</span><span class="sxs-lookup"><span data-stu-id="8c495-167">Browse to your web app in the Azure Portal and click on the **Settings** button.</span></span>
   
    ![Web App Settings][settings-button]
5. <span data-ttu-id="8c495-169">From the **Settings** blade select **Application Settings** and scroll to the **App settings** section.</span><span class="sxs-lookup"><span data-stu-id="8c495-169">From the **Settings** blade select **Application Settings** and scroll to the **App settings** section.</span></span>
6. <span data-ttu-id="8c495-170">In the **App settings** section, create a **PHP_EXTENSIONS** key.</span><span class="sxs-lookup"><span data-stu-id="8c495-170">In the **App settings** section, create a **PHP_EXTENSIONS** key.</span></span> <span data-ttu-id="8c495-171">The value for this key would be a path relative to website root: **bin\your-ext-file**.</span><span class="sxs-lookup"><span data-stu-id="8c495-171">The value for this key would be a path relative to website root: **bin\your-ext-file**.</span></span>
   
    ![Enable extension in app settings][php-extensions]
7. <span data-ttu-id="8c495-173">Click the **Save** button at the top of the **Web app settings** blade.</span><span class="sxs-lookup"><span data-stu-id="8c495-173">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![Save configuration settings][save-button]

<span data-ttu-id="8c495-175">Zend extensions are also supported by using a **PHP_ZENDEXTENSIONS** key.</span><span class="sxs-lookup"><span data-stu-id="8c495-175">Zend extensions are also supported by using a **PHP_ZENDEXTENSIONS** key.</span></span> <span data-ttu-id="8c495-176">To enable multiple extensions, include a comma-separated list of `.dll` files for the app setting value.</span><span class="sxs-lookup"><span data-stu-id="8c495-176">To enable multiple extensions, include a comma-separated list of `.dll` files for the app setting value.</span></span>

## <a name="how-to-use-a-custom-php-runtime"></a><span data-ttu-id="8c495-177">How to: Use a custom PHP runtime</span><span class="sxs-lookup"><span data-stu-id="8c495-177">How to: Use a custom PHP runtime</span></span>
<span data-ttu-id="8c495-178">Instead of the default PHP runtime, App Service Web Apps can use a PHP runtime that you provide to execute PHP scripts.</span><span class="sxs-lookup"><span data-stu-id="8c495-178">Instead of the default PHP runtime, App Service Web Apps can use a PHP runtime that you provide to execute PHP scripts.</span></span> <span data-ttu-id="8c495-179">The runtime that you provide can be configured by a `php.ini` file that you also provide.</span><span class="sxs-lookup"><span data-stu-id="8c495-179">The runtime that you provide can be configured by a `php.ini` file that you also provide.</span></span> <span data-ttu-id="8c495-180">To use a custom PHP runtime with Web Apps, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="8c495-180">To use a custom PHP runtime with Web Apps, follow the steps below.</span></span>

1. <span data-ttu-id="8c495-181">Obtain a non-thread-safe, VC9 or VC11 compatible version of PHP for Windows.</span><span class="sxs-lookup"><span data-stu-id="8c495-181">Obtain a non-thread-safe, VC9 or VC11 compatible version of PHP for Windows.</span></span> <span data-ttu-id="8c495-182">Recent releases of PHP for Windows can be found here: [http://windows.php.net/download/].</span><span class="sxs-lookup"><span data-stu-id="8c495-182">Recent releases of PHP for Windows can be found here: [http://windows.php.net/download/].</span></span> <span data-ttu-id="8c495-183">Older releases can be found in the archive here: [http://windows.php.net/downloads/releases/archives/].</span><span class="sxs-lookup"><span data-stu-id="8c495-183">Older releases can be found in the archive here: [http://windows.php.net/downloads/releases/archives/].</span></span>
2. <span data-ttu-id="8c495-184">Modify the `php.ini` file for your runtime.</span><span class="sxs-lookup"><span data-stu-id="8c495-184">Modify the `php.ini` file for your runtime.</span></span> <span data-ttu-id="8c495-185">Note that any configuration settings that are system-level-only directives will be ignored by Web Apps.</span><span class="sxs-lookup"><span data-stu-id="8c495-185">Note that any configuration settings that are system-level-only directives will be ignored by Web Apps.</span></span> <span data-ttu-id="8c495-186">(For information about system-level-only directives, see [List of php.ini directives]).</span><span class="sxs-lookup"><span data-stu-id="8c495-186">(For information about system-level-only directives, see [List of php.ini directives]).</span></span>
3. <span data-ttu-id="8c495-187">Optionally, add extensions to your PHP runtime and enable them in the `php.ini` file.</span><span class="sxs-lookup"><span data-stu-id="8c495-187">Optionally, add extensions to your PHP runtime and enable them in the `php.ini` file.</span></span>
4. <span data-ttu-id="8c495-188">Add a `bin` directory to your root directory, and put the directory that contains your PHP runtime in it (for example, `bin\php`).</span><span class="sxs-lookup"><span data-stu-id="8c495-188">Add a `bin` directory to your root directory, and put the directory that contains your PHP runtime in it (for example, `bin\php`).</span></span>
5. <span data-ttu-id="8c495-189">Deploy your web app.</span><span class="sxs-lookup"><span data-stu-id="8c495-189">Deploy your web app.</span></span>
6. <span data-ttu-id="8c495-190">Browse to your web app in the Azure Portal and click on the **Settings** button.</span><span class="sxs-lookup"><span data-stu-id="8c495-190">Browse to your web app in the Azure Portal and click on the **Settings** button.</span></span>
   
    ![Web App Settings][settings-button]
7. <span data-ttu-id="8c495-192">From the **Settings** blade select **Application Settings** and scroll to the **Handler mappings** section.</span><span class="sxs-lookup"><span data-stu-id="8c495-192">From the **Settings** blade select **Application Settings** and scroll to the **Handler mappings** section.</span></span> <span data-ttu-id="8c495-193">Add `*.php` to the Extension field and add the path to the `php-cgi.exe` executable.</span><span class="sxs-lookup"><span data-stu-id="8c495-193">Add `*.php` to the Extension field and add the path to the `php-cgi.exe` executable.</span></span> <span data-ttu-id="8c495-194">If you put your PHP runtime in the `bin` directory in the root of you application, the path will be `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span><span class="sxs-lookup"><span data-stu-id="8c495-194">If you put your PHP runtime in the `bin` directory in the root of you application, the path will be `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span></span>
   
    ![Specify handler in hander mappings][handler-mappings]
8. <span data-ttu-id="8c495-196">Click the **Save** button at the top of the **Web app settings** blade.</span><span class="sxs-lookup"><span data-stu-id="8c495-196">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![Save configuration settings][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a><span data-ttu-id="8c495-198">How to: Enable Composer automation in Azure</span><span class="sxs-lookup"><span data-stu-id="8c495-198">How to: Enable Composer automation in Azure</span></span>
<span data-ttu-id="8c495-199">By default, App Service doesn't do anything with composer.json, if you have one in your PHP project.</span><span class="sxs-lookup"><span data-stu-id="8c495-199">By default, App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="8c495-200">If you use [Git deployment](app-service-deploy-local-git.md), you can enable composer.json processing during `git push` by enabling the Composer extension.</span><span class="sxs-lookup"><span data-stu-id="8c495-200">If you use [Git deployment](app-service-deploy-local-git.md), you can enable composer.json processing during `git push` by enabling the Composer extension.</span></span>

> [!NOTE]
> <span data-ttu-id="8c495-201">You can [vote for first-class Composer support in App Service here](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span><span class="sxs-lookup"><span data-stu-id="8c495-201">You can [vote for first-class Composer support in App Service here](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span></span>
> 
> 

1. <span data-ttu-id="8c495-202">In your PHP web app's blade in the [Azure portal](https://portal.azure.com), click **Tools** > **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="8c495-202">In your PHP web app's blade in the [Azure portal](https://portal.azure.com), click **Tools** > **Extensions**.</span></span>
   
    ![Azure Portal settings blade to enable Composer automation in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-configure/composer-extension-settings.png)
2. <span data-ttu-id="8c495-204">Click **Add**, then click **Composer**.</span><span class="sxs-lookup"><span data-stu-id="8c495-204">Click **Add**, then click **Composer**.</span></span>
   
    ![Add Composer extension to enable Composer automation in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-configure/composer-extension-add.png)
3. <span data-ttu-id="8c495-206">Click **OK** to accept legal terms.</span><span class="sxs-lookup"><span data-stu-id="8c495-206">Click **OK** to accept legal terms.</span></span> <span data-ttu-id="8c495-207">Click **OK** again to add the extension.</span><span class="sxs-lookup"><span data-stu-id="8c495-207">Click **OK** again to add the extension.</span></span>
   
    <span data-ttu-id="8c495-208">The **Installed extensions** blade will now show the Composer extension.</span><span class="sxs-lookup"><span data-stu-id="8c495-208">The **Installed extensions** blade will now show the Composer extension.</span></span>  
    <span data-ttu-id="8c495-209">![Accept legal terms to enable Composer automation in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-configure/composer-extension-view.png)</span><span class="sxs-lookup"><span data-stu-id="8c495-209">![Accept legal terms to enable Composer automation in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-configure/composer-extension-view.png)</span></span>
4. <span data-ttu-id="8c495-210">Now, perform `git add`, `git commit`, and `git push` like in the previous section.</span><span class="sxs-lookup"><span data-stu-id="8c495-210">Now, perform `git add`, `git commit`, and `git push` like in the previous section.</span></span> <span data-ttu-id="8c495-211">You'll now see that Composer is installing dependencies defined in composer.json.</span><span class="sxs-lookup"><span data-stu-id="8c495-211">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Git deployment with Composer automation in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a><span data-ttu-id="8c495-213">Next steps</span><span class="sxs-lookup"><span data-stu-id="8c495-213">Next steps</span></span>
<span data-ttu-id="8c495-214">For more information, see the [PHP Developer Center](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="8c495-214">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

> [!NOTE]
> <span data-ttu-id="8c495-215">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span><span class="sxs-lookup"><span data-stu-id="8c495-215">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="8c495-216">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="8c495-216">No credit cards required; no commitments.</span></span>
> 
> 

[free trial]: https://www.windowsazure.com/pricing/free-trial/
[phpinfo()]: http://php.net/manual/en/function.phpinfo.php
[select-php-version]: ./media/web-sites-php-configure/select-php-version.png
[List of php.ini directives]: http://www.php.net/manual/en/ini.list.php
[.user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php
[ini_set()]: http://www.php.net/manual/en/function.ini-set.php
[application-settings]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-configure/application-settings.png
[settings-button]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-configure/settings-button.png
[save-button]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-configure/save-button.png
[php-extensions]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-configure/php-extensions.png
[handler-mappings]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-configure/handler-mappings.png
[http://windows.php.net/download/]: http://windows.php.net/download/
[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/
[SETPHPVERCLI]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-configure/ChangePHPVersion-XPlatCLI.png
[GETPHPVERCLI]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-configure/ShowPHPVersion-XplatCLI.png
[SETPHPVERPS]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-configure/ChangePHPVersion-PS.png
[GETPHPVERPS]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-php-configure/ShowPHPVersion-PS.png














