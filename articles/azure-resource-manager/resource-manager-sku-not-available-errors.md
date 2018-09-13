---
title: Azure SKU not available errors | Microsoft Docs
description: Describes how to troubleshoot the SKU not available error during deployment.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: ''
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: troubleshooting
ms.date: 03/09/2018
ms.author: tomfitz
ms.openlocfilehash: 490c912a6abd6570c9bc74de8b86a516a8e6f807
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967452"
---
# <a name="resolve-errors-for-sku-not-available"></a><span data-ttu-id="a9b6e-103">Resolve errors for SKU not available</span><span class="sxs-lookup"><span data-stu-id="a9b6e-103">Resolve errors for SKU not available</span></span>

<span data-ttu-id="a9b6e-104">This article describes how to resolve the **SkuNotAvailable** error.</span><span class="sxs-lookup"><span data-stu-id="a9b6e-104">This article describes how to resolve the **SkuNotAvailable** error.</span></span>

## <a name="symptom"></a><span data-ttu-id="a9b6e-105">Symptom</span><span class="sxs-lookup"><span data-stu-id="a9b6e-105">Symptom</span></span>

<span data-ttu-id="a9b6e-106">When deploying a resource (typically a virtual machine), you receive the following error code and error message:</span><span class="sxs-lookup"><span data-stu-id="a9b6e-106">When deploying a resource (typically a virtual machine), you receive the following error code and error message:</span></span>

```
Code: SkuNotAvailable
Message: The requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy to a different location.
```

## <a name="cause"></a><span data-ttu-id="a9b6e-107">Cause</span><span class="sxs-lookup"><span data-stu-id="a9b6e-107">Cause</span></span>

<span data-ttu-id="a9b6e-108">You receive this error when the resource SKU you have selected (such as VM size) is not available for the location you have selected.</span><span class="sxs-lookup"><span data-stu-id="a9b6e-108">You receive this error when the resource SKU you have selected (such as VM size) is not available for the location you have selected.</span></span>

## <a name="solution-1---powershell"></a><span data-ttu-id="a9b6e-109">Solution 1 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9b6e-109">Solution 1 - PowerShell</span></span>

<span data-ttu-id="a9b6e-110">To determine which SKUs are available in a region, use the [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) command.</span><span class="sxs-lookup"><span data-stu-id="a9b6e-110">To determine which SKUs are available in a region, use the [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) command.</span></span> <span data-ttu-id="a9b6e-111">Filter the results by location.</span><span class="sxs-lookup"><span data-stu-id="a9b6e-111">Filter the results by location.</span></span> <span data-ttu-id="a9b6e-112">You must have the latest version of PowerShell for this command.</span><span class="sxs-lookup"><span data-stu-id="a9b6e-112">You must have the latest version of PowerShell for this command.</span></span>

```powershell
Get-AzureRmComputeResourceSku | where {$_.Locations -icontains "southcentralus"}
```

<span data-ttu-id="a9b6e-113">The results include a list of SKUs for the location and any restrictions for that SKU.</span><span class="sxs-lookup"><span data-stu-id="a9b6e-113">The results include a list of SKUs for the location and any restrictions for that SKU.</span></span>

```powershell
ResourceType                Name      Locations Restriction                      Capability Value
------------                ----      --------- -----------                      ---------- -----
availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
virtualMachines      Standard_A0 southcentralus
virtualMachines      Standard_A1 southcentralus
virtualMachines      Standard_A2 southcentralus
```

## <a name="solution-2---azure-cli"></a><span data-ttu-id="a9b6e-114">Solution 2 - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a9b6e-114">Solution 2 - Azure CLI</span></span>

<span data-ttu-id="a9b6e-115">To determine which SKUs are available in a region, use the `az vm list-skus` command.</span><span class="sxs-lookup"><span data-stu-id="a9b6e-115">To determine which SKUs are available in a region, use the `az vm list-skus` command.</span></span> <span data-ttu-id="a9b6e-116">You can then use `grep` or a similar utility to filter the output.</span><span class="sxs-lookup"><span data-stu-id="a9b6e-116">You can then use `grep` or a similar utility to filter the output.</span></span>

