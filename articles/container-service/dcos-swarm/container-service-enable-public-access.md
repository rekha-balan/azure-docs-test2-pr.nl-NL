---
title: Enable access to Azure DC/OS container app
description: How to enable public access to DC/OS containers in Azure Container Service.
services: container-service
author: sauryadas
manager: madhana
ms.service: container-service
ms.topic: article
ms.date: 08/26/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: aedc97335a0b9ad00cf653477b62bf530b556900
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867739"
---
# <a name="enable-public-access-to-an-azure-container-service-application"></a><span data-ttu-id="82e34-103">Enable public access to an Azure Container Service application</span><span class="sxs-lookup"><span data-stu-id="82e34-103">Enable public access to an Azure Container Service application</span></span>

<span data-ttu-id="82e34-104">Any DC/OS container in the ACS [public agent pool](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) is automatically exposed to the internet.</span><span class="sxs-lookup"><span data-stu-id="82e34-104">Any DC/OS container in the ACS [public agent pool](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) is automatically exposed to the internet.</span></span> <span data-ttu-id="82e34-105">By default, ports **80**, **443**, **8080** are opened, and any (public) container listening on those ports are accessible.</span><span class="sxs-lookup"><span data-stu-id="82e34-105">By default, ports **80**, **443**, **8080** are opened, and any (public) container listening on those ports are accessible.</span></span> <span data-ttu-id="82e34-106">This article shows you how to open more ports for your applications in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="82e34-106">This article shows you how to open more ports for your applications in Azure Container Service.</span></span>

## <a name="open-a-port-portal"></a><span data-ttu-id="82e34-107">Open a port (portal)</span><span class="sxs-lookup"><span data-stu-id="82e34-107">Open a port (portal)</span></span>
<span data-ttu-id="82e34-108">First, we need to open the port we want.</span><span class="sxs-lookup"><span data-stu-id="82e34-108">First, we need to open the port we want.</span></span>

1. <span data-ttu-id="82e34-109">Log in to the portal.</span><span class="sxs-lookup"><span data-stu-id="82e34-109">Log in to the portal.</span></span>
2. <span data-ttu-id="82e34-110">Find the resource group that you deployed the Azure Container Service to.</span><span class="sxs-lookup"><span data-stu-id="82e34-110">Find the resource group that you deployed the Azure Container Service to.</span></span>
3. <span data-ttu-id="82e34-111">Select the agent load balancer (which is named similar to **XXXX-agent-lb-XXXX**).</span><span class="sxs-lookup"><span data-stu-id="82e34-111">Select the agent load balancer (which is named similar to **XXXX-agent-lb-XXXX**).</span></span>
   
    ![Azure container service load balancer](./media/container-service-enable-public-access/agent-load-balancer.png)
4. <span data-ttu-id="82e34-113">Click **Probes** and then **Add**.</span><span class="sxs-lookup"><span data-stu-id="82e34-113">Click **Probes** and then **Add**.</span></span>
   
    ![Azure container service load balancer probes](./media/container-service-enable-public-access/add-probe.png)
