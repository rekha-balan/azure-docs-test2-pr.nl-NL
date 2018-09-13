---
title: Log network traffic flow to and from a VM - tutorial - Azure portal | Microsoft Docs
description: Learn how to log network traffic flow to and from a VM using Network Watcher's NSG flow logs capability.
services: network-watcher
documentationcenter: na
author: jimdial
manager: jeconnoc
editor: ''
tags: azure-resource-manager
Customer intent: I need to log the network traffic to and from a VM so I can analyze it for anomalies.
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/30/2018
ms.author: jdial
ms.custom: mvc
ms.openlocfilehash: f010bebcf1130b3061c60987ffbd4e706a030773
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44795085"
---
# <a name="tutorial-log-network-traffic-to-and-from-a-virtual-machine-using-the-azure-portal"></a><span data-ttu-id="46bd5-103">Tutorial: Log network traffic to and from a virtual machine using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="46bd5-103">Tutorial: Log network traffic to and from a virtual machine using the Azure portal</span></span>

<span data-ttu-id="46bd5-104">A network security group (NSG) enables you to filter inbound traffic to, and outbound traffic from, a virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="46bd5-104">A network security group (NSG) enables you to filter inbound traffic to, and outbound traffic from, a virtual machine (VM).</span></span> <span data-ttu-id="46bd5-105">You can log network traffic that flows through an NSG with Network Watcher's NSG flow log capability.</span><span class="sxs-lookup"><span data-stu-id="46bd5-105">You can log network traffic that flows through an NSG with Network Watcher's NSG flow log capability.</span></span> <span data-ttu-id="46bd5-106">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="46bd5-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="46bd5-107">Create a VM with a network security group</span><span class="sxs-lookup"><span data-stu-id="46bd5-107">Create a VM with a network security group</span></span>
> * <span data-ttu-id="46bd5-108">Enable Network Watcher and register the Microsoft.Insights provider</span><span class="sxs-lookup"><span data-stu-id="46bd5-108">Enable Network Watcher and register the Microsoft.Insights provider</span></span>
> * <span data-ttu-id="46bd5-109">Enable a traffic flow log for an NSG, using Network Watcher's NSG flow log capability</span><span class="sxs-lookup"><span data-stu-id="46bd5-109">Enable a traffic flow log for an NSG, using Network Watcher's NSG flow log capability</span></span>
> * <span data-ttu-id="46bd5-110">Download logged data</span><span class="sxs-lookup"><span data-stu-id="46bd5-110">Download logged data</span></span>
> * <span data-ttu-id="46bd5-111">View logged data</span><span class="sxs-lookup"><span data-stu-id="46bd5-111">View logged data</span></span>

<span data-ttu-id="46bd5-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="46bd5-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="46bd5-113">Create a VM</span><span class="sxs-lookup"><span data-stu-id="46bd5-113">Create a VM</span></span>

