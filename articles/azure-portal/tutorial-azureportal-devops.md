---
title: 'Tutorial:  DevOps with the Azure Portal | Microsoft Docs'
description: Learn the various DevOps workflows in the Azure Portal.
services: azure-portal
documentationcenter: ''
author: mlearned
manager: douge
editor: mlearned
ms.assetid: 4f1c5bc1-c732-4d35-b5df-0fd68e547d38
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2016
ms.author: mlearned
ms.openlocfilehash: 28ab8389da5b2c65523429e1111a0179e1b1e46f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553619"
---
# <a name="tutorial-devops-with-the-azure-portal"></a><span data-ttu-id="93e5c-103">Tutorial: DevOps with the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="93e5c-103">Tutorial: DevOps with the Azure Portal</span></span>
<span data-ttu-id="93e5c-104">The Azure platform is full of flexible DevOps workflows.</span><span class="sxs-lookup"><span data-stu-id="93e5c-104">The Azure platform is full of flexible DevOps workflows.</span></span> <span data-ttu-id="93e5c-105">In this tutorial, you learn how to leverage the capabilities of the Azure Portal to develop, test, deploy, troubleshoot, monitor, and manage running applications.</span><span class="sxs-lookup"><span data-stu-id="93e5c-105">In this tutorial, you learn how to leverage the capabilities of the Azure Portal to develop, test, deploy, troubleshoot, monitor, and manage running applications.</span></span> <span data-ttu-id="93e5c-106">This tutorial focuses on the following:</span><span class="sxs-lookup"><span data-stu-id="93e5c-106">This tutorial focuses on the following:</span></span>

