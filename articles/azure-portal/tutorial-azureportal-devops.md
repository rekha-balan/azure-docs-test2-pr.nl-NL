---
title: 'Tutorial:  DevOps with the Azure portal | Microsoft Docs'
description: Learn the various DevOps workflows in the Azure Portal.
services: azure-portal
documentationcenter: ''
author: mlearned
manager: douge
editor: mlearned
ms.assetid: 4f1c5bc1-c732-4d35-b5df-0fd68e547d38
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/05/2016
ms.author: mlearned
ms.openlocfilehash: d0bf66a224a8a42f813bc817f78321167e309bdb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44814020"
---
# <a name="tutorial-devops-with-the-azure-portal"></a><span data-ttu-id="76837-103">Tutorial: DevOps with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="76837-103">Tutorial: DevOps with the Azure portal</span></span>
<span data-ttu-id="76837-104">The Azure platform is full of flexible DevOps workflows.</span><span class="sxs-lookup"><span data-stu-id="76837-104">The Azure platform is full of flexible DevOps workflows.</span></span> <span data-ttu-id="76837-105">In this tutorial, you learn how to leverage the capabilities of the Azure portal to develop, test, deploy, troubleshoot, monitor, and manage running applications.</span><span class="sxs-lookup"><span data-stu-id="76837-105">In this tutorial, you learn how to leverage the capabilities of the Azure portal to develop, test, deploy, troubleshoot, monitor, and manage running applications.</span></span> <span data-ttu-id="76837-106">This tutorial focuses on the following:</span><span class="sxs-lookup"><span data-stu-id="76837-106">This tutorial focuses on the following:</span></span>

