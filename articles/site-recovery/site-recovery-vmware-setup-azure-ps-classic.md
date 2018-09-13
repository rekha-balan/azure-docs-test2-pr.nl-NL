---
title: " Manage a Process Server running in Azure(Classic) | Microsoft Docs"
description: This article describes how to set up a failback Process Server(Classic) In Azure.
services: site-recovery
documentationcenter: ''
author: AnoopVasudavan
manager: gauravd
editor: ''
ms.assetid: ''
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 2/2/2017
ms.author: anoopkv
ms.openlocfilehash: f22fe8101dfbd82660e7e07c85ffdf34581f2b9a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670721"
---
# <a name="manage-a-process-server-running-in-azure-classic"></a>Manage a Process Server running in Azure (Classic)
> [!div class="op_single_selector"]
> * [Azure Classic ](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [Resource Manager](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

During failback, it is recommended to deploy Process Server in Azure if there is high latency between the Azure Virtual Network and your on-premises network. This article describes how you can set up, configure, and manage the process servers running in Azure.

> [!NOTE]
> This article is to be used if you used **Resource Manager** as the deployment model for the virtual machines during failover. If you used **Classic** as the deployment model follow the steps in [How to set up & configure a Failback Process Server (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

## <a name="prerequisites"></a>Prerequisites

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a>Deploy a Process Server on Azure

1. In Azure Marketplace, create a virtual machine using the **Microsoft Azure Site Recovery Process Server V2** </br>
    ![Marketplace_image_1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)
2. Ensure that you select the deployment model as **Classic** </br>
  ![Marketplace_image_2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)
3. In the Create virtual machine wizard > Basic Settings, ensure you select the Subscription and Location to where you failed over the virtual machines.</br>
  ![create_image_1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)
4. Ensure that the virtual machine is connected to the Azure Virtual Network to which the failed over virtual machine is connected.</br>
  ![create_image_2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)
5. Once the Process Server virtual machine is provisioned, you need to log in and register it with the Configuration Server.

> [!NOTE]
> To be able to use this Process Server for failback, you need to register it with the on-premises configuration server.

## <a name="registering-the-process-server-running-in-azure-to-a-configuration-server-running-on-premises"></a>Registering the Process Server (running in Azure) to a Configuration Server (running on-premises)

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-the-process-server-to-latest-version"></a>Upgrading the Process Server to latest version.

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-the-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a>Unregistering the Process Server (running in Azure) from a Configuration Server (running on-premises)

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]




