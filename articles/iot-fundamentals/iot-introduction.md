---
title: Azure Internet of Things (IoT) Introduction
description: Overview Azure IoT and related services and technologies.
author: BryanLa
manager: timlt
ms.service: iot-fundamentals
services: iot-fundamentals
ms.topic: overview
ms.date: 05/18/2018
ms.author: bryanla
ms.openlocfilehash: ed96181606e2db4102aa609973ade9ecbfde6c90
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856138"
---
# <a name="introduction-to-azure-and-the-internet-of-things"></a><span data-ttu-id="d00cd-103">Introduction to Azure and the Internet of Things</span><span class="sxs-lookup"><span data-stu-id="d00cd-103">Introduction to Azure and the Internet of Things</span></span>

<span data-ttu-id="d00cd-104">Azure IoT consists of three areas of technologies and solutions—solutions, platform services, and edge, all designed to facilitate the end-to-end development of your IoT application.</span><span class="sxs-lookup"><span data-stu-id="d00cd-104">Azure IoT consists of three areas of technologies and solutions—solutions, platform services, and edge, all designed to facilitate the end-to-end development of your IoT application.</span></span> <span data-ttu-id="d00cd-105">This article begins by describing the common characteristics of an IoT solution in the cloud, followed by an overview of how Azure IoT addresses challenges in IoT projects and why you should consider adopting Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="d00cd-105">This article begins by describing the common characteristics of an IoT solution in the cloud, followed by an overview of how Azure IoT addresses challenges in IoT projects and why you should consider adopting Azure IoT.</span></span>

## <a name="iot-solution-architecture"></a><span data-ttu-id="d00cd-106">IoT solution architecture</span><span class="sxs-lookup"><span data-stu-id="d00cd-106">IoT solution architecture</span></span>

<span data-ttu-id="d00cd-107">IoT solutions require secure, bidirectional communication between devices, possibly numbering in the millions, and a solution back end.</span><span class="sxs-lookup"><span data-stu-id="d00cd-107">IoT solutions require secure, bidirectional communication between devices, possibly numbering in the millions, and a solution back end.</span></span> <span data-ttu-id="d00cd-108">For example, a solution might use automated, predictive analytics to uncover insights from your device-to-cloud event stream.</span><span class="sxs-lookup"><span data-stu-id="d00cd-108">For example, a solution might use automated, predictive analytics to uncover insights from your device-to-cloud event stream.</span></span> 

<span data-ttu-id="d00cd-109">The following diagram shows the key elements of a typical IoT solution architecture.</span><span class="sxs-lookup"><span data-stu-id="d00cd-109">The following diagram shows the key elements of a typical IoT solution architecture.</span></span> <span data-ttu-id="d00cd-110">The diagram is agnostic of the specific implementation details such as the Azure services used, and device operating systems.</span><span class="sxs-lookup"><span data-stu-id="d00cd-110">The diagram is agnostic of the specific implementation details such as the Azure services used, and device operating systems.</span></span> <span data-ttu-id="d00cd-111">In this architecture, IoT devices collect data that they send to a cloud gateway.</span><span class="sxs-lookup"><span data-stu-id="d00cd-111">In this architecture, IoT devices collect data that they send to a cloud gateway.</span></span> <span data-ttu-id="d00cd-112">The cloud gateway makes the data available for processing by other back-end services.</span><span class="sxs-lookup"><span data-stu-id="d00cd-112">The cloud gateway makes the data available for processing by other back-end services.</span></span> <span data-ttu-id="d00cd-113">These back-end services can deliver data to:</span><span class="sxs-lookup"><span data-stu-id="d00cd-113">These back-end services can deliver data to:</span></span>

* <span data-ttu-id="d00cd-114">Other line-of-business applications.</span><span class="sxs-lookup"><span data-stu-id="d00cd-114">Other line-of-business applications.</span></span>
* <span data-ttu-id="d00cd-115">Human operators through a dashboard or other presentation device.</span><span class="sxs-lookup"><span data-stu-id="d00cd-115">Human operators through a dashboard or other presentation device.</span></span>

![IoT solution architecture][img-solution-architecture]

