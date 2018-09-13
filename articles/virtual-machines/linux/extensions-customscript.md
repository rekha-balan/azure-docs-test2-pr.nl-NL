---
title: Run custom scripts on Linux VMs in Azure | Microsoft Docs
description: Automate Linux VM configuration tasks by using the Custom Script Extension
services: virtual-machines-linux
documentationcenter: ''
author: neilpeterson
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: cf17ab2b-8d7e-4078-b6df-955c6d5071c2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/22/2016
ms.author: nepeters
ms.openlocfilehash: d5e4f7cd1650373b8edd27ad64a2677fc5be8e68
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554476"
---
# <a name="using-the-azure-custom-script-extension-with-linux-virtual-machines"></a><span data-ttu-id="f018e-103">Using the Azure Custom Script Extension with Linux Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="f018e-103">Using the Azure Custom Script Extension with Linux Virtual Machines</span></span>
<span data-ttu-id="f018e-104">The Custom Script Extension downloads and executes scripts on Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="f018e-104">The Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="f018e-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span><span class="sxs-lookup"><span data-stu-id="f018e-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="f018e-106">Scripts can be downloaded from Azure storage or other accessible internet location, or provided to the extension run time.</span><span class="sxs-lookup"><span data-stu-id="f018e-106">Scripts can be downloaded from Azure storage or other accessible internet location, or provided to the extension run time.</span></span> <span data-ttu-id="f018e-107">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span><span class="sxs-lookup"><span data-stu-id="f018e-107">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="f018e-108">This document details how to use the Custom Script Extension from the Azure CLI, and an Azure Resource Manager template, and also details troubleshooting steps on Linux systems.</span><span class="sxs-lookup"><span data-stu-id="f018e-108">This document details how to use the Custom Script Extension from the Azure CLI, and an Azure Resource Manager template, and also details troubleshooting steps on Linux systems.</span></span>

## <a name="extension-configuration"></a><span data-ttu-id="f018e-109">Extension Configuration</span><span class="sxs-lookup"><span data-stu-id="f018e-109">Extension Configuration</span></span>
<span data-ttu-id="f018e-110">The Custom Script Extension configuration specifies things like script location and the command to be run.</span><span class="sxs-lookup"><span data-stu-id="f018e-110">The Custom Script Extension configuration specifies things like script location and the command to be run.</span></span> <span data-ttu-id="f018e-111">This configuration can be stored in configuration files, specified on the command line, or in an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="f018e-111">This configuration can be stored in configuration files, specified on the command line, or in an Azure Resource Manager template.</span></span> <span data-ttu-id="f018e-112">Sensitive data can be stored in a protected configuration, which is encrypted and only decrypted inside the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f018e-112">Sensitive data can be stored in a protected configuration, which is encrypted and only decrypted inside the virtual machine.</span></span> <span data-ttu-id="f018e-113">The protected configuration is useful when the execution command includes secrets such as a password.</span><span class="sxs-lookup"><span data-stu-id="f018e-113">The protected configuration is useful when the execution command includes secrets such as a password.</span></span>

### <a name="public-configuration"></a><span data-ttu-id="f018e-114">Public Configuration</span><span class="sxs-lookup"><span data-stu-id="f018e-114">Public Configuration</span></span>
<span data-ttu-id="f018e-115">Schema:</span><span class="sxs-lookup"><span data-stu-id="f018e-115">Schema:</span></span>

* <span data-ttu-id="f018e-116">**commandToExecute**: (required, string) the entry point script to execute</span><span class="sxs-lookup"><span data-stu-id="f018e-116">**commandToExecute**: (required, string) the entry point script to execute</span></span>
* <span data-ttu-id="f018e-117">**fileUris**: (optional, string array) the URLs for files to be downloaded.</span><span class="sxs-lookup"><span data-stu-id="f018e-117">**fileUris**: (optional, string array) the URLs for files to be downloaded.</span></span>
* <span data-ttu-id="f018e-118">**timestamp** (optional, integer) use this field only to trigger a rerun of the script by changing value of this field.</span><span class="sxs-lookup"><span data-stu-id="f018e-118">**timestamp** (optional, integer) use this field only to trigger a rerun of the script by changing value of this field.</span></span>

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a><span data-ttu-id="f018e-119">Protected Configuration</span><span class="sxs-lookup"><span data-stu-id="f018e-119">Protected Configuration</span></span>
<span data-ttu-id="f018e-120">Schema:</span><span class="sxs-lookup"><span data-stu-id="f018e-120">Schema:</span></span>

