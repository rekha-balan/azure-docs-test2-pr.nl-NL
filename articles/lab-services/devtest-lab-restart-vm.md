---
title: Restart a VM in a lab in Azure DevTest Labs | Microsoft Docs
description: Learn how to restart a virtual machine in Azure DevTest Labs
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
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: 24a17ce09bee1097b0418ad4e20990d359b3e084
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867776"
---
# <a name="restart-a-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="f3cb8-103">Restart a VM in a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="f3cb8-103">Restart a VM in a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="f3cb8-104">You can quickly and easily restart a virtual machine in  DevTest Labs by following the steps in this article.</span><span class="sxs-lookup"><span data-stu-id="f3cb8-104">You can quickly and easily restart a virtual machine in  DevTest Labs by following the steps in this article.</span></span> <span data-ttu-id="f3cb8-105">Consider the following before restarting a VM:</span><span class="sxs-lookup"><span data-stu-id="f3cb8-105">Consider the following before restarting a VM:</span></span>

- <span data-ttu-id="f3cb8-106">The VM must be running for the restart feature to be enabled.</span><span class="sxs-lookup"><span data-stu-id="f3cb8-106">The VM must be running for the restart feature to be enabled.</span></span>
- <span data-ttu-id="f3cb8-107">If a user is connected to a running VM when they perform a restart, they must reconnect to the VM after it starts back up.</span><span class="sxs-lookup"><span data-stu-id="f3cb8-107">If a user is connected to a running VM when they perform a restart, they must reconnect to the VM after it starts back up.</span></span>
- <span data-ttu-id="f3cb8-108">If an artifact is being applied when you restart the VM, you receive a warning that the artifact might not be applied.</span><span class="sxs-lookup"><span data-stu-id="f3cb8-108">If an artifact is being applied when you restart the VM, you receive a warning that the artifact might not be applied.</span></span> 

    ![Warning when restarting while applying artifacts](./media/devtest-lab-restart-vm/devtest-lab-restart-vm-apply-artifacts.png)


   > [!NOTE]
   > <span data-ttu-id="f3cb8-110">If the VM has stalled while applying an artifact, you can use the restart VM feature as a potential way to resolve the issue.</span><span class="sxs-lookup"><span data-stu-id="f3cb8-110">If the VM has stalled while applying an artifact, you can use the restart VM feature as a potential way to resolve the issue.</span></span>
   >
   >

## <a name="steps-to-restart-a-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="f3cb8-111">Steps to restart a VM in a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="f3cb8-111">Steps to restart a VM in a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="f3cb8-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f3cb8-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="f3cb8-113">Select **All Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="f3cb8-113">Select **All Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="f3cb8-114">From the list of labs, select the lab that includes the VM  you want to restart.</span><span class="sxs-lookup"><span data-stu-id="f3cb8-114">From the list of labs, select the lab that includes the VM  you want to restart.</span></span>  
1. <span data-ttu-id="f3cb8-115">In the left panel, select **My Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="f3cb8-115">In the left panel, select **My Virtual Machines**.</span></span> 
1. <span data-ttu-id="f3cb8-116">From the list of VMs, select a running VM.</span><span class="sxs-lookup"><span data-stu-id="f3cb8-116">From the list of VMs, select a running VM.</span></span>
1. <span data-ttu-id="f3cb8-117">At the top of the VM management pane, select **Restart**.</span><span class="sxs-lookup"><span data-stu-id="f3cb8-117">At the top of the VM management pane, select **Restart**.</span></span>  

    ![Restart VM button](./media/devtest-lab-restart-vm/devtest-lab-restart-vm.png)

1. <span data-ttu-id="f3cb8-119">Monitor the status of the restart by selecting the **Notifications** icon at the top right of the window.</span><span class="sxs-lookup"><span data-stu-id="f3cb8-119">Monitor the status of the restart by selecting the **Notifications** icon at the top right of the window.</span></span>

    ![Viewing the status of the VM restart](./media/devtest-lab-restart-vm/devtest-lab-restart-notification.png)

<span data-ttu-id="f3cb8-121">You can also restart a running VM by selecting its ellipsis (...) in the list of **My Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="f3cb8-121">You can also restart a running VM by selecting its ellipsis (...) in the list of **My Virtual Machines**.</span></span>

![Restart VM through ellipses](./media/devtest-lab-restart-vm/devtest-lab-restart-elipses.png)

## <a name="next-steps"></a><span data-ttu-id="f3cb8-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="f3cb8-123">Next steps</span></span>
* <span data-ttu-id="f3cb8-124">Once it is restarted, you can reconnect to the VM by selecting **Connect** on the its management pane.</span><span class="sxs-lookup"><span data-stu-id="f3cb8-124">Once it is restarted, you can reconnect to the VM by selecting **Connect** on the its management pane.</span></span>
* <span data-ttu-id="f3cb8-125">Explore the [DevTest Labs Azure Resource Manager quickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples)</span><span class="sxs-lookup"><span data-stu-id="f3cb8-125">Explore the [DevTest Labs Azure Resource Manager quickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples)</span></span>
