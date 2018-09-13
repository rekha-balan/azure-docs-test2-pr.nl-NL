---
title: Continuous delivery with Git and Visual Studio Team Services in Azure | Microsoft Docs
description: Learn how to configure your Visual Studio Team Services team projects to use Git to automatically build and deploy to the Web App feature in Azure App Service or cloud services.
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: ''
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: 3cbefdf8c30746882037a834322d7152cdc1d03a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556768"
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services-and-git"></a><span data-ttu-id="aeb01-103">Continuous delivery to Azure using Visual Studio Team Services and Git</span><span class="sxs-lookup"><span data-stu-id="aeb01-103">Continuous delivery to Azure using Visual Studio Team Services and Git</span></span>
<span data-ttu-id="aeb01-104">You can use Visual Studio Team Services team projects to host a Git repository for your source code, and automatically build and deploy to Azure web apps or cloud services whenever you push a commit to the repository.</span><span class="sxs-lookup"><span data-stu-id="aeb01-104">You can use Visual Studio Team Services team projects to host a Git repository for your source code, and automatically build and deploy to Azure web apps or cloud services whenever you push a commit to the repository.</span></span>

<span data-ttu-id="aeb01-105">You'll need Visual Studio 2013 and the Azure SDK installed.</span><span class="sxs-lookup"><span data-stu-id="aeb01-105">You'll need Visual Studio 2013 and the Azure SDK installed.</span></span> <span data-ttu-id="aeb01-106">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="aeb01-106">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span></span> <span data-ttu-id="aeb01-107">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="aeb01-107">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="aeb01-108">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="aeb01-108">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="aeb01-109">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span><span class="sxs-lookup"><span data-stu-id="aeb01-109">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-git-repository"></a><span data-ttu-id="aeb01-110">1: Create a Git repository</span><span class="sxs-lookup"><span data-stu-id="aeb01-110">1: Create a Git repository</span></span>
1. <span data-ttu-id="aeb01-111">If you don’t already have a Visual Studio Team Services account, you can get one  [here](http://go.microsoft.com/fwlink/?LinkId=397665).</span><span class="sxs-lookup"><span data-stu-id="aeb01-111">If you don’t already have a Visual Studio Team Services account, you can get one  [here](http://go.microsoft.com/fwlink/?LinkId=397665).</span></span> <span data-ttu-id="aeb01-112">When you create your team project, choose Git as your source control system.</span><span class="sxs-lookup"><span data-stu-id="aeb01-112">When you create your team project, choose Git as your source control system.</span></span> <span data-ttu-id="aeb01-113">Follow the instructions to connect Visual Studio to your team project.</span><span class="sxs-lookup"><span data-stu-id="aeb01-113">Follow the instructions to connect Visual Studio to your team project.</span></span>
2. <span data-ttu-id="aeb01-114">In **Team Explorer**, choose the **Clone this repository** link.</span><span class="sxs-lookup"><span data-stu-id="aeb01-114">In **Team Explorer**, choose the **Clone this repository** link.</span></span>
   
    ![][3]
3. <span data-ttu-id="aeb01-115">Specify the location of the local copy and then choose the **Clone** button.</span><span class="sxs-lookup"><span data-stu-id="aeb01-115">Specify the location of the local copy and then choose the **Clone** button.</span></span>

## <a name="2-create-a-project-and-commit-it-to-the-repository"></a><span data-ttu-id="aeb01-116">2: Create a project and commit it to the repository</span><span class="sxs-lookup"><span data-stu-id="aeb01-116">2: Create a project and commit it to the repository</span></span>
1. <span data-ttu-id="aeb01-117">In **Team Explorer**, in the **Solutions** section, choose the **New** link to create a new project in the local repository.</span><span class="sxs-lookup"><span data-stu-id="aeb01-117">In **Team Explorer**, in the **Solutions** section, choose the **New** link to create a new project in the local repository.</span></span>
   
    ![][4]
2. <span data-ttu-id="aeb01-118">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="aeb01-118">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span></span> <span data-ttu-id="aeb01-119">Create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span><span class="sxs-lookup"><span data-stu-id="aeb01-119">Create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="aeb01-120">Make sure that the project targets the .NET Framework 4 or later.</span><span class="sxs-lookup"><span data-stu-id="aeb01-120">Make sure that the project targets the .NET Framework 4 or later.</span></span> <span data-ttu-id="aeb01-121">If you are creating a cloud service project, add an ASP.NET MVC web role and a worker role.</span><span class="sxs-lookup"><span data-stu-id="aeb01-121">If you are creating a cloud service project, add an ASP.NET MVC web role and a worker role.</span></span>
   <span data-ttu-id="aeb01-122">If you want to create a web app, choose the **ASP.NET Web Application** project template, and then choose **MVC**.</span><span class="sxs-lookup"><span data-stu-id="aeb01-122">If you want to create a web app, choose the **ASP.NET Web Application** project template, and then choose **MVC**.</span></span> <span data-ttu-id="aeb01-123">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="aeb01-123">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) for more information.</span></span>
