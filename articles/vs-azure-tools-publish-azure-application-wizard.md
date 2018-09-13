---
title: Using the Visual Studio Publish Azure Application Wizard | Microsoft Docs
description: Learn how to configure the various settings in the Visual Studio Publish Azure Application Wizard
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: 7d8f1ac9-e439-47e0-a183-0642c4ea1920
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: f2438ccc4f3492797c5642175f544a63a0697c1d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554813"
---
# <a name="using-the-visual-studio-publish-azure-application-wizard"></a><span data-ttu-id="f4838-103">Using the Visual Studio Publish Azure Application Wizard</span><span class="sxs-lookup"><span data-stu-id="f4838-103">Using the Visual Studio Publish Azure Application Wizard</span></span>
<span data-ttu-id="f4838-104">After you develop a web application in Visual Studio, you can publish that application to an Azure cloud service by using the **Publish Azure Application** wizard.</span><span class="sxs-lookup"><span data-stu-id="f4838-104">After you develop a web application in Visual Studio, you can publish that application to an Azure cloud service by using the **Publish Azure Application** wizard.</span></span> 

> [!NOTE]
> <span data-ttu-id="f4838-105">This topic is about deploying to cloud services, not to web sites.</span><span class="sxs-lookup"><span data-stu-id="f4838-105">This topic is about deploying to cloud services, not to web sites.</span></span> <span data-ttu-id="f4838-106">For information about deploying to web sites, see [How to Deploy an Azure Web Site](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false).</span><span class="sxs-lookup"><span data-stu-id="f4838-106">For information about deploying to web sites, see [How to Deploy an Azure Web Site](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false).</span></span>
> 
> 

## <a name="accessing-the-publish-azure-application-wizard"></a><span data-ttu-id="f4838-107">Accessing the Publish Azure Application wizard</span><span class="sxs-lookup"><span data-stu-id="f4838-107">Accessing the Publish Azure Application wizard</span></span>

<span data-ttu-id="f4838-108">You can access the Publish Azure Application wizard in two ways depending on the type of Visual Studio project you have.</span><span class="sxs-lookup"><span data-stu-id="f4838-108">You can access the Publish Azure Application wizard in two ways depending on the type of Visual Studio project you have.</span></span>

<span data-ttu-id="f4838-109">**If you have an Azure cloud service project:**</span><span class="sxs-lookup"><span data-stu-id="f4838-109">**If you have an Azure cloud service project:**</span></span>

1. <span data-ttu-id="f4838-110">Create or open an Azure cloud service project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f4838-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="f4838-111">In **Solution Explorer**, right-click the project, and, from the context menu, select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="f4838-111">In **Solution Explorer**, right-click the project, and, from the context menu, select **Publish**.</span></span>

<span data-ttu-id="f4838-112">**If you have a web application project that is not enabled for Azure:**</span><span class="sxs-lookup"><span data-stu-id="f4838-112">**If you have a web application project that is not enabled for Azure:**</span></span>

1. <span data-ttu-id="f4838-113">Create or open an Azure cloud service project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f4838-113">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="f4838-114">In **Solution Explorer**, right-click the project, and, from the context menu, select **Convert** > **Convert to Azure Cloud Service Project**.</span><span class="sxs-lookup"><span data-stu-id="f4838-114">In **Solution Explorer**, right-click the project, and, from the context menu, select **Convert** > **Convert to Azure Cloud Service Project**.</span></span> 

1. <span data-ttu-id="f4838-115">In **Solution Explorer**, right-click the newly created Azure project, and, from the context menu, select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="f4838-115">In **Solution Explorer**, right-click the newly created Azure project, and, from the context menu, select **Publish**.</span></span>

## <a name="sign-in-page"></a><span data-ttu-id="f4838-116">Sign-in page</span><span class="sxs-lookup"><span data-stu-id="f4838-116">Sign-in page</span></span>

![Sign-in page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-publish-azure-application-wizard/sign-in.png)

<span data-ttu-id="f4838-118">**Account** - Select an account or select **Add an account** in the account dropdown list.</span><span class="sxs-lookup"><span data-stu-id="f4838-118">**Account** - Select an account or select **Add an account** in the account dropdown list.</span></span>

