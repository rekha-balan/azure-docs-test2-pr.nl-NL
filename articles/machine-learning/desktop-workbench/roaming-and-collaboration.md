---
title: Roaming and collaboration in Azure Machine Learning Workbench | Microsoft Docs
description: Learn how to set up roaming and collaboration in Machine Learning Workbench.
services: machine-learning
author: hning86
ms.author: haining
manager: mwinkle
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: article
ms.date: 11/16/2017
ms.openlocfilehash: 0abc5e34d2bfa1cf2a9fc0569831e21ed295891c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867278"
---
# <a name="roaming-and-collaboration-in-azure-machine-learning-workbench"></a><span data-ttu-id="aa11d-103">Roaming and collaboration in Azure Machine Learning Workbench</span><span class="sxs-lookup"><span data-stu-id="aa11d-103">Roaming and collaboration in Azure Machine Learning Workbench</span></span>
<span data-ttu-id="aa11d-104">This article describes how you can use Azure Machine Learning Workbench to set up projects for roaming between computers and collaborate with team members.</span><span class="sxs-lookup"><span data-stu-id="aa11d-104">This article describes how you can use Azure Machine Learning Workbench to set up projects for roaming between computers and collaborate with team members.</span></span> 

<span data-ttu-id="aa11d-105">When you create an Azure Machine Learning project that has a remote Git repository (repo) link, the project metadata and snapshots are stored in the cloud.</span><span class="sxs-lookup"><span data-stu-id="aa11d-105">When you create an Azure Machine Learning project that has a remote Git repository (repo) link, the project metadata and snapshots are stored in the cloud.</span></span> <span data-ttu-id="aa11d-106">You can use the cloud link to access the project from a different computer (roaming).</span><span class="sxs-lookup"><span data-stu-id="aa11d-106">You can use the cloud link to access the project from a different computer (roaming).</span></span> <span data-ttu-id="aa11d-107">You can also collaborate with team members by giving them access to the project.</span><span class="sxs-lookup"><span data-stu-id="aa11d-107">You can also collaborate with team members by giving them access to the project.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="aa11d-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="aa11d-108">Prerequisites</span></span>
1. <span data-ttu-id="aa11d-109">Install the Machine Learning Workbench app.</span><span class="sxs-lookup"><span data-stu-id="aa11d-109">Install the Machine Learning Workbench app.</span></span> <span data-ttu-id="aa11d-110">Ensure that you have access to an Azure Machine Learning Experimentation account.</span><span class="sxs-lookup"><span data-stu-id="aa11d-110">Ensure that you have access to an Azure Machine Learning Experimentation account.</span></span> <span data-ttu-id="aa11d-111">For more information, see the [installation guide](../service/quickstart-installation.md).</span><span class="sxs-lookup"><span data-stu-id="aa11d-111">For more information, see the [installation guide](../service/quickstart-installation.md).</span></span>