> [!NOTE]
> <span data-ttu-id="d00cd-117">For an in-depth discussion of IoT architecture, see the [Microsoft Azure IoT Reference Architecture][lnk-refarch].</span><span class="sxs-lookup"><span data-stu-id="d00cd-117">For an in-depth discussion of IoT architecture, see the [Microsoft Azure IoT Reference Architecture][lnk-refarch].</span></span>

### <a name="device-connectivity"></a><span data-ttu-id="d00cd-118">Device connectivity</span><span class="sxs-lookup"><span data-stu-id="d00cd-118">Device connectivity</span></span>

<span data-ttu-id="d00cd-119">In an IoT solution architecture, devices typically send telemetry to the cloud for storage and processing.</span><span class="sxs-lookup"><span data-stu-id="d00cd-119">In an IoT solution architecture, devices typically send telemetry to the cloud for storage and processing.</span></span> <span data-ttu-id="d00cd-120">For example, in a predictive maintenance scenario, the solution back end might use the stream of sensor data to determine when a specific pump requires maintenance.</span><span class="sxs-lookup"><span data-stu-id="d00cd-120">For example, in a predictive maintenance scenario, the solution back end might use the stream of sensor data to determine when a specific pump requires maintenance.</span></span> <span data-ttu-id="d00cd-121">Devices can also receive and respond to cloud-to-device messages by reading messages from a cloud endpoint.</span><span class="sxs-lookup"><span data-stu-id="d00cd-121">Devices can also receive and respond to cloud-to-device messages by reading messages from a cloud endpoint.</span></span> <span data-ttu-id="d00cd-122">In the same example, the solution back end might send messages to other pumps in the pumping station to begin rerouting flows just before maintenance is due to start.</span><span class="sxs-lookup"><span data-stu-id="d00cd-122">In the same example, the solution back end might send messages to other pumps in the pumping station to begin rerouting flows just before maintenance is due to start.</span></span> <span data-ttu-id="d00cd-123">This procedure makes sure the maintenance engineer could get started as soon as she arrives.</span><span class="sxs-lookup"><span data-stu-id="d00cd-123">This procedure makes sure the maintenance engineer could get started as soon as she arrives.</span></span>

<span data-ttu-id="d00cd-124">Connecting devices securely and reliably is often the biggest challenge in IoT solutions.</span><span class="sxs-lookup"><span data-stu-id="d00cd-124">Connecting devices securely and reliably is often the biggest challenge in IoT solutions.</span></span> <span data-ttu-id="d00cd-125">This is because IoT devices have different characteristics as compared to other clients such as browsers and mobile apps.</span><span class="sxs-lookup"><span data-stu-id="d00cd-125">This is because IoT devices have different characteristics as compared to other clients such as browsers and mobile apps.</span></span> <span data-ttu-id="d00cd-126">Specifically, IoT devices:</span><span class="sxs-lookup"><span data-stu-id="d00cd-126">Specifically, IoT devices:</span></span>

* <span data-ttu-id="d00cd-127">Are often embedded systems with no human operator (unlike a phone).</span><span class="sxs-lookup"><span data-stu-id="d00cd-127">Are often embedded systems with no human operator (unlike a phone).</span></span>
* <span data-ttu-id="d00cd-128">Can be deployed in remote locations, where physical access is expensive.</span><span class="sxs-lookup"><span data-stu-id="d00cd-128">Can be deployed in remote locations, where physical access is expensive.</span></span>
* <span data-ttu-id="d00cd-129">May only be reachable through the solution back end.</span><span class="sxs-lookup"><span data-stu-id="d00cd-129">May only be reachable through the solution back end.</span></span> <span data-ttu-id="d00cd-130">There is no other way to interact with the device.</span><span class="sxs-lookup"><span data-stu-id="d00cd-130">There is no other way to interact with the device.</span></span>
* <span data-ttu-id="d00cd-131">May have limited power and processing resources.</span><span class="sxs-lookup"><span data-stu-id="d00cd-131">May have limited power and processing resources.</span></span>
* <span data-ttu-id="d00cd-132">May have intermittent, slow, or expensive network connectivity.</span><span class="sxs-lookup"><span data-stu-id="d00cd-132">May have intermittent, slow, or expensive network connectivity.</span></span>
* <span data-ttu-id="d00cd-133">May need to use proprietary, custom, or industry-specific application protocols.</span><span class="sxs-lookup"><span data-stu-id="d00cd-133">May need to use proprietary, custom, or industry-specific application protocols.</span></span>
* <span data-ttu-id="d00cd-134">Can be created using a large set of popular hardware and software platforms.</span><span class="sxs-lookup"><span data-stu-id="d00cd-134">Can be created using a large set of popular hardware and software platforms.</span></span>

