---
title: Virtual machine extensions and features for Linux | Microsoft Docs
description: Learn what extensions are available for Azure virtual machines, grouped by what they provide or improve.
services: virtual-machines-linux
documentationcenter: ''
author: neilpeterson
manager: timlt
editor: ''
tags: azure-service-management,azure-resource-manager
ms.assetid: 52f5d0ec-8f75-49e7-9e15-88d46b420e63
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/06/2017
ms.author: nepeters
ms.openlocfilehash: a2c86b7d1f781deea0bb8bb2404b0a3f9c90118a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554801"
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a><span data-ttu-id="317d2-103">Virtual machine extensions and features for Linux</span><span class="sxs-lookup"><span data-stu-id="317d2-103">Virtual machine extensions and features for Linux</span></span>

<span data-ttu-id="317d2-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="317d2-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="317d2-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used to complete these tasks.</span><span class="sxs-lookup"><span data-stu-id="317d2-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used to complete these tasks.</span></span> <span data-ttu-id="317d2-106">Azure VM extensions can be run using the Azure CLI, PowerShell, Azure Resource Manager templates, and the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="317d2-106">Azure VM extensions can be run using the Azure CLI, PowerShell, Azure Resource Manager templates, and the Azure portal.</span></span> <span data-ttu-id="317d2-107">Extensions can be bundled with a new virtual machine deployment, or run against any existing system.</span><span class="sxs-lookup"><span data-stu-id="317d2-107">Extensions can be bundled with a new virtual machine deployment, or run against any existing system.</span></span>

<span data-ttu-id="317d2-108">This document provides an overview of VM extensions, prerequisites for using Azure VM extensions, and guidance on how to detect, manage, and remove VM extensions.</span><span class="sxs-lookup"><span data-stu-id="317d2-108">This document provides an overview of VM extensions, prerequisites for using Azure VM extensions, and guidance on how to detect, manage, and remove VM extensions.</span></span> <span data-ttu-id="317d2-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span><span class="sxs-lookup"><span data-stu-id="317d2-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="317d2-110">Extension-specific details can be found in each document specific to the individual extension.</span><span class="sxs-lookup"><span data-stu-id="317d2-110">Extension-specific details can be found in each document specific to the individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="317d2-111">Use cases and samples</span><span class="sxs-lookup"><span data-stu-id="317d2-111">Use cases and samples</span></span>

<span data-ttu-id="317d2-112">Several different Azure VM extensions are available, each with a specific use case.</span><span class="sxs-lookup"><span data-stu-id="317d2-112">Several different Azure VM extensions are available, each with a specific use case.</span></span> <span data-ttu-id="317d2-113">Some examples are:</span><span class="sxs-lookup"><span data-stu-id="317d2-113">Some examples are:</span></span>

