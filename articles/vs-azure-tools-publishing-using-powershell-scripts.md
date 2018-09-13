---
title: Using Windows PowerShell Scripts to Publish to Dev and Test Environments | Microsoft Docs
description: Learn how to use Windows PowerShell scripts from Visual Studio to publish to development and test environments.
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: tarcher
ms.openlocfilehash: 772af98069441bc4ef9c2371acee3554128539e1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550240"
---
# <a name="using-windows-powershell-scripts-to-publish-to-dev-and-test-environments"></a><span data-ttu-id="44f39-103">Using Windows PowerShell scripts to publish to dev and test environments</span><span class="sxs-lookup"><span data-stu-id="44f39-103">Using Windows PowerShell scripts to publish to dev and test environments</span></span>
<span data-ttu-id="44f39-104">When you create a web application in Visual Studio, you can generate a Windows PowerShell script that you can use later to automate the publishing of your website to Azure as a Web App in Azure App Service or a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="44f39-104">When you create a web application in Visual Studio, you can generate a Windows PowerShell script that you can use later to automate the publishing of your website to Azure as a Web App in Azure App Service or a virtual machine.</span></span> <span data-ttu-id="44f39-105">You can edit and extend the Windows PowerShell script in the Visual Studio editor to suit your requirements, or integrate the script with existing build, test, and publishing scripts.</span><span class="sxs-lookup"><span data-stu-id="44f39-105">You can edit and extend the Windows PowerShell script in the Visual Studio editor to suit your requirements, or integrate the script with existing build, test, and publishing scripts.</span></span>

<span data-ttu-id="44f39-106">Using these scripts, you can provision customized versions (also known as dev and test environments) of your site for temporary use.</span><span class="sxs-lookup"><span data-stu-id="44f39-106">Using these scripts, you can provision customized versions (also known as dev and test environments) of your site for temporary use.</span></span> <span data-ttu-id="44f39-107">For example, you might set up a particular version of your website on an Azure virtual machine or on the staging slot on a website to run a test suite, reproduce a bug, test a bug fix, trial a proposed change, or set up a custom environment for a demo or presentation.</span><span class="sxs-lookup"><span data-stu-id="44f39-107">For example, you might set up a particular version of your website on an Azure virtual machine or on the staging slot on a website to run a test suite, reproduce a bug, test a bug fix, trial a proposed change, or set up a custom environment for a demo or presentation.</span></span> <span data-ttu-id="44f39-108">After you've created a script that publishes your project, you can recreate identical environments by re-running the script as needed, or run the script with your own build of your web application to create a custom environment for testing.</span><span class="sxs-lookup"><span data-stu-id="44f39-108">After you've created a script that publishes your project, you can recreate identical environments by re-running the script as needed, or run the script with your own build of your web application to create a custom environment for testing.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="44f39-109">What you need</span><span class="sxs-lookup"><span data-stu-id="44f39-109">What you need</span></span>
* <span data-ttu-id="44f39-110">Azure SDK 2.3 or later.</span><span class="sxs-lookup"><span data-stu-id="44f39-110">Azure SDK 2.3 or later.</span></span> <span data-ttu-id="44f39-111">See [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) for more information.</span><span class="sxs-lookup"><span data-stu-id="44f39-111">See [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) for more information.</span></span>

<span data-ttu-id="44f39-112">You do not need the Azure SDK to generate the scripts for web projects.</span><span class="sxs-lookup"><span data-stu-id="44f39-112">You do not need the Azure SDK to generate the scripts for web projects.</span></span> <span data-ttu-id="44f39-113">This feature is for web projects, not web roles in cloud services.</span><span class="sxs-lookup"><span data-stu-id="44f39-113">This feature is for web projects, not web roles in cloud services.</span></span>

* <span data-ttu-id="44f39-114">Azure PowerShell 0.7.4 or later.</span><span class="sxs-lookup"><span data-stu-id="44f39-114">Azure PowerShell 0.7.4 or later.</span></span> <span data-ttu-id="44f39-115">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information.</span><span class="sxs-lookup"><span data-stu-id="44f39-115">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information.</span></span>
* <span data-ttu-id="44f39-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) or later.</span><span class="sxs-lookup"><span data-stu-id="44f39-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) or later.</span></span>

