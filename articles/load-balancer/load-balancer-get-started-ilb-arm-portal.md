---
title: Create an Internal load balancer - Azure portal | Microsoft Docs
description: Learn how to create an Internal load balancer in Resource Manager using the Azure portal
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: 1ac14fb9-8d14-4892-bfe6-8bc74c48ae2c
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 8fbe9d5d04d745de51e0e41516d6c12683c98637
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551510"
---
# <a name="create-an-internal-load-balancer-in-the-azure-portal"></a><span data-ttu-id="55df3-103">Create an Internal load balancer in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="55df3-103">Create an Internal load balancer in the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [Azure Portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Template](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).  This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a><span data-ttu-id="55df3-110">Get started creating an Internal load balancer using Azure portal</span><span class="sxs-lookup"><span data-stu-id="55df3-110">Get started creating an Internal load balancer using Azure portal</span></span>

<span data-ttu-id="55df3-111">Use the following steps to create an internal load balancer from the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="55df3-111">Use the following steps to create an internal load balancer from the Azure Portal.</span></span>

1. <span data-ttu-id="55df3-112">Open a browser, navigate to the [Azure portal](http://portal.azure.com), and sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="55df3-112">Open a browser, navigate to the [Azure portal](http://portal.azure.com), and sign in with your Azure account.</span></span>
2. <span data-ttu-id="55df3-113">In the upper left hand side of the screen, click **New** > **Networking** > **Load balancer**.</span><span class="sxs-lookup"><span data-stu-id="55df3-113">In the upper left hand side of the screen, click **New** > **Networking** > **Load balancer**.</span></span>
3. <span data-ttu-id="55df3-114">In the **Create load balancer** blade, enter a **Name** for your load balancer.</span><span class="sxs-lookup"><span data-stu-id="55df3-114">In the **Create load balancer** blade, enter a **Name** for your load balancer.</span></span>
4. <span data-ttu-id="55df3-115">Under **Scheme**, click **Internal**.</span><span class="sxs-lookup"><span data-stu-id="55df3-115">Under **Scheme**, click **Internal**.</span></span>
5. <span data-ttu-id="55df3-116">Click **Virtual network**, and then select the virtual network where you want to create the load balancer.</span><span class="sxs-lookup"><span data-stu-id="55df3-116">Click **Virtual network**, and then select the virtual network where you want to create the load balancer.</span></span>

   > [!NOTE]
   > If you do not see the virtual network you want to use, check the **Location** you are using for the load balancer, and change it accordingly.

6. <span data-ttu-id="55df3-118">Click **Subnet**, and then select the subnet where you want to create the load balancer.</span><span class="sxs-lookup"><span data-stu-id="55df3-118">Click **Subnet**, and then select the subnet where you want to create the load balancer.</span></span>
7. <span data-ttu-id="55df3-119">Under **IP address assignment**, click either **Dynamic** or **Static**, depending on whether you want the IP address for the load balancer to be fixed (static) or not.</span><span class="sxs-lookup"><span data-stu-id="55df3-119">Under **IP address assignment**, click either **Dynamic** or **Static**, depending on whether you want the IP address for the load balancer to be fixed (static) or not.</span></span>

   > [!NOTE]
   > If you select to use a static IP address, you will have to provide an address for the load balancer.

8. <span data-ttu-id="55df3-121">Under **Resource group** either specify the name of a new resource group for the load balancer, or click **select existing** and select an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="55df3-121">Under **Resource group** either specify the name of a new resource group for the load balancer, or click **select existing** and select an existing resource group.</span></span>
9. <span data-ttu-id="55df3-122">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="55df3-122">Click **Create**.</span></span>

## <a name="configure-load-balancing-rules"></a><span data-ttu-id="55df3-123">Configure load balancing rules</span><span class="sxs-lookup"><span data-stu-id="55df3-123">Configure load balancing rules</span></span>

<span data-ttu-id="55df3-124">After the load balancer creation, navigate to the load balancer resource to configure it.</span><span class="sxs-lookup"><span data-stu-id="55df3-124">After the load balancer creation, navigate to the load balancer resource to configure it.</span></span>
<span data-ttu-id="55df3-125">You need to configure first a back-end address pool and a probe before configuring a load balancing rule.</span><span class="sxs-lookup"><span data-stu-id="55df3-125">You need to configure first a back-end address pool and a probe before configuring a load balancing rule.</span></span>

### <a name="step-1-configure-a-back-end-pool"></a><span data-ttu-id="55df3-126">Step 1: Configure a back-end pool</span><span class="sxs-lookup"><span data-stu-id="55df3-126">Step 1: Configure a back-end pool</span></span>

1. <span data-ttu-id="55df3-127">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span><span class="sxs-lookup"><span data-stu-id="55df3-127">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span></span>
2. <span data-ttu-id="55df3-128">In the **Settings** blade, click **Backend pools**.</span><span class="sxs-lookup"><span data-stu-id="55df3-128">In the **Settings** blade, click **Backend pools**.</span></span>
3. <span data-ttu-id="55df3-129">In the **Backend address pools** blade, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="55df3-129">In the **Backend address pools** blade, click **Add**.</span></span>
4. <span data-ttu-id="55df3-130">In the **Add backend pool** blade, enter a **Name** for the backend pool, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="55df3-130">In the **Add backend pool** blade, enter a **Name** for the backend pool, and then click **OK**.</span></span>

### <a name="step-2-configure-a-probe"></a><span data-ttu-id="55df3-131">Step 2: Configure a probe</span><span class="sxs-lookup"><span data-stu-id="55df3-131">Step 2: Configure a probe</span></span>

1. <span data-ttu-id="55df3-132">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span><span class="sxs-lookup"><span data-stu-id="55df3-132">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span></span>
2. <span data-ttu-id="55df3-133">In the **Settings** blade, click **Probes**.</span><span class="sxs-lookup"><span data-stu-id="55df3-133">In the **Settings** blade, click **Probes**.</span></span>
3. <span data-ttu-id="55df3-134">In the **Probes**  blade, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="55df3-134">In the **Probes**  blade, click **Add**.</span></span>
4. <span data-ttu-id="55df3-135">In the **Add probe** blade, enter a **Name** for the probe.</span><span class="sxs-lookup"><span data-stu-id="55df3-135">In the **Add probe** blade, enter a **Name** for the probe.</span></span>
5. <span data-ttu-id="55df3-136">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span><span class="sxs-lookup"><span data-stu-id="55df3-136">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="55df3-137">Under **Port**, specify the port to use when accessing the probe.</span><span class="sxs-lookup"><span data-stu-id="55df3-137">Under **Port**, specify the port to use when accessing the probe.</span></span>
7. <span data-ttu-id="55df3-138">Under **Path** (for HTTP probes only), specify the path to use as a probe.</span><span class="sxs-lookup"><span data-stu-id="55df3-138">Under **Path** (for HTTP probes only), specify the path to use as a probe.</span></span>
8. <span data-ttu-id="55df3-139">Under **Interval** specify how frequently to probe the application.</span><span class="sxs-lookup"><span data-stu-id="55df3-139">Under **Interval** specify how frequently to probe the application.</span></span>
9. <span data-ttu-id="55df3-140">Under **Unhealthy threshold**, specify how many attempts should fail before the backend virtual machine is marked as unhealthy.</span><span class="sxs-lookup"><span data-stu-id="55df3-140">Under **Unhealthy threshold**, specify how many attempts should fail before the backend virtual machine is marked as unhealthy.</span></span>
10. <span data-ttu-id="55df3-141">Click **OK** to create probe.</span><span class="sxs-lookup"><span data-stu-id="55df3-141">Click **OK** to create probe.</span></span>

### <a name="step-3-configure-load-balancing-rules"></a><span data-ttu-id="55df3-142">Step 3: Configure load balancing rules</span><span class="sxs-lookup"><span data-stu-id="55df3-142">Step 3: Configure load balancing rules</span></span>

1. <span data-ttu-id="55df3-143">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span><span class="sxs-lookup"><span data-stu-id="55df3-143">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span></span>
2. <span data-ttu-id="55df3-144">In the **Settings** blade, click **Load balancing rules**.</span><span class="sxs-lookup"><span data-stu-id="55df3-144">In the **Settings** blade, click **Load balancing rules**.</span></span>
3. <span data-ttu-id="55df3-145">In the **Load balancing rules** blade, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="55df3-145">In the **Load balancing rules** blade, click **Add**.</span></span>
4. <span data-ttu-id="55df3-146">In the **Add load balancing rule** blade, enter a **Name** for the rule.</span><span class="sxs-lookup"><span data-stu-id="55df3-146">In the **Add load balancing rule** blade, enter a **Name** for the rule.</span></span>
5. <span data-ttu-id="55df3-147">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span><span class="sxs-lookup"><span data-stu-id="55df3-147">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="55df3-148">Under **Port**, specify the port clients connect to in the load balancer.</span><span class="sxs-lookup"><span data-stu-id="55df3-148">Under **Port**, specify the port clients connect to in the load balancer.</span></span>
7. <span data-ttu-id="55df3-149">Under **Backend port**, specify the port to be used in the backend pool (usually, the load balancer port and the backend port are the same).</span><span class="sxs-lookup"><span data-stu-id="55df3-149">Under **Backend port**, specify the port to be used in the backend pool (usually, the load balancer port and the backend port are the same).</span></span>
8. <span data-ttu-id="55df3-150">Under **Backend pool**, select the backend pool you created above.</span><span class="sxs-lookup"><span data-stu-id="55df3-150">Under **Backend pool**, select the backend pool you created above.</span></span>
9. <span data-ttu-id="55df3-151">Under **Session persistence**, select how you want sessions to persist.</span><span class="sxs-lookup"><span data-stu-id="55df3-151">Under **Session persistence**, select how you want sessions to persist.</span></span>
10. <span data-ttu-id="55df3-152">Under **Idle timeout (minutes)**, specify the idle timeout.</span><span class="sxs-lookup"><span data-stu-id="55df3-152">Under **Idle timeout (minutes)**, specify the idle timeout.</span></span>
11. <span data-ttu-id="55df3-153">Under **Floating IP (direct server return)**, click **Disabled** or **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="55df3-153">Under **Floating IP (direct server return)**, click **Disabled** or **Enabled**.</span></span>
12. <span data-ttu-id="55df3-154">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="55df3-154">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55df3-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="55df3-155">Next steps</span></span>

[<span data-ttu-id="55df3-156">Configure a load balancer distribution mode</span><span class="sxs-lookup"><span data-stu-id="55df3-156">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="55df3-157">Configure idle TCP timeout settings for your load balancer</span><span class="sxs-lookup"><span data-stu-id="55df3-157">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

