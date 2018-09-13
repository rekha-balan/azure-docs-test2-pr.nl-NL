---
title: Node.js Getting Started Guide
description: Learn how to create a simple Node.js web application and deploy it to an Azure cloud service.
services: cloud-services
documentationcenter: nodejs
author: jpconnock
manager: timlt
editor: ''
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: jeconnoc
ms.openlocfilehash: 1a2dedaca44785634376b7b3b15579b96ee6ff5d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809327"
---
# <a name="build-and-deploy-a-nodejs-application-to-an-azure-cloud-service"></a><span data-ttu-id="34923-103">Build and deploy a Node.js application to an Azure Cloud Service</span><span class="sxs-lookup"><span data-stu-id="34923-103">Build and deploy a Node.js application to an Azure Cloud Service</span></span>

<span data-ttu-id="34923-104">This tutorial shows how to create a simple Node.js application running in an Azure Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="34923-104">This tutorial shows how to create a simple Node.js application running in an Azure Cloud Service.</span></span> <span data-ttu-id="34923-105">Cloud Services are the building blocks of scalable cloud applications in Azure.</span><span class="sxs-lookup"><span data-stu-id="34923-105">Cloud Services are the building blocks of scalable cloud applications in Azure.</span></span> <span data-ttu-id="34923-106">They allow the separation and independent management and scale-out of front-end and back-end components of your application.</span><span class="sxs-lookup"><span data-stu-id="34923-106">They allow the separation and independent management and scale-out of front-end and back-end components of your application.</span></span>  <span data-ttu-id="34923-107">Cloud Services provide a robust dedicated virtual machine for hosting each role reliably.</span><span class="sxs-lookup"><span data-stu-id="34923-107">Cloud Services provide a robust dedicated virtual machine for hosting each role reliably.</span></span>

<span data-ttu-id="34923-108">For more information on Cloud Services, and how they compare to Azure Websites and Virtual machines, see [Azure Websites, Cloud Services and Virtual Machines comparison].</span><span class="sxs-lookup"><span data-stu-id="34923-108">For more information on Cloud Services, and how they compare to Azure Websites and Virtual machines, see [Azure Websites, Cloud Services and Virtual Machines comparison].</span></span>

> [!TIP]
> <span data-ttu-id="34923-109">Looking to build a simple website?</span><span class="sxs-lookup"><span data-stu-id="34923-109">Looking to build a simple website?</span></span> <span data-ttu-id="34923-110">If your scenario involves just a simple website front-end, consider [using a lightweight web app].</span><span class="sxs-lookup"><span data-stu-id="34923-110">If your scenario involves just a simple website front-end, consider [using a lightweight web app].</span></span> <span data-ttu-id="34923-111">You can easily upgrade to a Cloud Service as your web app grows and your requirements change.</span><span class="sxs-lookup"><span data-stu-id="34923-111">You can easily upgrade to a Cloud Service as your web app grows and your requirements change.</span></span>

<span data-ttu-id="34923-112">By following this tutorial, you will build a simple web application hosted inside a web role.</span><span class="sxs-lookup"><span data-stu-id="34923-112">By following this tutorial, you will build a simple web application hosted inside a web role.</span></span> <span data-ttu-id="34923-113">You will use the compute emulator to test your application locally, then deploy it using PowerShell command-line tools.</span><span class="sxs-lookup"><span data-stu-id="34923-113">You will use the compute emulator to test your application locally, then deploy it using PowerShell command-line tools.</span></span>

<span data-ttu-id="34923-114">The application is a simple "hello world" application:</span><span class="sxs-lookup"><span data-stu-id="34923-114">The application is a simple "hello world" application:</span></span>

![A web browser displaying the Hello World web page][A web browser displaying the Hello World web page]

## <a name="prerequisites"></a><span data-ttu-id="34923-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="34923-116">Prerequisites</span></span>
> [!NOTE]
> <span data-ttu-id="34923-117">This tutorial uses Azure PowerShell, which requires Windows.</span><span class="sxs-lookup"><span data-stu-id="34923-117">This tutorial uses Azure PowerShell, which requires Windows.</span></span>