3. <span data-ttu-id="aeb01-124">Open the shortcut menu for the solution, and choose **Commit**.</span><span class="sxs-lookup"><span data-stu-id="aeb01-124">Open the shortcut menu for the solution, and choose **Commit**.</span></span>
   
    ![][7]
4. <span data-ttu-id="aeb01-125">If this is the first time you've used Git in Visual Studio Team Services, you'll need to provide some information to identify yourself in Git.</span><span class="sxs-lookup"><span data-stu-id="aeb01-125">If this is the first time you've used Git in Visual Studio Team Services, you'll need to provide some information to identify yourself in Git.</span></span> <span data-ttu-id="aeb01-126">In the **Pending Changes** area of **Team Explorer**, enter your username and email address.</span><span class="sxs-lookup"><span data-stu-id="aeb01-126">In the **Pending Changes** area of **Team Explorer**, enter your username and email address.</span></span> <span data-ttu-id="aeb01-127">Enter a comment for the commit and then choose the **Commit** button.</span><span class="sxs-lookup"><span data-stu-id="aeb01-127">Enter a comment for the commit and then choose the **Commit** button.</span></span>
   
    ![][8]
5. <span data-ttu-id="aeb01-128">Note the options to include or exclude specific changes when you check in.</span><span class="sxs-lookup"><span data-stu-id="aeb01-128">Note the options to include or exclude specific changes when you check in.</span></span> <span data-ttu-id="aeb01-129">If the changes you want are excluded, choose **Include All**.</span><span class="sxs-lookup"><span data-stu-id="aeb01-129">If the changes you want are excluded, choose **Include All**.</span></span>
6. <span data-ttu-id="aeb01-130">You've now committed the changes in your local copy of the repository.</span><span class="sxs-lookup"><span data-stu-id="aeb01-130">You've now committed the changes in your local copy of the repository.</span></span> <span data-ttu-id="aeb01-131">Next, sync those changes with the server by choosing the **Sync** link.</span><span class="sxs-lookup"><span data-stu-id="aeb01-131">Next, sync those changes with the server by choosing the **Sync** link.</span></span>

## <a name="3-connect-the-project-to-azure"></a><span data-ttu-id="aeb01-132">3: Connect the project to Azure</span><span class="sxs-lookup"><span data-stu-id="aeb01-132">3: Connect the project to Azure</span></span>
1. <span data-ttu-id="aeb01-133">Now that you have a Git repository in Visual Studio Team Services with some source code in it, you are ready to connect your git repository to Azure.</span><span class="sxs-lookup"><span data-stu-id="aeb01-133">Now that you have a Git repository in Visual Studio Team Services with some source code in it, you are ready to connect your git repository to Azure.</span></span>  <span data-ttu-id="aeb01-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the + icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span><span class="sxs-lookup"><span data-stu-id="aeb01-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the + icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span>
   
    ![][9]
