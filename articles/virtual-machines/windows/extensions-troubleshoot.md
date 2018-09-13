---
title: Troubleshooting Windows VM extension failures | Microsoft Docs
description: Learn about troubleshooting Azure Windows VM extension failures
services: virtual-machines-windows
documentationcenter: ''
author: kundanap
manager: timlt
editor: ''
tags: top-support-issue,azure-resource-manager
ms.assetid: 878ab9b6-c3e6-40be-82d4-d77fecd5030f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 62bbf17a9cd134830f5607633eff9a02c3335887
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552756"
---
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a><span data-ttu-id="83661-103">Troubleshooting Azure Windows VM extension failures</span><span class="sxs-lookup"><span data-stu-id="83661-103">Troubleshooting Azure Windows VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="83661-104">Viewing extension status</span><span class="sxs-lookup"><span data-stu-id="83661-104">Viewing extension status</span></span>
<span data-ttu-id="83661-105">Azure Resource Manager templates can be executed from Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83661-105">Azure Resource Manager templates can be executed from Azure PowerShell.</span></span> <span data-ttu-id="83661-106">Once the template is executed, the extension status can be viewed from Azure Resource Explorer or the command line tools.</span><span class="sxs-lookup"><span data-stu-id="83661-106">Once the template is executed, the extension status can be viewed from Azure Resource Explorer or the command line tools.</span></span>

<span data-ttu-id="83661-107">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="83661-107">Here is an example:</span></span>

<span data-ttu-id="83661-108">Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="83661-108">Azure PowerShell:</span></span>

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

<span data-ttu-id="83661-109">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="83661-109">Here is the sample output:</span></span>

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
  <span data-ttu-id="83661-110">]</span><span class="sxs-lookup"><span data-stu-id="83661-110">]</span></span>

## <a name="troubleshooting-extension-failures"></a><span data-ttu-id="83661-111">Troubleshooting extension failures</span><span class="sxs-lookup"><span data-stu-id="83661-111">Troubleshooting extension failures</span></span>
### <a name="re-running-the-extension-on-the-vm"></a><span data-ttu-id="83661-112">Re-running the extension on the VM</span><span class="sxs-lookup"><span data-stu-id="83661-112">Re-running the extension on the VM</span></span>
<span data-ttu-id="83661-113">If you are running scripts on the VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but the script has failed.</span><span class="sxs-lookup"><span data-stu-id="83661-113">If you are running scripts on the VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but the script has failed.</span></span> <span data-ttu-id="83661-114">Under these conditons, the recommended way to recover from this error is to remove the extension and rerun the template again.</span><span class="sxs-lookup"><span data-stu-id="83661-114">Under these conditons, the recommended way to recover from this error is to remove the extension and rerun the template again.</span></span>
<span data-ttu-id="83661-115">Note: In future, this functionality would be enhanced to remove the need for uninstalling the extension.</span><span class="sxs-lookup"><span data-stu-id="83661-115">Note: In future, this functionality would be enhanced to remove the need for uninstalling the extension.</span></span>

#### <a name="remove-the-extension-from-azure-powershell"></a><span data-ttu-id="83661-116">Remove the extension from Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="83661-116">Remove the extension from Azure PowerShell</span></span>
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

<span data-ttu-id="83661-117">Once the extension has been removed, the template can be re-executed to run the scripts on the VM.</span><span class="sxs-lookup"><span data-stu-id="83661-117">Once the extension has been removed, the template can be re-executed to run the scripts on the VM.</span></span>

