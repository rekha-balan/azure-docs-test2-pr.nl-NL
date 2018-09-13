---
title: Azure Stack Quick Start - Create a Windows virtual machine
description: Azure Stack Quick Start - Create a Windows VM using the portal
services: azure-stack
author: mattbriggs
manager: femila
ms.service: azure-stack
ms.topic: quickstart
ms.date: 09/05/2018
ms.author: mabrigg
ms.reviewer: ''
ms.custom: mvc
ms.openlocfilehash: 7277aeb97409815e2e218da8f233cd836bccc72b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871447"
---
# <a name="quickstart-create-a-windows-server-virtual-machine-with-the-azure-stack-portal"></a><span data-ttu-id="b070f-103">Quickstart: create a Windows server virtual machine with the Azure Stack portal</span><span class="sxs-lookup"><span data-stu-id="b070f-103">Quickstart: create a Windows server virtual machine with the Azure Stack portal</span></span>

<span data-ttu-id="b070f-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="b070f-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="b070f-105">You can create a Windows Server 2016 virtual machine by using the Azure Stack portal.</span><span class="sxs-lookup"><span data-stu-id="b070f-105">You can create a Windows Server 2016 virtual machine by using the Azure Stack portal.</span></span> <span data-ttu-id="b070f-106">Follow the steps in this article to create and use a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b070f-106">Follow the steps in this article to create and use a virtual machine.</span></span>

> [!NOTE]  
> <span data-ttu-id="b070f-107">The screen images in this article are updated to match the user interface that is introduced with Azure Stack version 1808.</span><span class="sxs-lookup"><span data-stu-id="b070f-107">The screen images in this article are updated to match the user interface that is introduced with Azure Stack version 1808.</span></span> <span data-ttu-id="b070f-108">1808 adds support for using *managed disks* in addition to unmanaged disks.</span><span class="sxs-lookup"><span data-stu-id="b070f-108">1808 adds support for using *managed disks* in addition to unmanaged disks.</span></span> <span data-ttu-id="b070f-109">If you use an earlier version, some images like disk selection, will be different than what is displayed in this article.</span><span class="sxs-lookup"><span data-stu-id="b070f-109">If you use an earlier version, some images like disk selection, will be different than what is displayed in this article.</span></span>  


## <a name="sign-in-to-the-azure-stack-portal"></a><span data-ttu-id="b070f-110">Sign in to the Azure Stack portal</span><span class="sxs-lookup"><span data-stu-id="b070f-110">Sign in to the Azure Stack portal</span></span>

<span data-ttu-id="b070f-111">Sign in to the Azure Stack portal.</span><span class="sxs-lookup"><span data-stu-id="b070f-111">Sign in to the Azure Stack portal.</span></span> <span data-ttu-id="b070f-112">The address of the Azure Stack portal depends on which Azure Stack product you're connecting to:</span><span class="sxs-lookup"><span data-stu-id="b070f-112">The address of the Azure Stack portal depends on which Azure Stack product you're connecting to:</span></span>

* <span data-ttu-id="b070f-113">For the Azure Stack Development Kit (ASDK) go to: https://portal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="b070f-113">For the Azure Stack Development Kit (ASDK) go to: https://portal.local.azurestack.external.</span></span>
* <span data-ttu-id="b070f-114">For an Azure Stack integrated system, go to the URL that your Azure Stack operator provided.</span><span class="sxs-lookup"><span data-stu-id="b070f-114">For an Azure Stack integrated system, go to the URL that your Azure Stack operator provided.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="b070f-115">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="b070f-115">Create a virtual machine</span></span>

1. <span data-ttu-id="b070f-116">Click **New** > **Compute** > **Windows Server 2016 Datacenter – Pay-as-you-use** > **Create**.</span><span class="sxs-lookup"><span data-stu-id="b070f-116">Click **New** > **Compute** > **Windows Server 2016 Datacenter – Pay-as-you-use** > **Create**.</span></span> <span data-ttu-id="b070f-117">If you don't see **Windows Server 2016 Datacenter – Pay-as-you-use** entry, contact your Azure Stack operator.</span><span class="sxs-lookup"><span data-stu-id="b070f-117">If you don't see **Windows Server 2016 Datacenter – Pay-as-you-use** entry, contact your Azure Stack operator.</span></span> <span data-ttu-id="b070f-118">Ask that they add it to the marketplace as explained in the [Add the Windows Server 2016 VM image to the Azure Stack marketplace](../azure-stack-add-default-image.md) article.</span><span class="sxs-lookup"><span data-stu-id="b070f-118">Ask that they add it to the marketplace as explained in the [Add the Windows Server 2016 VM image to the Azure Stack marketplace](../azure-stack-add-default-image.md) article.</span></span>

    ![Steps to create a Windows virtual machine in portal](media/azure-stack-quick-windows-portal/image01.png)
