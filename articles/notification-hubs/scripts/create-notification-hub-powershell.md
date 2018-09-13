---
title: 'PowerShell script: Create an Azure notification hub | Microsoft Docs'
description: This PowerShell script creates an Azure notification hub.
services: data-factory
author: dimazaid
manager: kpiteira
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2018
ms.author: dimazaid
ms.openlocfilehash: 747d743a0573bd959b4d3c7100be8ae9451c5ed5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870846"
---
# <a name="use-powershell-to-create-an-azure-notification-hub"></a><span data-ttu-id="c7758-103">Use PowerShell to create an Azure notification hub</span><span class="sxs-lookup"><span data-stu-id="c7758-103">Use PowerShell to create an Azure notification hub</span></span>

<span data-ttu-id="c7758-104">This sample PowerShell script creates a sample Azure notification hub.</span><span class="sxs-lookup"><span data-stu-id="c7758-104">This sample PowerShell script creates a sample Azure notification hub.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="prerequisites"></a><span data-ttu-id="c7758-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c7758-105">Prerequisites</span></span>
* <span data-ttu-id="c7758-106">**Azure subscription** - If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="c7758-106">**Azure subscription** - If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="sample-script"></a><span data-ttu-id="c7758-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="c7758-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/notification-hubs/create-notification-hub/create-notification-hub.ps1 "Create a notification hub")]


## <a name="clean-up-deployment"></a><span data-ttu-id="c7758-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="c7758-108">Clean up deployment</span></span>

<span data-ttu-id="c7758-109">After you run the sample script, you can use the following command to remove the resource group and all resources associated with it:</span><span class="sxs-lookup"><span data-stu-id="c7758-109">After you run the sample script, you can use the following command to remove the resource group and all resources associated with it:</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourceGroupName
```

## <a name="script-explanation"></a><span data-ttu-id="c7758-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="c7758-110">Script explanation</span></span>

<span data-ttu-id="c7758-111">This script uses the following commands:</span><span class="sxs-lookup"><span data-stu-id="c7758-111">This script uses the following commands:</span></span> 

| <span data-ttu-id="c7758-112">Command</span><span class="sxs-lookup"><span data-stu-id="c7758-112">Command</span></span> | <span data-ttu-id="c7758-113">Notes</span><span class="sxs-lookup"><span data-stu-id="c7758-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c7758-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c7758-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c7758-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="c7758-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c7758-116">New-AzureRmNotificationHubsNamespace</span><span class="sxs-lookup"><span data-stu-id="c7758-116">New-AzureRmNotificationHubsNamespace</span></span>](/powershell/module//azurerm.notificationhubs/new-azurermnotificationhubsnamespace) | <span data-ttu-id="c7758-117">Creates a namespace for the notification hub.</span><span class="sxs-lookup"><span data-stu-id="c7758-117">Creates a namespace for the notification hub.</span></span> |
| [<span data-ttu-id="c7758-118">New-AzureRmNotificationHub</span><span class="sxs-lookup"><span data-stu-id="c7758-118">New-AzureRmNotificationHub</span></span>](/powershell/module//azurerm.notificationhubs/new-azurermnotificationhubsnamespace) | <span data-ttu-id="c7758-119">Creates a notification hub.</span><span class="sxs-lookup"><span data-stu-id="c7758-119">Creates a notification hub.</span></span> |
| [<span data-ttu-id="c7758-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c7758-120">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="c7758-121">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="c7758-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="c7758-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="c7758-122">Next steps</span></span>

<span data-ttu-id="c7758-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="c7758-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>
