---
title: Reverse DNS for Azure services | Microsoft Docs
description: Learn how to configure reverse DNS lookups for services hosted in Azure
services: dns
documentationcenter: na
author: vhorne
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: victorh
ms.openlocfilehash: 0ff14ec2100d47e0edc5288f1c46f4fdd63fa683
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967218"
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a><span data-ttu-id="e7a5b-103">Configure reverse DNS for services hosted in Azure</span><span class="sxs-lookup"><span data-stu-id="e7a5b-103">Configure reverse DNS for services hosted in Azure</span></span>

<span data-ttu-id="e7a5b-104">This article explains how to configure reverse DNS lookups for services hosted in Azure.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-104">This article explains how to configure reverse DNS lookups for services hosted in Azure.</span></span>

<span data-ttu-id="e7a5b-105">Services in Azure use IP addresses assigned by Azure and owned by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-105">Services in Azure use IP addresses assigned by Azure and owned by Microsoft.</span></span> <span data-ttu-id="e7a5b-106">These reverse DNS records (PTR records) must be created in the corresponding Microsoft-owned reverse DNS lookup zones.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-106">These reverse DNS records (PTR records) must be created in the corresponding Microsoft-owned reverse DNS lookup zones.</span></span> <span data-ttu-id="e7a5b-107">This article explains how to do this.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-107">This article explains how to do this.</span></span>

<span data-ttu-id="e7a5b-108">This scenario should not be confused with the ability to [host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS](dns-reverse-dns-hosting.md).</span><span class="sxs-lookup"><span data-stu-id="e7a5b-108">This scenario should not be confused with the ability to [host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS](dns-reverse-dns-hosting.md).</span></span> <span data-ttu-id="e7a5b-109">In this case, the IP ranges represented by the reverse lookup zone must be assigned to your organization, typically by your ISP.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-109">In this case, the IP ranges represented by the reverse lookup zone must be assigned to your organization, typically by your ISP.</span></span>

<span data-ttu-id="e7a5b-110">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e7a5b-110">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="e7a5b-111">In Azure DNS, compute resources (such as virtual machines, virtual machine scale sets, or Service Fabric clusters) are exposed via a PublicIpAddress resource.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-111">In Azure DNS, compute resources (such as virtual machines, virtual machine scale sets, or Service Fabric clusters) are exposed via a PublicIpAddress resource.</span></span> <span data-ttu-id="e7a5b-112">Reverse DNS lookups are configured using the 'ReverseFqdn' property of the PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-112">Reverse DNS lookups are configured using the 'ReverseFqdn' property of the PublicIpAddress.</span></span>


<span data-ttu-id="e7a5b-113">Reverse DNS is not currently supported for the Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-113">Reverse DNS is not currently supported for the Azure App Service.</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="e7a5b-114">Validation of reverse DNS records</span><span class="sxs-lookup"><span data-stu-id="e7a5b-114">Validation of reverse DNS records</span></span>

<span data-ttu-id="e7a5b-115">A third party should not be able to create reverse DNS records for their Azure service mapping to your DNS domains.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-115">A third party should not be able to create reverse DNS records for their Azure service mapping to your DNS domains.</span></span> <span data-ttu-id="e7a5b-116">To prevent this, Azure only allows the creation of a reverse DNS record where domain name specified in the reverse DNS record is the same as, or resolves to, the DNS name or IP address of a PublicIpAddress or Cloud Service in the same Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-116">To prevent this, Azure only allows the creation of a reverse DNS record where domain name specified in the reverse DNS record is the same as, or resolves to, the DNS name or IP address of a PublicIpAddress or Cloud Service in the same Azure subscription.</span></span>

<span data-ttu-id="e7a5b-117">This validation is only performed when the reverse DNS record is set or modified.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-117">This validation is only performed when the reverse DNS record is set or modified.</span></span> <span data-ttu-id="e7a5b-118">Periodic re-validation is not performed.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-118">Periodic re-validation is not performed.</span></span>

