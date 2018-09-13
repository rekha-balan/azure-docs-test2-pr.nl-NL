---
title: Create Virtual Machines in Azure Government | Microsoft Docs
description: This tutorial shows steps for creating Virtual Machines with Azure Government
services: azure-government
cloud: gov
documentationcenter: ''
author: Juliako
manager: femila
ms.service: azure-government
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 08/10/2018
ms.author: yujhongmicrosoft; juliako
ms.openlocfilehash: 7010f76e5e679cff5c9c875154f05aa969b088f9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856781"
---
# <a name="tutorial-create-virtual-machines"></a><span data-ttu-id="e8329-103">Tutorial: Create Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="e8329-103">Tutorial: Create Virtual Machines</span></span> 

<span data-ttu-id="e8329-104">Microsoft Azure Government delivers a dedicated cloud with world-class security and compliance, enabling US government agencies and their partners to transform their workloads to the cloud.</span><span class="sxs-lookup"><span data-stu-id="e8329-104">Microsoft Azure Government delivers a dedicated cloud with world-class security and compliance, enabling US government agencies and their partners to transform their workloads to the cloud.</span></span> <span data-ttu-id="e8329-105">For example, your workload may include using virtual machines.</span><span class="sxs-lookup"><span data-stu-id="e8329-105">For example, your workload may include using virtual machines.</span></span> <span data-ttu-id="e8329-106">Before provisioning a VM, you need to create and configure a virtual network for your environment.</span><span class="sxs-lookup"><span data-stu-id="e8329-106">Before provisioning a VM, you need to create and configure a virtual network for your environment.</span></span> <span data-ttu-id="e8329-107">A virtual network enables resources to securely communicate with each other (within Azure and with servers accessing Azure).</span><span class="sxs-lookup"><span data-stu-id="e8329-107">A virtual network enables resources to securely communicate with each other (within Azure and with servers accessing Azure).</span></span>

<span data-ttu-id="e8329-108">This tutorial shows how to connect to Azure Government, create a virtual network and a virtual machine on this network in Azure Government cloud.</span><span class="sxs-lookup"><span data-stu-id="e8329-108">This tutorial shows how to connect to Azure Government, create a virtual network and a virtual machine on this network in Azure Government cloud.</span></span> <span data-ttu-id="e8329-109">The Azure Government marketplace provides a VM library, in this tutorial we use "Data Science Virtual Machine - Windows 2016 CSP".</span><span class="sxs-lookup"><span data-stu-id="e8329-109">The Azure Government marketplace provides a VM library, in this tutorial we use "Data Science Virtual Machine - Windows 2016 CSP".</span></span> <span data-ttu-id="e8329-110">To learn more about Azure Virtual Machines and see end-to-end scenarios, see [Virtual Machines Documentation](../virtual-machines/index.yml).</span><span class="sxs-lookup"><span data-stu-id="e8329-110">To learn more about Azure Virtual Machines and see end-to-end scenarios, see [Virtual Machines Documentation](../virtual-machines/index.yml).</span></span>

<span data-ttu-id="e8329-111">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="e8329-111">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e8329-112">Connect to Azure Government</span><span class="sxs-lookup"><span data-stu-id="e8329-112">Connect to Azure Government</span></span>
> * <span data-ttu-id="e8329-113">Create a Virtual Network</span><span class="sxs-lookup"><span data-stu-id="e8329-113">Create a Virtual Network</span></span>
> * <span data-ttu-id="e8329-114">Create a Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="e8329-114">Create a Virtual Machine</span></span>

