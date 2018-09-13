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
# <a name="use-an-azure-powershell-command-to-create-an-empty-cloud-service-container"></a><span data-ttu-id="a0425-104">Use an Azure PowerShell command to create an empty cloud service container</span><span class="sxs-lookup"><span data-stu-id="a0425-104">Use an Azure PowerShell command to create an empty cloud service container</span></span>
<span data-ttu-id="a0425-105">This article explains how to quickly create a Cloud Services container using Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="a0425-105">This article explains how to quickly create a Cloud Services container using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="a0425-106">Please follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="a0425-106">Please follow the steps below:</span></span>

1. <span data-ttu-id="a0425-107">Install the Microsoft Azure PowerShell cmdlet from the [Azure PowerShell downloads](http://aka.ms/webpi-azps) page.</span><span class="sxs-lookup"><span data-stu-id="a0425-107">Install the Microsoft Azure PowerShell cmdlet from the [Azure PowerShell downloads](http://aka.ms/webpi-azps) page.</span></span>
2. <span data-ttu-id="a0425-108">Open the PowerShell command prompt.</span><span class="sxs-lookup"><span data-stu-id="a0425-108">Open the PowerShell command prompt.</span></span>
3. <span data-ttu-id="a0425-109">Use the [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) to sign in.</span><span class="sxs-lookup"><span data-stu-id="a0425-109">Use the [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) to sign in.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a0425-110">For further instruction on installing the Azure PowerShell cmdlet and connecting to your Azure subscription, refer to [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="a0425-110">For further instruction on installing the Azure PowerShell cmdlet and connecting to your Azure subscription, refer to [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
   >
   >
4. <span data-ttu-id="a0425-111">Use the **New-AzureService** cmdlet to create an empty Azure cloud service container.</span><span class="sxs-lookup"><span data-stu-id="a0425-111">Use the **New-AzureService** cmdlet to create an empty Azure cloud service container.</span></span>

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. <span data-ttu-id="a0425-112">Follow this example to invoke the cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a0425-112">Follow this example to invoke the cmdlet:</span></span>

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

<span data-ttu-id="a0425-113">For more information about creating the Azure cloud service, run:</span><span class="sxs-lookup"><span data-stu-id="a0425-113">For more information about creating the Azure cloud service, run:</span></span>

```
Get-help New-AzureService
```

### <a name="next-steps"></a><span data-ttu-id="a0425-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="a0425-114">Next steps</span></span>
* <span data-ttu-id="a0425-115">To manage the cloud service deployment, refer to the [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), and [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commands.</span><span class="sxs-lookup"><span data-stu-id="a0425-115">To manage the cloud service deployment, refer to the [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), and [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commands.</span></span> <span data-ttu-id="a0425-116">You may also refer to [How to configure cloud services](cloud-services-how-to-configure.md) for further information.</span><span class="sxs-lookup"><span data-stu-id="a0425-116">You may also refer to [How to configure cloud services](cloud-services-how-to-configure.md) for further information.</span></span>
* <span data-ttu-id="a0425-117">To publish your cloud service project to Azure, refer to the  **PublishCloudService.ps1** code sample from [Continuous delivery for cloud service in Azure](cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="a0425-117">To publish your cloud service project to Azure, refer to the  **PublishCloudService.ps1** code sample from [Continuous delivery for cloud service in Azure](cloud-services-dotnet-continuous-delivery.md).</span></span>
