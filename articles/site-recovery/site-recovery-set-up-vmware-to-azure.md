---
title: Set up the source environment (VMware to Azure) | Microsoft Docs
description: This article describes how to set up your on-premises environment to start replicating VMware virtual machines to Azure.
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
ms.openlocfilehash: 1ea6d3d66f352bcb91a8449f0dd1142ff97282d0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555201"
---
# <a name="set-up-the-source-environment-vmware-to-azure"></a><span data-ttu-id="84696-103">Set up the source environment (VMware to Azure)</span><span class="sxs-lookup"><span data-stu-id="84696-103">Set up the source environment (VMware to Azure)</span></span>
> [!div class="op_single_selector"]
> * [VMware Virtual Machines](./site-recovery-set-up-vmware-to-azure.md)
> * [Physical Servers](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="84696-106">This article describes how to set up your on-premises environment to start replicating virtual machines running on VMware to Azure.</span><span class="sxs-lookup"><span data-stu-id="84696-106">This article describes how to set up your on-premises environment to start replicating virtual machines running on VMware to Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84696-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="84696-107">Prerequisites</span></span>

<span data-ttu-id="84696-108">The article assumes that you have already created:</span><span class="sxs-lookup"><span data-stu-id="84696-108">The article assumes that you have already created:</span></span>
- <span data-ttu-id="84696-109">A Recovery Services Vault in the [Azure portal](http://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="84696-109">A Recovery Services Vault in the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="84696-110">A dedicated account in your VMware vCenter that can be used for [automatic discovery](./site-recovery-vmware-to-azure.md#vmware-account-permissions).</span><span class="sxs-lookup"><span data-stu-id="84696-110">A dedicated account in your VMware vCenter that can be used for [automatic discovery](./site-recovery-vmware-to-azure.md#vmware-account-permissions).</span></span>
- <span data-ttu-id="84696-111">A virtual machine on which to install the configuration server.</span><span class="sxs-lookup"><span data-stu-id="84696-111">A virtual machine on which to install the configuration server.</span></span>

## <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="84696-112">Configuration server minimum requirements</span><span class="sxs-lookup"><span data-stu-id="84696-112">Configuration server minimum requirements</span></span>
<span data-ttu-id="84696-113">The configuration server software should be deployed on a highly available VMware virtual machine.</span><span class="sxs-lookup"><span data-stu-id="84696-113">The configuration server software should be deployed on a highly available VMware virtual machine.</span></span> <span data-ttu-id="84696-114">The following table lists the minimum hardware, software, and network requirements for a configuration server.</span><span class="sxs-lookup"><span data-stu-id="84696-114">The following table lists the minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> HTTPS-based proxy servers are not supported by the configuration server.

## <a name="choose-your-protection-goals"></a><span data-ttu-id="84696-116">Choose your protection goals</span><span class="sxs-lookup"><span data-stu-id="84696-116">Choose your protection goals</span></span>

1. <span data-ttu-id="84696-117">In the Azure portal, go to the **Recovery Services** vault blade and select your vault.</span><span class="sxs-lookup"><span data-stu-id="84696-117">In the Azure portal, go to the **Recovery Services** vault blade and select your vault.</span></span>
2. <span data-ttu-id="84696-118">On the resource menu of the vault, go to **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span><span class="sxs-lookup"><span data-stu-id="84696-118">On the resource menu of the vault, go to **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Choose goals](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. <span data-ttu-id="84696-120">In **Protection goal**, select **To Azure**, and choose **Yes, with VMware vSphere Hypervisor**.</span><span class="sxs-lookup"><span data-stu-id="84696-120">In **Protection goal**, select **To Azure**, and choose **Yes, with VMware vSphere Hypervisor**.</span></span> <span data-ttu-id="84696-121">Then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="84696-121">Then click **OK**.</span></span>

    ![Choose goals](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-the-source-environment"></a><span data-ttu-id="84696-123">Set up the source environment</span><span class="sxs-lookup"><span data-stu-id="84696-123">Set up the source environment</span></span>
<span data-ttu-id="84696-124">Setting up the source environment involves two main activities:</span><span class="sxs-lookup"><span data-stu-id="84696-124">Setting up the source environment involves two main activities:</span></span>

- <span data-ttu-id="84696-125">Install and register a configuration server with Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="84696-125">Install and register a configuration server with Site Recovery.</span></span>
- <span data-ttu-id="84696-126">Discover your on-premises virtual machines by connecting Site Recovery to your on-premises VMware vCenter or vSphere EXSi hosts.</span><span class="sxs-lookup"><span data-stu-id="84696-126">Discover your on-premises virtual machines by connecting Site Recovery to your on-premises VMware vCenter or vSphere EXSi hosts.</span></span>

### <a name="step-1-install-and-register-a-configuration-server"></a><span data-ttu-id="84696-127">Step 1: Install and register a configuration server</span><span class="sxs-lookup"><span data-stu-id="84696-127">Step 1: Install and register a configuration server</span></span>

1. <span data-ttu-id="84696-128">Click **Step 1: Prepare Infrastructure** > **Source**.</span><span class="sxs-lookup"><span data-stu-id="84696-128">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span> <span data-ttu-id="84696-129">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** to add one.</span><span class="sxs-lookup"><span data-stu-id="84696-129">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** to add one.</span></span>

    ![Set up source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. <span data-ttu-id="84696-131">On the **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span><span class="sxs-lookup"><span data-stu-id="84696-131">On the **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="84696-132">Download the Site Recovery Unified Setup installation file.</span><span class="sxs-lookup"><span data-stu-id="84696-132">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="84696-133">Download the vault registration key.</span><span class="sxs-lookup"><span data-stu-id="84696-133">Download the vault registration key.</span></span> <span data-ttu-id="84696-134">You need the registration key when you run Unified Setup.</span><span class="sxs-lookup"><span data-stu-id="84696-134">You need the registration key when you run Unified Setup.</span></span> <span data-ttu-id="84696-135">The key is valid for five days after you generate it.</span><span class="sxs-lookup"><span data-stu-id="84696-135">The key is valid for five days after you generate it.</span></span>

    ![Set up source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. <span data-ttu-id="84696-137">On the machine you’re using as the configuration server, run **Azure Site Recovery Unified Setup** to install the configuration server, the process server, and the master target server.</span><span class="sxs-lookup"><span data-stu-id="84696-137">On the machine you’re using as the configuration server, run **Azure Site Recovery Unified Setup** to install the configuration server, the process server, and the master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="84696-138">Run Azure Site Recovery Unified Setup</span><span class="sxs-lookup"><span data-stu-id="84696-138">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> Configuration server registration fails if the time on your computer's system clock differs from local time by more than five minutes. Synchronize your system clock with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting the installation.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> The configuration server can be installed via command line. For more information, see [Installing the configuration server using Command-line tools](http://aka.ms/installconfigsrv).

#### <a name="add-the-vmware-account-for-automatic-discovery"></a><span data-ttu-id="84696-143">Add the VMware account for automatic discovery</span><span class="sxs-lookup"><span data-stu-id="84696-143">Add the VMware account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a><span data-ttu-id="84696-144">Step 2: Add a vCenter</span><span class="sxs-lookup"><span data-stu-id="84696-144">Step 2: Add a vCenter</span></span>
<span data-ttu-id="84696-145">To allow Azure Site Recovery to discover virtual machines running in your on-premises environment, you need to connect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="84696-145">To allow Azure Site Recovery to discover virtual machines running in your on-premises environment, you need to connect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span>

<span data-ttu-id="84696-146">Select **+vCenter** to start connecting a VMware vCenter server or a VMware vSphere ESXi host.</span><span class="sxs-lookup"><span data-stu-id="84696-146">Select **+vCenter** to start connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a><span data-ttu-id="84696-147">Common issues</span><span class="sxs-lookup"><span data-stu-id="84696-147">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="84696-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="84696-148">Next steps</span></span>
<span data-ttu-id="84696-149">[Set up your target environment](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.</span><span class="sxs-lookup"><span data-stu-id="84696-149">[Set up your target environment](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.</span></span>




