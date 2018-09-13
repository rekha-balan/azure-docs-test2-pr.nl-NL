---
title: Specifying a Node.js Version
description: Learn how to specify the version of Node.js used by Azure Web Sites and Cloud Services
services: ''
documentationcenter: nodejs
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: 7129137e6deca6ae4cbb5096058b58b32056d415
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553336"
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a><span data-ttu-id="f760b-103">Specifying a Node.js version in an Azure application</span><span class="sxs-lookup"><span data-stu-id="f760b-103">Specifying a Node.js version in an Azure application</span></span>
<span data-ttu-id="f760b-104">When hosting a Node.js application, you may want to ensure that your application uses a specific version of Node.js.</span><span class="sxs-lookup"><span data-stu-id="f760b-104">When hosting a Node.js application, you may want to ensure that your application uses a specific version of Node.js.</span></span> <span data-ttu-id="f760b-105">There are several ways to accomplish this for applications hosted on Azure.</span><span class="sxs-lookup"><span data-stu-id="f760b-105">There are several ways to accomplish this for applications hosted on Azure.</span></span>

## <a name="default-versions"></a><span data-ttu-id="f760b-106">Default versions</span><span class="sxs-lookup"><span data-stu-id="f760b-106">Default versions</span></span>
<span data-ttu-id="f760b-107">The Node.js versions provided by Azure are constantly updated.</span><span class="sxs-lookup"><span data-stu-id="f760b-107">The Node.js versions provided by Azure are constantly updated.</span></span> <span data-ttu-id="f760b-108">Unless otherwise specified, the default version that is specified in the `WEBSITE_NODE_DEFAULT_VERSION` environment variable will be used.</span><span class="sxs-lookup"><span data-stu-id="f760b-108">Unless otherwise specified, the default version that is specified in the `WEBSITE_NODE_DEFAULT_VERSION` environment variable will be used.</span></span> <span data-ttu-id="f760b-109">To override this default value, follow the steps in following sections of this article</span><span class="sxs-lookup"><span data-stu-id="f760b-109">To override this default value, follow the steps in following sections of this article</span></span>

> [!NOTE]
> <span data-ttu-id="f760b-110">If you are hosting your application in an Azure Cloud Service (web or worker role,) and it is the first time you have deployed the application, Azure will attempt to use the same version of Node.js as you have installed on your development environment if it matches one of the default versions available on Azure.</span><span class="sxs-lookup"><span data-stu-id="f760b-110">If you are hosting your application in an Azure Cloud Service (web or worker role,) and it is the first time you have deployed the application, Azure will attempt to use the same version of Node.js as you have installed on your development environment if it matches one of the default versions available on Azure.</span></span>
>
>

## <a name="versioning-with-packagejson"></a><span data-ttu-id="f760b-111">Versioning with package.json</span><span class="sxs-lookup"><span data-stu-id="f760b-111">Versioning with package.json</span></span>
<span data-ttu-id="f760b-112">You can specify the version of Node.js to be used by adding the following to your **package.json** file:</span><span class="sxs-lookup"><span data-stu-id="f760b-112">You can specify the version of Node.js to be used by adding the following to your **package.json** file:</span></span>

    "engines":{"node":version}

<span data-ttu-id="f760b-113">Where *version* is the specific version number to use.</span><span class="sxs-lookup"><span data-stu-id="f760b-113">Where *version* is the specific version number to use.</span></span> <span data-ttu-id="f760b-114">You can specify more complex conditions for version, such as:</span><span class="sxs-lookup"><span data-stu-id="f760b-114">You can specify more complex conditions for version, such as:</span></span>

    "engines":{"node": "0.6.22 || 0.8.x"}

<span data-ttu-id="f760b-115">Since 0.6.22 is not one of the versions available in the hosting environment, the highest version of the 0.8 series that is available will be used instead - 0.8.4.</span><span class="sxs-lookup"><span data-stu-id="f760b-115">Since 0.6.22 is not one of the versions available in the hosting environment, the highest version of the 0.8 series that is available will be used instead - 0.8.4.</span></span>