<span data-ttu-id="d00cd-135">In addition to the previous constraints, any IoT solution must also be scalable, secure, and reliable.</span><span class="sxs-lookup"><span data-stu-id="d00cd-135">In addition to the previous constraints, any IoT solution must also be scalable, secure, and reliable.</span></span>

<span data-ttu-id="d00cd-136">Depending on the communication protocol and network availability, a device can either communicate directly, or through an intermediate gateway, with the cloud.</span><span class="sxs-lookup"><span data-stu-id="d00cd-136">Depending on the communication protocol and network availability, a device can either communicate directly, or through an intermediate gateway, with the cloud.</span></span> <span data-ttu-id="d00cd-137">IoT architectures often have a mix of these two communication patterns.</span><span class="sxs-lookup"><span data-stu-id="d00cd-137">IoT architectures often have a mix of these two communication patterns.</span></span>

### <a name="data-processing-and-analytics"></a><span data-ttu-id="d00cd-138">Data processing and analytics</span><span class="sxs-lookup"><span data-stu-id="d00cd-138">Data processing and analytics</span></span>

<span data-ttu-id="d00cd-139">In modern IoT solutions, data processing can occur in the cloud or on the device side.</span><span class="sxs-lookup"><span data-stu-id="d00cd-139">In modern IoT solutions, data processing can occur in the cloud or on the device side.</span></span> <span data-ttu-id="d00cd-140">Device-side processing is referred as *Edge computing*.</span><span class="sxs-lookup"><span data-stu-id="d00cd-140">Device-side processing is referred as *Edge computing*.</span></span> <span data-ttu-id="d00cd-141">The choice of where to process data depends on factors such as:</span><span class="sxs-lookup"><span data-stu-id="d00cd-141">The choice of where to process data depends on factors such as:</span></span>

* <span data-ttu-id="d00cd-142">Network constraints.</span><span class="sxs-lookup"><span data-stu-id="d00cd-142">Network constraints.</span></span> <span data-ttu-id="d00cd-143">If bandwidth between the devices and the cloud is limited, there is an incentive to do more edge processing.</span><span class="sxs-lookup"><span data-stu-id="d00cd-143">If bandwidth between the devices and the cloud is limited, there is an incentive to do more edge processing.</span></span>
* <span data-ttu-id="d00cd-144">Response time.</span><span class="sxs-lookup"><span data-stu-id="d00cd-144">Response time.</span></span> <span data-ttu-id="d00cd-145">If there is a requirement to act on a device in near real time, it may be better to process the response in the device itself.</span><span class="sxs-lookup"><span data-stu-id="d00cd-145">If there is a requirement to act on a device in near real time, it may be better to process the response in the device itself.</span></span> <span data-ttu-id="d00cd-146">For example, a robot arm that needs to be stopped in an emergency.</span><span class="sxs-lookup"><span data-stu-id="d00cd-146">For example, a robot arm that needs to be stopped in an emergency.</span></span>
* <span data-ttu-id="d00cd-147">Regulatory environment.</span><span class="sxs-lookup"><span data-stu-id="d00cd-147">Regulatory environment.</span></span> <span data-ttu-id="d00cd-148">Some data cannot be sent to the cloud.</span><span class="sxs-lookup"><span data-stu-id="d00cd-148">Some data cannot be sent to the cloud.</span></span>