```bash
$ az vm list-skus --output table
ResourceType      Locations           Name                    Capabilities                       Tier      Size           Restrictions
----------------  ------------------  ----------------------  ---------------------------------  --------  -------------  ---------------------------
availabilitySets  eastus              Classic                 MaximumPlatformFaultDomainCount=3
avilabilitySets   eastus              Aligned                 MaximumPlatformFaultDomainCount=3
availabilitySets  eastus2             Classic                 MaximumPlatformFaultDomainCount=3
availabilitySets  eastus2             Aligned                 MaximumPlatformFaultDomainCount=3
availabilitySets  westus              Classic                 MaximumPlatformFaultDomainCount=3
availabilitySets  westus              Aligned                 MaximumPlatformFaultDomainCount=3
availabilitySets  centralus           Classic                 MaximumPlatformFaultDomainCount=3
availabilitySets  centralus           Aligned                 MaximumPlatformFaultDomainCount=3
```

## <a name="solution-3---azure-portal"></a><span data-ttu-id="a9b6e-117">Solution 3 - Azure portal</span><span class="sxs-lookup"><span data-stu-id="a9b6e-117">Solution 3 - Azure portal</span></span>

<span data-ttu-id="a9b6e-118">To determine which SKUs are available in a region, use the [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a9b6e-118">To determine which SKUs are available in a region, use the [portal](https://portal.azure.com).</span></span> <span data-ttu-id="a9b6e-119">Log in to the portal, and add a resource through the interface.</span><span class="sxs-lookup"><span data-stu-id="a9b6e-119">Log in to the portal, and add a resource through the interface.</span></span> <span data-ttu-id="a9b6e-120">As you set the values, you see the available SKUs for that resource.</span><span class="sxs-lookup"><span data-stu-id="a9b6e-120">As you set the values, you see the available SKUs for that resource.</span></span> <span data-ttu-id="a9b6e-121">You do not need to complete the deployment.</span><span class="sxs-lookup"><span data-stu-id="a9b6e-121">You do not need to complete the deployment.</span></span>

![available SKUs](./media/resource-manager-sku-not-available-errors/view-sku.png)

## <a name="solution-4---rest"></a><span data-ttu-id="a9b6e-123">Solution 4 - REST</span><span class="sxs-lookup"><span data-stu-id="a9b6e-123">Solution 4 - REST</span></span>

<span data-ttu-id="a9b6e-124">To determine which SKUs are available in a region, use the REST API for virtual machines.</span><span class="sxs-lookup"><span data-stu-id="a9b6e-124">To determine which SKUs are available in a region, use the REST API for virtual machines.</span></span> <span data-ttu-id="a9b6e-125">Send the following request:</span><span class="sxs-lookup"><span data-stu-id="a9b6e-125">Send the following request:</span></span>

```HTTP 
GET
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
```

<span data-ttu-id="a9b6e-126">It returns available SKUs and regions in the following format:</span><span class="sxs-lookup"><span data-stu-id="a9b6e-126">It returns available SKUs and regions in the following format:</span></span>

```json
{
  "value": [
    {
      "resourceType": "virtualMachines",
      "name": "Standard_A0",
      "tier": "Standard",
      "size": "A0",
      "locations": [
        "eastus"
      ],
      "restrictions": []
    },
    {
      "resourceType": "virtualMachines",
      "name": "Standard_A1",
      "tier": "Standard",
      "size": "A1",
      "locations": [
        "eastus"
      ],
      "restrictions": []
    },
    ...
  ]
}
```

<span data-ttu-id="a9b6e-127">If you are unable to find a suitable SKU in that region or an alternative region that meets your business needs, submit a [SKU request](https://aka.ms/skurestriction) to Azure Support.</span><span class="sxs-lookup"><span data-stu-id="a9b6e-127">If you are unable to find a suitable SKU in that region or an alternative region that meets your business needs, submit a [SKU request](https://aka.ms/skurestriction) to Azure Support.</span></span>
