---
title: Get started with Azure DNS using the Azure portal | Microsoft Docs
description: Learn how to create a DNS zone and record in Azure DNS. This is a step-by-step guide to create and manage your first DNS zone and record using the Azure portal.
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 759312ea1f5f73f34a6b951dfcfd6388f96759bd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551122"
---
# <a name="get-started-with-azure-dns-using-the-azure-portal"></a><span data-ttu-id="a92fe-104">Get started with Azure DNS using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a92fe-104">Get started with Azure DNS using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Azure CLI 1.0](dns-getstarted-cli-nodejs.md)
> * [Azure CLI 2.0](dns-getstarted-cli.md)

<span data-ttu-id="a92fe-109">This article walks you through the steps to create your first DNS zone and record using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a92fe-109">This article walks you through the steps to create your first DNS zone and record using the Azure portal.</span></span> <span data-ttu-id="a92fe-110">You can also perform these steps using Azure PowerShell or the cross-platform Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a92fe-110">You can also perform these steps using Azure PowerShell or the cross-platform Azure CLI.</span></span>

<span data-ttu-id="a92fe-111">A DNS zone is used to host the DNS records for a particular domain.</span><span class="sxs-lookup"><span data-stu-id="a92fe-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="a92fe-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span><span class="sxs-lookup"><span data-stu-id="a92fe-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="a92fe-113">Each DNS record for your domain is then created inside this DNS zone.</span><span class="sxs-lookup"><span data-stu-id="a92fe-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="a92fe-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span><span class="sxs-lookup"><span data-stu-id="a92fe-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="a92fe-115">Each of these steps is described below.</span><span class="sxs-lookup"><span data-stu-id="a92fe-115">Each of these steps is described below.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="a92fe-116">Create a DNS zone</span><span class="sxs-lookup"><span data-stu-id="a92fe-116">Create a DNS zone</span></span>

1. <span data-ttu-id="a92fe-117">Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a92fe-117">Sign in to the Azure portal</span></span>
2. <span data-ttu-id="a92fe-118">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span><span class="sxs-lookup"><span data-stu-id="a92fe-118">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![DNS zone](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-getstarted-portal/openzone650.png)

4. <span data-ttu-id="a92fe-120">On the **Create DNS zone** blade, Name your DNS zone.</span><span class="sxs-lookup"><span data-stu-id="a92fe-120">On the **Create DNS zone** blade, Name your DNS zone.</span></span> <span data-ttu-id="a92fe-121">For example, *contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="a92fe-121">For example, *contoso.com*.</span></span>
 
    ![Create zone](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-getstarted-portal/newzone250.png)

5. <span data-ttu-id="a92fe-123">Next, specify the resource group that you want to use.</span><span class="sxs-lookup"><span data-stu-id="a92fe-123">Next, specify the resource group that you want to use.</span></span> <span data-ttu-id="a92fe-124">You can either create a new resource group, or select one that already exists.</span><span class="sxs-lookup"><span data-stu-id="a92fe-124">You can either create a new resource group, or select one that already exists.</span></span> <span data-ttu-id="a92fe-125">If you choose to create a new resource group, use the **Location** dropdown to specify the location of the resource group.</span><span class="sxs-lookup"><span data-stu-id="a92fe-125">If you choose to create a new resource group, use the **Location** dropdown to specify the location of the resource group.</span></span> <span data-ttu-id="a92fe-126">Note that this setting refers to the location of the resource group, and has no impact on the DNS zone.</span><span class="sxs-lookup"><span data-stu-id="a92fe-126">Note that this setting refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="a92fe-127">The DNS zone location is always "global", and is not shown.</span><span class="sxs-lookup"><span data-stu-id="a92fe-127">The DNS zone location is always "global", and is not shown.</span></span>

6. <span data-ttu-id="a92fe-128">You can leave the **Pin to dashboard** checkbox selected if you want to easily locate your new zone on your dashboard.</span><span class="sxs-lookup"><span data-stu-id="a92fe-128">You can leave the **Pin to dashboard** checkbox selected if you want to easily locate your new zone on your dashboard.</span></span> <span data-ttu-id="a92fe-129">Then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a92fe-129">Then click **Create**.</span></span>

    ![Pin to dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-getstarted-portal/pindashboard150.png)

7. <span data-ttu-id="a92fe-131">After you click Create, you'll see your new zone being configured on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="a92fe-131">After you click Create, you'll see your new zone being configured on the dashboard.</span></span>

    ![Creating](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-getstarted-portal/creating150.png)