5. <span data-ttu-id="82e34-115">Fill out the probe form and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="82e34-115">Fill out the probe form and click **OK**.</span></span>
   
   | <span data-ttu-id="82e34-116">Field</span><span class="sxs-lookup"><span data-stu-id="82e34-116">Field</span></span> | <span data-ttu-id="82e34-117">Description</span><span class="sxs-lookup"><span data-stu-id="82e34-117">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="82e34-118">Name</span><span class="sxs-lookup"><span data-stu-id="82e34-118">Name</span></span> |<span data-ttu-id="82e34-119">A descriptive name of the probe.</span><span class="sxs-lookup"><span data-stu-id="82e34-119">A descriptive name of the probe.</span></span> |
   | <span data-ttu-id="82e34-120">Port</span><span class="sxs-lookup"><span data-stu-id="82e34-120">Port</span></span> |<span data-ttu-id="82e34-121">The port of the container to test.</span><span class="sxs-lookup"><span data-stu-id="82e34-121">The port of the container to test.</span></span> |
   | <span data-ttu-id="82e34-122">Path</span><span class="sxs-lookup"><span data-stu-id="82e34-122">Path</span></span> |<span data-ttu-id="82e34-123">(When in HTTP mode) The relative website path to probe.</span><span class="sxs-lookup"><span data-stu-id="82e34-123">(When in HTTP mode) The relative website path to probe.</span></span> <span data-ttu-id="82e34-124">HTTPS not supported.</span><span class="sxs-lookup"><span data-stu-id="82e34-124">HTTPS not supported.</span></span> |
   | <span data-ttu-id="82e34-125">Interval</span><span class="sxs-lookup"><span data-stu-id="82e34-125">Interval</span></span> |<span data-ttu-id="82e34-126">The amount of time between probe attempts, in seconds.</span><span class="sxs-lookup"><span data-stu-id="82e34-126">The amount of time between probe attempts, in seconds.</span></span> |
   | <span data-ttu-id="82e34-127">Unhealthy threshold</span><span class="sxs-lookup"><span data-stu-id="82e34-127">Unhealthy threshold</span></span> |<span data-ttu-id="82e34-128">Number of consecutive probe attempts before considering the container unhealthy.</span><span class="sxs-lookup"><span data-stu-id="82e34-128">Number of consecutive probe attempts before considering the container unhealthy.</span></span> |
6. <span data-ttu-id="82e34-129">Back at the properties of the agent load balancer, click **Load balancing rules** and then **Add**.</span><span class="sxs-lookup"><span data-stu-id="82e34-129">Back at the properties of the agent load balancer, click **Load balancing rules** and then **Add**.</span></span>
   
    ![Azure container service load balancer rules](./media/container-service-enable-public-access/add-balancer-rule.png)
7. <span data-ttu-id="82e34-131">Fill out the load balancer form and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="82e34-131">Fill out the load balancer form and click **OK**.</span></span>
   
   | <span data-ttu-id="82e34-132">Field</span><span class="sxs-lookup"><span data-stu-id="82e34-132">Field</span></span> | <span data-ttu-id="82e34-133">Description</span><span class="sxs-lookup"><span data-stu-id="82e34-133">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="82e34-134">Name</span><span class="sxs-lookup"><span data-stu-id="82e34-134">Name</span></span> |<span data-ttu-id="82e34-135">A descriptive name of the load balancer.</span><span class="sxs-lookup"><span data-stu-id="82e34-135">A descriptive name of the load balancer.</span></span> |
   | <span data-ttu-id="82e34-136">Port</span><span class="sxs-lookup"><span data-stu-id="82e34-136">Port</span></span> |<span data-ttu-id="82e34-137">The public incoming port.</span><span class="sxs-lookup"><span data-stu-id="82e34-137">The public incoming port.</span></span> |
   | <span data-ttu-id="82e34-138">Backend port</span><span class="sxs-lookup"><span data-stu-id="82e34-138">Backend port</span></span> |<span data-ttu-id="82e34-139">The internal-public port of the container to route traffic to.</span><span class="sxs-lookup"><span data-stu-id="82e34-139">The internal-public port of the container to route traffic to.</span></span> |
   | <span data-ttu-id="82e34-140">Backend pool</span><span class="sxs-lookup"><span data-stu-id="82e34-140">Backend pool</span></span> |<span data-ttu-id="82e34-141">The containers in this pool will be the target for this load balancer.</span><span class="sxs-lookup"><span data-stu-id="82e34-141">The containers in this pool will be the target for this load balancer.</span></span> |
   | <span data-ttu-id="82e34-142">Probe</span><span class="sxs-lookup"><span data-stu-id="82e34-142">Probe</span></span> |<span data-ttu-id="82e34-143">The probe used to determine if a target in the **Backend pool** is healthy.</span><span class="sxs-lookup"><span data-stu-id="82e34-143">The probe used to determine if a target in the **Backend pool** is healthy.</span></span> |
   | <span data-ttu-id="82e34-144">Session persistence</span><span class="sxs-lookup"><span data-stu-id="82e34-144">Session persistence</span></span> |<span data-ttu-id="82e34-145">Determines how traffic from a client should be handled for the duration of the session.</span><span class="sxs-lookup"><span data-stu-id="82e34-145">Determines how traffic from a client should be handled for the duration of the session.</span></span><br><br><span data-ttu-id="82e34-146">**None**: Successive requests from the same client can be handled by any container.</span><span class="sxs-lookup"><span data-stu-id="82e34-146">**None**: Successive requests from the same client can be handled by any container.</span></span><br><span data-ttu-id="82e34-147">**Client IP**: Successive requests from the same client IP are handled by the same container.</span><span class="sxs-lookup"><span data-stu-id="82e34-147">**Client IP**: Successive requests from the same client IP are handled by the same container.</span></span><br><span data-ttu-id="82e34-148">**Client IP and protocol**: Successive requests from the same client IP and protocol combination are handled by the same container.</span><span class="sxs-lookup"><span data-stu-id="82e34-148">**Client IP and protocol**: Successive requests from the same client IP and protocol combination are handled by the same container.</span></span> |
   | <span data-ttu-id="82e34-149">Idle timeout</span><span class="sxs-lookup"><span data-stu-id="82e34-149">Idle timeout</span></span> |<span data-ttu-id="82e34-150">(TCP only) In minutes, the time to keep a TCP/HTTP client open without relying on *keep-alive* messages.</span><span class="sxs-lookup"><span data-stu-id="82e34-150">(TCP only) In minutes, the time to keep a TCP/HTTP client open without relying on *keep-alive* messages.</span></span> |

