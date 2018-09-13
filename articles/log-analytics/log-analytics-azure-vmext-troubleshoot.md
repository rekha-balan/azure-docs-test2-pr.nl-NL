---
title: Troubleshoot Azure Log Analytics VM Extension | Microsoft Docs
description: Describe the symptoms, causes, and resolution for the most common issues with the Log Analytics VM extension for Windows and Linux Azure VMs.
services: log-analytics
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: ''
ms.service: log-analytics
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/08/2018
ms.author: magoedte
ms.component: na
ms.openlocfilehash: 700d6b2c3bcd39aed38bf75556bcdcb59d1ab78b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867833"
---
# <a name="troubleshooting-the-log-analytics-vm-extension"></a><span data-ttu-id="ab6f8-103">Troubleshooting the Log Analytics VM extension</span><span class="sxs-lookup"><span data-stu-id="ab6f8-103">Troubleshooting the Log Analytics VM extension</span></span>
<span data-ttu-id="ab6f8-104">This article provides help troubleshooting errors you might experience with the Log Analytics VM extension for Windows and Linux virtual machines running on Microsoft Azure, and suggests possible solutions to resolve them.</span><span class="sxs-lookup"><span data-stu-id="ab6f8-104">This article provides help troubleshooting errors you might experience with the Log Analytics VM extension for Windows and Linux virtual machines running on Microsoft Azure, and suggests possible solutions to resolve them.</span></span>

<span data-ttu-id="ab6f8-105">To verify the status of the extension, perform the following steps from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ab6f8-105">To verify the status of the extension, perform the following steps from the Azure portal.</span></span>

1. <span data-ttu-id="ab6f8-106">Sign into the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ab6f8-106">Sign into the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="ab6f8-107">In the Azure portal, click **All services**.</span><span class="sxs-lookup"><span data-stu-id="ab6f8-107">In the Azure portal, click **All services**.</span></span> <span data-ttu-id="ab6f8-108">In the list of resources, type **virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="ab6f8-108">In the list of resources, type **virtual machines**.</span></span> <span data-ttu-id="ab6f8-109">As you begin typing, the list filters based on your input.</span><span class="sxs-lookup"><span data-stu-id="ab6f8-109">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="ab6f8-110">Select **Virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="ab6f8-110">Select **Virtual machines**.</span></span>
3. <span data-ttu-id="ab6f8-111">In your list of virtual machines, find and select it.</span><span class="sxs-lookup"><span data-stu-id="ab6f8-111">In your list of virtual machines, find and select it.</span></span>
3. <span data-ttu-id="ab6f8-112">On the virtual machine, click **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="ab6f8-112">On the virtual machine, click **Extensions**.</span></span>
4. <span data-ttu-id="ab6f8-113">From the list, check to see if the Log Analytics extension is enabled or not.</span><span class="sxs-lookup"><span data-stu-id="ab6f8-113">From the list, check to see if the Log Analytics extension is enabled or not.</span></span>  <span data-ttu-id="ab6f8-114">For Linux, the agent is listed as **OMSAgentforLinux** and for Windows, the agent is listed as **MicrosoftMonitoringAgent**.</span><span class="sxs-lookup"><span data-stu-id="ab6f8-114">For Linux, the agent is listed as **OMSAgentforLinux** and for Windows, the agent is listed as **MicrosoftMonitoringAgent**.</span></span>

   ![VM Extension View](./media/log-analytics-azure-vmext-troubleshoot/log-analytics-vmview-extensions.png)

4. <span data-ttu-id="ab6f8-116">Click on the extension to view details.</span><span class="sxs-lookup"><span data-stu-id="ab6f8-116">Click on the extension to view details.</span></span> 

   ![VM Extension Details](./media/log-analytics-azure-vmext-troubleshoot/log-analytics-vmview-extensiondetails.png)

## <a name="troubleshooting-azure-windows-vm-extension"></a><span data-ttu-id="ab6f8-118">Troubleshooting Azure Windows VM extension</span><span class="sxs-lookup"><span data-stu-id="ab6f8-118">Troubleshooting Azure Windows VM extension</span></span>

