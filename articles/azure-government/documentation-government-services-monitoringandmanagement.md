---
title: Azure Government Monitoring + Management | Microsoft Docs
description: This provides a comparison of features and guidance on developing applications for Azure Government.
services: azure-government
cloud: gov
documentationcenter: ''
author: ryansoc
manager: zakramer
ms.assetid: 4b7720c1-699e-432b-9246-6e49fb77f497
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 3/13/2017
ms.author: ryansoc
ms.openlocfilehash: 866658c1226dc068b2048d8fb3c62efded408932
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670578"
---
# <a name="azure-government-monitoring--management"></a><span data-ttu-id="90940-103">Azure Government Monitoring + Management</span><span class="sxs-lookup"><span data-stu-id="90940-103">Azure Government Monitoring + Management</span></span>
<span data-ttu-id="90940-104">This article outlines the monitoring and management services variations and considerations for the Azure Government environment.</span><span class="sxs-lookup"><span data-stu-id="90940-104">This article outlines the monitoring and management services variations and considerations for the Azure Government environment.</span></span>

## <a name="automation"></a><span data-ttu-id="90940-105">Automation</span><span class="sxs-lookup"><span data-stu-id="90940-105">Automation</span></span>
<span data-ttu-id="90940-106">Automation is generally available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="90940-106">Automation is generally available in Azure Government.</span></span>

### <a name="variations"></a><span data-ttu-id="90940-107">Variations</span><span class="sxs-lookup"><span data-stu-id="90940-107">Variations</span></span>
<span data-ttu-id="90940-108">The following Automation features are not currently available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="90940-108">The following Automation features are not currently available in Azure Government.</span></span>

* <span data-ttu-id="90940-109">Creation of a Service Principal credential for authentication</span><span class="sxs-lookup"><span data-stu-id="90940-109">Creation of a Service Principal credential for authentication</span></span>

<span data-ttu-id="90940-110">For more information, see [Automation public documentation](../automation/automation-intro.md).</span><span class="sxs-lookup"><span data-stu-id="90940-110">For more information, see [Automation public documentation](../automation/automation-intro.md).</span></span>

## <a name="backup"></a><span data-ttu-id="90940-111">Backup</span><span class="sxs-lookup"><span data-stu-id="90940-111">Backup</span></span>
<span data-ttu-id="90940-112">Backup is generally available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="90940-112">Backup is generally available in Azure Government.</span></span>

<span data-ttu-id="90940-113">For more information, see [Azure Government Backup](documentation-government-services-backup.md).</span><span class="sxs-lookup"><span data-stu-id="90940-113">For more information, see [Azure Government Backup](documentation-government-services-backup.md).</span></span>

## <a name="resource-policy"></a><span data-ttu-id="90940-114">Resource Policy</span><span class="sxs-lookup"><span data-stu-id="90940-114">Resource Policy</span></span>

<span data-ttu-id="90940-115">[Azure resource policies](../azure-resource-manager/resource-manager-policy.md) are not available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="90940-115">[Azure resource policies](../azure-resource-manager/resource-manager-policy.md) are not available in Azure Government.</span></span>

## <a name="site-recovery"></a><span data-ttu-id="90940-116">Site Recovery</span><span class="sxs-lookup"><span data-stu-id="90940-116">Site Recovery</span></span>
<span data-ttu-id="90940-117">Azure Site Recovery is generally available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="90940-117">Azure Site Recovery is generally available in Azure Government.</span></span>

