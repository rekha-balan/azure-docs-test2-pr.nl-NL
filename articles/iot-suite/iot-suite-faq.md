---
title: Azure IoT Suite FAQ | Microsoft Docs
description: Frequently asked questions for IoT Suite
services: ''
suite: iot-suite
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: cb537749-a8a1-4e53-b3bf-f1b64a38188a
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/15/2017
ms.author: corywink
ms.openlocfilehash: 8fa08ca6cefc10c1e1b47a7a498f69aca7de882e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551663"
---
# <a name="frequently-asked-questions-for-iot-suite"></a><span data-ttu-id="0138c-103">Frequently asked questions for IoT Suite</span><span class="sxs-lookup"><span data-stu-id="0138c-103">Frequently asked questions for IoT Suite</span></span>

### <a name="where-can-i-find-the-source-code-for-the-preconfigured-solutions"></a><span data-ttu-id="0138c-104">Where can I find the source code for the preconfigured solutions?</span><span class="sxs-lookup"><span data-stu-id="0138c-104">Where can I find the source code for the preconfigured solutions?</span></span>
<span data-ttu-id="0138c-105">The source code is stored in the following GitHub repositories:</span><span class="sxs-lookup"><span data-stu-id="0138c-105">The source code is stored in the following GitHub repositories:</span></span>
* <span data-ttu-id="0138c-106">[Remote Monitoring preconfigured solution][lnk-remote-monitoring-github]</span><span class="sxs-lookup"><span data-stu-id="0138c-106">[Remote Monitoring preconfigured solution][lnk-remote-monitoring-github]</span></span>
* <span data-ttu-id="0138c-107">[Predictive maintenance preconfigured solution][lnk-predictive-maintenance-github]</span><span class="sxs-lookup"><span data-stu-id="0138c-107">[Predictive maintenance preconfigured solution][lnk-predictive-maintenance-github]</span></span>