<span data-ttu-id="d00cd-149">In general, data processing both in the edge and in the cloud are a combination of the following capabilities:</span><span class="sxs-lookup"><span data-stu-id="d00cd-149">In general, data processing both in the edge and in the cloud are a combination of the following capabilities:</span></span>

* <span data-ttu-id="d00cd-150">Receiving telemetry at scale from your devices and determining how to process and store that data.</span><span class="sxs-lookup"><span data-stu-id="d00cd-150">Receiving telemetry at scale from your devices and determining how to process and store that data.</span></span>
* <span data-ttu-id="d00cd-151">Analyzing the telemetry to provide insights, whether they are in real time or after the fact.</span><span class="sxs-lookup"><span data-stu-id="d00cd-151">Analyzing the telemetry to provide insights, whether they are in real time or after the fact.</span></span>
* <span data-ttu-id="d00cd-152">Sending commands from the cloud or a gateway device to a specific device.</span><span class="sxs-lookup"><span data-stu-id="d00cd-152">Sending commands from the cloud or a gateway device to a specific device.</span></span>

<span data-ttu-id="d00cd-153">Additionally, an IoT cloud back end should provide:</span><span class="sxs-lookup"><span data-stu-id="d00cd-153">Additionally, an IoT cloud back end should provide:</span></span>

* <span data-ttu-id="d00cd-154">Device registration capabilities that enable you to:</span><span class="sxs-lookup"><span data-stu-id="d00cd-154">Device registration capabilities that enable you to:</span></span>
    * <span data-ttu-id="d00cd-155">Provision devices.</span><span class="sxs-lookup"><span data-stu-id="d00cd-155">Provision devices.</span></span>
    * <span data-ttu-id="d00cd-156">Control which devices are permitted to connect to your infrastructure.</span><span class="sxs-lookup"><span data-stu-id="d00cd-156">Control which devices are permitted to connect to your infrastructure.</span></span>
* <span data-ttu-id="d00cd-157">Device management to control the state of your devices and monitor their activities.</span><span class="sxs-lookup"><span data-stu-id="d00cd-157">Device management to control the state of your devices and monitor their activities.</span></span>

<span data-ttu-id="d00cd-158">For example, in a predictive maintenance scenario, the cloud back-end stores historical telemetry data.</span><span class="sxs-lookup"><span data-stu-id="d00cd-158">For example, in a predictive maintenance scenario, the cloud back-end stores historical telemetry data.</span></span> <span data-ttu-id="d00cd-159">The solution uses this data to identify potential anomalous behavior on specific pumps before they cause a real problem.</span><span class="sxs-lookup"><span data-stu-id="d00cd-159">The solution uses this data to identify potential anomalous behavior on specific pumps before they cause a real problem.</span></span> <span data-ttu-id="d00cd-160">Using data analytics, it can identify that the preventative solution is to send a command back to the device to take a corrective action.</span><span class="sxs-lookup"><span data-stu-id="d00cd-160">Using data analytics, it can identify that the preventative solution is to send a command back to the device to take a corrective action.</span></span> <span data-ttu-id="d00cd-161">This process generates an automated feedback loop between the device and the cloud that greatly increases the solution efficiency.</span><span class="sxs-lookup"><span data-stu-id="d00cd-161">This process generates an automated feedback loop between the device and the cloud that greatly increases the solution efficiency.</span></span>

### <a name="presentation-and-business-connectivity"></a><span data-ttu-id="d00cd-162">Presentation and business connectivity</span><span class="sxs-lookup"><span data-stu-id="d00cd-162">Presentation and business connectivity</span></span>