<span data-ttu-id="e7a5b-119">For example: suppose the PublicIpAddress resource has the DNS name contosoapp1.northus.cloudapp.azure.com and IP address 23.96.52.53.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-119">For example: suppose the PublicIpAddress resource has the DNS name contosoapp1.northus.cloudapp.azure.com and IP address 23.96.52.53.</span></span> <span data-ttu-id="e7a5b-120">The ReverseFqdn for the PublicIpAddress can be specified as:</span><span class="sxs-lookup"><span data-stu-id="e7a5b-120">The ReverseFqdn for the PublicIpAddress can be specified as:</span></span>
* <span data-ttu-id="e7a5b-121">The DNS name for the PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="e7a5b-121">The DNS name for the PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span></span>
* <span data-ttu-id="e7a5b-122">The DNS name for a different PublicIpAddress in the same subscription, such as contosoapp2.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="e7a5b-122">The DNS name for a different PublicIpAddress in the same subscription, such as contosoapp2.westus.cloudapp.azure.com</span></span>
* <span data-ttu-id="e7a5b-123">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as a CNAME to contosoapp1.northus.cloudapp.azure.com, or to a different PublicIpAddress in the same subscription.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-123">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as a CNAME to contosoapp1.northus.cloudapp.azure.com, or to a different PublicIpAddress in the same subscription.</span></span>
* <span data-ttu-id="e7a5b-124">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as an A record to the IP address 23.96.52.53, or to the IP address of a different PublicIpAddress in the same subscription.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-124">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as an A record to the IP address 23.96.52.53, or to the IP address of a different PublicIpAddress in the same subscription.</span></span>

<span data-ttu-id="e7a5b-125">The same constraints apply to reverse DNS for Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-125">The same constraints apply to reverse DNS for Cloud Services.</span></span>


## <a name="reverse-dns-for-publicipaddress-resources"></a><span data-ttu-id="e7a5b-126">Reverse DNS for PublicIpAddress resources</span><span class="sxs-lookup"><span data-stu-id="e7a5b-126">Reverse DNS for PublicIpAddress resources</span></span>

<span data-ttu-id="e7a5b-127">This section provides detailed instructions for how to configure reverse DNS for PublicIpAddress resources in the Resource Manager deployment model, using either Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-127">This section provides detailed instructions for how to configure reverse DNS for PublicIpAddress resources in the Resource Manager deployment model, using either Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span></span> <span data-ttu-id="e7a5b-128">Configuring reverse DNS for PublicIpAddress resources is not currently supported via the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-128">Configuring reverse DNS for PublicIpAddress resources is not currently supported via the Azure portal.</span></span>

<span data-ttu-id="e7a5b-129">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-129">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources.</span></span> <span data-ttu-id="e7a5b-130">It is not supported for IPv6.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-130">It is not supported for IPv6.</span></span>

### <a name="add-reverse-dns-to-an-existing-publicipaddresses"></a><span data-ttu-id="e7a5b-131">Add reverse DNS to an existing PublicIpAddresses</span><span class="sxs-lookup"><span data-stu-id="e7a5b-131">Add reverse DNS to an existing PublicIpAddresses</span></span>

#### <a name="powershell"></a><span data-ttu-id="e7a5b-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7a5b-132">PowerShell</span></span>

<span data-ttu-id="e7a5b-133">To add reverse DNS to an existing PublicIpAddress:</span><span class="sxs-lookup"><span data-stu-id="e7a5b-133">To add reverse DNS to an existing PublicIpAddress:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

<span data-ttu-id="e7a5b-134">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span><span class="sxs-lookup"><span data-stu-id="e7a5b-134">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="e7a5b-135">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e7a5b-135">Azure CLI 1.0</span></span>

<span data-ttu-id="e7a5b-136">To add reverse DNS to an existing PublicIpAddress:</span><span class="sxs-lookup"><span data-stu-id="e7a5b-136">To add reverse DNS to an existing PublicIpAddress:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="e7a5b-137">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span><span class="sxs-lookup"><span data-stu-id="e7a5b-137">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="e7a5b-138">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e7a5b-138">Azure CLI 2.0</span></span>