<span data-ttu-id="f4838-119">**Choose your subscription** - Choose the subscription to use for your deployment.</span><span class="sxs-lookup"><span data-stu-id="f4838-119">**Choose your subscription** - Choose the subscription to use for your deployment.</span></span>
   
## <a name="settings-page---common-settings-tab"></a><span data-ttu-id="f4838-120">Settings page - Common Settings tab</span><span class="sxs-lookup"><span data-stu-id="f4838-120">Settings page - Common Settings tab</span></span>   

![Common Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-publish-azure-application-wizard/settings-common-settings.png)

<span data-ttu-id="f4838-122">**Cloud service** - Using the dropdown, either select an existing cloud service, or select **&lt;Create New>**, and create a cloud service.</span><span class="sxs-lookup"><span data-stu-id="f4838-122">**Cloud service** - Using the dropdown, either select an existing cloud service, or select **&lt;Create New>**, and create a cloud service.</span></span> <span data-ttu-id="f4838-123">The data center displays in parentheses for each cloud service.</span><span class="sxs-lookup"><span data-stu-id="f4838-123">The data center displays in parentheses for each cloud service.</span></span> <span data-ttu-id="f4838-124">It is recommended that the data center location for the cloud service be the same as the data center location for the storage account (Advanced Settings).</span><span class="sxs-lookup"><span data-stu-id="f4838-124">It is recommended that the data center location for the cloud service be the same as the data center location for the storage account (Advanced Settings).</span></span>  

<span data-ttu-id="f4838-125">**Environment** - Select either **Production** or **Staging**.</span><span class="sxs-lookup"><span data-stu-id="f4838-125">**Environment** - Select either **Production** or **Staging**.</span></span> <span data-ttu-id="f4838-126">Choose the staging environment if you want to deploy your application in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f4838-126">Choose the staging environment if you want to deploy your application in a test environment.</span></span> 

<span data-ttu-id="f4838-127">**Build configuration** - Select either **Debug** or **Release**.</span><span class="sxs-lookup"><span data-stu-id="f4838-127">**Build configuration** - Select either **Debug** or **Release**.</span></span>

<span data-ttu-id="f4838-128">**Service configuration** - Select either **Cloud** or **Local**.</span><span class="sxs-lookup"><span data-stu-id="f4838-128">**Service configuration** - Select either **Cloud** or **Local**.</span></span>
   
<span data-ttu-id="f4838-129">**Enable Remote Desktop for all roles** - Check this option if you want to be able to remotely connect to the service.</span><span class="sxs-lookup"><span data-stu-id="f4838-129">**Enable Remote Desktop for all roles** - Check this option if you want to be able to remotely connect to the service.</span></span> <span data-ttu-id="f4838-130">This option is primarily used for troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="f4838-130">This option is primarily used for troubleshooting.</span></span> <span data-ttu-id="f4838-131">When you select this check box, the **Remote Desktop Configuration** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="f4838-131">When you select this check box, the **Remote Desktop Configuration** dialog box appears.</span></span> <span data-ttu-id="f4838-132">Choose the **Settings** link to change the configuration.</span><span class="sxs-lookup"><span data-stu-id="f4838-132">Choose the **Settings** link to change the configuration.</span></span>
   