2. <span data-ttu-id="aeb01-135">For cloud services, choose the **Set up publishing with Visual Studio Team Services** link.</span><span class="sxs-lookup"><span data-stu-id="aeb01-135">For cloud services, choose the **Set up publishing with Visual Studio Team Services** link.</span></span> <span data-ttu-id="aeb01-136">For web apps, choose the **Set up deployment from source control** link.</span><span class="sxs-lookup"><span data-stu-id="aeb01-136">For web apps, choose the **Set up deployment from source control** link.</span></span>
   
    ![][10]
3. <span data-ttu-id="aeb01-137">In the wizard, type the name of your Visual Studio Team Services account in the textbox and choose the **Authorize Now** link.</span><span class="sxs-lookup"><span data-stu-id="aeb01-137">In the wizard, type the name of your Visual Studio Team Services account in the textbox and choose the **Authorize Now** link.</span></span> <span data-ttu-id="aeb01-138">You might be asked to sign in.</span><span class="sxs-lookup"><span data-stu-id="aeb01-138">You might be asked to sign in.</span></span>
   
    ![][11]
4. <span data-ttu-id="aeb01-139">In the **Connection Request** pop-up dialog, choose **Accept** to authorize Azure to configure your team project in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="aeb01-139">In the **Connection Request** pop-up dialog, choose **Accept** to authorize Azure to configure your team project in Visual Studio Team Services.</span></span>
   
    ![][12]
5. <span data-ttu-id="aeb01-140">After authorization succeeds, you see a dropdown list that contains your Visual Studio Team Services team projects.</span><span class="sxs-lookup"><span data-stu-id="aeb01-140">After authorization succeeds, you see a dropdown list that contains your Visual Studio Team Services team projects.</span></span>  <span data-ttu-id="aeb01-141">Select the name of team project that you created in the previous steps, and choose the wizard's checkmark button.</span><span class="sxs-lookup"><span data-stu-id="aeb01-141">Select the name of team project that you created in the previous steps, and choose the wizard's checkmark button.</span></span>
   
    ![][13]
   
    <span data-ttu-id="aeb01-142">The next time you push a commit to your repository, Visual Studio Team Services will build and deploy your project to Azure.</span><span class="sxs-lookup"><span data-stu-id="aeb01-142">The next time you push a commit to your repository, Visual Studio Team Services will build and deploy your project to Azure.</span></span>

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="aeb01-143">4: Trigger a rebuild and redeploy your project</span><span class="sxs-lookup"><span data-stu-id="aeb01-143">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="aeb01-144">In Visual Studio, open up a file and change it.</span><span class="sxs-lookup"><span data-stu-id="aeb01-144">In Visual Studio, open up a file and change it.</span></span> <span data-ttu-id="aeb01-145">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span><span class="sxs-lookup"><span data-stu-id="aeb01-145">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
2. <span data-ttu-id="aeb01-146">Edit the footer text for the site and save the file.</span><span class="sxs-lookup"><span data-stu-id="aeb01-146">Edit the footer text for the site and save the file.</span></span>
   
    ![][18]
3. <span data-ttu-id="aeb01-147">In **Solution Explorer**, open the shortcut menu for the solution node, project node, or the file you changed, and then choose **Commit**.</span><span class="sxs-lookup"><span data-stu-id="aeb01-147">In **Solution Explorer**, open the shortcut menu for the solution node, project node, or the file you changed, and then choose **Commit**.</span></span>
4. <span data-ttu-id="aeb01-148">Type in a comment and choose **Commit**.</span><span class="sxs-lookup"><span data-stu-id="aeb01-148">Type in a comment and choose **Commit**.</span></span>
   
    ![][20]
5. <span data-ttu-id="aeb01-149">Choose the **Sync** link.</span><span class="sxs-lookup"><span data-stu-id="aeb01-149">Choose the **Sync** link.</span></span>
   
    ![][38]
