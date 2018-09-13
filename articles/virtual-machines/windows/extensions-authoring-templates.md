---
title: Authoring Templates with Windows VM extensions | Microsoft Docs
description: Learn about authoring Azure Resource Manager templates with extensions for Windows VMs
services: virtual-machines-windows
documentationcenter: ''
author: kundanap
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 418dd1f7-ded8-45ab-9a5a-a59d245e2555
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 95a2411649ce786aed6a2b7b72df37075855ae34
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660587"
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a><span data-ttu-id="cb7fa-103">Authoring Azure Resource Manager templates with Windows VM extensions</span><span class="sxs-lookup"><span data-stu-id="cb7fa-103">Authoring Azure Resource Manager templates with Windows VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="cb7fa-104">From Azure PowerShell, run the following Azure PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="cb7fa-104">From Azure PowerShell, run the following Azure PowerShell cmdlet:</span></span>

      Get-AzureVMAvailableExtension


<span data-ttu-id="cb7fa-105">This cmdlet returns the publisher name, extension name, and version as follows:</span><span class="sxs-lookup"><span data-stu-id="cb7fa-105">This cmdlet returns the publisher name, extension name, and version as follows:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="cb7fa-106">These three properties map to "publisher", "type", and "typeHandlerVersion" respectively in the above template snippet.</span><span class="sxs-lookup"><span data-stu-id="cb7fa-106">These three properties map to "publisher", "type", and "typeHandlerVersion" respectively in the above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="cb7fa-107">It's always recommended to use the latest extension version to get the most updated functionality.</span><span class="sxs-lookup"><span data-stu-id="cb7fa-107">It's always recommended to use the latest extension version to get the most updated functionality.</span></span>
> 
> 

## <a name="identifying-the-schema-for-the-extension-configuration-parameters"></a><span data-ttu-id="cb7fa-108">Identifying the schema for the extension configuration parameters</span><span class="sxs-lookup"><span data-stu-id="cb7fa-108">Identifying the schema for the extension configuration parameters</span></span>
<span data-ttu-id="cb7fa-109">The next step with authoring an extension template is to identify the format for providing configuration parameters.</span><span class="sxs-lookup"><span data-stu-id="cb7fa-109">The next step with authoring an extension template is to identify the format for providing configuration parameters.</span></span> <span data-ttu-id="cb7fa-110">Each extension supports its own set of parameters.</span><span class="sxs-lookup"><span data-stu-id="cb7fa-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="cb7fa-111">To look at sample configurations for Windows extensions, see [Windows extensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cb7fa-111">To look at sample configurations for Windows extensions, see [Windows extensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="cb7fa-112">Please refer to the following to get a fully complete template with VM extensions.</span><span class="sxs-lookup"><span data-stu-id="cb7fa-112">Please refer to the following to get a fully complete template with VM extensions.</span></span>

[<span data-ttu-id="cb7fa-113">Custom Script Extension on a Windows VM</span><span class="sxs-lookup"><span data-stu-id="cb7fa-113">Custom Script Extension on a Windows VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

<span data-ttu-id="cb7fa-114">After authoring the template, you can deploy it using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cb7fa-114">After authoring the template, you can deploy it using Azure PowerShell.</span></span>

