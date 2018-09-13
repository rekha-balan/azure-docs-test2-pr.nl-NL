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
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a>Network Watcher Agent virtual machine extension for Linux

## <a name="overview"></a>Overview

[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks. The Network Watcher Agent virtual machine extension is a requirement for some of the Network Watcher features on Azure virtual machines. This includes capturing network traffic on demand and other advanced functionality.

This document details the supported platforms and deployment options for the Network Watcher Agent virtual machine extension for Linux.

## <a name="prerequisites"></a>Prerequisites

### <a name="operating-system"></a>Operating system

The Network Watcher Agent extension can be run against these Linux distributions:

| Distribution | Version |
|---|---|
| Ubuntu | 16.04 LTS, 14.04 LTS and 12.04 LTS |
| Debian | 7 and 8 |
| RedHat | 6.x and 7.x |
| Oracle Linux | 7x |
| Suse | 11 and 12 |
| OpenSuse | 7.0 |
| CentOS | 7.0 |

Note that CoreOS is not supported at this time.

### <a name="internet-connectivity"></a>Internet connectivity

Some of the Network Watcher Agent functionality requires that the target virtual machine be connected to the Internet. Without the ability to establish outgoing connections some of the Network Watcher Agent features may malfunction or become unavailable. For more details, please see the [Network Watcher documentation](https://review.docs.microsoft.com/en-us/azure/network-watcher/).

## <a name="extension-schema"></a>Extension schema

The following JSON shows the schema for the Network Watcher Agent extension. The extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.

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

### <a name="property-values"></a>Property values

| Name | Value / Example |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.Azure.NetworkWatcher |
| type | NetworkWatcherAgentLinux |
| typeHandlerVersion | 1.4 |

## <a name="template-deployment"></a>Template deployment

Azure VM extensions can be deployed with Azure Resource Manager templates. The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Network Watcher Agent extension during an Azure Resource Manager template deployment.

## <a name="azure-cli-deployment"></a>Azure CLI deployment

The Azure CLI can be used to deploy the Network Watcher Agent VM extension to an existing virtual machine.

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a>Troubleshooting and support

### <a name="troubleshooting"></a>Troubleshooting

Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure CLI. To see the deployment state of extensions for a given VM, run the following command using the Azure CLI.

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

Extension execution output is logged to files found in the following directory:

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a>Support

If you need more help at any point in this article, you can refer to the Network Watcher documentation or contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/). Alternatively, you can file an Azure support incident. Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support. For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).