6. <span data-ttu-id="aeb01-150">Choose the **Push** link to push your commit to the repository in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="aeb01-150">Choose the **Push** link to push your commit to the repository in Visual Studio Team Services.</span></span> <span data-ttu-id="aeb01-151">(You can also use the **Sync** button to copy your commits to the repository.</span><span class="sxs-lookup"><span data-stu-id="aeb01-151">(You can also use the **Sync** button to copy your commits to the repository.</span></span> <span data-ttu-id="aeb01-152">The difference is that **Sync** also pulls the latest changes from the repository.)</span><span class="sxs-lookup"><span data-stu-id="aeb01-152">The difference is that **Sync** also pulls the latest changes from the repository.)</span></span>
   
    ![][39]
7. <span data-ttu-id="aeb01-153">Choose the **Home** button to return to the **Team Explorer** home page.</span><span class="sxs-lookup"><span data-stu-id="aeb01-153">Choose the **Home** button to return to the **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="aeb01-154">Choose **Builds** to view the builds in progress.</span><span class="sxs-lookup"><span data-stu-id="aeb01-154">Choose **Builds** to view the builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="aeb01-155">**Team Explorer** shows that a build has been triggered for your check-in.</span><span class="sxs-lookup"><span data-stu-id="aeb01-155">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="aeb01-156">To view a detailed log as the build progresses, double-click the name of the build in progress.</span><span class="sxs-lookup"><span data-stu-id="aeb01-156">To view a detailed log as the build progresses, double-click the name of the build in progress.</span></span>
10. <span data-ttu-id="aeb01-157">While the build is in-progress, take a look at the build definition that was created when you used the wizard to link to Azure.</span><span class="sxs-lookup"><span data-stu-id="aeb01-157">While the build is in-progress, take a look at the build definition that was created when you used the wizard to link to Azure.</span></span>  <span data-ttu-id="aeb01-158">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span><span class="sxs-lookup"><span data-stu-id="aeb01-158">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span></span>
    
    ![][25]
