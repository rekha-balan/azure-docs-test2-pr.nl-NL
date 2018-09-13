---
title: OMS Azure virtual machine extension for Linux | Microsoft Docs
description: Deploy the OMS agent on Linux virtual machine using a virtual machine extension.
services: virtual-machines-linux
documentationcenter: ''
author: neilpeterson
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: nepeters
ms.openlocfilehash: 644bcf56d9fe0d5acf5f4bff99a5bdfaf6a7a6e5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554727"
---
# <a name="oms-virtual-machine-extension-for-linux"></a><span data-ttu-id="acb86-103">OMS virtual machine extension for Linux</span><span class="sxs-lookup"><span data-stu-id="acb86-103">OMS virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="acb86-104">Overview</span><span class="sxs-lookup"><span data-stu-id="acb86-104">Overview</span></span>

<span data-ttu-id="acb86-105">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span><span class="sxs-lookup"><span data-stu-id="acb86-105">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="acb86-106">The OMS Agent virtual machine extension for Linux is published and supported by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="acb86-106">The OMS Agent virtual machine extension for Linux is published and supported by Microsoft.</span></span> <span data-ttu-id="acb86-107">The extension installs the OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span><span class="sxs-lookup"><span data-stu-id="acb86-107">The extension installs the OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="acb86-108">This document details the supported platforms, configurations, and deployment options for the OMS virtual machine extension for Linux.</span><span class="sxs-lookup"><span data-stu-id="acb86-108">This document details the supported platforms, configurations, and deployment options for the OMS virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acb86-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="acb86-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="acb86-110">Operating system</span><span class="sxs-lookup"><span data-stu-id="acb86-110">Operating system</span></span>

<span data-ttu-id="acb86-111">The OMS Agent extension can be run against these Linux distributions.</span><span class="sxs-lookup"><span data-stu-id="acb86-111">The OMS Agent extension can be run against these Linux distributions.</span></span>

| <span data-ttu-id="acb86-112">Distribution</span><span class="sxs-lookup"><span data-stu-id="acb86-112">Distribution</span></span> | <span data-ttu-id="acb86-113">Version</span><span class="sxs-lookup"><span data-stu-id="acb86-113">Version</span></span> |
|---|---|
| <span data-ttu-id="acb86-114">CentOS Linux</span><span class="sxs-lookup"><span data-stu-id="acb86-114">CentOS Linux</span></span> | <span data-ttu-id="acb86-115">5,6, and 7</span><span class="sxs-lookup"><span data-stu-id="acb86-115">5,6, and 7</span></span> |
| <span data-ttu-id="acb86-116">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="acb86-116">Oracle Linux</span></span> | <span data-ttu-id="acb86-117">5,6, and 7</span><span class="sxs-lookup"><span data-stu-id="acb86-117">5,6, and 7</span></span> |
| <span data-ttu-id="acb86-118">Red Hat Enterprise Linux Server</span><span class="sxs-lookup"><span data-stu-id="acb86-118">Red Hat Enterprise Linux Server</span></span> | <span data-ttu-id="acb86-119">5,6 and 7</span><span class="sxs-lookup"><span data-stu-id="acb86-119">5,6 and 7</span></span> |
| <span data-ttu-id="acb86-120">Debian GNU/Linux</span><span class="sxs-lookup"><span data-stu-id="acb86-120">Debian GNU/Linux</span></span> | <span data-ttu-id="acb86-121">6, 7, and 8</span><span class="sxs-lookup"><span data-stu-id="acb86-121">6, 7, and 8</span></span> |
| <span data-ttu-id="acb86-122">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="acb86-122">Ubuntu</span></span> | <span data-ttu-id="acb86-123">12.04 LTS, 14.04 LTS, 15.04</span><span class="sxs-lookup"><span data-stu-id="acb86-123">12.04 LTS, 14.04 LTS, 15.04</span></span> |
| <span data-ttu-id="acb86-124">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="acb86-124">SUSE Linux Enterprise Server</span></span> | <span data-ttu-id="acb86-125">11 and 12</span><span class="sxs-lookup"><span data-stu-id="acb86-125">11 and 12</span></span> |