<span data-ttu-id="d00cd-163">The presentation and business connectivity layer allows end users to interact with the IoT solution and the devices.</span><span class="sxs-lookup"><span data-stu-id="d00cd-163">The presentation and business connectivity layer allows end users to interact with the IoT solution and the devices.</span></span> <span data-ttu-id="d00cd-164">It enables users to view and analyze the data collected from their devices.</span><span class="sxs-lookup"><span data-stu-id="d00cd-164">It enables users to view and analyze the data collected from their devices.</span></span> <span data-ttu-id="d00cd-165">These views can take the form of dashboards or BI reports that can display both historical data or near real-time data.</span><span class="sxs-lookup"><span data-stu-id="d00cd-165">These views can take the form of dashboards or BI reports that can display both historical data or near real-time data.</span></span> <span data-ttu-id="d00cd-166">For example, an operator can check on the status of particular pumping station and see any alerts raised by the system.</span><span class="sxs-lookup"><span data-stu-id="d00cd-166">For example, an operator can check on the status of particular pumping station and see any alerts raised by the system.</span></span> <span data-ttu-id="d00cd-167">This layer also allows integration of the IoT solution back-end with existing line-of-business applications to tie into enterprise business processes or workflows.</span><span class="sxs-lookup"><span data-stu-id="d00cd-167">This layer also allows integration of the IoT solution back-end with existing line-of-business applications to tie into enterprise business processes or workflows.</span></span> <span data-ttu-id="d00cd-168">For example, a predictive maintenance solution can integrate with a scheduling system to book an engineer to visit a pumping station when it identifies a pump in need of maintenance.</span><span class="sxs-lookup"><span data-stu-id="d00cd-168">For example, a predictive maintenance solution can integrate with a scheduling system to book an engineer to visit a pumping station when it identifies a pump in need of maintenance.</span></span>

## <a name="why-azure-iot"></a><span data-ttu-id="d00cd-169">Why Azure IoT?</span><span class="sxs-lookup"><span data-stu-id="d00cd-169">Why Azure IoT?</span></span>

<span data-ttu-id="d00cd-170">Azure IoT simplifies the complexity of IoT projects and addresses the challenges such as security, infrastructure incompatibility, and scaling your IoT solution.</span><span class="sxs-lookup"><span data-stu-id="d00cd-170">Azure IoT simplifies the complexity of IoT projects and addresses the challenges such as security, infrastructure incompatibility, and scaling your IoT solution.</span></span> <span data-ttu-id="d00cd-171">Here is how:</span><span class="sxs-lookup"><span data-stu-id="d00cd-171">Here is how:</span></span>

<span data-ttu-id="d00cd-172">**Agile**</span><span class="sxs-lookup"><span data-stu-id="d00cd-172">**Agile**</span></span> <br>
<span data-ttu-id="d00cd-173">Accelerate your IoT journey</span><span class="sxs-lookup"><span data-stu-id="d00cd-173">Accelerate your IoT journey</span></span>
* <span data-ttu-id="d00cd-174">Scale: start small, grow to any size, anywhere and everywhere — millions of devices, terabytes of data, in the most regions worldwide.</span><span class="sxs-lookup"><span data-stu-id="d00cd-174">Scale: start small, grow to any size, anywhere and everywhere — millions of devices, terabytes of data, in the most regions worldwide.</span></span>

* <span data-ttu-id="d00cd-175">Open: use what you have, or modernize for the future by connecting to any device, software, or service.</span><span class="sxs-lookup"><span data-stu-id="d00cd-175">Open: use what you have, or modernize for the future by connecting to any device, software, or service.</span></span>

* <span data-ttu-id="d00cd-176">Hybrid: build according to your needs by deploying your IoT solution at the edge, in the cloud, or anywhere in between.</span><span class="sxs-lookup"><span data-stu-id="d00cd-176">Hybrid: build according to your needs by deploying your IoT solution at the edge, in the cloud, or anywhere in between.</span></span>

* <span data-ttu-id="d00cd-177">Pace: deploy faster, speed time-to-market, and stay ahead of your competition with the leader in solution accelerators and pace of innovation in IoT.</span><span class="sxs-lookup"><span data-stu-id="d00cd-177">Pace: deploy faster, speed time-to-market, and stay ahead of your competition with the leader in solution accelerators and pace of innovation in IoT.</span></span>

<span data-ttu-id="d00cd-178">**Comprehensive**</span><span class="sxs-lookup"><span data-stu-id="d00cd-178">**Comprehensive**</span></span> <br>
<span data-ttu-id="d00cd-179">Deliver impact for your business</span><span class="sxs-lookup"><span data-stu-id="d00cd-179">Deliver impact for your business</span></span>

