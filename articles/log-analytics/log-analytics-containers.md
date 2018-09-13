---
title: Containers solution in Azure Log Analytics | Microsoft Docs
description: The Containers solution in Log Analytics helps you view and manage your Docker and Windows container hosts in a single location.
services: log-analytics
documentationcenter: ''
author: bandersmsft
manager: carmonm
editor: ''
ms.assetid: e1e4b52b-92d5-4bfa-8a09-ff8c6b5a9f78
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: banders
ms.openlocfilehash: 5aa803ef4200c17ccd90252fa963437ff948bb3c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661654"
---
# <a name="containers-preview-solution-log-analytics"></a><span data-ttu-id="23394-103">Containers (Preview) solution Log Analytics</span><span class="sxs-lookup"><span data-stu-id="23394-103">Containers (Preview) solution Log Analytics</span></span>
<span data-ttu-id="23394-104">This article describes how to set up and use the Containers solution in Log Analytics, which helps you view and manage your Docker and Windows container hosts in a single location.</span><span class="sxs-lookup"><span data-stu-id="23394-104">This article describes how to set up and use the Containers solution in Log Analytics, which helps you view and manage your Docker and Windows container hosts in a single location.</span></span> <span data-ttu-id="23394-105">Docker is a software virtualization system used to create containers that automate software deployment to their IT infrastructure.</span><span class="sxs-lookup"><span data-stu-id="23394-105">Docker is a software virtualization system used to create containers that automate software deployment to their IT infrastructure.</span></span>

<span data-ttu-id="23394-106">With the solution, you can see which containers are running on your container hosts and what images are running in the containers.</span><span class="sxs-lookup"><span data-stu-id="23394-106">With the solution, you can see which containers are running on your container hosts and what images are running in the containers.</span></span> <span data-ttu-id="23394-107">You can view detailed audit information showing commands used with containers.</span><span class="sxs-lookup"><span data-stu-id="23394-107">You can view detailed audit information showing commands used with containers.</span></span> <span data-ttu-id="23394-108">And, you can troubleshoot containers by viewing and searching centralized logs without having to remotely view Docker or Windows hosts.</span><span class="sxs-lookup"><span data-stu-id="23394-108">And, you can troubleshoot containers by viewing and searching centralized logs without having to remotely view Docker or Windows hosts.</span></span> <span data-ttu-id="23394-109">You can find containers that may be noisy and consuming excess resources on a host.</span><span class="sxs-lookup"><span data-stu-id="23394-109">You can find containers that may be noisy and consuming excess resources on a host.</span></span> <span data-ttu-id="23394-110">And, you can view centralized CPU, memory, storage, and network usage and performance information for containers.</span><span class="sxs-lookup"><span data-stu-id="23394-110">And, you can view centralized CPU, memory, storage, and network usage and performance information for containers.</span></span> <span data-ttu-id="23394-111">On computers running Windows, you can centralize and compare logs from Windows Server, Hyper-V, and Docker containers.</span><span class="sxs-lookup"><span data-stu-id="23394-111">On computers running Windows, you can centralize and compare logs from Windows Server, Hyper-V, and Docker containers.</span></span>

<span data-ttu-id="23394-112">The following diagram shows the relationships between various container hosts and agents with OMS.</span><span class="sxs-lookup"><span data-stu-id="23394-112">The following diagram shows the relationships between various container hosts and agents with OMS.</span></span>

![Containers diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/containers-diagram.png)

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="23394-114">Installing and configuring the solution</span><span class="sxs-lookup"><span data-stu-id="23394-114">Installing and configuring the solution</span></span>
<span data-ttu-id="23394-115">Use the following information to install and configure the solution.</span><span class="sxs-lookup"><span data-stu-id="23394-115">Use the following information to install and configure the solution.</span></span>

<span data-ttu-id="23394-116">Add the Containers solution to your OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="23394-116">Add the Containers solution to your OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="23394-117">There are a few ways to install and use Docker with OMS:</span><span class="sxs-lookup"><span data-stu-id="23394-117">There are a few ways to install and use Docker with OMS:</span></span>

* <span data-ttu-id="23394-118">On supported Linux operating systems, install and run Docker and then install and configure the OMS Agent for Linux.</span><span class="sxs-lookup"><span data-stu-id="23394-118">On supported Linux operating systems, install and run Docker and then install and configure the OMS Agent for Linux.</span></span>
* <span data-ttu-id="23394-119">On CoreOS, you cannot run the OMS Agent for Linux.</span><span class="sxs-lookup"><span data-stu-id="23394-119">On CoreOS, you cannot run the OMS Agent for Linux.</span></span> <span data-ttu-id="23394-120">Instead, you run a containerized version of the OMS Agent for Linux.</span><span class="sxs-lookup"><span data-stu-id="23394-120">Instead, you run a containerized version of the OMS Agent for Linux.</span></span>
* <span data-ttu-id="23394-121">On Windows Server 2016 and Windows 10, install the Docker Engine and client then connect an agent to gather information and send it to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="23394-121">On Windows Server 2016 and Windows 10, install the Docker Engine and client then connect an agent to gather information and send it to Log Analytics.</span></span>


