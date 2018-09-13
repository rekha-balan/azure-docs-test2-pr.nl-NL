---
title: IoT security best practices | Microsoft Docs
description: Security best practices for securing your IoT infrastructure
services: ''
suite: iot-suite
documentationcenter: ''
author: YuriDio
manager: timlt
editor: ''
ms.assetid: 24e7bda2-5f7b-44e3-b8af-761abd3276ff
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: yurid
ms.openlocfilehash: 87647756be65f577850fe8209173280b89de15ea
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556058"
---
# <a name="internet-of-things-security-best-practices"></a><span data-ttu-id="71176-103">Internet of Things security best practices</span><span class="sxs-lookup"><span data-stu-id="71176-103">Internet of Things security best practices</span></span>
<span data-ttu-id="71176-104">To secure an Internet of Things (IoT) infrastructure requires a rigorous security-in-depth strategy.</span><span class="sxs-lookup"><span data-stu-id="71176-104">To secure an Internet of Things (IoT) infrastructure requires a rigorous security-in-depth strategy.</span></span> <span data-ttu-id="71176-105">This strategy requires you to secure data in the cloud, protect data integrity while in transit over the public internet, and securely provision devices.</span><span class="sxs-lookup"><span data-stu-id="71176-105">This strategy requires you to secure data in the cloud, protect data integrity while in transit over the public internet, and securely provision devices.</span></span> <span data-ttu-id="71176-106">Each layer builds greater security assurance in the overall infrastructure.</span><span class="sxs-lookup"><span data-stu-id="71176-106">Each layer builds greater security assurance in the overall infrastructure.</span></span>

## <a name="secure-an-iot-infrastructure"></a><span data-ttu-id="71176-107">Secure an IoT infrastructure</span><span class="sxs-lookup"><span data-stu-id="71176-107">Secure an IoT infrastructure</span></span>
<span data-ttu-id="71176-108">This security-in-depth strategy can be developed and executed with active participation of various players involved with the manufacturing, development, and deployment of IoT devices and infrastructure.</span><span class="sxs-lookup"><span data-stu-id="71176-108">This security-in-depth strategy can be developed and executed with active participation of various players involved with the manufacturing, development, and deployment of IoT devices and infrastructure.</span></span> <span data-ttu-id="71176-109">Following is a high-level description of these players.</span><span class="sxs-lookup"><span data-stu-id="71176-109">Following is a high-level description of these players.</span></span>  