8. <span data-ttu-id="a92fe-133">When your new zone has been created, the blade for your new zone opens on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="a92fe-133">When your new zone has been created, the blade for your new zone opens on the dashboard.</span></span>


## <a name="create-a-dns-record"></a><span data-ttu-id="a92fe-134">Create a DNS record</span><span class="sxs-lookup"><span data-stu-id="a92fe-134">Create a DNS record</span></span>

<span data-ttu-id="a92fe-135">The following example walks you through the process of creating new 'A' record.</span><span class="sxs-lookup"><span data-stu-id="a92fe-135">The following example walks you through the process of creating new 'A' record.</span></span> <span data-ttu-id="a92fe-136">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a92fe-136">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span> 


1. <span data-ttu-id="a92fe-137">At the top of the **DNS zone** blade, select **+ Record set** to open the **Add record set** blade.</span><span class="sxs-lookup"><span data-stu-id="a92fe-137">At the top of the **DNS zone** blade, select **+ Record set** to open the **Add record set** blade.</span></span>

    ![New record set](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-getstarted-portal/newrecordset500.png)

4. <span data-ttu-id="a92fe-139">On the **Add record set** blade, name your record set.</span><span class="sxs-lookup"><span data-stu-id="a92fe-139">On the **Add record set** blade, name your record set.</span></span> <span data-ttu-id="a92fe-140">For example, you could name your record set "**www**".</span><span class="sxs-lookup"><span data-stu-id="a92fe-140">For example, you could name your record set "**www**".</span></span>

    ![Add record set](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-getstarted-portal/addrecordset500.png)

5. <span data-ttu-id="a92fe-142">Select the type of record you want to create.</span><span class="sxs-lookup"><span data-stu-id="a92fe-142">Select the type of record you want to create.</span></span> <span data-ttu-id="a92fe-143">For this example, select **A**.</span><span class="sxs-lookup"><span data-stu-id="a92fe-143">For this example, select **A**.</span></span>
6. <span data-ttu-id="a92fe-144">Set the **TTL**.</span><span class="sxs-lookup"><span data-stu-id="a92fe-144">Set the **TTL**.</span></span> <span data-ttu-id="a92fe-145">The default time to live is one hour.</span><span class="sxs-lookup"><span data-stu-id="a92fe-145">The default time to live is one hour.</span></span>
7. <span data-ttu-id="a92fe-146">Add the IP address of the record.</span><span class="sxs-lookup"><span data-stu-id="a92fe-146">Add the IP address of the record.</span></span>
8. <span data-ttu-id="a92fe-147">Select **OK** at the bottom of the blade to create the DNS record.</span><span class="sxs-lookup"><span data-stu-id="a92fe-147">Select **OK** at the bottom of the blade to create the DNS record.</span></span>


## <a name="view-records"></a><span data-ttu-id="a92fe-148">View records</span><span class="sxs-lookup"><span data-stu-id="a92fe-148">View records</span></span>

<span data-ttu-id="a92fe-149">In the lower part of the DNS zone blade, you can see the records for the DNS zone.</span><span class="sxs-lookup"><span data-stu-id="a92fe-149">In the lower part of the DNS zone blade, you can see the records for the DNS zone.</span></span> <span data-ttu-id="a92fe-150">You should see the default DNS and SOA records, which are created in every zone, plus any new records you have created.</span><span class="sxs-lookup"><span data-stu-id="a92fe-150">You should see the default DNS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

![zone](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-getstarted-portal/viewzone500.png)


## <a name="update-name-servers"></a><span data-ttu-id="a92fe-152">Update name servers</span><span class="sxs-lookup"><span data-stu-id="a92fe-152">Update name servers</span></span>

<span data-ttu-id="a92fe-153">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span><span class="sxs-lookup"><span data-stu-id="a92fe-153">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="a92fe-154">This enables other users on the Internet to find your DNS records.</span><span class="sxs-lookup"><span data-stu-id="a92fe-154">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="a92fe-155">The name servers for your zone are given in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="a92fe-155">The name servers for your zone are given in the Azure portal:</span></span>

![zone](https://docstestmedia1.blob.core.windows.net/azure-media/articles/dns/media/dns-getstarted-portal/viewzonens500.png)

<span data-ttu-id="a92fe-157">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span><span class="sxs-lookup"><span data-stu-id="a92fe-157">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="a92fe-158">Your registrar will offer the option to set up the name servers for the domain.</span><span class="sxs-lookup"><span data-stu-id="a92fe-158">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="a92fe-159">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="a92fe-159">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="a92fe-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="a92fe-160">Next steps</span></span>

<span data-ttu-id="a92fe-161">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a92fe-161">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="a92fe-162">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a92fe-162">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>