## <a name="versioning-websites-with-app-settings"></a><span data-ttu-id="f760b-116">Versioning Websites with App Settings</span><span class="sxs-lookup"><span data-stu-id="f760b-116">Versioning Websites with App Settings</span></span>
<span data-ttu-id="f760b-117">If you are hosting the application in a Website, you can set the environment variable **WEBSITE_NODE_DEFAULT_VERSION** to the desired version.</span><span class="sxs-lookup"><span data-stu-id="f760b-117">If you are hosting the application in a Website, you can set the environment variable **WEBSITE_NODE_DEFAULT_VERSION** to the desired version.</span></span>

## <a name="versioning-cloud-services-with-powershell"></a><span data-ttu-id="f760b-118">Versioning Cloud Services with PowerShell</span><span class="sxs-lookup"><span data-stu-id="f760b-118">Versioning Cloud Services with PowerShell</span></span>
<span data-ttu-id="f760b-119">If you are hosting the application in a Cloud Service, and are deploying the application using Azure PowerShell, you can override the default Node.js version by using the **Set-AzureServiceProjectRole** PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f760b-119">If you are hosting the application in a Cloud Service, and are deploying the application using Azure PowerShell, you can override the default Node.js version by using the **Set-AzureServiceProjectRole** PowerShell cmdlet.</span></span> <span data-ttu-id="f760b-120">For example:</span><span class="sxs-lookup"><span data-stu-id="f760b-120">For example:</span></span>

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

<span data-ttu-id="f760b-121">Note the parameters in the above statement are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="f760b-121">Note the parameters in the above statement are case-sensitive.</span></span>  <span data-ttu-id="f760b-122">You can verify the correct version of Node.js has been selected by checking the **engines** property in your role's **package.json**.</span><span class="sxs-lookup"><span data-stu-id="f760b-122">You can verify the correct version of Node.js has been selected by checking the **engines** property in your role's **package.json**.</span></span>

<span data-ttu-id="f760b-123">You can also use the **Get-AzureServiceProjectRoleRuntime** to retrieve a list of Node.js versions available for applications hosted as a Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="f760b-123">You can also use the **Get-AzureServiceProjectRoleRuntime** to retrieve a list of Node.js versions available for applications hosted as a Cloud Service.</span></span>  <span data-ttu-id="f760b-124">Always verify the version of Node.js your project depends on is in this list.</span><span class="sxs-lookup"><span data-stu-id="f760b-124">Always verify the version of Node.js your project depends on is in this list.</span></span>

## <a name="using-a-custom-version-with-azure-websites"></a><span data-ttu-id="f760b-125">Using a custom version with Azure Websites</span><span class="sxs-lookup"><span data-stu-id="f760b-125">Using a custom version with Azure Websites</span></span>
<span data-ttu-id="f760b-126">While Azure provides several default versions of Node.js, you may want to use a version that is not provided by default.</span><span class="sxs-lookup"><span data-stu-id="f760b-126">While Azure provides several default versions of Node.js, you may want to use a version that is not provided by default.</span></span> <span data-ttu-id="f760b-127">If your application is hosted as an Azure Website, you can accomplish this by using the **iisnode.yml** file.</span><span class="sxs-lookup"><span data-stu-id="f760b-127">If your application is hosted as an Azure Website, you can accomplish this by using the **iisnode.yml** file.</span></span> <span data-ttu-id="f760b-128">The following steps walk through the process of using a custom version of Node.Js with an Azure Website:</span><span class="sxs-lookup"><span data-stu-id="f760b-128">The following steps walk through the process of using a custom version of Node.Js with an Azure Website:</span></span>

1. <span data-ttu-id="f760b-129">Create a new directory, and then create a **server.js** file within the directory.</span><span class="sxs-lookup"><span data-stu-id="f760b-129">Create a new directory, and then create a **server.js** file within the directory.</span></span> <span data-ttu-id="f760b-130">The **server.js** file should contain the following:</span><span class="sxs-lookup"><span data-stu-id="f760b-130">The **server.js** file should contain the following:</span></span>

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    <span data-ttu-id="f760b-131">This will display the Node.js version being used when you browse the website.</span><span class="sxs-lookup"><span data-stu-id="f760b-131">This will display the Node.js version being used when you browse the website.</span></span>
2. <span data-ttu-id="f760b-132">Create a new Website and note the name of the site.</span><span class="sxs-lookup"><span data-stu-id="f760b-132">Create a new Website and note the name of the site.</span></span> <span data-ttu-id="f760b-133">For example, the following uses the [Azure Command-line tools] to create a new Azure Website named **mywebsite**, and then enable a Git repository for the website.</span><span class="sxs-lookup"><span data-stu-id="f760b-133">For example, the following uses the [Azure Command-line tools] to create a new Azure Website named **mywebsite**, and then enable a Git repository for the website.</span></span>

        azure site create mywebsite --git
