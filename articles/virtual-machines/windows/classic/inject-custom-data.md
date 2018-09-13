---
title: Inject data into Windows VMs on Azure | Microsoft Docs
description: This topic describes how to inject custom data into an Azure virtual machine when the instance is created and how to locate the custom data on either Windows or Linux.
services: virtual-machines-windows
documentationcenter: ''
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 48759f76-eaa0-4202-ada0-706d3f9a9467
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 81939d1812a12cf01b3859c14ff849293ea1ba04
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552974"
---
# <a name="injecting-custom-data-into-an-azure-virtual-machine"></a><span data-ttu-id="0ca74-103">Injecting custom data into an Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="0ca74-103">Injecting custom data into an Azure virtual machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="0ca74-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0ca74-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0ca74-105">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="0ca74-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="0ca74-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="0ca74-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="0ca74-107">For information about using the Custom Script Extension with the Resource Manager model, see [here](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0ca74-107">For information about using the Custom Script Extension with the Resource Manager model, see [here](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-inject-custom-data](../../../../includes/virtual-machines-common-classic-inject-custom-data.md)]

