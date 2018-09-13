---
title: Connecting your security products to the Operations Management Suite (OMS) Security and Audit Solution | Microsoft Docs
description: This document helps you to connect your security products to Operations Management Suite Security and Audit Solution using Common Event Format.
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: ''
ms.assetid: 46eee484-e078-4bad-8c89-c88a3508f6aa
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 82d460e1ba2b72c85dc951ed4d901c5527f9703a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670375"
---
# <a name="connecting-your-security-products-to-the-operations-management-suite-oms-security-and-audit-solution"></a><span data-ttu-id="8458a-103">Connecting your security products to the Operations Management Suite (OMS) Security and Audit Solution</span><span class="sxs-lookup"><span data-stu-id="8458a-103">Connecting your security products to the Operations Management Suite (OMS) Security and Audit Solution</span></span> 
<span data-ttu-id="8458a-104">This document helps you connect your security products into the OMS Security and Audit Solution.</span><span class="sxs-lookup"><span data-stu-id="8458a-104">This document helps you connect your security products into the OMS Security and Audit Solution.</span></span> <span data-ttu-id="8458a-105">The following sources are supported:</span><span class="sxs-lookup"><span data-stu-id="8458a-105">The following sources are supported:</span></span>

- <span data-ttu-id="8458a-106">Common Event Format (CEF) events</span><span class="sxs-lookup"><span data-stu-id="8458a-106">Common Event Format (CEF) events</span></span>
- <span data-ttu-id="8458a-107">Cisco ASA events</span><span class="sxs-lookup"><span data-stu-id="8458a-107">Cisco ASA events</span></span>


## <a name="what-is-cef"></a><span data-ttu-id="8458a-108">What is CEF?</span><span class="sxs-lookup"><span data-stu-id="8458a-108">What is CEF?</span></span>
<span data-ttu-id="8458a-109">Common Event Format (CEF) is an industry standard format on top of Syslog messages, used by many security vendors to allow event interoperability among different platforms.</span><span class="sxs-lookup"><span data-stu-id="8458a-109">Common Event Format (CEF) is an industry standard format on top of Syslog messages, used by many security vendors to allow event interoperability among different platforms.</span></span> <span data-ttu-id="8458a-110">OMS Security and Audit Solution support data ingestion using CEF, which enables you to connect your security products with OMS Security.</span><span class="sxs-lookup"><span data-stu-id="8458a-110">OMS Security and Audit Solution support data ingestion using CEF, which enables you to connect your security products with OMS Security.</span></span> 

<span data-ttu-id="8458a-111">By connecting your data source to OMS, you are able to take advantage of the following capabilities that are part of this platform:</span><span class="sxs-lookup"><span data-stu-id="8458a-111">By connecting your data source to OMS, you are able to take advantage of the following capabilities that are part of this platform:</span></span>

- <span data-ttu-id="8458a-112">Search & Correlation</span><span class="sxs-lookup"><span data-stu-id="8458a-112">Search & Correlation</span></span>
- <span data-ttu-id="8458a-113">Auditing</span><span class="sxs-lookup"><span data-stu-id="8458a-113">Auditing</span></span>
- <span data-ttu-id="8458a-114">Alert</span><span class="sxs-lookup"><span data-stu-id="8458a-114">Alert</span></span>
- <span data-ttu-id="8458a-115">Threat Intelligence</span><span class="sxs-lookup"><span data-stu-id="8458a-115">Threat Intelligence</span></span>
- <span data-ttu-id="8458a-116">Notable Issues</span><span class="sxs-lookup"><span data-stu-id="8458a-116">Notable Issues</span></span>

## <a name="collection-of-security-solution-logs"></a><span data-ttu-id="8458a-117">Collection of security solution logs</span><span class="sxs-lookup"><span data-stu-id="8458a-117">Collection of security solution logs</span></span>

<span data-ttu-id="8458a-118">OMS Security supports collection of logs using CEF over Syslogs and [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) logs.</span><span class="sxs-lookup"><span data-stu-id="8458a-118">OMS Security supports collection of logs using CEF over Syslogs and [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) logs.</span></span> <span data-ttu-id="8458a-119">In this example, the source (computer that generates the logs) is a Linux computer running syslog-ng daemon and the target is OMS Security.</span><span class="sxs-lookup"><span data-stu-id="8458a-119">In this example, the source (computer that generates the logs) is a Linux computer running syslog-ng daemon and the target is OMS Security.</span></span> <span data-ttu-id="8458a-120">To prepare the Linux computer you will need to perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="8458a-120">To prepare the Linux computer you will need to perform the following tasks:</span></span>

