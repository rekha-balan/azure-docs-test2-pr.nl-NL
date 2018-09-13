---
title: " Manage a process server running in Azure (Resource Manager) | Microsoft Docs"
description: This article describes how to set up a failback process server (Resource Manager) In Azure.
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
ms.openlocfilehash: 49f3099dd97b8fa9c7539ef584949ccb66ad2974
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554407"
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a><span data-ttu-id="2b413-103">Manage a process server running in Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="2b413-103">Manage a process server running in Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [Classic ](./site-recovery-vmware-setup-azure-ps-classic.md)

<span data-ttu-id="2b413-106">During failback, it is recommended to deploy process server in Azure if there is high latency between the Azure Virtual Network and your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="2b413-106">During failback, it is recommended to deploy process server in Azure if there is high latency between the Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="2b413-107">This article describes how you can set up, configure, and manage the process servers running in Azure.</span><span class="sxs-lookup"><span data-stu-id="2b413-107">This article describes how you can set up, configure, and manage the process servers running in Azure.</span></span>

> [!NOTE]
> This article is to be used if you used **Resource Manager** as the deployment model for the virtual machines during failover. If you used **Classic** as the deployment model, follow the steps in [How to set up & configure a Failback process server (Classic)](./site-recovery-vmware-setup-azure-ps-classic.md)

