---
title: Azure Network Watcher Agent virtual machine extension for Linux | Microsoft Docs
description: Deploy the Network Watcher Agent on Linux virtual machine using a virtual machine extension.
services: virtual-machines-linux
documentationcenter: ''
author: dennisg
manager: amku
editor: ''
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: eaadd531b9e05a54446e61f98584ae9d75470a5f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672030"
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a><span data-ttu-id="d92fe-103">Network Watcher Agent virtual machine extension for Linux</span><span class="sxs-lookup"><span data-stu-id="d92fe-103">Network Watcher Agent virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="d92fe-104">Overview</span><span class="sxs-lookup"><span data-stu-id="d92fe-104">Overview</span></span>

<span data-ttu-id="d92fe-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span><span class="sxs-lookup"><span data-stu-id="d92fe-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="d92fe-106">The Network Watcher Agent virtual machine extension is a requirement for some of the Network Watcher features on Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="d92fe-106">The Network Watcher Agent virtual machine extension is a requirement for some of the Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="d92fe-107">This includes capturing network traffic on demand and other advanced functionality.</span><span class="sxs-lookup"><span data-stu-id="d92fe-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="d92fe-108">This document details the supported platforms and deployment options for the Network Watcher Agent virtual machine extension for Linux.</span><span class="sxs-lookup"><span data-stu-id="d92fe-108">This document details the supported platforms and deployment options for the Network Watcher Agent virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d92fe-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d92fe-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="d92fe-110">Operating system</span><span class="sxs-lookup"><span data-stu-id="d92fe-110">Operating system</span></span>

<span data-ttu-id="d92fe-111">The Network Watcher Agent extension can be run against these Linux distributions:</span><span class="sxs-lookup"><span data-stu-id="d92fe-111">The Network Watcher Agent extension can be run against these Linux distributions:</span></span>

| <span data-ttu-id="d92fe-112">Distribution</span><span class="sxs-lookup"><span data-stu-id="d92fe-112">Distribution</span></span> | <span data-ttu-id="d92fe-113">Version</span><span class="sxs-lookup"><span data-stu-id="d92fe-113">Version</span></span> |
|---|---|
| <span data-ttu-id="d92fe-114">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="d92fe-114">Ubuntu</span></span> | <span data-ttu-id="d92fe-115">16.04 LTS, 14.04 LTS and 12.04 LTS</span><span class="sxs-lookup"><span data-stu-id="d92fe-115">16.04 LTS, 14.04 LTS and 12.04 LTS</span></span> |
| <span data-ttu-id="d92fe-116">Debian</span><span class="sxs-lookup"><span data-stu-id="d92fe-116">Debian</span></span> | <span data-ttu-id="d92fe-117">7 and 8</span><span class="sxs-lookup"><span data-stu-id="d92fe-117">7 and 8</span></span> |
| <span data-ttu-id="d92fe-118">RedHat</span><span class="sxs-lookup"><span data-stu-id="d92fe-118">RedHat</span></span> | <span data-ttu-id="d92fe-119">6.x and 7.x</span><span class="sxs-lookup"><span data-stu-id="d92fe-119">6.x and 7.x</span></span> |
| <span data-ttu-id="d92fe-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="d92fe-120">Oracle Linux</span></span> | <span data-ttu-id="d92fe-121">7x</span><span class="sxs-lookup"><span data-stu-id="d92fe-121">7x</span></span> |
| <span data-ttu-id="d92fe-122">Suse</span><span class="sxs-lookup"><span data-stu-id="d92fe-122">Suse</span></span> | <span data-ttu-id="d92fe-123">11 and 12</span><span class="sxs-lookup"><span data-stu-id="d92fe-123">11 and 12</span></span> |
| <span data-ttu-id="d92fe-124">OpenSuse</span><span class="sxs-lookup"><span data-stu-id="d92fe-124">OpenSuse</span></span> | <span data-ttu-id="d92fe-125">7.0</span><span class="sxs-lookup"><span data-stu-id="d92fe-125">7.0</span></span> |
| <span data-ttu-id="d92fe-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="d92fe-126">CentOS</span></span> | <span data-ttu-id="d92fe-127">7.0</span><span class="sxs-lookup"><span data-stu-id="d92fe-127">7.0</span></span> |

<span data-ttu-id="d92fe-128">Note that CoreOS is not supported at this time.</span><span class="sxs-lookup"><span data-stu-id="d92fe-128">Note that CoreOS is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="d92fe-129">Internet connectivity</span><span class="sxs-lookup"><span data-stu-id="d92fe-129">Internet connectivity</span></span>

