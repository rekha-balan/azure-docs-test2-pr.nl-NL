---
title: Create a CI/CD pipeline for Ruby on Rails with the Azure DevOps Project  | Quickstart
description: The DevOps Project makes it easy to get started on Azure. It helps you launch a Ruby web app on an Azure service in a few quick steps.
ms.prod: devops
ms.technology: devops-cicd
services: vsts
documentationcenter: vs-devops-build
author: mlearned
manager: douge
editor: ''
ms.assetid: ''
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 07/09/2018
ms.author: mlearned
ms.custom: mvc
monikerRange: vsts
ms.openlocfilehash: cc4fc36bb865a0f95c6f6d7e7c3b2282a4da9f39
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855901"
---
# <a name="create-a-cicd-pipeline-for-ruby-on-rails-with-the-azure-devops-project"></a><span data-ttu-id="0a44c-104">Create a CI/CD pipeline for Ruby on Rails with the Azure DevOps Project</span><span class="sxs-lookup"><span data-stu-id="0a44c-104">Create a CI/CD pipeline for Ruby on Rails with the Azure DevOps Project</span></span>

<span data-ttu-id="0a44c-105">Configure continuous integration (CI) and continuous delivery (CD) for your Ruby on Rails application with The **Azure DevOps Project**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-105">Configure continuous integration (CI) and continuous delivery (CD) for your Ruby on Rails application with The **Azure DevOps Project**.</span></span>  <span data-ttu-id="0a44c-106">The Azure DevOps Project simplifies the initial configuration of an Azure DevOps Services build and release pipeline.</span><span class="sxs-lookup"><span data-stu-id="0a44c-106">The Azure DevOps Project simplifies the initial configuration of an Azure DevOps Services build and release pipeline.</span></span>

<span data-ttu-id="0a44c-107">If you don't have an Azure subscription, you can get one free through [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/).</span><span class="sxs-lookup"><span data-stu-id="0a44c-107">If you don't have an Azure subscription, you can get one free through [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/).</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="0a44c-108">Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="0a44c-108">Sign in to the Azure portal</span></span>

<span data-ttu-id="0a44c-109">The Azure DevOps Project creates a CI/CD pipeline in Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="0a44c-109">The Azure DevOps Project creates a CI/CD pipeline in Azure DevOps Services.</span></span>  <span data-ttu-id="0a44c-110">You can create a **new Azure DevOps Services** organization or use an **existing organization**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-110">You can create a **new Azure DevOps Services** organization or use an **existing organization**.</span></span>  <span data-ttu-id="0a44c-111">The Azure DevOps Project also creates **Azure resources** in the **Azure subscription** of your choice.</span><span class="sxs-lookup"><span data-stu-id="0a44c-111">The Azure DevOps Project also creates **Azure resources** in the **Azure subscription** of your choice.</span></span>