1. <span data-ttu-id="76837-107">Creating a web app and enabling continuous deployment</span><span class="sxs-lookup"><span data-stu-id="76837-107">Creating a web app and enabling continuous deployment</span></span>
2. <span data-ttu-id="76837-108">Develop and test an app</span><span class="sxs-lookup"><span data-stu-id="76837-108">Develop and test an app</span></span>
3. <span data-ttu-id="76837-109">Monitoring and Troubleshooting an app</span><span class="sxs-lookup"><span data-stu-id="76837-109">Monitoring and Troubleshooting an app</span></span>
4. <span data-ttu-id="76837-110">General application management tasks</span><span class="sxs-lookup"><span data-stu-id="76837-110">General application management tasks</span></span>

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a><span data-ttu-id="76837-111">Creating a web app and enabling continuous deployment</span><span class="sxs-lookup"><span data-stu-id="76837-111">Creating a web app and enabling continuous deployment</span></span>
<span data-ttu-id="76837-112">Create a Web app with [Azure App Service](https://azure.microsoft.com/services/app-service/), which you’ll use in the rest of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="76837-112">Create a Web app with [Azure App Service](https://azure.microsoft.com/services/app-service/), which you’ll use in the rest of this tutorial.</span></span> <span data-ttu-id="76837-113">You’ll initially enable continuous deployment from your source code repository into your running Azure environment.</span><span class="sxs-lookup"><span data-stu-id="76837-113">You’ll initially enable continuous deployment from your source code repository into your running Azure environment.</span></span>

1. <span data-ttu-id="76837-114">Sign into the Azure portal</span><span class="sxs-lookup"><span data-stu-id="76837-114">Sign into the Azure portal</span></span>
2. <span data-ttu-id="76837-115">Choose **App Services** &gt; **Add icon** and enter a name, choose your subscription, and create a new resource group to serve as the container for the service.</span><span class="sxs-lookup"><span data-stu-id="76837-115">Choose **App Services** &gt; **Add icon** and enter a name, choose your subscription, and create a new resource group to serve as the container for the service.</span></span>
   
   <span data-ttu-id="76837-116">Resource groups allow you to manage various aspects of the solution such as billing, deployments, and monitoring all as a single group via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="76837-116">Resource groups allow you to manage various aspects of the solution such as billing, deployments, and monitoring all as a single group via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>
   
   ![image1][image1]
3. <span data-ttu-id="76837-118">After a few moments, your app service is created.</span><span class="sxs-lookup"><span data-stu-id="76837-118">After a few moments, your app service is created.</span></span> <span data-ttu-id="76837-119">Take a few minutes to explore the various menu options for the service in the portal.</span><span class="sxs-lookup"><span data-stu-id="76837-119">Take a few minutes to explore the various menu options for the service in the portal.</span></span>
   
   ![image2][image2]    
4. <span data-ttu-id="76837-121">Click the URL.</span><span class="sxs-lookup"><span data-stu-id="76837-121">Click the URL.</span></span> <span data-ttu-id="76837-122">Notice the variety of available choices for tools and repositories.</span><span class="sxs-lookup"><span data-stu-id="76837-122">Notice the variety of available choices for tools and repositories.</span></span> <span data-ttu-id="76837-123">You can also use the languages and frameworks of your choice including .NET, Java, and Ruby.</span><span class="sxs-lookup"><span data-stu-id="76837-123">You can also use the languages and frameworks of your choice including .NET, Java, and Ruby.</span></span>
   
   ![image3][image3]    
5. <span data-ttu-id="76837-125">The Azure portal makes continuous deployment an easy process that involves only a few simple steps.</span><span class="sxs-lookup"><span data-stu-id="76837-125">The Azure portal makes continuous deployment an easy process that involves only a few simple steps.</span></span> <span data-ttu-id="76837-126">In the Azure portal, choose settings from the icon for the app service you created.</span><span class="sxs-lookup"><span data-stu-id="76837-126">In the Azure portal, choose settings from the icon for the app service you created.</span></span>
   
   ![image4][image4]
   
   <span data-ttu-id="76837-128">From the blade that opens on the right, scroll to the publishing section.</span><span class="sxs-lookup"><span data-stu-id="76837-128">From the blade that opens on the right, scroll to the publishing section.</span></span>
   
   ![image5][image5]
6. <span data-ttu-id="76837-130">Next, configure some settings to enable continuous deployment for the app.</span><span class="sxs-lookup"><span data-stu-id="76837-130">Next, configure some settings to enable continuous deployment for the app.</span></span> <span data-ttu-id="76837-131">Click Deployment Source and then click Choose Source.</span><span class="sxs-lookup"><span data-stu-id="76837-131">Click Deployment Source and then click Choose Source.</span></span> <span data-ttu-id="76837-132">Notice the variety of options you have for repository sources.</span><span class="sxs-lookup"><span data-stu-id="76837-132">Notice the variety of options you have for repository sources.</span></span>
   
   ![image6][image6]
7. <span data-ttu-id="76837-134">For this example, choose GitHub.</span><span class="sxs-lookup"><span data-stu-id="76837-134">For this example, choose GitHub.</span></span> <span data-ttu-id="76837-135">Optionally choose the repository of your choice and set up the authorization credentials.</span><span class="sxs-lookup"><span data-stu-id="76837-135">Optionally choose the repository of your choice and set up the authorization credentials.</span></span>
   
   ![image7][image7]
8. <span data-ttu-id="76837-137">After authorization to your repository, you can then choose a project and branch you wish to deploy.</span><span class="sxs-lookup"><span data-stu-id="76837-137">After authorization to your repository, you can then choose a project and branch you wish to deploy.</span></span> <span data-ttu-id="76837-138">There are several fictitious sample examples listed below.</span><span class="sxs-lookup"><span data-stu-id="76837-138">There are several fictitious sample examples listed below.</span></span>
   
   ![image8][image8]
9. <span data-ttu-id="76837-140">Once you choose your project and branch, click ok.</span><span class="sxs-lookup"><span data-stu-id="76837-140">Once you choose your project and branch, click ok.</span></span> <span data-ttu-id="76837-141">You should start to see notifications of a deployment.</span><span class="sxs-lookup"><span data-stu-id="76837-141">You should start to see notifications of a deployment.</span></span>
   
   ![image9][image9]
10. <span data-ttu-id="76837-143">Navigate back to GitHub to see the webhook that was created to integrate the source control repo with Azure.</span><span class="sxs-lookup"><span data-stu-id="76837-143">Navigate back to GitHub to see the webhook that was created to integrate the source control repo with Azure.</span></span> <span data-ttu-id="76837-144">The Azure portal enables integration with GitHub with only a few simple steps.</span><span class="sxs-lookup"><span data-stu-id="76837-144">The Azure portal enables integration with GitHub with only a few simple steps.</span></span>
    
    ![image10][image10]
11. <span data-ttu-id="76837-146">To demonstrate continuous deployment, you quickly add some content to the repository.</span><span class="sxs-lookup"><span data-stu-id="76837-146">To demonstrate continuous deployment, you quickly add some content to the repository.</span></span> <span data-ttu-id="76837-147">For a simple example, add a sample text file to a GitHub repo.</span><span class="sxs-lookup"><span data-stu-id="76837-147">For a simple example, add a sample text file to a GitHub repo.</span></span> <span data-ttu-id="76837-148">You are free to use .NET, Ruby, Python, or some other type of application with App Service.</span><span class="sxs-lookup"><span data-stu-id="76837-148">You are free to use .NET, Ruby, Python, or some other type of application with App Service.</span></span> <span data-ttu-id="76837-149">Feel free to add a text file, ASP.NET MVC, Java, or Ruby application to the repo of your choice.</span><span class="sxs-lookup"><span data-stu-id="76837-149">Feel free to add a text file, ASP.NET MVC, Java, or Ruby application to the repo of your choice.</span></span>
    
    ![image11][image11]
12. <span data-ttu-id="76837-151">After committing changes to your repository, you see a new deployment initiate in the portal notifications area.</span><span class="sxs-lookup"><span data-stu-id="76837-151">After committing changes to your repository, you see a new deployment initiate in the portal notifications area.</span></span> <span data-ttu-id="76837-152">Click Sync if you do not quickly see changes after committing to your repository.</span><span class="sxs-lookup"><span data-stu-id="76837-152">Click Sync if you do not quickly see changes after committing to your repository.</span></span>
    
    ![image12][image12]
13. <span data-ttu-id="76837-154">At this point, if you try and load the page for the app service, you may receive a 403 error.</span><span class="sxs-lookup"><span data-stu-id="76837-154">At this point, if you try and load the page for the app service, you may receive a 403 error.</span></span> <span data-ttu-id="76837-155">In this example, it is because there is no typical default document setup for the page such as a file like index.htm or default.html.</span><span class="sxs-lookup"><span data-stu-id="76837-155">In this example, it is because there is no typical default document setup for the page such as a file like index.htm or default.html.</span></span> <span data-ttu-id="76837-156">You can quickly remedy this with the tooling in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="76837-156">You can quickly remedy this with the tooling in the Azure portal.</span></span>  <span data-ttu-id="76837-157">In the Azure portal choose Settings &gt; Application Settings.</span><span class="sxs-lookup"><span data-stu-id="76837-157">In the Azure portal choose Settings &gt; Application Settings.</span></span>
    
     ![image13][image13]
14. <span data-ttu-id="76837-159">A blade opens for application settings.</span><span class="sxs-lookup"><span data-stu-id="76837-159">A blade opens for application settings.</span></span> <span data-ttu-id="76837-160">Enter the name of the page “SamplePage.html” and click Save.</span><span class="sxs-lookup"><span data-stu-id="76837-160">Enter the name of the page “SamplePage.html” and click Save.</span></span> <span data-ttu-id="76837-161">Take a few minutes to explore the other settings.</span><span class="sxs-lookup"><span data-stu-id="76837-161">Take a few minutes to explore the other settings.</span></span>
    
    ![image14][image14]
15. <span data-ttu-id="76837-163">Optionally refresh your browser URL to ensure you see the expected changes.</span><span class="sxs-lookup"><span data-stu-id="76837-163">Optionally refresh your browser URL to ensure you see the expected changes.</span></span> <span data-ttu-id="76837-164">In this case, there is some simple text now populating the page.</span><span class="sxs-lookup"><span data-stu-id="76837-164">In this case, there is some simple text now populating the page.</span></span> <span data-ttu-id="76837-165">Each additional change to the repository would result in a new automatic deployment.</span><span class="sxs-lookup"><span data-stu-id="76837-165">Each additional change to the repository would result in a new automatic deployment.</span></span>
    
    ![image15][image15]
    
    <span data-ttu-id="76837-167">Enabling continuous deployment with the Azure portal is an easy experience.</span><span class="sxs-lookup"><span data-stu-id="76837-167">Enabling continuous deployment with the Azure portal is an easy experience.</span></span> <span data-ttu-id="76837-168">You can also build more complex release pipelines and use many other techniques with existing source control and continuous integration systems to deploy to Azure, such as leveraging automated Azure Pipelines management systems.</span><span class="sxs-lookup"><span data-stu-id="76837-168">You can also build more complex release pipelines and use many other techniques with existing source control and continuous integration systems to deploy to Azure, such as leveraging automated Azure Pipelines management systems.</span></span>

## <a name="develop-and-test-an-app"></a><span data-ttu-id="76837-169">Develop and test an app</span><span class="sxs-lookup"><span data-stu-id="76837-169">Develop and test an app</span></span>
<span data-ttu-id="76837-170">Next, make some changes to the code base and rapidly deploy those changes.</span><span class="sxs-lookup"><span data-stu-id="76837-170">Next, make some changes to the code base and rapidly deploy those changes.</span></span> <span data-ttu-id="76837-171">You will also set up some performance testing for the Web app.</span><span class="sxs-lookup"><span data-stu-id="76837-171">You will also set up some performance testing for the Web app.</span></span>

1. <span data-ttu-id="76837-172">In the Azure portal choose App Services from the navigation pane, and locate your App Service.</span><span class="sxs-lookup"><span data-stu-id="76837-172">In the Azure portal choose App Services from the navigation pane, and locate your App Service.</span></span>
   
   ![image16][image16]
2. <span data-ttu-id="76837-174">Click Tools</span><span class="sxs-lookup"><span data-stu-id="76837-174">Click Tools</span></span>
   
   ![image17][image17]
3. <span data-ttu-id="76837-176">Notice the develop category under Tools.</span><span class="sxs-lookup"><span data-stu-id="76837-176">Notice the develop category under Tools.</span></span> <span data-ttu-id="76837-177">There are several useful tools here that allow us to work with apps without leaving the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="76837-177">There are several useful tools here that allow us to work with apps without leaving the Azure portal.</span></span> <span data-ttu-id="76837-178">Click on Console.</span><span class="sxs-lookup"><span data-stu-id="76837-178">Click on Console.</span></span>
   
   ![image18][image18]
4. <span data-ttu-id="76837-180">In the console window, you can issue live commands for your app.</span><span class="sxs-lookup"><span data-stu-id="76837-180">In the console window, you can issue live commands for your app.</span></span> <span data-ttu-id="76837-181">Type the dir command and hit enter.</span><span class="sxs-lookup"><span data-stu-id="76837-181">Type the dir command and hit enter.</span></span> <span data-ttu-id="76837-182">Note that commands requiring elevated privileges do not work.</span><span class="sxs-lookup"><span data-stu-id="76837-182">Note that commands requiring elevated privileges do not work.</span></span>
   
   ![image19][image19]
5. <span data-ttu-id="76837-184">Move back to the Develop category and choose Visual Studio Online.</span><span class="sxs-lookup"><span data-stu-id="76837-184">Move back to the Develop category and choose Visual Studio Online.</span></span> <span data-ttu-id="76837-185">Note: Visual Studio Online is now named Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="76837-185">Note: Visual Studio Online is now named Azure DevOps Services.</span></span>
   
   ![image20][image20]
6. <span data-ttu-id="76837-187">Toggle on the in-browser editing experience for your App.</span><span class="sxs-lookup"><span data-stu-id="76837-187">Toggle on the in-browser editing experience for your App.</span></span>
   
   ![image21][image21]
7. <span data-ttu-id="76837-189">A web extension installs for your app.</span><span class="sxs-lookup"><span data-stu-id="76837-189">A web extension installs for your app.</span></span> <span data-ttu-id="76837-190">Extensions quickly and easily add functionality to apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="76837-190">Extensions quickly and easily add functionality to apps in Azure.</span></span> <span data-ttu-id="76837-191">Notice some of the other extension types available in the screenshot below.</span><span class="sxs-lookup"><span data-stu-id="76837-191">Notice some of the other extension types available in the screenshot below.</span></span>
   
   ![image22][image22]
8. <span data-ttu-id="76837-193">Once the Visual Studio Online extension installs, click Go.</span><span class="sxs-lookup"><span data-stu-id="76837-193">Once the Visual Studio Online extension installs, click Go.</span></span>
   
   ![image23][image23]
9. <span data-ttu-id="76837-195">A browser tab opens where you see a development IDE directly in the browser.</span><span class="sxs-lookup"><span data-stu-id="76837-195">A browser tab opens where you see a development IDE directly in the browser.</span></span> <span data-ttu-id="76837-196">Notice the experience below is in Chrome.</span><span class="sxs-lookup"><span data-stu-id="76837-196">Notice the experience below is in Chrome.</span></span>
   
   ![image24][image24]
10. <span data-ttu-id="76837-198">You can perform several activities such as edit files, add files and folders, and download content from the live site.</span><span class="sxs-lookup"><span data-stu-id="76837-198">You can perform several activities such as edit files, add files and folders, and download content from the live site.</span></span> <span data-ttu-id="76837-199">Make a quick edit to the SamplePage.html file.</span><span class="sxs-lookup"><span data-stu-id="76837-199">Make a quick edit to the SamplePage.html file.</span></span>
    
    ![image25][image25]
11. <span data-ttu-id="76837-201">In a few moments, the changes are automatically saved.</span><span class="sxs-lookup"><span data-stu-id="76837-201">In a few moments, the changes are automatically saved.</span></span> <span data-ttu-id="76837-202">If you navigate back to the page, you can see the changes.</span><span class="sxs-lookup"><span data-stu-id="76837-202">If you navigate back to the page, you can see the changes.</span></span> <span data-ttu-id="76837-203">Keep in mind live edits like these are most likely not suitable for production environments.</span><span class="sxs-lookup"><span data-stu-id="76837-203">Keep in mind live edits like these are most likely not suitable for production environments.</span></span> <span data-ttu-id="76837-204">However, the tools make it very easy to make quick changes for dev and test environments.</span><span class="sxs-lookup"><span data-stu-id="76837-204">However, the tools make it very easy to make quick changes for dev and test environments.</span></span>
    
    ![image26][image26]
    
    ![image27][image27]
12. <span data-ttu-id="76837-207">Move back to the tools blade and under the Develop category, click on Performance Test.</span><span class="sxs-lookup"><span data-stu-id="76837-207">Move back to the tools blade and under the Develop category, click on Performance Test.</span></span>
    
    ![image28][image28]
13. <span data-ttu-id="76837-209">You need to set an Azure DevOps Services organization.</span><span class="sxs-lookup"><span data-stu-id="76837-209">You need to set an Azure DevOps Services organization.</span></span> <span data-ttu-id="76837-210">See here for more details: [Create an Azure DevOps Services Organization](https://docs.microsoft.com/vsts/organizations/accounts/create-organization-msa-or-work-student).</span><span class="sxs-lookup"><span data-stu-id="76837-210">See here for more details: [Create an Azure DevOps Services Organization](https://docs.microsoft.com/vsts/organizations/accounts/create-organization-msa-or-work-student).</span></span>
14. <span data-ttu-id="76837-211">Click on New to create a performance test.</span><span class="sxs-lookup"><span data-stu-id="76837-211">Click on New to create a performance test.</span></span>
    
    ![image29][image29]
    
    <span data-ttu-id="76837-213">Configure the various values and click Run Test at the bottom of the dialogue to initiate a performance test.</span><span class="sxs-lookup"><span data-stu-id="76837-213">Configure the various values and click Run Test at the bottom of the dialogue to initiate a performance test.</span></span>
    
    ![image30][image30]
    
    ![image31][image31]
15. <span data-ttu-id="76837-216">Once the test starts running, you can monitor the state.</span><span class="sxs-lookup"><span data-stu-id="76837-216">Once the test starts running, you can monitor the state.</span></span>
    
    ![image32][image32]
    
    <span data-ttu-id="76837-218">Once the test finishes, clicking on the result shows more details.</span><span class="sxs-lookup"><span data-stu-id="76837-218">Once the test finishes, clicking on the result shows more details.</span></span>
    
    ![image33][image33]
16. <span data-ttu-id="76837-220">In this example, you created a small test run, so there is limited data to analyze, but you can see various metrics as well as rerun your test from this view.</span><span class="sxs-lookup"><span data-stu-id="76837-220">In this example, you created a small test run, so there is limited data to analyze, but you can see various metrics as well as rerun your test from this view.</span></span> <span data-ttu-id="76837-221">The Azure portal makes creating, executing, and analyzing web performance tests an easy process.</span><span class="sxs-lookup"><span data-stu-id="76837-221">The Azure portal makes creating, executing, and analyzing web performance tests an easy process.</span></span> <span data-ttu-id="76837-222">The screenshots below display the performance data.</span><span class="sxs-lookup"><span data-stu-id="76837-222">The screenshots below display the performance data.</span></span>
    
    ![image34][image34]
    
    ![image35][image35]
    
    ![image36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a><span data-ttu-id="76837-226">Monitoring and troubleshooting an app</span><span class="sxs-lookup"><span data-stu-id="76837-226">Monitoring and troubleshooting an app</span></span>
<span data-ttu-id="76837-227">Azure provides many capabilities for monitoring and troubleshooting running applications.</span><span class="sxs-lookup"><span data-stu-id="76837-227">Azure provides many capabilities for monitoring and troubleshooting running applications.</span></span>

1. <span data-ttu-id="76837-228">In the Azure portal for Web app choose Tools.</span><span class="sxs-lookup"><span data-stu-id="76837-228">In the Azure portal for Web app choose Tools.</span></span>
   
   ![image37][image37]
2. <span data-ttu-id="76837-230">Under the Troubleshoot category, notice the various choices for using tools to troubleshoot potential issues with a running app.</span><span class="sxs-lookup"><span data-stu-id="76837-230">Under the Troubleshoot category, notice the various choices for using tools to troubleshoot potential issues with a running app.</span></span> <span data-ttu-id="76837-231">You can do things like monitor Live HTTP traffic, enable self-healing, view logs, and more.</span><span class="sxs-lookup"><span data-stu-id="76837-231">You can do things like monitor Live HTTP traffic, enable self-healing, view logs, and more.</span></span>
   
   ![image38][image38]
3. <span data-ttu-id="76837-233">Choose Site Metrics to quickly get a view of some HTTP codes.</span><span class="sxs-lookup"><span data-stu-id="76837-233">Choose Site Metrics to quickly get a view of some HTTP codes.</span></span>
   
   ![image39][image39]
4. <span data-ttu-id="76837-235">Choose Diagnostics as a Service.</span><span class="sxs-lookup"><span data-stu-id="76837-235">Choose Diagnostics as a Service.</span></span> <span data-ttu-id="76837-236">Choose your application type, then choose Run.</span><span class="sxs-lookup"><span data-stu-id="76837-236">Choose your application type, then choose Run.</span></span>
   
   ![image40][image40]
   
   <span data-ttu-id="76837-238">A collection begins.</span><span class="sxs-lookup"><span data-stu-id="76837-238">A collection begins.</span></span>
   
   ![image41][image41]
5. <span data-ttu-id="76837-240">You may choose the appropriate log to diagnose potential issues.</span><span class="sxs-lookup"><span data-stu-id="76837-240">You may choose the appropriate log to diagnose potential issues.</span></span> <span data-ttu-id="76837-241">You need to enable logging to see all of the available data options such as HTTP Logs.</span><span class="sxs-lookup"><span data-stu-id="76837-241">You need to enable logging to see all of the available data options such as HTTP Logs.</span></span>
   
   ![image42][image42]
   
   <span data-ttu-id="76837-243">By clicking on the Memory Dump file you can download and analyze a DebugDiag analysis report to help find potential issues.</span><span class="sxs-lookup"><span data-stu-id="76837-243">By clicking on the Memory Dump file you can download and analyze a DebugDiag analysis report to help find potential issues.</span></span>
   
   ![image43][image43]
6. <span data-ttu-id="76837-245">To view more data, you need to enable additional logging.</span><span class="sxs-lookup"><span data-stu-id="76837-245">To view more data, you need to enable additional logging.</span></span> <span data-ttu-id="76837-246">In the Azure portal, navigate to the Web app and choose Settings.</span><span class="sxs-lookup"><span data-stu-id="76837-246">In the Azure portal, navigate to the Web app and choose Settings.</span></span>
   
   ![image44][image44]
7. <span data-ttu-id="76837-248">Scroll down to the features category, and choose Diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="76837-248">Scroll down to the features category, and choose Diagnostic logs.</span></span>
   
      ![image45][image45]
8. <span data-ttu-id="76837-250">Notice the various options for logging.</span><span class="sxs-lookup"><span data-stu-id="76837-250">Notice the various options for logging.</span></span> <span data-ttu-id="76837-251">Toggle on Web server logging and click save.</span><span class="sxs-lookup"><span data-stu-id="76837-251">Toggle on Web server logging and click save.</span></span>
   
   ![image46][image46]
9. <span data-ttu-id="76837-253">Move back to the tools area for the app and choose Diagnostics as a service and click Run to rerun the data collection.</span><span class="sxs-lookup"><span data-stu-id="76837-253">Move back to the tools area for the app and choose Diagnostics as a service and click Run to rerun the data collection.</span></span>
   
   ![image47][image47]
10. <span data-ttu-id="76837-255">With the HTTP logging setting enabled, you now see data collected for HTTP Logs.</span><span class="sxs-lookup"><span data-stu-id="76837-255">With the HTTP logging setting enabled, you now see data collected for HTTP Logs.</span></span>
    
    ![image48][image48]
11. <span data-ttu-id="76837-257">By clicking the HTML file log, you produce a rich browser-based report for further investigation.</span><span class="sxs-lookup"><span data-stu-id="76837-257">By clicking the HTML file log, you produce a rich browser-based report for further investigation.</span></span>
    
    ![image49][image49]
12. <span data-ttu-id="76837-259">Move back to the tools section in the Azure portal for the app.</span><span class="sxs-lookup"><span data-stu-id="76837-259">Move back to the tools section in the Azure portal for the app.</span></span> <span data-ttu-id="76837-260">Scroll to the Tools section and choose Process Explorer.</span><span class="sxs-lookup"><span data-stu-id="76837-260">Scroll to the Tools section and choose Process Explorer.</span></span>
    
    ![image50][image50]
13. <span data-ttu-id="76837-262">By choosing Process Explorer, you can view details about running processes.</span><span class="sxs-lookup"><span data-stu-id="76837-262">By choosing Process Explorer, you can view details about running processes.</span></span> <span data-ttu-id="76837-263">Notice below you can drill into processes and even kill processes all from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="76837-263">Notice below you can drill into processes and even kill processes all from the Azure portal.</span></span>
    
    ![image51][image51]
    
    ![image52][image52]
14. <span data-ttu-id="76837-266">Move back to the Settings blade on the left.</span><span class="sxs-lookup"><span data-stu-id="76837-266">Move back to the Settings blade on the left.</span></span> <span data-ttu-id="76837-267">Click New support request.</span><span class="sxs-lookup"><span data-stu-id="76837-267">Click New support request.</span></span>
    
    ![image53][image53]
15. <span data-ttu-id="76837-269">From the blade on the right, you can fill out details about the issues, enter contact information, and even upload diagnostic data.</span><span class="sxs-lookup"><span data-stu-id="76837-269">From the blade on the right, you can fill out details about the issues, enter contact information, and even upload diagnostic data.</span></span> <span data-ttu-id="76837-270">The Azure portal enables working with Microsoft support a seamless experience.</span><span class="sxs-lookup"><span data-stu-id="76837-270">The Azure portal enables working with Microsoft support a seamless experience.</span></span>
    
    ![image54][image54]
    
    ![image55][image55]
    
    <span data-ttu-id="76837-273">The Azure portal helps provide powerful and familiar tooling experiences to help monitor and troubleshoot your running applications.</span><span class="sxs-lookup"><span data-stu-id="76837-273">The Azure portal helps provide powerful and familiar tooling experiences to help monitor and troubleshoot your running applications.</span></span> <span data-ttu-id="76837-274">You are also able to take action quickly by performing tasks such as recycling processes, enabling and disabling various data collections, and even integrating with Microsoft professional support.</span><span class="sxs-lookup"><span data-stu-id="76837-274">You are also able to take action quickly by performing tasks such as recycling processes, enabling and disabling various data collections, and even integrating with Microsoft professional support.</span></span>

## <a name="general-application-management"></a><span data-ttu-id="76837-275">General Application Management</span><span class="sxs-lookup"><span data-stu-id="76837-275">General Application Management</span></span>
<span data-ttu-id="76837-276">When managing applications, you often need to perform a broad variety of activities such as configuring backup strategies, implementing and managing identity providers, and configuring Role-based access control.</span><span class="sxs-lookup"><span data-stu-id="76837-276">When managing applications, you often need to perform a broad variety of activities such as configuring backup strategies, implementing and managing identity providers, and configuring Role-based access control.</span></span> <span data-ttu-id="76837-277">As with the other DevOps experiences, the Azure platform integrates these tasks directly into the portal.</span><span class="sxs-lookup"><span data-stu-id="76837-277">As with the other DevOps experiences, the Azure platform integrates these tasks directly into the portal.</span></span>

1. <span data-ttu-id="76837-278">To ensure you are keeping the Web App safe from data loss you need to configure backups.</span><span class="sxs-lookup"><span data-stu-id="76837-278">To ensure you are keeping the Web App safe from data loss you need to configure backups.</span></span> <span data-ttu-id="76837-279">Navigate to the Settings area for your Web app.</span><span class="sxs-lookup"><span data-stu-id="76837-279">Navigate to the Settings area for your Web app.</span></span>
   
   ![image56][image56]
2. <span data-ttu-id="76837-281">In the blade on the right, scroll down to the Features category.</span><span class="sxs-lookup"><span data-stu-id="76837-281">In the blade on the right, scroll down to the Features category.</span></span>
   
    ![image57][image57]
3. <span data-ttu-id="76837-283">Choose Backups; a blade opens on the right.</span><span class="sxs-lookup"><span data-stu-id="76837-283">Choose Backups; a blade opens on the right.</span></span>
   
   ![image58][image58]
4. <span data-ttu-id="76837-285">Click Configure, choose a storage account from the blade on the right.</span><span class="sxs-lookup"><span data-stu-id="76837-285">Click Configure, choose a storage account from the blade on the right.</span></span>
   
   ![image59][image59]
5. <span data-ttu-id="76837-287">Now create and choose a storage container to hold your backups.</span><span class="sxs-lookup"><span data-stu-id="76837-287">Now create and choose a storage container to hold your backups.</span></span> <span data-ttu-id="76837-288">Click create at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="76837-288">Click create at the bottom of the blade.</span></span> <span data-ttu-id="76837-289">Then select the container.</span><span class="sxs-lookup"><span data-stu-id="76837-289">Then select the container.</span></span>
   
   ![image60][image60]
6. <span data-ttu-id="76837-291">Once you have chosen the container, you can configure schedules, as well as set up backups for your databases.</span><span class="sxs-lookup"><span data-stu-id="76837-291">Once you have chosen the container, you can configure schedules, as well as set up backups for your databases.</span></span> <span data-ttu-id="76837-292">For this scenario, click the save icon.</span><span class="sxs-lookup"><span data-stu-id="76837-292">For this scenario, click the save icon.</span></span>
   
    ![image61][image61]
7. <span data-ttu-id="76837-294">After saving, scroll back to the blade on the left for Backups.</span><span class="sxs-lookup"><span data-stu-id="76837-294">After saving, scroll back to the blade on the left for Backups.</span></span> <span data-ttu-id="76837-295">Click Backup Now to back the application.</span><span class="sxs-lookup"><span data-stu-id="76837-295">Click Backup Now to back the application.</span></span>
   
    ![image62][image62]
8. <span data-ttu-id="76837-297">In a few moments, you see a backup created.</span><span class="sxs-lookup"><span data-stu-id="76837-297">In a few moments, you see a backup created.</span></span> <span data-ttu-id="76837-298">Notice the Restore Now option on the screen-shot below.</span><span class="sxs-lookup"><span data-stu-id="76837-298">Notice the Restore Now option on the screen-shot below.</span></span>
   
    ![image63][image63]
9. <span data-ttu-id="76837-300">Click on Restore Now and examine the options to the blade on the right.</span><span class="sxs-lookup"><span data-stu-id="76837-300">Click on Restore Now and examine the options to the blade on the right.</span></span> <span data-ttu-id="76837-301">You can choose an appropriate backup and easily restore to an earlier state as necessary.</span><span class="sxs-lookup"><span data-stu-id="76837-301">You can choose an appropriate backup and easily restore to an earlier state as necessary.</span></span> <span data-ttu-id="76837-302">The Azure portal has helped us easily enable a simple disaster recovery strategy for the app.</span><span class="sxs-lookup"><span data-stu-id="76837-302">The Azure portal has helped us easily enable a simple disaster recovery strategy for the app.</span></span>
   
    ![image64][image64]
10. <span data-ttu-id="76837-304">Move back to the Settings blade on the left, and under Features and choose Authentication/Authorization.</span><span class="sxs-lookup"><span data-stu-id="76837-304">Move back to the Settings blade on the left, and under Features and choose Authentication/Authorization.</span></span>
    
     ![image65][image65]
11. <span data-ttu-id="76837-306">In the blade on the right choose App Service Authentication.</span><span class="sxs-lookup"><span data-stu-id="76837-306">In the blade on the right choose App Service Authentication.</span></span> <span data-ttu-id="76837-307">Notice the variety of options you can configure with popular providers.</span><span class="sxs-lookup"><span data-stu-id="76837-307">Notice the variety of options you can configure with popular providers.</span></span>
    
     ![image66][image66]
12. <span data-ttu-id="76837-309">Choose the provider of your choice and notice the options for the scope.</span><span class="sxs-lookup"><span data-stu-id="76837-309">Choose the provider of your choice and notice the options for the scope.</span></span> <span data-ttu-id="76837-310">You can provide an App ID and App Secret and quickly enable Facebook authentication for the app.</span><span class="sxs-lookup"><span data-stu-id="76837-310">You can provide an App ID and App Secret and quickly enable Facebook authentication for the app.</span></span> <span data-ttu-id="76837-311">The Azure portal enables authentication as a turnkey solution for apps.</span><span class="sxs-lookup"><span data-stu-id="76837-311">The Azure portal enables authentication as a turnkey solution for apps.</span></span>
    
     ![image67][image67]
13. <span data-ttu-id="76837-313">Move back to the Settings blade and choose Users under the Resource Management category.</span><span class="sxs-lookup"><span data-stu-id="76837-313">Move back to the Settings blade and choose Users under the Resource Management category.</span></span>
    
     ![image68][image68]
14. <span data-ttu-id="76837-315">In the blade on the right examine the various options for adding roles and users.</span><span class="sxs-lookup"><span data-stu-id="76837-315">In the blade on the right examine the various options for adding roles and users.</span></span> <span data-ttu-id="76837-316">The Azure portal lets you easily control RBAC (Role-based access control) for the application.</span><span class="sxs-lookup"><span data-stu-id="76837-316">The Azure portal lets you easily control RBAC (Role-based access control) for the application.</span></span>
    
     ![image69][image69]

## <a name="summary"></a><span data-ttu-id="76837-318">Summary</span><span class="sxs-lookup"><span data-stu-id="76837-318">Summary</span></span>
<span data-ttu-id="76837-319">This tutorial demonstrated some of the power with the Azure platform by quickly enabling continuous deployment for a web app, performing various development and testing activities, monitoring and troubleshooting a live app, and finally managing key strategies such as disaster recovery, identity, and role-based access control.</span><span class="sxs-lookup"><span data-stu-id="76837-319">This tutorial demonstrated some of the power with the Azure platform by quickly enabling continuous deployment for a web app, performing various development and testing activities, monitoring and troubleshooting a live app, and finally managing key strategies such as disaster recovery, identity, and role-based access control.</span></span> <span data-ttu-id="76837-320">The Azure platform enables an integrated experience for these DevOps workflows, and you can work efficiently by staying in context for the task at hand.</span><span class="sxs-lookup"><span data-stu-id="76837-320">The Azure platform enables an integrated experience for these DevOps workflows, and you can work efficiently by staying in context for the task at hand.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76837-321">Next steps</span><span class="sxs-lookup"><span data-stu-id="76837-321">Next steps</span></span>
* <span data-ttu-id="76837-322">Azure Resource Manager is important for enabling DevOps on the Azure platform.</span><span class="sxs-lookup"><span data-stu-id="76837-322">Azure Resource Manager is important for enabling DevOps on the Azure platform.</span></span>  <span data-ttu-id="76837-323">To learn more visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="76837-323">To learn more visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
* <span data-ttu-id="76837-324">To learn more about Azure App Service deployment visit [Deploy your app to Azure App Service](../app-service/app-service-deploy-local-git.md)</span><span class="sxs-lookup"><span data-stu-id="76837-324">To learn more about Azure App Service deployment visit [Deploy your app to Azure App Service](../app-service/app-service-deploy-local-git.md)</span></span>

[image1]: ./media/tutorial-azureportal-devops/image1.png
[image2]: ./media/tutorial-azureportal-devops/image2.png
[image3]: ./media/tutorial-azureportal-devops/image3.png
[image4]: ./media/tutorial-azureportal-devops/image4.png
[image5]: ./media/tutorial-azureportal-devops/image5.png
[image6]: ./media/tutorial-azureportal-devops/image6.png
[image7]: ./media/tutorial-azureportal-devops/image7.png
[image8]: ./media/tutorial-azureportal-devops/image8.png
[image9]: ./media/tutorial-azureportal-devops/image9.png
[image10]: ./media/tutorial-azureportal-devops/image10.png
[image11]: ./media/tutorial-azureportal-devops/image11.png
[image12]: ./media/tutorial-azureportal-devops/image12.png
[image13]: ./media/tutorial-azureportal-devops/image13.png
[image14]: ./media/tutorial-azureportal-devops/image14.png
[image15]: ./media/tutorial-azureportal-devops/image15.png
[image16]: ./media/tutorial-azureportal-devops/image16.png
[image17]: ./media/tutorial-azureportal-devops/image17.png
[image18]: ./media/tutorial-azureportal-devops/image18.png
[image19]: ./media/tutorial-azureportal-devops/image19.png
[image20]: ./media/tutorial-azureportal-devops/image20.png
[image21]: ./media/tutorial-azureportal-devops/image21.png
[image22]: ./media/tutorial-azureportal-devops/image22.png
[image23]: ./media/tutorial-azureportal-devops/image23.png
[image24]: ./media/tutorial-azureportal-devops/image24.png
[image25]: ./media/tutorial-azureportal-devops/image25.png
[image26]: ./media/tutorial-azureportal-devops/image26.png
[image27]: ./media/tutorial-azureportal-devops/image27.png
[image28]: ./media/tutorial-azureportal-devops/image28.png
[image29]: ./media/tutorial-azureportal-devops/image29.png
[image30]: ./media/tutorial-azureportal-devops/image30.png
[image31]: ./media/tutorial-azureportal-devops/image31.png
[image32]: ./media/tutorial-azureportal-devops/image32.png
[image33]: ./media/tutorial-azureportal-devops/image33.png
[image34]: ./media/tutorial-azureportal-devops/image34.png
[image35]: ./media/tutorial-azureportal-devops/image35.png
[image36]: ./media/tutorial-azureportal-devops/image36.png
[image37]: ./media/tutorial-azureportal-devops/image37.png
[image38]: ./media/tutorial-azureportal-devops/image38.png
[image39]: ./media/tutorial-azureportal-devops/image39.png
[image40]: ./media/tutorial-azureportal-devops/image40.png
[image41]: ./media/tutorial-azureportal-devops/image41.png
[image42]: ./media/tutorial-azureportal-devops/image42.png
[image43]: ./media/tutorial-azureportal-devops/image43.png
[image44]: ./media/tutorial-azureportal-devops/image44.png
[image45]: ./media/tutorial-azureportal-devops/image45.png
[image46]: ./media/tutorial-azureportal-devops/image46.png
[image47]: ./media/tutorial-azureportal-devops/image47.png
[image48]: ./media/tutorial-azureportal-devops/image48.png
[image49]: ./media/tutorial-azureportal-devops/image49.png
[image50]: ./media/tutorial-azureportal-devops/image50.png
[image51]: ./media/tutorial-azureportal-devops/image51.png
[image52]: ./media/tutorial-azureportal-devops/image52.png
[image53]: ./media/tutorial-azureportal-devops/image53.png
[image54]: ./media/tutorial-azureportal-devops/image54.png
[image55]: ./media/tutorial-azureportal-devops/image55.png
[image56]: ./media/tutorial-azureportal-devops/image56.png
[image57]: ./media/tutorial-azureportal-devops/image57.png
[image58]: ./media/tutorial-azureportal-devops/image58.png
[image59]: ./media/tutorial-azureportal-devops/image59.png
[image60]: ./media/tutorial-azureportal-devops/image60.png
[image61]: ./media/tutorial-azureportal-devops/image61.png
[image62]: ./media/tutorial-azureportal-devops/image62.png
[image63]: ./media/tutorial-azureportal-devops/image63.png
[image64]: ./media/tutorial-azureportal-devops/image64.png
[image65]: ./media/tutorial-azureportal-devops/image65.png
[image66]: ./media/tutorial-azureportal-devops/image66.png
[image67]: ./media/tutorial-azureportal-devops/image67.png
[image68]: ./media/tutorial-azureportal-devops/image68.png
[image69]: ./media/tutorial-azureportal-devops/image69.png