2. <span data-ttu-id="b070f-120">Under **Basics**, type a **Name**, **User name**, and **Password**.</span><span class="sxs-lookup"><span data-stu-id="b070f-120">Under **Basics**, type a **Name**, **User name**, and **Password**.</span></span> <span data-ttu-id="b070f-121">Choose a **Subscription**.</span><span class="sxs-lookup"><span data-stu-id="b070f-121">Choose a **Subscription**.</span></span> <span data-ttu-id="b070f-122">Create a **Resource group**, or select an existing one, select a **Location**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b070f-122">Create a **Resource group**, or select an existing one, select a **Location**, and then click **OK**.</span></span>

    ![Configure basic settings](media/azure-stack-quick-windows-portal/image02.png)
3. <span data-ttu-id="b070f-124">Under **Size** select **D1 Standard**, and then click on **Select**.</span><span class="sxs-lookup"><span data-stu-id="b070f-124">Under **Size** select **D1 Standard**, and then click on **Select**.</span></span>  
    <span data-ttu-id="b070f-125">![Choose size of virtual machine](media/azure-stack-quick-windows-portal/image03.png)</span><span class="sxs-lookup"><span data-stu-id="b070f-125">![Choose size of virtual machine](media/azure-stack-quick-windows-portal/image03.png)</span></span>

4. <span data-ttu-id="b070f-126">On the **Settings** page, make any desired changes to the defaults.</span><span class="sxs-lookup"><span data-stu-id="b070f-126">On the **Settings** page, make any desired changes to the defaults.</span></span>
   - <span data-ttu-id="b070f-127">Beginning with Azure Stack version 1808, you can configure **Storage** where you can choose to use *managed disks*.</span><span class="sxs-lookup"><span data-stu-id="b070f-127">Beginning with Azure Stack version 1808, you can configure **Storage** where you can choose to use *managed disks*.</span></span> <span data-ttu-id="b070f-128">Prior to version 1808 only unmanaged disks can be used.</span><span class="sxs-lookup"><span data-stu-id="b070f-128">Prior to version 1808 only unmanaged disks can be used.</span></span>  
   <span data-ttu-id="b070f-129">![Configure virtual machine settings](media/azure-stack-quick-windows-portal/image04.png)</span><span class="sxs-lookup"><span data-stu-id="b070f-129">![Configure virtual machine settings](media/azure-stack-quick-windows-portal/image04.png)</span></span>  
   <span data-ttu-id="b070f-130">When your configurations are ready, select **OK** to continue.</span><span class="sxs-lookup"><span data-stu-id="b070f-130">When your configurations are ready, select **OK** to continue.</span></span>

5. <span data-ttu-id="b070f-131">Under **Summary**, click **OK** to create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b070f-131">Under **Summary**, click **OK** to create the virtual machine.</span></span>
    <span data-ttu-id="b070f-132">![View summary and create virtual machine](media/azure-stack-quick-windows-portal/image05.png)</span><span class="sxs-lookup"><span data-stu-id="b070f-132">![View summary and create virtual machine](media/azure-stack-quick-windows-portal/image05.png)</span></span>

6. <span data-ttu-id="b070f-133">To see your new virtual machine, click **All resources**, search for the virtual machine name, and then click its name in the search results.</span><span class="sxs-lookup"><span data-stu-id="b070f-133">To see your new virtual machine, click **All resources**, search for the virtual machine name, and then click its name in the search results.</span></span>
    <span data-ttu-id="b070f-134">![See virtual machine](media/azure-stack-quick-windows-portal/image06.png)</span><span class="sxs-lookup"><span data-stu-id="b070f-134">![See virtual machine](media/azure-stack-quick-windows-portal/image06.png)</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="b070f-135">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="b070f-135">Clean up resources</span></span>

<span data-ttu-id="b070f-136">When you're finished using the virtual machine, delete the virtual machine and its resources.</span><span class="sxs-lookup"><span data-stu-id="b070f-136">When you're finished using the virtual machine, delete the virtual machine and its resources.</span></span> <span data-ttu-id="b070f-137">To do so, select the resource group on the virtual machine page and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="b070f-137">To do so, select the resource group on the virtual machine page and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b070f-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="b070f-138">Next steps</span></span>

<span data-ttu-id="b070f-139">In this quick start, you deployed a basic Windows Server virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b070f-139">In this quick start, you deployed a basic Windows Server virtual machine.</span></span> <span data-ttu-id="b070f-140">To learn more about Azure Stack virtual machines, continue to [Considerations for Virtual Machines in Azure Stack](azure-stack-vm-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="b070f-140">To learn more about Azure Stack virtual machines, continue to [Considerations for Virtual Machines in Azure Stack](azure-stack-vm-considerations.md).</span></span>
