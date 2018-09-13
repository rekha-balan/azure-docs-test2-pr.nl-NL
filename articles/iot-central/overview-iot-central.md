---
title: What is Azure IoT Central | Microsoft Docs
description: Azure IoT Central is a end-to-end SaaS solution you can use to build and manage your custom IoT solution. This article provides an overview of the features of Azure IoT Central.
author: dominicbetts
ms.author: dobett
ms.date: 11/30/2017
ms.topic: overview
ms.service: iot-central
services: iot-central
ms.custom: mvc
manager: timlt
ms.openlocfilehash: 8c369ab05059e57f2e2a98339052c27292ac7c0d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870219"
---
<!---
Purpose of an Overview article: 
1. To give a TECHNICAL overview of a service/product: What is it? Why should I use it? It's a "learn" topic that describes key benefits and our competitive advantage. It's not a "do" topic.
2. To help audiences who are new to service but who may be familiar with related concepts. 
3. To compare the service to another service/product that has some similar functionality, ex. SQL Database / SQL Data Warehouse, if appropriate. This info can be in a short list or table. 
-->

# <a name="what-is-azure-iot-central"></a><span data-ttu-id="e1213-104">What is Azure IoT Central?</span><span class="sxs-lookup"><span data-stu-id="e1213-104">What is Azure IoT Central?</span></span>

<span data-ttu-id="e1213-105">Microsoft Azure IoT Central is a fully managed IoT Software-as-a-Service solution that makes it easy to create products that connect the physical and digital worlds.</span><span class="sxs-lookup"><span data-stu-id="e1213-105">Microsoft Azure IoT Central is a fully managed IoT Software-as-a-Service solution that makes it easy to create products that connect the physical and digital worlds.</span></span> <span data-ttu-id="e1213-106">You can bring your connected product vision to life by:</span><span class="sxs-lookup"><span data-stu-id="e1213-106">You can bring your connected product vision to life by:</span></span>

- <span data-ttu-id="e1213-107">Deriving new insights from connected devices to enable better products and experiences for your customers.</span><span class="sxs-lookup"><span data-stu-id="e1213-107">Deriving new insights from connected devices to enable better products and experiences for your customers.</span></span>
- <span data-ttu-id="e1213-108">Creating new business opportunities for your organization.</span><span class="sxs-lookup"><span data-stu-id="e1213-108">Creating new business opportunities for your organization.</span></span>

<span data-ttu-id="e1213-109">Azure IoT Central, as compared to a typical IoT project, takes the hassle out of managing an IoT solution by:</span><span class="sxs-lookup"><span data-stu-id="e1213-109">Azure IoT Central, as compared to a typical IoT project, takes the hassle out of managing an IoT solution by:</span></span>

- <span data-ttu-id="e1213-110">Reducing the management burden.</span><span class="sxs-lookup"><span data-stu-id="e1213-110">Reducing the management burden.</span></span>
- <span data-ttu-id="e1213-111">Reducing operational costs and overheads.</span><span class="sxs-lookup"><span data-stu-id="e1213-111">Reducing operational costs and overheads.</span></span>
- <span data-ttu-id="e1213-112">Making it easy to customize your application, while leveraging:</span><span class="sxs-lookup"><span data-stu-id="e1213-112">Making it easy to customize your application, while leveraging:</span></span>
  - <span data-ttu-id="e1213-113">Industry-leading technologies such as [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) and [Azure Time Series Insights](https://azure.microsoft.com/services/time-series-insights/).</span><span class="sxs-lookup"><span data-stu-id="e1213-113">Industry-leading technologies such as [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) and [Azure Time Series Insights](https://azure.microsoft.com/services/time-series-insights/).</span></span>
  - <span data-ttu-id="e1213-114">Enterprise-grade security features such as end-to-end encryption.</span><span class="sxs-lookup"><span data-stu-id="e1213-114">Enterprise-grade security features such as end-to-end encryption.</span></span>

<span data-ttu-id="e1213-115">The following video presents an overview of Azure IoT Central:</span><span class="sxs-lookup"><span data-stu-id="e1213-115">The following video presents an overview of Azure IoT Central:</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Internet-of-Things-Show/Microsoft-IoT-Central-intro-walkthrough/Player]

