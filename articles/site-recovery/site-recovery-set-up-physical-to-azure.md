---
title: Set up the source environment (physical servers to Azure) | Microsoft Docs
description: This article describes how to set up your on-premises environment to start replicating physical servers running Windows or Linux into Azure.
services: site-recovery
documentationcenter: ''
author: AnoopVasudavan
manager: gauravd
editor: ''
ms.assetid: ''
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 1/10/2017
ms.author: anoopkv
ms.openlocfilehash: b53fe95150f6485398667a23eeeaa1985cafda56
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554633"
---
# <a name="set-up-the-source-environment-physical-server-to-azure"></a><span data-ttu-id="bced9-103">Set up the source environment (physical server to Azure)</span><span class="sxs-lookup"><span data-stu-id="bced9-103">Set up the source environment (physical server to Azure)</span></span>
> [!div class="op_single_selector"]
> * [VMware Virtual Machines](./site-recovery-set-up-vmware-to-azure.md)
> * [Physical Servers](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="bced9-106">This article describes how to set up your on-premises environment to start replicating physical servers running Windows or Linux into Azure.</span><span class="sxs-lookup"><span data-stu-id="bced9-106">This article describes how to set up your on-premises environment to start replicating physical servers running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bced9-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bced9-107">Prerequisites</span></span>

<span data-ttu-id="bced9-108">The article assumes that you already have:</span><span class="sxs-lookup"><span data-stu-id="bced9-108">The article assumes that you already have:</span></span>
1. <span data-ttu-id="bced9-109">A Recovery Services vault in the [Azure portal](http://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="bced9-109">A Recovery Services vault in the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
3. <span data-ttu-id="bced9-110">A physical computer on which to install the configuration server.</span><span class="sxs-lookup"><span data-stu-id="bced9-110">A physical computer on which to install the configuration server.</span></span>

### <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="bced9-111">Configuration server minimum requirements</span><span class="sxs-lookup"><span data-stu-id="bced9-111">Configuration server minimum requirements</span></span>
<span data-ttu-id="bced9-112">The following table lists the minimum hardware, software, and network requirements for a configuration server.</span><span class="sxs-lookup"><span data-stu-id="bced9-112">The following table lists the minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> HTTPS-based proxy servers are not supported by the configuration server.

## <a name="choose-your-protection-goals"></a><span data-ttu-id="bced9-114">Choose your protection goals</span><span class="sxs-lookup"><span data-stu-id="bced9-114">Choose your protection goals</span></span>

1. <span data-ttu-id="bced9-115">In the Azure portal, go to the **Recovery Services** vaults blade and select your vault.</span><span class="sxs-lookup"><span data-stu-id="bced9-115">In the Azure portal, go to the **Recovery Services** vaults blade and select your vault.</span></span>
2. <span data-ttu-id="bced9-116">In the **Resource** menu of the vault, click **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span><span class="sxs-lookup"><span data-stu-id="bced9-116">In the **Resource** menu of the vault, click **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Choose goals](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. <span data-ttu-id="bced9-118">In **Protection goal**, select **To Azure** and **Not virtualized/Other**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="bced9-118">In **Protection goal**, select **To Azure** and **Not virtualized/Other**, and then click **OK**.</span></span>

    ![Choose goals](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-the-source-environment"></a><span data-ttu-id="bced9-120">Set up the source environment</span><span class="sxs-lookup"><span data-stu-id="bced9-120">Set up the source environment</span></span>

1. <span data-ttu-id="bced9-121">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** to add one.</span><span class="sxs-lookup"><span data-stu-id="bced9-121">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** to add one.</span></span>

  ![Set up source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. <span data-ttu-id="bced9-123">In the **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span><span class="sxs-lookup"><span data-stu-id="bced9-123">In the **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="bced9-124">Download the Site Recovery Unified Setup installation file.</span><span class="sxs-lookup"><span data-stu-id="bced9-124">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="bced9-125">Download the vault registration key.</span><span class="sxs-lookup"><span data-stu-id="bced9-125">Download the vault registration key.</span></span> <span data-ttu-id="bced9-126">You need the registration key when you run Unified Setup.</span><span class="sxs-lookup"><span data-stu-id="bced9-126">You need the registration key when you run Unified Setup.</span></span> <span data-ttu-id="bced9-127">The key is valid for five days after you generate it.</span><span class="sxs-lookup"><span data-stu-id="bced9-127">The key is valid for five days after you generate it.</span></span>

    ![Set up source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. <span data-ttu-id="bced9-129">On the machine you’re using as the configuration server, run **Azure Site Recovery Unified Setup** to install the configuration server, the process server, and the master target server.</span><span class="sxs-lookup"><span data-stu-id="bced9-129">On the machine you’re using as the configuration server, run **Azure Site Recovery Unified Setup** to install the configuration server, the process server, and the master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="bced9-130">Run Azure Site Recovery Unified Setup</span><span class="sxs-lookup"><span data-stu-id="bced9-130">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> Configuration server registration fails if the time on your computer's system clock is more than five minutes off of local time. Synchronize your system clock with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting the installation.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> The configuration server can be installed via a command line. For more information, see [Installing configuration server using command-line tools](http://aka.ms/installconfigsrv).


## <a name="common-issues"></a><span data-ttu-id="bced9-135">Common issues</span><span class="sxs-lookup"><span data-stu-id="bced9-135">Common issues</span></span>

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="bced9-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="bced9-136">Next steps</span></span>

<span data-ttu-id="bced9-137">Next step involves [setting up your target environment](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span><span class="sxs-lookup"><span data-stu-id="bced9-137">Next step involves [setting up your target environment](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span></span>





