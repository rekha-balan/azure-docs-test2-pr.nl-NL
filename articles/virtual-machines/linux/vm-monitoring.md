---
title: Enable or Disabling Azure VM Monitoring
description: Describes How to Enable or Disable Azure VM Monitoring
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: ''
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 94108ce7f9a774337a308e1bb6da3e78caf5b5f8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551690"
---
# <a name="enable-or-disable-azure-vm-monitoring"></a>Enable or Disable Azure VM Monitoring
This section describes how to enable or disable monitoring on Virtual machines running on Azure. By default monitoring is enabled on Azure Virtual machines if deployed from the [Azure portal](https://portal.azure.com) and monitoring graphs are provided by default with a 1-minute period. You can enable or disable monitoring using the portal or Azure Command-line Interface for Mac, Linux, and Windows (the Azure CLI). 

## <a name="enable--disable-monitoring-through-the-azure-portal"></a>Enable / Disable Monitoring through the Azure Portal
You can enable  monitoring of your Azure VM, which provides data about your instance in 1-minute periods. (storage changes apply). Detailed diagnostics data is then available for the VM in the portal graphs or through the API. By default, Azure portal enables monitoring, but you can turn it off as described below. You can enable monitoring while the VM is running or in stopped state.

* Open the Azure portal at **[https://portal.azure.com](https://portal.azure.com)**
* In the left navigation, click Virtual machines.
* In the list Virtual machines, select a running or stopped instance. Virtual machine blad will open.
* Click "All settings".
* Click "Diagnostics".
* Change status to On or Off. You can also pick in this blade the level of monitoring details you would like to enable for your virtual machine.

[Azure.Note] The Diagnostics On switch is the default when you create a new virtual machine

![Enable / Disable Monitoring through the Azure Portal.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a>Enable / Disable Monitoring with Azure CLI
To enable monitoring for an Azure VM.

* Create a file named such as PrivateConfig.json with the following content.
        { "storageAccountName":"the storage account to receive data", "storageAccountKey":"the key of the account" }
* Run the following Azure CLI command.
  
        azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.0 --private-config-path PrivateConfig.json

[Azure.Note] You can change from version 2.0 to a later version when available. 

For more details about configuring monitoring metrics and samples, visit the document - **[Using Linux Diagnostic Extension to Monitor Linux VM’s performance and diagnostic data](classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/vm-monitoring/portal-enable-disable.png



