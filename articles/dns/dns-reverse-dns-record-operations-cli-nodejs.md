---
title: Manage reverse DNS records for your Azure services using Azure CLI 1.0 | Microsoft Docs
description: How to manage reverse DNS records or PTR records for Azure services using the Azure CLI 1.0 in Resource Manager
services: DNS
documentationcenter: na
author: s-malone
manager: carmonm
editor: ''
tags: azure-resource-manager
ms.assetid: c655707e-1156-4893-b163-0b228ffd25d2
ms.service: DNS
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/28/2016
ms.author: smalone
ms.openlocfilehash: 227ede3445ced9cca71a3879afb0bb6c8c5c2482
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548852"
---
# <a name="how-to-manage-reverse-dns-records-for-your-azure-services-using-the-azure-cli-10"></a><span data-ttu-id="53e2d-103">How to manage reverse DNS records for your Azure services using the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="53e2d-103">How to manage reverse DNS records for your Azure services using the Azure CLI 1.0</span></span>

[!INCLUDE [dns-reverse-dns-record-operations-arm-selectors-include.md](../../includes/dns-reverse-dns-record-operations-arm-selectors-include.md)]


[!INCLUDE [dns-reverse-dns-record-operations-intro-include.md](../../includes/dns-reverse-dns-record-operations-intro-include.md)]

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="53e2d-104">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="53e2d-104">CLI versions to complete the task</span></span>