<span data-ttu-id="e7a5b-139">To add reverse DNS to an existing PublicIpAddress:</span><span class="sxs-lookup"><span data-stu-id="e7a5b-139">To add reverse DNS to an existing PublicIpAddress:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="e7a5b-140">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span><span class="sxs-lookup"><span data-stu-id="e7a5b-140">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="e7a5b-141">Create a Public IP Address with reverse DNS</span><span class="sxs-lookup"><span data-stu-id="e7a5b-141">Create a Public IP Address with reverse DNS</span></span>

<span data-ttu-id="e7a5b-142">To create a new PublicIpAddress with the reverse DNS property already specified:</span><span class="sxs-lookup"><span data-stu-id="e7a5b-142">To create a new PublicIpAddress with the reverse DNS property already specified:</span></span>

#### <a name="powershell"></a><span data-ttu-id="e7a5b-143">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7a5b-143">PowerShell</span></span>

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a><span data-ttu-id="e7a5b-144">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e7a5b-144">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="e7a5b-145">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e7a5b-145">Azure CLI 2.0</span></span>

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a><span data-ttu-id="e7a5b-146">View reverse DNS for an existing PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="e7a5b-146">View reverse DNS for an existing PublicIpAddress</span></span>

<span data-ttu-id="e7a5b-147">To view the configured value for an existing PublicIpAddress:</span><span class="sxs-lookup"><span data-stu-id="e7a5b-147">To view the configured value for an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="e7a5b-148">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7a5b-148">PowerShell</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a><span data-ttu-id="e7a5b-149">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e7a5b-149">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a><span data-ttu-id="e7a5b-150">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e7a5b-150">Azure CLI 2.0</span></span>

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="e7a5b-151">Remove reverse DNS from existing Public IP Addresses</span><span class="sxs-lookup"><span data-stu-id="e7a5b-151">Remove reverse DNS from existing Public IP Addresses</span></span>

<span data-ttu-id="e7a5b-152">To remove a reverse DNS property from an existing PublicIpAddress:</span><span class="sxs-lookup"><span data-stu-id="e7a5b-152">To remove a reverse DNS property from an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="e7a5b-153">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7a5b-153">PowerShell</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="e7a5b-154">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e7a5b-154">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a><span data-ttu-id="e7a5b-155">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e7a5b-155">Azure CLI 2.0</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a><span data-ttu-id="e7a5b-156">Configure reverse DNS for Cloud Services</span><span class="sxs-lookup"><span data-stu-id="e7a5b-156">Configure reverse DNS for Cloud Services</span></span>

<span data-ttu-id="e7a5b-157">This section provides detailed instructions for how to configure reverse DNS for Cloud Services in the Classic deployment model, using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-157">This section provides detailed instructions for how to configure reverse DNS for Cloud Services in the Classic deployment model, using Azure PowerShell.</span></span> <span data-ttu-id="e7a5b-158">Configuring reverse DNS for Cloud Services is not supported via the Azure portal, Azure CLI 1.0, or Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-158">Configuring reverse DNS for Cloud Services is not supported via the Azure portal, Azure CLI 1.0, or Azure CLI 2.0.</span></span>

### <a name="add-reverse-dns-to-existing-cloud-services"></a><span data-ttu-id="e7a5b-159">Add reverse DNS to existing Cloud Services</span><span class="sxs-lookup"><span data-stu-id="e7a5b-159">Add reverse DNS to existing Cloud Services</span></span>

<span data-ttu-id="e7a5b-160">To add a reverse DNS record to an existing Cloud Service:</span><span class="sxs-lookup"><span data-stu-id="e7a5b-160">To add a reverse DNS record to an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a><span data-ttu-id="e7a5b-161">Create a Cloud Service with reverse DNS</span><span class="sxs-lookup"><span data-stu-id="e7a5b-161">Create a Cloud Service with reverse DNS</span></span>

