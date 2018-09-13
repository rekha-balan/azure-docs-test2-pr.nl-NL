---
title: Manage DNS zones in Azure DNS - PowerShell | Microsoft Docs
description: You can manage DNS zones using Azure Powershell. This article describes how to update, delete and create DNS zones on Azure DNS
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: a67992ab-8166-4052-9b28-554c5a39e60c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: c86004a14983e9eea543fbd3aa09f2a447414291
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555834"
---
# <a name="how-to-manage-dns-zones-using-powershell"></a><span data-ttu-id="3c571-104">How to manage DNS Zones using PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c571-104">How to manage DNS Zones using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [Azure CLI](dns-operations-dnszones-cli.md)
> * [PowerShell](dns-operations-dnszones.md)

<span data-ttu-id="3c571-107">This article shows you how to manage your DNS zones by using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3c571-107">This article shows you how to manage your DNS zones by using Azure PowerShell.</span></span> <span data-ttu-id="3c571-108">You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3c571-108">You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure portal.</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a><span data-ttu-id="3c571-109">Create a DNS zone</span><span class="sxs-lookup"><span data-stu-id="3c571-109">Create a DNS zone</span></span>

<span data-ttu-id="3c571-110">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c571-110">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet.</span></span>

<span data-ttu-id="3c571-111">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="3c571-111">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="3c571-112">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:</span><span class="sxs-lookup"><span data-stu-id="3c571-112">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="3c571-113">Get a DNS zone</span><span class="sxs-lookup"><span data-stu-id="3c571-113">Get a DNS zone</span></span>

<span data-ttu-id="3c571-114">To retrieve a DNS zone, use the `Get-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c571-114">To retrieve a DNS zone, use the `Get-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="3c571-115">This operation returns a DNS zone object corresponding to an existing zone in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="3c571-115">This operation returns a DNS zone object corresponding to an existing zone in Azure DNS.</span></span> <span data-ttu-id="3c571-116">The object contains data about the zone (such as the number of record sets), but does not contain the record sets themselves (see `Get-AzureRmDnsRecordSet`).</span><span class="sxs-lookup"><span data-stu-id="3c571-116">The object contains data about the zone (such as the number of record sets), but does not contain the record sets themselves (see `Get-AzureRmDnsRecordSet`).</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com –ResourceGroupName MyAzureResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-8ec2-f4879750d201
Tags                  : {project, env}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org.,
                        ns4-01.azure-dns.info.}
NumberOfRecordSets    : 2
MaxNumberOfRecordSets : 5000
```

## <a name="list-dns-zones"></a><span data-ttu-id="3c571-117">List DNS zones</span><span class="sxs-lookup"><span data-stu-id="3c571-117">List DNS zones</span></span>

<span data-ttu-id="3c571-118">By omitting the zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span><span class="sxs-lookup"><span data-stu-id="3c571-118">By omitting the zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span></span> <span data-ttu-id="3c571-119">This operation returns an array of zone objects.</span><span class="sxs-lookup"><span data-stu-id="3c571-119">This operation returns an array of zone objects.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="3c571-120">By omitting both the zone name and the resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="3c571-120">By omitting both the zone name and the resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in the Azure subscription.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="3c571-121">Update a DNS zone</span><span class="sxs-lookup"><span data-stu-id="3c571-121">Update a DNS zone</span></span>

<span data-ttu-id="3c571-122">Changes to a DNS zone resource can be made by using `Set-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="3c571-122">Changes to a DNS zone resource can be made by using `Set-AzureRmDnsZone`.</span></span> <span data-ttu-id="3c571-123">This cmdlet does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets.md)).</span><span class="sxs-lookup"><span data-stu-id="3c571-123">This cmdlet does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets.md)).</span></span> <span data-ttu-id="3c571-124">It's only used to update properties of the zone resource itself.</span><span class="sxs-lookup"><span data-stu-id="3c571-124">It's only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="3c571-125">The writable zone properties are currently limited to the [Azure Resource Manager ‘tags’ for the zone resource](dns-zones-records.md#tags).</span><span class="sxs-lookup"><span data-stu-id="3c571-125">The writable zone properties are currently limited to the [Azure Resource Manager ‘tags’ for the zone resource](dns-zones-records.md#tags).</span></span>

<span data-ttu-id="3c571-126">Use one of the following two ways to update a DNS zone:</span><span class="sxs-lookup"><span data-stu-id="3c571-126">Use one of the following two ways to update a DNS zone:</span></span>

### <a name="specify-the-zone-using-the-zone-name-and-resource-group"></a><span data-ttu-id="3c571-127">Specify the zone using the zone name and resource group</span><span class="sxs-lookup"><span data-stu-id="3c571-127">Specify the zone using the zone name and resource group</span></span>

<span data-ttu-id="3c571-128">This approach replaces the existing zone tags with the values specified.</span><span class="sxs-lookup"><span data-stu-id="3c571-128">This approach replaces the existing zone tags with the values specified.</span></span>

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-the-zone-using-a-zone-object"></a><span data-ttu-id="3c571-129">Specify the zone using a $zone object</span><span class="sxs-lookup"><span data-stu-id="3c571-129">Specify the zone using a $zone object</span></span>

<span data-ttu-id="3c571-130">This approach retrieves the existing zone object, modifies the tags, and then commits the changes.</span><span class="sxs-lookup"><span data-stu-id="3c571-130">This approach retrieves the existing zone object, modifies the tags, and then commits the changes.</span></span> <span data-ttu-id="3c571-131">In this way, existing tags can be preserved.</span><span class="sxs-lookup"><span data-stu-id="3c571-131">In this way, existing tags can be preserved.</span></span>

```powershell
# Get the zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="3c571-132">When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span><span class="sxs-lookup"><span data-stu-id="3c571-132">When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="3c571-133">You can use the optional `-Overwrite` switch to suppress these checks.</span><span class="sxs-lookup"><span data-stu-id="3c571-133">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

## <a name="delete-a-dns-zone"></a><span data-ttu-id="3c571-134">Delete a DNS Zone</span><span class="sxs-lookup"><span data-stu-id="3c571-134">Delete a DNS Zone</span></span>

<span data-ttu-id="3c571-135">DNS zones can be deleted using the `Remove-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3c571-135">DNS zones can be deleted using the `Remove-AzureRmDnsZone` cmdlet.</span></span>

> [!NOTE]
> Deleting a DNS zone also deletes all DNS records within the zone. This operation cannot be undone. If the DNS zone is in use, services using the zone will fail when the zone is deleted.
>
>To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).