* <span data-ttu-id="34923-118">Install and configure [Azure Powershell].</span><span class="sxs-lookup"><span data-stu-id="34923-118">Install and configure [Azure Powershell].</span></span>
* <span data-ttu-id="34923-119">Download and install the [Azure SDK for .NET 2.7].</span><span class="sxs-lookup"><span data-stu-id="34923-119">Download and install the [Azure SDK for .NET 2.7].</span></span> <span data-ttu-id="34923-120">In the install setup, select:</span><span class="sxs-lookup"><span data-stu-id="34923-120">In the install setup, select:</span></span>
  * <span data-ttu-id="34923-121">MicrosoftAzureAuthoringTools</span><span class="sxs-lookup"><span data-stu-id="34923-121">MicrosoftAzureAuthoringTools</span></span>
  * <span data-ttu-id="34923-122">MicrosoftAzureComputeEmulator</span><span class="sxs-lookup"><span data-stu-id="34923-122">MicrosoftAzureComputeEmulator</span></span>

## <a name="create-an-azure-cloud-service-project"></a><span data-ttu-id="34923-123">Create an Azure Cloud Service project</span><span class="sxs-lookup"><span data-stu-id="34923-123">Create an Azure Cloud Service project</span></span>
<span data-ttu-id="34923-124">Perform the following tasks to create a new Azure Cloud Service project, along with basic Node.js scaffolding:</span><span class="sxs-lookup"><span data-stu-id="34923-124">Perform the following tasks to create a new Azure Cloud Service project, along with basic Node.js scaffolding:</span></span>

1. <span data-ttu-id="34923-125">Run **Windows PowerShell** as Administrator; from the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="34923-125">Run **Windows PowerShell** as Administrator; from the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span>
2. <span data-ttu-id="34923-126">[Connect PowerShell] to your subscription.</span><span class="sxs-lookup"><span data-stu-id="34923-126">[Connect PowerShell] to your subscription.</span></span>
3. <span data-ttu-id="34923-127">Enter the following PowerShell cmdlet to create to create the project:</span><span class="sxs-lookup"><span data-stu-id="34923-127">Enter the following PowerShell cmdlet to create to create the project:</span></span>

        New-AzureServiceProject helloworld

    ![The result of the New-AzureService helloworld command][The result of the New-AzureService helloworld command]

    <span data-ttu-id="34923-129">The **New-AzureServiceProject** cmdlet generates a basic structure for publishing a Node.js application to a Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="34923-129">The **New-AzureServiceProject** cmdlet generates a basic structure for publishing a Node.js application to a Cloud Service.</span></span> <span data-ttu-id="34923-130">It contains configuration files necessary for publishing to Azure.</span><span class="sxs-lookup"><span data-stu-id="34923-130">It contains configuration files necessary for publishing to Azure.</span></span> <span data-ttu-id="34923-131">The cmdlet also changes your working directory to the directory for the service.</span><span class="sxs-lookup"><span data-stu-id="34923-131">The cmdlet also changes your working directory to the directory for the service.</span></span>

    <span data-ttu-id="34923-132">The cmdlet creates the following files:</span><span class="sxs-lookup"><span data-stu-id="34923-132">The cmdlet creates the following files:</span></span>

   * <span data-ttu-id="34923-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** and **ServiceDefinition.csdef**: Azure-specific files necessary for publishing your application.</span><span class="sxs-lookup"><span data-stu-id="34923-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** and **ServiceDefinition.csdef**: Azure-specific files necessary for publishing your application.</span></span> <span data-ttu-id="34923-134">For more information, see [Overview of Creating a Hosted Service for Azure].</span><span class="sxs-lookup"><span data-stu-id="34923-134">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
   * <span data-ttu-id="34923-135">**deploymentSettings.json**: Stores local settings that are used by the Azure PowerShell deployment cmdlets.</span><span class="sxs-lookup"><span data-stu-id="34923-135">**deploymentSettings.json**: Stores local settings that are used by the Azure PowerShell deployment cmdlets.</span></span>
