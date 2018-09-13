---
title: Azure Stack telemetry | Microsoft Docs
description: Describes how to configure Azure Stack telemetry settings using PowerShell.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/07/2018
ms.author: jeffgilb
ms.reviewer: comartin
ms.openlocfilehash: ed3f09f942bdaa803ae8024d5c02230173190107
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867308"
---
# <a name="azure-stack-telemetry"></a><span data-ttu-id="22da0-103">Azure Stack telemetry</span><span class="sxs-lookup"><span data-stu-id="22da0-103">Azure Stack telemetry</span></span>

<span data-ttu-id="22da0-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="22da0-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="22da0-105">Azure Stack telemetry automatically uploads system data to Microsoft via the Connected User Experience.</span><span class="sxs-lookup"><span data-stu-id="22da0-105">Azure Stack telemetry automatically uploads system data to Microsoft via the Connected User Experience.</span></span> <span data-ttu-id="22da0-106">Microsoft teams use the data that Azure Stack telemetry gathers to improve customer experiences.</span><span class="sxs-lookup"><span data-stu-id="22da0-106">Microsoft teams use the data that Azure Stack telemetry gathers to improve customer experiences.</span></span> <span data-ttu-id="22da0-107">This data is also used for security, health, quality, and performance analysis.</span><span class="sxs-lookup"><span data-stu-id="22da0-107">This data is also used for security, health, quality, and performance analysis.</span></span>

<span data-ttu-id="22da0-108">For an Azure Stack operator, telemetry can provide valuable insights into enterprise deployments and gives you a voice that helps shape future versions of Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="22da0-108">For an Azure Stack operator, telemetry can provide valuable insights into enterprise deployments and gives you a voice that helps shape future versions of Azure Stack.</span></span>

