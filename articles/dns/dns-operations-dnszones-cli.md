---
title: Manage DNS zones in Azure DNS - Azure CLI 2.0 | Microsoft Docs
description: You can manage DNS zones using Azure CLI 2.0. This article shows how to update, delete and create DNS zones on Azure DNS.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 2da07ec11f15c1952d7d88a34f74c6e38810a79f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661647"
---
# <a name="how-to-manage-dns-zones-in-azure-dns-using-the-azure-cli-20"></a><span data-ttu-id="18e84-104">How to manage DNS Zones in Azure DNS using the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="18e84-104">How to manage DNS Zones in Azure DNS using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)
> * [PowerShell](dns-operations-dnszones.md)

<span data-ttu-id="18e84-108">This guide shows how to manage your DNS zones by using the cross-platform Azure CLI, which is available for Windows, Mac and Linux.</span><span class="sxs-lookup"><span data-stu-id="18e84-108">This guide shows how to manage your DNS zones by using the cross-platform Azure CLI, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="18e84-109">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="18e84-109">You can also manage your DNS zones using [Azure PowerShell](dns-operations-dnszones.md) or the Azure portal.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="18e84-110">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="18e84-110">CLI versions to complete the task</span></span>

<span data-ttu-id="18e84-111">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="18e84-111">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="18e84-112">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span><span class="sxs-lookup"><span data-stu-id="18e84-112">[Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="18e84-113">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for the resource management deployment model.</span><span class="sxs-lookup"><span data-stu-id="18e84-113">[Azure CLI 2.0](dns-operations-dnszones-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

## <a name="introduction"></a><span data-ttu-id="18e84-114">Introduction</span><span class="sxs-lookup"><span data-stu-id="18e84-114">Introduction</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a><span data-ttu-id="18e84-115">Set up Azure CLI 2.0 for Azure DNS</span><span class="sxs-lookup"><span data-stu-id="18e84-115">Set up Azure CLI 2.0 for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="18e84-116">Before you begin</span><span class="sxs-lookup"><span data-stu-id="18e84-116">Before you begin</span></span>

<span data-ttu-id="18e84-117">Verify that you have the following items before beginning your configuration.</span><span class="sxs-lookup"><span data-stu-id="18e84-117">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="18e84-118">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="18e84-118">An Azure subscription.</span></span> <span data-ttu-id="18e84-119">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="18e84-119">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="18e84-120">Install the latest version of the Azure CLI 2.0, available for Windows, Linux, or MAC.</span><span class="sxs-lookup"><span data-stu-id="18e84-120">Install the latest version of the Azure CLI 2.0, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="18e84-121">More information is available at [Install the Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="18e84-121">More information is available at [Install the Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="18e84-122">Sign in to your Azure account</span><span class="sxs-lookup"><span data-stu-id="18e84-122">Sign in to your Azure account</span></span>

<span data-ttu-id="18e84-123">Open a console window and authenticate with your credentials.</span><span class="sxs-lookup"><span data-stu-id="18e84-123">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="18e84-124">For more information, see Log in to Azure from the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="18e84-124">For more information, see Log in to Azure from the Azure CLI</span></span>

```
az login
```

### <a name="select-the-subscription"></a><span data-ttu-id="18e84-125">Select the subscription</span><span class="sxs-lookup"><span data-stu-id="18e84-125">Select the subscription</span></span>

<span data-ttu-id="18e84-126">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="18e84-126">Check the subscriptions for the account.</span></span>

```
az account list
```

### <a name="choose-which-of-your-azure-subscriptions-to-use"></a><span data-ttu-id="18e84-127">Choose which of your Azure subscriptions to use.</span><span class="sxs-lookup"><span data-stu-id="18e84-127">Choose which of your Azure subscriptions to use.</span></span>

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="18e84-128">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="18e84-128">Create a resource group</span></span>

<span data-ttu-id="18e84-129">Azure Resource Manager requires that all resource groups specify a location.</span><span class="sxs-lookup"><span data-stu-id="18e84-129">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="18e84-130">This is used as the default location for resources in that resource group.</span><span class="sxs-lookup"><span data-stu-id="18e84-130">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="18e84-131">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="18e84-131">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="18e84-132">You can skip this step if you are using an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="18e84-132">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a><span data-ttu-id="18e84-133">Getting help</span><span class="sxs-lookup"><span data-stu-id="18e84-133">Getting help</span></span>

<span data-ttu-id="18e84-134">All CLI 2.0 commands relating to Azure DNS start with `az network dns`.</span><span class="sxs-lookup"><span data-stu-id="18e84-134">All CLI 2.0 commands relating to Azure DNS start with `az network dns`.</span></span> <span data-ttu-id="18e84-135">Help is available for each command using the `--help` option (short form `-h`).</span><span class="sxs-lookup"><span data-stu-id="18e84-135">Help is available for each command using the `--help` option (short form `-h`).</span></span>  <span data-ttu-id="18e84-136">For example:</span><span class="sxs-lookup"><span data-stu-id="18e84-136">For example:</span></span>

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="18e84-137">Create a DNS zone</span><span class="sxs-lookup"><span data-stu-id="18e84-137">Create a DNS zone</span></span>

<span data-ttu-id="18e84-138">A DNS zone is created using the `az network dns zone create` command.</span><span class="sxs-lookup"><span data-stu-id="18e84-138">A DNS zone is created using the `az network dns zone create` command.</span></span> <span data-ttu-id="18e84-139">For help, see `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="18e84-139">For help, see `az network dns zone create -h`.</span></span>

<span data-ttu-id="18e84-140">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="18e84-140">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="to-create-a-dns-zone-with-tags"></a><span data-ttu-id="18e84-141">To create a DNS zone with tags.</span><span class="sxs-lookup"><span data-stu-id="18e84-141">To create a DNS zone with tags.</span></span>

<span data-ttu-id="18e84-142">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using the `--tags` parameter (short form `-t`):</span><span class="sxs-lookup"><span data-stu-id="18e84-142">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*, by using the `--tags` parameter (short form `-t`):</span></span>

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="18e84-143">Get a DNS zone</span><span class="sxs-lookup"><span data-stu-id="18e84-143">Get a DNS zone</span></span>

<span data-ttu-id="18e84-144">To retrieve a DNS zone, use `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="18e84-144">To retrieve a DNS zone, use `az network dns zone show`.</span></span> <span data-ttu-id="18e84-145">For help, see `az network dns zone show --help`.</span><span class="sxs-lookup"><span data-stu-id="18e84-145">For help, see `az network dns zone show --help`.</span></span>

<span data-ttu-id="18e84-146">The following example returns the DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="18e84-146">The following example returns the DNS zone *contoso.com* and its associated data from resource group *MyResourceGroup*.</span></span> 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

<span data-ttu-id="18e84-147">The following example is the response.</span><span class="sxs-lookup"><span data-stu-id="18e84-147">The following example is the response.</span></span>

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="18e84-148">Note that DNS records are not returned by `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="18e84-148">Note that DNS records are not returned by `az network dns zone show`.</span></span> <span data-ttu-id="18e84-149">To list DNS records, use `az network dns record-set list`.</span><span class="sxs-lookup"><span data-stu-id="18e84-149">To list DNS records, use `az network dns record-set list`.</span></span>


## <a name="list-dns-zones"></a><span data-ttu-id="18e84-150">List DNS zones</span><span class="sxs-lookup"><span data-stu-id="18e84-150">List DNS zones</span></span>

<span data-ttu-id="18e84-151">To enumerate DNS zones, use `az network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="18e84-151">To enumerate DNS zones, use `az network dns zone list`.</span></span> <span data-ttu-id="18e84-152">For help, see `az network dns zone list --help`.</span><span class="sxs-lookup"><span data-stu-id="18e84-152">For help, see `az network dns zone list --help`.</span></span>

<span data-ttu-id="18e84-153">Specifying the resource group lists only those zones within the resource group:</span><span class="sxs-lookup"><span data-stu-id="18e84-153">Specifying the resource group lists only those zones within the resource group:</span></span>

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

<span data-ttu-id="18e84-154">Omitting the resource group lists all zones in the subscription:</span><span class="sxs-lookup"><span data-stu-id="18e84-154">Omitting the resource group lists all zones in the subscription:</span></span>

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="18e84-155">Update a DNS zone</span><span class="sxs-lookup"><span data-stu-id="18e84-155">Update a DNS zone</span></span>

<span data-ttu-id="18e84-156">Changes to a DNS zone resource can be made using `az network dns zone update`.</span><span class="sxs-lookup"><span data-stu-id="18e84-156">Changes to a DNS zone resource can be made using `az network dns zone update`.</span></span> <span data-ttu-id="18e84-157">For help, see `az network dns zone update --help`.</span><span class="sxs-lookup"><span data-stu-id="18e84-157">For help, see `az network dns zone update --help`.</span></span>

<span data-ttu-id="18e84-158">This command does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets-cli.md)).</span><span class="sxs-lookup"><span data-stu-id="18e84-158">This command does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets-cli.md)).</span></span> <span data-ttu-id="18e84-159">It is only used to update properties of the zone resource itself.</span><span class="sxs-lookup"><span data-stu-id="18e84-159">It is only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="18e84-160">These properties are currently limited to the [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for the zone resource.</span><span class="sxs-lookup"><span data-stu-id="18e84-160">These properties are currently limited to the [Azure Resource Manager 'tags'](dns-zones-records.md#tags) for the zone resource.</span></span>

<span data-ttu-id="18e84-161">The following example shows how to update the tags on a DNS zone.</span><span class="sxs-lookup"><span data-stu-id="18e84-161">The following example shows how to update the tags on a DNS zone.</span></span> <span data-ttu-id="18e84-162">The existing tags are replaced by the value specified.</span><span class="sxs-lookup"><span data-stu-id="18e84-162">The existing tags are replaced by the value specified.</span></span>

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a><span data-ttu-id="18e84-163">Delete a DNS Zone</span><span class="sxs-lookup"><span data-stu-id="18e84-163">Delete a DNS Zone</span></span>

<span data-ttu-id="18e84-164">DNS zones can be deleted using `az network dns zone delete`.</span><span class="sxs-lookup"><span data-stu-id="18e84-164">DNS zones can be deleted using `az network dns zone delete`.</span></span> <span data-ttu-id="18e84-165">For help, see `az network dns zone delete --help`.</span><span class="sxs-lookup"><span data-stu-id="18e84-165">For help, see `az network dns zone delete --help`.</span></span>

> [!NOTE]
> Deleting a DNS zone also deletes all DNS records within the zone. This operation cannot be undone. If the DNS zone is in use, services using the zone will fail when the zone is deleted.
>
>To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).

<span data-ttu-id="18e84-170">This command prompts for confirmation.</span><span class="sxs-lookup"><span data-stu-id="18e84-170">This command prompts for confirmation.</span></span> <span data-ttu-id="18e84-171">The optional `--yes` switch suppresses this prompt.</span><span class="sxs-lookup"><span data-stu-id="18e84-171">The optional `--yes` switch suppresses this prompt.</span></span>

<span data-ttu-id="18e84-172">The following example shows how to delete the zone *contoso.com* from resource group *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="18e84-172">The following example shows how to delete the zone *contoso.com* from resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a><span data-ttu-id="18e84-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="18e84-173">Next steps</span></span>

<span data-ttu-id="18e84-174">Learn how to [manage record sets and records](dns-getstarted-create-recordset-cli.md) in your DNS zone.</span><span class="sxs-lookup"><span data-stu-id="18e84-174">Learn how to [manage record sets and records](dns-getstarted-create-recordset-cli.md) in your DNS zone.</span></span>

<span data-ttu-id="18e84-175">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="18e84-175">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

