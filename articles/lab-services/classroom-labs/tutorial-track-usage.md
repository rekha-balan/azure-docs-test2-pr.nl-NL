---
title: Track usage of a lab in Azure Lab Services | Microsoft Docs
description: In this tutorial, you, as a lab creator/owner, track the usage of your lab.
services: lab-services
documentationcenter: na
author: spelluru
manager: ''
editor: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.custom: mvc
ms.date: 07/23/2018
ms.author: spelluru
ms.openlocfilehash: 710d157dcf4c6d060e59bcfbb69455e2ddc91bdd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857271"
---
# <a name="tutorial-track-usage-of-a-lab-in-azure-lab-service"></a><span data-ttu-id="1c80e-103">Tutorial: Track usage of a lab in Azure Lab Service</span><span class="sxs-lookup"><span data-stu-id="1c80e-103">Tutorial: Track usage of a lab in Azure Lab Service</span></span>
<span data-ttu-id="1c80e-104">This tutorial shows you how a lab creator/owner can track usage of a lab.</span><span class="sxs-lookup"><span data-stu-id="1c80e-104">This tutorial shows you how a lab creator/owner can track usage of a lab.</span></span>

<span data-ttu-id="1c80e-105">In this tutorial, you do the following actions:</span><span class="sxs-lookup"><span data-stu-id="1c80e-105">In this tutorial, you do the following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1c80e-106">View users registered with your lab</span><span class="sxs-lookup"><span data-stu-id="1c80e-106">View users registered with your lab</span></span>
> * <span data-ttu-id="1c80e-107">View the usage of VMs in the lab</span><span class="sxs-lookup"><span data-stu-id="1c80e-107">View the usage of VMs in the lab</span></span>
> * <span data-ttu-id="1c80e-108">Manage student VMs</span><span class="sxs-lookup"><span data-stu-id="1c80e-108">Manage student VMs</span></span> 


## <a name="view-users-registered-with-the-lab"></a><span data-ttu-id="1c80e-109">View users registered with the lab</span><span class="sxs-lookup"><span data-stu-id="1c80e-109">View users registered with the lab</span></span>

1. <span data-ttu-id="1c80e-110">Navigate to [Azure Lab Services website](https://labs.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1c80e-110">Navigate to [Azure Lab Services website](https://labs.azure.com).</span></span> 
2. <span data-ttu-id="1c80e-111">Select **Sign in** and enter your credentials.</span><span class="sxs-lookup"><span data-stu-id="1c80e-111">Select **Sign in** and enter your credentials.</span></span> <span data-ttu-id="1c80e-112">Azure Lab Services supports organizational accounts and Microsoft accounts.</span><span class="sxs-lookup"><span data-stu-id="1c80e-112">Azure Lab Services supports organizational accounts and Microsoft accounts.</span></span>
3. <span data-ttu-id="1c80e-113">On the **My labs** page, select the lab for which you want to track the usage.</span><span class="sxs-lookup"><span data-stu-id="1c80e-113">On the **My labs** page, select the lab for which you want to track the usage.</span></span> 
4. <span data-ttu-id="1c80e-114">Select **Users** tab. You see students who have registered with your lab.</span><span class="sxs-lookup"><span data-stu-id="1c80e-114">Select **Users** tab. You see students who have registered with your lab.</span></span> <span data-ttu-id="1c80e-115">Select **Registration link**, copy the link, and send it any new student who hasn't registered with your lab yet.</span><span class="sxs-lookup"><span data-stu-id="1c80e-115">Select **Registration link**, copy the link, and send it any new student who hasn't registered with your lab yet.</span></span> 

    ![Registered users](../media/tutorial-track-usage/registered-users.png)

## <a name="view-the-usage-of-vms-in-the-lab"></a><span data-ttu-id="1c80e-117">View the usage of VMs in the lab</span><span class="sxs-lookup"><span data-stu-id="1c80e-117">View the usage of VMs in the lab</span></span> 

1. <span data-ttu-id="1c80e-118">Select **Virtual machines** on menu to the left.</span><span class="sxs-lookup"><span data-stu-id="1c80e-118">Select **Virtual machines** on menu to the left.</span></span> 
2. <span data-ttu-id="1c80e-119">Confirm that you see the status of VMs and the number of hours the VMs have been running.</span><span class="sxs-lookup"><span data-stu-id="1c80e-119">Confirm that you see the status of VMs and the number of hours the VMs have been running.</span></span> <span data-ttu-id="1c80e-120">The time you spend on a student VM is not counted against the usage time shown in the last column.</span><span class="sxs-lookup"><span data-stu-id="1c80e-120">The time you spend on a student VM is not counted against the usage time shown in the last column.</span></span> 

    ![VM usage](../media/tutorial-track-usage/vm-usage.png)

## <a name="manage-student-vms"></a><span data-ttu-id="1c80e-122">Manage student VMs</span><span class="sxs-lookup"><span data-stu-id="1c80e-122">Manage student VMs</span></span> 
<span data-ttu-id="1c80e-123">As you hover the mouse over a row in the list of virtual machine, you see controls to do the following tasks:</span><span class="sxs-lookup"><span data-stu-id="1c80e-123">As you hover the mouse over a row in the list of virtual machine, you see controls to do the following tasks:</span></span> 

- <span data-ttu-id="1c80e-124">Connect to a VM</span><span class="sxs-lookup"><span data-stu-id="1c80e-124">Connect to a VM</span></span>
- <span data-ttu-id="1c80e-125">Start a VM</span><span class="sxs-lookup"><span data-stu-id="1c80e-125">Start a VM</span></span>
- <span data-ttu-id="1c80e-126">Stop a VM</span><span class="sxs-lookup"><span data-stu-id="1c80e-126">Stop a VM</span></span>
- <span data-ttu-id="1c80e-127">Delete a VM</span><span class="sxs-lookup"><span data-stu-id="1c80e-127">Delete a VM</span></span>

![VM controls](../media/tutorial-track-usage/vm-controls.png) 



## <a name="next-steps"></a><span data-ttu-id="1c80e-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="1c80e-129">Next steps</span></span>
<span data-ttu-id="1c80e-130">In this tutorial, you learned how to find users who have registered with the lab, track usage of VMs in the lab, and manage VMs in the lab.</span><span class="sxs-lookup"><span data-stu-id="1c80e-130">In this tutorial, you learned how to find users who have registered with the lab, track usage of VMs in the lab, and manage VMs in the lab.</span></span>

<span data-ttu-id="1c80e-131">To learn more about classroom labs, see topics under [How-to guides](how-to-manage-lab-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="1c80e-131">To learn more about classroom labs, see topics under [How-to guides](how-to-manage-lab-accounts.md).</span></span>