11. <span data-ttu-id="aeb01-159">In the **Trigger** tab, you will see that the build definition is set to build on every check-in, by default.</span><span class="sxs-lookup"><span data-stu-id="aeb01-159">In the **Trigger** tab, you will see that the build definition is set to build on every check-in, by default.</span></span> <span data-ttu-id="aeb01-160">(For a cloud service, Visual Studio Team Services builds and deploys the master branch to the staging environment automatically.</span><span class="sxs-lookup"><span data-stu-id="aeb01-160">(For a cloud service, Visual Studio Team Services builds and deploys the master branch to the staging environment automatically.</span></span> <span data-ttu-id="aeb01-161">You still have to do a manual step to deploy to the live site.</span><span class="sxs-lookup"><span data-stu-id="aeb01-161">You still have to do a manual step to deploy to the live site.</span></span> <span data-ttu-id="aeb01-162">For a web app that doesn't have staging environment, it deploys the master branch directly to the live site.</span><span class="sxs-lookup"><span data-stu-id="aeb01-162">For a web app that doesn't have staging environment, it deploys the master branch directly to the live site.</span></span>
    
    ![][26]
12. <span data-ttu-id="aeb01-163">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span><span class="sxs-lookup"><span data-stu-id="aeb01-163">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span></span>
    
     ![][27]
13. <span data-ttu-id="aeb01-164">Specify values for the properties if you want different values than the defaults.</span><span class="sxs-lookup"><span data-stu-id="aeb01-164">Specify values for the properties if you want different values than the defaults.</span></span> <span data-ttu-id="aeb01-165">The properties for Azure publishing are in the **Deployment** section, and you might also need to set MSBuild parameters.</span><span class="sxs-lookup"><span data-stu-id="aeb01-165">The properties for Azure publishing are in the **Deployment** section, and you might also need to set MSBuild parameters.</span></span> <span data-ttu-id="aeb01-166">For example, in a cloud service project, to specify a service configuration other than "Cloud", set the MSbuild parameters to `/p:TargetProfile=[YourProfile]` where *[YourProfile]* matches a service configuration file with a name like ServiceConfiguration.*YourProfile*.cscfg.</span><span class="sxs-lookup"><span data-stu-id="aeb01-166">For example, in a cloud service project, to specify a service configuration other than "Cloud", set the MSbuild parameters to `/p:TargetProfile=[YourProfile]` where *[YourProfile]* matches a service configuration file with a name like ServiceConfiguration.*YourProfile*.cscfg.</span></span>
    
     <span data-ttu-id="aeb01-167">The following table shows the available properties in the **Deployment** section:</span><span class="sxs-lookup"><span data-stu-id="aeb01-167">The following table shows the available properties in the **Deployment** section:</span></span>
    
    | <span data-ttu-id="aeb01-168">Property</span><span class="sxs-lookup"><span data-stu-id="aeb01-168">Property</span></span> | <span data-ttu-id="aeb01-169">Default Value</span><span class="sxs-lookup"><span data-stu-id="aeb01-169">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="aeb01-170">Allow Untrusted Certificates</span><span class="sxs-lookup"><span data-stu-id="aeb01-170">Allow Untrusted Certificates</span></span> |<span data-ttu-id="aeb01-171">If false, SSL certificates must be signed by a root authority.</span><span class="sxs-lookup"><span data-stu-id="aeb01-171">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="aeb01-172">Allow Upgrade</span><span class="sxs-lookup"><span data-stu-id="aeb01-172">Allow Upgrade</span></span> |<span data-ttu-id="aeb01-173">Allows the deployment to update an existing deployment instead of creating a new one.</span><span class="sxs-lookup"><span data-stu-id="aeb01-173">Allows the deployment to update an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="aeb01-174">Preserves the IP address.</span><span class="sxs-lookup"><span data-stu-id="aeb01-174">Preserves the IP address.</span></span> |
    | <span data-ttu-id="aeb01-175">Do Not Delete</span><span class="sxs-lookup"><span data-stu-id="aeb01-175">Do Not Delete</span></span> |<span data-ttu-id="aeb01-176">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span><span class="sxs-lookup"><span data-stu-id="aeb01-176">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="aeb01-177">Path to Deployment Settings</span><span class="sxs-lookup"><span data-stu-id="aeb01-177">Path to Deployment Settings</span></span> |<span data-ttu-id="aeb01-178">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span><span class="sxs-lookup"><span data-stu-id="aeb01-178">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span></span> <span data-ttu-id="aeb01-179">Ignored for cloud services.</span><span class="sxs-lookup"><span data-stu-id="aeb01-179">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="aeb01-180">Sharepoint Deployment Environment</span><span class="sxs-lookup"><span data-stu-id="aeb01-180">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="aeb01-181">The same as the service name.</span><span class="sxs-lookup"><span data-stu-id="aeb01-181">The same as the service name.</span></span> |
    | <span data-ttu-id="aeb01-182">Azure Deployment Environment</span><span class="sxs-lookup"><span data-stu-id="aeb01-182">Azure Deployment Environment</span></span> |<span data-ttu-id="aeb01-183">The web app or cloud service name.</span><span class="sxs-lookup"><span data-stu-id="aeb01-183">The web app or cloud service name.</span></span> |
14. <span data-ttu-id="aeb01-184">By this time, your build should be completed successfully.</span><span class="sxs-lookup"><span data-stu-id="aeb01-184">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
15. <span data-ttu-id="aeb01-185">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span><span class="sxs-lookup"><span data-stu-id="aeb01-185">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
16. <span data-ttu-id="aeb01-186">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span><span class="sxs-lookup"><span data-stu-id="aeb01-186">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span></span>
    
     ![][30]
17. <span data-ttu-id="aeb01-187">Browse to your site's URL.</span><span class="sxs-lookup"><span data-stu-id="aeb01-187">Browse to your site's URL.</span></span> <span data-ttu-id="aeb01-188">For a web app, just choose  the **Browse** button in the portal.</span><span class="sxs-lookup"><span data-stu-id="aeb01-188">For a web app, just choose  the **Browse** button in the portal.</span></span> <span data-ttu-id="aeb01-189">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment.</span><span class="sxs-lookup"><span data-stu-id="aeb01-189">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment.</span></span>
    
    <span data-ttu-id="aeb01-190">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span><span class="sxs-lookup"><span data-stu-id="aeb01-190">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span></span> <span data-ttu-id="aeb01-191">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span><span class="sxs-lookup"><span data-stu-id="aeb01-191">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span></span> <span data-ttu-id="aeb01-192">Here's where the site URL is on the cloud service's dashboard page.</span><span class="sxs-lookup"><span data-stu-id="aeb01-192">Here's where the site URL is on the cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="aeb01-193">A new browser tab will open to reveal your running site.</span><span class="sxs-lookup"><span data-stu-id="aeb01-193">A new browser tab will open to reveal your running site.</span></span>
    
    ![][32]
18. <span data-ttu-id="aeb01-194">If you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span><span class="sxs-lookup"><span data-stu-id="aeb01-194">If you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="aeb01-195">The latest one is marked as Active.</span><span class="sxs-lookup"><span data-stu-id="aeb01-195">The latest one is marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="aeb01-196">5: Redeploy an earlier build</span><span class="sxs-lookup"><span data-stu-id="aeb01-196">5: Redeploy an earlier build</span></span>
<span data-ttu-id="aeb01-197">This step is optional.</span><span class="sxs-lookup"><span data-stu-id="aeb01-197">This step is optional.</span></span> <span data-ttu-id="aeb01-198">In the Azure classic portal, choose an earlier deployment and choose **Redeploy** to rewind your site to an earlier check-in.</span><span class="sxs-lookup"><span data-stu-id="aeb01-198">In the Azure classic portal, choose an earlier deployment and choose **Redeploy** to rewind your site to an earlier check-in.</span></span> <span data-ttu-id="aeb01-199">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span><span class="sxs-lookup"><span data-stu-id="aeb01-199">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-the-production-deployment"></a><span data-ttu-id="aeb01-200">6: Change the Production deployment</span><span class="sxs-lookup"><span data-stu-id="aeb01-200">6: Change the Production deployment</span></span>
<span data-ttu-id="aeb01-201">When you are ready, you can promote the Staging environment to the Production environment by choosing **Swap** in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="aeb01-201">When you are ready, you can promote the Staging environment to the Production environment by choosing **Swap** in the Azure classic portal.</span></span> <span data-ttu-id="aeb01-202">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span><span class="sxs-lookup"><span data-stu-id="aeb01-202">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="aeb01-203">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span><span class="sxs-lookup"><span data-stu-id="aeb01-203">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span></span>

![][35]

## <a name="7-deploy-from-a-working-branch"></a><span data-ttu-id="aeb01-204">7: Deploy from a working branch.</span><span class="sxs-lookup"><span data-stu-id="aeb01-204">7: Deploy from a working branch.</span></span>
<span data-ttu-id="aeb01-205">When you use Git, you usually make changes in a working branch and integrate into the master branch when your development reaches a finished state.</span><span class="sxs-lookup"><span data-stu-id="aeb01-205">When you use Git, you usually make changes in a working branch and integrate into the master branch when your development reaches a finished state.</span></span> <span data-ttu-id="aeb01-206">During the development phase of a project, you'll want to build and deploy the working branch to Azure.</span><span class="sxs-lookup"><span data-stu-id="aeb01-206">During the development phase of a project, you'll want to build and deploy the working branch to Azure.</span></span>

1. <span data-ttu-id="aeb01-207">In **Team Explorer**, choose the **Home** button and then choose the **Branches** button.</span><span class="sxs-lookup"><span data-stu-id="aeb01-207">In **Team Explorer**, choose the **Home** button and then choose the **Branches** button.</span></span>
   
    ![][40]
2. <span data-ttu-id="aeb01-208">Choose the **New Branch** link.</span><span class="sxs-lookup"><span data-stu-id="aeb01-208">Choose the **New Branch** link.</span></span>
   
    ![][41]
3. <span data-ttu-id="aeb01-209">Enter the name of the branch, such as "working," and choose **Create Branch**.</span><span class="sxs-lookup"><span data-stu-id="aeb01-209">Enter the name of the branch, such as "working," and choose **Create Branch**.</span></span> <span data-ttu-id="aeb01-210">This creates a new local branch.</span><span class="sxs-lookup"><span data-stu-id="aeb01-210">This creates a new local branch.</span></span>
   
    ![][42]
4. <span data-ttu-id="aeb01-211">Publish the branch.</span><span class="sxs-lookup"><span data-stu-id="aeb01-211">Publish the branch.</span></span> <span data-ttu-id="aeb01-212">Choose the branch name in **Unpublished branches**, and choose **Publish**.</span><span class="sxs-lookup"><span data-stu-id="aeb01-212">Choose the branch name in **Unpublished branches**, and choose **Publish**.</span></span>
   
    ![][44]
5. <span data-ttu-id="aeb01-213">By default, only changes to the master branch trigger a continuous build.</span><span class="sxs-lookup"><span data-stu-id="aeb01-213">By default, only changes to the master branch trigger a continuous build.</span></span> <span data-ttu-id="aeb01-214">To set up continuous build for a working branch, choose the **Builds** page in **Team Explorer**, and choose **Edit Build Definition**.</span><span class="sxs-lookup"><span data-stu-id="aeb01-214">To set up continuous build for a working branch, choose the **Builds** page in **Team Explorer**, and choose **Edit Build Definition**.</span></span>
6. <span data-ttu-id="aeb01-215">Open the **Source Settings** tab. Under **Monitored branches for continuous integration and build**, choose **Click here to add a new row**.</span><span class="sxs-lookup"><span data-stu-id="aeb01-215">Open the **Source Settings** tab. Under **Monitored branches for continuous integration and build**, choose **Click here to add a new row**.</span></span>
   
    ![][47]
7. <span data-ttu-id="aeb01-216">Specify the branch you created, such as refs/heads/working.</span><span class="sxs-lookup"><span data-stu-id="aeb01-216">Specify the branch you created, such as refs/heads/working.</span></span>
   
    ![][48]
8. <span data-ttu-id="aeb01-217">Make a change in the code, open the shortcut menu for the changed file, and then choose **Commit**.</span><span class="sxs-lookup"><span data-stu-id="aeb01-217">Make a change in the code, open the shortcut menu for the changed file, and then choose **Commit**.</span></span>
   
    ![][43]
9. <span data-ttu-id="aeb01-218">Choose the **Unsynced Commits** link, and choose  the **Sync** button or the **Push** link to copy the changes to the copy of the working branch in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="aeb01-218">Choose the **Unsynced Commits** link, and choose  the **Sync** button or the **Push** link to copy the changes to the copy of the working branch in Visual Studio Team Services.</span></span>
   
   ![][45]
10. <span data-ttu-id="aeb01-219">Navigate to the **Builds** view and find the build that just got triggered for the working branch.</span><span class="sxs-lookup"><span data-stu-id="aeb01-219">Navigate to the **Builds** view and find the build that just got triggered for the working branch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aeb01-220">Next steps</span><span class="sxs-lookup"><span data-stu-id="aeb01-220">Next steps</span></span>
<span data-ttu-id="aeb01-221">To learn more tips on using Git with Visual Studio Team Services, see [Develop and share your code in Git using Visual Studio](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and for information about using a Git repository that's not managed by Visual Studio Team Services to publish to Azure, see [Continuous Deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="aeb01-221">To learn more tips on using Git with Visual Studio Team Services, see [Develop and share your code in Git using Visual Studio](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and for information about using a Git repository that's not managed by Visual Studio Team Services to publish to Azure, see [Continuous Deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span> <span data-ttu-id="aeb01-222">For more information on Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="aeb01-222">For more information on Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG








