## <a name="add-a-security-rule-portal"></a><span data-ttu-id="82e34-151">Add a security rule (portal)</span><span class="sxs-lookup"><span data-stu-id="82e34-151">Add a security rule (portal)</span></span>
<span data-ttu-id="82e34-152">Next, we need to add a security rule that routes traffic from our opened port through the firewall.</span><span class="sxs-lookup"><span data-stu-id="82e34-152">Next, we need to add a security rule that routes traffic from our opened port through the firewall.</span></span>

1. <span data-ttu-id="82e34-153">Log in to the portal.</span><span class="sxs-lookup"><span data-stu-id="82e34-153">Log in to the portal.</span></span>
2. <span data-ttu-id="82e34-154">Find the resource group that you deployed the Azure Container Service to.</span><span class="sxs-lookup"><span data-stu-id="82e34-154">Find the resource group that you deployed the Azure Container Service to.</span></span>
3. <span data-ttu-id="82e34-155">Select the **public** agent network security group (which is named similar to **XXXX-agent-public-nsg-XXXX**).</span><span class="sxs-lookup"><span data-stu-id="82e34-155">Select the **public** agent network security group (which is named similar to **XXXX-agent-public-nsg-XXXX**).</span></span>
   
    ![Azure container service network security group](./media/container-service-enable-public-access/agent-nsg.png)
4. <span data-ttu-id="82e34-157">Select **Inbound security rules** and then **Add**.</span><span class="sxs-lookup"><span data-stu-id="82e34-157">Select **Inbound security rules** and then **Add**.</span></span>
   
    ![Azure container service network security group rules](./media/container-service-enable-public-access/add-firewall-rule.png)