<span data-ttu-id="e1213-116">The remainder of this article outlines for Azure IoT Central:</span><span class="sxs-lookup"><span data-stu-id="e1213-116">The remainder of this article outlines for Azure IoT Central:</span></span>

- <span data-ttu-id="e1213-117">The typical personas associated with a project.</span><span class="sxs-lookup"><span data-stu-id="e1213-117">The typical personas associated with a project.</span></span>
- <span data-ttu-id="e1213-118">How to create your application.</span><span class="sxs-lookup"><span data-stu-id="e1213-118">How to create your application.</span></span>
- <span data-ttu-id="e1213-119">How to connect your devices to your application</span><span class="sxs-lookup"><span data-stu-id="e1213-119">How to connect your devices to your application</span></span>
- <span data-ttu-id="e1213-120">How to manage your application.</span><span class="sxs-lookup"><span data-stu-id="e1213-120">How to manage your application.</span></span>

## <a name="personas"></a><span data-ttu-id="e1213-121">Personas</span><span class="sxs-lookup"><span data-stu-id="e1213-121">Personas</span></span>

<span data-ttu-id="e1213-122">The Azure IoT Central documentation refers to four typical personas who interact with an Azure IoT Central application:</span><span class="sxs-lookup"><span data-stu-id="e1213-122">The Azure IoT Central documentation refers to four typical personas who interact with an Azure IoT Central application:</span></span>

- <span data-ttu-id="e1213-123">A _builder_ is responsible for defining the types of devices that connect to the application and customizing the application for the operator.</span><span class="sxs-lookup"><span data-stu-id="e1213-123">A _builder_ is responsible for defining the types of devices that connect to the application and customizing the application for the operator.</span></span>
- <span data-ttu-id="e1213-124">An _operator_ manages the devices connected to the application.</span><span class="sxs-lookup"><span data-stu-id="e1213-124">An _operator_ manages the devices connected to the application.</span></span>
- <span data-ttu-id="e1213-125">An _administrator_ is responsible for administrative tasks such as managing users and roles within the application.</span><span class="sxs-lookup"><span data-stu-id="e1213-125">An _administrator_ is responsible for administrative tasks such as managing users and roles within the application.</span></span>
- <span data-ttu-id="e1213-126">A _device developer_ creates the code that runs on a device connected to your application.</span><span class="sxs-lookup"><span data-stu-id="e1213-126">A _device developer_ creates the code that runs on a device connected to your application.</span></span>

## <a name="create-your-azure-iot-central-application"></a><span data-ttu-id="e1213-127">Create your Azure IoT Central application</span><span class="sxs-lookup"><span data-stu-id="e1213-127">Create your Azure IoT Central application</span></span>

<span data-ttu-id="e1213-128">As a builder, you use Azure IoT Central to create a custom, cloud-hosted IoT solution for your organization.</span><span class="sxs-lookup"><span data-stu-id="e1213-128">As a builder, you use Azure IoT Central to create a custom, cloud-hosted IoT solution for your organization.</span></span> <span data-ttu-id="e1213-129">A custom IoT solution typically consists of:</span><span class="sxs-lookup"><span data-stu-id="e1213-129">A custom IoT solution typically consists of:</span></span>

- <span data-ttu-id="e1213-130">A cloud-based application that receives telemetry from your devices and enables you to manage those devices.</span><span class="sxs-lookup"><span data-stu-id="e1213-130">A cloud-based application that receives telemetry from your devices and enables you to manage those devices.</span></span>
- <span data-ttu-id="e1213-131">Multiple devices running custom code connected to your cloud-based application.</span><span class="sxs-lookup"><span data-stu-id="e1213-131">Multiple devices running custom code connected to your cloud-based application.</span></span>

