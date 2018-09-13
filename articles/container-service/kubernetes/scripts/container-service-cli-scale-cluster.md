---
title: Azure CLI Script Sample - Scale an ACS Cluster | Microsoft Docs
description: Azure CLI Script Sample - Scale an ACS Cluster
services: container-service
documentationcenter: ''
author: neilpeterson
manager: jeconnoc
editor: ''
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Kubernetes, DC/OS, Azure
ms.assetid: ''
ms.service: container-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: nepeters
ms.openlocfilehash: 1e5ca9fb44ea3ad15206f36a16e61f2865d79f5f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864853"
---
# <a name="scale-an-azure-container-service-cluster"></a>Scale an Azure Container Service Cluster

This sample scales and Azure Container Service. 

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Sample script

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a>Clean up deployment 

Run the following command to remove the resource group, VM, and all related resources.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Script explanation

This script uses the following commands to create the deployment. Each item in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [az acs scale](/cli/azure/acs#az-acs-scale) | Scale an ACS cluster. |

## <a name="next-steps"></a>Next steps

For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).

Additional Azure Container Service CLI script samples can be found in the [Azure Container Service documentation](../cli-samples.md).