<span data-ttu-id="23394-122">You can review the supported Docker and Linux operating system versions for your container host on [GitHub](https://github.com/Microsoft/OMS-docker).</span><span class="sxs-lookup"><span data-stu-id="23394-122">You can review the supported Docker and Linux operating system versions for your container host on [GitHub](https://github.com/Microsoft/OMS-docker).</span></span>

<span data-ttu-id="23394-123">Review the [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article for additional information about how to install and configure your Docker Engines on computers running Windows.</span><span class="sxs-lookup"><span data-stu-id="23394-123">Review the [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article for additional information about how to install and configure your Docker Engines on computers running Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23394-124">Docker must be running **before** you install the [OMS Agent for Linux](log-analytics-linux-agents.md) on your container hosts.</span><span class="sxs-lookup"><span data-stu-id="23394-124">Docker must be running **before** you install the [OMS Agent for Linux](log-analytics-linux-agents.md) on your container hosts.</span></span> <span data-ttu-id="23394-125">If you've already installed the agent before installing Docker, you'll need to reinstall the OMS Agent for Linux.</span><span class="sxs-lookup"><span data-stu-id="23394-125">If you've already installed the agent before installing Docker, you'll need to reinstall the OMS Agent for Linux.</span></span> <span data-ttu-id="23394-126">For more information about Docker, see the [Docker website](https://www.docker.com).</span><span class="sxs-lookup"><span data-stu-id="23394-126">For more information about Docker, see the [Docker website](https://www.docker.com).</span></span>
>
>

<span data-ttu-id="23394-127">You need the following settings configured on your container hosts before you can monitor containers.</span><span class="sxs-lookup"><span data-stu-id="23394-127">You need the following settings configured on your container hosts before you can monitor containers.</span></span>

## <a name="configure-settings-for-a-linux-container-host"></a><span data-ttu-id="23394-128">Configure settings for a Linux container host</span><span class="sxs-lookup"><span data-stu-id="23394-128">Configure settings for a Linux container host</span></span>

<span data-ttu-id="23394-129">The following x64 Linux distributions are supported as container hosts:</span><span class="sxs-lookup"><span data-stu-id="23394-129">The following x64 Linux distributions are supported as container hosts:</span></span>

- <span data-ttu-id="23394-130">Ubuntu 14.04 LTS, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="23394-130">Ubuntu 14.04 LTS, 16.04 LTS</span></span>
- <span data-ttu-id="23394-131">CoreOS(stable)</span><span class="sxs-lookup"><span data-stu-id="23394-131">CoreOS(stable)</span></span>
- <span data-ttu-id="23394-132">Amazon Linux 2016.09.0</span><span class="sxs-lookup"><span data-stu-id="23394-132">Amazon Linux 2016.09.0</span></span>
- <span data-ttu-id="23394-133">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="23394-133">openSUSE 13.2</span></span>
- <span data-ttu-id="23394-134">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="23394-134">CentOS 7</span></span>
- <span data-ttu-id="23394-135">SLES 12</span><span class="sxs-lookup"><span data-stu-id="23394-135">SLES 12</span></span>
- <span data-ttu-id="23394-136">RHEL 7.2</span><span class="sxs-lookup"><span data-stu-id="23394-136">RHEL 7.2</span></span>

<span data-ttu-id="23394-137">After you've installed Docker, use the following settings for your container host to configure the agent for use with Docker.</span><span class="sxs-lookup"><span data-stu-id="23394-137">After you've installed Docker, use the following settings for your container host to configure the agent for use with Docker.</span></span> <span data-ttu-id="23394-138">You'll need your [OMS workspace ID and key](log-analytics-linux-agents.md).</span><span class="sxs-lookup"><span data-stu-id="23394-138">You'll need your [OMS workspace ID and key](log-analytics-linux-agents.md).</span></span>


### <a name="for-all-linux-container-hosts-except-coreos"></a><span data-ttu-id="23394-139">For all Linux container hosts except CoreOS</span><span class="sxs-lookup"><span data-stu-id="23394-139">For all Linux container hosts except CoreOS</span></span>

- <span data-ttu-id="23394-140">Follow the instructions at  [Steps to install the OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md).</span><span class="sxs-lookup"><span data-stu-id="23394-140">Follow the instructions at  [Steps to install the OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md).</span></span>

### <a name="for-all-linux-container-hosts-including-coreos"></a><span data-ttu-id="23394-141">For all Linux container hosts including CoreOS</span><span class="sxs-lookup"><span data-stu-id="23394-141">For all Linux container hosts including CoreOS</span></span>

<span data-ttu-id="23394-142">Start the OMS container that you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="23394-142">Start the OMS container that you want to monitor.</span></span> <span data-ttu-id="23394-143">Modify and use the following example.</span><span class="sxs-lookup"><span data-stu-id="23394-143">Modify and use the following example.</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-to-one-in-a-container"></a><span data-ttu-id="23394-144">Switching from using an installed Linux agent to one in a container</span><span class="sxs-lookup"><span data-stu-id="23394-144">Switching from using an installed Linux agent to one in a container</span></span>
<span data-ttu-id="23394-145">If you previously used the directly-installed agent and want to instead use an agent running in a container, you must first remove OMSAgent.</span><span class="sxs-lookup"><span data-stu-id="23394-145">If you previously used the directly-installed agent and want to instead use an agent running in a container, you must first remove OMSAgent.</span></span> <span data-ttu-id="23394-146">See [Steps to install the OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md).</span><span class="sxs-lookup"><span data-stu-id="23394-146">See [Steps to install the OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md).</span></span>

## <a name="supported-windows-versions"></a><span data-ttu-id="23394-147">Supported Windows versions</span><span class="sxs-lookup"><span data-stu-id="23394-147">Supported Windows versions</span></span>

- <span data-ttu-id="23394-148">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="23394-148">Windows Server 2016</span></span>
- <span data-ttu-id="23394-149">Windows 10 Anniversary Edition (Professional or Enterprise)</span><span class="sxs-lookup"><span data-stu-id="23394-149">Windows 10 Anniversary Edition (Professional or Enterprise)</span></span>

### <a name="docker-versions-supported-on-windows"></a><span data-ttu-id="23394-150">Docker versions supported on Windows</span><span class="sxs-lookup"><span data-stu-id="23394-150">Docker versions supported on Windows</span></span>

- <span data-ttu-id="23394-151">Docker 1.12 – 1.13</span><span class="sxs-lookup"><span data-stu-id="23394-151">Docker 1.12 – 1.13</span></span>

### <a name="preparation-before-installing-agents"></a><span data-ttu-id="23394-152">Preparation before installing agents</span><span class="sxs-lookup"><span data-stu-id="23394-152">Preparation before installing agents</span></span>

<span data-ttu-id="23394-153">Before you install agents on computers running Windows, you need to configure the Docker service.</span><span class="sxs-lookup"><span data-stu-id="23394-153">Before you install agents on computers running Windows, you need to configure the Docker service.</span></span> <span data-ttu-id="23394-154">The configuration allows the Windows agent or the Log Analytics virtual machine extension to use the Docker TCP socket so that the agents can access the Docker daemon remotely and to capture data for monitoring.</span><span class="sxs-lookup"><span data-stu-id="23394-154">The configuration allows the Windows agent or the Log Analytics virtual machine extension to use the Docker TCP socket so that the agents can access the Docker daemon remotely and to capture data for monitoring.</span></span>

<span data-ttu-id="23394-155">Performance data is not supported on computers running Windows.</span><span class="sxs-lookup"><span data-stu-id="23394-155">Performance data is not supported on computers running Windows.</span></span>

<span data-ttu-id="23394-156">For more information about configuring the Docker daemon with Windows, see [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span><span class="sxs-lookup"><span data-stu-id="23394-156">For more information about configuring the Docker daemon with Windows, see [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span></span>

#### <a name="to-start-docker-and-verify-its-configuration"></a><span data-ttu-id="23394-157">To start Docker and verify its configuration</span><span class="sxs-lookup"><span data-stu-id="23394-157">To start Docker and verify its configuration</span></span>

1.  <span data-ttu-id="23394-158">In Windows PowerShell, enable TCP pipe and named pipe.</span><span class="sxs-lookup"><span data-stu-id="23394-158">In Windows PowerShell, enable TCP pipe and named pipe.</span></span>

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd -H npipe:// -H 0.0.0.0:2375 --register-service
    Start-Service docker
    ```

2.  <span data-ttu-id="23394-159">Verify your configuration with netstat.</span><span class="sxs-lookup"><span data-stu-id="23394-159">Verify your configuration with netstat.</span></span> <span data-ttu-id="23394-160">You should see port 2375.</span><span class="sxs-lookup"><span data-stu-id="23394-160">You should see port 2375.</span></span>

    ```
    PS C:\Users\User1> netstat -a | sls 2375

    TCP    127.0.0.1:2375         Win2016TP5:0           LISTENING
    TCP    127.0.0.1:2375         Win2016TP5:49705       ESTABLISHED
    TCP    127.0.0.1:2375         Win2016TP5:49706       ESTABLISHED
    TCP    127.0.0.1:2375         Win2016TP5:49707       ESTABLISHED
    TCP    127.0.0.1:2375         Win2016TP5:49708       ESTABLISHED
    TCP    127.0.0.1:49705        Win2016TP5:2375        ESTABLISHED
    TCP    127.0.0.1:49706        Win2016TP5:2375        ESTABLISHED
    TCP    127.0.0.1:49707        Win2016TP5:2375        ESTABLISHED
    TCP    127.0.0.1:49708        Win2016TP5:2375        ESTABLISHED
    ```

### <a name="install-windows-agents"></a><span data-ttu-id="23394-161">Install Windows agents</span><span class="sxs-lookup"><span data-stu-id="23394-161">Install Windows agents</span></span>

<span data-ttu-id="23394-162">To enable Windows and Hyper-V container monitoring, install agents on Windows computers that are container hosts.</span><span class="sxs-lookup"><span data-stu-id="23394-162">To enable Windows and Hyper-V container monitoring, install agents on Windows computers that are container hosts.</span></span> <span data-ttu-id="23394-163">For computers running Windows in your on-premises environment, see [Connect Windows computers to Log Analytics](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="23394-163">For computers running Windows in your on-premises environment, see [Connect Windows computers to Log Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="23394-164">For virtual machines running in Azure,  connect them to Log Analytics using the [virtual machine extension](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="23394-164">For virtual machines running in Azure,  connect them to Log Analytics using the [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="23394-165">To verify that the Containers solution is set correctly:</span><span class="sxs-lookup"><span data-stu-id="23394-165">To verify that the Containers solution is set correctly:</span></span>

- <span data-ttu-id="23394-166">Check whether the management pack was download properly, look for *ContainerManagement.xxx*.</span><span class="sxs-lookup"><span data-stu-id="23394-166">Check whether the management pack was download properly, look for *ContainerManagement.xxx*.</span></span>
    - <span data-ttu-id="23394-167">The files should be in the C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs folder.</span><span class="sxs-lookup"><span data-stu-id="23394-167">The files should be in the C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs folder.</span></span>
- <span data-ttu-id="23394-168">Verify that the OMS Workspace ID is correct by going to **Control Panel** > **System and Security**.</span><span class="sxs-lookup"><span data-stu-id="23394-168">Verify that the OMS Workspace ID is correct by going to **Control Panel** > **System and Security**.</span></span>
    - <span data-ttu-id="23394-169">Open **Microsoft Monitoring Agent** and verify that the workspace information is correct.</span><span class="sxs-lookup"><span data-stu-id="23394-169">Open **Microsoft Monitoring Agent** and verify that the workspace information is correct.</span></span>


## <a name="containers-data-collection-details"></a><span data-ttu-id="23394-170">Containers data collection details</span><span class="sxs-lookup"><span data-stu-id="23394-170">Containers data collection details</span></span>
<span data-ttu-id="23394-171">The Containers solution collects various performance metrics and log data from container hosts and containers using agents that you  enable.</span><span class="sxs-lookup"><span data-stu-id="23394-171">The Containers solution collects various performance metrics and log data from container hosts and containers using agents that you  enable.</span></span>

<span data-ttu-id="23394-172">The following table shows data collection methods and other details about how data is collected for Containers.</span><span class="sxs-lookup"><span data-stu-id="23394-172">The following table shows data collection methods and other details about how data is collected for Containers.</span></span>

| <span data-ttu-id="23394-173">platform</span><span class="sxs-lookup"><span data-stu-id="23394-173">platform</span></span> | [<span data-ttu-id="23394-174">OMS Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="23394-174">OMS Agent for Linux</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="23394-175">SCOM agent</span><span class="sxs-lookup"><span data-stu-id="23394-175">SCOM agent</span></span> | <span data-ttu-id="23394-176">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="23394-176">Azure Storage</span></span> | <span data-ttu-id="23394-177">SCOM required?</span><span class="sxs-lookup"><span data-stu-id="23394-177">SCOM required?</span></span> | <span data-ttu-id="23394-178">SCOM agent data sent via management group</span><span class="sxs-lookup"><span data-stu-id="23394-178">SCOM agent data sent via management group</span></span> | <span data-ttu-id="23394-179">collection frequency</span><span class="sxs-lookup"><span data-stu-id="23394-179">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="23394-180">Linux</span><span class="sxs-lookup"><span data-stu-id="23394-180">Linux</span></span> |![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/oms-bullet-green.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/oms-bullet-red.png) |<span data-ttu-id="23394-186">every 3 minutes</span><span class="sxs-lookup"><span data-stu-id="23394-186">every 3 minutes</span></span> |

| <span data-ttu-id="23394-187">platform</span><span class="sxs-lookup"><span data-stu-id="23394-187">platform</span></span> | [<span data-ttu-id="23394-188">Windows agent</span><span class="sxs-lookup"><span data-stu-id="23394-188">Windows agent</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="23394-189">SCOM agent</span><span class="sxs-lookup"><span data-stu-id="23394-189">SCOM agent</span></span> | <span data-ttu-id="23394-190">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="23394-190">Azure Storage</span></span> | <span data-ttu-id="23394-191">SCOM required?</span><span class="sxs-lookup"><span data-stu-id="23394-191">SCOM required?</span></span> | <span data-ttu-id="23394-192">SCOM agent data sent via management group</span><span class="sxs-lookup"><span data-stu-id="23394-192">SCOM agent data sent via management group</span></span> | <span data-ttu-id="23394-193">collection frequency</span><span class="sxs-lookup"><span data-stu-id="23394-193">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="23394-194">Windows</span><span class="sxs-lookup"><span data-stu-id="23394-194">Windows</span></span> |![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/oms-bullet-green.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/oms-bullet-red.png) |<span data-ttu-id="23394-200">every 3 minutes</span><span class="sxs-lookup"><span data-stu-id="23394-200">every 3 minutes</span></span> |

| <span data-ttu-id="23394-201">platform</span><span class="sxs-lookup"><span data-stu-id="23394-201">platform</span></span> | [<span data-ttu-id="23394-202">Log Analytics VM extension</span><span class="sxs-lookup"><span data-stu-id="23394-202">Log Analytics VM extension</span></span>](log-analytics-azure-vm-extension.md) | <span data-ttu-id="23394-203">SCOM agent</span><span class="sxs-lookup"><span data-stu-id="23394-203">SCOM agent</span></span> | <span data-ttu-id="23394-204">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="23394-204">Azure Storage</span></span> | <span data-ttu-id="23394-205">SCOM required?</span><span class="sxs-lookup"><span data-stu-id="23394-205">SCOM required?</span></span> | <span data-ttu-id="23394-206">SCOM agent data sent via management group</span><span class="sxs-lookup"><span data-stu-id="23394-206">SCOM agent data sent via management group</span></span> | <span data-ttu-id="23394-207">collection frequency</span><span class="sxs-lookup"><span data-stu-id="23394-207">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="23394-208">Azure</span><span class="sxs-lookup"><span data-stu-id="23394-208">Azure</span></span> |![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/oms-bullet-green.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/oms-bullet-red.png) |<span data-ttu-id="23394-214">every 3 minutes</span><span class="sxs-lookup"><span data-stu-id="23394-214">every 3 minutes</span></span> |

<span data-ttu-id="23394-215">The following table show examples of data types collected by the Containers solution and the data types that are used in Log Searches and results.</span><span class="sxs-lookup"><span data-stu-id="23394-215">The following table show examples of data types collected by the Containers solution and the data types that are used in Log Searches and results.</span></span> <span data-ttu-id="23394-216">However, performance data is not yet supported for computers running Windows.</span><span class="sxs-lookup"><span data-stu-id="23394-216">However, performance data is not yet supported for computers running Windows.</span></span>

| <span data-ttu-id="23394-217">Data type</span><span class="sxs-lookup"><span data-stu-id="23394-217">Data type</span></span> | <span data-ttu-id="23394-218">Data type in Log Search</span><span class="sxs-lookup"><span data-stu-id="23394-218">Data type in Log Search</span></span> | <span data-ttu-id="23394-219">Fields</span><span class="sxs-lookup"><span data-stu-id="23394-219">Fields</span></span> |
| --- | --- | --- |
| <span data-ttu-id="23394-220">Performance for hosts and containers</span><span class="sxs-lookup"><span data-stu-id="23394-220">Performance for hosts and containers</span></span> | `Type=Perf` | <span data-ttu-id="23394-221">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="23394-221">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span></span> |
| <span data-ttu-id="23394-222">Container inventory</span><span class="sxs-lookup"><span data-stu-id="23394-222">Container inventory</span></span> | `Type=ContainerInventory` | <span data-ttu-id="23394-223">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContinerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span><span class="sxs-lookup"><span data-stu-id="23394-223">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContinerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span></span> |
| <span data-ttu-id="23394-224">Container image inventory</span><span class="sxs-lookup"><span data-stu-id="23394-224">Container image inventory</span></span> | `Type=ContainerImageInventory` | <span data-ttu-id="23394-225">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span><span class="sxs-lookup"><span data-stu-id="23394-225">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span></span> |
| <span data-ttu-id="23394-226">Container log</span><span class="sxs-lookup"><span data-stu-id="23394-226">Container log</span></span> | `Type=ContainerLog` | <span data-ttu-id="23394-227">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="23394-227">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="23394-228">Container service log</span><span class="sxs-lookup"><span data-stu-id="23394-228">Container service log</span></span> | `Type=ContainerServiceLog`  | <span data-ttu-id="23394-229">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="23394-229">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span></span> |

## <a name="monitor-containers"></a><span data-ttu-id="23394-230">Monitor containers</span><span class="sxs-lookup"><span data-stu-id="23394-230">Monitor containers</span></span>
<span data-ttu-id="23394-231">After you have the solution enabled in the OMS portal, you'll see the **Containers** tile showing summary information about your container hosts and the containers running in hosts.</span><span class="sxs-lookup"><span data-stu-id="23394-231">After you have the solution enabled in the OMS portal, you'll see the **Containers** tile showing summary information about your container hosts and the containers running in hosts.</span></span>

![Containers tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/containers-title.png)

<span data-ttu-id="23394-233">The tile shows an overview of how many containers you have in the environment and whether they're failed, running, or stopped.</span><span class="sxs-lookup"><span data-stu-id="23394-233">The tile shows an overview of how many containers you have in the environment and whether they're failed, running, or stopped.</span></span>

### <a name="using-the-containers-dashboard"></a><span data-ttu-id="23394-234">Using the Containers dashboard</span><span class="sxs-lookup"><span data-stu-id="23394-234">Using the Containers dashboard</span></span>
<span data-ttu-id="23394-235">Click the **Containers** tile.</span><span class="sxs-lookup"><span data-stu-id="23394-235">Click the **Containers** tile.</span></span> <span data-ttu-id="23394-236">From there you'll see views organized by:</span><span class="sxs-lookup"><span data-stu-id="23394-236">From there you'll see views organized by:</span></span>

* <span data-ttu-id="23394-237">Container Events</span><span class="sxs-lookup"><span data-stu-id="23394-237">Container Events</span></span>
* <span data-ttu-id="23394-238">Errors</span><span class="sxs-lookup"><span data-stu-id="23394-238">Errors</span></span>
* <span data-ttu-id="23394-239">Containers Status</span><span class="sxs-lookup"><span data-stu-id="23394-239">Containers Status</span></span>
* <span data-ttu-id="23394-240">Container Image Inventory</span><span class="sxs-lookup"><span data-stu-id="23394-240">Container Image Inventory</span></span>
* <span data-ttu-id="23394-241">CPU and Memory performance</span><span class="sxs-lookup"><span data-stu-id="23394-241">CPU and Memory performance</span></span>

<span data-ttu-id="23394-242">Each pane in the dashboard is a visual representation of a search that is run on collected data.</span><span class="sxs-lookup"><span data-stu-id="23394-242">Each pane in the dashboard is a visual representation of a search that is run on collected data.</span></span>

![Containers dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/containers-dash01.png)

![Containers dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/containers-dash02.png)

<span data-ttu-id="23394-245">In the **Container Status** blade, click to top area, as shown below.</span><span class="sxs-lookup"><span data-stu-id="23394-245">In the **Container Status** blade, click to top area, as shown below.</span></span>

![Containers status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/containers-status.png)

<span data-ttu-id="23394-247">Log Search opens, displaying information about the hosts and containers running in them.</span><span class="sxs-lookup"><span data-stu-id="23394-247">Log Search opens, displaying information about the hosts and containers running in them.</span></span>

![Log Search for containers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/containers-log-search.png)

<span data-ttu-id="23394-249">From here, you can edit the search query to modify it to find the specific information you're interested in.</span><span class="sxs-lookup"><span data-stu-id="23394-249">From here, you can edit the search query to modify it to find the specific information you're interested in.</span></span> <span data-ttu-id="23394-250">For more information about Log Searches, see [Log searches in Log Analytics](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="23394-250">For more information about Log Searches, see [Log searches in Log Analytics](log-analytics-log-searches.md).</span></span>

<span data-ttu-id="23394-251">For example, you can modify the search query so that it shows all the stopped containers instead of the running containers by changing **Running** to **Stopped** in the search query.</span><span class="sxs-lookup"><span data-stu-id="23394-251">For example, you can modify the search query so that it shows all the stopped containers instead of the running containers by changing **Running** to **Stopped** in the search query.</span></span>

## <a name="troubleshoot-by-finding-a-failed-container"></a><span data-ttu-id="23394-252">Troubleshoot by finding a failed container</span><span class="sxs-lookup"><span data-stu-id="23394-252">Troubleshoot by finding a failed container</span></span>
<span data-ttu-id="23394-253">OMS marks a container as **Failed** if it has exited with a non-zero exit code.</span><span class="sxs-lookup"><span data-stu-id="23394-253">OMS marks a container as **Failed** if it has exited with a non-zero exit code.</span></span> <span data-ttu-id="23394-254">You can see an overview of the errors and failures in the environment in the **Failed Containers** blade.</span><span class="sxs-lookup"><span data-stu-id="23394-254">You can see an overview of the errors and failures in the environment in the **Failed Containers** blade.</span></span>

### <a name="to-find-failed-containers"></a><span data-ttu-id="23394-255">To find failed containers</span><span class="sxs-lookup"><span data-stu-id="23394-255">To find failed containers</span></span>
1. <span data-ttu-id="23394-256">Click the **Container Events** blade.</span><span class="sxs-lookup"><span data-stu-id="23394-256">Click the **Container Events** blade.</span></span>  
   <span data-ttu-id="23394-257">![containers events](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/containers-events.png)</span><span class="sxs-lookup"><span data-stu-id="23394-257">![containers events](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/containers-events.png)</span></span>
2. <span data-ttu-id="23394-258">Log Search opens, displaying the status of containers, similar to the following.</span><span class="sxs-lookup"><span data-stu-id="23394-258">Log Search opens, displaying the status of containers, similar to the following.</span></span>  
   ![containers state](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/containers-container-state.png)
3. <span data-ttu-id="23394-260">Next, click the failed value to view additional information such as image size and number of stopped and failed images.</span><span class="sxs-lookup"><span data-stu-id="23394-260">Next, click the failed value to view additional information such as image size and number of stopped and failed images.</span></span> <span data-ttu-id="23394-261">Expand **show more** to view the image ID.</span><span class="sxs-lookup"><span data-stu-id="23394-261">Expand **show more** to view the image ID.</span></span>  
   <span data-ttu-id="23394-262">![failed containers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/containers-state-failed.png)</span><span class="sxs-lookup"><span data-stu-id="23394-262">![failed containers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/containers-state-failed.png)</span></span>
4. <span data-ttu-id="23394-263">Next, find the container that is running this image.</span><span class="sxs-lookup"><span data-stu-id="23394-263">Next, find the container that is running this image.</span></span> <span data-ttu-id="23394-264">Type the following into the search query.</span><span class="sxs-lookup"><span data-stu-id="23394-264">Type the following into the search query.</span></span>
   <span data-ttu-id="23394-265">`Type=ContainerInventory <ImageID>` This displays the logs.</span><span class="sxs-lookup"><span data-stu-id="23394-265">`Type=ContainerInventory <ImageID>` This displays the logs.</span></span> <span data-ttu-id="23394-266">You can scroll to see the failed container.</span><span class="sxs-lookup"><span data-stu-id="23394-266">You can scroll to see the failed container.</span></span>  
   <span data-ttu-id="23394-267">![failed containers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/containers-failed04.png)</span><span class="sxs-lookup"><span data-stu-id="23394-267">![failed containers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/containers-failed04.png)</span></span>

## <a name="search-logs-for-container-data"></a><span data-ttu-id="23394-268">Search logs for container data</span><span class="sxs-lookup"><span data-stu-id="23394-268">Search logs for container data</span></span>
<span data-ttu-id="23394-269">When you're troubleshooting a specific error, it can help to see where it is occurring in your environment.</span><span class="sxs-lookup"><span data-stu-id="23394-269">When you're troubleshooting a specific error, it can help to see where it is occurring in your environment.</span></span> <span data-ttu-id="23394-270">The following log types will help you create queries to return the information you want.</span><span class="sxs-lookup"><span data-stu-id="23394-270">The following log types will help you create queries to return the information you want.</span></span>

* <span data-ttu-id="23394-271">**ContainerInventory** – Use this type when you want information about container location, what their names are, and what images they're running.</span><span class="sxs-lookup"><span data-stu-id="23394-271">**ContainerInventory** – Use this type when you want information about container location, what their names are, and what images they're running.</span></span>
* <span data-ttu-id="23394-272">**ContainerImageInventory** – Use this type when you're trying to find information organized by image and to view image information such as image IDs or sizes.</span><span class="sxs-lookup"><span data-stu-id="23394-272">**ContainerImageInventory** – Use this type when you're trying to find information organized by image and to view image information such as image IDs or sizes.</span></span>
* <span data-ttu-id="23394-273">**ContainerLog** – Use this type when you want to find specific error log information and entries.</span><span class="sxs-lookup"><span data-stu-id="23394-273">**ContainerLog** – Use this type when you want to find specific error log information and entries.</span></span>
* <span data-ttu-id="23394-274">**ContainerServiceLog** – Use this type when you're trying to find audit trail information for the Docker daemon, such as start, stop, delete, or pull commands.</span><span class="sxs-lookup"><span data-stu-id="23394-274">**ContainerServiceLog** – Use this type when you're trying to find audit trail information for the Docker daemon, such as start, stop, delete, or pull commands.</span></span>

### <a name="to-search-logs-for-container-data"></a><span data-ttu-id="23394-275">To search logs for container data</span><span class="sxs-lookup"><span data-stu-id="23394-275">To search logs for container data</span></span>
* <span data-ttu-id="23394-276">Choose an image that you know has failed recently and find the error logs for it.</span><span class="sxs-lookup"><span data-stu-id="23394-276">Choose an image that you know has failed recently and find the error logs for it.</span></span> <span data-ttu-id="23394-277">Start by finding a container name that is running that image with a **ContainerInventory** search.</span><span class="sxs-lookup"><span data-stu-id="23394-277">Start by finding a container name that is running that image with a **ContainerInventory** search.</span></span> <span data-ttu-id="23394-278">For example, search for `Type=ContainerInventory ubuntu Failed`</span><span class="sxs-lookup"><span data-stu-id="23394-278">For example, search for `Type=ContainerInventory ubuntu Failed`</span></span>  
    <span data-ttu-id="23394-279">![Search for Ubuntu containers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/search-ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="23394-279">![Search for Ubuntu containers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/search-ubuntu.png)</span></span>

  <span data-ttu-id="23394-280">Note the name of the container next to **Name**, and search for those logs.</span><span class="sxs-lookup"><span data-stu-id="23394-280">Note the name of the container next to **Name**, and search for those logs.</span></span> <span data-ttu-id="23394-281">In this example, it is `Type=ContainerLog adoring_meitner`.</span><span class="sxs-lookup"><span data-stu-id="23394-281">In this example, it is `Type=ContainerLog adoring_meitner`.</span></span>

<span data-ttu-id="23394-282">**View performance information**</span><span class="sxs-lookup"><span data-stu-id="23394-282">**View performance information**</span></span>

<span data-ttu-id="23394-283">When you're beginning to construct queries, it can help to see what's possible first.</span><span class="sxs-lookup"><span data-stu-id="23394-283">When you're beginning to construct queries, it can help to see what's possible first.</span></span> <span data-ttu-id="23394-284">For example, to see all performance data, try a broad query by typing the following search query.</span><span class="sxs-lookup"><span data-stu-id="23394-284">For example, to see all performance data, try a broad query by typing the following search query.</span></span>

```
Type=Perf
```

![containers performance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/containers-perf01.png)

<span data-ttu-id="23394-286">You can see this in a more graphical form when you click the word **Metrics** in the results.</span><span class="sxs-lookup"><span data-stu-id="23394-286">You can see this in a more graphical form when you click the word **Metrics** in the results.</span></span>

![containers performance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/containers-perf02.png)

<span data-ttu-id="23394-288">You can scope the performance data you're seeing to a specific container by typing the name of it to the right of your query.</span><span class="sxs-lookup"><span data-stu-id="23394-288">You can scope the performance data you're seeing to a specific container by typing the name of it to the right of your query.</span></span>

```
Type=Perf <containerName>
```

<span data-ttu-id="23394-289">That shows the list of performance metrics that are collected for an individual container.</span><span class="sxs-lookup"><span data-stu-id="23394-289">That shows the list of performance metrics that are collected for an individual container.</span></span>

![containers performance](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a><span data-ttu-id="23394-291">Example log search queries</span><span class="sxs-lookup"><span data-stu-id="23394-291">Example log search queries</span></span>
<span data-ttu-id="23394-292">It's often useful to build queries starting with an example or two and then modifying them to fit your environment.</span><span class="sxs-lookup"><span data-stu-id="23394-292">It's often useful to build queries starting with an example or two and then modifying them to fit your environment.</span></span> <span data-ttu-id="23394-293">As a starting point, you can experiment with the **Notable Queries** blade to help you build more advanced queries.</span><span class="sxs-lookup"><span data-stu-id="23394-293">As a starting point, you can experiment with the **Notable Queries** blade to help you build more advanced queries.</span></span>

![Containers queries](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-containers/containers-queries.png)

## <a name="saving-log-search-queries"></a><span data-ttu-id="23394-295">Saving log search queries</span><span class="sxs-lookup"><span data-stu-id="23394-295">Saving log search queries</span></span>
<span data-ttu-id="23394-296">Saving queries is a standard feature in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="23394-296">Saving queries is a standard feature in Log Analytics.</span></span> <span data-ttu-id="23394-297">By saving them, you'll have those that you've found useful handy for future use.</span><span class="sxs-lookup"><span data-stu-id="23394-297">By saving them, you'll have those that you've found useful handy for future use.</span></span>

<span data-ttu-id="23394-298">After you create a query that you find useful, save it by clicking **Favorites** at the top of the Log Search page.</span><span class="sxs-lookup"><span data-stu-id="23394-298">After you create a query that you find useful, save it by clicking **Favorites** at the top of the Log Search page.</span></span> <span data-ttu-id="23394-299">Then you can easily access it later from the **My Dashboard** page.</span><span class="sxs-lookup"><span data-stu-id="23394-299">Then you can easily access it later from the **My Dashboard** page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23394-300">Next steps</span><span class="sxs-lookup"><span data-stu-id="23394-300">Next steps</span></span>
* <span data-ttu-id="23394-301">[Search logs](log-analytics-log-searches.md) to view detailed container data records.</span><span class="sxs-lookup"><span data-stu-id="23394-301">[Search logs](log-analytics-log-searches.md) to view detailed container data records.</span></span>






























