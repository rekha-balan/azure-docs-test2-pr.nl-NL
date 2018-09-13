---
title: Team Data Science Process tasks for an individual contributor - Azure  | Microsoft Docs
description: An outline of the tasks for an individual contributor on a data science team project.
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
ms.openlocfilehash: f21098381d75a4843e9300beaae687adc6ec107d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969115"
---
# <a name="individual-contributor-tasks"></a><span data-ttu-id="70167-103">Individual Contributor tasks</span><span class="sxs-lookup"><span data-stu-id="70167-103">Individual Contributor tasks</span></span>

<span data-ttu-id="70167-104">This topic outlines the tasks that an individual contributor is expected to complete for their data science team.</span><span class="sxs-lookup"><span data-stu-id="70167-104">This topic outlines the tasks that an individual contributor is expected to complete for their data science team.</span></span> <span data-ttu-id="70167-105">The objective is to establish collaborative team environment that standardizes on the [Team Data Science Process](overview.md) (TDSP).</span><span class="sxs-lookup"><span data-stu-id="70167-105">The objective is to establish collaborative team environment that standardizes on the [Team Data Science Process](overview.md) (TDSP).</span></span> <span data-ttu-id="70167-106">For an outline of the personnel roles and their associated tasks that are handled by a data science team standardizing on this process, see [Team Data Science Process roles and tasks](roles-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="70167-106">For an outline of the personnel roles and their associated tasks that are handled by a data science team standardizing on this process, see [Team Data Science Process roles and tasks](roles-tasks.md).</span></span>

<span data-ttu-id="70167-107">The tasks of project individual contributors (data scientists) to set up the TDSP environment for the project are depicted as follows:</span><span class="sxs-lookup"><span data-stu-id="70167-107">The tasks of project individual contributors (data scientists) to set up the TDSP environment for the project are depicted as follows:</span></span> 

![1](./media/project-ic-tasks/project-ic-1-tdsp-data-scientist.png)

- <span data-ttu-id="70167-109">**GroupUtilities** is the repository that your group is maintaining to share useful utilities across the entire group.</span><span class="sxs-lookup"><span data-stu-id="70167-109">**GroupUtilities** is the repository that your group is maintaining to share useful utilities across the entire group.</span></span> 
- <span data-ttu-id="70167-110">**TeamUtilities** is the repository that your team is maintaining specifically for your team.</span><span class="sxs-lookup"><span data-stu-id="70167-110">**TeamUtilities** is the repository that your team is maintaining specifically for your team.</span></span> 

<span data-ttu-id="70167-111">For instructions on how to execute a data science project under TDSP, see [Execution of Data Science Projects](project-execution.md).</span><span class="sxs-lookup"><span data-stu-id="70167-111">For instructions on how to execute a data science project under TDSP, see [Execution of Data Science Projects](project-execution.md).</span></span> 

>[AZURE.NOTE] <span data-ttu-id="70167-112">We outline the steps needed to set up a TDSP team environment using Azure DevOps in the following instructions.</span><span class="sxs-lookup"><span data-stu-id="70167-112">We outline the steps needed to set up a TDSP team environment using Azure DevOps in the following instructions.</span></span> <span data-ttu-id="70167-113">We specify how to accomplish these tasks with Azure DevOps because that is how we implement TDSP at Microsoft.</span><span class="sxs-lookup"><span data-stu-id="70167-113">We specify how to accomplish these tasks with Azure DevOps because that is how we implement TDSP at Microsoft.</span></span> <span data-ttu-id="70167-114">If another code-hosting platform is used for your group, the tasks that need to be completed by the team lead generally do not change.</span><span class="sxs-lookup"><span data-stu-id="70167-114">If another code-hosting platform is used for your group, the tasks that need to be completed by the team lead generally do not change.</span></span> <span data-ttu-id="70167-115">But the way to complete these tasks is going to be different.</span><span class="sxs-lookup"><span data-stu-id="70167-115">But the way to complete these tasks is going to be different.</span></span>


## <a name="repositories-and-directories"></a><span data-ttu-id="70167-116">Repositories and directories</span><span class="sxs-lookup"><span data-stu-id="70167-116">Repositories and directories</span></span>

<span data-ttu-id="70167-117">This tutorial uses abbreviated names for repositories and directories.</span><span class="sxs-lookup"><span data-stu-id="70167-117">This tutorial uses abbreviated names for repositories and directories.</span></span> <span data-ttu-id="70167-118">These names make it easier to follow the operations between the repositories and directories.</span><span class="sxs-lookup"><span data-stu-id="70167-118">These names make it easier to follow the operations between the repositories and directories.</span></span> <span data-ttu-id="70167-119">This notation (**R** for Git repositories and **D** for local directories on your DSVM) is used in the following sections:</span><span class="sxs-lookup"><span data-stu-id="70167-119">This notation (**R** for Git repositories and **D** for local directories on your DSVM) is used in the following sections:</span></span>

- <span data-ttu-id="70167-120">**R2**: The GroupUtilities repository on Git that your group manager has set up on your Azure DevOps group server.</span><span class="sxs-lookup"><span data-stu-id="70167-120">**R2**: The GroupUtilities repository on Git that your group manager has set up on your Azure DevOps group server.</span></span>
- <span data-ttu-id="70167-121">**R4**: The TeamUtilities repository on Git that your team lead has set up.</span><span class="sxs-lookup"><span data-stu-id="70167-121">**R4**: The TeamUtilities repository on Git that your team lead has set up.</span></span>
- <span data-ttu-id="70167-122">**R5**: The Project repository on Git that has been set up by your project lead.</span><span class="sxs-lookup"><span data-stu-id="70167-122">**R5**: The Project repository on Git that has been set up by your project lead.</span></span>
- <span data-ttu-id="70167-123">**D2**: The local directory cloned from R2.</span><span class="sxs-lookup"><span data-stu-id="70167-123">**D2**: The local directory cloned from R2.</span></span>
- <span data-ttu-id="70167-124">**D4**: The local directory cloned from R4.</span><span class="sxs-lookup"><span data-stu-id="70167-124">**D4**: The local directory cloned from R4.</span></span>
- <span data-ttu-id="70167-125">**D5**: The local directory cloned from R5.</span><span class="sxs-lookup"><span data-stu-id="70167-125">**D5**: The local directory cloned from R5.</span></span>


## <a name="step-0-prerequisites"></a><span data-ttu-id="70167-126">Step-0: Prerequisites</span><span class="sxs-lookup"><span data-stu-id="70167-126">Step-0: Prerequisites</span></span>

<span data-ttu-id="70167-127">The prerequisites are satisfied by completing the tasks assigned to your group manager outlined in [Group Manager tasks for a data science team](group-manager-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="70167-127">The prerequisites are satisfied by completing the tasks assigned to your group manager outlined in [Group Manager tasks for a data science team](group-manager-tasks.md).</span></span> <span data-ttu-id="70167-128">To summarize here, the following requirements need to be met before you begin the team lead tasks:</span><span class="sxs-lookup"><span data-stu-id="70167-128">To summarize here, the following requirements need to be met before you begin the team lead tasks:</span></span> 
- <span data-ttu-id="70167-129">Your group manager has set up the **GroupUtilities** repository (if any).</span><span class="sxs-lookup"><span data-stu-id="70167-129">Your group manager has set up the **GroupUtilities** repository (if any).</span></span> 
- <span data-ttu-id="70167-130">Your team lead has set up the **TeamUtilities** repository (if any).</span><span class="sxs-lookup"><span data-stu-id="70167-130">Your team lead has set up the **TeamUtilities** repository (if any).</span></span>
- <span data-ttu-id="70167-131">Your project lead has set up the project repository.</span><span class="sxs-lookup"><span data-stu-id="70167-131">Your project lead has set up the project repository.</span></span> 
- <span data-ttu-id="70167-132">You have been added to your project repository by your project lead with the privilege to clone from and push back to the project repository.</span><span class="sxs-lookup"><span data-stu-id="70167-132">You have been added to your project repository by your project lead with the privilege to clone from and push back to the project repository.</span></span>

<span data-ttu-id="70167-133">The second, **TeamUtilities** repository, prerequisite is optional, depending on whether your team has a team-specific utility repository.</span><span class="sxs-lookup"><span data-stu-id="70167-133">The second, **TeamUtilities** repository, prerequisite is optional, depending on whether your team has a team-specific utility repository.</span></span> <span data-ttu-id="70167-134">If any of other three prerequisites has not been completed, contact your team lead, your project lead, or their delegates to set it up by following the instructions for [Team Lead tasks for a data science team](team-lead-tasks.md) or for [Project Lead tasks for a data science team](project-lead-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="70167-134">If any of other three prerequisites has not been completed, contact your team lead, your project lead, or their delegates to set it up by following the instructions for [Team Lead tasks for a data science team](team-lead-tasks.md) or for [Project Lead tasks for a data science team](project-lead-tasks.md).</span></span>

- <span data-ttu-id="70167-135">Git must be installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="70167-135">Git must be installed on your machine.</span></span> <span data-ttu-id="70167-136">If you are using a Data Science Virtual Machine (DSVM), Git has been pre-installed and you are good to go.</span><span class="sxs-lookup"><span data-stu-id="70167-136">If you are using a Data Science Virtual Machine (DSVM), Git has been pre-installed and you are good to go.</span></span> <span data-ttu-id="70167-137">Otherwise, see the [Platforms and tools appendix](platforms-and-tools.md#appendix).</span><span class="sxs-lookup"><span data-stu-id="70167-137">Otherwise, see the [Platforms and tools appendix](platforms-and-tools.md#appendix).</span></span>  
- <span data-ttu-id="70167-138">If you are using a **Windows DSVM**, you need to have [Git Credential Manager (GCM)](https://github.com/Microsoft/Git-Credential-Manager-for-Windows) installed on your machine.</span><span class="sxs-lookup"><span data-stu-id="70167-138">If you are using a **Windows DSVM**, you need to have [Git Credential Manager (GCM)](https://github.com/Microsoft/Git-Credential-Manager-for-Windows) installed on your machine.</span></span> <span data-ttu-id="70167-139">In the README.md file, scroll down to the **Download and Install** section and click the *latest installer*.</span><span class="sxs-lookup"><span data-stu-id="70167-139">In the README.md file, scroll down to the **Download and Install** section and click the *latest installer*.</span></span> <span data-ttu-id="70167-140">This takes you to the latest installer page.</span><span class="sxs-lookup"><span data-stu-id="70167-140">This takes you to the latest installer page.</span></span> <span data-ttu-id="70167-141">Download the .exe installer from here and run it.</span><span class="sxs-lookup"><span data-stu-id="70167-141">Download the .exe installer from here and run it.</span></span> 
- <span data-ttu-id="70167-142">If you are using **Linux DSVM**, create an SSH public key on your DSVM and add it to your group Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="70167-142">If you are using **Linux DSVM**, create an SSH public key on your DSVM and add it to your group Azure DevOps Services.</span></span> <span data-ttu-id="70167-143">For more information about SSH, see the **Create SSH public key** section in the [Platforms and tools appendix](platforms-and-tools.md#appendix).</span><span class="sxs-lookup"><span data-stu-id="70167-143">For more information about SSH, see the **Create SSH public key** section in the [Platforms and tools appendix](platforms-and-tools.md#appendix).</span></span> 
- <span data-ttu-id="70167-144">If your team and/or project lead has created some Azure file storage that you need to mount to your DSVM, you should get the Azure file storage information from them.</span><span class="sxs-lookup"><span data-stu-id="70167-144">If your team and/or project lead has created some Azure file storage that you need to mount to your DSVM, you should get the Azure file storage information from them.</span></span> 

## <a name="step-1-3-clone-group-team-and-project-repositories-to-local-machine"></a><span data-ttu-id="70167-145">Step 1-3: Clone group, team, and project repositories to local machine</span><span class="sxs-lookup"><span data-stu-id="70167-145">Step 1-3: Clone group, team, and project repositories to local machine</span></span>

<span data-ttu-id="70167-146">This section provides instructions on completing the first three tasks of project individual contributors:</span><span class="sxs-lookup"><span data-stu-id="70167-146">This section provides instructions on completing the first three tasks of project individual contributors:</span></span> 

- <span data-ttu-id="70167-147">Clone the **GroupUtilities** repository R2 to D2</span><span class="sxs-lookup"><span data-stu-id="70167-147">Clone the **GroupUtilities** repository R2 to D2</span></span>
- <span data-ttu-id="70167-148">Clone the **TeamUtilities** repository R4 to D4</span><span class="sxs-lookup"><span data-stu-id="70167-148">Clone the **TeamUtilities** repository R4 to D4</span></span> 
- <span data-ttu-id="70167-149">Clone the **Project** repository R5 to D5.</span><span class="sxs-lookup"><span data-stu-id="70167-149">Clone the **Project** repository R5 to D5.</span></span>

<span data-ttu-id="70167-150">On your local machine, create a directory ***C:\GitRepos*** (for Windows) or ***$home/GitRepos*** (forLinux), and then change to that directory.</span><span class="sxs-lookup"><span data-stu-id="70167-150">On your local machine, create a directory ***C:\GitRepos*** (for Windows) or ***$home/GitRepos*** (forLinux), and then change to that directory.</span></span> 

<span data-ttu-id="70167-151">Run the one of the following commands (as appropriate for your OS) to clone your **GroupUtilities**, **TeamUtilities**, and **Project** repositories to directories on your local machine:</span><span class="sxs-lookup"><span data-stu-id="70167-151">Run the one of the following commands (as appropriate for your OS) to clone your **GroupUtilities**, **TeamUtilities**, and **Project** repositories to directories on your local machine:</span></span> 

<span data-ttu-id="70167-152">**Windows**</span><span class="sxs-lookup"><span data-stu-id="70167-152">**Windows**</span></span>
    
    git clone <the URL of the GroupUtilities repository>
    git clone <the URL of the TeamUtilities repository>
    git clone <the URL of the Project repository>
    
![2](./media/project-ic-tasks/project-ic-2-clone-three-repo-to-ic.png)

<span data-ttu-id="70167-154">Confirm that you see the three folders under your project directory.</span><span class="sxs-lookup"><span data-stu-id="70167-154">Confirm that you see the three folders under your project directory.</span></span>

![3](./media/project-ic-tasks/project-ic-3-three-repo-cloned-to-ic.png)

<span data-ttu-id="70167-156">**Linux**</span><span class="sxs-lookup"><span data-stu-id="70167-156">**Linux**</span></span>
    
    git clone <the SSH URL of the GroupUtilities repository>
    git clone <the SSH URL of the TeamUtilities repository>
    git clone <the SSH URL of the Project repository>

![4](./media/project-ic-tasks/project-ic-4-clone-three-repo-to_ic-linux.png)

<span data-ttu-id="70167-158">Confirm that you see the three  folders under your project directory.</span><span class="sxs-lookup"><span data-stu-id="70167-158">Confirm that you see the three  folders under your project directory.</span></span>

![5](./media/project-ic-tasks/project-ic-5-three-repo-cloned-to-ic-linux.png)

## <a name="step-4-5-mount-azure-file-storage-to-your-dsvm-optional"></a><span data-ttu-id="70167-160">Step 4-5: Mount Azure file storage to your DSVM (Optional)</span><span class="sxs-lookup"><span data-stu-id="70167-160">Step 4-5: Mount Azure file storage to your DSVM (Optional)</span></span>

<span data-ttu-id="70167-161">To mount Azure file storage to your DSVM, see the instructions in Section 4 of the [Team lead tasks for a data science team](team-lead-tasks.md)</span><span class="sxs-lookup"><span data-stu-id="70167-161">To mount Azure file storage to your DSVM, see the instructions in Section 4 of the [Team lead tasks for a data science team](team-lead-tasks.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="70167-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="70167-162">Next steps</span></span>

<span data-ttu-id="70167-163">Here are links to the more detailed descriptions of the roles and tasks defined by the Team Data Science Process:</span><span class="sxs-lookup"><span data-stu-id="70167-163">Here are links to the more detailed descriptions of the roles and tasks defined by the Team Data Science Process:</span></span>

- [<span data-ttu-id="70167-164">Group Manager tasks for a data science team</span><span class="sxs-lookup"><span data-stu-id="70167-164">Group Manager tasks for a data science team</span></span>](group-manager-tasks.md)
- [<span data-ttu-id="70167-165">Team Lead tasks for a data science team</span><span class="sxs-lookup"><span data-stu-id="70167-165">Team Lead tasks for a data science team</span></span>](team-lead-tasks.md)
- [<span data-ttu-id="70167-166">Project Lead tasks for a data science team</span><span class="sxs-lookup"><span data-stu-id="70167-166">Project Lead tasks for a data science team</span></span>](project-lead-tasks.md)
- [<span data-ttu-id="70167-167">Project Individual Contributors for a data science team</span><span class="sxs-lookup"><span data-stu-id="70167-167">Project Individual Contributors for a data science team</span></span>](project-ic-tasks.md)

