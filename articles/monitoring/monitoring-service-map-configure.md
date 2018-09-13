---
title: Configure Service Map in Azure | Microsoft Docs
description: Service Map is a solution in Azure that automatically discovers application components on Windows and Linux systems and maps the communication between services. This article provides details for deploying Service Map in your environment and using it in a variety of scenarios.
services: monitoring
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: d3d66b45-9874-4aad-9c00-124734944b2e
ms.service: monitoring
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/20/2018
ms.author: daseidma;bwren
ms.openlocfilehash: faf4e06b714714fce206ef8227a934df8c290447
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869852"
---
# <a name="configure-service-map-in-azure"></a><span data-ttu-id="91ada-104">Configure Service Map in Azure</span><span class="sxs-lookup"><span data-stu-id="91ada-104">Configure Service Map in Azure</span></span>
<span data-ttu-id="91ada-105">Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services.</span><span class="sxs-lookup"><span data-stu-id="91ada-105">Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="91ada-106">You can use it to view your servers as you think of them--interconnected systems that deliver critical services.</span><span class="sxs-lookup"><span data-stu-id="91ada-106">You can use it to view your servers as you think of them--interconnected systems that deliver critical services.</span></span> <span data-ttu-id="91ada-107">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required, other than installation of an agent.</span><span class="sxs-lookup"><span data-stu-id="91ada-107">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required, other than installation of an agent.</span></span>

