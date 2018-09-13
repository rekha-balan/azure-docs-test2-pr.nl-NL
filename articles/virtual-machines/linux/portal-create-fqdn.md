---
title: Create FQDN for a Linux VM in the Azure portal | Microsoft Docs
description: Learn how to create a Fully Qualified Domain Name, or FQDN, for a Resource Manager based virtual machine in the Azure portal.
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2cd6c249-a737-4a0a-b5ba-e1c09e551b30
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 127cef214736501181b8028dbcd53d29c4efb5b4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553900"
---
# <a name="create-a-fully-qualified-domain-name-in-the-azure-portal-for-a-linux-vm"></a><span data-ttu-id="49c25-103">Create a Fully Qualified Domain Name in the Azure portal for a Linux VM</span><span class="sxs-lookup"><span data-stu-id="49c25-103">Create a Fully Qualified Domain Name in the Azure portal for a Linux VM</span></span>

<span data-ttu-id="49c25-104">When you create a virtual machine (VM) in the [Azure portal](https://portal.azure.com) using the Resource Manager deployment model, a public IP resource for the virtual machine is automatically created.</span><span class="sxs-lookup"><span data-stu-id="49c25-104">When you create a virtual machine (VM) in the [Azure portal](https://portal.azure.com) using the Resource Manager deployment model, a public IP resource for the virtual machine is automatically created.</span></span> <span data-ttu-id="49c25-105">You use this IP address to remotely access the VM.</span><span class="sxs-lookup"><span data-stu-id="49c25-105">You use this IP address to remotely access the VM.</span></span> <span data-ttu-id="49c25-106">Although the portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, by default, you can add one once the VM is created.</span><span class="sxs-lookup"><span data-stu-id="49c25-106">Although the portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, by default, you can add one once the VM is created.</span></span> <span data-ttu-id="49c25-107">This article demonstrates the steps to create a DNS name or FQDN.</span><span class="sxs-lookup"><span data-stu-id="49c25-107">This article demonstrates the steps to create a DNS name or FQDN.</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="49c25-108">You can now connect remotely to the VM using this DNS name such as with `ssh ops@mydns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="49c25-108">You can now connect remotely to the VM using this DNS name such as with `ssh ops@mydns.westus.cloudapp.azure.com`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49c25-109">Next steps</span><span class="sxs-lookup"><span data-stu-id="49c25-109">Next steps</span></span>
<span data-ttu-id="49c25-110">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as nginx, MongoDB, Docker, etc.</span><span class="sxs-lookup"><span data-stu-id="49c25-110">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as nginx, MongoDB, Docker, etc.</span></span>

<span data-ttu-id="49c25-111">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span><span class="sxs-lookup"><span data-stu-id="49c25-111">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

