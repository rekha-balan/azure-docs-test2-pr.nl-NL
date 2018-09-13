---
title: Azure PowerShell Script Sample - Create a scheduled backup for a web app | Microsoft Docs
description: Azure PowerShell Script Sample - Create a scheduled backup for a web app
services: app-service\web
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
tags: azure-service-management
ms.assetid: a2a27d94-d378-4c17-a6a9-ae1e69dc4a72
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 10/30/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: b2e5b66e93f94085484658f4cc43141354910e3a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869291"
---
# <a name="create-a-scheduled-backup-for-a-web-app"></a>Create a scheduled backup for a web app

This sample script creates a web app in App Service with its related resources, and then creates a scheduled backup for it. 

If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure. 

## <a name="sample-script"></a>Sample script

[!code-azurepowershell-interactive[main](../../../powershell_scripts/app-service/backup-scheduled/backup-scheduled.ps1?highlight=1-4 "Create a scheduled backup for a web app")]

## <a name="clean-up-deployment"></a>Clean up deployment 

After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a>Script explanation

This script uses the following commands. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Creates a resource group in which all resources are stored. |
| [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) | Creates a Storage account. |
| [New-AzureStorageContainer](/powershell/module/azure.storage/new-azurestoragecontainer) | Creates an Azure storage container. |
| [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) | Generates an SAS token for an Azure storage container. |
| [New-AzureRmAppServicePlan](/powershell/module/azurerm.websites/new-azurermappserviceplan) | Creates an App Service plan. |
| [New-AzureRmWebApp](/powershell/module/azurerm.websites/new-azurermwebapp) | Creates a web app. |
| [Edit-AzureRmWebAppBackupConfiguration](/powershell/module/azurerm.websites/edit-azurermwebappbackupconfiguration) | Edits the backup configuration for web app. |
| [Get-AzureRmWebAppBackupList](/powershell/module/azurerm.websites/get-azurermwebappbackuplist) | Gets a list of backups for a web app. |
| [Get-AzureRmWebAppBackupConfiguration](/powershell/module/azurerm.websites/get-azurermwebappbackupconfiguration) | Gets the backup configuration for web app. |

## <a name="next-steps"></a>Next steps

For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).

Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).
