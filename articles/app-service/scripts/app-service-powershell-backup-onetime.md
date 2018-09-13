---
title: Azure PowerShell Script Sample - Back up a web app | Microsoft Docs
description: Azure PowerShell Script Sample - Back up a web app
services: app-service\web
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
tags: azure-service-management
ms.assetid: fc755f82-ca3e-4532-b251-690b699324d6
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 10/30/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 1b10de7b102ea2e8e55d48fa9753dbe115e2016b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857770"
---
# <a name="back-up-a-web-app"></a>Back up a web app

This sample script creates a web app in App Service with its related resources, and then creates a one-time backup for it. 

If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Connect-AzureRmAccount` to create a connection with Azure. 

## <a name="sample-script"></a>Sample script

[!code-azurepowershell-interactive[main](../../../powershell_scripts/app-service/backup-onetime/backup-onetime.ps1?highlight=1-5 "Back up a web app")]

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
| [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) | Generates an SAS token for an Azure storage container.  |
| [New-AzureRmAppServicePlan](/powershell/module/azurerm.websites/new-azurermappserviceplan) | Creates an App Service plan. |
| [New-AzureRmWebApp](/powershell/module/azurerm.websites/new-azurermwebapp) | Creates a web app. |
| [New-AzureRmWebAppBackup](/powershell/module/azurerm.websites/new-azurermwebappbackup) | Creates a backup for a web app. |
| [Get-AzureRmWebAppBackupList](/powershell/module/azurerm.websites/get-azurermwebappbackuplist) | Gets a list of backups for a web app. |

## <a name="next-steps"></a>Next steps

For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).

Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).