### <a name="internet-connectivity"></a><span data-ttu-id="acb86-126">Internet connectivity</span><span class="sxs-lookup"><span data-stu-id="acb86-126">Internet connectivity</span></span>

<span data-ttu-id="acb86-127">The OMS Agent extension for Linux requires that the target virtual machine is connected to the internet.</span><span class="sxs-lookup"><span data-stu-id="acb86-127">The OMS Agent extension for Linux requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="acb86-128">Extension schema</span><span class="sxs-lookup"><span data-stu-id="acb86-128">Extension schema</span></span>

<span data-ttu-id="acb86-129">The following JSON shows the schema for the OMS Agent extension.</span><span class="sxs-lookup"><span data-stu-id="acb86-129">The following JSON shows the schema for the OMS Agent extension.</span></span> <span data-ttu-id="acb86-130">The extension requires the workspace Id and workspace key from the target OMS workspace, these can be found in the OMS portal.</span><span class="sxs-lookup"><span data-stu-id="acb86-130">The extension requires the workspace Id and workspace key from the target OMS workspace, these can be found in the OMS portal.</span></span> <span data-ttu-id="acb86-131">Because the workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span><span class="sxs-lookup"><span data-stu-id="acb86-131">Because the workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="acb86-132">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span><span class="sxs-lookup"><span data-stu-id="acb86-132">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span> <span data-ttu-id="acb86-133">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="acb86-133">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.0",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a><span data-ttu-id="acb86-134">Property values</span><span class="sxs-lookup"><span data-stu-id="acb86-134">Property values</span></span>

| <span data-ttu-id="acb86-135">Name</span><span class="sxs-lookup"><span data-stu-id="acb86-135">Name</span></span> | <span data-ttu-id="acb86-136">Value / Example</span><span class="sxs-lookup"><span data-stu-id="acb86-136">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="acb86-137">apiVersion</span><span class="sxs-lookup"><span data-stu-id="acb86-137">apiVersion</span></span> | <span data-ttu-id="acb86-138">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="acb86-138">2015-06-15</span></span> |
| <span data-ttu-id="acb86-139">publisher</span><span class="sxs-lookup"><span data-stu-id="acb86-139">publisher</span></span> | <span data-ttu-id="acb86-140">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="acb86-140">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="acb86-141">type</span><span class="sxs-lookup"><span data-stu-id="acb86-141">type</span></span> | <span data-ttu-id="acb86-142">OmsAgentForLinux</span><span class="sxs-lookup"><span data-stu-id="acb86-142">OmsAgentForLinux</span></span> |
| <span data-ttu-id="acb86-143">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="acb86-143">typeHandlerVersion</span></span> | <span data-ttu-id="acb86-144">1.0</span><span class="sxs-lookup"><span data-stu-id="acb86-144">1.0</span></span> |
| <span data-ttu-id="acb86-145">workspaceId (e.g)</span><span class="sxs-lookup"><span data-stu-id="acb86-145">workspaceId (e.g)</span></span> | <span data-ttu-id="acb86-146">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="acb86-146">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="acb86-147">workspaceKey (e.g)</span><span class="sxs-lookup"><span data-stu-id="acb86-147">workspaceKey (e.g)</span></span> | <span data-ttu-id="acb86-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="acb86-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="acb86-149">Template deployment</span><span class="sxs-lookup"><span data-stu-id="acb86-149">Template deployment</span></span>