4. <span data-ttu-id="34923-136">Enter the following command to add a new web role:</span><span class="sxs-lookup"><span data-stu-id="34923-136">Enter the following command to add a new web role:</span></span>

       Add-AzureNodeWebRole

   ![The output of the Add-AzureNodeWebRole command][The output of the Add-AzureNodeWebRole command]

   <span data-ttu-id="34923-138">The **Add-AzureNodeWebRole** cmdlet creates a basic Node.js application.</span><span class="sxs-lookup"><span data-stu-id="34923-138">The **Add-AzureNodeWebRole** cmdlet creates a basic Node.js application.</span></span> <span data-ttu-id="34923-139">It also modifies the **.csfg** and **.csdef** files to add configuration entries for the new role.</span><span class="sxs-lookup"><span data-stu-id="34923-139">It also modifies the **.csfg** and **.csdef** files to add configuration entries for the new role.</span></span>

   > [!NOTE]
   > <span data-ttu-id="34923-140">If you do not specify a role name, a default name is used.</span><span class="sxs-lookup"><span data-stu-id="34923-140">If you do not specify a role name, a default name is used.</span></span> <span data-ttu-id="34923-141">You can provide a name as the first cmdlet parameter: `Add-AzureNodeWebRole MyRole`</span><span class="sxs-lookup"><span data-stu-id="34923-141">You can provide a name as the first cmdlet parameter: `Add-AzureNodeWebRole MyRole`</span></span>

<span data-ttu-id="34923-142">The Node.js app is defined in the file **server.js**, located in the directory for the web role (**WebRole1** by default).</span><span class="sxs-lookup"><span data-stu-id="34923-142">The Node.js app is defined in the file **server.js**, located in the directory for the web role (**WebRole1** by default).</span></span> <span data-ttu-id="34923-143">Here is the code:</span><span class="sxs-lookup"><span data-stu-id="34923-143">Here is the code:</span></span>

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

<span data-ttu-id="34923-144">This code is essentially the same as the "Hello World" sample on the [nodejs.org] website, except it uses the port number assigned by the cloud environment.</span><span class="sxs-lookup"><span data-stu-id="34923-144">This code is essentially the same as the "Hello World" sample on the [nodejs.org] website, except it uses the port number assigned by the cloud environment.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="34923-145">Deploy the application to Azure</span><span class="sxs-lookup"><span data-stu-id="34923-145">Deploy the application to Azure</span></span>