<span data-ttu-id="3c571-140">Use one of the following two ways to delete a DNS zone:</span><span class="sxs-lookup"><span data-stu-id="3c571-140">Use one of the following two ways to delete a DNS zone:</span></span>

### <a name="specify-the-zone-using-the-zone-name-and-resource-group-name"></a><span data-ttu-id="3c571-141">Specify the zone using the zone name and resource group name</span><span class="sxs-lookup"><span data-stu-id="3c571-141">Specify the zone using the zone name and resource group name</span></span>

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-the-zone-using-a-zone-object"></a><span data-ttu-id="3c571-142">Specify the zone using a $zone object</span><span class="sxs-lookup"><span data-stu-id="3c571-142">Specify the zone using a $zone object</span></span>

<span data-ttu-id="3c571-143">You can specify the zone to be deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="3c571-143">You can specify the zone to be deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="3c571-144">The zone object can also be piped instead of being passed as a parameter:</span><span class="sxs-lookup"><span data-stu-id="3c571-144">The zone object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

<span data-ttu-id="3c571-145">As with `Set-AzureRmDnsZone`, specifying the zone using a `$zone` object enables Etag checks to ensure concurrent changes are not deleted.</span><span class="sxs-lookup"><span data-stu-id="3c571-145">As with `Set-AzureRmDnsZone`, specifying the zone using a `$zone` object enables Etag checks to ensure concurrent changes are not deleted.</span></span> <span data-ttu-id="3c571-146">Use the `-Overwrite` switch to suppress these checks.</span><span class="sxs-lookup"><span data-stu-id="3c571-146">Use the `-Overwrite` switch to suppress these checks.</span></span>

## <a name="confirmation-prompts"></a><span data-ttu-id="3c571-147">Confirmation prompts</span><span class="sxs-lookup"><span data-stu-id="3c571-147">Confirmation prompts</span></span>

<span data-ttu-id="3c571-148">The `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.</span><span class="sxs-lookup"><span data-stu-id="3c571-148">The `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="3c571-149">Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span><span class="sxs-lookup"><span data-stu-id="3c571-149">Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="3c571-150">Due to the potentially high impact of deleting a DNS zone, the `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell variable has any value other than `None`.</span><span class="sxs-lookup"><span data-stu-id="3c571-150">Due to the potentially high impact of deleting a DNS zone, the `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell variable has any value other than `None`.</span></span>

<span data-ttu-id="3c571-151">Since the default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.</span><span class="sxs-lookup"><span data-stu-id="3c571-151">Since the default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.</span></span>

<span data-ttu-id="3c571-152">You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter.</span><span class="sxs-lookup"><span data-stu-id="3c571-152">You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter.</span></span> <span data-ttu-id="3c571-153">If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs.</span><span class="sxs-lookup"><span data-stu-id="3c571-153">If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="3c571-154">If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.</span><span class="sxs-lookup"><span data-stu-id="3c571-154">If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.</span></span>

<span data-ttu-id="3c571-155">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="3c571-155">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c571-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="3c571-156">Next steps</span></span>

<span data-ttu-id="3c571-157">Learn how to [manage record sets and records](dns-operations-recordsets.md) in your DNS zone.</span><span class="sxs-lookup"><span data-stu-id="3c571-157">Learn how to [manage record sets and records](dns-operations-recordsets.md) in your DNS zone.</span></span>
<br>
<span data-ttu-id="3c571-158">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="3c571-158">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>
<br>
<span data-ttu-id="3c571-159">Review the [Azure DNS PowerShell reference documentation](/powershell/resourcemanager/azurerm.dns/v2.3.0/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="3c571-159">Review the [Azure DNS PowerShell reference documentation](/powershell/resourcemanager/azurerm.dns/v2.3.0/azurerm.dns).</span></span>

