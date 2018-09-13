---
title: Scale out worker roles in App Services - Azure Stack  | Microsoft Docs
description: Detailed guidance for scaling Azure Stack App Services
services: azure-stack
documentationcenter: ''
author: kathm
manager: slinehan
editor: anwestg
ms.assetid: 3cbe87bd-8ae2-47dc-a367-51e67ed4b3c0
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: kathm
ms.openlocfilehash: 004ffefa183a752b28d094f7b697346e4af1df9a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551702"
---
# <a name="app-service-on-azure-stack-adding-more-worker-roles"></a><span data-ttu-id="52a44-103">App Service on Azure Stack: Adding more worker roles</span><span class="sxs-lookup"><span data-stu-id="52a44-103">App Service on Azure Stack: Adding more worker roles</span></span> 

<span data-ttu-id="52a44-104">This document provides instructions about how to scale App Service on Azure Stack worker roles.</span><span class="sxs-lookup"><span data-stu-id="52a44-104">This document provides instructions about how to scale App Service on Azure Stack worker roles.</span></span> <span data-ttu-id="52a44-105">It contains steps for creating additional worker roles to support applications of any size.</span><span class="sxs-lookup"><span data-stu-id="52a44-105">It contains steps for creating additional worker roles to support applications of any size.</span></span>

> [!NOTE]
> <span data-ttu-id="52a44-106">If your Azure Stack POC Environment does not have more than 96-GB RAM you may have difficulties adding additional capacity.</span><span class="sxs-lookup"><span data-stu-id="52a44-106">If your Azure Stack POC Environment does not have more than 96-GB RAM you may have difficulties adding additional capacity.</span></span>

<span data-ttu-id="52a44-107">App Service on Azure Stack, by default, supports free and shared worker tiers.</span><span class="sxs-lookup"><span data-stu-id="52a44-107">App Service on Azure Stack, by default, supports free and shared worker tiers.</span></span> <span data-ttu-id="52a44-108">To add other worker tiers, you need to add more worker roles.</span><span class="sxs-lookup"><span data-stu-id="52a44-108">To add other worker tiers, you need to add more worker roles.</span></span>

<span data-ttu-id="52a44-109">If you are not sure what was deployed with the default App Service on Azure Stack installation, you can review additional information in the [App Service on Azure Stack overview](azure-stack-app-service-overview.md).</span><span class="sxs-lookup"><span data-stu-id="52a44-109">If you are not sure what was deployed with the default App Service on Azure Stack installation, you can review additional information in the [App Service on Azure Stack overview](azure-stack-app-service-overview.md).</span></span>

