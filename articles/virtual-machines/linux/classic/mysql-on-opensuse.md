---
title: Install MySQL on an OpenSUSE VM | Microsoft Docs
description: Learn to install MySQL on an OpenSUSE Linux VMirtual machine in Azure.
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: 1594e10e-c314-455a-9efb-a89441de364b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/19/2016
ms.author: cynthn
ms.openlocfilehash: 01b798a25575b66f89057315ce80d6cc0cde53b5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554280"
---
# <a name="install-mysql-on-a-virtual-machine-running-opensuse-linux-in-azure"></a><span data-ttu-id="62817-103">Install MySQL on a virtual machine running OpenSUSE Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="62817-103">Install MySQL on a virtual machine running OpenSUSE Linux in Azure</span></span>
<span data-ttu-id="62817-104">[MySQL][MySQL] is a popular, open-source SQL database.</span><span class="sxs-lookup"><span data-stu-id="62817-104">[MySQL][MySQL] is a popular, open-source SQL database.</span></span> <span data-ttu-id="62817-105">This tutorial shows you how to create a virtual machine running OpenSUSE Linux, then install MySQL.</span><span class="sxs-lookup"><span data-stu-id="62817-105">This tutorial shows you how to create a virtual machine running OpenSUSE Linux, then install MySQL.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="62817-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="62817-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="62817-107">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="62817-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="62817-108">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="62817-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<br>

## <a name="create-a-virtual-machine-running-opensuse-linux"></a><span data-ttu-id="62817-109">Create a virtual machine running OpenSUSE Linux</span><span class="sxs-lookup"><span data-stu-id="62817-109">Create a virtual machine running OpenSUSE Linux</span></span>
[!INCLUDE [create-and-configure-opensuse-vm-in-portal](../../../../includes/create-and-configure-opensuse-vm-in-portal.md)]

## <a name="install-and-run-mysql-on-the-virtual-machine"></a><span data-ttu-id="62817-110">Install and run MySQL on the virtual machine</span><span class="sxs-lookup"><span data-stu-id="62817-110">Install and run MySQL on the virtual machine</span></span>
[!INCLUDE [install-and-run-mysql-on-opensuse-vm](../../../../includes/install-and-run-mysql-on-opensuse-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="62817-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="62817-111">Next steps</span></span>
<span data-ttu-id="62817-112">For details about MySQL, see the [MySQL Documentation][MySQLDocs].</span><span class="sxs-lookup"><span data-stu-id="62817-112">For details about MySQL, see the [MySQL Documentation][MySQLDocs].</span></span>

[MySQLDocs]:http://dev.mysql.com/doc/index-topic.html
[MySQL]:http://www.mysql.com