2. <span data-ttu-id="aa11d-112">Access [Azure DevOps](https://www.visualstudio.com) and then create a repo to link your project to.</span><span class="sxs-lookup"><span data-stu-id="aa11d-112">Access [Azure DevOps](https://www.visualstudio.com) and then create a repo to link your project to.</span></span> <span data-ttu-id="aa11d-113">For more information, see [Using a Git repo with a Machine Learning Workbench project](using-git-ml-project.md).</span><span class="sxs-lookup"><span data-stu-id="aa11d-113">For more information, see [Using a Git repo with a Machine Learning Workbench project](using-git-ml-project.md).</span></span>

## <a name="create-a-new-machine-learning-project"></a><span data-ttu-id="aa11d-114">Create a new Machine Learning project</span><span class="sxs-lookup"><span data-stu-id="aa11d-114">Create a new Machine Learning project</span></span>
<span data-ttu-id="aa11d-115">Open Machine Learning Workbench, and then create a new project (for example, a project named iris).</span><span class="sxs-lookup"><span data-stu-id="aa11d-115">Open Machine Learning Workbench, and then create a new project (for example, a project named iris).</span></span> <span data-ttu-id="aa11d-116">In the **Visualstudio.com GIT Repository URL** box, enter a valid URL for an Azure DevOps Git repo.</span><span class="sxs-lookup"><span data-stu-id="aa11d-116">In the **Visualstudio.com GIT Repository URL** box, enter a valid URL for an Azure DevOps Git repo.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="aa11d-117">If you choose the blank project template, the Git repo you choose to use might already have a master branch.</span><span class="sxs-lookup"><span data-stu-id="aa11d-117">If you choose the blank project template, the Git repo you choose to use might already have a master branch.</span></span> <span data-ttu-id="aa11d-118">Machine Learning simply clones the master branch locally.</span><span class="sxs-lookup"><span data-stu-id="aa11d-118">Machine Learning simply clones the master branch locally.</span></span> <span data-ttu-id="aa11d-119">It adds the aml_config folder and other project metadata files to the local project folder.</span><span class="sxs-lookup"><span data-stu-id="aa11d-119">It adds the aml_config folder and other project metadata files to the local project folder.</span></span> 
>
> <span data-ttu-id="aa11d-120">If you choose any other project template, your Git repo *cannot* already have a master branch.</span><span class="sxs-lookup"><span data-stu-id="aa11d-120">If you choose any other project template, your Git repo *cannot* already have a master branch.</span></span> <span data-ttu-id="aa11d-121">If it does, you see an error.</span><span class="sxs-lookup"><span data-stu-id="aa11d-121">If it does, you see an error.</span></span> <span data-ttu-id="aa11d-122">The alternative is to use the `az ml project create` command to create the project, with a `--force` switch.</span><span class="sxs-lookup"><span data-stu-id="aa11d-122">The alternative is to use the `az ml project create` command to create the project, with a `--force` switch.</span></span> <span data-ttu-id="aa11d-123">This deletes the files in the original master branch and replaces them with the new files in the template that you choose.</span><span class="sxs-lookup"><span data-stu-id="aa11d-123">This deletes the files in the original master branch and replaces them with the new files in the template that you choose.</span></span>

<span data-ttu-id="aa11d-124">After the project is created, submit a few runs on any scripts that are in the project.</span><span class="sxs-lookup"><span data-stu-id="aa11d-124">After the project is created, submit a few runs on any scripts that are in the project.</span></span> <span data-ttu-id="aa11d-125">This action commits the project state to the remote Git repo's run history branch.</span><span class="sxs-lookup"><span data-stu-id="aa11d-125">This action commits the project state to the remote Git repo's run history branch.</span></span> 

> [!NOTE] 
> <span data-ttu-id="aa11d-126">Only script runs trigger commits to the run history branch.</span><span class="sxs-lookup"><span data-stu-id="aa11d-126">Only script runs trigger commits to the run history branch.</span></span> <span data-ttu-id="aa11d-127">Data prep execution and Notebook runs don't trigger project snapshots in the run history branch.</span><span class="sxs-lookup"><span data-stu-id="aa11d-127">Data prep execution and Notebook runs don't trigger project snapshots in the run history branch.</span></span>

<span data-ttu-id="aa11d-128">If you have set up Git authentication, you can also operate in the master branch.</span><span class="sxs-lookup"><span data-stu-id="aa11d-128">If you have set up Git authentication, you can also operate in the master branch.</span></span> <span data-ttu-id="aa11d-129">Or, you can create a new branch.</span><span class="sxs-lookup"><span data-stu-id="aa11d-129">Or, you can create a new branch.</span></span> 

<span data-ttu-id="aa11d-130">Example:</span><span class="sxs-lookup"><span data-stu-id="aa11d-130">Example:</span></span> 
```
# Check current repo status.
$ git status

# Stage all changes in the current repo.
$ git add -A

# Commit changes.
$ git commit -m "my commit fixes this weird bug!"

# Push to the remote repo.
$ git push origin master
```

## <a name="roaming"></a><span data-ttu-id="aa11d-131">Roaming</span><span class="sxs-lookup"><span data-stu-id="aa11d-131">Roaming</span></span>
<a name="roaming"></a>

### <a name="open-machine-learning-workbench-on-a-second-computer"></a><span data-ttu-id="aa11d-132">Open Machine Learning Workbench on a second computer</span><span class="sxs-lookup"><span data-stu-id="aa11d-132">Open Machine Learning Workbench on a second computer</span></span>
<span data-ttu-id="aa11d-133">After the Azure DevOps Git repo is linked with your project, you can access the iris project from any computer that has Machine Learning Workbench installed.</span><span class="sxs-lookup"><span data-stu-id="aa11d-133">After the Azure DevOps Git repo is linked with your project, you can access the iris project from any computer that has Machine Learning Workbench installed.</span></span> 

<span data-ttu-id="aa11d-134">To access the iris project on another computer, you must sign in to the app by using the same credentials that you used to create the project.</span><span class="sxs-lookup"><span data-stu-id="aa11d-134">To access the iris project on another computer, you must sign in to the app by using the same credentials that you used to create the project.</span></span> <span data-ttu-id="aa11d-135">You also need to be in the same Machine Learning Experimentation account and workspace.</span><span class="sxs-lookup"><span data-stu-id="aa11d-135">You also need to be in the same Machine Learning Experimentation account and workspace.</span></span> <span data-ttu-id="aa11d-136">The iris project is alphabetically listed with other projects in the workspace.</span><span class="sxs-lookup"><span data-stu-id="aa11d-136">The iris project is alphabetically listed with other projects in the workspace.</span></span> 

### <a name="download-the-project-on-a-second-computer"></a><span data-ttu-id="aa11d-137">Download the project on a second computer</span><span class="sxs-lookup"><span data-stu-id="aa11d-137">Download the project on a second computer</span></span>
<span data-ttu-id="aa11d-138">When the workspace is open on the second computer, the icon adjacent to the iris project is different from the typical folder icon.</span><span class="sxs-lookup"><span data-stu-id="aa11d-138">When the workspace is open on the second computer, the icon adjacent to the iris project is different from the typical folder icon.</span></span> <span data-ttu-id="aa11d-139">The download icon indicates that the contents of the project are in the cloud, and that the project is ready to be downloaded to the current computer.</span><span class="sxs-lookup"><span data-stu-id="aa11d-139">The download icon indicates that the contents of the project are in the cloud, and that the project is ready to be downloaded to the current computer.</span></span> 

![Create project](./media/roaming-and-collaboration/downloadable-project.png)

<span data-ttu-id="aa11d-141">Select the iris project to begin a download.</span><span class="sxs-lookup"><span data-stu-id="aa11d-141">Select the iris project to begin a download.</span></span> <span data-ttu-id="aa11d-142">When the download is finished, the project is ready to be accessed on the second computer.</span><span class="sxs-lookup"><span data-stu-id="aa11d-142">When the download is finished, the project is ready to be accessed on the second computer.</span></span> 

<span data-ttu-id="aa11d-143">On Windows, the project is located at C:\Users\\<username\>\Documents\AzureML.</span><span class="sxs-lookup"><span data-stu-id="aa11d-143">On Windows, the project is located at C:\Users\\<username\>\Documents\AzureML.</span></span>

<span data-ttu-id="aa11d-144">On macOS, the project is located at /home/\<username\>/Documents/AzureML.</span><span class="sxs-lookup"><span data-stu-id="aa11d-144">On macOS, the project is located at /home/\<username\>/Documents/AzureML.</span></span>

<span data-ttu-id="aa11d-145">In a future release, we plan to enhance functionality so that you can select a destination folder.</span><span class="sxs-lookup"><span data-stu-id="aa11d-145">In a future release, we plan to enhance functionality so that you can select a destination folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="aa11d-146">If you have a folder in the Machine Learning directory that has the exact same name as the project, the download fails.</span><span class="sxs-lookup"><span data-stu-id="aa11d-146">If you have a folder in the Machine Learning directory that has the exact same name as the project, the download fails.</span></span> <span data-ttu-id="aa11d-147">To work around this issue, temporarily rename the existing folder.</span><span class="sxs-lookup"><span data-stu-id="aa11d-147">To work around this issue, temporarily rename the existing folder.</span></span>


### <a name="work-on-the-downloaded-project"></a><span data-ttu-id="aa11d-148">Work on the downloaded project</span><span class="sxs-lookup"><span data-stu-id="aa11d-148">Work on the downloaded project</span></span> 
<span data-ttu-id="aa11d-149">The newly downloaded project reflects the project state at the last run in the project.</span><span class="sxs-lookup"><span data-stu-id="aa11d-149">The newly downloaded project reflects the project state at the last run in the project.</span></span> <span data-ttu-id="aa11d-150">A snapshot of the project state is automatically committed to the run history branch in the Azure DevOps Git repo every time you submit a run.</span><span class="sxs-lookup"><span data-stu-id="aa11d-150">A snapshot of the project state is automatically committed to the run history branch in the Azure DevOps Git repo every time you submit a run.</span></span> <span data-ttu-id="aa11d-151">The snapshot that is associated with the latest run is used to instantiate the project on the second computer.</span><span class="sxs-lookup"><span data-stu-id="aa11d-151">The snapshot that is associated with the latest run is used to instantiate the project on the second computer.</span></span> 
 

## <a name="collaboration"></a><span data-ttu-id="aa11d-152">Collaboration</span><span class="sxs-lookup"><span data-stu-id="aa11d-152">Collaboration</span></span>
<span data-ttu-id="aa11d-153">You can collaborate with team members on projects that are linked to an Azure DevOps Git repo.</span><span class="sxs-lookup"><span data-stu-id="aa11d-153">You can collaborate with team members on projects that are linked to an Azure DevOps Git repo.</span></span> <span data-ttu-id="aa11d-154">You can assign permissions to users for the Machine Learning Experimentation account, workspace, and project.</span><span class="sxs-lookup"><span data-stu-id="aa11d-154">You can assign permissions to users for the Machine Learning Experimentation account, workspace, and project.</span></span> <span data-ttu-id="aa11d-155">Currently, you can perform Azure Resource Manager commands by using Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="aa11d-155">Currently, you can perform Azure Resource Manager commands by using Azure CLI.</span></span> <span data-ttu-id="aa11d-156">You can also use the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aa11d-156">You can also use the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="aa11d-157">For more information, see [Use the Azure portal to add users](#portal).</span><span class="sxs-lookup"><span data-stu-id="aa11d-157">For more information, see [Use the Azure portal to add users](#portal).</span></span>    

### <a name="use-the-command-line-to-add-users"></a><span data-ttu-id="aa11d-158">Use the command line to add users</span><span class="sxs-lookup"><span data-stu-id="aa11d-158">Use the command line to add users</span></span>
<span data-ttu-id="aa11d-159">As an example, Alice is the Owner of the iris project.</span><span class="sxs-lookup"><span data-stu-id="aa11d-159">As an example, Alice is the Owner of the iris project.</span></span> <span data-ttu-id="aa11d-160">Alice wants to share access to the project with Bob.</span><span class="sxs-lookup"><span data-stu-id="aa11d-160">Alice wants to share access to the project with Bob.</span></span> 

<span data-ttu-id="aa11d-161">Alice selects the **File** menu, and then selects the **Command Prompt** menu item.</span><span class="sxs-lookup"><span data-stu-id="aa11d-161">Alice selects the **File** menu, and then selects the **Command Prompt** menu item.</span></span> <span data-ttu-id="aa11d-162">The Command Prompt window opens with the iris project.</span><span class="sxs-lookup"><span data-stu-id="aa11d-162">The Command Prompt window opens with the iris project.</span></span> <span data-ttu-id="aa11d-163">Alice can then decide what level of access she wants to give to Bob.</span><span class="sxs-lookup"><span data-stu-id="aa11d-163">Alice can then decide what level of access she wants to give to Bob.</span></span> <span data-ttu-id="aa11d-164">She grants permissions by executing the following commands:</span><span class="sxs-lookup"><span data-stu-id="aa11d-164">She grants permissions by executing the following commands:</span></span>  

```azurecli
# Find the Resource Manager ID of the Experimentation account.
az ml account experimentation show --query "id"

# Add Bob to the Experimentation account as a Contributor.
# Bob now has read/write access to all workspaces and projects under the account by inheritance.
az role assignment create --assignee bob@contoso.com --role Contributor --scope <Experimentation account Resource Manager ID>

# Find the Resource Manager ID of the workspace.
az ml workspace show --query "id"

# Add Bob to the workspace as an Owner.
# Bob now has read/write access to all projects under the workspace by inheritance. Bob can invite or remove other users.
az role assignment create --assignee bob@contoso.com --role Owner --scope <workspace Resource Manager ID>
```

<span data-ttu-id="aa11d-165">After role assignment, either directly or by inheritance, Bob can see the project in the Machine Learning Workbench project list.</span><span class="sxs-lookup"><span data-stu-id="aa11d-165">After role assignment, either directly or by inheritance, Bob can see the project in the Machine Learning Workbench project list.</span></span> <span data-ttu-id="aa11d-166">Bob might need to restart the application to see the project.</span><span class="sxs-lookup"><span data-stu-id="aa11d-166">Bob might need to restart the application to see the project.</span></span> <span data-ttu-id="aa11d-167">Bob can then download the project as described in [Roaming](#roaming), and begin to collaborate with Alice.</span><span class="sxs-lookup"><span data-stu-id="aa11d-167">Bob can then download the project as described in [Roaming](#roaming), and begin to collaborate with Alice.</span></span> 

<span data-ttu-id="aa11d-168">The run history for all users that collaborate on a project is committed to the same remote Git repo.</span><span class="sxs-lookup"><span data-stu-id="aa11d-168">The run history for all users that collaborate on a project is committed to the same remote Git repo.</span></span> <span data-ttu-id="aa11d-169">When Alice executes a run, Bob can see the run in the run history section of the project in the Machine Learning Workbench app.</span><span class="sxs-lookup"><span data-stu-id="aa11d-169">When Alice executes a run, Bob can see the run in the run history section of the project in the Machine Learning Workbench app.</span></span> <span data-ttu-id="aa11d-170">Bob can also restore the project to the state of any run, including runs that Alice started.</span><span class="sxs-lookup"><span data-stu-id="aa11d-170">Bob can also restore the project to the state of any run, including runs that Alice started.</span></span> 

<span data-ttu-id="aa11d-171">By sharing a remote Git repo for the project, Alice and Bob can also collaborate in the master branch.</span><span class="sxs-lookup"><span data-stu-id="aa11d-171">By sharing a remote Git repo for the project, Alice and Bob can also collaborate in the master branch.</span></span> <span data-ttu-id="aa11d-172">If needed, they can also create personal branches and use Git pull requests and merges to collaborate.</span><span class="sxs-lookup"><span data-stu-id="aa11d-172">If needed, they can also create personal branches and use Git pull requests and merges to collaborate.</span></span> 

### <a name="use-the-azure-portal-to-add-users"></a><span data-ttu-id="aa11d-173">Use the Azure portal to add users</span><span class="sxs-lookup"><span data-stu-id="aa11d-173">Use the Azure portal to add users</span></span>
<a name="portal"></a>

<span data-ttu-id="aa11d-174">Machine Learning Experimentation accounts, workspaces, and projects are Azure Resource Manager resources.</span><span class="sxs-lookup"><span data-stu-id="aa11d-174">Machine Learning Experimentation accounts, workspaces, and projects are Azure Resource Manager resources.</span></span> <span data-ttu-id="aa11d-175">To assign roles, you can use the **Access Control** link in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aa11d-175">To assign roles, you can use the **Access Control** link in the [Azure portal](https://portal.azure.com).</span></span> 

<span data-ttu-id="aa11d-176">Find the resource that you want to add users to by using the **All Resources** view.</span><span class="sxs-lookup"><span data-stu-id="aa11d-176">Find the resource that you want to add users to by using the **All Resources** view.</span></span> <span data-ttu-id="aa11d-177">Select the **Access control (IAM)** link, and then select **Add users**.</span><span class="sxs-lookup"><span data-stu-id="aa11d-177">Select the **Access control (IAM)** link, and then select **Add users**.</span></span> 

<img src="./media/roaming-and-collaboration/iam.png" width="320px">

## <a name="sample-collaboration-workflow"></a><span data-ttu-id="aa11d-178">Sample collaboration workflow</span><span class="sxs-lookup"><span data-stu-id="aa11d-178">Sample collaboration workflow</span></span>
<span data-ttu-id="aa11d-179">To illustrate the collaboration workflow, let's walk through an example.</span><span class="sxs-lookup"><span data-stu-id="aa11d-179">To illustrate the collaboration workflow, let's walk through an example.</span></span> <span data-ttu-id="aa11d-180">Contoso employees Alice and Bob want to collaborate on a data science project by using Machine Learning Workbench.</span><span class="sxs-lookup"><span data-stu-id="aa11d-180">Contoso employees Alice and Bob want to collaborate on a data science project by using Machine Learning Workbench.</span></span> <span data-ttu-id="aa11d-181">Their identities belong to the same Contoso Azure Active Directory (Azure AD) tenant.</span><span class="sxs-lookup"><span data-stu-id="aa11d-181">Their identities belong to the same Contoso Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="aa11d-182">Here are the steps Alice and Bob take:</span><span class="sxs-lookup"><span data-stu-id="aa11d-182">Here are the steps Alice and Bob take:</span></span>

1. <span data-ttu-id="aa11d-183">Alice creates an empty Git repo in an Azure DevOps project.</span><span class="sxs-lookup"><span data-stu-id="aa11d-183">Alice creates an empty Git repo in an Azure DevOps project.</span></span> <span data-ttu-id="aa11d-184">The Azure DevOps project should be in an Azure subscription that is created under the Contoso Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="aa11d-184">The Azure DevOps project should be in an Azure subscription that is created under the Contoso Azure AD tenant.</span></span> 

2. <span data-ttu-id="aa11d-185">Alice creates a Machine Learning Experimentation account, a workspace, and a Machine Learning Workbench project on her computer.</span><span class="sxs-lookup"><span data-stu-id="aa11d-185">Alice creates a Machine Learning Experimentation account, a workspace, and a Machine Learning Workbench project on her computer.</span></span> <span data-ttu-id="aa11d-186">When she creates the project, she enters the Azure DevOps Git repo URL.</span><span class="sxs-lookup"><span data-stu-id="aa11d-186">When she creates the project, she enters the Azure DevOps Git repo URL.</span></span>

3. <span data-ttu-id="aa11d-187">Alice starts to work on the project.</span><span class="sxs-lookup"><span data-stu-id="aa11d-187">Alice starts to work on the project.</span></span> <span data-ttu-id="aa11d-188">She creates some scripts and executes a few runs.</span><span class="sxs-lookup"><span data-stu-id="aa11d-188">She creates some scripts and executes a few runs.</span></span> <span data-ttu-id="aa11d-189">For each run, a snapshot of the entire project folder is automatically pushed as a commit to a run history branch of the Azure DevOps Git repo that Machine Learning Workbench creates.</span><span class="sxs-lookup"><span data-stu-id="aa11d-189">For each run, a snapshot of the entire project folder is automatically pushed as a commit to a run history branch of the Azure DevOps Git repo that Machine Learning Workbench creates.</span></span>

4. <span data-ttu-id="aa11d-190">Alice is happy with the work in progress.</span><span class="sxs-lookup"><span data-stu-id="aa11d-190">Alice is happy with the work in progress.</span></span> <span data-ttu-id="aa11d-191">She wants to commit her changes in the local master branch and then push them to Azure DevOps Git repo master branch.</span><span class="sxs-lookup"><span data-stu-id="aa11d-191">She wants to commit her changes in the local master branch and then push them to Azure DevOps Git repo master branch.</span></span> <span data-ttu-id="aa11d-192">With the project open, in Machine Learning Workbench, she opens the Command Prompt window, and then enters these commands:</span><span class="sxs-lookup"><span data-stu-id="aa11d-192">With the project open, in Machine Learning Workbench, she opens the Command Prompt window, and then enters these commands:</span></span>
    
    ```sh
    # Verify that the Git remote is pointing to the Azure DevOps Git repo.
    $ git remote -v

    # Verify that the current branch is master.
    $ git branch

    # Stage all changes.
    $ git add -A

    # Commit changes with a comment.
    $ git commit -m "this is a good milestone"

    # Push the commit to the master branch of the remote Git repo in Azure DevOps.
    $ git push
    ```

5. <span data-ttu-id="aa11d-193">Alice adds Bob to the workspace as a Contributor.</span><span class="sxs-lookup"><span data-stu-id="aa11d-193">Alice adds Bob to the workspace as a Contributor.</span></span> <span data-ttu-id="aa11d-194">She can do this in the Azure portal, or by using the `az role assignment` command, as demonstrated earlier.</span><span class="sxs-lookup"><span data-stu-id="aa11d-194">She can do this in the Azure portal, or by using the `az role assignment` command, as demonstrated earlier.</span></span> <span data-ttu-id="aa11d-195">Alice also grants Bob read/write permissions to the Azure DevOps Git repo.</span><span class="sxs-lookup"><span data-stu-id="aa11d-195">Alice also grants Bob read/write permissions to the Azure DevOps Git repo.</span></span>

6. <span data-ttu-id="aa11d-196">Bob signs in to Machine Learning Workbench on his computer.</span><span class="sxs-lookup"><span data-stu-id="aa11d-196">Bob signs in to Machine Learning Workbench on his computer.</span></span> <span data-ttu-id="aa11d-197">He can see the workspace that Alice shared with him.</span><span class="sxs-lookup"><span data-stu-id="aa11d-197">He can see the workspace that Alice shared with him.</span></span> <span data-ttu-id="aa11d-198">He can see the iris project listed under that workspace.</span><span class="sxs-lookup"><span data-stu-id="aa11d-198">He can see the iris project listed under that workspace.</span></span> 

7. <span data-ttu-id="aa11d-199">Bob selects the project name.</span><span class="sxs-lookup"><span data-stu-id="aa11d-199">Bob selects the project name.</span></span> <span data-ttu-id="aa11d-200">The project is downloaded to his computer.</span><span class="sxs-lookup"><span data-stu-id="aa11d-200">The project is downloaded to his computer.</span></span>
    * <span data-ttu-id="aa11d-201">The downloaded project files are a copy of the snapshot of the latest run that's recorded in the run history.</span><span class="sxs-lookup"><span data-stu-id="aa11d-201">The downloaded project files are a copy of the snapshot of the latest run that's recorded in the run history.</span></span> <span data-ttu-id="aa11d-202">They are not the last commit on the master branch.</span><span class="sxs-lookup"><span data-stu-id="aa11d-202">They are not the last commit on the master branch.</span></span>
    * <span data-ttu-id="aa11d-203">The local project folder is set to the master branch, with the unstaged changes.</span><span class="sxs-lookup"><span data-stu-id="aa11d-203">The local project folder is set to the master branch, with the unstaged changes.</span></span>

8. <span data-ttu-id="aa11d-204">Bob can browse runs that were executed by Alice.</span><span class="sxs-lookup"><span data-stu-id="aa11d-204">Bob can browse runs that were executed by Alice.</span></span> <span data-ttu-id="aa11d-205">He can restore snapshots of any earlier runs.</span><span class="sxs-lookup"><span data-stu-id="aa11d-205">He can restore snapshots of any earlier runs.</span></span>

9. <span data-ttu-id="aa11d-206">Bob wants to get the latest changes that Alice pushed, and then start working in a different branch.</span><span class="sxs-lookup"><span data-stu-id="aa11d-206">Bob wants to get the latest changes that Alice pushed, and then start working in a different branch.</span></span> <span data-ttu-id="aa11d-207">In Machine Learning Workbench, Bob opens a Command Prompt window and executes the following commands:</span><span class="sxs-lookup"><span data-stu-id="aa11d-207">In Machine Learning Workbench, Bob opens a Command Prompt window and executes the following commands:</span></span>

    ```sh
    # Verify that the Git remote is pointing to the Azure DevOps Git repo.
    $ git remote -v

    # Verify that the current branch is master.
    $ git branch

    # Get the latest commit in the Azure DevOps Git master branch and overwrite current files.
    $ git pull --force

    # Create a new local branch named "bob" so that Bob's work is done in the "bob" branch
    $ git checkout -b bob
    ```

10. <span data-ttu-id="aa11d-208">Bob modifies the project and submits new runs.</span><span class="sxs-lookup"><span data-stu-id="aa11d-208">Bob modifies the project and submits new runs.</span></span> <span data-ttu-id="aa11d-209">The changes are made on the bob branch.</span><span class="sxs-lookup"><span data-stu-id="aa11d-209">The changes are made on the bob branch.</span></span> <span data-ttu-id="aa11d-210">Bob's runs also become visible to Alice.</span><span class="sxs-lookup"><span data-stu-id="aa11d-210">Bob's runs also become visible to Alice.</span></span>

11. <span data-ttu-id="aa11d-211">Bob is ready to push his changes to the remote Git repo.</span><span class="sxs-lookup"><span data-stu-id="aa11d-211">Bob is ready to push his changes to the remote Git repo.</span></span> <span data-ttu-id="aa11d-212">To avoid conflict with the master branch, where Alice is working, Bob pushes his work to a new remote branch, which is also named bob.</span><span class="sxs-lookup"><span data-stu-id="aa11d-212">To avoid conflict with the master branch, where Alice is working, Bob pushes his work to a new remote branch, which is also named bob.</span></span>

    ```sh
    # Verify that the current branch is "bob," and that it has unstaged changes.
    $ git status
    
    # Stage all changes.
    $ git add -A

    # Commit the changes with a comment.
    $ git commit -m "I found a cool new trick."

    # Create a new branch on the remote Azure DevOps Git repo, and then push the changes.
    $ git push origin bob
    ```

12. <span data-ttu-id="aa11d-213">To tell Alice about the cool new trick in his code, Bob creates a pull request on the remote Git repo from the bob branch to the master branch.</span><span class="sxs-lookup"><span data-stu-id="aa11d-213">To tell Alice about the cool new trick in his code, Bob creates a pull request on the remote Git repo from the bob branch to the master branch.</span></span> <span data-ttu-id="aa11d-214">Alice can then merge the pull request into the master branch.</span><span class="sxs-lookup"><span data-stu-id="aa11d-214">Alice can then merge the pull request into the master branch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa11d-215">Next steps</span><span class="sxs-lookup"><span data-stu-id="aa11d-215">Next steps</span></span>
- <span data-ttu-id="aa11d-216">Learn more about [using a Git repo with a Machine Learning Workbench project](using-git-ml-project.md).</span><span class="sxs-lookup"><span data-stu-id="aa11d-216">Learn more about [using a Git repo with a Machine Learning Workbench project](using-git-ml-project.md).</span></span>