5. <span data-ttu-id="82e34-159">Fill out the firewall rule to allow your public port and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="82e34-159">Fill out the firewall rule to allow your public port and click **OK**.</span></span>
   
   | <span data-ttu-id="82e34-160">Field</span><span class="sxs-lookup"><span data-stu-id="82e34-160">Field</span></span> | <span data-ttu-id="82e34-161">Description</span><span class="sxs-lookup"><span data-stu-id="82e34-161">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="82e34-162">Name</span><span class="sxs-lookup"><span data-stu-id="82e34-162">Name</span></span> |<span data-ttu-id="82e34-163">A descriptive name of the firewall rule.</span><span class="sxs-lookup"><span data-stu-id="82e34-163">A descriptive name of the firewall rule.</span></span> |
   | <span data-ttu-id="82e34-164">Priority</span><span class="sxs-lookup"><span data-stu-id="82e34-164">Priority</span></span> |<span data-ttu-id="82e34-165">Priority rank for the rule.</span><span class="sxs-lookup"><span data-stu-id="82e34-165">Priority rank for the rule.</span></span> <span data-ttu-id="82e34-166">The lower the number the higher the priority.</span><span class="sxs-lookup"><span data-stu-id="82e34-166">The lower the number the higher the priority.</span></span> |
   | <span data-ttu-id="82e34-167">Source</span><span class="sxs-lookup"><span data-stu-id="82e34-167">Source</span></span> |<span data-ttu-id="82e34-168">Restrict the incoming IP address range to be allowed or denied by this rule.</span><span class="sxs-lookup"><span data-stu-id="82e34-168">Restrict the incoming IP address range to be allowed or denied by this rule.</span></span> <span data-ttu-id="82e34-169">Use **Any** to not specify a restriction.</span><span class="sxs-lookup"><span data-stu-id="82e34-169">Use **Any** to not specify a restriction.</span></span> |
   | <span data-ttu-id="82e34-170">Service</span><span class="sxs-lookup"><span data-stu-id="82e34-170">Service</span></span> |<span data-ttu-id="82e34-171">Select a set of predefined services this security rule is for.</span><span class="sxs-lookup"><span data-stu-id="82e34-171">Select a set of predefined services this security rule is for.</span></span> <span data-ttu-id="82e34-172">Otherwise use **Custom** to create your own.</span><span class="sxs-lookup"><span data-stu-id="82e34-172">Otherwise use **Custom** to create your own.</span></span> |
   | <span data-ttu-id="82e34-173">Protocol</span><span class="sxs-lookup"><span data-stu-id="82e34-173">Protocol</span></span> |<span data-ttu-id="82e34-174">Restrict traffic based on **TCP** or **UDP**.</span><span class="sxs-lookup"><span data-stu-id="82e34-174">Restrict traffic based on **TCP** or **UDP**.</span></span> <span data-ttu-id="82e34-175">Use **Any** to not specify a restriction.</span><span class="sxs-lookup"><span data-stu-id="82e34-175">Use **Any** to not specify a restriction.</span></span> |
   | <span data-ttu-id="82e34-176">Port range</span><span class="sxs-lookup"><span data-stu-id="82e34-176">Port range</span></span> |<span data-ttu-id="82e34-177">When **Service** is **Custom**, specifies the range of ports that this rule affects.</span><span class="sxs-lookup"><span data-stu-id="82e34-177">When **Service** is **Custom**, specifies the range of ports that this rule affects.</span></span> <span data-ttu-id="82e34-178">You can use a single port, such as **80**, or a range like **1024-1500**.</span><span class="sxs-lookup"><span data-stu-id="82e34-178">You can use a single port, such as **80**, or a range like **1024-1500**.</span></span> |
   | <span data-ttu-id="82e34-179">Action</span><span class="sxs-lookup"><span data-stu-id="82e34-179">Action</span></span> |<span data-ttu-id="82e34-180">Allow or deny traffic that meets the criteria.</span><span class="sxs-lookup"><span data-stu-id="82e34-180">Allow or deny traffic that meets the criteria.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="82e34-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="82e34-181">Next steps</span></span>
<span data-ttu-id="82e34-182">Learn about the difference between [public and private DC/OS agents](container-service-dcos-agents.md).</span><span class="sxs-lookup"><span data-stu-id="82e34-182">Learn about the difference between [public and private DC/OS agents](container-service-dcos-agents.md).</span></span>

<span data-ttu-id="82e34-183">Read more information about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="82e34-183">Read more information about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

