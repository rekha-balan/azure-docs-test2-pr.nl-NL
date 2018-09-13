---
title: Collaborative coding with Git - Azure Machine Learning | Microsoft Docs
description: How to do collaborative code development for data science projects using Git with agile planning.
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
ms.openlocfilehash: 78bbdb244d9bd52a06623f7a6fa3bca123ef3828
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870988"
---
# <a name="collaborative-coding-with-git"></a><span data-ttu-id="e2de7-103">Collaborative coding with Git</span><span class="sxs-lookup"><span data-stu-id="e2de7-103">Collaborative coding with Git</span></span>

<span data-ttu-id="e2de7-104">In this article we describe how to do collaborative code development for data science projects using Git as the shared code development framework.</span><span class="sxs-lookup"><span data-stu-id="e2de7-104">In this article we describe how to do collaborative code development for data science projects using Git as the shared code development framework.</span></span> <span data-ttu-id="e2de7-105">It covers how to link these coding activities to the work planned in [Agile development](agile-development.md) and how to do code reviews.</span><span class="sxs-lookup"><span data-stu-id="e2de7-105">It covers how to link these coding activities to the work planned in [Agile development](agile-development.md) and how to do code reviews.</span></span>


## <span data-ttu-id="e2de7-106">1. <a name='Linkaworkitemwithagitbranch-1'></a>Link a work item with a Git branch</span><span class="sxs-lookup"><span data-stu-id="e2de7-106">1. <a name='Linkaworkitemwithagitbranch-1'></a>Link a work item with a Git branch</span></span> 

<span data-ttu-id="e2de7-107">Azure DevOps Services provides a convenient way to connect a work item (a story or task) with a Git branch.</span><span class="sxs-lookup"><span data-stu-id="e2de7-107">Azure DevOps Services provides a convenient way to connect a work item (a story or task) with a Git branch.</span></span> <span data-ttu-id="e2de7-108">This enables you to link your story or task directly to the code associated with it.</span><span class="sxs-lookup"><span data-stu-id="e2de7-108">This enables you to link your story or task directly to the code associated with it.</span></span> 

<span data-ttu-id="e2de7-109">To connect a work item to a new branch, double-click a work item, and in the pop-up window, click **Create a new branch** under **+ Add link**.</span><span class="sxs-lookup"><span data-stu-id="e2de7-109">To connect a work item to a new branch, double-click a work item, and in the pop-up window, click **Create a new branch** under **+ Add link**.</span></span>  

![1](./media/collaborative-coding-with-git/1-sprint-board-view.png)

<span data-ttu-id="e2de7-111">Provide the information for this new branch, such as the branch name, base Git repository, and the branch.</span><span class="sxs-lookup"><span data-stu-id="e2de7-111">Provide the information for this new branch, such as the branch name, base Git repository, and the branch.</span></span> <span data-ttu-id="e2de7-112">The Git repository  chosen must be the repository under the same project that the work item belongs to.</span><span class="sxs-lookup"><span data-stu-id="e2de7-112">The Git repository  chosen must be the repository under the same project that the work item belongs to.</span></span> <span data-ttu-id="e2de7-113">The base branch can be the master branch or some other existing branch.</span><span class="sxs-lookup"><span data-stu-id="e2de7-113">The base branch can be the master branch or some other existing branch.</span></span>

![2](./media/collaborative-coding-with-git/2-create-a-branch.png)

<span data-ttu-id="e2de7-115">A good practice is to create a Git branch for each story work item.</span><span class="sxs-lookup"><span data-stu-id="e2de7-115">A good practice is to create a Git branch for each story work item.</span></span> <span data-ttu-id="e2de7-116">Then, for each task work item, you create a branch based on the story branch.</span><span class="sxs-lookup"><span data-stu-id="e2de7-116">Then, for each task work item, you create a branch based on the story branch.</span></span> <span data-ttu-id="e2de7-117">Organizing the branches in this hierarchical way that corresponds to the story-task relationships is helpful when you have multiple people working on different stories of the same project, or you have multiple people working on different tasks of the same story.</span><span class="sxs-lookup"><span data-stu-id="e2de7-117">Organizing the branches in this hierarchical way that corresponds to the story-task relationships is helpful when you have multiple people working on different stories of the same project, or you have multiple people working on different tasks of the same story.</span></span> <span data-ttu-id="e2de7-118">Conflicts can be minimized when each team member works on a different branch and when each member works on different codes or other artifacts when sharing a branch.</span><span class="sxs-lookup"><span data-stu-id="e2de7-118">Conflicts can be minimized when each team member works on a different branch and when each member works on different codes or other artifacts when sharing a branch.</span></span> 

