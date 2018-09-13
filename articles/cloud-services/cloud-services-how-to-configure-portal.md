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
# <a name="how-to-configure-cloud-services"></a><span data-ttu-id="11c3d-105">How to Configure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="11c3d-105">How to Configure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-how-to-configure-portal.md)
> * [Azure classic portal](cloud-services-how-to-configure.md)
>
>

<span data-ttu-id="11c3d-108">You can configure the most commonly used settings for a cloud service in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="11c3d-108">You can configure the most commonly used settings for a cloud service in the Azure portal.</span></span> <span data-ttu-id="11c3d-109">Or, if you like to update your configuration files directly, download a service configuration file to update, and then upload the updated file and update the cloud service with the configuration changes.</span><span class="sxs-lookup"><span data-stu-id="11c3d-109">Or, if you like to update your configuration files directly, download a service configuration file to update, and then upload the updated file and update the cloud service with the configuration changes.</span></span> <span data-ttu-id="11c3d-110">Either way, the configuration updates are pushed out to all role instances.</span><span class="sxs-lookup"><span data-stu-id="11c3d-110">Either way, the configuration updates are pushed out to all role instances.</span></span>

<span data-ttu-id="11c3d-111">You can also manage the instances of your cloud service roles, or remote desktop into them.</span><span class="sxs-lookup"><span data-stu-id="11c3d-111">You can also manage the instances of your cloud service roles, or remote desktop into them.</span></span>