## <a name="prerequisites"></a><span data-ttu-id="2b413-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2b413-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="2b413-111">Deploy a process server on Azure</span><span class="sxs-lookup"><span data-stu-id="2b413-111">Deploy a process server on Azure</span></span>
1. <span data-ttu-id="2b413-112">In the Vault > **Site Recovery Infrastructure** (under the "Manage" heading) > **Configuration Servers** (under "For VMware and Physical Machines" heading), select the configuration server.</span><span class="sxs-lookup"><span data-stu-id="2b413-112">In the Vault > **Site Recovery Infrastructure** (under the "Manage" heading) > **Configuration Servers** (under "For VMware and Physical Machines" heading), select the configuration server.</span></span>
2. <span data-ttu-id="2b413-113">In the Configuration Server details page that opens click "+ Process server"</span><span class="sxs-lookup"><span data-stu-id="2b413-113">In the Configuration Server details page that opens click "+ Process server"</span></span>

  ![Add process server gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  <span data-ttu-id="2b413-115">On the **Add process server** page, select the following values</span><span class="sxs-lookup"><span data-stu-id="2b413-115">On the **Add process server** page, select the following values</span></span>

  ![Add process server gallery item](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|<span data-ttu-id="2b413-117">**Field Name**</span><span class="sxs-lookup"><span data-stu-id="2b413-117">**Field Name**</span></span>|<span data-ttu-id="2b413-118">**Value**</span><span class="sxs-lookup"><span data-stu-id="2b413-118">**Value**</span></span>|
|-|-|
|<span data-ttu-id="2b413-119">Choose where you want to deploy your process server</span><span class="sxs-lookup"><span data-stu-id="2b413-119">Choose where you want to deploy your process server</span></span>|<span data-ttu-id="2b413-120">Select the value **Deploy a failback process server in Azure**</span><span class="sxs-lookup"><span data-stu-id="2b413-120">Select the value **Deploy a failback process server in Azure**</span></span> |
|<span data-ttu-id="2b413-121">Subscription</span><span class="sxs-lookup"><span data-stu-id="2b413-121">Subscription</span></span>|<span data-ttu-id="2b413-122">Select the Azure Subscription where you failed over the virtual machines</span><span class="sxs-lookup"><span data-stu-id="2b413-122">Select the Azure Subscription where you failed over the virtual machines</span></span>|
|<span data-ttu-id="2b413-123">Resource Group</span><span class="sxs-lookup"><span data-stu-id="2b413-123">Resource Group</span></span>|<span data-ttu-id="2b413-124">You can create a Resource Group to deploy this process server or choose to deploy the process server in an existing Resource Group</span><span class="sxs-lookup"><span data-stu-id="2b413-124">You can create a Resource Group to deploy this process server or choose to deploy the process server in an existing Resource Group</span></span>|
|<span data-ttu-id="2b413-125">Location</span><span class="sxs-lookup"><span data-stu-id="2b413-125">Location</span></span>|<span data-ttu-id="2b413-126">Select the Azure Data Center into which the virtual machines where failed over into</span><span class="sxs-lookup"><span data-stu-id="2b413-126">Select the Azure Data Center into which the virtual machines where failed over into</span></span>|
|<span data-ttu-id="2b413-127">Azure Network</span><span class="sxs-lookup"><span data-stu-id="2b413-127">Azure Network</span></span>|<span data-ttu-id="2b413-128">Select the Azure Virtual Network(VNet) that the virtual machines where failed over into.</span><span class="sxs-lookup"><span data-stu-id="2b413-128">Select the Azure Virtual Network(VNet) that the virtual machines where failed over into.</span></span> <span data-ttu-id="2b413-129">If you failed over virtual machines into multiple Azure VNets, then you need a process server deployed per VNet</span><span class="sxs-lookup"><span data-stu-id="2b413-129">If you failed over virtual machines into multiple Azure VNets, then you need a process server deployed per VNet</span></span>|

4. <span data-ttu-id="2b413-130">Fill in the rest of the properties for the process server</span><span class="sxs-lookup"><span data-stu-id="2b413-130">Fill in the rest of the properties for the process server</span></span>

  ![Add process server summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|<span data-ttu-id="2b413-132">**Field Name**</span><span class="sxs-lookup"><span data-stu-id="2b413-132">**Field Name**</span></span>|<span data-ttu-id="2b413-133">**Value**</span><span class="sxs-lookup"><span data-stu-id="2b413-133">**Value**</span></span>|
|-|-|
|<span data-ttu-id="2b413-134">Server Name</span><span class="sxs-lookup"><span data-stu-id="2b413-134">Server Name</span></span>|<span data-ttu-id="2b413-135">Display name & Host name for your process server virtual machine</span><span class="sxs-lookup"><span data-stu-id="2b413-135">Display name & Host name for your process server virtual machine</span></span>|
| <span data-ttu-id="2b413-136">User Name</span><span class="sxs-lookup"><span data-stu-id="2b413-136">User Name</span></span>|<span data-ttu-id="2b413-137">A user name that becomes an Administrator on that virtual machine</span><span class="sxs-lookup"><span data-stu-id="2b413-137">A user name that becomes an Administrator on that virtual machine</span></span>|
|<span data-ttu-id="2b413-138">Storage Account</span><span class="sxs-lookup"><span data-stu-id="2b413-138">Storage Account</span></span>|<span data-ttu-id="2b413-139">Name of the Storage Account where the virtual machine's virtual disk's are placed</span><span class="sxs-lookup"><span data-stu-id="2b413-139">Name of the Storage Account where the virtual machine's virtual disk's are placed</span></span>|
|<span data-ttu-id="2b413-140">Subnet</span><span class="sxs-lookup"><span data-stu-id="2b413-140">Subnet</span></span>|<span data-ttu-id="2b413-141">The subnet of the Azure VNet to which the virtual machine is connected</span><span class="sxs-lookup"><span data-stu-id="2b413-141">The subnet of the Azure VNet to which the virtual machine is connected</span></span>|
| <span data-ttu-id="2b413-142">IP Address</span><span class="sxs-lookup"><span data-stu-id="2b413-142">IP Address</span></span>|<span data-ttu-id="2b413-143">IP Address that you would like the process server to assume once it boots up</span><span class="sxs-lookup"><span data-stu-id="2b413-143">IP Address that you would like the process server to assume once it boots up</span></span>|
5. <span data-ttu-id="2b413-144">Click the OK button to start deploying the process server virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2b413-144">Click the OK button to start deploying the process server virtual machine.</span></span>

> [!NOTE]
> To be able to use this process server for failback, you need to register it with the on-premises configuration server.

## <a name="registering-the-process-server-running-in-azure-to-a-configuration-server-running-on-premises"></a><span data-ttu-id="2b413-146">Registering the process server (running in Azure) to a Configuration Server (running on-premises)</span><span class="sxs-lookup"><span data-stu-id="2b413-146">Registering the process server (running in Azure) to a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-the-process-server-to-latest-version"></a><span data-ttu-id="2b413-147">Upgrading the process server to latest version.</span><span class="sxs-lookup"><span data-stu-id="2b413-147">Upgrading the process server to latest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-the-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="2b413-148">Unregistering the process server (running in Azure) from a Configuration Server (running on-premises)</span><span class="sxs-lookup"><span data-stu-id="2b413-148">Unregistering the process server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]