### <a name="how-do-i-update-to-the-latest-version-of-the-remote-monitoring-preconfigured-solution-that-uses-the-iot-hub-device-management-features"></a><span data-ttu-id="0138c-108">How do I update to the latest version of the remote monitoring preconfigured solution that uses the IoT Hub device management features?</span><span class="sxs-lookup"><span data-stu-id="0138c-108">How do I update to the latest version of the remote monitoring preconfigured solution that uses the IoT Hub device management features?</span></span>
* <span data-ttu-id="0138c-109">If you deploy a preconfigured solution from the https://www.azureiotsuite.com/ site, it always deploys a new instance of the latest version of the solution.</span><span class="sxs-lookup"><span data-stu-id="0138c-109">If you deploy a preconfigured solution from the https://www.azureiotsuite.com/ site, it always deploys a new instance of the latest version of the solution.</span></span>
* <span data-ttu-id="0138c-110">If you deploy a preconfigured solution using the command line, you can update an existing deployment with new code.</span><span class="sxs-lookup"><span data-stu-id="0138c-110">If you deploy a preconfigured solution using the command line, you can update an existing deployment with new code.</span></span> <span data-ttu-id="0138c-111">See [Cloud deployment][lnk-cloud-deployment] in the GitHub [repository][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="0138c-111">See [Cloud deployment][lnk-cloud-deployment] in the GitHub [repository][lnk-remote-monitoring-github].</span></span>

### <a name="how-can-i-add-support-for-a-new-device-method-to-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="0138c-112">How can I add support for a new device method to the remote monitoring preconfigured solution?</span><span class="sxs-lookup"><span data-stu-id="0138c-112">How can I add support for a new device method to the remote monitoring preconfigured solution?</span></span>
<span data-ttu-id="0138c-113">See the section [Add support for a new method to the simulator][lnk-add-method] in the [Customize a preconfigured solution][lnk-customize] article.</span><span class="sxs-lookup"><span data-stu-id="0138c-113">See the section [Add support for a new method to the simulator][lnk-add-method] in the [Customize a preconfigured solution][lnk-customize] article.</span></span>

### <a name="the-simulated-device-is-ignoring-my-desired-property-changes-why"></a><span data-ttu-id="0138c-114">The simulated device is ignoring my desired property changes, why?</span><span class="sxs-lookup"><span data-stu-id="0138c-114">The simulated device is ignoring my desired property changes, why?</span></span>
<span data-ttu-id="0138c-115">In the remote monitoring preconfigured solution, the simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties.</span><span class="sxs-lookup"><span data-stu-id="0138c-115">In the remote monitoring preconfigured solution, the simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties.</span></span> <span data-ttu-id="0138c-116">All other desired property change requests are ignored.</span><span class="sxs-lookup"><span data-stu-id="0138c-116">All other desired property change requests are ignored.</span></span>

### <a name="my-device-does-not-appear-in-the-list-of-devices-in-the-solution-dashboard-why"></a><span data-ttu-id="0138c-117">My device does not appear in the list of devices in the solution dashboard, why?</span><span class="sxs-lookup"><span data-stu-id="0138c-117">My device does not appear in the list of devices in the solution dashboard, why?</span></span>
<span data-ttu-id="0138c-118">The list of devices in the solution dashboard uses a query to return the list of devices.</span><span class="sxs-lookup"><span data-stu-id="0138c-118">The list of devices in the solution dashboard uses a query to return the list of devices.</span></span> <span data-ttu-id="0138c-119">Currently, a query cannot return more than 10K devices.</span><span class="sxs-lookup"><span data-stu-id="0138c-119">Currently, a query cannot return more than 10K devices.</span></span> <span data-ttu-id="0138c-120">Try making the search criteria for your query more restrictive.</span><span class="sxs-lookup"><span data-stu-id="0138c-120">Try making the search criteria for your query more restrictive.</span></span>

### <a name="whats-the-difference-between-deleting-a-resource-group-in-the-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a><span data-ttu-id="0138c-121">What's the difference between deleting a resource group in the Azure portal and clicking delete on a preconfigured solution in azureiotsuite.com?</span><span class="sxs-lookup"><span data-stu-id="0138c-121">What's the difference between deleting a resource group in the Azure portal and clicking delete on a preconfigured solution in azureiotsuite.com?</span></span>
* <span data-ttu-id="0138c-122">If you delete the preconfigured solution in [azureiotsuite.com][lnk-azureiotsuite], you delete all the resources that were provisioned when you created the preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="0138c-122">If you delete the preconfigured solution in [azureiotsuite.com][lnk-azureiotsuite], you delete all the resources that were provisioned when you created the preconfigured solution.</span></span> <span data-ttu-id="0138c-123">If you added additional resources to the resource group, these resources are also deleted.</span><span class="sxs-lookup"><span data-stu-id="0138c-123">If you added additional resources to the resource group, these resources are also deleted.</span></span> 
* <span data-ttu-id="0138c-124">If you delete the resource group in the [Azure portal][lnk-azure-portal], you only delete the resources in that resource group.</span><span class="sxs-lookup"><span data-stu-id="0138c-124">If you delete the resource group in the [Azure portal][lnk-azure-portal], you only delete the resources in that resource group.</span></span> <span data-ttu-id="0138c-125">You also need to delete the Azure Active Directory application associated with the preconfigured solution in the [Azure classic portal][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="0138c-125">You also need to delete the Azure Active Directory application associated with the preconfigured solution in the [Azure classic portal][lnk-classic-portal].</span></span>

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="0138c-126">How many IoT Hub instances can I provision in a subscription?</span><span class="sxs-lookup"><span data-stu-id="0138c-126">How many IoT Hub instances can I provision in a subscription?</span></span>
<span data-ttu-id="0138c-127">By default you can provision [10 IoT hubs per subscription][link-azuresublimits].</span><span class="sxs-lookup"><span data-stu-id="0138c-127">By default you can provision [10 IoT hubs per subscription][link-azuresublimits].</span></span> <span data-ttu-id="0138c-128">You can create an [Azure support ticket][link-azuresupportticket] to raise this limit.</span><span class="sxs-lookup"><span data-stu-id="0138c-128">You can create an [Azure support ticket][link-azuresupportticket] to raise this limit.</span></span> <span data-ttu-id="0138c-129">As a result, since every preconfigured solution provisions a new IoT Hub, you can only provision up to 10 preconfigured solutions in a given subscription.</span><span class="sxs-lookup"><span data-stu-id="0138c-129">As a result, since every preconfigured solution provisions a new IoT Hub, you can only provision up to 10 preconfigured solutions in a given subscription.</span></span> 

### <a name="how-many-documentdb-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="0138c-130">How many DocumentDB instances can I provision in a subscription?</span><span class="sxs-lookup"><span data-stu-id="0138c-130">How many DocumentDB instances can I provision in a subscription?</span></span>
<span data-ttu-id="0138c-131">Fifty.</span><span class="sxs-lookup"><span data-stu-id="0138c-131">Fifty.</span></span> <span data-ttu-id="0138c-132">You can create an [Azure support ticket][link-azuresupportticket] to raise this limit, but by default, you can only provision 50 DocumentDB instances per subscription.</span><span class="sxs-lookup"><span data-stu-id="0138c-132">You can create an [Azure support ticket][link-azuresupportticket] to raise this limit, but by default, you can only provision 50 DocumentDB instances per subscription.</span></span> 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a><span data-ttu-id="0138c-133">How many Free Bing Maps APIs can I provision in a subscription?</span><span class="sxs-lookup"><span data-stu-id="0138c-133">How many Free Bing Maps APIs can I provision in a subscription?</span></span>
<span data-ttu-id="0138c-134">Two.</span><span class="sxs-lookup"><span data-stu-id="0138c-134">Two.</span></span> <span data-ttu-id="0138c-135">You can create only two Internal Transactions Level 1 Bing Maps for Enterprise plans in an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0138c-135">You can create only two Internal Transactions Level 1 Bing Maps for Enterprise plans in an Azure subscription.</span></span> <span data-ttu-id="0138c-136">The remote monitoring solution is provisioned by default with the Internal Transactions Level 1 plan.</span><span class="sxs-lookup"><span data-stu-id="0138c-136">The remote monitoring solution is provisioned by default with the Internal Transactions Level 1 plan.</span></span> <span data-ttu-id="0138c-137">As a result, you can only provision up to two remote monitoring solutions in a subscription with no modifications.</span><span class="sxs-lookup"><span data-stu-id="0138c-137">As a result, you can only provision up to two remote monitoring solutions in a subscription with no modifications.</span></span>

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a><span data-ttu-id="0138c-138">I have a remote monitoring solution deployment with a static map, how do I add an interactive Bing map?</span><span class="sxs-lookup"><span data-stu-id="0138c-138">I have a remote monitoring solution deployment with a static map, how do I add an interactive Bing map?</span></span>
1. <span data-ttu-id="0138c-139">Get your Bing Maps API for Enterprise QueryKey from [Azure portal][lnk-azure-portal]:</span><span class="sxs-lookup"><span data-stu-id="0138c-139">Get your Bing Maps API for Enterprise QueryKey from [Azure portal][lnk-azure-portal]:</span></span> 
   
   1. <span data-ttu-id="0138c-140">Navigate to the Resource Group where your Bing Maps API for Enterprise is in the [Azure portal][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="0138c-140">Navigate to the Resource Group where your Bing Maps API for Enterprise is in the [Azure portal][lnk-azure-portal].</span></span>
   2. <span data-ttu-id="0138c-141">Click **All Settings**, then **Key Management**.</span><span class="sxs-lookup"><span data-stu-id="0138c-141">Click **All Settings**, then **Key Management**.</span></span> 
   3. <span data-ttu-id="0138c-142">You can see two keys: **MasterKey** and **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="0138c-142">You can see two keys: **MasterKey** and **QueryKey**.</span></span> <span data-ttu-id="0138c-143">Copy the value for **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="0138c-143">Copy the value for **QueryKey**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="0138c-144">Don't have a Bing Maps API for Enterprise account?</span><span class="sxs-lookup"><span data-stu-id="0138c-144">Don't have a Bing Maps API for Enterprise account?</span></span> <span data-ttu-id="0138c-145">Create one in the [Azure portal][lnk-azure-portal] by clicking + New, searching for Bing Maps API for Enterprise and follow prompts to create.</span><span class="sxs-lookup"><span data-stu-id="0138c-145">Create one in the [Azure portal][lnk-azure-portal] by clicking + New, searching for Bing Maps API for Enterprise and follow prompts to create.</span></span>
      > 
      > 
2. <span data-ttu-id="0138c-146">Pull down the latest code from the [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="0138c-146">Pull down the latest code from the [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span></span>
3. <span data-ttu-id="0138c-147">Run a local or cloud deployment following the command-line deployment guidance in the /docs/ folder in the repository.</span><span class="sxs-lookup"><span data-stu-id="0138c-147">Run a local or cloud deployment following the command-line deployment guidance in the /docs/ folder in the repository.</span></span> 
4. <span data-ttu-id="0138c-148">After you've run a local or cloud deployment, look in your root folder for the \*.user.config file created during deployment.</span><span class="sxs-lookup"><span data-stu-id="0138c-148">After you've run a local or cloud deployment, look in your root folder for the \*.user.config file created during deployment.</span></span> <span data-ttu-id="0138c-149">Open this file in a text editor.</span><span class="sxs-lookup"><span data-stu-id="0138c-149">Open this file in a text editor.</span></span> 
5. <span data-ttu-id="0138c-150">Change the following line to include the value you copied from your **QueryKey**:</span><span class="sxs-lookup"><span data-stu-id="0138c-150">Change the following line to include the value you copied from your **QueryKey**:</span></span> 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a><span data-ttu-id="0138c-151">Can I create a preconfigured solution if I have Microsoft Azure for DreamSpark?</span><span class="sxs-lookup"><span data-stu-id="0138c-151">Can I create a preconfigured solution if I have Microsoft Azure for DreamSpark?</span></span>
<span data-ttu-id="0138c-152">Currently, you cannot create a preconfigured solution with a [Microsoft Azure for DreamSpark][lnk-dreamspark] account.</span><span class="sxs-lookup"><span data-stu-id="0138c-152">Currently, you cannot create a preconfigured solution with a [Microsoft Azure for DreamSpark][lnk-dreamspark] account.</span></span> <span data-ttu-id="0138c-153">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="0138c-153">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a><span data-ttu-id="0138c-154">Can I create a preconfigured solution if I have Cloud Solution Provider (CSP) subscription?</span><span class="sxs-lookup"><span data-stu-id="0138c-154">Can I create a preconfigured solution if I have Cloud Solution Provider (CSP) subscription?</span></span>
<span data-ttu-id="0138c-155">Currently, you cannot create a preconfigured solution with a Cloud Solution Provider (CSP) subscription.</span><span class="sxs-lookup"><span data-stu-id="0138c-155">Currently, you cannot create a preconfigured solution with a Cloud Solution Provider (CSP) subscription.</span></span> <span data-ttu-id="0138c-156">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="0138c-156">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="how-do-i-delete-an-aad-tenant"></a><span data-ttu-id="0138c-157">How do I delete an AAD tenant?</span><span class="sxs-lookup"><span data-stu-id="0138c-157">How do I delete an AAD tenant?</span></span>
<span data-ttu-id="0138c-158">See Eric Golpe's blog post [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant].</span><span class="sxs-lookup"><span data-stu-id="0138c-158">See Eric Golpe's blog post [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant].</span></span>

### <a name="next-steps"></a><span data-ttu-id="0138c-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="0138c-159">Next steps</span></span>
<span data-ttu-id="0138c-160">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span><span class="sxs-lookup"><span data-stu-id="0138c-160">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="0138c-161">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="0138c-161">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* <span data-ttu-id="0138c-162">[IoT security from the ground up][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="0138c-162">[IoT security from the ground up][lnk-security-groundup]</span></span>

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-security-groundup]: securing-iot-ground-up.md

[link-azuresupportticket]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade 
[link-azuresublimits]: https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/#iot-hub-limits
[lnk-azure-portal]: https://portal.azure.com
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring 
[lnk-dreamspark]: https://www.dreamspark.com/Product/Product.aspx?productid=99 
[lnk-30daytrial]: https://azure.microsoft.com/free/
[lnk-delete-aad-tennant]: http://blogs.msdn.com/b/ericgolpe/archive/2015/04/30/walkthrough-of-deleting-an-azure-ad-tenant.aspx
[lnk-cloud-deployment]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
[lnk-add-method]: iot-suite-guidance-on-customizing-preconfigured-solutions.md#add-support-for-a-new-method-to-the-simulator
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-predictive-maintenance-github]: https://github.com/Azure/azure-iot-predictive-maintenance