* <span data-ttu-id="71176-110">**IoT hardware manufacturer/integrator**: Typically, these are the manufacturers of IoT hardware being deployed, integrators assembling hardware from various manufacturers, or suppliers providing hardware for an IoT deployment manufactured or integrated by other suppliers.</span><span class="sxs-lookup"><span data-stu-id="71176-110">**IoT hardware manufacturer/integrator**: Typically, these are the manufacturers of IoT hardware being deployed, integrators assembling hardware from various manufacturers, or suppliers providing hardware for an IoT deployment manufactured or integrated by other suppliers.</span></span>
* <span data-ttu-id="71176-111">**IoT solution developer**: The development of an IoT solution is typically done by a solution developer.</span><span class="sxs-lookup"><span data-stu-id="71176-111">**IoT solution developer**: The development of an IoT solution is typically done by a solution developer.</span></span> <span data-ttu-id="71176-112">This developer may part of an in-house team or a system integrator (SI) specializing in this activity.</span><span class="sxs-lookup"><span data-stu-id="71176-112">This developer may part of an in-house team or a system integrator (SI) specializing in this activity.</span></span> <span data-ttu-id="71176-113">The IoT solution developer can develop various components of the IoT solution from scratch, integrate various off-the-shelf or open-source components, or adopt preconfigured solutions with minor adaptation.</span><span class="sxs-lookup"><span data-stu-id="71176-113">The IoT solution developer can develop various components of the IoT solution from scratch, integrate various off-the-shelf or open-source components, or adopt preconfigured solutions with minor adaptation.</span></span>
* <span data-ttu-id="71176-114">**IoT solution deployer**: After an IoT solution is developed, it needs to be deployed in the field.</span><span class="sxs-lookup"><span data-stu-id="71176-114">**IoT solution deployer**: After an IoT solution is developed, it needs to be deployed in the field.</span></span> <span data-ttu-id="71176-115">This involves deployment of hardware, interconnection of devices, and deployment of solutions in hardware devices or the cloud.</span><span class="sxs-lookup"><span data-stu-id="71176-115">This involves deployment of hardware, interconnection of devices, and deployment of solutions in hardware devices or the cloud.</span></span>
* <span data-ttu-id="71176-116">**IoT solution operator**: After the IoT solution is deployed, it requires long-term operations, monitoring, upgrades, and maintenance.</span><span class="sxs-lookup"><span data-stu-id="71176-116">**IoT solution operator**: After the IoT solution is deployed, it requires long-term operations, monitoring, upgrades, and maintenance.</span></span> <span data-ttu-id="71176-117">This can be done by an in-house team that comprises information technology specialists, hardware operations and maintenance teams, and domain specialists who monitor the correct behavior of overall IoT infrastructure.</span><span class="sxs-lookup"><span data-stu-id="71176-117">This can be done by an in-house team that comprises information technology specialists, hardware operations and maintenance teams, and domain specialists who monitor the correct behavior of overall IoT infrastructure.</span></span>

<span data-ttu-id="71176-118">The sections that follow provide best practices for each of these players to help develop, deploy, and operate a secure IoT infrastructure.</span><span class="sxs-lookup"><span data-stu-id="71176-118">The sections that follow provide best practices for each of these players to help develop, deploy, and operate a secure IoT infrastructure.</span></span>

## <a name="iot-hardware-manufacturerintegrator"></a><span data-ttu-id="71176-119">IoT hardware manufacturer/integrator</span><span class="sxs-lookup"><span data-stu-id="71176-119">IoT hardware manufacturer/integrator</span></span>
<span data-ttu-id="71176-120">The following are the best practices for IoT hardware manufacturers and hardware integrators.</span><span class="sxs-lookup"><span data-stu-id="71176-120">The following are the best practices for IoT hardware manufacturers and hardware integrators.</span></span>

* <span data-ttu-id="71176-121">**Scope hardware to minimum requirements**: The hardware design should include the minimum features required for operation of the hardware, and nothing more.</span><span class="sxs-lookup"><span data-stu-id="71176-121">**Scope hardware to minimum requirements**: The hardware design should include the minimum features required for operation of the hardware, and nothing more.</span></span> <span data-ttu-id="71176-122">An example is to include USB ports only if necessary for the operation of the device.</span><span class="sxs-lookup"><span data-stu-id="71176-122">An example is to include USB ports only if necessary for the operation of the device.</span></span> <span data-ttu-id="71176-123">These additional features open the device for unwanted attack vectors that should be avoided.</span><span class="sxs-lookup"><span data-stu-id="71176-123">These additional features open the device for unwanted attack vectors that should be avoided.</span></span>
* <span data-ttu-id="71176-124">**Make hardware tamper proof**: Build in mechanisms to detect physical tampering, such as opening of the device cover or removing a part of the device.</span><span class="sxs-lookup"><span data-stu-id="71176-124">**Make hardware tamper proof**: Build in mechanisms to detect physical tampering, such as opening of the device cover or removing a part of the device.</span></span> <span data-ttu-id="71176-125">These tamper signals may be part of the data stream uploaded to the cloud, which could alert operators of these events.</span><span class="sxs-lookup"><span data-stu-id="71176-125">These tamper signals may be part of the data stream uploaded to the cloud, which could alert operators of these events.</span></span>
* <span data-ttu-id="71176-126">**Build around secure hardware**: If COGS permits, build security features such as secure and encrypted storage, or boot functionality based on Trusted Platform Module (TPM).</span><span class="sxs-lookup"><span data-stu-id="71176-126">**Build around secure hardware**: If COGS permits, build security features such as secure and encrypted storage, or boot functionality based on Trusted Platform Module (TPM).</span></span> <span data-ttu-id="71176-127">These features make devices more secure and help protect the overall IoT infrastructure.</span><span class="sxs-lookup"><span data-stu-id="71176-127">These features make devices more secure and help protect the overall IoT infrastructure.</span></span>
* <span data-ttu-id="71176-128">**Make upgrades secure**: Firmware upgrades during the lifetime of the device are inevitable.</span><span class="sxs-lookup"><span data-stu-id="71176-128">**Make upgrades secure**: Firmware upgrades during the lifetime of the device are inevitable.</span></span> <span data-ttu-id="71176-129">Building devices with secure paths for upgrades and cryptographic assurance of firmware versions will allow the device to be secure during and after upgrades.</span><span class="sxs-lookup"><span data-stu-id="71176-129">Building devices with secure paths for upgrades and cryptographic assurance of firmware versions will allow the device to be secure during and after upgrades.</span></span>