<span data-ttu-id="e7a5b-162">To create a new Cloud Service with the reverse DNS property already specified:</span><span class="sxs-lookup"><span data-stu-id="e7a5b-162">To create a new Cloud Service with the reverse DNS property already specified:</span></span>

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a><span data-ttu-id="e7a5b-163">View reverse DNS for existing Cloud Services</span><span class="sxs-lookup"><span data-stu-id="e7a5b-163">View reverse DNS for existing Cloud Services</span></span>

<span data-ttu-id="e7a5b-164">To view the reverse DNS property for an existing Cloud Service:</span><span class="sxs-lookup"><span data-stu-id="e7a5b-164">To view the reverse DNS property for an existing Cloud Service:</span></span>

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a><span data-ttu-id="e7a5b-165">Remove reverse DNS from existing Cloud Services</span><span class="sxs-lookup"><span data-stu-id="e7a5b-165">Remove reverse DNS from existing Cloud Services</span></span>

<span data-ttu-id="e7a5b-166">To remove a reverse DNS property from an existing Cloud Service:</span><span class="sxs-lookup"><span data-stu-id="e7a5b-166">To remove a reverse DNS property from an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a><span data-ttu-id="e7a5b-167">FAQ</span><span class="sxs-lookup"><span data-stu-id="e7a5b-167">FAQ</span></span>

### <a name="how-much-do-reverse-dns-records-cost"></a><span data-ttu-id="e7a5b-168">How much do reverse DNS records cost?</span><span class="sxs-lookup"><span data-stu-id="e7a5b-168">How much do reverse DNS records cost?</span></span>

<span data-ttu-id="e7a5b-169">They're free!</span><span class="sxs-lookup"><span data-stu-id="e7a5b-169">They're free!</span></span>  <span data-ttu-id="e7a5b-170">There is no additional cost for reverse DNS records or queries.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-170">There is no additional cost for reverse DNS records or queries.</span></span>

### <a name="will-my-reverse-dns-records-resolve-from-the-internet"></a><span data-ttu-id="e7a5b-171">Will my reverse DNS records resolve from the internet?</span><span class="sxs-lookup"><span data-stu-id="e7a5b-171">Will my reverse DNS records resolve from the internet?</span></span>

<span data-ttu-id="e7a5b-172">Yes.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-172">Yes.</span></span> <span data-ttu-id="e7a5b-173">Once you set the reverse DNS property for your Azure service, Azure manages all the DNS delegations and DNS zones required to ensure that reverse DNS record resolves for all Internet users.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-173">Once you set the reverse DNS property for your Azure service, Azure manages all the DNS delegations and DNS zones required to ensure that reverse DNS record resolves for all Internet users.</span></span>

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a><span data-ttu-id="e7a5b-174">Are default reverse DNS records created for my Azure services?</span><span class="sxs-lookup"><span data-stu-id="e7a5b-174">Are default reverse DNS records created for my Azure services?</span></span>

<span data-ttu-id="e7a5b-175">No.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-175">No.</span></span> <span data-ttu-id="e7a5b-176">Reverse DNS is an opt-in feature.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-176">Reverse DNS is an opt-in feature.</span></span> <span data-ttu-id="e7a5b-177">No default reverse DNS records are created if you choose not to configure them.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-177">No default reverse DNS records are created if you choose not to configure them.</span></span>

### <a name="what-is-the-format-for-the-fully-qualified-domain-name-fqdn"></a><span data-ttu-id="e7a5b-178">What is the format for the fully-qualified domain name (FQDN)?</span><span class="sxs-lookup"><span data-stu-id="e7a5b-178">What is the format for the fully-qualified domain name (FQDN)?</span></span>

<span data-ttu-id="e7a5b-179">FQDNs are specified in forward order, and must be terminated by a dot (for example, "app1.contoso.com.").</span><span class="sxs-lookup"><span data-stu-id="e7a5b-179">FQDNs are specified in forward order, and must be terminated by a dot (for example, "app1.contoso.com.").</span></span>

