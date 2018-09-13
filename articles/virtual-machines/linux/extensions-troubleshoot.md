---
title: Troubleshooting Linux VM extension failures | Microsoft Docs
description: Learn about troubleshooting Azure Linux VM extension failures
services: virtual-machines-linux
documentationcenter: ''
author: kundanap
manager: timlt
editor: ''
tags: top-support-issue,azure-resource-manager
ms.assetid: f05d93f3-42fc-4a09-9798-d92f7929c417
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 371305db545783dd3b1ecbde39943cd87274034c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549119"
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a>Troubleshooting Azure Linux VM extension failures
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>Viewing extension status
Azure Resource Manager templates can be executed from the  Azure CLI. Once the template is executed, the extension status can be viewed from Azure Resource Explorer or the command line tools.

Here is an example:

Azure CLI:

      azure vm get-instance-view


Here is the sample output:

      Extensions:  {
      "ExtensionType": "Microsoft.Compute.CustomScriptExtension",
      "Name": "myCustomScriptExtension",
      "SubStatuses": [
        {
          "Code": "ComponentStatus/StdOut/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "    Directory: C:\\temp\\n\\n\\nMode                LastWriteTime     Length Name
              \\n----                -------------     ------ ----                              \\n-a---          9/1/2015   2:03 AM         11
              test.txt                          \\n\\n",
                      "Time": null
          },
        {
          "Code": "ComponentStatus/StdErr/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "",
          "Time": null
        }
    }
  ]

## <a name="troubleshooting-extenson-failures"></a>Troubleshooting Extenson failures:
### <a name="re-running-the-extension-on-the-vm"></a>Re-running the extension on the VM
If you are running scripts on the VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but the script has failed. Under these conditons, the recommended way to recover from this error is to remove the extension and rerun the template again.
Note: In future, this functionality would be enhanced to remove the need for uninstalling the extension.

#### <a name="remove-the-extension-from-azure-cli"></a>Remove the extension from Azure CLI
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

Where "publsher-name" corresponds to the extension type from the output of "azure vm get-instance-view" and name is the name of the extension resource from the template

Once the extension has been removed, the template can be re-executed to run the scripts on the VM.

