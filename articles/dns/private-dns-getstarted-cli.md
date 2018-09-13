---
title: Create an Azure DNS private zone using Azure CLI
description: In this tutorial, you create and test a private DNS zone and record in Azure DNS. This is a step-by-step guide to create and manage your first private DNS zone and record using Azure CLI.
services: dns
author: vhorne
ms.service: dns
ms.topic: tutorial
ms.date: 7/25/2018
ms.author: victorh
ms.openlocfilehash: 023a1ecb6afc49dd20a14d57558d72a44779dbe9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870614"
---
# <a name="create-an-azure-dns-private-zone-using-azure-cli"></a><span data-ttu-id="2959e-104">Create an Azure DNS private zone using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2959e-104">Create an Azure DNS private zone using Azure CLI</span></span>

<span data-ttu-id="2959e-105">This tutorial walks you through the steps to create your first private DNS zone and record using Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2959e-105">This tutorial walks you through the steps to create your first private DNS zone and record using Azure CLI.</span></span>

[!INCLUDE [private-dns-public-preview-notice](../../includes/private-dns-public-preview-notice.md)]

<span data-ttu-id="2959e-106">A DNS zone is used to host the DNS records for a particular domain.</span><span class="sxs-lookup"><span data-stu-id="2959e-106">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="2959e-107">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span><span class="sxs-lookup"><span data-stu-id="2959e-107">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="2959e-108">Each DNS record for your domain is then created inside this DNS zone.</span><span class="sxs-lookup"><span data-stu-id="2959e-108">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="2959e-109">To publish a private DNS zone to your virtual network, you specify the list of virtual networks that are allowed to resolve records within the zone.</span><span class="sxs-lookup"><span data-stu-id="2959e-109">To publish a private DNS zone to your virtual network, you specify the list of virtual networks that are allowed to resolve records within the zone.</span></span>  <span data-ttu-id="2959e-110">These are called *resolution virtual networks*.</span><span class="sxs-lookup"><span data-stu-id="2959e-110">These are called *resolution virtual networks*.</span></span> <span data-ttu-id="2959e-111">You may also specify a virtual network for which Azure DNS maintains hostname records whenever a VM is created, changes IP, or is deleted.</span><span class="sxs-lookup"><span data-stu-id="2959e-111">You may also specify a virtual network for which Azure DNS maintains hostname records whenever a VM is created, changes IP, or is deleted.</span></span>  <span data-ttu-id="2959e-112">This is called a *registration virtual network*.</span><span class="sxs-lookup"><span data-stu-id="2959e-112">This is called a *registration virtual network*.</span></span>

<span data-ttu-id="2959e-113">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="2959e-113">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2959e-114">Create a DNS private zone</span><span class="sxs-lookup"><span data-stu-id="2959e-114">Create a DNS private zone</span></span>
> * <span data-ttu-id="2959e-115">Create test virtual machines</span><span class="sxs-lookup"><span data-stu-id="2959e-115">Create test virtual machines</span></span>
> * <span data-ttu-id="2959e-116">Create an additional DNS record</span><span class="sxs-lookup"><span data-stu-id="2959e-116">Create an additional DNS record</span></span>
> * <span data-ttu-id="2959e-117">Test the private zone</span><span class="sxs-lookup"><span data-stu-id="2959e-117">Test the private zone</span></span>

