---
title: Create DNS zones and record sets in Azure DNS using the .NET SDK | Microsoft Docs
description: How to create DNS zones and record sets in Azure DNS by using the .NET SDK.
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: eed99b87-f4d4-4fbf-a926-263f7e30b884
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/19/2016
ms.author: jonatul
ms.openlocfilehash: c0fb0be8da1c0ca48a4d43ea027d30a0bc17fe30
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553649"
---
# <a name="create-dns-zones-and-record-sets-using-the-net-sdk"></a><span data-ttu-id="d9376-103">Create DNS zones and record sets using the .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d9376-103">Create DNS zones and record sets using the .NET SDK</span></span>

<span data-ttu-id="d9376-104">You can automate operations to create, delete, or update DNS zones, record sets, and records by using DNS SDK with .NET DNS Management library.</span><span class="sxs-lookup"><span data-stu-id="d9376-104">You can automate operations to create, delete, or update DNS zones, record sets, and records by using DNS SDK with .NET DNS Management library.</span></span> <span data-ttu-id="d9376-105">A full Visual Studio project is available [here.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span><span class="sxs-lookup"><span data-stu-id="d9376-105">A full Visual Studio project is available [here.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span></span>

## <a name="create-a-service-principal-account"></a><span data-ttu-id="d9376-106">Create a service principal account</span><span class="sxs-lookup"><span data-stu-id="d9376-106">Create a service principal account</span></span>

<span data-ttu-id="d9376-107">Typically, programmatic access to Azure resources is granted via a dedicated account rather than your own user credentials.</span><span class="sxs-lookup"><span data-stu-id="d9376-107">Typically, programmatic access to Azure resources is granted via a dedicated account rather than your own user credentials.</span></span> <span data-ttu-id="d9376-108">These dedicated accounts are called 'service principal' accounts.</span><span class="sxs-lookup"><span data-stu-id="d9376-108">These dedicated accounts are called 'service principal' accounts.</span></span> <span data-ttu-id="d9376-109">To use the Azure DNS SDK sample project, you first need to create a service principal account and assign it the correct permissions.</span><span class="sxs-lookup"><span data-stu-id="d9376-109">To use the Azure DNS SDK sample project, you first need to create a service principal account and assign it the correct permissions.</span></span>

1. <span data-ttu-id="d9376-110">Follow [these instructions](../azure-resource-manager/resource-group-authenticate-service-principal.md) to create a service principal account (the Azure DNS SDK sample project assumes password-based authentication.)</span><span class="sxs-lookup"><span data-stu-id="d9376-110">Follow [these instructions](../azure-resource-manager/resource-group-authenticate-service-principal.md) to create a service principal account (the Azure DNS SDK sample project assumes password-based authentication.)</span></span>
2. <span data-ttu-id="d9376-111">Create a resource group ([here's how](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span><span class="sxs-lookup"><span data-stu-id="d9376-111">Create a resource group ([here's how](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span></span>
3. <span data-ttu-id="d9376-112">Use Azure RBAC to grant the service principal account 'DNS Zone Contributor' permissions to the resource group ([here's how](../active-directory/role-based-access-control-configure.md).)</span><span class="sxs-lookup"><span data-stu-id="d9376-112">Use Azure RBAC to grant the service principal account 'DNS Zone Contributor' permissions to the resource group ([here's how](../active-directory/role-based-access-control-configure.md).)</span></span>
4. <span data-ttu-id="d9376-113">If using the Azure DNS SDK sample project, edit the 'program.cs' file as follows:</span><span class="sxs-lookup"><span data-stu-id="d9376-113">If using the Azure DNS SDK sample project, edit the 'program.cs' file as follows:</span></span>

   * <span data-ttu-id="d9376-114">Insert the correct values for the tenantId, clientId (also known as account ID), secret (service principal account password) and subscriptionId as used in step 1.</span><span class="sxs-lookup"><span data-stu-id="d9376-114">Insert the correct values for the tenantId, clientId (also known as account ID), secret (service principal account password) and subscriptionId as used in step 1.</span></span>
   * <span data-ttu-id="d9376-115">Enter the resource group name chosen in step 2.</span><span class="sxs-lookup"><span data-stu-id="d9376-115">Enter the resource group name chosen in step 2.</span></span>
   * <span data-ttu-id="d9376-116">Enter a DNS zone name of your choice.</span><span class="sxs-lookup"><span data-stu-id="d9376-116">Enter a DNS zone name of your choice.</span></span>

## <a name="nuget-packages-and-namespace-declarations"></a><span data-ttu-id="d9376-117">NuGet packages and namespace declarations</span><span class="sxs-lookup"><span data-stu-id="d9376-117">NuGet packages and namespace declarations</span></span>

<span data-ttu-id="d9376-118">To use the Azure DNS .NET SDK, you need to install the **Azure DNS Management Library** NuGet package and other required Azure packages.</span><span class="sxs-lookup"><span data-stu-id="d9376-118">To use the Azure DNS .NET SDK, you need to install the **Azure DNS Management Library** NuGet package and other required Azure packages.</span></span>

1. <span data-ttu-id="d9376-119">In **Visual Studio**, open a project or new project.</span><span class="sxs-lookup"><span data-stu-id="d9376-119">In **Visual Studio**, open a project or new project.</span></span>
2. <span data-ttu-id="d9376-120">Go to **Tools** **>** **NuGet Package Manager** **>** **Manage NuGet Packages for Solution...**.</span><span class="sxs-lookup"><span data-stu-id="d9376-120">Go to **Tools** **>** **NuGet Package Manager** **>** **Manage NuGet Packages for Solution...**.</span></span>
3. <span data-ttu-id="d9376-121">Click **Browse**, enable the **Include prerelease** checkbox, and type **Microsoft.Azure.Management.Dns** in the search box.</span><span class="sxs-lookup"><span data-stu-id="d9376-121">Click **Browse**, enable the **Include prerelease** checkbox, and type **Microsoft.Azure.Management.Dns** in the search box.</span></span>
4. <span data-ttu-id="d9376-122">Select the package and click **Install** to add it to your Visual Studio project.</span><span class="sxs-lookup"><span data-stu-id="d9376-122">Select the package and click **Install** to add it to your Visual Studio project.</span></span>
5. <span data-ttu-id="d9376-123">Repeat the process above to also install the following packages: **Microsoft.Rest.ClientRuntime.Azure.Authentication** and **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="d9376-123">Repeat the process above to also install the following packages: **Microsoft.Rest.ClientRuntime.Azure.Authentication** and **Microsoft.Azure.Management.ResourceManager**.</span></span>

## <a name="add-namespace-declarations"></a><span data-ttu-id="d9376-124">Add namespace declarations</span><span class="sxs-lookup"><span data-stu-id="d9376-124">Add namespace declarations</span></span>

<span data-ttu-id="d9376-125">Add the following namespace declarations</span><span class="sxs-lookup"><span data-stu-id="d9376-125">Add the following namespace declarations</span></span>

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-the-dns-management-client"></a><span data-ttu-id="d9376-126">Initialize the DNS management client</span><span class="sxs-lookup"><span data-stu-id="d9376-126">Initialize the DNS management client</span></span>

<span data-ttu-id="d9376-127">The *DnsManagementClient* contains the methods and properties necessary for managing DNS zones and recordsets.</span><span class="sxs-lookup"><span data-stu-id="d9376-127">The *DnsManagementClient* contains the methods and properties necessary for managing DNS zones and recordsets.</span></span>  <span data-ttu-id="d9376-128">The following code logs in to the service principal account and creates a DnsManagementClient object.</span><span class="sxs-lookup"><span data-stu-id="d9376-128">The following code logs in to the service principal account and creates a DnsManagementClient object.</span></span>

```cs
// Build the service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a><span data-ttu-id="d9376-129">Create or update a DNS zone</span><span class="sxs-lookup"><span data-stu-id="d9376-129">Create or update a DNS zone</span></span>

<span data-ttu-id="d9376-130">To create a DNS zone, first a "Zone" object is created to contain the DNS zone parameters.</span><span class="sxs-lookup"><span data-stu-id="d9376-130">To create a DNS zone, first a "Zone" object is created to contain the DNS zone parameters.</span></span> <span data-ttu-id="d9376-131">Because DNS zones are not linked to a specific region, the location is set to 'global'.</span><span class="sxs-lookup"><span data-stu-id="d9376-131">Because DNS zones are not linked to a specific region, the location is set to 'global'.</span></span> <span data-ttu-id="d9376-132">In this example, an [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) is also added to the zone.</span><span class="sxs-lookup"><span data-stu-id="d9376-132">In this example, an [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) is also added to the zone.</span></span>

<span data-ttu-id="d9376-133">To actually create or update the zone in Azure DNS, the zone object containing the zone parameters is passed to the *DnsManagementClient.Zones.CreateOrUpdateAsyc* method.</span><span class="sxs-lookup"><span data-stu-id="d9376-133">To actually create or update the zone in Azure DNS, the zone object containing the zone parameters is passed to the *DnsManagementClient.Zones.CreateOrUpdateAsyc* method.</span></span>

> [!NOTE]
> <span data-ttu-id="d9376-134">DnsManagementClient supports three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access to the HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span><span class="sxs-lookup"><span data-stu-id="d9376-134">DnsManagementClient supports three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access to the HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>  <span data-ttu-id="d9376-135">You can choose any of these modes, depending on your application needs.</span><span class="sxs-lookup"><span data-stu-id="d9376-135">You can choose any of these modes, depending on your application needs.</span></span>

<span data-ttu-id="d9376-136">Azure DNS supports optimistic concurrency, called [Etags](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="d9376-136">Azure DNS supports optimistic concurrency, called [Etags](dns-getstarted-create-dnszone.md).</span></span> <span data-ttu-id="d9376-137">In this example, specifying "\*" for the 'If-None-Match' header tells Azure DNS to create a DNS zone if one does not already exist.</span><span class="sxs-lookup"><span data-stu-id="d9376-137">In this example, specifying "\*" for the 'If-None-Match' header tells Azure DNS to create a DNS zone if one does not already exist.</span></span>  <span data-ttu-id="d9376-138">The call fails if a zone with the given name already exists in the given resource group.</span><span class="sxs-lookup"><span data-stu-id="d9376-138">The call fails if a zone with the given name already exists in the given resource group.</span></span>

```cs
// Create zone parameters
var dnsZoneParams = new Zone("global"); // All DNS zones must have location = "global"

// Create a Azure Resource Manager 'tag'.  This is optional.  You can add multiple tags
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");

// Create the actual zone.
// Note: Uses 'If-None-Match *' ETAG check, so will fail if the zone exists already.
// Note: For non-async usage, call dnsClient.Zones.CreateOrUpdate(resourceGroupName, zoneName, dnsZoneParams, null, "*")
// Note: For getting the http response, call dnsClient.Zones.CreateOrUpdateWithHttpMessagesAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*")
var dnsZone = await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

## <a name="create-dns-record-sets-and-records"></a><span data-ttu-id="d9376-139">Create DNS record sets and records</span><span class="sxs-lookup"><span data-stu-id="d9376-139">Create DNS record sets and records</span></span>

<span data-ttu-id="d9376-140">DNS records are managed as a record set.</span><span class="sxs-lookup"><span data-stu-id="d9376-140">DNS records are managed as a record set.</span></span> <span data-ttu-id="d9376-141">A record set is a set of records with the same name and record type within a zone.</span><span class="sxs-lookup"><span data-stu-id="d9376-141">A record set is a set of records with the same name and record type within a zone.</span></span>  <span data-ttu-id="d9376-142">The record set name is relative to the zone name, not the fully qualified DNS name.</span><span class="sxs-lookup"><span data-stu-id="d9376-142">The record set name is relative to the zone name, not the fully qualified DNS name.</span></span>

<span data-ttu-id="d9376-143">To create or update a record set, a "RecordSet" parameters object is created and passed to *DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span><span class="sxs-lookup"><span data-stu-id="d9376-143">To create or update a record set, a "RecordSet" parameters object is created and passed to *DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span></span> <span data-ttu-id="d9376-144">As with DNS zones, there are three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access to the HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span><span class="sxs-lookup"><span data-stu-id="d9376-144">As with DNS zones, there are three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access to the HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>

<span data-ttu-id="d9376-145">As with DNS zones, operations on record sets include support for optimistic concurrency.</span><span class="sxs-lookup"><span data-stu-id="d9376-145">As with DNS zones, operations on record sets include support for optimistic concurrency.</span></span>  <span data-ttu-id="d9376-146">In this example, since neither 'If-Match' nor 'If-None-Match' are specified, the record set is always created.</span><span class="sxs-lookup"><span data-stu-id="d9376-146">In this example, since neither 'If-Match' nor 'If-None-Match' are specified, the record set is always created.</span></span>  <span data-ttu-id="d9376-147">This call overwrites any existing record set with the same name and record type in this DNS zone.</span><span class="sxs-lookup"><span data-stu-id="d9376-147">This call overwrites any existing record set with the same name and record type in this DNS zone.</span></span>

```cs
// Create record set parameters
var recordSetParams = new RecordSet();
recordSetParams.TTL = 3600;

// Add records to the record set parameter object.  In this case, we'll add a record of type 'A'
recordSetParams.ARecords = new List<ARecord>();
recordSetParams.ARecords.Add(new ARecord("1.2.3.4"));

// Add metadata to the record set.  Similar to Azure Resource Manager tags, this is optional and you can add multiple metadata name/value pairs
recordSetParams.Metadata = new Dictionary<string, string>();
recordSetParams.Metadata.Add("user", "Mary");

// Create the actual record set in Azure DNS
// Note: no ETAG checks specified, will overwrite existing record set if one exists
var recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSetParams);
```

## <a name="get-zones-and-record-sets"></a><span data-ttu-id="d9376-148">Get zones and record sets</span><span class="sxs-lookup"><span data-stu-id="d9376-148">Get zones and record sets</span></span>

<span data-ttu-id="d9376-149">The *DnsManagementClient.Zones.Get* and *DnsManagementClient.RecordSets.Get* methods retrieve individual zones and record sets, respectively.</span><span class="sxs-lookup"><span data-stu-id="d9376-149">The *DnsManagementClient.Zones.Get* and *DnsManagementClient.RecordSets.Get* methods retrieve individual zones and record sets, respectively.</span></span> <span data-ttu-id="d9376-150">RecordSets are identified by their type, name, and the zone and resource group they exist in.</span><span class="sxs-lookup"><span data-stu-id="d9376-150">RecordSets are identified by their type, name, and the zone and resource group they exist in.</span></span> <span data-ttu-id="d9376-151">Zones are identified by their name and the resource group they exist in.</span><span class="sxs-lookup"><span data-stu-id="d9376-151">Zones are identified by their name and the resource group they exist in.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a><span data-ttu-id="d9376-152">Update an existing record set</span><span class="sxs-lookup"><span data-stu-id="d9376-152">Update an existing record set</span></span>

<span data-ttu-id="d9376-153">To update an existing DNS record set, first retrieve the record set, then update the record set contents, then submit the change.</span><span class="sxs-lookup"><span data-stu-id="d9376-153">To update an existing DNS record set, first retrieve the record set, then update the record set contents, then submit the change.</span></span>  <span data-ttu-id="d9376-154">In this example, we specify the 'Etag' from the retrieved record set in the 'If-Match' parameter.</span><span class="sxs-lookup"><span data-stu-id="d9376-154">In this example, we specify the 'Etag' from the retrieved record set in the 'If-Match' parameter.</span></span> <span data-ttu-id="d9376-155">The call fails if a concurrent operation has modified the record set in the meantime.</span><span class="sxs-lookup"><span data-stu-id="d9376-155">The call fails if a concurrent operation has modified the record set in the meantime.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record to the local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update the record set in Azure DNS
// Note: ETAG check specified, update will be rejected if the record set has changed in the meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a><span data-ttu-id="d9376-156">List zones and record sets</span><span class="sxs-lookup"><span data-stu-id="d9376-156">List zones and record sets</span></span>

<span data-ttu-id="d9376-157">To list zones, use the *DnsManagementClient.Zones.List...* methods, which support listing either all zones in a given resource group or all zones in a given Azure subscription (across resource groups.) To list record sets, use *DnsManagementClient.RecordSets.List...* methods, which support either listing all record sets in a given zone or only those record sets of a specific type.</span><span class="sxs-lookup"><span data-stu-id="d9376-157">To list zones, use the *DnsManagementClient.Zones.List...* methods, which support listing either all zones in a given resource group or all zones in a given Azure subscription (across resource groups.) To list record sets, use *DnsManagementClient.RecordSets.List...* methods, which support either listing all record sets in a given zone or only those record sets of a specific type.</span></span>

<span data-ttu-id="d9376-158">Note when listing zones and record sets that results may be paginated.</span><span class="sxs-lookup"><span data-stu-id="d9376-158">Note when listing zones and record sets that results may be paginated.</span></span>  <span data-ttu-id="d9376-159">The following example shows how to iterate through the pages of results.</span><span class="sxs-lookup"><span data-stu-id="d9376-159">The following example shows how to iterate through the pages of results.</span></span> <span data-ttu-id="d9376-160">(An artificially small page size of '2' is used to force paging; in practice this parameter should be omitted and the default page size used.)</span><span class="sxs-lookup"><span data-stu-id="d9376-160">(An artificially small page size of '2' is used to force paging; in practice this parameter should be omitted and the default page size used.)</span></span>

```cs
// Note: in this demo, we'll use a very small page size (2 record sets) to demonstrate paging
// In practice, to improve performance you would use a large page size or just use the system default
int recordSets = 0;
var page = await dnsClient.RecordSets.ListAllInResourceGroupAsync(resourceGroupName, zoneName, "2");
recordSets += page.Count();

while (page.NextPageLink != null)
{
    page = await dnsClient.RecordSets.ListAllInResourceGroupNextAsync(page.NextPageLink);
    recordSets += page.Count();
}
```

## <a name="next-steps"></a><span data-ttu-id="d9376-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="d9376-161">Next steps</span></span>

<span data-ttu-id="d9376-162">Download the [Azure DNS .NET SDK sample project](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), which includes further examples of how to use the Azure DNS .NET SDK, including examples for other DNS record types.</span><span class="sxs-lookup"><span data-stu-id="d9376-162">Download the [Azure DNS .NET SDK sample project](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), which includes further examples of how to use the Azure DNS .NET SDK, including examples for other DNS record types.</span></span>