* <span data-ttu-id="d00cd-180">Complete: Microsoft is the only IoT solution provider with a complete platform spanning device to cloud, across big data, advanced analytics, and with managed services.</span><span class="sxs-lookup"><span data-stu-id="d00cd-180">Complete: Microsoft is the only IoT solution provider with a complete platform spanning device to cloud, across big data, advanced analytics, and with managed services.</span></span>

* <span data-ttu-id="d00cd-181">Partner for success: tap into the power of the world’s  largest partner ecosystem, and bring line-of-business and technology to life, across industry and around the world.</span><span class="sxs-lookup"><span data-stu-id="d00cd-181">Partner for success: tap into the power of the world’s  largest partner ecosystem, and bring line-of-business and technology to life, across industry and around the world.</span></span>

* <span data-ttu-id="d00cd-182">Data-driven: IoT is about data, and the best IoT solutions bring together all of the tools you need to store, interpret, transform, analyze, and present data to right user, in the right place, at the right time.</span><span class="sxs-lookup"><span data-stu-id="d00cd-182">Data-driven: IoT is about data, and the best IoT solutions bring together all of the tools you need to store, interpret, transform, analyze, and present data to right user, in the right place, at the right time.</span></span>

* <span data-ttu-id="d00cd-183">Device-centric: Microsoft IoT allows you to connect anything, from legacy equipment to a vast ecosystem of certified hardware, and the ability to build your own devices across edge, mobile, and embedded systems.</span><span class="sxs-lookup"><span data-stu-id="d00cd-183">Device-centric: Microsoft IoT allows you to connect anything, from legacy equipment to a vast ecosystem of certified hardware, and the ability to build your own devices across edge, mobile, and embedded systems.</span></span>

<span data-ttu-id="d00cd-184">**Secure**</span><span class="sxs-lookup"><span data-stu-id="d00cd-184">**Secure**</span></span> <br>
<span data-ttu-id="d00cd-185">Solve the hardest part of IoT — security</span><span class="sxs-lookup"><span data-stu-id="d00cd-185">Solve the hardest part of IoT — security</span></span>

* <span data-ttu-id="d00cd-186">Empower: with Microsoft IoT, you can bring together your vision, with the technology, best practices, and the capabilities to solve for the hardest part of IoT — security.</span><span class="sxs-lookup"><span data-stu-id="d00cd-186">Empower: with Microsoft IoT, you can bring together your vision, with the technology, best practices, and the capabilities to solve for the hardest part of IoT — security.</span></span>

* <span data-ttu-id="d00cd-187">Take action: secure your IoT data and manage risk with identity and access management, threat and information protection, and security management.</span><span class="sxs-lookup"><span data-stu-id="d00cd-187">Take action: secure your IoT data and manage risk with identity and access management, threat and information protection, and security management.</span></span>

* <span data-ttu-id="d00cd-188">Peace of mind: ensure the safety of sensitive information across devices, software, applications, and cloud services, as well as on-premises environments.</span><span class="sxs-lookup"><span data-stu-id="d00cd-188">Peace of mind: ensure the safety of sensitive information across devices, software, applications, and cloud services, as well as on-premises environments.</span></span>

* <span data-ttu-id="d00cd-189">Compliance: Microsoft has been leading the industry in establishing security requirements that meet a broad set of international and industry-specific standards for IoT devices, data, and services.</span><span class="sxs-lookup"><span data-stu-id="d00cd-189">Compliance: Microsoft has been leading the industry in establishing security requirements that meet a broad set of international and industry-specific standards for IoT devices, data, and services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d00cd-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="d00cd-190">Next steps</span></span>

<span data-ttu-id="d00cd-191">Explore the following areas of technologies and solutions, or see the Table of Contents to the left for the list of Azure IoT services.</span><span class="sxs-lookup"><span data-stu-id="d00cd-191">Explore the following areas of technologies and solutions, or see the Table of Contents to the left for the list of Azure IoT services.</span></span>