1. <span data-ttu-id="93e5c-107">Creating a web app and enabling continuous deployment</span><span class="sxs-lookup"><span data-stu-id="93e5c-107">Creating a web app and enabling continuous deployment</span></span>
2. <span data-ttu-id="93e5c-108">Develop and test an app</span><span class="sxs-lookup"><span data-stu-id="93e5c-108">Develop and test an app</span></span>
3. <span data-ttu-id="93e5c-109">Monitoring and Troubleshooting an app</span><span class="sxs-lookup"><span data-stu-id="93e5c-109">Monitoring and Troubleshooting an app</span></span>
4. <span data-ttu-id="93e5c-110">General application management tasks</span><span class="sxs-lookup"><span data-stu-id="93e5c-110">General application management tasks</span></span>

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a><span data-ttu-id="93e5c-111">Creating a web app and enabling continuous deployment</span><span class="sxs-lookup"><span data-stu-id="93e5c-111">Creating a web app and enabling continuous deployment</span></span>
<span data-ttu-id="93e5c-112">Create a Web app with [Azure App Service](https://azure.microsoft.com/services/app-service/), which you’ll use in the rest of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="93e5c-112">Create a Web app with [Azure App Service](https://azure.microsoft.com/services/app-service/), which you’ll use in the rest of this tutorial.</span></span> <span data-ttu-id="93e5c-113">You’ll initially enable continuous deployment from your source code repository into our running Azure environment.</span><span class="sxs-lookup"><span data-stu-id="93e5c-113">You’ll initially enable continuous deployment from your source code repository into our running Azure environment.</span></span>

1. <span data-ttu-id="93e5c-114">Sign into the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="93e5c-114">Sign into the Azure Portal</span></span>
2. <span data-ttu-id="93e5c-115">Choose **App Services** &gt; **Add icon** and enter a name, choose your subscription, and create a new resource group to serve as the container for the service.</span><span class="sxs-lookup"><span data-stu-id="93e5c-115">Choose **App Services** &gt; **Add icon** and enter a name, choose your subscription, and create a new resource group to serve as the container for the service.</span></span>
   
   <span data-ttu-id="93e5c-116">Resource groups allow you to manage various aspects of the solution such as billing, deployments and monitoring all as a single group via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="93e5c-116">Resource groups allow you to manage various aspects of the solution such as billing, deployments and monitoring all as a single group via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>
   
   ![image1][image1]
3. <span data-ttu-id="93e5c-118">After a few moments, your app service is created.</span><span class="sxs-lookup"><span data-stu-id="93e5c-118">After a few moments, your app service is created.</span></span> <span data-ttu-id="93e5c-119">Take a few minutes to explore the various menu options for the service in the portal.</span><span class="sxs-lookup"><span data-stu-id="93e5c-119">Take a few minutes to explore the various menu options for the service in the portal.</span></span>
   
   ![image2][image2]    
4. <span data-ttu-id="93e5c-121">Click the URL.</span><span class="sxs-lookup"><span data-stu-id="93e5c-121">Click the URL.</span></span> <span data-ttu-id="93e5c-122">Notice the variety of available choices for tools and repositories.</span><span class="sxs-lookup"><span data-stu-id="93e5c-122">Notice the variety of available choices for tools and repositories.</span></span> <span data-ttu-id="93e5c-123">You can also use the languages and frameworks of your choice including .NET, Java, and Ruby.</span><span class="sxs-lookup"><span data-stu-id="93e5c-123">You can also use the languages and frameworks of your choice including .NET, Java, and Ruby.</span></span>
   
   ![image3][image3]    
5. <span data-ttu-id="93e5c-125">The Azure portal makes continuous deployment an easy process that involves only a few simple steps.</span><span class="sxs-lookup"><span data-stu-id="93e5c-125">The Azure portal makes continuous deployment an easy process that involves only a few simple steps.</span></span> <span data-ttu-id="93e5c-126">In the Azure portal, choose settings from the icon for the app service you just created.</span><span class="sxs-lookup"><span data-stu-id="93e5c-126">In the Azure portal, choose settings from the icon for the app service you just created.</span></span>
   
   ![image4][image4]
   
   <span data-ttu-id="93e5c-128">From the blade that opens on the right, scroll to the publishing section.</span><span class="sxs-lookup"><span data-stu-id="93e5c-128">From the blade that opens on the right, scroll to the publishing section.</span></span>
   
   ![image5][image5]
6. <span data-ttu-id="93e5c-130">Next, configure some settings to enable continuous deployment for the app.</span><span class="sxs-lookup"><span data-stu-id="93e5c-130">Next, configure some settings to enable continuous deployment for the app.</span></span> <span data-ttu-id="93e5c-131">Click Deployment Source and then click Choose Source.</span><span class="sxs-lookup"><span data-stu-id="93e5c-131">Click Deployment Source and then click Choose Source.</span></span> <span data-ttu-id="93e5c-132">Notice the variety of options you have for repository sources.</span><span class="sxs-lookup"><span data-stu-id="93e5c-132">Notice the variety of options you have for repository sources.</span></span>
   
   ![image6][image6]
7. <span data-ttu-id="93e5c-134">For this example choose GitHub.</span><span class="sxs-lookup"><span data-stu-id="93e5c-134">For this example choose GitHub.</span></span> <span data-ttu-id="93e5c-135">Optionally choose the repository of your choice and setup the authorization credentials.</span><span class="sxs-lookup"><span data-stu-id="93e5c-135">Optionally choose the repository of your choice and setup the authorization credentials.</span></span>
   
   ![image7][image7]
8. <span data-ttu-id="93e5c-137">After authorization to your repository, you can then choose a project and branch you wish to deploy.</span><span class="sxs-lookup"><span data-stu-id="93e5c-137">After authorization to your repository, you can then choose a project and branch you wish to deploy.</span></span> <span data-ttu-id="93e5c-138">There are several fictitious sample examples listed below.</span><span class="sxs-lookup"><span data-stu-id="93e5c-138">There are several fictitious sample examples listed below.</span></span>
   
   ![image8][image8]
9. <span data-ttu-id="93e5c-140">Once you choose your project and branch, click ok.</span><span class="sxs-lookup"><span data-stu-id="93e5c-140">Once you choose your project and branch, click ok.</span></span> <span data-ttu-id="93e5c-141">You should start to see notifications of a deployment.</span><span class="sxs-lookup"><span data-stu-id="93e5c-141">You should start to see notifications of a deployment.</span></span>
   
   ![image9][image9]
10. <span data-ttu-id="93e5c-143">Navigate back to GitHub to see the webhook that was created to integrate the source control repo with Azure.</span><span class="sxs-lookup"><span data-stu-id="93e5c-143">Navigate back to GitHub to see the webhook that was created to integrate the source control repo with Azure.</span></span> <span data-ttu-id="93e5c-144">The Azure Portal enables integration with GitHub with only a few simple steps.</span><span class="sxs-lookup"><span data-stu-id="93e5c-144">The Azure Portal enables integration with GitHub with only a few simple steps.</span></span>
    
    ![image10][image10]
11. <span data-ttu-id="93e5c-146">To demonstrate continuous deployment, you quickly add some content to the repository.</span><span class="sxs-lookup"><span data-stu-id="93e5c-146">To demonstrate continuous deployment, you quickly add some content to the repository.</span></span> <span data-ttu-id="93e5c-147">For a simple example, add a sample text file to a GitHub repo.</span><span class="sxs-lookup"><span data-stu-id="93e5c-147">For a simple example, add a sample text file to a GitHub repo.</span></span> <span data-ttu-id="93e5c-148">You are free to use .NET, Ruby, Python, or some other type of application with App Service.</span><span class="sxs-lookup"><span data-stu-id="93e5c-148">You are free to use .NET, Ruby, Python, or some other type of application with App Service.</span></span> <span data-ttu-id="93e5c-149">Feel free to add a text file, ASP.NET MVC, Java, or Ruby application to the repo of your choice.</span><span class="sxs-lookup"><span data-stu-id="93e5c-149">Feel free to add a text file, ASP.NET MVC, Java, or Ruby application to the repo of your choice.</span></span>
    
    ![image11][image11]
12. <span data-ttu-id="93e5c-151">After committing changes to your repository, you see a new deployment initiate in the portal notifications area.</span><span class="sxs-lookup"><span data-stu-id="93e5c-151">After committing changes to your repository, you see a new deployment initiate in the portal notifications area.</span></span> <span data-ttu-id="93e5c-152">Click Sync if you do not quickly see changes after committing to your repository.</span><span class="sxs-lookup"><span data-stu-id="93e5c-152">Click Sync if you do not quickly see changes after committing to your repository.</span></span>
    
    ![image12][image12]
13. <span data-ttu-id="93e5c-154">At this point, if you try and load the page for the app service, you may receive a 403 error.</span><span class="sxs-lookup"><span data-stu-id="93e5c-154">At this point, if you try and load the page for the app service, you may receive a 403 error.</span></span> <span data-ttu-id="93e5c-155">In this example, it is because there is no typical default document setup for the page such as a file like index.htm or default.html.</span><span class="sxs-lookup"><span data-stu-id="93e5c-155">In this example, it is because there is no typical default document setup for the page such as a file like index.htm or default.html.</span></span> <span data-ttu-id="93e5c-156">You can quickly remedy this with the tooling in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="93e5c-156">You can quickly remedy this with the tooling in the Azure Portal.</span></span>  <span data-ttu-id="93e5c-157">In the Azure Portal choose Settings &gt; Application Settings.</span><span class="sxs-lookup"><span data-stu-id="93e5c-157">In the Azure Portal choose Settings &gt; Application Settings.</span></span>
    
     ![image13][image13]
14. <span data-ttu-id="93e5c-159">A blade opens for application settings.</span><span class="sxs-lookup"><span data-stu-id="93e5c-159">A blade opens for application settings.</span></span> <span data-ttu-id="93e5c-160">Enter the name of the page “SamplePage.html” and click Save.</span><span class="sxs-lookup"><span data-stu-id="93e5c-160">Enter the name of the page “SamplePage.html” and click Save.</span></span> <span data-ttu-id="93e5c-161">Take a few minutes to explore the other settings.</span><span class="sxs-lookup"><span data-stu-id="93e5c-161">Take a few minutes to explore the other settings.</span></span>
    
    ![image14][image14]
15. <span data-ttu-id="93e5c-163">Optionally refresh your browser URL to ensure you see the expected changes.</span><span class="sxs-lookup"><span data-stu-id="93e5c-163">Optionally refresh your browser URL to ensure you see the expected changes.</span></span> <span data-ttu-id="93e5c-164">In this case, there is some simple text now populating the page.</span><span class="sxs-lookup"><span data-stu-id="93e5c-164">In this case, there is some simple text now populating the page.</span></span> <span data-ttu-id="93e5c-165">Each additional change to the repository would result in a new automatic deployment.</span><span class="sxs-lookup"><span data-stu-id="93e5c-165">Each additional change to the repository would result in a new automatic deployment.</span></span>
    
    ![image15][image15]
    
    <span data-ttu-id="93e5c-167">Enabling continuous deployment with the Azure Portal is an easy experience.</span><span class="sxs-lookup"><span data-stu-id="93e5c-167">Enabling continuous deployment with the Azure Portal is an easy experience.</span></span> <span data-ttu-id="93e5c-168">You can also build more complex release pipelines and use many other techniques with existing source control and continuous integration systems to deploy to Azure, such as leveraging automated build and release management systems.</span><span class="sxs-lookup"><span data-stu-id="93e5c-168">You can also build more complex release pipelines and use many other techniques with existing source control and continuous integration systems to deploy to Azure, such as leveraging automated build and release management systems.</span></span>

## <a name="develop-and-test-an-app"></a><span data-ttu-id="93e5c-169">Develop and test an app</span><span class="sxs-lookup"><span data-stu-id="93e5c-169">Develop and test an app</span></span>
<span data-ttu-id="93e5c-170">Next, make some changes to the code base and rapidly deploy those changes.</span><span class="sxs-lookup"><span data-stu-id="93e5c-170">Next, make some changes to the code base and rapidly deploy those changes.</span></span> <span data-ttu-id="93e5c-171">You will also setup up some performance testing for the Web app.</span><span class="sxs-lookup"><span data-stu-id="93e5c-171">You will also setup up some performance testing for the Web app.</span></span>

1. <span data-ttu-id="93e5c-172">In the Azure Portal choose App Services from the navigation pane, and locate your App Service.</span><span class="sxs-lookup"><span data-stu-id="93e5c-172">In the Azure Portal choose App Services from the navigation pane, and locate your App Service.</span></span>
   
   ![image16][image16]
2. <span data-ttu-id="93e5c-174">Click Tools</span><span class="sxs-lookup"><span data-stu-id="93e5c-174">Click Tools</span></span>
   
   ![image17][image17]
3. <span data-ttu-id="93e5c-176">Notice the develop category under Tools.</span><span class="sxs-lookup"><span data-stu-id="93e5c-176">Notice the develop category under Tools.</span></span> <span data-ttu-id="93e5c-177">There are several useful tools here that allow us to work with apps without leaving the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="93e5c-177">There are several useful tools here that allow us to work with apps without leaving the Azure Portal.</span></span> <span data-ttu-id="93e5c-178">Click on Console.</span><span class="sxs-lookup"><span data-stu-id="93e5c-178">Click on Console.</span></span>
   
   ![image18][image18]
4. <span data-ttu-id="93e5c-180">In the console window, you can issue live commands for your app.</span><span class="sxs-lookup"><span data-stu-id="93e5c-180">In the console window, you can issue live commands for your app.</span></span> <span data-ttu-id="93e5c-181">Type the dir command and hit enter.</span><span class="sxs-lookup"><span data-stu-id="93e5c-181">Type the dir command and hit enter.</span></span> <span data-ttu-id="93e5c-182">Note that commands requiring elevated privileges do not work.</span><span class="sxs-lookup"><span data-stu-id="93e5c-182">Note that commands requiring elevated privileges do not work.</span></span>
   
   ![image19][image19]
5. <span data-ttu-id="93e5c-184">Move back to the Develop category and choose Visual Studio Online.</span><span class="sxs-lookup"><span data-stu-id="93e5c-184">Move back to the Develop category and choose Visual Studio Online.</span></span> <span data-ttu-id="93e5c-185">Note: Visual Studio Online is now named Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="93e5c-185">Note: Visual Studio Online is now named Visual Studio Team Services.</span></span>
   
   ![image20][image20]
6. <span data-ttu-id="93e5c-187">Toggle on the in-browser editing experience for your App.</span><span class="sxs-lookup"><span data-stu-id="93e5c-187">Toggle on the in-browser editing experience for your App.</span></span>
   
   ![image21][image21]
7. <span data-ttu-id="93e5c-189">A web extension installs for your app.</span><span class="sxs-lookup"><span data-stu-id="93e5c-189">A web extension installs for your app.</span></span> <span data-ttu-id="93e5c-190">Extensions quickly and easily add functionality to apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="93e5c-190">Extensions quickly and easily add functionality to apps in Azure.</span></span> <span data-ttu-id="93e5c-191">Notice some of the other extension types available in the screenshot below.</span><span class="sxs-lookup"><span data-stu-id="93e5c-191">Notice some of the other extension types available in the screenshot below.</span></span>
   
   ![image22][image22]
8. <span data-ttu-id="93e5c-193">Once the Visual Studio Online extension installs, click Go.</span><span class="sxs-lookup"><span data-stu-id="93e5c-193">Once the Visual Studio Online extension installs, click Go.</span></span>
   
   ![image23][image23]
9. <span data-ttu-id="93e5c-195">A browser tab opens where you see a development IDE directly in the browser.</span><span class="sxs-lookup"><span data-stu-id="93e5c-195">A browser tab opens where you see a development IDE directly in the browser.</span></span> <span data-ttu-id="93e5c-196">Notice the experience below is in Chrome.</span><span class="sxs-lookup"><span data-stu-id="93e5c-196">Notice the experience below is in Chrome.</span></span>
   
   ![image24][image24]
10. <span data-ttu-id="93e5c-198">You can perform several activities such as edit files, add files and folders, and download content from the live site.</span><span class="sxs-lookup"><span data-stu-id="93e5c-198">You can perform several activities such as edit files, add files and folders, and download content from the live site.</span></span> <span data-ttu-id="93e5c-199">Make a quick edit to the SamplePage.html file.</span><span class="sxs-lookup"><span data-stu-id="93e5c-199">Make a quick edit to the SamplePage.html file.</span></span>
    
    ![image25][image25]
11. <span data-ttu-id="93e5c-201">In a few moments, the changes are automatically saved.</span><span class="sxs-lookup"><span data-stu-id="93e5c-201">In a few moments, the changes are automatically saved.</span></span> <span data-ttu-id="93e5c-202">If you navigate back to the page, you can see the changes.</span><span class="sxs-lookup"><span data-stu-id="93e5c-202">If you navigate back to the page, you can see the changes.</span></span> <span data-ttu-id="93e5c-203">Keep in mind live edits like these are most likely not suitable for production environments.</span><span class="sxs-lookup"><span data-stu-id="93e5c-203">Keep in mind live edits like these are most likely not suitable for production environments.</span></span> <span data-ttu-id="93e5c-204">However, the tools make it very easy to make quick changes for dev and test environments.</span><span class="sxs-lookup"><span data-stu-id="93e5c-204">However, the tools make it very easy to make quick changes for dev and test environments.</span></span>
    
    ![image26][image26]
    
    ![image27][image27]
12. <span data-ttu-id="93e5c-207">Move back to the tools blade and under the Develop category, click on Performance Test.</span><span class="sxs-lookup"><span data-stu-id="93e5c-207">Move back to the tools blade and under the Develop category, click on Performance Test.</span></span>
    
    ![image28][image28]
13. <span data-ttu-id="93e5c-209">You need to set a team services account.</span><span class="sxs-lookup"><span data-stu-id="93e5c-209">You need to set a team services account.</span></span> <span data-ttu-id="93e5c-210">See here for more details: [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span><span class="sxs-lookup"><span data-stu-id="93e5c-210">See here for more details: [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span></span>
14. <span data-ttu-id="93e5c-211">Click on New to create a performance test.</span><span class="sxs-lookup"><span data-stu-id="93e5c-211">Click on New to create a performance test.</span></span>
    
    ![image29][image29]
    
    <span data-ttu-id="93e5c-213">Configure the various values and click Run Test at the bottom of the dialogue to initiate a performance test.</span><span class="sxs-lookup"><span data-stu-id="93e5c-213">Configure the various values and click Run Test at the bottom of the dialogue to initiate a performance test.</span></span>
    
    ![image30][image30]
    
    ![image31][image31]
15. <span data-ttu-id="93e5c-216">Once the test starts running, you can monitor the state.</span><span class="sxs-lookup"><span data-stu-id="93e5c-216">Once the test starts running, you can monitor the state.</span></span>
    
    ![image32][image32]
    
    <span data-ttu-id="93e5c-218">Once the test finishes, clicking on the result shows more details.</span><span class="sxs-lookup"><span data-stu-id="93e5c-218">Once the test finishes, clicking on the result shows more details.</span></span>
    
    ![image33][image33]
16. <span data-ttu-id="93e5c-220">In this example, you created a small test run, so there is limited data to analyze, but you can see various metrics as well as rerun your test from this view.</span><span class="sxs-lookup"><span data-stu-id="93e5c-220">In this example, you created a small test run, so there is limited data to analyze, but you can see various metrics as well as rerun your test from this view.</span></span> <span data-ttu-id="93e5c-221">The Azure Portal makes creating, executing, and analyzing web performance tests an easy process.</span><span class="sxs-lookup"><span data-stu-id="93e5c-221">The Azure Portal makes creating, executing, and analyzing web performance tests an easy process.</span></span> <span data-ttu-id="93e5c-222">The screenshots below display the performance data.</span><span class="sxs-lookup"><span data-stu-id="93e5c-222">The screenshots below display the performance data.</span></span>
    
    ![image34][image34]
    
    ![image35][image35]
    
    ![image36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a><span data-ttu-id="93e5c-226">Monitoring and troubleshooting an app</span><span class="sxs-lookup"><span data-stu-id="93e5c-226">Monitoring and troubleshooting an app</span></span>
<span data-ttu-id="93e5c-227">Azure provides many capabilities for monitoring and troubleshooting running applications.</span><span class="sxs-lookup"><span data-stu-id="93e5c-227">Azure provides many capabilities for monitoring and troubleshooting running applications.</span></span>

1. <span data-ttu-id="93e5c-228">In the Azure Portal for our Web app choose Tools.</span><span class="sxs-lookup"><span data-stu-id="93e5c-228">In the Azure Portal for our Web app choose Tools.</span></span>
   
   ![image37][image37]
2. <span data-ttu-id="93e5c-230">Under the Troubleshoot category, notice the various choices for using tools to troubleshoot potential issues with a running app.</span><span class="sxs-lookup"><span data-stu-id="93e5c-230">Under the Troubleshoot category, notice the various choices for using tools to troubleshoot potential issues with a running app.</span></span> <span data-ttu-id="93e5c-231">You can do things like monitor Live HTTP traffic, enable self-healing, view logs, and more.</span><span class="sxs-lookup"><span data-stu-id="93e5c-231">You can do things like monitor Live HTTP traffic, enable self-healing, view logs, and more.</span></span>
   
   ![image38][image38]
3. <span data-ttu-id="93e5c-233">Choose Site Metrics to quickly get a view of some HTTP codes.</span><span class="sxs-lookup"><span data-stu-id="93e5c-233">Choose Site Metrics to quickly get a view of some HTTP codes.</span></span>
   
   ![image39][image39]
4. <span data-ttu-id="93e5c-235">Choose Diagnostics as a Service.</span><span class="sxs-lookup"><span data-stu-id="93e5c-235">Choose Diagnostics as a Service.</span></span> <span data-ttu-id="93e5c-236">Choose your application type, then choose Run.</span><span class="sxs-lookup"><span data-stu-id="93e5c-236">Choose your application type, then choose Run.</span></span>
   
   ![image40][image40]
   
   <span data-ttu-id="93e5c-238">A collection begins.</span><span class="sxs-lookup"><span data-stu-id="93e5c-238">A collection begins.</span></span>
   
   ![image41][image41]
5. <span data-ttu-id="93e5c-240">You may choose the appropriate log to diagnose potential issues.</span><span class="sxs-lookup"><span data-stu-id="93e5c-240">You may choose the appropriate log to diagnose potential issues.</span></span> <span data-ttu-id="93e5c-241">You need to enable logging to see all of the available data options such as HTTP Logs.</span><span class="sxs-lookup"><span data-stu-id="93e5c-241">You need to enable logging to see all of the available data options such as HTTP Logs.</span></span>
   
   ![image42][image42]
   
   <span data-ttu-id="93e5c-243">By clicking on the Memory Dump file you can download and analyze a DebugDiag analysis report to help find potential issues.</span><span class="sxs-lookup"><span data-stu-id="93e5c-243">By clicking on the Memory Dump file you can download and analyze a DebugDiag analysis report to help find potential issues.</span></span>
   
   ![image43][image43]
6. <span data-ttu-id="93e5c-245">To view more data, you need to enable additional logging.</span><span class="sxs-lookup"><span data-stu-id="93e5c-245">To view more data, you need to enable additional logging.</span></span> <span data-ttu-id="93e5c-246">In the Azure Portal, navigate to the Web app and choose Settings.</span><span class="sxs-lookup"><span data-stu-id="93e5c-246">In the Azure Portal, navigate to the Web app and choose Settings.</span></span>
   
   ![image44][image44]
7. <span data-ttu-id="93e5c-248">Scroll down to the features category, and choose Diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="93e5c-248">Scroll down to the features category, and choose Diagnostic logs.</span></span>
   
      ![image45][image45]
8. <span data-ttu-id="93e5c-250">Notice the various options for logging.</span><span class="sxs-lookup"><span data-stu-id="93e5c-250">Notice the various options for logging.</span></span> <span data-ttu-id="93e5c-251">Toggle on Web server logging and click save.</span><span class="sxs-lookup"><span data-stu-id="93e5c-251">Toggle on Web server logging and click save.</span></span>
   
   ![image46][image46]
9. <span data-ttu-id="93e5c-253">Move back to the tools area for the app and choose Diagnostics as a service and click Run to rerun the data collection.</span><span class="sxs-lookup"><span data-stu-id="93e5c-253">Move back to the tools area for the app and choose Diagnostics as a service and click Run to rerun the data collection.</span></span>
   
   ![image47][image47]
10. <span data-ttu-id="93e5c-255">With the HTTP logging setting enabled, you now see data collected for HTTP Logs.</span><span class="sxs-lookup"><span data-stu-id="93e5c-255">With the HTTP logging setting enabled, you now see data collected for HTTP Logs.</span></span>
    
    ![image48][image48]
11. <span data-ttu-id="93e5c-257">By clicking the HTML file log, you produce a rich browser-based report for further investigation.</span><span class="sxs-lookup"><span data-stu-id="93e5c-257">By clicking the HTML file log, you produce a rich browser-based report for further investigation.</span></span>
    
    ![image49][image49]
12. <span data-ttu-id="93e5c-259">Move back to the tools section in the Azure Portal for the app.</span><span class="sxs-lookup"><span data-stu-id="93e5c-259">Move back to the tools section in the Azure Portal for the app.</span></span> <span data-ttu-id="93e5c-260">Scroll to the Tools section and choose Process Explorer.</span><span class="sxs-lookup"><span data-stu-id="93e5c-260">Scroll to the Tools section and choose Process Explorer.</span></span>
    
    ![image50][image50]
13. <span data-ttu-id="93e5c-262">By choosing Process Explorer, you can view details about running processes.</span><span class="sxs-lookup"><span data-stu-id="93e5c-262">By choosing Process Explorer, you can view details about running processes.</span></span> <span data-ttu-id="93e5c-263">Notice below you can drill into processes and even kill processes all from the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="93e5c-263">Notice below you can drill into processes and even kill processes all from the Azure Portal.</span></span>
    
    ![image51][image51]
    
    ![image52][image52]
14. <span data-ttu-id="93e5c-266">Move back to the Settings blade on the left.</span><span class="sxs-lookup"><span data-stu-id="93e5c-266">Move back to the Settings blade on the left.</span></span> <span data-ttu-id="93e5c-267">Click New support request.</span><span class="sxs-lookup"><span data-stu-id="93e5c-267">Click New support request.</span></span>
    
    ![image53][image53]
15. <span data-ttu-id="93e5c-269">From the blade on the right, you can fill out details about the issues, enter contact information, and even upload diagnostic data.</span><span class="sxs-lookup"><span data-stu-id="93e5c-269">From the blade on the right, you can fill out details about the issues, enter contact information, and even upload diagnostic data.</span></span> <span data-ttu-id="93e5c-270">The Azure Portal enables working with Microsoft support a seamless experience.</span><span class="sxs-lookup"><span data-stu-id="93e5c-270">The Azure Portal enables working with Microsoft support a seamless experience.</span></span>
    
    ![image54][image54]
    
    ![image55][image55]
    
    <span data-ttu-id="93e5c-273">The Azure Portal helps provide powerful and familiar tooling experiences to help monitor and troubleshoot our running applications.</span><span class="sxs-lookup"><span data-stu-id="93e5c-273">The Azure Portal helps provide powerful and familiar tooling experiences to help monitor and troubleshoot our running applications.</span></span> <span data-ttu-id="93e5c-274">You are also able to take action quickly by performing tasks such as recycling processes, enabling and disabling various data collections, and even integrating with Microsoft professional support.</span><span class="sxs-lookup"><span data-stu-id="93e5c-274">You are also able to take action quickly by performing tasks such as recycling processes, enabling and disabling various data collections, and even integrating with Microsoft professional support.</span></span>

## <a name="general-application-management"></a><span data-ttu-id="93e5c-275">General Application Management</span><span class="sxs-lookup"><span data-stu-id="93e5c-275">General Application Management</span></span>
<span data-ttu-id="93e5c-276">When managing applications, you often need to perform a broad variety of activities such as configuring backup strategies, implementing and managing identity providers, and configuring Role-based access control.</span><span class="sxs-lookup"><span data-stu-id="93e5c-276">When managing applications, you often need to perform a broad variety of activities such as configuring backup strategies, implementing and managing identity providers, and configuring Role-based access control.</span></span> <span data-ttu-id="93e5c-277">As with the other DevOps experiences, the Azure platform integrates these tasks directly into the portal.</span><span class="sxs-lookup"><span data-stu-id="93e5c-277">As with the other DevOps experiences, the Azure platform integrates these tasks directly into the portal.</span></span>

1. <span data-ttu-id="93e5c-278">To ensure you are keeping the Web App safe from data loss you need to configure backups.</span><span class="sxs-lookup"><span data-stu-id="93e5c-278">To ensure you are keeping the Web App safe from data loss you need to configure backups.</span></span> <span data-ttu-id="93e5c-279">Navigate to the Settings area for your Web app.</span><span class="sxs-lookup"><span data-stu-id="93e5c-279">Navigate to the Settings area for your Web app.</span></span>
   
   ![image56][image56]
2. <span data-ttu-id="93e5c-281">In the blade on the right, scroll down to the Features category.</span><span class="sxs-lookup"><span data-stu-id="93e5c-281">In the blade on the right, scroll down to the Features category.</span></span>
   
    ![image57][image57]
3. <span data-ttu-id="93e5c-283">Choose Backups; a blade opens on the right.</span><span class="sxs-lookup"><span data-stu-id="93e5c-283">Choose Backups; a blade opens on the right.</span></span>
   
   ![image58][image58]
4. <span data-ttu-id="93e5c-285">Click Configure, choose a storage account from the blade on the right.</span><span class="sxs-lookup"><span data-stu-id="93e5c-285">Click Configure, choose a storage account from the blade on the right.</span></span>
   
   ![image59][image59]
5. <span data-ttu-id="93e5c-287">Now create and choose a storage container to hold your backups.</span><span class="sxs-lookup"><span data-stu-id="93e5c-287">Now create and choose a storage container to hold your backups.</span></span> <span data-ttu-id="93e5c-288">Click create at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="93e5c-288">Click create at the bottom of the blade.</span></span> <span data-ttu-id="93e5c-289">Then select the container.</span><span class="sxs-lookup"><span data-stu-id="93e5c-289">Then select the container.</span></span>
   
   ![image60][image60]
6. <span data-ttu-id="93e5c-291">Once you have chosen the container, you can configure schedules, as well as setup backups for your databases.</span><span class="sxs-lookup"><span data-stu-id="93e5c-291">Once you have chosen the container, you can configure schedules, as well as setup backups for your databases.</span></span> <span data-ttu-id="93e5c-292">For this scenario, click the save icon.</span><span class="sxs-lookup"><span data-stu-id="93e5c-292">For this scenario, click the save icon.</span></span>
   
    ![image61][image61]
7. <span data-ttu-id="93e5c-294">After saving, scroll back to the blade on the left for Backups.</span><span class="sxs-lookup"><span data-stu-id="93e5c-294">After saving, scroll back to the blade on the left for Backups.</span></span> <span data-ttu-id="93e5c-295">Click Backup Now to back the application.</span><span class="sxs-lookup"><span data-stu-id="93e5c-295">Click Backup Now to back the application.</span></span>
   
    ![image62][image62]
8. <span data-ttu-id="93e5c-297">In a few moments, you see a backup created.</span><span class="sxs-lookup"><span data-stu-id="93e5c-297">In a few moments, you see a backup created.</span></span> <span data-ttu-id="93e5c-298">Notice the Restore Now option on the screen-shot below.</span><span class="sxs-lookup"><span data-stu-id="93e5c-298">Notice the Restore Now option on the screen-shot below.</span></span>
   
    ![image63][image63]
9. <span data-ttu-id="93e5c-300">Click on Restore Now and examine the options to the blade on the right.</span><span class="sxs-lookup"><span data-stu-id="93e5c-300">Click on Restore Now and examine the options to the blade on the right.</span></span> <span data-ttu-id="93e5c-301">You can choose an appropriate backup and easily restore to an earlier state as necessary.</span><span class="sxs-lookup"><span data-stu-id="93e5c-301">You can choose an appropriate backup and easily restore to an earlier state as necessary.</span></span> <span data-ttu-id="93e5c-302">The Azure portal has helped us easily enable a simple disaster recovery strategy for the app.</span><span class="sxs-lookup"><span data-stu-id="93e5c-302">The Azure portal has helped us easily enable a simple disaster recovery strategy for the app.</span></span>
   
    ![image64][image64]
10. <span data-ttu-id="93e5c-304">Move back to the Settings blade on the left, and under Features and choose Authentication/Authorization.</span><span class="sxs-lookup"><span data-stu-id="93e5c-304">Move back to the Settings blade on the left, and under Features and choose Authentication/Authorization.</span></span>
    
     ![image65][image65]
11. <span data-ttu-id="93e5c-306">In the blade on the right choose App Service Authentication.</span><span class="sxs-lookup"><span data-stu-id="93e5c-306">In the blade on the right choose App Service Authentication.</span></span> <span data-ttu-id="93e5c-307">Notice the variety of options you can configure with popular providers.</span><span class="sxs-lookup"><span data-stu-id="93e5c-307">Notice the variety of options you can configure with popular providers.</span></span>
    
     ![image66][image66]
12. <span data-ttu-id="93e5c-309">Choose the provider of your choice and notice the options for the scope.</span><span class="sxs-lookup"><span data-stu-id="93e5c-309">Choose the provider of your choice and notice the options for the scope.</span></span> <span data-ttu-id="93e5c-310">You can provide an App ID and App Secret and quickly enable Facebook authentication for the app.</span><span class="sxs-lookup"><span data-stu-id="93e5c-310">You can provide an App ID and App Secret and quickly enable Facebook authentication for the app.</span></span> <span data-ttu-id="93e5c-311">The Azure Portal enables authentication as a turnkey solution for apps.</span><span class="sxs-lookup"><span data-stu-id="93e5c-311">The Azure Portal enables authentication as a turnkey solution for apps.</span></span>
    
     ![image67][image67]
13. <span data-ttu-id="93e5c-313">Move back to the Settings blade and choose Users under the Resource Management category.</span><span class="sxs-lookup"><span data-stu-id="93e5c-313">Move back to the Settings blade and choose Users under the Resource Management category.</span></span>
    
     ![image68][image68]
14. <span data-ttu-id="93e5c-315">In the blade on the right examine the various options for adding roles and users.</span><span class="sxs-lookup"><span data-stu-id="93e5c-315">In the blade on the right examine the various options for adding roles and users.</span></span> <span data-ttu-id="93e5c-316">The Azure Portal lets you easily control RBAC (Role-based access control) for the application.</span><span class="sxs-lookup"><span data-stu-id="93e5c-316">The Azure Portal lets you easily control RBAC (Role-based access control) for the application.</span></span>
    
     ![image69][image69]

## <a name="summary"></a><span data-ttu-id="93e5c-318">Summary</span><span class="sxs-lookup"><span data-stu-id="93e5c-318">Summary</span></span>
<span data-ttu-id="93e5c-319">This tutorial demonstrated some of the power with the Azure platform by quickly enabling continuous deployment for a web app, performing various development and testing activities, monitoring and troubleshooting a live app, and finally managing key strategies such as disaster recovery, identity, and role-based access control.</span><span class="sxs-lookup"><span data-stu-id="93e5c-319">This tutorial demonstrated some of the power with the Azure platform by quickly enabling continuous deployment for a web app, performing various development and testing activities, monitoring and troubleshooting a live app, and finally managing key strategies such as disaster recovery, identity, and role-based access control.</span></span> <span data-ttu-id="93e5c-320">The Azure platform enables an integrated experience for these DevOps workflows, and you can work efficiently by staying in context for the task at hand.</span><span class="sxs-lookup"><span data-stu-id="93e5c-320">The Azure platform enables an integrated experience for these DevOps workflows, and you can work efficiently by staying in context for the task at hand.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93e5c-321">Next steps</span><span class="sxs-lookup"><span data-stu-id="93e5c-321">Next steps</span></span>
* <span data-ttu-id="93e5c-322">Azure Resource Manager is important for enabling DevOps on the Azure platform.</span><span class="sxs-lookup"><span data-stu-id="93e5c-322">Azure Resource Manager is important for enabling DevOps on the Azure platform.</span></span>  <span data-ttu-id="93e5c-323">To learn more visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="93e5c-323">To learn more visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
* <span data-ttu-id="93e5c-324">To learn more about Azure App Service deployment visit [Deploy your app to Azure App Service](../app-service-web/web-sites-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="93e5c-324">To learn more about Azure App Service deployment visit [Deploy your app to Azure App Service](../app-service-web/web-sites-deploy.md)</span></span>

[image1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image1.png
[image2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image2.png
[image3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image3.png
[image4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image4.png
[image5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image5.png
[image6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image6.png
[image7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image7.png
[image8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image8.png
[image9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image9.png
[image10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image10.png
[image11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image11.png
[image12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image12.png
[image13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image13.png
[image14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image14.png
[image15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image15.png
[image16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image16.png
[image17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image17.png
[image18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image18.png
[image19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image19.png
[image20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image20.png
[image21]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image21.png
[image22]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image22.png
[image23]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image23.png
[image24]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image24.png
[image25]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image25.png
[image26]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image26.png
[image27]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image27.png
[image28]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image28.png
[image29]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image29.png
[image30]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image30.png
[image31]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image31.png
[image32]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image32.png
[image33]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image33.png
[image34]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image34.png
[image35]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image35.png
[image36]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image36.png
[image37]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image37.png
[image38]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image38.png
[image39]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image39.png
[image40]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image40.png
[image41]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image41.png
[image42]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image42.png
[image43]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image43.png
[image44]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image44.png
[image45]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image45.png
[image46]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image46.png
[image47]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image47.png
[image48]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image48.png
[image49]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image49.png
[image50]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image50.png
[image51]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image51.png
[image52]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image52.png
[image53]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image53.png
[image54]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image54.png
[image55]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image55.png
[image56]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image56.png
[image57]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image57.png
[image58]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image58.png
[image59]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image59.png
[image60]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image60.png
[image61]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image61.png
[image62]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image62.png
[image63]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image63.png
[image64]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image64.png
[image65]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image65.png
[image66]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image66.png
[image67]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image67.png
[image68]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image68.png
[image69]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-portal/media/tutorial-azureportal-devops/image69.png





































