* <span data-ttu-id="f018e-121">**commandToExecute**: (optional, string) the entry point script to execute.</span><span class="sxs-lookup"><span data-stu-id="f018e-121">**commandToExecute**: (optional, string) the entry point script to execute.</span></span> <span data-ttu-id="f018e-122">Use this field instead if your command contains secrets such as passwords.</span><span class="sxs-lookup"><span data-stu-id="f018e-122">Use this field instead if your command contains secrets such as passwords.</span></span>
* <span data-ttu-id="f018e-123">**storageAccountName**: (optional, string) the name of storage account.</span><span class="sxs-lookup"><span data-stu-id="f018e-123">**storageAccountName**: (optional, string) the name of storage account.</span></span> <span data-ttu-id="f018e-124">If you specify storage credentials, all fileUris must be URLs for Azure Blobs.</span><span class="sxs-lookup"><span data-stu-id="f018e-124">If you specify storage credentials, all fileUris must be URLs for Azure Blobs.</span></span>
* <span data-ttu-id="f018e-125">**storageAccountKey**: (optional, string) the access key of storage account.</span><span class="sxs-lookup"><span data-stu-id="f018e-125">**storageAccountKey**: (optional, string) the access key of storage account.</span></span>

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a><span data-ttu-id="f018e-126">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f018e-126">Azure CLI</span></span>
<span data-ttu-id="f018e-127">When using the Azure CLI to run the Custom Script Extension, create a configuration file or files containing at minimum the file uri, and the script execution command.</span><span class="sxs-lookup"><span data-stu-id="f018e-127">When using the Azure CLI to run the Custom Script Extension, create a configuration file or files containing at minimum the file uri, and the script execution command.</span></span>

```azurecli
azure vm extension set myResourceGroup myVM CustomScript Microsoft.Azure.Extensions 2.0 \
  --auto-upgrade-minor-version --public-config-path /script-config.json
```

<span data-ttu-id="f018e-128">Optionally, the command can be run using the `--public-config` and `--private-config` option, which allows the configuration to be specified during execution and without a separate configuration file.</span><span class="sxs-lookup"><span data-stu-id="f018e-128">Optionally, the command can be run using the `--public-config` and `--private-config` option, which allows the configuration to be specified during execution and without a separate configuration file.</span></span>

```azurecli
azure vm extension set myResourceGroup myVM CustomScript Microsoft.Azure.Extensions 2.0 \
  --auto-upgrade-minor-version \
  --public-config '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

### <a name="azure-cli-examples"></a><span data-ttu-id="f018e-129">Azure CLI Examples</span><span class="sxs-lookup"><span data-stu-id="f018e-129">Azure CLI Examples</span></span>
<span data-ttu-id="f018e-130">**Example 1** - Public configuration with script file.</span><span class="sxs-lookup"><span data-stu-id="f018e-130">**Example 1** - Public configuration with script file.</span></span>

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],
  "commandToExecute": "./hello.sh"
}
```

<span data-ttu-id="f018e-131">Azure CLI command:</span><span class="sxs-lookup"><span data-stu-id="f018e-131">Azure CLI command:</span></span>

```azurecli
azure vm extension set myResourceGroup myVM CustomScript Microsoft.Azure.Extensions 2.0 \
  --auto-upgrade-minor-version --public-config-path /public.json
```

<span data-ttu-id="f018e-132">**Example 2** - Public configuration with no script file.</span><span class="sxs-lookup"><span data-stu-id="f018e-132">**Example 2** - Public configuration with no script file.</span></span>

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

<span data-ttu-id="f018e-133">Azure CLI command:</span><span class="sxs-lookup"><span data-stu-id="f018e-133">Azure CLI command:</span></span>

```azurecli
azure vm extension set myResourceGroup myVM CustomScript Microsoft.Azure.Extensions 2.0 \
  --auto-upgrade-minor-version --public-config-path /public.json
```

<span data-ttu-id="f018e-134">**Example 3** - A public configuration file is used to specify the script file URI, and a protected configuration file is used to specify the command to be executed.</span><span class="sxs-lookup"><span data-stu-id="f018e-134">**Example 3** - A public configuration file is used to specify the script file URI, and a protected configuration file is used to specify the command to be executed.</span></span>

