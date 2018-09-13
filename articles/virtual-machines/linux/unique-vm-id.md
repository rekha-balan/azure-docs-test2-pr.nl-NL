---
title: Get an Azure Linux VM ID  | Microsoft Docs
description: Describes how to get and use an Azure Linux VM Unique ID.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: ''
ms.assetid: 136c5d28-ff6b-4466-b27f-7a29785b5d27
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 01/23/2017
ms.author: kmouss
ms.openlocfilehash: 6c39ee3a709c65ffbb5dd8f2c466e72d0c56d624
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563081"
---
# <a name="accessing-and-using-azure-vm-unique-id"></a><span data-ttu-id="0e123-103">Accessing and Using Azure VM Unique ID</span><span class="sxs-lookup"><span data-stu-id="0e123-103">Accessing and Using Azure VM Unique ID</span></span>
<span data-ttu-id="0e123-104">Azure VM unique ID is a 128bits identifier encoded and stored in all Azure IaaS VM’s SMBIOS and can currently be read using platform BIOS commands.</span><span class="sxs-lookup"><span data-stu-id="0e123-104">Azure VM unique ID is a 128bits identifier encoded and stored in all Azure IaaS VM’s SMBIOS and can currently be read using platform BIOS commands.</span></span>

<span data-ttu-id="0e123-105">Azure VM unique ID is a Read-only property.</span><span class="sxs-lookup"><span data-stu-id="0e123-105">Azure VM unique ID is a Read-only property.</span></span> <span data-ttu-id="0e123-106">Azure Unique VM ID won’t change upon reboot shutdown (either planned for unplanned), Start/Stop de-allocate, service healing or restore in place.</span><span class="sxs-lookup"><span data-stu-id="0e123-106">Azure Unique VM ID won’t change upon reboot shutdown (either planned for unplanned), Start/Stop de-allocate, service healing or restore in place.</span></span> <span data-ttu-id="0e123-107">However, if the VM is a snapshot and copied to create a new instance, new Azure VM ID is configured.</span><span class="sxs-lookup"><span data-stu-id="0e123-107">However, if the VM is a snapshot and copied to create a new instance, new Azure VM ID is configured.</span></span>

> [!NOTE]
> <span data-ttu-id="0e123-108">If you have older VMs created and running since this new feature got rolled out (September 18, 2014), please restart your VM to automatically get an Azure unique ID.</span><span class="sxs-lookup"><span data-stu-id="0e123-108">If you have older VMs created and running since this new feature got rolled out (September 18, 2014), please restart your VM to automatically get an Azure unique ID.</span></span>
> 
> 

<span data-ttu-id="0e123-109">To access Azure Unique VM ID from within the VM:</span><span class="sxs-lookup"><span data-stu-id="0e123-109">To access Azure Unique VM ID from within the VM:</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="0e123-110">Create a VM</span><span class="sxs-lookup"><span data-stu-id="0e123-110">Create a VM</span></span>
<span data-ttu-id="0e123-111">For more information, see [Create a Virtual Machine](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="0e123-111">For more information, see [Create a Virtual Machine](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="connect-to-the-vm"></a><span data-ttu-id="0e123-112">Connect to the VM</span><span class="sxs-lookup"><span data-stu-id="0e123-112">Connect to the VM</span></span>
<span data-ttu-id="0e123-113">For more information, see [SSH from Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="0e123-113">For more information, see [SSH from Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="query-vm-unique-id"></a><span data-ttu-id="0e123-114">Query VM Unique ID</span><span class="sxs-lookup"><span data-stu-id="0e123-114">Query VM Unique ID</span></span>
<span data-ttu-id="0e123-115">Command (example uses **Ubuntu**):</span><span class="sxs-lookup"><span data-stu-id="0e123-115">Command (example uses **Ubuntu**):</span></span>

```bash
sudo dmidecode | grep UUID
```

<span data-ttu-id="0e123-116">Example Expected Results:</span><span class="sxs-lookup"><span data-stu-id="0e123-116">Example Expected Results:</span></span>

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

<span data-ttu-id="0e123-117">Due to Big Endian bit ordering, the actual Unique VM ID in this case will be:</span><span class="sxs-lookup"><span data-stu-id="0e123-117">Due to Big Endian bit ordering, the actual Unique VM ID in this case will be:</span></span>

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

<span data-ttu-id="0e123-118">Azure VM unique ID can be used in different scenarios whether the VM is running on Azure or on-premises and can help your licensing, reporting or general tracking requirements you may have on your Azure IaaS deployments.</span><span class="sxs-lookup"><span data-stu-id="0e123-118">Azure VM unique ID can be used in different scenarios whether the VM is running on Azure or on-premises and can help your licensing, reporting or general tracking requirements you may have on your Azure IaaS deployments.</span></span> <span data-ttu-id="0e123-119">Many independent software vendors building applications and certifying them on Azure may require to identify an Azure VM throughout its lifecycle and to tell if the VM is running on Azure, on-Premises or on other cloud providers.</span><span class="sxs-lookup"><span data-stu-id="0e123-119">Many independent software vendors building applications and certifying them on Azure may require to identify an Azure VM throughout its lifecycle and to tell if the VM is running on Azure, on-Premises or on other cloud providers.</span></span> <span data-ttu-id="0e123-120">This platform identifier can for example help detect if the software is properly licensed or help to correlate any VM data to its source such as to assist on setting the right metrics for the right platform and to track and correlate these metrics amongst other uses.</span><span class="sxs-lookup"><span data-stu-id="0e123-120">This platform identifier can for example help detect if the software is properly licensed or help to correlate any VM data to its source such as to assist on setting the right metrics for the right platform and to track and correlate these metrics amongst other uses.</span></span>