<span data-ttu-id="53e2d-105">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="53e2d-105">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="53e2d-106">[Azure CLI 1.0](dns-reverse-dns-record-operations-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span><span class="sxs-lookup"><span data-stu-id="53e2d-106">[Azure CLI 1.0](dns-reverse-dns-record-operations-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="53e2d-107">[Azure CLI 2.0](dns-reverse-dns-record-operations-cli.md) - our next generation CLI for the resource management deployment model.</span><span class="sxs-lookup"><span data-stu-id="53e2d-107">[Azure CLI 2.0](dns-reverse-dns-record-operations-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="53e2d-108">Introduction</span><span class="sxs-lookup"><span data-stu-id="53e2d-108">Introduction</span></span>

[!INCLUDE [azure-arm-classic-important-include](../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="53e2d-109">For more information about the classic deployment model, see [How to manage reverse DNS records for your Azure services (classic) using Azure PowerShell](dns-reverse-dns-record-operations-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="53e2d-109">For more information about the classic deployment model, see [How to manage reverse DNS records for your Azure services (classic) using Azure PowerShell](dns-reverse-dns-record-operations-classic-ps.md).</span></span>


## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="53e2d-110">Validation of reverse DNS records</span><span class="sxs-lookup"><span data-stu-id="53e2d-110">Validation of reverse DNS records</span></span>
<span data-ttu-id="53e2d-111">To ensure a third party can’t create reverse DNS records mapping to your DNS domains, Azure only allows the creation of a reverse DNS record where one of the following is true:</span><span class="sxs-lookup"><span data-stu-id="53e2d-111">To ensure a third party can’t create reverse DNS records mapping to your DNS domains, Azure only allows the creation of a reverse DNS record where one of the following is true:</span></span>

* <span data-ttu-id="53e2d-112">The “ReverseFqdn” is the same as the “Fqdn” for the Public IP Address resource for which it has been specified, or the “Fqdn” for any Public IP Address within the same subscription e.g., “ReverseFqdn” is “contosoapp1.northus.cloudapp.azure.com.”.</span><span class="sxs-lookup"><span data-stu-id="53e2d-112">The “ReverseFqdn” is the same as the “Fqdn” for the Public IP Address resource for which it has been specified, or the “Fqdn” for any Public IP Address within the same subscription e.g., “ReverseFqdn” is “contosoapp1.northus.cloudapp.azure.com.”.</span></span>
* <span data-ttu-id="53e2d-113">The “ReverseFqdn” forward resolves to the name or IP of the Public IP Address for which it has been specified, or to any Public IP Address “Fqdn” or IP within the same subscription e.g., “ReverseFqdn” is “app1.contoso.com.”</span><span class="sxs-lookup"><span data-stu-id="53e2d-113">The “ReverseFqdn” forward resolves to the name or IP of the Public IP Address for which it has been specified, or to any Public IP Address “Fqdn” or IP within the same subscription e.g., “ReverseFqdn” is “app1.contoso.com.”</span></span> <span data-ttu-id="53e2d-114">which is a CName alias for “contosoapp1.northus.cloudapp.azure.com.”</span><span class="sxs-lookup"><span data-stu-id="53e2d-114">which is a CName alias for “contosoapp1.northus.cloudapp.azure.com.”</span></span>

<span data-ttu-id="53e2d-115">Validation checks are only performed when the reverse DNS property for a Public IP Address is set or modified.</span><span class="sxs-lookup"><span data-stu-id="53e2d-115">Validation checks are only performed when the reverse DNS property for a Public IP Address is set or modified.</span></span> <span data-ttu-id="53e2d-116">Periodic re-validation is not performed.</span><span class="sxs-lookup"><span data-stu-id="53e2d-116">Periodic re-validation is not performed.</span></span>

## <a name="add-reverse-dns-to-existing-public-ip-addresses"></a><span data-ttu-id="53e2d-117">Add reverse DNS to existing Public IP addresses</span><span class="sxs-lookup"><span data-stu-id="53e2d-117">Add reverse DNS to existing Public IP addresses</span></span>
<span data-ttu-id="53e2d-118">You can add reverse DNS to an existing Public IP address using the azure network public-ip set:</span><span class="sxs-lookup"><span data-stu-id="53e2d-118">You can add reverse DNS to an existing Public IP address using the azure network public-ip set:</span></span>

    azure network public-ip set -n PublicIp -g NRP-DemoRG-PS -f contosoapp1.westus.cloudapp.azure.com.

<span data-ttu-id="53e2d-119">If you wish to add reverse DNS to an existing Public IP Address that doesn't already have a DNS name, you must also specify a DNS name.</span><span class="sxs-lookup"><span data-stu-id="53e2d-119">If you wish to add reverse DNS to an existing Public IP Address that doesn't already have a DNS name, you must also specify a DNS name.</span></span> <span data-ttu-id="53e2d-120">You can add achieve this using the azure network public-ip set:</span><span class="sxs-lookup"><span data-stu-id="53e2d-120">You can add achieve this using the azure network public-ip set:</span></span>

    azure network public-ip set -n PublicIp -g NRP-DemoRG-PS -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.

## <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="53e2d-121">Create a Public IP Address with reverse DNS</span><span class="sxs-lookup"><span data-stu-id="53e2d-121">Create a Public IP Address with reverse DNS</span></span>
<span data-ttu-id="53e2d-122">You can add a new Public IP Address with the reverse DNS property specified using the azure network public-ip create:</span><span class="sxs-lookup"><span data-stu-id="53e2d-122">You can add a new Public IP Address with the reverse DNS property specified using the azure network public-ip create:</span></span>

    azure network public-ip create -n PublicIp3 -g NRP-DemoRG-PS -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.

## <a name="view-reverse-dns-for-existing-public-ip-addresses"></a><span data-ttu-id="53e2d-123">View reverse DNS for existing Public IP Addresses</span><span class="sxs-lookup"><span data-stu-id="53e2d-123">View reverse DNS for existing Public IP Addresses</span></span>
<span data-ttu-id="53e2d-124">You can view the configured value for an existing Public IP Address using the azure network public-ip show:</span><span class="sxs-lookup"><span data-stu-id="53e2d-124">You can view the configured value for an existing Public IP Address using the azure network public-ip show:</span></span>

    azure network public-ip show -n PublicIp3 -g NRP-DemoRG-PS

## <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="53e2d-125">Remove reverse DNS from existing Public IP Addresses</span><span class="sxs-lookup"><span data-stu-id="53e2d-125">Remove reverse DNS from existing Public IP Addresses</span></span>
<span data-ttu-id="53e2d-126">You can remove a reverse DNS property from an existing Public IP Address using azure network public-ip set.</span><span class="sxs-lookup"><span data-stu-id="53e2d-126">You can remove a reverse DNS property from an existing Public IP Address using azure network public-ip set.</span></span> <span data-ttu-id="53e2d-127">This is done by setting the ReverseFqdn property value to blank:</span><span class="sxs-lookup"><span data-stu-id="53e2d-127">This is done by setting the ReverseFqdn property value to blank:</span></span>

    azure network public-ip set -n PublicIp3 -g NRP-DemoRG-PS –f “”

[!INCLUDE [FAQ1](../../includes/dns-reverse-dns-record-operations-faq-host-own-arpa-zone-include.md)]

[!INCLUDE [FAQ2](../../includes/dns-reverse-dns-record-operations-faq-arm-include.md)]