<span data-ttu-id="f018e-135">Public configuration file:</span><span class="sxs-lookup"><span data-stu-id="f018e-135">Public configuration file:</span></span>

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],
}
```

<span data-ttu-id="f018e-136">Protected configuration file:</span><span class="sxs-lookup"><span data-stu-id="f018e-136">Protected configuration file:</span></span>  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

<span data-ttu-id="f018e-137">Azure CLI command:</span><span class="sxs-lookup"><span data-stu-id="f018e-137">Azure CLI command:</span></span>

```azurecli
azure vm extension set myResourceGroup myVM CustomScript Microsoft.Azure.Extensions 2.0 \
  --auto-upgrade-minor-version --public-config-path ./public.json --private-config-path ./protected.json
```

## <a name="resource-manager-template"></a><span data-ttu-id="f018e-138">Resource Manager Template</span><span class="sxs-lookup"><span data-stu-id="f018e-138">Resource Manager Template</span></span>
<span data-ttu-id="f018e-139">The Azure Custom Script Extension can be run at Virtual Machine deployment time using a Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="f018e-139">The Azure Custom Script Extension can be run at Virtual Machine deployment time using a Resource Manager template.</span></span> <span data-ttu-id="f018e-140">To do so, add properly formatted JSON to the deployment template.</span><span class="sxs-lookup"><span data-stu-id="f018e-140">To do so, add properly formatted JSON to the deployment template.</span></span>

### <a name="resource-manager-examples"></a><span data-ttu-id="f018e-141">Resource Manager Examples</span><span class="sxs-lookup"><span data-stu-id="f018e-141">Resource Manager Examples</span></span>
<span data-ttu-id="f018e-142">**Example 1** - public configuration.</span><span class="sxs-lookup"><span data-stu-id="f018e-142">**Example 1** - public configuration.</span></span>

```json
{
    "name": "scriptextensiondemo",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-15",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', parameters('scriptextensiondemoName'))]"
    ],
    "tags": {
        "displayName": "scriptextensiondemo"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
      "settings": {
        "fileUris": [
          "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
        ],
        "commandToExecute": "sh hello.sh"
      }
    }
}
```

<span data-ttu-id="f018e-143">**Example 2** - execution command in protected configuration.</span><span class="sxs-lookup"><span data-stu-id="f018e-143">**Example 2** - execution command in protected configuration.</span></span>

```json
{
  "name": "config-app",
  "type": "extensions",
  "location": "[resourceGroup().location]",
  "apiVersion": "2015-06-15",
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
        "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
      ]              
    },
    "protectedSettings": {
      "commandToExecute": "sh hello.sh <password>"
    }
  }
}
```

<span data-ttu-id="f018e-144">See the .Net Core Music Store Demo for a complete example - [Music Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span><span class="sxs-lookup"><span data-stu-id="f018e-144">See the .Net Core Music Store Demo for a complete example - [Music Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f018e-145">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="f018e-145">Troubleshooting</span></span>
<span data-ttu-id="f018e-146">When the Custom Script Extension runs, the script is created or downloaded into a directory similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="f018e-146">When the Custom Script Extension runs, the script is created or downloaded into a directory similar to the following example.</span></span> <span data-ttu-id="f018e-147">The command output is also saved into this directory in `stdout` and `stderr` file.</span><span class="sxs-lookup"><span data-stu-id="f018e-147">The command output is also saved into this directory in `stdout` and `stderr` file.</span></span>

```bash
/var/lib/waagent/custom-script/download/0/
```

<span data-ttu-id="f018e-148">The Azure Script Extension produces a log, which can be found here.</span><span class="sxs-lookup"><span data-stu-id="f018e-148">The Azure Script Extension produces a log, which can be found here.</span></span>

```bash
/var/log/azure/custom-script/handler.log
```

<span data-ttu-id="f018e-149">The execution state of the Custom Script Extension can also be retrieved with the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f018e-149">The execution state of the Custom Script Extension can also be retrieved with the Azure CLI.</span></span>

```azurecli
azure vm extension get myResourceGroup myVM
```

<span data-ttu-id="f018e-150">The output looks like the following text:</span><span class="sxs-lookup"><span data-stu-id="f018e-150">The output looks like the following text:</span></span>

```azurecli
info:    Executing command vm extension get
+ Looking up the VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a><span data-ttu-id="f018e-151">Next Steps</span><span class="sxs-lookup"><span data-stu-id="f018e-151">Next Steps</span></span>
<span data-ttu-id="f018e-152">For information on other VM Script Extensions, see [Azure Script Extension overview for Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f018e-152">For information on other VM Script Extensions, see [Azure Script Extension overview for Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