<span data-ttu-id="52a44-110">There are two ways to add additional capacity to App Service on Azure Stack:</span><span class="sxs-lookup"><span data-stu-id="52a44-110">There are two ways to add additional capacity to App Service on Azure Stack:</span></span>
1.  <span data-ttu-id="52a44-111">[Add additional workers directly from with within the App Service Resource Provider Admin](#Add-additional-workers-directly-from-within-the-App-Service-Resource-Provider-Admin).</span><span class="sxs-lookup"><span data-stu-id="52a44-111">[Add additional workers directly from with within the App Service Resource Provider Admin](#Add-additional-workers-directly-from-within-the-App-Service-Resource-Provider-Admin).</span></span>
2.  <span data-ttu-id="52a44-112">[Create additional VMs manually and add them to the App Service Resource Provider](#Create-additional-VMs-manually-and-add-them-to-the-App-Service-Resource-Provider).</span><span class="sxs-lookup"><span data-stu-id="52a44-112">[Create additional VMs manually and add them to the App Service Resource Provider](#Create-additional-VMs-manually-and-add-them-to-the-App-Service-Resource-Provider).</span></span>

## <a name="add-additional-workers-directly-within-the-app-service-resource-provider-admin"></a><span data-ttu-id="52a44-113">Add additional workers directly within the App Service Resource Provider Admin.</span><span class="sxs-lookup"><span data-stu-id="52a44-113">Add additional workers directly within the App Service Resource Provider Admin.</span></span>

1.  <span data-ttu-id="52a44-114">Log in to the Azure Stack portal as the service administrator;</span><span class="sxs-lookup"><span data-stu-id="52a44-114">Log in to the Azure Stack portal as the service administrator;</span></span>
2.  <span data-ttu-id="52a44-115">Browse to **Resource Providers** and select the **App Service Resource Provider Admin**. ![Azure Stack Resource Providers][1]</span><span class="sxs-lookup"><span data-stu-id="52a44-115">Browse to **Resource Providers** and select the **App Service Resource Provider Admin**. ![Azure Stack Resource Providers][1]</span></span>
3.  <span data-ttu-id="52a44-116">Click **Roles**.</span><span class="sxs-lookup"><span data-stu-id="52a44-116">Click **Roles**.</span></span>  <span data-ttu-id="52a44-117">Here you see the breakdown of all App Service roles deployed.</span><span class="sxs-lookup"><span data-stu-id="52a44-117">Here you see the breakdown of all App Service roles deployed.</span></span>
4.  <span data-ttu-id="52a44-118">Click the option **New Role Instance** ![Add new role instance][2]</span><span class="sxs-lookup"><span data-stu-id="52a44-118">Click the option **New Role Instance** ![Add new role instance][2]</span></span>
5.  <span data-ttu-id="52a44-119">In the **New Role Instance** blade:</span><span class="sxs-lookup"><span data-stu-id="52a44-119">In the **New Role Instance** blade:</span></span>
    1. <span data-ttu-id="52a44-120">Choose how many additional **role instances** you would like to add.</span><span class="sxs-lookup"><span data-stu-id="52a44-120">Choose how many additional **role instances** you would like to add.</span></span>  <span data-ttu-id="52a44-121">In the preview, there is a maximum of 10.</span><span class="sxs-lookup"><span data-stu-id="52a44-121">In the preview, there is a maximum of 10.</span></span>
    2. <span data-ttu-id="52a44-122">Select the **role type**.</span><span class="sxs-lookup"><span data-stu-id="52a44-122">Select the **role type**.</span></span>  <span data-ttu-id="52a44-123">In this preview, this option is limited to Web Worker.</span><span class="sxs-lookup"><span data-stu-id="52a44-123">In this preview, this option is limited to Web Worker.</span></span>
    3. <span data-ttu-id="52a44-124">Select the **worker tier** you would like to deploy this worker into, default choices are Small, Medium, Large, or Shared.</span><span class="sxs-lookup"><span data-stu-id="52a44-124">Select the **worker tier** you would like to deploy this worker into, default choices are Small, Medium, Large, or Shared.</span></span>  <span data-ttu-id="52a44-125">If, you have created your own worker tiers, your worker tiers will also be available for selection.</span><span class="sxs-lookup"><span data-stu-id="52a44-125">If, you have created your own worker tiers, your worker tiers will also be available for selection.</span></span>
    4. <span data-ttu-id="52a44-126">Click **OK** to deploy the additional workers</span><span class="sxs-lookup"><span data-stu-id="52a44-126">Click **OK** to deploy the additional workers</span></span>
6.  <span data-ttu-id="52a44-127">App Service on Azure Stack will now add the additional VMs, configure them, install all the required software and mark them as ready when this process is complete.</span><span class="sxs-lookup"><span data-stu-id="52a44-127">App Service on Azure Stack will now add the additional VMs, configure them, install all the required software and mark them as ready when this process is complete.</span></span>  <span data-ttu-id="52a44-128">This process can take approximately 80 minutes.</span><span class="sxs-lookup"><span data-stu-id="52a44-128">This process can take approximately 80 minutes.</span></span>
7.  <span data-ttu-id="52a44-129">You can monitor the progress of the readiness of the new workers by viewing the workers in the **roles** blade.</span><span class="sxs-lookup"><span data-stu-id="52a44-129">You can monitor the progress of the readiness of the new workers by viewing the workers in the **roles** blade.</span></span>

>[!NOTE]
>  <span data-ttu-id="52a44-130">In this preview, the integrated New Role Instance flow is limited to Worker Roles and deploy VMs of size A1 only.</span><span class="sxs-lookup"><span data-stu-id="52a44-130">In this preview, the integrated New Role Instance flow is limited to Worker Roles and deploy VMs of size A1 only.</span></span>  <span data-ttu-id="52a44-131">We will be expanding this capability in a future release.</span><span class="sxs-lookup"><span data-stu-id="52a44-131">We will be expanding this capability in a future release.</span></span>

## <a name="manually-adding-additional-capacity-to-app-service-on-azure-stack"></a><span data-ttu-id="52a44-132">Manually adding additional capacity to App Service on Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="52a44-132">Manually adding additional capacity to App Service on Azure Stack.</span></span>

<span data-ttu-id="52a44-133">The following steps are required to add additional roles:</span><span class="sxs-lookup"><span data-stu-id="52a44-133">The following steps are required to add additional roles:</span></span>

1. [<span data-ttu-id="52a44-134">Create a new virtual machine</span><span class="sxs-lookup"><span data-stu-id="52a44-134">Create a new virtual machine</span></span>](#step-1-create-a-new-vm-to-support-the-new-instance-size)
2. [<span data-ttu-id="52a44-135">Configure the virtual machine</span><span class="sxs-lookup"><span data-stu-id="52a44-135">Configure the virtual machine</span></span>](#step-2-configure-the-virtual-machine)
3. [<span data-ttu-id="52a44-136">Configure the web worker role in the Azure Stack portal</span><span class="sxs-lookup"><span data-stu-id="52a44-136">Configure the web worker role in the Azure Stack portal</span></span>](#step-3-configure-the-web-worker-role-in-the-azure-stack-portal)
4. [<span data-ttu-id="52a44-137">Configure app service plans</span><span class="sxs-lookup"><span data-stu-id="52a44-137">Configure app service plans</span></span>](#step-4-configure-app-service-plans)

## <a name="step-1-create-a-new-vm-to-support-the-new-instance-size"></a><span data-ttu-id="52a44-138">Step 1: Create a new VM to support the new instance size</span><span class="sxs-lookup"><span data-stu-id="52a44-138">Step 1: Create a new VM to support the new instance size</span></span>
<span data-ttu-id="52a44-139">Create a virtual machine as described in [this article](azure-stack-provision-vm.md), ensuring that the following selections are made:</span><span class="sxs-lookup"><span data-stu-id="52a44-139">Create a virtual machine as described in [this article](azure-stack-provision-vm.md), ensuring that the following selections are made:</span></span>

* <span data-ttu-id="52a44-140">User name and password: Provide the same user name and password you provided when you installed App Service on Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="52a44-140">User name and password: Provide the same user name and password you provided when you installed App Service on Azure Stack.</span></span>
* <span data-ttu-id="52a44-141">Subscription: Use the default provider subscription.</span><span class="sxs-lookup"><span data-stu-id="52a44-141">Subscription: Use the default provider subscription.</span></span>
* <span data-ttu-id="52a44-142">Resource group: Choose **AppService-LOCAL**.</span><span class="sxs-lookup"><span data-stu-id="52a44-142">Resource group: Choose **AppService-LOCAL**.</span></span>

> [!NOTE]
> <span data-ttu-id="52a44-143">Store the virtual machines for worker roles in the same resource group as App Service on Azure Stack is deployed to.</span><span class="sxs-lookup"><span data-stu-id="52a44-143">Store the virtual machines for worker roles in the same resource group as App Service on Azure Stack is deployed to.</span></span> <span data-ttu-id="52a44-144">(This is recommended for this release.)</span><span class="sxs-lookup"><span data-stu-id="52a44-144">(This is recommended for this release.)</span></span>
> 
> 

## <a name="step-2-configure-the-virtual-machine"></a><span data-ttu-id="52a44-145">Step 2: Configure the Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="52a44-145">Step 2: Configure the Virtual Machine</span></span>
<span data-ttu-id="52a44-146">Once the deployment has completed, the following configuration is required to support the web worker role:</span><span class="sxs-lookup"><span data-stu-id="52a44-146">Once the deployment has completed, the following configuration is required to support the web worker role:</span></span>

1. <span data-ttu-id="52a44-147">Browse to the **AppService-LOCAL** resource group in the portal and select the new machine you created in Step 1.</span><span class="sxs-lookup"><span data-stu-id="52a44-147">Browse to the **AppService-LOCAL** resource group in the portal and select the new machine you created in Step 1.</span></span>
2. <span data-ttu-id="52a44-148">Click connect in the VM blade to download the remote desktop profile.</span><span class="sxs-lookup"><span data-stu-id="52a44-148">Click connect in the VM blade to download the remote desktop profile.</span></span>  <span data-ttu-id="52a44-149">Open the profile to open a remote desktop session to your VM.</span><span class="sxs-lookup"><span data-stu-id="52a44-149">Open the profile to open a remote desktop session to your VM.</span></span>
3. <span data-ttu-id="52a44-150">Log in to the VM using the username and password you specified in Step 1.</span><span class="sxs-lookup"><span data-stu-id="52a44-150">Log in to the VM using the username and password you specified in Step 1.</span></span>
4. <span data-ttu-id="52a44-151">Open PowerShell by clicking the **Start** button and typing PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52a44-151">Open PowerShell by clicking the **Start** button and typing PowerShell.</span></span> <span data-ttu-id="52a44-152">Right-click **PowerShell.exe**, and select **Run as administrator** to open PowerShell in administrator mode.</span><span class="sxs-lookup"><span data-stu-id="52a44-152">Right-click **PowerShell.exe**, and select **Run as administrator** to open PowerShell in administrator mode.</span></span>
5. <span data-ttu-id="52a44-153">Copy and paste each of the following commands (one at a time) into the PowerShell window, and press enter:</span><span class="sxs-lookup"><span data-stu-id="52a44-153">Copy and paste each of the following commands (one at a time) into the PowerShell window, and press enter:</span></span>
   
   ```netsh advfirewall firewall set rule group="File and Printer Sharing" new enable=Yes```
   ```netsh advfirewall firewall set rule group="Windows Management Instrumentation (WMI)" new enable=yes```
   ```reg add HKLM\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Policies\\system /v LocalAccountTokenFilterPolicy /t REG\_DWORD /d 1 /f```
   
6. <span data-ttu-id="52a44-154">Close your remote desktop session.</span><span class="sxs-lookup"><span data-stu-id="52a44-154">Close your remote desktop session.</span></span>
7. <span data-ttu-id="52a44-155">Restart the VM from the portal.</span><span class="sxs-lookup"><span data-stu-id="52a44-155">Restart the VM from the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="52a44-156">These are minimum requirements for App Service on Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="52a44-156">These are minimum requirements for App Service on Azure Stack.</span></span> <span data-ttu-id="52a44-157">They are the default settings of the Windows 2012 R2 image included with Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="52a44-157">They are the default settings of the Windows 2012 R2 image included with Azure Stack.</span></span> <span data-ttu-id="52a44-158">The instructions have been provided for future reference, and for those using a different image.</span><span class="sxs-lookup"><span data-stu-id="52a44-158">The instructions have been provided for future reference, and for those using a different image.</span></span>
> 
> 

## <a name="step-3-configure-the-worker-role-in-the-azure-stack-portal"></a><span data-ttu-id="52a44-159">Step 3: Configure the worker role in the Azure Stack portal</span><span class="sxs-lookup"><span data-stu-id="52a44-159">Step 3: Configure the worker role in the Azure Stack portal</span></span>
1. <span data-ttu-id="52a44-160">Open the portal as the service administrator on **ClientVM**.</span><span class="sxs-lookup"><span data-stu-id="52a44-160">Open the portal as the service administrator on **ClientVM**.</span></span>
2. <span data-ttu-id="52a44-161">Navigate to **Resource Providers** &gt; **App Service Resource Provider Admin**.![App Service Resource Provider Admin][3]</span><span class="sxs-lookup"><span data-stu-id="52a44-161">Navigate to **Resource Providers** &gt; **App Service Resource Provider Admin**.![App Service Resource Provider Admin][3]</span></span>
3. <span data-ttu-id="52a44-162">In the settings blade, click **Roles**.![App Service Resource Provider Roles][4]</span><span class="sxs-lookup"><span data-stu-id="52a44-162">In the settings blade, click **Roles**.![App Service Resource Provider Roles][4]</span></span>
4. <span data-ttu-id="52a44-163">Click **Add Role Instance**.</span><span class="sxs-lookup"><span data-stu-id="52a44-163">Click **Add Role Instance**.</span></span>
5. <span data-ttu-id="52a44-164">In the textbox for **Server Name** enter the **IP Address** of the server you created earlier (in Section 1).</span><span class="sxs-lookup"><span data-stu-id="52a44-164">In the textbox for **Server Name** enter the **IP Address** of the server you created earlier (in Section 1).</span></span>
6. <span data-ttu-id="52a44-165">Select the **Role Type** you would like to add - Controller, Management Server, Front End, Web Worker, Publisher, or File Server.</span><span class="sxs-lookup"><span data-stu-id="52a44-165">Select the **Role Type** you would like to add - Controller, Management Server, Front End, Web Worker, Publisher, or File Server.</span></span>  <span data-ttu-id="52a44-166">In this instance, select Web Worker.</span><span class="sxs-lookup"><span data-stu-id="52a44-166">In this instance, select Web Worker.</span></span>
7. <span data-ttu-id="52a44-167">Click the **Tier** you would like to deploy the new instance to (small, medium, large, or shared).</span><span class="sxs-lookup"><span data-stu-id="52a44-167">Click the **Tier** you would like to deploy the new instance to (small, medium, large, or shared).</span></span>  <span data-ttu-id="52a44-168">If you have created your own worker tiers these will also be available for selection.</span><span class="sxs-lookup"><span data-stu-id="52a44-168">If you have created your own worker tiers these will also be available for selection.</span></span>
8. <span data-ttu-id="52a44-169">Click **OK.**</span><span class="sxs-lookup"><span data-stu-id="52a44-169">Click **OK.**</span></span>
9. <span data-ttu-id="52a44-170">Go back to the **Roles** view</span><span class="sxs-lookup"><span data-stu-id="52a44-170">Go back to the **Roles** view</span></span>
10. <span data-ttu-id="52a44-171">Click the row corresponding to the Role Type and Worker Tier combination you assigned your VM to.</span><span class="sxs-lookup"><span data-stu-id="52a44-171">Click the row corresponding to the Role Type and Worker Tier combination you assigned your VM to.</span></span>
11. <span data-ttu-id="52a44-172">Look for the Server Name you just added.</span><span class="sxs-lookup"><span data-stu-id="52a44-172">Look for the Server Name you just added.</span></span> <span data-ttu-id="52a44-173">Review the status column, and wait to move to the next step until the status is "Ready."</span><span class="sxs-lookup"><span data-stu-id="52a44-173">Review the status column, and wait to move to the next step until the status is "Ready."</span></span> <span data-ttu-id="52a44-174">This can take approximately 80 minutes.</span><span class="sxs-lookup"><span data-stu-id="52a44-174">This can take approximately 80 minutes.</span></span> <span data-ttu-id="52a44-175">![App Service Resource Provider Role Ready][5]</span><span class="sxs-lookup"><span data-stu-id="52a44-175">![App Service Resource Provider Role Ready][5]</span></span>

## <a name="step-4-configure-app-service-plans"></a><span data-ttu-id="52a44-176">Step 4: Configure app service plans</span><span class="sxs-lookup"><span data-stu-id="52a44-176">Step 4: Configure app service plans</span></span>

1. <span data-ttu-id="52a44-177">Sign in to the portal on the ClientVM.</span><span class="sxs-lookup"><span data-stu-id="52a44-177">Sign in to the portal on the ClientVM.</span></span>
2. <span data-ttu-id="52a44-178">Navigate to **New** &gt; **Web and Mobile**.</span><span class="sxs-lookup"><span data-stu-id="52a44-178">Navigate to **New** &gt; **Web and Mobile**.</span></span>
3. <span data-ttu-id="52a44-179">Select the type of application you would like to deploy.</span><span class="sxs-lookup"><span data-stu-id="52a44-179">Select the type of application you would like to deploy.</span></span>
4. <span data-ttu-id="52a44-180">Provide the information for the application, and then select **AppService Plan / Location**.</span><span class="sxs-lookup"><span data-stu-id="52a44-180">Provide the information for the application, and then select **AppService Plan / Location**.</span></span>
    1. <span data-ttu-id="52a44-181">Click **Create New**.</span><span class="sxs-lookup"><span data-stu-id="52a44-181">Click **Create New**.</span></span>
    2. <span data-ttu-id="52a44-182">Create your plan, selecting the corresponding pricing tier for the plan.</span><span class="sxs-lookup"><span data-stu-id="52a44-182">Create your plan, selecting the corresponding pricing tier for the plan.</span></span>

> [!NOTE]
> <span data-ttu-id="52a44-183">You can create multiple plans while on this blade.</span><span class="sxs-lookup"><span data-stu-id="52a44-183">You can create multiple plans while on this blade.</span></span> <span data-ttu-id="52a44-184">Before you deploy, however, ensure you have selected the appropriate plan.</span><span class="sxs-lookup"><span data-stu-id="52a44-184">Before you deploy, however, ensure you have selected the appropriate plan.</span></span>
> 
> 

<span data-ttu-id="52a44-185">The following shows an example of the multiple pricing tiers available by default.</span><span class="sxs-lookup"><span data-stu-id="52a44-185">The following shows an example of the multiple pricing tiers available by default.</span></span>  <span data-ttu-id="52a44-186">You notice that if there are no available workers for a particular worker tier, the option to choose the corresponding pricing tier is unavailable.</span><span class="sxs-lookup"><span data-stu-id="52a44-186">You notice that if there are no available workers for a particular worker tier, the option to choose the corresponding pricing tier is unavailable.</span></span>![App Service on Azure Stack Default Pricing Tiers][6]

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-add-worker-roles/azure-stack-resource-providers.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-add-worker-roles/app-service-new-role-instance.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-admin.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-roles.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-role-ready.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-pricing-tier.png






