---
title: Quickstart - Create an Azure DNS zone and record using Azure CLI
description: Quickstart - Learn how to create a DNS zone and record in Azure DNS. This is a step-by-step guide to create and manage your first DNS zone and record using the Azure CLI.
services: dns
author: vhorne
ms.service: dns
ms.topic: quickstart
ms.date: 7/16/2018
ms.author: victorh
ms.openlocfilehash: 3fb39558ff99c35786dedc133a9d1d1a450b5928
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44776873"
---
# <a name="quickstart-create-an-azure-dns-zone-and-record-using-azure-cli"></a><span data-ttu-id="f41ae-104">Quickstart: Create an Azure DNS zone and record using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f41ae-104">Quickstart: Create an Azure DNS zone and record using Azure CLI</span></span>

<span data-ttu-id="f41ae-105">This article walks you through the steps to create your first DNS zone and record using Azure CLI, which is available for Windows, Mac and Linux.</span><span class="sxs-lookup"><span data-stu-id="f41ae-105">This article walks you through the steps to create your first DNS zone and record using Azure CLI, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="f41ae-106">You can also perform these steps using the [Azure portal](dns-getstarted-portal.md) or [Azure PowerShell](dns-getstarted-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f41ae-106">You can also perform these steps using the [Azure portal](dns-getstarted-portal.md) or [Azure PowerShell](dns-getstarted-powershell.md).</span></span>

<span data-ttu-id="f41ae-107">A DNS zone is used to host the DNS records for a particular domain.</span><span class="sxs-lookup"><span data-stu-id="f41ae-107">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="f41ae-108">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span><span class="sxs-lookup"><span data-stu-id="f41ae-108">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="f41ae-109">Each DNS record for your domain is then created inside this DNS zone.</span><span class="sxs-lookup"><span data-stu-id="f41ae-109">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="f41ae-110">Finally,to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span><span class="sxs-lookup"><span data-stu-id="f41ae-110">Finally,to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="f41ae-111">Each of these steps is described below.</span><span class="sxs-lookup"><span data-stu-id="f41ae-111">Each of these steps is described below.</span></span>

<span data-ttu-id="f41ae-112">Azure DNS now also supports private DNS zones (currently in public preview).</span><span class="sxs-lookup"><span data-stu-id="f41ae-112">Azure DNS now also supports private DNS zones (currently in public preview).</span></span> <span data-ttu-id="f41ae-113">To learn more about private DNS zones, see [Using Azure DNS for private domains](private-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f41ae-113">To learn more about private DNS zones, see [Using Azure DNS for private domains](private-dns-overview.md).</span></span> <span data-ttu-id="f41ae-114">For an example of how to create a private DNS zone, see [Get started with Azure DNS private zones using CLI](./private-dns-getstarted-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f41ae-114">For an example of how to create a private DNS zone, see [Get started with Azure DNS private zones using CLI](./private-dns-getstarted-cli.md).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f41ae-115">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="f41ae-115">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="f41ae-116">Create the resource group</span><span class="sxs-lookup"><span data-stu-id="f41ae-116">Create the resource group</span></span>

<span data-ttu-id="f41ae-117">Before you create the DNS zone, create a resource group to contain the DNS zone:</span><span class="sxs-lookup"><span data-stu-id="f41ae-117">Before you create the DNS zone, create a resource group to contain the DNS zone:</span></span>

```azurecli
az group create --name MyResourceGroup --location "East US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="f41ae-118">Create a DNS zone</span><span class="sxs-lookup"><span data-stu-id="f41ae-118">Create a DNS zone</span></span>

<span data-ttu-id="f41ae-119">A DNS zone is created using the `az network dns zone create` command.</span><span class="sxs-lookup"><span data-stu-id="f41ae-119">A DNS zone is created using the `az network dns zone create` command.</span></span> <span data-ttu-id="f41ae-120">To see help for this command, type `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="f41ae-120">To see help for this command, type `az network dns zone create -h`.</span></span>

<span data-ttu-id="f41ae-121">The following example creates a DNS zone called *contoso.com* in the resource group *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="f41ae-121">The following example creates a DNS zone called *contoso.com* in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="f41ae-122">Use the example to create a DNS zone, substituting the values for your own.</span><span class="sxs-lookup"><span data-stu-id="f41ae-122">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n contoso.com
```

## <a name="create-a-dns-record"></a><span data-ttu-id="f41ae-123">Create a DNS record</span><span class="sxs-lookup"><span data-stu-id="f41ae-123">Create a DNS record</span></span>

<span data-ttu-id="f41ae-124">To create a DNS record, use the `az network dns record-set [record type] add-record` command.</span><span class="sxs-lookup"><span data-stu-id="f41ae-124">To create a DNS record, use the `az network dns record-set [record type] add-record` command.</span></span> <span data-ttu-id="f41ae-125">For help, for A records for example, see `azure network dns record-set A add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="f41ae-125">For help, for A records for example, see `azure network dns record-set A add-record -h`.</span></span>

<span data-ttu-id="f41ae-126">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span><span class="sxs-lookup"><span data-stu-id="f41ae-126">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="f41ae-127">The fully-qualified name of the record set is "www.contoso.com".</span><span class="sxs-lookup"><span data-stu-id="f41ae-127">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="f41ae-128">The record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span><span class="sxs-lookup"><span data-stu-id="f41ae-128">The record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
az network dns record-set a add-record -g MyResourceGroup -z contoso.com -n www -a 1.2.3.4
```

## <a name="view-records"></a><span data-ttu-id="f41ae-129">View records</span><span class="sxs-lookup"><span data-stu-id="f41ae-129">View records</span></span>

<span data-ttu-id="f41ae-130">To list the DNS records in your zone, use:</span><span class="sxs-lookup"><span data-stu-id="f41ae-130">To list the DNS records in your zone, use:</span></span>

```azurecli
az network dns record-set list -g MyResourceGroup -z contoso.com
```

## <a name="update-name-servers"></a><span data-ttu-id="f41ae-131">Update name servers</span><span class="sxs-lookup"><span data-stu-id="f41ae-131">Update name servers</span></span>

<span data-ttu-id="f41ae-132">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span><span class="sxs-lookup"><span data-stu-id="f41ae-132">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="f41ae-133">This enables other users on the Internet to find your DNS records.</span><span class="sxs-lookup"><span data-stu-id="f41ae-133">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="f41ae-134">The name servers for your zone are given by the `az network dns zone show` command.</span><span class="sxs-lookup"><span data-stu-id="f41ae-134">The name servers for your zone are given by the `az network dns zone show` command.</span></span> <span data-ttu-id="f41ae-135">To see the name server names, use JSON output, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="f41ae-135">To see the name server names, use JSON output, as shown in the following example.</span></span>

```azurecli
az network dns zone show -g MyResourceGroup -n contoso.com -o json

{
  "etag": "00000003-0000-0000-b40d-0996b97ed101",
  "id": "/subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-01.azure-dns.com.",
    "ns2-01.azure-dns.net.",
    "ns3-01.azure-dns.org.",
    "ns4-01.azure-dns.info."
  ],
  "numberOfRecordSets": 3,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="f41ae-136">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span><span class="sxs-lookup"><span data-stu-id="f41ae-136">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="f41ae-137">Your registrar will offer the option to set up the name servers for the domain.</span><span class="sxs-lookup"><span data-stu-id="f41ae-137">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="f41ae-138">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="f41ae-138">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="f41ae-139">Delete all resources</span><span class="sxs-lookup"><span data-stu-id="f41ae-139">Delete all resources</span></span>
 
<span data-ttu-id="f41ae-140">When no longer needed, you can delete all resources created in this quickstart by deleting the resource group:</span><span class="sxs-lookup"><span data-stu-id="f41ae-140">When no longer needed, you can delete all resources created in this quickstart by deleting the resource group:</span></span>

```azurecli
az group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f41ae-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="f41ae-141">Next steps</span></span>

<span data-ttu-id="f41ae-142">Now that you've created your first DNS zone and record using Azure CLI, you can create records for a web app in a custom domain.</span><span class="sxs-lookup"><span data-stu-id="f41ae-142">Now that you've created your first DNS zone and record using Azure CLI, you can create records for a web app in a custom domain.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f41ae-143">Create DNS records for a web app in a custom domain</span><span class="sxs-lookup"><span data-stu-id="f41ae-143">Create DNS records for a web app in a custom domain</span></span>](./dns-web-sites-custom-domain.md)
