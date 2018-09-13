---
title: Configure private IP addresses for VMs (Classic) - Azure CLI 1.0| Microsoft Docs
description: Learn how to configure private IP addresses for virtual machines (Classic) using the Azure command-line interface (CLI) 1.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17386acf-c708-4103-9b22-ff9bf04b778d
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed0fe2fea20671063395b9ff089599853278989d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556024"
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-the-azure-cli-10"></a><span data-ttu-id="ee3a8-103">Configure private IP addresses for a virtual machine (Classic) using the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="ee3a8-103">Configure private IP addresses for a virtual machine (Classic) using the Azure CLI 1.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="ee3a8-104">This article covers the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-104">This article covers the classic deployment model.</span></span> <span data-ttu-id="ee3a8-105">You can also [manage a static private IP address in the Resource Manager deployment model](virtual-networks-static-private-ip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ee3a8-105">You can also [manage a static private IP address in the Resource Manager deployment model](virtual-networks-static-private-ip-arm-cli.md).</span></span>

<span data-ttu-id="ee3a8-106">The sample Azure CLI commands below expect a simple environment already created.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-106">The sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="ee3a8-107">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ee3a8-107">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-to-specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="ee3a8-108">How to specify a static private IP address when creating a VM</span><span class="sxs-lookup"><span data-stu-id="ee3a8-108">How to specify a static private IP address when creating a VM</span></span>
<span data-ttu-id="ee3a8-109">To create a new VM named *DNS01* in a new cloud service named *TestService* based on the scenario above, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="ee3a8-109">To create a new VM named *DNS01* in a new cloud service named *TestService* based on the scenario above, follow these steps:</span></span>

1. <span data-ttu-id="ee3a8-110">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-110">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="ee3a8-111">Run the **azure service create** command to create the cloud service.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-111">Run the **azure service create** command to create the cloud service.</span></span>
   
        azure service create TestService --location uscentral
   
    <span data-ttu-id="ee3a8-112">Expected output:</span><span class="sxs-lookup"><span data-stu-id="ee3a8-112">Expected output:</span></span>
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. <span data-ttu-id="ee3a8-113">Run the **azure create vm** command to create the VM.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-113">Run the **azure create vm** command to create the VM.</span></span> <span data-ttu-id="ee3a8-114">Notice the value for a static private IP address.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-114">Notice the value for a static private IP address.</span></span> <span data-ttu-id="ee3a8-115">The list shown after the output explains the parameters used.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-115">The list shown after the output explains the parameters used.</span></span>
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    <span data-ttu-id="ee3a8-116">Expected output:</span><span class="sxs-lookup"><span data-stu-id="ee3a8-116">Expected output:</span></span>
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting to "Small".
        info:    Looking up image bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
        info:    Looking up virtual network
        info:    Looking up cloud service
        warn:    --location option will be ignored
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Retrieving storage accounts
        info:    Creating VM
        info:    OK
        info:    vm create command OK
   
   * <span data-ttu-id="ee3a8-117">**-l (or --location)**.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-117">**-l (or --location)**.</span></span> <span data-ttu-id="ee3a8-118">Azure region where the VM will be created.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-118">Azure region where the VM will be created.</span></span> <span data-ttu-id="ee3a8-119">For our scenario, *centralus*.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-119">For our scenario, *centralus*.</span></span>
   * <span data-ttu-id="ee3a8-120">**-n (or --vm-name)**.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-120">**-n (or --vm-name)**.</span></span> <span data-ttu-id="ee3a8-121">Name of the VM to be created.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-121">Name of the VM to be created.</span></span>
   * <span data-ttu-id="ee3a8-122">**-w (or --virtual-network-name)**.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-122">**-w (or --virtual-network-name)**.</span></span> <span data-ttu-id="ee3a8-123">Name of the VNet where the VM will be created.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-123">Name of the VNet where the VM will be created.</span></span> 
   * <span data-ttu-id="ee3a8-124">**-S (or --static-ip)**.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-124">**-S (or --static-ip)**.</span></span> <span data-ttu-id="ee3a8-125">Static private IP address for the VM.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-125">Static private IP address for the VM.</span></span>
   * <span data-ttu-id="ee3a8-126">**TestService**.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-126">**TestService**.</span></span> <span data-ttu-id="ee3a8-127">Name of the cloud service where the VM will be created.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-127">Name of the cloud service where the VM will be created.</span></span>
   * <span data-ttu-id="ee3a8-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span></span> <span data-ttu-id="ee3a8-129">Image used to create the VM.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-129">Image used to create the VM.</span></span>
   * <span data-ttu-id="ee3a8-130">**adminuser**.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-130">**adminuser**.</span></span> <span data-ttu-id="ee3a8-131">Local administrator for the Windows VM.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-131">Local administrator for the Windows VM.</span></span>
   * <span data-ttu-id="ee3a8-132">**AdminP@ssw0rd**.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-132">**AdminP@ssw0rd**.</span></span> <span data-ttu-id="ee3a8-133">Local administrator password for the Windows VM.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-133">Local administrator password for the Windows VM.</span></span>

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="ee3a8-134">How to retrieve static private IP address information for a VM</span><span class="sxs-lookup"><span data-stu-id="ee3a8-134">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="ee3a8-135">To view the static private IP address information for the VM created with the script above, run the following Azure CLI command and observe the value for *Network StaticIP*:</span><span class="sxs-lookup"><span data-stu-id="ee3a8-135">To view the static private IP address information for the VM created with the script above, run the following Azure CLI command and observe the value for *Network StaticIP*:</span></span>

    azure vm static-ip show DNS01

<span data-ttu-id="ee3a8-136">Expected output:</span><span class="sxs-lookup"><span data-stu-id="ee3a8-136">Expected output:</span></span>

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="ee3a8-137">How to remove a static private IP address from a VM</span><span class="sxs-lookup"><span data-stu-id="ee3a8-137">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="ee3a8-138">To remove the static private IP address added to the VM in the script above, run the following Azure CLI command:</span><span class="sxs-lookup"><span data-stu-id="ee3a8-138">To remove the static private IP address added to the VM in the script above, run the following Azure CLI command:</span></span>

    azure vm static-ip remove DNS01

<span data-ttu-id="ee3a8-139">Expected output:</span><span class="sxs-lookup"><span data-stu-id="ee3a8-139">Expected output:</span></span>

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-to-add-a-static-private-ip-to-an-existing-vm"></a><span data-ttu-id="ee3a8-140">How to add a static private IP to an existing VM</span><span class="sxs-lookup"><span data-stu-id="ee3a8-140">How to add a static private IP to an existing VM</span></span>
<span data-ttu-id="ee3a8-141">To add a static private IP address to the VM created using the script above, runt he following command:</span><span class="sxs-lookup"><span data-stu-id="ee3a8-141">To add a static private IP address to the VM created using the script above, runt he following command:</span></span>

    azure vm static-ip set DNS01 192.168.1.101

<span data-ttu-id="ee3a8-142">Expected output:</span><span class="sxs-lookup"><span data-stu-id="ee3a8-142">Expected output:</span></span>

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a><span data-ttu-id="ee3a8-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="ee3a8-143">Next steps</span></span>
* <span data-ttu-id="ee3a8-144">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-144">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="ee3a8-145">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-145">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="ee3a8-146">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="ee3a8-146">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

