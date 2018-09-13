---
title: include file
description: include file
ms.custom: include file
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.component: azds-kubernetes
author: ghogen
ms.author: ghogen
ms.date: 05/11/2018
ms.topic: include
manager: douge
ms.openlocfilehash: b8b8b1a593328197c61f8edba9f8f849518dd2e5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45180387"
---
## <a name="clean-up"></a><span data-ttu-id="ea0c9-103">Clean up</span><span class="sxs-lookup"><span data-stu-id="ea0c9-103">Clean up</span></span>
<span data-ttu-id="ea0c9-104">To completely delete an Azure Dev Spaces instance on a cluster, including all the dev spaces and running services within it, use the `az aks remove-dev-spaces` command.</span><span class="sxs-lookup"><span data-stu-id="ea0c9-104">To completely delete an Azure Dev Spaces instance on a cluster, including all the dev spaces and running services within it, use the `az aks remove-dev-spaces` command.</span></span> <span data-ttu-id="ea0c9-105">Bear in mind that this action is irreversible.</span><span class="sxs-lookup"><span data-stu-id="ea0c9-105">Bear in mind that this action is irreversible.</span></span> <span data-ttu-id="ea0c9-106">You can add support for Azure Dev Spaces again on the cluster, but it will be as if you are starting again.</span><span class="sxs-lookup"><span data-stu-id="ea0c9-106">You can add support for Azure Dev Spaces again on the cluster, but it will be as if you are starting again.</span></span> <span data-ttu-id="ea0c9-107">Your old services and spaces won't be restored.</span><span class="sxs-lookup"><span data-stu-id="ea0c9-107">Your old services and spaces won't be restored.</span></span>

<span data-ttu-id="ea0c9-108">The following example lists the Azure Dev Spaces controllers in your active subscription, and then deletes the Azure Dev Spaces controller that is associated with AKS cluster 'myaks' in resource group 'myaks-rg'.</span><span class="sxs-lookup"><span data-stu-id="ea0c9-108">The following example lists the Azure Dev Spaces controllers in your active subscription, and then deletes the Azure Dev Spaces controller that is associated with AKS cluster 'myaks' in resource group 'myaks-rg'.</span></span>

```cmd
    azds controller list
    az aks remove-dev-spaces --name myaks --resource-group myaks-rg
```