<span data-ttu-id="ab6f8-119">If the *Microsoft Monitoring Agent* VM extension is not installing or reporting, you can perform the following steps to troubleshoot the issue.</span><span class="sxs-lookup"><span data-stu-id="ab6f8-119">If the *Microsoft Monitoring Agent* VM extension is not installing or reporting, you can perform the following steps to troubleshoot the issue.</span></span>

1. <span data-ttu-id="ab6f8-120">Check if the Azure VM agent is installed and working correctly by using the steps in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span><span class="sxs-lookup"><span data-stu-id="ab6f8-120">Check if the Azure VM agent is installed and working correctly by using the steps in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span></span>
   * <span data-ttu-id="ab6f8-121">You can also review the VM agent log file `C:\WindowsAzure\logs\WaAppAgent.log`</span><span class="sxs-lookup"><span data-stu-id="ab6f8-121">You can also review the VM agent log file `C:\WindowsAzure\logs\WaAppAgent.log`</span></span>
   * <span data-ttu-id="ab6f8-122">If the log does not exist, the VM agent is not installed.</span><span class="sxs-lookup"><span data-stu-id="ab6f8-122">If the log does not exist, the VM agent is not installed.</span></span>
   * [<span data-ttu-id="ab6f8-123">Install the Azure VM Agent</span><span class="sxs-lookup"><span data-stu-id="ab6f8-123">Install the Azure VM Agent</span></span>](log-analytics-quick-collect-azurevm.md#enable-the-log-analytics-vm-extension)
2. <span data-ttu-id="ab6f8-124">Confirm the Microsoft Monitoring Agent extension heartbeat task is running using the following steps:</span><span class="sxs-lookup"><span data-stu-id="ab6f8-124">Confirm the Microsoft Monitoring Agent extension heartbeat task is running using the following steps:</span></span>
   * <span data-ttu-id="ab6f8-125">Log in to the virtual machine</span><span class="sxs-lookup"><span data-stu-id="ab6f8-125">Log in to the virtual machine</span></span>
   * <span data-ttu-id="ab6f8-126">Open task scheduler and find the `update_azureoperationalinsight_agent_heartbeat` task</span><span class="sxs-lookup"><span data-stu-id="ab6f8-126">Open task scheduler and find the `update_azureoperationalinsight_agent_heartbeat` task</span></span>
   * <span data-ttu-id="ab6f8-127">Confirm the task is enabled and is running every one minute</span><span class="sxs-lookup"><span data-stu-id="ab6f8-127">Confirm the task is enabled and is running every one minute</span></span>
   * <span data-ttu-id="ab6f8-128">Check the heartbeat logfile in `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span><span class="sxs-lookup"><span data-stu-id="ab6f8-128">Check the heartbeat logfile in `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span></span>
3. <span data-ttu-id="ab6f8-129">Review the Microsoft Monitoring Agent VM extension log files in `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span><span class="sxs-lookup"><span data-stu-id="ab6f8-129">Review the Microsoft Monitoring Agent VM extension log files in `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span></span>
4. <span data-ttu-id="ab6f8-130">Ensure the virtual machine can run PowerShell scripts</span><span class="sxs-lookup"><span data-stu-id="ab6f8-130">Ensure the virtual machine can run PowerShell scripts</span></span>
5. <span data-ttu-id="ab6f8-131">Ensure permissions on C:\Windows\temp haven’t been changed</span><span class="sxs-lookup"><span data-stu-id="ab6f8-131">Ensure permissions on C:\Windows\temp haven’t been changed</span></span>
6. <span data-ttu-id="ab6f8-132">View the status of the Microsoft Monitoring Agent by typing the following in an elevated PowerShell window on the virtual machine `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span><span class="sxs-lookup"><span data-stu-id="ab6f8-132">View the status of the Microsoft Monitoring Agent by typing the following in an elevated PowerShell window on the virtual machine `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span></span>
7. <span data-ttu-id="ab6f8-133">Review the Microsoft Monitoring Agent setup log files in `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span><span class="sxs-lookup"><span data-stu-id="ab6f8-133">Review the Microsoft Monitoring Agent setup log files in `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span></span>

<span data-ttu-id="ab6f8-134">For more information, see [troubleshooting Windows extensions](../virtual-machines/windows/extensions-oms.md).</span><span class="sxs-lookup"><span data-stu-id="ab6f8-134">For more information, see [troubleshooting Windows extensions](../virtual-machines/windows/extensions-oms.md).</span></span>

## <a name="troubleshooting-linux-vm-extension"></a><span data-ttu-id="ab6f8-135">Troubleshooting Linux VM extension</span><span class="sxs-lookup"><span data-stu-id="ab6f8-135">Troubleshooting Linux VM extension</span></span>
<span data-ttu-id="ab6f8-136">If the *OMS Agent for Linux* VM extension is not installing or reporting, you can perform the following steps to troubleshoot the issue.</span><span class="sxs-lookup"><span data-stu-id="ab6f8-136">If the *OMS Agent for Linux* VM extension is not installing or reporting, you can perform the following steps to troubleshoot the issue.</span></span>

1. <span data-ttu-id="ab6f8-137">If the extension status is *Unknown* check if the Azure VM agent is installed and working correctly by reviewing the VM agent log file `/var/log/waagent.log`</span><span class="sxs-lookup"><span data-stu-id="ab6f8-137">If the extension status is *Unknown* check if the Azure VM agent is installed and working correctly by reviewing the VM agent log file `/var/log/waagent.log`</span></span>
   * <span data-ttu-id="ab6f8-138">If the log does not exist, the VM agent is not installed.</span><span class="sxs-lookup"><span data-stu-id="ab6f8-138">If the log does not exist, the VM agent is not installed.</span></span>
   * [<span data-ttu-id="ab6f8-139">Install the Azure VM Agent on Linux VMs</span><span class="sxs-lookup"><span data-stu-id="ab6f8-139">Install the Azure VM Agent on Linux VMs</span></span>](log-analytics-quick-collect-azurevm.md#enable-the-log-analytics-vm-extension)
2. <span data-ttu-id="ab6f8-140">For other unhealthy statuses, review the OMS Agent for Linux VM extension logs files in `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` and `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span><span class="sxs-lookup"><span data-stu-id="ab6f8-140">For other unhealthy statuses, review the OMS Agent for Linux VM extension logs files in `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` and `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span></span>
3. <span data-ttu-id="ab6f8-141">If the extension status is healthy, but data is not being uploaded review the OMS Agent for Linux log files in `/var/opt/microsoft/omsagent/log/omsagent.log`</span><span class="sxs-lookup"><span data-stu-id="ab6f8-141">If the extension status is healthy, but data is not being uploaded review the OMS Agent for Linux log files in `/var/opt/microsoft/omsagent/log/omsagent.log`</span></span>

<span data-ttu-id="ab6f8-142">For more information, see [troubleshooting Linux extensions](../virtual-machines/linux/extensions-oms.md).</span><span class="sxs-lookup"><span data-stu-id="ab6f8-142">For more information, see [troubleshooting Linux extensions](../virtual-machines/linux/extensions-oms.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab6f8-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="ab6f8-143">Next steps</span></span>

<span data-ttu-id="ab6f8-144">For additional troubleshooting guidance related to the OMS Agent for Linux hosted on computers outside of Azure, see [Troubleshoot Azure Log Analytics Linux Agent](log-analytics-agent-linux-support.md).</span><span class="sxs-lookup"><span data-stu-id="ab6f8-144">For additional troubleshooting guidance related to the OMS Agent for Linux hosted on computers outside of Azure, see [Troubleshoot Azure Log Analytics Linux Agent](log-analytics-agent-linux-support.md).</span></span>  