<span data-ttu-id="2959e-118">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="2959e-118">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="2959e-119">If you prefer, you can complete this tutorial using [Azure PowerShell](private-dns-getstarted-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2959e-119">If you prefer, you can complete this tutorial using [Azure PowerShell](private-dns-getstarted-powershell.md).</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-the-resource-group"></a><span data-ttu-id="2959e-120">Create the resource group</span><span class="sxs-lookup"><span data-stu-id="2959e-120">Create the resource group</span></span>

<span data-ttu-id="2959e-121">First, create a resource group to contain the DNS zone:</span><span class="sxs-lookup"><span data-stu-id="2959e-121">First, create a resource group to contain the DNS zone:</span></span> 

```azurecli
az group create --name MyAzureResourceGroup --location "East US"
```

## <a name="create-a-dns-private-zone"></a><span data-ttu-id="2959e-122">Create a DNS private zone</span><span class="sxs-lookup"><span data-stu-id="2959e-122">Create a DNS private zone</span></span>

<span data-ttu-id="2959e-123">A DNS zone is created by using the `az network dns zone create` command with a value of *Private* for the **ZoneType** parameter.</span><span class="sxs-lookup"><span data-stu-id="2959e-123">A DNS zone is created by using the `az network dns zone create` command with a value of *Private* for the **ZoneType** parameter.</span></span> <span data-ttu-id="2959e-124">The following example creates a DNS zone called **contoso.local** in the resource group called **MyAzureResourceGroup** and makes the DNS zone available to the virtual network called **MyAzureVnet**.</span><span class="sxs-lookup"><span data-stu-id="2959e-124">The following example creates a DNS zone called **contoso.local** in the resource group called **MyAzureResourceGroup** and makes the DNS zone available to the virtual network called **MyAzureVnet**.</span></span>

<span data-ttu-id="2959e-125">If the **ZoneType** parameter is omitted, the zone is created as a public zone, so it is required to create a private zone.</span><span class="sxs-lookup"><span data-stu-id="2959e-125">If the **ZoneType** parameter is omitted, the zone is created as a public zone, so it is required to create a private zone.</span></span>

```azurecli
az network vnet create \
  --name myAzureVNet \
  --resource-group MyAzureResourceGroup \
  --location eastus \
  --address-prefix 10.2.0.0/16 \
  --subnet-name backendSubnet \
  --subnet-prefix 10.2.0.0/24

az network dns zone create -g MyAzureResourceGroup \
   -n contoso.local \
  --zone-type Private \
  --registration-vnets myAzureVNet
```

<span data-ttu-id="2959e-126">If you wanted to create a zone just for name resolution (no automatic hostname creation), you could use the *resolution-vnets* parameter instead of the *registration-vnets* parameter.</span><span class="sxs-lookup"><span data-stu-id="2959e-126">If you wanted to create a zone just for name resolution (no automatic hostname creation), you could use the *resolution-vnets* parameter instead of the *registration-vnets* parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="2959e-127">You won't be able to see the automatically created hostname records.</span><span class="sxs-lookup"><span data-stu-id="2959e-127">You won't be able to see the automatically created hostname records.</span></span> <span data-ttu-id="2959e-128">But later, you will test to ensure they exist.</span><span class="sxs-lookup"><span data-stu-id="2959e-128">But later, you will test to ensure they exist.</span></span>

### <a name="list-dns-private-zones"></a><span data-ttu-id="2959e-129">List DNS private zones</span><span class="sxs-lookup"><span data-stu-id="2959e-129">List DNS private zones</span></span>

<span data-ttu-id="2959e-130">To enumerate DNS zones, use `az network dns zone list`.</span><span class="sxs-lookup"><span data-stu-id="2959e-130">To enumerate DNS zones, use `az network dns zone list`.</span></span> <span data-ttu-id="2959e-131">For help, see `az network dns zone list --help`.</span><span class="sxs-lookup"><span data-stu-id="2959e-131">For help, see `az network dns zone list --help`.</span></span>

<span data-ttu-id="2959e-132">Specifying the resource group lists only those zones within the resource group:</span><span class="sxs-lookup"><span data-stu-id="2959e-132">Specifying the resource group lists only those zones within the resource group:</span></span>

```azurecli
az network dns zone list \
  --resource-group MyAzureResourceGroup
```

<span data-ttu-id="2959e-133">Omitting the resource group lists all zones in the subscription:</span><span class="sxs-lookup"><span data-stu-id="2959e-133">Omitting the resource group lists all zones in the subscription:</span></span>

```azurecli
az network dns zone list 
```

## <a name="create-the-test-virtual-machines"></a><span data-ttu-id="2959e-134">Create the test virtual machines</span><span class="sxs-lookup"><span data-stu-id="2959e-134">Create the test virtual machines</span></span>

<span data-ttu-id="2959e-135">Now, create two virtual machines so you can test your private DNS zone:</span><span class="sxs-lookup"><span data-stu-id="2959e-135">Now, create two virtual machines so you can test your private DNS zone:</span></span>

```azurecli
az vm create \
 -n myVM01 \
 --admin-username test-user \
 -g MyAzureResourceGroup \
 -l eastus \
 --subnet backendSubnet \
 --vnet-name myAzureVnet \
 --image win2016datacenter

az vm create \
 -n myVM02 \
 --admin-username test-user \
 -g MyAzureResourceGroup \
 -l eastus \
 --subnet backendSubnet \
 --vnet-name myAzureVnet \
 --image win2016datacenter
```

<span data-ttu-id="2959e-136">This will take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="2959e-136">This will take a few minutes to complete.</span></span>

## <a name="create-an-additional-dns-record"></a><span data-ttu-id="2959e-137">Create an additional DNS record</span><span class="sxs-lookup"><span data-stu-id="2959e-137">Create an additional DNS record</span></span>

<span data-ttu-id="2959e-138">To create a DNS record, use the `az network dns record-set [record type] add-record` command.</span><span class="sxs-lookup"><span data-stu-id="2959e-138">To create a DNS record, use the `az network dns record-set [record type] add-record` command.</span></span> <span data-ttu-id="2959e-139">For help with adding A records for example, see `azure network dns record-set A add-record --help`.</span><span class="sxs-lookup"><span data-stu-id="2959e-139">For help with adding A records for example, see `azure network dns record-set A add-record --help`.</span></span>

 <span data-ttu-id="2959e-140">The following example creates a record with the relative name **db** in the DNS Zone **contoso.local**, in resource group **MyAzureResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="2959e-140">The following example creates a record with the relative name **db** in the DNS Zone **contoso.local**, in resource group **MyAzureResourceGroup**.</span></span> <span data-ttu-id="2959e-141">The fully qualified name of the record set is **db.contoso.local**.</span><span class="sxs-lookup"><span data-stu-id="2959e-141">The fully qualified name of the record set is **db.contoso.local**.</span></span> <span data-ttu-id="2959e-142">The record type is "A", with IP address "10.2.0.4".</span><span class="sxs-lookup"><span data-stu-id="2959e-142">The record type is "A", with IP address "10.2.0.4".</span></span>

```azurecli
az network dns record-set a add-record \
  -g MyAzureResourceGroup \
  -z contoso.local \
  -n db \
  -a 10.2.0.4
```

### <a name="view-dns-records"></a><span data-ttu-id="2959e-143">View DNS records</span><span class="sxs-lookup"><span data-stu-id="2959e-143">View DNS records</span></span>

<span data-ttu-id="2959e-144">To list the DNS records in your zone, run:</span><span class="sxs-lookup"><span data-stu-id="2959e-144">To list the DNS records in your zone, run:</span></span>

```azurecli
az network dns record-set list \
  -g MyAzureResourceGroup \
  -z contoso.local
```
<span data-ttu-id="2959e-145">Remember, you won't see the automatically created A records for your two test virtual machines.</span><span class="sxs-lookup"><span data-stu-id="2959e-145">Remember, you won't see the automatically created A records for your two test virtual machines.</span></span>

## <a name="test-the-private-zone"></a><span data-ttu-id="2959e-146">Test the private zone</span><span class="sxs-lookup"><span data-stu-id="2959e-146">Test the private zone</span></span>

<span data-ttu-id="2959e-147">Now you can test the name resolution for your **contoso.local** private zone.</span><span class="sxs-lookup"><span data-stu-id="2959e-147">Now you can test the name resolution for your **contoso.local** private zone.</span></span>

### <a name="configure-vms-to-allow-inbound-icmp"></a><span data-ttu-id="2959e-148">Configure VMs to allow inbound ICMP</span><span class="sxs-lookup"><span data-stu-id="2959e-148">Configure VMs to allow inbound ICMP</span></span>

<span data-ttu-id="2959e-149">You can use the ping command to test name resolution.</span><span class="sxs-lookup"><span data-stu-id="2959e-149">You can use the ping command to test name resolution.</span></span> <span data-ttu-id="2959e-150">So, configure the firewall on both virtual machines to allow inbound ICMP packets.</span><span class="sxs-lookup"><span data-stu-id="2959e-150">So, configure the firewall on both virtual machines to allow inbound ICMP packets.</span></span>

1. <span data-ttu-id="2959e-151">Connect to myVM01, and open a Windows PowerShell window with administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="2959e-151">Connect to myVM01, and open a Windows PowerShell window with administrator privileges.</span></span>
2. <span data-ttu-id="2959e-152">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="2959e-152">Run the following command:</span></span>

   ```powershell
   New-NetFirewallRule –DisplayName “Allow ICMPv4-In” –Protocol ICMPv4
   ```

<span data-ttu-id="2959e-153">Repeat for myVM02.</span><span class="sxs-lookup"><span data-stu-id="2959e-153">Repeat for myVM02.</span></span>

### <a name="ping-the-vms-by-name"></a><span data-ttu-id="2959e-154">Ping the VMs by name</span><span class="sxs-lookup"><span data-stu-id="2959e-154">Ping the VMs by name</span></span>

1. <span data-ttu-id="2959e-155">From the myVM02 Windows PowerShell command prompt, ping myVM01 using the automatically registered host name:</span><span class="sxs-lookup"><span data-stu-id="2959e-155">From the myVM02 Windows PowerShell command prompt, ping myVM01 using the automatically registered host name:</span></span>
   ```
   ping myVM01.contoso.local
   ```
   <span data-ttu-id="2959e-156">You should see output that looks similar to this:</span><span class="sxs-lookup"><span data-stu-id="2959e-156">You should see output that looks similar to this:</span></span>
   ```
   PS C:\> ping myvm01.contoso.local

   Pinging myvm01.contoso.local [10.2.0.4] with 32 bytes of data:
   Reply from 10.2.0.4: bytes=32 time<1ms TTL=128
   Reply from 10.2.0.4: bytes=32 time=1ms TTL=128
   Reply from 10.2.0.4: bytes=32 time<1ms TTL=128
   Reply from 10.2.0.4: bytes=32 time<1ms TTL=128

   Ping statistics for 10.2.0.4:
       Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
   Approximate round trip times in milli-seconds:
       Minimum = 0ms, Maximum = 1ms, Average = 0ms
   PS C:\>
   ```
2. <span data-ttu-id="2959e-157">Now ping the **db** name you created previously:</span><span class="sxs-lookup"><span data-stu-id="2959e-157">Now ping the **db** name you created previously:</span></span>
   ```
   ping db.contoso.local
   ```
   <span data-ttu-id="2959e-158">You should see output that looks similar to this:</span><span class="sxs-lookup"><span data-stu-id="2959e-158">You should see output that looks similar to this:</span></span>
   ```
   PS C:\> ping db.contoso.local

   Pinging db.contoso.local [10.2.0.4] with 32 bytes of data:
   Reply from 10.2.0.4: bytes=32 time<1ms TTL=128
   Reply from 10.2.0.4: bytes=32 time<1ms TTL=128
   Reply from 10.2.0.4: bytes=32 time<1ms TTL=128
   Reply from 10.2.0.4: bytes=32 time<1ms TTL=128

   Ping statistics for 10.2.0.4:
       Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
   Approximate round trip times in milli-seconds:
       Minimum = 0ms, Maximum = 0ms, Average = 0ms
   PS C:\>
   ```

## <a name="delete-all-resources"></a><span data-ttu-id="2959e-159">Delete all resources</span><span class="sxs-lookup"><span data-stu-id="2959e-159">Delete all resources</span></span>

<span data-ttu-id="2959e-160">When no longer needed, delete the **MyAzureResourceGroup** resource group to delete the resources created in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="2959e-160">When no longer needed, delete the **MyAzureResourceGroup** resource group to delete the resources created in this tutorial.</span></span>

```azurecli
az group delete --name MyAzureResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="2959e-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="2959e-161">Next steps</span></span>

<span data-ttu-id="2959e-162">In this tutorial, you deployed a private DNS zone, created a DNS record, and tested the zone.</span><span class="sxs-lookup"><span data-stu-id="2959e-162">In this tutorial, you deployed a private DNS zone, created a DNS record, and tested the zone.</span></span>
<span data-ttu-id="2959e-163">Next, you can learn more about private DNS zones.</span><span class="sxs-lookup"><span data-stu-id="2959e-163">Next, you can learn more about private DNS zones.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2959e-164">Using Azure DNS for private domains</span><span class="sxs-lookup"><span data-stu-id="2959e-164">Using Azure DNS for private domains</span></span>](private-dns-overview.md)