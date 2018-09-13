---
title: Create FQDN for a Windows VM in the Azure portal | Microsoft Docs
description: Learn how to create a Fully Qualified Domain Name, or FQDN, for a Resource Manager based virtual machine in the Azure portal.
services: virtual-machines-windows
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a2ae5887-76df-485e-ae19-0efd96df8600
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c9b14b7684f8083651d9dfa4cca2e39b77a8ec23
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555571"
---
# <a name="create-a-fully-qualified-domain-name-in-the-azure-portal-for-a-windows-vm"></a><span data-ttu-id="08f66-103">Create a Fully Qualified Domain Name in the Azure portal for a Windows VM</span><span class="sxs-lookup"><span data-stu-id="08f66-103">Create a Fully Qualified Domain Name in the Azure portal for a Windows VM</span></span>

<span data-ttu-id="08f66-104">When you create a virtual machine (VM) in the [Azure portal](https://portal.azure.com) using the Resource Manager deployment model, a public IP resource for the virtual machine is automatically created.</span><span class="sxs-lookup"><span data-stu-id="08f66-104">When you create a virtual machine (VM) in the [Azure portal](https://portal.azure.com) using the Resource Manager deployment model, a public IP resource for the virtual machine is automatically created.</span></span> <span data-ttu-id="08f66-105">You use this IP address to remotely access the VM.</span><span class="sxs-lookup"><span data-stu-id="08f66-105">You use this IP address to remotely access the VM.</span></span> <span data-ttu-id="08f66-106">Although the portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, by default, you can create one once the VM is created.</span><span class="sxs-lookup"><span data-stu-id="08f66-106">Although the portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, by default, you can create one once the VM is created.</span></span> <span data-ttu-id="08f66-107">This article demonstrates the steps to create a DNS name or FQDN.</span><span class="sxs-lookup"><span data-stu-id="08f66-107">This article demonstrates the steps to create a DNS name or FQDN.</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="08f66-108">You can now connect remotely to the VM using this DNS name such as for Remote Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="08f66-108">You can now connect remotely to the VM using this DNS name such as for Remote Desktop Protocol (RDP).</span></span>

## <a name="next-steps"></a><span data-ttu-id="08f66-109">Next steps</span><span class="sxs-lookup"><span data-stu-id="08f66-109">Next steps</span></span>
<span data-ttu-id="08f66-110">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as IIS, SQL, or SharePoint.</span><span class="sxs-lookup"><span data-stu-id="08f66-110">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as IIS, SQL, or SharePoint.</span></span>

<span data-ttu-id="08f66-111">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span><span class="sxs-lookup"><span data-stu-id="08f66-111">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

