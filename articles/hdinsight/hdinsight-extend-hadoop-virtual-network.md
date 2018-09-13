---
title: Extend HDInsight with Virtual Network | Microsoft Docs
description: Learn how to use Azure Virtual Network to connect HDInsight to other cloud resources, or resources in your datacenter
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 37b9b600-d7f8-4cb1-a04a-0b3a827c6dcc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/20/2017
ms.author: larryfr
ms.openlocfilehash: 1f21ff6ca9ac9b60ba6f5692e6e5e1100149e825
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671766"
---
# <a name="extend-hdinsight-capabilities-by-using-azure-virtual-network"></a><span data-ttu-id="a4d0c-103">Extend HDInsight capabilities by using Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="a4d0c-103">Extend HDInsight capabilities by using Azure Virtual Network</span></span>

<span data-ttu-id="a4d0c-104">Learn how to use Azure Virtual Networks with HDInsight to enable the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="a4d0c-104">Learn how to use Azure Virtual Networks with HDInsight to enable the following scenarios:</span></span>

* <span data-ttu-id="a4d0c-105">Restrict access to HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-105">Restrict access to HDInsight.</span></span> <span data-ttu-id="a4d0c-106">For example, prevent inbound traffic from the internet.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-106">For example, prevent inbound traffic from the internet.</span></span>

* <span data-ttu-id="a4d0c-107">Directly access services on HDInsight that aren't exposed over the Internet.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-107">Directly access services on HDInsight that aren't exposed over the Internet.</span></span> <span data-ttu-id="a4d0c-108">For example, directly work with Kafka brokers or use the HBase Java API.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-108">For example, directly work with Kafka brokers or use the HBase Java API.</span></span>

* <span data-ttu-id="a4d0c-109">Directly connect services to HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-109">Directly connect services to HDInsight.</span></span> <span data-ttu-id="a4d0c-110">For example, use Oozie to import or export data to a SQL Server within your data center.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-110">For example, use Oozie to import or export data to a SQL Server within your data center.</span></span>

* <span data-ttu-id="a4d0c-111">Create solutions that involve multiple HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-111">Create solutions that involve multiple HDInsight clusters.</span></span> <span data-ttu-id="a4d0c-112">For example, use Spark or Storm to analyze data stored in Kafka.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-112">For example, use Spark or Storm to analyze data stored in Kafka.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4d0c-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a4d0c-113">Prerequisites</span></span>

