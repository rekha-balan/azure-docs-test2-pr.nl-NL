---
title: Prepare target (Physical to Azure) | Microsoft Docs
description: This article describes how to prepare your Azure environment to start replicating physical servers running Windows or Linux to Azure.
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
ms.openlocfilehash: 6c9e8f349a7769e7b757fa236b6582f36a938053
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563713"
---
# <a name="prepare-target-vmware-to-azure"></a><span data-ttu-id="21c1d-103">Prepare target (VMware to Azure)</span><span class="sxs-lookup"><span data-stu-id="21c1d-103">Prepare target (VMware to Azure)</span></span>
> [!div class="op_single_selector"]
> * [VMware Virtual Machines](./site-recovery-prepare-target-vmware-to-azure.md)
> * [Physical Servers](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="21c1d-106">This article describes how to prepare your Azure environment to start replicating physical servers (x64) running Windows or Linux into Azure.</span><span class="sxs-lookup"><span data-stu-id="21c1d-106">This article describes how to prepare your Azure environment to start replicating physical servers (x64) running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21c1d-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="21c1d-107">Prerequisites</span></span>

<span data-ttu-id="21c1d-108">The article assumes the following:</span><span class="sxs-lookup"><span data-stu-id="21c1d-108">The article assumes the following:</span></span>
- <span data-ttu-id="21c1d-109">You have created a Recovery Services Vault to protect your physical servers.</span><span class="sxs-lookup"><span data-stu-id="21c1d-109">You have created a Recovery Services Vault to protect your physical servers.</span></span> <span data-ttu-id="21c1d-110">You can create a Recovery Services Vault from the [Azure portal](http://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="21c1d-110">You can create a Recovery Services Vault from the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="21c1d-111">You have [setup your on-premises environment](./site-recovery-set-up-physical-to-azure.md) to replicate physical servers to Azure.</span><span class="sxs-lookup"><span data-stu-id="21c1d-111">You have [setup your on-premises environment](./site-recovery-set-up-physical-to-azure.md) to replicate physical servers to Azure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="21c1d-112">Prepare target</span><span class="sxs-lookup"><span data-stu-id="21c1d-112">Prepare target</span></span>

<span data-ttu-id="21c1d-113">After completing the **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken to **Step 3: Target**</span><span class="sxs-lookup"><span data-stu-id="21c1d-113">After completing the **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken to **Step 3: Target**</span></span>

![Prepare target](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-prepare-target-physical-to-azure/prepare-target-physical-to-azure.PNG)

1. <span data-ttu-id="21c1d-115">**Subscription:** From the drop down menu, select the Subscription that you want to replicate your physical servers to.</span><span class="sxs-lookup"><span data-stu-id="21c1d-115">**Subscription:** From the drop down menu, select the Subscription that you want to replicate your physical servers to.</span></span>
2. <span data-ttu-id="21c1d-116">**Deployment Model:** Select the deployment model (Classic or Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="21c1d-116">**Deployment Model:** Select the deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="21c1d-117">Based on the chosen deployment model, a validation is run to ensure that you have at least one compatible storage account and virtual network in the target subscription to replicate and failover your physical servers to.</span><span class="sxs-lookup"><span data-stu-id="21c1d-117">Based on the chosen deployment model, a validation is run to ensure that you have at least one compatible storage account and virtual network in the target subscription to replicate and failover your physical servers to.</span></span>

<span data-ttu-id="21c1d-118">Once the validations complete successfully, click OK to go to the next step.</span><span class="sxs-lookup"><span data-stu-id="21c1d-118">Once the validations complete successfully, click OK to go to the next step.</span></span>

<span data-ttu-id="21c1d-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like to add more, you can do so by clicking the **+ Storage Account** or **+ Network** buttons on the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="21c1d-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like to add more, you can do so by clicking the **+ Storage Account** or **+ Network** buttons on the top of the blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21c1d-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="21c1d-120">Next steps</span></span>
<span data-ttu-id="21c1d-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="21c1d-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>

