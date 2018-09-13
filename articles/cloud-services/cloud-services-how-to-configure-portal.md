---
title: How to configure a cloud service (portal) | Microsoft Docs
description: Learn how to configure cloud services in Azure. Learn to update the cloud service configuration and configure remote access to role instances. These examples use the Azure portal.
services: cloud-services
documentationcenter: ''
author: jpconnock
manager: timlt
editor: ''
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: jeconnoc
ms.openlocfilehash: 904056363c685ef0a16b229ce72383eb80701a39
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44812187"
---
# <a name="how-to-configure-cloud-services"></a><span data-ttu-id="f4309-105">How to Configure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="f4309-105">How to Configure Cloud Services</span></span>

<span data-ttu-id="f4309-106">You can configure the most commonly used settings for a cloud service in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f4309-106">You can configure the most commonly used settings for a cloud service in the Azure portal.</span></span> <span data-ttu-id="f4309-107">Or, if you like to update your configuration files directly, download a service configuration file to update, and then upload the updated file and update the cloud service with the configuration changes.</span><span class="sxs-lookup"><span data-stu-id="f4309-107">Or, if you like to update your configuration files directly, download a service configuration file to update, and then upload the updated file and update the cloud service with the configuration changes.</span></span> <span data-ttu-id="f4309-108">Either way, the configuration updates are pushed out to all role instances.</span><span class="sxs-lookup"><span data-stu-id="f4309-108">Either way, the configuration updates are pushed out to all role instances.</span></span>

<span data-ttu-id="f4309-109">You can also manage the instances of your cloud service roles, or remote desktop into them.</span><span class="sxs-lookup"><span data-stu-id="f4309-109">You can also manage the instances of your cloud service roles, or remote desktop into them.</span></span>

<span data-ttu-id="f4309-110">Azure can only ensure 99.95 percent service availability during the configuration updates if you have at least two role instances for every role.</span><span class="sxs-lookup"><span data-stu-id="f4309-110">Azure can only ensure 99.95 percent service availability during the configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="f4309-111">That enables one virtual machine to process client requests while the other is being updated.</span><span class="sxs-lookup"><span data-stu-id="f4309-111">That enables one virtual machine to process client requests while the other is being updated.</span></span> <span data-ttu-id="f4309-112">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="f4309-112">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="f4309-113">Change a cloud service</span><span class="sxs-lookup"><span data-stu-id="f4309-113">Change a cloud service</span></span>

