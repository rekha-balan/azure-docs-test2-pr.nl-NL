---
title: Azure CLI Samples | Microsoft Docs
description: Azure CLI Samples
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/08/2017
ms.author: nepeters
ms.openlocfilehash: a76ffc7e5b36f53b9799dc5e213d6bc2b580bbf6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550873"
---
# <a name="azure-cli-samples-for-linux-virtual-machines"></a><span data-ttu-id="c0128-103">Azure CLI Samples for Linux virtual machines</span><span class="sxs-lookup"><span data-stu-id="c0128-103">Azure CLI Samples for Linux virtual machines</span></span>

<span data-ttu-id="c0128-104">The following table includes links to bash scripts built using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c0128-104">The following table includes links to bash scripts built using the Azure CLI.</span></span>

| | |
|---|---|
|<span data-ttu-id="c0128-105">**Create virtual machines**</span><span class="sxs-lookup"><span data-stu-id="c0128-105">**Create virtual machines**</span></span>||
| [<span data-ttu-id="c0128-106">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="c0128-106">Create a virtual machine</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="c0128-107">Creates a Linux virtual machine with minimal configuration.</span><span class="sxs-lookup"><span data-stu-id="c0128-107">Creates a Linux virtual machine with minimal configuration.</span></span> |
| [<span data-ttu-id="c0128-108">Create a fully configured virtual machine</span><span class="sxs-lookup"><span data-stu-id="c0128-108">Create a fully configured virtual machine</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="c0128-109">Creates a resource group, virtual machine, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="c0128-109">Creates a resource group, virtual machine, and all related resources.</span></span>|
| [<span data-ttu-id="c0128-110">Create highly available virtual machines</span><span class="sxs-lookup"><span data-stu-id="c0128-110">Create highly available virtual machines</span></span>](./../scripts/virtual-machines-linux-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="c0128-111">Creates several virtual machines in a highly available and load balanced configuration.</span><span class="sxs-lookup"><span data-stu-id="c0128-111">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="c0128-112">Create a VM with Docker enabled</span><span class="sxs-lookup"><span data-stu-id="c0128-112">Create a VM with Docker enabled</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-docker-host.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="c0128-113">Creates a virtual machine, configures this VM as a Docker host, and runs an NGINX container.</span><span class="sxs-lookup"><span data-stu-id="c0128-113">Creates a virtual machine, configures this VM as a Docker host, and runs an NGINX container.</span></span> |
| [<span data-ttu-id="c0128-114">Create a VM and run configuration script</span><span class="sxs-lookup"><span data-stu-id="c0128-114">Create a VM and run configuration script</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="c0128-115">Creates a virtual machine and uses the Azure Custom Script extension to install NGINX.</span><span class="sxs-lookup"><span data-stu-id="c0128-115">Creates a virtual machine and uses the Azure Custom Script extension to install NGINX.</span></span> |
| [<span data-ttu-id="c0128-116">Create a VM with WordPress installed</span><span class="sxs-lookup"><span data-stu-id="c0128-116">Create a VM with WordPress installed</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm-wordpress.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="c0128-117">Creates a virtual machine and uses the Azure Custom Script extension to install WordPress.</span><span class="sxs-lookup"><span data-stu-id="c0128-117">Creates a virtual machine and uses the Azure Custom Script extension to install WordPress.</span></span> |
|<span data-ttu-id="c0128-118">**Network virtual machines**</span><span class="sxs-lookup"><span data-stu-id="c0128-118">**Network virtual machines**</span></span>||
| [<span data-ttu-id="c0128-119">Secure network traffic between virtual machines</span><span class="sxs-lookup"><span data-stu-id="c0128-119">Secure network traffic between virtual machines</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="c0128-120">Creates two virtual machines, all related resources, and an internal and external network security groups (NSG).</span><span class="sxs-lookup"><span data-stu-id="c0128-120">Creates two virtual machines, all related resources, and an internal and external network security groups (NSG).</span></span> |
|<span data-ttu-id="c0128-121">**Monitor virtual machines**</span><span class="sxs-lookup"><span data-stu-id="c0128-121">**Monitor virtual machines**</span></span>||
| [<span data-ttu-id="c0128-122">Monitor a VM with Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="c0128-122">Monitor a VM with Operations Management Suite</span></span>](./../scripts/virtual-machines-linux-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="c0128-123">Creates a virtual machine, installs the Operations Management Suite agent, and enrolls the VM in an OMS Workspace.</span><span class="sxs-lookup"><span data-stu-id="c0128-123">Creates a virtual machine, installs the Operations Management Suite agent, and enrolls the VM in an OMS Workspace.</span></span>  |
|<span data-ttu-id="c0128-124">**Troubleshoot virtual machines**</span><span class="sxs-lookup"><span data-stu-id="c0128-124">**Troubleshoot virtual machines**</span></span>||
| [<span data-ttu-id="c0128-125">Troubleshoot a VMs operating system disk</span><span class="sxs-lookup"><span data-stu-id="c0128-125">Troubleshoot a VMs operating system disk</span></span>](./../scripts/virtual-machines-linux-cli-sample-mount-os-disk.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="c0128-126">Mounts the operating system disk from one VM as a data disk on a second VM.</span><span class="sxs-lookup"><span data-stu-id="c0128-126">Mounts the operating system disk from one VM as a data disk on a second VM.</span></span> |
| | |