## <a name="iot-solution-developer"></a><span data-ttu-id="71176-130">IoT solution developer</span><span class="sxs-lookup"><span data-stu-id="71176-130">IoT solution developer</span></span>
<span data-ttu-id="71176-131">The following are the best practices for IoT solution developers:</span><span class="sxs-lookup"><span data-stu-id="71176-131">The following are the best practices for IoT solution developers:</span></span>

* <span data-ttu-id="71176-132">**Follow secure software development methodology**: Development of secure software requires ground-up thinking about security, from the inception of the project all the way to its implementation, testing, and deployment.</span><span class="sxs-lookup"><span data-stu-id="71176-132">**Follow secure software development methodology**: Development of secure software requires ground-up thinking about security, from the inception of the project all the way to its implementation, testing, and deployment.</span></span> <span data-ttu-id="71176-133">The choices of platforms, languages, and tools are all influenced with this methodology.</span><span class="sxs-lookup"><span data-stu-id="71176-133">The choices of platforms, languages, and tools are all influenced with this methodology.</span></span> <span data-ttu-id="71176-134">The Microsoft Security Development Lifecycle provides a step-by-step approach to building secure software.</span><span class="sxs-lookup"><span data-stu-id="71176-134">The Microsoft Security Development Lifecycle provides a step-by-step approach to building secure software.</span></span>
* <span data-ttu-id="71176-135">**Choose open-source software with care**: Open-source software provides an opportunity to quickly develop solutions.</span><span class="sxs-lookup"><span data-stu-id="71176-135">**Choose open-source software with care**: Open-source software provides an opportunity to quickly develop solutions.</span></span> <span data-ttu-id="71176-136">When you're choosing open-source software, consider the activity level of the community for each open-source component.</span><span class="sxs-lookup"><span data-stu-id="71176-136">When you're choosing open-source software, consider the activity level of the community for each open-source component.</span></span> <span data-ttu-id="71176-137">An active community ensures that software is supported and that issues are discovered and addressed.</span><span class="sxs-lookup"><span data-stu-id="71176-137">An active community ensures that software is supported and that issues are discovered and addressed.</span></span> <span data-ttu-id="71176-138">Alternatively, an obscure and inactive open-source software might not be supported and issues will probably not be discovered.</span><span class="sxs-lookup"><span data-stu-id="71176-138">Alternatively, an obscure and inactive open-source software might not be supported and issues will probably not be discovered.</span></span>
* <span data-ttu-id="71176-139">**Integrate with care**: Many software security flaws exist at the boundary of libraries and APIs.</span><span class="sxs-lookup"><span data-stu-id="71176-139">**Integrate with care**: Many software security flaws exist at the boundary of libraries and APIs.</span></span> <span data-ttu-id="71176-140">Functionality that may not be required for the current deployment might still be available via an API layer.</span><span class="sxs-lookup"><span data-stu-id="71176-140">Functionality that may not be required for the current deployment might still be available via an API layer.</span></span> <span data-ttu-id="71176-141">To ensure overall security, make sure to check all interfaces of components being integrated for security flaws.</span><span class="sxs-lookup"><span data-stu-id="71176-141">To ensure overall security, make sure to check all interfaces of components being integrated for security flaws.</span></span>      

