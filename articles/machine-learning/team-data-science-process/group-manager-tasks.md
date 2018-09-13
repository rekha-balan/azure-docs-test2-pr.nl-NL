---
title: Team Data Science Process Group Manager tasks - Azure  | Microsoft Docs
description: An outline of the tasks for a group manager on a data science team project.
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: ''
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/13/2017
ms.author: deguhath
ms.openlocfilehash: a89c0f916f67de1bae81a5e1b3dcfc2cae41d248
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855741"
---
# <a name="group-manager-tasks"></a><span data-ttu-id="a368a-103">Group Manager tasks</span><span class="sxs-lookup"><span data-stu-id="a368a-103">Group Manager tasks</span></span>

<span data-ttu-id="a368a-104">This topic outlines the tasks that a Group Manager is expected to complete for hist/her data science organization.</span><span class="sxs-lookup"><span data-stu-id="a368a-104">This topic outlines the tasks that a Group Manager is expected to complete for hist/her data science organization.</span></span> <span data-ttu-id="a368a-105">The objective is to establish collaborative group environment that standardizes on the [Team Data Science Process](overview.md) (TDSP).</span><span class="sxs-lookup"><span data-stu-id="a368a-105">The objective is to establish collaborative group environment that standardizes on the [Team Data Science Process](overview.md) (TDSP).</span></span> <span data-ttu-id="a368a-106">For an outline of the personnel roles and their associated tasks that are handled by a data science team standardizing on this process, see [Team Data Science Process roles and tasks](roles-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="a368a-106">For an outline of the personnel roles and their associated tasks that are handled by a data science team standardizing on this process, see [Team Data Science Process roles and tasks](roles-tasks.md).</span></span>

<span data-ttu-id="a368a-107">The **Group Manager** is the manager of the entire data science unit in an enterprise.</span><span class="sxs-lookup"><span data-stu-id="a368a-107">The **Group Manager** is the manager of the entire data science unit in an enterprise.</span></span> <span data-ttu-id="a368a-108">A data science unit may have multiple teams, each of which is working on multiple data science projects in distinct business verticals.</span><span class="sxs-lookup"><span data-stu-id="a368a-108">A data science unit may have multiple teams, each of which is working on multiple data science projects in distinct business verticals.</span></span> <span data-ttu-id="a368a-109">A Group Manager may delegate their tasks to a surrogate, but the tasks associated with the role are the same.</span><span class="sxs-lookup"><span data-stu-id="a368a-109">A Group Manager may delegate their tasks to a surrogate, but the tasks associated with the role are the same.</span></span> <span data-ttu-id="a368a-110">There are six main tasks as shown in the following diagram:</span><span class="sxs-lookup"><span data-stu-id="a368a-110">There are six main tasks as shown in the following diagram:</span></span>

![0](./media/group-manager-tasks/tdsp-group-manager.png)


>[AZURE.NOTE] <span data-ttu-id="a368a-112">We outline the steps needed to set up a TDSP group environment using Azure DevOps Services in the instructions that follow.</span><span class="sxs-lookup"><span data-stu-id="a368a-112">We outline the steps needed to set up a TDSP group environment using Azure DevOps Services in the instructions that follow.</span></span> <span data-ttu-id="a368a-113">We specify how to accomplish these tasks with Azure DevOps Services because that is how we implement TDSP at Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a368a-113">We specify how to accomplish these tasks with Azure DevOps Services because that is how we implement TDSP at Microsoft.</span></span> <span data-ttu-id="a368a-114">If another code hosting platform is used for your group, the tasks that need to be completed by the group manager generally do not change.</span><span class="sxs-lookup"><span data-stu-id="a368a-114">If another code hosting platform is used for your group, the tasks that need to be completed by the group manager generally do not change.</span></span> <span data-ttu-id="a368a-115">But the way to complete these tasks is going to be different.</span><span class="sxs-lookup"><span data-stu-id="a368a-115">But the way to complete these tasks is going to be different.</span></span>

1. <span data-ttu-id="a368a-116">Set up **Azure DevOps Services** for the group.</span><span class="sxs-lookup"><span data-stu-id="a368a-116">Set up **Azure DevOps Services** for the group.</span></span>
2. <span data-ttu-id="a368a-117">Create a **group project** on Azure DevOps Services (for Azure DevOps Services users)</span><span class="sxs-lookup"><span data-stu-id="a368a-117">Create a **group project** on Azure DevOps Services (for Azure DevOps Services users)</span></span>
3. <span data-ttu-id="a368a-118">Create the **GroupProjectTemplate** repository</span><span class="sxs-lookup"><span data-stu-id="a368a-118">Create the **GroupProjectTemplate** repository</span></span>
4. <span data-ttu-id="a368a-119">Create the **GroupUtilities** repository</span><span class="sxs-lookup"><span data-stu-id="a368a-119">Create the **GroupUtilities** repository</span></span>
5. <span data-ttu-id="a368a-120">Seed the **GroupProjectTemplate** and **GroupUtilities** repositories for the Azure DevOps Services with content from the TDSP repositories.</span><span class="sxs-lookup"><span data-stu-id="a368a-120">Seed the **GroupProjectTemplate** and **GroupUtilities** repositories for the Azure DevOps Services with content from the TDSP repositories.</span></span>
6. <span data-ttu-id="a368a-121">Set up the **security controls** for team members to access to the GroupProjectTemplate and GroupUtilities repositories.</span><span class="sxs-lookup"><span data-stu-id="a368a-121">Set up the **security controls** for team members to access to the GroupProjectTemplate and GroupUtilities repositories.</span></span>

<span data-ttu-id="a368a-122">Each of the preceding steps is described in detail.</span><span class="sxs-lookup"><span data-stu-id="a368a-122">Each of the preceding steps is described in detail.</span></span> <span data-ttu-id="a368a-123">But first, we familiarize you with the abbreviations and discuss the pre-requisites for working with repositories.</span><span class="sxs-lookup"><span data-stu-id="a368a-123">But first, we familiarize you with the abbreviations and discuss the pre-requisites for working with repositories.</span></span>

### <a name="abbreviations-for-repositories-and-directories"></a><span data-ttu-id="a368a-124">Abbreviations for repositories and directories</span><span class="sxs-lookup"><span data-stu-id="a368a-124">Abbreviations for repositories and directories</span></span>

<span data-ttu-id="a368a-125">This tutorial uses abbreviated names for repositories and directories.</span><span class="sxs-lookup"><span data-stu-id="a368a-125">This tutorial uses abbreviated names for repositories and directories.</span></span> <span data-ttu-id="a368a-126">These definitions make it easier to follow the operations between the repositories and directories.</span><span class="sxs-lookup"><span data-stu-id="a368a-126">These definitions make it easier to follow the operations between the repositories and directories.</span></span> <span data-ttu-id="a368a-127">This notation is used in the following sections:</span><span class="sxs-lookup"><span data-stu-id="a368a-127">This notation is used in the following sections:</span></span>

- <span data-ttu-id="a368a-128">**G1**: The project template repository developed and managed by TDSP team of Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a368a-128">**G1**: The project template repository developed and managed by TDSP team of Microsoft.</span></span>
- <span data-ttu-id="a368a-129">**G2**: The utilities repository developed and managed by TDSP team of Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a368a-129">**G2**: The utilities repository developed and managed by TDSP team of Microsoft.</span></span>
- <span data-ttu-id="a368a-130">**R1**: The GroupProjectTemplate repository on Git you set up on your Azure DevOps group server.</span><span class="sxs-lookup"><span data-stu-id="a368a-130">**R1**: The GroupProjectTemplate repository on Git you set up on your Azure DevOps group server.</span></span>
- <span data-ttu-id="a368a-131">**R2**: The GroupUtilities repository on Git you set up on your Azure DevOps group server.</span><span class="sxs-lookup"><span data-stu-id="a368a-131">**R2**: The GroupUtilities repository on Git you set up on your Azure DevOps group server.</span></span>
- <span data-ttu-id="a368a-132">**LG1** and **LG2**: The local directories on your machine that you clone G1 and G2 to, respectively.</span><span class="sxs-lookup"><span data-stu-id="a368a-132">**LG1** and **LG2**: The local directories on your machine that you clone G1 and G2 to, respectively.</span></span>
- <span data-ttu-id="a368a-133">**LR1** and **LR2**: The local directories on your machine that you clone R1 and R2 to, respectively.</span><span class="sxs-lookup"><span data-stu-id="a368a-133">**LR1** and **LR2**: The local directories on your machine that you clone R1 and R2 to, respectively.</span></span>

### <a name="pre-requisites-for-cloning-repositories-and-checking-code-in-and-out"></a><span data-ttu-id="a368a-134">Pre-requisites for cloning repositories and checking code in and out</span><span class="sxs-lookup"><span data-stu-id="a368a-134">Pre-requisites for cloning repositories and checking code in and out</span></span>
 
- <span data-ttu-id="a368a-135">Git must be installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="a368a-135">Git must be installed on your machine.</span></span> <span data-ttu-id="a368a-136">If you are using a Data Science Virtual Machine (DSVM), Git has been pre-installed and you are good to go.</span><span class="sxs-lookup"><span data-stu-id="a368a-136">If you are using a Data Science Virtual Machine (DSVM), Git has been pre-installed and you are good to go.</span></span> <span data-ttu-id="a368a-137">Otherwise, see the [Platforms and tools appendix](platforms-and-tools.md#appendix).</span><span class="sxs-lookup"><span data-stu-id="a368a-137">Otherwise, see the [Platforms and tools appendix](platforms-and-tools.md#appendix).</span></span>  
- <span data-ttu-id="a368a-138">If you are using a **Windows DSVM**, you need to have [Git Credential Manager (GCM)](https://github.com/Microsoft/Git-Credential-Manager-for-Windows) installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="a368a-138">If you are using a **Windows DSVM**, you need to have [Git Credential Manager (GCM)](https://github.com/Microsoft/Git-Credential-Manager-for-Windows) installed on your machine.</span></span> <span data-ttu-id="a368a-139">In the README.md file, scroll down to the **Download and Install** section and click the *latest installer*.</span><span class="sxs-lookup"><span data-stu-id="a368a-139">In the README.md file, scroll down to the **Download and Install** section and click the *latest installer*.</span></span> <span data-ttu-id="a368a-140">This step takes you to the latest installer page.</span><span class="sxs-lookup"><span data-stu-id="a368a-140">This step takes you to the latest installer page.</span></span> <span data-ttu-id="a368a-141">Download the .exe installer from here and run it.</span><span class="sxs-lookup"><span data-stu-id="a368a-141">Download the .exe installer from here and run it.</span></span> 
- <span data-ttu-id="a368a-142">If you are using **Linux DSVM**, create an SSH public key on your DSVM and add it to your group Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="a368a-142">If you are using **Linux DSVM**, create an SSH public key on your DSVM and add it to your group Azure DevOps Services.</span></span> <span data-ttu-id="a368a-143">For more information about SSH, see the **Create SSH public key** section in the [Platforms and tools appendix](platforms-and-tools.md#appendix).</span><span class="sxs-lookup"><span data-stu-id="a368a-143">For more information about SSH, see the **Create SSH public key** section in the [Platforms and tools appendix](platforms-and-tools.md#appendix).</span></span> 


## <a name="1-create-account-on-azure-devops-services"></a><span data-ttu-id="a368a-144">1. Create Account on Azure DevOps Services</span><span class="sxs-lookup"><span data-stu-id="a368a-144">1. Create Account on Azure DevOps Services</span></span>

<span data-ttu-id="a368a-145">The Azure DevOps Services hosts the following repositories:</span><span class="sxs-lookup"><span data-stu-id="a368a-145">The Azure DevOps Services hosts the following repositories:</span></span>

- <span data-ttu-id="a368a-146">**group common repositories**: General-purpose repositories that can be adopted by multiple teams within a group for multiple data science projects.</span><span class="sxs-lookup"><span data-stu-id="a368a-146">**group common repositories**: General-purpose repositories that can be adopted by multiple teams within a group for multiple data science projects.</span></span> <span data-ttu-id="a368a-147">For example, the *GroupProjectTemplate* and *GroupUtilities* repositories.</span><span class="sxs-lookup"><span data-stu-id="a368a-147">For example, the *GroupProjectTemplate* and *GroupUtilities* repositories.</span></span>
- <span data-ttu-id="a368a-148">**team repositories**:  Repositories for specific teams within a group.</span><span class="sxs-lookup"><span data-stu-id="a368a-148">**team repositories**:  Repositories for specific teams within a group.</span></span> <span data-ttu-id="a368a-149">These repositories are specific for a team's need, and can be adopted by multiple projects executed by that team, but not general enough to be useful to multiple teams within a data science group.</span><span class="sxs-lookup"><span data-stu-id="a368a-149">These repositories are specific for a team's need, and can be adopted by multiple projects executed by that team, but not general enough to be useful to multiple teams within a data science group.</span></span> 
- <span data-ttu-id="a368a-150">**project repositories**: Repositories available for specific projects.</span><span class="sxs-lookup"><span data-stu-id="a368a-150">**project repositories**: Repositories available for specific projects.</span></span> <span data-ttu-id="a368a-151">Such repositories may not be general enough to be useful to multiple projects performed by a team, and to multiple teams in a data science group.</span><span class="sxs-lookup"><span data-stu-id="a368a-151">Such repositories may not be general enough to be useful to multiple projects performed by a team, and to multiple teams in a data science group.</span></span>


### <a name="setting-up-the-azure-devops-services-sign-into-your-microsoft-account"></a><span data-ttu-id="a368a-152">Setting up the Azure DevOps Services Sign into your Microsoft account</span><span class="sxs-lookup"><span data-stu-id="a368a-152">Setting up the Azure DevOps Services Sign into your Microsoft account</span></span>
    
<span data-ttu-id="a368a-153">Go to [Visual Studio online](https://www.visualstudio.com/), click **Sign in** in the upper right corner and sign into your Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="a368a-153">Go to [Visual Studio online](https://www.visualstudio.com/), click **Sign in** in the upper right corner and sign into your Microsoft account.</span></span> 
    
![1](./media/group-manager-tasks/login.PNG)

<span data-ttu-id="a368a-155">If you do not have a Microsoft account, click **Sign up now** to create a Microsoft account, and then sign in using this account.</span><span class="sxs-lookup"><span data-stu-id="a368a-155">If you do not have a Microsoft account, click **Sign up now** to create a Microsoft account, and then sign in using this account.</span></span> 

<span data-ttu-id="a368a-156">If your organization has a Visual Studio/MSDN subscription, click the green **Sign in with your work or school account** box and sign in with the credentials associated with this subscription.</span><span class="sxs-lookup"><span data-stu-id="a368a-156">If your organization has a Visual Studio/MSDN subscription, click the green **Sign in with your work or school account** box and sign in with the credentials associated with this subscription.</span></span> 
        
![2](./media/group-manager-tasks/signin.PNG)


        
<span data-ttu-id="a368a-158">After you sign in, click **Create New Account** in the upper right corner as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="a368a-158">After you sign in, click **Create New Account** in the upper right corner as shown in the following image:</span></span>
        
![3](./media/group-manager-tasks/create-account-1.PNG)
        
<span data-ttu-id="a368a-160">Fill in the information for the Azure DevOps Services that you want to create in the **Create your account** wizard with the following values:</span><span class="sxs-lookup"><span data-stu-id="a368a-160">Fill in the information for the Azure DevOps Services that you want to create in the **Create your account** wizard with the following values:</span></span> 

- <span data-ttu-id="a368a-161">**Server URL**: Replace *mysamplegroup* with your own *server name*.</span><span class="sxs-lookup"><span data-stu-id="a368a-161">**Server URL**: Replace *mysamplegroup* with your own *server name*.</span></span> <span data-ttu-id="a368a-162">The URL of your server is going to be: *https://\<servername\>.visualstudio.com*.</span><span class="sxs-lookup"><span data-stu-id="a368a-162">The URL of your server is going to be: *https://\<servername\>.visualstudio.com*.</span></span> 
- <span data-ttu-id="a368a-163">**Manage code using:** Select **_Git_**.</span><span class="sxs-lookup"><span data-stu-id="a368a-163">**Manage code using:** Select **_Git_**.</span></span>
- <span data-ttu-id="a368a-164">**Project name:** Enter *GroupCommon*.</span><span class="sxs-lookup"><span data-stu-id="a368a-164">**Project name:** Enter *GroupCommon*.</span></span> 
- <span data-ttu-id="a368a-165">**Organize work using:** Choose *Agile*.</span><span class="sxs-lookup"><span data-stu-id="a368a-165">**Organize work using:** Choose *Agile*.</span></span>
- <span data-ttu-id="a368a-166">**Host your projects in:** Choose a geo location.</span><span class="sxs-lookup"><span data-stu-id="a368a-166">**Host your projects in:** Choose a geo location.</span></span> <span data-ttu-id="a368a-167">In this example, we choose *South Central US*.</span><span class="sxs-lookup"><span data-stu-id="a368a-167">In this example, we choose *South Central US*.</span></span> 
        
![4](./media/group-manager-tasks/fill-in-account-information.png)

>[AZURE.NOTE] <span data-ttu-id="a368a-169">If you see the following pop-up window after you click **Create new account**, then you need to click **Change details** to display all the fields itemized.</span><span class="sxs-lookup"><span data-stu-id="a368a-169">If you see the following pop-up window after you click **Create new account**, then you need to click **Change details** to display all the fields itemized.</span></span>

![5](./media/group-manager-tasks/create-account-2.png)


<span data-ttu-id="a368a-171">Click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="a368a-171">Click **Continue**.</span></span> 

## <a name="2-groupcommon-project"></a><span data-ttu-id="a368a-172">2. GroupCommon Project</span><span class="sxs-lookup"><span data-stu-id="a368a-172">2. GroupCommon Project</span></span>

<span data-ttu-id="a368a-173">The **GroupCommon** page (*https://\<servername\>.visualstudio.com/GroupCommon*) opens after your Azure DevOps Services is created.</span><span class="sxs-lookup"><span data-stu-id="a368a-173">The **GroupCommon** page (*https://\<servername\>.visualstudio.com/GroupCommon*) opens after your Azure DevOps Services is created.</span></span>
                            
![6](./media/group-manager-tasks/server-created-2.PNG)

## <a name="3-create-the-grouputilities-r2-repository"></a><span data-ttu-id="a368a-175">3. Create the GroupUtilities (R2) repository</span><span class="sxs-lookup"><span data-stu-id="a368a-175">3. Create the GroupUtilities (R2) repository</span></span>

<span data-ttu-id="a368a-176">To create the **GroupUtilities** (R2) repository under Azure DevOps Services:</span><span class="sxs-lookup"><span data-stu-id="a368a-176">To create the **GroupUtilities** (R2) repository under Azure DevOps Services:</span></span>

- <span data-ttu-id="a368a-177">To open the **Create a new repository** wizard, click **New repository** on the **Version Control** tab of your project.</span><span class="sxs-lookup"><span data-stu-id="a368a-177">To open the **Create a new repository** wizard, click **New repository** on the **Version Control** tab of your project.</span></span> 

![7](./media/group-manager-tasks/create-grouputilities-repo-1.png) 

- <span data-ttu-id="a368a-179">Select *Git* as the **Type**, and enter *GroupUtilities* as the **Name**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a368a-179">Select *Git* as the **Type**, and enter *GroupUtilities* as the **Name**, and then click **Create**.</span></span> 

![8](./media/group-manager-tasks/create-grouputilities-repo-2.png)
                
<span data-ttu-id="a368a-181">Now you should see two Git repositories **GroupProjectTemplate** and **GroupUtilities** in the left column of the **Version Control** page:</span><span class="sxs-lookup"><span data-stu-id="a368a-181">Now you should see two Git repositories **GroupProjectTemplate** and **GroupUtilities** in the left column of the **Version Control** page:</span></span> 

![9](./media/group-manager-tasks/two-repo-under-groupCommon.PNG)


## <a name="4-create-the-groupprojecttemplate-r1-repository"></a><span data-ttu-id="a368a-183">4. Create the GroupProjectTemplate (R1) repository</span><span class="sxs-lookup"><span data-stu-id="a368a-183">4. Create the GroupProjectTemplate (R1) repository</span></span>

<span data-ttu-id="a368a-184">The setup of the repositories for the Azure DevOps group server consists of two tasks:</span><span class="sxs-lookup"><span data-stu-id="a368a-184">The setup of the repositories for the Azure DevOps group server consists of two tasks:</span></span>

- <span data-ttu-id="a368a-185">Rename the default **GroupCommon** repository***GroupProjectTemplate***.</span><span class="sxs-lookup"><span data-stu-id="a368a-185">Rename the default **GroupCommon** repository***GroupProjectTemplate***.</span></span>
- <span data-ttu-id="a368a-186">Create the **GroupUtilities** repository on the Azure DevOps Services under project **GroupCommon**.</span><span class="sxs-lookup"><span data-stu-id="a368a-186">Create the **GroupUtilities** repository on the Azure DevOps Services under project **GroupCommon**.</span></span> 

<span data-ttu-id="a368a-187">Instructions for the first task are contained in this section after remarks on naming conventions or our repositories and directories.</span><span class="sxs-lookup"><span data-stu-id="a368a-187">Instructions for the first task are contained in this section after remarks on naming conventions or our repositories and directories.</span></span> <span data-ttu-id="a368a-188">The instructions for the second task are contained in the following section for step 4.</span><span class="sxs-lookup"><span data-stu-id="a368a-188">The instructions for the second task are contained in the following section for step 4.</span></span>

### <a name="rename-the-default-groupcommon-repository"></a><span data-ttu-id="a368a-189">Rename the default GroupCommon repository</span><span class="sxs-lookup"><span data-stu-id="a368a-189">Rename the default GroupCommon repository</span></span>

<span data-ttu-id="a368a-190">To rename the default **GroupCommon** repository as *GroupProjectTemplate* (referred as **R1** in this tutorial):</span><span class="sxs-lookup"><span data-stu-id="a368a-190">To rename the default **GroupCommon** repository as *GroupProjectTemplate* (referred as **R1** in this tutorial):</span></span>
    
- <span data-ttu-id="a368a-191">Click **Collaborate on code** on the **GroupCommon** project page.</span><span class="sxs-lookup"><span data-stu-id="a368a-191">Click **Collaborate on code** on the **GroupCommon** project page.</span></span> <span data-ttu-id="a368a-192">This takes you to the default Git repository page of the project **GroupCommon**.</span><span class="sxs-lookup"><span data-stu-id="a368a-192">This takes you to the default Git repository page of the project **GroupCommon**.</span></span> <span data-ttu-id="a368a-193">Currently, this Git repository is empty.</span><span class="sxs-lookup"><span data-stu-id="a368a-193">Currently, this Git repository is empty.</span></span> 

![10](./media/group-manager-tasks/rename-groupcommon-repo-3.png)
        
- <span data-ttu-id="a368a-195">Click **GroupCommon** on the top left corner (highlighted with a red box in the following figure) on the Git repository page of **GroupCommon** and select **Manage repositories** (highlighted with a green box in the following figure).</span><span class="sxs-lookup"><span data-stu-id="a368a-195">Click **GroupCommon** on the top left corner (highlighted with a red box in the following figure) on the Git repository page of **GroupCommon** and select **Manage repositories** (highlighted with a green box in the following figure).</span></span> <span data-ttu-id="a368a-196">This  procedure brings up the **CONTROL PANEL**.</span><span class="sxs-lookup"><span data-stu-id="a368a-196">This  procedure brings up the **CONTROL PANEL**.</span></span> 
- <span data-ttu-id="a368a-197">Select the **Version Control** tab of your project.</span><span class="sxs-lookup"><span data-stu-id="a368a-197">Select the **Version Control** tab of your project.</span></span> 

![11](./media/group-manager-tasks/rename-groupcommon-repo-4.png)

- <span data-ttu-id="a368a-199">Click the **...** to the right of the **GroupCommon** repository on the left panel, and select **Rename repository**.</span><span class="sxs-lookup"><span data-stu-id="a368a-199">Click the **...** to the right of the **GroupCommon** repository on the left panel, and select **Rename repository**.</span></span> 

![12](./media/group-manager-tasks/rename-groupcommon-repo-5.png)
        
- <span data-ttu-id="a368a-201">In the **Rename the GroupCommon repository** wizard that pops up, enter *GroupProjectTemplate* in the **Repository name** box, and then click **Rename**.</span><span class="sxs-lookup"><span data-stu-id="a368a-201">In the **Rename the GroupCommon repository** wizard that pops up, enter *GroupProjectTemplate* in the **Repository name** box, and then click **Rename**.</span></span> 

![13](./media/group-manager-tasks/rename-groupcommon-repo-6.png)



## <a name="5-seed-the-r1--r2-repositories-on-the-azure-devops-services"></a><span data-ttu-id="a368a-203">5. Seed the R1 & R2 repositories on the Azure DevOps Services</span><span class="sxs-lookup"><span data-stu-id="a368a-203">5. Seed the R1 & R2 repositories on the Azure DevOps Services</span></span>

<span data-ttu-id="a368a-204">In this stage of the procedure, you seed the *GroupProjectTemplate* (R1) and *GroupUtilities* (R2) repositories that you set up in the previous section.</span><span class="sxs-lookup"><span data-stu-id="a368a-204">In this stage of the procedure, you seed the *GroupProjectTemplate* (R1) and *GroupUtilities* (R2) repositories that you set up in the previous section.</span></span> <span data-ttu-id="a368a-205">These repositories are seeded with the ***ProjectTemplate*** (**G1**) and ***Utilities*** (**G2**) repositories that are managed by Microsoft for the Team Data Science Process.</span><span class="sxs-lookup"><span data-stu-id="a368a-205">These repositories are seeded with the ***ProjectTemplate*** (**G1**) and ***Utilities*** (**G2**) repositories that are managed by Microsoft for the Team Data Science Process.</span></span> <span data-ttu-id="a368a-206">When this seeding is completed:</span><span class="sxs-lookup"><span data-stu-id="a368a-206">When this seeding is completed:</span></span>

- <span data-ttu-id="a368a-207">your R1 repository is going to have the same set of directories and document templates that the G1 does</span><span class="sxs-lookup"><span data-stu-id="a368a-207">your R1 repository is going to have the same set of directories and document templates that the G1 does</span></span>
- <span data-ttu-id="a368a-208">your R2 repository is going to contain the set of data science utilities developed by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a368a-208">your R2 repository is going to contain the set of data science utilities developed by Microsoft.</span></span>

<span data-ttu-id="a368a-209">The seeding procedure uses the directories on your local DSVM as intermediate staging sites.</span><span class="sxs-lookup"><span data-stu-id="a368a-209">The seeding procedure uses the directories on your local DSVM as intermediate staging sites.</span></span> <span data-ttu-id="a368a-210">Here are the steps followed in this section:</span><span class="sxs-lookup"><span data-stu-id="a368a-210">Here are the steps followed in this section:</span></span>

- <span data-ttu-id="a368a-211">G1 & G2 - cloned to -> LG1 & LG2</span><span class="sxs-lookup"><span data-stu-id="a368a-211">G1 & G2 - cloned to -> LG1 & LG2</span></span>
- <span data-ttu-id="a368a-212">R1 & R2 - cloned to -> LR1 & LR2</span><span class="sxs-lookup"><span data-stu-id="a368a-212">R1 & R2 - cloned to -> LR1 & LR2</span></span>
- <span data-ttu-id="a368a-213">LG1 & LG2 - files copied into -> LR1 & LR2</span><span class="sxs-lookup"><span data-stu-id="a368a-213">LG1 & LG2 - files copied into -> LR1 & LR2</span></span>
- <span data-ttu-id="a368a-214">(Optional) customization of LR1 & LR2</span><span class="sxs-lookup"><span data-stu-id="a368a-214">(Optional) customization of LR1 & LR2</span></span>
- <span data-ttu-id="a368a-215">LR1 & LR2 - contents add to -> R1 & R2</span><span class="sxs-lookup"><span data-stu-id="a368a-215">LR1 & LR2 - contents add to -> R1 & R2</span></span>


### <a name="clone-g1--g2-repositories-to-your-local-dsvm"></a><span data-ttu-id="a368a-216">Clone G1 & G2 repositories to your local DSVM</span><span class="sxs-lookup"><span data-stu-id="a368a-216">Clone G1 & G2 repositories to your local DSVM</span></span>

<span data-ttu-id="a368a-217">In this step, you clone the Team Data Science Process (TDSP) ProjectTemplate repository (G1) and Utilities (G2) from the TDSP github repositories to folders in your local DSVM as LG1 and LG2:</span><span class="sxs-lookup"><span data-stu-id="a368a-217">In this step, you clone the Team Data Science Process (TDSP) ProjectTemplate repository (G1) and Utilities (G2) from the TDSP github repositories to folders in your local DSVM as LG1 and LG2:</span></span>

- <span data-ttu-id="a368a-218">Create a directory to serve as the root directory to host all your clones of the repositories.</span><span class="sxs-lookup"><span data-stu-id="a368a-218">Create a directory to serve as the root directory to host all your clones of the repositories.</span></span> 
    -  <span data-ttu-id="a368a-219">In the Windows DSVM, create a directory *C:\GitRepos\TDSPCommon*.</span><span class="sxs-lookup"><span data-stu-id="a368a-219">In the Windows DSVM, create a directory *C:\GitRepos\TDSPCommon*.</span></span> 
    -  <span data-ttu-id="a368a-220">In the Linux DSVM, create a directory *GitRepos\TDSPCommon* in your home directory.</span><span class="sxs-lookup"><span data-stu-id="a368a-220">In the Linux DSVM, create a directory *GitRepos\TDSPCommon* in your home directory.</span></span> 

- <span data-ttu-id="a368a-221">Run the following set of commands from the *GitRepos\TDSPCommon* directory.</span><span class="sxs-lookup"><span data-stu-id="a368a-221">Run the following set of commands from the *GitRepos\TDSPCommon* directory.</span></span>

    `git clone https://github.com/Azure/Azure-TDSP-ProjectTemplate`<br>
    `git clone https://github.com/Azure/Azure-TDSP-Utilities`
        
![14](./media/group-manager-tasks/two-folder-cloned-from-TDSP-windows.PNG)

- <span data-ttu-id="a368a-223">Using our abbreviated repository names, this is what these scripts have achieved:</span><span class="sxs-lookup"><span data-stu-id="a368a-223">Using our abbreviated repository names, this is what these scripts have achieved:</span></span> 
    - <span data-ttu-id="a368a-224">G1 - cloned into -> LG1</span><span class="sxs-lookup"><span data-stu-id="a368a-224">G1 - cloned into -> LG1</span></span>
    - <span data-ttu-id="a368a-225">G2 - cloned into -> LG2</span><span class="sxs-lookup"><span data-stu-id="a368a-225">G2 - cloned into -> LG2</span></span>
- <span data-ttu-id="a368a-226">After the cloning is completed, you should be able to see two directories, _ProjectTemplate_ and _Utilities_, under **GitRepos\TDSPCommon** directory.</span><span class="sxs-lookup"><span data-stu-id="a368a-226">After the cloning is completed, you should be able to see two directories, _ProjectTemplate_ and _Utilities_, under **GitRepos\TDSPCommon** directory.</span></span> 

### <a name="clone-r1--r2-repositories-to-your-local-dsvm"></a><span data-ttu-id="a368a-227">Clone R1 & R2 repositories to your local DSVM</span><span class="sxs-lookup"><span data-stu-id="a368a-227">Clone R1 & R2 repositories to your local DSVM</span></span>

<span data-ttu-id="a368a-228">In this step, you clone the GroupProjectTemplate repository (R1) and GroupUtilities repository (R2) on local directories (referred as LR1 and LR2, respectively) under **GitRepos\GroupCommon** on your DSVM.</span><span class="sxs-lookup"><span data-stu-id="a368a-228">In this step, you clone the GroupProjectTemplate repository (R1) and GroupUtilities repository (R2) on local directories (referred as LR1 and LR2, respectively) under **GitRepos\GroupCommon** on your DSVM.</span></span>

- <span data-ttu-id="a368a-229">To get the URLs of the R1 and R2 repositories, go to your **GroupCommon** home page on Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="a368a-229">To get the URLs of the R1 and R2 repositories, go to your **GroupCommon** home page on Azure DevOps Services.</span></span> <span data-ttu-id="a368a-230">This usually has the URL *https://\<Your Azure DevOps Services Name\>.visualstudio.com/GroupCommon*.</span><span class="sxs-lookup"><span data-stu-id="a368a-230">This usually has the URL *https://\<Your Azure DevOps Services Name\>.visualstudio.com/GroupCommon*.</span></span> 
- <span data-ttu-id="a368a-231">Click **CODE**.</span><span class="sxs-lookup"><span data-stu-id="a368a-231">Click **CODE**.</span></span> 
- <span data-ttu-id="a368a-232">Choose the **GroupProjectTemplate** and **GroupUtilities** repositories.</span><span class="sxs-lookup"><span data-stu-id="a368a-232">Choose the **GroupProjectTemplate** and **GroupUtilities** repositories.</span></span> <span data-ttu-id="a368a-233">Copy and save each of the URLs (HTTPS for Windows; SSH for Linux) from the **Clone URL** element, in turn, for use in the following scripts:</span><span class="sxs-lookup"><span data-stu-id="a368a-233">Copy and save each of the URLs (HTTPS for Windows; SSH for Linux) from the **Clone URL** element, in turn, for use in the following scripts:</span></span>  

![15](./media/group-manager-tasks/find_https_ssh_2.PNG)

- <span data-ttu-id="a368a-235">Change into the **GitRepos\GroupCommon** directory on your Windows or Linux DSVM and run one of the following sets of commands to clone R1 and R2 into that directory.</span><span class="sxs-lookup"><span data-stu-id="a368a-235">Change into the **GitRepos\GroupCommon** directory on your Windows or Linux DSVM and run one of the following sets of commands to clone R1 and R2 into that directory.</span></span>
        
<span data-ttu-id="a368a-236">Here are the Windows and Linux scripts:</span><span class="sxs-lookup"><span data-stu-id="a368a-236">Here are the Windows and Linux scripts:</span></span>

    # Windows DSVM

    git clone <the HTTPS URL of the GroupProjectTemplate repository>
    git clone <the HTTPS URL of the GroupUtilities repository>

![16](./media/group-manager-tasks/clone-two-empty-group-reo-windows-2.PNG)

    # Linux DSVM

    git clone <the SSH URL of the GroupProjectTemplate repository>
    git clone <the SSH URL of the GroupUtilities repository>

![17](./media/group-manager-tasks/clone-two-empty-group-reo-linux-2.PNG)

>[AZURE.NOTE] <span data-ttu-id="a368a-239">Expect to receive warning messages that LR1 and LR2 are empty.</span><span class="sxs-lookup"><span data-stu-id="a368a-239">Expect to receive warning messages that LR1 and LR2 are empty.</span></span>    

- <span data-ttu-id="a368a-240">Using our abbreviated repository names, this is what these scripts have achieved:</span><span class="sxs-lookup"><span data-stu-id="a368a-240">Using our abbreviated repository names, this is what these scripts have achieved:</span></span> 
    - <span data-ttu-id="a368a-241">R1 - cloned into -> LR1</span><span class="sxs-lookup"><span data-stu-id="a368a-241">R1 - cloned into -> LR1</span></span>
    - <span data-ttu-id="a368a-242">R2 - cloned into -> LR2</span><span class="sxs-lookup"><span data-stu-id="a368a-242">R2 - cloned into -> LR2</span></span>   


### <a name="seed-your-groupprojecttemplate-lr1-and-grouputilities-lr2"></a><span data-ttu-id="a368a-243">Seed your GroupProjectTemplate (LR1) and GroupUtilities (LR2)</span><span class="sxs-lookup"><span data-stu-id="a368a-243">Seed your GroupProjectTemplate (LR1) and GroupUtilities (LR2)</span></span>

<span data-ttu-id="a368a-244">Next, in your local machine, copy the content of ProjectTemplate and Utilities directories (except the metadata in the .git directories) under GitRepos\TDSPCommon to your GroupProjectTemplate and GroupUtilities directories under **GitRepos\GroupCommon**.</span><span class="sxs-lookup"><span data-stu-id="a368a-244">Next, in your local machine, copy the content of ProjectTemplate and Utilities directories (except the metadata in the .git directories) under GitRepos\TDSPCommon to your GroupProjectTemplate and GroupUtilities directories under **GitRepos\GroupCommon**.</span></span> <span data-ttu-id="a368a-245">Here are the two tasks to complete in this step:</span><span class="sxs-lookup"><span data-stu-id="a368a-245">Here are the two tasks to complete in this step:</span></span>

- <span data-ttu-id="a368a-246">Copy the files in GitRepos\TDSPCommon\ProjectTemplate (**LG1**) to GitRepos\GroupCommon\GroupProjectTemplate (**LR1**)</span><span class="sxs-lookup"><span data-stu-id="a368a-246">Copy the files in GitRepos\TDSPCommon\ProjectTemplate (**LG1**) to GitRepos\GroupCommon\GroupProjectTemplate (**LR1**)</span></span> 
- <span data-ttu-id="a368a-247">Copy the files in GitRepos\TDSPCommon\Utilities (**LG2** to GitRepos\GroupCommon\Utilities (**LR2**).</span><span class="sxs-lookup"><span data-stu-id="a368a-247">Copy the files in GitRepos\TDSPCommon\Utilities (**LG2** to GitRepos\GroupCommon\Utilities (**LR2**).</span></span> 

<span data-ttu-id="a368a-248">To achieve these two tasks, run the following scripts in PowerShell console (Windows) or Shell script console (Linux).</span><span class="sxs-lookup"><span data-stu-id="a368a-248">To achieve these two tasks, run the following scripts in PowerShell console (Windows) or Shell script console (Linux).</span></span> <span data-ttu-id="a368a-249">You are prompted to input the complete paths to LG1, LR1, LG2, and LR2.</span><span class="sxs-lookup"><span data-stu-id="a368a-249">You are prompted to input the complete paths to LG1, LR1, LG2, and LR2.</span></span> <span data-ttu-id="a368a-250">The paths that you input are validated.</span><span class="sxs-lookup"><span data-stu-id="a368a-250">The paths that you input are validated.</span></span> <span data-ttu-id="a368a-251">If you input a directory that does not exist, you are asked to input it again.</span><span class="sxs-lookup"><span data-stu-id="a368a-251">If you input a directory that does not exist, you are asked to input it again.</span></span> 

    # Windows DSVM      
    
    wget "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/TDSP/tdsp_local_copy_win.ps1" -outfile "tdsp_local_copy_win.ps1"
    .\tdsp_local_copy_win.ps1 1

![18](./media/group-manager-tasks/copy-two-folder-to-group-folder-windows-2.PNG)

<span data-ttu-id="a368a-253">Now you can see that files in directories LG1 and LG1 (except files in the .git directory) have been copied to LR1 and LR2, respectively.</span><span class="sxs-lookup"><span data-stu-id="a368a-253">Now you can see that files in directories LG1 and LG1 (except files in the .git directory) have been copied to LR1 and LR2, respectively.</span></span>

![19](./media/group-manager-tasks/copy-two-folder-to-group-folder-windows.PNG)

    # Linux DSVM

    wget "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/TDSP/tdsp_local_copy_linux.sh"
    bash tdsp_local_copy_linux.sh 1

![20](./media/group-manager-tasks/copy-two-folder-to-group-folder-linux-2.PNG)
        
<span data-ttu-id="a368a-256">Now you see that the files in the two folders (except files in the .git directory) are copied to GroupProjectTemplate and GroupUtilities respectively.</span><span class="sxs-lookup"><span data-stu-id="a368a-256">Now you see that the files in the two folders (except files in the .git directory) are copied to GroupProjectTemplate and GroupUtilities respectively.</span></span>
    
![21](./media/group-manager-tasks/copy-two-folder-to-group-folder-linux.PNG)

- <span data-ttu-id="a368a-258">Using our abbreviated repository names, this is what these scripts have achieved:</span><span class="sxs-lookup"><span data-stu-id="a368a-258">Using our abbreviated repository names, this is what these scripts have achieved:</span></span>
    - <span data-ttu-id="a368a-259">LG1 - files copied into -> LR1</span><span class="sxs-lookup"><span data-stu-id="a368a-259">LG1 - files copied into -> LR1</span></span>
    - <span data-ttu-id="a368a-260">LG2 - files copied into -> LR2</span><span class="sxs-lookup"><span data-stu-id="a368a-260">LG2 - files copied into -> LR2</span></span>

### <a name="option-to-customize-the-contents-of-lr1--lr2"></a><span data-ttu-id="a368a-261">Option to customize the contents of LR1 & LR2</span><span class="sxs-lookup"><span data-stu-id="a368a-261">Option to customize the contents of LR1 & LR2</span></span>
    
<span data-ttu-id="a368a-262">If you want to customize the contents of LR1 and LR2 to meet the specific needs of your group, this is the stage of the procedure where that is appropriate.</span><span class="sxs-lookup"><span data-stu-id="a368a-262">If you want to customize the contents of LR1 and LR2 to meet the specific needs of your group, this is the stage of the procedure where that is appropriate.</span></span> <span data-ttu-id="a368a-263">You can modify the template documents, change the directory structure, and add existing utilities that your group has developed or that are helpful for your entire group.</span><span class="sxs-lookup"><span data-stu-id="a368a-263">You can modify the template documents, change the directory structure, and add existing utilities that your group has developed or that are helpful for your entire group.</span></span> 

### <a name="add-the-contents-in-lr1--lr2-to-r1--r2-on-group-server"></a><span data-ttu-id="a368a-264">Add the contents in LR1 & LR2 to R1 & R2 on group server</span><span class="sxs-lookup"><span data-stu-id="a368a-264">Add the contents in LR1 & LR2 to R1 & R2 on group server</span></span>

<span data-ttu-id="a368a-265">Now, you need to add the contents in LR1 and LR2 to repositories R1 and R2.</span><span class="sxs-lookup"><span data-stu-id="a368a-265">Now, you need to add the contents in LR1 and LR2 to repositories R1 and R2.</span></span> <span data-ttu-id="a368a-266">Here are the git bash commands you can run in either Windows PowerShell or Linux.</span><span class="sxs-lookup"><span data-stu-id="a368a-266">Here are the git bash commands you can run in either Windows PowerShell or Linux.</span></span> 

<span data-ttu-id="a368a-267">Run the following commands from the GitRepos\GroupCommon\GroupProjectTemplate directory:</span><span class="sxs-lookup"><span data-stu-id="a368a-267">Run the following commands from the GitRepos\GroupCommon\GroupProjectTemplate directory:</span></span>

    git status
    git add .
    git commit -m"push from DSVM"
    git push

<span data-ttu-id="a368a-268">The -m option lets you set a message for your git commit.</span><span class="sxs-lookup"><span data-stu-id="a368a-268">The -m option lets you set a message for your git commit.</span></span>

![22](./media/group-manager-tasks/push-to-group-server-2.PNG)

<span data-ttu-id="a368a-270">You can see that in your group's Azure DevOps Services, in the GroupProjectTemplate repository, the files are synced instantly.</span><span class="sxs-lookup"><span data-stu-id="a368a-270">You can see that in your group's Azure DevOps Services, in the GroupProjectTemplate repository, the files are synced instantly.</span></span>

![23](./media/group-manager-tasks/push-to-group-server-showed-up-2.PNG)

<span data-ttu-id="a368a-272">Finally, change to the **GitRepos\GroupCommon\GroupUtilities** directory and run the same set of git bash commands:</span><span class="sxs-lookup"><span data-stu-id="a368a-272">Finally, change to the **GitRepos\GroupCommon\GroupUtilities** directory and run the same set of git bash commands:</span></span>

    git status
    git add .
    git commit -m"push from DSVM"
    git push

>[AZURE.NOTE] <span data-ttu-id="a368a-273">If this is the first time you commit to a Git repository, you need to configure global parameters *user.name* and *user.email* before you run the `git commit` command.</span><span class="sxs-lookup"><span data-stu-id="a368a-273">If this is the first time you commit to a Git repository, you need to configure global parameters *user.name* and *user.email* before you run the `git commit` command.</span></span> <span data-ttu-id="a368a-274">Run the following two commands:</span><span class="sxs-lookup"><span data-stu-id="a368a-274">Run the following two commands:</span></span>
        
    git config --global user.name <your name>
    git config --global user.email <your email address>
 
><span data-ttu-id="a368a-275">If you are committing to multiple Git repositories, use the same name and email address when you commit to each of them.</span><span class="sxs-lookup"><span data-stu-id="a368a-275">If you are committing to multiple Git repositories, use the same name and email address when you commit to each of them.</span></span> <span data-ttu-id="a368a-276">Using the same name and email address proves convenient later on when you build PowerBI dashboards to track your Git activities on multiple repositories.</span><span class="sxs-lookup"><span data-stu-id="a368a-276">Using the same name and email address proves convenient later on when you build PowerBI dashboards to track your Git activities on multiple repositories.</span></span>


- <span data-ttu-id="a368a-277">Using our abbreviated repository names, this is what these scripts have achieved:</span><span class="sxs-lookup"><span data-stu-id="a368a-277">Using our abbreviated repository names, this is what these scripts have achieved:</span></span>
    - <span data-ttu-id="a368a-278">LR1 - contents add to -> R1</span><span class="sxs-lookup"><span data-stu-id="a368a-278">LR1 - contents add to -> R1</span></span>
    - <span data-ttu-id="a368a-279">LR2 - contents add to -> R2</span><span class="sxs-lookup"><span data-stu-id="a368a-279">LR2 - contents add to -> R2</span></span>

## <a name="6-add-group-members-to-the-group-server"></a><span data-ttu-id="a368a-280">6. Add group members to the group server</span><span class="sxs-lookup"><span data-stu-id="a368a-280">6. Add group members to the group server</span></span>

<span data-ttu-id="a368a-281">From your group Azure DevOps Services's homepage, click the **gear icon** next to your user name in the upper right corner, then select the **Security** tab. You can add members to your group here with various permissions.</span><span class="sxs-lookup"><span data-stu-id="a368a-281">From your group Azure DevOps Services's homepage, click the **gear icon** next to your user name in the upper right corner, then select the **Security** tab. You can add members to your group here with various permissions.</span></span>

![24](./media/group-manager-tasks/add_member_to_group.PNG) 


## <a name="next-steps"></a><span data-ttu-id="a368a-283">Next steps</span><span class="sxs-lookup"><span data-stu-id="a368a-283">Next steps</span></span>

<span data-ttu-id="a368a-284">Here are links to the more detailed descriptions of the roles and tasks defined by the Team Data Science Process:</span><span class="sxs-lookup"><span data-stu-id="a368a-284">Here are links to the more detailed descriptions of the roles and tasks defined by the Team Data Science Process:</span></span>

- [<span data-ttu-id="a368a-285">Group Manager tasks for a data science team</span><span class="sxs-lookup"><span data-stu-id="a368a-285">Group Manager tasks for a data science team</span></span>](group-manager-tasks.md)
- [<span data-ttu-id="a368a-286">Team Lead tasks for a data science team</span><span class="sxs-lookup"><span data-stu-id="a368a-286">Team Lead tasks for a data science team</span></span>](team-lead-tasks.md)
- [<span data-ttu-id="a368a-287">Project Lead tasks for a data science team</span><span class="sxs-lookup"><span data-stu-id="a368a-287">Project Lead tasks for a data science team</span></span>](project-lead-tasks.md)
- [<span data-ttu-id="a368a-288">Project Individual Contributors for a data science team</span><span class="sxs-lookup"><span data-stu-id="a368a-288">Project Individual Contributors for a data science team</span></span>](project-ic-tasks.md)