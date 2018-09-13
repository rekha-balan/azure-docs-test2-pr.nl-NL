---
title: Azure CLI Script Sample - Stop and delete a virtual machine in a lab | Microsoft Docs
description: This Azure CLI script stops and delets a virtual machine in a lab.
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
ms.openlocfilehash: a0dbcc530bd799b9fa457ba9b948e9ad99ce2a67
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865836"
---
# <a name="use-azure-cli-to-stop-and-delete-a-virtual-machine-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="16dbc-103">Use Azure CLI to stop and delete a virtual machine in a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="16dbc-103">Use Azure CLI to stop and delete a virtual machine in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="16dbc-104">This Azure CLI script stops and deletes a virtual machine (VM) in a lab.</span><span class="sxs-lookup"><span data-stu-id="16dbc-104">This Azure CLI script stops and deletes a virtual machine (VM) in a lab.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="16dbc-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="16dbc-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/devtest-lab/stop-delete-virtual-machine-in-lab/stop-delete-virtual-machine-in-lab.sh "Stop and delete a VM in a lab")]

## <a name="script-explanation"></a><span data-ttu-id="16dbc-106">Script explanation</span><span class="sxs-lookup"><span data-stu-id="16dbc-106">Script explanation</span></span>

<span data-ttu-id="16dbc-107">This script uses the following commands:</span><span class="sxs-lookup"><span data-stu-id="16dbc-107">This script uses the following commands:</span></span>

| <span data-ttu-id="16dbc-108">Command</span><span class="sxs-lookup"><span data-stu-id="16dbc-108">Command</span></span> | <span data-ttu-id="16dbc-109">Notes</span><span class="sxs-lookup"><span data-stu-id="16dbc-109">Notes</span></span> |
|---|---|
| [<span data-ttu-id="16dbc-110">az lab vm stop</span><span class="sxs-lookup"><span data-stu-id="16dbc-110">az lab vm stop</span></span>](/cli/azure/lab/vm?view=azure-cli-latest#az-lab-vm-stop) | <span data-ttu-id="16dbc-111">Stops a virtual machine (VM) in a lab.</span><span class="sxs-lookup"><span data-stu-id="16dbc-111">Stops a virtual machine (VM) in a lab.</span></span> <span data-ttu-id="16dbc-112">This operation can take a while to complete.</span><span class="sxs-lookup"><span data-stu-id="16dbc-112">This operation can take a while to complete.</span></span> |
| [<span data-ttu-id="16dbc-113">az lab vm delete</span><span class="sxs-lookup"><span data-stu-id="16dbc-113">az lab vm delete</span></span>](/cli/azure/lab/vm?view=azure-cli-latest#az-lab-vm-delete) | <span data-ttu-id="16dbc-114">Delets a virtual machine (VM) in a lab.</span><span class="sxs-lookup"><span data-stu-id="16dbc-114">Delets a virtual machine (VM) in a lab.</span></span> <span data-ttu-id="16dbc-115">This operation can take a while to complete.</span><span class="sxs-lookup"><span data-stu-id="16dbc-115">This operation can take a while to complete.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="16dbc-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="16dbc-116">Next steps</span></span>

<span data-ttu-id="16dbc-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="16dbc-117">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="16dbc-118">Additional Azure Lab Services CLI script samples can be found in the [Azure Lab Services CLI samples](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="16dbc-118">Additional Azure Lab Services CLI script samples can be found in the [Azure Lab Services CLI samples](../samples-cli.md).</span></span>
