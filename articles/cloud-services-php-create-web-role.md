---
title: Create Azure web and worker roles for PHP
description: A guide to creating PHP web and worker roles in an Azure cloud service, and configuring the PHP runtime.
services: ''
documentationcenter: php
author: msangapu
manager: cfowler
ms.assetid: 9f7ccda0-bd96-4f7b-a7af-fb279a9e975b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/11/2018
ms.author: msangapu
ms.openlocfilehash: 30afc1c577ab6dd18374d5ef5199c7e7d9e89fe4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44810250"
---
# <a name="create-php-web-and-worker-roles"></a><span data-ttu-id="478d1-103">Create PHP web and worker roles</span><span class="sxs-lookup"><span data-stu-id="478d1-103">Create PHP web and worker roles</span></span>

## <a name="overview"></a><span data-ttu-id="478d1-104">Overview</span><span class="sxs-lookup"><span data-stu-id="478d1-104">Overview</span></span>

<span data-ttu-id="478d1-105">This guide will show you how to create PHP web or worker roles in a Windows development environment, choose a specific version of PHP from the "built-in" versions available, change the PHP configuration, enable extensions, and finally, deploy to Azure.</span><span class="sxs-lookup"><span data-stu-id="478d1-105">This guide will show you how to create PHP web or worker roles in a Windows development environment, choose a specific version of PHP from the "built-in" versions available, change the PHP configuration, enable extensions, and finally, deploy to Azure.</span></span> <span data-ttu-id="478d1-106">It also describes how to configure a web or worker role to use a PHP runtime (with custom configuration and extensions) that you provide.</span><span class="sxs-lookup"><span data-stu-id="478d1-106">It also describes how to configure a web or worker role to use a PHP runtime (with custom configuration and extensions) that you provide.</span></span>