<span data-ttu-id="d92fe-130">Some of the Network Watcher Agent functionality requires that the target virtual machine be connected to the Internet.</span><span class="sxs-lookup"><span data-stu-id="d92fe-130">Some of the Network Watcher Agent functionality requires that the target virtual machine be connected to the Internet.</span></span> <span data-ttu-id="d92fe-131">Without the ability to establish outgoing connections some of the Network Watcher Agent features may malfunction or become unavailable.</span><span class="sxs-lookup"><span data-stu-id="d92fe-131">Without the ability to establish outgoing connections some of the Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="d92fe-132">For more details, please see the [Network Watcher documentation](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span><span class="sxs-lookup"><span data-stu-id="d92fe-132">For more details, please see the [Network Watcher documentation](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="d92fe-133">Extension schema</span><span class="sxs-lookup"><span data-stu-id="d92fe-133">Extension schema</span></span>

<span data-ttu-id="d92fe-134">The following JSON shows the schema for the Network Watcher Agent extension.</span><span class="sxs-lookup"><span data-stu-id="d92fe-134">The following JSON shows the schema for the Network Watcher Agent extension.</span></span> <span data-ttu-id="d92fe-135">The extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span><span class="sxs-lookup"><span data-stu-id="d92fe-135">The extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

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
        "type": "NetworkWatcherAgentLinux",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="d92fe-136">Property values</span><span class="sxs-lookup"><span data-stu-id="d92fe-136">Property values</span></span>

| <span data-ttu-id="d92fe-137">Name</span><span class="sxs-lookup"><span data-stu-id="d92fe-137">Name</span></span> | <span data-ttu-id="d92fe-138">Value / Example</span><span class="sxs-lookup"><span data-stu-id="d92fe-138">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="d92fe-139">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d92fe-139">apiVersion</span></span> | <span data-ttu-id="d92fe-140">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="d92fe-140">2015-06-15</span></span> |
| <span data-ttu-id="d92fe-141">publisher</span><span class="sxs-lookup"><span data-stu-id="d92fe-141">publisher</span></span> | <span data-ttu-id="d92fe-142">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="d92fe-142">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="d92fe-143">type</span><span class="sxs-lookup"><span data-stu-id="d92fe-143">type</span></span> | <span data-ttu-id="d92fe-144">NetworkWatcherAgentLinux</span><span class="sxs-lookup"><span data-stu-id="d92fe-144">NetworkWatcherAgentLinux</span></span> |
| <span data-ttu-id="d92fe-145">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="d92fe-145">typeHandlerVersion</span></span> | <span data-ttu-id="d92fe-146">1.4</span><span class="sxs-lookup"><span data-stu-id="d92fe-146">1.4</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="d92fe-147">Template deployment</span><span class="sxs-lookup"><span data-stu-id="d92fe-147">Template deployment</span></span>

<span data-ttu-id="d92fe-148">Azure VM extensions can be deployed with Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="d92fe-148">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="d92fe-149">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Network Watcher Agent extension during an Azure Resource Manager template deployment.</span><span class="sxs-lookup"><span data-stu-id="d92fe-149">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="azure-cli-deployment"></a><span data-ttu-id="d92fe-150">Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="d92fe-150">Azure CLI deployment</span></span>

<span data-ttu-id="d92fe-151">The Azure CLI can be used to deploy the Network Watcher Agent VM extension to an existing virtual machine.</span><span class="sxs-lookup"><span data-stu-id="d92fe-151">The Azure CLI can be used to deploy the Network Watcher Agent VM extension to an existing virtual machine.</span></span>

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="d92fe-152">Troubleshooting and support</span><span class="sxs-lookup"><span data-stu-id="d92fe-152">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="d92fe-153">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="d92fe-153">Troubleshooting</span></span>

<span data-ttu-id="d92fe-154">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d92fe-154">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure CLI.</span></span> <span data-ttu-id="d92fe-155">To see the deployment state of extensions for a given VM, run the following command using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d92fe-155">To see the deployment state of extensions for a given VM, run the following command using the Azure CLI.</span></span>

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

<span data-ttu-id="d92fe-156">Extension execution output is logged to files found in the following directory:</span><span class="sxs-lookup"><span data-stu-id="d92fe-156">Extension execution output is logged to files found in the following directory:</span></span>

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a><span data-ttu-id="d92fe-157">Support</span><span class="sxs-lookup"><span data-stu-id="d92fe-157">Support</span></span>

<span data-ttu-id="d92fe-158">If you need more help at any point in this article, you can refer to the Network Watcher documentation or contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="d92fe-158">If you need more help at any point in this article, you can refer to the Network Watcher documentation or contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="d92fe-159">Alternatively, you can file an Azure support incident.</span><span class="sxs-lookup"><span data-stu-id="d92fe-159">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="d92fe-160">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span><span class="sxs-lookup"><span data-stu-id="d92fe-160">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="d92fe-161">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="d92fe-161">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
