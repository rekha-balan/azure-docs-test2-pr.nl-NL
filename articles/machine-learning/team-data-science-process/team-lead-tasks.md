---
title: Team Data Science Process Team Lead tasks - Azure  | Microsoft Docs
description: An outline of the tasks for a team lead on a data science team project.
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
ms.openlocfilehash: 86ab49cb0acd9ffee47fb1f8f531c3a0cd6e6730
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864686"
---
# <a name="team-lead-tasks"></a><span data-ttu-id="e49e7-103">Team Lead tasks</span><span class="sxs-lookup"><span data-stu-id="e49e7-103">Team Lead tasks</span></span>

<span data-ttu-id="e49e7-104">This topic outlines the tasks that a team lead is expected to complete for their data science team.</span><span class="sxs-lookup"><span data-stu-id="e49e7-104">This topic outlines the tasks that a team lead is expected to complete for their data science team.</span></span> <span data-ttu-id="e49e7-105">The objective is to establish collaborative team environment that standardizes on the [Team Data Science Process](overview.md) (TDSP).</span><span class="sxs-lookup"><span data-stu-id="e49e7-105">The objective is to establish collaborative team environment that standardizes on the [Team Data Science Process](overview.md) (TDSP).</span></span> <span data-ttu-id="e49e7-106">TDSP is an agile, iterative data science methodology to deliver predictive analytics solutions and intelligent applications efficiently.</span><span class="sxs-lookup"><span data-stu-id="e49e7-106">TDSP is an agile, iterative data science methodology to deliver predictive analytics solutions and intelligent applications efficiently.</span></span> <span data-ttu-id="e49e7-107">It is designed to help improve collaboration and team learning.</span><span class="sxs-lookup"><span data-stu-id="e49e7-107">It is designed to help improve collaboration and team learning.</span></span> <span data-ttu-id="e49e7-108">The process is a distillation of the best practices and structures from both Microsoft as well as from the industry, needed for successful implementation of data science initiatives to help companies fully realize the benefits of their analytics programs.</span><span class="sxs-lookup"><span data-stu-id="e49e7-108">The process is a distillation of the best practices and structures from both Microsoft as well as from the industry, needed for successful implementation of data science initiatives to help companies fully realize the benefits of their analytics programs.</span></span> <span data-ttu-id="e49e7-109">For an outline of the personnel roles and their associated tasks that are handled by a data science team standardizing on this process, see [Team Data Science Process roles and tasks](roles-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="e49e7-109">For an outline of the personnel roles and their associated tasks that are handled by a data science team standardizing on this process, see [Team Data Science Process roles and tasks](roles-tasks.md).</span></span>

<span data-ttu-id="e49e7-110">A **Team Lead** manages a team in the data science unit of an enterprise.</span><span class="sxs-lookup"><span data-stu-id="e49e7-110">A **Team Lead** manages a team in the data science unit of an enterprise.</span></span> <span data-ttu-id="e49e7-111">A team consists of multiple data scientists.</span><span class="sxs-lookup"><span data-stu-id="e49e7-111">A team consists of multiple data scientists.</span></span> <span data-ttu-id="e49e7-112">For data science unit with only a small number of data scientists, the **Group Manager** and the **Team Lead** might be the same person or they could delegate their task to a surrogate.</span><span class="sxs-lookup"><span data-stu-id="e49e7-112">For data science unit with only a small number of data scientists, the **Group Manager** and the **Team Lead** might be the same person or they could delegate their task to a surrogate.</span></span> <span data-ttu-id="e49e7-113">But the tasks themselves do not change.</span><span class="sxs-lookup"><span data-stu-id="e49e7-113">But the tasks themselves do not change.</span></span> <span data-ttu-id="e49e7-114">The workflow for the tasks to be completed by team leads to set up this environment are depicted in the following figure:</span><span class="sxs-lookup"><span data-stu-id="e49e7-114">The workflow for the tasks to be completed by team leads to set up this environment are depicted in the following figure:</span></span>

![1](./media/team-lead-tasks/team-leads-1-creating-teams.png)

>[AZURE.NOTE] <span data-ttu-id="e49e7-116">The tasks in blocks 1 and 2 of the figure are needed if you are using Azure DevOps as the code hosting platform and you want to have a separate Azure DevOps project for your own team.</span><span class="sxs-lookup"><span data-stu-id="e49e7-116">The tasks in blocks 1 and 2 of the figure are needed if you are using Azure DevOps as the code hosting platform and you want to have a separate Azure DevOps project for your own team.</span></span> <span data-ttu-id="e49e7-117">Once these tasks are completed, all repositories of your team can be created under this project.</span><span class="sxs-lookup"><span data-stu-id="e49e7-117">Once these tasks are completed, all repositories of your team can be created under this project.</span></span> 

<span data-ttu-id="e49e7-118">After several prerequisites tasks specified in a following section are satisfied by the group manager, there are the five principal tasks (some optional) that you complete in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="e49e7-118">After several prerequisites tasks specified in a following section are satisfied by the group manager, there are the five principal tasks (some optional) that you complete in this tutorial.</span></span> <span data-ttu-id="e49e7-119">These tasks correspond the main numbered sections of this topic:</span><span class="sxs-lookup"><span data-stu-id="e49e7-119">These tasks correspond the main numbered sections of this topic:</span></span>

1. <span data-ttu-id="e49e7-120">Create a **project** on the group's Azure DevOps Services of the group and two team repositories in the project:</span><span class="sxs-lookup"><span data-stu-id="e49e7-120">Create a **project** on the group's Azure DevOps Services of the group and two team repositories in the project:</span></span>
    - <span data-ttu-id="e49e7-121">**ProjectTemplate repository**</span><span class="sxs-lookup"><span data-stu-id="e49e7-121">**ProjectTemplate repository**</span></span> 
    - <span data-ttu-id="e49e7-122">**TeamUtilities repository**</span><span class="sxs-lookup"><span data-stu-id="e49e7-122">**TeamUtilities repository**</span></span>
2. <span data-ttu-id="e49e7-123">Seed the team **ProjectTemplate** repository from the **GroupProjectTemplate** repository which has been set up by your group manager.</span><span class="sxs-lookup"><span data-stu-id="e49e7-123">Seed the team **ProjectTemplate** repository from the **GroupProjectTemplate** repository which has been set up by your group manager.</span></span> 
3. <span data-ttu-id="e49e7-124">Create team data and analytics resources:</span><span class="sxs-lookup"><span data-stu-id="e49e7-124">Create team data and analytics resources:</span></span>
    - <span data-ttu-id="e49e7-125">Add the team-specific utilities to the **TeamUtilities** repository.</span><span class="sxs-lookup"><span data-stu-id="e49e7-125">Add the team-specific utilities to the **TeamUtilities** repository.</span></span> 
    - <span data-ttu-id="e49e7-126">(Optional) Create an **Azure file storage** to be used to store data assets that can be useful for the entire team.</span><span class="sxs-lookup"><span data-stu-id="e49e7-126">(Optional) Create an **Azure file storage** to be used to store data assets that can be useful for the entire team.</span></span> 
4. <span data-ttu-id="e49e7-127">(Optional) Mount the Azure file storage to the **Data Science Virtual Machine** (DSVM) of the team lead and add data assets on it.</span><span class="sxs-lookup"><span data-stu-id="e49e7-127">(Optional) Mount the Azure file storage to the **Data Science Virtual Machine** (DSVM) of the team lead and add data assets on it.</span></span>
5. <span data-ttu-id="e49e7-128">Set up the **security control** by adding team members and configure their privileges.</span><span class="sxs-lookup"><span data-stu-id="e49e7-128">Set up the **security control** by adding team members and configure their privileges.</span></span>

>[AZURE.NOTE] <span data-ttu-id="e49e7-129">We outline the steps needed to set up a TDSP team environment using Azure DevOps in the following instructions.</span><span class="sxs-lookup"><span data-stu-id="e49e7-129">We outline the steps needed to set up a TDSP team environment using Azure DevOps in the following instructions.</span></span> <span data-ttu-id="e49e7-130">We specify how to accomplish these tasks with Azure DevOps because that is how we implement TDSP at Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e49e7-130">We specify how to accomplish these tasks with Azure DevOps because that is how we implement TDSP at Microsoft.</span></span> <span data-ttu-id="e49e7-131">If another code hosting platform is used for your group, the tasks that need to be completed by the team lead generally do not change.</span><span class="sxs-lookup"><span data-stu-id="e49e7-131">If another code hosting platform is used for your group, the tasks that need to be completed by the team lead generally do not change.</span></span> <span data-ttu-id="e49e7-132">But the way to complete these tasks is going to be different.</span><span class="sxs-lookup"><span data-stu-id="e49e7-132">But the way to complete these tasks is going to be different.</span></span>

## <a name="repositories-and-directories"></a><span data-ttu-id="e49e7-133">Repositories and directories</span><span class="sxs-lookup"><span data-stu-id="e49e7-133">Repositories and directories</span></span>

<span data-ttu-id="e49e7-134">This topic   uses abbreviated names for repositories and directories.</span><span class="sxs-lookup"><span data-stu-id="e49e7-134">This topic   uses abbreviated names for repositories and directories.</span></span> <span data-ttu-id="e49e7-135">These names make it easier to follow the operations between the repositories and directories.</span><span class="sxs-lookup"><span data-stu-id="e49e7-135">These names make it easier to follow the operations between the repositories and directories.</span></span> <span data-ttu-id="e49e7-136">This notation (**R** for Git repositories and **D** for local directories on your DSVM) is used in the following sections:</span><span class="sxs-lookup"><span data-stu-id="e49e7-136">This notation (**R** for Git repositories and **D** for local directories on your DSVM) is used in the following sections:</span></span>

- <span data-ttu-id="e49e7-137">**R1**: The **GroupProjectTemplate** repository on Git that your group manager set up on your Azure DevOps group server.</span><span class="sxs-lookup"><span data-stu-id="e49e7-137">**R1**: The **GroupProjectTemplate** repository on Git that your group manager set up on your Azure DevOps group server.</span></span>
- <span data-ttu-id="e49e7-138">**R3**: The team **ProjectTemplate** repository on Git you set up.</span><span class="sxs-lookup"><span data-stu-id="e49e7-138">**R3**: The team **ProjectTemplate** repository on Git you set up.</span></span>
- <span data-ttu-id="e49e7-139">**R4**: The **TeamUtilities** repository on Git you set up.</span><span class="sxs-lookup"><span data-stu-id="e49e7-139">**R4**: The **TeamUtilities** repository on Git you set up.</span></span>
- <span data-ttu-id="e49e7-140">**D1**: The local directory cloned from R1 and copied to D3.</span><span class="sxs-lookup"><span data-stu-id="e49e7-140">**D1**: The local directory cloned from R1 and copied to D3.</span></span>
- <span data-ttu-id="e49e7-141">**D3**: The local directory cloned from R3, customize, and copied back to R3.</span><span class="sxs-lookup"><span data-stu-id="e49e7-141">**D3**: The local directory cloned from R3, customize, and copied back to R3.</span></span>
- <span data-ttu-id="e49e7-142">**D4**: The local directory cloned from R4, customize, and copied back to R4.</span><span class="sxs-lookup"><span data-stu-id="e49e7-142">**D4**: The local directory cloned from R4, customize, and copied back to R4.</span></span>

<span data-ttu-id="e49e7-143">The names specified for the repositories and directories in this tutorial have been provided on the assumption that your objective is to establish a separate project for your own team within a larger data science group.</span><span class="sxs-lookup"><span data-stu-id="e49e7-143">The names specified for the repositories and directories in this tutorial have been provided on the assumption that your objective is to establish a separate project for your own team within a larger data science group.</span></span> <span data-ttu-id="e49e7-144">But there are other options open to you as team lead:</span><span class="sxs-lookup"><span data-stu-id="e49e7-144">But there are other options open to you as team lead:</span></span>

- <span data-ttu-id="e49e7-145">The entire group can choose to create a single project.</span><span class="sxs-lookup"><span data-stu-id="e49e7-145">The entire group can choose to create a single project.</span></span> <span data-ttu-id="e49e7-146">Then all projects from all data science teams would be under this single project.</span><span class="sxs-lookup"><span data-stu-id="e49e7-146">Then all projects from all data science teams would be under this single project.</span></span> <span data-ttu-id="e49e7-147">To achieve this, you can designate a git administrator to follow these instructions to create a single project.</span><span class="sxs-lookup"><span data-stu-id="e49e7-147">To achieve this, you can designate a git administrator to follow these instructions to create a single project.</span></span> <span data-ttu-id="e49e7-148">This scenario might be valid, for example, for:</span><span class="sxs-lookup"><span data-stu-id="e49e7-148">This scenario might be valid, for example, for:</span></span>
    -  <span data-ttu-id="e49e7-149">a small data science group that does not have multiple data science teams</span><span class="sxs-lookup"><span data-stu-id="e49e7-149">a small data science group that does not have multiple data science teams</span></span> 
    -  <span data-ttu-id="e49e7-150">a larger data science group with multiple data science teams that nevertheless wants to optimize inter-team collaboration with activities such as group-level sprint planning.</span><span class="sxs-lookup"><span data-stu-id="e49e7-150">a larger data science group with multiple data science teams that nevertheless wants to optimize inter-team collaboration with activities such as group-level sprint planning.</span></span> 
- <span data-ttu-id="e49e7-151">Teams can choose to have team-specific project templates or team-specific utilities under the single project for the entire group.</span><span class="sxs-lookup"><span data-stu-id="e49e7-151">Teams can choose to have team-specific project templates or team-specific utilities under the single project for the entire group.</span></span> <span data-ttu-id="e49e7-152">In this case, the team leads should create project template repositories and/or team utilities repositories under the same project.</span><span class="sxs-lookup"><span data-stu-id="e49e7-152">In this case, the team leads should create project template repositories and/or team utilities repositories under the same project.</span></span> <span data-ttu-id="e49e7-153">Name these repositories *<TeamName\>ProjectTemplate* and *<TeamName\>Utilities*, for instance, *TeamJohnProjectTemplate* and *TeamJohnUtilities*.</span><span class="sxs-lookup"><span data-stu-id="e49e7-153">Name these repositories *<TeamName\>ProjectTemplate* and *<TeamName\>Utilities*, for instance, *TeamJohnProjectTemplate* and *TeamJohnUtilities*.</span></span> 

<span data-ttu-id="e49e7-154">In any case, team leads need to let their team members know which template and utilities repositories to adopt when they are setting up and cloning the project and utilities repositories.</span><span class="sxs-lookup"><span data-stu-id="e49e7-154">In any case, team leads need to let their team members know which template and utilities repositories to adopt when they are setting up and cloning the project and utilities repositories.</span></span> <span data-ttu-id="e49e7-155">Project leads should follow the [Project Lead tasks for a data science team](project-lead-tasks.md) to create project repositories, whether under separate projects or under a single project.</span><span class="sxs-lookup"><span data-stu-id="e49e7-155">Project leads should follow the [Project Lead tasks for a data science team](project-lead-tasks.md) to create project repositories, whether under separate projects or under a single project.</span></span> 


## <a name="0-prerequisites"></a><span data-ttu-id="e49e7-156">0. Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e49e7-156">0. Prerequisites</span></span>

<span data-ttu-id="e49e7-157">The prerequisites are satisfied by completing the tasks assigned to your group manager outlined in [Group Manager tasks for a data science team](group-manager-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="e49e7-157">The prerequisites are satisfied by completing the tasks assigned to your group manager outlined in [Group Manager tasks for a data science team](group-manager-tasks.md).</span></span> <span data-ttu-id="e49e7-158">To summarize here, the following requirements need to meet before you begin the team lead tasks:</span><span class="sxs-lookup"><span data-stu-id="e49e7-158">To summarize here, the following requirements need to meet before you begin the team lead tasks:</span></span> 

- <span data-ttu-id="e49e7-159">Your **group Azure DevOps Services** (or group account on some other code hosting platform) has been set up by your group manager.</span><span class="sxs-lookup"><span data-stu-id="e49e7-159">Your **group Azure DevOps Services** (or group account on some other code hosting platform) has been set up by your group manager.</span></span>
- <span data-ttu-id="e49e7-160">Your **GroupProjectTemplate repository** (R1) has been set up on your group account by your group manager on the code hosting platform you plan to use.</span><span class="sxs-lookup"><span data-stu-id="e49e7-160">Your **GroupProjectTemplate repository** (R1) has been set up on your group account by your group manager on the code hosting platform you plan to use.</span></span>
- <span data-ttu-id="e49e7-161">You have been **authorized** on your group account to create repositories for your team.</span><span class="sxs-lookup"><span data-stu-id="e49e7-161">You have been **authorized** on your group account to create repositories for your team.</span></span>
- <span data-ttu-id="e49e7-162">Git must be installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="e49e7-162">Git must be installed on your machine.</span></span> <span data-ttu-id="e49e7-163">If you are using a Data Science Virtual Machine (DSVM), Git has been pre-installed and you are good to go.</span><span class="sxs-lookup"><span data-stu-id="e49e7-163">If you are using a Data Science Virtual Machine (DSVM), Git has been pre-installed and you are good to go.</span></span> <span data-ttu-id="e49e7-164">Otherwise, see the [Platforms and tools appendix](platforms-and-tools.md#appendix).</span><span class="sxs-lookup"><span data-stu-id="e49e7-164">Otherwise, see the [Platforms and tools appendix](platforms-and-tools.md#appendix).</span></span>  
- <span data-ttu-id="e49e7-165">If you are using a **Windows DSVM**, you need to have [Git Credential Manager (GCM)](https://github.com/Microsoft/Git-Credential-Manager-for-Windows) installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="e49e7-165">If you are using a **Windows DSVM**, you need to have [Git Credential Manager (GCM)](https://github.com/Microsoft/Git-Credential-Manager-for-Windows) installed on your machine.</span></span> <span data-ttu-id="e49e7-166">In the README.md file, scroll down to the **Download and Install** section and click the *latest installer*.</span><span class="sxs-lookup"><span data-stu-id="e49e7-166">In the README.md file, scroll down to the **Download and Install** section and click the *latest installer*.</span></span> <span data-ttu-id="e49e7-167">This takes you to the latest installer page.</span><span class="sxs-lookup"><span data-stu-id="e49e7-167">This takes you to the latest installer page.</span></span> <span data-ttu-id="e49e7-168">Download the .exe installer from here and run it.</span><span class="sxs-lookup"><span data-stu-id="e49e7-168">Download the .exe installer from here and run it.</span></span> 
- <span data-ttu-id="e49e7-169">If you are using **Linux DSVM**, create an SSH public key on your DSVM and add it to your group Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="e49e7-169">If you are using **Linux DSVM**, create an SSH public key on your DSVM and add it to your group Azure DevOps Services.</span></span> <span data-ttu-id="e49e7-170">For more information about SSH, see the **Create SSH public key** section in the [Platforms and tools appendix](platforms-and-tools.md#appendix).</span><span class="sxs-lookup"><span data-stu-id="e49e7-170">For more information about SSH, see the **Create SSH public key** section in the [Platforms and tools appendix](platforms-and-tools.md#appendix).</span></span> 
    
## <a name="1-create-a-project-and-repositories"></a><span data-ttu-id="e49e7-171">1. Create a project and repositories</span><span class="sxs-lookup"><span data-stu-id="e49e7-171">1. Create a project and repositories</span></span>

<span data-ttu-id="e49e7-172">Complete this step if you are using Azure DevOps as your code hosting platform for versioning and collaboration.</span><span class="sxs-lookup"><span data-stu-id="e49e7-172">Complete this step if you are using Azure DevOps as your code hosting platform for versioning and collaboration.</span></span> <span data-ttu-id="e49e7-173">This section has you create three artifacts in the Azure DevOps Services of your group:</span><span class="sxs-lookup"><span data-stu-id="e49e7-173">This section has you create three artifacts in the Azure DevOps Services of your group:</span></span>

- <span data-ttu-id="e49e7-174">**MyTeam** project in Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="e49e7-174">**MyTeam** project in Azure DevOps</span></span>
- <span data-ttu-id="e49e7-175">**MyProjectTemplate** repository (**R3**) on Git</span><span class="sxs-lookup"><span data-stu-id="e49e7-175">**MyProjectTemplate** repository (**R3**) on Git</span></span>
- <span data-ttu-id="e49e7-176">**MyTeamUtilities** repository (**R4**) on Git</span><span class="sxs-lookup"><span data-stu-id="e49e7-176">**MyTeamUtilities** repository (**R4**) on Git</span></span>

### <a name="create-the-myteam-project"></a><span data-ttu-id="e49e7-177">Create the MyTeam project</span><span class="sxs-lookup"><span data-stu-id="e49e7-177">Create the MyTeam project</span></span>

- <span data-ttu-id="e49e7-178">Go to your group's Azure DevOps Services homepage at URL `https://<Azure DevOps Services Name\>.visualstudio.com`.</span><span class="sxs-lookup"><span data-stu-id="e49e7-178">Go to your group's Azure DevOps Services homepage at URL `https://<Azure DevOps Services Name\>.visualstudio.com`.</span></span> 
- <span data-ttu-id="e49e7-179">Click **New** to create a project.</span><span class="sxs-lookup"><span data-stu-id="e49e7-179">Click **New** to create a project.</span></span> 

    ![2](./media/team-lead-tasks/team-leads-2-create-new-team.png)

- <span data-ttu-id="e49e7-181">A Create project window asks you to input the Project name (**MyTeam** in this example).</span><span class="sxs-lookup"><span data-stu-id="e49e7-181">A Create project window asks you to input the Project name (**MyTeam** in this example).</span></span> <span data-ttu-id="e49e7-182">Make sure that you select **Agile** as the **Process template** and **Git** as the **Version control**.</span><span class="sxs-lookup"><span data-stu-id="e49e7-182">Make sure that you select **Agile** as the **Process template** and **Git** as the **Version control**.</span></span> 

    ![3](./media/team-lead-tasks/team-leads-3-create-new-team-2.png)

- <span data-ttu-id="e49e7-184">Click **Create project**.</span><span class="sxs-lookup"><span data-stu-id="e49e7-184">Click **Create project**.</span></span> <span data-ttu-id="e49e7-185">Your project **MyTeam** is created in less than 1 minute.</span><span class="sxs-lookup"><span data-stu-id="e49e7-185">Your project **MyTeam** is created in less than 1 minute.</span></span> 

- <span data-ttu-id="e49e7-186">After the project **MyTeam** is created, click **Navigate to project** button, to be directed to the home page of your project.</span><span class="sxs-lookup"><span data-stu-id="e49e7-186">After the project **MyTeam** is created, click **Navigate to project** button, to be directed to the home page of your project.</span></span> 

    ![4](./media/team-lead-tasks/team-leads-4-create-new-team-3.png)

- <span data-ttu-id="e49e7-188">If you see a **Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="e49e7-188">If you see a **Congratulations!**</span></span> <span data-ttu-id="e49e7-189">popup window, click the **Add code** (button in red box).</span><span class="sxs-lookup"><span data-stu-id="e49e7-189">popup window, click the **Add code** (button in red box).</span></span> <span data-ttu-id="e49e7-190">Otherwise, click **Code** (in yellow box).</span><span class="sxs-lookup"><span data-stu-id="e49e7-190">Otherwise, click **Code** (in yellow box).</span></span> <span data-ttu-id="e49e7-191">This directs you to the Git repository page of your project.</span><span class="sxs-lookup"><span data-stu-id="e49e7-191">This directs you to the Git repository page of your project.</span></span> 

    ![5](./media/team-lead-tasks/team-leads-5-team-project-home.png)

### <a name="create-the-myprojecttemplate-repository-r3-on-git"></a><span data-ttu-id="e49e7-193">Create the MyProjectTemplate repository (R3) on Git</span><span class="sxs-lookup"><span data-stu-id="e49e7-193">Create the MyProjectTemplate repository (R3) on Git</span></span>

- <span data-ttu-id="e49e7-194">On the Git repository page of your project, click the downward arrow beside repository name **MyTeam**, and select **Manage repositories...**.</span><span class="sxs-lookup"><span data-stu-id="e49e7-194">On the Git repository page of your project, click the downward arrow beside repository name **MyTeam**, and select **Manage repositories...**.</span></span>

    ![6](./media/team-lead-tasks/team-leads-6-rename-team-project-repo.png)

- <span data-ttu-id="e49e7-196">On the **Version control** tab of the control panel of your project, click **MyTeam**, then select **Rename repository...**.</span><span class="sxs-lookup"><span data-stu-id="e49e7-196">On the **Version control** tab of the control panel of your project, click **MyTeam**, then select **Rename repository...**.</span></span> 

    ![7](./media/team-lead-tasks/team-leads-7-rename-team-project-repo-2.png)

- <span data-ttu-id="e49e7-198">Input a new name to the repository in the **Rename the MyTeam repository** window.</span><span class="sxs-lookup"><span data-stu-id="e49e7-198">Input a new name to the repository in the **Rename the MyTeam repository** window.</span></span> <span data-ttu-id="e49e7-199">In this example, *MyTeamProjectTemplate*.</span><span class="sxs-lookup"><span data-stu-id="e49e7-199">In this example, *MyTeamProjectTemplate*.</span></span> <span data-ttu-id="e49e7-200">You can choose something like *<Your team name\>ProjectTemplate*.</span><span class="sxs-lookup"><span data-stu-id="e49e7-200">You can choose something like *<Your team name\>ProjectTemplate*.</span></span> <span data-ttu-id="e49e7-201">Click **Rename** to continue.</span><span class="sxs-lookup"><span data-stu-id="e49e7-201">Click **Rename** to continue.</span></span>

    ![8](./media/team-lead-tasks/team-leads-8-rename-team-project-repo-3.png)

### <a name="create-the-myteamutilities-repository-r4-on-git"></a><span data-ttu-id="e49e7-203">Create the MyTeamUtilities repository (R4) on Git</span><span class="sxs-lookup"><span data-stu-id="e49e7-203">Create the MyTeamUtilities repository (R4) on Git</span></span>

- <span data-ttu-id="e49e7-204">To create a new repository *<your team name\>Utilities* under your project, click **New repository...** on the **Version control** tab of your project's control panel.</span><span class="sxs-lookup"><span data-stu-id="e49e7-204">To create a new repository *<your team name\>Utilities* under your project, click **New repository...** on the **Version control** tab of your project's control panel.</span></span>  

    ![9](./media/team-lead-tasks/team-leads-9-create-team-utilities.png)

- <span data-ttu-id="e49e7-206">In the **Create a new repository** window that pops up, provide a name for this repository.</span><span class="sxs-lookup"><span data-stu-id="e49e7-206">In the **Create a new repository** window that pops up, provide a name for this repository.</span></span> <span data-ttu-id="e49e7-207">In this example, we name it as *MyTeamUtilities*, which is **R4** in our notation.</span><span class="sxs-lookup"><span data-stu-id="e49e7-207">In this example, we name it as *MyTeamUtilities*, which is **R4** in our notation.</span></span> <span data-ttu-id="e49e7-208">Choose something like *<your team name\>Utilities*.</span><span class="sxs-lookup"><span data-stu-id="e49e7-208">Choose something like *<your team name\>Utilities*.</span></span> <span data-ttu-id="e49e7-209">Make sure that you select **Git** for **Type**.</span><span class="sxs-lookup"><span data-stu-id="e49e7-209">Make sure that you select **Git** for **Type**.</span></span> <span data-ttu-id="e49e7-210">Then, click **Create** to continue.</span><span class="sxs-lookup"><span data-stu-id="e49e7-210">Then, click **Create** to continue.</span></span>

    ![10](./media/team-lead-tasks/team-leads-10-create-team-utilities-2.png)

- <span data-ttu-id="e49e7-212">Confirm that you see the two new Git repositories created under your project **MyTeam**.</span><span class="sxs-lookup"><span data-stu-id="e49e7-212">Confirm that you see the two new Git repositories created under your project **MyTeam**.</span></span> <span data-ttu-id="e49e7-213">In this example:</span><span class="sxs-lookup"><span data-stu-id="e49e7-213">In this example:</span></span> 

- <span data-ttu-id="e49e7-214">**MyTeamProjectTemplate** (R3)</span><span class="sxs-lookup"><span data-stu-id="e49e7-214">**MyTeamProjectTemplate** (R3)</span></span> 
- <span data-ttu-id="e49e7-215">**MyTeamUtilities** (R4).</span><span class="sxs-lookup"><span data-stu-id="e49e7-215">**MyTeamUtilities** (R4).</span></span>

    ![11](./media/team-lead-tasks/team-leads-11-two-repo-in-team.png)


## <a name="2-seed-your-projecttemplate-and-teamutilities-repositories"></a><span data-ttu-id="e49e7-217">2. Seed your ProjectTemplate and TeamUtilities repositories</span><span class="sxs-lookup"><span data-stu-id="e49e7-217">2. Seed your ProjectTemplate and TeamUtilities repositories</span></span>

<span data-ttu-id="e49e7-218">The seeding procedure uses the directories on your local DSVM as intermediate staging sites.</span><span class="sxs-lookup"><span data-stu-id="e49e7-218">The seeding procedure uses the directories on your local DSVM as intermediate staging sites.</span></span> <span data-ttu-id="e49e7-219">If you need to customize your **ProjectTemplate** and **TeamUtilities** repositories to meet some specific team needs, you do so in the penultimate step of following procedure.</span><span class="sxs-lookup"><span data-stu-id="e49e7-219">If you need to customize your **ProjectTemplate** and **TeamUtilities** repositories to meet some specific team needs, you do so in the penultimate step of following procedure.</span></span> <span data-ttu-id="e49e7-220">Here is a summary of the steps used to seed the content of the **MyTeamProjectTemplate** and **MyTeamUtilities** repositories for a data science team.</span><span class="sxs-lookup"><span data-stu-id="e49e7-220">Here is a summary of the steps used to seed the content of the **MyTeamProjectTemplate** and **MyTeamUtilities** repositories for a data science team.</span></span> <span data-ttu-id="e49e7-221">The individual steps correspond to the subsections in the seeding procedure:</span><span class="sxs-lookup"><span data-stu-id="e49e7-221">The individual steps correspond to the subsections in the seeding procedure:</span></span>

- <span data-ttu-id="e49e7-222">Clone group repository into local directory: team R1 - cloned to -> local D1</span><span class="sxs-lookup"><span data-stu-id="e49e7-222">Clone group repository into local directory: team R1 - cloned to -> local D1</span></span>
- <span data-ttu-id="e49e7-223">Clone your team repositories into local directories: team R3 & R4 - cloned to -> local D3 & D4</span><span class="sxs-lookup"><span data-stu-id="e49e7-223">Clone your team repositories into local directories: team R3 & R4 - cloned to -> local D3 & D4</span></span>
- <span data-ttu-id="e49e7-224">Copy the group project template content to the local team folder:  D1 - contents copied to -> D3</span><span class="sxs-lookup"><span data-stu-id="e49e7-224">Copy the group project template content to the local team folder:  D1 - contents copied to -> D3</span></span>
- <span data-ttu-id="e49e7-225">(Optional) customization of local D3 & D4</span><span class="sxs-lookup"><span data-stu-id="e49e7-225">(Optional) customization of local D3 & D4</span></span>
- <span data-ttu-id="e49e7-226">Push local directory content to team repositories: D3 & D4 - contents add to -> team R3 & R4</span><span class="sxs-lookup"><span data-stu-id="e49e7-226">Push local directory content to team repositories: D3 & D4 - contents add to -> team R3 & R4</span></span>


### <a name="initialize-the-team-repositories"></a><span data-ttu-id="e49e7-227">Initialize the team repositories</span><span class="sxs-lookup"><span data-stu-id="e49e7-227">Initialize the team repositories</span></span>

<span data-ttu-id="e49e7-228">In this step, you initialize your project template repository from the group project template repository:</span><span class="sxs-lookup"><span data-stu-id="e49e7-228">In this step, you initialize your project template repository from the group project template repository:</span></span>

- <span data-ttu-id="e49e7-229">**MyTeamProjectTemplate** repository (**R3**) from your **GroupProjectTemplate** (**R1**) repository</span><span class="sxs-lookup"><span data-stu-id="e49e7-229">**MyTeamProjectTemplate** repository (**R3**) from your **GroupProjectTemplate** (**R1**) repository</span></span>


### <a name="clone-group-repositories-into-local-directories"></a><span data-ttu-id="e49e7-230">Clone group repositories into local directories</span><span class="sxs-lookup"><span data-stu-id="e49e7-230">Clone group repositories into local directories</span></span>

<span data-ttu-id="e49e7-231">To begin this procedure:</span><span class="sxs-lookup"><span data-stu-id="e49e7-231">To begin this procedure:</span></span>

- <span data-ttu-id="e49e7-232">Create directories on your local machine:</span><span class="sxs-lookup"><span data-stu-id="e49e7-232">Create directories on your local machine:</span></span>
    - <span data-ttu-id="e49e7-233">For **Windows**: **C:\GitRepos\GroupCommon** and **C:\GitRepos\MyTeam**</span><span class="sxs-lookup"><span data-stu-id="e49e7-233">For **Windows**: **C:\GitRepos\GroupCommon** and **C:\GitRepos\MyTeam**</span></span>
    - <span data-ttu-id="e49e7-234">For **Linux**: **GitRepos\GroupCommon** and **GitRepos\MyTeam** on your home directory</span><span class="sxs-lookup"><span data-stu-id="e49e7-234">For **Linux**: **GitRepos\GroupCommon** and **GitRepos\MyTeam** on your home directory</span></span> 
- <span data-ttu-id="e49e7-235">Change to directory **GitRepos\GroupCommon**.</span><span class="sxs-lookup"><span data-stu-id="e49e7-235">Change to directory **GitRepos\GroupCommon**.</span></span>
- <span data-ttu-id="e49e7-236">Run the following command, as appropriate, on the operating system of your local machine.</span><span class="sxs-lookup"><span data-stu-id="e49e7-236">Run the following command, as appropriate, on the operating system of your local machine.</span></span>

<span data-ttu-id="e49e7-237">**Windows**</span><span class="sxs-lookup"><span data-stu-id="e49e7-237">**Windows**</span></span>

    git clone https://<Your Azure DevOps Services name>.visualstudio.com/GroupCommon/_git/GroupProjectTemplate
    

![12](./media/team-lead-tasks/team-leads-12-create-two-group-repos.png)

<span data-ttu-id="e49e7-239">**Linux**</span><span class="sxs-lookup"><span data-stu-id="e49e7-239">**Linux**</span></span>
    
    git clone ssh://<Your Azure DevOps Services name>@<Your Azure DevOps Services name>.visualstudio.com:22/GroupCommon/_git/GroupProjectTemplate
    
    
![13](./media/team-lead-tasks/team-leads-13-clone_two_group_repos_linux.png)

<span data-ttu-id="e49e7-241">These commands clone your **GroupProjectTemplate** (R1) repository on your group Azure DevOps Services to local directory in **GitRepos\GroupCommon** on your local machine.</span><span class="sxs-lookup"><span data-stu-id="e49e7-241">These commands clone your **GroupProjectTemplate** (R1) repository on your group Azure DevOps Services to local directory in **GitRepos\GroupCommon** on your local machine.</span></span> <span data-ttu-id="e49e7-242">After cloning, directory **GroupProjectTemplate** (D1) is created in directory **GitRepos\GroupCommon**.</span><span class="sxs-lookup"><span data-stu-id="e49e7-242">After cloning, directory **GroupProjectTemplate** (D1) is created in directory **GitRepos\GroupCommon**.</span></span> <span data-ttu-id="e49e7-243">Here, we assume that your group manager created a project **GroupCommon**, and the **GroupProjectTemplate** repository is under this project.</span><span class="sxs-lookup"><span data-stu-id="e49e7-243">Here, we assume that your group manager created a project **GroupCommon**, and the **GroupProjectTemplate** repository is under this project.</span></span> 


### <a name="clone-your-team-repositories-into-local-directories"></a><span data-ttu-id="e49e7-244">Clone your team repositories into local directories</span><span class="sxs-lookup"><span data-stu-id="e49e7-244">Clone your team repositories into local directories</span></span>

<span data-ttu-id="e49e7-245">These commands clone your **MyTeamProjectTemplate** (R3) and **MyTeamUtilities** (R4) repositories under your project **MyTeam** on your group Azure DevOps Services to the **MyTeamProjectTemplate** (D3) and **MyTeamUtilities** (D4) directories in **GitRepos\MyTeam** on your local machine.</span><span class="sxs-lookup"><span data-stu-id="e49e7-245">These commands clone your **MyTeamProjectTemplate** (R3) and **MyTeamUtilities** (R4) repositories under your project **MyTeam** on your group Azure DevOps Services to the **MyTeamProjectTemplate** (D3) and **MyTeamUtilities** (D4) directories in **GitRepos\MyTeam** on your local machine.</span></span> 

- <span data-ttu-id="e49e7-246">Change to directory **GitRepos\MyTeam**</span><span class="sxs-lookup"><span data-stu-id="e49e7-246">Change to directory **GitRepos\MyTeam**</span></span>
- <span data-ttu-id="e49e7-247">Run the following commands, as appropriate, on the operating system of your local machine.</span><span class="sxs-lookup"><span data-stu-id="e49e7-247">Run the following commands, as appropriate, on the operating system of your local machine.</span></span> 

<span data-ttu-id="e49e7-248">**Windows**</span><span class="sxs-lookup"><span data-stu-id="e49e7-248">**Windows**</span></span>

    git clone https://<Your Azure DevOps Services name>.visualstudio.com/<Your Team Name>/_git/MyTeamProjectTemplate
    git clone https://<Your Azure DevOps Services name>.visualstudio.com/<Your Team Name>/_git/MyTeamUtilities

![14](./media/team-lead-tasks/team-leads-14-clone_two_empty_team_repos.png)
        
<span data-ttu-id="e49e7-250">**Linux**</span><span class="sxs-lookup"><span data-stu-id="e49e7-250">**Linux**</span></span>
    
    git clone ssh://<Your Azure DevOps Services name>@<Your Azure DevOps Services name>.visualstudio.com:22/<Your Team Name>/_git/MyTeamProjectTemplate
    git clone ssh://<Your Azure DevOps Services name>@<Your Azure DevOps Services name>.visualstudio.com:22/<Your Team Name>/_git/MyTeamUtilities
    
![15](./media/team-lead-tasks/team-leads-15-clone_two_empty_team_repos_linux.png)

<span data-ttu-id="e49e7-252">After cloning, two directories **MyTeamProjectTemplate** (D3) and **MyTeamUtilities** (D4) are created in directory **GitRepos\MyTeam**.</span><span class="sxs-lookup"><span data-stu-id="e49e7-252">After cloning, two directories **MyTeamProjectTemplate** (D3) and **MyTeamUtilities** (D4) are created in directory **GitRepos\MyTeam**.</span></span> <span data-ttu-id="e49e7-253">We have assumed here that you named your project template and utilities repositories **MyTeamProjectTemplate** and **MyTeamUtilities**.</span><span class="sxs-lookup"><span data-stu-id="e49e7-253">We have assumed here that you named your project template and utilities repositories **MyTeamProjectTemplate** and **MyTeamUtilities**.</span></span> 

### <a name="copy-the-group-project-template-content-to-the-local-project-template-directory"></a><span data-ttu-id="e49e7-254">Copy the group project template content to the local project template directory</span><span class="sxs-lookup"><span data-stu-id="e49e7-254">Copy the group project template content to the local project template directory</span></span>

<span data-ttu-id="e49e7-255">To copy the content of the local **GroupProjectTemplate** (D1) folder to the local **MyTeamProjectTemplate** (D3), run one of the following shell scripts:</span><span class="sxs-lookup"><span data-stu-id="e49e7-255">To copy the content of the local **GroupProjectTemplate** (D1) folder to the local **MyTeamProjectTemplate** (D3), run one of the following shell scripts:</span></span> 

#### <a name="from-the-powershell-command-line-for-windows"></a><span data-ttu-id="e49e7-256">From the PowerShell command-line for Windows</span><span class="sxs-lookup"><span data-stu-id="e49e7-256">From the PowerShell command-line for Windows</span></span>       

    wget "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/TDSP/tdsp_local_copy_win.ps1" -outfile "tdsp_local_copy_win.ps1"
    .\tdsp_local_copy_win.ps1 2

    
![16](./media/team-lead-tasks/team-leads-16-local_copy_team_lead_new.png)

#### <a name="from-the-linux-shell-for-the-linux-dsvm"></a><span data-ttu-id="e49e7-258">From the Linux shell for the **Linux DSVM**</span><span class="sxs-lookup"><span data-stu-id="e49e7-258">From the Linux shell for the **Linux DSVM**</span></span>
    
    wget "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/TDSP/tdsp_local_copy_linux.sh"
    bash tdsp_local_copy_linux.sh 2
    
![17](./media/team-lead-tasks/team-leads-17-local-copy-team-lead-linux-new.png)

<span data-ttu-id="e49e7-260">The scripts exclude the contents of the .git directory.</span><span class="sxs-lookup"><span data-stu-id="e49e7-260">The scripts exclude the contents of the .git directory.</span></span> <span data-ttu-id="e49e7-261">The scripts prompt you to provide the **complete paths** to the source directory D1 and to the destination directory D3.</span><span class="sxs-lookup"><span data-stu-id="e49e7-261">The scripts prompt you to provide the **complete paths** to the source directory D1 and to the destination directory D3.</span></span>
        

### <a name="customize-your-project-template-or-team-utilities-optional"></a><span data-ttu-id="e49e7-262">Customize your project template or team utilities (optional)</span><span class="sxs-lookup"><span data-stu-id="e49e7-262">Customize your project template or team utilities (optional)</span></span>

<span data-ttu-id="e49e7-263">Customize your **MyTeamProjectTemplate** (D3) and **MyTeamUtilities** (D4), if needed, at this stage of the setup process.</span><span class="sxs-lookup"><span data-stu-id="e49e7-263">Customize your **MyTeamProjectTemplate** (D3) and **MyTeamUtilities** (D4), if needed, at this stage of the setup process.</span></span> 

- <span data-ttu-id="e49e7-264">If you want to customize the contents of D3 to meet the specific needs of your team, you can modify the template documents or change the directory structure.</span><span class="sxs-lookup"><span data-stu-id="e49e7-264">If you want to customize the contents of D3 to meet the specific needs of your team, you can modify the template documents or change the directory structure.</span></span>

- <span data-ttu-id="e49e7-265">If your team has developed some utilities that you want to share with your entire team, copy and paste these utilities into directory D4.</span><span class="sxs-lookup"><span data-stu-id="e49e7-265">If your team has developed some utilities that you want to share with your entire team, copy and paste these utilities into directory D4.</span></span> 


### <a name="push-local-directory-content-to-team-repositories"></a><span data-ttu-id="e49e7-266">Push local directory content to team repositories</span><span class="sxs-lookup"><span data-stu-id="e49e7-266">Push local directory content to team repositories</span></span>

<span data-ttu-id="e49e7-267">To add the contents in the (optionally customized) local directories D3 and D4 to the team repositories R3 and R4, run the following git bash commands either from a Windows PowerShell console or from the Linux shell.</span><span class="sxs-lookup"><span data-stu-id="e49e7-267">To add the contents in the (optionally customized) local directories D3 and D4 to the team repositories R3 and R4, run the following git bash commands either from a Windows PowerShell console or from the Linux shell.</span></span> <span data-ttu-id="e49e7-268">Run the commands from the **GitRepos\MyTeam\MyTeamProjectTemplate** directory.</span><span class="sxs-lookup"><span data-stu-id="e49e7-268">Run the commands from the **GitRepos\MyTeam\MyTeamProjectTemplate** directory.</span></span>

    git status
    git add .
    git commit -m"push from DSVM"
    git push
    
![18](./media/team-lead-tasks/team-leads-18-push-to-group-server-2.png)

<span data-ttu-id="e49e7-270">The files in the MyTeamProjectTemplate repository of your group's Azure DevOps Services are synced nearly instantly when this script is run.</span><span class="sxs-lookup"><span data-stu-id="e49e7-270">The files in the MyTeamProjectTemplate repository of your group's Azure DevOps Services are synced nearly instantly when this script is run.</span></span>

![19](./media/team-lead-tasks/team-leads-19-push-to-group-server-showed-up.png)

<span data-ttu-id="e49e7-272">Now run the same set of four git commands from the **GitRepos\MyTeam\MyTeamUtilities** directory.</span><span class="sxs-lookup"><span data-stu-id="e49e7-272">Now run the same set of four git commands from the **GitRepos\MyTeam\MyTeamUtilities** directory.</span></span> 

> [AZURE.NOTE]<span data-ttu-id="e49e7-273">If this is the first time you commit to a Git repository, you need to configure global parameters *user.name* and *user.email* before you run the `git commit` command.</span><span class="sxs-lookup"><span data-stu-id="e49e7-273">If this is the first time you commit to a Git repository, you need to configure global parameters *user.name* and *user.email* before you run the `git commit` command.</span></span> <span data-ttu-id="e49e7-274">Run the following two commands:</span><span class="sxs-lookup"><span data-stu-id="e49e7-274">Run the following two commands:</span></span>
        
    git config --global user.name <your name>
    git config --global user.email <your email address>
 
> <span data-ttu-id="e49e7-275">If you are committing to multiple Git repositories, use the same name and email address when you commit to each of them.</span><span class="sxs-lookup"><span data-stu-id="e49e7-275">If you are committing to multiple Git repositories, use the same name and email address when you commit to each of them.</span></span> <span data-ttu-id="e49e7-276">Using the same name and email address proves convenient later on when you build PowerBI dashboards to track your Git activities on multiple repositories.</span><span class="sxs-lookup"><span data-stu-id="e49e7-276">Using the same name and email address proves convenient later on when you build PowerBI dashboards to track your Git activities on multiple repositories.</span></span>

![20](./media/team-lead-tasks/team-leads-20-git-config-name.png)


## <a name="3-create-team-data-and-analytics-resources-optional"></a><span data-ttu-id="e49e7-278">3. Create team data and analytics resources (Optional)</span><span class="sxs-lookup"><span data-stu-id="e49e7-278">3. Create team data and analytics resources (Optional)</span></span>

<span data-ttu-id="e49e7-279">Sharing data and analytics resources with your entire team has performance and cost benefits: team members can execute their projects on the shared resources, save on budgets, and collaborate more efficiently.</span><span class="sxs-lookup"><span data-stu-id="e49e7-279">Sharing data and analytics resources with your entire team has performance and cost benefits: team members can execute their projects on the shared resources, save on budgets, and collaborate more efficiently.</span></span> <span data-ttu-id="e49e7-280">In this section, we provide instructions on how to create Azure file storage.</span><span class="sxs-lookup"><span data-stu-id="e49e7-280">In this section, we provide instructions on how to create Azure file storage.</span></span> <span data-ttu-id="e49e7-281">In the next section, we provide instruction on how to mount Azure file storage to your local machine.</span><span class="sxs-lookup"><span data-stu-id="e49e7-281">In the next section, we provide instruction on how to mount Azure file storage to your local machine.</span></span> <span data-ttu-id="e49e7-282">For additional information on sharing other resources, such as Azure Data Science Virtual Machines, Azure HDInsight Spark Clusters, see [Platforms and tools](platforms-and-tools.md).</span><span class="sxs-lookup"><span data-stu-id="e49e7-282">For additional information on sharing other resources, such as Azure Data Science Virtual Machines, Azure HDInsight Spark Clusters, see [Platforms and tools](platforms-and-tools.md).</span></span> <span data-ttu-id="e49e7-283">This topic provides you guidance from a data science perspective on selecting resources that are appropriate for your needs, and links to product pages and other relevant and useful tutorials that we have published.</span><span class="sxs-lookup"><span data-stu-id="e49e7-283">This topic provides you guidance from a data science perspective on selecting resources that are appropriate for your needs, and links to product pages and other relevant and useful tutorials that we have published.</span></span>

>[AZURE.NOTE] <span data-ttu-id="e49e7-284">To avoid data transmitting cross data centers, which might be slow and costly, make sure that the resource group, storage account, and the Azure VM (e.g., DSVM) are in the same Azure data center.</span><span class="sxs-lookup"><span data-stu-id="e49e7-284">To avoid data transmitting cross data centers, which might be slow and costly, make sure that the resource group, storage account, and the Azure VM (e.g., DSVM) are in the same Azure data center.</span></span> 

<span data-ttu-id="e49e7-285">Run the following scripts to create Azure file storage for your team.</span><span class="sxs-lookup"><span data-stu-id="e49e7-285">Run the following scripts to create Azure file storage for your team.</span></span> <span data-ttu-id="e49e7-286">Azure file storage for your team can be used to store data assets that are useful for your entire team.</span><span class="sxs-lookup"><span data-stu-id="e49e7-286">Azure file storage for your team can be used to store data assets that are useful for your entire team.</span></span> <span data-ttu-id="e49e7-287">The scripts prompt you for your Azure account and subscription information, so have these credentials ready to enter.</span><span class="sxs-lookup"><span data-stu-id="e49e7-287">The scripts prompt you for your Azure account and subscription information, so have these credentials ready to enter.</span></span> 

### <a name="create-azure-file-storage-with-powershell-from-windows"></a><span data-ttu-id="e49e7-288">Create Azure file storage with PowerShell from Windows</span><span class="sxs-lookup"><span data-stu-id="e49e7-288">Create Azure file storage with PowerShell from Windows</span></span>

<span data-ttu-id="e49e7-289">Run this script from the PowerShell command-line:</span><span class="sxs-lookup"><span data-stu-id="e49e7-289">Run this script from the PowerShell command-line:</span></span>

    wget "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/TDSP/CreateFileShare.ps1" -outfile "CreateFileShare.ps1"
    .\CreateFileShare.ps1

![21](./media/team-lead-tasks/team-leads-21-create-fileshare-win.png)   

<span data-ttu-id="e49e7-291">Log in to your Microsoft Azure account when prompted:</span><span class="sxs-lookup"><span data-stu-id="e49e7-291">Log in to your Microsoft Azure account when prompted:</span></span>

![22](./media/team-lead-tasks/team-leads-22-file-create-s1.png)

<span data-ttu-id="e49e7-293">Select the Azure subscription you want to use:</span><span class="sxs-lookup"><span data-stu-id="e49e7-293">Select the Azure subscription you want to use:</span></span>

![23](./media/team-lead-tasks/team-leads-23-file-create-s2.png)

<span data-ttu-id="e49e7-295">Select which storage account to use or create a new one under your selected subscription:</span><span class="sxs-lookup"><span data-stu-id="e49e7-295">Select which storage account to use or create a new one under your selected subscription:</span></span>

![24](./media/team-lead-tasks/team-leads-24-file-create-s3.png)

<span data-ttu-id="e49e7-297">Enter the name of the Azure file storage to create.</span><span class="sxs-lookup"><span data-stu-id="e49e7-297">Enter the name of the Azure file storage to create.</span></span> <span data-ttu-id="e49e7-298">Only lower case characters, numbers and - are accepted:</span><span class="sxs-lookup"><span data-stu-id="e49e7-298">Only lower case characters, numbers and - are accepted:</span></span>

![25](./media/team-lead-tasks/team-leads-25-file-create-s4.png)

<span data-ttu-id="e49e7-300">To facilitate mounting and sharing this storage after it is created, save the Azure file storage information into a text file and make a note of the path to its location.</span><span class="sxs-lookup"><span data-stu-id="e49e7-300">To facilitate mounting and sharing this storage after it is created, save the Azure file storage information into a text file and make a note of the path to its location.</span></span> <span data-ttu-id="e49e7-301">In particular, you need this file to mount your Azure file storage to your Azure virtual machines in the next section.</span><span class="sxs-lookup"><span data-stu-id="e49e7-301">In particular, you need this file to mount your Azure file storage to your Azure virtual machines in the next section.</span></span> 

<span data-ttu-id="e49e7-302">It is a good practice to check in this text file into your ProjectTemplate repository.</span><span class="sxs-lookup"><span data-stu-id="e49e7-302">It is a good practice to check in this text file into your ProjectTemplate repository.</span></span> <span data-ttu-id="e49e7-303">We recommend to put in the directory **Docs\DataDictionaries**.</span><span class="sxs-lookup"><span data-stu-id="e49e7-303">We recommend to put in the directory **Docs\DataDictionaries**.</span></span> <span data-ttu-id="e49e7-304">Therefore, this data asset can be accessed by all projects in your team.</span><span class="sxs-lookup"><span data-stu-id="e49e7-304">Therefore, this data asset can be accessed by all projects in your team.</span></span> 

![26](./media/team-lead-tasks/team-leads-26-file-create-s5.png)


### <a name="create-azure-file-storage-with-a-linux-script"></a><span data-ttu-id="e49e7-306">Create Azure file storage with a Linux script</span><span class="sxs-lookup"><span data-stu-id="e49e7-306">Create Azure file storage with a Linux script</span></span>

<span data-ttu-id="e49e7-307">Run this script from the Linux shell:</span><span class="sxs-lookup"><span data-stu-id="e49e7-307">Run this script from the Linux shell:</span></span>

    wget "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/TDSP/CreateFileShare.sh"
    bash CreateFileShare.sh

<span data-ttu-id="e49e7-308">Log in to your Microsoft Azure account following the instructions on this screen:</span><span class="sxs-lookup"><span data-stu-id="e49e7-308">Log in to your Microsoft Azure account following the instructions on this screen:</span></span>

![27](./media/team-lead-tasks/team-leads-27-file-create-linux-s1.png)

<span data-ttu-id="e49e7-310">Select the Azure subscription that you want to use:</span><span class="sxs-lookup"><span data-stu-id="e49e7-310">Select the Azure subscription that you want to use:</span></span>

![28](./media/team-lead-tasks/team-leads-28-file-create-linux-s2.png)

<span data-ttu-id="e49e7-312">Select which storage account to use or create a new one under your selected subscription:</span><span class="sxs-lookup"><span data-stu-id="e49e7-312">Select which storage account to use or create a new one under your selected subscription:</span></span>

![29](./media/team-lead-tasks/team-leads-29-file-create-linux-s3.png)

<span data-ttu-id="e49e7-314">Enter the name of the Azure file storage to create, only lower case characters, numbers and - are accepted:</span><span class="sxs-lookup"><span data-stu-id="e49e7-314">Enter the name of the Azure file storage to create, only lower case characters, numbers and - are accepted:</span></span>

![30](./media/team-lead-tasks/team-leads-30-file-create-linux-s4.png)

<span data-ttu-id="e49e7-316">To facilitate accessing this storage after it is created, save the Azure file storage information into a text file and make a note of the path to its location.</span><span class="sxs-lookup"><span data-stu-id="e49e7-316">To facilitate accessing this storage after it is created, save the Azure file storage information into a text file and make a note of the path to its location.</span></span> <span data-ttu-id="e49e7-317">In particular, you need this file to mount your Azure file storage to your Azure virtual machines in the next section.</span><span class="sxs-lookup"><span data-stu-id="e49e7-317">In particular, you need this file to mount your Azure file storage to your Azure virtual machines in the next section.</span></span>

<span data-ttu-id="e49e7-318">It is a good practice to check in this text file into your ProjectTemplate repository.</span><span class="sxs-lookup"><span data-stu-id="e49e7-318">It is a good practice to check in this text file into your ProjectTemplate repository.</span></span> <span data-ttu-id="e49e7-319">We recommend to put in the directory **Docs\DataDictionaries**.</span><span class="sxs-lookup"><span data-stu-id="e49e7-319">We recommend to put in the directory **Docs\DataDictionaries**.</span></span> <span data-ttu-id="e49e7-320">Therefore, this data asset can be accessed by all projects in your team.</span><span class="sxs-lookup"><span data-stu-id="e49e7-320">Therefore, this data asset can be accessed by all projects in your team.</span></span> 

![31](./media/team-lead-tasks/team-leads-31-file-create-linux-s5.png)


## <a name="4-mount-azure-file-storage-optional"></a><span data-ttu-id="e49e7-322">4. Mount Azure file storage (Optional)</span><span class="sxs-lookup"><span data-stu-id="e49e7-322">4. Mount Azure file storage (Optional)</span></span>

<span data-ttu-id="e49e7-323">After Azure file storage is created successfully, it can be mounted to your local machine using the one of the following PowerShell or Linux scripts.</span><span class="sxs-lookup"><span data-stu-id="e49e7-323">After Azure file storage is created successfully, it can be mounted to your local machine using the one of the following PowerShell or Linux scripts.</span></span>

### <a name="mount-azure-file-storage-with-powershell-from-windows"></a><span data-ttu-id="e49e7-324">Mount Azure file storage with PowerShell from Windows</span><span class="sxs-lookup"><span data-stu-id="e49e7-324">Mount Azure file storage with PowerShell from Windows</span></span>

    wget "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/TDSP/AttachFileShare.ps1" -outfile "AttachFileShare.ps1"
    .\AttachFileShare.ps1
    
<span data-ttu-id="e49e7-325">You are asked to log in first, if you have not logged in.</span><span class="sxs-lookup"><span data-stu-id="e49e7-325">You are asked to log in first, if you have not logged in.</span></span> 

<span data-ttu-id="e49e7-326">Click **Enter** or **y** to continue when you are asked if you have an Azure file storage information file, and then input the \***complete path and name** of the file you create in previous step.</span><span class="sxs-lookup"><span data-stu-id="e49e7-326">Click **Enter** or **y** to continue when you are asked if you have an Azure file storage information file, and then input the \***complete path and name** of the file you create in previous step.</span></span> <span data-ttu-id="e49e7-327">The information to mount an Azure file storage is read directly from that file and you are ready to go to the next step.</span><span class="sxs-lookup"><span data-stu-id="e49e7-327">The information to mount an Azure file storage is read directly from that file and you are ready to go to the next step.</span></span>

![32](./media/team-lead-tasks/team-leads-32-attach-s1.png)

> [AZURE.NOTE] <span data-ttu-id="e49e7-329">If you do not have a file containing the Azure file storage information, the steps to input the information from keyboard are provided at the end of this section.</span><span class="sxs-lookup"><span data-stu-id="e49e7-329">If you do not have a file containing the Azure file storage information, the steps to input the information from keyboard are provided at the end of this section.</span></span>

<span data-ttu-id="e49e7-330">Then you are asked to enter the name of the drive to be added to your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e49e7-330">Then you are asked to enter the name of the drive to be added to your virtual machine.</span></span> <span data-ttu-id="e49e7-331">A list of existing drive names is printed on the screen.</span><span class="sxs-lookup"><span data-stu-id="e49e7-331">A list of existing drive names is printed on the screen.</span></span> <span data-ttu-id="e49e7-332">You should provide a drive name that does not already exist in the list.</span><span class="sxs-lookup"><span data-stu-id="e49e7-332">You should provide a drive name that does not already exist in the list.</span></span>

![33](./media/team-lead-tasks/team-leads-33-attach-s2.png)

<span data-ttu-id="e49e7-334">Confirm that a new F drive has been successfully mounted to your machine.</span><span class="sxs-lookup"><span data-stu-id="e49e7-334">Confirm that a new F drive has been successfully mounted to your machine.</span></span>

![34](./media/team-lead-tasks/team-leads-34-attach-s3.png)

<span data-ttu-id="e49e7-336">**How to enter the Azure file storage information manually:** If you do not have your Azure file storage information on a text file, you can follow the instructions on the following screen to type in the required subscription, storage account, and Azure file storage information:</span><span class="sxs-lookup"><span data-stu-id="e49e7-336">**How to enter the Azure file storage information manually:** If you do not have your Azure file storage information on a text file, you can follow the instructions on the following screen to type in the required subscription, storage account, and Azure file storage information:</span></span>

![35](./media/team-lead-tasks/team-leads-35-attach-s4.png)

<span data-ttu-id="e49e7-338">Type in your Azure subscription name, select the storage account where the Azure file storage is created, and type in the Azure file storage name:</span><span class="sxs-lookup"><span data-stu-id="e49e7-338">Type in your Azure subscription name, select the storage account where the Azure file storage is created, and type in the Azure file storage name:</span></span>

![36](./media/team-lead-tasks/team-leads-36-attach-s5.png)

### <a name="mount-azure-file-storage-with-a-linux-script"></a><span data-ttu-id="e49e7-340">Mount Azure file storage with a Linux script</span><span class="sxs-lookup"><span data-stu-id="e49e7-340">Mount Azure file storage with a Linux script</span></span>

    wget "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/TDSP/AttachFileShare.sh"
    bash AttachFileShare.sh

![37](./media/team-lead-tasks/team-leads-37-attach-s1-linux.png)

<span data-ttu-id="e49e7-342">You are asked to log in first, if you have not logged in.</span><span class="sxs-lookup"><span data-stu-id="e49e7-342">You are asked to log in first, if you have not logged in.</span></span> 

<span data-ttu-id="e49e7-343">Click **Enter** or **y** to continue when you are asked if you have an Azure file storage information file, and then input the \***complete path and name** of the file you create in previous step.</span><span class="sxs-lookup"><span data-stu-id="e49e7-343">Click **Enter** or **y** to continue when you are asked if you have an Azure file storage information file, and then input the \***complete path and name** of the file you create in previous step.</span></span> <span data-ttu-id="e49e7-344">The information to mount an Azure file storage is read directly from that file and you are ready to go to the next step.</span><span class="sxs-lookup"><span data-stu-id="e49e7-344">The information to mount an Azure file storage is read directly from that file and you are ready to go to the next step.</span></span>

![38](./media/team-lead-tasks/team-leads-38-attach-s2-linux.png)

<span data-ttu-id="e49e7-346">Then you are asked to enter the name of the drive to be added to your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e49e7-346">Then you are asked to enter the name of the drive to be added to your virtual machine.</span></span> <span data-ttu-id="e49e7-347">A list of existing drive names is printed on the screen.</span><span class="sxs-lookup"><span data-stu-id="e49e7-347">A list of existing drive names is printed on the screen.</span></span> <span data-ttu-id="e49e7-348">You should provide a drive name that does not already exist in the list.</span><span class="sxs-lookup"><span data-stu-id="e49e7-348">You should provide a drive name that does not already exist in the list.</span></span>

![39](./media/team-lead-tasks/team-leads-39-attach-s3-linux.png)

<span data-ttu-id="e49e7-350">Confirm that a new F drive has been successfully mounted to your machine.</span><span class="sxs-lookup"><span data-stu-id="e49e7-350">Confirm that a new F drive has been successfully mounted to your machine.</span></span>

![40](./media/team-lead-tasks/team-leads-40-attach-s4-linux.png)

<span data-ttu-id="e49e7-352">**How to enter the Azure file storage information manually:** If you do not have your Azure file storage information on a text file, you can follow the instructions on the following screen to type in the required subscription, storage account, and Azure file storage information:</span><span class="sxs-lookup"><span data-stu-id="e49e7-352">**How to enter the Azure file storage information manually:** If you do not have your Azure file storage information on a text file, you can follow the instructions on the following screen to type in the required subscription, storage account, and Azure file storage information:</span></span>

- <span data-ttu-id="e49e7-353">Input **n**.</span><span class="sxs-lookup"><span data-stu-id="e49e7-353">Input **n**.</span></span>
- <span data-ttu-id="e49e7-354">Select the index of the subscription name where the Azure file storage was created in the previous step:</span><span class="sxs-lookup"><span data-stu-id="e49e7-354">Select the index of the subscription name where the Azure file storage was created in the previous step:</span></span>

    ![41](./media/team-lead-tasks/team-leads-41-attach-s5-linux.png)

- <span data-ttu-id="e49e7-356">Select the storage account under your subscription and type in the Azure file storage name:</span><span class="sxs-lookup"><span data-stu-id="e49e7-356">Select the storage account under your subscription and type in the Azure file storage name:</span></span>

    ![42](./media/team-lead-tasks/team-leads-42-attach-s6-linux.png)

- <span data-ttu-id="e49e7-358">Enter the name of drive to be added to your machine, which should be distinct from any existing ones:</span><span class="sxs-lookup"><span data-stu-id="e49e7-358">Enter the name of drive to be added to your machine, which should be distinct from any existing ones:</span></span>

    ![43](./media/team-lead-tasks/team-leads-43-attach-s7-linux.png)


## <a name="5-set-up-security-control-policy"></a><span data-ttu-id="e49e7-360">5. Set up security control policy</span><span class="sxs-lookup"><span data-stu-id="e49e7-360">5. Set up security control policy</span></span> 

<span data-ttu-id="e49e7-361">From your group Azure DevOps Services's homepage, click the **gear icon** next to your user name in the upper right corner, then select the **Security** tab. You can add members to your team here with various permissions.</span><span class="sxs-lookup"><span data-stu-id="e49e7-361">From your group Azure DevOps Services's homepage, click the **gear icon** next to your user name in the upper right corner, then select the **Security** tab. You can add members to your team here with various permissions.</span></span>

![44](./media/team-lead-tasks/team-leads-44-add-team-members.png)

## <a name="next-steps"></a><span data-ttu-id="e49e7-363">Next steps</span><span class="sxs-lookup"><span data-stu-id="e49e7-363">Next steps</span></span>

<span data-ttu-id="e49e7-364">Here are links to the more detailed descriptions of the roles and tasks defined by the Team Data Science Process:</span><span class="sxs-lookup"><span data-stu-id="e49e7-364">Here are links to the more detailed descriptions of the roles and tasks defined by the Team Data Science Process:</span></span>

- [<span data-ttu-id="e49e7-365">Group Manager tasks for a data science team</span><span class="sxs-lookup"><span data-stu-id="e49e7-365">Group Manager tasks for a data science team</span></span>](group-manager-tasks.md)
- [<span data-ttu-id="e49e7-366">Team Lead tasks for a data science team</span><span class="sxs-lookup"><span data-stu-id="e49e7-366">Team Lead tasks for a data science team</span></span>](team-lead-tasks.md)
- [<span data-ttu-id="e49e7-367">Project Lead tasks for a data science team</span><span class="sxs-lookup"><span data-stu-id="e49e7-367">Project Lead tasks for a data science team</span></span>](project-lead-tasks.md)
- [<span data-ttu-id="e49e7-368">Project Individual Contributors for a data science team</span><span class="sxs-lookup"><span data-stu-id="e49e7-368">Project Individual Contributors for a data science team</span></span>](project-ic-tasks.md)