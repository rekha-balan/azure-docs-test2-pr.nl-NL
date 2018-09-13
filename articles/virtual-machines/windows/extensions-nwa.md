---
title: Azure Network Watcher Agent virtual machine extension for Windows | Microsoft Docs
description: Deploy the Network Watcher Agent on Windows virtual machine using a virtual machine extension.
services: virtual-machines-windows
documentationcenter: ''
author: dennisg
manager: amku
editor: ''
tags: azure-resource-manager
ms.assetid: 27e46af7-2150-45e8-b084-ba33de8c5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 5df1eb686075c3dd04e9f992885b79dfa07935ad
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549690"
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a><span data-ttu-id="b1644-103">Network Watcher Agent virtual machine extension for Windows</span><span class="sxs-lookup"><span data-stu-id="b1644-103">Network Watcher Agent virtual machine extension for Windows</span></span>

## <a name="overview"></a><span data-ttu-id="b1644-104">Overview</span><span class="sxs-lookup"><span data-stu-id="b1644-104">Overview</span></span>

<span data-ttu-id="b1644-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span><span class="sxs-lookup"><span data-stu-id="b1644-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="b1644-106">The Network Watcher Agent virtual machine extension is a requirement for some of the Network Watcher features on Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="b1644-106">The Network Watcher Agent virtual machine extension is a requirement for some of the Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="b1644-107">This includes capturing network traffic on demand and other advanced functionality.</span><span class="sxs-lookup"><span data-stu-id="b1644-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="b1644-108">This document details the supported platforms and deployment options for the Network Watcher Agent virtual machine extension for Windows.</span><span class="sxs-lookup"><span data-stu-id="b1644-108">This document details the supported platforms and deployment options for the Network Watcher Agent virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1644-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b1644-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="b1644-110">Operating system</span><span class="sxs-lookup"><span data-stu-id="b1644-110">Operating system</span></span>

<span data-ttu-id="b1644-111">The Network Watcher Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span><span class="sxs-lookup"><span data-stu-id="b1644-111">The Network Watcher Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span> <span data-ttu-id="b1644-112">Note that the Nano Server is not supported at this time.</span><span class="sxs-lookup"><span data-stu-id="b1644-112">Note that the Nano Server is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="b1644-113">Internet connectivity</span><span class="sxs-lookup"><span data-stu-id="b1644-113">Internet connectivity</span></span>

<span data-ttu-id="b1644-114">Some of the Network Watcher Agent functionality requires that the target virtual machine be connected to the Internet.</span><span class="sxs-lookup"><span data-stu-id="b1644-114">Some of the Network Watcher Agent functionality requires that the target virtual machine be connected to the Internet.</span></span> <span data-ttu-id="b1644-115">Without the ability to establish outgoing connections some of the Network Watcher Agent features may malfunction or become unavailable.</span><span class="sxs-lookup"><span data-stu-id="b1644-115">Without the ability to establish outgoing connections some of the Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="b1644-116">For more details, please see the [Network Watcher documentation](../../network-watcher/network-watcher-monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b1644-116">For more details, please see the [Network Watcher documentation](../../network-watcher/network-watcher-monitoring-overview.md).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="b1644-117">Extension schema</span><span class="sxs-lookup"><span data-stu-id="b1644-117">Extension schema</span></span>

<span data-ttu-id="b1644-118">The following JSON shows the schema for the Network Watcher Agent extension.</span><span class="sxs-lookup"><span data-stu-id="b1644-118">The following JSON shows the schema for the Network Watcher Agent extension.</span></span> <span data-ttu-id="b1644-119">The extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span><span class="sxs-lookup"><span data-stu-id="b1644-119">The extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentWindows",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="b1644-120">Property values</span><span class="sxs-lookup"><span data-stu-id="b1644-120">Property values</span></span>

| <span data-ttu-id="b1644-121">Name</span><span class="sxs-lookup"><span data-stu-id="b1644-121">Name</span></span> | <span data-ttu-id="b1644-122">Value / Example</span><span class="sxs-lookup"><span data-stu-id="b1644-122">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="b1644-123">apiVersion</span><span class="sxs-lookup"><span data-stu-id="b1644-123">apiVersion</span></span> | <span data-ttu-id="b1644-124">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="b1644-124">2015-06-15</span></span> |
| <span data-ttu-id="b1644-125">publisher</span><span class="sxs-lookup"><span data-stu-id="b1644-125">publisher</span></span> | <span data-ttu-id="b1644-126">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="b1644-126">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="b1644-127">type</span><span class="sxs-lookup"><span data-stu-id="b1644-127">type</span></span> | <span data-ttu-id="b1644-128">NetworkWatcherAgentWindows</span><span class="sxs-lookup"><span data-stu-id="b1644-128">NetworkWatcherAgentWindows</span></span> |
| <span data-ttu-id="b1644-129">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="b1644-129">typeHandlerVersion</span></span> | <span data-ttu-id="b1644-130">1.4</span><span class="sxs-lookup"><span data-stu-id="b1644-130">1.4</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="b1644-131">Template deployment</span><span class="sxs-lookup"><span data-stu-id="b1644-131">Template deployment</span></span>

<span data-ttu-id="b1644-132">Azure VM extensions can be deployed with Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="b1644-132">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="b1644-133">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Network Watcher Agent extension during an Azure Resource Manager template deployment.</span><span class="sxs-lookup"><span data-stu-id="b1644-133">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="b1644-134">PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="b1644-134">PowerShell deployment</span></span>

<span data-ttu-id="b1644-135">The `Set-AzureRmVMExtension` command can be used to deploy the Network Watcher Agent virtual machine extension to an existing virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b1644-135">The `Set-AzureRmVMExtension` command can be used to deploy the Network Watcher Agent virtual machine extension to an existing virtual machine.</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="b1644-136">Troubleshooting and support</span><span class="sxs-lookup"><span data-stu-id="b1644-136">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="b1644-137">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="b1644-137">Troubleshooting</span></span>

<span data-ttu-id="b1644-138">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="b1644-138">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="b1644-139">To see the deployment state of extensions for a given VM, run the following command using the Azure PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="b1644-139">To see the deployment state of extensions for a given VM, run the following command using the Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

<span data-ttu-id="b1644-140">Extension execution output is logged to files found in the following directory:</span><span class="sxs-lookup"><span data-stu-id="b1644-140">Extension execution output is logged to files found in the following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a><span data-ttu-id="b1644-141">Support</span><span class="sxs-lookup"><span data-stu-id="b1644-141">Support</span></span>

<span data-ttu-id="b1644-142">If you need more help at any point in this article, you can refer to the Network Watcher User Guide documentation or contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="b1644-142">If you need more help at any point in this article, you can refer to the Network Watcher User Guide documentation or contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="b1644-143">Alternatively, you can file an Azure support incident.</span><span class="sxs-lookup"><span data-stu-id="b1644-143">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="b1644-144">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span><span class="sxs-lookup"><span data-stu-id="b1644-144">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="b1644-145">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="b1644-145">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
