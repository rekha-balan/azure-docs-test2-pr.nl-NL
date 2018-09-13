---
title: Azure CLI Script Sample - Start a virtual machine in a lab | Microsoft Docs
description: This Azure CLI script starts a virtual machine in a lab in Azure DevTest Labs.
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
ms.openlocfilehash: a635766c1a7fb9ae10a651d09ecd7da9a5f01e51
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866584"
---
# <a name="use-azure-cli-to-start-a-virtual-machine-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="f11bc-103">Use Azure CLI to start a virtual machine in a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="f11bc-103">Use Azure CLI to start a virtual machine in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="f11bc-104">This Azure CLI script starts a virtual machine (VM) in a lab.</span><span class="sxs-lookup"><span data-stu-id="f11bc-104">This Azure CLI script starts a virtual machine (VM) in a lab.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f11bc-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="f11bc-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/devtest-lab/start-connect-virtual-machine-in-lab/start-connect-virtual-machine-in-lab.sh "Start a VM")]


## <a name="script-explanation"></a><span data-ttu-id="f11bc-106">Script explanation</span><span class="sxs-lookup"><span data-stu-id="f11bc-106">Script explanation</span></span>

<span data-ttu-id="f11bc-107">This script uses the following commands:</span><span class="sxs-lookup"><span data-stu-id="f11bc-107">This script uses the following commands:</span></span>

| <span data-ttu-id="f11bc-108">Command</span><span class="sxs-lookup"><span data-stu-id="f11bc-108">Command</span></span> | <span data-ttu-id="f11bc-109">Notes</span><span class="sxs-lookup"><span data-stu-id="f11bc-109">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f11bc-110">az lab vm start </span><span class="sxs-lookup"><span data-stu-id="f11bc-110">az lab vm start </span></span>](/cli/azure/lab/vm?view=azure-cli-latest#az-lab-vm-start) | <span data-ttu-id="f11bc-111">Starts a virtual machine (VM) in a lab.</span><span class="sxs-lookup"><span data-stu-id="f11bc-111">Starts a virtual machine (VM) in a lab.</span></span> <span data-ttu-id="f11bc-112">This operation can take a while to complete.</span><span class="sxs-lookup"><span data-stu-id="f11bc-112">This operation can take a while to complete.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f11bc-113">Next steps</span><span class="sxs-lookup"><span data-stu-id="f11bc-113">Next steps</span></span>

<span data-ttu-id="f11bc-114">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="f11bc-114">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="f11bc-115">Additional Azure Lab Services CLI script samples can be found in the [Azure Lab Services CLI samples](../samples-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f11bc-115">Additional Azure Lab Services CLI script samples can be found in the [Azure Lab Services CLI samples](../samples-cli.md).</span></span>