1. <span data-ttu-id="46bd5-114">Select **+ Create a resource** found on the upper, left corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="46bd5-114">Select **+ Create a resource** found on the upper, left corner of the Azure portal.</span></span>
2. <span data-ttu-id="46bd5-115">Select **Compute**, and then select **Windows Server 2016 Datacenter** or **Ubuntu Server 17.10 VM**.</span><span class="sxs-lookup"><span data-stu-id="46bd5-115">Select **Compute**, and then select **Windows Server 2016 Datacenter** or **Ubuntu Server 17.10 VM**.</span></span>
3. <span data-ttu-id="46bd5-116">Enter, or select, the following information, accept the defaults for the remaining settings, and then select **OK**:</span><span class="sxs-lookup"><span data-stu-id="46bd5-116">Enter, or select, the following information, accept the defaults for the remaining settings, and then select **OK**:</span></span>

    |<span data-ttu-id="46bd5-117">Setting</span><span class="sxs-lookup"><span data-stu-id="46bd5-117">Setting</span></span>|<span data-ttu-id="46bd5-118">Value</span><span class="sxs-lookup"><span data-stu-id="46bd5-118">Value</span></span>|
    |---|---|
    |<span data-ttu-id="46bd5-119">Name</span><span class="sxs-lookup"><span data-stu-id="46bd5-119">Name</span></span>|<span data-ttu-id="46bd5-120">myVm</span><span class="sxs-lookup"><span data-stu-id="46bd5-120">myVm</span></span>|
    |<span data-ttu-id="46bd5-121">User name</span><span class="sxs-lookup"><span data-stu-id="46bd5-121">User name</span></span>| <span data-ttu-id="46bd5-122">Enter a user name of your choosing.</span><span class="sxs-lookup"><span data-stu-id="46bd5-122">Enter a user name of your choosing.</span></span>|
    |<span data-ttu-id="46bd5-123">Password</span><span class="sxs-lookup"><span data-stu-id="46bd5-123">Password</span></span>| <span data-ttu-id="46bd5-124">Enter a password of your choosing.</span><span class="sxs-lookup"><span data-stu-id="46bd5-124">Enter a password of your choosing.</span></span> <span data-ttu-id="46bd5-125">The password must be at least 12 characters long and meet the [defined complexity requirements](../virtual-machines/windows/faq.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json#what-are-the-password-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="46bd5-125">The password must be at least 12 characters long and meet the [defined complexity requirements](../virtual-machines/windows/faq.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json#what-are-the-password-requirements-when-creating-a-vm).</span></span>|
    |<span data-ttu-id="46bd5-126">Subscription</span><span class="sxs-lookup"><span data-stu-id="46bd5-126">Subscription</span></span>| <span data-ttu-id="46bd5-127">Select your subscription.</span><span class="sxs-lookup"><span data-stu-id="46bd5-127">Select your subscription.</span></span>|
    |<span data-ttu-id="46bd5-128">Resource group</span><span class="sxs-lookup"><span data-stu-id="46bd5-128">Resource group</span></span>| <span data-ttu-id="46bd5-129">Select **Create new** and enter **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="46bd5-129">Select **Create new** and enter **myResourceGroup**.</span></span>|
    |<span data-ttu-id="46bd5-130">Location</span><span class="sxs-lookup"><span data-stu-id="46bd5-130">Location</span></span>| <span data-ttu-id="46bd5-131">Select **East US**</span><span class="sxs-lookup"><span data-stu-id="46bd5-131">Select **East US**</span></span>|

4. <span data-ttu-id="46bd5-132">Select a size for the VM and then select **Select**.</span><span class="sxs-lookup"><span data-stu-id="46bd5-132">Select a size for the VM and then select **Select**.</span></span>
5. <span data-ttu-id="46bd5-133">Under **Settings**, accept all the defaults, and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="46bd5-133">Under **Settings**, accept all the defaults, and select **OK**.</span></span>
6. <span data-ttu-id="46bd5-134">Under **Create** of the **Summary**, select **Create** to start VM deployment.</span><span class="sxs-lookup"><span data-stu-id="46bd5-134">Under **Create** of the **Summary**, select **Create** to start VM deployment.</span></span> <span data-ttu-id="46bd5-135">The VM takes a few minutes to deploy.</span><span class="sxs-lookup"><span data-stu-id="46bd5-135">The VM takes a few minutes to deploy.</span></span> <span data-ttu-id="46bd5-136">Wait for the VM to finish deploying before continuing with the remaining steps.</span><span class="sxs-lookup"><span data-stu-id="46bd5-136">Wait for the VM to finish deploying before continuing with the remaining steps.</span></span>

<span data-ttu-id="46bd5-137">The VM takes a few minutes to create.</span><span class="sxs-lookup"><span data-stu-id="46bd5-137">The VM takes a few minutes to create.</span></span> <span data-ttu-id="46bd5-138">Don't continue with remaining steps until the VM has finished creating.</span><span class="sxs-lookup"><span data-stu-id="46bd5-138">Don't continue with remaining steps until the VM has finished creating.</span></span> <span data-ttu-id="46bd5-139">While the portal creates the VM, it also creates a network security group with the name **myVm-nsg**, and associates it to the network interface for the VM.</span><span class="sxs-lookup"><span data-stu-id="46bd5-139">While the portal creates the VM, it also creates a network security group with the name **myVm-nsg**, and associates it to the network interface for the VM.</span></span>

## <a name="enable-network-watcher"></a><span data-ttu-id="46bd5-140">Enable Network Watcher</span><span class="sxs-lookup"><span data-stu-id="46bd5-140">Enable Network Watcher</span></span>

<span data-ttu-id="46bd5-141">If you already have a network watcher enabled in the East US region, skip to [Register Insights provider](#register-insights-provider).</span><span class="sxs-lookup"><span data-stu-id="46bd5-141">If you already have a network watcher enabled in the East US region, skip to [Register Insights provider](#register-insights-provider).</span></span>

1. <span data-ttu-id="46bd5-142">In the portal, select **All services**.</span><span class="sxs-lookup"><span data-stu-id="46bd5-142">In the portal, select **All services**.</span></span> <span data-ttu-id="46bd5-143">In the **Filter box**, enter *Network Watcher*.</span><span class="sxs-lookup"><span data-stu-id="46bd5-143">In the **Filter box**, enter *Network Watcher*.</span></span> <span data-ttu-id="46bd5-144">When **Network Watcher** appears in the results, select it.</span><span class="sxs-lookup"><span data-stu-id="46bd5-144">When **Network Watcher** appears in the results, select it.</span></span>
2. <span data-ttu-id="46bd5-145">Select **Regions**, to expand it, and then select **...** to the right of **East US**, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="46bd5-145">Select **Regions**, to expand it, and then select **...** to the right of **East US**, as shown in the following picture:</span></span>

    ![Enable Network Watcher](./media/network-watcher-nsg-flow-logging-portal/enable-network-watcher.png)

3. <span data-ttu-id="46bd5-147">Select **Enable Network Watcher**.</span><span class="sxs-lookup"><span data-stu-id="46bd5-147">Select **Enable Network Watcher**.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="46bd5-148">Register Insights provider</span><span class="sxs-lookup"><span data-stu-id="46bd5-148">Register Insights provider</span></span>

<span data-ttu-id="46bd5-149">NSG flow logging requires the **Microsoft.Insights** provider.</span><span class="sxs-lookup"><span data-stu-id="46bd5-149">NSG flow logging requires the **Microsoft.Insights** provider.</span></span> <span data-ttu-id="46bd5-150">To register the provider, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="46bd5-150">To register the provider, complete the following steps:</span></span>

1. <span data-ttu-id="46bd5-151">In the top, left corner of portal, select **All services**.</span><span class="sxs-lookup"><span data-stu-id="46bd5-151">In the top, left corner of portal, select **All services**.</span></span> <span data-ttu-id="46bd5-152">In the Filter box, type *Subscriptions*.</span><span class="sxs-lookup"><span data-stu-id="46bd5-152">In the Filter box, type *Subscriptions*.</span></span> <span data-ttu-id="46bd5-153">When **Subscriptions** appear in the search results, select it.</span><span class="sxs-lookup"><span data-stu-id="46bd5-153">When **Subscriptions** appear in the search results, select it.</span></span>
2. <span data-ttu-id="46bd5-154">From the list of subscriptions, select the subscription you want to enable the provider for.</span><span class="sxs-lookup"><span data-stu-id="46bd5-154">From the list of subscriptions, select the subscription you want to enable the provider for.</span></span>
3. <span data-ttu-id="46bd5-155">Select **Resource providers**, under **SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="46bd5-155">Select **Resource providers**, under **SETTINGS**.</span></span>
4. <span data-ttu-id="46bd5-156">Confirm that the **STATUS** for the **microsoft.insights** provider is **Registered**, as shown in the picture that follows.</span><span class="sxs-lookup"><span data-stu-id="46bd5-156">Confirm that the **STATUS** for the **microsoft.insights** provider is **Registered**, as shown in the picture that follows.</span></span> <span data-ttu-id="46bd5-157">If the status is **Unregistered**, then select **Register**, to the right of the provider.</span><span class="sxs-lookup"><span data-stu-id="46bd5-157">If the status is **Unregistered**, then select **Register**, to the right of the provider.</span></span>

    ![Register provider](./media/network-watcher-nsg-flow-logging-portal/register-provider.png)

## <a name="enable-nsg-flow-log"></a><span data-ttu-id="46bd5-159">Enable NSG flow log</span><span class="sxs-lookup"><span data-stu-id="46bd5-159">Enable NSG flow log</span></span>

1. <span data-ttu-id="46bd5-160">NSG flow log data is written to an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="46bd5-160">NSG flow log data is written to an Azure Storage account.</span></span> <span data-ttu-id="46bd5-161">To create an Azure Storage account, select **+ Create a resource** at the top, left corner of the portal.</span><span class="sxs-lookup"><span data-stu-id="46bd5-161">To create an Azure Storage account, select **+ Create a resource** at the top, left corner of the portal.</span></span>
2. <span data-ttu-id="46bd5-162">Select **Storage**, then select **Storage account - blob, file, table, queue**.</span><span class="sxs-lookup"><span data-stu-id="46bd5-162">Select **Storage**, then select **Storage account - blob, file, table, queue**.</span></span>
3. <span data-ttu-id="46bd5-163">Enter, or select the following information, accept the remaining defaults, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="46bd5-163">Enter, or select the following information, accept the remaining defaults, and then select **Create**.</span></span>

    | <span data-ttu-id="46bd5-164">Setting</span><span class="sxs-lookup"><span data-stu-id="46bd5-164">Setting</span></span>        | <span data-ttu-id="46bd5-165">Value</span><span class="sxs-lookup"><span data-stu-id="46bd5-165">Value</span></span>                                                        |
    | ---            | ---   |
    | <span data-ttu-id="46bd5-166">Name</span><span class="sxs-lookup"><span data-stu-id="46bd5-166">Name</span></span>           | <span data-ttu-id="46bd5-167">3-24 characters in length, can only contain lowercase letters and numbers, and must be unique across all Azure Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="46bd5-167">3-24 characters in length, can only contain lowercase letters and numbers, and must be unique across all Azure Storage accounts.</span></span>                                                               |
    | <span data-ttu-id="46bd5-168">Location</span><span class="sxs-lookup"><span data-stu-id="46bd5-168">Location</span></span>       | <span data-ttu-id="46bd5-169">Select **East US**</span><span class="sxs-lookup"><span data-stu-id="46bd5-169">Select **East US**</span></span>                                           |
    | <span data-ttu-id="46bd5-170">Resource group</span><span class="sxs-lookup"><span data-stu-id="46bd5-170">Resource group</span></span> | <span data-ttu-id="46bd5-171">Select **Use existing**, and then select **myResourceGroup**</span><span class="sxs-lookup"><span data-stu-id="46bd5-171">Select **Use existing**, and then select **myResourceGroup**</span></span> |

    <span data-ttu-id="46bd5-172">The storage account may take around minute to create.</span><span class="sxs-lookup"><span data-stu-id="46bd5-172">The storage account may take around minute to create.</span></span> <span data-ttu-id="46bd5-173">Don't continue with remaining steps until the storage account is created.</span><span class="sxs-lookup"><span data-stu-id="46bd5-173">Don't continue with remaining steps until the storage account is created.</span></span> <span data-ttu-id="46bd5-174">If you use an existing storage account instead of creating one, ensure you select a storage account that has **All networks** (default) selected for **Firewalls and virtual networks**, under the **SETTINGS** for the storage account.</span><span class="sxs-lookup"><span data-stu-id="46bd5-174">If you use an existing storage account instead of creating one, ensure you select a storage account that has **All networks** (default) selected for **Firewalls and virtual networks**, under the **SETTINGS** for the storage account.</span></span>
4. <span data-ttu-id="46bd5-175">In the top, left corner of portal, select **All services**.</span><span class="sxs-lookup"><span data-stu-id="46bd5-175">In the top, left corner of portal, select **All services**.</span></span> <span data-ttu-id="46bd5-176">In the **Filter** box, type *Network Watcher*.</span><span class="sxs-lookup"><span data-stu-id="46bd5-176">In the **Filter** box, type *Network Watcher*.</span></span> <span data-ttu-id="46bd5-177">When **Network Watcher** appears in the search results, select it.</span><span class="sxs-lookup"><span data-stu-id="46bd5-177">When **Network Watcher** appears in the search results, select it.</span></span>
5. <span data-ttu-id="46bd5-178">Under **LOGS**, select **NSG flow logs**, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="46bd5-178">Under **LOGS**, select **NSG flow logs**, as shown in the following picture:</span></span>

    ![NSGs](./media/network-watcher-nsg-flow-logging-portal/nsgs.png)

6. <span data-ttu-id="46bd5-180">From the list of NSGs, select the NSG named **myVm-nsg**.</span><span class="sxs-lookup"><span data-stu-id="46bd5-180">From the list of NSGs, select the NSG named **myVm-nsg**.</span></span>
7. <span data-ttu-id="46bd5-181">Under **Flow logs settings**, select **On**.</span><span class="sxs-lookup"><span data-stu-id="46bd5-181">Under **Flow logs settings**, select **On**.</span></span>
8. <span data-ttu-id="46bd5-182">Select the storage account that you created in step 3.</span><span class="sxs-lookup"><span data-stu-id="46bd5-182">Select the storage account that you created in step 3.</span></span>
9. <span data-ttu-id="46bd5-183">Set **Retention (days)** to 5, and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="46bd5-183">Set **Retention (days)** to 5, and then select **Save**.</span></span>

## <a name="download-flow-log"></a><span data-ttu-id="46bd5-184">Download flow log</span><span class="sxs-lookup"><span data-stu-id="46bd5-184">Download flow log</span></span>

1. <span data-ttu-id="46bd5-185">From Network Watcher, in the portal, select **NSG flow logs** under **LOGS**.</span><span class="sxs-lookup"><span data-stu-id="46bd5-185">From Network Watcher, in the portal, select **NSG flow logs** under **LOGS**.</span></span>
2. <span data-ttu-id="46bd5-186">Select **You can download flow logs from configured storage accounts**, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="46bd5-186">Select **You can download flow logs from configured storage accounts**, as shown in the following picture:</span></span>

  ![Download flow logs](./media/network-watcher-nsg-flow-logging-portal/download-flow-logs.png)

3. <span data-ttu-id="46bd5-188">Select the storage account that you configured in step 2 of [Enable NSG flow log](#enable-nsg-flow-log).</span><span class="sxs-lookup"><span data-stu-id="46bd5-188">Select the storage account that you configured in step 2 of [Enable NSG flow log](#enable-nsg-flow-log).</span></span>
4. <span data-ttu-id="46bd5-189">Select **Containers**, under **BLOB SERVICE**, and then select the **insights-logs-networksecuritygroupflowevent** container, as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="46bd5-189">Select **Containers**, under **BLOB SERVICE**, and then select the **insights-logs-networksecuritygroupflowevent** container, as shown in the following picture:</span></span>

    ![Select container](./media/network-watcher-nsg-flow-logging-portal/select-container.png)
5. <span data-ttu-id="46bd5-191">Navigate the folder hierarchy and then until you get to a PT1H.json file as shown in the following picture:</span><span class="sxs-lookup"><span data-stu-id="46bd5-191">Navigate the folder hierarchy and then until you get to a PT1H.json file as shown in the following picture:</span></span>

    ![Log file](./media/network-watcher-nsg-flow-logging-portal/log-file.png)

    <span data-ttu-id="46bd5-193">Log files are written to a folder hierarchy that follows the following name convention:  https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId=/SUBSCRIPTIONS/{subscriptionID}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/{nsgName}/y={year}/m={month}/d={day}/h={hour}/m=00/macAddress={macAddress}/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="46bd5-193">Log files are written to a folder hierarchy that follows the following name convention:  https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId=/SUBSCRIPTIONS/{subscriptionID}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/{nsgName}/y={year}/m={month}/d={day}/h={hour}/m=00/macAddress={macAddress}/PT1H.json</span></span>

6. <span data-ttu-id="46bd5-194">Select **...** to the right of the PT1H.json file and select **Download**.</span><span class="sxs-lookup"><span data-stu-id="46bd5-194">Select **...** to the right of the PT1H.json file and select **Download**.</span></span>

## <a name="view-flow-log"></a><span data-ttu-id="46bd5-195">View flow log</span><span class="sxs-lookup"><span data-stu-id="46bd5-195">View flow log</span></span>

<span data-ttu-id="46bd5-196">The following json is an example of what you'll see in the PT1H.json file for each flow that data is logged for:</span><span class="sxs-lookup"><span data-stu-id="46bd5-196">The following json is an example of what you'll see in the PT1H.json file for each flow that data is logged for:</span></span>

```json
{
    "time": "2018-05-01T15:00:02.1713710Z",
    "systemId": "<Id>",
    "category": "NetworkSecurityGroupFlowEvent",
    "resourceId": "/SUBSCRIPTIONS/<Id>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/MYVM-NSG",
    "operationName": "NetworkSecurityGroupFlowEvents",
    "properties": {
        "Version": 1,
        "flows": [{
            "rule": "UserRule_default-allow-rdp",
            "flows": [{
                "mac": "000D3A170C69",
                "flowTuples": ["1525186745,192.168.1.4,10.0.0.4,55960,3389,T,I,A"]
            }]
        }]
    }
}
```

<span data-ttu-id="46bd5-197">The value for **mac** in the previous output is the MAC address of the network interface that was created when the VM was created.</span><span class="sxs-lookup"><span data-stu-id="46bd5-197">The value for **mac** in the previous output is the MAC address of the network interface that was created when the VM was created.</span></span> <span data-ttu-id="46bd5-198">The comma-separated information for **flowTuples**, is as follows:</span><span class="sxs-lookup"><span data-stu-id="46bd5-198">The comma-separated information for **flowTuples**, is as follows:</span></span>

| <span data-ttu-id="46bd5-199">Example data</span><span class="sxs-lookup"><span data-stu-id="46bd5-199">Example data</span></span> | <span data-ttu-id="46bd5-200">What data represents</span><span class="sxs-lookup"><span data-stu-id="46bd5-200">What data represents</span></span>   | <span data-ttu-id="46bd5-201">Explanation</span><span class="sxs-lookup"><span data-stu-id="46bd5-201">Explanation</span></span>                                                                              |
| ---          | ---                    | ---                                                                                      |
| <span data-ttu-id="46bd5-202">1525186745</span><span class="sxs-lookup"><span data-stu-id="46bd5-202">1525186745</span></span>   | <span data-ttu-id="46bd5-203">Time stamp</span><span class="sxs-lookup"><span data-stu-id="46bd5-203">Time stamp</span></span>             | <span data-ttu-id="46bd5-204">The time stamp of when the flow occurred, in UNIX EPOCH format.</span><span class="sxs-lookup"><span data-stu-id="46bd5-204">The time stamp of when the flow occurred, in UNIX EPOCH format.</span></span> <span data-ttu-id="46bd5-205">In the previous example, the date converts to May 1, 2018 at 2:59:05 PM GMT.</span><span class="sxs-lookup"><span data-stu-id="46bd5-205">In the previous example, the date converts to May 1, 2018 at 2:59:05 PM GMT.</span></span>                                                                                    |
| <span data-ttu-id="46bd5-206">192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="46bd5-206">192.168.1.4</span></span>  | <span data-ttu-id="46bd5-207">Source IP address</span><span class="sxs-lookup"><span data-stu-id="46bd5-207">Source IP address</span></span>      | <span data-ttu-id="46bd5-208">The source IP address that the flow originated from.</span><span class="sxs-lookup"><span data-stu-id="46bd5-208">The source IP address that the flow originated from.</span></span>
| <span data-ttu-id="46bd5-209">10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="46bd5-209">10.0.0.4</span></span>     | <span data-ttu-id="46bd5-210">Destination IP address</span><span class="sxs-lookup"><span data-stu-id="46bd5-210">Destination IP address</span></span> | <span data-ttu-id="46bd5-211">The destination IP address that the flow was destined to.</span><span class="sxs-lookup"><span data-stu-id="46bd5-211">The destination IP address that the flow was destined to.</span></span> <span data-ttu-id="46bd5-212">10.0.0.4 is the private IP address of the VM you created in [Create a VM](#create-a-vm).</span><span class="sxs-lookup"><span data-stu-id="46bd5-212">10.0.0.4 is the private IP address of the VM you created in [Create a VM](#create-a-vm).</span></span>                                                                                 |
| <span data-ttu-id="46bd5-213">55960</span><span class="sxs-lookup"><span data-stu-id="46bd5-213">55960</span></span>        | <span data-ttu-id="46bd5-214">Source port</span><span class="sxs-lookup"><span data-stu-id="46bd5-214">Source port</span></span>            | <span data-ttu-id="46bd5-215">The source port that the flow originated from.</span><span class="sxs-lookup"><span data-stu-id="46bd5-215">The source port that the flow originated from.</span></span>                                           |
| <span data-ttu-id="46bd5-216">3389</span><span class="sxs-lookup"><span data-stu-id="46bd5-216">3389</span></span>         | <span data-ttu-id="46bd5-217">Destination port</span><span class="sxs-lookup"><span data-stu-id="46bd5-217">Destination port</span></span>       | <span data-ttu-id="46bd5-218">The destination port that the flow was destined to.</span><span class="sxs-lookup"><span data-stu-id="46bd5-218">The destination port that the flow was destined to.</span></span> <span data-ttu-id="46bd5-219">Since the traffic was destined to port 3389, the rule named **UserRule_default-allow-rdp**, in the log file processed the flow.</span><span class="sxs-lookup"><span data-stu-id="46bd5-219">Since the traffic was destined to port 3389, the rule named **UserRule_default-allow-rdp**, in the log file processed the flow.</span></span>                                                |
| <span data-ttu-id="46bd5-220">T</span><span class="sxs-lookup"><span data-stu-id="46bd5-220">T</span></span>            | <span data-ttu-id="46bd5-221">Protocol</span><span class="sxs-lookup"><span data-stu-id="46bd5-221">Protocol</span></span>               | <span data-ttu-id="46bd5-222">Whether the protocol of the flow was TCP (T) or UDP (U).</span><span class="sxs-lookup"><span data-stu-id="46bd5-222">Whether the protocol of the flow was TCP (T) or UDP (U).</span></span>                                  |
| <span data-ttu-id="46bd5-223">I</span><span class="sxs-lookup"><span data-stu-id="46bd5-223">I</span></span>            | <span data-ttu-id="46bd5-224">Direction</span><span class="sxs-lookup"><span data-stu-id="46bd5-224">Direction</span></span>              | <span data-ttu-id="46bd5-225">Whether the traffic was inbound (I) or outbound (O).</span><span class="sxs-lookup"><span data-stu-id="46bd5-225">Whether the traffic was inbound (I) or outbound (O).</span></span>                                     |
| <span data-ttu-id="46bd5-226">A</span><span class="sxs-lookup"><span data-stu-id="46bd5-226">A</span></span>            | <span data-ttu-id="46bd5-227">Action</span><span class="sxs-lookup"><span data-stu-id="46bd5-227">Action</span></span>                 | <span data-ttu-id="46bd5-228">Whether the traffic was allowed (A) or denied (D).</span><span class="sxs-lookup"><span data-stu-id="46bd5-228">Whether the traffic was allowed (A) or denied (D).</span></span>                                           |

## <a name="next-steps"></a><span data-ttu-id="46bd5-229">Next steps</span><span class="sxs-lookup"><span data-stu-id="46bd5-229">Next steps</span></span>

<span data-ttu-id="46bd5-230">In this tutorial, you learned how to enable NSG flow logging for an NSG.</span><span class="sxs-lookup"><span data-stu-id="46bd5-230">In this tutorial, you learned how to enable NSG flow logging for an NSG.</span></span> <span data-ttu-id="46bd5-231">You also learned how to download and view data logged in a file.</span><span class="sxs-lookup"><span data-stu-id="46bd5-231">You also learned how to download and view data logged in a file.</span></span> <span data-ttu-id="46bd5-232">The raw data in the json file can be difficult to interpret.</span><span class="sxs-lookup"><span data-stu-id="46bd5-232">The raw data in the json file can be difficult to interpret.</span></span> <span data-ttu-id="46bd5-233">To visualize the data, you can use Network Watcher [traffic analytics](traffic-analytics.md), Microsoft [PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md), and other tools.</span><span class="sxs-lookup"><span data-stu-id="46bd5-233">To visualize the data, you can use Network Watcher [traffic analytics](traffic-analytics.md), Microsoft [PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md), and other tools.</span></span>