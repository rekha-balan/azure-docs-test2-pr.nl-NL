---
title: Azure Cloud Shell usage data for LUIS
titleSuffix: Azure Cognitive Services
description: Learn how to get usage information in Azure Cloud Shell for LUIS.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 09/06/2017
ms.author: diberry
ms.openlocfilehash: 95bd1e83b4a0ed08850862ec4f4addb3353a9481
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867785"
---
# <a name="usage-data-for-luis-service-from-azure-cloud-shell"></a><span data-ttu-id="d6f12-103">Usage data for LUIS service from Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="d6f12-103">Usage data for LUIS service from Azure Cloud Shell</span></span>
<span data-ttu-id="d6f12-104">The Azure portal allows you to use PowerShell cmdlets to work with LUIS resources.</span><span class="sxs-lookup"><span data-stu-id="d6f12-104">The Azure portal allows you to use PowerShell cmdlets to work with LUIS resources.</span></span> 

<span data-ttu-id="d6f12-105">These cmdlets allow you to [create](https://docs.microsoft.com/powershell/module/azurerm.cognitiveservices/new-azurermcognitiveservicesaccount?view=azurermps-6.0.0) a LUIS subscription, get information about the subscription, including [usage](https://docs.microsoft.com/powershell/module/azurerm.cognitiveservices/get-azurermcognitiveservicesaccountusage?view=azurermps-6.0.0), and [remove](https://docs.microsoft.com/powershell/module/azurerm.cognitiveservices/remove-azurermcognitiveservicesaccount?view=azurermps-6.0.0) the subscription.</span><span class="sxs-lookup"><span data-stu-id="d6f12-105">These cmdlets allow you to [create](https://docs.microsoft.com/powershell/module/azurerm.cognitiveservices/new-azurermcognitiveservicesaccount?view=azurermps-6.0.0) a LUIS subscription, get information about the subscription, including [usage](https://docs.microsoft.com/powershell/module/azurerm.cognitiveservices/get-azurermcognitiveservicesaccountusage?view=azurermps-6.0.0), and [remove](https://docs.microsoft.com/powershell/module/azurerm.cognitiveservices/remove-azurermcognitiveservicesaccount?view=azurermps-6.0.0) the subscription.</span></span> 

## <a name="cloud-shell-storage-account-and-authentication"></a><span data-ttu-id="d6f12-106">Cloud shell storage account and authentication</span><span class="sxs-lookup"><span data-stu-id="d6f12-106">Cloud shell storage account and authentication</span></span>
<span data-ttu-id="d6f12-107">In order to use PowerShell in the Azure portal [cloud shell](https://docs.microsoft.com/azure/cloud-shell/quickstart-powershell), you need to have an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="d6f12-107">In order to use PowerShell in the Azure portal [cloud shell](https://docs.microsoft.com/azure/cloud-shell/quickstart-powershell), you need to have an Azure storage account.</span></span> <span data-ttu-id="d6f12-108">If you don't have a [storage account](https://docs.microsoft.com/azure/cloud-shell/persisting-shell-storage#set-up-a-clouddrive-file-share), you will be prompted to create one.</span><span class="sxs-lookup"><span data-stu-id="d6f12-108">If you don't have a [storage account](https://docs.microsoft.com/azure/cloud-shell/persisting-shell-storage#set-up-a-clouddrive-file-share), you will be prompted to create one.</span></span> <span data-ttu-id="d6f12-109">The storage account allows you to save PowerShell scripts in the cloud shell.</span><span class="sxs-lookup"><span data-stu-id="d6f12-109">The storage account allows you to save PowerShell scripts in the cloud shell.</span></span>  

<span data-ttu-id="d6f12-110">You also need to authenticate to Azure in the cloud shell to access any resources.</span><span class="sxs-lookup"><span data-stu-id="d6f12-110">You also need to authenticate to Azure in the cloud shell to access any resources.</span></span> 

<span data-ttu-id="d6f12-111">Once you have a storage account and are authenticated, you can run PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="d6f12-111">Once you have a storage account and are authenticated, you can run PowerShell cmdlets.</span></span>

## <a name="open-cloud-shell"></a><span data-ttu-id="d6f12-112">Open Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="d6f12-112">Open Cloud Shell</span></span>
<span data-ttu-id="d6f12-113">When you use the Azure portal cloud shell, you are always on the most current PowerShell version.</span><span class="sxs-lookup"><span data-stu-id="d6f12-113">When you use the Azure portal cloud shell, you are always on the most current PowerShell version.</span></span> 

<span data-ttu-id="d6f12-114">Use the **Launch Cloud Shell**  button to open the Cloud Shell or open a browser with [https://shell.azure.com](https://shell.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d6f12-114">Use the **Launch Cloud Shell**  button to open the Cloud Shell or open a browser with [https://shell.azure.com](https://shell.azure.com).</span></span> 

<a style="cursor:pointer" onclick='javascript:window.open("https://shell.azure.com", "_blank", "toolbar=no,scrollbars=yes,resizable=yes,menubar=no,location=no,status=no")'><image src="https://shell.azure.com/images/launchcloudshell.png" /></a>

## <a name="luis-endpoint-usage-information"></a><span data-ttu-id="d6f12-115">LUIS endpoint usage information</span><span class="sxs-lookup"><span data-stu-id="d6f12-115">LUIS endpoint usage information</span></span>

<span data-ttu-id="d6f12-116">The PowerShell 6.x cmdlet, `Get-AzureRmCognitiveServicesAccountUsage`, provides usage information for Microsoft Cognitive Services including LUIS.</span><span class="sxs-lookup"><span data-stu-id="d6f12-116">The PowerShell 6.x cmdlet, `Get-AzureRmCognitiveServicesAccountUsage`, provides usage information for Microsoft Cognitive Services including LUIS.</span></span> <span data-ttu-id="d6f12-117">[Get-AzureRmCognitiveServicesAccountUsage](https://docs.microsoft.com/powershell/module/azurerm.cognitiveservices/get-azurermcognitiveservicesaccountusage?view=azurermps-6.0.0) requires the resource group and resource name of the service.</span><span class="sxs-lookup"><span data-stu-id="d6f12-117">[Get-AzureRmCognitiveServicesAccountUsage](https://docs.microsoft.com/powershell/module/azurerm.cognitiveservices/get-azurermcognitiveservicesaccountusage?view=azurermps-6.0.0) requires the resource group and resource name of the service.</span></span> 

<span data-ttu-id="d6f12-118">The command syntax is:</span><span class="sxs-lookup"><span data-stu-id="d6f12-118">The command syntax is:</span></span>

```
Get-AzureRmCognitiveServicesAccountUsage -ResourceGroupName my-resource-group -Name my-luis-service-name
```

<span data-ttu-id="d6f12-119">In the following example, the resource group name is `luis-westus-rg` and the LUIS service subscription name is `luis-westus-1`.</span><span class="sxs-lookup"><span data-stu-id="d6f12-119">In the following example, the resource group name is `luis-westus-rg` and the LUIS service subscription name is `luis-westus-1`.</span></span> <span data-ttu-id="d6f12-120">Both these names are chosen when the LUIS service is created.</span><span class="sxs-lookup"><span data-stu-id="d6f12-120">Both these names are chosen when the LUIS service is created.</span></span> 

<span data-ttu-id="d6f12-121">The cmdlet returns usage information of 16 of 10,000 endpoint hits used in a 30 day period with the period ending on June 7 :</span><span class="sxs-lookup"><span data-stu-id="d6f12-121">The cmdlet returns usage information of 16 of 10,000 endpoint hits used in a 30 day period with the period ending on June 7 :</span></span>

```
CurrentValue  : 16
Name          : LUIS.Calls
Limit         : 10000
Status        : Included
Unit          : Count
QuotaPeriod   : 30.00:00:00
NextResetTime : 2018-06-07T18:28:52Z
```

<span data-ttu-id="d6f12-122">Save the command as a PowerShell file, \*.ps1, in the Azure storage account associated with the cloud shell and execute at any time.</span><span class="sxs-lookup"><span data-stu-id="d6f12-122">Save the command as a PowerShell file, \*.ps1, in the Azure storage account associated with the cloud shell and execute at any time.</span></span> 

![Run script from storage](./media/luis-how-to-manage-from-powershell/run-script-from-storage.png)

<span data-ttu-id="d6f12-124">Once the script is saved on the cloud drive, you can run the PowerShell script from the Azure phone app's cloud shell.</span><span class="sxs-lookup"><span data-stu-id="d6f12-124">Once the script is saved on the cloud drive, you can run the PowerShell script from the Azure phone app's cloud shell.</span></span> 

![Run script from storage in phone app](./media/luis-how-to-manage-from-powershell/phone-app.png)