---
title: Manage reverse DNS records for your Azure services using Azure CLI | Microsoft Docs
description: How to manage reverse DNS records or PTR records for Azure services using the Azure CLI in Resource Manager
services: DNS
documentationcenter: na
author: s-malone
manager: carmonm
editor: ''
tags: azure-resource-manager
ms.assetid: c655707e-1156-4893-b163-0b228ffd25d2
ms.service: DNS
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: smalone
ms.openlocfilehash: 879e343b3362a54d81586ac76daac0ebed317388
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556796"
---
# <a name="how-to-manage-reverse-dns-records-for-your-azure-services-using-the-azure-cli"></a><span data-ttu-id="1abb5-103">How to manage reverse DNS records for your Azure services using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1abb5-103">How to manage reverse DNS records for your Azure services using the Azure CLI</span></span>

[!INCLUDE [dns-reverse-dns-record-operations-arm-selectors-include.md](../../includes/dns-reverse-dns-record-operations-arm-selectors-include.md)]


[!INCLUDE [dns-reverse-dns-record-operations-intro-include.md](../../includes/dns-reverse-dns-record-operations-intro-include.md)]

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="1abb5-104">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="1abb5-104">CLI versions to complete the task</span></span>

<span data-ttu-id="1abb5-105">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="1abb5-105">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="1abb5-106">[Azure CLI 1.0](dns-reverse-dns-record-operations-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span><span class="sxs-lookup"><span data-stu-id="1abb5-106">[Azure CLI 1.0](dns-reverse-dns-record-operations-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="1abb5-107">[Azure CLI 2.0](dns-reverse-dns-record-operations-cli.md) - our next generation CLI for the resource management deployment model.</span><span class="sxs-lookup"><span data-stu-id="1abb5-107">[Azure CLI 2.0](dns-reverse-dns-record-operations-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="1abb5-108">Introduction</span><span class="sxs-lookup"><span data-stu-id="1abb5-108">Introduction</span></span>

[!INCLUDE [azure-arm-classic-important-include](../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="1abb5-109">For more information about the classic deployment model, see [How to manage reverse DNS records for your Azure services (classic) using Azure PowerShell](dns-reverse-dns-record-operations-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="1abb5-109">For more information about the classic deployment model, see [How to manage reverse DNS records for your Azure services (classic) using Azure PowerShell](dns-reverse-dns-record-operations-classic-ps.md).</span></span>


## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="1abb5-110">Validation of reverse DNS records</span><span class="sxs-lookup"><span data-stu-id="1abb5-110">Validation of reverse DNS records</span></span>
<span data-ttu-id="1abb5-111">To ensure a third party can’t create reverse DNS records mapping to your DNS domains, Azure only allows the creation of a reverse DNS record where one of the following is true:</span><span class="sxs-lookup"><span data-stu-id="1abb5-111">To ensure a third party can’t create reverse DNS records mapping to your DNS domains, Azure only allows the creation of a reverse DNS record where one of the following is true:</span></span>

* <span data-ttu-id="1abb5-112">The “ReverseFqdn” is the same as the “Fqdn” for the Public IP Address resource for which it has been specified, or the “Fqdn” for any Public IP Address within the same subscription e.g., “ReverseFqdn” is “contosoapp1.northus.cloudapp.azure.com.”.</span><span class="sxs-lookup"><span data-stu-id="1abb5-112">The “ReverseFqdn” is the same as the “Fqdn” for the Public IP Address resource for which it has been specified, or the “Fqdn” for any Public IP Address within the same subscription e.g., “ReverseFqdn” is “contosoapp1.northus.cloudapp.azure.com.”.</span></span>
* <span data-ttu-id="1abb5-113">The “ReverseFqdn” forward resolves to the name or IP of the Public IP Address for which it has been specified, or to any Public IP Address “Fqdn” or IP within the same subscription e.g., “ReverseFqdn” is “app1.contoso.com.”</span><span class="sxs-lookup"><span data-stu-id="1abb5-113">The “ReverseFqdn” forward resolves to the name or IP of the Public IP Address for which it has been specified, or to any Public IP Address “Fqdn” or IP within the same subscription e.g., “ReverseFqdn” is “app1.contoso.com.”</span></span> <span data-ttu-id="1abb5-114">which is a CName alias for “contosoapp1.northus.cloudapp.azure.com.”</span><span class="sxs-lookup"><span data-stu-id="1abb5-114">which is a CName alias for “contosoapp1.northus.cloudapp.azure.com.”</span></span>

<span data-ttu-id="1abb5-115">Validation checks are only performed when the reverse DNS property for a Public IP Address is set or modified.</span><span class="sxs-lookup"><span data-stu-id="1abb5-115">Validation checks are only performed when the reverse DNS property for a Public IP Address is set or modified.</span></span> <span data-ttu-id="1abb5-116">Periodic re-validation is not performed.</span><span class="sxs-lookup"><span data-stu-id="1abb5-116">Periodic re-validation is not performed.</span></span>

## <a name="add-reverse-dns-to-existing-public-ip-addresses"></a><span data-ttu-id="1abb5-117">Add reverse DNS to existing Public IP addresses</span><span class="sxs-lookup"><span data-stu-id="1abb5-117">Add reverse DNS to existing Public IP addresses</span></span>
<span data-ttu-id="1abb5-118">You can add reverse DNS to an existing Public IP address using the azure network public-ip set:</span><span class="sxs-lookup"><span data-stu-id="1abb5-118">You can add reverse DNS to an existing Public IP address using the azure network public-ip set:</span></span>

```azurecli
az network public-ip update --resource-group NRP-DemoRG-PS --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="1abb5-119">If you wish to add reverse DNS to an existing Public IP Address that doesn't already have a DNS name, you must also specify a DNS name.</span><span class="sxs-lookup"><span data-stu-id="1abb5-119">If you wish to add reverse DNS to an existing Public IP Address that doesn't already have a DNS name, you must also specify a DNS name.</span></span> <span data-ttu-id="1abb5-120">You can add achieve this using the azure network public-ip set:</span><span class="sxs-lookup"><span data-stu-id="1abb5-120">You can add achieve this using the azure network public-ip set:</span></span>

```azurecli
az network public-ip update --resource-group NRP-DemoRG-PS --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

## <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="1abb5-121">Create a Public IP Address with reverse DNS</span><span class="sxs-lookup"><span data-stu-id="1abb5-121">Create a Public IP Address with reverse DNS</span></span>
<span data-ttu-id="1abb5-122">You can add a new Public IP Address with the reverse DNS property specified using the azure network public-ip create:</span><span class="sxs-lookup"><span data-stu-id="1abb5-122">You can add a new Public IP Address with the reverse DNS property specified using the azure network public-ip create:</span></span>

```azurecli
az network public-ip create --name PublicIp --resource-group NRP-DemoRG-PS --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

## <a name="view-reverse-dns-for-existing-public-ip-addresses"></a><span data-ttu-id="1abb5-123">View reverse DNS for existing Public IP Addresses</span><span class="sxs-lookup"><span data-stu-id="1abb5-123">View reverse DNS for existing Public IP Addresses</span></span>
<span data-ttu-id="1abb5-124">You can view the configured value for an existing Public IP Address using the azure network public-ip show:</span><span class="sxs-lookup"><span data-stu-id="1abb5-124">You can view the configured value for an existing Public IP Address using the azure network public-ip show:</span></span>

```azurecli
 az network public-ip show --name PublicIp --resource-group NRP-DemoRG-PS
```

## <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="1abb5-125">Remove reverse DNS from existing Public IP Addresses</span><span class="sxs-lookup"><span data-stu-id="1abb5-125">Remove reverse DNS from existing Public IP Addresses</span></span>
<span data-ttu-id="1abb5-126">You can remove a reverse DNS property from an existing Public IP Address using azure network public-ip set.</span><span class="sxs-lookup"><span data-stu-id="1abb5-126">You can remove a reverse DNS property from an existing Public IP Address using azure network public-ip set.</span></span> <span data-ttu-id="1abb5-127">This is done by setting the ReverseFqdn property value to blank:</span><span class="sxs-lookup"><span data-stu-id="1abb5-127">This is done by setting the ReverseFqdn property value to blank:</span></span>

```azurecli
az network public-ip update --resource-group NRP-DemoRG-PS --name PublicIp --reverse-fqdn ""
```

[!INCLUDE [FAQ1](../../includes/dns-reverse-dns-record-operations-faq-host-own-arpa-zone-include.md)]

[!INCLUDE [FAQ2](../../includes/dns-reverse-dns-record-operations-faq-arm-include.md)]

