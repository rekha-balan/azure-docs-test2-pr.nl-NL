---
title: Redeploy Azure Stack | Microsoft Docs
description: Redeploy Azure Stack.
services: azure-stack
documentationcenter: ''
author: ErikjeMS
manager: byronr
editor: ''
ms.assetid: 795af5ea-892d-40b1-a080-42e4472e4bba
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/1/2017
ms.author: erikje
ms.openlocfilehash: eaa2897e797f5f54dc1ea32ebacd1d42b82acc0c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556112"
---
# <a name="redeploy-azure-stack"></a><span data-ttu-id="09381-103">Redeploy Azure Stack</span><span class="sxs-lookup"><span data-stu-id="09381-103">Redeploy Azure Stack</span></span>
<span data-ttu-id="09381-104">To redeploy Azure Stack, you must start over from scratch as described below.</span><span class="sxs-lookup"><span data-stu-id="09381-104">To redeploy Azure Stack, you must start over from scratch as described below.</span></span>

## <a name="steps-to-redeploy-azure-stack"></a><span data-ttu-id="09381-105">Steps to redeploy Azure Stack</span><span class="sxs-lookup"><span data-stu-id="09381-105">Steps to redeploy Azure Stack</span></span>
1. <span data-ttu-id="09381-106">Reboot the host into the original operating system (installed to bare metal).</span><span class="sxs-lookup"><span data-stu-id="09381-106">Reboot the host into the original operating system (installed to bare metal).</span></span> <span data-ttu-id="09381-107">This is not the default setting in the boot menu, so you must use KVM or local console to select it during the reboot (during setup, you named the “Boot from VHD” OS to “AzureStack”, this will help identify which OS is which).</span><span class="sxs-lookup"><span data-stu-id="09381-107">This is not the default setting in the boot menu, so you must use KVM or local console to select it during the reboot (during setup, you named the “Boot from VHD” OS to “AzureStack”, this will help identify which OS is which).</span></span>
   
    <span data-ttu-id="09381-108">You don't need to remove the existing boot entry (the new support script “PrepareBootFromVHD.ps1” takes care of that for you.)</span><span class="sxs-lookup"><span data-stu-id="09381-108">You don't need to remove the existing boot entry (the new support script “PrepareBootFromVHD.ps1” takes care of that for you.)</span></span>
2. <span data-ttu-id="09381-109">If you do not have KVM, or would like to choose the Boot OS before rebooting:</span><span class="sxs-lookup"><span data-stu-id="09381-109">If you do not have KVM, or would like to choose the Boot OS before rebooting:</span></span>
   
   1. <span data-ttu-id="09381-110">Locate the script .\BootMenuNoKVM.ps1.</span><span class="sxs-lookup"><span data-stu-id="09381-110">Locate the script .\BootMenuNoKVM.ps1.</span></span> <span data-ttu-id="09381-111">This file is available with the other support scripts provided along with this build.</span><span class="sxs-lookup"><span data-stu-id="09381-111">This file is available with the other support scripts provided along with this build.</span></span>
   2. <span data-ttu-id="09381-112">Run the script with elevated privileges.</span><span class="sxs-lookup"><span data-stu-id="09381-112">Run the script with elevated privileges.</span></span> <span data-ttu-id="09381-113">Select the name of Original Host OS.</span><span class="sxs-lookup"><span data-stu-id="09381-113">Select the name of Original Host OS.</span></span> <span data-ttu-id="09381-114">This will boot the host into the original host OS without requiring KVM access.</span><span class="sxs-lookup"><span data-stu-id="09381-114">This will boot the host into the original host OS without requiring KVM access.</span></span>
   3. <span data-ttu-id="09381-115">When the script is complete you will be asked to confirm the reboot.</span><span class="sxs-lookup"><span data-stu-id="09381-115">When the script is complete you will be asked to confirm the reboot.</span></span>
   4. <span data-ttu-id="09381-116">If there are other users logged in, this command will fail.</span><span class="sxs-lookup"><span data-stu-id="09381-116">If there are other users logged in, this command will fail.</span></span>
   5. <span data-ttu-id="09381-117">Please just run the following command: Restart-Computer -force</span><span class="sxs-lookup"><span data-stu-id="09381-117">Please just run the following command: Restart-Computer -force</span></span> 
3. <span data-ttu-id="09381-118">Delete the CloudBuilder.vhdx file that was used as part of the previous deployment.</span><span class="sxs-lookup"><span data-stu-id="09381-118">Delete the CloudBuilder.vhdx file that was used as part of the previous deployment.</span></span>
   
    <span data-ttu-id="09381-119">You don't need to delete the existing Storage Pool from the previous deployment.</span><span class="sxs-lookup"><span data-stu-id="09381-119">You don't need to delete the existing Storage Pool from the previous deployment.</span></span> <span data-ttu-id="09381-120">The deployment script detects and cleans up the existing, then creates new.</span><span class="sxs-lookup"><span data-stu-id="09381-120">The deployment script detects and cleans up the existing, then creates new.</span></span>
4. <span data-ttu-id="09381-121">Redeploy from copying a new copy of the CloudBuilder.vhdx, boot to it, etc.</span><span class="sxs-lookup"><span data-stu-id="09381-121">Redeploy from copying a new copy of the CloudBuilder.vhdx, boot to it, etc.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09381-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="09381-122">Next steps</span></span>
[<span data-ttu-id="09381-123">Connect to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="09381-123">Connect to Azure Stack</span></span>](azure-stack-connect-azure-stack.md)

