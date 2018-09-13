---
title: Authoring templates with Linux VM extensions | Microsoft Docs
description: Learn about authoring Azure Resource Manager templates with extensions for Linux VMs
services: virtual-machines-linux
documentationcenter: ''
author: kundanap
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 322f8f0b-6697-4acb-b5f3-b3f58d28358b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 5d12f470fc7313664ca0b44e8b1168422ceb494a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553356"
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a><span data-ttu-id="9c3d4-103">Authoring Azure Resource Manager templates with Linux VM extensions</span><span class="sxs-lookup"><span data-stu-id="9c3d4-103">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="9c3d4-104">From Azure CLI, run the following commnad:</span><span class="sxs-lookup"><span data-stu-id="9c3d4-104">From Azure CLI, run the following commnad:</span></span>

      Azure VM extension list

<span data-ttu-id="9c3d4-105">This command returns the publisher name, extension name and version as following:</span><span class="sxs-lookup"><span data-stu-id="9c3d4-105">This command returns the publisher name, extension name and version as following:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="9c3d4-106">These three properties map to "publisher", "type", and "typeHandlerVersion" respectively in the above template snippet.</span><span class="sxs-lookup"><span data-stu-id="9c3d4-106">These three properties map to "publisher", "type", and "typeHandlerVersion" respectively in the above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="9c3d4-107">It's always recommended to use the latest extension version to get the most updated functionality.</span><span class="sxs-lookup"><span data-stu-id="9c3d4-107">It's always recommended to use the latest extension version to get the most updated functionality.</span></span>
> 
> 

## <a name="identifying-the-schema-for-the-extension-configuration-parameters"></a><span data-ttu-id="9c3d4-108">Identifying the schema for the extension configuration parameters</span><span class="sxs-lookup"><span data-stu-id="9c3d4-108">Identifying the schema for the extension configuration parameters</span></span>
<span data-ttu-id="9c3d4-109">The next step with authoring an extension template is to identify the format for providing configuration parameters.</span><span class="sxs-lookup"><span data-stu-id="9c3d4-109">The next step with authoring an extension template is to identify the format for providing configuration parameters.</span></span> <span data-ttu-id="9c3d4-110">Each extension supports its own set of parameters.</span><span class="sxs-lookup"><span data-stu-id="9c3d4-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="9c3d4-111">To look at sample configurations for Linux extensions, click the documentation for see [Linux eExtensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9c3d4-111">To look at sample configurations for Linux extensions, click the documentation for see [Linux eExtensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="9c3d4-112">Please refer to the following to get a fully complete template with VM Extensions.</span><span class="sxs-lookup"><span data-stu-id="9c3d4-112">Please refer to the following to get a fully complete template with VM Extensions.</span></span>

[<span data-ttu-id="9c3d4-113">Custom script extension on a Linux VM</span><span class="sxs-lookup"><span data-stu-id="9c3d4-113">Custom script extension on a Linux VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

<span data-ttu-id="9c3d4-114">After authoring the template, you can deploy it using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="9c3d4-114">After authoring the template, you can deploy it using the Azure CLI.</span></span>

