---
title: " Manage a Process Server running in Azure(Classic) | Microsoft Docs"
description: This article describes how to set up a failback Process Server(Classic) In Azure.
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
ms.date: 2/2/2017
ms.author: anoopkv
ms.openlocfilehash: f22fe8101dfbd82660e7e07c85ffdf34581f2b9a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670721"
---
# <a name="manage-a-process-server-running-in-azure-classic"></a><span data-ttu-id="1eee2-103">Manage a Process Server running in Azure (Classic)</span><span class="sxs-lookup"><span data-stu-id="1eee2-103">Manage a Process Server running in Azure (Classic)</span></span>
> [!div class="op_single_selector"]
> * [Azure Classic ](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [Resource Manager](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

<span data-ttu-id="1eee2-106">During failback, it is recommended to deploy Process Server in Azure if there is high latency between the Azure Virtual Network and your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="1eee2-106">During failback, it is recommended to deploy Process Server in Azure if there is high latency between the Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="1eee2-107">This article describes how you can set up, configure, and manage the process servers running in Azure.</span><span class="sxs-lookup"><span data-stu-id="1eee2-107">This article describes how you can set up, configure, and manage the process servers running in Azure.</span></span>

> [!NOTE]
> This article is to be used if you used **Resource Manager** as the deployment model for the virtual machines during failover. If you used **Classic** as the deployment model follow the steps in [How to set up & configure a Failback Process Server (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

## <a name="prerequisites"></a><span data-ttu-id="1eee2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1eee2-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="1eee2-111">Deploy a Process Server on Azure</span><span class="sxs-lookup"><span data-stu-id="1eee2-111">Deploy a Process Server on Azure</span></span>

1. <span data-ttu-id="1eee2-112">In Azure Marketplace, create a virtual machine using the **Microsoft Azure Site Recovery Process Server V2**</span><span class="sxs-lookup"><span data-stu-id="1eee2-112">In Azure Marketplace, create a virtual machine using the **Microsoft Azure Site Recovery Process Server V2**</span></span> </br>
    <span data-ttu-id="1eee2-113">![Marketplace_image_1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span><span class="sxs-lookup"><span data-stu-id="1eee2-113">![Marketplace_image_1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span></span>
2. <span data-ttu-id="1eee2-114">Ensure that you select the deployment model as **Classic**</span><span class="sxs-lookup"><span data-stu-id="1eee2-114">Ensure that you select the deployment model as **Classic**</span></span> </br>
  <span data-ttu-id="1eee2-115">![Marketplace_image_2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span><span class="sxs-lookup"><span data-stu-id="1eee2-115">![Marketplace_image_2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span></span>
3. <span data-ttu-id="1eee2-116">In the Create virtual machine wizard > Basic Settings, ensure you select the Subscription and Location to where you failed over the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1eee2-116">In the Create virtual machine wizard > Basic Settings, ensure you select the Subscription and Location to where you failed over the virtual machines.</span></span></br>
  <span data-ttu-id="1eee2-117">![create_image_1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span><span class="sxs-lookup"><span data-stu-id="1eee2-117">![create_image_1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span></span>
4. <span data-ttu-id="1eee2-118">Ensure that the virtual machine is connected to the Azure Virtual Network to which the failed over virtual machine is connected.</span><span class="sxs-lookup"><span data-stu-id="1eee2-118">Ensure that the virtual machine is connected to the Azure Virtual Network to which the failed over virtual machine is connected.</span></span></br>
  <span data-ttu-id="1eee2-119">![create_image_2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span><span class="sxs-lookup"><span data-stu-id="1eee2-119">![create_image_2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span></span>
5. <span data-ttu-id="1eee2-120">Once the Process Server virtual machine is provisioned, you need to log in and register it with the Configuration Server.</span><span class="sxs-lookup"><span data-stu-id="1eee2-120">Once the Process Server virtual machine is provisioned, you need to log in and register it with the Configuration Server.</span></span>

> [!NOTE]
> To be able to use this Process Server for failback, you need to register it with the on-premises configuration server.

## <a name="registering-the-process-server-running-in-azure-to-a-configuration-server-running-on-premises"></a><span data-ttu-id="1eee2-122">Registering the Process Server (running in Azure) to a Configuration Server (running on-premises)</span><span class="sxs-lookup"><span data-stu-id="1eee2-122">Registering the Process Server (running in Azure) to a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-the-process-server-to-latest-version"></a><span data-ttu-id="1eee2-123">Upgrading the Process Server to latest version.</span><span class="sxs-lookup"><span data-stu-id="1eee2-123">Upgrading the Process Server to latest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-the-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="1eee2-124">Unregistering the Process Server (running in Azure) from a Configuration Server (running on-premises)</span><span class="sxs-lookup"><span data-stu-id="1eee2-124">Unregistering the Process Server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]