<span data-ttu-id="478d1-107">Azure provides three compute models for running applications: Azure App Service, Azure Virtual Machines, and Azure Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="478d1-107">Azure provides three compute models for running applications: Azure App Service, Azure Virtual Machines, and Azure Cloud Services.</span></span> <span data-ttu-id="478d1-108">All three models support PHP.</span><span class="sxs-lookup"><span data-stu-id="478d1-108">All three models support PHP.</span></span> <span data-ttu-id="478d1-109">Cloud Services, which includes web and worker roles, provides *platform as a service (PaaS)*.</span><span class="sxs-lookup"><span data-stu-id="478d1-109">Cloud Services, which includes web and worker roles, provides *platform as a service (PaaS)*.</span></span> <span data-ttu-id="478d1-110">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server to host front-end web applications.</span><span class="sxs-lookup"><span data-stu-id="478d1-110">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server to host front-end web applications.</span></span> <span data-ttu-id="478d1-111">A worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span><span class="sxs-lookup"><span data-stu-id="478d1-111">A worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="478d1-112">For more information about these options, see [Compute hosting options provided by Azure](cloud-services/cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="478d1-112">For more information about these options, see [Compute hosting options provided by Azure](cloud-services/cloud-services-choose-me.md).</span></span>

## <a name="download-the-azure-sdk-for-php"></a><span data-ttu-id="478d1-113">Download the Azure SDK for PHP</span><span class="sxs-lookup"><span data-stu-id="478d1-113">Download the Azure SDK for PHP</span></span>

<span data-ttu-id="478d1-114">The [Azure SDK for PHP](php-download-sdk.md) consists of several components.</span><span class="sxs-lookup"><span data-stu-id="478d1-114">The [Azure SDK for PHP](php-download-sdk.md) consists of several components.</span></span> <span data-ttu-id="478d1-115">This article will use two of them: Azure PowerShell and the Azure emulators.</span><span class="sxs-lookup"><span data-stu-id="478d1-115">This article will use two of them: Azure PowerShell and the Azure emulators.</span></span> <span data-ttu-id="478d1-116">These two components can be installed via the Microsoft Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="478d1-116">These two components can be installed via the Microsoft Web Platform Installer.</span></span> <span data-ttu-id="478d1-117">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="478d1-117">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="create-a-cloud-services-project"></a><span data-ttu-id="478d1-118">Create a Cloud Services project</span><span class="sxs-lookup"><span data-stu-id="478d1-118">Create a Cloud Services project</span></span>

<span data-ttu-id="478d1-119">The first step in creating a PHP web or worker role is to create an Azure Service project.</span><span class="sxs-lookup"><span data-stu-id="478d1-119">The first step in creating a PHP web or worker role is to create an Azure Service project.</span></span> <span data-ttu-id="478d1-120">an Azure Service project serves as a logical container for web and worker roles, and it contains the project's [service definition (.csdef)] and [service configuration (.cscfg)] files.</span><span class="sxs-lookup"><span data-stu-id="478d1-120">an Azure Service project serves as a logical container for web and worker roles, and it contains the project's [service definition (.csdef)] and [service configuration (.cscfg)] files.</span></span>

<span data-ttu-id="478d1-121">To create a new Azure Service project, run Azure PowerShell as an administrator, and execute the following command:</span><span class="sxs-lookup"><span data-stu-id="478d1-121">To create a new Azure Service project, run Azure PowerShell as an administrator, and execute the following command:</span></span>

    PS C:\>New-AzureServiceProject myProject

<span data-ttu-id="478d1-122">This command will create a new directory (`myProject`) to which you can add web and worker roles.</span><span class="sxs-lookup"><span data-stu-id="478d1-122">This command will create a new directory (`myProject`) to which you can add web and worker roles.</span></span>

## <a name="add-php-web-or-worker-roles"></a><span data-ttu-id="478d1-123">Add PHP web or worker roles</span><span class="sxs-lookup"><span data-stu-id="478d1-123">Add PHP web or worker roles</span></span>

<span data-ttu-id="478d1-124">To add a PHP web role to a project, run the following command from within the project's root directory:</span><span class="sxs-lookup"><span data-stu-id="478d1-124">To add a PHP web role to a project, run the following command from within the project's root directory:</span></span>

    PS C:\myProject> Add-AzurePHPWebRole roleName

<span data-ttu-id="478d1-125">For a worker role, use this command:</span><span class="sxs-lookup"><span data-stu-id="478d1-125">For a worker role, use this command:</span></span>

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> <span data-ttu-id="478d1-126">The `roleName` parameter is optional.</span><span class="sxs-lookup"><span data-stu-id="478d1-126">The `roleName` parameter is optional.</span></span> <span data-ttu-id="478d1-127">If it is omitted, the role name will be automatically generated.</span><span class="sxs-lookup"><span data-stu-id="478d1-127">If it is omitted, the role name will be automatically generated.</span></span> <span data-ttu-id="478d1-128">The first web role created will be `WebRole1`, the second will be `WebRole2`, and so on.</span><span class="sxs-lookup"><span data-stu-id="478d1-128">The first web role created will be `WebRole1`, the second will be `WebRole2`, and so on.</span></span> <span data-ttu-id="478d1-129">The first worker role created will be `WorkerRole1`, the second will be `WorkerRole2`, and so on.</span><span class="sxs-lookup"><span data-stu-id="478d1-129">The first worker role created will be `WorkerRole1`, the second will be `WorkerRole2`, and so on.</span></span>
>
>

## <a name="specify-the-built-in-php-version"></a><span data-ttu-id="478d1-130">Specify the built-in PHP version</span><span class="sxs-lookup"><span data-stu-id="478d1-130">Specify the built-in PHP version</span></span>

<span data-ttu-id="478d1-131">When you add a PHP web or worker role to a project, the project's configuration files are modified so that PHP will be installed on each web or worker instance of your application when it is deployed.</span><span class="sxs-lookup"><span data-stu-id="478d1-131">When you add a PHP web or worker role to a project, the project's configuration files are modified so that PHP will be installed on each web or worker instance of your application when it is deployed.</span></span> <span data-ttu-id="478d1-132">To see the version of PHP that will be installed by default, run the following command:</span><span class="sxs-lookup"><span data-stu-id="478d1-132">To see the version of PHP that will be installed by default, run the following command:</span></span>

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

<span data-ttu-id="478d1-133">The output from the command above will look similar to what is shown below.</span><span class="sxs-lookup"><span data-stu-id="478d1-133">The output from the command above will look similar to what is shown below.</span></span> <span data-ttu-id="478d1-134">In this example, the `IsDefault` flag is set to `true` for PHP 5.3.17, indicating that it will be the default PHP version installed.</span><span class="sxs-lookup"><span data-stu-id="478d1-134">In this example, the `IsDefault` flag is set to `true` for PHP 5.3.17, indicating that it will be the default PHP version installed.</span></span>

```
Runtime Version     PackageUri                      IsDefault
------- -------     ----------                      ---------
Node 0.6.17         http://nodertncu.blob.core...   False
Node 0.6.20         http://nodertncu.blob.core...   True
Node 0.8.4          http://nodertncu.blob.core...   False
IISNode 0.1.21      http://nodertncu.blob.core...   True
Cache 1.8.0         http://nodertncu.blob.core...   True
PHP 5.3.17          http://nodertncu.blob.core...   True
PHP 5.4.0           http://nodertncu.blob.core...   False
```

<span data-ttu-id="478d1-135">You can set the PHP runtime version to any of the PHP versions that are listed.</span><span class="sxs-lookup"><span data-stu-id="478d1-135">You can set the PHP runtime version to any of the PHP versions that are listed.</span></span> <span data-ttu-id="478d1-136">For example, to set the PHP version (for a role with the name `roleName`) to 5.4.0, use the following command:</span><span class="sxs-lookup"><span data-stu-id="478d1-136">For example, to set the PHP version (for a role with the name `roleName`) to 5.4.0, use the following command:</span></span>

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> <span data-ttu-id="478d1-137">Available PHP versions may change in the future.</span><span class="sxs-lookup"><span data-stu-id="478d1-137">Available PHP versions may change in the future.</span></span>
>
>

## <a name="customize-the-built-in-php-runtime"></a><span data-ttu-id="478d1-138">Customize the built-in PHP runtime</span><span class="sxs-lookup"><span data-stu-id="478d1-138">Customize the built-in PHP runtime</span></span>

<span data-ttu-id="478d1-139">You have complete control over the configuration of the PHP runtime that is installed when you follow the steps above, including modification of `php.ini` settings and enabling of extensions.</span><span class="sxs-lookup"><span data-stu-id="478d1-139">You have complete control over the configuration of the PHP runtime that is installed when you follow the steps above, including modification of `php.ini` settings and enabling of extensions.</span></span>

<span data-ttu-id="478d1-140">To customize the built-in PHP runtime, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="478d1-140">To customize the built-in PHP runtime, follow these steps:</span></span>

1. <span data-ttu-id="478d1-141">Add a new folder, named `php`, to the `bin` directory of your web role.</span><span class="sxs-lookup"><span data-stu-id="478d1-141">Add a new folder, named `php`, to the `bin` directory of your web role.</span></span> <span data-ttu-id="478d1-142">For a worker role, add it to the role's root directory.</span><span class="sxs-lookup"><span data-stu-id="478d1-142">For a worker role, add it to the role's root directory.</span></span>
2. <span data-ttu-id="478d1-143">In the `php` folder, create another folder called `ext`.</span><span class="sxs-lookup"><span data-stu-id="478d1-143">In the `php` folder, create another folder called `ext`.</span></span> <span data-ttu-id="478d1-144">Put any `.dll` extension files (e.g., `php_mongo.dll`) that you want to enable in this folder.</span><span class="sxs-lookup"><span data-stu-id="478d1-144">Put any `.dll` extension files (e.g., `php_mongo.dll`) that you want to enable in this folder.</span></span>
3. <span data-ttu-id="478d1-145">Add a `php.ini` file to the `php` folder.</span><span class="sxs-lookup"><span data-stu-id="478d1-145">Add a `php.ini` file to the `php` folder.</span></span> <span data-ttu-id="478d1-146">Enable any custom extensions and set any PHP directives in this file.</span><span class="sxs-lookup"><span data-stu-id="478d1-146">Enable any custom extensions and set any PHP directives in this file.</span></span> <span data-ttu-id="478d1-147">For example, if you wanted to turn `display_errors` on and enable the `php_mongo.dll` extension, the contents of your `php.ini` file would be as follows:</span><span class="sxs-lookup"><span data-stu-id="478d1-147">For example, if you wanted to turn `display_errors` on and enable the `php_mongo.dll` extension, the contents of your `php.ini` file would be as follows:</span></span>

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> <span data-ttu-id="478d1-148">Any settings that you don't explicitly set in the `php.ini` file that you provide will automatically be set to their default values.</span><span class="sxs-lookup"><span data-stu-id="478d1-148">Any settings that you don't explicitly set in the `php.ini` file that you provide will automatically be set to their default values.</span></span> <span data-ttu-id="478d1-149">However, keep in mind that you can add a complete `php.ini` file.</span><span class="sxs-lookup"><span data-stu-id="478d1-149">However, keep in mind that you can add a complete `php.ini` file.</span></span>
>
>

## <a name="use-your-own-php-runtime"></a><span data-ttu-id="478d1-150">Use your own PHP runtime</span><span class="sxs-lookup"><span data-stu-id="478d1-150">Use your own PHP runtime</span></span>

<span data-ttu-id="478d1-151">In some cases, instead of selecting a built-in PHP runtime and configuring it as described above, you may want to provide your own PHP runtime.</span><span class="sxs-lookup"><span data-stu-id="478d1-151">In some cases, instead of selecting a built-in PHP runtime and configuring it as described above, you may want to provide your own PHP runtime.</span></span> <span data-ttu-id="478d1-152">For example, you can use the same PHP runtime in a web or worker role that you use in your development environment.</span><span class="sxs-lookup"><span data-stu-id="478d1-152">For example, you can use the same PHP runtime in a web or worker role that you use in your development environment.</span></span> <span data-ttu-id="478d1-153">This makes it easier to ensure that the application will not change behavior in your production environment.</span><span class="sxs-lookup"><span data-stu-id="478d1-153">This makes it easier to ensure that the application will not change behavior in your production environment.</span></span>

### <a name="configure-a-web-role-to-use-your-own-php-runtime"></a><span data-ttu-id="478d1-154">Configure a web role to use your own PHP runtime</span><span class="sxs-lookup"><span data-stu-id="478d1-154">Configure a web role to use your own PHP runtime</span></span>

<span data-ttu-id="478d1-155">To configure a web role to use a PHP runtime that you provide, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="478d1-155">To configure a web role to use a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="478d1-156">Create an Azure Service project and add a PHP web role as described previously in this topic.</span><span class="sxs-lookup"><span data-stu-id="478d1-156">Create an Azure Service project and add a PHP web role as described previously in this topic.</span></span>
2. <span data-ttu-id="478d1-157">Create a `php` folder in the `bin` folder that is in your web role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) to the `php` folder.</span><span class="sxs-lookup"><span data-stu-id="478d1-157">Create a `php` folder in the `bin` folder that is in your web role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) to the `php` folder.</span></span>
3. <span data-ttu-id="478d1-158">(OPTIONAL) If your PHP runtime uses the [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need to configure your web role to install [SQL Server Native Client 2012][sql native client] when it is provisioned.</span><span class="sxs-lookup"><span data-stu-id="478d1-158">(OPTIONAL) If your PHP runtime uses the [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need to configure your web role to install [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="478d1-159">To do this, add the [sqlncli.msi x64 installer] to the `bin` folder in your web role's root directory.</span><span class="sxs-lookup"><span data-stu-id="478d1-159">To do this, add the [sqlncli.msi x64 installer] to the `bin` folder in your web role's root directory.</span></span> <span data-ttu-id="478d1-160">The startup script described in the next step will silently run the installer when the role is provisioned.</span><span class="sxs-lookup"><span data-stu-id="478d1-160">The startup script described in the next step will silently run the installer when the role is provisioned.</span></span> <span data-ttu-id="478d1-161">If your PHP runtime does not use the Microsoft Drivers for PHP for SQL Server, you can remove the following line from the script shown in the next step:</span><span class="sxs-lookup"><span data-stu-id="478d1-161">If your PHP runtime does not use the Microsoft Drivers for PHP for SQL Server, you can remove the following line from the script shown in the next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="478d1-162">Define a startup task that configures [Internet Information Services (IIS)][iis.net] to use your PHP runtime to handle requests for `.php` pages.</span><span class="sxs-lookup"><span data-stu-id="478d1-162">Define a startup task that configures [Internet Information Services (IIS)][iis.net] to use your PHP runtime to handle requests for `.php` pages.</span></span> <span data-ttu-id="478d1-163">To do this, open the `setup_web.cmd` file (in the `bin` file of your web role's root directory) in a text editor and replace its contents with the following script:</span><span class="sxs-lookup"><span data-stu-id="478d1-163">To do this, open the `setup_web.cmd` file (in the `bin` file of your web role's root directory) in a text editor and replace its contents with the following script:</span></span>

    ```cmd
    @ECHO ON
    cd "%~dp0"

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    SET PHP_FULL_PATH=%~dp0php\php-cgi.exe
    SET NEW_PATH=%PATH%;%RoleRoot%\base\x86

    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%',maxInstances='12',idleTimeout='60000',activityTimeout='3600',requestTimeout='60000',instanceMaxRequests='10000',protocol='NamedPipe',flushNamedPipe='False']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PATH',value='%NEW_PATH%']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PHP_FCGI_MAX_REQUESTS',value='10000']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/handlers /+"[name='PHP',path='*.php',verb='GET,HEAD,POST',modules='FastCgiModule',scriptProcessor='%PHP_FULL_PATH%',resourceType='Either',requireAccess='Script']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /"[fullPath='%PHP_FULL_PATH%'].queueLength:50000"
    ```
5. <span data-ttu-id="478d1-164">Add your application files to your web role's root directory.</span><span class="sxs-lookup"><span data-stu-id="478d1-164">Add your application files to your web role's root directory.</span></span> <span data-ttu-id="478d1-165">This will be the web server's root directory.</span><span class="sxs-lookup"><span data-stu-id="478d1-165">This will be the web server's root directory.</span></span>
6. <span data-ttu-id="478d1-166">Publish your application as described in the [Publish your application](#publish-your-application) section below.</span><span class="sxs-lookup"><span data-stu-id="478d1-166">Publish your application as described in the [Publish your application](#publish-your-application) section below.</span></span>

> [!NOTE]
> <span data-ttu-id="478d1-167">The `download.ps1` script (in the `bin` folder of the web role's root directory) can be deleted after you follow the steps described above for using your own PHP runtime.</span><span class="sxs-lookup"><span data-stu-id="478d1-167">The `download.ps1` script (in the `bin` folder of the web role's root directory) can be deleted after you follow the steps described above for using your own PHP runtime.</span></span>
>
>

### <a name="configure-a-worker-role-to-use-your-own-php-runtime"></a><span data-ttu-id="478d1-168">Configure a worker role to use your own PHP runtime</span><span class="sxs-lookup"><span data-stu-id="478d1-168">Configure a worker role to use your own PHP runtime</span></span>

<span data-ttu-id="478d1-169">To configure a worker role to use a PHP runtime that you provide, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="478d1-169">To configure a worker role to use a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="478d1-170">Create an Azure Service project and add a PHP worker role as described previously in this topic.</span><span class="sxs-lookup"><span data-stu-id="478d1-170">Create an Azure Service project and add a PHP worker role as described previously in this topic.</span></span>
2. <span data-ttu-id="478d1-171">Create a `php` folder in the worker role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) to the `php` folder.</span><span class="sxs-lookup"><span data-stu-id="478d1-171">Create a `php` folder in the worker role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) to the `php` folder.</span></span>
3. <span data-ttu-id="478d1-172">(OPTIONAL) If your PHP runtime uses [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need to configure your worker role to install [SQL Server Native Client 2012][sql native client] when it is provisioned.</span><span class="sxs-lookup"><span data-stu-id="478d1-172">(OPTIONAL) If your PHP runtime uses [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need to configure your worker role to install [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="478d1-173">To do this, add the [sqlncli.msi x64 installer] to the worker role's root directory.</span><span class="sxs-lookup"><span data-stu-id="478d1-173">To do this, add the [sqlncli.msi x64 installer] to the worker role's root directory.</span></span> <span data-ttu-id="478d1-174">The startup script described in the next step will silently run the installer when the role is provisioned.</span><span class="sxs-lookup"><span data-stu-id="478d1-174">The startup script described in the next step will silently run the installer when the role is provisioned.</span></span> <span data-ttu-id="478d1-175">If your PHP runtime does not use the Microsoft Drivers for PHP for SQL Server, you can remove the following line from the script shown in the next step:</span><span class="sxs-lookup"><span data-stu-id="478d1-175">If your PHP runtime does not use the Microsoft Drivers for PHP for SQL Server, you can remove the following line from the script shown in the next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="478d1-176">Define a startup task that adds your `php.exe` executable to the worker role's PATH environment variable when the role is provisioned.</span><span class="sxs-lookup"><span data-stu-id="478d1-176">Define a startup task that adds your `php.exe` executable to the worker role's PATH environment variable when the role is provisioned.</span></span> <span data-ttu-id="478d1-177">To do this, open the `setup_worker.cmd` file (in the worker role's root directory) in a text editor and replace its contents with the following script:</span><span class="sxs-lookup"><span data-stu-id="478d1-177">To do this, open the `setup_worker.cmd` file (in the worker role's root directory) in a text editor and replace its contents with the following script:</span></span>

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service to the web root directory...
    icacls ..\ /grant "Network Service":(OI)(CI)W
    if %ERRORLEVEL% neq 0 goto error
    echo OK

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    setx Path "%PATH%;%~dp0php" /M

    if %ERRORLEVEL% neq 0 goto error

    echo SUCCESS
    exit /b 0

    :error

    echo FAILED
    exit /b -1
    ```
5. <span data-ttu-id="478d1-178">Add your application files to your worker role's root directory.</span><span class="sxs-lookup"><span data-stu-id="478d1-178">Add your application files to your worker role's root directory.</span></span>
6. <span data-ttu-id="478d1-179">Publish your application as described in the [Publish your application](#publish-your-application) section below.</span><span class="sxs-lookup"><span data-stu-id="478d1-179">Publish your application as described in the [Publish your application](#publish-your-application) section below.</span></span>

## <a name="run-your-application-in-the-compute-and-storage-emulators"></a><span data-ttu-id="478d1-180">Run your application in the compute and storage emulators</span><span class="sxs-lookup"><span data-stu-id="478d1-180">Run your application in the compute and storage emulators</span></span>

<span data-ttu-id="478d1-181">The Azure emulators provide a local environment in which you can test your Azure application before you deploy it to the cloud.</span><span class="sxs-lookup"><span data-stu-id="478d1-181">The Azure emulators provide a local environment in which you can test your Azure application before you deploy it to the cloud.</span></span> <span data-ttu-id="478d1-182">There are some differences between the emulators and the Azure environment.</span><span class="sxs-lookup"><span data-stu-id="478d1-182">There are some differences between the emulators and the Azure environment.</span></span> <span data-ttu-id="478d1-183">To understand this better, see [Use the Azure storage emulator for development and testing](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="478d1-183">To understand this better, see [Use the Azure storage emulator for development and testing](storage/common/storage-use-emulator.md).</span></span>

<span data-ttu-id="478d1-184">Note that you must have PHP installed locally to use the compute emulator.</span><span class="sxs-lookup"><span data-stu-id="478d1-184">Note that you must have PHP installed locally to use the compute emulator.</span></span> <span data-ttu-id="478d1-185">The compute emulator will use your local PHP installation to run your application.</span><span class="sxs-lookup"><span data-stu-id="478d1-185">The compute emulator will use your local PHP installation to run your application.</span></span>

<span data-ttu-id="478d1-186">To run your project in the emulators, execute the following command from your project's root directory:</span><span class="sxs-lookup"><span data-stu-id="478d1-186">To run your project in the emulators, execute the following command from your project's root directory:</span></span>

    PS C:\MyProject> Start-AzureEmulator

<span data-ttu-id="478d1-187">You will see output similar to this:</span><span class="sxs-lookup"><span data-stu-id="478d1-187">You will see output similar to this:</span></span>

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

<span data-ttu-id="478d1-188">You can see your application running in the emulator by opening a web browser and browsing to the local address shown in the output (`http://127.0.0.1:81` in the example output above).</span><span class="sxs-lookup"><span data-stu-id="478d1-188">You can see your application running in the emulator by opening a web browser and browsing to the local address shown in the output (`http://127.0.0.1:81` in the example output above).</span></span>

<span data-ttu-id="478d1-189">To stop the emulators, execute this command:</span><span class="sxs-lookup"><span data-stu-id="478d1-189">To stop the emulators, execute this command:</span></span>

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a><span data-ttu-id="478d1-190">Publish your application</span><span class="sxs-lookup"><span data-stu-id="478d1-190">Publish your application</span></span>

<span data-ttu-id="478d1-191">To publish your application, you need to first import your publish settings by using the [Import-AzurePublishSettingsFile](https://docs.microsoft.com/powershell/module/servicemanagement/azure/import-azurepublishsettingsfile) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="478d1-191">To publish your application, you need to first import your publish settings by using the [Import-AzurePublishSettingsFile](https://docs.microsoft.com/powershell/module/servicemanagement/azure/import-azurepublishsettingsfile) cmdlet.</span></span> <span data-ttu-id="478d1-192">Then you can publish your application by using the [Publish-AzureServiceProject](https://docs.microsoft.com/powershell/module/servicemanagement/azure/publish-azureserviceproject) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="478d1-192">Then you can publish your application by using the [Publish-AzureServiceProject](https://docs.microsoft.com/powershell/module/servicemanagement/azure/publish-azureserviceproject) cmdlet.</span></span> <span data-ttu-id="478d1-193">For information about signing in, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="478d1-193">For information about signing in, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="next-steps"></a><span data-ttu-id="478d1-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="478d1-194">Next steps</span></span>

<span data-ttu-id="478d1-195">For more information, see the [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="478d1-195">For more information, see the [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[service definition (.csdef)]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[service configuration (.cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation
[sqlsrv drivers]: http://php.net/sqlsrv
[sqlncli.msi x64 installer]: http://go.microsoft.com/fwlink/?LinkID=239648
