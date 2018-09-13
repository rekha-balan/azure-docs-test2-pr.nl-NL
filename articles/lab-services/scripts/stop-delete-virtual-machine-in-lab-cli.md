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
# <a name="use-azure-cli-to-stop-and-delete-a-virtual-machine-in-a-lab-in-azure-devtest-labs"></a>Use Azure CLI to stop and delete a virtual machine in a lab in Azure DevTest Labs

This Azure CLI script stops and deletes a virtual machine (VM) in a lab. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Sample script

[!code-azurecli-interactive[main](../../../cli_scripts/devtest-lab/stop-delete-virtual-machine-in-lab/stop-delete-virtual-machine-in-lab.sh "Stop and delete a VM in a lab")]

## <a name="script-explanation"></a>Script explanation

This script uses the following commands:

| Command | Notes |
|---|---|
| [az lab vm stop](/cli/azure/lab/vm?view=azure-cli-latest#az-lab-vm-stop) | Stops a virtual machine (VM) in a lab. This operation can take a while to complete. |
| [az lab vm delete](/cli/azure/lab/vm?view=azure-cli-latest#az-lab-vm-delete) | Delets a virtual machine (VM) in a lab. This operation can take a while to complete. |


## <a name="next-steps"></a>Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).

Additional Azure Lab Services CLI script samples can be found in the [Azure Lab Services CLI samples](../samples-cli.md).
