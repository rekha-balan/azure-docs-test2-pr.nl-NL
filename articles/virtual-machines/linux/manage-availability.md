---
title: Manage the availability of Linux VMs in Azure | Microsoft Docs
description: Learn how to use multiple virtual machines to ensure high availability for your Linux application in Azure
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 891c852a-84c0-4940-a61e-ada6e185bf37
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/27/2018
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 952c5e6bce0a11ced01626ca5be5d3232945e25b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44814384"
---
# <a name="manage-the-availability-of-linux-virtual-machines"></a><span data-ttu-id="3f1e6-103">Manage the availability of Linux virtual machines</span><span class="sxs-lookup"><span data-stu-id="3f1e6-103">Manage the availability of Linux virtual machines</span></span>

<span data-ttu-id="3f1e6-104">Learn ways to set up and manage multiple virtual machines to ensure high availability for your Linux application in Azure.</span><span class="sxs-lookup"><span data-stu-id="3f1e6-104">Learn ways to set up and manage multiple virtual machines to ensure high availability for your Linux application in Azure.</span></span> <span data-ttu-id="3f1e6-105">You can also [manage the availability of Windows virtual machines](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3f1e6-105">You can also [manage the availability of Windows virtual machines](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="3f1e6-106">For instructions on creating an availability set using CLI in the Resource Manager deployment model, see [azure availset: commands to manage your availability sets](../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets).</span><span class="sxs-lookup"><span data-stu-id="3f1e6-106">For instructions on creating an availability set using CLI in the Resource Manager deployment model, see [azure availset: commands to manage your availability sets](../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets).</span></span>

[!INCLUDE [virtual-machines-common-manage-availability](../../../includes/virtual-machines-common-manage-availability.md)]

## <a name="next-steps"></a><span data-ttu-id="3f1e6-107">Next steps</span><span class="sxs-lookup"><span data-stu-id="3f1e6-107">Next steps</span></span>
<span data-ttu-id="3f1e6-108">To learn more about load balancing your virtual machines, see [Load Balancing virtual machines](../virtual-machines-linux-load-balance.md).</span><span class="sxs-lookup"><span data-stu-id="3f1e6-108">To learn more about load balancing your virtual machines, see [Load Balancing virtual machines](../virtual-machines-linux-load-balance.md).</span></span>

