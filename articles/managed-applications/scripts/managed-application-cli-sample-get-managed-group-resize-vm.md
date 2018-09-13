---
title: Azure CLI script sample - Get a managed resource group and resize VMs | Microsoft Docs
description: Azure CLI script sample - Get a managed resource group and resize VMs
services: managed-applications
documentationcenter: na
author: tfitzmac
manager: timlt
ms.service: managed-applications
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/25/2017
ms.author: tomfitz
ms.openlocfilehash: 85d58538e15881308ee1f645f7ddd12ec27c94de
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857128"
---
# <a name="get-resources-in-a-managed-resource-group-and-resize-vms-with-azure-cli"></a><span data-ttu-id="af53c-103">Get resources in a managed resource group and resize VMs with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="af53c-103">Get resources in a managed resource group and resize VMs with Azure CLI</span></span>

<span data-ttu-id="af53c-104">This script retrieves resources from a managed resource group, and resizes the VMs in that resource group.</span><span class="sxs-lookup"><span data-stu-id="af53c-104">This script retrieves resources from a managed resource group, and resizes the VMs in that resource group.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="af53c-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="af53c-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/managed-applications/get-application/get-application.sh "Get application")]


## <a name="script-explanation"></a><span data-ttu-id="af53c-106">Script explanation</span><span class="sxs-lookup"><span data-stu-id="af53c-106">Script explanation</span></span>

<span data-ttu-id="af53c-107">This script uses the following commands to deploy the managed application.</span><span class="sxs-lookup"><span data-stu-id="af53c-107">This script uses the following commands to deploy the managed application.</span></span> <span data-ttu-id="af53c-108">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="af53c-108">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="af53c-109">Command</span><span class="sxs-lookup"><span data-stu-id="af53c-109">Command</span></span> | <span data-ttu-id="af53c-110">Notes</span><span class="sxs-lookup"><span data-stu-id="af53c-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="af53c-111">az managedapp list</span><span class="sxs-lookup"><span data-stu-id="af53c-111">az managedapp list</span></span>](https://docs.microsoft.com/cli/azure/managedapp#az-managedapp-list) | <span data-ttu-id="af53c-112">List managed applications.</span><span class="sxs-lookup"><span data-stu-id="af53c-112">List managed applications.</span></span> <span data-ttu-id="af53c-113">Provide query values to focus the results.</span><span class="sxs-lookup"><span data-stu-id="af53c-113">Provide query values to focus the results.</span></span> |
| [<span data-ttu-id="af53c-114">az resource list</span><span class="sxs-lookup"><span data-stu-id="af53c-114">az resource list</span></span>](https://docs.microsoft.com/cli/azure/resource#az-resource-list) | <span data-ttu-id="af53c-115">List resources.</span><span class="sxs-lookup"><span data-stu-id="af53c-115">List resources.</span></span> <span data-ttu-id="af53c-116">Provide a resource group and query values to focus the result.</span><span class="sxs-lookup"><span data-stu-id="af53c-116">Provide a resource group and query values to focus the result.</span></span> |
| [<span data-ttu-id="af53c-117">az vm resize</span><span class="sxs-lookup"><span data-stu-id="af53c-117">az vm resize</span></span>](https://docs.microsoft.com/cli/azure/vm#az-vm-resize) | <span data-ttu-id="af53c-118">Update a virtual machine's size.</span><span class="sxs-lookup"><span data-stu-id="af53c-118">Update a virtual machine's size.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="af53c-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="af53c-119">Next steps</span></span>

* <span data-ttu-id="af53c-120">For an introduction to managed applications, see [Azure Managed Application overview](../overview.md).</span><span class="sxs-lookup"><span data-stu-id="af53c-120">For an introduction to managed applications, see [Azure Managed Application overview](../overview.md).</span></span>
* <span data-ttu-id="af53c-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="af53c-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>
