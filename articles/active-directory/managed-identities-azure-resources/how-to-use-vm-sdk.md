---
title: How to use managed identities for Azure resources on an Azure VM with Azure SDKs
description: Code samples for using Azure SDKs with an Azure VM that has managed identities for Azure resources.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/01/2017
ms.author: daveba
ms.openlocfilehash: 6827b01e72cd72d3f017df36205ccb985b4f242e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968675"
---
# <a name="how-to-use-managed-identities-for-azure-resources-on-an-azure-vm-with-azure-sdks"></a><span data-ttu-id="6aa72-103">How to use managed identities for Azure resources on an Azure VM with Azure SDKs</span><span class="sxs-lookup"><span data-stu-id="6aa72-103">How to use managed identities for Azure resources on an Azure VM with Azure SDKs</span></span> 

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]  
<span data-ttu-id="6aa72-104">This article provides a list of SDK samples, which demonstrate use of their respective Azure SDK's support for managed identities for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="6aa72-104">This article provides a list of SDK samples, which demonstrate use of their respective Azure SDK's support for managed identities for Azure resources.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6aa72-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6aa72-105">Prerequisites</span></span>

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

> [!IMPORTANT]
> - <span data-ttu-id="6aa72-106">All sample code/script in this article assumes the client is running on a VM with managed identities for Azure resources enabled.</span><span class="sxs-lookup"><span data-stu-id="6aa72-106">All sample code/script in this article assumes the client is running on a VM with managed identities for Azure resources enabled.</span></span> <span data-ttu-id="6aa72-107">Use the VM "Connect" feature in the Azure portal, to remotely connect to your VM.</span><span class="sxs-lookup"><span data-stu-id="6aa72-107">Use the VM "Connect" feature in the Azure portal, to remotely connect to your VM.</span></span> <span data-ttu-id="6aa72-108">For details on enabling managed identities for Azure resources on a VM, see [Configure managed identities for Azure resources on a VM using the Azure portal](qs-configure-portal-windows-vm.md), or one of the variant articles (using PowerShell, CLI, a template, or an Azure SDK).</span><span class="sxs-lookup"><span data-stu-id="6aa72-108">For details on enabling managed identities for Azure resources on a VM, see [Configure managed identities for Azure resources on a VM using the Azure portal](qs-configure-portal-windows-vm.md), or one of the variant articles (using PowerShell, CLI, a template, or an Azure SDK).</span></span> 

## <a name="sdk-code-samples"></a><span data-ttu-id="6aa72-109">SDK code samples</span><span class="sxs-lookup"><span data-stu-id="6aa72-109">SDK code samples</span></span>

| <span data-ttu-id="6aa72-110">SDK</span><span class="sxs-lookup"><span data-stu-id="6aa72-110">SDK</span></span>             | <span data-ttu-id="6aa72-111">Code sample</span><span class="sxs-lookup"><span data-stu-id="6aa72-111">Code sample</span></span> |
| --------------- | ----------- |
| <span data-ttu-id="6aa72-112">.NET</span><span class="sxs-lookup"><span data-stu-id="6aa72-112">.NET</span></span>            | [<span data-ttu-id="6aa72-113">Deploy an Azure Resource Manager template from a Windows VM using managed identities for Azure resources</span><span class="sxs-lookup"><span data-stu-id="6aa72-113">Deploy an Azure Resource Manager template from a Windows VM using managed identities for Azure resources</span></span>](https://github.com/Azure-Samples/windowsvm-msi-arm-dotnet) |
| <span data-ttu-id="6aa72-114">.NET Core</span><span class="sxs-lookup"><span data-stu-id="6aa72-114">.NET Core</span></span>       | [<span data-ttu-id="6aa72-115">Call Azure services from a Linux VM using managed identities for Azure resources</span><span class="sxs-lookup"><span data-stu-id="6aa72-115">Call Azure services from a Linux VM using managed identities for Azure resources</span></span>](https://github.com/Azure-Samples/linuxvm-msi-keyvault-arm-dotnet/) |
| <span data-ttu-id="6aa72-116">Node.js</span><span class="sxs-lookup"><span data-stu-id="6aa72-116">Node.js</span></span>         | [<span data-ttu-id="6aa72-117">Manage resources using managed identities for Azure resources</span><span class="sxs-lookup"><span data-stu-id="6aa72-117">Manage resources using managed identities for Azure resources</span></span>](https://azure.microsoft.com/resources/samples/resources-node-manage-resources-with-msi/) |
| <span data-ttu-id="6aa72-118">Python</span><span class="sxs-lookup"><span data-stu-id="6aa72-118">Python</span></span>          | [<span data-ttu-id="6aa72-119">Use managed identities for Azure resources to authenticate simply from inside a VM</span><span class="sxs-lookup"><span data-stu-id="6aa72-119">Use managed identities for Azure resources to authenticate simply from inside a VM</span></span>](https://azure.microsoft.com/resources/samples/resource-manager-python-manage-resources-with-msi/) |
| <span data-ttu-id="6aa72-120">Ruby</span><span class="sxs-lookup"><span data-stu-id="6aa72-120">Ruby</span></span>            | [<span data-ttu-id="6aa72-121">Manage resources from a VM with managed identities for Azure resources enabled</span><span class="sxs-lookup"><span data-stu-id="6aa72-121">Manage resources from a VM with managed identities for Azure resources enabled</span></span>](https://azure.microsoft.com/resources/samples/resources-ruby-manage-resources-with-msi/) |

## <a name="next-steps"></a><span data-ttu-id="6aa72-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="6aa72-122">Next steps</span></span>

- <span data-ttu-id="6aa72-123">See [Azure SDKs](https://azure.microsoft.com/downloads/) for the full list of Azure SDK resources, including library downloads, documentation, and more.</span><span class="sxs-lookup"><span data-stu-id="6aa72-123">See [Azure SDKs](https://azure.microsoft.com/downloads/) for the full list of Azure SDK resources, including library downloads, documentation, and more.</span></span>
- <span data-ttu-id="6aa72-124">To enable managed identities for Azure resources on an Azure VM, see [Configure managed identities for Azure resources on a VM using the Azure portal](qs-configure-portal-windows-vm.md).</span><span class="sxs-lookup"><span data-stu-id="6aa72-124">To enable managed identities for Azure resources on an Azure VM, see [Configure managed identities for Azure resources on a VM using the Azure portal](qs-configure-portal-windows-vm.md).</span></span>








