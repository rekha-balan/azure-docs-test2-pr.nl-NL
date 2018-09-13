---
title: Azure Security Center Troubleshooting Guide | Microsoft Docs
description: This document helps to troubleshoot issues in Azure Security Center.
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: ''
ms.assetid: 44462de6-2cc5-4672-b1d3-dbb4749a28cd
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/15/2017
ms.author: yurid
ms.openlocfilehash: b055234d198ab174ca11827178705e9a38cbbadb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564218"
---
# <a name="azure-security-center-troubleshooting-guide"></a><span data-ttu-id="2c2e1-103">Azure Security Center Troubleshooting Guide</span><span class="sxs-lookup"><span data-stu-id="2c2e1-103">Azure Security Center Troubleshooting Guide</span></span>
<span data-ttu-id="2c2e1-104">This guide is for information technology (IT) professionals, information security analysts, and cloud administrators whose organizations are using Azure Security Center and need to troubleshoot Security Center related issues.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-104">This guide is for information technology (IT) professionals, information security analysts, and cloud administrators whose organizations are using Azure Security Center and need to troubleshoot Security Center related issues.</span></span>

## <a name="troubleshooting-guide"></a><span data-ttu-id="2c2e1-105">Troubleshooting guide</span><span class="sxs-lookup"><span data-stu-id="2c2e1-105">Troubleshooting guide</span></span>
<span data-ttu-id="2c2e1-106">This guide explains how to troubleshoot Security Center related issues.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-106">This guide explains how to troubleshoot Security Center related issues.</span></span> <span data-ttu-id="2c2e1-107">Most of the troubleshooting done in Security Center will take place by first looking at the [Audit Log](https://azure.microsoft.com/updates/audit-logs-in-azure-preview-portal/) records for the failed component.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-107">Most of the troubleshooting done in Security Center will take place by first looking at the [Audit Log](https://azure.microsoft.com/updates/audit-logs-in-azure-preview-portal/) records for the failed component.</span></span> <span data-ttu-id="2c2e1-108">Through audit logs, you can determine:</span><span class="sxs-lookup"><span data-stu-id="2c2e1-108">Through audit logs, you can determine:</span></span>

* <span data-ttu-id="2c2e1-109">Which operations were taken place</span><span class="sxs-lookup"><span data-stu-id="2c2e1-109">Which operations were taken place</span></span>
* <span data-ttu-id="2c2e1-110">Who initiated the operation</span><span class="sxs-lookup"><span data-stu-id="2c2e1-110">Who initiated the operation</span></span>
* <span data-ttu-id="2c2e1-111">When the operation occurred</span><span class="sxs-lookup"><span data-stu-id="2c2e1-111">When the operation occurred</span></span>
* <span data-ttu-id="2c2e1-112">The status of the operation</span><span class="sxs-lookup"><span data-stu-id="2c2e1-112">The status of the operation</span></span>
* <span data-ttu-id="2c2e1-113">The values of other properties that might help you research the operation</span><span class="sxs-lookup"><span data-stu-id="2c2e1-113">The values of other properties that might help you research the operation</span></span>

<span data-ttu-id="2c2e1-114">The audit log contains all write operations (PUT, POST, DELETE) performed on your resources, however it does not include read operations (GET).</span><span class="sxs-lookup"><span data-stu-id="2c2e1-114">The audit log contains all write operations (PUT, POST, DELETE) performed on your resources, however it does not include read operations (GET).</span></span>

## <a name="troubleshooting-monitoring-agent-installation-in-windows"></a><span data-ttu-id="2c2e1-115">Troubleshooting monitoring agent installation in Windows</span><span class="sxs-lookup"><span data-stu-id="2c2e1-115">Troubleshooting monitoring agent installation in Windows</span></span>
<span data-ttu-id="2c2e1-116">The Security Center monitoring agent is used to perform data collection.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-116">The Security Center monitoring agent is used to perform data collection.</span></span> <span data-ttu-id="2c2e1-117">After data collection is enabled and the agent is correctly installed in the target machine, these processes should be in execution:</span><span class="sxs-lookup"><span data-stu-id="2c2e1-117">After data collection is enabled and the agent is correctly installed in the target machine, these processes should be in execution:</span></span>

* <span data-ttu-id="2c2e1-118">ASMAgentLauncher.exe - Azure Monitoring Agent</span><span class="sxs-lookup"><span data-stu-id="2c2e1-118">ASMAgentLauncher.exe - Azure Monitoring Agent</span></span> 
* <span data-ttu-id="2c2e1-119">ASMMonitoringAgent.exe - Azure Security Monitoring extension</span><span class="sxs-lookup"><span data-stu-id="2c2e1-119">ASMMonitoringAgent.exe - Azure Security Monitoring extension</span></span>
* <span data-ttu-id="2c2e1-120">ASMSoftwareScanner.exe – Azure Scan Manager</span><span class="sxs-lookup"><span data-stu-id="2c2e1-120">ASMSoftwareScanner.exe – Azure Scan Manager</span></span>

<span data-ttu-id="2c2e1-121">The Azure Security Monitoring extension scans for various security relevant configurations and collects security logs from the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-121">The Azure Security Monitoring extension scans for various security relevant configurations and collects security logs from the virtual machine.</span></span> <span data-ttu-id="2c2e1-122">The scan manager will be used as a patch scanner.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-122">The scan manager will be used as a patch scanner.</span></span>

<span data-ttu-id="2c2e1-123">If the installation is successfully performed you should see an entry similar to the one below in the Audit Logs for the target VM:</span><span class="sxs-lookup"><span data-stu-id="2c2e1-123">If the installation is successfully performed you should see an entry similar to the one below in the Audit Logs for the target VM:</span></span>

![Audit Logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig1.png)

<span data-ttu-id="2c2e1-125">You can also obtain more information about the installation process by reading the agent logs, located at *%systemdrive%\windowsazure\logs* (example: C:\WindowsAzure\Logs).</span><span class="sxs-lookup"><span data-stu-id="2c2e1-125">You can also obtain more information about the installation process by reading the agent logs, located at *%systemdrive%\windowsazure\logs* (example: C:\WindowsAzure\Logs).</span></span>

> [!NOTE]
> <span data-ttu-id="2c2e1-126">If the Azure Security Center Agent is misbehaving, you will need to restart the target VM since there is no command to stop and start the agent.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-126">If the Azure Security Center Agent is misbehaving, you will need to restart the target VM since there is no command to stop and start the agent.</span></span>


<span data-ttu-id="2c2e1-127">If you are still having problems with data collection, you can uninstall the agent by following the steps below:</span><span class="sxs-lookup"><span data-stu-id="2c2e1-127">If you are still having problems with data collection, you can uninstall the agent by following the steps below:</span></span>

1. <span data-ttu-id="2c2e1-128">From the **Azure Portal**, select the virtual machine that is experience data collection issues and click **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-128">From the **Azure Portal**, select the virtual machine that is experience data collection issues and click **Extensions**.</span></span>
2. <span data-ttu-id="2c2e1-129">Right click in **Microsoft.Azure.Security.Monitoring** and select click **Uninstall**.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-129">Right click in **Microsoft.Azure.Security.Monitoring** and select click **Uninstall**.</span></span>

![Removing agent](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig4.png)

<span data-ttu-id="2c2e1-131">The Azure Security Monitoring extension should automatically reinstall itself within several minutes.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-131">The Azure Security Monitoring extension should automatically reinstall itself within several minutes.</span></span>

## <a name="troubleshooting-monitoring-agent-installation-in-linux"></a><span data-ttu-id="2c2e1-132">Troubleshooting monitoring agent installation in Linux</span><span class="sxs-lookup"><span data-stu-id="2c2e1-132">Troubleshooting monitoring agent installation in Linux</span></span>
<span data-ttu-id="2c2e1-133">When troubleshooting VM Agent installation in a Linux system you should ensure that the extension was downloaded to /var/lib/waagent/.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-133">When troubleshooting VM Agent installation in a Linux system you should ensure that the extension was downloaded to /var/lib/waagent/.</span></span> <span data-ttu-id="2c2e1-134">You can run the command below to verify if it was installed:</span><span class="sxs-lookup"><span data-stu-id="2c2e1-134">You can run the command below to verify if it was installed:</span></span>

`cat /var/log/waagent.log` 

<span data-ttu-id="2c2e1-135">The other log files that you can review for troubleshooting purpose are:</span><span class="sxs-lookup"><span data-stu-id="2c2e1-135">The other log files that you can review for troubleshooting purpose are:</span></span> 

* <span data-ttu-id="2c2e1-136">/var/log/mdsd.err</span><span class="sxs-lookup"><span data-stu-id="2c2e1-136">/var/log/mdsd.err</span></span>
* <span data-ttu-id="2c2e1-137">/var/log/azure/</span><span class="sxs-lookup"><span data-stu-id="2c2e1-137">/var/log/azure/</span></span>

<span data-ttu-id="2c2e1-138">In a working system you should see a connection to the mdsd process on TCP 29130.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-138">In a working system you should see a connection to the mdsd process on TCP 29130.</span></span> <span data-ttu-id="2c2e1-139">This is the syslog communicating with the mdsd process.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-139">This is the syslog communicating with the mdsd process.</span></span> <span data-ttu-id="2c2e1-140">You can validate this behavior by running the command below:</span><span class="sxs-lookup"><span data-stu-id="2c2e1-140">You can validate this behavior by running the command below:</span></span>

`netstat -plantu | grep 29130`

## <a name="troubleshooting-endpoint-protection-not-working-properly"></a><span data-ttu-id="2c2e1-141">Troubleshooting endpoint protection not working properly</span><span class="sxs-lookup"><span data-stu-id="2c2e1-141">Troubleshooting endpoint protection not working properly</span></span>

<span data-ttu-id="2c2e1-142">The guest agent is the parent process of everything the [Microsoft Antimalware](../security/azure-security-antimalware.md) extension does.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-142">The guest agent is the parent process of everything the [Microsoft Antimalware](../security/azure-security-antimalware.md) extension does.</span></span> <span data-ttu-id="2c2e1-143">When the guest agent process fails, the Microsoft Antimalware that runs as a child process of the guest agent may also fail.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-143">When the guest agent process fails, the Microsoft Antimalware that runs as a child process of the guest agent may also fail.</span></span>  <span data-ttu-id="2c2e1-144">In scenarios like that is recommended to verify the following options:</span><span class="sxs-lookup"><span data-stu-id="2c2e1-144">In scenarios like that is recommended to verify the following options:</span></span>

- <span data-ttu-id="2c2e1-145">If the target VM is a custom image and the creator of the VM never installed guest agent.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-145">If the target VM is a custom image and the creator of the VM never installed guest agent.</span></span>
- <span data-ttu-id="2c2e1-146">If the target is a Linux VM instead of a Windows VM then installing the Windows version of the antimalware extension on a Linux VM will fail.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-146">If the target is a Linux VM instead of a Windows VM then installing the Windows version of the antimalware extension on a Linux VM will fail.</span></span> <span data-ttu-id="2c2e1-147">The Linux guest agent has specific requirements in terms of OS version and required packages, and if those requirements are not met the VM agent will not work there either.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-147">The Linux guest agent has specific requirements in terms of OS version and required packages, and if those requirements are not met the VM agent will not work there either.</span></span> 
- <span data-ttu-id="2c2e1-148">If the VM was created with an old version of guest agent.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-148">If the VM was created with an old version of guest agent.</span></span> <span data-ttu-id="2c2e1-149">If it was, you should be aware that some old agents could not auto-update itself to the newer version and this could lead to this problem.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-149">If it was, you should be aware that some old agents could not auto-update itself to the newer version and this could lead to this problem.</span></span> <span data-ttu-id="2c2e1-150">Always use the latest version of guest agent if creating your own images.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-150">Always use the latest version of guest agent if creating your own images.</span></span>
- <span data-ttu-id="2c2e1-151">Some third-party administration software may disable the guest agent, or block access to certain file locations.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-151">Some third-party administration software may disable the guest agent, or block access to certain file locations.</span></span> <span data-ttu-id="2c2e1-152">If you have third-party installed on your VM, make sure that the agent is on the exclusion list.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-152">If you have third-party installed on your VM, make sure that the agent is on the exclusion list.</span></span>
- <span data-ttu-id="2c2e1-153">Certain firewall settings or Network Security Group (NSG) may block network traffic to and from guest agent.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-153">Certain firewall settings or Network Security Group (NSG) may block network traffic to and from guest agent.</span></span>
- <span data-ttu-id="2c2e1-154">Certain Access Control List (ACL) may prevent disk access.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-154">Certain Access Control List (ACL) may prevent disk access.</span></span>
- <span data-ttu-id="2c2e1-155">Lack of disk space can block the guest agent from functioning properly.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-155">Lack of disk space can block the guest agent from functioning properly.</span></span> 

<span data-ttu-id="2c2e1-156">By default the Microsoft Antimalware User Interface is disabled, read [Enabling Microsoft Antimalware User Interface on Azure Resource Manager VMs Post Deployment](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/09/enabling-microsoft-antimalware-user-interface-post-deployment/) for more information on how to enable it if you need.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-156">By default the Microsoft Antimalware User Interface is disabled, read [Enabling Microsoft Antimalware User Interface on Azure Resource Manager VMs Post Deployment](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/09/enabling-microsoft-antimalware-user-interface-post-deployment/) for more information on how to enable it if you need.</span></span>

## <a name="troubleshooting-problems-loading-the-dashboard"></a><span data-ttu-id="2c2e1-157">Troubleshooting problems loading the dashboard</span><span class="sxs-lookup"><span data-stu-id="2c2e1-157">Troubleshooting problems loading the dashboard</span></span>

<span data-ttu-id="2c2e1-158">If you experience issues loading the Security Center dashboard, ensure that the user that registers the subscription to Security Center (i.e. the first user one who opened Security Center with the subscription) and the user who would like to turn on data collection should be *Owner* or *Contributor* on the subscription.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-158">If you experience issues loading the Security Center dashboard, ensure that the user that registers the subscription to Security Center (i.e. the first user one who opened Security Center with the subscription) and the user who would like to turn on data collection should be *Owner* or *Contributor* on the subscription.</span></span> <span data-ttu-id="2c2e1-159">From that moment on also users with *Reader* on the subscription can see the dashboard/alerts/recommendation/policy.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-159">From that moment on also users with *Reader* on the subscription can see the dashboard/alerts/recommendation/policy.</span></span>

## <a name="contacting-microsoft-support"></a><span data-ttu-id="2c2e1-160">Contacting Microsoft Support</span><span class="sxs-lookup"><span data-stu-id="2c2e1-160">Contacting Microsoft Support</span></span>
<span data-ttu-id="2c2e1-161">Some issues can be identified using the guidelines provided in this article, others you can also find documented at the Security Center public [Forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureSecurityCenter).</span><span class="sxs-lookup"><span data-stu-id="2c2e1-161">Some issues can be identified using the guidelines provided in this article, others you can also find documented at the Security Center public [Forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureSecurityCenter).</span></span> <span data-ttu-id="2c2e1-162">However if you need further troubleshooting, you can open a new support request using **Azure Portal** as shown below:</span><span class="sxs-lookup"><span data-stu-id="2c2e1-162">However if you need further troubleshooting, you can open a new support request using **Azure Portal** as shown below:</span></span> 

![Microsoft Support](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig2.png)

## <a name="see-also"></a><span data-ttu-id="2c2e1-164">See also</span><span class="sxs-lookup"><span data-stu-id="2c2e1-164">See also</span></span>
<span data-ttu-id="2c2e1-165">In this document, you learned how to configure security policies in Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-165">In this document, you learned how to configure security policies in Azure Security Center.</span></span> <span data-ttu-id="2c2e1-166">To learn more about Azure Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="2c2e1-166">To learn more about Azure Security Center, see the following:</span></span>

* <span data-ttu-id="2c2e1-167">[Azure Security Center Planning and Operations Guide](security-center-planning-and-operations-guide.md) — Learn how to plan and understand the design considerations to adopt Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-167">[Azure Security Center Planning and Operations Guide](security-center-planning-and-operations-guide.md) — Learn how to plan and understand the design considerations to adopt Azure Security Center.</span></span>
* <span data-ttu-id="2c2e1-168">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources</span><span class="sxs-lookup"><span data-stu-id="2c2e1-168">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources</span></span>
* <span data-ttu-id="2c2e1-169">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts</span><span class="sxs-lookup"><span data-stu-id="2c2e1-169">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts</span></span>
* <span data-ttu-id="2c2e1-170">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span><span class="sxs-lookup"><span data-stu-id="2c2e1-170">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="2c2e1-171">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service</span><span class="sxs-lookup"><span data-stu-id="2c2e1-171">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service</span></span>
* <span data-ttu-id="2c2e1-172">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance</span><span class="sxs-lookup"><span data-stu-id="2c2e1-172">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance</span></span>




