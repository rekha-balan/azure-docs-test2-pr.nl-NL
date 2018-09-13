---
title: Diagnose a communication problem between networks - tutorial - Azure portal | Microsoft Docs
description: Learn how to diagnose a communication problem between an Azure virtual network connected to an on-premises, or other virtual network, through an Azure virtual network gateway, using Network Watcher's VPN diagnostics capability.
services: network-watcher
documentationcenter: na
author: jimdial
manager: jeconnoc
editor: ''
Customer intent: I need to determine why resources in a virtual network can't communicate with resources in a different network.
ms.service: network-watcher
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2018
ms.author: jdial
ms.custom: mvc
ms.openlocfilehash: d89c5a3f2545edd7c02b67fa9d2e2b78937a9791
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869521"
---
# <a name="tutorial-diagnose-a-communication-problem-between-networks-using-the-azure-portal"></a><span data-ttu-id="906a3-103">Tutorial: Diagnose a communication problem between networks using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="906a3-103">Tutorial: Diagnose a communication problem between networks using the Azure portal</span></span>

<span data-ttu-id="906a3-104">A virtual network gateway connects an Azure virtual network to an on-premises, or other virtual network.</span><span class="sxs-lookup"><span data-stu-id="906a3-104">A virtual network gateway connects an Azure virtual network to an on-premises, or other virtual network.</span></span> <span data-ttu-id="906a3-105">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="906a3-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="906a3-106">Diagnose a problem with a virtual network gateway with Network Watcher's VPN diagnostics capability</span><span class="sxs-lookup"><span data-stu-id="906a3-106">Diagnose a problem with a virtual network gateway with Network Watcher's VPN diagnostics capability</span></span>
> * <span data-ttu-id="906a3-107">Diagnose a problem with a gateway connection</span><span class="sxs-lookup"><span data-stu-id="906a3-107">Diagnose a problem with a gateway connection</span></span>
> * <span data-ttu-id="906a3-108">Resolve a problem with a gateway</span><span class="sxs-lookup"><span data-stu-id="906a3-108">Resolve a problem with a gateway</span></span>

<span data-ttu-id="906a3-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="906a3-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="906a3-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="906a3-110">Prerequisites</span></span>