1. <span data-ttu-id="0a44c-112">Sign into the [Microsoft Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0a44c-112">Sign into the [Microsoft Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="0a44c-113">Choose the **Create a resource** icon in the left navigation bar, then search for **DevOps Project**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-113">Choose the **Create a resource** icon in the left navigation bar, then search for **DevOps Project**.</span></span>  <span data-ttu-id="0a44c-114">Choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-114">Choose **Create**.</span></span>

    ![Starting Continuous Delivery](_img/azure-devops-project-ruby/fullbrowser.png)

## <a name="select-a-sample-application-and-azure-service"></a><span data-ttu-id="0a44c-116">Select a sample application and Azure service</span><span class="sxs-lookup"><span data-stu-id="0a44c-116">Select a sample application and Azure service</span></span>

1. <span data-ttu-id="0a44c-117">Select the **Ruby** sample application.</span><span class="sxs-lookup"><span data-stu-id="0a44c-117">Select the **Ruby** sample application.</span></span>

1. <span data-ttu-id="0a44c-118">Select the **Ruby on Rails** application framework.</span><span class="sxs-lookup"><span data-stu-id="0a44c-118">Select the **Ruby on Rails** application framework.</span></span>  <span data-ttu-id="0a44c-119">When you're done, choose **Next**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-119">When you're done, choose **Next**.</span></span>

1. <span data-ttu-id="0a44c-120">**Web App on Linux** is the default deployment target.</span><span class="sxs-lookup"><span data-stu-id="0a44c-120">**Web App on Linux** is the default deployment target.</span></span>  <span data-ttu-id="0a44c-121">Optionally, you can choose Web App for Containers.</span><span class="sxs-lookup"><span data-stu-id="0a44c-121">Optionally, you can choose Web App for Containers.</span></span>  <span data-ttu-id="0a44c-122">The application framework, which you chose on the previous steps, dictates the type of Azure service deployment target available here.</span><span class="sxs-lookup"><span data-stu-id="0a44c-122">The application framework, which you chose on the previous steps, dictates the type of Azure service deployment target available here.</span></span>  <span data-ttu-id="0a44c-123">Select the **target service** of your choice.</span><span class="sxs-lookup"><span data-stu-id="0a44c-123">Select the **target service** of your choice.</span></span>  <span data-ttu-id="0a44c-124">When you're done, choose **Next**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-124">When you're done, choose **Next**.</span></span>

## <a name="configure-azure-devops-services-and-an-azure-subscription"></a><span data-ttu-id="0a44c-125">Configure Azure DevOps Services and an Azure subscription</span><span class="sxs-lookup"><span data-stu-id="0a44c-125">Configure Azure DevOps Services and an Azure subscription</span></span> 

1. <span data-ttu-id="0a44c-126">Create a **new** free Azure DevOps Services organization or choose an **existing** organization.</span><span class="sxs-lookup"><span data-stu-id="0a44c-126">Create a **new** free Azure DevOps Services organization or choose an **existing** organization.</span></span>  <span data-ttu-id="0a44c-127">Choose a **name** for your Azure DevOps project.</span><span class="sxs-lookup"><span data-stu-id="0a44c-127">Choose a **name** for your Azure DevOps project.</span></span>  <span data-ttu-id="0a44c-128">Select your **Azure subscription**, **location**, and choose a **name** for your application.</span><span class="sxs-lookup"><span data-stu-id="0a44c-128">Select your **Azure subscription**, **location**, and choose a **name** for your application.</span></span>  <span data-ttu-id="0a44c-129">When you're done, choose **Done**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-129">When you're done, choose **Done**.</span></span>

    ![Enter Azure DevOps info](_img/azure-devops-project-ruby/vstsazureinfo.png)

1. <span data-ttu-id="0a44c-131">In a few minutes, the **Azure DevOps Project dashboard** loads in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0a44c-131">In a few minutes, the **Azure DevOps Project dashboard** loads in the Azure portal.</span></span>  <span data-ttu-id="0a44c-132">A sample application is set up in a repository in your Azure DevOps Services organization, a build executes, and your application deploys to Azure.</span><span class="sxs-lookup"><span data-stu-id="0a44c-132">A sample application is set up in a repository in your Azure DevOps Services organization, a build executes, and your application deploys to Azure.</span></span>  <span data-ttu-id="0a44c-133">This dashboard provides visibility into your **code repository**, **Azure CI/CD pipeline**, and your **application in Azure**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-133">This dashboard provides visibility into your **code repository**, **Azure CI/CD pipeline**, and your **application in Azure**.</span></span>  <span data-ttu-id="0a44c-134">On the right side of the dashboard, select **Browse** to view your running application.</span><span class="sxs-lookup"><span data-stu-id="0a44c-134">On the right side of the dashboard, select **Browse** to view your running application.</span></span>

    ![Dashboard view](_img/azure-devops-project-ruby/dashboardnopreview.png) 

## <a name="commit-code-changes-and-execute-cicd"></a><span data-ttu-id="0a44c-136">Commit code changes and execute CI/CD</span><span class="sxs-lookup"><span data-stu-id="0a44c-136">Commit code changes and execute CI/CD</span></span>

<span data-ttu-id="0a44c-137">The Azure DevOps Project created a Git repository in your Azure DevOps Services organization or GitHub account.</span><span class="sxs-lookup"><span data-stu-id="0a44c-137">The Azure DevOps Project created a Git repository in your Azure DevOps Services organization or GitHub account.</span></span>  <span data-ttu-id="0a44c-138">Follow the steps below to view the repository and make code changes to your application.</span><span class="sxs-lookup"><span data-stu-id="0a44c-138">Follow the steps below to view the repository and make code changes to your application.</span></span>

1. <span data-ttu-id="0a44c-139">On the left-hand side of the DevOps Project dashboard, select the link for your **master** branch.</span><span class="sxs-lookup"><span data-stu-id="0a44c-139">On the left-hand side of the DevOps Project dashboard, select the link for your **master** branch.</span></span>  <span data-ttu-id="0a44c-140">This link opens a view to the newly created Git repository.</span><span class="sxs-lookup"><span data-stu-id="0a44c-140">This link opens a view to the newly created Git repository.</span></span>

1. <span data-ttu-id="0a44c-141">To view the repository clone URL, select **Clone** from the top right of the browser.</span><span class="sxs-lookup"><span data-stu-id="0a44c-141">To view the repository clone URL, select **Clone** from the top right of the browser.</span></span> <span data-ttu-id="0a44c-142">You can clone your Git repository in your favorite IDE.</span><span class="sxs-lookup"><span data-stu-id="0a44c-142">You can clone your Git repository in your favorite IDE.</span></span>  <span data-ttu-id="0a44c-143">In the next few steps, you can use the web browser to make and commit code changes directly to the master branch.</span><span class="sxs-lookup"><span data-stu-id="0a44c-143">In the next few steps, you can use the web browser to make and commit code changes directly to the master branch.</span></span>

1. <span data-ttu-id="0a44c-144">On the left-hand side of the browser, navigate to the **app/views/pages/home.html.erb** file.</span><span class="sxs-lookup"><span data-stu-id="0a44c-144">On the left-hand side of the browser, navigate to the **app/views/pages/home.html.erb** file.</span></span>

1. <span data-ttu-id="0a44c-145">Select **Edit**, and make a change to some text.</span><span class="sxs-lookup"><span data-stu-id="0a44c-145">Select **Edit**, and make a change to some text.</span></span>  <span data-ttu-id="0a44c-146">For example, modify text inside one of the div tags.</span><span class="sxs-lookup"><span data-stu-id="0a44c-146">For example, modify text inside one of the div tags.</span></span>

1. <span data-ttu-id="0a44c-147">Choose **Commit**, then save your changes.</span><span class="sxs-lookup"><span data-stu-id="0a44c-147">Choose **Commit**, then save your changes.</span></span>

1. <span data-ttu-id="0a44c-148">In your browser, navigate to the **Azure DevOps Project dashboard**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-148">In your browser, navigate to the **Azure DevOps Project dashboard**.</span></span>  <span data-ttu-id="0a44c-149">You should now see a build is in progress.</span><span class="sxs-lookup"><span data-stu-id="0a44c-149">You should now see a build is in progress.</span></span>  <span data-ttu-id="0a44c-150">The changes you just made are automatically built and deployed via an Azure CI/CD pipeline.</span><span class="sxs-lookup"><span data-stu-id="0a44c-150">The changes you just made are automatically built and deployed via an Azure CI/CD pipeline.</span></span>

## <a name="examine-the-azure-cicd-pipeline"></a><span data-ttu-id="0a44c-151">Examine the Azure CI/CD pipeline</span><span class="sxs-lookup"><span data-stu-id="0a44c-151">Examine the Azure CI/CD pipeline</span></span>

<span data-ttu-id="0a44c-152">The Azure DevOps Project automatically configured a full Azure CI/CD pipeline in your Azure DevOps Services organization.</span><span class="sxs-lookup"><span data-stu-id="0a44c-152">The Azure DevOps Project automatically configured a full Azure CI/CD pipeline in your Azure DevOps Services organization.</span></span>  <span data-ttu-id="0a44c-153">Explore and customize the pipeline as needed.</span><span class="sxs-lookup"><span data-stu-id="0a44c-153">Explore and customize the pipeline as needed.</span></span>  <span data-ttu-id="0a44c-154">Follow the steps below to familiarize yourself with the Azure DevOps Services build and release pipelines.</span><span class="sxs-lookup"><span data-stu-id="0a44c-154">Follow the steps below to familiarize yourself with the Azure DevOps Services build and release pipelines.</span></span>

1. <span data-ttu-id="0a44c-155">Select **Build Pipelines** from the **top** of the Azure DevOps Project dashboard.</span><span class="sxs-lookup"><span data-stu-id="0a44c-155">Select **Build Pipelines** from the **top** of the Azure DevOps Project dashboard.</span></span>  <span data-ttu-id="0a44c-156">This link opens a browser tab and opens the Azure DevOps Services build pipeline for your new project.</span><span class="sxs-lookup"><span data-stu-id="0a44c-156">This link opens a browser tab and opens the Azure DevOps Services build pipeline for your new project.</span></span>

1. <span data-ttu-id="0a44c-157">Select the **ellipsis**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-157">Select the **ellipsis**.</span></span>  <span data-ttu-id="0a44c-158">This action opens a menu where you can start several activities such as queue a new build, pause a build, and edit the build pipeline.</span><span class="sxs-lookup"><span data-stu-id="0a44c-158">This action opens a menu where you can start several activities such as queue a new build, pause a build, and edit the build pipeline.</span></span>

1. <span data-ttu-id="0a44c-159">Select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-159">Select **Edit**.</span></span>

1. <span data-ttu-id="0a44c-160">From this view, **examine the various tasks** for your build pipeline.</span><span class="sxs-lookup"><span data-stu-id="0a44c-160">From this view, **examine the various tasks** for your build pipeline.</span></span>  <span data-ttu-id="0a44c-161">The build executes various tasks such as fetching sources from the Git repository, restoring dependencies, and publishing outputs used for deployments.</span><span class="sxs-lookup"><span data-stu-id="0a44c-161">The build executes various tasks such as fetching sources from the Git repository, restoring dependencies, and publishing outputs used for deployments.</span></span>

1. <span data-ttu-id="0a44c-162">At the top of the build pipeline, select the **build pipeline name**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-162">At the top of the build pipeline, select the **build pipeline name**.</span></span>

1. <span data-ttu-id="0a44c-163">Change the **name** of your build pipeline to something more descriptive.</span><span class="sxs-lookup"><span data-stu-id="0a44c-163">Change the **name** of your build pipeline to something more descriptive.</span></span>  <span data-ttu-id="0a44c-164">Select **Save & queue**, then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-164">Select **Save & queue**, then select **Save**.</span></span>

1. <span data-ttu-id="0a44c-165">Under your build pipeline name, select **History**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-165">Under your build pipeline name, select **History**.</span></span>  <span data-ttu-id="0a44c-166">You see an audit trail of your recent changes for the build.</span><span class="sxs-lookup"><span data-stu-id="0a44c-166">You see an audit trail of your recent changes for the build.</span></span>  <span data-ttu-id="0a44c-167">Azure DevOps Services keeps track of any changes made to the build pipeline, and allows you to compare versions.</span><span class="sxs-lookup"><span data-stu-id="0a44c-167">Azure DevOps Services keeps track of any changes made to the build pipeline, and allows you to compare versions.</span></span>

1. <span data-ttu-id="0a44c-168">Select **Triggers**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-168">Select **Triggers**.</span></span>  <span data-ttu-id="0a44c-169">The Azure DevOps Project automatically created a CI trigger, and every commit to the repository starts a new build.</span><span class="sxs-lookup"><span data-stu-id="0a44c-169">The Azure DevOps Project automatically created a CI trigger, and every commit to the repository starts a new build.</span></span>  <span data-ttu-id="0a44c-170">You can optionally choose to include or exclude branches from the CI process.</span><span class="sxs-lookup"><span data-stu-id="0a44c-170">You can optionally choose to include or exclude branches from the CI process.</span></span>

1. <span data-ttu-id="0a44c-171">Select **Retention**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-171">Select **Retention**.</span></span>  <span data-ttu-id="0a44c-172">Based on your scenario, you can specify policies to keep or remove a certain number of builds.</span><span class="sxs-lookup"><span data-stu-id="0a44c-172">Based on your scenario, you can specify policies to keep or remove a certain number of builds.</span></span>

1. <span data-ttu-id="0a44c-173">Select **Build and Release**, then choose **Releases**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-173">Select **Build and Release**, then choose **Releases**.</span></span>  <span data-ttu-id="0a44c-174">The Azure DevOps Project created an Azure DevOps Services release pipeline to manage deployments to Azure.</span><span class="sxs-lookup"><span data-stu-id="0a44c-174">The Azure DevOps Project created an Azure DevOps Services release pipeline to manage deployments to Azure.</span></span>

1. <span data-ttu-id="0a44c-175">On the left-hand side of the browser, select the **ellipsis** next to your release pipeline, then choose **Edit**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-175">On the left-hand side of the browser, select the **ellipsis** next to your release pipeline, then choose **Edit**.</span></span>

1. <span data-ttu-id="0a44c-176">The release pipeline contains a **pipeline**, which defines the release process.</span><span class="sxs-lookup"><span data-stu-id="0a44c-176">The release pipeline contains a **pipeline**, which defines the release process.</span></span>  <span data-ttu-id="0a44c-177">Under **Artifacts**, select **Drop**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-177">Under **Artifacts**, select **Drop**.</span></span>  <span data-ttu-id="0a44c-178">The build pipeline you examined in the previous steps produces the output used for the artifact.</span><span class="sxs-lookup"><span data-stu-id="0a44c-178">The build pipeline you examined in the previous steps produces the output used for the artifact.</span></span> 

1. <span data-ttu-id="0a44c-179">To the right-hand side of the **Drop** icon, select the **Continuous deployment trigger**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-179">To the right-hand side of the **Drop** icon, select the **Continuous deployment trigger**.</span></span>  <span data-ttu-id="0a44c-180">This release pipeline has an enabled CD trigger, which executes a deployment every time there is a new build artifact available.</span><span class="sxs-lookup"><span data-stu-id="0a44c-180">This release pipeline has an enabled CD trigger, which executes a deployment every time there is a new build artifact available.</span></span>  <span data-ttu-id="0a44c-181">Optionally, you can disable the trigger, so your deployments require manual execution.</span><span class="sxs-lookup"><span data-stu-id="0a44c-181">Optionally, you can disable the trigger, so your deployments require manual execution.</span></span> 

1. <span data-ttu-id="0a44c-182">On the left-hand side of the browser, select **Tasks**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-182">On the left-hand side of the browser, select **Tasks**.</span></span>  <span data-ttu-id="0a44c-183">The tasks are the activities your deployment process performs.</span><span class="sxs-lookup"><span data-stu-id="0a44c-183">The tasks are the activities your deployment process performs.</span></span>  <span data-ttu-id="0a44c-184">In this example, a task was created to deploy to **Azure App service**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-184">In this example, a task was created to deploy to **Azure App service**.</span></span>

1. <span data-ttu-id="0a44c-185">On the right-hand side of the browser, select **View releases**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-185">On the right-hand side of the browser, select **View releases**.</span></span>  <span data-ttu-id="0a44c-186">This view shows a history of releases.</span><span class="sxs-lookup"><span data-stu-id="0a44c-186">This view shows a history of releases.</span></span>

1. <span data-ttu-id="0a44c-187">Select the **ellipsis** next to one of your releases, and choose **Open**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-187">Select the **ellipsis** next to one of your releases, and choose **Open**.</span></span>  <span data-ttu-id="0a44c-188">There are several menus to explore from this view such as a release summary, associated work items, and tests.</span><span class="sxs-lookup"><span data-stu-id="0a44c-188">There are several menus to explore from this view such as a release summary, associated work items, and tests.</span></span>

1. <span data-ttu-id="0a44c-189">Select **Commits**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-189">Select **Commits**.</span></span>  <span data-ttu-id="0a44c-190">This view shows code commits associated with the specific deployment.</span><span class="sxs-lookup"><span data-stu-id="0a44c-190">This view shows code commits associated with the specific deployment.</span></span> 

1. <span data-ttu-id="0a44c-191">Select **Logs**.</span><span class="sxs-lookup"><span data-stu-id="0a44c-191">Select **Logs**.</span></span>  <span data-ttu-id="0a44c-192">The logs contain useful information about the deployment process.</span><span class="sxs-lookup"><span data-stu-id="0a44c-192">The logs contain useful information about the deployment process.</span></span>  <span data-ttu-id="0a44c-193">They can be viewed both during and after deployments.</span><span class="sxs-lookup"><span data-stu-id="0a44c-193">They can be viewed both during and after deployments.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="0a44c-194">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="0a44c-194">Clean up resources</span></span>

<span data-ttu-id="0a44c-195">When no longer needed, you can delete the Azure App service and related resources created in this quickstart by using the **Delete** function from the Azure DevOps Project dashboard.</span><span class="sxs-lookup"><span data-stu-id="0a44c-195">When no longer needed, you can delete the Azure App service and related resources created in this quickstart by using the **Delete** function from the Azure DevOps Project dashboard.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a44c-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="0a44c-196">Next steps</span></span>

<span data-ttu-id="0a44c-197">To learn more about modifying the build and release pipelines to meet the needs of your team, see this tutorial:</span><span class="sxs-lookup"><span data-stu-id="0a44c-197">To learn more about modifying the build and release pipelines to meet the needs of your team, see this tutorial:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0a44c-198">Customize CD process</span><span class="sxs-lookup"><span data-stu-id="0a44c-198">Customize CD process</span></span>](https://docs.microsoft.com/azure/devops/pipelines/release/define-multistage-release-process?view=vsts)