<span data-ttu-id="acb86-150">Azure VM extensions can be deployed with Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="acb86-150">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="acb86-151">Templates are ideal when deploying one or more virtual machines that require post deployment configuration such as onboarding to OMS.</span><span class="sxs-lookup"><span data-stu-id="acb86-151">Templates are ideal when deploying one or more virtual machines that require post deployment configuration such as onboarding to OMS.</span></span> <span data-ttu-id="acb86-152">A sample Resource Manager template that includes the OMS Agent VM extension can be found on the [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span><span class="sxs-lookup"><span data-stu-id="acb86-152">A sample Resource Manager template that includes the OMS Agent VM extension can be found on the [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span></span> 

<span data-ttu-id="acb86-153">The JSON for a virtual machine extension can be nested inside the virtual machine resource, or placed at the root or top level of a Resource Manager JSON template.</span><span class="sxs-lookup"><span data-stu-id="acb86-153">The JSON for a virtual machine extension can be nested inside the virtual machine resource, or placed at the root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="acb86-154">The placement of the JSON affects the value of the resource name and type.</span><span class="sxs-lookup"><span data-stu-id="acb86-154">The placement of the JSON affects the value of the resource name and type.</span></span> <span data-ttu-id="acb86-155">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span><span class="sxs-lookup"><span data-stu-id="acb86-155">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="acb86-156">The following example assumes the OMS extension is nested inside the virtual machine resource.</span><span class="sxs-lookup"><span data-stu-id="acb86-156">The following example assumes the OMS extension is nested inside the virtual machine resource.</span></span> <span data-ttu-id="acb86-157">When nesting the extension resource, the JSON is placed in the `"resources": []` object of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="acb86-157">When nesting the extension resource, the JSON is placed in the `"resources": []` object of the virtual machine.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.0",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

<span data-ttu-id="acb86-158">When placing the extension JSON at the root of the template, the resource name includes a reference to the parent virtual machine, and the type reflects the nested configuration.</span><span class="sxs-lookup"><span data-stu-id="acb86-158">When placing the extension JSON at the root of the template, the resource name includes a reference to the parent virtual machine, and the type reflects the nested configuration.</span></span>  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.0",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a><span data-ttu-id="acb86-159">Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="acb86-159">Azure CLI deployment</span></span>

<span data-ttu-id="acb86-160">The Azure CLI can be used to deploy the OMS Agent VM extension to an existing virtual machine.</span><span class="sxs-lookup"><span data-stu-id="acb86-160">The Azure CLI can be used to deploy the OMS Agent VM extension to an existing virtual machine.</span></span> <span data-ttu-id="acb86-161">Before deploying OMS Agent Extension, create a public.json and protected.json file.</span><span class="sxs-lookup"><span data-stu-id="acb86-161">Before deploying OMS Agent Extension, create a public.json and protected.json file.</span></span> <span data-ttu-id="acb86-162">The schema for these files is detailed earlier in this document.</span><span class="sxs-lookup"><span data-stu-id="acb86-162">The schema for these files is detailed earlier in this document.</span></span>

```azurecli
azure vm extension set myResourceGroup myVM \
  OmsAgentForLinux Microsoft.EnterpriseCloud.Monitoring 1.0 \
  --public-config-path public.json  \
  --private-config-path protected.json
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="acb86-163">Troubleshoot and support</span><span class="sxs-lookup"><span data-stu-id="acb86-163">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="acb86-164">Troubleshoot</span><span class="sxs-lookup"><span data-stu-id="acb86-164">Troubleshoot</span></span>

<span data-ttu-id="acb86-165">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="acb86-165">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure CLI.</span></span> <span data-ttu-id="acb86-166">To see the deployment state of extensions for a given VM, run the following command using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="acb86-166">To see the deployment state of extensions for a given VM, run the following command using the Azure CLI.</span></span>

```azurecli
azure vm extension get myResourceGroup myVM
```

<span data-ttu-id="acb86-167">Extension execution output is logged to the following file:</span><span class="sxs-lookup"><span data-stu-id="acb86-167">Extension execution output is logged to the following file:</span></span>

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="support"></a><span data-ttu-id="acb86-168">Support</span><span class="sxs-lookup"><span data-stu-id="acb86-168">Support</span></span>

<span data-ttu-id="acb86-169">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="acb86-169">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="acb86-170">Alternatively, you can file an Azure support incident.</span><span class="sxs-lookup"><span data-stu-id="acb86-170">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="acb86-171">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span><span class="sxs-lookup"><span data-stu-id="acb86-171">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="acb86-172">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="acb86-172">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
