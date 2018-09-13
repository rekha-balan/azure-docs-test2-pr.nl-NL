---
title: Reverse DNS records for your classic Azure services using PowerShell | Microsoft Docs
description: Azure DNS allows you to manage reverse DNS records or PTR records for Azure services using PowerShell in the classic deployment model.
services: DNS
documentationcenter: na
author: s-malone
manager: carmonm
editor: ''
tags: azure-service-management
ms.assetid: 9c24d176-6bce-4277-a14c-80fe44a20a87
ms.service: DNS
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/28/2016
ms.author: smalone
ms.openlocfilehash: 399cfcad5c17cdb12a4063e11e1ff353e88e56a7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555972"
---
# <a name="how-to-manage-reverse-dns-records-for-your-azure-services-classic-using-azure-powershell"></a><span data-ttu-id="5767e-103">How to manage reverse DNS records for your Azure services (classic) using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5767e-103">How to manage reverse DNS records for your Azure services (classic) using Azure PowerShell</span></span>

[!INCLUDE [dns-reverse-dns-record-operations-arm-selectors-include.md](../../includes/dns-reverse-dns-record-operations-arm-selectors-include.md)]


[!INCLUDE [DNS-reverse-dns-record-operations-intro-include.md](../../includes/dns-reverse-dns-record-operations-intro-include.md)]


> [!IMPORTANT]
> <span data-ttu-id="5767e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5767e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5767e-105">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="5767e-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="5767e-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="5767e-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="5767e-107">Learn how to [perform these steps using the Resource Manager model](dns-reverse-dns-record-operations-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5767e-107">Learn how to [perform these steps using the Resource Manager model](dns-reverse-dns-record-operations-ps.md).</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="5767e-108">Validation of reverse DNS records</span><span class="sxs-lookup"><span data-stu-id="5767e-108">Validation of reverse DNS records</span></span>
<span data-ttu-id="5767e-109">To ensure a third party can’t create reverse DNS records mapping to your DNS domains, Azure only allows the creation of a reverse DNS record where one of the following is true:</span><span class="sxs-lookup"><span data-stu-id="5767e-109">To ensure a third party can’t create reverse DNS records mapping to your DNS domains, Azure only allows the creation of a reverse DNS record where one of the following is true:</span></span>

* <span data-ttu-id="5767e-110">The reverse DNS FQDN is the name of the Cloud Service for which it has been specified, or any Cloud Service name within the same subscription e.g., reverse DNS is "contosoapp1.cloudapp.net.".</span><span class="sxs-lookup"><span data-stu-id="5767e-110">The reverse DNS FQDN is the name of the Cloud Service for which it has been specified, or any Cloud Service name within the same subscription e.g., reverse DNS is "contosoapp1.cloudapp.net.".</span></span>
* <span data-ttu-id="5767e-111">The reverse DNS FQDN forward resolves to the name or IP of the Cloud Service for which it has been specified, or to any Cloud Service name or IP within the same subscription e.g., reverse DNS is "app1.contoso.com."</span><span class="sxs-lookup"><span data-stu-id="5767e-111">The reverse DNS FQDN forward resolves to the name or IP of the Cloud Service for which it has been specified, or to any Cloud Service name or IP within the same subscription e.g., reverse DNS is "app1.contoso.com."</span></span> <span data-ttu-id="5767e-112">which is a CName alias for contosoapp1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="5767e-112">which is a CName alias for contosoapp1.cloudapp.net.</span></span>

<span data-ttu-id="5767e-113">Validation checks are only performed when the reverse DNS property for a Cloud Service is set or modified.</span><span class="sxs-lookup"><span data-stu-id="5767e-113">Validation checks are only performed when the reverse DNS property for a Cloud Service is set or modified.</span></span> <span data-ttu-id="5767e-114">Periodic re-validation is not performed.</span><span class="sxs-lookup"><span data-stu-id="5767e-114">Periodic re-validation is not performed.</span></span>

## <a name="add-reverse-dns-to-existing-cloud-services"></a><span data-ttu-id="5767e-115">Add reverse DNS to existing Cloud Services</span><span class="sxs-lookup"><span data-stu-id="5767e-115">Add reverse DNS to existing Cloud Services</span></span>
<span data-ttu-id="5767e-116">You can add a reverse DNS record to an existing Cloud Service using the "Set-AzureService" cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5767e-116">You can add a reverse DNS record to an existing Cloud Service using the "Set-AzureService" cmdlet:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

## <a name="create-a-cloud-service-with-reverse-dns"></a><span data-ttu-id="5767e-117">Create a Cloud Service with reverse DNS</span><span class="sxs-lookup"><span data-stu-id="5767e-117">Create a Cloud Service with reverse DNS</span></span>
<span data-ttu-id="5767e-118">You can add a new Cloud Service with the reverse DNS property specified using the "Set-AzureService" cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5767e-118">You can add a new Cloud Service with the reverse DNS property specified using the "Set-AzureService" cmdlet:</span></span>

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

## <a name="view-reverse-dns-for-existing-cloud-services"></a><span data-ttu-id="5767e-119">View reverse DNS for existing Cloud Services</span><span class="sxs-lookup"><span data-stu-id="5767e-119">View reverse DNS for existing Cloud Services</span></span>
<span data-ttu-id="5767e-120">You can view the configured value for an existing Cloud Service using the "Get-AzureService" cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5767e-120">You can view the configured value for an existing Cloud Service using the "Get-AzureService" cmdlet:</span></span>

```powershell
Get-AzureService "contosoapp1"
```

## <a name="remove-reverse-dns-from-existing-cloud-services"></a><span data-ttu-id="5767e-121">Remove reverse DNS from existing Cloud Services</span><span class="sxs-lookup"><span data-stu-id="5767e-121">Remove reverse DNS from existing Cloud Services</span></span>
<span data-ttu-id="5767e-122">You can remove a reverse DNS property from an existing Cloud Service using the "Set-AzureService" cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5767e-122">You can remove a reverse DNS property from an existing Cloud Service using the "Set-AzureService" cmdlet.</span></span> <span data-ttu-id="5767e-123">This is done by setting the reverse DNS property value to blank:</span><span class="sxs-lookup"><span data-stu-id="5767e-123">This is done by setting the reverse DNS property value to blank:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

[!INCLUDE [FAQ1](../../includes/dns-reverse-dns-record-operations-faq-host-own-arpa-zone-include.md)]

[!INCLUDE [FAQ2](../../includes/dns-reverse-dns-record-operations-faq-asm-include.md)]

