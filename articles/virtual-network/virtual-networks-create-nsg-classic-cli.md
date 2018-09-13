---
title: How to create NSGs in classic mode using the Azure CLI| Microsoft Docs
description: Learn how to create and deploy NSGs in classic mode using the Azure CLI
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 17d98950-5fbb-4653-bef6-d822ab37541e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 115a1937a4c88ba2b986a40c84b1b759ed5e03b5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563538"
---
# <a name="how-to-create-nsgs-classic-in-the-azure-cli"></a><span data-ttu-id="4a0bc-103">How to create NSGs (classic) in the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4a0bc-103">How to create NSGs (classic) in the Azure CLI</span></span>
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="4a0bc-104">This article covers the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-104">This article covers the classic deployment model.</span></span> <span data-ttu-id="4a0bc-105">You can also [create NSGs in the Resource Manager deployment model](virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4a0bc-105">You can also [create NSGs in the Resource Manager deployment model](virtual-networks-create-nsg-arm-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="4a0bc-106">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-106">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="4a0bc-107">If you want to run the commands as they are displayed in this document, first build the test environment by [creating a VNet](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4a0bc-107">If you want to run the commands as they are displayed in this document, first build the test environment by [creating a VNet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a><span data-ttu-id="4a0bc-108">How to create the NSG for the front end subnet</span><span class="sxs-lookup"><span data-stu-id="4a0bc-108">How to create the NSG for the front end subnet</span></span>
<span data-ttu-id="4a0bc-109">To create an NSG named named **NSG-FrontEnd** based on the scenario above, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-109">To create an NSG named named **NSG-FrontEnd** based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="4a0bc-110">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-110">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="4a0bc-111">Run the **`azure config mode`** command to switch to classic mode, as shown below.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-111">Run the **`azure config mode`** command to switch to classic mode, as shown below.</span></span>
   
        azure config mode asm
   
    <span data-ttu-id="4a0bc-112">Expected output:</span><span class="sxs-lookup"><span data-stu-id="4a0bc-112">Expected output:</span></span>
   
        info:    New mode is asm
3. <span data-ttu-id="4a0bc-113">Run the **`azure network nsg create`** command to create an NSG.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-113">Run the **`azure network nsg create`** command to create an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    <span data-ttu-id="4a0bc-114">Expected output:</span><span class="sxs-lookup"><span data-stu-id="4a0bc-114">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Name                            : NSG-FrontEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="4a0bc-115">Parameters:</span><span class="sxs-lookup"><span data-stu-id="4a0bc-115">Parameters:</span></span>
   
   * <span data-ttu-id="4a0bc-116">**-l (or --location)**.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-116">**-l (or --location)**.</span></span> <span data-ttu-id="4a0bc-117">Azure region where the new NSG will be created.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-117">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="4a0bc-118">For our scenario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-118">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="4a0bc-119">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-119">**-n (or --name)**.</span></span> <span data-ttu-id="4a0bc-120">Name for the new NSG.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-120">Name for the new NSG.</span></span> <span data-ttu-id="4a0bc-121">For our scenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-121">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="4a0bc-122">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 3389 (RDP) from the Internet.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-122">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 3389 (RDP) from the Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="4a0bc-123">Expected output:</span><span class="sxs-lookup"><span data-stu-id="4a0bc-123">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Name                            : rdp-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 3389
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    <span data-ttu-id="4a0bc-124">Parameters:</span><span class="sxs-lookup"><span data-stu-id="4a0bc-124">Parameters:</span></span>
   
   * <span data-ttu-id="4a0bc-125">**-a (or --nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-125">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="4a0bc-126">Name of the NSG in which the rule will be created.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-126">Name of the NSG in which the rule will be created.</span></span> <span data-ttu-id="4a0bc-127">For our scenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-127">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="4a0bc-128">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-128">**-n (or --name)**.</span></span> <span data-ttu-id="4a0bc-129">Name for the new rule.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-129">Name for the new rule.</span></span> <span data-ttu-id="4a0bc-130">For our scenario, *rdp-rule*.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-130">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="4a0bc-131">**-c (or --action)**.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-131">**-c (or --action)**.</span></span> <span data-ttu-id="4a0bc-132">Access level for the rule (Deny or Allow).</span><span class="sxs-lookup"><span data-stu-id="4a0bc-132">Access level for the rule (Deny or Allow).</span></span>
   * <span data-ttu-id="4a0bc-133">**-p (or --protocol)**.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-133">**-p (or --protocol)**.</span></span> <span data-ttu-id="4a0bc-134">Protocol (Tcp, Udp, or \*) for the rule.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-134">Protocol (Tcp, Udp, or \*) for the rule.</span></span>
   * <span data-ttu-id="4a0bc-135">**-r (or --type)**.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-135">**-r (or --type)**.</span></span> <span data-ttu-id="4a0bc-136">Direction of connection (Inbound or Outbound).</span><span class="sxs-lookup"><span data-stu-id="4a0bc-136">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="4a0bc-137">**-y (or --priority)**.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-137">**-y (or --priority)**.</span></span> <span data-ttu-id="4a0bc-138">Priority for the rule.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-138">Priority for the rule.</span></span>
   * <span data-ttu-id="4a0bc-139">**-f (or --source-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-139">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="4a0bc-140">Source address prefix in CIDR or using default tags.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-140">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="4a0bc-141">**-o (or --source-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-141">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="4a0bc-142">Source port, or port range.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-142">Source port, or port range.</span></span>
   * <span data-ttu-id="4a0bc-143">**-e (or --destination-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-143">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="4a0bc-144">Destination address prefix in CIDR or using default tags.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-144">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="4a0bc-145">**-u (or --destination-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-145">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="4a0bc-146">Destination port, or port range.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-146">Destination port, or port range.</span></span>
5. <span data-ttu-id="4a0bc-147">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 80 (HTTP) from the Internet.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-147">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 80 (HTTP) from the Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="4a0bc-148">Expected putput:</span><span class="sxs-lookup"><span data-stu-id="4a0bc-148">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. <span data-ttu-id="4a0bc-149">Run the **`azure network nsg subnet add`** command to link the NSG to the front end subnet.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-149">Run the **`azure network nsg subnet add`** command to link the NSG to the front end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    <span data-ttu-id="4a0bc-150">Expected output:</span><span class="sxs-lookup"><span data-stu-id="4a0bc-150">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a><span data-ttu-id="4a0bc-151">How to create the NSG for the back end subnet</span><span class="sxs-lookup"><span data-stu-id="4a0bc-151">How to create the NSG for the back end subnet</span></span>
<span data-ttu-id="4a0bc-152">To create an NSG named named *NSG-BackEnd* based on the scenario above, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-152">To create an NSG named named *NSG-BackEnd* based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="4a0bc-153">Run the **`azure network nsg create`** command to create an NSG.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-153">Run the **`azure network nsg create`** command to create an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    <span data-ttu-id="4a0bc-154">Expected output:</span><span class="sxs-lookup"><span data-stu-id="4a0bc-154">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Name                            : NSG-BackEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="4a0bc-155">Parameters:</span><span class="sxs-lookup"><span data-stu-id="4a0bc-155">Parameters:</span></span>
   
   * <span data-ttu-id="4a0bc-156">**-l (or --location)**.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-156">**-l (or --location)**.</span></span> <span data-ttu-id="4a0bc-157">Azure region where the new NSG will be created.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-157">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="4a0bc-158">For our scenario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-158">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="4a0bc-159">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-159">**-n (or --name)**.</span></span> <span data-ttu-id="4a0bc-160">Name for the new NSG.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-160">Name for the new NSG.</span></span> <span data-ttu-id="4a0bc-161">For our scenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-161">For our scenario, *NSG-FrontEnd*.</span></span>
2. <span data-ttu-id="4a0bc-162">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 1433 (SQL) from the front end subnet.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-162">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 1433 (SQL) from the front end subnet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="4a0bc-163">Expected output:</span><span class="sxs-lookup"><span data-stu-id="4a0bc-163">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Name                            : sql-rule
        data:    Source address prefix           : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 1433
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. <span data-ttu-id="4a0bc-164">Run the **`azure network nsg rule create`** command to create a rule that denies access to the Internet.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-164">Run the **`azure network nsg rule create`** command to create a rule that denies access to the Internet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    <span data-ttu-id="4a0bc-165">Expected putput:</span><span class="sxs-lookup"><span data-stu-id="4a0bc-165">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : *
        data:    Source Port                     : *
        data:    Destination address prefix      : INTERNET
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Outbound
        data:    Action                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. <span data-ttu-id="4a0bc-166">Run the **`azure network nsg subnet add`** command to link the NSG to the back end subnet.</span><span class="sxs-lookup"><span data-stu-id="4a0bc-166">Run the **`azure network nsg subnet add`** command to link the NSG to the back end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    <span data-ttu-id="4a0bc-167">Expected output:</span><span class="sxs-lookup"><span data-stu-id="4a0bc-167">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up the network security group "NSG-BackEndX"
        info:    Looking up the subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

