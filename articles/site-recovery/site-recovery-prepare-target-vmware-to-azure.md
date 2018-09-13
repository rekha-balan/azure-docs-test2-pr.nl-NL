---
title: Prepare target (VMware to Azure) | Microsoft Docs
description: This article describes how to prepare your Azure environment to start replicating VMware virtual machines to Azure.
services: site-recovery
documentationcenter: ''
author: bsiva
manager: abhemraj
editor: ''
ms.assetid: ''
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 2/11/2017
ms.author: bsiva
ms.openlocfilehash: ef6007ddbe4946d028dc1a3de312ed9ce8241a99
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662946"
---
# <a name="prepare-target-vmware-to-azure"></a><span data-ttu-id="04ad8-103">Prepare target (VMware to Azure)</span><span class="sxs-lookup"><span data-stu-id="04ad8-103">Prepare target (VMware to Azure)</span></span>
> [!div class="op_single_selector"]
> * [VMware Virtual Machines](./site-recovery-prepare-target-vmware-to-azure.md)
> * [Physical Servers](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="04ad8-106">This article describes how to prepare your Azure environment to start replicating VMware virtual machines to Azure.</span><span class="sxs-lookup"><span data-stu-id="04ad8-106">This article describes how to prepare your Azure environment to start replicating VMware virtual machines to Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04ad8-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="04ad8-107">Prerequisites</span></span>

<span data-ttu-id="04ad8-108">The article assumes the following:</span><span class="sxs-lookup"><span data-stu-id="04ad8-108">The article assumes the following:</span></span>
- <span data-ttu-id="04ad8-109">You have created a Recovery Services Vault to protect your VMware virtual machines.</span><span class="sxs-lookup"><span data-stu-id="04ad8-109">You have created a Recovery Services Vault to protect your VMware virtual machines.</span></span> <span data-ttu-id="04ad8-110">You can create a Recovery Services Vault from the [Azure portal](http://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="04ad8-110">You can create a Recovery Services Vault from the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="04ad8-111">You have [setup your on-premises environment](./site-recovery-set-up-vmware-to-azure.md) to replicate VMware virtual machines to Azure.</span><span class="sxs-lookup"><span data-stu-id="04ad8-111">You have [setup your on-premises environment](./site-recovery-set-up-vmware-to-azure.md) to replicate VMware virtual machines to Azure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="04ad8-112">Prepare target</span><span class="sxs-lookup"><span data-stu-id="04ad8-112">Prepare target</span></span>

<span data-ttu-id="04ad8-113">After completing the **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken to **Step 3: Target**</span><span class="sxs-lookup"><span data-stu-id="04ad8-113">After completing the **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken to **Step 3: Target**</span></span>

![Prepare target](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-prepare-target-vmware-to-azure/prepare-target-vmware-to-azure.PNG)

1. <span data-ttu-id="04ad8-115">**Subscription:** From the drop down menu, select the Subscription that you want to replicate your virtual machines to.</span><span class="sxs-lookup"><span data-stu-id="04ad8-115">**Subscription:** From the drop down menu, select the Subscription that you want to replicate your virtual machines to.</span></span>
2. <span data-ttu-id="04ad8-116">**Deployment Model:** Select the deployment model (Classic or Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="04ad8-116">**Deployment Model:** Select the deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="04ad8-117">Based on the chosen deployment model, a validation is run to ensure that you have at least one compatible storage account and virtual network in the target subscription to replicate and failover your virtual machine to.</span><span class="sxs-lookup"><span data-stu-id="04ad8-117">Based on the chosen deployment model, a validation is run to ensure that you have at least one compatible storage account and virtual network in the target subscription to replicate and failover your virtual machine to.</span></span>

<span data-ttu-id="04ad8-118">Once the validations complete successfully, click OK to go to the next step.</span><span class="sxs-lookup"><span data-stu-id="04ad8-118">Once the validations complete successfully, click OK to go to the next step.</span></span>

<span data-ttu-id="04ad8-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like to add more, you can do so by clicking the **+ Storage Account** or **+ Network** buttons on the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="04ad8-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like to add more, you can do so by clicking the **+ Storage Account** or **+ Network** buttons on the top of the blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04ad8-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="04ad8-120">Next steps</span></span>
<span data-ttu-id="04ad8-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="04ad8-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>

