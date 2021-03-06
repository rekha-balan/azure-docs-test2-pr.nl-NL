---
title: Azure CLI Script Example - Create an Azure Event Grid subscription | Microsoft Docs
description: The Azure CLI script in this topic shows how to create an account level Event Grid subscription for Job State Changes.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: ''
ms.service: media-services
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/11/2018
ms.author: juliako
ms.openlocfilehash: 5293ac55fdb13bba85996f5ed81034d4ebeeff12
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856431"
---
# <a name="cli-example-create-an-azure-event-grid-subscription"></a>CLI example: Create an Azure Event Grid subscription 

The Azure CLI script in this article shows how to create an account level Event Grid subscription for Job State Changes.

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0.20 or later. Run `az --version` to find the version. If you need to install or upgrade, see [Install the Azure CLI](/cli/azure/install-azure-cli). 

## <a name="example-script"></a>Example script

[!code-azurecli-interactive[main](../../../../cli_scripts/media-services/create-event-grid/Create-EventGrid.sh "Create an EventGrid subscription")]

## <a name="next-steps"></a>Next steps

For more examples, see [Azure CLI samples](../cli-samples.md).
