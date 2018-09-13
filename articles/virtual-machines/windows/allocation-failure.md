---
title: Troubleshooting Windows VM allocation failures | Microsoft Docs
description: Troubleshoot allocation failures when you create, restart, or resize a Windows VM in Azure
services: virtual-machines-windows, azure-resource-manager
documentationcenter: ''
author: JiangChen79
manager: felixwu
editor: ''
tags: top-support-issue,azure-resource-manager,azure-service-management
ms.assetid: bb939e23-77fc-4948-96f7-5037761c30e8
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cjiang
ms.openlocfilehash: d1d72a5ee0574fd74583e9e0011cbea73f9ddaf0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662147"
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-windows-vms-in-azure"></a><span data-ttu-id="92b25-103">Troubleshoot allocation failures when you create, restart, or resize Windows VMs in Azure</span><span class="sxs-lookup"><span data-stu-id="92b25-103">Troubleshoot allocation failures when you create, restart, or resize Windows VMs in Azure</span></span>
<span data-ttu-id="92b25-104">When you create a VM, restart stopped (deallocated) VMs, or resize a VM, Microsoft Azure allocates compute resources to your subscription.</span><span class="sxs-lookup"><span data-stu-id="92b25-104">When you create a VM, restart stopped (deallocated) VMs, or resize a VM, Microsoft Azure allocates compute resources to your subscription.</span></span> <span data-ttu-id="92b25-105">You may occasionally receive errors when performing these operations -- even before you reach the Azure subscription limits.</span><span class="sxs-lookup"><span data-stu-id="92b25-105">You may occasionally receive errors when performing these operations -- even before you reach the Azure subscription limits.</span></span> <span data-ttu-id="92b25-106">This article explains the causes of some of the common allocation failures and suggests possible remediation.</span><span class="sxs-lookup"><span data-stu-id="92b25-106">This article explains the causes of some of the common allocation failures and suggests possible remediation.</span></span> <span data-ttu-id="92b25-107">The information may also be useful when you plan the deployment of your services.</span><span class="sxs-lookup"><span data-stu-id="92b25-107">The information may also be useful when you plan the deployment of your services.</span></span> <span data-ttu-id="92b25-108">You can also [troubleshoot allocation failures when you create, restart, or resize Linux VMs in Azure](../linux/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="92b25-108">You can also [troubleshoot allocation failures when you create, restart, or resize Linux VMs in Azure](../linux/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

