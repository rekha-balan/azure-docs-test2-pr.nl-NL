---
title: Create a work or school identity in AAD for Linux | Microsoft Docs
description: Learn how to create a work or school identity in Azure Active Directory to use with your Linux virtual machines.
services: virtual-machines-linux
documentationcenter: ''
author: squillace
manager: timlt
editor: ''
tags: azure-service-management,azure-resource-manager
ms.assetid: b0f86d77-c669-4aa1-a095-c2aa4d9105fe
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 827af348e1d39d279e69d6261279aba4e0cc899a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556143"
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-to-use-with-linux-vms"></a><span data-ttu-id="a6863-103">Creating a Work or School identity in Azure Active Directory to use with Linux VMs</span><span class="sxs-lookup"><span data-stu-id="a6863-103">Creating a Work or School identity in Azure Active Directory to use with Linux VMs</span></span>
<span data-ttu-id="a6863-104">If you created a personal Azure account or have a personal MSDN subscription and created the Azure account to take advantage of the MSDN Azure credits -- you used a *Microsoft account* identity to create it.</span><span class="sxs-lookup"><span data-stu-id="a6863-104">If you created a personal Azure account or have a personal MSDN subscription and created the Azure account to take advantage of the MSDN Azure credits -- you used a *Microsoft account* identity to create it.</span></span> <span data-ttu-id="a6863-105">Many great features of Azure -- [resource group templates](../../azure-resource-manager/resource-group-overview.md) is one example -- require a work or school account (an identity managed by Azure Active Directory) to work.</span><span class="sxs-lookup"><span data-stu-id="a6863-105">Many great features of Azure -- [resource group templates](../../azure-resource-manager/resource-group-overview.md) is one example -- require a work or school account (an identity managed by Azure Active Directory) to work.</span></span> <span data-ttu-id="a6863-106">You can follow the instructions below to create a new work or school account because fortunately, one of the best things about your personal Azure account is that it comes with a default Azure Active Directory domain that you can use to create a new work or school account that you can use with Azure features that require it.</span><span class="sxs-lookup"><span data-stu-id="a6863-106">You can follow the instructions below to create a new work or school account because fortunately, one of the best things about your personal Azure account is that it comes with a default Azure Active Directory domain that you can use to create a new work or school account that you can use with Azure features that require it.</span></span>

<span data-ttu-id="a6863-107">However, recent changes make it possible to manage your subscription with any type of Azure account using the `azure login` interactive login method described [here](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="a6863-107">However, recent changes make it possible to manage your subscription with any type of Azure account using the `azure login` interactive login method described [here](../../xplat-cli-connect.md).</span></span> <span data-ttu-id="a6863-108">You can either use that mechanism, or you can follow the instructions that follow.</span><span class="sxs-lookup"><span data-stu-id="a6863-108">You can either use that mechanism, or you can follow the instructions that follow.</span></span> <span data-ttu-id="a6863-109">You can also [create a work or school identity in Azure Active Directory to use with Windows VMs](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6863-109">You can also [create a work or school identity in Azure Active Directory to use with Windows VMs](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