- <span data-ttu-id="8458a-121">Download the OMS Agent for Linux, version 1.2.0-25 or above.</span><span class="sxs-lookup"><span data-stu-id="8458a-121">Download the OMS Agent for Linux, version 1.2.0-25 or above.</span></span>
- <span data-ttu-id="8458a-122">Follow the section **Quick Install Guide** from [this article](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) to install and onboard the agent to your workspace.</span><span class="sxs-lookup"><span data-stu-id="8458a-122">Follow the section **Quick Install Guide** from [this article](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) to install and onboard the agent to your workspace.</span></span>

<span data-ttu-id="8458a-123">Typically, the agent is installed on a different computer from the one on which the logs are generated.</span><span class="sxs-lookup"><span data-stu-id="8458a-123">Typically, the agent is installed on a different computer from the one on which the logs are generated.</span></span> <span data-ttu-id="8458a-124">Forwarding the logs to the agent machine will usually require the following steps:</span><span class="sxs-lookup"><span data-stu-id="8458a-124">Forwarding the logs to the agent machine will usually require the following steps:</span></span>

- <span data-ttu-id="8458a-125">Configure the logging product/machine to forward the required events to the syslog daemon (rsyslog or syslog-ng) on the agent machine.</span><span class="sxs-lookup"><span data-stu-id="8458a-125">Configure the logging product/machine to forward the required events to the syslog daemon (rsyslog or syslog-ng) on the agent machine.</span></span>
- <span data-ttu-id="8458a-126">Enable the syslog daemon on the agent machine to receive messages from a remote system.</span><span class="sxs-lookup"><span data-stu-id="8458a-126">Enable the syslog daemon on the agent machine to receive messages from a remote system.</span></span>

<span data-ttu-id="8458a-127">On the agent machine, the events need to be sent from the syslog daemon to local UDP port 25226.</span><span class="sxs-lookup"><span data-stu-id="8458a-127">On the agent machine, the events need to be sent from the syslog daemon to local UDP port 25226.</span></span> <span data-ttu-id="8458a-128">The agent is listening for incoming events on this port.</span><span class="sxs-lookup"><span data-stu-id="8458a-128">The agent is listening for incoming events on this port.</span></span> <span data-ttu-id="8458a-129">The following is an example configuration for sending all events from the local system to the agent (you can modify the configuration to fit your local settings):</span><span class="sxs-lookup"><span data-stu-id="8458a-129">The following is an example configuration for sending all events from the local system to the agent (you can modify the configuration to fit your local settings):</span></span>

