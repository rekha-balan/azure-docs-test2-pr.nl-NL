---
title: Create FQDN for a Windows VM in the Azure portal | Microsoft Docs
description: Learn how to create a Fully Qualified Domain Name, or FQDN, for a Resource Manager based virtual machine in the Azure portal.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: tysonn
tags: azure-resource-manager
ms.assetid: a2ae5887-76df-485e-ae19-0efd96df8600
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/15/2018
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5395732ab8de52cdd3c2cea8657b2ed6b896d78b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44776340"
---
# <a name="create-a-fully-qualified-domain-name-in-the-azure-portal-for-a-windows-vm"></a>Create a fully qualified domain name in the Azure portal for a Windows VM

When you create a virtual machine (VM) in the [Azure portal](https://portal.azure.com), a public IP resource for the virtual machine is automatically created. You use this IP address to remotely access the VM. Although the portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can create one once the VM is created. This article demonstrates the steps to create a DNS name or FQDN.

## <a name="create-a-fqdn"></a>Create a FQDN
This article assumes that you have already created a VM. If needed, you can [create a VM in the portal](quick-create-portal.md) or [with Azure PowerShell](quick-create-powershell.md). Follow these steps once your VM is up and running:

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

You can now connect remotely to the VM using this DNS name such as for Remote Desktop Protocol (RDP).

## <a name="next-steps"></a>Next steps
Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as IIS, SQL, or SharePoint.

You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.