<span data-ttu-id="e2de7-119">The following picture depicts the recommended branching strategy for TDSP.</span><span class="sxs-lookup"><span data-stu-id="e2de7-119">The following picture depicts the recommended branching strategy for TDSP.</span></span> <span data-ttu-id="e2de7-120">You might not need as many branches as are shown here, especially when you only have one or two people working on the same project, or only one person works on all tasks of a story.</span><span class="sxs-lookup"><span data-stu-id="e2de7-120">You might not need as many branches as are shown here, especially when you only have one or two people working on the same project, or only one person works on all tasks of a story.</span></span> <span data-ttu-id="e2de7-121">But separating the development branch from the master branch is always a good practice.</span><span class="sxs-lookup"><span data-stu-id="e2de7-121">But separating the development branch from the master branch is always a good practice.</span></span> <span data-ttu-id="e2de7-122">This can help prevent the release branch from being interrupted by the development activities.</span><span class="sxs-lookup"><span data-stu-id="e2de7-122">This can help prevent the release branch from being interrupted by the development activities.</span></span> <span data-ttu-id="e2de7-123">More complete description of Git branch model can be found in [A Successful Git Branching Model](http://nvie.com/posts/a-successful-git-branching-model/).</span><span class="sxs-lookup"><span data-stu-id="e2de7-123">More complete description of Git branch model can be found in [A Successful Git Branching Model](http://nvie.com/posts/a-successful-git-branching-model/).</span></span>

![3](./media/collaborative-coding-with-git/3-git-branches.png)

<span data-ttu-id="e2de7-125">To switch to the branch that you want to work on, run the following command in a shell command (Windows or Linux).</span><span class="sxs-lookup"><span data-stu-id="e2de7-125">To switch to the branch that you want to work on, run the following command in a shell command (Windows or Linux).</span></span> 

    git checkout <branch name>

<span data-ttu-id="e2de7-126">Changing the *<branch name\>* to **master** switches you back to the **master** branch.</span><span class="sxs-lookup"><span data-stu-id="e2de7-126">Changing the *<branch name\>* to **master** switches you back to the **master** branch.</span></span> <span data-ttu-id="e2de7-127">After you switch to the working branch, you can start working on that work item, developing the code or documentation artifacts needed to complete the item.</span><span class="sxs-lookup"><span data-stu-id="e2de7-127">After you switch to the working branch, you can start working on that work item, developing the code or documentation artifacts needed to complete the item.</span></span> 

<span data-ttu-id="e2de7-128">You can also link a work item to an existing branch.</span><span class="sxs-lookup"><span data-stu-id="e2de7-128">You can also link a work item to an existing branch.</span></span> <span data-ttu-id="e2de7-129">In the **Detail** page of a work item, instead of clicking **Create a new branch**, you click **+ Add link**.</span><span class="sxs-lookup"><span data-stu-id="e2de7-129">In the **Detail** page of a work item, instead of clicking **Create a new branch**, you click **+ Add link**.</span></span> <span data-ttu-id="e2de7-130">Then, select the branch you want to link the work item to.</span><span class="sxs-lookup"><span data-stu-id="e2de7-130">Then, select the branch you want to link the work item to.</span></span> 

![4](./media/collaborative-coding-with-git/4-link-to-an-existing-branch.png)

<span data-ttu-id="e2de7-132">You can also create a new branch in Git Bash commands.</span><span class="sxs-lookup"><span data-stu-id="e2de7-132">You can also create a new branch in Git Bash commands.</span></span> <span data-ttu-id="e2de7-133">If <base branch name\> is missing, the <new branch name\> is based on _master_ branch.</span><span class="sxs-lookup"><span data-stu-id="e2de7-133">If <base branch name\> is missing, the <new branch name\> is based on _master_ branch.</span></span> 
    
    git checkout -b <new branch name> <base branch name>


## <span data-ttu-id="e2de7-134">2. <a name='WorkonaBranchandCommittheChanges-2'></a>Work on a branch and commit the changes</span><span class="sxs-lookup"><span data-stu-id="e2de7-134">2. <a name='WorkonaBranchandCommittheChanges-2'></a>Work on a branch and commit the changes</span></span> 

<span data-ttu-id="e2de7-135">Now suppose you make some change to the *data\_ingestion* branch for the work item, such as adding an R file on the branch in your local machine.</span><span class="sxs-lookup"><span data-stu-id="e2de7-135">Now suppose you make some change to the *data\_ingestion* branch for the work item, such as adding an R file on the branch in your local machine.</span></span> <span data-ttu-id="e2de7-136">You can commit the R file added to the branch for this work item, provided you are in that branch in your Git shell, using the following Git commands:</span><span class="sxs-lookup"><span data-stu-id="e2de7-136">You can commit the R file added to the branch for this work item, provided you are in that branch in your Git shell, using the following Git commands:</span></span>

    git status
    git add .
    git commit -m"added a R scripts"
    git push origin data_ingestion

![5](./media/collaborative-coding-with-git/5-sprint-push-to-branch.png)

## <span data-ttu-id="e2de7-138">3. <a name='CreateapullrequestonVSTS-3'></a>Create a pull request on Azure DevOps Services</span><span class="sxs-lookup"><span data-stu-id="e2de7-138">3. <a name='CreateapullrequestonVSTS-3'></a>Create a pull request on Azure DevOps Services</span></span> 

<span data-ttu-id="e2de7-139">When you are ready after a few commits and pushes, to merge the current branch into its base branch, you can submit a **pull request** on Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="e2de7-139">When you are ready after a few commits and pushes, to merge the current branch into its base branch, you can submit a **pull request** on Azure DevOps Services.</span></span> 

<span data-ttu-id="e2de7-140">Go to the main page of your project and click **CODE**.</span><span class="sxs-lookup"><span data-stu-id="e2de7-140">Go to the main page of your project and click **CODE**.</span></span> <span data-ttu-id="e2de7-141">Select the branch to be merged and the Git repository name that you want to merge the branch into.</span><span class="sxs-lookup"><span data-stu-id="e2de7-141">Select the branch to be merged and the Git repository name that you want to merge the branch into.</span></span> <span data-ttu-id="e2de7-142">Then click **Pull Requests**, click **New pull request** to create a pull request review before the work on the branch is merged to its base branch.</span><span class="sxs-lookup"><span data-stu-id="e2de7-142">Then click **Pull Requests**, click **New pull request** to create a pull request review before the work on the branch is merged to its base branch.</span></span>

![6](./media/collaborative-coding-with-git/6-spring-create-pull-request.png)

<span data-ttu-id="e2de7-144">Fill in some description about this pull request, add reviewers, and send it out.</span><span class="sxs-lookup"><span data-stu-id="e2de7-144">Fill in some description about this pull request, add reviewers, and send it out.</span></span>

![7](./media/collaborative-coding-with-git/7-spring-send-pull-request.png)

## <span data-ttu-id="e2de7-146">4. <a name='ReviewandMerge-4'></a>Review and merge</span><span class="sxs-lookup"><span data-stu-id="e2de7-146">4. <a name='ReviewandMerge-4'></a>Review and merge</span></span> 

<span data-ttu-id="e2de7-147">When the pull request is created, your reviewers get an email notification to review the pull requests.</span><span class="sxs-lookup"><span data-stu-id="e2de7-147">When the pull request is created, your reviewers get an email notification to review the pull requests.</span></span> <span data-ttu-id="e2de7-148">The reviewers need to check whether the changes are working or not and test the changes with the requester if possible.</span><span class="sxs-lookup"><span data-stu-id="e2de7-148">The reviewers need to check whether the changes are working or not and test the changes with the requester if possible.</span></span> <span data-ttu-id="e2de7-149">Based on their assessment, the reviewers can approve or reject the pull request.</span><span class="sxs-lookup"><span data-stu-id="e2de7-149">Based on their assessment, the reviewers can approve or reject the pull request.</span></span> 

![8](./media/collaborative-coding-with-git/8-add_comments.png)

![9](./media/collaborative-coding-with-git/9-spring-approve-pullrequest.png)

<span data-ttu-id="e2de7-152">After the review is done, the working branch is merged to its base branch by clicking the **Complete** button.</span><span class="sxs-lookup"><span data-stu-id="e2de7-152">After the review is done, the working branch is merged to its base branch by clicking the **Complete** button.</span></span> <span data-ttu-id="e2de7-153">You may choose to delete the working branch after it has merged.</span><span class="sxs-lookup"><span data-stu-id="e2de7-153">You may choose to delete the working branch after it has merged.</span></span> 

![10](./media/collaborative-coding-with-git/10-spring-complete-pullrequest.png)

<span data-ttu-id="e2de7-155">Confirm on the top left corner that the request is marked as **COMPLETED**.</span><span class="sxs-lookup"><span data-stu-id="e2de7-155">Confirm on the top left corner that the request is marked as **COMPLETED**.</span></span> 

![11](./media/collaborative-coding-with-git/11-spring-merge-pullrequest.png)

<span data-ttu-id="e2de7-157">When you go back to the repository under **CODE**, you are told that you have been switched to the master branch.</span><span class="sxs-lookup"><span data-stu-id="e2de7-157">When you go back to the repository under **CODE**, you are told that you have been switched to the master branch.</span></span>

![12](./media/collaborative-coding-with-git/12-spring-branch-deleted.png)

<span data-ttu-id="e2de7-159">You can also use the following Git commands to merge your working branch to its base branch and delete the working branch after merging:</span><span class="sxs-lookup"><span data-stu-id="e2de7-159">You can also use the following Git commands to merge your working branch to its base branch and delete the working branch after merging:</span></span>

    git checkout master
    git merge data_ingestion
    git branch -d data_ingestion

![13](./media/collaborative-coding-with-git/13-spring-branch-deleted-commandline.png)


 
## <a name="next-steps"></a><span data-ttu-id="e2de7-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="e2de7-161">Next steps</span></span>

<span data-ttu-id="e2de7-162">[Execute of data science tasks](execute-data-science-tasks.md) shows how to use utilities to complete several common data science tasks such as interactive data exploration, data analysis, reporting, and model creation.</span><span class="sxs-lookup"><span data-stu-id="e2de7-162">[Execute of data science tasks](execute-data-science-tasks.md) shows how to use utilities to complete several common data science tasks such as interactive data exploration, data analysis, reporting, and model creation.</span></span>

<span data-ttu-id="e2de7-163">Walkthroughs that demonstrate all the steps in the process for **specific scenarios** are also provided.</span><span class="sxs-lookup"><span data-stu-id="e2de7-163">Walkthroughs that demonstrate all the steps in the process for **specific scenarios** are also provided.</span></span> <span data-ttu-id="e2de7-164">They are listed and linked with thumbnail descriptions in the [Example walkthroughs](walkthroughs.md) article.</span><span class="sxs-lookup"><span data-stu-id="e2de7-164">They are listed and linked with thumbnail descriptions in the [Example walkthroughs](walkthroughs.md) article.</span></span> <span data-ttu-id="e2de7-165">They illustrate how to combine cloud, on-premises tools, and services into a workflow or pipeline to create an intelligent application.</span><span class="sxs-lookup"><span data-stu-id="e2de7-165">They illustrate how to combine cloud, on-premises tools, and services into a workflow or pipeline to create an intelligent application.</span></span> 