<span data-ttu-id="f4838-133">**Enable Web Deploy for all web roles** - Check this option, to enable web deployment for the service.</span><span class="sxs-lookup"><span data-stu-id="f4838-133">**Enable Web Deploy for all web roles** - Check this option, to enable web deployment for the service.</span></span> <span data-ttu-id="f4838-134">You must select the **Enable Remote Desktop for all roles** option to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f4838-134">You must select the **Enable Remote Desktop for all roles** option to use this feature.</span></span> <span data-ttu-id="f4838-135">For more information, see [[Publishing a Azure cloud service using Visual Studio](https://msdn.microsoft.com/library/azure/ff683672.aspx)](https://msdn.microsoft.com/library/azure/ff683672.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4838-135">For more information, see [[Publishing a Azure cloud service using Visual Studio](https://msdn.microsoft.com/library/azure/ff683672.aspx)](https://msdn.microsoft.com/library/azure/ff683672.aspx).</span></span> 

## <a name="settings-page---advanced-settings-tab"></a><span data-ttu-id="f4838-136">Settings page - Advanced Settings tab</span><span class="sxs-lookup"><span data-stu-id="f4838-136">Settings page - Advanced Settings tab</span></span>

![Advanced settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-publish-azure-application-wizard/settings-advanced-settings.png)

<span data-ttu-id="f4838-138">**Deployment label** - Either accept the default name, or enter a name of your choosing.</span><span class="sxs-lookup"><span data-stu-id="f4838-138">**Deployment label** - Either accept the default name, or enter a name of your choosing.</span></span> <span data-ttu-id="f4838-139">To append the date to the deployment label, leave the check box selected.</span><span class="sxs-lookup"><span data-stu-id="f4838-139">To append the date to the deployment label, leave the check box selected.</span></span> 
   
<span data-ttu-id="f4838-140">**Storage account** - Select the storage account to use for this deployment, \*\*&lt;Create New> to create a storage account.</span><span class="sxs-lookup"><span data-stu-id="f4838-140">**Storage account** - Select the storage account to use for this deployment, \*\*&lt;Create New> to create a storage account.</span></span> <span data-ttu-id="f4838-141">The data center displays in parentheses for each storage account.</span><span class="sxs-lookup"><span data-stu-id="f4838-141">The data center displays in parentheses for each storage account.</span></span> <span data-ttu-id="f4838-142">It is recommended that the data center location for the storage account be the same as the data center location for the cloud service (Common Settings).</span><span class="sxs-lookup"><span data-stu-id="f4838-142">It is recommended that the data center location for the storage account be the same as the data center location for the cloud service (Common Settings).</span></span>  
   
<span data-ttu-id="f4838-143">The Azure storage account stores the package for the application deployment.</span><span class="sxs-lookup"><span data-stu-id="f4838-143">The Azure storage account stores the package for the application deployment.</span></span> <span data-ttu-id="f4838-144">After the application is deployed, the package is removed from the storage account.</span><span class="sxs-lookup"><span data-stu-id="f4838-144">After the application is deployed, the package is removed from the storage account.</span></span>

<span data-ttu-id="f4838-145">**Delete deployment on failure** - Select this option to have the deployment deleted if any errors are encountered during publishing.</span><span class="sxs-lookup"><span data-stu-id="f4838-145">**Delete deployment on failure** - Select this option to have the deployment deleted if any errors are encountered during publishing.</span></span> <span data-ttu-id="f4838-146">This should be unchecked if you want to maintain a constant virtual IP address for your cloud service.</span><span class="sxs-lookup"><span data-stu-id="f4838-146">This should be unchecked if you want to maintain a constant virtual IP address for your cloud service.</span></span>

<span data-ttu-id="f4838-147">**Deployment update** - Select this option if you want to deploy only updated components.</span><span class="sxs-lookup"><span data-stu-id="f4838-147">**Deployment update** - Select this option if you want to deploy only updated components.</span></span> <span data-ttu-id="f4838-148">This type of deployment can be faster than a full deployment.</span><span class="sxs-lookup"><span data-stu-id="f4838-148">This type of deployment can be faster than a full deployment.</span></span> <span data-ttu-id="f4838-149">This should be checked if you want to maintain a constant virtual IP address for your cloud service.</span><span class="sxs-lookup"><span data-stu-id="f4838-149">This should be checked if you want to maintain a constant virtual IP address for your cloud service.</span></span> 

<span data-ttu-id="f4838-150">**Deployment update - settings** - This dialog is used to further specify how you want the roles to be updated.</span><span class="sxs-lookup"><span data-stu-id="f4838-150">**Deployment update - settings** - This dialog is used to further specify how you want the roles to be updated.</span></span> <span data-ttu-id="f4838-151">If you choose **Incremental update**, each instance of your application is updated one after another, so that the application is always available.</span><span class="sxs-lookup"><span data-stu-id="f4838-151">If you choose **Incremental update**, each instance of your application is updated one after another, so that the application is always available.</span></span> <span data-ttu-id="f4838-152">If you choose **Simultaneous update**, all instances of your application are updated at the same time.</span><span class="sxs-lookup"><span data-stu-id="f4838-152">If you choose **Simultaneous update**, all instances of your application are updated at the same time.</span></span> <span data-ttu-id="f4838-153">Simultaneous updating is faster, but your service might not be available during the update process.</span><span class="sxs-lookup"><span data-stu-id="f4838-153">Simultaneous updating is faster, but your service might not be available during the update process.</span></span> 

![Deployment settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-publish-azure-application-wizard/deployment-settings.png)

<span data-ttu-id="f4838-155">**Enable IntelliTrace** - Specify if you want to enable IntelliTrace.</span><span class="sxs-lookup"><span data-stu-id="f4838-155">**Enable IntelliTrace** - Specify if you want to enable IntelliTrace.</span></span> <span data-ttu-id="f4838-156">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span><span class="sxs-lookup"><span data-stu-id="f4838-156">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span></span> <span data-ttu-id="f4838-157">If you need to find the cause of a problem, you can use the IntelliTrace logs to step through your code from Visual Studio as if it were running in Azure.</span><span class="sxs-lookup"><span data-stu-id="f4838-157">If you need to find the cause of a problem, you can use the IntelliTrace logs to step through your code from Visual Studio as if it were running in Azure.</span></span> <span data-ttu-id="f4838-158">For more information about using IntelliTrace, see [Debugging a published Azure cloud service with Visual Studio and IntelliTrace](./vs-azure-tools-intellitrace-debug-published-cloud-services.md).</span><span class="sxs-lookup"><span data-stu-id="f4838-158">For more information about using IntelliTrace, see [Debugging a published Azure cloud service with Visual Studio and IntelliTrace](./vs-azure-tools-intellitrace-debug-published-cloud-services.md).</span></span> 

<span data-ttu-id="f4838-159">**Enable profiling** - Specify if you want to enable performance profiling.</span><span class="sxs-lookup"><span data-stu-id="f4838-159">**Enable profiling** - Specify if you want to enable performance profiling.</span></span> <span data-ttu-id="f4838-160">The Visual Studio profiler enables you to get an in-depth analysis of the computational aspects of how your cloud service runs.</span><span class="sxs-lookup"><span data-stu-id="f4838-160">The Visual Studio profiler enables you to get an in-depth analysis of the computational aspects of how your cloud service runs.</span></span> <span data-ttu-id="f4838-161">For more information on using the Visual Studio profiler, see [Test the performance of an Azure cloud service](./vs-azure-tools-performance-profiling-cloud-services.md).</span><span class="sxs-lookup"><span data-stu-id="f4838-161">For more information on using the Visual Studio profiler, see [Test the performance of an Azure cloud service](./vs-azure-tools-performance-profiling-cloud-services.md).</span></span>

<span data-ttu-id="f4838-162">**Enable Remote Debugger for all roles** - Specify if you want to enable remote debugging.</span><span class="sxs-lookup"><span data-stu-id="f4838-162">**Enable Remote Debugger for all roles** - Specify if you want to enable remote debugging.</span></span> <span data-ttu-id="f4838-163">For more information on debugging cloud services using Visual Studio, see [Debugging an Azure cloud service or virtual machine in Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="f4838-163">For more information on debugging cloud services using Visual Studio, see [Debugging an Azure cloud service or virtual machine in Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md).</span></span>

## <a name="diagnostics-settings-page"></a><span data-ttu-id="f4838-164">Diagnostics Settings page</span><span class="sxs-lookup"><span data-stu-id="f4838-164">Diagnostics Settings page</span></span>

![Diagnostics settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-publish-azure-application-wizard/diagnostic-settings.png)

<span data-ttu-id="f4838-166">Diagnostics enables you to troubleshoot an Azure cloud service (or Azure virtual machine).</span><span class="sxs-lookup"><span data-stu-id="f4838-166">Diagnostics enables you to troubleshoot an Azure cloud service (or Azure virtual machine).</span></span> <span data-ttu-id="f4838-167">For information about diagnostics, see [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="f4838-167">For information about diagnostics, see [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span> <span data-ttu-id="f4838-168">For information about Application Insights, see [What is Application Insights?](./application-insights/app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f4838-168">For information about Application Insights, see [What is Application Insights?](./application-insights/app-insights-overview.md).</span></span>

## <a name="summary-page"></a><span data-ttu-id="f4838-169">Summary page</span><span class="sxs-lookup"><span data-stu-id="f4838-169">Summary page</span></span>

![Summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-publish-azure-application-wizard/summary.png)

<span data-ttu-id="f4838-171">**Target profile** - You can choose to create a publishing profile from the settings that you have chosen.</span><span class="sxs-lookup"><span data-stu-id="f4838-171">**Target profile** - You can choose to create a publishing profile from the settings that you have chosen.</span></span> <span data-ttu-id="f4838-172">For example, you might create one profile for a test environment and another for production.</span><span class="sxs-lookup"><span data-stu-id="f4838-172">For example, you might create one profile for a test environment and another for production.</span></span> <span data-ttu-id="f4838-173">To save this profile, choose the **Save** icon.</span><span class="sxs-lookup"><span data-stu-id="f4838-173">To save this profile, choose the **Save** icon.</span></span> <span data-ttu-id="f4838-174">The wizard creates the profile and saves it in the Visual Studio project.</span><span class="sxs-lookup"><span data-stu-id="f4838-174">The wizard creates the profile and saves it in the Visual Studio project.</span></span> <span data-ttu-id="f4838-175">To modify the profile name, open the **Target profile** list, and then choose **<Manage…>**.</span><span class="sxs-lookup"><span data-stu-id="f4838-175">To modify the profile name, open the **Target profile** list, and then choose **<Manage…>**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f4838-176">The publishing profile appears in Solution Explorer in Visual Studio, and the profile settings are written to a file with an .azurePubxml extension.</span><span class="sxs-lookup"><span data-stu-id="f4838-176">The publishing profile appears in Solution Explorer in Visual Studio, and the profile settings are written to a file with an .azurePubxml extension.</span></span> <span data-ttu-id="f4838-177">Settings are saved as attributes of XML tags.</span><span class="sxs-lookup"><span data-stu-id="f4838-177">Settings are saved as attributes of XML tags.</span></span>
   > 
   > 

## <a name="publishing-your-application"></a><span data-ttu-id="f4838-178">Publishing your application</span><span class="sxs-lookup"><span data-stu-id="f4838-178">Publishing your application</span></span>

<span data-ttu-id="f4838-179">Once you configure all the settings for your project's deployment, select **Publish** at the bottom of the dialog.</span><span class="sxs-lookup"><span data-stu-id="f4838-179">Once you configure all the settings for your project's deployment, select **Publish** at the bottom of the dialog.</span></span> <span data-ttu-id="f4838-180">You can monitor the process status in the **Output** window in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f4838-180">You can monitor the process status in the **Output** window in Visual Studio.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4838-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="f4838-181">Next steps</span></span>
- [<span data-ttu-id="f4838-182">Migrate and publish a Web Application to an Azure cloud service from Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f4838-182">Migrate and publish a Web Application to an Azure cloud service from Visual Studio</span></span>](./vs-azure-tools-migrate-publish-web-app-to-cloud-service.md)
- [<span data-ttu-id="f4838-183">Learn how to use Visual Studio to publish an Azure cloud service</span><span class="sxs-lookup"><span data-stu-id="f4838-183">Learn how to use Visual Studio to publish an Azure cloud service</span></span>](./vs-azure-tools-publishing-a-cloud-service.md)
- [<span data-ttu-id="f4838-184">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="f4838-184">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span></span>](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)
- [<span data-ttu-id="f4838-185">Test the performance of an Azure cloud service</span><span class="sxs-lookup"><span data-stu-id="f4838-185">Test the performance of an Azure cloud service</span></span>](./vs-azure-tools-performance-profiling-cloud-services.md)
- <span data-ttu-id="f4838-186">[Configuring Diagnostics for Azure Cloud Services and Virtual Machines](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="f4838-186">[Configuring Diagnostics for Azure Cloud Services and Virtual Machines](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span> 
- [<span data-ttu-id="f4838-187">What is Application Insights?</span><span class="sxs-lookup"><span data-stu-id="f4838-187">What is Application Insights?</span></span>](./application-insights/app-insights-overview.md)