<span data-ttu-id="11c3d-112">Azure can only ensure 99.95 percent service availability during the configuration updates if you have at least two role instances for every role.</span><span class="sxs-lookup"><span data-stu-id="11c3d-112">Azure can only ensure 99.95 percent service availability during the configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="11c3d-113">That enables one virtual machine to process client requests while the other is being updated.</span><span class="sxs-lookup"><span data-stu-id="11c3d-113">That enables one virtual machine to process client requests while the other is being updated.</span></span> <span data-ttu-id="11c3d-114">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="11c3d-114">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="11c3d-115">Change a cloud service</span><span class="sxs-lookup"><span data-stu-id="11c3d-115">Change a cloud service</span></span>
<span data-ttu-id="11c3d-116">After opening the [Azure portal](https://portal.azure.com/), navigate to your cloud service.</span><span class="sxs-lookup"><span data-stu-id="11c3d-116">After opening the [Azure portal](https://portal.azure.com/), navigate to your cloud service.</span></span> <span data-ttu-id="11c3d-117">From here, you manage many aspects of it.</span><span class="sxs-lookup"><span data-stu-id="11c3d-117">From here, you manage many aspects of it.</span></span>

![Settings Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cloud-service.png)

<span data-ttu-id="11c3d-119">The **Settings** or **All settings** links will open up the **Settings** blade where you can change the **Properties**, change the **Configuration**, manage the **Certificates**, setup **Alert rules**, and manage the **Users** who have access to this cloud service.</span><span class="sxs-lookup"><span data-stu-id="11c3d-119">The **Settings** or **All settings** links will open up the **Settings** blade where you can change the **Properties**, change the **Configuration**, manage the **Certificates**, setup **Alert rules**, and manage the **Users** who have access to this cloud service.</span></span>

![Azure cloud service settings blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a><span data-ttu-id="11c3d-121">Manage Guest OS version</span><span class="sxs-lookup"><span data-stu-id="11c3d-121">Manage Guest OS version</span></span>

<span data-ttu-id="11c3d-122">By default, Azure periodically updates your guest OS to the latest supported image within the OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="11c3d-122">By default, Azure periodically updates your guest OS to the latest supported image within the OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span></span>

<span data-ttu-id="11c3d-123">If you need to target a specific OS version, you can set it in the **Configuration** blade.</span><span class="sxs-lookup"><span data-stu-id="11c3d-123">If you need to target a specific OS version, you can set it in the **Configuration** blade.</span></span>

![Set OS version](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> Choosing a specific OS version disables automatic OS updates and makes patching your responsibility. You must ensure that your role instances are receiving updates or you may expose your application to security vulnerabilities.

## <a name="monitoring"></a><span data-ttu-id="11c3d-127">Monitoring</span><span class="sxs-lookup"><span data-stu-id="11c3d-127">Monitoring</span></span>
<span data-ttu-id="11c3d-128">You can add alerts to your cloud service.</span><span class="sxs-lookup"><span data-stu-id="11c3d-128">You can add alerts to your cloud service.</span></span> <span data-ttu-id="11c3d-129">Click **Settings** > **Alert Rules** > **Add alert**.</span><span class="sxs-lookup"><span data-stu-id="11c3d-129">Click **Settings** > **Alert Rules** > **Add alert**.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cs-alerts.png)

<span data-ttu-id="11c3d-130">From here, you can setup an alert.</span><span class="sxs-lookup"><span data-stu-id="11c3d-130">From here, you can setup an alert.</span></span> <span data-ttu-id="11c3d-131">With the **Metric** drop down box, you can setup an alert for the following types of data.</span><span class="sxs-lookup"><span data-stu-id="11c3d-131">With the **Metric** drop down box, you can setup an alert for the following types of data.</span></span>

* <span data-ttu-id="11c3d-132">Disk read</span><span class="sxs-lookup"><span data-stu-id="11c3d-132">Disk read</span></span>
* <span data-ttu-id="11c3d-133">Disk write</span><span class="sxs-lookup"><span data-stu-id="11c3d-133">Disk write</span></span>
* <span data-ttu-id="11c3d-134">Network in</span><span class="sxs-lookup"><span data-stu-id="11c3d-134">Network in</span></span>
* <span data-ttu-id="11c3d-135">Network out</span><span class="sxs-lookup"><span data-stu-id="11c3d-135">Network out</span></span>
* <span data-ttu-id="11c3d-136">CPU percentage</span><span class="sxs-lookup"><span data-stu-id="11c3d-136">CPU percentage</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a><span data-ttu-id="11c3d-137">Configure monitoring from a metric tile</span><span class="sxs-lookup"><span data-stu-id="11c3d-137">Configure monitoring from a metric tile</span></span>
<span data-ttu-id="11c3d-138">Instead of using **Settings** > **Alert Rules**, you can click on one of the metric tiles in the **Monitoring** section of the **Cloud service** blade.</span><span class="sxs-lookup"><span data-stu-id="11c3d-138">Instead of using **Settings** > **Alert Rules**, you can click on one of the metric tiles in the **Monitoring** section of the **Cloud service** blade.</span></span>

![Cloud Service Monitoring](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cs-monitoring.png)

<span data-ttu-id="11c3d-140">From here you can customize the chart used with the tile, or add an alert rule.</span><span class="sxs-lookup"><span data-stu-id="11c3d-140">From here you can customize the chart used with the tile, or add an alert rule.</span></span>

## <a name="reboot-reimage-or-remote-desktop"></a><span data-ttu-id="11c3d-141">Reboot, reimage, or remote desktop</span><span class="sxs-lookup"><span data-stu-id="11c3d-141">Reboot, reimage, or remote desktop</span></span>
<span data-ttu-id="11c3d-142">At this time you cannot configure remote desktop using the **Azure portal**.</span><span class="sxs-lookup"><span data-stu-id="11c3d-142">At this time you cannot configure remote desktop using the **Azure portal**.</span></span> <span data-ttu-id="11c3d-143">However, you can set it up through the [Azure classic portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="11c3d-143">However, you can set it up through the [Azure classic portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span></span>

<span data-ttu-id="11c3d-144">First, click on the cloud service instance.</span><span class="sxs-lookup"><span data-stu-id="11c3d-144">First, click on the cloud service instance.</span></span>

![Cloud Service Instance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cs-instance.png)

<span data-ttu-id="11c3d-146">From the blade that opens you can initiate a remote desktop connection, remotely reboot the instance, or remotely reimage (start with a fresh image) the instance.</span><span class="sxs-lookup"><span data-stu-id="11c3d-146">From the blade that opens you can initiate a remote desktop connection, remotely reboot the instance, or remotely reimage (start with a fresh image) the instance.</span></span>

![Cloud Service Instance Buttons](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a><span data-ttu-id="11c3d-148">Reconfigure your .cscfg</span><span class="sxs-lookup"><span data-stu-id="11c3d-148">Reconfigure your .cscfg</span></span>
<span data-ttu-id="11c3d-149">You may need to reconfigure your cloud service through the [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span><span class="sxs-lookup"><span data-stu-id="11c3d-149">You may need to reconfigure your cloud service through the [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span></span> <span data-ttu-id="11c3d-150">First you need to download your .cscfg file, modify it, then upload it.</span><span class="sxs-lookup"><span data-stu-id="11c3d-150">First you need to download your .cscfg file, modify it, then upload it.</span></span>

1. <span data-ttu-id="11c3d-151">Click on the **Settings** icon or the **All settings** link to open up the **Settings** blade.</span><span class="sxs-lookup"><span data-stu-id="11c3d-151">Click on the **Settings** icon or the **All settings** link to open up the **Settings** blade.</span></span>

    ![Settings Page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cloud-service.png)
2. <span data-ttu-id="11c3d-153">Click on the **Configuration** item.</span><span class="sxs-lookup"><span data-stu-id="11c3d-153">Click on the **Configuration** item.</span></span>

    ![Configuration Blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. <span data-ttu-id="11c3d-155">Click on the **Download** button.</span><span class="sxs-lookup"><span data-stu-id="11c3d-155">Click on the **Download** button.</span></span>

    ![Download](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. <span data-ttu-id="11c3d-157">After you update the service configuration file, upload and apply the configuration updates:</span><span class="sxs-lookup"><span data-stu-id="11c3d-157">After you update the service configuration file, upload and apply the configuration updates:</span></span>

    ![Upload](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. <span data-ttu-id="11c3d-159">Select the .cscfg file and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="11c3d-159">Select the .cscfg file and click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11c3d-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="11c3d-160">Next steps</span></span>
* <span data-ttu-id="11c3d-161">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="11c3d-161">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="11c3d-162">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="11c3d-162">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="11c3d-163">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="11c3d-163">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="11c3d-164">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="11c3d-164">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>












