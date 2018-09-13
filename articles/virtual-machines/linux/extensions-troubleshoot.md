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
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a><span data-ttu-id="6fbeb-103">Troubleshooting Azure Linux VM extension failures</span><span class="sxs-lookup"><span data-stu-id="6fbeb-103">Troubleshooting Azure Linux VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="6fbeb-104">Viewing extension status</span><span class="sxs-lookup"><span data-stu-id="6fbeb-104">Viewing extension status</span></span>
<span data-ttu-id="6fbeb-105">Azure Resource Manager templates can be executed from the  Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="6fbeb-105">Azure Resource Manager templates can be executed from the  Azure CLI.</span></span> <span data-ttu-id="6fbeb-106">Once the template is executed, the extension status can be viewed from Azure Resource Explorer or the command line tools.</span><span class="sxs-lookup"><span data-stu-id="6fbeb-106">Once the template is executed, the extension status can be viewed from Azure Resource Explorer or the command line tools.</span></span>

<span data-ttu-id="6fbeb-107">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="6fbeb-107">Here is an example:</span></span>

<span data-ttu-id="6fbeb-108">Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="6fbeb-108">Azure CLI:</span></span>

      azure vm get-instance-view


<span data-ttu-id="6fbeb-109">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="6fbeb-109">Here is the sample output:</span></span>

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
  <span data-ttu-id="6fbeb-110">]</span><span class="sxs-lookup"><span data-stu-id="6fbeb-110">]</span></span>

## <a name="troubleshooting-extenson-failures"></a><span data-ttu-id="6fbeb-111">Troubleshooting Extenson failures:</span><span class="sxs-lookup"><span data-stu-id="6fbeb-111">Troubleshooting Extenson failures:</span></span>
### <a name="re-running-the-extension-on-the-vm"></a><span data-ttu-id="6fbeb-112">Re-running the extension on the VM</span><span class="sxs-lookup"><span data-stu-id="6fbeb-112">Re-running the extension on the VM</span></span>
<span data-ttu-id="6fbeb-113">If you are running scripts on the VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but the script has failed.</span><span class="sxs-lookup"><span data-stu-id="6fbeb-113">If you are running scripts on the VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but the script has failed.</span></span> <span data-ttu-id="6fbeb-114">Under these conditons, the recommended way to recover from this error is to remove the extension and rerun the template again.</span><span class="sxs-lookup"><span data-stu-id="6fbeb-114">Under these conditons, the recommended way to recover from this error is to remove the extension and rerun the template again.</span></span>
<span data-ttu-id="6fbeb-115">Note: In future, this functionality would be enhanced to remove the need for uninstalling the extension.</span><span class="sxs-lookup"><span data-stu-id="6fbeb-115">Note: In future, this functionality would be enhanced to remove the need for uninstalling the extension.</span></span>

#### <a name="remove-the-extension-from-azure-cli"></a><span data-ttu-id="6fbeb-116">Remove the extension from Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6fbeb-116">Remove the extension from Azure CLI</span></span>
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

<span data-ttu-id="6fbeb-117">Where "publsher-name" corresponds to the extension type from the output of "azure vm get-instance-view" and name is the name of the extension resource from the template</span><span class="sxs-lookup"><span data-stu-id="6fbeb-117">Where "publsher-name" corresponds to the extension type from the output of "azure vm get-instance-view" and name is the name of the extension resource from the template</span></span>

<span data-ttu-id="6fbeb-118">Once the extension has been removed, the template can be re-executed to run the scripts on the VM.</span><span class="sxs-lookup"><span data-stu-id="6fbeb-118">Once the extension has been removed, the template can be re-executed to run the scripts on the VM.</span></span>

