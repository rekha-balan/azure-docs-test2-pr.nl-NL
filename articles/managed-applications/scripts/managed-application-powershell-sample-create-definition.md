---
title: Azure PowerShell script sample - Create a managed application definition | Microsoft Docs
description: Azure PowerShell script sample - Create a managed application definition
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
ms.openlocfilehash: ee721b7c68924f5e05fbdc4bc4b919837d4cc05b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869820"
---
# <a name="create-a-managed-application-definition-with-powershell"></a>Create a managed application definition with PowerShell

This script publishes a managed application definition to a service catalog.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Sample script

[!code-powershell[main](../../../powershell_scripts/managed-applications/create-definition/create-definition.ps1 "Create definition")]


## <a name="script-explanation"></a>Script explanation

This script uses the following command to create the managed application definition. Each command in the table links to command-specific documentation.

| Command | Notes |
|---|---|
| [New-AzureRmManagedApplicationDefinition](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermmanagedapplicationdefinition) | Create a managed application definition. Provide the package that contains the required files. |


## <a name="next-steps"></a>Next steps

* For an introduction to managed applications, see [Azure Managed Application overview](../overview.md).
* For more information on PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/get-started-azureps).
