---
title: Add a Git artifact repository to a lab in Azure DevTest Labs | Microsoft Docs
description: Add a GitHub or Visual Studio Team Services Git repository for your custom artifacts source in Azure DevTest Labs
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: ''
ms.assetid: 01b459f7-eaf2-45a8-b4b5-2c0a821b33c8
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 6f4ace7f71f8c86276a94868cf690300547d1831
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563745"
---
# <a name="add-a-git-artifact-repository-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="2e8c0-103">Add a Git artifact repository to a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="2e8c0-103">Add a Git artifact repository to a lab in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-add-your-private-Artifacts-Repository-in-a-DevTest-Lab/player]
> 
> 

<span data-ttu-id="2e8c0-104">In Azure DevTest Labs, artifacts are *actions* - such as installing software or running scripts and commands - when a VM is created.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-104">In Azure DevTest Labs, artifacts are *actions* - such as installing software or running scripts and commands - when a VM is created.</span></span> <span data-ttu-id="2e8c0-105">By default, a lab includes artifacts from the official Azure DevTest Labs artifact repository.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-105">By default, a lab includes artifacts from the official Azure DevTest Labs artifact repository.</span></span> <span data-ttu-id="2e8c0-106">You can add a Git artifact repository to your lab to include the artifacts that your team creates.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-106">You can add a Git artifact repository to your lab to include the artifacts that your team creates.</span></span> <span data-ttu-id="2e8c0-107">The repository can be hosted on [GitHub](https://github.com) or on [Visual Studio Team Services (VSTS)](https://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="2e8c0-107">The repository can be hosted on [GitHub](https://github.com) or on [Visual Studio Team Services (VSTS)](https://visualstudio.com).</span></span>

