---
title: Create FQDN for a Linux VM in the Azure portal | Microsoft Docs
description: Learn how to create a Fully Qualified Domain Name, or FQDN, for a Resource Manager based virtual machine in the Azure portal.
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2cd6c249-a737-4a0a-b5ba-e1c09e551b30
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/15/2018
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a6c8f01164f83302d2df443a6db2d70d61cd2712
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809106"
---
# <a name="create-a-fully-qualified-domain-name-in-the-azure-portal-for-a-linux-vm"></a><span data-ttu-id="ecab3-103">Create a fully qualified domain name in the Azure portal for a Linux VM</span><span class="sxs-lookup"><span data-stu-id="ecab3-103">Create a fully qualified domain name in the Azure portal for a Linux VM</span></span>

<span data-ttu-id="ecab3-104">When you create a virtual machine (VM) in the [Azure portal](https://portal.azure.com), a public IP resource for the virtual machine is automatically created.</span><span class="sxs-lookup"><span data-stu-id="ecab3-104">When you create a virtual machine (VM) in the [Azure portal](https://portal.azure.com), a public IP resource for the virtual machine is automatically created.</span></span> <span data-ttu-id="ecab3-105">You use this IP address to remotely access the VM.</span><span class="sxs-lookup"><span data-stu-id="ecab3-105">You use this IP address to remotely access the VM.</span></span> <span data-ttu-id="ecab3-106">Although the portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can add one once the VM is created.</span><span class="sxs-lookup"><span data-stu-id="ecab3-106">Although the portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can add one once the VM is created.</span></span> <span data-ttu-id="ecab3-107">This article demonstrates the steps to create a DNS name or FQDN.</span><span class="sxs-lookup"><span data-stu-id="ecab3-107">This article demonstrates the steps to create a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="ecab3-108">Create a FQDN</span><span class="sxs-lookup"><span data-stu-id="ecab3-108">Create a FQDN</span></span>
<span data-ttu-id="ecab3-109">This article assumes that you have already created a VM.</span><span class="sxs-lookup"><span data-stu-id="ecab3-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="ecab3-110">If needed, you can [create a VM in the portal](quick-create-portal.md) or [with the Azure CLI](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ecab3-110">If needed, you can [create a VM in the portal](quick-create-portal.md) or [with the Azure CLI](quick-create-cli.md).</span></span> <span data-ttu-id="ecab3-111">Follow these steps once your VM is up and running:</span><span class="sxs-lookup"><span data-stu-id="ecab3-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="ecab3-112">You can now connect remotely to the VM using this DNS name such as with `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="ecab3-112">You can now connect remotely to the VM using this DNS name such as with `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecab3-113">Next steps</span><span class="sxs-lookup"><span data-stu-id="ecab3-113">Next steps</span></span>
<span data-ttu-id="ecab3-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as nginx, MongoDB, Docker, etc.</span><span class="sxs-lookup"><span data-stu-id="ecab3-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as nginx, MongoDB, Docker, etc.</span></span>

<span data-ttu-id="ecab3-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span><span class="sxs-lookup"><span data-stu-id="ecab3-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