<ul class="panelContent cardsF">  
    <li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardText">
                        <h3><span data-ttu-id="d00cd-192">Solutions</span><span class="sxs-lookup"><span data-stu-id="d00cd-192">Solutions</span></span></h3><span data-ttu-id="d00cd-193">
                        <a href="/azure/iot-suite">IoT solution accelerators</a></span><span class="sxs-lookup"><span data-stu-id="d00cd-193">
                        <a href="/azure/iot-suite">IoT solution accelerators</a></span></span><br/><span data-ttu-id="d00cd-194">
                        <a href="/azure/iot-central">IoT Central</a>
                    </span><span class="sxs-lookup"><span data-stu-id="d00cd-194">
                        <a href="/azure/iot-central">IoT Central</a>
                    </span></span></div>
                </div>
            </div>
        </div>
    </li>
    <li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardText">
                        <h3><span data-ttu-id="d00cd-195">Platform services</span><span class="sxs-lookup"><span data-stu-id="d00cd-195">Platform services</span></span></h3><span data-ttu-id="d00cd-196">
                        <a href="/azure/iot-hub">IoT Hub</a></span><span class="sxs-lookup"><span data-stu-id="d00cd-196">
                        <a href="/azure/iot-hub">IoT Hub</a></span></span><br/><span data-ttu-id="d00cd-197">
                        <a href="/azure/iot-dps">IoT Hub Device Provisioning Service</a></span><span class="sxs-lookup"><span data-stu-id="d00cd-197">
                        <a href="/azure/iot-dps">IoT Hub Device Provisioning Service</a></span></span><br/><span data-ttu-id="d00cd-198">
                        <a href="/azure/azure-maps">Maps</a></span><span class="sxs-lookup"><span data-stu-id="d00cd-198">
                        <a href="/azure/azure-maps">Maps</a></span></span><br/><span data-ttu-id="d00cd-199">
                        <a href="/azure/time-series-insights">Time Series Insights</a>
                    </span><span class="sxs-lookup"><span data-stu-id="d00cd-199">
                        <a href="/azure/time-series-insights">Time Series Insights</a>
                    </span></span></div>
                </div>
            </div>
        </div>
    </li>  
    <li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardText">
                        <h3><span data-ttu-id="d00cd-200">Edge</span><span class="sxs-lookup"><span data-stu-id="d00cd-200">Edge</span></span></h3><span data-ttu-id="d00cd-201">
                        <a href="/azure/iot-edge">IoT Edge</a></span><span class="sxs-lookup"><span data-stu-id="d00cd-201">
                        <a href="/azure/iot-edge">IoT Edge</a></span></span><br/><span data-ttu-id="d00cd-202">
                        <a href="/azure/iot-edge/how-iot-edge-works">What is IoT Edge?</a>
                    </span><span class="sxs-lookup"><span data-stu-id="d00cd-202">
                        <a href="/azure/iot-edge/how-iot-edge-works">What is IoT Edge?</a>
                    </span></span></div>
                </div>
            </div>
        </div>
    </li>      
</ul>

[img-paas-saas-technologies-solutions]: media/index/paas-saas-technologies-solutions.png
[img-solution-architecture]: ./media/iot-introduction/iot-reference-architecture.png
[img-dashboard]: ./media/iot-introduction/iot-suite.png

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-central-land]: https://docs.microsoft.com/microsoft-iot-central/
[lnk-iot-dps-land]: /azure/iot-dps/index.yml
[lnk-iot-edge-land]: /azure/iot-edge/index.yml
[lnk-iot-hub-land]: /azure/iot-hub/index.md
[lnk-iot-maps-land]: /azure/maps/index.yml
[lnk-iot-sa-land]: ../iot-accelerators/index.yml
[lnk-iot-tsi-land]: /azure/time-series-insights/index.yml

[lnk-iot-hub]: ../iot-hub/about-iot-hub.md
[lnk-iot-sa]: ../iot-accelerators/about-iot-accelerators.md
[lnk-machinelearning]: http://azure.microsoft.com/documentation/services/machine-learning/
[lnk-protocol-gateway]:  ../iot-hub/iot-hub-protocol-gateway.md
[lnk-refarch]: https://aka.ms/iotrefarchitecture


