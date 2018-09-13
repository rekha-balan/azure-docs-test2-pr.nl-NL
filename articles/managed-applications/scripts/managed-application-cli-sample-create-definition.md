---
title: Azure CLI script sample - Create a managed application definition | Microsoft Docs
description: Azure CLI script sample - Create a managed application definition
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
ms.openlocfilehash: 1cc407e07aee307b00116aad1c44bf8e2b97e33e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856466"
---
# <a name="create-a-managed-application-definition-with-azure-cli"></a>Create a managed application definition with Azure CLI

This script publishes a managed application definition to a service catalog. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Sample script

[!code-azurecli[main](../../../cli_scripts/managed-applications/create-definition/create-definition.sh "Create definition")]


## <a name="script-explanation"></a>Script explanation

This script uses the following command to create the managed application definition. Each command in the table links to command-specific documentation.

| Command | Notes |
|---|---|
| [az managedapp definition create](https://docs.microsoft.com/cli/azure/managedapp/definition#az-managedapp-definition-create) | Create a managed application definition. Provide the package that contains the required files. |


## <a name="next-steps"></a>Next steps

* For an introduction to managed applications, see [Azure Managed Application overview](../overview.md).
* For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).