<span data-ttu-id="906a3-111">To use VPN diagnostics, you must have an existing, running VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="906a3-111">To use VPN diagnostics, you must have an existing, running VPN gateway.</span></span> <span data-ttu-id="906a3-112">If you don't have an existing VPN gateway to diagnose, you can deploy one using a [PowerShell script](../vpn-gateway/scripts/vpn-gateway-sample-site-to-site-powershell.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="906a3-112">If you don't have an existing VPN gateway to diagnose, you can deploy one using a [PowerShell script](../vpn-gateway/scripts/vpn-gateway-sample-site-to-site-powershell.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json).</span></span> <span data-ttu-id="906a3-113">You can run the PowerShell script from:</span><span class="sxs-lookup"><span data-stu-id="906a3-113">You can run the PowerShell script from:</span></span>
    - <span data-ttu-id="906a3-114">**A local PowerShell installation**: The script requires the AzureRM PowerShell module version 5.7.0 or later.</span><span class="sxs-lookup"><span data-stu-id="906a3-114">**A local PowerShell installation**: The script requires the AzureRM PowerShell module version 5.7.0 or later.</span></span> <span data-ttu-id="906a3-115">Run `Get-Module -ListAvailable AzureRM` to find the installed version.</span><span class="sxs-lookup"><span data-stu-id="906a3-115">Run `Get-Module -ListAvailable AzureRM` to find the installed version.</span></span> <span data-ttu-id="906a3-116">If you need to upgrade, see [Install Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="906a3-116">If you need to upgrade, see [Install Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="906a3-117">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="906a3-117">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span></span>
    - <span data-ttu-id="906a3-118">**The Azure Cloud Shell**: The [Azure Cloud Shell](https://shell.azure.com/powershell) has the latest version of PowerShell installed and configured, and logs you into Azure.</span><span class="sxs-lookup"><span data-stu-id="906a3-118">**The Azure Cloud Shell**: The [Azure Cloud Shell](https://shell.azure.com/powershell) has the latest version of PowerShell installed and configured, and logs you into Azure.</span></span>

<span data-ttu-id="906a3-119">The script takes approximately an hour to create a VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="906a3-119">The script takes approximately an hour to create a VPN gateway.</span></span> <span data-ttu-id="906a3-120">The remaining steps assume that the gateway you're diagnosing is the one deployed by this script.</span><span class="sxs-lookup"><span data-stu-id="906a3-120">The remaining steps assume that the gateway you're diagnosing is the one deployed by this script.</span></span> <span data-ttu-id="906a3-121">If you diagnose your own existing gateway instead, your results will vary.</span><span class="sxs-lookup"><span data-stu-id="906a3-121">If you diagnose your own existing gateway instead, your results will vary.</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="906a3-122">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="906a3-122">Sign in to Azure</span></span>

<span data-ttu-id="906a3-123">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="906a3-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="enable-network-watcher"></a><span data-ttu-id="906a3-124">Enable Network Watcher</span><span class="sxs-lookup"><span data-stu-id="906a3-124">Enable Network Watcher</span></span>

<span data-ttu-id="906a3-125">If you already have a network watcher enabled in the East US region, skip to [Diagnose a gateway](#diagnose-a-gateway).</span><span class="sxs-lookup"><span data-stu-id="906a3-125">If you already have a network watcher enabled in the East US region, skip to [Diagnose a gateway](#diagnose-a-gateway).</span></span>

1. <span data-ttu-id="906a3-126">In the portal, select **All services**.</span><span class="sxs-lookup"><span data-stu-id="906a3-126">In the portal, select **All services**.</span></span> <span data-ttu-id="906a3-127">In the **Filter box**, enter *Network Watcher*.</span><span class="sxs-lookup"><span data-stu-id="906a3-127">In the **Filter box**, enter *Network Watcher*.</span></span> <span data-ttu-id="906a3-128">When **Network Watcher** appears in the results, select it.</span><span class="sxs-lookup"><span data-stu-id="906a3-128">When **Network Watcher** appears in the results, select it.</span></span>
2. <span data-ttu-id="906a3-129">Select **Regions**, to expand it, and then select **...** to the right of **East US**, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="906a3-129">Select **Regions**, to expand it, and then select **...** to the right of **East US**, as shown in the following picture:</span></span>

    ![Enable Network Watcher](./media/diagnose-communication-problem-between-networks/enable-network-watcher.png)

3. <span data-ttu-id="906a3-131">Select **Enable Network Watcher**.</span><span class="sxs-lookup"><span data-stu-id="906a3-131">Select **Enable Network Watcher**.</span></span>

## <a name="diagnose-a-gateway"></a><span data-ttu-id="906a3-132">Diagnose a gateway</span><span class="sxs-lookup"><span data-stu-id="906a3-132">Diagnose a gateway</span></span>

1. <span data-ttu-id="906a3-133">On the left side of the portal, select **All services**.</span><span class="sxs-lookup"><span data-stu-id="906a3-133">On the left side of the portal, select **All services**.</span></span>
2. <span data-ttu-id="906a3-134">Start typing *network watcher* in the **Filter** box.</span><span class="sxs-lookup"><span data-stu-id="906a3-134">Start typing *network watcher* in the **Filter** box.</span></span> <span data-ttu-id="906a3-135">When **Network Watcher** appears in the search results, select it.</span><span class="sxs-lookup"><span data-stu-id="906a3-135">When **Network Watcher** appears in the search results, select it.</span></span>
3. <span data-ttu-id="906a3-136">Under **NETWORK DIAGNOSTIC TOOLS**, select **VPN Diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="906a3-136">Under **NETWORK DIAGNOSTIC TOOLS**, select **VPN Diagnostics**.</span></span>
4. <span data-ttu-id="906a3-137">Select **Storage account**, and then select the storage account you want to write diagnostic information to.</span><span class="sxs-lookup"><span data-stu-id="906a3-137">Select **Storage account**, and then select the storage account you want to write diagnostic information to.</span></span>
5. <span data-ttu-id="906a3-138">From the list of **Storage accounts**, select the storage account you want to use.</span><span class="sxs-lookup"><span data-stu-id="906a3-138">From the list of **Storage accounts**, select the storage account you want to use.</span></span> <span data-ttu-id="906a3-139">If you don't have an existing storage account, select **+ Storage account**, enter, or select the required information, and then select **Create**, to create one.</span><span class="sxs-lookup"><span data-stu-id="906a3-139">If you don't have an existing storage account, select **+ Storage account**, enter, or select the required information, and then select **Create**, to create one.</span></span> <span data-ttu-id="906a3-140">If you created a VPN gateway using the script in [prerequisites](#prerequisites), you may want to create the storage account in the same resource group, *TestRG1*, as the gateway.</span><span class="sxs-lookup"><span data-stu-id="906a3-140">If you created a VPN gateway using the script in [prerequisites](#prerequisites), you may want to create the storage account in the same resource group, *TestRG1*, as the gateway.</span></span>
6. <span data-ttu-id="906a3-141">From the list of **Containers**, select the container you want to use, and then select **Select**.</span><span class="sxs-lookup"><span data-stu-id="906a3-141">From the list of **Containers**, select the container you want to use, and then select **Select**.</span></span> <span data-ttu-id="906a3-142">If you don't have any containers, select **+ Container**, enter a name for the container, then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="906a3-142">If you don't have any containers, select **+ Container**, enter a name for the container, then select **OK**.</span></span>
7. <span data-ttu-id="906a3-143">Select a gateway, and then select **Start troubleshooting**.</span><span class="sxs-lookup"><span data-stu-id="906a3-143">Select a gateway, and then select **Start troubleshooting**.</span></span> <span data-ttu-id="906a3-144">As shown in the following picture, the test is run against a gateway named **Vnet1GW**:</span><span class="sxs-lookup"><span data-stu-id="906a3-144">As shown in the following picture, the test is run against a gateway named **Vnet1GW**:</span></span>

    ![VPN diagnostics](./media/diagnose-communication-problem-between-networks/vpn-diagnostics.png)

8. <span data-ttu-id="906a3-146">While the test is running, **Running** appears in the **TROUBLESHOOTING STATUS** column where **Not started** is shown, in the previous picture.</span><span class="sxs-lookup"><span data-stu-id="906a3-146">While the test is running, **Running** appears in the **TROUBLESHOOTING STATUS** column where **Not started** is shown, in the previous picture.</span></span> <span data-ttu-id="906a3-147">The test may take several minutes to run.</span><span class="sxs-lookup"><span data-stu-id="906a3-147">The test may take several minutes to run.</span></span>
9. <span data-ttu-id="906a3-148">View the status of a completed test.</span><span class="sxs-lookup"><span data-stu-id="906a3-148">View the status of a completed test.</span></span> <span data-ttu-id="906a3-149">The following picture shows the status results of a completed diagnostic test:</span><span class="sxs-lookup"><span data-stu-id="906a3-149">The following picture shows the status results of a completed diagnostic test:</span></span>

    ![Status](./media/diagnose-communication-problem-between-networks/status.png)

    <span data-ttu-id="906a3-151">You can see that the **TROUBLESHOOTING STATUS** is **Unhealthy**, as well as a **Summary** and **Detail** of the problem on the **Status** tab.</span><span class="sxs-lookup"><span data-stu-id="906a3-151">You can see that the **TROUBLESHOOTING STATUS** is **Unhealthy**, as well as a **Summary** and **Detail** of the problem on the **Status** tab.</span></span>
10. <span data-ttu-id="906a3-152">When you select the **Action** tab, VPN diagnostics provides additional information.</span><span class="sxs-lookup"><span data-stu-id="906a3-152">When you select the **Action** tab, VPN diagnostics provides additional information.</span></span> <span data-ttu-id="906a3-153">In the example, shown in the following picture, VPN diagnostics lets you know that you should check the health of each connection:</span><span class="sxs-lookup"><span data-stu-id="906a3-153">In the example, shown in the following picture, VPN diagnostics lets you know that you should check the health of each connection:</span></span>

  ![Action](./media/diagnose-communication-problem-between-networks/action.png)

## <a name="diagnose-a-gateway-connection"></a><span data-ttu-id="906a3-155">Diagnose a gateway connection</span><span class="sxs-lookup"><span data-stu-id="906a3-155">Diagnose a gateway connection</span></span>

<span data-ttu-id="906a3-156">A gateway is connected to other networks via a gateway connection.</span><span class="sxs-lookup"><span data-stu-id="906a3-156">A gateway is connected to other networks via a gateway connection.</span></span> <span data-ttu-id="906a3-157">Both the gateway and gateway connections must be healthy for successful communication between a virtual network and a connected network.</span><span class="sxs-lookup"><span data-stu-id="906a3-157">Both the gateway and gateway connections must be healthy for successful communication between a virtual network and a connected network.</span></span>

1. <span data-ttu-id="906a3-158">Complete step 7 of [Diagnose a gateway](#diagnose-a-gateway) again, this time, selecting a connection.</span><span class="sxs-lookup"><span data-stu-id="906a3-158">Complete step 7 of [Diagnose a gateway](#diagnose-a-gateway) again, this time, selecting a connection.</span></span> <span data-ttu-id="906a3-159">In the following example, a connection named **VNet1toSite1** is tested:</span><span class="sxs-lookup"><span data-stu-id="906a3-159">In the following example, a connection named **VNet1toSite1** is tested:</span></span>

    ![Connection](./media/diagnose-communication-problem-between-networks/connection.png)

    <span data-ttu-id="906a3-161">The test runs for several minutes.</span><span class="sxs-lookup"><span data-stu-id="906a3-161">The test runs for several minutes.</span></span>
2. <span data-ttu-id="906a3-162">After the test of the connection is complete, you receive results similar to the results shown in the following pictures on the **Status** and **Action** tabs:</span><span class="sxs-lookup"><span data-stu-id="906a3-162">After the test of the connection is complete, you receive results similar to the results shown in the following pictures on the **Status** and **Action** tabs:</span></span>

    ![Connection status](./media/diagnose-communication-problem-between-networks/connection-status.png)

    ![Connection action](./media/diagnose-communication-problem-between-networks/connection-action.png)

    <span data-ttu-id="906a3-165">VPN diagnostics informs you what is wrong on the **Status** tab, and gives you several suggestions for what may be causing the problem on the **Action** tab.</span><span class="sxs-lookup"><span data-stu-id="906a3-165">VPN diagnostics informs you what is wrong on the **Status** tab, and gives you several suggestions for what may be causing the problem on the **Action** tab.</span></span>

    <span data-ttu-id="906a3-166">If the gateway you tested was the one deployed by the [script](../vpn-gateway/scripts/vpn-gateway-sample-site-to-site-powershell.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json) in [Prerequisites](#prerequisites), then the problem on the **Status** tab, and the first two items on the **Actions** tab are exactly what the problem is.</span><span class="sxs-lookup"><span data-stu-id="906a3-166">If the gateway you tested was the one deployed by the [script](../vpn-gateway/scripts/vpn-gateway-sample-site-to-site-powershell.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json) in [Prerequisites](#prerequisites), then the problem on the **Status** tab, and the first two items on the **Actions** tab are exactly what the problem is.</span></span> <span data-ttu-id="906a3-167">The script configures a placeholder IP address, 23.99.221.164, for the on-premises VPN gateway device.</span><span class="sxs-lookup"><span data-stu-id="906a3-167">The script configures a placeholder IP address, 23.99.221.164, for the on-premises VPN gateway device.</span></span>

    <span data-ttu-id="906a3-168">To resolve the issue, you need to ensure that your on-premises VPN gateway is [configured properly](../vpn-gateway/vpn-gateway-about-vpn-devices.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json), and change the IP address configured by the script for the local network gateway, to the actual public address of your on-premises VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="906a3-168">To resolve the issue, you need to ensure that your on-premises VPN gateway is [configured properly](../vpn-gateway/vpn-gateway-about-vpn-devices.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json), and change the IP address configured by the script for the local network gateway, to the actual public address of your on-premises VPN gateway.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="906a3-169">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="906a3-169">Clean up resources</span></span>

<span data-ttu-id="906a3-170">If you created a VPN gateway using the script in the [prerequisites](#prerequisites) solely to complete this tutorial, and no longer need it, delete the resource group and all of the resources it contains:</span><span class="sxs-lookup"><span data-stu-id="906a3-170">If you created a VPN gateway using the script in the [prerequisites](#prerequisites) solely to complete this tutorial, and no longer need it, delete the resource group and all of the resources it contains:</span></span>

1. <span data-ttu-id="906a3-171">Enter *TestRG1* in the **Search** box at the top of the portal.</span><span class="sxs-lookup"><span data-stu-id="906a3-171">Enter *TestRG1* in the **Search** box at the top of the portal.</span></span> <span data-ttu-id="906a3-172">When you see **TestRG1** in the search results, select it.</span><span class="sxs-lookup"><span data-stu-id="906a3-172">When you see **TestRG1** in the search results, select it.</span></span>
2. <span data-ttu-id="906a3-173">Select **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="906a3-173">Select **Delete resource group**.</span></span>
3. <span data-ttu-id="906a3-174">Enter *TestRG1* for **TYPE THE RESOURCE GROUP NAME:** and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="906a3-174">Enter *TestRG1* for **TYPE THE RESOURCE GROUP NAME:** and select **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="906a3-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="906a3-175">Next steps</span></span>

<span data-ttu-id="906a3-176">In this tutorial, you learned how to diagnose a problem with a virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="906a3-176">In this tutorial, you learned how to diagnose a problem with a virtual network gateway.</span></span> <span data-ttu-id="906a3-177">You may want to log network communication to and from a VM so that you can review the log for anomalies.</span><span class="sxs-lookup"><span data-stu-id="906a3-177">You may want to log network communication to and from a VM so that you can review the log for anomalies.</span></span> <span data-ttu-id="906a3-178">To learn how, advance to the next tutorial.</span><span class="sxs-lookup"><span data-stu-id="906a3-178">To learn how, advance to the next tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="906a3-179">Log network traffic to and from a VM</span><span class="sxs-lookup"><span data-stu-id="906a3-179">Log network traffic to and from a VM</span></span>](network-watcher-nsg-flow-logging-portal.md)