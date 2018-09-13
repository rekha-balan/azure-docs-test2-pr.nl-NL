---
title: Resize a VM in a lab in Azure DevTest Labs | Microsoft Docs
description: Learn how to resize a virtual machine in Azure DevTest Labs
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
ms.openlocfilehash: 9b9a1839bf4b028aec13b764b4de66385de4189e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968975"
---
# <a name="resize-a-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="6a525-103">Resize a VM in a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="6a525-103">Resize a VM in a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="6a525-104">One of the important features of Azure virtual machines is that it lets you change the size of a virtual machine (VM) based on your needs for CPU, network, or disk performance.</span><span class="sxs-lookup"><span data-stu-id="6a525-104">One of the important features of Azure virtual machines is that it lets you change the size of a virtual machine (VM) based on your needs for CPU, network, or disk performance.</span></span> <span data-ttu-id="6a525-105">Azure DevTest Labs supports this feature for VMs in a lab now.</span><span class="sxs-lookup"><span data-stu-id="6a525-105">Azure DevTest Labs supports this feature for VMs in a lab now.</span></span> <span data-ttu-id="6a525-106">The resize feature adheres to the lab policy for allowed VM sizes in the lab.</span><span class="sxs-lookup"><span data-stu-id="6a525-106">The resize feature adheres to the lab policy for allowed VM sizes in the lab.</span></span> <span data-ttu-id="6a525-107">That is, you can change the size of a VM to only allowed sizes in the lab.</span><span class="sxs-lookup"><span data-stu-id="6a525-107">That is, you can change the size of a VM to only allowed sizes in the lab.</span></span> 


## <a name="steps-to-resize-a-vm-in-a-lab"></a><span data-ttu-id="6a525-108">Steps to resize a VM in a lab</span><span class="sxs-lookup"><span data-stu-id="6a525-108">Steps to resize a VM in a lab</span></span> 
<span data-ttu-id="6a525-109">To resize a VM in a lab in Azure DevTest Labs, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="6a525-109">To resize a VM in a lab in Azure DevTest Labs, take the following steps:</span></span> 

> [!NOTE]
> <span data-ttu-id="6a525-110">If you are connected to the VM via a remote desktop session (RDP), save your work, and disconnect from the VM before resizing it.</span><span class="sxs-lookup"><span data-stu-id="6a525-110">If you are connected to the VM via a remote desktop session (RDP), save your work, and disconnect from the VM before resizing it.</span></span>

1. <span data-ttu-id="6a525-111">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6a525-111">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6a525-112">Select **All Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="6a525-112">Select **All Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="6a525-113">From the list of labs, select the lab that includes the VM  you want to resize.</span><span class="sxs-lookup"><span data-stu-id="6a525-113">From the list of labs, select the lab that includes the VM  you want to resize.</span></span>  
4. <span data-ttu-id="6a525-114">In the left panel, select **My Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="6a525-114">In the left panel, select **My Virtual Machines**.</span></span> 
5. <span data-ttu-id="6a525-115">From the list of VMs, select a VM.</span><span class="sxs-lookup"><span data-stu-id="6a525-115">From the list of VMs, select a VM.</span></span>
6. <span data-ttu-id="6a525-116">Select **Stop** on the toolbar if the VM is running.</span><span class="sxs-lookup"><span data-stu-id="6a525-116">Select **Stop** on the toolbar if the VM is running.</span></span> <span data-ttu-id="6a525-117">Check the status of the operation in the **Notifications** window.</span><span class="sxs-lookup"><span data-stu-id="6a525-117">Check the status of the operation in the **Notifications** window.</span></span> <span data-ttu-id="6a525-118">Wait until the VM is stopped and then close the **Notifications** window.</span><span class="sxs-lookup"><span data-stu-id="6a525-118">Wait until the VM is stopped and then close the **Notifications** window.</span></span> 

    ![Stop the VM](media/devtest-lab-resize-vm/stop-vm.png)
1. <span data-ttu-id="6a525-120">In the Virtual Machine page for your VM, select **Size** under **SETTINGS** in the left menu.</span><span class="sxs-lookup"><span data-stu-id="6a525-120">In the Virtual Machine page for your VM, select **Size** under **SETTINGS** in the left menu.</span></span>

    ![Size menu](media/devtest-lab-resize-vm/size-menu.png)
1. <span data-ttu-id="6a525-122">In the **Choose a size** window, browse and select a size for your VM, and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="6a525-122">In the **Choose a size** window, browse and select a size for your VM, and click **Select**.</span></span>     
1. <span data-ttu-id="6a525-123">Check the status of the resize operation in the **Notifications** window.</span><span class="sxs-lookup"><span data-stu-id="6a525-123">Check the status of the resize operation in the **Notifications** window.</span></span>

    ![Resize status](media/devtest-lab-resize-vm/resize-status.png)
10. <span data-ttu-id="6a525-125">After the resize operation succeeds, close the **Notifications** window.</span><span class="sxs-lookup"><span data-stu-id="6a525-125">After the resize operation succeeds, close the **Notifications** window.</span></span> 
11. <span data-ttu-id="6a525-126">Select **Overview** in the left menu, and select **Restart** on the toolbar to restart the VM.</span><span class="sxs-lookup"><span data-stu-id="6a525-126">Select **Overview** in the left menu, and select **Restart** on the toolbar to restart the VM.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6a525-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="6a525-127">Next steps</span></span>
<span data-ttu-id="6a525-128">For detailed information about the resize feature supported by Azure virtual machines, see [Resize virtual machines](https://azure.microsoft.com/blog/resize-virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="6a525-128">For detailed information about the resize feature supported by Azure virtual machines, see [Resize virtual machines](https://azure.microsoft.com/blog/resize-virtual-machines/).</span></span>