<span data-ttu-id="e1213-132">You can quickly deploy a new Azure IoT Central application and then customize it to your specific requirements right in your browser.</span><span class="sxs-lookup"><span data-stu-id="e1213-132">You can quickly deploy a new Azure IoT Central application and then customize it to your specific requirements right in your browser.</span></span> <span data-ttu-id="e1213-133">As an Azure IoT Central builder, you can use the web-based tools to create a _device template_ for the devices that connect to your application.</span><span class="sxs-lookup"><span data-stu-id="e1213-133">As an Azure IoT Central builder, you can use the web-based tools to create a _device template_ for the devices that connect to your application.</span></span> <span data-ttu-id="e1213-134">A device template is the blueprint of a device model that all devices created from the device template share.</span><span class="sxs-lookup"><span data-stu-id="e1213-134">A device template is the blueprint of a device model that all devices created from the device template share.</span></span> <span data-ttu-id="e1213-135">A device template defines the characteristics and behavior of a type of device such as:</span><span class="sxs-lookup"><span data-stu-id="e1213-135">A device template defines the characteristics and behavior of a type of device such as:</span></span>

- <span data-ttu-id="e1213-136">The telemetry it sends.</span><span class="sxs-lookup"><span data-stu-id="e1213-136">The telemetry it sends.</span></span>
- <span data-ttu-id="e1213-137">Business properties that an operator can modify.</span><span class="sxs-lookup"><span data-stu-id="e1213-137">Business properties that an operator can modify.</span></span>
- <span data-ttu-id="e1213-138">Device properties that are set by a device and that are read-only in the application.</span><span class="sxs-lookup"><span data-stu-id="e1213-138">Device properties that are set by a device and that are read-only in the application.</span></span>
- <span data-ttu-id="e1213-139">The thresholds the application responds to.</span><span class="sxs-lookup"><span data-stu-id="e1213-139">The thresholds the application responds to.</span></span>
- <span data-ttu-id="e1213-140">Settings that determine the behavior of the device.</span><span class="sxs-lookup"><span data-stu-id="e1213-140">Settings that determine the behavior of the device.</span></span>

<span data-ttu-id="e1213-141">You can immediately test your device templates and application with simulated data that Azure IoT Central generates for you.</span><span class="sxs-lookup"><span data-stu-id="e1213-141">You can immediately test your device templates and application with simulated data that Azure IoT Central generates for you.</span></span>

<span data-ttu-id="e1213-142">As a builder, you can also customize the Azure IoT Central application UI for the operators who are responsible for the day-to-day use of the application.</span><span class="sxs-lookup"><span data-stu-id="e1213-142">As a builder, you can also customize the Azure IoT Central application UI for the operators who are responsible for the day-to-day use of the application.</span></span> <span data-ttu-id="e1213-143">Customizations that a builder can make include:</span><span class="sxs-lookup"><span data-stu-id="e1213-143">Customizations that a builder can make include:</span></span>

- <span data-ttu-id="e1213-144">Defining the layout of properties and settings on a device template.</span><span class="sxs-lookup"><span data-stu-id="e1213-144">Defining the layout of properties and settings on a device template.</span></span>
- <span data-ttu-id="e1213-145">Configuring custom dashboards to help operators discover insights and resolve issues faster.</span><span class="sxs-lookup"><span data-stu-id="e1213-145">Configuring custom dashboards to help operators discover insights and resolve issues faster.</span></span>
- <span data-ttu-id="e1213-146">Configuring custom analytics to explore time series data from your connected devices.</span><span class="sxs-lookup"><span data-stu-id="e1213-146">Configuring custom analytics to explore time series data from your connected devices.</span></span>