### <a name="what-happens-if-the-validation-check-for-the-reverse-dns-ive-specified-fails"></a><span data-ttu-id="e7a5b-180">What happens if the validation check for the reverse DNS I've specified fails?</span><span class="sxs-lookup"><span data-stu-id="e7a5b-180">What happens if the validation check for the reverse DNS I've specified fails?</span></span>

<span data-ttu-id="e7a5b-181">Where the reverse DNS validation check fails, the operation to configure the reverse DNS record fails.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-181">Where the reverse DNS validation check fails, the operation to configure the reverse DNS record fails.</span></span> <span data-ttu-id="e7a5b-182">Correct the reverse DNS value as required, and retry.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-182">Correct the reverse DNS value as required, and retry.</span></span>

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a><span data-ttu-id="e7a5b-183">Can I configure reverse DNS for Azure App Service?</span><span class="sxs-lookup"><span data-stu-id="e7a5b-183">Can I configure reverse DNS for Azure App Service?</span></span>

<span data-ttu-id="e7a5b-184">No.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-184">No.</span></span> <span data-ttu-id="e7a5b-185">Reverse DNS is not supported for the Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-185">Reverse DNS is not supported for the Azure App Service.</span></span>

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a><span data-ttu-id="e7a5b-186">Can I configure multiple reverse DNS records for my Azure service?</span><span class="sxs-lookup"><span data-stu-id="e7a5b-186">Can I configure multiple reverse DNS records for my Azure service?</span></span>

<span data-ttu-id="e7a5b-187">No.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-187">No.</span></span> <span data-ttu-id="e7a5b-188">Azure supports a single reverse DNS record for each Azure Cloud Service or PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-188">Azure supports a single reverse DNS record for each Azure Cloud Service or PublicIpAddress.</span></span>

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a><span data-ttu-id="e7a5b-189">Can I configure reverse DNS for IPv6 PublicIpAddress resources?</span><span class="sxs-lookup"><span data-stu-id="e7a5b-189">Can I configure reverse DNS for IPv6 PublicIpAddress resources?</span></span>

<span data-ttu-id="e7a5b-190">No.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-190">No.</span></span> <span data-ttu-id="e7a5b-191">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources and Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-191">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources and Cloud Services.</span></span>

### <a name="can-i-send-emails-to-external-domains-from-my-azure-compute-services"></a><span data-ttu-id="e7a5b-192">Can I send emails to external domains from my Azure Compute services?</span><span class="sxs-lookup"><span data-stu-id="e7a5b-192">Can I send emails to external domains from my Azure Compute services?</span></span>

<span data-ttu-id="e7a5b-193">The technical ability to send email directly from an Azure deployment depends on the subscription type.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-193">The technical ability to send email directly from an Azure deployment depends on the subscription type.</span></span> <span data-ttu-id="e7a5b-194">Regardless of subscription type, Microsoft recommends using trusted mail relay services to send outgoing mail.</span><span class="sxs-lookup"><span data-stu-id="e7a5b-194">Regardless of subscription type, Microsoft recommends using trusted mail relay services to send outgoing mail.</span></span> <span data-ttu-id="e7a5b-195">For further details, see [Enhanced Azure Security for sending Emails – November 2017 Update](https://blogs.msdn.microsoft.com/mast/2017/11/15/enhanced-azure-security-for-sending-emails-november-2017-update/).</span><span class="sxs-lookup"><span data-stu-id="e7a5b-195">For further details, see [Enhanced Azure Security for sending Emails – November 2017 Update](https://blogs.msdn.microsoft.com/mast/2017/11/15/enhanced-azure-security-for-sending-emails-november-2017-update/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7a5b-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="e7a5b-196">Next steps</span></span>

<span data-ttu-id="e7a5b-197">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="e7a5b-197">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="e7a5b-198">Learn how to [host the reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="e7a5b-198">Learn how to [host the reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>

