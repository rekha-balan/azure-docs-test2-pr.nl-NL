---
title: Azure CLI Script Sample - Create and verify a virtual machine in a lab | Microsoft Docs
description: This Azure CLI script creates a virtual machine in a lab, and verifies that it's available.
services: lab-services
author: spelluru
manager: ''
editor: ''
ms.assetid: ''
ms.service: lab-services
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2018
ms.author: spelluru
ms.custom: mvc
ms.openlocfilehash: b8d48f221dc54a3cd96bf2dbec08e40a047b7940
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857175"
---
# <a name="use-azure-cli-to-create-and-verify-availability-of-a-virtual-machine-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="3080c-103">Use Azure CLI to create and verify availability of a virtual machine in a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="3080c-103">Use Azure CLI to create and verify availability of a virtual machine in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="3080c-104">This Azure CLI script creates a virtual machine (VM) in a lab.</span><span class="sxs-lookup"><span data-stu-id="3080c-104">This Azure CLI script creates a virtual machine (VM) in a lab.</span></span> <span data-ttu-id="3080c-105">The VM created based on a marketplace image with ssh authentication.</span><span class="sxs-lookup"><span data-stu-id="3080c-105">The VM created based on a marketplace image with ssh authentication.</span></span> <span data-ttu-id="3080c-106">The script then verifies that the VM is available for use.</span><span class="sxs-lookup"><span data-stu-id="3080c-106">The script then verifies that the VM is available for use.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3080c-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="3080c-107">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/devtest-lab/create-verify-virtual-machine-in-lab/create-verify-virtual-machine-in-lab.sh "Create and verify availability of a VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3080c-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="3080c-108">Clean up deployment</span></span> 

<span data-ttu-id="3080c-109">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="3080c-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="3080c-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="3080c-110">Script explanation</span></span>

<span data-ttu-id="3080c-111">This script uses the following commands:</span><span class="sxs-lookup"><span data-stu-id="3080c-111">This script uses the following commands:</span></span>

| <span data-ttu-id="3080c-112">Command</span><span class="sxs-lookup"><span data-stu-id="3080c-112">Command</span></span> | <span data-ttu-id="3080c-113">Notes</span><span class="sxs-lookup"><span data-stu-id="3080c-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3080c-114">az group create</span><span class="sxs-lookup"><span data-stu-id="3080c-114">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="3080c-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="3080c-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3080c-116">az lab vm create </span><span class="sxs-lookup"><span data-stu-id="3080c-116">az lab vm create </span></span>](/cli/azure/lab/vm?view=azure-cli-latest#az-lab-vm-create) | <span data-ttu-id="3080c-117">Creates a virtual machine (VM) in a lab.</span><span class="sxs-lookup"><span data-stu-id="3080c-117">Creates a virtual machine (VM) in a lab.</span></span> |
| [<span data-ttu-id="3080c-118">az lab vm show</span><span class="sxs-lookup"><span data-stu-id="3080c-118">az lab vm show</span></span>](/cli/azure/lab/vm?view=azure-cli-latest#az-lab-vm-show) | <span data-ttu-id="3080c-119">Displays the status of the VM in a lab.</span><span class="sxs-lookup"><span data-stu-id="3080c-119">Displays the status of the VM in a lab.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3080c-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="3080c-120">Next steps</span></span>

<span data-ttu-id="3080c-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="3080c-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="3080c-122">Additional Azure Lab Services CLI script samples can be found in the [Azure Lab Services CLI samples](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="3080c-122">Additional Azure Lab Services CLI script samples can be found in the [Azure Lab Services CLI samples](../samples-cli.md).</span></span>
