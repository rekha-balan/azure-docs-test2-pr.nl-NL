---
title: Add a Git repository to a lab in Azure DevTest Labs | Microsoft Docs
description: Add a GitHub or Visual Studio Team Services Git repository for your custom artifacts source or Azure Resource Manager templates in Azure DevTest Labs
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: ''
ms.assetid: 102a8a14-e17c-4b91-80fd-ce81640d04c9
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tarcher
ms.openlocfilehash: e76bb89da30aae8ddbb06d6df6a20acdd9718ab1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564649"
---
# <a name="add-a-git-repository-to-store-custom-artifacts-and-azure-resource-manager-templates-for-use-in-azure-devtest-labs"></a><span data-ttu-id="6cae2-103">Add a Git repository to store custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="6cae2-103">Add a Git repository to store custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>

<span data-ttu-id="6cae2-104">If you want to [create custom artifacts](devtest-lab-artifact-author.md) for the VMs in your lab, or [use Azure Resource Manager templates to create a custom test environment](devtest-lab-create-environment-from-arm.md), you must also add a private Git repository to include the artifacts or Azure Resource Manager templates that your team creates.</span><span class="sxs-lookup"><span data-stu-id="6cae2-104">If you want to [create custom artifacts](devtest-lab-artifact-author.md) for the VMs in your lab, or [use Azure Resource Manager templates to create a custom test environment](devtest-lab-create-environment-from-arm.md), you must also add a private Git repository to include the artifacts or Azure Resource Manager templates that your team creates.</span></span> <span data-ttu-id="6cae2-105">The repository can be hosted on [GitHub](https://github.com) or on [Visual Studio Team Services (VSTS)](https://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="6cae2-105">The repository can be hosted on [GitHub](https://github.com) or on [Visual Studio Team Services (VSTS)](https://visualstudio.com).</span></span>

<span data-ttu-id="6cae2-106">We have provided a [Github repository of artifacts](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts) that you can deploy as-is or customize for your labs.</span><span class="sxs-lookup"><span data-stu-id="6cae2-106">We have provided a [Github repository of artifacts](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts) that you can deploy as-is or customize for your labs.</span></span> <span data-ttu-id="6cae2-107">When you customize or create an artifact, you cannot store them in the public repository – you must create your own private repo.</span><span class="sxs-lookup"><span data-stu-id="6cae2-107">When you customize or create an artifact, you cannot store them in the public repository – you must create your own private repo.</span></span> 

<span data-ttu-id="6cae2-108">When you create a VM, you can save the Azure Resource Manager template, customize it if you want, and then use it later to easily create more VMs.</span><span class="sxs-lookup"><span data-stu-id="6cae2-108">When you create a VM, you can save the Azure Resource Manager template, customize it if you want, and then use it later to easily create more VMs.</span></span> <span data-ttu-id="6cae2-109">You must create your own private repository to store your custom Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="6cae2-109">You must create your own private repository to store your custom Azure Resource Manager templates.</span></span>  

* <span data-ttu-id="6cae2-110">To learn how to create a GitHub repository, see [GitHub Bootcamp](https://help.github.com/categories/bootcamp/).</span><span class="sxs-lookup"><span data-stu-id="6cae2-110">To learn how to create a GitHub repository, see [GitHub Bootcamp](https://help.github.com/categories/bootcamp/).</span></span>
* <span data-ttu-id="6cae2-111">To learn how to create a Team Services project with a Git Repository, see [Connect to Visual Studio Team Services](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online).</span><span class="sxs-lookup"><span data-stu-id="6cae2-111">To learn how to create a Team Services project with a Git Repository, see [Connect to Visual Studio Team Services](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online).</span></span>

<span data-ttu-id="6cae2-112">The following screen shot shows an example of how a repository containing artifacts might look in GitHub:</span><span class="sxs-lookup"><span data-stu-id="6cae2-112">The following screen shot shows an example of how a repository containing artifacts might look in GitHub:</span></span>  
![Sample GitHub artifacts repo](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-add-repo/devtestlab-github-artifact-repo-home.png)

## <a name="get-the-repository-information-and-credentials"></a><span data-ttu-id="6cae2-114">Get the repository information and credentials</span><span class="sxs-lookup"><span data-stu-id="6cae2-114">Get the repository information and credentials</span></span>
<span data-ttu-id="6cae2-115">To add a repository to your lab, you must first get certain information from your repository.</span><span class="sxs-lookup"><span data-stu-id="6cae2-115">To add a repository to your lab, you must first get certain information from your repository.</span></span> <span data-ttu-id="6cae2-116">The following sections guide you through getting this information for repositories hosted on GitHub and Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="6cae2-116">The following sections guide you through getting this information for repositories hosted on GitHub and Visual Studio Team Services.</span></span>

### <a name="get-the-github-repository-clone-url-and-personal-access-token"></a><span data-ttu-id="6cae2-117">Get the GitHub repository clone URL and personal access token</span><span class="sxs-lookup"><span data-stu-id="6cae2-117">Get the GitHub repository clone URL and personal access token</span></span>
<span data-ttu-id="6cae2-118">To get the GitHub repository clone URL and personal access token, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="6cae2-118">To get the GitHub repository clone URL and personal access token, follow these steps:</span></span>

1. <span data-ttu-id="6cae2-119">Browse to the home page of the GitHub repository that contains the artifact or Azure Resource Manager template definitions.</span><span class="sxs-lookup"><span data-stu-id="6cae2-119">Browse to the home page of the GitHub repository that contains the artifact or Azure Resource Manager template definitions.</span></span>
2. <span data-ttu-id="6cae2-120">Select **Clone or download**.</span><span class="sxs-lookup"><span data-stu-id="6cae2-120">Select **Clone or download**.</span></span>
3. <span data-ttu-id="6cae2-121">Select the button to copy the **HTTPS clone url** to the clipboard, and save the URL for later use.</span><span class="sxs-lookup"><span data-stu-id="6cae2-121">Select the button to copy the **HTTPS clone url** to the clipboard, and save the URL for later use.</span></span>
4. <span data-ttu-id="6cae2-122">Select the profile image in the upper-right corner of GitHub, and select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="6cae2-122">Select the profile image in the upper-right corner of GitHub, and select **Settings**.</span></span>
5. <span data-ttu-id="6cae2-123">In the **Personal settings** menu on the left, select **Personal access tokens**.</span><span class="sxs-lookup"><span data-stu-id="6cae2-123">In the **Personal settings** menu on the left, select **Personal access tokens**.</span></span>
6. <span data-ttu-id="6cae2-124">Select **Generate new token**.</span><span class="sxs-lookup"><span data-stu-id="6cae2-124">Select **Generate new token**.</span></span>
7. <span data-ttu-id="6cae2-125">On the **New personal access token** page, enter a **Token description**, accept the default items in the **Select scopes**, and then choose **Generate Token**.</span><span class="sxs-lookup"><span data-stu-id="6cae2-125">On the **New personal access token** page, enter a **Token description**, accept the default items in the **Select scopes**, and then choose **Generate Token**.</span></span>
8. <span data-ttu-id="6cae2-126">Save the generated token as you need it later.</span><span class="sxs-lookup"><span data-stu-id="6cae2-126">Save the generated token as you need it later.</span></span>
9. <span data-ttu-id="6cae2-127">You can close GitHub now.</span><span class="sxs-lookup"><span data-stu-id="6cae2-127">You can close GitHub now.</span></span>   
10. <span data-ttu-id="6cae2-128">Continue to the [Connect your lab to the repository](#connect-your-lab-to-the-repository) section.</span><span class="sxs-lookup"><span data-stu-id="6cae2-128">Continue to the [Connect your lab to the repository](#connect-your-lab-to-the-repository) section.</span></span>

### <a name="get-the-visual-studio-team-services-repository-clone-url-and-personal-access-token"></a><span data-ttu-id="6cae2-129">Get the Visual Studio Team Services repository clone URL and personal access token</span><span class="sxs-lookup"><span data-stu-id="6cae2-129">Get the Visual Studio Team Services repository clone URL and personal access token</span></span>
<span data-ttu-id="6cae2-130">To get the Visual Studio Team Services repository clone URL and personal access token, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="6cae2-130">To get the Visual Studio Team Services repository clone URL and personal access token, follow these steps:</span></span>

1. <span data-ttu-id="6cae2-131">Open the home page of your team collection (for example, `https://contoso-web-team.visualstudio.com`), and then select your project.</span><span class="sxs-lookup"><span data-stu-id="6cae2-131">Open the home page of your team collection (for example, `https://contoso-web-team.visualstudio.com`), and then select your project.</span></span>
2. <span data-ttu-id="6cae2-132">On the project home page, select **Code**.</span><span class="sxs-lookup"><span data-stu-id="6cae2-132">On the project home page, select **Code**.</span></span>
3. <span data-ttu-id="6cae2-133">To view the clone URL, on the project **Code** page, select **Clone**.</span><span class="sxs-lookup"><span data-stu-id="6cae2-133">To view the clone URL, on the project **Code** page, select **Clone**.</span></span>
4. <span data-ttu-id="6cae2-134">Save the URL as you need it later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="6cae2-134">Save the URL as you need it later in this tutorial.</span></span>
5. <span data-ttu-id="6cae2-135">To create a Personal Access Token, select **My profile** from the user account drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="6cae2-135">To create a Personal Access Token, select **My profile** from the user account drop-down menu.</span></span>
6. <span data-ttu-id="6cae2-136">On the profile information page, select **Security**.</span><span class="sxs-lookup"><span data-stu-id="6cae2-136">On the profile information page, select **Security**.</span></span>
7. <span data-ttu-id="6cae2-137">On the **Security** tab, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="6cae2-137">On the **Security** tab, select **Add**.</span></span>
8. <span data-ttu-id="6cae2-138">In the **Create a personal access token** page:</span><span class="sxs-lookup"><span data-stu-id="6cae2-138">In the **Create a personal access token** page:</span></span>

   * <span data-ttu-id="6cae2-139">Enter a **Description** for the token.</span><span class="sxs-lookup"><span data-stu-id="6cae2-139">Enter a **Description** for the token.</span></span>
   * <span data-ttu-id="6cae2-140">Select **180 days** from the **Expires In** list.</span><span class="sxs-lookup"><span data-stu-id="6cae2-140">Select **180 days** from the **Expires In** list.</span></span>
   * <span data-ttu-id="6cae2-141">Choose **All accessible accounts** from the **Accounts** list.</span><span class="sxs-lookup"><span data-stu-id="6cae2-141">Choose **All accessible accounts** from the **Accounts** list.</span></span>
   * <span data-ttu-id="6cae2-142">Choose the **All scopes** option.</span><span class="sxs-lookup"><span data-stu-id="6cae2-142">Choose the **All scopes** option.</span></span>
   * <span data-ttu-id="6cae2-143">Choose **Create Token**.</span><span class="sxs-lookup"><span data-stu-id="6cae2-143">Choose **Create Token**.</span></span>
9. <span data-ttu-id="6cae2-144">When finished, the new token appears in the **Personal Access Tokens** list.</span><span class="sxs-lookup"><span data-stu-id="6cae2-144">When finished, the new token appears in the **Personal Access Tokens** list.</span></span> <span data-ttu-id="6cae2-145">Select **Copy Token**, and then save the token value for later use.</span><span class="sxs-lookup"><span data-stu-id="6cae2-145">Select **Copy Token**, and then save the token value for later use.</span></span>
10. <span data-ttu-id="6cae2-146">Continue to the [Connect your lab to the repository](#connect-your-lab-to-the-repository) section.</span><span class="sxs-lookup"><span data-stu-id="6cae2-146">Continue to the [Connect your lab to the repository](#connect-your-lab-to-the-repository) section.</span></span>

## <a name="connect-your-lab-to-the-repository"></a><span data-ttu-id="6cae2-147">Connect your lab to the repository</span><span class="sxs-lookup"><span data-stu-id="6cae2-147">Connect your lab to the repository</span></span>
1. <span data-ttu-id="6cae2-148">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="6cae2-148">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="6cae2-149">Select **More Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="6cae2-149">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="6cae2-150">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="6cae2-150">From the list of labs, select the desired lab.</span></span>   
4. <span data-ttu-id="6cae2-151">On the lab's blade, select **Configuration and policies**.</span><span class="sxs-lookup"><span data-stu-id="6cae2-151">On the lab's blade, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="6cae2-152">On the lab's **Configuration and policies** blade, select **Repositories**.</span><span class="sxs-lookup"><span data-stu-id="6cae2-152">On the lab's **Configuration and policies** blade, select **Repositories**.</span></span>
6. <span data-ttu-id="6cae2-153">On the **Repositories** blade, select **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="6cae2-153">On the **Repositories** blade, select **+ Add**.</span></span>

    ![Add repository button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-add-repo/devtestlab-add-repo.png)
7. <span data-ttu-id="6cae2-155">On the second **Repositories** blade, specify the following:</span><span class="sxs-lookup"><span data-stu-id="6cae2-155">On the second **Repositories** blade, specify the following:</span></span>

   * <span data-ttu-id="6cae2-156">**Name** - Enter a name for the repository.</span><span class="sxs-lookup"><span data-stu-id="6cae2-156">**Name** - Enter a name for the repository.</span></span>
   * <span data-ttu-id="6cae2-157">**Git Clone Url** - Enter the Git HTTPS clone URL that you copied earlier from either GitHub or Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="6cae2-157">**Git Clone Url** - Enter the Git HTTPS clone URL that you copied earlier from either GitHub or Visual Studio Team Services.</span></span>
   * <span data-ttu-id="6cae2-158">**Branch** - Enter the branch to get your definitions.</span><span class="sxs-lookup"><span data-stu-id="6cae2-158">**Branch** - Enter the branch to get your definitions.</span></span>
   * <span data-ttu-id="6cae2-159">**Personal Access Token** - Enter the personal access token you obtained earlier from either GitHub or Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="6cae2-159">**Personal Access Token** - Enter the personal access token you obtained earlier from either GitHub or Visual Studio Team Services.</span></span>
   * <span data-ttu-id="6cae2-160">**Folder Paths** - Enter at least one folder path relative to the clone URL that contains your artifact or Azure Resource Manager template definitions.</span><span class="sxs-lookup"><span data-stu-id="6cae2-160">**Folder Paths** - Enter at least one folder path relative to the clone URL that contains your artifact or Azure Resource Manager template definitions.</span></span> <span data-ttu-id="6cae2-161">When specifying a subdirectory, make sure to include the forward slash in the folder path.</span><span class="sxs-lookup"><span data-stu-id="6cae2-161">When specifying a subdirectory, make sure to include the forward slash in the folder path.</span></span>

     ![Repo blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-add-repo/devtestlab-repo-blade.png)
8. <span data-ttu-id="6cae2-163">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="6cae2-163">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cae2-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="6cae2-164">Next steps</span></span>
<span data-ttu-id="6cae2-165">After you have created your private Git repository, you can do one or both of the following, depending on your needs:</span><span class="sxs-lookup"><span data-stu-id="6cae2-165">After you have created your private Git repository, you can do one or both of the following, depending on your needs:</span></span>
* <span data-ttu-id="6cae2-166">Store your [custom artifacts](devtest-lab-artifact-author.md), which you can use later to create new VMs.</span><span class="sxs-lookup"><span data-stu-id="6cae2-166">Store your [custom artifacts](devtest-lab-artifact-author.md), which you can use later to create new VMs.</span></span>
* <span data-ttu-id="6cae2-167">[Create multi-VM environments and PaaS resources with Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md) and then store the templates in your private repo.</span><span class="sxs-lookup"><span data-stu-id="6cae2-167">[Create multi-VM environments and PaaS resources with Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md) and then store the templates in your private repo.</span></span>

<span data-ttu-id="6cae2-168">When you create a VM, you'll be able to verify that the artifacts or templates are added to your Git repository.</span><span class="sxs-lookup"><span data-stu-id="6cae2-168">When you create a VM, you'll be able to verify that the artifacts or templates are added to your Git repository.</span></span> <span data-ttu-id="6cae2-169">They will be available immediately in the list of artifacts or templates, with the name of your private repo shown in the column that specifies the source.</span><span class="sxs-lookup"><span data-stu-id="6cae2-169">They will be available immediately in the list of artifacts or templates, with the name of your private repo shown in the column that specifies the source.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="related-blog-posts"></a><span data-ttu-id="6cae2-170">Related blog posts</span><span class="sxs-lookup"><span data-stu-id="6cae2-170">Related blog posts</span></span>
* [<span data-ttu-id="6cae2-171">How to troubleshoot failing Artifacts in AzureDevTestLabs</span><span class="sxs-lookup"><span data-stu-id="6cae2-171">How to troubleshoot failing Artifacts in AzureDevTestLabs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-to-troubleshoot-failing-artifacts-in-AzureDevTestLabs)
* [<span data-ttu-id="6cae2-172">Join a VM to existing AD Domain using ARM template in Azure Dev Test Lab</span><span class="sxs-lookup"><span data-stu-id="6cae2-172">Join a VM to existing AD Domain using ARM template in Azure Dev Test Lab</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)



