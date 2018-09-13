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
# <a name="how-to-manage-dns-zones-using-powershell"></a>How to manage DNS Zones using PowerShell

> [!div class="op_single_selector"]
> * [Azure CLI](dns-operations-dnszones-cli.md)
> * [PowerShell](dns-operations-dnszones.md)

This article shows you how to manage your DNS zones by using Azure PowerShell. You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure portal.

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a>Create a DNS zone

A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet.

The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a>Get a DNS zone

To retrieve a DNS zone, use the `Get-AzureRmDnsZone` cmdlet. This operation returns a DNS zone object corresponding to an existing zone in Azure DNS. The object contains data about the zone (such as the number of record sets), but does not contain the record sets themselves (see `Get-AzureRmDnsRecordSet`).

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

## <a name="list-dns-zones"></a>List DNS zones

By omitting the zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group. This operation returns an array of zone objects.

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

By omitting both the zone name and the resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in the Azure subscription.

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a>Update a DNS zone

Changes to a DNS zone resource can be made by using `Set-AzureRmDnsZone`. This cmdlet does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets.md)). It's only used to update properties of the zone resource itself. The writable zone properties are currently limited to the [Azure Resource Manager ‘tags’ for the zone resource](dns-zones-records.md#tags).

Use one of the following two ways to update a DNS zone:

### <a name="specify-the-zone-using-the-zone-name-and-resource-group"></a>Specify the zone using the zone name and resource group

This approach replaces the existing zone tags with the values specified.

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-the-zone-using-a-zone-object"></a>Specify the zone using a $zone object

This approach retrieves the existing zone object, modifies the tags, and then commits the changes. In this way, existing tags can be preserved.

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

When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten. You can use the optional `-Overwrite` switch to suppress these checks.

## <a name="delete-a-dns-zone"></a>Delete a DNS Zone

DNS zones can be deleted using the `Remove-AzureRmDnsZone` cmdlet.

> [!NOTE]
> Deleting a DNS zone also deletes all DNS records within the zone. This operation cannot be undone. If the DNS zone is in use, services using the zone will fail when the zone is deleted.
>
>To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).


Use one of the following two ways to delete a DNS zone:

### <a name="specify-the-zone-using-the-zone-name-and-resource-group-name"></a>Specify the zone using the zone name and resource group name

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-the-zone-using-a-zone-object"></a>Specify the zone using a $zone object

You can specify the zone to be deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

The zone object can also be piped instead of being passed as a parameter:

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

As with `Set-AzureRmDnsZone`, specifying the zone using a `$zone` object enables Etag checks to ensure concurrent changes are not deleted. Use the `-Overwrite` switch to suppress these checks.

## <a name="confirmation-prompts"></a>Confirmation prompts

The `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.

Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower. Due to the potentially high impact of deleting a DNS zone, the `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell variable has any value other than `None`.

Since the default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.

You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter. If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs. If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.

For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).

## <a name="next-steps"></a>Next steps

Learn how to [manage record sets and records](dns-operations-recordsets.md) in your DNS zone.
<br>
Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).
<br>
Review the [Azure DNS PowerShell reference documentation](/powershell/resourcemanager/azurerm.dns/v2.3.0/azurerm.dns).

