---
title: How to configure a cloud service (portal) | Microsoft Docs
description: Learn how to configure cloud services in Azure. Learn to update the cloud service configuration and configure remote access to role instances. These examples use the Azure portal.
services: cloud-services
documentationcenter: ''
author: Thraka
manager: timlt
editor: ''
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: 457c7902720187d6b6e0f32048fe86a757234ce1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552470"
---
# <a name="how-to-configure-cloud-services"></a>How to Configure Cloud Services
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-how-to-configure-portal.md)
> * [Azure classic portal](cloud-services-how-to-configure.md)
>
>

You can configure the most commonly used settings for a cloud service in the Azure portal. Or, if you like to update your configuration files directly, download a service configuration file to update, and then upload the updated file and update the cloud service with the configuration changes. Either way, the configuration updates are pushed out to all role instances.

You can also manage the instances of your cloud service roles, or remote desktop into them.

Azure can only ensure 99.95 percent service availability during the configuration updates if you have at least two role instances for every role. That enables one virtual machine to process client requests while the other is being updated. For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).

## <a name="change-a-cloud-service"></a>Change a cloud service
After opening the [Azure portal](https://portal.azure.com/), navigate to your cloud service. From here, you manage many aspects of it.

![Settings Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cloud-service.png)

The **Settings** or **All settings** links will open up the **Settings** blade where you can change the **Properties**, change the **Configuration**, manage the **Certificates**, setup **Alert rules**, and manage the **Users** who have access to this cloud service.

![Azure cloud service settings blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a>Manage Guest OS version

By default, Azure periodically updates your guest OS to the latest supported image within the OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.

If you need to target a specific OS version, you can set it in the **Configuration** blade.

![Set OS version](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> Choosing a specific OS version disables automatic OS updates and makes patching your responsibility. You must ensure that your role instances are receiving updates or you may expose your application to security vulnerabilities.

## <a name="monitoring"></a>Monitoring
You can add alerts to your cloud service. Click **Settings** > **Alert Rules** > **Add alert**.

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cs-alerts.png)

From here, you can setup an alert. With the **Metric** drop down box, you can setup an alert for the following types of data.

* Disk read
* Disk write
* Network in
* Network out
* CPU percentage

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a>Configure monitoring from a metric tile
Instead of using **Settings** > **Alert Rules**, you can click on one of the metric tiles in the **Monitoring** section of the **Cloud service** blade.

![Cloud Service Monitoring](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cs-monitoring.png)

From here you can customize the chart used with the tile, or add an alert rule.

## <a name="reboot-reimage-or-remote-desktop"></a>Reboot, reimage, or remote desktop
At this time you cannot configure remote desktop using the **Azure portal**. However, you can set it up through the [Azure classic portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).

First, click on the cloud service instance.

![Cloud Service Instance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cs-instance.png)

From the blade that opens you can initiate a remote desktop connection, remotely reboot the instance, or remotely reimage (start with a fresh image) the instance.

![Cloud Service Instance Buttons](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a>Reconfigure your .cscfg
You may need to reconfigure your cloud service through the [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file. First you need to download your .cscfg file, modify it, then upload it.

1. Click on the **Settings** icon or the **All settings** link to open up the **Settings** blade.

    ![Settings Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cloud-service.png)
2. Click on the **Configuration** item.

    ![Configuration Blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. Click on the **Download** button.

    ![Download](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. After you update the service configuration file, upload and apply the configuration updates:

    ![Upload](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. Select the .cscfg file and click **OK**.

## <a name="next-steps"></a>Next steps
* Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).
* Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).
* [Manage your cloud service](cloud-services-how-to-manage-portal.md).
* Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).