## <a name="additional-tools"></a><span data-ttu-id="44f39-117">Additional tools</span><span class="sxs-lookup"><span data-stu-id="44f39-117">Additional tools</span></span>
<span data-ttu-id="44f39-118">Additional tools and resources for working with PowerShell in Visual Studio for Azure development are available.</span><span class="sxs-lookup"><span data-stu-id="44f39-118">Additional tools and resources for working with PowerShell in Visual Studio for Azure development are available.</span></span> <span data-ttu-id="44f39-119">See [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span><span class="sxs-lookup"><span data-stu-id="44f39-119">See [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span></span>

## <a name="generating-the-publish-scripts"></a><span data-ttu-id="44f39-120">Generating the publish scripts</span><span class="sxs-lookup"><span data-stu-id="44f39-120">Generating the publish scripts</span></span>
<span data-ttu-id="44f39-121">You can generate the publish scripts for a virtual machine that hosts your website when you create a new project by following [these instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="44f39-121">You can generate the publish scripts for a virtual machine that hosts your website when you create a new project by following [these instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="44f39-122">You can also [generate publish scripts for web apps in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="44f39-122">You can also [generate publish scripts for web apps in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span></span>

## <a name="scripts-that-visual-studio-generates"></a><span data-ttu-id="44f39-123">Scripts that Visual Studio generates</span><span class="sxs-lookup"><span data-stu-id="44f39-123">Scripts that Visual Studio generates</span></span>
<span data-ttu-id="44f39-124">Visual Studio generates a solution-level folder called **PublishScripts** that contains two Windows PowerShell files, a publish script for your virtual machine or website, and a module that contains functions that you can use in the scripts.</span><span class="sxs-lookup"><span data-stu-id="44f39-124">Visual Studio generates a solution-level folder called **PublishScripts** that contains two Windows PowerShell files, a publish script for your virtual machine or website, and a module that contains functions that you can use in the scripts.</span></span> <span data-ttu-id="44f39-125">Visual Studio also generates a file in the JSON format that specifies the details of the project you are deploying.</span><span class="sxs-lookup"><span data-stu-id="44f39-125">Visual Studio also generates a file in the JSON format that specifies the details of the project you are deploying.</span></span>

### <a name="windows-powershell-publish-script"></a><span data-ttu-id="44f39-126">Windows PowerShell publish script</span><span class="sxs-lookup"><span data-stu-id="44f39-126">Windows PowerShell publish script</span></span>
<span data-ttu-id="44f39-127">The publish script contains specific publish steps for deploying to a website or virtual machine.</span><span class="sxs-lookup"><span data-stu-id="44f39-127">The publish script contains specific publish steps for deploying to a website or virtual machine.</span></span> <span data-ttu-id="44f39-128">Visual Studio provides syntax coloring for Windows PowerShell development.</span><span class="sxs-lookup"><span data-stu-id="44f39-128">Visual Studio provides syntax coloring for Windows PowerShell development.</span></span> <span data-ttu-id="44f39-129">Help for the functions is available, and you can freely edit the functions in the script to suit your changing requirements.</span><span class="sxs-lookup"><span data-stu-id="44f39-129">Help for the functions is available, and you can freely edit the functions in the script to suit your changing requirements.</span></span>

### <a name="windows-powershell-module"></a><span data-ttu-id="44f39-130">Windows PowerShell module</span><span class="sxs-lookup"><span data-stu-id="44f39-130">Windows PowerShell module</span></span>
<span data-ttu-id="44f39-131">The Windows PowerShell module that Visual Studio generates contains functions that the publish script uses.</span><span class="sxs-lookup"><span data-stu-id="44f39-131">The Windows PowerShell module that Visual Studio generates contains functions that the publish script uses.</span></span> <span data-ttu-id="44f39-132">These are Azure PowerShell functions and are not intended to be modified.</span><span class="sxs-lookup"><span data-stu-id="44f39-132">These are Azure PowerShell functions and are not intended to be modified.</span></span> <span data-ttu-id="44f39-133">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information.</span><span class="sxs-lookup"><span data-stu-id="44f39-133">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information.</span></span>

### <a name="json-configuration-file"></a><span data-ttu-id="44f39-134">JSON configuration file</span><span class="sxs-lookup"><span data-stu-id="44f39-134">JSON configuration file</span></span>
<span data-ttu-id="44f39-135">The JSON file is created in the **Configurations** folder and contains configuration data that specifies exactly which resources to deploy to Azure.</span><span class="sxs-lookup"><span data-stu-id="44f39-135">The JSON file is created in the **Configurations** folder and contains configuration data that specifies exactly which resources to deploy to Azure.</span></span> <span data-ttu-id="44f39-136">The name of the file that Visual Studio generates is project-name-WAWS-dev.json if you created a website, or project name-VM-dev.json if you created a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="44f39-136">The name of the file that Visual Studio generates is project-name-WAWS-dev.json if you created a website, or project name-VM-dev.json if you created a virtual machine.</span></span> <span data-ttu-id="44f39-137">Here's an example of a JSON configuration file that's generated when you create a website.</span><span class="sxs-lookup"><span data-stu-id="44f39-137">Here's an example of a JSON configuration file that's generated when you create a website.</span></span> <span data-ttu-id="44f39-138">Most of the values are self-explanatory.</span><span class="sxs-lookup"><span data-stu-id="44f39-138">Most of the values are self-explanatory.</span></span> <span data-ttu-id="44f39-139">The website name is generated by Azure, so it might not match your project name.</span><span class="sxs-lookup"><span data-stu-id="44f39-139">The website name is generated by Azure, so it might not match your project name.</span></span>

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```
<span data-ttu-id="44f39-140">When you create a virtual machine, the JSON configuration file looks similar to the following.</span><span class="sxs-lookup"><span data-stu-id="44f39-140">When you create a virtual machine, the JSON configuration file looks similar to the following.</span></span> <span data-ttu-id="44f39-141">Note that a cloud service is created as a container for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="44f39-141">Note that a cloud service is created as a container for the virtual machine.</span></span> <span data-ttu-id="44f39-142">The virtual machine contains the usual endpoints for web access through HTTP and HTTPS, as well as endpoints for Web Deploy, which lets you publish to the website from your local machine, Remote Desktop, and Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="44f39-142">The virtual machine contains the usual endpoints for web access through HTTP and HTTPS, as well as endpoints for Web Deploy, which lets you publish to the website from your local machine, Remote Desktop, and Windows PowerShell.</span></span>

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="44f39-143">You can edit the JSON configuration to change what happens when you run the publish scripts.</span><span class="sxs-lookup"><span data-stu-id="44f39-143">You can edit the JSON configuration to change what happens when you run the publish scripts.</span></span> <span data-ttu-id="44f39-144">The `cloudService` and `virtualMachine` sections are required, but you can delete the `databases` section if you don't need it.</span><span class="sxs-lookup"><span data-stu-id="44f39-144">The `cloudService` and `virtualMachine` sections are required, but you can delete the `databases` section if you don't need it.</span></span> <span data-ttu-id="44f39-145">The properties that are empty in the default configuration file that Visual Studio generates are optional; those that have values in the default configuration file are required.</span><span class="sxs-lookup"><span data-stu-id="44f39-145">The properties that are empty in the default configuration file that Visual Studio generates are optional; those that have values in the default configuration file are required.</span></span>

<span data-ttu-id="44f39-146">If you have a website that has multiple deployment environments (known as slots) instead of a single production site in Azure, you can include the slot name in the name of the website in the JSON configuration file.</span><span class="sxs-lookup"><span data-stu-id="44f39-146">If you have a website that has multiple deployment environments (known as slots) instead of a single production site in Azure, you can include the slot name in the name of the website in the JSON configuration file.</span></span> <span data-ttu-id="44f39-147">For example, if you have a website that's named **mysite** and a slot for it named **test** then the URI is mysite-test.cloudapp.net, but the correct name to use in the configuration file is mysite(test).</span><span class="sxs-lookup"><span data-stu-id="44f39-147">For example, if you have a website that's named **mysite** and a slot for it named **test** then the URI is mysite-test.cloudapp.net, but the correct name to use in the configuration file is mysite(test).</span></span> <span data-ttu-id="44f39-148">You can only do this if the website and slots already exist in your subscription.</span><span class="sxs-lookup"><span data-stu-id="44f39-148">You can only do this if the website and slots already exist in your subscription.</span></span> <span data-ttu-id="44f39-149">If they don't exist, create the website by running the script without specifying the slot, then create the slot in the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and thereafter run the script with the modified website name.</span><span class="sxs-lookup"><span data-stu-id="44f39-149">If they don't exist, create the website by running the script without specifying the slot, then create the slot in the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and thereafter run the script with the modified website name.</span></span> <span data-ttu-id="44f39-150">For more information about deployment slots for web apps, see [Set up staging environments for web apps in Azure App Service](app-service-web/web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="44f39-150">For more information about deployment slots for web apps, see [Set up staging environments for web apps in Azure App Service](app-service-web/web-sites-staged-publishing.md).</span></span>

## <a name="how-to-run-the-publish-scripts"></a><span data-ttu-id="44f39-151">How to run the publish scripts</span><span class="sxs-lookup"><span data-stu-id="44f39-151">How to run the publish scripts</span></span>
<span data-ttu-id="44f39-152">If you have never run a Windows PowerShell script before, you must first set the execution policy to enable scripts to run.</span><span class="sxs-lookup"><span data-stu-id="44f39-152">If you have never run a Windows PowerShell script before, you must first set the execution policy to enable scripts to run.</span></span> <span data-ttu-id="44f39-153">This is a security feature to prevent users from running Windows PowerShell scripts if they're vulnerable to malware or viruses that involve executing scripts.</span><span class="sxs-lookup"><span data-stu-id="44f39-153">This is a security feature to prevent users from running Windows PowerShell scripts if they're vulnerable to malware or viruses that involve executing scripts.</span></span>

### <a name="run-the-script"></a><span data-ttu-id="44f39-154">Run the script</span><span class="sxs-lookup"><span data-stu-id="44f39-154">Run the script</span></span>
1. <span data-ttu-id="44f39-155">Create the Web Deploy package for your project.</span><span class="sxs-lookup"><span data-stu-id="44f39-155">Create the Web Deploy package for your project.</span></span> <span data-ttu-id="44f39-156">A Web Deploy package is a compressed archive (.zip file) that contain files that you want to copy to your website or virtual machine.</span><span class="sxs-lookup"><span data-stu-id="44f39-156">A Web Deploy package is a compressed archive (.zip file) that contain files that you want to copy to your website or virtual machine.</span></span> <span data-ttu-id="44f39-157">You can create Web Deploy packages in Visual Studio for any web application.</span><span class="sxs-lookup"><span data-stu-id="44f39-157">You can create Web Deploy packages in Visual Studio for any web application.</span></span>

![Create Web Deploy Package](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

<span data-ttu-id="44f39-159">For more information, see [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="44f39-159">For more information, see [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span> <span data-ttu-id="44f39-160">You can also automate the creation of your Web Deploy package, as described in the section **Customizing and extending the publish scripts** later in this topic.</span><span class="sxs-lookup"><span data-stu-id="44f39-160">You can also automate the creation of your Web Deploy package, as described in the section **Customizing and extending the publish scripts** later in this topic.</span></span>

1. <span data-ttu-id="44f39-161">In **Solution Explorer**, open the context menu for the script, and then choose **Open with PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="44f39-161">In **Solution Explorer**, open the context menu for the script, and then choose **Open with PowerShell ISE**.</span></span>
2. <span data-ttu-id="44f39-162">If this is the first time you've run Windows PowerShell scripts on this computer, open a command prompt window with Administrator privileges and type the following command:</span><span class="sxs-lookup"><span data-stu-id="44f39-162">If this is the first time you've run Windows PowerShell scripts on this computer, open a command prompt window with Administrator privileges and type the following command:</span></span>

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. <span data-ttu-id="44f39-163">Sign in to Azure by using the following command.</span><span class="sxs-lookup"><span data-stu-id="44f39-163">Sign in to Azure by using the following command.</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="44f39-164">When prompted, supply your username and password.</span><span class="sxs-lookup"><span data-stu-id="44f39-164">When prompted, supply your username and password.</span></span>

    <span data-ttu-id="44f39-165">Note that when you automate the script, this method of providing Azure credentials won't work.</span><span class="sxs-lookup"><span data-stu-id="44f39-165">Note that when you automate the script, this method of providing Azure credentials won't work.</span></span> <span data-ttu-id="44f39-166">Instead, you should use the .publishsettings file to provide credentials.</span><span class="sxs-lookup"><span data-stu-id="44f39-166">Instead, you should use the .publishsettings file to provide credentials.</span></span> <span data-ttu-id="44f39-167">One time only, you use the command **Get-AzurePublishSettingsFile** to download the file from Azure, and thereafter use **Import-AzurePublishSettingsFile** to import the file.</span><span class="sxs-lookup"><span data-stu-id="44f39-167">One time only, you use the command **Get-AzurePublishSettingsFile** to download the file from Azure, and thereafter use **Import-AzurePublishSettingsFile** to import the file.</span></span> <span data-ttu-id="44f39-168">For detailed instructions, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="44f39-168">For detailed instructions, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

4. <span data-ttu-id="44f39-169">(Optional) If you want to create Azure resources such as the virtual machine, database, and website without publishing your web application, use the **Publish-WebApplication.ps1** command with the **-Configuration** argument set to the JSON configuration file.</span><span class="sxs-lookup"><span data-stu-id="44f39-169">(Optional) If you want to create Azure resources such as the virtual machine, database, and website without publishing your web application, use the **Publish-WebApplication.ps1** command with the **-Configuration** argument set to the JSON configuration file.</span></span> <span data-ttu-id="44f39-170">This command line uses the JSON configuration file to determine which resources to create.</span><span class="sxs-lookup"><span data-stu-id="44f39-170">This command line uses the JSON configuration file to determine which resources to create.</span></span> <span data-ttu-id="44f39-171">Because it uses the default settings for other command-line arguments, it creates the resources, but doesn't publish your web application.</span><span class="sxs-lookup"><span data-stu-id="44f39-171">Because it uses the default settings for other command-line arguments, it creates the resources, but doesn't publish your web application.</span></span> <span data-ttu-id="44f39-172">The –Verbose option gives you more information about what's happening.</span><span class="sxs-lookup"><span data-stu-id="44f39-172">The –Verbose option gives you more information about what's happening.</span></span>

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. <span data-ttu-id="44f39-173">Use the **Publish-WebApplication.ps1** command as shown in one of the following examples to invoke the script and publish your web application.</span><span class="sxs-lookup"><span data-stu-id="44f39-173">Use the **Publish-WebApplication.ps1** command as shown in one of the following examples to invoke the script and publish your web application.</span></span> <span data-ttu-id="44f39-174">If you need to override the default settings for any of the other arguments, such as the subscription name, publish package name, virtual machine credentials, or database server credentials, you can specify those parameters.</span><span class="sxs-lookup"><span data-stu-id="44f39-174">If you need to override the default settings for any of the other arguments, such as the subscription name, publish package name, virtual machine credentials, or database server credentials, you can specify those parameters.</span></span> <span data-ttu-id="44f39-175">Use the **–Verbose** option to see more information about the progress of the publishing process.</span><span class="sxs-lookup"><span data-stu-id="44f39-175">Use the **–Verbose** option to see more information about the progress of the publishing process.</span></span>

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    <span data-ttu-id="44f39-176">If you're creating a virtual machine, the command looks like the following.</span><span class="sxs-lookup"><span data-stu-id="44f39-176">If you're creating a virtual machine, the command looks like the following.</span></span> <span data-ttu-id="44f39-177">This example also shows how to specify the credentials for multiple databases.</span><span class="sxs-lookup"><span data-stu-id="44f39-177">This example also shows how to specify the credentials for multiple databases.</span></span> <span data-ttu-id="44f39-178">For the virtual machines that these scripts create, the SSL certificate is not from a trusted root authority.</span><span class="sxs-lookup"><span data-stu-id="44f39-178">For the virtual machines that these scripts create, the SSL certificate is not from a trusted root authority.</span></span> <span data-ttu-id="44f39-179">Therefore, you need to use the **–AllowUntrusted** option.</span><span class="sxs-lookup"><span data-stu-id="44f39-179">Therefore, you need to use the **–AllowUntrusted** option.</span></span>

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    <span data-ttu-id="44f39-180">The script can create databases, but it doesn't create database servers.</span><span class="sxs-lookup"><span data-stu-id="44f39-180">The script can create databases, but it doesn't create database servers.</span></span> <span data-ttu-id="44f39-181">If you want to create a database server, you can use the **New-AzureSqlDatabaseServer** function in the Azure module.</span><span class="sxs-lookup"><span data-stu-id="44f39-181">If you want to create a database server, you can use the **New-AzureSqlDatabaseServer** function in the Azure module.</span></span>

## <a name="customizing-and-extending-the-publish-scripts"></a><span data-ttu-id="44f39-182">Customizing and extending the publish scripts</span><span class="sxs-lookup"><span data-stu-id="44f39-182">Customizing and extending the publish scripts</span></span>
<span data-ttu-id="44f39-183">You can customize the publish script and JSON configuration file.</span><span class="sxs-lookup"><span data-stu-id="44f39-183">You can customize the publish script and JSON configuration file.</span></span> <span data-ttu-id="44f39-184">The functions in the Windows PowerShell module **AzureWebAppPublishModule.psm1** are not intended to be modified.</span><span class="sxs-lookup"><span data-stu-id="44f39-184">The functions in the Windows PowerShell module **AzureWebAppPublishModule.psm1** are not intended to be modified.</span></span> <span data-ttu-id="44f39-185">If you just want to specify a different database or change some of the properties of the virtual machine, edit the JSON configuration file.</span><span class="sxs-lookup"><span data-stu-id="44f39-185">If you just want to specify a different database or change some of the properties of the virtual machine, edit the JSON configuration file.</span></span> <span data-ttu-id="44f39-186">If you want to extend the functionality of the script to automate building and testing your project, you can implement function stubs in **Publish-WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="44f39-186">If you want to extend the functionality of the script to automate building and testing your project, you can implement function stubs in **Publish-WebApplication.ps1**.</span></span>

<span data-ttu-id="44f39-187">To automate building your project, add code that calls MSBuild to `New-WebDeployPackage` as shown in this code example.</span><span class="sxs-lookup"><span data-stu-id="44f39-187">To automate building your project, add code that calls MSBuild to `New-WebDeployPackage` as shown in this code example.</span></span> <span data-ttu-id="44f39-188">The path to the MSBuild command is different depending on the version of Visual Studio you have installed.</span><span class="sxs-lookup"><span data-stu-id="44f39-188">The path to the MSBuild command is different depending on the version of Visual Studio you have installed.</span></span> <span data-ttu-id="44f39-189">To get the correct path, you can use the function **Get-MSBuildCmd**, as shown in this example.</span><span class="sxs-lookup"><span data-stu-id="44f39-189">To get the correct path, you can use the function **Get-MSBuildCmd**, as shown in this example.</span></span>

### <a name="to-automate-building-your-project"></a><span data-ttu-id="44f39-190">To automate building your project</span><span class="sxs-lookup"><span data-stu-id="44f39-190">To automate building your project</span></span>
1. <span data-ttu-id="44f39-191">Add the `$ProjectFile` parameter in the global param section.</span><span class="sxs-lookup"><span data-stu-id="44f39-191">Add the `$ProjectFile` parameter in the global param section.</span></span>

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. <span data-ttu-id="44f39-192">Copy the function `Get-MSBuildCmd` into your script file.</span><span class="sxs-lookup"><span data-stu-id="44f39-192">Copy the function `Get-MSBuildCmd` into your script file.</span></span>

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

3. <span data-ttu-id="44f39-193">Replace `New-WebDeployPackage` with the following code and replace the placeholders in the line constructing `$msbuildCmd`.</span><span class="sxs-lookup"><span data-stu-id="44f39-193">Replace `New-WebDeployPackage` with the following code and replace the placeholders in the line constructing `$msbuildCmd`.</span></span> <span data-ttu-id="44f39-194">This code is for Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="44f39-194">This code is for Visual Studio 2015.</span></span> <span data-ttu-id="44f39-195">If you're using Visual Studio 2013, change the **VisualStudioVersion** property below to `12.0`.</span><span class="sxs-lookup"><span data-stu-id="44f39-195">If you're using Visual Studio 2013, change the **VisualStudioVersion** property below to `12.0`.</span></span>

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function to build and package your web application
    ```

    <span data-ttu-id="44f39-196">To build your web application, use MsBuild.exe.</span><span class="sxs-lookup"><span data-stu-id="44f39-196">To build your web application, use MsBuild.exe.</span></span> <span data-ttu-id="44f39-197">For help, see MSBuild Command-Line Reference at: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span><span class="sxs-lookup"><span data-stu-id="44f39-197">For help, see MSBuild Command-Line Reference at: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span></span>

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-the-build-command"></a><span data-ttu-id="44f39-198">Start execution of the build command</span><span class="sxs-lookup"><span data-stu-id="44f39-198">Start execution of the build command</span></span>

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain the project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct the path to web deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get the full path for the web deploy zip package. This is required for MSDeploy to work
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. <span data-ttu-id="44f39-199">Call the `New-WebDeployPackage` function before this line: `$Config = Read-ConfigFile $Configuration` for web apps or `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` for virtual machines.</span><span class="sxs-lookup"><span data-stu-id="44f39-199">Call the `New-WebDeployPackage` function before this line: `$Config = Read-ConfigFile $Configuration` for web apps or `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` for virtual machines.</span></span>

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. <span data-ttu-id="44f39-200">Invoke the customized script from command line using passing the `$Project` argument, as in the following example command line.</span><span class="sxs-lookup"><span data-stu-id="44f39-200">Invoke the customized script from command line using passing the `$Project` argument, as in the following example command line.</span></span>

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    <span data-ttu-id="44f39-201">To automate testing of your application, add code to `Test-WebApplication`.</span><span class="sxs-lookup"><span data-stu-id="44f39-201">To automate testing of your application, add code to `Test-WebApplication`.</span></span> <span data-ttu-id="44f39-202">Be sure to uncomment the lines in **Publish-WebApplication.ps1** where these functions are called.</span><span class="sxs-lookup"><span data-stu-id="44f39-202">Be sure to uncomment the lines in **Publish-WebApplication.ps1** where these functions are called.</span></span> <span data-ttu-id="44f39-203">If you don't provide an implementation, you can manually build your project with Visual Studio, and then run the publish script to publish to Azure.</span><span class="sxs-lookup"><span data-stu-id="44f39-203">If you don't provide an implementation, you can manually build your project with Visual Studio, and then run the publish script to publish to Azure.</span></span>

## <a name="publishing-function-summary"></a><span data-ttu-id="44f39-204">Publishing function summary</span><span class="sxs-lookup"><span data-stu-id="44f39-204">Publishing function summary</span></span>
<span data-ttu-id="44f39-205">To get help for functions you can use at the Windows PowerShell command prompt, use the command `Get-Help function-name`.</span><span class="sxs-lookup"><span data-stu-id="44f39-205">To get help for functions you can use at the Windows PowerShell command prompt, use the command `Get-Help function-name`.</span></span> <span data-ttu-id="44f39-206">The help includes parameter help and examples.</span><span class="sxs-lookup"><span data-stu-id="44f39-206">The help includes parameter help and examples.</span></span> <span data-ttu-id="44f39-207">The same help text is also in the script source files, **AzureWebAppPublishModule.psm1** and **Publish-WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="44f39-207">The same help text is also in the script source files, **AzureWebAppPublishModule.psm1** and **Publish-WebApplication.ps1**.</span></span> <span data-ttu-id="44f39-208">The script and help are localized in your Visual Studio language.</span><span class="sxs-lookup"><span data-stu-id="44f39-208">The script and help are localized in your Visual Studio language.</span></span>

<span data-ttu-id="44f39-209">**AzureWebAppPublishModule**</span><span class="sxs-lookup"><span data-stu-id="44f39-209">**AzureWebAppPublishModule**</span></span>

| <span data-ttu-id="44f39-210">Function name</span><span class="sxs-lookup"><span data-stu-id="44f39-210">Function name</span></span> | <span data-ttu-id="44f39-211">Description</span><span class="sxs-lookup"><span data-stu-id="44f39-211">Description</span></span> |
| --- | --- |
| <span data-ttu-id="44f39-212">Add-AzureSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="44f39-212">Add-AzureSQLDatabase</span></span> |<span data-ttu-id="44f39-213">Creates a new Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="44f39-213">Creates a new Azure SQL database.</span></span> |
| <span data-ttu-id="44f39-214">Add-AzureSQLDatabases</span><span class="sxs-lookup"><span data-stu-id="44f39-214">Add-AzureSQLDatabases</span></span> |<span data-ttu-id="44f39-215">Creates Azure SQL databases from the values in the JSON configuration file that Visual Studio generates.</span><span class="sxs-lookup"><span data-stu-id="44f39-215">Creates Azure SQL databases from the values in the JSON configuration file that Visual Studio generates.</span></span> |
| <span data-ttu-id="44f39-216">Add-AzureVM</span><span class="sxs-lookup"><span data-stu-id="44f39-216">Add-AzureVM</span></span> |<span data-ttu-id="44f39-217">Creates a Azure virtual machine and returns the URL of the deployed VM.</span><span class="sxs-lookup"><span data-stu-id="44f39-217">Creates a Azure virtual machine and returns the URL of the deployed VM.</span></span> <span data-ttu-id="44f39-218">The function sets up the prerequisites and then calls the **New-AzureVM** function (Azure module) to create a new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="44f39-218">The function sets up the prerequisites and then calls the **New-AzureVM** function (Azure module) to create a new virtual machine.</span></span> |
| <span data-ttu-id="44f39-219">Add-AzureVMEndpoints</span><span class="sxs-lookup"><span data-stu-id="44f39-219">Add-AzureVMEndpoints</span></span> |<span data-ttu-id="44f39-220">Adds new input endpoints to a virtual machine and returns the virtual machine with the new endpoint.</span><span class="sxs-lookup"><span data-stu-id="44f39-220">Adds new input endpoints to a virtual machine and returns the virtual machine with the new endpoint.</span></span> |
| <span data-ttu-id="44f39-221">Add-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="44f39-221">Add-AzureVMStorage</span></span> |<span data-ttu-id="44f39-222">Creates a new Azure storage account in the current subscription.</span><span class="sxs-lookup"><span data-stu-id="44f39-222">Creates a new Azure storage account in the current subscription.</span></span> <span data-ttu-id="44f39-223">The name of the account begins with "devtest" followed by a unique alphanumeric string.</span><span class="sxs-lookup"><span data-stu-id="44f39-223">The name of the account begins with "devtest" followed by a unique alphanumeric string.</span></span> <span data-ttu-id="44f39-224">The function returns the name of the new storage account.</span><span class="sxs-lookup"><span data-stu-id="44f39-224">The function returns the name of the new storage account.</span></span> <span data-ttu-id="44f39-225">You must specify either a location or an affinity group for the new storage account.</span><span class="sxs-lookup"><span data-stu-id="44f39-225">You must specify either a location or an affinity group for the new storage account.</span></span> |
| <span data-ttu-id="44f39-226">Add-AzureWebsite</span><span class="sxs-lookup"><span data-stu-id="44f39-226">Add-AzureWebsite</span></span> |<span data-ttu-id="44f39-227">Creates a website with the specified name and location.</span><span class="sxs-lookup"><span data-stu-id="44f39-227">Creates a website with the specified name and location.</span></span> <span data-ttu-id="44f39-228">This function calls the **New-AzureWebsite** function in the Azure module.</span><span class="sxs-lookup"><span data-stu-id="44f39-228">This function calls the **New-AzureWebsite** function in the Azure module.</span></span> <span data-ttu-id="44f39-229">If the subscription doesn't already include a website with the specified name, this function creates the website and returns a website object.</span><span class="sxs-lookup"><span data-stu-id="44f39-229">If the subscription doesn't already include a website with the specified name, this function creates the website and returns a website object.</span></span> <span data-ttu-id="44f39-230">Otherwise, it returns `$null`.</span><span class="sxs-lookup"><span data-stu-id="44f39-230">Otherwise, it returns `$null`.</span></span> |
| <span data-ttu-id="44f39-231">Backup-Subscription</span><span class="sxs-lookup"><span data-stu-id="44f39-231">Backup-Subscription</span></span> |<span data-ttu-id="44f39-232">Saves the current Azure subscription in the `$Script:originalSubscription` variable in script scope.This function saves the current Azure subscription (as obtained by `Get-AzureSubscription -Current`) and its storage account, and the subscription that is changed by this script (stored in the variable `$UserSpecifiedSubscription`) and its storage account, in script scope.</span><span class="sxs-lookup"><span data-stu-id="44f39-232">Saves the current Azure subscription in the `$Script:originalSubscription` variable in script scope.This function saves the current Azure subscription (as obtained by `Get-AzureSubscription -Current`) and its storage account, and the subscription that is changed by this script (stored in the variable `$UserSpecifiedSubscription`) and its storage account, in script scope.</span></span> <span data-ttu-id="44f39-233">By saving the values, you can use a function, such as `Restore-Subscription`, to restore the original current subscription and storage account to current status if the current status has changed.</span><span class="sxs-lookup"><span data-stu-id="44f39-233">By saving the values, you can use a function, such as `Restore-Subscription`, to restore the original current subscription and storage account to current status if the current status has changed.</span></span> |
| <span data-ttu-id="44f39-234">Find-AzureVM</span><span class="sxs-lookup"><span data-stu-id="44f39-234">Find-AzureVM</span></span> |<span data-ttu-id="44f39-235">Gets the specified Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="44f39-235">Gets the specified Azure virtual machine.</span></span> |
| <span data-ttu-id="44f39-236">Format-DevTestMessageWithTime</span><span class="sxs-lookup"><span data-stu-id="44f39-236">Format-DevTestMessageWithTime</span></span> |<span data-ttu-id="44f39-237">Prepends the date and time to a message.</span><span class="sxs-lookup"><span data-stu-id="44f39-237">Prepends the date and time to a message.</span></span> <span data-ttu-id="44f39-238">This function is designed for messages written to the Error and Verbose streams.</span><span class="sxs-lookup"><span data-stu-id="44f39-238">This function is designed for messages written to the Error and Verbose streams.</span></span> |
| <span data-ttu-id="44f39-239">Get-AzureSQLDatabaseConnectionString</span><span class="sxs-lookup"><span data-stu-id="44f39-239">Get-AzureSQLDatabaseConnectionString</span></span> |<span data-ttu-id="44f39-240">Assembles a connection string to connect to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="44f39-240">Assembles a connection string to connect to an Azure SQL database.</span></span> |
| <span data-ttu-id="44f39-241">Get-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="44f39-241">Get-AzureVMStorage</span></span> |<span data-ttu-id="44f39-242">Returns the name of the first storage account with the name pattern "devtest *" (case insensitive) in the specified location or affinity group. If the "devtest*" storage account doesn't match the location or affinity group, the function ignores it.</span><span class="sxs-lookup"><span data-stu-id="44f39-242">Returns the name of the first storage account with the name pattern "devtest *" (case insensitive) in the specified location or affinity group. If the "devtest*" storage account doesn't match the location or affinity group, the function ignores it.</span></span> <span data-ttu-id="44f39-243">You must specify either a location or an affinity group.</span><span class="sxs-lookup"><span data-stu-id="44f39-243">You must specify either a location or an affinity group.</span></span> |
| <span data-ttu-id="44f39-244">Get-MSDeployCmd</span><span class="sxs-lookup"><span data-stu-id="44f39-244">Get-MSDeployCmd</span></span> |<span data-ttu-id="44f39-245">Returns a command to run the MsDeploy.exe tool.</span><span class="sxs-lookup"><span data-stu-id="44f39-245">Returns a command to run the MsDeploy.exe tool.</span></span> |
| <span data-ttu-id="44f39-246">New-AzureVMEnvironment</span><span class="sxs-lookup"><span data-stu-id="44f39-246">New-AzureVMEnvironment</span></span> |<span data-ttu-id="44f39-247">Finds or creates a virtual machine in the subscription that matches the values in the JSON configuration file.</span><span class="sxs-lookup"><span data-stu-id="44f39-247">Finds or creates a virtual machine in the subscription that matches the values in the JSON configuration file.</span></span> |
| <span data-ttu-id="44f39-248">Publish-WebPackage</span><span class="sxs-lookup"><span data-stu-id="44f39-248">Publish-WebPackage</span></span> |<span data-ttu-id="44f39-249">Uses MsDeploy.exe and a web publish package .Zip file to deploy resources to a website.</span><span class="sxs-lookup"><span data-stu-id="44f39-249">Uses MsDeploy.exe and a web publish package .Zip file to deploy resources to a website.</span></span> <span data-ttu-id="44f39-250">This function doesn't generate any output.</span><span class="sxs-lookup"><span data-stu-id="44f39-250">This function doesn't generate any output.</span></span> <span data-ttu-id="44f39-251">If the call to MSDeploy.exe fails, the function throws an exception.</span><span class="sxs-lookup"><span data-stu-id="44f39-251">If the call to MSDeploy.exe fails, the function throws an exception.</span></span> <span data-ttu-id="44f39-252">To get more detailed output, use the **-Verbose** option.</span><span class="sxs-lookup"><span data-stu-id="44f39-252">To get more detailed output, use the **-Verbose** option.</span></span> |
| <span data-ttu-id="44f39-253">Publish-WebPackageToVM</span><span class="sxs-lookup"><span data-stu-id="44f39-253">Publish-WebPackageToVM</span></span> |<span data-ttu-id="44f39-254">Verifies the parameter values, and then calls the **Publish-WebPackage** function.</span><span class="sxs-lookup"><span data-stu-id="44f39-254">Verifies the parameter values, and then calls the **Publish-WebPackage** function.</span></span> |
| <span data-ttu-id="44f39-255">Read-ConfigFile</span><span class="sxs-lookup"><span data-stu-id="44f39-255">Read-ConfigFile</span></span> |<span data-ttu-id="44f39-256">Validates the JSON configuration file and returns a hash table of selected values.</span><span class="sxs-lookup"><span data-stu-id="44f39-256">Validates the JSON configuration file and returns a hash table of selected values.</span></span> |
| <span data-ttu-id="44f39-257">Restore-Subscription</span><span class="sxs-lookup"><span data-stu-id="44f39-257">Restore-Subscription</span></span> |<span data-ttu-id="44f39-258">Resets the current subscription to the original subscription.</span><span class="sxs-lookup"><span data-stu-id="44f39-258">Resets the current subscription to the original subscription.</span></span> |
| <span data-ttu-id="44f39-259">Test-AzureModule</span><span class="sxs-lookup"><span data-stu-id="44f39-259">Test-AzureModule</span></span> |<span data-ttu-id="44f39-260">Returns `$true` if the installed Azure module version is 0.7.4 or later.</span><span class="sxs-lookup"><span data-stu-id="44f39-260">Returns `$true` if the installed Azure module version is 0.7.4 or later.</span></span> <span data-ttu-id="44f39-261">Returns `$false` if the module isn't installed or is an earlier version.</span><span class="sxs-lookup"><span data-stu-id="44f39-261">Returns `$false` if the module isn't installed or is an earlier version.</span></span> <span data-ttu-id="44f39-262">This function has no parameters.</span><span class="sxs-lookup"><span data-stu-id="44f39-262">This function has no parameters.</span></span> |
| <span data-ttu-id="44f39-263">Test-AzureModuleVersion</span><span class="sxs-lookup"><span data-stu-id="44f39-263">Test-AzureModuleVersion</span></span> |<span data-ttu-id="44f39-264">Returns `$true` if the version of the Azure module is 0.7.4 or later.</span><span class="sxs-lookup"><span data-stu-id="44f39-264">Returns `$true` if the version of the Azure module is 0.7.4 or later.</span></span> <span data-ttu-id="44f39-265">Returns `$false` if the module isn't installed or is an earlier version.</span><span class="sxs-lookup"><span data-stu-id="44f39-265">Returns `$false` if the module isn't installed or is an earlier version.</span></span> <span data-ttu-id="44f39-266">This function has no parameters.</span><span class="sxs-lookup"><span data-stu-id="44f39-266">This function has no parameters.</span></span> |
| <span data-ttu-id="44f39-267">Test-HttpsUrl</span><span class="sxs-lookup"><span data-stu-id="44f39-267">Test-HttpsUrl</span></span> |<span data-ttu-id="44f39-268">Converts the input URL to a System.Uri object.</span><span class="sxs-lookup"><span data-stu-id="44f39-268">Converts the input URL to a System.Uri object.</span></span> <span data-ttu-id="44f39-269">Returns `$True` if the URL is absolute and its scheme is https.</span><span class="sxs-lookup"><span data-stu-id="44f39-269">Returns `$True` if the URL is absolute and its scheme is https.</span></span> <span data-ttu-id="44f39-270">Returns `$false` if the URL is relative, its scheme isn't HTTPS, or the input string can't be converted to a URL.</span><span class="sxs-lookup"><span data-stu-id="44f39-270">Returns `$false` if the URL is relative, its scheme isn't HTTPS, or the input string can't be converted to a URL.</span></span> |
| <span data-ttu-id="44f39-271">Test-Member</span><span class="sxs-lookup"><span data-stu-id="44f39-271">Test-Member</span></span> |<span data-ttu-id="44f39-272">Returns `$true` if a property or method is a member of the object.</span><span class="sxs-lookup"><span data-stu-id="44f39-272">Returns `$true` if a property or method is a member of the object.</span></span> <span data-ttu-id="44f39-273">Otherwise, returns `$false`.</span><span class="sxs-lookup"><span data-stu-id="44f39-273">Otherwise, returns `$false`.</span></span> |
| <span data-ttu-id="44f39-274">Write-ErrorWithTime</span><span class="sxs-lookup"><span data-stu-id="44f39-274">Write-ErrorWithTime</span></span> |<span data-ttu-id="44f39-275">Writes an error message prefixed with the current time.</span><span class="sxs-lookup"><span data-stu-id="44f39-275">Writes an error message prefixed with the current time.</span></span> <span data-ttu-id="44f39-276">This function calls the **Format-DevTestMessageWithTime** function to prepend the time before writing the message to the Error stream.</span><span class="sxs-lookup"><span data-stu-id="44f39-276">This function calls the **Format-DevTestMessageWithTime** function to prepend the time before writing the message to the Error stream.</span></span> |
| <span data-ttu-id="44f39-277">Write-HostWithTime</span><span class="sxs-lookup"><span data-stu-id="44f39-277">Write-HostWithTime</span></span> |<span data-ttu-id="44f39-278">Writes a message to the host program (**Write-Host**) prefixed with the current time.</span><span class="sxs-lookup"><span data-stu-id="44f39-278">Writes a message to the host program (**Write-Host**) prefixed with the current time.</span></span> <span data-ttu-id="44f39-279">The effect of writing to the host program varies.</span><span class="sxs-lookup"><span data-stu-id="44f39-279">The effect of writing to the host program varies.</span></span> <span data-ttu-id="44f39-280">Most programs that host Windows PowerShell write these messages to standard output.</span><span class="sxs-lookup"><span data-stu-id="44f39-280">Most programs that host Windows PowerShell write these messages to standard output.</span></span> |
| <span data-ttu-id="44f39-281">Write-VerboseWithTime</span><span class="sxs-lookup"><span data-stu-id="44f39-281">Write-VerboseWithTime</span></span> |<span data-ttu-id="44f39-282">Writes a verbose message prefixed with the current time.</span><span class="sxs-lookup"><span data-stu-id="44f39-282">Writes a verbose message prefixed with the current time.</span></span> <span data-ttu-id="44f39-283">Because it calls **Write-Verbose**, the message displays only when the script runs with the **Verbose** parameter or when the **VerbosePreference** preference is set to **Continue**.</span><span class="sxs-lookup"><span data-stu-id="44f39-283">Because it calls **Write-Verbose**, the message displays only when the script runs with the **Verbose** parameter or when the **VerbosePreference** preference is set to **Continue**.</span></span> |

<span data-ttu-id="44f39-284">**Publish-WebApplication**</span><span class="sxs-lookup"><span data-stu-id="44f39-284">**Publish-WebApplication**</span></span>

| <span data-ttu-id="44f39-285">Function name</span><span class="sxs-lookup"><span data-stu-id="44f39-285">Function name</span></span> | <span data-ttu-id="44f39-286">Description</span><span class="sxs-lookup"><span data-stu-id="44f39-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="44f39-287">New-AzureWebApplicationEnvironment</span><span class="sxs-lookup"><span data-stu-id="44f39-287">New-AzureWebApplicationEnvironment</span></span> |<span data-ttu-id="44f39-288">Creates Azure resources, such as a website or virtual machine.</span><span class="sxs-lookup"><span data-stu-id="44f39-288">Creates Azure resources, such as a website or virtual machine.</span></span> |
| <span data-ttu-id="44f39-289">New-WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="44f39-289">New-WebDeployPackage</span></span> |<span data-ttu-id="44f39-290">This function isn't implemented.</span><span class="sxs-lookup"><span data-stu-id="44f39-290">This function isn't implemented.</span></span> <span data-ttu-id="44f39-291">You can add commands in this function to build your project.</span><span class="sxs-lookup"><span data-stu-id="44f39-291">You can add commands in this function to build your project.</span></span> |
| <span data-ttu-id="44f39-292">Publish-AzureWebApplication</span><span class="sxs-lookup"><span data-stu-id="44f39-292">Publish-AzureWebApplication</span></span> |<span data-ttu-id="44f39-293">Publishes a web application to Azure.</span><span class="sxs-lookup"><span data-stu-id="44f39-293">Publishes a web application to Azure.</span></span> |
| <span data-ttu-id="44f39-294">Publish-WebApplication</span><span class="sxs-lookup"><span data-stu-id="44f39-294">Publish-WebApplication</span></span> |<span data-ttu-id="44f39-295">Creates and deploys Web Apps, virtual machines, SQL databases, and storage accounts for a Visual Studio web project.</span><span class="sxs-lookup"><span data-stu-id="44f39-295">Creates and deploys Web Apps, virtual machines, SQL databases, and storage accounts for a Visual Studio web project.</span></span> |
| <span data-ttu-id="44f39-296">Test-WebApplication</span><span class="sxs-lookup"><span data-stu-id="44f39-296">Test-WebApplication</span></span> |<span data-ttu-id="44f39-297">This function isn't implemented.</span><span class="sxs-lookup"><span data-stu-id="44f39-297">This function isn't implemented.</span></span> <span data-ttu-id="44f39-298">You can add commands in this function to test your application.</span><span class="sxs-lookup"><span data-stu-id="44f39-298">You can add commands in this function to test your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="44f39-299">Next steps</span><span class="sxs-lookup"><span data-stu-id="44f39-299">Next steps</span></span>
<span data-ttu-id="44f39-300">Learn more about PowerShell scripting by reading [Scripting with Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) and see other Azure PowerShell scripts at the [Script Center](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="44f39-300">Learn more about PowerShell scripting by reading [Scripting with Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) and see other Azure PowerShell scripts at the [Script Center](https://azure.microsoft.com/documentation/scripts/).</span></span>