> [!NOTE]
> <span data-ttu-id="34923-146">To complete this tutorial, you need an Azure account.</span><span class="sxs-lookup"><span data-stu-id="34923-146">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="34923-147">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) or [sign up for a free account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span><span class="sxs-lookup"><span data-stu-id="34923-147">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) or [sign up for a free account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span></span>

### <a name="download-the-azure-publishing-settings"></a><span data-ttu-id="34923-148">Download the Azure publishing settings</span><span class="sxs-lookup"><span data-stu-id="34923-148">Download the Azure publishing settings</span></span>
<span data-ttu-id="34923-149">To deploy your application to Azure, you must first download the publishing settings for your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="34923-149">To deploy your application to Azure, you must first download the publishing settings for your Azure subscription.</span></span>

1. <span data-ttu-id="34923-150">Run the following Azure PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="34923-150">Run the following Azure PowerShell cmdlet:</span></span>

       Get-AzurePublishSettingsFile

   <span data-ttu-id="34923-151">This will use your browser to navigate to the publish settings download page.</span><span class="sxs-lookup"><span data-stu-id="34923-151">This will use your browser to navigate to the publish settings download page.</span></span> <span data-ttu-id="34923-152">You may be prompted to log in with a Microsoft Account.</span><span class="sxs-lookup"><span data-stu-id="34923-152">You may be prompted to log in with a Microsoft Account.</span></span> <span data-ttu-id="34923-153">If so, use the account associated with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="34923-153">If so, use the account associated with your Azure subscription.</span></span>

   <span data-ttu-id="34923-154">Save the downloaded profile to a file location you can easily access.</span><span class="sxs-lookup"><span data-stu-id="34923-154">Save the downloaded profile to a file location you can easily access.</span></span>
2. <span data-ttu-id="34923-155">Run following cmdlet to import the publishing profile you downloaded:</span><span class="sxs-lookup"><span data-stu-id="34923-155">Run following cmdlet to import the publishing profile you downloaded:</span></span>

       Import-AzurePublishSettingsFile [path to file]

    > [!NOTE]
    > <span data-ttu-id="34923-156">After importing the publish settings, consider deleting the downloaded .publishSettings file, because it contains information that could allow someone to access your account.</span><span class="sxs-lookup"><span data-stu-id="34923-156">After importing the publish settings, consider deleting the downloaded .publishSettings file, because it contains information that could allow someone to access your account.</span></span>

### <a name="publish-the-application"></a><span data-ttu-id="34923-157">Publish the application</span><span class="sxs-lookup"><span data-stu-id="34923-157">Publish the application</span></span>
<span data-ttu-id="34923-158">To publish, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="34923-158">To publish, run the following commands:</span></span>

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* <span data-ttu-id="34923-159">**-ServiceName** specifies the name for the deployment.</span><span class="sxs-lookup"><span data-stu-id="34923-159">**-ServiceName** specifies the name for the deployment.</span></span> <span data-ttu-id="34923-160">This must be a unique name, otherwise the publish process will fail.</span><span class="sxs-lookup"><span data-stu-id="34923-160">This must be a unique name, otherwise the publish process will fail.</span></span> <span data-ttu-id="34923-161">The **Get-Date** command tacks on a date/time string that should make the name unique.</span><span class="sxs-lookup"><span data-stu-id="34923-161">The **Get-Date** command tacks on a date/time string that should make the name unique.</span></span>
* <span data-ttu-id="34923-162">**-Location** specifies the datacenter that the application will be hosted in.</span><span class="sxs-lookup"><span data-stu-id="34923-162">**-Location** specifies the datacenter that the application will be hosted in.</span></span> <span data-ttu-id="34923-163">To see a list of available datacenters, use the **Get-AzureLocation** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="34923-163">To see a list of available datacenters, use the **Get-AzureLocation** cmdlet.</span></span>
* <span data-ttu-id="34923-164">**-Launch** opens a browser window and navigates to the hosted service after deployment has completed.</span><span class="sxs-lookup"><span data-stu-id="34923-164">**-Launch** opens a browser window and navigates to the hosted service after deployment has completed.</span></span>

<span data-ttu-id="34923-165">After publishing succeeds, you will see a response similar to the following:</span><span class="sxs-lookup"><span data-stu-id="34923-165">After publishing succeeds, you will see a response similar to the following:</span></span>

![The output of the Publish-AzureService command][The output of the Publish-AzureService command]

> [!NOTE]
> <span data-ttu-id="34923-167">It can take several minutes for the application to deploy and become available when first published.</span><span class="sxs-lookup"><span data-stu-id="34923-167">It can take several minutes for the application to deploy and become available when first published.</span></span>

<span data-ttu-id="34923-168">Once the deployment has completed, a browser window will open and navigate to the cloud service.</span><span class="sxs-lookup"><span data-stu-id="34923-168">Once the deployment has completed, a browser window will open and navigate to the cloud service.</span></span>

![A browser window displaying the hello world page; the URL indicates the page is hosted on Azure.][A browser window displaying the hello world page; the URL indicates the page is hosted on Azure.]

<span data-ttu-id="34923-170">Your application is now running on Azure.</span><span class="sxs-lookup"><span data-stu-id="34923-170">Your application is now running on Azure.</span></span>

<span data-ttu-id="34923-171">The **Publish-AzureServiceProject** cmdlet performs the following steps:</span><span class="sxs-lookup"><span data-stu-id="34923-171">The **Publish-AzureServiceProject** cmdlet performs the following steps:</span></span>

1. <span data-ttu-id="34923-172">Creates a package to deploy.</span><span class="sxs-lookup"><span data-stu-id="34923-172">Creates a package to deploy.</span></span> <span data-ttu-id="34923-173">The package contains all the files in your application folder.</span><span class="sxs-lookup"><span data-stu-id="34923-173">The package contains all the files in your application folder.</span></span>
2. <span data-ttu-id="34923-174">Creates a new **storage account** if one does not exist.</span><span class="sxs-lookup"><span data-stu-id="34923-174">Creates a new **storage account** if one does not exist.</span></span> <span data-ttu-id="34923-175">The Azure storage account is used to store the application package during deployment.</span><span class="sxs-lookup"><span data-stu-id="34923-175">The Azure storage account is used to store the application package during deployment.</span></span> <span data-ttu-id="34923-176">You can safely delete the storage account after deployment is done.</span><span class="sxs-lookup"><span data-stu-id="34923-176">You can safely delete the storage account after deployment is done.</span></span>
3. <span data-ttu-id="34923-177">Creates a new **cloud service** if one does not already exist.</span><span class="sxs-lookup"><span data-stu-id="34923-177">Creates a new **cloud service** if one does not already exist.</span></span> <span data-ttu-id="34923-178">A **cloud service** is the container in which your application is hosted when it is deployed to Azure.</span><span class="sxs-lookup"><span data-stu-id="34923-178">A **cloud service** is the container in which your application is hosted when it is deployed to Azure.</span></span> <span data-ttu-id="34923-179">For more information, see [Overview of Creating a Hosted Service for Azure].</span><span class="sxs-lookup"><span data-stu-id="34923-179">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
4. <span data-ttu-id="34923-180">Publishes the deployment package to Azure.</span><span class="sxs-lookup"><span data-stu-id="34923-180">Publishes the deployment package to Azure.</span></span>

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="34923-181">Stopping and deleting your application</span><span class="sxs-lookup"><span data-stu-id="34923-181">Stopping and deleting your application</span></span>
<span data-ttu-id="34923-182">After deploying your application, you may want to disable it so you can avoid extra costs.</span><span class="sxs-lookup"><span data-stu-id="34923-182">After deploying your application, you may want to disable it so you can avoid extra costs.</span></span> <span data-ttu-id="34923-183">Azure bills web role instances per hour of server time consumed.</span><span class="sxs-lookup"><span data-stu-id="34923-183">Azure bills web role instances per hour of server time consumed.</span></span> <span data-ttu-id="34923-184">Server time is consumed once your application is deployed, even if the instances are not running and are in the stopped state.</span><span class="sxs-lookup"><span data-stu-id="34923-184">Server time is consumed once your application is deployed, even if the instances are not running and are in the stopped state.</span></span>

1. <span data-ttu-id="34923-185">In the Windows PowerShell window, stop the service deployment created in the previous section with the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="34923-185">In the Windows PowerShell window, stop the service deployment created in the previous section with the following cmdlet:</span></span>

       Stop-AzureService

   <span data-ttu-id="34923-186">Stopping the service may take several minutes.</span><span class="sxs-lookup"><span data-stu-id="34923-186">Stopping the service may take several minutes.</span></span> <span data-ttu-id="34923-187">When the service is stopped, you receive a message indicating that it has stopped.</span><span class="sxs-lookup"><span data-stu-id="34923-187">When the service is stopped, you receive a message indicating that it has stopped.</span></span>

   ![The status of the Stop-AzureService command][The status of the Stop-AzureService command]
2. <span data-ttu-id="34923-189">To delete the service, call the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="34923-189">To delete the service, call the following cmdlet:</span></span>

       Remove-AzureService

   <span data-ttu-id="34923-190">When prompted, enter **Y** to delete the service.</span><span class="sxs-lookup"><span data-stu-id="34923-190">When prompted, enter **Y** to delete the service.</span></span>

   <span data-ttu-id="34923-191">Deleting the service may take several minutes.</span><span class="sxs-lookup"><span data-stu-id="34923-191">Deleting the service may take several minutes.</span></span> <span data-ttu-id="34923-192">After the service has been deleted you receive a message indicating that the service was deleted.</span><span class="sxs-lookup"><span data-stu-id="34923-192">After the service has been deleted you receive a message indicating that the service was deleted.</span></span>

   ![The status of the Remove-AzureService command][The status of the Remove-AzureService command]

   > [!NOTE]
   > <span data-ttu-id="34923-194">Deleting the service does not delete the storage account that was created when the service was initially published, and you will continue to be billed for storage used.</span><span class="sxs-lookup"><span data-stu-id="34923-194">Deleting the service does not delete the storage account that was created when the service was initially published, and you will continue to be billed for storage used.</span></span> <span data-ttu-id="34923-195">If nothing else is using the storage, you may want to delete it.</span><span class="sxs-lookup"><span data-stu-id="34923-195">If nothing else is using the storage, you may want to delete it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34923-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="34923-196">Next steps</span></span>
<span data-ttu-id="34923-197">For more information, see the [Node.js Developer Center].</span><span class="sxs-lookup"><span data-stu-id="34923-197">For more information, see the [Node.js Developer Center].</span></span>

<!-- URL List -->

[Azure Websites, Cloud Services and Virtual Machines comparison]: ../app-service/choose-web-site-cloud-service-vm.md
[using a lightweight web app]: ../app-service/app-service-web-get-started-nodejs.md
[Azure Powershell]: /powershell/azureps-cmdlets-docs
[Azure SDK for .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[Connect PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[Overview of Creating a Hosted Service for Azure]: https://azure.microsoft.com/documentation/services/cloud-services/
[Node.js Developer Center]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[The result of the New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[The output of the Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying the Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[The output of the Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying the hello world page; the URL indicates the page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[The status of the Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[The status of the Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