* <span data-ttu-id="2e8c0-108">To learn how to create a GitHub repository, see [GitHub Bootcamp](https://help.github.com/categories/bootcamp/).</span><span class="sxs-lookup"><span data-stu-id="2e8c0-108">To learn how to create a GitHub repository, see [GitHub Bootcamp](https://help.github.com/categories/bootcamp/).</span></span>
* <span data-ttu-id="2e8c0-109">To learn how to create a Team Services project with a Git Repository, see [Connect to Visual Studio Team Services](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online).</span><span class="sxs-lookup"><span data-stu-id="2e8c0-109">To learn how to create a Team Services project with a Git Repository, see [Connect to Visual Studio Team Services](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online).</span></span>

<span data-ttu-id="2e8c0-110">The following screen shot shows an example of how a repository containing artifacts might look in GitHub:</span><span class="sxs-lookup"><span data-stu-id="2e8c0-110">The following screen shot shows an example of how a repository containing artifacts might look in GitHub:</span></span>  
![Sample GitHub artifacts repo](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-add-artifact-repo/devtestlab-github-artifact-repo-home.png)

## <a name="get-the-repository-information-and-credentials"></a><span data-ttu-id="2e8c0-112">Get the repository information and credentials</span><span class="sxs-lookup"><span data-stu-id="2e8c0-112">Get the repository information and credentials</span></span>
<span data-ttu-id="2e8c0-113">To add an artifact repository to your lab, you must first get certain information from your repository.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-113">To add an artifact repository to your lab, you must first get certain information from your repository.</span></span> <span data-ttu-id="2e8c0-114">The following sections guide you through getting this information for artifact repositories hosted on GitHub and Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-114">The following sections guide you through getting this information for artifact repositories hosted on GitHub and Visual Studio Team Services.</span></span>

### <a name="get-the-github-repository-clone-url-and-personal-access-token"></a><span data-ttu-id="2e8c0-115">Get the GitHub repository clone URL and personal access token</span><span class="sxs-lookup"><span data-stu-id="2e8c0-115">Get the GitHub repository clone URL and personal access token</span></span>
<span data-ttu-id="2e8c0-116">To get the GitHub repository clone URL and personal access token, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="2e8c0-116">To get the GitHub repository clone URL and personal access token, follow these steps:</span></span>

1. <span data-ttu-id="2e8c0-117">Browse to the home page of the GitHub repository that contains the artifact definitions.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-117">Browse to the home page of the GitHub repository that contains the artifact definitions.</span></span>
2. <span data-ttu-id="2e8c0-118">Select **Clone or download**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-118">Select **Clone or download**.</span></span>
3. <span data-ttu-id="2e8c0-119">Select the button to copy the **HTTPS clone url** to the clipboard, and save the URL for later use.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-119">Select the button to copy the **HTTPS clone url** to the clipboard, and save the URL for later use.</span></span>
4. <span data-ttu-id="2e8c0-120">Select the profile image in the upper-right corner of GitHub, and select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-120">Select the profile image in the upper-right corner of GitHub, and select **Settings**.</span></span>
5. <span data-ttu-id="2e8c0-121">In the **Personal settings** menu on the left, select **Personal access tokens**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-121">In the **Personal settings** menu on the left, select **Personal access tokens**.</span></span>
6. <span data-ttu-id="2e8c0-122">Select **Generate new token**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-122">Select **Generate new token**.</span></span>
7. <span data-ttu-id="2e8c0-123">On the **New personal access token** page, enter a **Token description**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-123">On the **New personal access token** page, enter a **Token description**.</span></span> <span data-ttu-id="2e8c0-124">If it's a public repo, accept the default items in the **Select scopes**; otherwise, select **repo** scope.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-124">If it's a public repo, accept the default items in the **Select scopes**; otherwise, select **repo** scope.</span></span> <span data-ttu-id="2e8c0-125">Then choose **Generate Token**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-125">Then choose **Generate Token**.</span></span> <span data-ttu-id="2e8c0-126">[Read more about OAuth scopes in GitHub](https://developer.github.com/v3/oauth/#scopes).</span><span class="sxs-lookup"><span data-stu-id="2e8c0-126">[Read more about OAuth scopes in GitHub](https://developer.github.com/v3/oauth/#scopes).</span></span>
8. <span data-ttu-id="2e8c0-127">Save the generated token as you need it later.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-127">Save the generated token as you need it later.</span></span>
9. <span data-ttu-id="2e8c0-128">You can close GitHub now.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-128">You can close GitHub now.</span></span>   
10. <span data-ttu-id="2e8c0-129">Continue to the [Connect your lab to the artifact repository](#connect-your-lab-to-the-artifact-repository) section.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-129">Continue to the [Connect your lab to the artifact repository](#connect-your-lab-to-the-artifact-repository) section.</span></span>

### <a name="get-the-visual-studio-team-services-repository-clone-url-and-personal-access-token"></a><span data-ttu-id="2e8c0-130">Get the Visual Studio Team Services repository clone URL and personal access token</span><span class="sxs-lookup"><span data-stu-id="2e8c0-130">Get the Visual Studio Team Services repository clone URL and personal access token</span></span>
<span data-ttu-id="2e8c0-131">To get the Visual Studio Team Services repository clone URL and personal access token, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="2e8c0-131">To get the Visual Studio Team Services repository clone URL and personal access token, follow these steps:</span></span>

1. <span data-ttu-id="2e8c0-132">Open the home page of your team collection (for example, `https://contoso-web-team.visualstudio.com`), and then select the artifact project.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-132">Open the home page of your team collection (for example, `https://contoso-web-team.visualstudio.com`), and then select the artifact project.</span></span>
2. <span data-ttu-id="2e8c0-133">On the project home page, select **Code**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-133">On the project home page, select **Code**.</span></span>
3. <span data-ttu-id="2e8c0-134">To view the clone URL, on the project **Code** page, select **Clone**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-134">To view the clone URL, on the project **Code** page, select **Clone**.</span></span>
4. <span data-ttu-id="2e8c0-135">Save the URL as you need it later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-135">Save the URL as you need it later in this tutorial.</span></span>
5. <span data-ttu-id="2e8c0-136">To create a Personal Access Token, select **My profile** from the user account drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-136">To create a Personal Access Token, select **My profile** from the user account drop-down menu.</span></span>
6. <span data-ttu-id="2e8c0-137">On the profile information page, select **Security**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-137">On the profile information page, select **Security**.</span></span>
7. <span data-ttu-id="2e8c0-138">On the **Security** tab, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-138">On the **Security** tab, select **Add**.</span></span>
8. <span data-ttu-id="2e8c0-139">In the **Create a personal access token** page:</span><span class="sxs-lookup"><span data-stu-id="2e8c0-139">In the **Create a personal access token** page:</span></span>
   
   * <span data-ttu-id="2e8c0-140">Enter a **Description** for the token.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-140">Enter a **Description** for the token.</span></span>
   * <span data-ttu-id="2e8c0-141">Select **180 days** from the **Expires In** list.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-141">Select **180 days** from the **Expires In** list.</span></span>
   * <span data-ttu-id="2e8c0-142">Choose **All accessible accounts** from the **Accounts** list.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-142">Choose **All accessible accounts** from the **Accounts** list.</span></span>
   * <span data-ttu-id="2e8c0-143">Choose the **All scopes** option.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-143">Choose the **All scopes** option.</span></span>
   * <span data-ttu-id="2e8c0-144">Choose **Create Token**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-144">Choose **Create Token**.</span></span>
9. <span data-ttu-id="2e8c0-145">When finished, the new token appears in the **Personal Access Tokens** list.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-145">When finished, the new token appears in the **Personal Access Tokens** list.</span></span> <span data-ttu-id="2e8c0-146">Select **Copy Token**, and then save the token value for later use.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-146">Select **Copy Token**, and then save the token value for later use.</span></span>
10. <span data-ttu-id="2e8c0-147">Continue to the [Connect your lab to the artifact repository](#connect-your-lab-to-the-artifact-repository) section.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-147">Continue to the [Connect your lab to the artifact repository](#connect-your-lab-to-the-artifact-repository) section.</span></span>

## <a name="connect-your-lab-to-the-artifact-repository"></a><span data-ttu-id="2e8c0-148">Connect your lab to the artifact repository</span><span class="sxs-lookup"><span data-stu-id="2e8c0-148">Connect your lab to the artifact repository</span></span>
1. <span data-ttu-id="2e8c0-149">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="2e8c0-149">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="2e8c0-150">Select **More Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-150">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="2e8c0-151">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-151">From the list of labs, select the desired lab.</span></span>   
4. <span data-ttu-id="2e8c0-152">On the lab's blade, select **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-152">On the lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="2e8c0-153">On the lab's **Configuration** blade, select **Artifacts Repositories**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-153">On the lab's **Configuration** blade, select **Artifacts Repositories**.</span></span>
6. <span data-ttu-id="2e8c0-154">On the **Artifacts Repositories** blade, select **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-154">On the **Artifacts Repositories** blade, select **+ Add**.</span></span>
   
    ![Add artifact repository button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-add-artifact-repo/add-artifact-repo.png)
7. <span data-ttu-id="2e8c0-156">On the second **Artifacts Repositories** blade, specify the following:</span><span class="sxs-lookup"><span data-stu-id="2e8c0-156">On the second **Artifacts Repositories** blade, specify the following:</span></span>
   
   * <span data-ttu-id="2e8c0-157">**Name** - Enter a name for the repository.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-157">**Name** - Enter a name for the repository.</span></span>
   * <span data-ttu-id="2e8c0-158">**Git Clone Url** - Enter the Git HTTPS clone URL that you copied earlier from either GitHub or Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-158">**Git Clone Url** - Enter the Git HTTPS clone URL that you copied earlier from either GitHub or Visual Studio Team Services.</span></span> 
   * <span data-ttu-id="2e8c0-159">**Folder Path** - Enter the folder path relative to the clone URL that contains your artifact definitions.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-159">**Folder Path** - Enter the folder path relative to the clone URL that contains your artifact definitions.</span></span>
   * <span data-ttu-id="2e8c0-160">**Branch** - Enter the branch to get your artifact definitions.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-160">**Branch** - Enter the branch to get your artifact definitions.</span></span>
   * <span data-ttu-id="2e8c0-161">**Personal Access Token** - Enter the personal access token you obtained earlier from either GitHub or Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-161">**Personal Access Token** - Enter the personal access token you obtained earlier from either GitHub or Visual Studio Team Services.</span></span> 
     
     ![Artifact repo blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-add-artifact-repo/artifact-repo-blade.png)
8. <span data-ttu-id="2e8c0-163">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-163">Select **Save**.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="2e8c0-164">Related blog posts</span><span class="sxs-lookup"><span data-stu-id="2e8c0-164">Related blog posts</span></span>
* [<span data-ttu-id="2e8c0-165">How to troubleshoot failing Artifacts in AzureDevTestLabs</span><span class="sxs-lookup"><span data-stu-id="2e8c0-165">How to troubleshoot failing Artifacts in AzureDevTestLabs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-to-troubleshoot-failing-artifacts-in-AzureDevTestLabs)
* [<span data-ttu-id="2e8c0-166">Join a VM to existing AD Domain using ARM template in Azure Dev Test Lab</span><span class="sxs-lookup"><span data-stu-id="2e8c0-166">Join a VM to existing AD Domain using ARM template in Azure Dev Test Lab</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)




