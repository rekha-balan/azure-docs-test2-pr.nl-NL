---
title: Diagnose artifact failures in an Azure DevTest Labs virtual machine | Microsoft Docs
description: Learn how to troubleshoot artifact failures in Azure DevTest Labs.
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: 115e0086-3293-4adf-8738-9f639f31f918
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: ebc64215683989ce07f4dd88dc352ecaefe184cd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855819"
---
# <a name="diagnose-artifact-failures-in-the-lab"></a><span data-ttu-id="6e2b5-103">Diagnose artifact failures in the lab</span><span class="sxs-lookup"><span data-stu-id="6e2b5-103">Diagnose artifact failures in the lab</span></span> 
<span data-ttu-id="6e2b5-104">After you have created an artifact, you can check to see whether it succeeded or failed.</span><span class="sxs-lookup"><span data-stu-id="6e2b5-104">After you have created an artifact, you can check to see whether it succeeded or failed.</span></span> <span data-ttu-id="6e2b5-105">Artifact logs in Azure DevTest Labs provide information that you can use to diagnose an artifact failure.</span><span class="sxs-lookup"><span data-stu-id="6e2b5-105">Artifact logs in Azure DevTest Labs provide information that you can use to diagnose an artifact failure.</span></span> <span data-ttu-id="6e2b5-106">You have a couple of options for viewing the artifact log information for a Windows VM:</span><span class="sxs-lookup"><span data-stu-id="6e2b5-106">You have a couple of options for viewing the artifact log information for a Windows VM:</span></span>

* <span data-ttu-id="6e2b5-107">In the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6e2b5-107">In the Azure portal</span></span>
* <span data-ttu-id="6e2b5-108">In the VM</span><span class="sxs-lookup"><span data-stu-id="6e2b5-108">In the VM</span></span>

> [!NOTE]
> <span data-ttu-id="6e2b5-109">To ensure that failures are correctly identified and explained, it's important that the artifact has the proper structure.</span><span class="sxs-lookup"><span data-stu-id="6e2b5-109">To ensure that failures are correctly identified and explained, it's important that the artifact has the proper structure.</span></span> <span data-ttu-id="6e2b5-110">For information about how to correctly construct an artifact, see [Create custom artifacts](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="6e2b5-110">For information about how to correctly construct an artifact, see [Create custom artifacts](devtest-lab-artifact-author.md).</span></span> <span data-ttu-id="6e2b5-111">To see an example of a properly structured artifact, check out the [Test parameter types](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artifact.</span><span class="sxs-lookup"><span data-stu-id="6e2b5-111">To see an example of a properly structured artifact, check out the [Test parameter types](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artifact.</span></span>

## <a name="troubleshoot-artifact-failures-by-using-the-azure-portal"></a><span data-ttu-id="6e2b5-112">Troubleshoot artifact failures by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6e2b5-112">Troubleshoot artifact failures by using the Azure portal</span></span>

1. <span data-ttu-id="6e2b5-113">In the Azure portal, in your list of resources, select your lab.</span><span class="sxs-lookup"><span data-stu-id="6e2b5-113">In the Azure portal, in your list of resources, select your lab.</span></span>
2. <span data-ttu-id="6e2b5-114">Choose the Windows VM that includes the artifact that you want to investigate.</span><span class="sxs-lookup"><span data-stu-id="6e2b5-114">Choose the Windows VM that includes the artifact that you want to investigate.</span></span>
3. <span data-ttu-id="6e2b5-115">In the left panel, under **GENERAL**, select **Artifacts**.</span><span class="sxs-lookup"><span data-stu-id="6e2b5-115">In the left panel, under **GENERAL**, select **Artifacts**.</span></span> <span data-ttu-id="6e2b5-116">A list of artifacts associated with that VM appears.</span><span class="sxs-lookup"><span data-stu-id="6e2b5-116">A list of artifacts associated with that VM appears.</span></span> <span data-ttu-id="6e2b5-117">The name of the artifact and the artifact status are indicated.</span><span class="sxs-lookup"><span data-stu-id="6e2b5-117">The name of the artifact and the artifact status are indicated.</span></span>

   ![Artifact status](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. <span data-ttu-id="6e2b5-119">Select an artifact that shows a **Failed** status.</span><span class="sxs-lookup"><span data-stu-id="6e2b5-119">Select an artifact that shows a **Failed** status.</span></span> <span data-ttu-id="6e2b5-120">The artifact opens.</span><span class="sxs-lookup"><span data-stu-id="6e2b5-120">The artifact opens.</span></span> <span data-ttu-id="6e2b5-121">An extension message that includes details about the failure of the artifact is displayed.</span><span class="sxs-lookup"><span data-stu-id="6e2b5-121">An extension message that includes details about the failure of the artifact is displayed.</span></span>

   ![Artifact error message](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-the-virtual-machine"></a><span data-ttu-id="6e2b5-123">Troubleshoot artifact failures from within the virtual machine</span><span class="sxs-lookup"><span data-stu-id="6e2b5-123">Troubleshoot artifact failures from within the virtual machine</span></span>

1. <span data-ttu-id="6e2b5-124">Sign in to the VM that contains the artifact you want to diagnose.</span><span class="sxs-lookup"><span data-stu-id="6e2b5-124">Sign in to the VM that contains the artifact you want to diagnose.</span></span>
2. <span data-ttu-id="6e2b5-125">Go to C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\\*1.9*\Status, where *1.9* is the Azure Custom Script Extension version number.</span><span class="sxs-lookup"><span data-stu-id="6e2b5-125">Go to C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\\*1.9*\Status, where *1.9* is the Azure Custom Script Extension version number.</span></span>

   ![The Status file](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. <span data-ttu-id="6e2b5-127">Open the **status** file.</span><span class="sxs-lookup"><span data-stu-id="6e2b5-127">Open the **status** file.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="6e2b5-128">Related blog posts</span><span class="sxs-lookup"><span data-stu-id="6e2b5-128">Related blog posts</span></span>
* [<span data-ttu-id="6e2b5-129">Join a VM to an existing Active Directory domain by using a Resource Manager template in DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="6e2b5-129">Join a VM to an existing Active Directory domain by using a Resource Manager template in DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="6e2b5-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="6e2b5-130">Next steps</span></span>
* <span data-ttu-id="6e2b5-131">Learn how to [add a Git repository to a lab](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="6e2b5-131">Learn how to [add a Git repository to a lab](devtest-lab-add-artifact-repo.md).</span></span>

