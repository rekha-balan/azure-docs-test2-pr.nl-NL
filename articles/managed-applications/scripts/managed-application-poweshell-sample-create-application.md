---
title: Azure PowerShell script sample - Deploy a managed application | Microsoft Docs
description: Azure PowerShell script sample - Deploy a managed application definition
services: managed-applications
documentationcenter: na
author: tfitzmac
manager: timlt
ms.service: managed-applications
ms.devlang: powershell
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/27/2017
ms.author: tomfitz
ms.openlocfilehash: 2429d561beffed5bc171b9dbc2c2c9c88eba3313
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856403"
---
# <a name="deploy-a-managed-application-for-a-service-catalog-with-powershell"></a>Deploy a managed application for a service catalog with PowerShell

This script deploys a managed application definition from the service catalog.


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Sample script

[!code-powershell[main](../../../powershell_scripts/managed-applications/create-application/create-application.ps1 "Create application")]


## <a name="script-explanation"></a>Script explanation

This script uses the following command to deploy the managed application. Each command in the table links to command-specific documentation.

| Command | Notes |
|---|---|
| [New-AzureRmManagedApplication](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermmanagedapplication) | Create a managed application. Provide the definition ID and parameters for the template. |


## <a name="next-steps"></a>Next steps

* For an introduction to managed applications, see [Azure Managed Application overview](../overview.md).
* For more information on PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/get-started-azureps).
