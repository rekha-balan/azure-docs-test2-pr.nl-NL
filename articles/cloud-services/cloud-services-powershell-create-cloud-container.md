---
title: Create a cloud service container with PowerShell | Microsoft Docs
description: This article explains how to create a cloud service container with PowerShell. The container hosts web and worker roles.
services: cloud-services
documentationcenter: .net
author: cawaMS
manager: timlt
editor: ''
ms.assetid: c8f32469-610e-4f37-a3aa-4fac5c714e13
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 89e517a17417475f975dbaa0cee8517145a7c6c3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549348"
---
# <a name="use-an-azure-powershell-command-to-create-an-empty-cloud-service-container"></a>Use an Azure PowerShell command to create an empty cloud service container
This article explains how to quickly create a Cloud Services container using Azure PowerShell cmdlets. Please follow the steps below:

1. Install the Microsoft Azure PowerShell cmdlet from the [Azure PowerShell downloads](http://aka.ms/webpi-azps) page.
2. Open the PowerShell command prompt.
3. Use the [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) to sign in.

   > [!NOTE]
   > For further instruction on installing the Azure PowerShell cmdlet and connecting to your Azure subscription, refer to [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).
   >
   >
4. Use the **New-AzureService** cmdlet to create an empty Azure cloud service container.

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. Follow this example to invoke the cmdlet:

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

For more information about creating the Azure cloud service, run:

```
Get-help New-AzureService
```

### <a name="next-steps"></a>Next steps
* To manage the cloud service deployment, refer to the [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), and [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commands. You may also refer to [How to configure cloud services](cloud-services-how-to-configure.md) for further information.
* To publish your cloud service project to Azure, refer to the  **PublishCloudService.ps1** code sample from [Continuous delivery for cloud service in Azure](cloud-services-dotnet-continuous-delivery.md).