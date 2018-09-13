---
title: Manage reverse DNS records in Azure DNS using PowerShell | Microsoft Docs
description: Azure DNS allows you to manage reverse DNS records or PTR records for Azure services using PowerShell in Resource Manager
services: DNS
documentationcenter: na
author: s-malone
manager: carmonm
editor: ''
tags: azure-resource-manager
ms.assetid: b95703c5-e94e-4009-ab37-0c3f7908783c
ms.service: DNS
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/28/2016
ms.author: smalone
ms.openlocfilehash: 78de3b8dd2d8bd0992bfbacb1079825dca486442
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563314"
---
# <a name="manage-reverse-dns-records-for-your-azure-services-using-powershell"></a><span data-ttu-id="2ccf0-103">Manage reverse DNS records for your Azure services using PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ccf0-103">Manage reverse DNS records for your Azure services using PowerShell</span></span>

[!INCLUDE [dns-reverse-dns-record-operations-arm-selectors-include.md](../../includes/dns-reverse-dns-record-operations-arm-selectors-include.md)]


[!INCLUDE [DNS-reverse-dns-record-operations-intro-include.md](../../includes/dns-reverse-dns-record-operations-intro-include.md)]


[!INCLUDE [azure-arm-classic-important-include](../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="2ccf0-104">For more information about the classic deployment model, see [How to manage reverse DNS records for your Azure services (classic) using Azure PowerShell](dns-reverse-dns-record-operations-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2ccf0-104">For more information about the classic deployment model, see [How to manage reverse DNS records for your Azure services (classic) using Azure PowerShell](dns-reverse-dns-record-operations-classic-ps.md).</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="2ccf0-105">Validation of reverse DNS records</span><span class="sxs-lookup"><span data-stu-id="2ccf0-105">Validation of reverse DNS records</span></span>

<span data-ttu-id="2ccf0-106">To ensure a third party can’t create reverse DNS records mapping to your DNS domains, Azure only allows the creation of a reverse DNS record where one of the following is true:</span><span class="sxs-lookup"><span data-stu-id="2ccf0-106">To ensure a third party can’t create reverse DNS records mapping to your DNS domains, Azure only allows the creation of a reverse DNS record where one of the following is true:</span></span>

* <span data-ttu-id="2ccf0-107">The "ReverseFqdn" is the same as the "Fqdn" for the Public IP Address resource for which it has been specified, or the "Fqdn" for any Public IP Address within the same subscription e.g., "ReverseFqdn" is "contosoapp1.northus.cloudapp.azure.com.".</span><span class="sxs-lookup"><span data-stu-id="2ccf0-107">The "ReverseFqdn" is the same as the "Fqdn" for the Public IP Address resource for which it has been specified, or the "Fqdn" for any Public IP Address within the same subscription e.g., "ReverseFqdn" is "contosoapp1.northus.cloudapp.azure.com.".</span></span>
* <span data-ttu-id="2ccf0-108">The "ReverseFqdn" forward resolves to the name or IP of the Public IP Address for which it has been specified, or to any Public IP Address "Fqdn" or IP within the same subscription e.g., "ReverseFqdn" is "app1.contoso.com."</span><span class="sxs-lookup"><span data-stu-id="2ccf0-108">The "ReverseFqdn" forward resolves to the name or IP of the Public IP Address for which it has been specified, or to any Public IP Address "Fqdn" or IP within the same subscription e.g., "ReverseFqdn" is "app1.contoso.com."</span></span> <span data-ttu-id="2ccf0-109">which is a CName alias for "contosoapp1.northus.cloudapp.azure.com."</span><span class="sxs-lookup"><span data-stu-id="2ccf0-109">which is a CName alias for "contosoapp1.northus.cloudapp.azure.com."</span></span>

<span data-ttu-id="2ccf0-110">Validation checks are only performed when the reverse DNS property for a Public IP Address is set or modified.</span><span class="sxs-lookup"><span data-stu-id="2ccf0-110">Validation checks are only performed when the reverse DNS property for a Public IP Address is set or modified.</span></span> <span data-ttu-id="2ccf0-111">Periodic re-validation is not performed.</span><span class="sxs-lookup"><span data-stu-id="2ccf0-111">Periodic re-validation is not performed.</span></span>

## <a name="add-reverse-dns-to-existing-public-ip-addresses"></a><span data-ttu-id="2ccf0-112">Add reverse DNS to existing Public IP addresses</span><span class="sxs-lookup"><span data-stu-id="2ccf0-112">Add reverse DNS to existing Public IP addresses</span></span>

<span data-ttu-id="2ccf0-113">You can add reverse DNS to an existing Public IP Address using the `Set-AzureRmPublicIpAddress` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="2ccf0-113">You can add reverse DNS to an existing Public IP Address using the `Set-AzureRmPublicIpAddress` cmdlet:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIP" -ResourceGroupName "NRP-DemoRG-PS"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

<span data-ttu-id="2ccf0-114">If you wish to add reverse DNS to an existing Public IP Address that doesn't already have a DNS name, you must also specify a DNS name.</span><span class="sxs-lookup"><span data-stu-id="2ccf0-114">If you wish to add reverse DNS to an existing Public IP Address that doesn't already have a DNS name, you must also specify a DNS name.</span></span> <span data-ttu-id="2ccf0-115">You can add achieve this using the "Set-AzureRmPublicIpAddress" cmdlet:</span><span class="sxs-lookup"><span data-stu-id="2ccf0-115">You can add achieve this using the "Set-AzureRmPublicIpAddress" cmdlet:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIP" -ResourceGroupName "NRP-DemoRG-PS"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

## <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="2ccf0-116">Create a Public IP Address with reverse DNS</span><span class="sxs-lookup"><span data-stu-id="2ccf0-116">Create a Public IP Address with reverse DNS</span></span>

<span data-ttu-id="2ccf0-117">You can add a new Public IP Address with the reverse DNS property specified using the `New-AzureRmPublicIpAddress` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="2ccf0-117">You can add a new Public IP Address with the reverse DNS property specified using the `New-AzureRmPublicIpAddress` cmdlet:</span></span>

```powershell
New-AzureRmPublicIpAddress -Name "PublicIP2" -ResourceGroupName "NRP-DemoRG-PS" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

## <a name="view-reverse-dns-for-existing-public-ip-addresses"></a><span data-ttu-id="2ccf0-118">View reverse DNS for existing Public IP Addresses</span><span class="sxs-lookup"><span data-stu-id="2ccf0-118">View reverse DNS for existing Public IP Addresses</span></span>

<span data-ttu-id="2ccf0-119">You can view the configured value for an existing Public IP Address using the `Get-AzureRmPublicIpAddress` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="2ccf0-119">You can view the configured value for an existing Public IP Address using the `Get-AzureRmPublicIpAddress` cmdlet:</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIP2" -ResourceGroupName "NRP-DemoRG-PS"
```

## <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="2ccf0-120">Remove reverse DNS from existing Public IP Addresses</span><span class="sxs-lookup"><span data-stu-id="2ccf0-120">Remove reverse DNS from existing Public IP Addresses</span></span>

<span data-ttu-id="2ccf0-121">You can remove a reverse DNS property from an existing Public IP Address using the `Set-AzureRmPublicIpAddress` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2ccf0-121">You can remove a reverse DNS property from an existing Public IP Address using the `Set-AzureRmPublicIpAddress` cmdlet.</span></span> <span data-ttu-id="2ccf0-122">This is done by setting the ReverseFqdn property value to blank:</span><span class="sxs-lookup"><span data-stu-id="2ccf0-122">This is done by setting the ReverseFqdn property value to blank:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIP" -ResourceGroupName "NRP-DemoRG-PS"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

[!INCLUDE [FAQ1](../../includes/dns-reverse-dns-record-operations-faq-host-own-arpa-zone-include.md)]

[!INCLUDE [FAQ2](../../includes/dns-reverse-dns-record-operations-faq-arm-include.md)]

