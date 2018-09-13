---
title: Team Data Science Process Project Lead tasks - Azure  | Microsoft Docs
description: An outline of the tasks for a project lead on a data science team project.
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
ms.openlocfilehash: 6a618efc6860371883bff7ebb953880293ad3120
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869858"
---
# <a name="project-lead-tasks"></a><span data-ttu-id="47732-103">Project Lead tasks</span><span class="sxs-lookup"><span data-stu-id="47732-103">Project Lead tasks</span></span>

<span data-ttu-id="47732-104">This tutorial outlines the tasks that a project lead is expected to complete for his/her project team.</span><span class="sxs-lookup"><span data-stu-id="47732-104">This tutorial outlines the tasks that a project lead is expected to complete for his/her project team.</span></span> <span data-ttu-id="47732-105">The objective is to establish collaborative team environment that standardizes on the [Team Data Science Process](overview.md) (TDSP).</span><span class="sxs-lookup"><span data-stu-id="47732-105">The objective is to establish collaborative team environment that standardizes on the [Team Data Science Process](overview.md) (TDSP).</span></span> <span data-ttu-id="47732-106">The TDSP is a framework developed by Microsoft that provides a structured sequence of activities to execute cloud-based, predictive analytics solutions efficiently.</span><span class="sxs-lookup"><span data-stu-id="47732-106">The TDSP is a framework developed by Microsoft that provides a structured sequence of activities to execute cloud-based, predictive analytics solutions efficiently.</span></span> <span data-ttu-id="47732-107">For an outline of the personnel roles and their associated tasks that are handled by a data science team standardizing on this process, see [Team Data Science Process roles and tasks](roles-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="47732-107">For an outline of the personnel roles and their associated tasks that are handled by a data science team standardizing on this process, see [Team Data Science Process roles and tasks](roles-tasks.md).</span></span>

<span data-ttu-id="47732-108">A **Project Lead** manages the daily activities of individual data scientists on a specific data science project.</span><span class="sxs-lookup"><span data-stu-id="47732-108">A **Project Lead** manages the daily activities of individual data scientists on a specific data science project.</span></span> <span data-ttu-id="47732-109">The workflow for the tasks to be completed by project leads to set up this environment are depicted in the following figure:</span><span class="sxs-lookup"><span data-stu-id="47732-109">The workflow for the tasks to be completed by project leads to set up this environment are depicted in the following figure:</span></span>

![1](./media/project-lead-tasks/project-leads-1-tdsp-creating-projects.png)

<span data-ttu-id="47732-111">This topic currently covers tasks 1,2 and 6 of this workflow for project leads.</span><span class="sxs-lookup"><span data-stu-id="47732-111">This topic currently covers tasks 1,2 and 6 of this workflow for project leads.</span></span>

>[AZURE.NOTE] <span data-ttu-id="47732-112">We outline the steps needed to set up a TDSP team environment for a project using Azure DevOps in the following instructions.</span><span class="sxs-lookup"><span data-stu-id="47732-112">We outline the steps needed to set up a TDSP team environment for a project using Azure DevOps in the following instructions.</span></span> <span data-ttu-id="47732-113">We specify how to accomplish these tasks with Azure DevOps because that is how we implement TDSP at Microsoft.</span><span class="sxs-lookup"><span data-stu-id="47732-113">We specify how to accomplish these tasks with Azure DevOps because that is how we implement TDSP at Microsoft.</span></span> <span data-ttu-id="47732-114">If another code-hosting platform is used for your group, the tasks that need to be completed by the team lead generally do not change.</span><span class="sxs-lookup"><span data-stu-id="47732-114">If another code-hosting platform is used for your group, the tasks that need to be completed by the team lead generally do not change.</span></span> <span data-ttu-id="47732-115">But the way to complete these tasks is going to be different.</span><span class="sxs-lookup"><span data-stu-id="47732-115">But the way to complete these tasks is going to be different.</span></span>


## <a name="repositories-and-directories"></a><span data-ttu-id="47732-116">Repositories and directories</span><span class="sxs-lookup"><span data-stu-id="47732-116">Repositories and directories</span></span>

<span data-ttu-id="47732-117">This tutorial uses abbreviated names for repositories and directories.</span><span class="sxs-lookup"><span data-stu-id="47732-117">This tutorial uses abbreviated names for repositories and directories.</span></span> <span data-ttu-id="47732-118">These names make it easier to follow the operations between the repositories and directories.</span><span class="sxs-lookup"><span data-stu-id="47732-118">These names make it easier to follow the operations between the repositories and directories.</span></span> <span data-ttu-id="47732-119">This notation (R for Git repositories and D for local directories on your DSVM) is used in the following sections:</span><span class="sxs-lookup"><span data-stu-id="47732-119">This notation (R for Git repositories and D for local directories on your DSVM) is used in the following sections:</span></span>

- <span data-ttu-id="47732-120">**R3**: The team **ProjectTemplate** repository on Git your team lead has set up.</span><span class="sxs-lookup"><span data-stu-id="47732-120">**R3**: The team **ProjectTemplate** repository on Git your team lead has set up.</span></span>
- <span data-ttu-id="47732-121">**R5**: The project repository on Git you setup for your project.</span><span class="sxs-lookup"><span data-stu-id="47732-121">**R5**: The project repository on Git you setup for your project.</span></span>
- <span data-ttu-id="47732-122">**D3**: The local directory cloned from R3.</span><span class="sxs-lookup"><span data-stu-id="47732-122">**D3**: The local directory cloned from R3.</span></span>
- <span data-ttu-id="47732-123">**D5**: The local directory cloned from R5.</span><span class="sxs-lookup"><span data-stu-id="47732-123">**D5**: The local directory cloned from R5.</span></span>


## <a name="0-prerequisites"></a><span data-ttu-id="47732-124">0. Prerequisites</span><span class="sxs-lookup"><span data-stu-id="47732-124">0. Prerequisites</span></span>

<span data-ttu-id="47732-125">The prerequisites are satisfied by completing the tasks assigned to your group manager outlined in [Group Manager tasks for a data science team](group-manager-tasks.md) and to you team lead outlined in [Team lead tasks for a data science team](team-lead-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="47732-125">The prerequisites are satisfied by completing the tasks assigned to your group manager outlined in [Group Manager tasks for a data science team](group-manager-tasks.md) and to you team lead outlined in [Team lead tasks for a data science team](team-lead-tasks.md).</span></span> 

<span data-ttu-id="47732-126">To summarize here, the following requirements need to meet before you begin the team lead tasks:</span><span class="sxs-lookup"><span data-stu-id="47732-126">To summarize here, the following requirements need to meet before you begin the team lead tasks:</span></span> 

- <span data-ttu-id="47732-127">Your **group Azure DevOps Services** (or group account on some other code-hosting platform) has been set up by your group manager.</span><span class="sxs-lookup"><span data-stu-id="47732-127">Your **group Azure DevOps Services** (or group account on some other code-hosting platform) has been set up by your group manager.</span></span>
- <span data-ttu-id="47732-128">Your **TeamProjectTemplate repository** (R3) has been set up under your group account by your team lead on the code-hosting platform you plan to use.</span><span class="sxs-lookup"><span data-stu-id="47732-128">Your **TeamProjectTemplate repository** (R3) has been set up under your group account by your team lead on the code-hosting platform you plan to use.</span></span>
- <span data-ttu-id="47732-129">You have been **authorized** by your team lead to create repositories on your group account for your team.</span><span class="sxs-lookup"><span data-stu-id="47732-129">You have been **authorized** by your team lead to create repositories on your group account for your team.</span></span>
- <span data-ttu-id="47732-130">Git must be installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="47732-130">Git must be installed on your machine.</span></span> <span data-ttu-id="47732-131">If you are using a Data Science Virtual Machine (DSVM), Git has been pre-installed and you are good to go.</span><span class="sxs-lookup"><span data-stu-id="47732-131">If you are using a Data Science Virtual Machine (DSVM), Git has been pre-installed and you are good to go.</span></span> <span data-ttu-id="47732-132">Otherwise, see the [Platforms and tools appendix](platforms-and-tools.md#appendix).</span><span class="sxs-lookup"><span data-stu-id="47732-132">Otherwise, see the [Platforms and tools appendix](platforms-and-tools.md#appendix).</span></span>  
- <span data-ttu-id="47732-133">If you are using a **Windows DSVM**, you need to have [Git Credential Manager (GCM)](https://github.com/Microsoft/Git-Credential-Manager-for-Windows) installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="47732-133">If you are using a **Windows DSVM**, you need to have [Git Credential Manager (GCM)](https://github.com/Microsoft/Git-Credential-Manager-for-Windows) installed on your machine.</span></span> <span data-ttu-id="47732-134">In the README.md file, scroll down to the **Download and Install** section and click the *latest installer*.</span><span class="sxs-lookup"><span data-stu-id="47732-134">In the README.md file, scroll down to the **Download and Install** section and click the *latest installer*.</span></span> <span data-ttu-id="47732-135">This takes you to the latest installer page.</span><span class="sxs-lookup"><span data-stu-id="47732-135">This takes you to the latest installer page.</span></span> <span data-ttu-id="47732-136">Download the .exe installer from here and run it.</span><span class="sxs-lookup"><span data-stu-id="47732-136">Download the .exe installer from here and run it.</span></span> 
- <span data-ttu-id="47732-137">If you are using **Linux DSVM**, create an SSH public key on your DSVM and add it to your group Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="47732-137">If you are using **Linux DSVM**, create an SSH public key on your DSVM and add it to your group Azure DevOps Services.</span></span> <span data-ttu-id="47732-138">For more information about SSH, see the **Create SSH public key** section in the [Platforms and tools appendix](platforms-and-tools.md#appendix).</span><span class="sxs-lookup"><span data-stu-id="47732-138">For more information about SSH, see the **Create SSH public key** section in the [Platforms and tools appendix](platforms-and-tools.md#appendix).</span></span> 


## <a name="1-create-a-project-repository-r5"></a><span data-ttu-id="47732-139">1. Create a project repository (R5)</span><span class="sxs-lookup"><span data-stu-id="47732-139">1. Create a project repository (R5)</span></span>

- <span data-ttu-id="47732-140">Log in to your group Azure DevOps Services at *https://\<Azure DevOps Services Name\>.visualstudio.com*.</span><span class="sxs-lookup"><span data-stu-id="47732-140">Log in to your group Azure DevOps Services at *https://\<Azure DevOps Services Name\>.visualstudio.com*.</span></span> 
- <span data-ttu-id="47732-141">Under **Recent projects & teams**, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="47732-141">Under **Recent projects & teams**, click **Browse**.</span></span> <span data-ttu-id="47732-142">A window that pops up lists all projects on the Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="47732-142">A window that pops up lists all projects on the Azure DevOps Services.</span></span> 

    ![2](./media/project-lead-tasks/project-leads-2-create-project-repo.png)

- <span data-ttu-id="47732-144">Click the project name in which you are going to create your project repository.</span><span class="sxs-lookup"><span data-stu-id="47732-144">Click the project name in which you are going to create your project repository.</span></span> <span data-ttu-id="47732-145">In this example, click **MyTeam**.</span><span class="sxs-lookup"><span data-stu-id="47732-145">In this example, click **MyTeam**.</span></span> 
- <span data-ttu-id="47732-146">Then, click **Navigate** to be directed to the home page of the project **MyTeam**:</span><span class="sxs-lookup"><span data-stu-id="47732-146">Then, click **Navigate** to be directed to the home page of the project **MyTeam**:</span></span>

    ![3](./media/project-lead-tasks/project-leads-3-create-project-repo-2.png)

- <span data-ttu-id="47732-148">Click **Collaborate on code** to be directed to the git home page of your project.</span><span class="sxs-lookup"><span data-stu-id="47732-148">Click **Collaborate on code** to be directed to the git home page of your project.</span></span>  

    ![4](./media/project-lead-tasks/project-leads-4-create-project-repo-3.png)

- <span data-ttu-id="47732-150">Click the downward arrow at the top left corner, and select **+ New repository**.</span><span class="sxs-lookup"><span data-stu-id="47732-150">Click the downward arrow at the top left corner, and select **+ New repository**.</span></span> 
    
    ![5](./media/project-lead-tasks/project-leads-5-create-project-repo-4.png)

- <span data-ttu-id="47732-152">In the **Create a new repository** window, input a name for your project git repository.</span><span class="sxs-lookup"><span data-stu-id="47732-152">In the **Create a new repository** window, input a name for your project git repository.</span></span> <span data-ttu-id="47732-153">Make sure that you select **Git** as the type of the repository.</span><span class="sxs-lookup"><span data-stu-id="47732-153">Make sure that you select **Git** as the type of the repository.</span></span> <span data-ttu-id="47732-154">In this example, we use the name *DSProject1*.</span><span class="sxs-lookup"><span data-stu-id="47732-154">In this example, we use the name *DSProject1*.</span></span> 

    ![6](./media/project-lead-tasks/project-leads-6-create-project-repo-5.png)

- <span data-ttu-id="47732-156">To create your ***DSProject1*** project git repository, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="47732-156">To create your ***DSProject1*** project git repository, click **Create**.</span></span>


## <a name="2-seed-the-dsproject1-project-repository"></a><span data-ttu-id="47732-157">2. Seed the DSProject1 project repository</span><span class="sxs-lookup"><span data-stu-id="47732-157">2. Seed the DSProject1 project repository</span></span>

<span data-ttu-id="47732-158">The task here is to seed the **DSProject1** project repository (R5) from your project template repository (R3).</span><span class="sxs-lookup"><span data-stu-id="47732-158">The task here is to seed the **DSProject1** project repository (R5) from your project template repository (R3).</span></span> <span data-ttu-id="47732-159">The seeding procedure uses the directories D3 and D5 on your local DSVM as intermediate staging sites.</span><span class="sxs-lookup"><span data-stu-id="47732-159">The seeding procedure uses the directories D3 and D5 on your local DSVM as intermediate staging sites.</span></span> <span data-ttu-id="47732-160">In summary, the seeding path is: R3 -> D3 -> D5 -> R5.</span><span class="sxs-lookup"><span data-stu-id="47732-160">In summary, the seeding path is: R3 -> D3 -> D5 -> R5.</span></span>

<span data-ttu-id="47732-161">If you need to customize your **DSProject1** project repository to meet some specific project needs, you do so in the penultimate step of following procedure.</span><span class="sxs-lookup"><span data-stu-id="47732-161">If you need to customize your **DSProject1** project repository to meet some specific project needs, you do so in the penultimate step of following procedure.</span></span> <span data-ttu-id="47732-162">Here is a summary of the steps used to seed the content of the **DSProject1** project repository.</span><span class="sxs-lookup"><span data-stu-id="47732-162">Here is a summary of the steps used to seed the content of the **DSProject1** project repository.</span></span> <span data-ttu-id="47732-163">The individual steps correspond to the subsections in the seeding procedure:</span><span class="sxs-lookup"><span data-stu-id="47732-163">The individual steps correspond to the subsections in the seeding procedure:</span></span>

- <span data-ttu-id="47732-164">Clone project template repository into local directory: team R3 - cloned to -> local D3.</span><span class="sxs-lookup"><span data-stu-id="47732-164">Clone project template repository into local directory: team R3 - cloned to -> local D3.</span></span>
- <span data-ttu-id="47732-165">Clone DSProject1 repository to a local directory: team R5 - cloned to -> local D5.</span><span class="sxs-lookup"><span data-stu-id="47732-165">Clone DSProject1 repository to a local directory: team R5 - cloned to -> local D5.</span></span>
- <span data-ttu-id="47732-166">Copy cloned project template content to local clone of DSProject1 repository:  D3 - contents copied to -> D5.</span><span class="sxs-lookup"><span data-stu-id="47732-166">Copy cloned project template content to local clone of DSProject1 repository:  D3 - contents copied to -> D5.</span></span>
- <span data-ttu-id="47732-167">(Optional) Customization local D5.</span><span class="sxs-lookup"><span data-stu-id="47732-167">(Optional) Customization local D5.</span></span>
- <span data-ttu-id="47732-168">Push local DSProject1 content to team repositories: D5 - contents add to -> team R5.</span><span class="sxs-lookup"><span data-stu-id="47732-168">Push local DSProject1 content to team repositories: D5 - contents add to -> team R5.</span></span>


### <a name="clone-your-project-template-repository-r3-to-a-directory-d3-on-your-local-machine"></a><span data-ttu-id="47732-169">Clone your project template repository (R3) to a directory (D3) on your local machine.</span><span class="sxs-lookup"><span data-stu-id="47732-169">Clone your project template repository (R3) to a directory (D3) on your local machine.</span></span>

<span data-ttu-id="47732-170">On your local machine, create a directory:</span><span class="sxs-lookup"><span data-stu-id="47732-170">On your local machine, create a directory:</span></span>

- <span data-ttu-id="47732-171">*C:\GitRepos\MyTeamCommon* for Windows</span><span class="sxs-lookup"><span data-stu-id="47732-171">*C:\GitRepos\MyTeamCommon* for Windows</span></span> 
- <span data-ttu-id="47732-172">*$home/GitRepos/MyTeamCommon* for Linux</span><span class="sxs-lookup"><span data-stu-id="47732-172">*$home/GitRepos/MyTeamCommon* for Linux</span></span>

<span data-ttu-id="47732-173">Change to that directory.</span><span class="sxs-lookup"><span data-stu-id="47732-173">Change to that directory.</span></span> <span data-ttu-id="47732-174">Then, run the following command to clone your project template repository to your local machine.</span><span class="sxs-lookup"><span data-stu-id="47732-174">Then, run the following command to clone your project template repository to your local machine.</span></span> 

<span data-ttu-id="47732-175">**Windows**</span><span class="sxs-lookup"><span data-stu-id="47732-175">**Windows**</span></span>
            
    git clone <the HTTPS URL of the TeamProjectTemplate repository>
    
<span data-ttu-id="47732-176">If you are using Azure DevOps as the code-hosting platform, typically, the *HTTPS URL of your project template repository* is:</span><span class="sxs-lookup"><span data-stu-id="47732-176">If you are using Azure DevOps as the code-hosting platform, typically, the *HTTPS URL of your project template repository* is:</span></span>

 <span data-ttu-id="47732-177">***https://\<Azure DevOps Services Name\>.visualstudio.com/\<Your project name\>/_git/\<Your project template repository name\>***.</span><span class="sxs-lookup"><span data-stu-id="47732-177">***https://\<Azure DevOps Services Name\>.visualstudio.com/\<Your project name\>/_git/\<Your project template repository name\>***.</span></span> 

<span data-ttu-id="47732-178">In this example, we have:</span><span class="sxs-lookup"><span data-stu-id="47732-178">In this example, we have:</span></span>

<span data-ttu-id="47732-179">***https://mysamplegroup.visualstudio.com/MyTeam/_git/MyTeamProjectTemplate***.</span><span class="sxs-lookup"><span data-stu-id="47732-179">***https://mysamplegroup.visualstudio.com/MyTeam/_git/MyTeamProjectTemplate***.</span></span> 

![7](./media/project-lead-tasks/project-leads-7-clone-team-project-template.png)
            
<span data-ttu-id="47732-181">**Linux**</span><span class="sxs-lookup"><span data-stu-id="47732-181">**Linux**</span></span>

    git clone <the SSH URL of the TeamProjectTemplate repository>
        
![8](./media/project-lead-tasks/project-leads-8-clone-team-project-template-linux.png)

<span data-ttu-id="47732-183">If you are using Azure DevOps as the code-hosting platform, typically, the *SSH URL of the project template repository* is:</span><span class="sxs-lookup"><span data-stu-id="47732-183">If you are using Azure DevOps as the code-hosting platform, typically, the *SSH URL of the project template repository* is:</span></span>

<span data-ttu-id="47732-184">***ssh://\<Azure DevOps Services Name\>@\<Azure DevOps Services Name\>.visualstudio.com:22/\<Your Project Name>/_git/\<Your project template repository name\>.***</span><span class="sxs-lookup"><span data-stu-id="47732-184">***ssh://\<Azure DevOps Services Name\>@\<Azure DevOps Services Name\>.visualstudio.com:22/\<Your Project Name>/_git/\<Your project template repository name\>.***</span></span> 

<span data-ttu-id="47732-185">In this example, we have:</span><span class="sxs-lookup"><span data-stu-id="47732-185">In this example, we have:</span></span>

<span data-ttu-id="47732-186">***ssh://mysamplegroup@mysamplegroup.visualstudio.com:22/MyTeam/_git/MyTeamProjectTemplate***.</span><span class="sxs-lookup"><span data-stu-id="47732-186">***ssh://mysamplegroup@mysamplegroup.visualstudio.com:22/MyTeam/_git/MyTeamProjectTemplate***.</span></span> 

### <a name="clone-dsproject1-repository-r5-to-a-directory-d5-on-your-local-machine"></a><span data-ttu-id="47732-187">Clone DSProject1 repository (R5) to a directory (D5) on your local machine</span><span class="sxs-lookup"><span data-stu-id="47732-187">Clone DSProject1 repository (R5) to a directory (D5) on your local machine</span></span>

<span data-ttu-id="47732-188">Change directory to **GitRepos**, and run the following command to clone your project repository to your local machine.</span><span class="sxs-lookup"><span data-stu-id="47732-188">Change directory to **GitRepos**, and run the following command to clone your project repository to your local machine.</span></span> 

<span data-ttu-id="47732-189">**Windows**</span><span class="sxs-lookup"><span data-stu-id="47732-189">**Windows**</span></span>
            
    git clone <the HTTPS URL of the Project repository>

![9](./media/project-lead-tasks/project-leads-9-clone-project-repository.png)

<span data-ttu-id="47732-191">If you are using Azure DevOps as the code-hosting platform, typically, the _HTTPS URL of the Project repository_ is ***https://\<Azure DevOps Services Name\>.visualstudio.com/\<Your Project Name>/_git/<Your project repository name\>***.</span><span class="sxs-lookup"><span data-stu-id="47732-191">If you are using Azure DevOps as the code-hosting platform, typically, the _HTTPS URL of the Project repository_ is ***https://\<Azure DevOps Services Name\>.visualstudio.com/\<Your Project Name>/_git/<Your project repository name\>***.</span></span> <span data-ttu-id="47732-192">In this example, we have ***https://mysamplegroup.visualstudio.com/MyTeam/_git/DSProject1***.</span><span class="sxs-lookup"><span data-stu-id="47732-192">In this example, we have ***https://mysamplegroup.visualstudio.com/MyTeam/_git/DSProject1***.</span></span>

<span data-ttu-id="47732-193">**Linux**</span><span class="sxs-lookup"><span data-stu-id="47732-193">**Linux**</span></span>

    git clone <the SSH URL of the Project repository>

![10](./media/project-lead-tasks/project-leads-10-clone-project-repository-linux.png)

<span data-ttu-id="47732-195">If you are using Azure DevOps as the code-hosting platform, typically, the _SSH URL of the project repository_ is _ssh://<Azure DevOps Services Name\>@<Azure DevOps Services Name\>.visualstudio.com:22/<Your Project Name>/\_git/<Your project repository name\>.</span><span class="sxs-lookup"><span data-stu-id="47732-195">If you are using Azure DevOps as the code-hosting platform, typically, the _SSH URL of the project repository_ is _ssh://<Azure DevOps Services Name\>@<Azure DevOps Services Name\>.visualstudio.com:22/<Your Project Name>/\_git/<Your project repository name\>.</span></span> <span data-ttu-id="47732-196">In this example, we have ***ssh://mysamplegroup@mysamplegroup.visualstudio.com:22/MyTeam/_git/DSProject1***.</span><span class="sxs-lookup"><span data-stu-id="47732-196">In this example, we have ***ssh://mysamplegroup@mysamplegroup.visualstudio.com:22/MyTeam/_git/DSProject1***.</span></span>

### <a name="copy-contents-of-d3-to-d5"></a><span data-ttu-id="47732-197">Copy contents of D3 to D5</span><span class="sxs-lookup"><span data-stu-id="47732-197">Copy contents of D3 to D5</span></span> 

<span data-ttu-id="47732-198">Now in your local machine, you need to copy the content of _D3_ to _D5_, except the git metadata in .git directory.</span><span class="sxs-lookup"><span data-stu-id="47732-198">Now in your local machine, you need to copy the content of _D3_ to _D5_, except the git metadata in .git directory.</span></span> <span data-ttu-id="47732-199">The following scripts will do the job.</span><span class="sxs-lookup"><span data-stu-id="47732-199">The following scripts will do the job.</span></span> <span data-ttu-id="47732-200">Make sure to type in the correct and full paths to the directories.</span><span class="sxs-lookup"><span data-stu-id="47732-200">Make sure to type in the correct and full paths to the directories.</span></span> <span data-ttu-id="47732-201">Source folder is the one for your team (_D3_); destination folder is the one for your project (_D5_).</span><span class="sxs-lookup"><span data-stu-id="47732-201">Source folder is the one for your team (_D3_); destination folder is the one for your project (_D5_).</span></span>    

<span data-ttu-id="47732-202">**Windows**</span><span class="sxs-lookup"><span data-stu-id="47732-202">**Windows**</span></span>
    
    wget "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/TDSP/tdsp_local_copy_win.ps1" -outfile "tdsp_local_copy_win.ps1"
    .\tdsp_local_copy_win.ps1 -role 3
    
![11](./media/project-lead-tasks/project-leads-11-local-copy-project-lead-new.png)

<span data-ttu-id="47732-204">Now you can see in _DSProject1_ folder, all the files (excluding the .git) are copied from _MyTeamProjectTemplate_.</span><span class="sxs-lookup"><span data-stu-id="47732-204">Now you can see in _DSProject1_ folder, all the files (excluding the .git) are copied from _MyTeamProjectTemplate_.</span></span>

![12](./media/project-lead-tasks/project-leads-12-teamprojectTemplate_copied_to_local.png)

<span data-ttu-id="47732-206">**Linux**</span><span class="sxs-lookup"><span data-stu-id="47732-206">**Linux**</span></span>
            
    wget "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/TDSP/tdsp_local_copy_linux.sh"
    bash tdsp_local_copy_linux.sh 3
        
![13](./media/project-lead-tasks/project-leads-13-local_copy_project_lead_linux_new.png)

<span data-ttu-id="47732-208">Now you can see in _DSProject1_ folder, all the files (except the metadata in .git) are copied from _MyTeamProjectTemplate_.</span><span class="sxs-lookup"><span data-stu-id="47732-208">Now you can see in _DSProject1_ folder, all the files (except the metadata in .git) are copied from _MyTeamProjectTemplate_.</span></span>

![14](./media/project-lead-tasks/project-leads-14-teamprojectTemplate_copied_to_local_linux_new.png)


### <a name="customize-d5-if-you-need-to-optional"></a><span data-ttu-id="47732-210">Customize D5 if you need to (Optional)</span><span class="sxs-lookup"><span data-stu-id="47732-210">Customize D5 if you need to (Optional)</span></span>

<span data-ttu-id="47732-211">If your project needs some specific directories or documents, other than the ones you get from your project template (copied to your D5 directory in the previous step), you can customize the content of D5 now.</span><span class="sxs-lookup"><span data-stu-id="47732-211">If your project needs some specific directories or documents, other than the ones you get from your project template (copied to your D5 directory in the previous step), you can customize the content of D5 now.</span></span> 

### <a name="add-contents-of-dsproject1-in-d5-to-r5-on-your-group-azure-devops-services"></a><span data-ttu-id="47732-212">Add contents of DSProject1 in D5 to R5 on your group Azure DevOps Services</span><span class="sxs-lookup"><span data-stu-id="47732-212">Add contents of DSProject1 in D5 to R5 on your group Azure DevOps Services</span></span>

<span data-ttu-id="47732-213">You now need to push contents in **_DSProject1_** to _R5_ repository in your project on your group's Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="47732-213">You now need to push contents in **_DSProject1_** to _R5_ repository in your project on your group's Azure DevOps Services.</span></span> 


- <span data-ttu-id="47732-214">Change to directory **D5**.</span><span class="sxs-lookup"><span data-stu-id="47732-214">Change to directory **D5**.</span></span> 
- <span data-ttu-id="47732-215">Use the following git commands to add the contents in **D5** to **R5**.</span><span class="sxs-lookup"><span data-stu-id="47732-215">Use the following git commands to add the contents in **D5** to **R5**.</span></span> <span data-ttu-id="47732-216">The commands are the same for both Windows and Linux systems.</span><span class="sxs-lookup"><span data-stu-id="47732-216">The commands are the same for both Windows and Linux systems.</span></span> 
    
    <span data-ttu-id="47732-217">git status git add .</span><span class="sxs-lookup"><span data-stu-id="47732-217">git status git add .</span></span>
    <span data-ttu-id="47732-218">git commit -m"push from win DSVM" git push</span><span class="sxs-lookup"><span data-stu-id="47732-218">git commit -m"push from win DSVM" git push</span></span>
    
- <span data-ttu-id="47732-219">Commit the change and push.</span><span class="sxs-lookup"><span data-stu-id="47732-219">Commit the change and push.</span></span> 

>[AZURE.NOTE] <span data-ttu-id="47732-220">If this is the first time you commit to a Git repository, you need to configure global parameters *user.name* and *user.email* before you run the `git commit` command.</span><span class="sxs-lookup"><span data-stu-id="47732-220">If this is the first time you commit to a Git repository, you need to configure global parameters *user.name* and *user.email* before you run the `git commit` command.</span></span> <span data-ttu-id="47732-221">Run the following two commands:</span><span class="sxs-lookup"><span data-stu-id="47732-221">Run the following two commands:</span></span>
        
    git config --global user.name <your name>
    git config --global user.email <your email address>
 
> <span data-ttu-id="47732-222">If you are committing to multiple Git repositories, use the same name and email address across all of them.</span><span class="sxs-lookup"><span data-stu-id="47732-222">If you are committing to multiple Git repositories, use the same name and email address across all of them.</span></span> <span data-ttu-id="47732-223">Using the same name and email address proves convenient later on when you build PowerBI dashboards to track your Git activities on multiple repositories.</span><span class="sxs-lookup"><span data-stu-id="47732-223">Using the same name and email address proves convenient later on when you build PowerBI dashboards to track your Git activities on multiple repositories.</span></span>

![15](./media/project-lead-tasks/project-leads-15-git-config-name.png)


## <a name="6-create-and-mount-azure-file-storage-as-project-resources-optional"></a><span data-ttu-id="47732-225">6. Create and mount Azure file storage as project resources (Optional)</span><span class="sxs-lookup"><span data-stu-id="47732-225">6. Create and mount Azure file storage as project resources (Optional)</span></span>

<span data-ttu-id="47732-226">If you want to create Azure file storage to share data, such as the project raw data or the features generated for your project, so that all project members have access to the same datasets from multiple DSVMs, follow the instructions in sections 3 and 4 of [Team Lead tasks for a data science team](team-lead-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="47732-226">If you want to create Azure file storage to share data, such as the project raw data or the features generated for your project, so that all project members have access to the same datasets from multiple DSVMs, follow the instructions in sections 3 and 4 of [Team Lead tasks for a data science team](team-lead-tasks.md).</span></span> 


## <a name="next-steps"></a><span data-ttu-id="47732-227">Next steps</span><span class="sxs-lookup"><span data-stu-id="47732-227">Next steps</span></span>

<span data-ttu-id="47732-228">Here are links to the more detailed descriptions of the roles and tasks defined by the Team Data Science Process:</span><span class="sxs-lookup"><span data-stu-id="47732-228">Here are links to the more detailed descriptions of the roles and tasks defined by the Team Data Science Process:</span></span>

- [<span data-ttu-id="47732-229">Group Manager tasks for a data science team</span><span class="sxs-lookup"><span data-stu-id="47732-229">Group Manager tasks for a data science team</span></span>](group-manager-tasks.md)
- [<span data-ttu-id="47732-230">Team Lead tasks for a data science team</span><span class="sxs-lookup"><span data-stu-id="47732-230">Team Lead tasks for a data science team</span></span>](team-lead-tasks.md)
- [<span data-ttu-id="47732-231">Project Lead tasks for a data science team</span><span class="sxs-lookup"><span data-stu-id="47732-231">Project Lead tasks for a data science team</span></span>](project-lead-tasks.md)
- [<span data-ttu-id="47732-232">Project Individual Contributors for a data science team</span><span class="sxs-lookup"><span data-stu-id="47732-232">Project Individual Contributors for a data science team</span></span>](project-ic-tasks.md)