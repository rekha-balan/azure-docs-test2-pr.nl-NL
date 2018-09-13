---
title: Agile development of data science projects - Azure Machine Learning | Microsoft Docs
description: How developers can execute a data science project in a systematic, version controlled, and collaborative way within a project team by using the Team Data Science Process.
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
ms.date: 11/28/2017
ms.author: deguhath
ms.openlocfilehash: a032127d249f944d08cc6578a03f1a7e5a658361
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871613"
---
# <a name="agile-development-of-data-science-projects"></a><span data-ttu-id="cf460-103">Agile development of data science projects</span><span class="sxs-lookup"><span data-stu-id="cf460-103">Agile development of data science projects</span></span>

<span data-ttu-id="cf460-104">This document describes how developers can execute a data science project in a systematic, version controlled, and collaborative way within a project team by using the [Team Data Science Process](overview.md) (TDSP).</span><span class="sxs-lookup"><span data-stu-id="cf460-104">This document describes how developers can execute a data science project in a systematic, version controlled, and collaborative way within a project team by using the [Team Data Science Process](overview.md) (TDSP).</span></span> <span data-ttu-id="cf460-105">The TDSP is a framework developed by Microsoft that provides a structured sequence of activities to execute cloud-based, predictive analytics solutions efficiently.</span><span class="sxs-lookup"><span data-stu-id="cf460-105">The TDSP is a framework developed by Microsoft that provides a structured sequence of activities to execute cloud-based, predictive analytics solutions efficiently.</span></span> <span data-ttu-id="cf460-106">For an outline of the personnel roles, and their associated tasks that are handled by a data science team standardizing on this process, see [Team Data Science Process roles and tasks](roles-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="cf460-106">For an outline of the personnel roles, and their associated tasks that are handled by a data science team standardizing on this process, see [Team Data Science Process roles and tasks](roles-tasks.md).</span></span> 

<span data-ttu-id="cf460-107">This article includes instructions on how to:</span><span class="sxs-lookup"><span data-stu-id="cf460-107">This article includes instructions on how to:</span></span> 

1. <span data-ttu-id="cf460-108">do **sprint planning** for work items involved in a project.</span><span class="sxs-lookup"><span data-stu-id="cf460-108">do **sprint planning** for work items involved in a project.</span></span><br> <span data-ttu-id="cf460-109">If you are unfamiliar with sprint planning, you can find details and general information [here](https://en.wikipedia.org/wiki/Sprint_(software_development) "here").</span><span class="sxs-lookup"><span data-stu-id="cf460-109">If you are unfamiliar with sprint planning, you can find details and general information [here](https://en.wikipedia.org/wiki/Sprint_(software_development) "here").</span></span> 
2. <span data-ttu-id="cf460-110">**add work items** to sprints.</span><span class="sxs-lookup"><span data-stu-id="cf460-110">**add work items** to sprints.</span></span> 

> [!NOTE]
> <span data-ttu-id="cf460-111">The steps needed to set up a TDSP team environment using Azure DevOps Services are outlined in the following set of instructions.</span><span class="sxs-lookup"><span data-stu-id="cf460-111">The steps needed to set up a TDSP team environment using Azure DevOps Services are outlined in the following set of instructions.</span></span> <span data-ttu-id="cf460-112">They specify how to accomplish these tasks with Azure DevOps Services because that is how to implement TDSP at Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cf460-112">They specify how to accomplish these tasks with Azure DevOps Services because that is how to implement TDSP at Microsoft.</span></span>  <span data-ttu-id="cf460-113">If you choose to use Azure DevOps Services, items (3) and (4) in the previous list are benefits that you get naturally.</span><span class="sxs-lookup"><span data-stu-id="cf460-113">If you choose to use Azure DevOps Services, items (3) and (4) in the previous list are benefits that you get naturally.</span></span> <span data-ttu-id="cf460-114">If another code hosting platform is used for your group, the tasks that need to be completed by the team lead generally do not change.</span><span class="sxs-lookup"><span data-stu-id="cf460-114">If another code hosting platform is used for your group, the tasks that need to be completed by the team lead generally do not change.</span></span> <span data-ttu-id="cf460-115">But the way to complete these tasks is going to be different.</span><span class="sxs-lookup"><span data-stu-id="cf460-115">But the way to complete these tasks is going to be different.</span></span> <span data-ttu-id="cf460-116">For example, the item in section six, **Link a work item with a Git branch**, might not be as easy as it is on Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="cf460-116">For example, the item in section six, **Link a work item with a Git branch**, might not be as easy as it is on Azure DevOps Services.</span></span>
>
>

<span data-ttu-id="cf460-117">The following figure illustrates a typical sprint planning, coding, and source-control workflow involved in implementing a data science project:</span><span class="sxs-lookup"><span data-stu-id="cf460-117">The following figure illustrates a typical sprint planning, coding, and source-control workflow involved in implementing a data science project:</span></span>

![1](./media/agile-development/1-project-execute.png)


##  <span data-ttu-id="cf460-119">1. <a name='Terminology-1'></a>Terminology</span><span class="sxs-lookup"><span data-stu-id="cf460-119">1. <a name='Terminology-1'></a>Terminology</span></span> 

<span data-ttu-id="cf460-120">In the TDSP sprint planning framework, there are four frequently used types of **work items**: **Feature**, **User Story**, **Task**, and **Bug**.</span><span class="sxs-lookup"><span data-stu-id="cf460-120">In the TDSP sprint planning framework, there are four frequently used types of **work items**: **Feature**, **User Story**, **Task**, and **Bug**.</span></span> <span data-ttu-id="cf460-121">Each project maintains a single backlog for all work items.</span><span class="sxs-lookup"><span data-stu-id="cf460-121">Each project maintains a single backlog for all work items.</span></span> <span data-ttu-id="cf460-122">There is no backlog at the Git repository level under a project.</span><span class="sxs-lookup"><span data-stu-id="cf460-122">There is no backlog at the Git repository level under a project.</span></span> <span data-ttu-id="cf460-123">Here are their definitions:</span><span class="sxs-lookup"><span data-stu-id="cf460-123">Here are their definitions:</span></span>

- <span data-ttu-id="cf460-124">**Feature**: A feature corresponds to a project engagement.</span><span class="sxs-lookup"><span data-stu-id="cf460-124">**Feature**: A feature corresponds to a project engagement.</span></span> <span data-ttu-id="cf460-125">Different engagements with a client are considered different features.</span><span class="sxs-lookup"><span data-stu-id="cf460-125">Different engagements with a client are considered different features.</span></span> <span data-ttu-id="cf460-126">Similarly, it is best to consider different phases of a project with a client as different features.</span><span class="sxs-lookup"><span data-stu-id="cf460-126">Similarly, it is best to consider different phases of a project with a client as different features.</span></span> <span data-ttu-id="cf460-127">If you choose a schema such as ***ClientName-EngagementName*** to name your features, then you can easily recognize the context of the project/engagement from the names themselves.</span><span class="sxs-lookup"><span data-stu-id="cf460-127">If you choose a schema such as ***ClientName-EngagementName*** to name your features, then you can easily recognize the context of the project/engagement from the names themselves.</span></span>
- <span data-ttu-id="cf460-128">**Story**: Stories are different work items that are needed to complete a feature (project) end-to-end.</span><span class="sxs-lookup"><span data-stu-id="cf460-128">**Story**: Stories are different work items that are needed to complete a feature (project) end-to-end.</span></span> <span data-ttu-id="cf460-129">Examples of stories include:</span><span class="sxs-lookup"><span data-stu-id="cf460-129">Examples of stories include:</span></span>
    - <span data-ttu-id="cf460-130">Getting Data</span><span class="sxs-lookup"><span data-stu-id="cf460-130">Getting Data</span></span> 
    - <span data-ttu-id="cf460-131">Exploring Data</span><span class="sxs-lookup"><span data-stu-id="cf460-131">Exploring Data</span></span> 
    - <span data-ttu-id="cf460-132">Generating Features</span><span class="sxs-lookup"><span data-stu-id="cf460-132">Generating Features</span></span>
    - <span data-ttu-id="cf460-133">Building Models</span><span class="sxs-lookup"><span data-stu-id="cf460-133">Building Models</span></span>
    - <span data-ttu-id="cf460-134">Operationalizing Models</span><span class="sxs-lookup"><span data-stu-id="cf460-134">Operationalizing Models</span></span> 
    - <span data-ttu-id="cf460-135">Retraining Models</span><span class="sxs-lookup"><span data-stu-id="cf460-135">Retraining Models</span></span>
- <span data-ttu-id="cf460-136">**Task**: Tasks are assignable code or document work items or other activities that need to be done to complete a specific story.</span><span class="sxs-lookup"><span data-stu-id="cf460-136">**Task**: Tasks are assignable code or document work items or other activities that need to be done to complete a specific story.</span></span> <span data-ttu-id="cf460-137">For example, tasks in the story *Getting Data* could be:</span><span class="sxs-lookup"><span data-stu-id="cf460-137">For example, tasks in the story *Getting Data* could be:</span></span>
    -  <span data-ttu-id="cf460-138">Getting Credentials of SQL Server</span><span class="sxs-lookup"><span data-stu-id="cf460-138">Getting Credentials of SQL Server</span></span> 
    -  <span data-ttu-id="cf460-139">Uploading Data to SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cf460-139">Uploading Data to SQL Data Warehouse.</span></span> 
- <span data-ttu-id="cf460-140">**Bug**: Bugs usually refer to fixes that are needed for an existing code or document that are done when completing a task.</span><span class="sxs-lookup"><span data-stu-id="cf460-140">**Bug**: Bugs usually refer to fixes that are needed for an existing code or document that are done when completing a task.</span></span> <span data-ttu-id="cf460-141">If the bug is caused by missing stages or tasks respectively, it can escalate to being a story or a task.</span><span class="sxs-lookup"><span data-stu-id="cf460-141">If the bug is caused by missing stages or tasks respectively, it can escalate to being a story or a task.</span></span> 

> [!NOTE]
> <span data-ttu-id="cf460-142">Concepts are borrowed of features, stories, tasks, and bugs from software code management (SCM) to be used in data science.</span><span class="sxs-lookup"><span data-stu-id="cf460-142">Concepts are borrowed of features, stories, tasks, and bugs from software code management (SCM) to be used in data science.</span></span> <span data-ttu-id="cf460-143">They might differ slightly from their conventional SCM definitions.</span><span class="sxs-lookup"><span data-stu-id="cf460-143">They might differ slightly from their conventional SCM definitions.</span></span>
>
>

> [!NOTE]
> <span data-ttu-id="cf460-144">Data scientists may feel more comfortable using an agile template that specifically aligns with the TDSP lifecycle stages.</span><span class="sxs-lookup"><span data-stu-id="cf460-144">Data scientists may feel more comfortable using an agile template that specifically aligns with the TDSP lifecycle stages.</span></span> <span data-ttu-id="cf460-145">With that in mind, an Agile-derived sprint planning template has been created, where Epics, Stories etc. are replaced by TDSP lifecycle stages or substages.</span><span class="sxs-lookup"><span data-stu-id="cf460-145">With that in mind, an Agile-derived sprint planning template has been created, where Epics, Stories etc. are replaced by TDSP lifecycle stages or substages.</span></span> <span data-ttu-id="cf460-146">For instructions on how to create an agile template, see [Set up agile data science process in Visual Studio Online](agile-development.md#set-up-agile-dsp-6).</span><span class="sxs-lookup"><span data-stu-id="cf460-146">For instructions on how to create an agile template, see [Set up agile data science process in Visual Studio Online](agile-development.md#set-up-agile-dsp-6).</span></span>
>
>

## <span data-ttu-id="cf460-147">2. <a name='SprintPlanning-2'></a>Sprint planning</span><span class="sxs-lookup"><span data-stu-id="cf460-147">2. <a name='SprintPlanning-2'></a>Sprint planning</span></span> 

<span data-ttu-id="cf460-148">Sprint planning is useful for project prioritization, and resource planning and allocation.</span><span class="sxs-lookup"><span data-stu-id="cf460-148">Sprint planning is useful for project prioritization, and resource planning and allocation.</span></span> <span data-ttu-id="cf460-149">Many data scientists are engaged with multiple projects, each of which can take months to complete.</span><span class="sxs-lookup"><span data-stu-id="cf460-149">Many data scientists are engaged with multiple projects, each of which can take months to complete.</span></span> <span data-ttu-id="cf460-150">Projects often proceed at different paces.</span><span class="sxs-lookup"><span data-stu-id="cf460-150">Projects often proceed at different paces.</span></span> <span data-ttu-id="cf460-151">On the Azure DevOps Services, you can easily create, manage, and track work items in your project and conduct sprint planning to ensure that your projects are moving forward as expected.</span><span class="sxs-lookup"><span data-stu-id="cf460-151">On the Azure DevOps Services, you can easily create, manage, and track work items in your project and conduct sprint planning to ensure that your projects are moving forward as expected.</span></span> 

<span data-ttu-id="cf460-152">Follow [this link](https://www.visualstudio.com/en-us/docs/work/scrum/sprint-planning) for the step-by-step instructions on sprint planning in Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="cf460-152">Follow [this link](https://www.visualstudio.com/en-us/docs/work/scrum/sprint-planning) for the step-by-step instructions on sprint planning in Azure DevOps Services.</span></span> 


## <span data-ttu-id="cf460-153">3. <a name='AddFeature-3'></a>Add a feature</span><span class="sxs-lookup"><span data-stu-id="cf460-153">3. <a name='AddFeature-3'></a>Add a feature</span></span>  

<span data-ttu-id="cf460-154">After your project repository is created under a project, go to the team **Overview** page and click **Manage work**.</span><span class="sxs-lookup"><span data-stu-id="cf460-154">After your project repository is created under a project, go to the team **Overview** page and click **Manage work**.</span></span>

![2](./media/agile-development/2-sprint-team-overview.png)

<span data-ttu-id="cf460-156">To include a feature in the backlog, click **Backlogs** --> **Features** --> **New**, type in the feature **Title** (usually your project name), and then click **Add** .</span><span class="sxs-lookup"><span data-stu-id="cf460-156">To include a feature in the backlog, click **Backlogs** --> **Features** --> **New**, type in the feature **Title** (usually your project name), and then click **Add** .</span></span>

![3](./media/agile-development/3-sprint-team-add-work.png)

<span data-ttu-id="cf460-158">Double-click the feature you created.</span><span class="sxs-lookup"><span data-stu-id="cf460-158">Double-click the feature you created.</span></span> <span data-ttu-id="cf460-159">Fill in the descriptions, assign team members for this feature, and set planning parameters for this feature.</span><span class="sxs-lookup"><span data-stu-id="cf460-159">Fill in the descriptions, assign team members for this feature, and set planning parameters for this feature.</span></span> 

<span data-ttu-id="cf460-160">You can also link this feature to the project repository.</span><span class="sxs-lookup"><span data-stu-id="cf460-160">You can also link this feature to the project repository.</span></span> <span data-ttu-id="cf460-161">Click **Add link** under the **Development** section.</span><span class="sxs-lookup"><span data-stu-id="cf460-161">Click **Add link** under the **Development** section.</span></span> <span data-ttu-id="cf460-162">After you have finished editing the feature, click **Save & Close** to exit.</span><span class="sxs-lookup"><span data-stu-id="cf460-162">After you have finished editing the feature, click **Save & Close** to exit.</span></span>


## <span data-ttu-id="cf460-163">4. <a name='AddStoryunderfeature-4'></a>Add Story under feature</span><span class="sxs-lookup"><span data-stu-id="cf460-163">4. <a name='AddStoryunderfeature-4'></a>Add Story under feature</span></span> 

<span data-ttu-id="cf460-164">Under the feature, stories can be added to describe major steps needed to finish the (feature) project.</span><span class="sxs-lookup"><span data-stu-id="cf460-164">Under the feature, stories can be added to describe major steps needed to finish the (feature) project.</span></span> <span data-ttu-id="cf460-165">To add a new story, click the **+** sign to the left of the feature in backlog view.</span><span class="sxs-lookup"><span data-stu-id="cf460-165">To add a new story, click the **+** sign to the left of the feature in backlog view.</span></span>  

![4](./media/agile-development/4-sprint-add-story.png)

<span data-ttu-id="cf460-167">You can edit the details of the story, such as the status, description, comments, planning, and priority In the pop-up window.</span><span class="sxs-lookup"><span data-stu-id="cf460-167">You can edit the details of the story, such as the status, description, comments, planning, and priority In the pop-up window.</span></span>

![5](./media/agile-development/5-sprint-edit-story.png)

<span data-ttu-id="cf460-169">You can link this story to an existing repository by clicking **+ Add link** under **Development**.</span><span class="sxs-lookup"><span data-stu-id="cf460-169">You can link this story to an existing repository by clicking **+ Add link** under **Development**.</span></span> 

![6](./media/agile-development/6-sprint-link-existing-branch.png)


## <span data-ttu-id="cf460-171">5. <a name='AddTaskunderstory-5'></a>Add a task to a story</span><span class="sxs-lookup"><span data-stu-id="cf460-171">5. <a name='AddTaskunderstory-5'></a>Add a task to a story</span></span> 

<span data-ttu-id="cf460-172">Tasks are specific detailed steps that are needed to complete each story.</span><span class="sxs-lookup"><span data-stu-id="cf460-172">Tasks are specific detailed steps that are needed to complete each story.</span></span> <span data-ttu-id="cf460-173">After all tasks of a story are completed, the story should be completed too.</span><span class="sxs-lookup"><span data-stu-id="cf460-173">After all tasks of a story are completed, the story should be completed too.</span></span> 

<span data-ttu-id="cf460-174">To add a task to a story, click the **+** sign next to the story item, select **Task**, and then fill in the detailed information of this task in the pop-up window.</span><span class="sxs-lookup"><span data-stu-id="cf460-174">To add a task to a story, click the **+** sign next to the story item, select **Task**, and then fill in the detailed information of this task in the pop-up window.</span></span>

![7](./media/agile-development/7-sprint-add-task.png)

<span data-ttu-id="cf460-176">After the features, stories, and tasks are created, you can view them in the **Backlog** or **Board** views to track their status.</span><span class="sxs-lookup"><span data-stu-id="cf460-176">After the features, stories, and tasks are created, you can view them in the **Backlog** or **Board** views to track their status.</span></span>

![8](./media/agile-development/8-sprint-backlog-view.png)

![9](./media/agile-development/9-link-to-a-new-branch.png)


## <span data-ttu-id="cf460-179">6. <a name='set-up-agile-dsp-6'></a> Set up an Agile TDSP work template in Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="cf460-179">6. <a name='set-up-agile-dsp-6'></a> Set up an Agile TDSP work template in Visual Studio Online</span></span>

<span data-ttu-id="cf460-180">This article explains how to set up an agile data science process template that uses the TDSP data science lifecycle stages and tracks work items with Visual Studio Online (vso).</span><span class="sxs-lookup"><span data-stu-id="cf460-180">This article explains how to set up an agile data science process template that uses the TDSP data science lifecycle stages and tracks work items with Visual Studio Online (vso).</span></span> <span data-ttu-id="cf460-181">The steps below walk through an example of setting up the data science-specific agile process template *AgileDataScienceProcess* and show how to create data science work items based on the template.</span><span class="sxs-lookup"><span data-stu-id="cf460-181">The steps below walk through an example of setting up the data science-specific agile process template *AgileDataScienceProcess* and show how to create data science work items based on the template.</span></span>

### <a name="agile-data-science-process-template-setup"></a><span data-ttu-id="cf460-182">Agile Data Science Process Template Setup</span><span class="sxs-lookup"><span data-stu-id="cf460-182">Agile Data Science Process Template Setup</span></span>

1. <span data-ttu-id="cf460-183">Navigate to server homepage,  **Configure** -> **Process**.</span><span class="sxs-lookup"><span data-stu-id="cf460-183">Navigate to server homepage,  **Configure** -> **Process**.</span></span>

    ![10](./media/agile-development/10-settings.png) 

2. <span data-ttu-id="cf460-185">Navigate to **All processes** -> **Processes**, under **Agile** and click on **Create inherited process**.</span><span class="sxs-lookup"><span data-stu-id="cf460-185">Navigate to **All processes** -> **Processes**, under **Agile** and click on **Create inherited process**.</span></span> <span data-ttu-id="cf460-186">Then put the process name "AgileDataScienceProcess" and click **Create process**.</span><span class="sxs-lookup"><span data-stu-id="cf460-186">Then put the process name "AgileDataScienceProcess" and click **Create process**.</span></span>

    ![11](./media/agile-development/11-agileds.png)

3. <span data-ttu-id="cf460-188">Under the **AgileDataScienceProcess** -> **Work item types** tab, disable **Epic**, **Feature**, **User Story**, and **Task** work item types by **Configure -> Disable**</span><span class="sxs-lookup"><span data-stu-id="cf460-188">Under the **AgileDataScienceProcess** -> **Work item types** tab, disable **Epic**, **Feature**, **User Story**, and **Task** work item types by **Configure -> Disable**</span></span>

    ![12](./media/agile-development/12-disable.png)

4. <span data-ttu-id="cf460-190">Navigate to **AgileDataScienceProcess** -> **Backlog levels** tab. Rename "Epics" to "TDSP Projects" by  clicking on the **Configure** -> **Edit/Rename**.</span><span class="sxs-lookup"><span data-stu-id="cf460-190">Navigate to **AgileDataScienceProcess** -> **Backlog levels** tab. Rename "Epics" to "TDSP Projects" by  clicking on the **Configure** -> **Edit/Rename**.</span></span> <span data-ttu-id="cf460-191">In the same dialog box, click **+New work item type** in "Data Science Project" and set the value of **Default work item type** to "TDSP Project"</span><span class="sxs-lookup"><span data-stu-id="cf460-191">In the same dialog box, click **+New work item type** in "Data Science Project" and set the value of **Default work item type** to "TDSP Project"</span></span> 

    ![13](./media/agile-development/13-rename.png)  

5. <span data-ttu-id="cf460-193">Similarly, change Backlog name "Features" to "TDSP Stages" and add the following to the **New work item type**:</span><span class="sxs-lookup"><span data-stu-id="cf460-193">Similarly, change Backlog name "Features" to "TDSP Stages" and add the following to the **New work item type**:</span></span>

    - <span data-ttu-id="cf460-194">Business Understanding</span><span class="sxs-lookup"><span data-stu-id="cf460-194">Business Understanding</span></span>
    - <span data-ttu-id="cf460-195">Data Acquisition</span><span class="sxs-lookup"><span data-stu-id="cf460-195">Data Acquisition</span></span>
    - <span data-ttu-id="cf460-196">Modeling</span><span class="sxs-lookup"><span data-stu-id="cf460-196">Modeling</span></span>
    - <span data-ttu-id="cf460-197">Deployment</span><span class="sxs-lookup"><span data-stu-id="cf460-197">Deployment</span></span>

6. <span data-ttu-id="cf460-198">Rename "User Story" to "TDSP Substages" with default work item type set to newly created "TDSP Substage" type.</span><span class="sxs-lookup"><span data-stu-id="cf460-198">Rename "User Story" to "TDSP Substages" with default work item type set to newly created "TDSP Substage" type.</span></span>

7. <span data-ttu-id="cf460-199">Set the "Tasks" to newly created Work item type "TDSP Task"</span><span class="sxs-lookup"><span data-stu-id="cf460-199">Set the "Tasks" to newly created Work item type "TDSP Task"</span></span> 

8. <span data-ttu-id="cf460-200">After these steps, the Backlog levels should look like this:</span><span class="sxs-lookup"><span data-stu-id="cf460-200">After these steps, the Backlog levels should look like this:</span></span>

    ![14](./media/agile-development/14-template.png)  

 
### <a name="create-data-science-work-items"></a><span data-ttu-id="cf460-202">Create Data Science Work Items</span><span class="sxs-lookup"><span data-stu-id="cf460-202">Create Data Science Work Items</span></span>

<span data-ttu-id="cf460-203">After the data science process template is created, you can create and track your data science work items that correspond to the TDSP lifecycle.</span><span class="sxs-lookup"><span data-stu-id="cf460-203">After the data science process template is created, you can create and track your data science work items that correspond to the TDSP lifecycle.</span></span>

1. <span data-ttu-id="cf460-204">When you create a new project, select "Agile\AgileDataScienceProcess" as the **Work item process**:</span><span class="sxs-lookup"><span data-stu-id="cf460-204">When you create a new project, select "Agile\AgileDataScienceProcess" as the **Work item process**:</span></span>

    ![15](./media/agile-development/15-newproject.png)

2. <span data-ttu-id="cf460-206">Navigate to the newly created project, and click on **Work** -> **Backlogs**.</span><span class="sxs-lookup"><span data-stu-id="cf460-206">Navigate to the newly created project, and click on **Work** -> **Backlogs**.</span></span>

3. <span data-ttu-id="cf460-207">Make "TDSP Projects" visible by clicking on **Configure team settings** and check "TDSP Projects"; then save.</span><span class="sxs-lookup"><span data-stu-id="cf460-207">Make "TDSP Projects" visible by clicking on **Configure team settings** and check "TDSP Projects"; then save.</span></span>

    ![16](./media/agile-development/16-enabledsprojects.png)

4. <span data-ttu-id="cf460-209">Now you can start creating the data science-specific work items.</span><span class="sxs-lookup"><span data-stu-id="cf460-209">Now you can start creating the data science-specific work items.</span></span>

    ![17](./media/agile-development/17-dsworkitems.png)

5. <span data-ttu-id="cf460-211">Here is an example of how the data science project work items should appear:</span><span class="sxs-lookup"><span data-stu-id="cf460-211">Here is an example of how the data science project work items should appear:</span></span>

    ![18](./media/agile-development/18-workitems.png)


## <a name="next-steps"></a><span data-ttu-id="cf460-213">Next steps</span><span class="sxs-lookup"><span data-stu-id="cf460-213">Next steps</span></span>

<span data-ttu-id="cf460-214">[Collaborative coding with Git](collaborative-coding-with-git.md) describes how to do collaborative code development for data science projects using Git as the shared code development framework and how to link these coding activities to the work planned with the agile process.</span><span class="sxs-lookup"><span data-stu-id="cf460-214">[Collaborative coding with Git](collaborative-coding-with-git.md) describes how to do collaborative code development for data science projects using Git as the shared code development framework and how to link these coding activities to the work planned with the agile process.</span></span>

<span data-ttu-id="cf460-215">Here are additional links to resources on agile processes.</span><span class="sxs-lookup"><span data-stu-id="cf460-215">Here are additional links to resources on agile processes.</span></span>

- <span data-ttu-id="cf460-216">Agile process   [https://www.visualstudio.com/en-us/docs/work/guidance/agile-process](https://www.visualstudio.com/en-us/docs/work/guidance/agile-process)</span><span class="sxs-lookup"><span data-stu-id="cf460-216">Agile process   [https://www.visualstudio.com/en-us/docs/work/guidance/agile-process](https://www.visualstudio.com/en-us/docs/work/guidance/agile-process)</span></span>
- <span data-ttu-id="cf460-217">Agile process work item types and workflow   [https://www.visualstudio.com/en-us/docs/work/guidance/agile-process-workflow](https://www.visualstudio.com/en-us/docs/work/guidance/agile-process-workflow)</span><span class="sxs-lookup"><span data-stu-id="cf460-217">Agile process work item types and workflow   [https://www.visualstudio.com/en-us/docs/work/guidance/agile-process-workflow](https://www.visualstudio.com/en-us/docs/work/guidance/agile-process-workflow)</span></span>


<span data-ttu-id="cf460-218">Walkthroughs that demonstrate all the steps in the process for **specific scenarios** are also provided.</span><span class="sxs-lookup"><span data-stu-id="cf460-218">Walkthroughs that demonstrate all the steps in the process for **specific scenarios** are also provided.</span></span> <span data-ttu-id="cf460-219">They are listed and linked with thumbnail descriptions in the [Example walkthroughs](walkthroughs.md) article.</span><span class="sxs-lookup"><span data-stu-id="cf460-219">They are listed and linked with thumbnail descriptions in the [Example walkthroughs](walkthroughs.md) article.</span></span> <span data-ttu-id="cf460-220">They illustrate how to combine cloud, on-premises tools, and services into a workflow or pipeline to create an intelligent application.</span><span class="sxs-lookup"><span data-stu-id="cf460-220">They illustrate how to combine cloud, on-premises tools, and services into a workflow or pipeline to create an intelligent application.</span></span> 
