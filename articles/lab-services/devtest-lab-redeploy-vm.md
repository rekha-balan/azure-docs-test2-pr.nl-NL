---
title: Redeploy a VM in a lab in Azure DevTest Labs | Microsoft Docs
description: Learn how to redeploy a virtual machine (move from one Azure node to another) in Azure DevTest Labs.
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: 8460f09e-482f-48ba-a57a-c95fe8afa001
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2018
ms.author: spelluru
ms.openlocfilehash: 273b0f1105d8b71b90a06e2627e201b97f12a754
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857187"
---
# <a name="redeploy-a-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="f71ce-103">Redeploy a VM in a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="f71ce-103">Redeploy a VM in a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="f71ce-104">If you can't connect to a virtual machine (VM) in a lab via a remote desktop connection, redeploy the VM and try conencting to it again.</span><span class="sxs-lookup"><span data-stu-id="f71ce-104">If you can't connect to a virtual machine (VM) in a lab via a remote desktop connection, redeploy the VM and try conencting to it again.</span></span> <span data-ttu-id="f71ce-105">When you redeploy a VM, DevTest Labs moves the VM from the node on which it's running to a new node within the Azure infrastructure.</span><span class="sxs-lookup"><span data-stu-id="f71ce-105">When you redeploy a VM, DevTest Labs moves the VM from the node on which it's running to a new node within the Azure infrastructure.</span></span> <span data-ttu-id="f71ce-106">It then starts the VM while retaining all your configuration options and associated resources.</span><span class="sxs-lookup"><span data-stu-id="f71ce-106">It then starts the VM while retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="f71ce-107">This feature saves you the time spent in troubleshooting your remote desktop connection or application access to Windows-based VMs in the lab.</span><span class="sxs-lookup"><span data-stu-id="f71ce-107">This feature saves you the time spent in troubleshooting your remote desktop connection or application access to Windows-based VMs in the lab.</span></span> 

## <a name="steps-to-redeploy-a-vm-in-a-lab"></a><span data-ttu-id="f71ce-108">Steps to redeploy a VM in a lab</span><span class="sxs-lookup"><span data-stu-id="f71ce-108">Steps to redeploy a VM in a lab</span></span> 
<span data-ttu-id="f71ce-109">To redeploy a VM in a lab in Azure DevTest Labs, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="f71ce-109">To redeploy a VM in a lab in Azure DevTest Labs, take the following steps:</span></span> 

1. <span data-ttu-id="f71ce-110">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f71ce-110">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f71ce-111">Select **All Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="f71ce-111">Select **All Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="f71ce-112">From the list of labs, select the lab that includes the VM  you want to redeploy.</span><span class="sxs-lookup"><span data-stu-id="f71ce-112">From the list of labs, select the lab that includes the VM  you want to redeploy.</span></span>  
4. <span data-ttu-id="f71ce-113">In the left panel, select **My Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="f71ce-113">In the left panel, select **My Virtual Machines**.</span></span> 
5. <span data-ttu-id="f71ce-114">From the list of VMs, select a VM.</span><span class="sxs-lookup"><span data-stu-id="f71ce-114">From the list of VMs, select a VM.</span></span>
6. <span data-ttu-id="f71ce-115">In the Virtual Machine page for your VM, select **Redeploy** under **OPERATIONS** in the left menu.</span><span class="sxs-lookup"><span data-stu-id="f71ce-115">In the Virtual Machine page for your VM, select **Redeploy** under **OPERATIONS** in the left menu.</span></span>

    ![Redeploy](media/devtest-lab-redeploy-vm/redeploy.png)
7. <span data-ttu-id="f71ce-117">Read the information on the page, and select **Redeploy** button.</span><span class="sxs-lookup"><span data-stu-id="f71ce-117">Read the information on the page, and select **Redeploy** button.</span></span> <span data-ttu-id="f71ce-118">9.</span><span class="sxs-lookup"><span data-stu-id="f71ce-118">9.</span></span> <span data-ttu-id="f71ce-119">Check the status of the redeploy operation in the **Notifications** window.</span><span class="sxs-lookup"><span data-stu-id="f71ce-119">Check the status of the redeploy operation in the **Notifications** window.</span></span>

    ![Redeploy status](media/devtest-lab-redeploy-vm/redeploy-status.png)

## <a name="next-steps"></a><span data-ttu-id="f71ce-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="f71ce-121">Next steps</span></span>
<span data-ttu-id="f71ce-122">Learn how to resize a VM in Azure DevTest Labs, see [Resize a VM](devtest-lab-resize-vm.md).</span><span class="sxs-lookup"><span data-stu-id="f71ce-122">Learn how to resize a VM in Azure DevTest Labs, see [Resize a VM](devtest-lab-resize-vm.md).</span></span>