## <a name="connect-your-devices"></a><span data-ttu-id="e1213-147">Connect your devices</span><span class="sxs-lookup"><span data-stu-id="e1213-147">Connect your devices</span></span>

<span data-ttu-id="e1213-148">After the builder defines the types of devices that can connect to the application, a device developer creates the code to run on the devices.</span><span class="sxs-lookup"><span data-stu-id="e1213-148">After the builder defines the types of devices that can connect to the application, a device developer creates the code to run on the devices.</span></span> <span data-ttu-id="e1213-149">As a device developer, you use Microsoft's open-source [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) to create your device code.</span><span class="sxs-lookup"><span data-stu-id="e1213-149">As a device developer, you use Microsoft's open-source [Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks) to create your device code.</span></span> <span data-ttu-id="e1213-150">These SDKs have broad language, platform, and protocol support to meet your needs to connect your devices to your Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="e1213-150">These SDKs have broad language, platform, and protocol support to meet your needs to connect your devices to your Azure IoT Central application.</span></span> <span data-ttu-id="e1213-151">The SDKs help you to perform the following tasks on the device  connected to Azure IoT Central:</span><span class="sxs-lookup"><span data-stu-id="e1213-151">The SDKs help you to perform the following tasks on the device  connected to Azure IoT Central:</span></span>

- <span data-ttu-id="e1213-152">Create a secure connection.</span><span class="sxs-lookup"><span data-stu-id="e1213-152">Create a secure connection.</span></span>
- <span data-ttu-id="e1213-153">Send telemetry.</span><span class="sxs-lookup"><span data-stu-id="e1213-153">Send telemetry.</span></span>
- <span data-ttu-id="e1213-154">Report status.</span><span class="sxs-lookup"><span data-stu-id="e1213-154">Report status.</span></span>
- <span data-ttu-id="e1213-155">Receive configuration updates.</span><span class="sxs-lookup"><span data-stu-id="e1213-155">Receive configuration updates.</span></span>

