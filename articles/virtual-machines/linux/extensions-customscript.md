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
# <a name="using-the-azure-custom-script-extension-with-linux-virtual-machines"></a>Using the Azure Custom Script Extension with Linux Virtual Machines
The Custom Script Extension downloads and executes scripts on Azure virtual machines. This extension is useful for post deployment configuration, software installation, or any other configuration / management task. Scripts can be downloaded from Azure storage or other accessible internet location, or provided to the extension run time. The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.

This document details how to use the Custom Script Extension from the Azure CLI, and an Azure Resource Manager template, and also details troubleshooting steps on Linux systems.

## <a name="extension-configuration"></a>Extension Configuration
The Custom Script Extension configuration specifies things like script location and the command to be run. This configuration can be stored in configuration files, specified on the command line, or in an Azure Resource Manager template. Sensitive data can be stored in a protected configuration, which is encrypted and only decrypted inside the virtual machine. The protected configuration is useful when the execution command includes secrets such as a password.

### <a name="public-configuration"></a>Public Configuration
Schema:

* **commandToExecute**: (required, string) the entry point script to execute
* **fileUris**: (optional, string array) the URLs for files to be downloaded.
* **timestamp** (optional, integer) use this field only to trigger a rerun of the script by changing value of this field.

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a>Protected Configuration
Schema:

* **commandToExecute**: (optional, string) the entry point script to execute. Use this field instead if your command contains secrets such as passwords.
* **storageAccountName**: (optional, string) the name of storage account. If you specify storage credentials, all fileUris must be URLs for Azure Blobs.
* **storageAccountKey**: (optional, string) the access key of storage account.

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a>Azure CLI
When using the Azure CLI to run the Custom Script Extension, create a configuration file or files containing at minimum the file uri, and the script execution command.

```azurecli
azure vm extension set myResourceGroup myVM CustomScript Microsoft.Azure.Extensions 2.0 \
  --auto-upgrade-minor-version --public-config-path /script-config.json
```

Optionally, the command can be run using the `--public-config` and `--private-config` option, which allows the configuration to be specified during execution and without a separate configuration file.

```azurecli
azure vm extension set myResourceGroup myVM CustomScript Microsoft.Azure.Extensions 2.0 \
  --auto-upgrade-minor-version \
  --public-config '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

### <a name="azure-cli-examples"></a>Azure CLI Examples
**Example 1** - Public configuration with script file.

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],
  "commandToExecute": "./hello.sh"
}
```

Azure CLI command:

```azurecli
azure vm extension set myResourceGroup myVM CustomScript Microsoft.Azure.Extensions 2.0 \
  --auto-upgrade-minor-version --public-config-path /public.json
```

**Example 2** - Public configuration with no script file.

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

Azure CLI command:

```azurecli
azure vm extension set myResourceGroup myVM CustomScript Microsoft.Azure.Extensions 2.0 \
  --auto-upgrade-minor-version --public-config-path /public.json
```

**Example 3** - A public configuration file is used to specify the script file URI, and a protected configuration file is used to specify the command to be executed.

Public configuration file:

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],
}
```

Protected configuration file:  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

Azure CLI command:

```azurecli
azure vm extension set myResourceGroup myVM CustomScript Microsoft.Azure.Extensions 2.0 \
  --auto-upgrade-minor-version --public-config-path ./public.json --private-config-path ./protected.json
```

## <a name="resource-manager-template"></a>Resource Manager Template
The Azure Custom Script Extension can be run at Virtual Machine deployment time using a Resource Manager template. To do so, add properly formatted JSON to the deployment template.

### <a name="resource-manager-examples"></a>Resource Manager Examples
**Example 1** - public configuration.

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

**Example 2** - execution command in protected configuration.

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

See the .Net Core Music Store Demo for a complete example - [Music Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).

## <a name="troubleshooting"></a>Troubleshooting
When the Custom Script Extension runs, the script is created or downloaded into a directory similar to the following example. The command output is also saved into this directory in `stdout` and `stderr` file.

```bash
/var/lib/waagent/custom-script/download/0/
```

The Azure Script Extension produces a log, which can be found here.

```bash
/var/log/azure/custom-script/handler.log
```

The execution state of the Custom Script Extension can also be retrieved with the Azure CLI.

```azurecli
azure vm extension get myResourceGroup myVM
```

The output looks like the following text:

```azurecli
info:    Executing command vm extension get
+ Looking up the VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a>Next Steps
For information on other VM Script Extensions, see [Azure Script Extension overview for Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

