---
title: Continuous delivery with Visual Studio Team Services in Azure | Microsoft Docs
description: Learn how to configure your Visual Studio Team Services team projects to automatically build and deploy to the Web App feature in Azure App Service or cloud services.
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: ''
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: 8d7c95006ce586294e9b160da88ca4701dc13884
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556189"
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services"></a><span data-ttu-id="1382b-103">Continuous delivery to Azure using Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="1382b-103">Continuous delivery to Azure using Visual Studio Team Services</span></span>
<span data-ttu-id="1382b-104">You can configure your Visual Studio Team Services team projects to automatically build and deploy to Azure web apps or cloud services.</span><span class="sxs-lookup"><span data-stu-id="1382b-104">You can configure your Visual Studio Team Services team projects to automatically build and deploy to Azure web apps or cloud services.</span></span>  <span data-ttu-id="1382b-105">(For information on how to set up a continuous build and deploy system using an *on-premises* Team Foundation Server, see [Continuous Delivery for Cloud Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span><span class="sxs-lookup"><span data-stu-id="1382b-105">(For information on how to set up a continuous build and deploy system using an *on-premises* Team Foundation Server, see [Continuous Delivery for Cloud Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span></span>

<span data-ttu-id="1382b-106">This tutorial assumes you have Visual Studio 2013 and the Azure SDK installed.</span><span class="sxs-lookup"><span data-stu-id="1382b-106">This tutorial assumes you have Visual Studio 2013 and the Azure SDK installed.</span></span> <span data-ttu-id="1382b-107">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="1382b-107">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span></span> <span data-ttu-id="1382b-108">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="1382b-108">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="1382b-109">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="1382b-109">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="1382b-110">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="1382b-110">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-team-project"></a><span data-ttu-id="1382b-111">1: Create a team project</span><span class="sxs-lookup"><span data-stu-id="1382b-111">1: Create a team project</span></span>
<span data-ttu-id="1382b-112">Follow the instructions [here](http://go.microsoft.com/fwlink/?LinkId=512980) to create your team project and link it to Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1382b-112">Follow the instructions [here](http://go.microsoft.com/fwlink/?LinkId=512980) to create your team project and link it to Visual Studio.</span></span> <span data-ttu-id="1382b-113">This walkthrough assumes you are using Team Foundation Version Control (TFVC) as your source control solution.</span><span class="sxs-lookup"><span data-stu-id="1382b-113">This walkthrough assumes you are using Team Foundation Version Control (TFVC) as your source control solution.</span></span> <span data-ttu-id="1382b-114">If you want to use Git for version control, see [the Git version of this walkthrough](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span><span class="sxs-lookup"><span data-stu-id="1382b-114">If you want to use Git for version control, see [the Git version of this walkthrough](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span></span>

## <a name="2-check-in-a-project-to-source-control"></a><span data-ttu-id="1382b-115">2: Check in a project to source control</span><span class="sxs-lookup"><span data-stu-id="1382b-115">2: Check in a project to source control</span></span>
1. <span data-ttu-id="1382b-116">In Visual Studio, open the solution you want to deploy, or create a new one.</span><span class="sxs-lookup"><span data-stu-id="1382b-116">In Visual Studio, open the solution you want to deploy, or create a new one.</span></span>
   <span data-ttu-id="1382b-117">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="1382b-117">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span></span>
   <span data-ttu-id="1382b-118">If you want to create a new solution, create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span><span class="sxs-lookup"><span data-stu-id="1382b-118">If you want to create a new solution, create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="1382b-119">Make sure that the project targets .NET Framework 4 or 4.5, and if you are creating a cloud service project, add an ASP.NET MVC web role and a worker role, and choose Internet application for the web role.</span><span class="sxs-lookup"><span data-stu-id="1382b-119">Make sure that the project targets .NET Framework 4 or 4.5, and if you are creating a cloud service project, add an ASP.NET MVC web role and a worker role, and choose Internet application for the web role.</span></span> <span data-ttu-id="1382b-120">When prompted, choose **Internet Application**.</span><span class="sxs-lookup"><span data-stu-id="1382b-120">When prompted, choose **Internet Application**.</span></span>
   <span data-ttu-id="1382b-121">If you want to create a web app, choose the ASP.NET Web Application project template, and then choose MVC.</span><span class="sxs-lookup"><span data-stu-id="1382b-121">If you want to create a web app, choose the ASP.NET Web Application project template, and then choose MVC.</span></span> <span data-ttu-id="1382b-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="1382b-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1382b-123">Visual Studio Team Services only support CI deployments of Visual Studio Web Applications at this time.</span><span class="sxs-lookup"><span data-stu-id="1382b-123">Visual Studio Team Services only support CI deployments of Visual Studio Web Applications at this time.</span></span> <span data-ttu-id="1382b-124">Web Site projects are out of scope.</span><span class="sxs-lookup"><span data-stu-id="1382b-124">Web Site projects are out of scope.</span></span>
   > 
   > 
2. <span data-ttu-id="1382b-125">Open the context menu for the solution, and choose **Add Solution to Source Control**.</span><span class="sxs-lookup"><span data-stu-id="1382b-125">Open the context menu for the solution, and choose **Add Solution to Source Control**.</span></span>
   
    ![][5]
3. <span data-ttu-id="1382b-126">Accept or change the defaults and choose the **OK** button.</span><span class="sxs-lookup"><span data-stu-id="1382b-126">Accept or change the defaults and choose the **OK** button.</span></span> <span data-ttu-id="1382b-127">Once the process completes, source control icons appear in **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="1382b-127">Once the process completes, source control icons appear in **Solution Explorer**.</span></span>
   
    ![][6]
4. <span data-ttu-id="1382b-128">Open the shortcut menu for the solution, and choose **Check In**.</span><span class="sxs-lookup"><span data-stu-id="1382b-128">Open the shortcut menu for the solution, and choose **Check In**.</span></span>
   
    ![][7]
5. <span data-ttu-id="1382b-129">In the **Pending Changes** area of **Team Explorer**, type a comment for the check-in and choose the **Check In** button.</span><span class="sxs-lookup"><span data-stu-id="1382b-129">In the **Pending Changes** area of **Team Explorer**, type a comment for the check-in and choose the **Check In** button.</span></span>
   
    ![][8]
   
    <span data-ttu-id="1382b-130">Note the options to include or exclude specific changes when you check in.</span><span class="sxs-lookup"><span data-stu-id="1382b-130">Note the options to include or exclude specific changes when you check in.</span></span> <span data-ttu-id="1382b-131">If desired changes are excluded, choose the **Include All** link.</span><span class="sxs-lookup"><span data-stu-id="1382b-131">If desired changes are excluded, choose the **Include All** link.</span></span>
   
    ![][9]

## <a name="3-connect-the-project-to-azure"></a><span data-ttu-id="1382b-132">3: Connect the project to Azure</span><span class="sxs-lookup"><span data-stu-id="1382b-132">3: Connect the project to Azure</span></span>
1. <span data-ttu-id="1382b-133">Now that you have a VS Team Services team project with some source code in it, you are ready to connect your team project to Azure.</span><span class="sxs-lookup"><span data-stu-id="1382b-133">Now that you have a VS Team Services team project with some source code in it, you are ready to connect your team project to Azure.</span></span>  <span data-ttu-id="1382b-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the **+** icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span><span class="sxs-lookup"><span data-stu-id="1382b-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the **+** icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span> <span data-ttu-id="1382b-135">Choose the **Set up publishing with Visual Studio Team Services** link.</span><span class="sxs-lookup"><span data-stu-id="1382b-135">Choose the **Set up publishing with Visual Studio Team Services** link.</span></span>
   
    ![][10]
2. <span data-ttu-id="1382b-136">In the wizard, type the name of your Visual Studio Team Services account in the textbox and click the **Authorize Now** link.</span><span class="sxs-lookup"><span data-stu-id="1382b-136">In the wizard, type the name of your Visual Studio Team Services account in the textbox and click the **Authorize Now** link.</span></span> <span data-ttu-id="1382b-137">You might be asked to sign in.</span><span class="sxs-lookup"><span data-stu-id="1382b-137">You might be asked to sign in.</span></span>
   
    ![][11]
3. <span data-ttu-id="1382b-138">In the **Connection Request** pop-up dialog, choose the **Accept** button to authorize Azure to configure your team project in VS Team Services.</span><span class="sxs-lookup"><span data-stu-id="1382b-138">In the **Connection Request** pop-up dialog, choose the **Accept** button to authorize Azure to configure your team project in VS Team Services.</span></span>
   
    ![][12]
4. <span data-ttu-id="1382b-139">When authorization succeeds, you see a dropdown containing a list of your Visual Studio Team Services team projects.</span><span class="sxs-lookup"><span data-stu-id="1382b-139">When authorization succeeds, you see a dropdown containing a list of your Visual Studio Team Services team projects.</span></span> <span data-ttu-id="1382b-140">Choose  the name of team project that you created in the previous steps, and then choose the wizard's checkmark button.</span><span class="sxs-lookup"><span data-stu-id="1382b-140">Choose  the name of team project that you created in the previous steps, and then choose the wizard's checkmark button.</span></span>
   
    ![][13]
5. <span data-ttu-id="1382b-141">After your project is linked, you will see some instructions for checking in changes to your Visual Studio Team Services team project.</span><span class="sxs-lookup"><span data-stu-id="1382b-141">After your project is linked, you will see some instructions for checking in changes to your Visual Studio Team Services team project.</span></span>  <span data-ttu-id="1382b-142">On your next check-in, Visual Studio Team Services will build and deploy your project to Azure.</span><span class="sxs-lookup"><span data-stu-id="1382b-142">On your next check-in, Visual Studio Team Services will build and deploy your project to Azure.</span></span>  <span data-ttu-id="1382b-143">Try this now by clicking the **Check In from Visual Studio** link, and then the **Launch Visual Studio** link (or the equivalent **Visual Studio** button at the bottom of the portal screen).</span><span class="sxs-lookup"><span data-stu-id="1382b-143">Try this now by clicking the **Check In from Visual Studio** link, and then the **Launch Visual Studio** link (or the equivalent **Visual Studio** button at the bottom of the portal screen).</span></span>
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="1382b-144">4: Trigger a rebuild and redeploy your project</span><span class="sxs-lookup"><span data-stu-id="1382b-144">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="1382b-145">In Visual Studio's **Team Explorer**, choose the **Source Control Explorer** link.</span><span class="sxs-lookup"><span data-stu-id="1382b-145">In Visual Studio's **Team Explorer**, choose the **Source Control Explorer** link.</span></span>
   
    ![][15]
2. <span data-ttu-id="1382b-146">Navigate to your solution file and open it.</span><span class="sxs-lookup"><span data-stu-id="1382b-146">Navigate to your solution file and open it.</span></span>
   
    ![][16]
3. <span data-ttu-id="1382b-147">In **Solution Explorer**, open up a file and change it.</span><span class="sxs-lookup"><span data-stu-id="1382b-147">In **Solution Explorer**, open up a file and change it.</span></span> <span data-ttu-id="1382b-148">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span><span class="sxs-lookup"><span data-stu-id="1382b-148">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
4. <span data-ttu-id="1382b-149">Edit the logo for the site and choose **Ctrl+S** to save the file.</span><span class="sxs-lookup"><span data-stu-id="1382b-149">Edit the logo for the site and choose **Ctrl+S** to save the file.</span></span>
   
    ![][18]
5. <span data-ttu-id="1382b-150">In **Team Explorer**, choose the **Pending Changes** link.</span><span class="sxs-lookup"><span data-stu-id="1382b-150">In **Team Explorer**, choose the **Pending Changes** link.</span></span>
   
    ![][19]
6. <span data-ttu-id="1382b-151">Enter a comment and then choose the **Check In** button.</span><span class="sxs-lookup"><span data-stu-id="1382b-151">Enter a comment and then choose the **Check In** button.</span></span>
   
    ![][20]
7. <span data-ttu-id="1382b-152">Choose the **Home** button to return to the **Team Explorer** home page.</span><span class="sxs-lookup"><span data-stu-id="1382b-152">Choose the **Home** button to return to the **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="1382b-153">Choose the **Builds** link to view the builds in progress.</span><span class="sxs-lookup"><span data-stu-id="1382b-153">Choose the **Builds** link to view the builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="1382b-154">**Team Explorer** shows that a build has been triggered for your check-in.</span><span class="sxs-lookup"><span data-stu-id="1382b-154">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="1382b-155">Double-click the name of the build in progress to view a detailed log as the build progresses.</span><span class="sxs-lookup"><span data-stu-id="1382b-155">Double-click the name of the build in progress to view a detailed log as the build progresses.</span></span>
   
    ![][24]
10. <span data-ttu-id="1382b-156">While the build is in-progress, take a look at the build definition that was created when you linked TFS to Azure by using the wizard.</span><span class="sxs-lookup"><span data-stu-id="1382b-156">While the build is in-progress, take a look at the build definition that was created when you linked TFS to Azure by using the wizard.</span></span>  <span data-ttu-id="1382b-157">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span><span class="sxs-lookup"><span data-stu-id="1382b-157">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span></span>
    
     ![][25]
    
     <span data-ttu-id="1382b-158">In the **Trigger** tab, you will see that the build definition is set to build on every check-in by default.</span><span class="sxs-lookup"><span data-stu-id="1382b-158">In the **Trigger** tab, you will see that the build definition is set to build on every check-in by default.</span></span>
    
     ![][26]
    
     <span data-ttu-id="1382b-159">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span><span class="sxs-lookup"><span data-stu-id="1382b-159">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span></span> <span data-ttu-id="1382b-160">If you are working with web apps, the properties you see will be different from those shown here.</span><span class="sxs-lookup"><span data-stu-id="1382b-160">If you are working with web apps, the properties you see will be different from those shown here.</span></span>
    
     ![][27]
11. <span data-ttu-id="1382b-161">Specify values for the properties if you want different values than the defaults.</span><span class="sxs-lookup"><span data-stu-id="1382b-161">Specify values for the properties if you want different values than the defaults.</span></span> <span data-ttu-id="1382b-162">The properties for Azure publishing are in the **Deployment** section.</span><span class="sxs-lookup"><span data-stu-id="1382b-162">The properties for Azure publishing are in the **Deployment** section.</span></span>
    
     <span data-ttu-id="1382b-163">The following table shows the available properties in the **Deployment** section:</span><span class="sxs-lookup"><span data-stu-id="1382b-163">The following table shows the available properties in the **Deployment** section:</span></span>
    
    | <span data-ttu-id="1382b-164">Property</span><span class="sxs-lookup"><span data-stu-id="1382b-164">Property</span></span> | <span data-ttu-id="1382b-165">Default Value</span><span class="sxs-lookup"><span data-stu-id="1382b-165">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="1382b-166">Allow Untrusted Certificates</span><span class="sxs-lookup"><span data-stu-id="1382b-166">Allow Untrusted Certificates</span></span> |<span data-ttu-id="1382b-167">If false, SSL certificates must be signed by a root authority.</span><span class="sxs-lookup"><span data-stu-id="1382b-167">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="1382b-168">Allow Upgrade</span><span class="sxs-lookup"><span data-stu-id="1382b-168">Allow Upgrade</span></span> |<span data-ttu-id="1382b-169">Allows the deployment to update an existing deployment instead of creating a new one.</span><span class="sxs-lookup"><span data-stu-id="1382b-169">Allows the deployment to update an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="1382b-170">Preserves the IP address.</span><span class="sxs-lookup"><span data-stu-id="1382b-170">Preserves the IP address.</span></span> |
    | <span data-ttu-id="1382b-171">Do Not Delete</span><span class="sxs-lookup"><span data-stu-id="1382b-171">Do Not Delete</span></span> |<span data-ttu-id="1382b-172">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span><span class="sxs-lookup"><span data-stu-id="1382b-172">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="1382b-173">Path to Deployment Settings</span><span class="sxs-lookup"><span data-stu-id="1382b-173">Path to Deployment Settings</span></span> |<span data-ttu-id="1382b-174">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span><span class="sxs-lookup"><span data-stu-id="1382b-174">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span></span> <span data-ttu-id="1382b-175">Ignored for cloud services.</span><span class="sxs-lookup"><span data-stu-id="1382b-175">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="1382b-176">Sharepoint Deployment Environment</span><span class="sxs-lookup"><span data-stu-id="1382b-176">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="1382b-177">The same as the service name.</span><span class="sxs-lookup"><span data-stu-id="1382b-177">The same as the service name.</span></span> |
    | <span data-ttu-id="1382b-178">Azure Deployment Environment</span><span class="sxs-lookup"><span data-stu-id="1382b-178">Azure Deployment Environment</span></span> |<span data-ttu-id="1382b-179">The web app or cloud service name.</span><span class="sxs-lookup"><span data-stu-id="1382b-179">The web app or cloud service name.</span></span> |
12. <span data-ttu-id="1382b-180">If you are using multiple service configurations (.cscfg files), you can specify the desired service configuration in the **Build, Advanced, MSBuild arguments** setting.</span><span class="sxs-lookup"><span data-stu-id="1382b-180">If you are using multiple service configurations (.cscfg files), you can specify the desired service configuration in the **Build, Advanced, MSBuild arguments** setting.</span></span> <span data-ttu-id="1382b-181">For example, to use ServiceConfiguration.Test.cscfg, set MSBuild arguments line option `/p:TargetProfile=Test`.</span><span class="sxs-lookup"><span data-stu-id="1382b-181">For example, to use ServiceConfiguration.Test.cscfg, set MSBuild arguments line option `/p:TargetProfile=Test`.</span></span>
    
     ![][38]
    
     <span data-ttu-id="1382b-182">By this time, your build should be completed successfully.</span><span class="sxs-lookup"><span data-stu-id="1382b-182">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
13. <span data-ttu-id="1382b-183">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span><span class="sxs-lookup"><span data-stu-id="1382b-183">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
14. <span data-ttu-id="1382b-184">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span><span class="sxs-lookup"><span data-stu-id="1382b-184">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span></span>
    
     ![][30]
15. <span data-ttu-id="1382b-185">Browse to your site's URL.</span><span class="sxs-lookup"><span data-stu-id="1382b-185">Browse to your site's URL.</span></span> <span data-ttu-id="1382b-186">For a web app, just click the **Browse** button on the command bar.</span><span class="sxs-lookup"><span data-stu-id="1382b-186">For a web app, just click the **Browse** button on the command bar.</span></span> <span data-ttu-id="1382b-187">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment for a cloud service.</span><span class="sxs-lookup"><span data-stu-id="1382b-187">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment for a cloud service.</span></span> <span data-ttu-id="1382b-188">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span><span class="sxs-lookup"><span data-stu-id="1382b-188">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span></span> <span data-ttu-id="1382b-189">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span><span class="sxs-lookup"><span data-stu-id="1382b-189">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span></span> <span data-ttu-id="1382b-190">This screenshot shows where the site URL is on the cloud service's dashboard page.</span><span class="sxs-lookup"><span data-stu-id="1382b-190">This screenshot shows where the site URL is on the cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="1382b-191">A new browser tab will open to reveal your running site.</span><span class="sxs-lookup"><span data-stu-id="1382b-191">A new browser tab will open to reveal your running site.</span></span>
    
    ![][32]
    
    <span data-ttu-id="1382b-192">For cloud services, if you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span><span class="sxs-lookup"><span data-stu-id="1382b-192">For cloud services, if you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="1382b-193">The latest one marked as Active.</span><span class="sxs-lookup"><span data-stu-id="1382b-193">The latest one marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="1382b-194">5: Redeploy an earlier build</span><span class="sxs-lookup"><span data-stu-id="1382b-194">5: Redeploy an earlier build</span></span>
<span data-ttu-id="1382b-195">This step applies to cloud services and is optional.</span><span class="sxs-lookup"><span data-stu-id="1382b-195">This step applies to cloud services and is optional.</span></span> <span data-ttu-id="1382b-196">In the Azure classic portal, choose an earlier deployment and then choose the **Redeploy** button to rewind your site to an earlier check-in.</span><span class="sxs-lookup"><span data-stu-id="1382b-196">In the Azure classic portal, choose an earlier deployment and then choose the **Redeploy** button to rewind your site to an earlier check-in.</span></span>  <span data-ttu-id="1382b-197">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span><span class="sxs-lookup"><span data-stu-id="1382b-197">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-the-production-deployment"></a><span data-ttu-id="1382b-198">6: Change the Production deployment</span><span class="sxs-lookup"><span data-stu-id="1382b-198">6: Change the Production deployment</span></span>
<span data-ttu-id="1382b-199">This step applies only to cloud services, not web apps.</span><span class="sxs-lookup"><span data-stu-id="1382b-199">This step applies only to cloud services, not web apps.</span></span> <span data-ttu-id="1382b-200">When you are ready, you can promote the Staging environment to the production environment by choosing the **Swap** button in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="1382b-200">When you are ready, you can promote the Staging environment to the production environment by choosing the **Swap** button in the Azure classic portal.</span></span> <span data-ttu-id="1382b-201">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span><span class="sxs-lookup"><span data-stu-id="1382b-201">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="1382b-202">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span><span class="sxs-lookup"><span data-stu-id="1382b-202">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span></span>

![][35]

## <a name="7-run-unit-tests"></a><span data-ttu-id="1382b-203">7: Run unit tests</span><span class="sxs-lookup"><span data-stu-id="1382b-203">7: Run unit tests</span></span>
<span data-ttu-id="1382b-204">This step applies only to web apps, not cloud services.</span><span class="sxs-lookup"><span data-stu-id="1382b-204">This step applies only to web apps, not cloud services.</span></span> <span data-ttu-id="1382b-205">To put a quality gate on your deployment, you can run unit tests and if they fail, you can stop the deployment.</span><span class="sxs-lookup"><span data-stu-id="1382b-205">To put a quality gate on your deployment, you can run unit tests and if they fail, you can stop the deployment.</span></span>

1. <span data-ttu-id="1382b-206">In Visual Studio, add a unit test project.</span><span class="sxs-lookup"><span data-stu-id="1382b-206">In Visual Studio, add a unit test project.</span></span>
   
   ![][39]
2. <span data-ttu-id="1382b-207">Add project references to the project you want to test.</span><span class="sxs-lookup"><span data-stu-id="1382b-207">Add project references to the project you want to test.</span></span>
   
   ![][40]
3. <span data-ttu-id="1382b-208">Add some unit tests.</span><span class="sxs-lookup"><span data-stu-id="1382b-208">Add some unit tests.</span></span> <span data-ttu-id="1382b-209">To get started, try a dummy test that will always pass.</span><span class="sxs-lookup"><span data-stu-id="1382b-209">To get started, try a dummy test that will always pass.</span></span>
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. <span data-ttu-id="1382b-210">Edit the build definition, choose the **Process** tab, and expand the **Test** node.</span><span class="sxs-lookup"><span data-stu-id="1382b-210">Edit the build definition, choose the **Process** tab, and expand the **Test** node.</span></span>
5. <span data-ttu-id="1382b-211">Set the **Fail build on test failure** to True.</span><span class="sxs-lookup"><span data-stu-id="1382b-211">Set the **Fail build on test failure** to True.</span></span> <span data-ttu-id="1382b-212">This means that the deployment won't occur unless the tests pass.</span><span class="sxs-lookup"><span data-stu-id="1382b-212">This means that the deployment won't occur unless the tests pass.</span></span>
   
   ![][41]
6. <span data-ttu-id="1382b-213">Queue a new build.</span><span class="sxs-lookup"><span data-stu-id="1382b-213">Queue a new build.</span></span>
   
   ![][42]
   
   ![][43]
7. <span data-ttu-id="1382b-214">While the build is proceeding, check on its progress.</span><span class="sxs-lookup"><span data-stu-id="1382b-214">While the build is proceeding, check on its progress.</span></span>
   
    ![][44]
   
    ![][45]
8. <span data-ttu-id="1382b-215">When the build is done, check the test results.</span><span class="sxs-lookup"><span data-stu-id="1382b-215">When the build is done, check the test results.</span></span>
   
    ![][46]
   
    ![][47]
9. <span data-ttu-id="1382b-216">Try creating a test that will fail.</span><span class="sxs-lookup"><span data-stu-id="1382b-216">Try creating a test that will fail.</span></span> <span data-ttu-id="1382b-217">Add a new test by copying the first one, rename it, and comment out the line of code that states NotImplementedException is an expected exception.</span><span class="sxs-lookup"><span data-stu-id="1382b-217">Add a new test by copying the first one, rename it, and comment out the line of code that states NotImplementedException is an expected exception.</span></span>
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. <span data-ttu-id="1382b-218">Check in the change to queue a new build.</span><span class="sxs-lookup"><span data-stu-id="1382b-218">Check in the change to queue a new build.</span></span>
    
     ![][48]
11. <span data-ttu-id="1382b-219">View the test results to see details about the failure.</span><span class="sxs-lookup"><span data-stu-id="1382b-219">View the test results to see details about the failure.</span></span>
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a><span data-ttu-id="1382b-220">Next steps</span><span class="sxs-lookup"><span data-stu-id="1382b-220">Next steps</span></span>
<span data-ttu-id="1382b-221">For more about unit testing in Visual Studio Team Services, see [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span><span class="sxs-lookup"><span data-stu-id="1382b-221">For more about unit testing in Visual Studio Team Services, see [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span></span> <span data-ttu-id="1382b-222">If you're using Git, see [Share your code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and [Continuous deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="1382b-222">If you're using Git, see [Share your code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and [Continuous deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span>  <span data-ttu-id="1382b-223">For more information about Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="1382b-223">For more information about Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG












