1. <span data-ttu-id="8458a-130">Open the terminal window, and go to the directory */etc/syslog-ng/*</span><span class="sxs-lookup"><span data-stu-id="8458a-130">Open the terminal window, and go to the directory */etc/syslog-ng/*</span></span> 
2. <span data-ttu-id="8458a-131">Create a new file *security-config-omsagent.conf* and add the following content:  OMS_facility = local4</span><span class="sxs-lookup"><span data-stu-id="8458a-131">Create a new file *security-config-omsagent.conf* and add the following content:  OMS_facility = local4</span></span>
    
    <span data-ttu-id="8458a-132">filter f_local4_oms { facility(local4); };</span><span class="sxs-lookup"><span data-stu-id="8458a-132">filter f_local4_oms { facility(local4); };</span></span>

    <span data-ttu-id="8458a-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span><span class="sxs-lookup"><span data-stu-id="8458a-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span></span>

    <span data-ttu-id="8458a-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span><span class="sxs-lookup"><span data-stu-id="8458a-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span></span>
    
3. <span data-ttu-id="8458a-135">Download the file *security_events.conf* and place at */etc/opt/microsoft/omsagent/conf/omsagent.d/* in the OMS Agent computer.</span><span class="sxs-lookup"><span data-stu-id="8458a-135">Download the file *security_events.conf* and place at */etc/opt/microsoft/omsagent/conf/omsagent.d/* in the OMS Agent computer.</span></span>
4. <span data-ttu-id="8458a-136">Type the command below to restart the syslog daemon:  *For syslog-ng run:*</span><span class="sxs-lookup"><span data-stu-id="8458a-136">Type the command below to restart the syslog daemon:  *For syslog-ng run:*</span></span>
    
    ```
    sudo service rsyslog restart
    ```

    <span data-ttu-id="8458a-137">*For rsyslog run:*</span><span class="sxs-lookup"><span data-stu-id="8458a-137">*For rsyslog run:*</span></span>
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. <span data-ttu-id="8458a-138">Type the command below to restart the OMS Agent:</span><span class="sxs-lookup"><span data-stu-id="8458a-138">Type the command below to restart the OMS Agent:</span></span>

    <span data-ttu-id="8458a-139">*For syslog-ng run:*</span><span class="sxs-lookup"><span data-stu-id="8458a-139">*For syslog-ng run:*</span></span>
    
    ```
    sudo service omsagent restart
    ```

    <span data-ttu-id="8458a-140">*For rsyslog run:*</span><span class="sxs-lookup"><span data-stu-id="8458a-140">*For rsyslog run:*</span></span>
    
    ```
    systemctl restart omsagent
    ```
6. <span data-ttu-id="8458a-141">Type the command below and review the result to confirm that there are no errors in the OMS Agent log:</span><span class="sxs-lookup"><span data-stu-id="8458a-141">Type the command below and review the result to confirm that there are no errors in the OMS Agent log:</span></span>

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a><span data-ttu-id="8458a-142">Reviewing collected security events</span><span class="sxs-lookup"><span data-stu-id="8458a-142">Reviewing collected security events</span></span>

<span data-ttu-id="8458a-143">After the configuration is over, the security event will start to be ingested by OMS Security.</span><span class="sxs-lookup"><span data-stu-id="8458a-143">After the configuration is over, the security event will start to be ingested by OMS Security.</span></span> <span data-ttu-id="8458a-144">To visualize those events, open the Log Search, type the command *Type=CommonSecurityLog* in the search field and press ENTER.</span><span class="sxs-lookup"><span data-stu-id="8458a-144">To visualize those events, open the Log Search, type the command *Type=CommonSecurityLog* in the search field and press ENTER.</span></span> <span data-ttu-id="8458a-145">The following example shows the result of this command, notice that in this case OMS Security already ingested security logs from multiple vendors:</span><span class="sxs-lookup"><span data-stu-id="8458a-145">The following example shows the result of this command, notice that in this case OMS Security already ingested security logs from multiple vendors:</span></span>
   
![OMS Security and Audit Baseline Assessment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/operations-management-suite/media/oms-security-connect-products/oms-security-connect-products-fig1.png)

<span data-ttu-id="8458a-147">You can refine this search for one single vendor, for example, to visualize online Cisco logs, type: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span><span class="sxs-lookup"><span data-stu-id="8458a-147">You can refine this search for one single vendor, for example, to visualize online Cisco logs, type: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span></span> <span data-ttu-id="8458a-148">The “CommonSecurityLog” has predefined fields for any CEF header including the basic extensios, while any other extension whether it’s “Custom Extension” or not, will be inserted into "AdditionalExtensions" field.</span><span class="sxs-lookup"><span data-stu-id="8458a-148">The “CommonSecurityLog” has predefined fields for any CEF header including the basic extensios, while any other extension whether it’s “Custom Extension” or not, will be inserted into "AdditionalExtensions" field.</span></span> <span data-ttu-id="8458a-149">You can use the Custom Fields feature to get dedicated fields from it.</span><span class="sxs-lookup"><span data-stu-id="8458a-149">You can use the Custom Fields feature to get dedicated fields from it.</span></span> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="8458a-150">Accessing computers missing baseline assessment</span><span class="sxs-lookup"><span data-stu-id="8458a-150">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="8458a-151">OMS supports the domain member baseline profile on Windows Server 2008 R2 up to Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="8458a-151">OMS supports the domain member baseline profile on Windows Server 2008 R2 up to Windows Server 2012 R2.</span></span> <span data-ttu-id="8458a-152">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span><span class="sxs-lookup"><span data-stu-id="8458a-152">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="8458a-153">All other operating systems scanned via OMS Security and Audit baseline assessment appear under the **Computers missing baseline assessment** section.</span><span class="sxs-lookup"><span data-stu-id="8458a-153">All other operating systems scanned via OMS Security and Audit baseline assessment appear under the **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="8458a-154">See also</span><span class="sxs-lookup"><span data-stu-id="8458a-154">See also</span></span>
<span data-ttu-id="8458a-155">In this document, you learned how to connect your CEF solution to OMS.</span><span class="sxs-lookup"><span data-stu-id="8458a-155">In this document, you learned how to connect your CEF solution to OMS.</span></span> <span data-ttu-id="8458a-156">To learn more about OMS Security, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="8458a-156">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="8458a-157">Operations Management Suite (OMS) overview</span><span class="sxs-lookup"><span data-stu-id="8458a-157">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="8458a-158">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span><span class="sxs-lookup"><span data-stu-id="8458a-158">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="8458a-159">Monitoring Resources in Operations Management Suite Security and Audit Solution</span><span class="sxs-lookup"><span data-stu-id="8458a-159">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)