## <a name="iot-solution-deployer"></a><span data-ttu-id="71176-142">IoT solution deployer</span><span class="sxs-lookup"><span data-stu-id="71176-142">IoT solution deployer</span></span>
<span data-ttu-id="71176-143">The following are best practices for IoT solution deployers:</span><span class="sxs-lookup"><span data-stu-id="71176-143">The following are best practices for IoT solution deployers:</span></span>

* <span data-ttu-id="71176-144">**Deploy hardware securely**: IoT deployments may require hardware to be deployed in unsecure locations, such as in public spaces or unsupervised locales.</span><span class="sxs-lookup"><span data-stu-id="71176-144">**Deploy hardware securely**: IoT deployments may require hardware to be deployed in unsecure locations, such as in public spaces or unsupervised locales.</span></span> <span data-ttu-id="71176-145">In such situations, ensure that hardware deployment is tamper-proof to the maximum extent.</span><span class="sxs-lookup"><span data-stu-id="71176-145">In such situations, ensure that hardware deployment is tamper-proof to the maximum extent.</span></span> <span data-ttu-id="71176-146">If USB or other ports are available on the hardware, ensure that they are covered securely.</span><span class="sxs-lookup"><span data-stu-id="71176-146">If USB or other ports are available on the hardware, ensure that they are covered securely.</span></span> <span data-ttu-id="71176-147">Many attack vectors can use these as entry points.</span><span class="sxs-lookup"><span data-stu-id="71176-147">Many attack vectors can use these as entry points.</span></span>
* <span data-ttu-id="71176-148">**Keep authentication keys safe**: During deployment, each device requires device IDs and associated authentication keys generated by the cloud service.</span><span class="sxs-lookup"><span data-stu-id="71176-148">**Keep authentication keys safe**: During deployment, each device requires device IDs and associated authentication keys generated by the cloud service.</span></span> <span data-ttu-id="71176-149">Keep these keys physically safe even after the deployment.</span><span class="sxs-lookup"><span data-stu-id="71176-149">Keep these keys physically safe even after the deployment.</span></span> <span data-ttu-id="71176-150">Any compromised key can be used by a malicious device to masquerade as an existing device.</span><span class="sxs-lookup"><span data-stu-id="71176-150">Any compromised key can be used by a malicious device to masquerade as an existing device.</span></span>

## <a name="iot-solution-operator"></a><span data-ttu-id="71176-151">IoT solution operator</span><span class="sxs-lookup"><span data-stu-id="71176-151">IoT solution operator</span></span>
<span data-ttu-id="71176-152">The following are the best practices for IoT solution operators:</span><span class="sxs-lookup"><span data-stu-id="71176-152">The following are the best practices for IoT solution operators:</span></span>