- <span data-ttu-id="317d2-114">Apply PowerShell Desired State configurations to a virtual machine using the DSC extension for Linux.</span><span class="sxs-lookup"><span data-stu-id="317d2-114">Apply PowerShell Desired State configurations to a virtual machine using the DSC extension for Linux.</span></span> <span data-ttu-id="317d2-115">For more information, see [Azure Desired State configuration extension](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span><span class="sxs-lookup"><span data-stu-id="317d2-115">For more information, see [Azure Desired State configuration extension](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span></span>
- <span data-ttu-id="317d2-116">Configure monitoring of a virtual machine with the Microsoft Monitoring Agent VM extension.</span><span class="sxs-lookup"><span data-stu-id="317d2-116">Configure monitoring of a virtual machine with the Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="317d2-117">For more information, see [Enable or disable VM monitoring](vm-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="317d2-117">For more information, see [Enable or disable VM monitoring](vm-monitoring.md).</span></span>
- <span data-ttu-id="317d2-118">Configure monitoring of your Azure infrastructure with the Datadog extension.</span><span class="sxs-lookup"><span data-stu-id="317d2-118">Configure monitoring of your Azure infrastructure with the Datadog extension.</span></span> <span data-ttu-id="317d2-119">For more information, see the [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="317d2-119">For more information, see the [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="317d2-120">Configure a Docker host on an Azure virtual machine using the Docker VM extension.</span><span class="sxs-lookup"><span data-stu-id="317d2-120">Configure a Docker host on an Azure virtual machine using the Docker VM extension.</span></span> <span data-ttu-id="317d2-121">For more information, see [Docker VM extension](dockerextension.md).</span><span class="sxs-lookup"><span data-stu-id="317d2-121">For more information, see [Docker VM extension](dockerextension.md).</span></span>

<span data-ttu-id="317d2-122">In addition to process-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span><span class="sxs-lookup"><span data-stu-id="317d2-122">In addition to process-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="317d2-123">The Custom Script extension for Linux allows any Bash script to be run on a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="317d2-123">The Custom Script extension for Linux allows any Bash script to be run on a virtual machine.</span></span> <span data-ttu-id="317d2-124">Custom scripts are useful for designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span><span class="sxs-lookup"><span data-stu-id="317d2-124">Custom scripts are useful for designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="317d2-125">For more information, see [Linux VM Custom Script extension](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="317d2-125">For more information, see [Linux VM Custom Script extension](extensions-customscript.md).</span></span>

<span data-ttu-id="317d2-126">To work through an example where a VM extension is used in an end-to-end application deployment, see [Automating application deployments to Azure virtual machines](../windows/dotnet-core-1-landing.md).</span><span class="sxs-lookup"><span data-stu-id="317d2-126">To work through an example where a VM extension is used in an end-to-end application deployment, see [Automating application deployments to Azure virtual machines](../windows/dotnet-core-1-landing.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="317d2-127">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="317d2-127">Prerequisites</span></span>

<span data-ttu-id="317d2-128">Each virtual machine extension might have its own set of prerequisites.</span><span class="sxs-lookup"><span data-stu-id="317d2-128">Each virtual machine extension might have its own set of prerequisites.</span></span> <span data-ttu-id="317d2-129">For instance, the Docker VM extension has a prerequisite of a supported Linux distribution.</span><span class="sxs-lookup"><span data-stu-id="317d2-129">For instance, the Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="317d2-130">Requirements of individual extensions are detailed in the extension-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="317d2-130">Requirements of individual extensions are detailed in the extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="317d2-131">Azure VM agent</span><span class="sxs-lookup"><span data-stu-id="317d2-131">Azure VM agent</span></span>

<span data-ttu-id="317d2-132">The Azure VM agent manages interactions between an Azure virtual machine and the Azure fabric controller.</span><span class="sxs-lookup"><span data-stu-id="317d2-132">The Azure VM agent manages interactions between an Azure virtual machine and the Azure fabric controller.</span></span> <span data-ttu-id="317d2-133">The VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span><span class="sxs-lookup"><span data-stu-id="317d2-133">The VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="317d2-134">The Azure VM agent is preinstalled on Azure Marketplace images and can be installed manually on supported operating systems.</span><span class="sxs-lookup"><span data-stu-id="317d2-134">The Azure VM agent is preinstalled on Azure Marketplace images and can be installed manually on supported operating systems.</span></span>

<span data-ttu-id="317d2-135">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](../windows/classic/agents-and-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="317d2-135">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](../windows/classic/agents-and-extensions.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="317d2-136">Discover VM extensions</span><span class="sxs-lookup"><span data-stu-id="317d2-136">Discover VM extensions</span></span>

<span data-ttu-id="317d2-137">Many different VM extensions are available for use with Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="317d2-137">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="317d2-138">To see a complete list, run the following command with the Azure CLI, replacing the example location with the location of your choice.</span><span class="sxs-lookup"><span data-stu-id="317d2-138">To see a complete list, run the following command with the Azure CLI, replacing the example location with the location of your choice.</span></span>

```azurecli
azure vm extension-image list westus
```

## <a name="run-vm-extensions"></a><span data-ttu-id="317d2-139">Run VM extensions</span><span class="sxs-lookup"><span data-stu-id="317d2-139">Run VM extensions</span></span>

<span data-ttu-id="317d2-140">Azure virtual machine extensions can be run on existing virtual machines, which are useful when you need to make configuration changes or recover connectivity on an already deployed VM.</span><span class="sxs-lookup"><span data-stu-id="317d2-140">Azure virtual machine extensions can be run on existing virtual machines, which are useful when you need to make configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="317d2-141">VM extensions can also be bundled with Azure Resource Manager template deployments.</span><span class="sxs-lookup"><span data-stu-id="317d2-141">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="317d2-142">By using extensions with Resource Manager templates, Azure virtual machines can be deployed and configured without post-deployment intervention.</span><span class="sxs-lookup"><span data-stu-id="317d2-142">By using extensions with Resource Manager templates, Azure virtual machines can be deployed and configured without post-deployment intervention.</span></span>

<span data-ttu-id="317d2-143">The following methods can be used to run an extension against an existing virtual machine.</span><span class="sxs-lookup"><span data-stu-id="317d2-143">The following methods can be used to run an extension against an existing virtual machine.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="317d2-144">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="317d2-144">Azure CLI</span></span>

<span data-ttu-id="317d2-145">Azure virtual machine extensions can be run against an existing virtual machine by using the `azure vm extension set` command.</span><span class="sxs-lookup"><span data-stu-id="317d2-145">Azure virtual machine extensions can be run against an existing virtual machine by using the `azure vm extension set` command.</span></span> <span data-ttu-id="317d2-146">This example runs the custom script extension against a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="317d2-146">This example runs the custom script extension against a virtual machine.</span></span>

```azurecli
azure vm extension set myResourceGroup myVM CustomScript Microsoft.Azure.Extensions 2.0 \
  --auto-upgrade-minor-version \
  --public-config '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

<span data-ttu-id="317d2-147">The script produces output similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="317d2-147">The script produces output similar to the following text:</span></span>

```azurecli
info:    Executing command vm extension set
+ Looking up the VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a><span data-ttu-id="317d2-148">Azure portal</span><span class="sxs-lookup"><span data-stu-id="317d2-148">Azure portal</span></span>

<span data-ttu-id="317d2-149">VM extensions can be applied to an existing virtual machine through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="317d2-149">VM extensions can be applied to an existing virtual machine through the Azure portal.</span></span> <span data-ttu-id="317d2-150">To do so, select the virtual machine, choose **Extensions**, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="317d2-150">To do so, select the virtual machine, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="317d2-151">Select the extension you want from the list of available extensions and follow the instructions in the wizard.</span><span class="sxs-lookup"><span data-stu-id="317d2-151">Select the extension you want from the list of available extensions and follow the instructions in the wizard.</span></span>

<span data-ttu-id="317d2-152">The following image shows the installation of the Linux Custom Script extension from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="317d2-152">The following image shows the installation of the Linux Custom Script extension from the Azure portal.</span></span>

![Install custom script extension](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="317d2-154">Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="317d2-154">Azure Resource Manager templates</span></span>

<span data-ttu-id="317d2-155">VM extensions can be added to an Azure Resource Manager template and executed with the deployment of the template.</span><span class="sxs-lookup"><span data-stu-id="317d2-155">VM extensions can be added to an Azure Resource Manager template and executed with the deployment of the template.</span></span> <span data-ttu-id="317d2-156">When you deploy an extension with a template, you can create fully configured Azure deployments.</span><span class="sxs-lookup"><span data-stu-id="317d2-156">When you deploy an extension with a template, you can create fully configured Azure deployments.</span></span> <span data-ttu-id="317d2-157">For example, the following JSON is taken from a Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="317d2-157">For example, the following JSON is taken from a Resource Manager template.</span></span> <span data-ttu-id="317d2-158">The template deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span><span class="sxs-lookup"><span data-stu-id="317d2-158">The template deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="317d2-159">The VM extension takes care of the software installation.</span><span class="sxs-lookup"><span data-stu-id="317d2-159">The VM extension takes care of the software installation.</span></span>

<span data-ttu-id="317d2-160">For more information, see the full [Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="317d2-160">For more information, see the full [Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
    }
}
```

<span data-ttu-id="317d2-161">For more information, see [Authoring Azure Resource Manager templates with Linux VM extensions](../windows/extensions-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="317d2-161">For more information, see [Authoring Azure Resource Manager templates with Linux VM extensions](../windows/extensions-authoring-templates.md).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="317d2-162">Secure VM extension data</span><span class="sxs-lookup"><span data-stu-id="317d2-162">Secure VM extension data</span></span>

<span data-ttu-id="317d2-163">When you're running a VM extension, it may be necessary to include sensitive information such as credentials, storage account names, and storage account access keys.</span><span class="sxs-lookup"><span data-stu-id="317d2-163">When you're running a VM extension, it may be necessary to include sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="317d2-164">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside the target virtual machine.</span><span class="sxs-lookup"><span data-stu-id="317d2-164">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside the target virtual machine.</span></span> <span data-ttu-id="317d2-165">Each extension has a specific protected configuration schema, and each is detailed in extension-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="317d2-165">Each extension has a specific protected configuration schema, and each is detailed in extension-specific documentation.</span></span>

<span data-ttu-id="317d2-166">The following example shows an instance of the Custom Script extension for Linux.</span><span class="sxs-lookup"><span data-stu-id="317d2-166">The following example shows an instance of the Custom Script extension for Linux.</span></span> <span data-ttu-id="317d2-167">Notice that the command to execute includes a set of credentials.</span><span class="sxs-lookup"><span data-stu-id="317d2-167">Notice that the command to execute includes a set of credentials.</span></span> <span data-ttu-id="317d2-168">In this example, the command to execute will not be encrypted.</span><span class="sxs-lookup"><span data-stu-id="317d2-168">In this example, the command to execute will not be encrypted.</span></span>


```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ],
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

<span data-ttu-id="317d2-169">Moving the **command to execute** property to the **protected** configuration secures the execution string.</span><span class="sxs-lookup"><span data-stu-id="317d2-169">Moving the **command to execute** property to the **protected** configuration secures the execution string.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="317d2-170">Troubleshoot VM extensions</span><span class="sxs-lookup"><span data-stu-id="317d2-170">Troubleshoot VM extensions</span></span>

<span data-ttu-id="317d2-171">Each VM extension may have troubleshooting steps specific to the extension.</span><span class="sxs-lookup"><span data-stu-id="317d2-171">Each VM extension may have troubleshooting steps specific to the extension.</span></span> <span data-ttu-id="317d2-172">For example, when you're using the Custom Script extension, script execution details can be found locally on the virtual machine on which the extension was run.</span><span class="sxs-lookup"><span data-stu-id="317d2-172">For example, when you're using the Custom Script extension, script execution details can be found locally on the virtual machine on which the extension was run.</span></span> <span data-ttu-id="317d2-173">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="317d2-173">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="317d2-174">The following troubleshooting steps apply to all virtual machine extensions.</span><span class="sxs-lookup"><span data-stu-id="317d2-174">The following troubleshooting steps apply to all virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="317d2-175">View extension status</span><span class="sxs-lookup"><span data-stu-id="317d2-175">View extension status</span></span>

<span data-ttu-id="317d2-176">After a virtual machine extension has been run against a virtual machine, use the following Azure CLI command to return extension status.</span><span class="sxs-lookup"><span data-stu-id="317d2-176">After a virtual machine extension has been run against a virtual machine, use the following Azure CLI command to return extension status.</span></span> <span data-ttu-id="317d2-177">Replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="317d2-177">Replace example parameter names with your own values.</span></span>

```azurecli
azure vm extension get myResourceGroup myVM
```

<span data-ttu-id="317d2-178">The output looks like the following text:</span><span class="sxs-lookup"><span data-stu-id="317d2-178">The output looks like the following text:</span></span>

```azurecli
info:    Executing command vm extension get
+ Looking up the VM "myVM"
data:    Publisher                   Name             Version  State
data:    --------------------------  ---------------  -------  ---------
data:    Microsoft.Azure.Extensions  DockerExtension  1.0      Succeeded
info:    vm extension get command OK         :
```

<span data-ttu-id="317d2-179">Extension execution status can also be found in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="317d2-179">Extension execution status can also be found in the Azure portal.</span></span> <span data-ttu-id="317d2-180">To view the status of an extension, select the virtual machine, choose **Extensions**, and select the desired extension.</span><span class="sxs-lookup"><span data-stu-id="317d2-180">To view the status of an extension, select the virtual machine, choose **Extensions**, and select the desired extension.</span></span>

### <a name="rerun-a-vm-extension"></a><span data-ttu-id="317d2-181">Rerun a VM extension</span><span class="sxs-lookup"><span data-stu-id="317d2-181">Rerun a VM extension</span></span>

<span data-ttu-id="317d2-182">There may be cases in which a virtual machine extension needs to be rerun.</span><span class="sxs-lookup"><span data-stu-id="317d2-182">There may be cases in which a virtual machine extension needs to be rerun.</span></span> <span data-ttu-id="317d2-183">You can rerun an extension by removing it, and then rerunning the extension with an execution method of your choice.</span><span class="sxs-lookup"><span data-stu-id="317d2-183">You can rerun an extension by removing it, and then rerunning the extension with an execution method of your choice.</span></span> <span data-ttu-id="317d2-184">To remove an extension, run the following command with the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="317d2-184">To remove an extension, run the following command with the Azure CLI.</span></span> <span data-ttu-id="317d2-185">Replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="317d2-185">Replace example parameter names with your own values.</span></span>

```azurecli
azure vm extension set myResourceGroup myVM --uninstall CustomScript Microsoft.Azure.Extensions 2.0
```

<span data-ttu-id="317d2-186">You can remove an extension by using the following steps in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="317d2-186">You can remove an extension by using the following steps in the Azure portal:</span></span>

1. <span data-ttu-id="317d2-187">Select a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="317d2-187">Select a virtual machine.</span></span>
2. <span data-ttu-id="317d2-188">Choose **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="317d2-188">Choose **Extensions**.</span></span>
3. <span data-ttu-id="317d2-189">Select the desired extension.</span><span class="sxs-lookup"><span data-stu-id="317d2-189">Select the desired extension.</span></span>
4. <span data-ttu-id="317d2-190">Choose **Uninstall**.</span><span class="sxs-lookup"><span data-stu-id="317d2-190">Choose **Uninstall**.</span></span>

## <a name="common-vm-extension-reference"></a><span data-ttu-id="317d2-191">Common VM extension reference</span><span class="sxs-lookup"><span data-stu-id="317d2-191">Common VM extension reference</span></span>
| <span data-ttu-id="317d2-192">Extension name</span><span class="sxs-lookup"><span data-stu-id="317d2-192">Extension name</span></span> | <span data-ttu-id="317d2-193">Description</span><span class="sxs-lookup"><span data-stu-id="317d2-193">Description</span></span> | <span data-ttu-id="317d2-194">More information</span><span class="sxs-lookup"><span data-stu-id="317d2-194">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="317d2-195">Custom Script extension for Linux</span><span class="sxs-lookup"><span data-stu-id="317d2-195">Custom Script extension for Linux</span></span> |<span data-ttu-id="317d2-196">Run scripts against an Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="317d2-196">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="317d2-197">Custom Script extension for Linux</span><span class="sxs-lookup"><span data-stu-id="317d2-197">Custom Script extension for Linux</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="317d2-198">Docker extension</span><span class="sxs-lookup"><span data-stu-id="317d2-198">Docker extension</span></span> |<span data-ttu-id="317d2-199">Install the Docker daemon to support remote Docker commands.</span><span class="sxs-lookup"><span data-stu-id="317d2-199">Install the Docker daemon to support remote Docker commands.</span></span> |[<span data-ttu-id="317d2-200">Docker VM extension</span><span class="sxs-lookup"><span data-stu-id="317d2-200">Docker VM extension</span></span>](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="317d2-201">VM Access extension</span><span class="sxs-lookup"><span data-stu-id="317d2-201">VM Access extension</span></span> |<span data-ttu-id="317d2-202">Regain access to an Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="317d2-202">Regain access to an Azure virtual machine</span></span> |[<span data-ttu-id="317d2-203">VM Access extension</span><span class="sxs-lookup"><span data-stu-id="317d2-203">VM Access extension</span></span>](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| <span data-ttu-id="317d2-204">Azure Diagnostics extension</span><span class="sxs-lookup"><span data-stu-id="317d2-204">Azure Diagnostics extension</span></span> |<span data-ttu-id="317d2-205">Manage Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="317d2-205">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="317d2-206">Azure Diagnostics extension</span><span class="sxs-lookup"><span data-stu-id="317d2-206">Azure Diagnostics extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="317d2-207">Azure VM Access extension</span><span class="sxs-lookup"><span data-stu-id="317d2-207">Azure VM Access extension</span></span> |<span data-ttu-id="317d2-208">Manage users and credentials</span><span class="sxs-lookup"><span data-stu-id="317d2-208">Manage users and credentials</span></span> |[<span data-ttu-id="317d2-209">VM Access extension for Linux</span><span class="sxs-lookup"><span data-stu-id="317d2-209">VM Access extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |

