---
title: Enable access to Azure DC/OS container app | Microsoft Docs
description: How to enable public access to DC/OS containers in Azure Container Service.
services: container-service
documentationcenter: ''
author: sauryadas
manager: madhana
editor: ''
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure
ms.assetid: 5dea3c4d-a687-4024-93ea-f7a9a7243ab4
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: saudas
ms.openlocfilehash: 8c82611ad6082b2bbbe29ba3e8131131b8d7d5ba
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660861"
---
# <a name="enable-public-access-to-an-azure-container-service-application"></a><span data-ttu-id="775e4-104">Enable public access to an Azure Container Service application</span><span class="sxs-lookup"><span data-stu-id="775e4-104">Enable public access to an Azure Container Service application</span></span>
<span data-ttu-id="775e4-105">Any DC/OS container in the ACS [public agent pool](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) is automatically exposed to the internet.</span><span class="sxs-lookup"><span data-stu-id="775e4-105">Any DC/OS container in the ACS [public agent pool](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) is automatically exposed to the internet.</span></span> <span data-ttu-id="775e4-106">By default, ports **80**, **443**, **8080** are opened, and any (public) container listening on those ports are accessible.</span><span class="sxs-lookup"><span data-stu-id="775e4-106">By default, ports **80**, **443**, **8080** are opened, and any (public) container listening on those ports are accessible.</span></span> <span data-ttu-id="775e4-107">This article shows you how to open more ports for your applications in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="775e4-107">This article shows you how to open more ports for your applications in Azure Container Service.</span></span>

## <a name="open-a-port-portal"></a><span data-ttu-id="775e4-108">Open a port (portal)</span><span class="sxs-lookup"><span data-stu-id="775e4-108">Open a port (portal)</span></span>
<span data-ttu-id="775e4-109">First, we need to open the port we want.</span><span class="sxs-lookup"><span data-stu-id="775e4-109">First, we need to open the port we want.</span></span>

1. <span data-ttu-id="775e4-110">Log in to the portal.</span><span class="sxs-lookup"><span data-stu-id="775e4-110">Log in to the portal.</span></span>
2. <span data-ttu-id="775e4-111">Find the resource group that you deployed the Azure Container Service to.</span><span class="sxs-lookup"><span data-stu-id="775e4-111">Find the resource group that you deployed the Azure Container Service to.</span></span>
3. <span data-ttu-id="775e4-112">Select the agent load balancer (which is named similar to **XXXX-agent-lb-XXXX**).</span><span class="sxs-lookup"><span data-stu-id="775e4-112">Select the agent load balancer (which is named similar to **XXXX-agent-lb-XXXX**).</span></span>
   
    ![Azure container service load balancer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-dcos-agents/agent-load-balancer.png)
4. <span data-ttu-id="775e4-114">Click **Probes** and then **Add**.</span><span class="sxs-lookup"><span data-stu-id="775e4-114">Click **Probes** and then **Add**.</span></span>
   
    ![Azure container service load balancer probes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-dcos-agents/add-probe.png)
5. <span data-ttu-id="775e4-116">Fill out the probe form and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="775e4-116">Fill out the probe form and click **OK**.</span></span>
   
   | <span data-ttu-id="775e4-117">Field</span><span class="sxs-lookup"><span data-stu-id="775e4-117">Field</span></span> | <span data-ttu-id="775e4-118">Description</span><span class="sxs-lookup"><span data-stu-id="775e4-118">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="775e4-119">Name</span><span class="sxs-lookup"><span data-stu-id="775e4-119">Name</span></span> |<span data-ttu-id="775e4-120">A descriptive name of the probe.</span><span class="sxs-lookup"><span data-stu-id="775e4-120">A descriptive name of the probe.</span></span> |
   | <span data-ttu-id="775e4-121">Port</span><span class="sxs-lookup"><span data-stu-id="775e4-121">Port</span></span> |<span data-ttu-id="775e4-122">The port of the container to test.</span><span class="sxs-lookup"><span data-stu-id="775e4-122">The port of the container to test.</span></span> |
   | <span data-ttu-id="775e4-123">Path</span><span class="sxs-lookup"><span data-stu-id="775e4-123">Path</span></span> |<span data-ttu-id="775e4-124">(When in HTTP mode) The relative website path to probe.</span><span class="sxs-lookup"><span data-stu-id="775e4-124">(When in HTTP mode) The relative website path to probe.</span></span> <span data-ttu-id="775e4-125">HTTPS not supported.</span><span class="sxs-lookup"><span data-stu-id="775e4-125">HTTPS not supported.</span></span> |
   | <span data-ttu-id="775e4-126">Interval</span><span class="sxs-lookup"><span data-stu-id="775e4-126">Interval</span></span> |<span data-ttu-id="775e4-127">The amount of time between probe attempts, in seconds.</span><span class="sxs-lookup"><span data-stu-id="775e4-127">The amount of time between probe attempts, in seconds.</span></span> |
   | <span data-ttu-id="775e4-128">Unhealthy threshold</span><span class="sxs-lookup"><span data-stu-id="775e4-128">Unhealthy threshold</span></span> |<span data-ttu-id="775e4-129">Number of consecutive probe attempts before considering the container unhealthy.</span><span class="sxs-lookup"><span data-stu-id="775e4-129">Number of consecutive probe attempts before considering the container unhealthy.</span></span> |
6. <span data-ttu-id="775e4-130">Back at the properties of the agent load balancer, click **Load balancing rules** and then **Add**.</span><span class="sxs-lookup"><span data-stu-id="775e4-130">Back at the properties of the agent load balancer, click **Load balancing rules** and then **Add**.</span></span>
   
    ![Azure container service load balancer rules](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-dcos-agents/add-balancer-rule.png)
7. <span data-ttu-id="775e4-132">Fill out the load balancer form and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="775e4-132">Fill out the load balancer form and click **OK**.</span></span>
   
   | <span data-ttu-id="775e4-133">Field</span><span class="sxs-lookup"><span data-stu-id="775e4-133">Field</span></span> | <span data-ttu-id="775e4-134">Description</span><span class="sxs-lookup"><span data-stu-id="775e4-134">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="775e4-135">Name</span><span class="sxs-lookup"><span data-stu-id="775e4-135">Name</span></span> |<span data-ttu-id="775e4-136">A descriptive name of the load balancer.</span><span class="sxs-lookup"><span data-stu-id="775e4-136">A descriptive name of the load balancer.</span></span> |
   | <span data-ttu-id="775e4-137">Port</span><span class="sxs-lookup"><span data-stu-id="775e4-137">Port</span></span> |<span data-ttu-id="775e4-138">The public incoming port.</span><span class="sxs-lookup"><span data-stu-id="775e4-138">The public incoming port.</span></span> |
   | <span data-ttu-id="775e4-139">Backend port</span><span class="sxs-lookup"><span data-stu-id="775e4-139">Backend port</span></span> |<span data-ttu-id="775e4-140">The internal-public port of the container to route traffic to.</span><span class="sxs-lookup"><span data-stu-id="775e4-140">The internal-public port of the container to route traffic to.</span></span> |
   | <span data-ttu-id="775e4-141">Backend pool</span><span class="sxs-lookup"><span data-stu-id="775e4-141">Backend pool</span></span> |<span data-ttu-id="775e4-142">The containers in this pool will be the target for this load balancer.</span><span class="sxs-lookup"><span data-stu-id="775e4-142">The containers in this pool will be the target for this load balancer.</span></span> |
   | <span data-ttu-id="775e4-143">Probe</span><span class="sxs-lookup"><span data-stu-id="775e4-143">Probe</span></span> |<span data-ttu-id="775e4-144">The probe used to determine if a target in the **Backend pool** is healthy.</span><span class="sxs-lookup"><span data-stu-id="775e4-144">The probe used to determine if a target in the **Backend pool** is healthy.</span></span> |
   | <span data-ttu-id="775e4-145">Session persistence</span><span class="sxs-lookup"><span data-stu-id="775e4-145">Session persistence</span></span> |<span data-ttu-id="775e4-146">Determines how traffic from a client should be handled for the duration of the session.</span><span class="sxs-lookup"><span data-stu-id="775e4-146">Determines how traffic from a client should be handled for the duration of the session.</span></span><br><br><span data-ttu-id="775e4-147">**None**: Successive requests from the same client can be handled by any container.</span><span class="sxs-lookup"><span data-stu-id="775e4-147">**None**: Successive requests from the same client can be handled by any container.</span></span><br><span data-ttu-id="775e4-148">**Client IP**: Successive requests from the same client IP are handled by the same container.</span><span class="sxs-lookup"><span data-stu-id="775e4-148">**Client IP**: Successive requests from the same client IP are handled by the same container.</span></span><br><span data-ttu-id="775e4-149">**Client IP and protocol**: Successive requests from the same client IP and protocol combination are handled by the same container.</span><span class="sxs-lookup"><span data-stu-id="775e4-149">**Client IP and protocol**: Successive requests from the same client IP and protocol combination are handled by the same container.</span></span> |
   | <span data-ttu-id="775e4-150">Idle timeout</span><span class="sxs-lookup"><span data-stu-id="775e4-150">Idle timeout</span></span> |<span data-ttu-id="775e4-151">(TCP only) In minutes, the time to keep a TCP/HTTP client open without relying on *keep-alive* messages.</span><span class="sxs-lookup"><span data-stu-id="775e4-151">(TCP only) In minutes, the time to keep a TCP/HTTP client open without relying on *keep-alive* messages.</span></span> |

## <a name="add-a-security-rule-portal"></a><span data-ttu-id="775e4-152">Add a security rule (portal)</span><span class="sxs-lookup"><span data-stu-id="775e4-152">Add a security rule (portal)</span></span>
<span data-ttu-id="775e4-153">Next, we need to add a security rule that routes traffic from our opened port through the firewall.</span><span class="sxs-lookup"><span data-stu-id="775e4-153">Next, we need to add a security rule that routes traffic from our opened port through the firewall.</span></span>

1. <span data-ttu-id="775e4-154">Log in to the portal.</span><span class="sxs-lookup"><span data-stu-id="775e4-154">Log in to the portal.</span></span>
2. <span data-ttu-id="775e4-155">Find the resource group that you deployed the Azure Container Service to.</span><span class="sxs-lookup"><span data-stu-id="775e4-155">Find the resource group that you deployed the Azure Container Service to.</span></span>
3. <span data-ttu-id="775e4-156">Select the **public** agent network security group (which is named similar to **XXXX-agent-public-nsg-XXXX**).</span><span class="sxs-lookup"><span data-stu-id="775e4-156">Select the **public** agent network security group (which is named similar to **XXXX-agent-public-nsg-XXXX**).</span></span>
   
    ![Azure container service network security group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-dcos-agents/agent-nsg.png)
4. <span data-ttu-id="775e4-158">Select **Inbound security rules** and then **Add**.</span><span class="sxs-lookup"><span data-stu-id="775e4-158">Select **Inbound security rules** and then **Add**.</span></span>
   
    ![Azure container service network security group rules](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-service/media/container-service-dcos-agents/add-firewall-rule.png)