<span data-ttu-id="90940-118">For more information, see [Site Recovery commercial documentation](../site-recovery/site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="90940-118">For more information, see [Site Recovery commercial documentation](../site-recovery/site-recovery-overview.md).</span></span>

### <a name="variations"></a><span data-ttu-id="90940-119">Variations</span><span class="sxs-lookup"><span data-stu-id="90940-119">Variations</span></span>
<span data-ttu-id="90940-120">The following Site Recovery features are not currently available in Azure Government:</span><span class="sxs-lookup"><span data-stu-id="90940-120">The following Site Recovery features are not currently available in Azure Government:</span></span>

* <span data-ttu-id="90940-121">Azure Resource Manager Site Recovery vaults</span><span class="sxs-lookup"><span data-stu-id="90940-121">Azure Resource Manager Site Recovery vaults</span></span>
* <span data-ttu-id="90940-122">Email notification</span><span class="sxs-lookup"><span data-stu-id="90940-122">Email notification</span></span>

| <span data-ttu-id="90940-123">Site Recovery</span><span class="sxs-lookup"><span data-stu-id="90940-123">Site Recovery</span></span> | <span data-ttu-id="90940-124">Classic</span><span class="sxs-lookup"><span data-stu-id="90940-124">Classic</span></span> | <span data-ttu-id="90940-125">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="90940-125">Resource Manager</span></span> |
| --- | --- | --- |
| <span data-ttu-id="90940-126">VMWare/Physical</span><span class="sxs-lookup"><span data-stu-id="90940-126">VMWare/Physical</span></span>  | <span data-ttu-id="90940-127">GA</span><span class="sxs-lookup"><span data-stu-id="90940-127">GA</span></span> | <span data-ttu-id="90940-128">GA</span><span class="sxs-lookup"><span data-stu-id="90940-128">GA</span></span> |
| <span data-ttu-id="90940-129">Hyper-V</span><span class="sxs-lookup"><span data-stu-id="90940-129">Hyper-V</span></span> | <span data-ttu-id="90940-130">GA</span><span class="sxs-lookup"><span data-stu-id="90940-130">GA</span></span> | <span data-ttu-id="90940-131">GA</span><span class="sxs-lookup"><span data-stu-id="90940-131">GA</span></span> |
| <span data-ttu-id="90940-132">Site to Site</span><span class="sxs-lookup"><span data-stu-id="90940-132">Site to Site</span></span> | <span data-ttu-id="90940-133">GA</span><span class="sxs-lookup"><span data-stu-id="90940-133">GA</span></span> | <span data-ttu-id="90940-134">GA</span><span class="sxs-lookup"><span data-stu-id="90940-134">GA</span></span> |

>[!NOTE]
><span data-ttu-id="90940-135">Table applies to US Gov Virginia and US Gov Iowa.</span><span class="sxs-lookup"><span data-stu-id="90940-135">Table applies to US Gov Virginia and US Gov Iowa.</span></span>

<span data-ttu-id="90940-136">The following URLs for Site Recovery are different in Azure Government:</span><span class="sxs-lookup"><span data-stu-id="90940-136">The following URLs for Site Recovery are different in Azure Government:</span></span>

| <span data-ttu-id="90940-137">Azure Public</span><span class="sxs-lookup"><span data-stu-id="90940-137">Azure Public</span></span> | <span data-ttu-id="90940-138">Azure Government</span><span class="sxs-lookup"><span data-stu-id="90940-138">Azure Government</span></span> | <span data-ttu-id="90940-139">Notes</span><span class="sxs-lookup"><span data-stu-id="90940-139">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="90940-140">\*.hypervrecoverymanager.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="90940-140">\*.hypervrecoverymanager.windowsazure.com</span></span> | <span data-ttu-id="90940-141">\*.hypervrecoverymanager.windowsazure.us</span><span class="sxs-lookup"><span data-stu-id="90940-141">\*.hypervrecoverymanager.windowsazure.us</span></span> | <span data-ttu-id="90940-142">Access to the Site Recovery Service</span><span class="sxs-lookup"><span data-stu-id="90940-142">Access to the Site Recovery Service</span></span> |
| <span data-ttu-id="90940-143">\*.backup.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="90940-143">\*.backup.windowsazure.com</span></span>  | <span data-ttu-id="90940-144">\*.backup.windowsazure.us</span><span class="sxs-lookup"><span data-stu-id="90940-144">\*.backup.windowsazure.us</span></span> | <span data-ttu-id="90940-145">Access to Protection Service</span><span class="sxs-lookup"><span data-stu-id="90940-145">Access to Protection Service</span></span> |
| <span data-ttu-id="90940-146">\*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="90940-146">\*.blob.core.windows.net</span></span> | <span data-ttu-id="90940-147">\*.blob.core.usgovcloudapi.net</span><span class="sxs-lookup"><span data-stu-id="90940-147">\*.blob.core.usgovcloudapi.net</span></span> | <span data-ttu-id="90940-148">For storing the VM Snapshots</span><span class="sxs-lookup"><span data-stu-id="90940-148">For storing the VM Snapshots</span></span> |
| http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi | http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi | <span data-ttu-id="90940-149">To download MySQL</span><span class="sxs-lookup"><span data-stu-id="90940-149">To download MySQL</span></span> |


## <a name="monitor"></a><span data-ttu-id="90940-150">Monitor</span><span class="sxs-lookup"><span data-stu-id="90940-150">Monitor</span></span>
<span data-ttu-id="90940-151">Azure Monitor is in public preview in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="90940-151">Azure Monitor is in public preview in Azure Government.</span></span>

<span data-ttu-id="90940-152">For more information, see [Monitor commercial documentation](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview).</span><span class="sxs-lookup"><span data-stu-id="90940-152">For more information, see [Monitor commercial documentation](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview).</span></span>

### <a name="variations"></a><span data-ttu-id="90940-153">Variations</span><span class="sxs-lookup"><span data-stu-id="90940-153">Variations</span></span>
<span data-ttu-id="90940-154">The following Monitor features are not currently available in Azure Government:</span><span class="sxs-lookup"><span data-stu-id="90940-154">The following Monitor features are not currently available in Azure Government:</span></span>

* <span data-ttu-id="90940-155">Metrics and Alerts</span><span class="sxs-lookup"><span data-stu-id="90940-155">Metrics and Alerts</span></span>
* <span data-ttu-id="90940-156">Diagnostic Logs</span><span class="sxs-lookup"><span data-stu-id="90940-156">Diagnostic Logs</span></span>
* <span data-ttu-id="90940-157">Autoscale</span><span class="sxs-lookup"><span data-stu-id="90940-157">Autoscale</span></span>
* <span data-ttu-id="90940-158">Action Groups</span><span class="sxs-lookup"><span data-stu-id="90940-158">Action Groups</span></span>


## <a name="log-analytics"></a><span data-ttu-id="90940-159">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="90940-159">Log Analytics</span></span>
<span data-ttu-id="90940-160">Log Analytics is generally available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="90940-160">Log Analytics is generally available in Azure Government.</span></span>

### <a name="variations"></a><span data-ttu-id="90940-161">Variations</span><span class="sxs-lookup"><span data-stu-id="90940-161">Variations</span></span>
<span data-ttu-id="90940-162">The following Log Analytics features and solutions are not currently available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="90940-162">The following Log Analytics features and solutions are not currently available in Azure Government.</span></span>

* <span data-ttu-id="90940-163">Solutions that are in preview in Microsoft Azure, including:</span><span class="sxs-lookup"><span data-stu-id="90940-163">Solutions that are in preview in Microsoft Azure, including:</span></span>
  * <span data-ttu-id="90940-164">Network Monitoring solution</span><span class="sxs-lookup"><span data-stu-id="90940-164">Network Monitoring solution</span></span>
  * <span data-ttu-id="90940-165">Service Map</span><span class="sxs-lookup"><span data-stu-id="90940-165">Service Map</span></span>
  * <span data-ttu-id="90940-166">Office 365 solution</span><span class="sxs-lookup"><span data-stu-id="90940-166">Office 365 solution</span></span>
  * <span data-ttu-id="90940-167">Windows 10 Upgrade Analytics solution</span><span class="sxs-lookup"><span data-stu-id="90940-167">Windows 10 Upgrade Analytics solution</span></span>
  * <span data-ttu-id="90940-168">Application Insights solution</span><span class="sxs-lookup"><span data-stu-id="90940-168">Application Insights solution</span></span>
  * <span data-ttu-id="90940-169">Azure Networking Analytics solution</span><span class="sxs-lookup"><span data-stu-id="90940-169">Azure Networking Analytics solution</span></span>
  * <span data-ttu-id="90940-170">Azure Automation Analytics solution</span><span class="sxs-lookup"><span data-stu-id="90940-170">Azure Automation Analytics solution</span></span>
  * <span data-ttu-id="90940-171">Key Vault Analytics solution</span><span class="sxs-lookup"><span data-stu-id="90940-171">Key Vault Analytics solution</span></span>
* <span data-ttu-id="90940-172">Solutions and features that require updates to on-premises software, including:</span><span class="sxs-lookup"><span data-stu-id="90940-172">Solutions and features that require updates to on-premises software, including:</span></span>
  * <span data-ttu-id="90940-173">Surface Hub solution</span><span class="sxs-lookup"><span data-stu-id="90940-173">Surface Hub solution</span></span>
* <span data-ttu-id="90940-174">Features that are in preview in public Azure, including:</span><span class="sxs-lookup"><span data-stu-id="90940-174">Features that are in preview in public Azure, including:</span></span>
  * <span data-ttu-id="90940-175">Export of data to Power BI</span><span class="sxs-lookup"><span data-stu-id="90940-175">Export of data to Power BI</span></span>
* <span data-ttu-id="90940-176">Azure metrics and Azure diagnostics</span><span class="sxs-lookup"><span data-stu-id="90940-176">Azure metrics and Azure diagnostics</span></span>
* <span data-ttu-id="90940-177">Operations Management Suite mobile applications</span><span class="sxs-lookup"><span data-stu-id="90940-177">Operations Management Suite mobile applications</span></span>

<span data-ttu-id="90940-178">The URLs for Log Analytics are different in Azure Government:</span><span class="sxs-lookup"><span data-stu-id="90940-178">The URLs for Log Analytics are different in Azure Government:</span></span>

| <span data-ttu-id="90940-179">Azure Public</span><span class="sxs-lookup"><span data-stu-id="90940-179">Azure Public</span></span> | <span data-ttu-id="90940-180">Azure Government</span><span class="sxs-lookup"><span data-stu-id="90940-180">Azure Government</span></span> | <span data-ttu-id="90940-181">Notes</span><span class="sxs-lookup"><span data-stu-id="90940-181">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="90940-182">mms.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="90940-182">mms.microsoft.com</span></span> |<span data-ttu-id="90940-183">oms.microsoft.us</span><span class="sxs-lookup"><span data-stu-id="90940-183">oms.microsoft.us</span></span> |<span data-ttu-id="90940-184">Log Analytics portal</span><span class="sxs-lookup"><span data-stu-id="90940-184">Log Analytics portal</span></span> |
| <span data-ttu-id="90940-185">*workspaceId*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="90940-185">*workspaceId*.ods.opinsights.azure.com</span></span> |<span data-ttu-id="90940-186">*workspaceId*.ods.opinsights.azure.us</span><span class="sxs-lookup"><span data-stu-id="90940-186">*workspaceId*.ods.opinsights.azure.us</span></span> |[<span data-ttu-id="90940-187">Data collector API</span><span class="sxs-lookup"><span data-stu-id="90940-187">Data collector API</span></span>](../log-analytics/log-analytics-data-collector-api.md) |
| <span data-ttu-id="90940-188">\*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="90940-188">\*.ods.opinsights.azure.com</span></span> |<span data-ttu-id="90940-189">\*.ods.opinsights.azure.us</span><span class="sxs-lookup"><span data-stu-id="90940-189">\*.ods.opinsights.azure.us</span></span> |<span data-ttu-id="90940-190">Agent communication - [configuring firewall settings](../log-analytics/log-analytics-proxy-firewall.md)</span><span class="sxs-lookup"><span data-stu-id="90940-190">Agent communication - [configuring firewall settings](../log-analytics/log-analytics-proxy-firewall.md)</span></span> |
| <span data-ttu-id="90940-191">\*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="90940-191">\*.oms.opinsights.azure.com</span></span> |<span data-ttu-id="90940-192">\*.oms.opinsights.azure.us</span><span class="sxs-lookup"><span data-stu-id="90940-192">\*.oms.opinsights.azure.us</span></span> |<span data-ttu-id="90940-193">Agent communication - [configuring firewall settings](../log-analytics/log-analytics-proxy-firewall.md)</span><span class="sxs-lookup"><span data-stu-id="90940-193">Agent communication - [configuring firewall settings](../log-analytics/log-analytics-proxy-firewall.md)</span></span> |
| <span data-ttu-id="90940-194">\*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="90940-194">\*.blob.core.windows.net</span></span> |<span data-ttu-id="90940-195">\*.blob.core.usgovcloudapi.net</span><span class="sxs-lookup"><span data-stu-id="90940-195">\*.blob.core.usgovcloudapi.net</span></span> |<span data-ttu-id="90940-196">Agent communication - [configuring firewall settings](../log-analytics/log-analytics-proxy-firewall.md)</span><span class="sxs-lookup"><span data-stu-id="90940-196">Agent communication - [configuring firewall settings](../log-analytics/log-analytics-proxy-firewall.md)</span></span> |

<span data-ttu-id="90940-197">The following Log Analytics features behave differently in Azure Government:</span><span class="sxs-lookup"><span data-stu-id="90940-197">The following Log Analytics features behave differently in Azure Government:</span></span>

* <span data-ttu-id="90940-198">To connect your System Center Operations Manager management server to Log Analytics, you need to download and import updated management packs.</span><span class="sxs-lookup"><span data-stu-id="90940-198">To connect your System Center Operations Manager management server to Log Analytics, you need to download and import updated management packs.</span></span>
  + <span data-ttu-id="90940-199">System Center Operations Manager 2016</span><span class="sxs-lookup"><span data-stu-id="90940-199">System Center Operations Manager 2016</span></span>
    1. <span data-ttu-id="90940-200">Install [Update Rollup 2 for System Center Operations Manager 2016](https://support.microsoft.com/help/3209591).</span><span class="sxs-lookup"><span data-stu-id="90940-200">Install [Update Rollup 2 for System Center Operations Manager 2016](https://support.microsoft.com/help/3209591).</span></span>
    2. <span data-ttu-id="90940-201">Import the management packs included as part of Update Rollup 2 into Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="90940-201">Import the management packs included as part of Update Rollup 2 into Operations Manager.</span></span> <span data-ttu-id="90940-202">For information about how to import a management pack from a disk, see [How to Import an Operations Manager Management Pack](http://technet.microsoft.com/library/hh212691.aspx).</span><span class="sxs-lookup"><span data-stu-id="90940-202">For information about how to import a management pack from a disk, see [How to Import an Operations Manager Management Pack](http://technet.microsoft.com/library/hh212691.aspx).</span></span>
    3. <span data-ttu-id="90940-203">To connect Operations Manager to Log Analytics, follow the steps in [Connect Operations Manager to Log Analytics](../log-analytics/log-analytics-om-agents.md).</span><span class="sxs-lookup"><span data-stu-id="90940-203">To connect Operations Manager to Log Analytics, follow the steps in [Connect Operations Manager to Log Analytics](../log-analytics/log-analytics-om-agents.md).</span></span>
  + <span data-ttu-id="90940-204">System Center Operations Manager 2012 R2 UR3 (or later) / Operations Manager 2012 SP1 UR7 (or later)</span><span class="sxs-lookup"><span data-stu-id="90940-204">System Center Operations Manager 2012 R2 UR3 (or later) / Operations Manager 2012 SP1 UR7 (or later)</span></span>
    1. <span data-ttu-id="90940-205">Download and save the [updated management packs](http://go.microsoft.com/fwlink/?LinkId=828749).</span><span class="sxs-lookup"><span data-stu-id="90940-205">Download and save the [updated management packs](http://go.microsoft.com/fwlink/?LinkId=828749).</span></span>
    2. <span data-ttu-id="90940-206">Unzip the file that you downloaded.</span><span class="sxs-lookup"><span data-stu-id="90940-206">Unzip the file that you downloaded.</span></span>
    3. <span data-ttu-id="90940-207">Import the management packs into Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="90940-207">Import the management packs into Operations Manager.</span></span> <span data-ttu-id="90940-208">For information about how to import a management pack from a disk, see [How to Import an Operations Manager Management Pack](http://technet.microsoft.com/library/hh212691.aspx).</span><span class="sxs-lookup"><span data-stu-id="90940-208">For information about how to import a management pack from a disk, see [How to Import an Operations Manager Management Pack](http://technet.microsoft.com/library/hh212691.aspx).</span></span>
    4. <span data-ttu-id="90940-209">To connect Operations Manager to Log Analytics, follow the steps in [Connect Operations Manager to Log Analytics](../log-analytics/log-analytics-om-agents.md).</span><span class="sxs-lookup"><span data-stu-id="90940-209">To connect Operations Manager to Log Analytics, follow the steps in [Connect Operations Manager to Log Analytics](../log-analytics/log-analytics-om-agents.md).</span></span>
  
* <span data-ttu-id="90940-210">To use [computer groups from System Center Configuration Manager 2016](../log-analytics/log-analytics-sccm.md), you need to be using [Technical Preview 1701](https://docs.microsoft.com/en-us/sccm/core/get-started/technical-preview) or later.</span><span class="sxs-lookup"><span data-stu-id="90940-210">To use [computer groups from System Center Configuration Manager 2016](../log-analytics/log-analytics-sccm.md), you need to be using [Technical Preview 1701](https://docs.microsoft.com/en-us/sccm/core/get-started/technical-preview) or later.</span></span>

### <a name="frequently-asked-questions"></a><span data-ttu-id="90940-211">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="90940-211">Frequently asked questions</span></span>
* <span data-ttu-id="90940-212">Can I migrate data from Log Analytics in Microsoft Azure to Azure Government?</span><span class="sxs-lookup"><span data-stu-id="90940-212">Can I migrate data from Log Analytics in Microsoft Azure to Azure Government?</span></span>
  * <span data-ttu-id="90940-213">No.</span><span class="sxs-lookup"><span data-stu-id="90940-213">No.</span></span> <span data-ttu-id="90940-214">It is not possible to move data or your workspace from Microsoft Azure to Azure Government.</span><span class="sxs-lookup"><span data-stu-id="90940-214">It is not possible to move data or your workspace from Microsoft Azure to Azure Government.</span></span>
* <span data-ttu-id="90940-215">Can I switch between Microsoft Azure and Azure Government workspaces from the Operations Management Suite Log Analytics portal?</span><span class="sxs-lookup"><span data-stu-id="90940-215">Can I switch between Microsoft Azure and Azure Government workspaces from the Operations Management Suite Log Analytics portal?</span></span>
  * <span data-ttu-id="90940-216">No.</span><span class="sxs-lookup"><span data-stu-id="90940-216">No.</span></span> <span data-ttu-id="90940-217">The portals for Microsoft Azure and Azure Government are separate and do not share information.</span><span class="sxs-lookup"><span data-stu-id="90940-217">The portals for Microsoft Azure and Azure Government are separate and do not share information.</span></span>

<span data-ttu-id="90940-218">For more information, see [Log Analytics public documentation](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="90940-218">For more information, see [Log Analytics public documentation](../log-analytics/log-analytics-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="90940-219">Next steps</span><span class="sxs-lookup"><span data-stu-id="90940-219">Next steps</span></span>
<span data-ttu-id="90940-220">For supplemental information and updates, subscribe to the <a href="https://blogs.msdn.microsoft.com/azuregov/">Microsoft Azure Government Blog. </a></span><span class="sxs-lookup"><span data-stu-id="90940-220">For supplemental information and updates, subscribe to the <a href="https://blogs.msdn.microsoft.com/azuregov/">Microsoft Azure Government Blog. </a></span></span>