<span data-ttu-id="e1213-156">For more information, see the blog post [Benefits of using the Azure IoT SDKs, and pitfalls to avoid if you don't](https://azure.microsoft.com/blog/benefits-of-using-the-azure-iot-sdks-in-your-azure-iot-solution/).</span><span class="sxs-lookup"><span data-stu-id="e1213-156">For more information, see the blog post [Benefits of using the Azure IoT SDKs, and pitfalls to avoid if you don't](https://azure.microsoft.com/blog/benefits-of-using-the-azure-iot-sdks-in-your-azure-iot-solution/).</span></span>

## <a name="manage-your-application"></a><span data-ttu-id="e1213-157">Manage your application</span><span class="sxs-lookup"><span data-stu-id="e1213-157">Manage your application</span></span>

<span data-ttu-id="e1213-158">Azure IoT Central applications are fully hosted by Microsoft, which reduces the administration overhead of managing your applications.</span><span class="sxs-lookup"><span data-stu-id="e1213-158">Azure IoT Central applications are fully hosted by Microsoft, which reduces the administration overhead of managing your applications.</span></span>

<span data-ttu-id="e1213-159">As an operator, you use the Azure IoT Central application to manage the devices in your Azure IoT Central solution.</span><span class="sxs-lookup"><span data-stu-id="e1213-159">As an operator, you use the Azure IoT Central application to manage the devices in your Azure IoT Central solution.</span></span> <span data-ttu-id="e1213-160">Operators can perform tasks such as:</span><span class="sxs-lookup"><span data-stu-id="e1213-160">Operators can perform tasks such as:</span></span>

- <span data-ttu-id="e1213-161">Monitoring the devices connected to the application.</span><span class="sxs-lookup"><span data-stu-id="e1213-161">Monitoring the devices connected to the application.</span></span>
- <span data-ttu-id="e1213-162">Troubleshooting and remediating issues with devices.</span><span class="sxs-lookup"><span data-stu-id="e1213-162">Troubleshooting and remediating issues with devices.</span></span>
- <span data-ttu-id="e1213-163">Provisioning new devices.</span><span class="sxs-lookup"><span data-stu-id="e1213-163">Provisioning new devices.</span></span>

<span data-ttu-id="e1213-164">A builder can define custom rules and actions that operate over streaming data at the device template level.</span><span class="sxs-lookup"><span data-stu-id="e1213-164">A builder can define custom rules and actions that operate over streaming data at the device template level.</span></span> <span data-ttu-id="e1213-165">An operator can enable or disable these rules at the device level to control and automate tasks within the application.</span><span class="sxs-lookup"><span data-stu-id="e1213-165">An operator can enable or disable these rules at the device level to control and automate tasks within the application.</span></span>

<span data-ttu-id="e1213-166">Administrators can manage access to your application with [user roles and permissions](howto-administer.md).</span><span class="sxs-lookup"><span data-stu-id="e1213-166">Administrators can manage access to your application with [user roles and permissions](howto-administer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1213-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="e1213-167">Next steps</span></span>

<span data-ttu-id="e1213-168">Now that you have an overview of Azure IoT Central, here are suggested next steps:</span><span class="sxs-lookup"><span data-stu-id="e1213-168">Now that you have an overview of Azure IoT Central, here are suggested next steps:</span></span>

- <span data-ttu-id="e1213-169">Understand the differences between [Azure IoT Central and Azure IoT solution accelerators](overview-iot-options.md).</span><span class="sxs-lookup"><span data-stu-id="e1213-169">Understand the differences between [Azure IoT Central and Azure IoT solution accelerators](overview-iot-options.md).</span></span>
- <span data-ttu-id="e1213-170">Familiarize yourself with the [Azure IoT Central UI](overview-iot-central-tour.md).</span><span class="sxs-lookup"><span data-stu-id="e1213-170">Familiarize yourself with the [Azure IoT Central UI](overview-iot-central-tour.md).</span></span>
- <span data-ttu-id="e1213-171">Get started by [creating an Azure IoT Central application](quick-deploy-iot-central.md).</span><span class="sxs-lookup"><span data-stu-id="e1213-171">Get started by [creating an Azure IoT Central application](quick-deploy-iot-central.md).</span></span>
- <span data-ttu-id="e1213-172">Follow a sequence of tutorials that show you how to:</span><span class="sxs-lookup"><span data-stu-id="e1213-172">Follow a sequence of tutorials that show you how to:</span></span>
  - [<span data-ttu-id="e1213-173">As a builder, to create a device template</span><span class="sxs-lookup"><span data-stu-id="e1213-173">As a builder, to create a device template</span></span>](tutorial-define-device-type.md)
  - [<span data-ttu-id="e1213-174">As a builder, add rules to automate your solution</span><span class="sxs-lookup"><span data-stu-id="e1213-174">As a builder, add rules to automate your solution</span></span>](tutorial-configure-rules.md)
  - [<span data-ttu-id="e1213-175">As a builder, customize the application for your operators</span><span class="sxs-lookup"><span data-stu-id="e1213-175">As a builder, customize the application for your operators</span></span>](tutorial-customize-operator.md)
  - [<span data-ttu-id="e1213-176">As an operator, monitor your devices</span><span class="sxs-lookup"><span data-stu-id="e1213-176">As an operator, monitor your devices</span></span>](tutorial-monitor-devices.md)
  - [<span data-ttu-id="e1213-177">As an operator, add a real device to your solution</span><span class="sxs-lookup"><span data-stu-id="e1213-177">As an operator, add a real device to your solution</span></span>](tutorial-add-device.md)
  - [<span data-ttu-id="e1213-178">As a device developer, create code for your devices</span><span class="sxs-lookup"><span data-stu-id="e1213-178">As a device developer, create code for your devices</span></span>](tutorial-add-device.md#prepare-the-client-code)