5. <span data-ttu-id="775e4-160">Fill out the firewall rule to allow your public port and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="775e4-160">Fill out the firewall rule to allow your public port and click **OK**.</span></span>
   
   | <span data-ttu-id="775e4-161">Field</span><span class="sxs-lookup"><span data-stu-id="775e4-161">Field</span></span> | <span data-ttu-id="775e4-162">Description</span><span class="sxs-lookup"><span data-stu-id="775e4-162">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="775e4-163">Name</span><span class="sxs-lookup"><span data-stu-id="775e4-163">Name</span></span> |<span data-ttu-id="775e4-164">A descriptive name of the firewall rule.</span><span class="sxs-lookup"><span data-stu-id="775e4-164">A descriptive name of the firewall rule.</span></span> |
   | <span data-ttu-id="775e4-165">Priority</span><span class="sxs-lookup"><span data-stu-id="775e4-165">Priority</span></span> |<span data-ttu-id="775e4-166">Priority rank for the rule.</span><span class="sxs-lookup"><span data-stu-id="775e4-166">Priority rank for the rule.</span></span> <span data-ttu-id="775e4-167">The lower the number the higher the priority.</span><span class="sxs-lookup"><span data-stu-id="775e4-167">The lower the number the higher the priority.</span></span> |
   | <span data-ttu-id="775e4-168">Source</span><span class="sxs-lookup"><span data-stu-id="775e4-168">Source</span></span> |<span data-ttu-id="775e4-169">Restrict the incoming IP address range to be allowed or denied by this rule.</span><span class="sxs-lookup"><span data-stu-id="775e4-169">Restrict the incoming IP address range to be allowed or denied by this rule.</span></span> <span data-ttu-id="775e4-170">Use **Any** to not specify a restriction.</span><span class="sxs-lookup"><span data-stu-id="775e4-170">Use **Any** to not specify a restriction.</span></span> |
   | <span data-ttu-id="775e4-171">Service</span><span class="sxs-lookup"><span data-stu-id="775e4-171">Service</span></span> |<span data-ttu-id="775e4-172">Select a set of predefined services this security rule is for.</span><span class="sxs-lookup"><span data-stu-id="775e4-172">Select a set of predefined services this security rule is for.</span></span> <span data-ttu-id="775e4-173">Otherwise use **Custom** to create your own.</span><span class="sxs-lookup"><span data-stu-id="775e4-173">Otherwise use **Custom** to create your own.</span></span> |
   | <span data-ttu-id="775e4-174">Protocol</span><span class="sxs-lookup"><span data-stu-id="775e4-174">Protocol</span></span> |<span data-ttu-id="775e4-175">Restrict traffic based on **TCP** or **UDP**.</span><span class="sxs-lookup"><span data-stu-id="775e4-175">Restrict traffic based on **TCP** or **UDP**.</span></span> <span data-ttu-id="775e4-176">Use **Any** to not specify a restriction.</span><span class="sxs-lookup"><span data-stu-id="775e4-176">Use **Any** to not specify a restriction.</span></span> |
   | <span data-ttu-id="775e4-177">Port range</span><span class="sxs-lookup"><span data-stu-id="775e4-177">Port range</span></span> |<span data-ttu-id="775e4-178">When **Service** is **Custom**, specifies the range of ports that this rule affects.</span><span class="sxs-lookup"><span data-stu-id="775e4-178">When **Service** is **Custom**, specifies the range of ports that this rule affects.</span></span> <span data-ttu-id="775e4-179">You can use a single port, such as **80**, or a range like **1024-1500**.</span><span class="sxs-lookup"><span data-stu-id="775e4-179">You can use a single port, such as **80**, or a range like **1024-1500**.</span></span> |
   | <span data-ttu-id="775e4-180">Action</span><span class="sxs-lookup"><span data-stu-id="775e4-180">Action</span></span> |<span data-ttu-id="775e4-181">Allow or deny traffic that meets the criteria.</span><span class="sxs-lookup"><span data-stu-id="775e4-181">Allow or deny traffic that meets the criteria.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="775e4-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="775e4-182">Next steps</span></span>
<span data-ttu-id="775e4-183">Learn about the difference between [public and private DC/OS agents](container-service-dcos-agents.md).</span><span class="sxs-lookup"><span data-stu-id="775e4-183">Learn about the difference between [public and private DC/OS agents](container-service-dcos-agents.md).</span></span>

<span data-ttu-id="775e4-184">Read more information about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="775e4-184">Read more information about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>






