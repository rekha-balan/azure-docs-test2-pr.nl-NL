---
title: Understanding DNS in Azure Stack | Microsoft Docs
description: Understanding DNS features and capabilities in Azure Stack
services: azure-stack
documentationcenter: ''
author: ScottNapolitan
manager: darmour
editor: ''
ms.assetid: 60f5ac85-be19-49ac-a7c1-f290d682b5de
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/6/2017
ms.author: scottnap
ms.openlocfilehash: a1e41cf6fb0591c142ba127c185e603a098a0c5f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562932"
---
# <a name="introducing-idns-for-azure-stack"></a><span data-ttu-id="4ec32-103">Introducing iDNS for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="4ec32-103">Introducing iDNS for Azure Stack</span></span>
================================

<span data-ttu-id="4ec32-104">iDNS is a new feature in Technology Preview 2 for Azure Stack that allows you to resolve external DNS names (such as http://www.bing.com).</span><span class="sxs-lookup"><span data-stu-id="4ec32-104">iDNS is a new feature in Technology Preview 2 for Azure Stack that allows you to resolve external DNS names (such as http://www.bing.com).</span></span>
<span data-ttu-id="4ec32-105">It also allows you to register internal virtual network names.</span><span class="sxs-lookup"><span data-stu-id="4ec32-105">It also allows you to register internal virtual network names.</span></span> <span data-ttu-id="4ec32-106">By doing so, you can resolve VMs on the same virtual network by name rather than IP address, without having to provide custom DNS server entries.</span><span class="sxs-lookup"><span data-stu-id="4ec32-106">By doing so, you can resolve VMs on the same virtual network by name rather than IP address, without having to provide custom DNS server entries.</span></span>

<span data-ttu-id="4ec32-107">It’s something that’s always been there in Azure, but now it's available in Windows Server 2016 and Azure Stack, too.</span><span class="sxs-lookup"><span data-stu-id="4ec32-107">It’s something that’s always been there in Azure, but now it's available in Windows Server 2016 and Azure Stack, too.</span></span>

## <a name="what-does-idns-do"></a><span data-ttu-id="4ec32-108">What does iDNS do?</span><span class="sxs-lookup"><span data-stu-id="4ec32-108">What does iDNS do?</span></span>
<span data-ttu-id="4ec32-109">With iDNS in Azure Stack, you get the following capabilities, without having to specify custom DNS server entries.</span><span class="sxs-lookup"><span data-stu-id="4ec32-109">With iDNS in Azure Stack, you get the following capabilities, without having to specify custom DNS server entries.</span></span>

* <span data-ttu-id="4ec32-110">Shared DNS name resolution services for tenant workloads.</span><span class="sxs-lookup"><span data-stu-id="4ec32-110">Shared DNS name resolution services for tenant workloads.</span></span>
* <span data-ttu-id="4ec32-111">Authoritative DNS service for name resolution and DNS registration within the tenant virtual network.</span><span class="sxs-lookup"><span data-stu-id="4ec32-111">Authoritative DNS service for name resolution and DNS registration within the tenant virtual network.</span></span>
* <span data-ttu-id="4ec32-112">Recursive DNS service for resolution of Internet names from tenant VMs.</span><span class="sxs-lookup"><span data-stu-id="4ec32-112">Recursive DNS service for resolution of Internet names from tenant VMs.</span></span> <span data-ttu-id="4ec32-113">Tenants no longer need to specify custom DNS entries to resolve Internet names (for example, www.bing.com).</span><span class="sxs-lookup"><span data-stu-id="4ec32-113">Tenants no longer need to specify custom DNS entries to resolve Internet names (for example, www.bing.com).</span></span>

<span data-ttu-id="4ec32-114">You can still bring your own DNS and use custom DNS servers if you want.</span><span class="sxs-lookup"><span data-stu-id="4ec32-114">You can still bring your own DNS and use custom DNS servers if you want.</span></span> <span data-ttu-id="4ec32-115">But now, if you just want to be able to resolve Internet DNS names and be able to connect to other virtual machines in the same virtual network, you don’t need to specify anything and it will just work.</span><span class="sxs-lookup"><span data-stu-id="4ec32-115">But now, if you just want to be able to resolve Internet DNS names and be able to connect to other virtual machines in the same virtual network, you don’t need to specify anything and it will just work.</span></span>

## <a name="what-does-idns-not-do"></a><span data-ttu-id="4ec32-116">What does iDNS not do?</span><span class="sxs-lookup"><span data-stu-id="4ec32-116">What does iDNS not do?</span></span>
<span data-ttu-id="4ec32-117">What iDNS does not allow you to do is create a DNS record for a name that can be resolved from outside the virtual network.</span><span class="sxs-lookup"><span data-stu-id="4ec32-117">What iDNS does not allow you to do is create a DNS record for a name that can be resolved from outside the virtual network.</span></span>

<span data-ttu-id="4ec32-118">In Azure, you have the option of specifying a DNS name label that can be associated with a public IP address.</span><span class="sxs-lookup"><span data-stu-id="4ec32-118">In Azure, you have the option of specifying a DNS name label that can be associated with a public IP address.</span></span> <span data-ttu-id="4ec32-119">You can choose the label (prefix), but Azure chooses the suffix, which is based on the region in which you create the public IP address.</span><span class="sxs-lookup"><span data-stu-id="4ec32-119">You can choose the label (prefix), but Azure chooses the suffix, which is based on the region in which you create the public IP address.</span></span>

![Screenshot of DNS name label](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-understanding-dns-in-tp2/image3.png)

<span data-ttu-id="4ec32-121">In the image above, Azure will create an “A” record in DNS for the DNS name label specified under the zone **westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="4ec32-121">In the image above, Azure will create an “A” record in DNS for the DNS name label specified under the zone **westus.cloudapp.azure.com**.</span></span> <span data-ttu-id="4ec32-122">The prefix and the suffix together compose a Fully Qualified Domain Name (FQDN) that can be resolved from anywhere on the public Internet.</span><span class="sxs-lookup"><span data-stu-id="4ec32-122">The prefix and the suffix together compose a Fully Qualified Domain Name (FQDN) that can be resolved from anywhere on the public Internet.</span></span>

<span data-ttu-id="4ec32-123">In TP2, Azure Stack only supports iDNS for internal name registration, so it cannot do the following.</span><span class="sxs-lookup"><span data-stu-id="4ec32-123">In TP2, Azure Stack only supports iDNS for internal name registration, so it cannot do the following.</span></span>

* <span data-ttu-id="4ec32-124">Create a DNS record under an existing hosted DNS zone (for example, local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="4ec32-124">Create a DNS record under an existing hosted DNS zone (for example, local.azurestack.external).</span></span>
* <span data-ttu-id="4ec32-125">Create a DNS zone (such as Contoso.com).</span><span class="sxs-lookup"><span data-stu-id="4ec32-125">Create a DNS zone (such as Contoso.com).</span></span>
* <span data-ttu-id="4ec32-126">Create a record under your own custom DNS zone.</span><span class="sxs-lookup"><span data-stu-id="4ec32-126">Create a record under your own custom DNS zone.</span></span>
* <span data-ttu-id="4ec32-127">Support the purchase of domain names.</span><span class="sxs-lookup"><span data-stu-id="4ec32-127">Support the purchase of domain names.</span></span>

## <a name="changes-in-dns-from-azure-stack-tp1"></a><span data-ttu-id="4ec32-128">Changes in DNS from Azure Stack TP1</span><span class="sxs-lookup"><span data-stu-id="4ec32-128">Changes in DNS from Azure Stack TP1</span></span>
<span data-ttu-id="4ec32-129">In the Technology Preview 1 (TP1) release of Azure Stack, you had to provide custom DNS servers if you wanted to be able to resolve hosts by name rather than by IP address.</span><span class="sxs-lookup"><span data-stu-id="4ec32-129">In the Technology Preview 1 (TP1) release of Azure Stack, you had to provide custom DNS servers if you wanted to be able to resolve hosts by name rather than by IP address.</span></span> <span data-ttu-id="4ec32-130">This means that if you were creating a virtual network or a VM, you had to provide at least one DNS server entry.</span><span class="sxs-lookup"><span data-stu-id="4ec32-130">This means that if you were creating a virtual network or a VM, you had to provide at least one DNS server entry.</span></span> <span data-ttu-id="4ec32-131">For the TP1 POC environment, this meant entering the IP of the POC Fabric DNS server, namely 192.168.200.2.</span><span class="sxs-lookup"><span data-stu-id="4ec32-131">For the TP1 POC environment, this meant entering the IP of the POC Fabric DNS server, namely 192.168.200.2.</span></span>

<span data-ttu-id="4ec32-132">If you created a VM via the portal, you had to select **Custom DNS** in the virtual network or ethernet adapter settings.</span><span class="sxs-lookup"><span data-stu-id="4ec32-132">If you created a VM via the portal, you had to select **Custom DNS** in the virtual network or ethernet adapter settings.</span></span>

![Screenshot of specifying a custom DNS server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-understanding-dns-in-tp2/image1.png)

<span data-ttu-id="4ec32-134">In TP2, you can select Azure DNS and do not need to specify custom DNS server entries.</span><span class="sxs-lookup"><span data-stu-id="4ec32-134">In TP2, you can select Azure DNS and do not need to specify custom DNS server entries.</span></span>

<span data-ttu-id="4ec32-135">If you created a VM via a template with your own image, you had to add the **DHCPOptions** property and the DNS server in order to get the DNS name resolution to work.</span><span class="sxs-lookup"><span data-stu-id="4ec32-135">If you created a VM via a template with your own image, you had to add the **DHCPOptions** property and the DNS server in order to get the DNS name resolution to work.</span></span> <span data-ttu-id="4ec32-136">The following image shows what this looked like.</span><span class="sxs-lookup"><span data-stu-id="4ec32-136">The following image shows what this looked like.</span></span>

![Screenshot of DHCPOptions property](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-understanding-dns-in-tp2/image2.png)

<span data-ttu-id="4ec32-138">In TP2, you no longer need to make these changes to your VM templates to allow your VMs to resolve Internet names.</span><span class="sxs-lookup"><span data-stu-id="4ec32-138">In TP2, you no longer need to make these changes to your VM templates to allow your VMs to resolve Internet names.</span></span> <span data-ttu-id="4ec32-139">They should just work.</span><span class="sxs-lookup"><span data-stu-id="4ec32-139">They should just work.</span></span>



