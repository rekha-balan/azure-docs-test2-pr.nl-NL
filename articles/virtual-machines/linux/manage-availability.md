---
title: Manage the availability of Linux VMs in Azure | Microsoft Docs
description: Learn how to use multiple virtual machines to ensure high availability for your Linux application in Azure
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 891c852a-84c0-4940-a61e-ada6e185bf37
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fafb5e2fba3586818a8cd8af11e60abcfde05bcd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564566"
---
# <a name="manage-the-availability-of-linux-virtual-machines"></a>Manage the availability of Linux virtual machines

Learn ways to set up and manage multiple virtual machines to ensure high availability for your Linux application in Azure. You can also [manage the availability of Windows virtual machines](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

For instructions on creating an availability set using CLI in the Resource Manager deployment model, see [azure availset: commands to manage your availability sets](../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets).

[!INCLUDE [virtual-machines-common-manage-availability](../../../includes/virtual-machines-common-manage-availability.md)]

## <a name="next-steps"></a>Next steps
To learn more about load balancing your virtual machines, see [Load Balancing virtual machines](../virtual-machines-linux-load-balance.md).