* <span data-ttu-id="71176-153">**Keep the system up to date**: Ensure that device operating systems and all device drivers are upgraded to the latest versions.</span><span class="sxs-lookup"><span data-stu-id="71176-153">**Keep the system up to date**: Ensure that device operating systems and all device drivers are upgraded to the latest versions.</span></span> <span data-ttu-id="71176-154">If you turn on automatic updates in Windows 10 (IoT or other SKUs), Microsoft keeps it up to date, providing a secure operating system for IoT devices.</span><span class="sxs-lookup"><span data-stu-id="71176-154">If you turn on automatic updates in Windows 10 (IoT or other SKUs), Microsoft keeps it up to date, providing a secure operating system for IoT devices.</span></span> <span data-ttu-id="71176-155">Keeping other operating systems (such as Linux) up to date helps ensure that they are also protected against malicious attacks.</span><span class="sxs-lookup"><span data-stu-id="71176-155">Keeping other operating systems (such as Linux) up to date helps ensure that they are also protected against malicious attacks.</span></span>
* <span data-ttu-id="71176-156">**Protect against malicious activity**: If the operating system permits, install the latest antivirus and antimalware capabilities on each device operating system.</span><span class="sxs-lookup"><span data-stu-id="71176-156">**Protect against malicious activity**: If the operating system permits, install the latest antivirus and antimalware capabilities on each device operating system.</span></span> <span data-ttu-id="71176-157">This can help mitigate most external threats.</span><span class="sxs-lookup"><span data-stu-id="71176-157">This can help mitigate most external threats.</span></span> <span data-ttu-id="71176-158">You can protect most modern operating systems against threats by taking appropriate steps.</span><span class="sxs-lookup"><span data-stu-id="71176-158">You can protect most modern operating systems against threats by taking appropriate steps.</span></span>
* <span data-ttu-id="71176-159">**Audit frequently**: Auditing IoT infrastructure for security-related issues is key when responding to security incidents.</span><span class="sxs-lookup"><span data-stu-id="71176-159">**Audit frequently**: Auditing IoT infrastructure for security-related issues is key when responding to security incidents.</span></span> <span data-ttu-id="71176-160">Most operating systems provide built-in event logging that should be reviewed frequently to make sure no security breach has occurred.</span><span class="sxs-lookup"><span data-stu-id="71176-160">Most operating systems provide built-in event logging that should be reviewed frequently to make sure no security breach has occurred.</span></span> <span data-ttu-id="71176-161">Audit information can be sent as a separate telemetry stream to the cloud service where it can be analyzed.</span><span class="sxs-lookup"><span data-stu-id="71176-161">Audit information can be sent as a separate telemetry stream to the cloud service where it can be analyzed.</span></span>
* <span data-ttu-id="71176-162">**Physically protect the IoT infrastructure**: The worst security attacks against IoT infrastructure are launched using physical access to devices.</span><span class="sxs-lookup"><span data-stu-id="71176-162">**Physically protect the IoT infrastructure**: The worst security attacks against IoT infrastructure are launched using physical access to devices.</span></span> <span data-ttu-id="71176-163">One important safety practice is to protect against malicious use of USB ports and other physical access.</span><span class="sxs-lookup"><span data-stu-id="71176-163">One important safety practice is to protect against malicious use of USB ports and other physical access.</span></span> <span data-ttu-id="71176-164">One key to uncovering breaches that might have occurred is logging of physical access, such as USB port use.</span><span class="sxs-lookup"><span data-stu-id="71176-164">One key to uncovering breaches that might have occurred is logging of physical access, such as USB port use.</span></span> <span data-ttu-id="71176-165">Again, Windows 10 (IoT and other SKUs) enables detailed logging of these events.</span><span class="sxs-lookup"><span data-stu-id="71176-165">Again, Windows 10 (IoT and other SKUs) enables detailed logging of these events.</span></span>
* <span data-ttu-id="71176-166">**Protect cloud credentials**: Cloud authentication credentials used for configuring and operating an IoT deployment are possibly the easiest way to gain access and compromise an IoT system.</span><span class="sxs-lookup"><span data-stu-id="71176-166">**Protect cloud credentials**: Cloud authentication credentials used for configuring and operating an IoT deployment are possibly the easiest way to gain access and compromise an IoT system.</span></span> <span data-ttu-id="71176-167">Protect the credentials by changing the password frequently, and refrain from using these credentials on public machines.</span><span class="sxs-lookup"><span data-stu-id="71176-167">Protect the credentials by changing the password frequently, and refrain from using these credentials on public machines.</span></span>