> [!NOTE]
> <span data-ttu-id="22da0-109">You can also configure Azure Stack to forward usage information to Azure for billing.</span><span class="sxs-lookup"><span data-stu-id="22da0-109">You can also configure Azure Stack to forward usage information to Azure for billing.</span></span> <span data-ttu-id="22da0-110">This is required for Multi-Node Azure Stack customers who choose pay-as-you-use billing.</span><span class="sxs-lookup"><span data-stu-id="22da0-110">This is required for Multi-Node Azure Stack customers who choose pay-as-you-use billing.</span></span> <span data-ttu-id="22da0-111">Usage reporting is controlled independently from telemetry and is not required for Multi-Node customers who choose the capacity model or for Azure Stack Development Kit users.</span><span class="sxs-lookup"><span data-stu-id="22da0-111">Usage reporting is controlled independently from telemetry and is not required for Multi-Node customers who choose the capacity model or for Azure Stack Development Kit users.</span></span> <span data-ttu-id="22da0-112">For these scenarios, usage reporting can be turned off [using the registration script](https://docs.microsoft.com/azure/azure-stack/azure-stack-usage-reporting).</span><span class="sxs-lookup"><span data-stu-id="22da0-112">For these scenarios, usage reporting can be turned off [using the registration script](https://docs.microsoft.com/azure/azure-stack/azure-stack-usage-reporting).</span></span>

<span data-ttu-id="22da0-113">Azure Stack telemetry is based on the Windows Server 2016 Connected User Experience and Telemetry component, which uses the [Event Tracing for Windows (ETW)](https://msdn.microsoft.com/library/dn904632(v=vs.85).aspx) TraceLogging technology to gather and store events and data.</span><span class="sxs-lookup"><span data-stu-id="22da0-113">Azure Stack telemetry is based on the Windows Server 2016 Connected User Experience and Telemetry component, which uses the [Event Tracing for Windows (ETW)](https://msdn.microsoft.com/library/dn904632(v=vs.85).aspx) TraceLogging technology to gather and store events and data.</span></span> <span data-ttu-id="22da0-114">Azure Stack components use the same technology to publish events and data gathered by using public operating system event logging and tracing APIs.</span><span class="sxs-lookup"><span data-stu-id="22da0-114">Azure Stack components use the same technology to publish events and data gathered by using public operating system event logging and tracing APIs.</span></span> <span data-ttu-id="22da0-115">Examples of these Azure Stack components include these providers: Network Resource, Storage Resource, Monitoring Resource, and Update Resource.</span><span class="sxs-lookup"><span data-stu-id="22da0-115">Examples of these Azure Stack components include these providers: Network Resource, Storage Resource, Monitoring Resource, and Update Resource.</span></span> <span data-ttu-id="22da0-116">The Connected User Experience and Telemetry component encrypts data using SSL and uses certificate pinning to transmit data over HTTPS to the Microsoft Data Management service.</span><span class="sxs-lookup"><span data-stu-id="22da0-116">The Connected User Experience and Telemetry component encrypts data using SSL and uses certificate pinning to transmit data over HTTPS to the Microsoft Data Management service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="22da0-117">To enable telemetry data flow, port 443 (HTTPS) must be open in your network.</span><span class="sxs-lookup"><span data-stu-id="22da0-117">To enable telemetry data flow, port 443 (HTTPS) must be open in your network.</span></span> <span data-ttu-id="22da0-118">The Connected User Experience and Telemetry component connects to the Microsoft Data Management service at https://v10.vortex-win.data.microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="22da0-118">The Connected User Experience and Telemetry component connects to the Microsoft Data Management service at https://v10.vortex-win.data.microsoft.com.</span></span> <span data-ttu-id="22da0-119">The Connected User Experience and Telemetry component also connects to https://settings-win.data.microsoft.com to download configuration information.</span><span class="sxs-lookup"><span data-stu-id="22da0-119">The Connected User Experience and Telemetry component also connects to https://settings-win.data.microsoft.com to download configuration information.</span></span>

## <a name="privacy-considerations"></a><span data-ttu-id="22da0-120">Privacy considerations</span><span class="sxs-lookup"><span data-stu-id="22da0-120">Privacy considerations</span></span>

<span data-ttu-id="22da0-121">The ETW service routes telemetry data back to protected cloud storage.</span><span class="sxs-lookup"><span data-stu-id="22da0-121">The ETW service routes telemetry data back to protected cloud storage.</span></span> <span data-ttu-id="22da0-122">The principle of least privilege guides access to telemetry data.</span><span class="sxs-lookup"><span data-stu-id="22da0-122">The principle of least privilege guides access to telemetry data.</span></span> <span data-ttu-id="22da0-123">Only Microsoft personnel with a valid business need are given access to the telemetry data.</span><span class="sxs-lookup"><span data-stu-id="22da0-123">Only Microsoft personnel with a valid business need are given access to the telemetry data.</span></span> <span data-ttu-id="22da0-124">Microsoft doesn't share personal customer data with third parties, except at the customer’s discretion or for the limited purposes described in the [Microsoft Privacy Statement](https://privacy.microsoft.com/PrivacyStatement).</span><span class="sxs-lookup"><span data-stu-id="22da0-124">Microsoft doesn't share personal customer data with third parties, except at the customer’s discretion or for the limited purposes described in the [Microsoft Privacy Statement](https://privacy.microsoft.com/PrivacyStatement).</span></span> <span data-ttu-id="22da0-125">Business reports that are shared with OEMs and partners include aggregated, anonymized data.</span><span class="sxs-lookup"><span data-stu-id="22da0-125">Business reports that are shared with OEMs and partners include aggregated, anonymized data.</span></span> <span data-ttu-id="22da0-126">Data sharing decisions are made by an internal Microsoft team including privacy, legal, and data management stakeholders.</span><span class="sxs-lookup"><span data-stu-id="22da0-126">Data sharing decisions are made by an internal Microsoft team including privacy, legal, and data management stakeholders.</span></span>

<span data-ttu-id="22da0-127">Microsoft believes in, and practices information minimization.</span><span class="sxs-lookup"><span data-stu-id="22da0-127">Microsoft believes in, and practices information minimization.</span></span> <span data-ttu-id="22da0-128">We strive to gather only the information that's needed, and store it for only as long as necessary to provide a service or for analysis.</span><span class="sxs-lookup"><span data-stu-id="22da0-128">We strive to gather only the information that's needed, and store it for only as long as necessary to provide a service or for analysis.</span></span> <span data-ttu-id="22da0-129">Much of the information about how the Azure Stack system and Azure services are functioning is deleted within six months.</span><span class="sxs-lookup"><span data-stu-id="22da0-129">Much of the information about how the Azure Stack system and Azure services are functioning is deleted within six months.</span></span> <span data-ttu-id="22da0-130">Summarized or aggregated data will be kept for a longer period.</span><span class="sxs-lookup"><span data-stu-id="22da0-130">Summarized or aggregated data will be kept for a longer period.</span></span>

<span data-ttu-id="22da0-131">We understand that the privacy and security of customer information is important.</span><span class="sxs-lookup"><span data-stu-id="22da0-131">We understand that the privacy and security of customer information is important.</span></span>  <span data-ttu-id="22da0-132">Microsoft takes a thoughtful and comprehensive approach to customer privacy and the protection of customer data in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="22da0-132">Microsoft takes a thoughtful and comprehensive approach to customer privacy and the protection of customer data in Azure Stack.</span></span> <span data-ttu-id="22da0-133">IT administrators have controls to customize features and privacy settings at any time.</span><span class="sxs-lookup"><span data-stu-id="22da0-133">IT administrators have controls to customize features and privacy settings at any time.</span></span> <span data-ttu-id="22da0-134">Our commitment to transparency and trust is clear:</span><span class="sxs-lookup"><span data-stu-id="22da0-134">Our commitment to transparency and trust is clear:</span></span>

- <span data-ttu-id="22da0-135">We're open with customers about the types of data we gather.</span><span class="sxs-lookup"><span data-stu-id="22da0-135">We're open with customers about the types of data we gather.</span></span>
- <span data-ttu-id="22da0-136">We put enterprise customers in control — they can customize their own privacy settings.</span><span class="sxs-lookup"><span data-stu-id="22da0-136">We put enterprise customers in control — they can customize their own privacy settings.</span></span>
- <span data-ttu-id="22da0-137">We put customer privacy and security first.</span><span class="sxs-lookup"><span data-stu-id="22da0-137">We put customer privacy and security first.</span></span>
- <span data-ttu-id="22da0-138">We're transparent about how telemetry data gets used.</span><span class="sxs-lookup"><span data-stu-id="22da0-138">We're transparent about how telemetry data gets used.</span></span>
- <span data-ttu-id="22da0-139">We use telemetry data to improve customer experiences.</span><span class="sxs-lookup"><span data-stu-id="22da0-139">We use telemetry data to improve customer experiences.</span></span>

<span data-ttu-id="22da0-140">Microsoft doesn't intend to gather sensitive data, such as credit card numbers, usernames and passwords, email addresses, or similar sensitive information.</span><span class="sxs-lookup"><span data-stu-id="22da0-140">Microsoft doesn't intend to gather sensitive data, such as credit card numbers, usernames and passwords, email addresses, or similar sensitive information.</span></span> <span data-ttu-id="22da0-141">If we determine that sensitive information has been inadvertently received, we delete it.</span><span class="sxs-lookup"><span data-stu-id="22da0-141">If we determine that sensitive information has been inadvertently received, we delete it.</span></span>

## <a name="examples-of-how-microsoft-uses-the-telemetry-data"></a><span data-ttu-id="22da0-142">Examples of how Microsoft uses the telemetry data</span><span class="sxs-lookup"><span data-stu-id="22da0-142">Examples of how Microsoft uses the telemetry data</span></span>

<span data-ttu-id="22da0-143">Telemetry plays an important role in helping to quickly identify and fix critical reliability issues in customer deployments and configurations.</span><span class="sxs-lookup"><span data-stu-id="22da0-143">Telemetry plays an important role in helping to quickly identify and fix critical reliability issues in customer deployments and configurations.</span></span> <span data-ttu-id="22da0-144">Insights from telemetry data can help identify issues with services or hardware configurations.</span><span class="sxs-lookup"><span data-stu-id="22da0-144">Insights from telemetry data can help identify issues with services or hardware configurations.</span></span> <span data-ttu-id="22da0-145">Microsoft’s ability to get this data from customers and drive improvements to the ecosystem, raises the bar for the quality of integrated Azure Stack solutions.</span><span class="sxs-lookup"><span data-stu-id="22da0-145">Microsoft’s ability to get this data from customers and drive improvements to the ecosystem, raises the bar for the quality of integrated Azure Stack solutions.</span></span>

<span data-ttu-id="22da0-146">Telemetry also helps Microsoft to better understand how customers deploy components, use features, and use services to achieve their business goals.</span><span class="sxs-lookup"><span data-stu-id="22da0-146">Telemetry also helps Microsoft to better understand how customers deploy components, use features, and use services to achieve their business goals.</span></span> <span data-ttu-id="22da0-147">These insights help prioritize engineering investments in areas that can directly impact customer experiences and workloads.</span><span class="sxs-lookup"><span data-stu-id="22da0-147">These insights help prioritize engineering investments in areas that can directly impact customer experiences and workloads.</span></span>

<span data-ttu-id="22da0-148">Some examples include customer use of containers, storage, and networking configurations that are associated with Azure Stack roles.</span><span class="sxs-lookup"><span data-stu-id="22da0-148">Some examples include customer use of containers, storage, and networking configurations that are associated with Azure Stack roles.</span></span> <span data-ttu-id="22da0-149">We also use the insights to drive improvements and intelligence into Azure Stack management and monitoring solutions.</span><span class="sxs-lookup"><span data-stu-id="22da0-149">We also use the insights to drive improvements and intelligence into Azure Stack management and monitoring solutions.</span></span> <span data-ttu-id="22da0-150">These improvements make it easier for customers to diagnose issues and save money by making fewer support calls to Microsoft.</span><span class="sxs-lookup"><span data-stu-id="22da0-150">These improvements make it easier for customers to diagnose issues and save money by making fewer support calls to Microsoft.</span></span>

## <a name="manage-telemetry-collection"></a><span data-ttu-id="22da0-151">Manage telemetry collection</span><span class="sxs-lookup"><span data-stu-id="22da0-151">Manage telemetry collection</span></span>

<span data-ttu-id="22da0-152">We don't recommended turning off telemetry in your organization.</span><span class="sxs-lookup"><span data-stu-id="22da0-152">We don't recommended turning off telemetry in your organization.</span></span> <span data-ttu-id="22da0-153">However, in some scenarios this may be necessary.</span><span class="sxs-lookup"><span data-stu-id="22da0-153">However, in some scenarios this may be necessary.</span></span>

<span data-ttu-id="22da0-154">In these scenarios, you can configure the telemetry level sent to Microsoft by using registry settings before you deploy Azure Stack, or by using the Telemetry Endpoints after you deploy Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="22da0-154">In these scenarios, you can configure the telemetry level sent to Microsoft by using registry settings before you deploy Azure Stack, or by using the Telemetry Endpoints after you deploy Azure Stack.</span></span>

### <a name="telemetry-levels-and-data-collection"></a><span data-ttu-id="22da0-155">Telemetry levels and data collection</span><span class="sxs-lookup"><span data-stu-id="22da0-155">Telemetry levels and data collection</span></span>

<span data-ttu-id="22da0-156">Before you change telemetry settings, you should understand the telemetry levels and what data is collected at each level.</span><span class="sxs-lookup"><span data-stu-id="22da0-156">Before you change telemetry settings, you should understand the telemetry levels and what data is collected at each level.</span></span>

<span data-ttu-id="22da0-157">The telemetry settings are grouped into four levels (0-3) that are cumulative and categorized as the follows:</span><span class="sxs-lookup"><span data-stu-id="22da0-157">The telemetry settings are grouped into four levels (0-3) that are cumulative and categorized as the follows:</span></span>

<span data-ttu-id="22da0-158">**0 (Security)**</span><span class="sxs-lookup"><span data-stu-id="22da0-158">**0 (Security)**</span></span></br>
<span data-ttu-id="22da0-159">Security data only.</span><span class="sxs-lookup"><span data-stu-id="22da0-159">Security data only.</span></span> <span data-ttu-id="22da0-160">Information that’s required to keep the operating system secure.</span><span class="sxs-lookup"><span data-stu-id="22da0-160">Information that’s required to keep the operating system secure.</span></span> <span data-ttu-id="22da0-161">This includes data about the Connected User Experience and Telemetry component settings, and Windows Defender.</span><span class="sxs-lookup"><span data-stu-id="22da0-161">This includes data about the Connected User Experience and Telemetry component settings, and Windows Defender.</span></span> <span data-ttu-id="22da0-162">No telemetry specific to Azure Stack is emitted at this level.</span><span class="sxs-lookup"><span data-stu-id="22da0-162">No telemetry specific to Azure Stack is emitted at this level.</span></span>

<span data-ttu-id="22da0-163">**1 (Basic)**</span><span class="sxs-lookup"><span data-stu-id="22da0-163">**1 (Basic)**</span></span></br>
<span data-ttu-id="22da0-164">Security data, and Basic Health and Quality data.</span><span class="sxs-lookup"><span data-stu-id="22da0-164">Security data, and Basic Health and Quality data.</span></span> <span data-ttu-id="22da0-165">Basic device information, including: quality-related data, app compatibility, app usage data, and data from the **Security** level.</span><span class="sxs-lookup"><span data-stu-id="22da0-165">Basic device information, including: quality-related data, app compatibility, app usage data, and data from the **Security** level.</span></span> <span data-ttu-id="22da0-166">Setting your telemetry level to Basic enables Azure Stack telemetry.</span><span class="sxs-lookup"><span data-stu-id="22da0-166">Setting your telemetry level to Basic enables Azure Stack telemetry.</span></span> <span data-ttu-id="22da0-167">The data gathered at this level includes:</span><span class="sxs-lookup"><span data-stu-id="22da0-167">The data gathered at this level includes:</span></span>

- <span data-ttu-id="22da0-168">*Basic device information* that provides an understanding about the types and configurations of native and virtual Windows Server 2016 instances in the ecosystem.</span><span class="sxs-lookup"><span data-stu-id="22da0-168">*Basic device information* that provides an understanding about the types and configurations of native and virtual Windows Server 2016 instances in the ecosystem.</span></span> <span data-ttu-id="22da0-169">This includes:</span><span class="sxs-lookup"><span data-stu-id="22da0-169">This includes:</span></span>

  - <span data-ttu-id="22da0-170">Machine attributes, such as the OEM, and model.</span><span class="sxs-lookup"><span data-stu-id="22da0-170">Machine attributes, such as the OEM, and model.</span></span>
  - <span data-ttu-id="22da0-171">Networking attributes, such as the number of network adapters and their speed.</span><span class="sxs-lookup"><span data-stu-id="22da0-171">Networking attributes, such as the number of network adapters and their speed.</span></span>
  - <span data-ttu-id="22da0-172">Processor and memory attributes, such as the number of cores, and amount of installed memory.</span><span class="sxs-lookup"><span data-stu-id="22da0-172">Processor and memory attributes, such as the number of cores, and amount of installed memory.</span></span>
  - <span data-ttu-id="22da0-173">Storage attributes, such as the number of drives, type of drive, and drive size.</span><span class="sxs-lookup"><span data-stu-id="22da0-173">Storage attributes, such as the number of drives, type of drive, and drive size.</span></span>

- <span data-ttu-id="22da0-174">*Telemetry functionality*, including the percentage of uploaded events, dropped events, and the last data upload time.</span><span class="sxs-lookup"><span data-stu-id="22da0-174">*Telemetry functionality*, including the percentage of uploaded events, dropped events, and the last data upload time.</span></span>
- <span data-ttu-id="22da0-175">*Quality-related information* that helps Microsoft develop a basic understanding of how Azure Stack is performing.</span><span class="sxs-lookup"><span data-stu-id="22da0-175">*Quality-related information* that helps Microsoft develop a basic understanding of how Azure Stack is performing.</span></span> <span data-ttu-id="22da0-176">For example, the count of critical alerts on a particular hardware configuration.</span><span class="sxs-lookup"><span data-stu-id="22da0-176">For example, the count of critical alerts on a particular hardware configuration.</span></span>
- <span data-ttu-id="22da0-177">*Compatibility data* that helps provide an understanding about which Resource Providers are installed on a system and a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="22da0-177">*Compatibility data* that helps provide an understanding about which Resource Providers are installed on a system and a virtual machine.</span></span> <span data-ttu-id="22da0-178">This identifies potential compatibility problems.</span><span class="sxs-lookup"><span data-stu-id="22da0-178">This identifies potential compatibility problems.</span></span>

<span data-ttu-id="22da0-179">**2 (Enhanced)**</span><span class="sxs-lookup"><span data-stu-id="22da0-179">**2 (Enhanced)**</span></span></br>
<span data-ttu-id="22da0-180">Additional insights, including: how the operating system and Azure Stack services are used, how these services perform, advanced reliability data, and data from the **Security** and **Basic** levels.</span><span class="sxs-lookup"><span data-stu-id="22da0-180">Additional insights, including: how the operating system and Azure Stack services are used, how these services perform, advanced reliability data, and data from the **Security** and **Basic** levels.</span></span>

> [!NOTE]
> <span data-ttu-id="22da0-181">This is the default telemetry setting.</span><span class="sxs-lookup"><span data-stu-id="22da0-181">This is the default telemetry setting.</span></span>

<span data-ttu-id="22da0-182">**3 (Full)**</span><span class="sxs-lookup"><span data-stu-id="22da0-182">**3 (Full)**</span></span></br>
<span data-ttu-id="22da0-183">All data necessary to identify and help to fix problems, plus data from the **Security**, **Basic**, and **Enhanced** levels.</span><span class="sxs-lookup"><span data-stu-id="22da0-183">All data necessary to identify and help to fix problems, plus data from the **Security**, **Basic**, and **Enhanced** levels.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="22da0-184">These telemetry levels only apply to Microsoft Azure Stack components.</span><span class="sxs-lookup"><span data-stu-id="22da0-184">These telemetry levels only apply to Microsoft Azure Stack components.</span></span> <span data-ttu-id="22da0-185">Non-Microsoft software components and services that are running in the Hardware Lifecycle Host from Azure Stack hardware partners may communicate with their cloud services outside of these telemetry levels.</span><span class="sxs-lookup"><span data-stu-id="22da0-185">Non-Microsoft software components and services that are running in the Hardware Lifecycle Host from Azure Stack hardware partners may communicate with their cloud services outside of these telemetry levels.</span></span> <span data-ttu-id="22da0-186">You should work with your Azure Stack hardware solution provider to understand their telemetry policy, and how you can opt in or opt out.</span><span class="sxs-lookup"><span data-stu-id="22da0-186">You should work with your Azure Stack hardware solution provider to understand their telemetry policy, and how you can opt in or opt out.</span></span>

<span data-ttu-id="22da0-187">Turning off Windows and Azure Stack telemetry also disables SQL telemetry.</span><span class="sxs-lookup"><span data-stu-id="22da0-187">Turning off Windows and Azure Stack telemetry also disables SQL telemetry.</span></span> <span data-ttu-id="22da0-188">For more information about the implications of the Windows Server telemetry settings, see the [Windows Telemetry Whitepaper](https://aka.ms/winservtelemetry).</span><span class="sxs-lookup"><span data-stu-id="22da0-188">For more information about the implications of the Windows Server telemetry settings, see the [Windows Telemetry Whitepaper](https://aka.ms/winservtelemetry).</span></span>

### <a name="asdk-set-the-telemetry-level-in-the-windows-registry"></a><span data-ttu-id="22da0-189">ASDK: set the telemetry level in the Windows registry</span><span class="sxs-lookup"><span data-stu-id="22da0-189">ASDK: set the telemetry level in the Windows registry</span></span>

<span data-ttu-id="22da0-190">You can use the Windows Registry Editor to manually set the telemetry level on the physical host computer before you deploy Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="22da0-190">You can use the Windows Registry Editor to manually set the telemetry level on the physical host computer before you deploy Azure Stack.</span></span> <span data-ttu-id="22da0-191">If a management policy already exists, such as Group Policy, it overrides this registry setting.</span><span class="sxs-lookup"><span data-stu-id="22da0-191">If a management policy already exists, such as Group Policy, it overrides this registry setting.</span></span>

<span data-ttu-id="22da0-192">Before deploying Azure Stack on the development kit host, boot into CloudBuilder.vhdx and run the following script in an elevated PowerShell window:</span><span class="sxs-lookup"><span data-stu-id="22da0-192">Before deploying Azure Stack on the development kit host, boot into CloudBuilder.vhdx and run the following script in an elevated PowerShell window:</span></span>

```powershell
### Get current AllowTelmetry value on DVM Host
(Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name AllowTelemetry).AllowTelemetry
### Set & Get updated AllowTelemetry value for ASDK-Host
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name "AllowTelemetry" -Value '0' # Set this value to 0,1,2,or3.  
(Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name AllowTelemetry).AllowTelemetry
```

### <a name="asdk-and-multi-node-enable-or-disable-telemetry-after-deployment"></a><span data-ttu-id="22da0-193">ASDK and Multi-Node: enable or disable telemetry after deployment</span><span class="sxs-lookup"><span data-stu-id="22da0-193">ASDK and Multi-Node: enable or disable telemetry after deployment</span></span>

<span data-ttu-id="22da0-194">To enable or disable telemetry after deployment, you need to have access to the Privileged End Point (PEP) which is exposed on the ERCS VMs.</span><span class="sxs-lookup"><span data-stu-id="22da0-194">To enable or disable telemetry after deployment, you need to have access to the Privileged End Point (PEP) which is exposed on the ERCS VMs.</span></span>

1. <span data-ttu-id="22da0-195">To Enable: `Set-Telemetry -Enable`</span><span class="sxs-lookup"><span data-stu-id="22da0-195">To Enable: `Set-Telemetry -Enable`</span></span>
2. <span data-ttu-id="22da0-196">To Disable: `Set-Telemetry -Disable`</span><span class="sxs-lookup"><span data-stu-id="22da0-196">To Disable: `Set-Telemetry -Disable`</span></span>

<span data-ttu-id="22da0-197">PARAMETER details:</span><span class="sxs-lookup"><span data-stu-id="22da0-197">PARAMETER details:</span></span>
> <span data-ttu-id="22da0-198">.PARAMETER Enable - Turn On telemetry data upload</span><span class="sxs-lookup"><span data-stu-id="22da0-198">.PARAMETER Enable - Turn On telemetry data upload</span></span></br>
> <span data-ttu-id="22da0-199">.PARAMETER Disable - Turn Off telemetry data upload</span><span class="sxs-lookup"><span data-stu-id="22da0-199">.PARAMETER Disable - Turn Off telemetry data upload</span></span>  

<span data-ttu-id="22da0-200">**Script to enable telemetry:**</span><span class="sxs-lookup"><span data-stu-id="22da0-200">**Script to enable telemetry:**</span></span>

```powershell
$ip = "<IP ADDRESS OF THE PEP VM>" # You can also use the machine name instead of IP here.
$pwd= ConvertTo-SecureString "<CLOUD ADMIN PASSWORD>" -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("<DOMAIN NAME>\CloudAdmin", $pwd)
$psSession = New-PSSession -ComputerName $ip -ConfigurationName PrivilegedEndpoint -Credential $cred
Invoke-Command -Session $psSession {Set-Telemetry -Enable}
if($psSession)
{
    Remove-PSSession $psSession
}
```

<span data-ttu-id="22da0-201">**Script to disable telemetry:**</span><span class="sxs-lookup"><span data-stu-id="22da0-201">**Script to disable telemetry:**</span></span>

```powershell
$ip = "<IP ADDRESS OF THE PEP VM>" # You can also use the machine name instead of IP here.
$pwd= ConvertTo-SecureString "<CLOUD ADMIN PASSWORD>" -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("<DOMAIN NAME>\CloudAdmin", $pwd)
$psSession = New-PSSession -ComputerName $ip -ConfigurationName PrivilegedEndpoint -Credential $cred
Invoke-Command -Session $psSession {Set-Telemetry -Disable}
if($psSession)
{
    Remove-PSSession $psSession
}
```

## <a name="next-steps"></a><span data-ttu-id="22da0-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="22da0-202">Next steps</span></span>

- [<span data-ttu-id="22da0-203">Download the Azure Stack development kit deployment package</span><span class="sxs-lookup"><span data-stu-id="22da0-203">Download the Azure Stack development kit deployment package</span></span>](https://azure.microsoft.com/overview/azure-stack/try/?v=try)

- [<span data-ttu-id="22da0-204">Deploy Azure Stack development kit</span><span class="sxs-lookup"><span data-stu-id="22da0-204">Deploy Azure Stack development kit</span></span>](azure-stack-run-powershell-script.md)