3. <span data-ttu-id="f760b-134">Create a new directory named **bin** as a child of the directory containing the **server.js** file.</span><span class="sxs-lookup"><span data-stu-id="f760b-134">Create a new directory named **bin** as a child of the directory containing the **server.js** file.</span></span>
4. <span data-ttu-id="f760b-135">Download the specific version of **node.exe** (the Windows version) that you wish to use with your application.</span><span class="sxs-lookup"><span data-stu-id="f760b-135">Download the specific version of **node.exe** (the Windows version) that you wish to use with your application.</span></span> <span data-ttu-id="f760b-136">For example, the following uses **curl** to download version 0.8.1:</span><span class="sxs-lookup"><span data-stu-id="f760b-136">For example, the following uses **curl** to download version 0.8.1:</span></span>

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    <span data-ttu-id="f760b-137">Save the **node.exe** file into the **bin** folder created previously.</span><span class="sxs-lookup"><span data-stu-id="f760b-137">Save the **node.exe** file into the **bin** folder created previously.</span></span>
5. <span data-ttu-id="f760b-138">Create an **iisnode.yml** file in the same directory as the **server.js** file, and then add the following content to the **iisnode.yml** file:</span><span class="sxs-lookup"><span data-stu-id="f760b-138">Create an **iisnode.yml** file in the same directory as the **server.js** file, and then add the following content to the **iisnode.yml** file:</span></span>

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    <span data-ttu-id="f760b-139">This path is where the **node.exe** file within your project will be located once you have published your application to the Azure Website.</span><span class="sxs-lookup"><span data-stu-id="f760b-139">This path is where the **node.exe** file within your project will be located once you have published your application to the Azure Website.</span></span>
6. <span data-ttu-id="f760b-140">Publish your application.</span><span class="sxs-lookup"><span data-stu-id="f760b-140">Publish your application.</span></span> <span data-ttu-id="f760b-141">For example, since I created a new website with the --git parameter earlier, the following commands will add the application files to my local Git repository, and then push them to the website repository:</span><span class="sxs-lookup"><span data-stu-id="f760b-141">For example, since I created a new website with the --git parameter earlier, the following commands will add the application files to my local Git repository, and then push them to the website repository:</span></span>

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    <span data-ttu-id="f760b-142">After the application has published, open the website in a browser.</span><span class="sxs-lookup"><span data-stu-id="f760b-142">After the application has published, open the website in a browser.</span></span> <span data-ttu-id="f760b-143">You should see a message stating "Hello from Azure running node version: v0.8.1".</span><span class="sxs-lookup"><span data-stu-id="f760b-143">You should see a message stating "Hello from Azure running node version: v0.8.1".</span></span>

## <a name="next-steps"></a><span data-ttu-id="f760b-144">Next Steps</span><span class="sxs-lookup"><span data-stu-id="f760b-144">Next Steps</span></span>
<span data-ttu-id="f760b-145">Now that you understand how to specify the version of Node.js used by your application, learn how to [work with modules], [build and deploy a Node.js Web Site](app-service-web/app-service-web-get-started-nodejs.md), and [How to use the Azure Command-Line Tools for Mac and Linux].</span><span class="sxs-lookup"><span data-stu-id="f760b-145">Now that you understand how to specify the version of Node.js used by your application, learn how to [work with modules], [build and deploy a Node.js Web Site](app-service-web/app-service-web-get-started-nodejs.md), and [How to use the Azure Command-Line Tools for Mac and Linux].</span></span>

<span data-ttu-id="f760b-146">For more information, see the [Node.js Developer Center](https://azure.microsoft.com/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="f760b-146">For more information, see the [Node.js Developer Center](https://azure.microsoft.com/develop/nodejs/).</span></span>

[How to use the Azure Command-Line Tools for Mac and Linux]:cli-install-nodejs.md
[Azure Command-line tools]:cli-install-nodejs.md
[work with modules]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