<span data-ttu-id="91ada-108">This article describes the details of configuring Service Map and onboarding agents.</span><span class="sxs-lookup"><span data-stu-id="91ada-108">This article describes the details of configuring Service Map and onboarding agents.</span></span> <span data-ttu-id="91ada-109">For information on using Service Map, see [Use the Service Map solution in Azure]( monitoring-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="91ada-109">For information on using Service Map, see [Use the Service Map solution in Azure]( monitoring-service-map.md).</span></span>

## <a name="supported-azure-regions"></a><span data-ttu-id="91ada-110">Supported Azure regions</span><span class="sxs-lookup"><span data-stu-id="91ada-110">Supported Azure regions</span></span>
<span data-ttu-id="91ada-111">Service Map is currently available in the following Azure regions:</span><span class="sxs-lookup"><span data-stu-id="91ada-111">Service Map is currently available in the following Azure regions:</span></span>
- <span data-ttu-id="91ada-112">East US</span><span class="sxs-lookup"><span data-stu-id="91ada-112">East US</span></span>
- <span data-ttu-id="91ada-113">West Europe</span><span class="sxs-lookup"><span data-stu-id="91ada-113">West Europe</span></span>
- <span data-ttu-id="91ada-114">West Central US</span><span class="sxs-lookup"><span data-stu-id="91ada-114">West Central US</span></span>
- <span data-ttu-id="91ada-115">Southeast Asia</span><span class="sxs-lookup"><span data-stu-id="91ada-115">Southeast Asia</span></span>

## <a name="supported-windows-operating-systems"></a><span data-ttu-id="91ada-116">Supported Windows operating systems</span><span class="sxs-lookup"><span data-stu-id="91ada-116">Supported Windows operating systems</span></span>
<span data-ttu-id="91ada-117">The following section list the supported operating systems for the Dependency agent on Windows.</span><span class="sxs-lookup"><span data-stu-id="91ada-117">The following section list the supported operating systems for the Dependency agent on Windows.</span></span> 

>[!NOTE]
><span data-ttu-id="91ada-118">Service Map supports only 64-bit platforms.</span><span class="sxs-lookup"><span data-stu-id="91ada-118">Service Map supports only 64-bit platforms.</span></span>
>

### <a name="windows-server"></a><span data-ttu-id="91ada-119">Windows Server</span><span class="sxs-lookup"><span data-stu-id="91ada-119">Windows Server</span></span>
- <span data-ttu-id="91ada-120">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="91ada-120">Windows Server 2016</span></span>
- <span data-ttu-id="91ada-121">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="91ada-121">Windows Server 2012 R2</span></span>
- <span data-ttu-id="91ada-122">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="91ada-122">Windows Server 2012</span></span>
- <span data-ttu-id="91ada-123">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="91ada-123">Windows Server 2008 R2 SP1</span></span>

### <a name="windows-desktop"></a><span data-ttu-id="91ada-124">Windows desktop</span><span class="sxs-lookup"><span data-stu-id="91ada-124">Windows desktop</span></span>
- <span data-ttu-id="91ada-125">Windows 10</span><span class="sxs-lookup"><span data-stu-id="91ada-125">Windows 10</span></span>
- <span data-ttu-id="91ada-126">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="91ada-126">Windows 8.1</span></span>
- <span data-ttu-id="91ada-127">Windows 8</span><span class="sxs-lookup"><span data-stu-id="91ada-127">Windows 8</span></span>
- <span data-ttu-id="91ada-128">Windows 7</span><span class="sxs-lookup"><span data-stu-id="91ada-128">Windows 7</span></span>

## <a name="supported-linux-operating-systems"></a><span data-ttu-id="91ada-129">Supported Linux operating systems</span><span class="sxs-lookup"><span data-stu-id="91ada-129">Supported Linux operating systems</span></span>
<span data-ttu-id="91ada-130">The following section list the supported operating systems for the Dependency agent on Red Hat Enterprise Linux, CentOS Linux, and Oracle Linux (with RHEL Kernel).</span><span class="sxs-lookup"><span data-stu-id="91ada-130">The following section list the supported operating systems for the Dependency agent on Red Hat Enterprise Linux, CentOS Linux, and Oracle Linux (with RHEL Kernel).</span></span>  

- <span data-ttu-id="91ada-131">Only default and SMP Linux kernel releases are supported.</span><span class="sxs-lookup"><span data-stu-id="91ada-131">Only default and SMP Linux kernel releases are supported.</span></span>
- <span data-ttu-id="91ada-132">Nonstandard kernel releases, such as PAE and Xen, are not supported for any Linux distribution.</span><span class="sxs-lookup"><span data-stu-id="91ada-132">Nonstandard kernel releases, such as PAE and Xen, are not supported for any Linux distribution.</span></span> <span data-ttu-id="91ada-133">For example, a system with the release string of "2.6.16.21-0.8-xen" is not supported.</span><span class="sxs-lookup"><span data-stu-id="91ada-133">For example, a system with the release string of "2.6.16.21-0.8-xen" is not supported.</span></span>
- <span data-ttu-id="91ada-134">Custom kernels, including recompiles of standard kernels, are not supported.</span><span class="sxs-lookup"><span data-stu-id="91ada-134">Custom kernels, including recompiles of standard kernels, are not supported.</span></span>
- <span data-ttu-id="91ada-135">CentOSPlus kernel is not supported.</span><span class="sxs-lookup"><span data-stu-id="91ada-135">CentOSPlus kernel is not supported.</span></span>
- <span data-ttu-id="91ada-136">Oracle Unbreakable Enterprise Kernel (UEK) is covered in a later section of this article.</span><span class="sxs-lookup"><span data-stu-id="91ada-136">Oracle Unbreakable Enterprise Kernel (UEK) is covered in a later section of this article.</span></span>

### <a name="red-hat-linux-7"></a><span data-ttu-id="91ada-137">Red Hat Linux 7</span><span class="sxs-lookup"><span data-stu-id="91ada-137">Red Hat Linux 7</span></span>

| <span data-ttu-id="91ada-138">OS version</span><span class="sxs-lookup"><span data-stu-id="91ada-138">OS version</span></span> | <span data-ttu-id="91ada-139">Kernel version</span><span class="sxs-lookup"><span data-stu-id="91ada-139">Kernel version</span></span> |
|:--|:--|
| <span data-ttu-id="91ada-140">7.0</span><span class="sxs-lookup"><span data-stu-id="91ada-140">7.0</span></span> | <span data-ttu-id="91ada-141">3.10.0-123</span><span class="sxs-lookup"><span data-stu-id="91ada-141">3.10.0-123</span></span> |
| <span data-ttu-id="91ada-142">7.1</span><span class="sxs-lookup"><span data-stu-id="91ada-142">7.1</span></span> | <span data-ttu-id="91ada-143">3.10.0-229</span><span class="sxs-lookup"><span data-stu-id="91ada-143">3.10.0-229</span></span> |
| <span data-ttu-id="91ada-144">7.2</span><span class="sxs-lookup"><span data-stu-id="91ada-144">7.2</span></span> | <span data-ttu-id="91ada-145">3.10.0-327</span><span class="sxs-lookup"><span data-stu-id="91ada-145">3.10.0-327</span></span> |
| <span data-ttu-id="91ada-146">7.3</span><span class="sxs-lookup"><span data-stu-id="91ada-146">7.3</span></span> | <span data-ttu-id="91ada-147">3.10.0-514</span><span class="sxs-lookup"><span data-stu-id="91ada-147">3.10.0-514</span></span> |
| <span data-ttu-id="91ada-148">7.4</span><span class="sxs-lookup"><span data-stu-id="91ada-148">7.4</span></span> | <span data-ttu-id="91ada-149">3.10.0-693</span><span class="sxs-lookup"><span data-stu-id="91ada-149">3.10.0-693</span></span> |
| <span data-ttu-id="91ada-150">7.5</span><span class="sxs-lookup"><span data-stu-id="91ada-150">7.5</span></span> | <span data-ttu-id="91ada-151">3.10.0-862</span><span class="sxs-lookup"><span data-stu-id="91ada-151">3.10.0-862</span></span> |

### <a name="red-hat-linux-6"></a><span data-ttu-id="91ada-152">Red Hat Linux 6</span><span class="sxs-lookup"><span data-stu-id="91ada-152">Red Hat Linux 6</span></span>

| <span data-ttu-id="91ada-153">OS version</span><span class="sxs-lookup"><span data-stu-id="91ada-153">OS version</span></span> | <span data-ttu-id="91ada-154">Kernel version</span><span class="sxs-lookup"><span data-stu-id="91ada-154">Kernel version</span></span> |
|:--|:--|
| <span data-ttu-id="91ada-155">6.0</span><span class="sxs-lookup"><span data-stu-id="91ada-155">6.0</span></span> | <span data-ttu-id="91ada-156">2.6.32-71</span><span class="sxs-lookup"><span data-stu-id="91ada-156">2.6.32-71</span></span> |
| <span data-ttu-id="91ada-157">6.1</span><span class="sxs-lookup"><span data-stu-id="91ada-157">6.1</span></span> | <span data-ttu-id="91ada-158">2.6.32-131</span><span class="sxs-lookup"><span data-stu-id="91ada-158">2.6.32-131</span></span> |
| <span data-ttu-id="91ada-159">6.2</span><span class="sxs-lookup"><span data-stu-id="91ada-159">6.2</span></span> | <span data-ttu-id="91ada-160">2.6.32-220</span><span class="sxs-lookup"><span data-stu-id="91ada-160">2.6.32-220</span></span> |
| <span data-ttu-id="91ada-161">6.3</span><span class="sxs-lookup"><span data-stu-id="91ada-161">6.3</span></span> | <span data-ttu-id="91ada-162">2.6.32-279</span><span class="sxs-lookup"><span data-stu-id="91ada-162">2.6.32-279</span></span> |
| <span data-ttu-id="91ada-163">6.4</span><span class="sxs-lookup"><span data-stu-id="91ada-163">6.4</span></span> | <span data-ttu-id="91ada-164">2.6.32-358</span><span class="sxs-lookup"><span data-stu-id="91ada-164">2.6.32-358</span></span> |
| <span data-ttu-id="91ada-165">6.5</span><span class="sxs-lookup"><span data-stu-id="91ada-165">6.5</span></span> | <span data-ttu-id="91ada-166">2.6.32-431</span><span class="sxs-lookup"><span data-stu-id="91ada-166">2.6.32-431</span></span> |
| <span data-ttu-id="91ada-167">6.6</span><span class="sxs-lookup"><span data-stu-id="91ada-167">6.6</span></span> | <span data-ttu-id="91ada-168">2.6.32-504</span><span class="sxs-lookup"><span data-stu-id="91ada-168">2.6.32-504</span></span> |
| <span data-ttu-id="91ada-169">6.7</span><span class="sxs-lookup"><span data-stu-id="91ada-169">6.7</span></span> | <span data-ttu-id="91ada-170">2.6.32-573</span><span class="sxs-lookup"><span data-stu-id="91ada-170">2.6.32-573</span></span> |
| <span data-ttu-id="91ada-171">6.8</span><span class="sxs-lookup"><span data-stu-id="91ada-171">6.8</span></span> | <span data-ttu-id="91ada-172">2.6.32-642</span><span class="sxs-lookup"><span data-stu-id="91ada-172">2.6.32-642</span></span> |
| <span data-ttu-id="91ada-173">6.9</span><span class="sxs-lookup"><span data-stu-id="91ada-173">6.9</span></span> | <span data-ttu-id="91ada-174">2.6.32-696</span><span class="sxs-lookup"><span data-stu-id="91ada-174">2.6.32-696</span></span> |

### <a name="ubuntu-server"></a><span data-ttu-id="91ada-175">Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="91ada-175">Ubuntu Server</span></span>

| <span data-ttu-id="91ada-176">OS version</span><span class="sxs-lookup"><span data-stu-id="91ada-176">OS version</span></span> | <span data-ttu-id="91ada-177">Kernel version</span><span class="sxs-lookup"><span data-stu-id="91ada-177">Kernel version</span></span> |
|:--|:--|
| <span data-ttu-id="91ada-178">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="91ada-178">Ubuntu 18.04</span></span> | <span data-ttu-id="91ada-179">kernel 4.15.\*</span><span class="sxs-lookup"><span data-stu-id="91ada-179">kernel 4.15.\*</span></span> |
| <span data-ttu-id="91ada-180">Ubuntu 16.04.3</span><span class="sxs-lookup"><span data-stu-id="91ada-180">Ubuntu 16.04.3</span></span> | <span data-ttu-id="91ada-181">kernel 4.15.\*</span><span class="sxs-lookup"><span data-stu-id="91ada-181">kernel 4.15.\*</span></span> |
| <span data-ttu-id="91ada-182">16.04</span><span class="sxs-lookup"><span data-stu-id="91ada-182">16.04</span></span> | <span data-ttu-id="91ada-183">4.4.\*</span><span class="sxs-lookup"><span data-stu-id="91ada-183">4.4.\*</span></span><br><span data-ttu-id="91ada-184">4.8.\*</span><span class="sxs-lookup"><span data-stu-id="91ada-184">4.8.\*</span></span><br><span data-ttu-id="91ada-185">4.10.\*</span><span class="sxs-lookup"><span data-stu-id="91ada-185">4.10.\*</span></span><br><span data-ttu-id="91ada-186">4.11.\*</span><span class="sxs-lookup"><span data-stu-id="91ada-186">4.11.\*</span></span><br><span data-ttu-id="91ada-187">4.13.\*</span><span class="sxs-lookup"><span data-stu-id="91ada-187">4.13.\*</span></span> |
| <span data-ttu-id="91ada-188">14.04</span><span class="sxs-lookup"><span data-stu-id="91ada-188">14.04</span></span> | <span data-ttu-id="91ada-189">3.13.\*</span><span class="sxs-lookup"><span data-stu-id="91ada-189">3.13.\*</span></span><br><span data-ttu-id="91ada-190">4.4.\*</span><span class="sxs-lookup"><span data-stu-id="91ada-190">4.4.\*</span></span> |

### <a name="oracle-enterprise-linux-6-with-unbreakable-enterprise-kernel"></a><span data-ttu-id="91ada-191">Oracle Enterprise Linux 6 with Unbreakable Enterprise Kernel</span><span class="sxs-lookup"><span data-stu-id="91ada-191">Oracle Enterprise Linux 6 with Unbreakable Enterprise Kernel</span></span>
| <span data-ttu-id="91ada-192">OS version</span><span class="sxs-lookup"><span data-stu-id="91ada-192">OS version</span></span> | <span data-ttu-id="91ada-193">Kernel version</span><span class="sxs-lookup"><span data-stu-id="91ada-193">Kernel version</span></span>
|:--|:--|
| <span data-ttu-id="91ada-194">6.2</span><span class="sxs-lookup"><span data-stu-id="91ada-194">6.2</span></span> | <span data-ttu-id="91ada-195">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="91ada-195">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="91ada-196">6.3</span><span class="sxs-lookup"><span data-stu-id="91ada-196">6.3</span></span> | <span data-ttu-id="91ada-197">Oracle 2.6.39-200 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="91ada-197">Oracle 2.6.39-200 (UEK R2)</span></span> |
| <span data-ttu-id="91ada-198">6.4</span><span class="sxs-lookup"><span data-stu-id="91ada-198">6.4</span></span> | <span data-ttu-id="91ada-199">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="91ada-199">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="91ada-200">6.5</span><span class="sxs-lookup"><span data-stu-id="91ada-200">6.5</span></span> | <span data-ttu-id="91ada-201">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="91ada-201">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |
| <span data-ttu-id="91ada-202">6.6</span><span class="sxs-lookup"><span data-stu-id="91ada-202">6.6</span></span> | <span data-ttu-id="91ada-203">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="91ada-203">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |

### <a name="oracle-enterprise-linux-5-with-unbreakable-enterprise-kernel"></a><span data-ttu-id="91ada-204">Oracle Enterprise Linux 5 with Unbreakable Enterprise Kernel</span><span class="sxs-lookup"><span data-stu-id="91ada-204">Oracle Enterprise Linux 5 with Unbreakable Enterprise Kernel</span></span>

| <span data-ttu-id="91ada-205">OS version</span><span class="sxs-lookup"><span data-stu-id="91ada-205">OS version</span></span> | <span data-ttu-id="91ada-206">Kernel version</span><span class="sxs-lookup"><span data-stu-id="91ada-206">Kernel version</span></span>
|:--|:--|
| <span data-ttu-id="91ada-207">5.10</span><span class="sxs-lookup"><span data-stu-id="91ada-207">5.10</span></span> | <span data-ttu-id="91ada-208">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="91ada-208">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="91ada-209">5.11</span><span class="sxs-lookup"><span data-stu-id="91ada-209">5.11</span></span> | <span data-ttu-id="91ada-210">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="91ada-210">Oracle 2.6.39-400 (UEK R2)</span></span> |

## <a name="suse-linux-12-enterprise-server"></a><span data-ttu-id="91ada-211">SUSE Linux 12 Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="91ada-211">SUSE Linux 12 Enterprise Server</span></span>

| <span data-ttu-id="91ada-212">OS version</span><span class="sxs-lookup"><span data-stu-id="91ada-212">OS version</span></span> | <span data-ttu-id="91ada-213">Kernel version</span><span class="sxs-lookup"><span data-stu-id="91ada-213">Kernel version</span></span>
|:--|:--|
|<span data-ttu-id="91ada-214">12 SP2</span><span class="sxs-lookup"><span data-stu-id="91ada-214">12 SP2</span></span> | <span data-ttu-id="91ada-215">4.4.\*</span><span class="sxs-lookup"><span data-stu-id="91ada-215">4.4.\*</span></span> |
|<span data-ttu-id="91ada-216">12 SP3</span><span class="sxs-lookup"><span data-stu-id="91ada-216">12 SP3</span></span> | <span data-ttu-id="91ada-217">4.4.\*</span><span class="sxs-lookup"><span data-stu-id="91ada-217">4.4.\*</span></span> |

## <a name="dependency-agent-downloads"></a><span data-ttu-id="91ada-218">Dependency agent downloads</span><span class="sxs-lookup"><span data-stu-id="91ada-218">Dependency agent downloads</span></span>

| <span data-ttu-id="91ada-219">File</span><span class="sxs-lookup"><span data-stu-id="91ada-219">File</span></span> | <span data-ttu-id="91ada-220">OS</span><span class="sxs-lookup"><span data-stu-id="91ada-220">OS</span></span> | <span data-ttu-id="91ada-221">Version</span><span class="sxs-lookup"><span data-stu-id="91ada-221">Version</span></span> | <span data-ttu-id="91ada-222">SHA-256</span><span class="sxs-lookup"><span data-stu-id="91ada-222">SHA-256</span></span> |
|:--|:--|:--|:--|
| [<span data-ttu-id="91ada-223">InstallDependencyAgent-Windows.exe</span><span class="sxs-lookup"><span data-stu-id="91ada-223">InstallDependencyAgent-Windows.exe</span></span>](https://aka.ms/dependencyagentwindows) | <span data-ttu-id="91ada-224">Windows</span><span class="sxs-lookup"><span data-stu-id="91ada-224">Windows</span></span> | <span data-ttu-id="91ada-225">9.5.0</span><span class="sxs-lookup"><span data-stu-id="91ada-225">9.5.0</span></span> | <span data-ttu-id="91ada-226">8B8FE0F6B0A9F589C4B7B52945C2C25DF008058EB4D4866DC45EE2485062C9D7</span><span class="sxs-lookup"><span data-stu-id="91ada-226">8B8FE0F6B0A9F589C4B7B52945C2C25DF008058EB4D4866DC45EE2485062C9D7</span></span> |
| [<span data-ttu-id="91ada-227">InstallDependencyAgent-Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="91ada-227">InstallDependencyAgent-Linux64.bin</span></span>](https://aka.ms/dependencyagentlinux) | <span data-ttu-id="91ada-228">Linux</span><span class="sxs-lookup"><span data-stu-id="91ada-228">Linux</span></span> | <span data-ttu-id="91ada-229">9.5.1</span><span class="sxs-lookup"><span data-stu-id="91ada-229">9.5.1</span></span> | <span data-ttu-id="91ada-230">09D56EF43703A350FF586B774900E1F48E72FE3671144B5C99BB1A494C201E9E</span><span class="sxs-lookup"><span data-stu-id="91ada-230">09D56EF43703A350FF586B774900E1F48E72FE3671144B5C99BB1A494C201E9E</span></span> |

## <a name="connected-sources"></a><span data-ttu-id="91ada-231">Connected sources</span><span class="sxs-lookup"><span data-stu-id="91ada-231">Connected sources</span></span>
<span data-ttu-id="91ada-232">Service Map gets its data from the Microsoft Dependency agent.</span><span class="sxs-lookup"><span data-stu-id="91ada-232">Service Map gets its data from the Microsoft Dependency agent.</span></span> <span data-ttu-id="91ada-233">The Dependency agent relies on the Log Analytics agent for its connections to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="91ada-233">The Dependency agent relies on the Log Analytics agent for its connections to Log Analytics.</span></span> <span data-ttu-id="91ada-234">This means that a server must have the Log Analytics agent installed and configured with the Dependency agent.</span><span class="sxs-lookup"><span data-stu-id="91ada-234">This means that a server must have the Log Analytics agent installed and configured with the Dependency agent.</span></span>  <span data-ttu-id="91ada-235">The following table describes the connected sources that the Service Map solution supports.</span><span class="sxs-lookup"><span data-stu-id="91ada-235">The following table describes the connected sources that the Service Map solution supports.</span></span>

| <span data-ttu-id="91ada-236">Connected source</span><span class="sxs-lookup"><span data-stu-id="91ada-236">Connected source</span></span> | <span data-ttu-id="91ada-237">Supported</span><span class="sxs-lookup"><span data-stu-id="91ada-237">Supported</span></span> | <span data-ttu-id="91ada-238">Description</span><span class="sxs-lookup"><span data-stu-id="91ada-238">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="91ada-239">Windows agents</span><span class="sxs-lookup"><span data-stu-id="91ada-239">Windows agents</span></span> | <span data-ttu-id="91ada-240">Yes</span><span class="sxs-lookup"><span data-stu-id="91ada-240">Yes</span></span> | <span data-ttu-id="91ada-241">Service Map analyzes and collects data from Windows computers.</span><span class="sxs-lookup"><span data-stu-id="91ada-241">Service Map analyzes and collects data from Windows computers.</span></span> <br><br><span data-ttu-id="91ada-242">In addition to the [Log Analytics agent for Windows](../log-analytics/log-analytics-concept-hybrid.md), Windows agents require the Microsoft Dependency agent.</span><span class="sxs-lookup"><span data-stu-id="91ada-242">In addition to the [Log Analytics agent for Windows](../log-analytics/log-analytics-concept-hybrid.md), Windows agents require the Microsoft Dependency agent.</span></span> <span data-ttu-id="91ada-243">See the [supported operating systems](#supported-operating-systems) for a complete list of operating system versions.</span><span class="sxs-lookup"><span data-stu-id="91ada-243">See the [supported operating systems](#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="91ada-244">Linux agents</span><span class="sxs-lookup"><span data-stu-id="91ada-244">Linux agents</span></span> | <span data-ttu-id="91ada-245">Yes</span><span class="sxs-lookup"><span data-stu-id="91ada-245">Yes</span></span> | <span data-ttu-id="91ada-246">Service Map analyzes and collects data from Linux computers.</span><span class="sxs-lookup"><span data-stu-id="91ada-246">Service Map analyzes and collects data from Linux computers.</span></span> <br><br><span data-ttu-id="91ada-247">In addition to the [Log Analytics agent for Linux](../log-analytics/log-analytics-concept-hybrid.md), Linux agents require the Microsoft Dependency agent.</span><span class="sxs-lookup"><span data-stu-id="91ada-247">In addition to the [Log Analytics agent for Linux](../log-analytics/log-analytics-concept-hybrid.md), Linux agents require the Microsoft Dependency agent.</span></span> <span data-ttu-id="91ada-248">See the [supported operating systems](#supported-operating-systems) for a complete list of operating system versions.</span><span class="sxs-lookup"><span data-stu-id="91ada-248">See the [supported operating systems](#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="91ada-249">System Center Operations Manager management group</span><span class="sxs-lookup"><span data-stu-id="91ada-249">System Center Operations Manager management group</span></span> | <span data-ttu-id="91ada-250">Yes</span><span class="sxs-lookup"><span data-stu-id="91ada-250">Yes</span></span> | <span data-ttu-id="91ada-251">Service Map analyzes and collects data from Windows and Linux agents in a connected [System Center Operations Manager management group](../log-analytics/log-analytics-om-agents.md).</span><span class="sxs-lookup"><span data-stu-id="91ada-251">Service Map analyzes and collects data from Windows and Linux agents in a connected [System Center Operations Manager management group](../log-analytics/log-analytics-om-agents.md).</span></span> <br><br><span data-ttu-id="91ada-252">A direct connection from the System Center Operations Manager agent computer to Log Analytics is required.</span><span class="sxs-lookup"><span data-stu-id="91ada-252">A direct connection from the System Center Operations Manager agent computer to Log Analytics is required.</span></span> |
| <span data-ttu-id="91ada-253">Azure storage account</span><span class="sxs-lookup"><span data-stu-id="91ada-253">Azure storage account</span></span> | <span data-ttu-id="91ada-254">No</span><span class="sxs-lookup"><span data-stu-id="91ada-254">No</span></span> | <span data-ttu-id="91ada-255">Service Map collects data from agent computers, so there is no data from it to collect from Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="91ada-255">Service Map collects data from agent computers, so there is no data from it to collect from Azure Storage.</span></span> |

<span data-ttu-id="91ada-256">On Windows, the Microsoft Monitoring Agent (MMA) is used by both System Center Operations Manager and Log Analytics to gather and send monitoring data.</span><span class="sxs-lookup"><span data-stu-id="91ada-256">On Windows, the Microsoft Monitoring Agent (MMA) is used by both System Center Operations Manager and Log Analytics to gather and send monitoring data.</span></span> <span data-ttu-id="91ada-257">(This agent is called the System Center Operations Manager agent, OMS Agent, Log Analytics agent, MMA, or Direct Agent, depending on the context.) System Center Operations Manager and Log Analytics provide different out-of-the box versions of the MMA.</span><span class="sxs-lookup"><span data-stu-id="91ada-257">(This agent is called the System Center Operations Manager agent, OMS Agent, Log Analytics agent, MMA, or Direct Agent, depending on the context.) System Center Operations Manager and Log Analytics provide different out-of-the box versions of the MMA.</span></span> <span data-ttu-id="91ada-258">These versions can each report to System Center Operations Manager, to Log Analytics, or to both.</span><span class="sxs-lookup"><span data-stu-id="91ada-258">These versions can each report to System Center Operations Manager, to Log Analytics, or to both.</span></span>  

<span data-ttu-id="91ada-259">On Linux, the Log Analytics agent for Linux gathers and sends monitoring data to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="91ada-259">On Linux, the Log Analytics agent for Linux gathers and sends monitoring data to Log Analytics.</span></span> <span data-ttu-id="91ada-260">You can use Service Map on servers with Log Analytics agents connected directly to the service, or that are reporting to an Operations Manager management group integrated with Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="91ada-260">You can use Service Map on servers with Log Analytics agents connected directly to the service, or that are reporting to an Operations Manager management group integrated with Log Analytics.</span></span>  

<span data-ttu-id="91ada-261">In this article, we'll refer to all agents, whether Linux or Windows connected to a System Center Operations Manager management group or directly to Log Analytics, as the *Log Analytics agent*.</span><span class="sxs-lookup"><span data-stu-id="91ada-261">In this article, we'll refer to all agents, whether Linux or Windows connected to a System Center Operations Manager management group or directly to Log Analytics, as the *Log Analytics agent*.</span></span> 

<span data-ttu-id="91ada-262">The Service Map agent does not transmit any data itself, and it does not require any changes to firewalls or ports.</span><span class="sxs-lookup"><span data-stu-id="91ada-262">The Service Map agent does not transmit any data itself, and it does not require any changes to firewalls or ports.</span></span> <span data-ttu-id="91ada-263">The data in Service Map is always transmitted by the Log Analytics agent to the Log Analytics service, either directly or through the OMS Gateway.</span><span class="sxs-lookup"><span data-stu-id="91ada-263">The data in Service Map is always transmitted by the Log Analytics agent to the Log Analytics service, either directly or through the OMS Gateway.</span></span>

![Service Map agents](media/monitoring-service-map/agents.png)

<span data-ttu-id="91ada-265">If you are a System Center Operations Manager customer with a management group connected to Log Analytics:</span><span class="sxs-lookup"><span data-stu-id="91ada-265">If you are a System Center Operations Manager customer with a management group connected to Log Analytics:</span></span>

- <span data-ttu-id="91ada-266">If your System Center Operations Manager agents can access the Internet to connect to Log Analytics, no additional configuration is required.</span><span class="sxs-lookup"><span data-stu-id="91ada-266">If your System Center Operations Manager agents can access the Internet to connect to Log Analytics, no additional configuration is required.</span></span>  
- <span data-ttu-id="91ada-267">If your System Center Operations Manager agents cannot access Log Analytics over the Internet, you need to configure the OMS Gateway to work with System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="91ada-267">If your System Center Operations Manager agents cannot access Log Analytics over the Internet, you need to configure the OMS Gateway to work with System Center Operations Manager.</span></span>
  
<span data-ttu-id="91ada-268">If your Windows or Linux computers cannot directly connect to the service, you need to configure the Log Analytics agent to connect to Log Analytics using the OMS Gateway.</span><span class="sxs-lookup"><span data-stu-id="91ada-268">If your Windows or Linux computers cannot directly connect to the service, you need to configure the Log Analytics agent to connect to Log Analytics using the OMS Gateway.</span></span> <span data-ttu-id="91ada-269">For further information on how to deploy and configure the OMS Gateway, see [Connect computers without Internet access using the OMS Gateway](../log-analytics/log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="91ada-269">For further information on how to deploy and configure the OMS Gateway, see [Connect computers without Internet access using the OMS Gateway](../log-analytics/log-analytics-oms-gateway.md).</span></span>  

### <a name="management-packs"></a><span data-ttu-id="91ada-270">Management packs</span><span class="sxs-lookup"><span data-stu-id="91ada-270">Management packs</span></span>
<span data-ttu-id="91ada-271">When Service Map is activated in a Log Analytics workspace, a 300-KB management pack is forwarded to all the Windows servers in that workspace.</span><span class="sxs-lookup"><span data-stu-id="91ada-271">When Service Map is activated in a Log Analytics workspace, a 300-KB management pack is forwarded to all the Windows servers in that workspace.</span></span> <span data-ttu-id="91ada-272">If you are using System Center Operations Manager agents in a [connected management group](../log-analytics/log-analytics-om-agents.md), the Service Map management pack is deployed from System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="91ada-272">If you are using System Center Operations Manager agents in a [connected management group](../log-analytics/log-analytics-om-agents.md), the Service Map management pack is deployed from System Center Operations Manager.</span></span> 

<span data-ttu-id="91ada-273">The management pack is named Microsoft.IntelligencePacks.ApplicationDependencyMonitor.</span><span class="sxs-lookup"><span data-stu-id="91ada-273">The management pack is named Microsoft.IntelligencePacks.ApplicationDependencyMonitor.</span></span> <span data-ttu-id="91ada-274">It's written to %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs\.</span><span class="sxs-lookup"><span data-stu-id="91ada-274">It's written to %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs\.</span></span> <span data-ttu-id="91ada-275">The data source that the management pack uses is %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources\<AutoGeneratedID>\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span><span class="sxs-lookup"><span data-stu-id="91ada-275">The data source that the management pack uses is %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources\<AutoGeneratedID>\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span></span>

## <a name="data-collection"></a><span data-ttu-id="91ada-276">Data collection</span><span class="sxs-lookup"><span data-stu-id="91ada-276">Data collection</span></span>
<span data-ttu-id="91ada-277">You can expect each agent to transmit roughly 25 MB per day, depending on how complex your system dependencies are.</span><span class="sxs-lookup"><span data-stu-id="91ada-277">You can expect each agent to transmit roughly 25 MB per day, depending on how complex your system dependencies are.</span></span> <span data-ttu-id="91ada-278">Each agent sends Service Map dependency data every 15 seconds.</span><span class="sxs-lookup"><span data-stu-id="91ada-278">Each agent sends Service Map dependency data every 15 seconds.</span></span>  

<span data-ttu-id="91ada-279">The Dependency agent typically consumes 0.1 percent of system memory and 0.1 percent of system CPU.</span><span class="sxs-lookup"><span data-stu-id="91ada-279">The Dependency agent typically consumes 0.1 percent of system memory and 0.1 percent of system CPU.</span></span>

## <a name="diagnostic-and-usage-data"></a><span data-ttu-id="91ada-280">Diagnostic and usage data</span><span class="sxs-lookup"><span data-stu-id="91ada-280">Diagnostic and usage data</span></span>
<span data-ttu-id="91ada-281">Microsoft automatically collects usage and performance data through your use of the Service Map service.</span><span class="sxs-lookup"><span data-stu-id="91ada-281">Microsoft automatically collects usage and performance data through your use of the Service Map service.</span></span> <span data-ttu-id="91ada-282">Microsoft uses this data to provide and improve the quality, security, and integrity of the Service Map service.</span><span class="sxs-lookup"><span data-stu-id="91ada-282">Microsoft uses this data to provide and improve the quality, security, and integrity of the Service Map service.</span></span> <span data-ttu-id="91ada-283">Data includes information about the configuration of your software, like operating system and version.</span><span class="sxs-lookup"><span data-stu-id="91ada-283">Data includes information about the configuration of your software, like operating system and version.</span></span> <span data-ttu-id="91ada-284">It also includes IP address, DNS name, and workstation name in order to provide accurate and efficient troubleshooting capabilities.</span><span class="sxs-lookup"><span data-stu-id="91ada-284">It also includes IP address, DNS name, and workstation name in order to provide accurate and efficient troubleshooting capabilities.</span></span> <span data-ttu-id="91ada-285">We do not collect names, addresses, or other contact information.</span><span class="sxs-lookup"><span data-stu-id="91ada-285">We do not collect names, addresses, or other contact information.</span></span>

<span data-ttu-id="91ada-286">For more information on data collection and usage, see the [Microsoft Online Services Privacy Statement](https://go.microsoft.com/fwlink/?LinkId=512132).</span><span class="sxs-lookup"><span data-stu-id="91ada-286">For more information on data collection and usage, see the [Microsoft Online Services Privacy Statement](https://go.microsoft.com/fwlink/?LinkId=512132).</span></span>

## <a name="installation"></a><span data-ttu-id="91ada-287">Installation</span><span class="sxs-lookup"><span data-stu-id="91ada-287">Installation</span></span>

## <a name="azure-vm-extension"></a><span data-ttu-id="91ada-288">Azure VM Extension</span><span class="sxs-lookup"><span data-stu-id="91ada-288">Azure VM Extension</span></span>
<span data-ttu-id="91ada-289">There is an extension available for both Windows (DependencyAgentWindows) and Linux (DependencyAgentLinux), and you can easily deploy the Dependency agent to your Azure VMs using an [Azure VM Extension](https://docs.microsoft.com/azure/virtual-machines/windows/extensions-features).</span><span class="sxs-lookup"><span data-stu-id="91ada-289">There is an extension available for both Windows (DependencyAgentWindows) and Linux (DependencyAgentLinux), and you can easily deploy the Dependency agent to your Azure VMs using an [Azure VM Extension](https://docs.microsoft.com/azure/virtual-machines/windows/extensions-features).</span></span>  <span data-ttu-id="91ada-290">With the Azure VM Extension, you can deploy the Dependency agent to your Windows and Linux VMs using either a PowerShell script or directly in the VM using an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="91ada-290">With the Azure VM Extension, you can deploy the Dependency agent to your Windows and Linux VMs using either a PowerShell script or directly in the VM using an Azure Resource Manager template.</span></span>  <span data-ttu-id="91ada-291">If you deploy the agent with the Azure VM Extension, your agents are automatically updated to the latest version.</span><span class="sxs-lookup"><span data-stu-id="91ada-291">If you deploy the agent with the Azure VM Extension, your agents are automatically updated to the latest version.</span></span>

<span data-ttu-id="91ada-292">To deploy the Azure VM Extension with PowerShell, you can use the following example:</span><span class="sxs-lookup"><span data-stu-id="91ada-292">To deploy the Azure VM Extension with PowerShell, you can use the following example:</span></span>

```PowerShell
#
# Deploy the Dependency agent to every VM in a Resource Group
#

$version = "9.4"
$ExtPublisher = "Microsoft.Azure.Monitoring.DependencyAgent"
$OsExtensionMap = @{ "Windows" = "DependencyAgentWindows"; "Linux" = "DependencyAgentLinux" }
$rmgroup = "<Your Resource Group Here>"

Get-AzureRmVM -ResourceGroupName $rmgroup |
ForEach-Object {
    ""
    $name = $_.Name
    $os = $_.StorageProfile.OsDisk.OsType
    $location = $_.Location
    $vmRmGroup = $_.ResourceGroupName
    "${name}: ${os} (${location})"
    Date -Format o
    $ext = $OsExtensionMap.($os.ToString())
    $result = Set-AzureRmVMExtension -ResourceGroupName $vmRmGroup -VMName $name -Location $location `
    -Publisher $ExtPublisher -ExtensionType $ext -Name "DependencyAgent" -TypeHandlerVersion $version
    $result.IsSuccessStatusCode
}
```

<span data-ttu-id="91ada-293">An even easier way to ensure the Dependency agent is installed on your VMs is to include the agent in your Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="91ada-293">An even easier way to ensure the Dependency agent is installed on your VMs is to include the agent in your Azure Resource Manager template.</span></span>  <span data-ttu-id="91ada-294">The following JSON code example can be added to the *resources* section of your template.</span><span class="sxs-lookup"><span data-stu-id="91ada-294">The following JSON code example can be added to the *resources* section of your template.</span></span>

```JSON
"type": "Microsoft.Compute/virtualMachines/extensions",
"name": "[concat(parameters('vmName'), '/DependencyAgent')]",
"apiVersion": "2017-03-30",
"location": "[resourceGroup().location]",
"dependsOn": [
"[concat('Microsoft.Compute/virtualMachines/', parameters('vmName'))]"
],
"properties": {
    "publisher": "Microsoft.Azure.Monitoring.DependencyAgent",
    "type": "DependencyAgentWindows",
    "typeHandlerVersion": "9.4",
    "autoUpgradeMinorVersion": true
}

```

### <a name="install-the-dependency-agent-on-microsoft-windows"></a><span data-ttu-id="91ada-295">Install the Dependency agent on Microsoft Windows</span><span class="sxs-lookup"><span data-stu-id="91ada-295">Install the Dependency agent on Microsoft Windows</span></span>
<span data-ttu-id="91ada-296">The Dependency agent can be installed manually on Windows computers by running  `InstallDependencyAgent-Windows.exe`.</span><span class="sxs-lookup"><span data-stu-id="91ada-296">The Dependency agent can be installed manually on Windows computers by running  `InstallDependencyAgent-Windows.exe`.</span></span> <span data-ttu-id="91ada-297">If you run this executable file without any options, it starts a setup wizard that you can follow to install interactively.</span><span class="sxs-lookup"><span data-stu-id="91ada-297">If you run this executable file without any options, it starts a setup wizard that you can follow to install interactively.</span></span>  

>[!NOTE]
><span data-ttu-id="91ada-298">Administrator privileges are required to install or uninstall the agent.</span><span class="sxs-lookup"><span data-stu-id="91ada-298">Administrator privileges are required to install or uninstall the agent.</span></span>

<span data-ttu-id="91ada-299">Use the following steps to install the Dependency agent on each Windows computer:</span><span class="sxs-lookup"><span data-stu-id="91ada-299">Use the following steps to install the Dependency agent on each Windows computer:</span></span>

1.  <span data-ttu-id="91ada-300">Install the Log Analytics agent for Windows following one of the methods described in [Collect data in a hybrid environment with Log Analytics agent](../log-analytics/log-analytics-concept-hybrid.md).</span><span class="sxs-lookup"><span data-stu-id="91ada-300">Install the Log Analytics agent for Windows following one of the methods described in [Collect data in a hybrid environment with Log Analytics agent](../log-analytics/log-analytics-concept-hybrid.md).</span></span>
2.  <span data-ttu-id="91ada-301">Download the Windows agent and run it by using the following command:</span><span class="sxs-lookup"><span data-stu-id="91ada-301">Download the Windows agent and run it by using the following command:</span></span> 
    
    `InstallDependencyAgent-Windows.exe`

3.  <span data-ttu-id="91ada-302">Follow the setup wizard to install the agent.</span><span class="sxs-lookup"><span data-stu-id="91ada-302">Follow the setup wizard to install the agent.</span></span>
4.  <span data-ttu-id="91ada-303">If the Dependency agent fails to start, check the logs for detailed error information.</span><span class="sxs-lookup"><span data-stu-id="91ada-303">If the Dependency agent fails to start, check the logs for detailed error information.</span></span> <span data-ttu-id="91ada-304">On Windows agents, the log directory is %Programfiles%\Microsoft Dependency Agent\logs.</span><span class="sxs-lookup"><span data-stu-id="91ada-304">On Windows agents, the log directory is %Programfiles%\Microsoft Dependency Agent\logs.</span></span> 

#### <a name="windows-command-line"></a><span data-ttu-id="91ada-305">Windows command line</span><span class="sxs-lookup"><span data-stu-id="91ada-305">Windows command line</span></span>
<span data-ttu-id="91ada-306">Use options from the following table to install from a command line.</span><span class="sxs-lookup"><span data-stu-id="91ada-306">Use options from the following table to install from a command line.</span></span> <span data-ttu-id="91ada-307">To see a list of the installation flags, run the installer by using the /?</span><span class="sxs-lookup"><span data-stu-id="91ada-307">To see a list of the installation flags, run the installer by using the /?</span></span> <span data-ttu-id="91ada-308">flag as follows.</span><span class="sxs-lookup"><span data-stu-id="91ada-308">flag as follows.</span></span>

    InstallDependencyAgent-Windows.exe /?

| <span data-ttu-id="91ada-309">Flag</span><span class="sxs-lookup"><span data-stu-id="91ada-309">Flag</span></span> | <span data-ttu-id="91ada-310">Description</span><span class="sxs-lookup"><span data-stu-id="91ada-310">Description</span></span> |
|:--|:--|
| <span data-ttu-id="91ada-311">/?</span><span class="sxs-lookup"><span data-stu-id="91ada-311">/?</span></span> | <span data-ttu-id="91ada-312">Get a list of the command-line options.</span><span class="sxs-lookup"><span data-stu-id="91ada-312">Get a list of the command-line options.</span></span> |
| <span data-ttu-id="91ada-313">/S</span><span class="sxs-lookup"><span data-stu-id="91ada-313">/S</span></span> | <span data-ttu-id="91ada-314">Perform a silent installation with no user prompts.</span><span class="sxs-lookup"><span data-stu-id="91ada-314">Perform a silent installation with no user prompts.</span></span> |

<span data-ttu-id="91ada-315">Files for the Windows Dependency agent are placed in C:\Program Files\Microsoft Dependency Agent by default.</span><span class="sxs-lookup"><span data-stu-id="91ada-315">Files for the Windows Dependency agent are placed in C:\Program Files\Microsoft Dependency Agent by default.</span></span>

### <a name="install-the-dependency-agent-on-linux"></a><span data-ttu-id="91ada-316">Install the Dependency agent on Linux</span><span class="sxs-lookup"><span data-stu-id="91ada-316">Install the Dependency agent on Linux</span></span>
<span data-ttu-id="91ada-317">The Dependency agent is installed on Linux computers from `InstallDependencyAgent-Linux64.bin`, a shell script with a self-extracting binary.</span><span class="sxs-lookup"><span data-stu-id="91ada-317">The Dependency agent is installed on Linux computers from `InstallDependencyAgent-Linux64.bin`, a shell script with a self-extracting binary.</span></span> <span data-ttu-id="91ada-318">You can run the file by using `sh` or add execute permissions to the file itself.</span><span class="sxs-lookup"><span data-stu-id="91ada-318">You can run the file by using `sh` or add execute permissions to the file itself.</span></span>

>[!NOTE]
> <span data-ttu-id="91ada-319">Root access is required to install or configure the agent.</span><span class="sxs-lookup"><span data-stu-id="91ada-319">Root access is required to install or configure the agent.</span></span>

<span data-ttu-id="91ada-320">Use the following steps to install the Dependency agent on each Linux computer:</span><span class="sxs-lookup"><span data-stu-id="91ada-320">Use the following steps to install the Dependency agent on each Linux computer:</span></span>

1.  <span data-ttu-id="91ada-321">Install the Log Analytics agent following one of the methods described in [Collect data in a hybrid environment with Log Analytics agent](../log-analytics/log-analytics-concept-hybrid.md).</span><span class="sxs-lookup"><span data-stu-id="91ada-321">Install the Log Analytics agent following one of the methods described in [Collect data in a hybrid environment with Log Analytics agent](../log-analytics/log-analytics-concept-hybrid.md).</span></span>
2.  <span data-ttu-id="91ada-322">Install the Linux Dependency agent as root by running the following command:</span><span class="sxs-lookup"><span data-stu-id="91ada-322">Install the Linux Dependency agent as root by running the following command:</span></span>
    
    `sh InstallDependencyAgent-Linux64.bin`

3.  <span data-ttu-id="91ada-323">If the Dependency agent fails to start, check the logs for detailed error information.</span><span class="sxs-lookup"><span data-stu-id="91ada-323">If the Dependency agent fails to start, check the logs for detailed error information.</span></span> <span data-ttu-id="91ada-324">On Linux agents, the log directory is /var/opt/microsoft/dependency-agent/log.</span><span class="sxs-lookup"><span data-stu-id="91ada-324">On Linux agents, the log directory is /var/opt/microsoft/dependency-agent/log.</span></span>

<span data-ttu-id="91ada-325">To see a list of the installation flags, run the installation program with the -help flag as follows.</span><span class="sxs-lookup"><span data-stu-id="91ada-325">To see a list of the installation flags, run the installation program with the -help flag as follows.</span></span>

    InstallDependencyAgent-Linux64.bin -help

| <span data-ttu-id="91ada-326">Flag</span><span class="sxs-lookup"><span data-stu-id="91ada-326">Flag</span></span> | <span data-ttu-id="91ada-327">Description</span><span class="sxs-lookup"><span data-stu-id="91ada-327">Description</span></span> |
|:--|:--|
| <span data-ttu-id="91ada-328">-help</span><span class="sxs-lookup"><span data-stu-id="91ada-328">-help</span></span> | <span data-ttu-id="91ada-329">Get a list of the command-line options.</span><span class="sxs-lookup"><span data-stu-id="91ada-329">Get a list of the command-line options.</span></span> |
| <span data-ttu-id="91ada-330">-s</span><span class="sxs-lookup"><span data-stu-id="91ada-330">-s</span></span> | <span data-ttu-id="91ada-331">Perform a silent installation with no user prompts.</span><span class="sxs-lookup"><span data-stu-id="91ada-331">Perform a silent installation with no user prompts.</span></span> |
| <span data-ttu-id="91ada-332">--check</span><span class="sxs-lookup"><span data-stu-id="91ada-332">--check</span></span> | <span data-ttu-id="91ada-333">Check permissions and the operating system but do not install the agent.</span><span class="sxs-lookup"><span data-stu-id="91ada-333">Check permissions and the operating system but do not install the agent.</span></span> |

<span data-ttu-id="91ada-334">Files for the Dependency agent are placed in the following directories:</span><span class="sxs-lookup"><span data-stu-id="91ada-334">Files for the Dependency agent are placed in the following directories:</span></span>

| <span data-ttu-id="91ada-335">Files</span><span class="sxs-lookup"><span data-stu-id="91ada-335">Files</span></span> | <span data-ttu-id="91ada-336">Location</span><span class="sxs-lookup"><span data-stu-id="91ada-336">Location</span></span> |
|:--|:--|
| <span data-ttu-id="91ada-337">Core files</span><span class="sxs-lookup"><span data-stu-id="91ada-337">Core files</span></span> | <span data-ttu-id="91ada-338">/opt/microsoft/dependency-agent</span><span class="sxs-lookup"><span data-stu-id="91ada-338">/opt/microsoft/dependency-agent</span></span> |
| <span data-ttu-id="91ada-339">Log files</span><span class="sxs-lookup"><span data-stu-id="91ada-339">Log files</span></span> | <span data-ttu-id="91ada-340">/var/opt/microsoft/dependency-agent/log</span><span class="sxs-lookup"><span data-stu-id="91ada-340">/var/opt/microsoft/dependency-agent/log</span></span> |
| <span data-ttu-id="91ada-341">Config files</span><span class="sxs-lookup"><span data-stu-id="91ada-341">Config files</span></span> | <span data-ttu-id="91ada-342">/etc/opt/microsoft/dependency-agent/config</span><span class="sxs-lookup"><span data-stu-id="91ada-342">/etc/opt/microsoft/dependency-agent/config</span></span> |
| <span data-ttu-id="91ada-343">Service executable files</span><span class="sxs-lookup"><span data-stu-id="91ada-343">Service executable files</span></span> | <span data-ttu-id="91ada-344">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span><span class="sxs-lookup"><span data-stu-id="91ada-344">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span></span><br><span data-ttu-id="91ada-345">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span><span class="sxs-lookup"><span data-stu-id="91ada-345">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span></span> |
| <span data-ttu-id="91ada-346">Binary storage files</span><span class="sxs-lookup"><span data-stu-id="91ada-346">Binary storage files</span></span> | <span data-ttu-id="91ada-347">/var/opt/microsoft/dependency-agent/storage</span><span class="sxs-lookup"><span data-stu-id="91ada-347">/var/opt/microsoft/dependency-agent/storage</span></span> |

## <a name="installation-script-examples"></a><span data-ttu-id="91ada-348">Installation script examples</span><span class="sxs-lookup"><span data-stu-id="91ada-348">Installation script examples</span></span>
<span data-ttu-id="91ada-349">To easily deploy the Dependency agent on many servers at once, the following script example is provided to download and install the Dependency agent on either Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="91ada-349">To easily deploy the Dependency agent on many servers at once, the following script example is provided to download and install the Dependency agent on either Windows or Linux.</span></span>

### <a name="powershell-script-for-windows"></a><span data-ttu-id="91ada-350">PowerShell script for Windows</span><span class="sxs-lookup"><span data-stu-id="91ada-350">PowerShell script for Windows</span></span>
```PowerShell
Invoke-WebRequest "https://aka.ms/dependencyagentwindows" -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S
```

### <a name="shell-script-for-linux"></a><span data-ttu-id="91ada-351">Shell script for Linux</span><span class="sxs-lookup"><span data-stu-id="91ada-351">Shell script for Linux</span></span>
```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
sudo sh InstallDependencyAgent-Linux64.bin -s
```
## <a name="desired-state-configuration"></a><span data-ttu-id="91ada-352">Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="91ada-352">Desired State Configuration</span></span>
<span data-ttu-id="91ada-353">To deploy the Dependency agent using Desired State Configuration (DSC), you can use the xPSDesiredStateConfiguration module with the following example code:</span><span class="sxs-lookup"><span data-stu-id="91ada-353">To deploy the Dependency agent using Desired State Configuration (DSC), you can use the xPSDesiredStateConfiguration module with the following example code:</span></span>

```
configuration ServiceMap {

Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = "C:\InstallDependencyAgent-Windows.exe"

Node localhost
{ 
    # Download and install the Dependency agent
    xRemoteFile DAPackage 
    {
        Uri = "https://aka.ms/dependencyagentwindows"
        DestinationPath = $DAPackageLocalPath
    }

    xPackage DA
    {
        Ensure="Present"
        Name = "Dependency Agent"
        Path = $DAPackageLocalPath
        Arguments = '/S'
        ProductId = ""
        InstalledCheckRegKey = "HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent"
        InstalledCheckRegValueName = "DisplayName"
        InstalledCheckRegValueData = "Dependency Agent"
        DependsOn = "[xRemoteFile]DAPackage"
    }
  }
}
```

## <a name="remove-the-dependency-agent"></a><span data-ttu-id="91ada-354">Remove the Dependency agent</span><span class="sxs-lookup"><span data-stu-id="91ada-354">Remove the Dependency agent</span></span>
### <a name="uinstall-agent-on-windows"></a><span data-ttu-id="91ada-355">Uinstall agent on Windows</span><span class="sxs-lookup"><span data-stu-id="91ada-355">Uinstall agent on Windows</span></span>
<span data-ttu-id="91ada-356">An administrator can uninstall the Dependency agent for Windows through Control Panel.</span><span class="sxs-lookup"><span data-stu-id="91ada-356">An administrator can uninstall the Dependency agent for Windows through Control Panel.</span></span>

<span data-ttu-id="91ada-357">An administrator can also run %Programfiles%\Microsoft Dependency Agent\Uninstall.exe to uninstall the Dependency agent.</span><span class="sxs-lookup"><span data-stu-id="91ada-357">An administrator can also run %Programfiles%\Microsoft Dependency Agent\Uninstall.exe to uninstall the Dependency agent.</span></span>

### <a name="uninstall-agent-on-linux"></a><span data-ttu-id="91ada-358">Uninstall agent on Linux</span><span class="sxs-lookup"><span data-stu-id="91ada-358">Uninstall agent on Linux</span></span>
<span data-ttu-id="91ada-359">You can uninstall the Dependency agent from Linux with the following command.</span><span class="sxs-lookup"><span data-stu-id="91ada-359">You can uninstall the Dependency agent from Linux with the following command.</span></span>

<span data-ttu-id="91ada-360">RHEL, CentOs, or Oracle:</span><span class="sxs-lookup"><span data-stu-id="91ada-360">RHEL, CentOs, or Oracle:</span></span>

```
sudo rpm -e dependency-agent
```

<span data-ttu-id="91ada-361">Ubuntu:</span><span class="sxs-lookup"><span data-stu-id="91ada-361">Ubuntu:</span></span>

```
sudo apt -y purge dependency-agent
```

## <a name="troubleshooting"></a><span data-ttu-id="91ada-362">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="91ada-362">Troubleshooting</span></span>
<span data-ttu-id="91ada-363">If you have any problems installing or running Service Map, this section can help you.</span><span class="sxs-lookup"><span data-stu-id="91ada-363">If you have any problems installing or running Service Map, this section can help you.</span></span> <span data-ttu-id="91ada-364">If you still can't resolve your problem, please contact Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="91ada-364">If you still can't resolve your problem, please contact Microsoft Support.</span></span>

### <a name="dependency-agent-installation-problems"></a><span data-ttu-id="91ada-365">Dependency agent installation problems</span><span class="sxs-lookup"><span data-stu-id="91ada-365">Dependency agent installation problems</span></span>
#### <a name="installer-prompts-for-a-reboot"></a><span data-ttu-id="91ada-366">Installer prompts for a reboot</span><span class="sxs-lookup"><span data-stu-id="91ada-366">Installer prompts for a reboot</span></span>
<span data-ttu-id="91ada-367">The Dependency agent *generally* does not require a reboot upon installation or uninstallation.</span><span class="sxs-lookup"><span data-stu-id="91ada-367">The Dependency agent *generally* does not require a reboot upon installation or uninstallation.</span></span> <span data-ttu-id="91ada-368">However, in certain rare cases, Windows Server requires a reboot to continue with an installation.</span><span class="sxs-lookup"><span data-stu-id="91ada-368">However, in certain rare cases, Windows Server requires a reboot to continue with an installation.</span></span> <span data-ttu-id="91ada-369">This happens when a dependency, usually the Microsoft Visual C++ Redistributable, requires a reboot because of a locked file.</span><span class="sxs-lookup"><span data-stu-id="91ada-369">This happens when a dependency, usually the Microsoft Visual C++ Redistributable, requires a reboot because of a locked file.</span></span>

#### <a name="message-unable-to-install-dependency-agent-visual-studio-runtime-libraries-failed-to-install-code--codenumber-appears"></a><span data-ttu-id="91ada-370">Message "Unable to install Dependency agent: Visual Studio Runtime libraries failed to install (code = [code_number])" appears</span><span class="sxs-lookup"><span data-stu-id="91ada-370">Message "Unable to install Dependency agent: Visual Studio Runtime libraries failed to install (code = [code_number])" appears</span></span>

<span data-ttu-id="91ada-371">The Microsoft Dependency agent is built on the Microsoft Visual Studio runtime libraries.</span><span class="sxs-lookup"><span data-stu-id="91ada-371">The Microsoft Dependency agent is built on the Microsoft Visual Studio runtime libraries.</span></span> <span data-ttu-id="91ada-372">You'll get a message if there's a problem during installation of the libraries.</span><span class="sxs-lookup"><span data-stu-id="91ada-372">You'll get a message if there's a problem during installation of the libraries.</span></span> 

<span data-ttu-id="91ada-373">The runtime library installers create logs in the %LOCALAPPDATA%\temp folder.</span><span class="sxs-lookup"><span data-stu-id="91ada-373">The runtime library installers create logs in the %LOCALAPPDATA%\temp folder.</span></span> <span data-ttu-id="91ada-374">The file is dd_vcredist_arch_yyyymmddhhmmss.log, where *arch* is "x86" or "amd64" and *yyyymmddhhmmss* is the date and time (24-hour clock) when the log was created.</span><span class="sxs-lookup"><span data-stu-id="91ada-374">The file is dd_vcredist_arch_yyyymmddhhmmss.log, where *arch* is "x86" or "amd64" and *yyyymmddhhmmss* is the date and time (24-hour clock) when the log was created.</span></span> <span data-ttu-id="91ada-375">The log provides details about the problem that's blocking installation.</span><span class="sxs-lookup"><span data-stu-id="91ada-375">The log provides details about the problem that's blocking installation.</span></span>

<span data-ttu-id="91ada-376">It might be useful to install the [latest runtime libraries](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) yourself first.</span><span class="sxs-lookup"><span data-stu-id="91ada-376">It might be useful to install the [latest runtime libraries](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) yourself first.</span></span>

<span data-ttu-id="91ada-377">The following table lists code numbers and suggested resolutions.</span><span class="sxs-lookup"><span data-stu-id="91ada-377">The following table lists code numbers and suggested resolutions.</span></span>

| <span data-ttu-id="91ada-378">Code</span><span class="sxs-lookup"><span data-stu-id="91ada-378">Code</span></span> | <span data-ttu-id="91ada-379">Description</span><span class="sxs-lookup"><span data-stu-id="91ada-379">Description</span></span> | <span data-ttu-id="91ada-380">Resolution</span><span class="sxs-lookup"><span data-stu-id="91ada-380">Resolution</span></span> |
|:--|:--|:--|
| <span data-ttu-id="91ada-381">0x17</span><span class="sxs-lookup"><span data-stu-id="91ada-381">0x17</span></span> | <span data-ttu-id="91ada-382">The library installer requires a Windows update that hasn't been installed.</span><span class="sxs-lookup"><span data-stu-id="91ada-382">The library installer requires a Windows update that hasn't been installed.</span></span> | <span data-ttu-id="91ada-383">Look in the most recent library installer log.</span><span class="sxs-lookup"><span data-stu-id="91ada-383">Look in the most recent library installer log.</span></span><br><br><span data-ttu-id="91ada-384">If a reference to "Windows8.1-KB2999226-x64.msu" is followed by a line "Error 0x80240017: Failed to execute MSU package," you don't have the prerequisites to install KB2999226.</span><span class="sxs-lookup"><span data-stu-id="91ada-384">If a reference to "Windows8.1-KB2999226-x64.msu" is followed by a line "Error 0x80240017: Failed to execute MSU package," you don't have the prerequisites to install KB2999226.</span></span> <span data-ttu-id="91ada-385">Follow the instructions in the prerequisites section in [Universal C Runtime in Windows](https://support.microsoft.com/kb/2999226).</span><span class="sxs-lookup"><span data-stu-id="91ada-385">Follow the instructions in the prerequisites section in [Universal C Runtime in Windows](https://support.microsoft.com/kb/2999226).</span></span> <span data-ttu-id="91ada-386">You might need to run Windows Update and reboot multiple times in order to install the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="91ada-386">You might need to run Windows Update and reboot multiple times in order to install the prerequisites.</span></span><br><br><span data-ttu-id="91ada-387">Run the Microsoft Dependency agent installer again.</span><span class="sxs-lookup"><span data-stu-id="91ada-387">Run the Microsoft Dependency agent installer again.</span></span> |

### <a name="post-installation-issues"></a><span data-ttu-id="91ada-388">Post-installation issues</span><span class="sxs-lookup"><span data-stu-id="91ada-388">Post-installation issues</span></span>
#### <a name="server-doesnt-appear-in-service-map"></a><span data-ttu-id="91ada-389">Server doesn't appear in Service Map</span><span class="sxs-lookup"><span data-stu-id="91ada-389">Server doesn't appear in Service Map</span></span>
<span data-ttu-id="91ada-390">If your Dependency agent installation succeeded, but you don't see your server in the Service Map solution:</span><span class="sxs-lookup"><span data-stu-id="91ada-390">If your Dependency agent installation succeeded, but you don't see your server in the Service Map solution:</span></span>
* <span data-ttu-id="91ada-391">Is the Dependency agent installed successfully?</span><span class="sxs-lookup"><span data-stu-id="91ada-391">Is the Dependency agent installed successfully?</span></span> <span data-ttu-id="91ada-392">You can validate this by checking to see if the service is installed and running.</span><span class="sxs-lookup"><span data-stu-id="91ada-392">You can validate this by checking to see if the service is installed and running.</span></span><br><br>
<span data-ttu-id="91ada-393">**Windows**: Look for the service named "Microsoft Dependency agent."</span><span class="sxs-lookup"><span data-stu-id="91ada-393">**Windows**: Look for the service named "Microsoft Dependency agent."</span></span><br>
<span data-ttu-id="91ada-394">**Linux**: Look for the running process "microsoft-dependency-agent."</span><span class="sxs-lookup"><span data-stu-id="91ada-394">**Linux**: Look for the running process "microsoft-dependency-agent."</span></span>

* <span data-ttu-id="91ada-395">Are you on the [Free pricing tier of Operations Management Suite/Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)?</span><span class="sxs-lookup"><span data-stu-id="91ada-395">Are you on the [Free pricing tier of Operations Management Suite/Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)?</span></span> <span data-ttu-id="91ada-396">The Free plan allows for up to five unique Service Map servers.</span><span class="sxs-lookup"><span data-stu-id="91ada-396">The Free plan allows for up to five unique Service Map servers.</span></span> <span data-ttu-id="91ada-397">Any subsequent servers won't show up in Service Map, even if the prior five are no longer sending data.</span><span class="sxs-lookup"><span data-stu-id="91ada-397">Any subsequent servers won't show up in Service Map, even if the prior five are no longer sending data.</span></span>

* <span data-ttu-id="91ada-398">Is your server sending log and perf data to Log Analytics?</span><span class="sxs-lookup"><span data-stu-id="91ada-398">Is your server sending log and perf data to Log Analytics?</span></span> <span data-ttu-id="91ada-399">Go to Log Search and run the following query for your computer:</span><span class="sxs-lookup"><span data-stu-id="91ada-399">Go to Log Search and run the following query for your computer:</span></span> 

        Usage | where Computer == "admdemo-appsvr" | summarize sum(Quantity), any(QuantityUnit) by DataType

<span data-ttu-id="91ada-400">Did you get a variety of events in the results?</span><span class="sxs-lookup"><span data-stu-id="91ada-400">Did you get a variety of events in the results?</span></span> <span data-ttu-id="91ada-401">Is the data recent?</span><span class="sxs-lookup"><span data-stu-id="91ada-401">Is the data recent?</span></span> <span data-ttu-id="91ada-402">If so, your Log Analytics Agent is operating correctly and communicating with Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="91ada-402">If so, your Log Analytics Agent is operating correctly and communicating with Log Analytics.</span></span> <span data-ttu-id="91ada-403">If not, check the agent on your server: [Log Analytics agent for Windows troubleshooting](https://support.microsoft.com/help/3126513/how-to-troubleshoot-monitoring-onboarding-issues) or [Log Analytics agent for Linux troubleshooting](../log-analytics/log-analytics-agent-linux-support.md).</span><span class="sxs-lookup"><span data-stu-id="91ada-403">If not, check the agent on your server: [Log Analytics agent for Windows troubleshooting](https://support.microsoft.com/help/3126513/how-to-troubleshoot-monitoring-onboarding-issues) or [Log Analytics agent for Linux troubleshooting](../log-analytics/log-analytics-agent-linux-support.md).</span></span>

#### <a name="server-appears-in-service-map-but-has-no-processes"></a><span data-ttu-id="91ada-404">Server appears in Service Map but has no processes</span><span class="sxs-lookup"><span data-stu-id="91ada-404">Server appears in Service Map but has no processes</span></span>
<span data-ttu-id="91ada-405">If you see your server in Service Map, but it has no process or connection data, that indicates that the Dependency agent is installed and running, but the kernel driver didn't load.</span><span class="sxs-lookup"><span data-stu-id="91ada-405">If you see your server in Service Map, but it has no process or connection data, that indicates that the Dependency agent is installed and running, but the kernel driver didn't load.</span></span> 

<span data-ttu-id="91ada-406">Check the C:\Program Files\Microsoft Dependency Agent\logs\wrapper.log file (Windows) or /var/opt/microsoft/dependency-agent/log/service.log file (Linux).</span><span class="sxs-lookup"><span data-stu-id="91ada-406">Check the C:\Program Files\Microsoft Dependency Agent\logs\wrapper.log file (Windows) or /var/opt/microsoft/dependency-agent/log/service.log file (Linux).</span></span> <span data-ttu-id="91ada-407">The last lines of the file should indicate why the kernel didn't load.</span><span class="sxs-lookup"><span data-stu-id="91ada-407">The last lines of the file should indicate why the kernel didn't load.</span></span> <span data-ttu-id="91ada-408">For example, the kernel might not be supported on Linux if you updated your kernel.</span><span class="sxs-lookup"><span data-stu-id="91ada-408">For example, the kernel might not be supported on Linux if you updated your kernel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="91ada-409">Next steps</span><span class="sxs-lookup"><span data-stu-id="91ada-409">Next steps</span></span>
- <span data-ttu-id="91ada-410">Learn how to [use Service Map]( monitoring-service-map.md) after it has been deployed and configured.</span><span class="sxs-lookup"><span data-stu-id="91ada-410">Learn how to [use Service Map]( monitoring-service-map.md) after it has been deployed and configured.</span></span>
