---
title: Provision a VM in Azure Stack | Microsoft Docs
description: Learn how to provision a VM in Azure Stack.
services: azure-stack
documentationcenter: ''
author: ErikjeMS
manager: byronr
editor: ''
ms.assetid: c86646e1-a12e-493f-b396-f17bfacd60c2
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 3/1/2017
ms.author: erikje
ms.openlocfilehash: 4a0728604e923afdd42bc1ca537d183e21ce4bd0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670968"
---
# <a name="provision-a-virtual-machine"></a><span data-ttu-id="19359-103">Provision a virtual machine</span><span class="sxs-lookup"><span data-stu-id="19359-103">Provision a virtual machine</span></span>
<span data-ttu-id="19359-104">As an administrator, you can create virtual machines to evaluate resources before offering them in plans.</span><span class="sxs-lookup"><span data-stu-id="19359-104">As an administrator, you can create virtual machines to evaluate resources before offering them in plans.</span></span>

> [!NOTE]
> <span data-ttu-id="19359-105">Before you can provision virtual machines, you must [add the Windows Server 2016 Eval image to the Azure Stack marketplace](azure-stack-add-default-image.md).</span><span class="sxs-lookup"><span data-stu-id="19359-105">Before you can provision virtual machines, you must [add the Windows Server 2016 Eval image to the Azure Stack marketplace](azure-stack-add-default-image.md).</span></span>
> 
> 

## <a name="provision-a-virtual-machine"></a><span data-ttu-id="19359-106">Provision a virtual machine</span><span class="sxs-lookup"><span data-stu-id="19359-106">Provision a virtual machine</span></span>
1. <span data-ttu-id="19359-107">On the Azure Stack POC computer, log in to `https://portal.local.azurestack.external` as [an admin](azure-stack-connect-azure-stack.md), and then click **New** > **Virtual machines** > **Windows Server 2016 Datacenter Eval**.</span><span class="sxs-lookup"><span data-stu-id="19359-107">On the Azure Stack POC computer, log in to `https://portal.local.azurestack.external` as [an admin](azure-stack-connect-azure-stack.md), and then click **New** > **Virtual machines** > **Windows Server 2016 Datacenter Eval**.</span></span>  

2. <span data-ttu-id="19359-108">In the **Basics** blade, type a **Name**, **User name**, and **Password**.</span><span class="sxs-lookup"><span data-stu-id="19359-108">In the **Basics** blade, type a **Name**, **User name**, and **Password**.</span></span> <span data-ttu-id="19359-109">For **VM disk type**, choose **HDD**.</span><span class="sxs-lookup"><span data-stu-id="19359-109">For **VM disk type**, choose **HDD**.</span></span> <span data-ttu-id="19359-110">Choose a **Subscription**.</span><span class="sxs-lookup"><span data-stu-id="19359-110">Choose a **Subscription**.</span></span> <span data-ttu-id="19359-111">Create a **Resource group**, or select an existing one, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="19359-111">Create a **Resource group**, or select an existing one, and then click **OK**.</span></span>  
3. <span data-ttu-id="19359-112">In the **Choose a size** blade, click **A1 Basic**, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="19359-112">In the **Choose a size** blade, click **A1 Basic**, and then click **Select**.</span></span>  
4. <span data-ttu-id="19359-113">In the **Settings** blade, click **Virtual network**.</span><span class="sxs-lookup"><span data-stu-id="19359-113">In the **Settings** blade, click **Virtual network**.</span></span> <span data-ttu-id="19359-114">In the **Choose virtual network** blade, click **Create new**.</span><span class="sxs-lookup"><span data-stu-id="19359-114">In the **Choose virtual network** blade, click **Create new**.</span></span> <span data-ttu-id="19359-115">In the **Create virtual network** blade, accept all the defaults, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="19359-115">In the **Create virtual network** blade, accept all the defaults, and click **OK**.</span></span> <span data-ttu-id="19359-116">In the **Settings** blade, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="19359-116">In the **Settings** blade, click **OK**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-provision-vm/image04.png)
5. <span data-ttu-id="19359-117">In the **Summary** blade, click **OK** to create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="19359-117">In the **Summary** blade, click **OK** to create the virtual machine.</span></span>  
6. <span data-ttu-id="19359-118">To see your new virtual machine, click **All resources**, then search for the virtual machine and click its name.</span><span class="sxs-lookup"><span data-stu-id="19359-118">To see your new virtual machine, click **All resources**, then search for the virtual machine and click its name.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-provision-vm/image06.png)

## <a name="next-steps"></a><span data-ttu-id="19359-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="19359-119">Next steps</span></span>
[<span data-ttu-id="19359-120">Storage accounts</span><span class="sxs-lookup"><span data-stu-id="19359-120">Storage accounts</span></span>](azure-stack-provision-storage-account.md)


