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
ms.openlocfilehash: a8f5adc8e6745fdbfd31d1a9cb9407672d61da07
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45181266"
---
### <a name="configure-your-aks-cluster-to-use-azure-dev-spaces"></a>Configure your AKS cluster to use Azure Dev Spaces

Open a command window and enter the following Azure CLI command, using the resource group that contains your AKS cluster, and your AKS cluster name. The command configures your cluster with support for Azure Dev Spaces.

   ```cmd
   az aks use-dev-spaces -g MyResourceGroup -n MyAKS
   ```