> [!VIDEO https://www.youtube.com/embed/cyucpJXKMRs]

<span data-ttu-id="e8329-115">If you don't have an Azure Government subscription, create a [free account](https://azure.microsoft.com/global-infrastructure/government/request/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="e8329-115">If you don't have an Azure Government subscription, create a [free account](https://azure.microsoft.com/global-infrastructure/government/request/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8329-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e8329-116">Prerequisites</span></span>

* <span data-ttu-id="e8329-117">Review [Guidance for developers](documentation-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="e8329-117">Review [Guidance for developers](documentation-government-developer-guide.md).</span></span><br/> <span data-ttu-id="e8329-118">This article discusses Azure Government's unique URLs and endpoints for managing your environment.</span><span class="sxs-lookup"><span data-stu-id="e8329-118">This article discusses Azure Government's unique URLs and endpoints for managing your environment.</span></span> <span data-ttu-id="e8329-119">You must know about these endpoints in order to connect to Azure Government.</span><span class="sxs-lookup"><span data-stu-id="e8329-119">You must know about these endpoints in order to connect to Azure Government.</span></span> 
* <span data-ttu-id="e8329-120">Review [Compare Azure Government and global Azure](compare-azure-government-global-azure.md) and click on a service of interest to see variations between Azure Government and global Azure.</span><span class="sxs-lookup"><span data-stu-id="e8329-120">Review [Compare Azure Government and global Azure](compare-azure-government-global-azure.md) and click on a service of interest to see variations between Azure Government and global Azure.</span></span>

## <a name="sign-in-to-azure-government"></a><span data-ttu-id="e8329-121">Sign in to Azure Government</span><span class="sxs-lookup"><span data-stu-id="e8329-121">Sign in to Azure Government</span></span> 

<span data-ttu-id="e8329-122">To connect, browse to the portal at [https://portal.azure.us](https://portal.azure.us) and sign in with your Azure Government credentials.</span><span class="sxs-lookup"><span data-stu-id="e8329-122">To connect, browse to the portal at [https://portal.azure.us](https://portal.azure.us) and sign in with your Azure Government credentials.</span></span> 

<span data-ttu-id="e8329-123">Once you sign in, you should see "Microsoft Azure Government" in the upper left of the main navigation bar.</span><span class="sxs-lookup"><span data-stu-id="e8329-123">Once you sign in, you should see "Microsoft Azure Government" in the upper left of the main navigation bar.</span></span>

![Azure Government Portal](./media/connect-with-portal/azure-gov-portal.png)

## <a name="create-a-new-virtual-network"></a><span data-ttu-id="e8329-125">Create a new Virtual Network</span><span class="sxs-lookup"><span data-stu-id="e8329-125">Create a new Virtual Network</span></span>
 
<span data-ttu-id="e8329-126">Click on **Create a resource** in the upper left corner on the portal and click on **Networking** > **Virtual Network**.</span><span class="sxs-lookup"><span data-stu-id="e8329-126">Click on **Create a resource** in the upper left corner on the portal and click on **Networking** > **Virtual Network**.</span></span> 

![createvn1](./media/create-virtual-machines/documentation-government-quickstarts-vm1.png)

<span data-ttu-id="e8329-128">In the **Create Virtual Network** dialog, use the following settings.</span><span class="sxs-lookup"><span data-stu-id="e8329-128">In the **Create Virtual Network** dialog, use the following settings.</span></span>

| <span data-ttu-id="e8329-129">Setting</span><span class="sxs-lookup"><span data-stu-id="e8329-129">Setting</span></span> | <span data-ttu-id="e8329-130">Suggested Value</span><span class="sxs-lookup"><span data-stu-id="e8329-130">Suggested Value</span></span> | <span data-ttu-id="e8329-131">Description</span><span class="sxs-lookup"><span data-stu-id="e8329-131">Description</span></span> |
|-|-|-|
| <span data-ttu-id="e8329-132">Name</span><span class="sxs-lookup"><span data-stu-id="e8329-132">Name</span></span>| <span data-ttu-id="e8329-133">vnettest</span><span class="sxs-lookup"><span data-stu-id="e8329-133">vnettest</span></span> | <span data-ttu-id="e8329-134">Name of the Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="e8329-134">Name of the Virtual Network.</span></span> |
| <span data-ttu-id="e8329-135">Address space</span><span class="sxs-lookup"><span data-stu-id="e8329-135">Address space</span></span> | <span data-ttu-id="e8329-136">10.128.0.0/24</span><span class="sxs-lookup"><span data-stu-id="e8329-136">10.128.0.0/24</span></span> | <span data-ttu-id="e8329-137">The Virtual Network address range.</span><span class="sxs-lookup"><span data-stu-id="e8329-137">The Virtual Network address range.</span></span> |
| <span data-ttu-id="e8329-138">Subscription</span><span class="sxs-lookup"><span data-stu-id="e8329-138">Subscription</span></span> | <span data-ttu-id="e8329-139">Azure Government Free Trial</span><span class="sxs-lookup"><span data-stu-id="e8329-139">Azure Government Free Trial</span></span> | |
| <span data-ttu-id="e8329-140">Resource group</span><span class="sxs-lookup"><span data-stu-id="e8329-140">Resource group</span></span>|<span data-ttu-id="e8329-141">vnettestgroup</span><span class="sxs-lookup"><span data-stu-id="e8329-141">vnettestgroup</span></span>|<span data-ttu-id="e8329-142">Create a new resource group.</span><span class="sxs-lookup"><span data-stu-id="e8329-142">Create a new resource group.</span></span>|
| <span data-ttu-id="e8329-143">Location</span><span class="sxs-lookup"><span data-stu-id="e8329-143">Location</span></span> | <span data-ttu-id="e8329-144">USGov Virginia</span><span class="sxs-lookup"><span data-stu-id="e8329-144">USGov Virginia</span></span> |<span data-ttu-id="e8329-145">Choose one of the Azure Government locations.</span><span class="sxs-lookup"><span data-stu-id="e8329-145">Choose one of the Azure Government locations.</span></span>|
| <span data-ttu-id="e8329-146">Subnet</span><span class="sxs-lookup"><span data-stu-id="e8329-146">Subnet</span></span> | <span data-ttu-id="e8329-147">vnetsubnet</span><span class="sxs-lookup"><span data-stu-id="e8329-147">vnetsubnet</span></span>||
| <span data-ttu-id="e8329-148">Address range</span><span class="sxs-lookup"><span data-stu-id="e8329-148">Address range</span></span> |<span data-ttu-id="e8329-149">10.128.0.0/26</span><span class="sxs-lookup"><span data-stu-id="e8329-149">10.128.0.0/26</span></span>|<span data-ttu-id="e8329-150">The subnet's address range in CIDR notation (for example, 192.168.1.0/24).</span><span class="sxs-lookup"><span data-stu-id="e8329-150">The subnet's address range in CIDR notation (for example, 192.168.1.0/24).</span></span> <span data-ttu-id="e8329-151">It must be contained by the address space of the virtual network.</span><span class="sxs-lookup"><span data-stu-id="e8329-151">It must be contained by the address space of the virtual network.</span></span> <span data-ttu-id="e8329-152">The address range of a subnet, which is in use can't be edited.</span><span class="sxs-lookup"><span data-stu-id="e8329-152">The address range of a subnet, which is in use can't be edited.</span></span>|

<span data-ttu-id="e8329-153">Navigate to **Virtual networks** from the menu on the left and click on the Virtual Network you created.</span><span class="sxs-lookup"><span data-stu-id="e8329-153">Navigate to **Virtual networks** from the menu on the left and click on the Virtual Network you created.</span></span> <span data-ttu-id="e8329-154">Under **Settings** click **Subnets**.</span><span class="sxs-lookup"><span data-stu-id="e8329-154">Under **Settings** click **Subnets**.</span></span>

![createvn3](./media/create-virtual-machines/documentation-government-quickstarts-vm3.png)

<span data-ttu-id="e8329-156">On the top left-hand corner of the page choose **Subnet**.</span><span class="sxs-lookup"><span data-stu-id="e8329-156">On the top left-hand corner of the page choose **Subnet**.</span></span> <span data-ttu-id="e8329-157">In the **Add subnet** dialog, use the following settings.</span><span class="sxs-lookup"><span data-stu-id="e8329-157">In the **Add subnet** dialog, use the following settings.</span></span>

| <span data-ttu-id="e8329-158">Setting</span><span class="sxs-lookup"><span data-stu-id="e8329-158">Setting</span></span> | <span data-ttu-id="e8329-159">Suggested Value</span><span class="sxs-lookup"><span data-stu-id="e8329-159">Suggested Value</span></span> | <span data-ttu-id="e8329-160">Description</span><span class="sxs-lookup"><span data-stu-id="e8329-160">Description</span></span> |
|-|-|-|
|<span data-ttu-id="e8329-161">Name</span><span class="sxs-lookup"><span data-stu-id="e8329-161">Name</span></span>|<span data-ttu-id="e8329-162">subnet-vnet</span><span class="sxs-lookup"><span data-stu-id="e8329-162">subnet-vnet</span></span>|<span data-ttu-id="e8329-163">The name of the virtual network.</span><span class="sxs-lookup"><span data-stu-id="e8329-163">The name of the virtual network.</span></span>|
|<span data-ttu-id="e8329-164">Address range</span><span class="sxs-lookup"><span data-stu-id="e8329-164">Address range</span></span>|<span data-ttu-id="e8329-165">10.128.0.64/28</span><span class="sxs-lookup"><span data-stu-id="e8329-165">10.128.0.64/28</span></span>|<span data-ttu-id="e8329-166">The subnet's address range in CIDR notation (for example, 192.168.1.0/24).</span><span class="sxs-lookup"><span data-stu-id="e8329-166">The subnet's address range in CIDR notation (for example, 192.168.1.0/24).</span></span> <span data-ttu-id="e8329-167">It must be contained by the address space of the virtual network.</span><span class="sxs-lookup"><span data-stu-id="e8329-167">It must be contained by the address space of the virtual network.</span></span> <span data-ttu-id="e8329-168">The address range of a subnet, which is in use can't be edited.</span><span class="sxs-lookup"><span data-stu-id="e8329-168">The address range of a subnet, which is in use can't be edited.</span></span>|
|<span data-ttu-id="e8329-169">Network security group</span><span class="sxs-lookup"><span data-stu-id="e8329-169">Network security group</span></span>|<span data-ttu-id="e8329-170">None</span><span class="sxs-lookup"><span data-stu-id="e8329-170">None</span></span>||
|<span data-ttu-id="e8329-171">Route table</span><span class="sxs-lookup"><span data-stu-id="e8329-171">Route table</span></span>|<span data-ttu-id="e8329-172">None</span><span class="sxs-lookup"><span data-stu-id="e8329-172">None</span></span>||

<span data-ttu-id="e8329-173">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="e8329-173">Click **Ok**.</span></span> <span data-ttu-id="e8329-174">When finished select **Gateway Subnet** from the top of the window.</span><span class="sxs-lookup"><span data-stu-id="e8329-174">When finished select **Gateway Subnet** from the top of the window.</span></span> 

![createvn6](./media/create-virtual-machines/documentation-government-quickstarts-vm7.png)

<span data-ttu-id="e8329-176">You will have address range shown below.</span><span class="sxs-lookup"><span data-stu-id="e8329-176">You will have address range shown below.</span></span> <span data-ttu-id="e8329-177">Press **Ok**.</span><span class="sxs-lookup"><span data-stu-id="e8329-177">Press **Ok**.</span></span>  

![createvn7](./media/create-virtual-machines/documentation-government-quickstarts-vm8.png)
  
<span data-ttu-id="e8329-179">At the end of this step, you should have the Virtual Network running on Azure Government.</span><span class="sxs-lookup"><span data-stu-id="e8329-179">At the end of this step, you should have the Virtual Network running on Azure Government.</span></span>

## <a name="create-a-new-virtual-machine"></a><span data-ttu-id="e8329-180">Create a new Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="e8329-180">Create a new Virtual Machine</span></span>

<span data-ttu-id="e8329-181">In the Azure Government portal, select **Create a resource** in the upper left corner and click on **Compute**.</span><span class="sxs-lookup"><span data-stu-id="e8329-181">In the Azure Government portal, select **Create a resource** in the upper left corner and click on **Compute**.</span></span> 

<span data-ttu-id="e8329-182">Search for "Data science" and then click on "Data Science Virtual Machine - Windows 2016 CSP".</span><span class="sxs-lookup"><span data-stu-id="e8329-182">Search for "Data science" and then click on "Data Science Virtual Machine - Windows 2016 CSP".</span></span> 

![createvn8](./media/create-virtual-machines/documentation-government-quickstarts-vm9.png)

<span data-ttu-id="e8329-184">Scroll to the bottom of the window on the right and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e8329-184">Scroll to the bottom of the window on the right and click **Create**.</span></span> <span data-ttu-id="e8329-185">In the **Basics** dialog, use the following settings and click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="e8329-185">In the **Basics** dialog, use the following settings and click **Ok**.</span></span>

| <span data-ttu-id="e8329-186">Setting</span><span class="sxs-lookup"><span data-stu-id="e8329-186">Setting</span></span> | <span data-ttu-id="e8329-187">Suggested Value</span><span class="sxs-lookup"><span data-stu-id="e8329-187">Suggested Value</span></span> | <span data-ttu-id="e8329-188">Description</span><span class="sxs-lookup"><span data-stu-id="e8329-188">Description</span></span> |
|-|-|-|
|<span data-ttu-id="e8329-189">Name</span><span class="sxs-lookup"><span data-stu-id="e8329-189">Name</span></span>|<span data-ttu-id="e8329-190">vm-test</span><span class="sxs-lookup"><span data-stu-id="e8329-190">vm-test</span></span>|<span data-ttu-id="e8329-191">The name of the VM.</span><span class="sxs-lookup"><span data-stu-id="e8329-191">The name of the VM.</span></span>|
|<span data-ttu-id="e8329-192">VM disk type</span><span class="sxs-lookup"><span data-stu-id="e8329-192">VM disk type</span></span>|<span data-ttu-id="e8329-193">HDD</span><span class="sxs-lookup"><span data-stu-id="e8329-193">HDD</span></span>|<span data-ttu-id="e8329-194">The type of physical hard disk type to use for the VM storage.</span><span class="sxs-lookup"><span data-stu-id="e8329-194">The type of physical hard disk type to use for the VM storage.</span></span> <span data-ttu-id="e8329-195">This would be the same as installing HDD or SSD disks in your server on-premises.</span><span class="sxs-lookup"><span data-stu-id="e8329-195">This would be the same as installing HDD or SSD disks in your server on-premises.</span></span>|
|<span data-ttu-id="e8329-196">User name</span><span class="sxs-lookup"><span data-stu-id="e8329-196">User name</span></span> |<span data-ttu-id="e8329-197">vmtest</span><span class="sxs-lookup"><span data-stu-id="e8329-197">vmtest</span></span>||
|<span data-ttu-id="e8329-198">Password</span><span class="sxs-lookup"><span data-stu-id="e8329-198">Password</span></span>|<span data-ttu-id="e8329-199">A password</span><span class="sxs-lookup"><span data-stu-id="e8329-199">A password</span></span>| <span data-ttu-id="e8329-200">Choose a password that you will remember!</span><span class="sxs-lookup"><span data-stu-id="e8329-200">Choose a password that you will remember!</span></span>|
|<span data-ttu-id="e8329-201">Subscription</span><span class="sxs-lookup"><span data-stu-id="e8329-201">Subscription</span></span>|<span data-ttu-id="e8329-202">Your subscription</span><span class="sxs-lookup"><span data-stu-id="e8329-202">Your subscription</span></span>||
|<span data-ttu-id="e8329-203">Resource group</span><span class="sxs-lookup"><span data-stu-id="e8329-203">Resource group</span></span>|<span data-ttu-id="e8329-204">vnettestgroup</span><span class="sxs-lookup"><span data-stu-id="e8329-204">vnettestgroup</span></span>|<span data-ttu-id="e8329-205">Choose existing resource, same group as you created earlier.</span><span class="sxs-lookup"><span data-stu-id="e8329-205">Choose existing resource, same group as you created earlier.</span></span>|
|<span data-ttu-id="e8329-206">Location</span><span class="sxs-lookup"><span data-stu-id="e8329-206">Location</span></span>|<span data-ttu-id="e8329-207">USGov Virginia</span><span class="sxs-lookup"><span data-stu-id="e8329-207">USGov Virginia</span></span>|<span data-ttu-id="e8329-208">Our virtual network is hosted in Virginia, so this VM has to be in the US Virginia region as well.</span><span class="sxs-lookup"><span data-stu-id="e8329-208">Our virtual network is hosted in Virginia, so this VM has to be in the US Virginia region as well.</span></span>||

<span data-ttu-id="e8329-209">Open the Supported disk type dropdown box and select HDD.</span><span class="sxs-lookup"><span data-stu-id="e8329-209">Open the Supported disk type dropdown box and select HDD.</span></span> <span data-ttu-id="e8329-210">Click **View All** in the options at the top right corner.</span><span class="sxs-lookup"><span data-stu-id="e8329-210">Click **View All** in the options at the top right corner.</span></span> <span data-ttu-id="e8329-211">Scroll down the A4_v2 size and select it.</span><span class="sxs-lookup"><span data-stu-id="e8329-211">Scroll down the A4_v2 size and select it.</span></span> <span data-ttu-id="e8329-212">Click on Select.</span><span class="sxs-lookup"><span data-stu-id="e8329-212">Click on Select.</span></span>

![createvn10](./media/create-virtual-machines/documentation-government-quickstarts-vm11.png)

<span data-ttu-id="e8329-214">On the left hand of settings box click on **Network** and select the **vnettest** virtual network.</span><span class="sxs-lookup"><span data-stu-id="e8329-214">On the left hand of settings box click on **Network** and select the **vnettest** virtual network.</span></span>

<span data-ttu-id="e8329-215">Click on **Subnet** and choose the subnet that you created.</span><span class="sxs-lookup"><span data-stu-id="e8329-215">Click on **Subnet** and choose the subnet that you created.</span></span> 

![createvn12](./media/create-virtual-machines/documentation-government-quickstarts-vm13.png)

<span data-ttu-id="e8329-217">Click on **Public IP address** and then click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="e8329-217">Click on **Public IP address** and then click **Ok**.</span></span>

![createvn13](./media/create-virtual-machines/documentation-government-quickstarts-vm14.png)

<span data-ttu-id="e8329-219">Click **Ok** to create the VM.</span><span class="sxs-lookup"><span data-stu-id="e8329-219">Click **Ok** to create the VM.</span></span>

<span data-ttu-id="e8329-220">The VM will now be provisioned.</span><span class="sxs-lookup"><span data-stu-id="e8329-220">The VM will now be provisioned.</span></span> <span data-ttu-id="e8329-221">It will take several minutes to complete, but afterwards you will be able to connect to the VM with RDP using the public IP address.</span><span class="sxs-lookup"><span data-stu-id="e8329-221">It will take several minutes to complete, but afterwards you will be able to connect to the VM with RDP using the public IP address.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="e8329-222">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="e8329-222">Clean up resources</span></span>

<span data-ttu-id="e8329-223">In the preceding steps, you created Azure resources in a resource group.</span><span class="sxs-lookup"><span data-stu-id="e8329-223">In the preceding steps, you created Azure resources in a resource group.</span></span> <span data-ttu-id="e8329-224">If you don't expect to need these resources in the future, you can delete them by deleting the resource group.</span><span class="sxs-lookup"><span data-stu-id="e8329-224">If you don't expect to need these resources in the future, you can delete them by deleting the resource group.</span></span>

<span data-ttu-id="e8329-225">From the left menu in the Azure Government portal, select Resource groups and then select **vnettestgroup**.</span><span class="sxs-lookup"><span data-stu-id="e8329-225">From the left menu in the Azure Government portal, select Resource groups and then select **vnettestgroup**.</span></span>

<span data-ttu-id="e8329-226">On the resource group page, make sure that the listed resources are the ones you want to delete.</span><span class="sxs-lookup"><span data-stu-id="e8329-226">On the resource group page, make sure that the listed resources are the ones you want to delete.</span></span>

<span data-ttu-id="e8329-227">Select **Delete**, type **vnettestgroup** in the text box, and then select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="e8329-227">Select **Delete**, type **vnettestgroup** in the text box, and then select **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8329-228">Next steps</span><span class="sxs-lookup"><span data-stu-id="e8329-228">Next steps</span></span>

<span data-ttu-id="e8329-229">This tutorial showed you how to create Virtual Machines in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="e8329-229">This tutorial showed you how to create Virtual Machines in Azure Government.</span></span> <span data-ttu-id="e8329-230">To see the latest information and insights on building cloud solution for the Azure Government Cloud, check out Azure Government blog.</span><span class="sxs-lookup"><span data-stu-id="e8329-230">To see the latest information and insights on building cloud solution for the Azure Government Cloud, check out Azure Government blog.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="e8329-231">[Microsoft Azure Government Blog](https://blogs.msdn.microsoft.com/azuregov/).</span><span class="sxs-lookup"><span data-stu-id="e8329-231">[Microsoft Azure Government Blog](https://blogs.msdn.microsoft.com/azuregov/).</span></span>