<span data-ttu-id="71176-168">Capabilities of different IoT devices vary.</span><span class="sxs-lookup"><span data-stu-id="71176-168">Capabilities of different IoT devices vary.</span></span> <span data-ttu-id="71176-169">Some devices might be computers running common desktop operating systems, and some devices might be running very light-weight operating systems.</span><span class="sxs-lookup"><span data-stu-id="71176-169">Some devices might be computers running common desktop operating systems, and some devices might be running very light-weight operating systems.</span></span> <span data-ttu-id="71176-170">The security best practices described previously might be applicable to these devices in varying degrees.</span><span class="sxs-lookup"><span data-stu-id="71176-170">The security best practices described previously might be applicable to these devices in varying degrees.</span></span> <span data-ttu-id="71176-171">If provided, additional security and deployment best practices from the manufacturers of these devices should be followed.</span><span class="sxs-lookup"><span data-stu-id="71176-171">If provided, additional security and deployment best practices from the manufacturers of these devices should be followed.</span></span>

<span data-ttu-id="71176-172">Some legacy and constrained devices might not have been designed specifically for IoT deployment.</span><span class="sxs-lookup"><span data-stu-id="71176-172">Some legacy and constrained devices might not have been designed specifically for IoT deployment.</span></span> <span data-ttu-id="71176-173">These devices might lack the capability to encrypt data, connect with the Internet, or provide advanced auditing.</span><span class="sxs-lookup"><span data-stu-id="71176-173">These devices might lack the capability to encrypt data, connect with the Internet, or provide advanced auditing.</span></span> <span data-ttu-id="71176-174">In these cases, a modern and secure field gateway can aggregate data from legacy devices and provide the security required for connecting these devices over the Internet.</span><span class="sxs-lookup"><span data-stu-id="71176-174">In these cases, a modern and secure field gateway can aggregate data from legacy devices and provide the security required for connecting these devices over the Internet.</span></span> <span data-ttu-id="71176-175">Field gateways can provide secure authentication, negotiation of encrypted sessions, receipt of commands from the cloud, and many other security features.</span><span class="sxs-lookup"><span data-stu-id="71176-175">Field gateways can provide secure authentication, negotiation of encrypted sessions, receipt of commands from the cloud, and many other security features.</span></span>

## <a name="see-also"></a><span data-ttu-id="71176-176">See also</span><span class="sxs-lookup"><span data-stu-id="71176-176">See also</span></span>
<span data-ttu-id="71176-177">To learn more about securing your IoT solution, see:</span><span class="sxs-lookup"><span data-stu-id="71176-177">To learn more about securing your IoT solution, see:</span></span>

* <span data-ttu-id="71176-178">[IoT security architecture][lnk-security-architecture]</span><span class="sxs-lookup"><span data-stu-id="71176-178">[IoT security architecture][lnk-security-architecture]</span></span>
* <span data-ttu-id="71176-179">[Secure your IoT deployment][lnk-security-deployment]</span><span class="sxs-lookup"><span data-stu-id="71176-179">[Secure your IoT deployment][lnk-security-deployment]</span></span>

<span data-ttu-id="71176-180">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span><span class="sxs-lookup"><span data-stu-id="71176-180">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="71176-181">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="71176-181">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* <span data-ttu-id="71176-182">[Frequently asked questions for Azure IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="71176-182">[Frequently asked questions for Azure IoT Suite][lnk-faq]</span></span>

<span data-ttu-id="71176-183">You can read about IoT Hub security in [Control access to IoT Hub][lnk-devguide-security] in the IoT Hub developer guide.</span><span class="sxs-lookup"><span data-stu-id="71176-183">You can read about IoT Hub security in [Control access to IoT Hub][lnk-devguide-security] in the IoT Hub developer guide.</span></span>

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md

[lnk-security-architecture]: iot-security-architecture.md
[lnk-security-deployment]: iot-suite-security-deployment.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md