<span data-ttu-id="f4309-114">After opening the [Azure portal](https://portal.azure.com/), navigate to your cloud service.</span><span class="sxs-lookup"><span data-stu-id="f4309-114">After opening the [Azure portal](https://portal.azure.com/), navigate to your cloud service.</span></span> <span data-ttu-id="f4309-115">From here, you manage many aspects of it.</span><span class="sxs-lookup"><span data-stu-id="f4309-115">From here, you manage many aspects of it.</span></span>

![Settings Page](./media/cloud-services-how-to-configure-portal/cloud-service.png)

<span data-ttu-id="f4309-117">The **Settings** or **All settings** links will open up **Settings** where you can change the **Properties**, change the **Configuration**, manage the **Certificates**, set up **Alert rules**, and manage the **Users** who have access to this cloud service.</span><span class="sxs-lookup"><span data-stu-id="f4309-117">The **Settings** or **All settings** links will open up **Settings** where you can change the **Properties**, change the **Configuration**, manage the **Certificates**, set up **Alert rules**, and manage the **Users** who have access to this cloud service.</span></span>

![Azure cloud service settings](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a><span data-ttu-id="f4309-119">Manage Guest OS version</span><span class="sxs-lookup"><span data-stu-id="f4309-119">Manage Guest OS version</span></span>

<span data-ttu-id="f4309-120">By default, Azure periodically updates your guest OS to the latest supported image within the OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="f4309-120">By default, Azure periodically updates your guest OS to the latest supported image within the OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span></span>

<span data-ttu-id="f4309-121">If you need to target a specific OS version, you can set it in **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="f4309-121">If you need to target a specific OS version, you can set it in **Configuration**.</span></span>

![Set OS version](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)

>[!IMPORTANT]
> <span data-ttu-id="f4309-123">Choosing a specific OS version disables automatic OS updates and makes patching your responsibility.</span><span class="sxs-lookup"><span data-stu-id="f4309-123">Choosing a specific OS version disables automatic OS updates and makes patching your responsibility.</span></span> <span data-ttu-id="f4309-124">You must ensure that your role instances are receiving updates or you may expose your application to security vulnerabilities.</span><span class="sxs-lookup"><span data-stu-id="f4309-124">You must ensure that your role instances are receiving updates or you may expose your application to security vulnerabilities.</span></span>

## <a name="monitoring"></a><span data-ttu-id="f4309-125">Monitoring</span><span class="sxs-lookup"><span data-stu-id="f4309-125">Monitoring</span></span>

<span data-ttu-id="f4309-126">You can add alerts to your cloud service.</span><span class="sxs-lookup"><span data-stu-id="f4309-126">You can add alerts to your cloud service.</span></span> <span data-ttu-id="f4309-127">Click **Settings** > **Alert Rules** > **Add alert**.</span><span class="sxs-lookup"><span data-stu-id="f4309-127">Click **Settings** > **Alert Rules** > **Add alert**.</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

<span data-ttu-id="f4309-128">From here, you can set up an alert.</span><span class="sxs-lookup"><span data-stu-id="f4309-128">From here, you can set up an alert.</span></span> <span data-ttu-id="f4309-129">With the **Metric** drop-down box, you can set up an alert for the following types of data.</span><span class="sxs-lookup"><span data-stu-id="f4309-129">With the **Metric** drop-down box, you can set up an alert for the following types of data.</span></span>

* <span data-ttu-id="f4309-130">Disk read</span><span class="sxs-lookup"><span data-stu-id="f4309-130">Disk read</span></span>
* <span data-ttu-id="f4309-131">Disk write</span><span class="sxs-lookup"><span data-stu-id="f4309-131">Disk write</span></span>
* <span data-ttu-id="f4309-132">Network in</span><span class="sxs-lookup"><span data-stu-id="f4309-132">Network in</span></span>
* <span data-ttu-id="f4309-133">Network out</span><span class="sxs-lookup"><span data-stu-id="f4309-133">Network out</span></span>
* <span data-ttu-id="f4309-134">CPU percentage</span><span class="sxs-lookup"><span data-stu-id="f4309-134">CPU percentage</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a><span data-ttu-id="f4309-135">Configure monitoring from a metric tile</span><span class="sxs-lookup"><span data-stu-id="f4309-135">Configure monitoring from a metric tile</span></span>

<span data-ttu-id="f4309-136">Instead of using **Settings** > **Alert Rules**, you can click on one of the metric tiles in the **Monitoring** section of the cloud service.</span><span class="sxs-lookup"><span data-stu-id="f4309-136">Instead of using **Settings** > **Alert Rules**, you can click on one of the metric tiles in the **Monitoring** section of the cloud service.</span></span>

![Cloud Service Monitoring](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

<span data-ttu-id="f4309-138">From here you can customize the chart used with the tile, or add an alert rule.</span><span class="sxs-lookup"><span data-stu-id="f4309-138">From here you can customize the chart used with the tile, or add an alert rule.</span></span>

## <a name="reboot-reimage-or-remote-desktop"></a><span data-ttu-id="f4309-139">Reboot, reimage, or remote desktop</span><span class="sxs-lookup"><span data-stu-id="f4309-139">Reboot, reimage, or remote desktop</span></span>

<span data-ttu-id="f4309-140">You can set up remote desktop through the [Azure portal (set up remote desktop)](cloud-services-role-enable-remote-desktop-new-portal.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](cloud-services-role-enable-remote-desktop-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="f4309-140">You can set up remote desktop through the [Azure portal (set up remote desktop)](cloud-services-role-enable-remote-desktop-new-portal.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](cloud-services-role-enable-remote-desktop-visual-studio.md).</span></span>

<span data-ttu-id="f4309-141">To reboot, reimage, or remote into a Cloud Service, select the cloud service instance.</span><span class="sxs-lookup"><span data-stu-id="f4309-141">To reboot, reimage, or remote into a Cloud Service, select the cloud service instance.</span></span>

![Cloud Service Instance](./media/cloud-services-how-to-configure-portal/cs-instance.png)

<span data-ttu-id="f4309-143">You can then initiate a remote desktop connection, remotely reboot the instance, or remotely reimage (start with a fresh image) the instance.</span><span class="sxs-lookup"><span data-stu-id="f4309-143">You can then initiate a remote desktop connection, remotely reboot the instance, or remotely reimage (start with a fresh image) the instance.</span></span>

![Cloud Service Instance Buttons](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a><span data-ttu-id="f4309-145">Reconfigure your .cscfg</span><span class="sxs-lookup"><span data-stu-id="f4309-145">Reconfigure your .cscfg</span></span>

<span data-ttu-id="f4309-146">You may need to reconfigure your cloud service through the [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span><span class="sxs-lookup"><span data-stu-id="f4309-146">You may need to reconfigure your cloud service through the [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span></span> <span data-ttu-id="f4309-147">First you need to download your .cscfg file, modify it, then upload it.</span><span class="sxs-lookup"><span data-stu-id="f4309-147">First you need to download your .cscfg file, modify it, then upload it.</span></span>

1. <span data-ttu-id="f4309-148">Click on the **Settings** icon or the **All settings** link to open up **Settings**.</span><span class="sxs-lookup"><span data-stu-id="f4309-148">Click on the **Settings** icon or the **All settings** link to open up **Settings**.</span></span>

    ![Settings Page](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. <span data-ttu-id="f4309-150">Click on the **Configuration** item.</span><span class="sxs-lookup"><span data-stu-id="f4309-150">Click on the **Configuration** item.</span></span>

    ![Configuration Blade](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. <span data-ttu-id="f4309-152">Click on the **Download** button.</span><span class="sxs-lookup"><span data-stu-id="f4309-152">Click on the **Download** button.</span></span>

    ![Download](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. <span data-ttu-id="f4309-154">After you update the service configuration file, upload and apply the configuration updates:</span><span class="sxs-lookup"><span data-stu-id="f4309-154">After you update the service configuration file, upload and apply the configuration updates:</span></span>

    ![Upload](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. <span data-ttu-id="f4309-156">Select the .cscfg file and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f4309-156">Select the .cscfg file and click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4309-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="f4309-157">Next steps</span></span>

* <span data-ttu-id="f4309-158">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f4309-158">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="f4309-159">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f4309-159">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="f4309-160">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f4309-160">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="f4309-161">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f4309-161">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
