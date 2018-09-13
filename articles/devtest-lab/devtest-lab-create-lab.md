---
title: Create a lab in Azure DevTest Labs | Microsoft Docs
description: Create a lab in Azure DevTest Labs for virtual machines
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: ''
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/12/2016
ms.author: tarcher
ms.openlocfilehash: 0e1d108f01ddcde65b944b1e8b5f849e8219791b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552107"
---
# <a name="create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="75c06-103">Create a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="75c06-103">Create a lab in Azure DevTest Labs</span></span>
## <a name="prerequisites"></a><span data-ttu-id="75c06-104">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="75c06-104">Prerequisites</span></span>
<span data-ttu-id="75c06-105">To create a lab, you need:</span><span class="sxs-lookup"><span data-stu-id="75c06-105">To create a lab, you need:</span></span>

* <span data-ttu-id="75c06-106">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="75c06-106">An Azure subscription.</span></span> <span data-ttu-id="75c06-107">To learn about Azure purchase options, see [How to buy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="75c06-107">To learn about Azure purchase options, see [How to buy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="75c06-108">You must be the owner of the subscription to create the lab.</span><span class="sxs-lookup"><span data-stu-id="75c06-108">You must be the owner of the subscription to create the lab.</span></span>

## <a name="steps-to-create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="75c06-109">Steps to create a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="75c06-109">Steps to create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="75c06-110">The following steps illustrate how to use the Azure portal to create a lab in Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="75c06-110">The following steps illustrate how to use the Azure portal to create a lab in Azure DevTest Labs.</span></span> 

1. <span data-ttu-id="75c06-111">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="75c06-111">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="75c06-112">Select **More services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="75c06-112">Select **More services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="75c06-113">On the **DevTest Labs** blade, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="75c06-113">On the **DevTest Labs** blade, select **Add**.</span></span>
   
    ![Add a lab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-create-lab/add-lab-button.png)
4. <span data-ttu-id="75c06-115">On the **Create a DevTest Lab** blade:</span><span class="sxs-lookup"><span data-stu-id="75c06-115">On the **Create a DevTest Lab** blade:</span></span>
   
   1. <span data-ttu-id="75c06-116">Enter a **Lab Name** for the new lab.</span><span class="sxs-lookup"><span data-stu-id="75c06-116">Enter a **Lab Name** for the new lab.</span></span>
   2. <span data-ttu-id="75c06-117">Select the **Subscription** to associate with the lab.</span><span class="sxs-lookup"><span data-stu-id="75c06-117">Select the **Subscription** to associate with the lab.</span></span>
   3. <span data-ttu-id="75c06-118">Select a **Location** in which to store the lab.</span><span class="sxs-lookup"><span data-stu-id="75c06-118">Select a **Location** in which to store the lab.</span></span>
   4. <span data-ttu-id="75c06-119">Select **Auto-shutdown** to specify if you want to enable - and define the parameters for - the automatic shutting down of all the lab's VMs.</span><span class="sxs-lookup"><span data-stu-id="75c06-119">Select **Auto-shutdown** to specify if you want to enable - and define the parameters for - the automatic shutting down of all the lab's VMs.</span></span> 
   5. <span data-ttu-id="75c06-120">Select **Pin to Dashboard** if you want a shortcut of the lab to appear on the portal dashboard.</span><span class="sxs-lookup"><span data-stu-id="75c06-120">Select **Pin to Dashboard** if you want a shortcut of the lab to appear on the portal dashboard.</span></span>
   6. <span data-ttu-id="75c06-121">Select **Automation options** to get Azure Resource Manager templates for configuration automation.</span><span class="sxs-lookup"><span data-stu-id="75c06-121">Select **Automation options** to get Azure Resource Manager templates for configuration automation.</span></span> 
   7. <span data-ttu-id="75c06-122">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="75c06-122">Select **Create**.</span></span>
    
    ![Create a lab blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="75c06-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="75c06-124">Next steps</span></span>
<span data-ttu-id="75c06-125">Once you've created your lab, here are some next steps to consider:</span><span class="sxs-lookup"><span data-stu-id="75c06-125">Once you've created your lab, here are some next steps to consider:</span></span>

* <span data-ttu-id="75c06-126">[Secure access to a lab](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="75c06-126">[Secure access to a lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="75c06-127">[Set lab policies](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="75c06-127">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="75c06-128">[Create a lab template](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="75c06-128">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="75c06-129">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="75c06-129">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="75c06-130">[Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="75c06-130">[Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span></span>