* <span data-ttu-id="a4d0c-114">Azure CLI 2.0: For more information, see [Install and Configure Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="a4d0c-114">Azure CLI 2.0: For more information, see [Install and Configure Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

* <span data-ttu-id="a4d0c-115">Azure PowerShell: For more information, see [Install and Configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a4d0c-115">Azure PowerShell: For more information, see [Install and Configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>

> [!NOTE]
> <span data-ttu-id="a4d0c-116">The steps in this document require the latest version of the Azure CLI and Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-116">The steps in this document require the latest version of the Azure CLI and Azure PowerShell.</span></span> <span data-ttu-id="a4d0c-117">If you are using an older version, the commands may be different.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-117">If you are using an older version, the commands may be different.</span></span> <span data-ttu-id="a4d0c-118">For best results, use the previous links to install the latest versions.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-118">For best results, use the previous links to install the latest versions.</span></span>

## <a id="whatis"></a><span data-ttu-id="a4d0c-119">What is Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="a4d0c-119">What is Azure Virtual Network</span></span>

<span data-ttu-id="a4d0c-120">[Azure Virtual Network](https://azure.microsoft.com/documentation/services/virtual-network/) allows you to create a secure, persistent network containing the resources you need for your solution.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-120">[Azure Virtual Network](https://azure.microsoft.com/documentation/services/virtual-network/) allows you to create a secure, persistent network containing the resources you need for your solution.</span></span>

<span data-ttu-id="a4d0c-121">The following are a list of considerations when using HDInsight in a virtual network:</span><span class="sxs-lookup"><span data-stu-id="a4d0c-121">The following are a list of considerations when using HDInsight in a virtual network:</span></span>

* <span data-ttu-id="a4d0c-122">__Classic and Resource Manager virtual networks__: Use the following table to determine the type of network to use based on the HDInsight cluster operating system:</span><span class="sxs-lookup"><span data-stu-id="a4d0c-122">__Classic and Resource Manager virtual networks__: Use the following table to determine the type of network to use based on the HDInsight cluster operating system:</span></span>

    | <span data-ttu-id="a4d0c-123">HDInsight operating system</span><span class="sxs-lookup"><span data-stu-id="a4d0c-123">HDInsight operating system</span></span> | <span data-ttu-id="a4d0c-124">Classic virtual network</span><span class="sxs-lookup"><span data-stu-id="a4d0c-124">Classic virtual network</span></span> | <span data-ttu-id="a4d0c-125">Resource Manager virtual network</span><span class="sxs-lookup"><span data-stu-id="a4d0c-125">Resource Manager virtual network</span></span> |
    | ---- | ---- | ---- |
    | <span data-ttu-id="a4d0c-126">Linux</span><span class="sxs-lookup"><span data-stu-id="a4d0c-126">Linux</span></span> | <span data-ttu-id="a4d0c-127">no</span><span class="sxs-lookup"><span data-stu-id="a4d0c-127">no</span></span> | <span data-ttu-id="a4d0c-128">yes</span><span class="sxs-lookup"><span data-stu-id="a4d0c-128">yes</span></span> |
    | <span data-ttu-id="a4d0c-129">Windows</span><span class="sxs-lookup"><span data-stu-id="a4d0c-129">Windows</span></span> | <span data-ttu-id="a4d0c-130">yes</span><span class="sxs-lookup"><span data-stu-id="a4d0c-130">yes</span></span> | <span data-ttu-id="a4d0c-131">no</span><span class="sxs-lookup"><span data-stu-id="a4d0c-131">no</span></span> |

    <span data-ttu-id="a4d0c-132">To access resources in an incompatible virtual network, join the two networks.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-132">To access resources in an incompatible virtual network, join the two networks.</span></span> <span data-ttu-id="a4d0c-133">For more information on connecting classic and Resource Manager Virtual Networks, see [Connecting classic VNets to new VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a4d0c-133">For more information on connecting classic and Resource Manager Virtual Networks, see [Connecting classic VNets to new VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

* <span data-ttu-id="a4d0c-134">__Custom DNS__: Azure provides name resolution for Azure services that are installed in an Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-134">__Custom DNS__: Azure provides name resolution for Azure services that are installed in an Azure Virtual Network.</span></span> <span data-ttu-id="a4d0c-135">This name resolution does not extend outside the virtual network.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-135">This name resolution does not extend outside the virtual network.</span></span> <span data-ttu-id="a4d0c-136">To enable name resolution for resources outside the virtual network, you must use a custom DNS server.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-136">To enable name resolution for resources outside the virtual network, you must use a custom DNS server.</span></span> <span data-ttu-id="a4d0c-137">For more information on using a custom DNS server, see the [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-137">For more information on using a custom DNS server, see the [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span></span>

* <span data-ttu-id="a4d0c-138">__Forced tunneling__: HDInsight does not support the forced tunneling configuration of Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-138">__Forced tunneling__: HDInsight does not support the forced tunneling configuration of Azure Virtual Network.</span></span>

* <span data-ttu-id="a4d0c-139">__Restricting network traffic__: HDInsight does support using Network Security Groups to restrict network traffic, but requires unrestricted access to several Azure IPs.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-139">__Restricting network traffic__: HDInsight does support using Network Security Groups to restrict network traffic, but requires unrestricted access to several Azure IPs.</span></span> <span data-ttu-id="a4d0c-140">For more information, see the [Secured virtual networks](#secured-virtual-networks) section.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-140">For more information, see the [Secured virtual networks](#secured-virtual-networks) section.</span></span>

### <a name="connect-cloud-resources-together-in-a-private-network-cloud-only"></a><span data-ttu-id="a4d0c-141">Connect cloud resources together in a private network (cloud-only)</span><span class="sxs-lookup"><span data-stu-id="a4d0c-141">Connect cloud resources together in a private network (cloud-only)</span></span>

![diagram of cloud-only configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-extend-hadoop-virtual-network/cloud-only.png)

<span data-ttu-id="a4d0c-143">Using Virtual Network to link Azure services with Azure HDInsight enables the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="a4d0c-143">Using Virtual Network to link Azure services with Azure HDInsight enables the following scenarios:</span></span>

* <span data-ttu-id="a4d0c-144">**Invoking HDInsight services or jobs** from Azure websites or services running in Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-144">**Invoking HDInsight services or jobs** from Azure websites or services running in Azure virtual machines.</span></span>

* <span data-ttu-id="a4d0c-145">**Directly transferring data** between HDInsight and Azure SQL Database, SQL Server, or another data storage solution running on a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-145">**Directly transferring data** between HDInsight and Azure SQL Database, SQL Server, or another data storage solution running on a virtual machine.</span></span>

* <span data-ttu-id="a4d0c-146">**Combining multiple HDInsight servers** into a single solution.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-146">**Combining multiple HDInsight servers** into a single solution.</span></span> <span data-ttu-id="a4d0c-147">There are several types of HDInsight clusters, which correspond to the workload or technology that the cluster is tuned for.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-147">There are several types of HDInsight clusters, which correspond to the workload or technology that the cluster is tuned for.</span></span> <span data-ttu-id="a4d0c-148">There is no supported method to create a cluster that combines multiple types, such as Storm and HBase on one cluster.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-148">There is no supported method to create a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span> <span data-ttu-id="a4d0c-149">Using a virtual network allows multiple clusters to directly communicate with each other.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-149">Using a virtual network allows multiple clusters to directly communicate with each other.</span></span>

### <a name="connect-cloud-resources-to-a-local-datacenter-network"></a><span data-ttu-id="a4d0c-150">Connect cloud resources to a local datacenter network</span><span class="sxs-lookup"><span data-stu-id="a4d0c-150">Connect cloud resources to a local datacenter network</span></span>

<span data-ttu-id="a4d0c-151">Site-to-site configuration allows you to connect multiple resources in your datacenter to the Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-151">Site-to-site configuration allows you to connect multiple resources in your datacenter to the Azure virtual network.</span></span> <span data-ttu-id="a4d0c-152">The connection can be made using a hardware VPN device or the Routing and Remote Access service.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-152">The connection can be made using a hardware VPN device or the Routing and Remote Access service.</span></span>

![diagram of site-to-site configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-extend-hadoop-virtual-network/site-to-site.png)

<span data-ttu-id="a4d0c-154">Point-to-site configuration allows you to connect a specific resource to the Azure virtual network by using software VPN.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-154">Point-to-site configuration allows you to connect a specific resource to the Azure virtual network by using software VPN.</span></span>

![diagram of point-to-site configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-extend-hadoop-virtual-network/point-to-site.png)

<span data-ttu-id="a4d0c-156">Using Virtual Network to link the cloud and your datacenter enables similar scenarios to the cloud-only configuration.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-156">Using Virtual Network to link the cloud and your datacenter enables similar scenarios to the cloud-only configuration.</span></span> <span data-ttu-id="a4d0c-157">But instead of being limited to working with resources in the cloud, you can also work with resources in your datacenter.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-157">But instead of being limited to working with resources in the cloud, you can also work with resources in your datacenter.</span></span>

* <span data-ttu-id="a4d0c-158">**Directly transferring data** between HDInsight and your datacenter.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-158">**Directly transferring data** between HDInsight and your datacenter.</span></span> <span data-ttu-id="a4d0c-159">An example is using Sqoop to transfer data to or from SQL Server or reading data generated by a line-of-business (LOB) application.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-159">An example is using Sqoop to transfer data to or from SQL Server or reading data generated by a line-of-business (LOB) application.</span></span>

* <span data-ttu-id="a4d0c-160">**Invoking HDInsight services or jobs** from an LOB application.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-160">**Invoking HDInsight services or jobs** from an LOB application.</span></span> <span data-ttu-id="a4d0c-161">An example is using HBase Java APIs to store and retrieve data from an HDInsight HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-161">An example is using HBase Java APIs to store and retrieve data from an HDInsight HBase cluster.</span></span>

<span data-ttu-id="a4d0c-162">For more information on Virtual Network features, benefits, and capabilities, see the [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4d0c-162">For more information on Virtual Network features, benefits, and capabilities, see the [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a4d0c-163">Create the Azure Virtual Network before provisioning an HDInsight cluster, then specify the network when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-163">Create the Azure Virtual Network before provisioning an HDInsight cluster, then specify the network when creating the cluster.</span></span> <span data-ttu-id="a4d0c-164">For more information, see [Virtual Network configuration tasks](https://azure.microsoft.com/documentation/services/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="a4d0c-164">For more information, see [Virtual Network configuration tasks](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="secured-virtual-networks"></a><span data-ttu-id="a4d0c-165">Secured virtual networks</span><span class="sxs-lookup"><span data-stu-id="a4d0c-165">Secured virtual networks</span></span>

<span data-ttu-id="a4d0c-166">The HDInsight service is a managed service, and requires access to Azure management services during provisioning and while running.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-166">The HDInsight service is a managed service, and requires access to Azure management services during provisioning and while running.</span></span> <span data-ttu-id="a4d0c-167">Azure management performs the following services:</span><span class="sxs-lookup"><span data-stu-id="a4d0c-167">Azure management performs the following services:</span></span>

* <span data-ttu-id="a4d0c-168">Monitor the health of the cluster</span><span class="sxs-lookup"><span data-stu-id="a4d0c-168">Monitor the health of the cluster</span></span>
* <span data-ttu-id="a4d0c-169">Initiate failover of cluster resources</span><span class="sxs-lookup"><span data-stu-id="a4d0c-169">Initiate failover of cluster resources</span></span>
* <span data-ttu-id="a4d0c-170">Change the number of nodes in the cluster through scaling operations</span><span class="sxs-lookup"><span data-stu-id="a4d0c-170">Change the number of nodes in the cluster through scaling operations</span></span>
* <span data-ttu-id="a4d0c-171">Other management tasks</span><span class="sxs-lookup"><span data-stu-id="a4d0c-171">Other management tasks</span></span>

> [!NOTE]
> <span data-ttu-id="a4d0c-172">These operations do not require full access to the internet.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-172">These operations do not require full access to the internet.</span></span> <span data-ttu-id="a4d0c-173">When restricting internet access, allow inbound access on port 443 for the following IP addresses.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-173">When restricting internet access, allow inbound access on port 443 for the following IP addresses.</span></span> <span data-ttu-id="a4d0c-174">This allows Azure to manage HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a4d0c-174">This allows Azure to manage HDInsight:</span></span>

<span data-ttu-id="a4d0c-175">The IP addresses that should be allowed are specific to the region that the HDInsight cluster and Virtual Network reside in.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-175">The IP addresses that should be allowed are specific to the region that the HDInsight cluster and Virtual Network reside in.</span></span> <span data-ttu-id="a4d0c-176">Use the following table to find the IP addresses for the region you are using.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-176">Use the following table to find the IP addresses for the region you are using.</span></span>

| <span data-ttu-id="a4d0c-177">Country</span><span class="sxs-lookup"><span data-stu-id="a4d0c-177">Country</span></span> | <span data-ttu-id="a4d0c-178">Region</span><span class="sxs-lookup"><span data-stu-id="a4d0c-178">Region</span></span> | <span data-ttu-id="a4d0c-179">Allowed IP addresses</span><span class="sxs-lookup"><span data-stu-id="a4d0c-179">Allowed IP addresses</span></span> | <span data-ttu-id="a4d0c-180">Allowed port</span><span class="sxs-lookup"><span data-stu-id="a4d0c-180">Allowed port</span></span> |
| ---- | ---- | ---- | ---- |
| <span data-ttu-id="a4d0c-181">Brazil</span><span class="sxs-lookup"><span data-stu-id="a4d0c-181">Brazil</span></span> | <span data-ttu-id="a4d0c-182">Brazil South</span><span class="sxs-lookup"><span data-stu-id="a4d0c-182">Brazil South</span></span> | <span data-ttu-id="a4d0c-183">191.235.84.104</span><span class="sxs-lookup"><span data-stu-id="a4d0c-183">191.235.84.104</span></span></br><span data-ttu-id="a4d0c-184">191.235.87.113</span><span class="sxs-lookup"><span data-stu-id="a4d0c-184">191.235.87.113</span></span> | <span data-ttu-id="a4d0c-185">443</span><span class="sxs-lookup"><span data-stu-id="a4d0c-185">443</span></span> |
| <span data-ttu-id="a4d0c-186">Canada</span><span class="sxs-lookup"><span data-stu-id="a4d0c-186">Canada</span></span> | <span data-ttu-id="a4d0c-187">Canada East</span><span class="sxs-lookup"><span data-stu-id="a4d0c-187">Canada East</span></span> | <span data-ttu-id="a4d0c-188">52.229.127.96</span><span class="sxs-lookup"><span data-stu-id="a4d0c-188">52.229.127.96</span></span></br><span data-ttu-id="a4d0c-189">52.229.123.172</span><span class="sxs-lookup"><span data-stu-id="a4d0c-189">52.229.123.172</span></span> | <span data-ttu-id="a4d0c-190">443</span><span class="sxs-lookup"><span data-stu-id="a4d0c-190">443</span></span> |
| &nbsp; | <span data-ttu-id="a4d0c-191">Canada Central</span><span class="sxs-lookup"><span data-stu-id="a4d0c-191">Canada Central</span></span> | <span data-ttu-id="a4d0c-192">52.228.37.66</span><span class="sxs-lookup"><span data-stu-id="a4d0c-192">52.228.37.66</span></span></br><span data-ttu-id="a4d0c-193">52.228.45.222</span><span class="sxs-lookup"><span data-stu-id="a4d0c-193">52.228.45.222</span></span> | <span data-ttu-id="a4d0c-194">443</span><span class="sxs-lookup"><span data-stu-id="a4d0c-194">443</span></span> |
| <span data-ttu-id="a4d0c-195">Germany</span><span class="sxs-lookup"><span data-stu-id="a4d0c-195">Germany</span></span> | <span data-ttu-id="a4d0c-196">Germany Central</span><span class="sxs-lookup"><span data-stu-id="a4d0c-196">Germany Central</span></span> | <span data-ttu-id="a4d0c-197">51.4.146.68</span><span class="sxs-lookup"><span data-stu-id="a4d0c-197">51.4.146.68</span></span></br><span data-ttu-id="a4d0c-198">51.4.146.80</span><span class="sxs-lookup"><span data-stu-id="a4d0c-198">51.4.146.80</span></span> | <span data-ttu-id="a4d0c-199">443</span><span class="sxs-lookup"><span data-stu-id="a4d0c-199">443</span></span> |
| &nbsp; | <span data-ttu-id="a4d0c-200">Germany Northeast</span><span class="sxs-lookup"><span data-stu-id="a4d0c-200">Germany Northeast</span></span> | <span data-ttu-id="a4d0c-201">51.5.150.132</span><span class="sxs-lookup"><span data-stu-id="a4d0c-201">51.5.150.132</span></span></br><span data-ttu-id="a4d0c-202">51.5.144.101</span><span class="sxs-lookup"><span data-stu-id="a4d0c-202">51.5.144.101</span></span> | <span data-ttu-id="a4d0c-203">443</span><span class="sxs-lookup"><span data-stu-id="a4d0c-203">443</span></span> |
| <span data-ttu-id="a4d0c-204">India</span><span class="sxs-lookup"><span data-stu-id="a4d0c-204">India</span></span> | <span data-ttu-id="a4d0c-205">Central India</span><span class="sxs-lookup"><span data-stu-id="a4d0c-205">Central India</span></span> | <span data-ttu-id="a4d0c-206">52.172.153.209</span><span class="sxs-lookup"><span data-stu-id="a4d0c-206">52.172.153.209</span></span></br><span data-ttu-id="a4d0c-207">52.172.152.49</span><span class="sxs-lookup"><span data-stu-id="a4d0c-207">52.172.152.49</span></span> | <span data-ttu-id="a4d0c-208">443</span><span class="sxs-lookup"><span data-stu-id="a4d0c-208">443</span></span> |
| <span data-ttu-id="a4d0c-209">United Kingdom</span><span class="sxs-lookup"><span data-stu-id="a4d0c-209">United Kingdom</span></span> | <span data-ttu-id="a4d0c-210">UK West</span><span class="sxs-lookup"><span data-stu-id="a4d0c-210">UK West</span></span> | <span data-ttu-id="a4d0c-211">51.141.13.110</span><span class="sxs-lookup"><span data-stu-id="a4d0c-211">51.141.13.110</span></span></br><span data-ttu-id="a4d0c-212">51.141.7.20</span><span class="sxs-lookup"><span data-stu-id="a4d0c-212">51.141.7.20</span></span> | <span data-ttu-id="a4d0c-213">443</span><span class="sxs-lookup"><span data-stu-id="a4d0c-213">443</span></span> |
| &nbsp; | <span data-ttu-id="a4d0c-214">UK South</span><span class="sxs-lookup"><span data-stu-id="a4d0c-214">UK South</span></span> | <span data-ttu-id="a4d0c-215">51.140.47.39</span><span class="sxs-lookup"><span data-stu-id="a4d0c-215">51.140.47.39</span></span></br><span data-ttu-id="a4d0c-216">51.140.52.16</span><span class="sxs-lookup"><span data-stu-id="a4d0c-216">51.140.52.16</span></span> | <span data-ttu-id="a4d0c-217">443</span><span class="sxs-lookup"><span data-stu-id="a4d0c-217">443</span></span> |
| <span data-ttu-id="a4d0c-218">United States</span><span class="sxs-lookup"><span data-stu-id="a4d0c-218">United States</span></span> | <span data-ttu-id="a4d0c-219">West Central US</span><span class="sxs-lookup"><span data-stu-id="a4d0c-219">West Central US</span></span> | <span data-ttu-id="a4d0c-220">52.161.23.15</span><span class="sxs-lookup"><span data-stu-id="a4d0c-220">52.161.23.15</span></span></br><span data-ttu-id="a4d0c-221">52.161.10.167</span><span class="sxs-lookup"><span data-stu-id="a4d0c-221">52.161.10.167</span></span> | <span data-ttu-id="a4d0c-222">443</span><span class="sxs-lookup"><span data-stu-id="a4d0c-222">443</span></span> |
| &nbsp; | <span data-ttu-id="a4d0c-223">West US 2</span><span class="sxs-lookup"><span data-stu-id="a4d0c-223">West US 2</span></span> | <span data-ttu-id="a4d0c-224">52.175.211.210</span><span class="sxs-lookup"><span data-stu-id="a4d0c-224">52.175.211.210</span></span></br><span data-ttu-id="a4d0c-225">52.175.222.222</span><span class="sxs-lookup"><span data-stu-id="a4d0c-225">52.175.222.222</span></span> | <span data-ttu-id="a4d0c-226">443</span><span class="sxs-lookup"><span data-stu-id="a4d0c-226">443</span></span> |

<span data-ttu-id="a4d0c-227">__If your region is not listed in the table__, allow traffic to port __443__ on the following IP addresses:</span><span class="sxs-lookup"><span data-stu-id="a4d0c-227">__If your region is not listed in the table__, allow traffic to port __443__ on the following IP addresses:</span></span>

* <span data-ttu-id="a4d0c-228">168.61.49.99</span><span class="sxs-lookup"><span data-stu-id="a4d0c-228">168.61.49.99</span></span>
* <span data-ttu-id="a4d0c-229">23.99.5.239</span><span class="sxs-lookup"><span data-stu-id="a4d0c-229">23.99.5.239</span></span>
* <span data-ttu-id="a4d0c-230">168.61.48.131</span><span class="sxs-lookup"><span data-stu-id="a4d0c-230">168.61.48.131</span></span>
* <span data-ttu-id="a4d0c-231">138.91.141.162</span><span class="sxs-lookup"><span data-stu-id="a4d0c-231">138.91.141.162</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a4d0c-232">HDInsight doesn't support restricting outbound traffic, only inbound traffic.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-232">HDInsight doesn't support restricting outbound traffic, only inbound traffic.</span></span> <span data-ttu-id="a4d0c-233">When defining Network Security Group rules for the subnet that contains HDInsight, __only use inbound rules__.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-233">When defining Network Security Group rules for the subnet that contains HDInsight, __only use inbound rules__.</span></span>

### <a name="working-with-hdinsight-in-secured-virtual-networks"></a><span data-ttu-id="a4d0c-234">Working with HDInsight in secured virtual networks</span><span class="sxs-lookup"><span data-stu-id="a4d0c-234">Working with HDInsight in secured virtual networks</span></span>

<span data-ttu-id="a4d0c-235">If you block internet access, you cannot use HDInsight services that are normally exposed through the public gateway for a cluster.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-235">If you block internet access, you cannot use HDInsight services that are normally exposed through the public gateway for a cluster.</span></span> <span data-ttu-id="a4d0c-236">These include Ambari and SSH.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-236">These include Ambari and SSH.</span></span> <span data-ttu-id="a4d0c-237">Instead, you must access services using the internal IP address of the cluster head nodes.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-237">Instead, you must access services using the internal IP address of the cluster head nodes.</span></span>

<span data-ttu-id="a4d0c-238">To find the internal IP address of the head nodes, use the scripts in the [Internal IPs and FQDNs](#internal-ips-and-fqdns) section.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-238">To find the internal IP address of the head nodes, use the scripts in the [Internal IPs and FQDNs](#internal-ips-and-fqdns) section.</span></span>

### <a name="example-secured-virtual-network"></a><span data-ttu-id="a4d0c-239">Example: Secured virtual network</span><span class="sxs-lookup"><span data-stu-id="a4d0c-239">Example: Secured virtual network</span></span>

<span data-ttu-id="a4d0c-240">The following examples demonstrate how to create a Network Security Group that allows inbound traffic on port 443 from the following IP addresses:</span><span class="sxs-lookup"><span data-stu-id="a4d0c-240">The following examples demonstrate how to create a Network Security Group that allows inbound traffic on port 443 from the following IP addresses:</span></span>

* <span data-ttu-id="a4d0c-241">168.61.49.99</span><span class="sxs-lookup"><span data-stu-id="a4d0c-241">168.61.49.99</span></span>
* <span data-ttu-id="a4d0c-242">23.99.5.239</span><span class="sxs-lookup"><span data-stu-id="a4d0c-242">23.99.5.239</span></span>
* <span data-ttu-id="a4d0c-243">168.61.48.131</span><span class="sxs-lookup"><span data-stu-id="a4d0c-243">168.61.48.131</span></span>
* <span data-ttu-id="a4d0c-244">138.91.141.162</span><span class="sxs-lookup"><span data-stu-id="a4d0c-244">138.91.141.162</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a4d0c-245">These addresses are for regions that do not have specific IP addresses listed.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-245">These addresses are for regions that do not have specific IP addresses listed.</span></span> <span data-ttu-id="a4d0c-246">To find the IP addresses for your region, use the information in the [Secured Virtual Networks](#secured-virtual-networks) section.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-246">To find the IP addresses for your region, use the information in the [Secured Virtual Networks](#secured-virtual-networks) section.</span></span>

<span data-ttu-id="a4d0c-247">These steps assume that you have already created a Virtual Network and subnet that you want to install HDInsight into.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-247">These steps assume that you have already created a Virtual Network and subnet that you want to install HDInsight into.</span></span> <span data-ttu-id="a4d0c-248">See [Create a virtual network using the Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="a4d0c-248">See [Create a virtual network using the Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

> [!WARNING]
> <span data-ttu-id="a4d0c-249">Rules are tested against network traffic in order by __priority__.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-249">Rules are tested against network traffic in order by __priority__.</span></span> <span data-ttu-id="a4d0c-250">Once a rule matches the test criteria, it is applied and no more rules are tested for that request.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-250">Once a rule matches the test criteria, it is applied and no more rules are tested for that request.</span></span> <span data-ttu-id="a4d0c-251">If you have a rule that broadly blocks inbound traffic (such as a **deny all** rule), it __must__ come after the rules that allow traffic.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-251">If you have a rule that broadly blocks inbound traffic (such as a **deny all** rule), it __must__ come after the rules that allow traffic.</span></span>
>
> <span data-ttu-id="a4d0c-252">For more information on Network Security Group rules, see the [What is a Network Security Group](../virtual-network/virtual-networks-nsg.md) document.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-252">For more information on Network Security Group rules, see the [What is a Network Security Group](../virtual-network/virtual-networks-nsg.md) document.</span></span>

<span data-ttu-id="a4d0c-253">**Example: Azure Resource Management template**</span><span class="sxs-lookup"><span data-stu-id="a4d0c-253">**Example: Azure Resource Management template**</span></span>

<span data-ttu-id="a4d0c-254">Using the following Resource Management template from the [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/) to create an HDInsight cluster in a VNet with the secure network configurations:</span><span class="sxs-lookup"><span data-stu-id="a4d0c-254">Using the following Resource Management template from the [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/) to create an HDInsight cluster in a VNet with the secure network configurations:</span></span>

[<span data-ttu-id="a4d0c-255">Deploy a secured Azure VNet and an HDInsight Hadoop cluster within the VNet</span><span class="sxs-lookup"><span data-stu-id="a4d0c-255">Deploy a secured Azure VNet and an HDInsight Hadoop cluster within the VNet</span></span>](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

<span data-ttu-id="a4d0c-256">**Example: Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="a4d0c-256">**Example: Azure PowerShell**</span></span>

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with the resource group the virtual network is in"
$subnetName = "Replace with the name of the subnet that HDInsight will be installed into"
# Get the Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get the region the Virtual network is in.
$location = $vnet.Location
# Get the subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for the HDInsight health and management services.
$nsg = New-AzureRmNetworkSecurityGroup `
    -Name "hdisecure" `
    -ResourceGroupName $resourceGroupName `
    -Location $location `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -name "hdirule1" `
        -Description "HDI health and management address 168.61.49.99" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.49.99" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 300 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 23.99.5.239" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "23.99.5.239" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 301 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule3" `
        -Description "HDI health and management 168.61.48.131" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.48.131" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 302 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule4" `
        -Description "HDI health and management 138.91.141.162" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "138.91.141.162" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 303 `
        -Direction Inbound
# Set the changes to the security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply the NSG to the subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

<span data-ttu-id="a4d0c-257">**Example: Azure CLI**</span><span class="sxs-lookup"><span data-stu-id="a4d0c-257">**Example: Azure CLI**</span></span>

1. <span data-ttu-id="a4d0c-258">Use the following command to create a new network security group named `hdisecure`.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-258">Use the following command to create a new network security group named `hdisecure`.</span></span> <span data-ttu-id="a4d0c-259">Replace **RESOURCEGROUPNAME** with the resource group that contains the Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-259">Replace **RESOURCEGROUPNAME** with the resource group that contains the Azure Virtual Network.</span></span> <span data-ttu-id="a4d0c-260">Replace **LOCATION** with the location (region) that the group was created in.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-260">Replace **LOCATION** with the location (region) that the group was created in.</span></span>

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    <span data-ttu-id="a4d0c-261">Once the group has been created, you receive information on the new group.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-261">Once the group has been created, you receive information on the new group.</span></span>

2. <span data-ttu-id="a4d0c-262">Use the following to add rules to the new network security group that allow inbound communication on port 443 from the Azure HDInsight health and management service.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-262">Use the following to add rules to the new network security group that allow inbound communication on port 443 from the Azure HDInsight health and management service.</span></span> <span data-ttu-id="a4d0c-263">Replace **RESOURCEGROUPNAME** with the name of the resource group that contains the Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-263">Replace **RESOURCEGROUPNAME** with the name of the resource group that contains the Azure Virtual Network.</span></span>

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99/24" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239/24" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule3 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131/24" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule4 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162/24" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    ```

3. <span data-ttu-id="a4d0c-264">Once the rules have been created, use the following to retrieve the unique identifier for this network security group:</span><span class="sxs-lookup"><span data-stu-id="a4d0c-264">Once the rules have been created, use the following to retrieve the unique identifier for this network security group:</span></span>

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    <span data-ttu-id="a4d0c-265">This command returns a value similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="a4d0c-265">This command returns a value similar to the following text:</span></span>

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    <span data-ttu-id="a4d0c-266">Use double-quotes around id in the command if you don't get the expected results.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-266">Use double-quotes around id in the command if you don't get the expected results.</span></span>

4. <span data-ttu-id="a4d0c-267">Using the following command to apply the network security group to a subnet.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-267">Using the following command to apply the network security group to a subnet.</span></span> <span data-ttu-id="a4d0c-268">Replace the __GUID__ and __RESOURCEGROUPNAME__ values with the ones returned from the previous step.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-268">Replace the __GUID__ and __RESOURCEGROUPNAME__ values with the ones returned from the previous step.</span></span> <span data-ttu-id="a4d0c-269">Replace __VNETNAME__ and __SUBNETNAME__ with the virtual network name and subnet name that you want to use when creating an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-269">Replace __VNETNAME__ and __SUBNETNAME__ with the virtual network name and subnet name that you want to use when creating an HDInsight cluster.</span></span>

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    <span data-ttu-id="a4d0c-270">Once this command completes, you can successfully install HDInsight into the secured Virtual Network on the subnet used in these steps.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-270">Once this command completes, you can successfully install HDInsight into the secured Virtual Network on the subnet used in these steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a4d0c-271">Using the preceding steps only open access to the HDInsight health and management service on the Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-271">Using the preceding steps only open access to the HDInsight health and management service on the Azure cloud.</span></span> <span data-ttu-id="a4d0c-272">Any other access to the HDInsight cluster from outside the Virtual Network is blocked.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-272">Any other access to the HDInsight cluster from outside the Virtual Network is blocked.</span></span> <span data-ttu-id="a4d0c-273">To enable access from outside the virtual network, you must add additional Network Security Group rules.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-273">To enable access from outside the virtual network, you must add additional Network Security Group rules.</span></span>
>
> <span data-ttu-id="a4d0c-274">The following example demonstrates how to enable SSH access from the Internet:</span><span class="sxs-lookup"><span data-stu-id="a4d0c-274">The following example demonstrates how to enable SSH access from the Internet:</span></span>
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 304 -Direction Inbound
> ```
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
> ```

<span data-ttu-id="a4d0c-275">For more information on Network Security Groups, see [Network Security Groups overview](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="a4d0c-275">For more information on Network Security Groups, see [Network Security Groups overview](../virtual-network/virtual-networks-nsg.md).</span></span> <span data-ttu-id="a4d0c-276">For information on controlling routing in an Azure Virtual Network, see [User-defined Routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4d0c-276">For information on controlling routing in an Azure Virtual Network, see [User-defined Routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>

## <a name="retrieve-internal-ips-and-fqdns"></a><span data-ttu-id="a4d0c-277">Retrieve internal IPs and FQDNs</span><span class="sxs-lookup"><span data-stu-id="a4d0c-277">Retrieve internal IPs and FQDNs</span></span>

<span data-ttu-id="a4d0c-278">When connecting to HDInsight using a virtual network, you can connect directly to the nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-278">When connecting to HDInsight using a virtual network, you can connect directly to the nodes in the cluster.</span></span> <span data-ttu-id="a4d0c-279">Use the following scripts to determine the internal IP address and fully qualified domain names (FQDN) for the nodes in the cluster:</span><span class="sxs-lookup"><span data-stu-id="a4d0c-279">Use the following scripts to determine the internal IP address and fully qualified domain names (FQDN) for the nodes in the cluster:</span></span>

<span data-ttu-id="a4d0c-280">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="a4d0c-280">**Azure PowerShell**</span></span>

```powershell
$resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"

$clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

$nodes = @()
foreach($nic in $clusterNICs) {
    $node = new-object System.Object
    $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
    $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
    $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
    $nodes += $node
}
$nodes | sort-object Type
```

<span data-ttu-id="a4d0c-281">__Azure CLI__</span><span class="sxs-lookup"><span data-stu-id="a4d0c-281">__Azure CLI__</span></span>

```azurecli
az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
```

> [!IMPORTANT]
> <span data-ttu-id="a4d0c-282">In the Azure CLI 2.0 example, replace `<resourcegroupname>` with the name of the resource group that contains the virtual network.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-282">In the Azure CLI 2.0 example, replace `<resourcegroupname>` with the name of the resource group that contains the virtual network.</span></span>

<span data-ttu-id="a4d0c-283">The scripts work by querying the virtual network interface cards (NICs) for the cluster.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-283">The scripts work by querying the virtual network interface cards (NICs) for the cluster.</span></span> <span data-ttu-id="a4d0c-284">The NICs exist in the resource group that contains the virtual network used by HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a4d0c-284">The NICs exist in the resource group that contains the virtual network used by HDInsight.</span></span>

## <a id="nextsteps"></a><span data-ttu-id="a4d0c-285">Next steps</span><span class="sxs-lookup"><span data-stu-id="a4d0c-285">Next steps</span></span>

<span data-ttu-id="a4d0c-286">The following examples demonstrate how to use HDInsight with Azure Virtual Network:</span><span class="sxs-lookup"><span data-stu-id="a4d0c-286">The following examples demonstrate how to use HDInsight with Azure Virtual Network:</span></span>

* [<span data-ttu-id="a4d0c-287">HBase clusters in Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="a4d0c-287">HBase clusters in Azure Virtual Network</span></span>](hdinsight-hbase-provision-vnet.md)

* [<span data-ttu-id="a4d0c-288">Analyze sensor data with Storm and HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="a4d0c-288">Analyze sensor data with Storm and HBase in HDInsight</span></span>](hdinsight-storm-sensor-data-analysis.md)

* [<span data-ttu-id="a4d0c-289">Provision Hadoop clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="a4d0c-289">Provision Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)

* [<span data-ttu-id="a4d0c-290">Use Sqoop with Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="a4d0c-290">Use Sqoop with Hadoop in HDInsight</span></span>](hdinsight-use-sqoop-mac-linux.md)

<span data-ttu-id="a4d0c-291">To learn more about Azure virtual networks, see the [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4d0c-291">To learn more about Azure virtual networks, see the [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>




