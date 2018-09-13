---
title: Security alerts by type in Azure Security Center | Microsoft Docs
description: This article discusses the different kinds of security alerts available in Azure Security Center.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: ''
ms.assetid: b3e7b4bc-5ee0-4280-ad78-f49998675af1
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/05/2017
ms.author: yurid
ms.openlocfilehash: 5bdba817e15f59c9f6d6ccfdfb7f3ebc45eb2172
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549964"
---
# <a name="security-alerts-by-type-in-azure-security-center"></a><span data-ttu-id="b854e-103">Security alerts by type in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="b854e-103">Security alerts by type in Azure Security Center</span></span>
<span data-ttu-id="b854e-104">This article helps you to understand the different types of security alerts that are available in Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="b854e-104">This article helps you to understand the different types of security alerts that are available in Azure Security Center.</span></span> <span data-ttu-id="b854e-105">For more information on how to manage alerts, see [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="b854e-105">For more information on how to manage alerts, see [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b854e-106">To set up advanced detections, upgrade to Azure Security Center Standard.</span><span class="sxs-lookup"><span data-stu-id="b854e-106">To set up advanced detections, upgrade to Azure Security Center Standard.</span></span> <span data-ttu-id="b854e-107">A free 60-day trial is available.</span><span class="sxs-lookup"><span data-stu-id="b854e-107">A free 60-day trial is available.</span></span> <span data-ttu-id="b854e-108">To upgrade, select **Pricing Tier** in the [security policy](security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="b854e-108">To upgrade, select **Pricing Tier** in the [security policy](security-center-policies.md).</span></span> <span data-ttu-id="b854e-109">To learn more, see the [pricing page](https://azure.microsoft.com/pricing/details/security-center/).</span><span class="sxs-lookup"><span data-stu-id="b854e-109">To learn more, see the [pricing page](https://azure.microsoft.com/pricing/details/security-center/).</span></span>
>
>

## <a name="what-type-of-alerts-are-available"></a><span data-ttu-id="b854e-110">What type of alerts are available?</span><span class="sxs-lookup"><span data-stu-id="b854e-110">What type of alerts are available?</span></span>
<span data-ttu-id="b854e-111">Azure Security Center provides a variety of alerts that align with the stages of the cyber kill chain.</span><span class="sxs-lookup"><span data-stu-id="b854e-111">Azure Security Center provides a variety of alerts that align with the stages of the cyber kill chain.</span></span> <span data-ttu-id="b854e-112">The following illustration shows various alerts as they relate to some of these stages.</span><span class="sxs-lookup"><span data-stu-id="b854e-112">The following illustration shows various alerts as they relate to some of these stages.</span></span>

![Kill chain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-alerts-type/security-center-alerts-type-fig1.png)

<span data-ttu-id="b854e-114">**Target and attack**</span><span class="sxs-lookup"><span data-stu-id="b854e-114">**Target and attack**</span></span>

* <span data-ttu-id="b854e-115">Inbound RDP/SSH attacks</span><span class="sxs-lookup"><span data-stu-id="b854e-115">Inbound RDP/SSH attacks</span></span>
* <span data-ttu-id="b854e-116">Application and DDoS attacks (WAF partners)</span><span class="sxs-lookup"><span data-stu-id="b854e-116">Application and DDoS attacks (WAF partners)</span></span>
* <span data-ttu-id="b854e-117">Intrusion detection (NG Firewall partners)</span><span class="sxs-lookup"><span data-stu-id="b854e-117">Intrusion detection (NG Firewall partners)</span></span>

<span data-ttu-id="b854e-118">**Install and exploit**</span><span class="sxs-lookup"><span data-stu-id="b854e-118">**Install and exploit**</span></span>

* <span data-ttu-id="b854e-119">Known malware signatures (AM partners)</span><span class="sxs-lookup"><span data-stu-id="b854e-119">Known malware signatures (AM partners)</span></span>
* <span data-ttu-id="b854e-120">In-memory malware and exploit attempts</span><span class="sxs-lookup"><span data-stu-id="b854e-120">In-memory malware and exploit attempts</span></span>
* <span data-ttu-id="b854e-121">Suspicious process execution</span><span class="sxs-lookup"><span data-stu-id="b854e-121">Suspicious process execution</span></span>
* <span data-ttu-id="b854e-122">Evasive maneuvers to avoid discovery</span><span class="sxs-lookup"><span data-stu-id="b854e-122">Evasive maneuvers to avoid discovery</span></span>
* <span data-ttu-id="b854e-123">Lateral movement</span><span class="sxs-lookup"><span data-stu-id="b854e-123">Lateral movement</span></span>
* <span data-ttu-id="b854e-124">Internal reconnaissance</span><span class="sxs-lookup"><span data-stu-id="b854e-124">Internal reconnaissance</span></span>
* <span data-ttu-id="b854e-125">Suspicious PowerShell activity</span><span class="sxs-lookup"><span data-stu-id="b854e-125">Suspicious PowerShell activity</span></span>

<span data-ttu-id="b854e-126">**Post breach**</span><span class="sxs-lookup"><span data-stu-id="b854e-126">**Post breach**</span></span>  

* <span data-ttu-id="b854e-127">Communication to a known malicious IP (data exfiltration or command and control)</span><span class="sxs-lookup"><span data-stu-id="b854e-127">Communication to a known malicious IP (data exfiltration or command and control)</span></span>
* <span data-ttu-id="b854e-128">Using compromised resources to mount additional attacks (outbound port scanning RDP/SSH brute force attacks, and spam)</span><span class="sxs-lookup"><span data-stu-id="b854e-128">Using compromised resources to mount additional attacks (outbound port scanning RDP/SSH brute force attacks, and spam)</span></span>

<span data-ttu-id="b854e-129">Different types of attacks are associated with each stage, and they target different subsystems.</span><span class="sxs-lookup"><span data-stu-id="b854e-129">Different types of attacks are associated with each stage, and they target different subsystems.</span></span> <span data-ttu-id="b854e-130">To address attacks during these stages, Security Center has three categories of alerts:</span><span class="sxs-lookup"><span data-stu-id="b854e-130">To address attacks during these stages, Security Center has three categories of alerts:</span></span>

* <span data-ttu-id="b854e-131">Virtual Machine Behavioral Analysis (VMBA)</span><span class="sxs-lookup"><span data-stu-id="b854e-131">Virtual Machine Behavioral Analysis (VMBA)</span></span>
* <span data-ttu-id="b854e-132">Network Analysis</span><span class="sxs-lookup"><span data-stu-id="b854e-132">Network Analysis</span></span>
* <span data-ttu-id="b854e-133">Resource Analysis</span><span class="sxs-lookup"><span data-stu-id="b854e-133">Resource Analysis</span></span>

## <a name="virtual-machine-behavioral-analysis"></a><span data-ttu-id="b854e-134">Virtual machine behavioral analysis</span><span class="sxs-lookup"><span data-stu-id="b854e-134">Virtual machine behavioral analysis</span></span>
<span data-ttu-id="b854e-135">Azure Security Center can use behavioral analytics to identify compromised resources based on analysis of virtual machine event logs.</span><span class="sxs-lookup"><span data-stu-id="b854e-135">Azure Security Center can use behavioral analytics to identify compromised resources based on analysis of virtual machine event logs.</span></span> <span data-ttu-id="b854e-136">For example, Process Creation Events and Login Events.</span><span class="sxs-lookup"><span data-stu-id="b854e-136">For example, Process Creation Events and Login Events.</span></span> <span data-ttu-id="b854e-137">In addition, there is correlation with other signals to check for supporting evidence of a widespread campaign.</span><span class="sxs-lookup"><span data-stu-id="b854e-137">In addition, there is correlation with other signals to check for supporting evidence of a widespread campaign.</span></span>

> [!NOTE]
> <span data-ttu-id="b854e-138">For more information on how Security Center detection capabilities work, see [Azure Security Center detection capabilities](security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="b854e-138">For more information on how Security Center detection capabilities work, see [Azure Security Center detection capabilities](security-center-detection-capabilities.md).</span></span>
>
>

### <a name="crash-analysis"></a><span data-ttu-id="b854e-139">Crash analysis</span><span class="sxs-lookup"><span data-stu-id="b854e-139">Crash analysis</span></span>
<span data-ttu-id="b854e-140">Crash dump memory analysis is a method used to detect sophisticated malware that is able to evade traditional security solutions.</span><span class="sxs-lookup"><span data-stu-id="b854e-140">Crash dump memory analysis is a method used to detect sophisticated malware that is able to evade traditional security solutions.</span></span> <span data-ttu-id="b854e-141">Various forms of malware try to reduce the chance of being detected by antivirus products by never writing to disk, or by encrypting software components written to disk.</span><span class="sxs-lookup"><span data-stu-id="b854e-141">Various forms of malware try to reduce the chance of being detected by antivirus products by never writing to disk, or by encrypting software components written to disk.</span></span> <span data-ttu-id="b854e-142">This makes the malware difficult to detect by using traditional antimalware approaches.</span><span class="sxs-lookup"><span data-stu-id="b854e-142">This makes the malware difficult to detect by using traditional antimalware approaches.</span></span> <span data-ttu-id="b854e-143">However, this kind of malware can be detected by using memory analysis, because malware must leave traces in memory in order to function.</span><span class="sxs-lookup"><span data-stu-id="b854e-143">However, this kind of malware can be detected by using memory analysis, because malware must leave traces in memory in order to function.</span></span>

<span data-ttu-id="b854e-144">When software crashes, a crash dump captures a portion of memory at the time of the crash.</span><span class="sxs-lookup"><span data-stu-id="b854e-144">When software crashes, a crash dump captures a portion of memory at the time of the crash.</span></span> <span data-ttu-id="b854e-145">The crash may be caused by malware, general application or system issues.</span><span class="sxs-lookup"><span data-stu-id="b854e-145">The crash may be caused by malware, general application or system issues.</span></span> <span data-ttu-id="b854e-146">By analyzing the memory in the crash dump, Security Center can detect techniques used to exploit vulnerabilities in software, access confidential data, and surreptitiously persist within a compromised machine.</span><span class="sxs-lookup"><span data-stu-id="b854e-146">By analyzing the memory in the crash dump, Security Center can detect techniques used to exploit vulnerabilities in software, access confidential data, and surreptitiously persist within a compromised machine.</span></span> <span data-ttu-id="b854e-147">This is accomplished with minimum performance impact to hosts as the analysis is performed by the Security Center back end.</span><span class="sxs-lookup"><span data-stu-id="b854e-147">This is accomplished with minimum performance impact to hosts as the analysis is performed by the Security Center back end.</span></span>

<span data-ttu-id="b854e-148">The following fields are common to the crash dump alert examples that appear later in this article:</span><span class="sxs-lookup"><span data-stu-id="b854e-148">The following fields are common to the crash dump alert examples that appear later in this article:</span></span>

* <span data-ttu-id="b854e-149">DUMPFILE: Name of the crash dump file.</span><span class="sxs-lookup"><span data-stu-id="b854e-149">DUMPFILE: Name of the crash dump file.</span></span>
* <span data-ttu-id="b854e-150">PROCESSNAME: Name of the crashing process.</span><span class="sxs-lookup"><span data-stu-id="b854e-150">PROCESSNAME: Name of the crashing process.</span></span>
* <span data-ttu-id="b854e-151">PROCESSVERSION: Version of the crashing process.</span><span class="sxs-lookup"><span data-stu-id="b854e-151">PROCESSVERSION: Version of the crashing process.</span></span>

### <a name="shellcode-discovered"></a><span data-ttu-id="b854e-152">Shellcode discovered</span><span class="sxs-lookup"><span data-stu-id="b854e-152">Shellcode discovered</span></span>
<span data-ttu-id="b854e-153">Shellcode is the payload that is run after malware exploits a software vulnerability.</span><span class="sxs-lookup"><span data-stu-id="b854e-153">Shellcode is the payload that is run after malware exploits a software vulnerability.</span></span> <span data-ttu-id="b854e-154">This alert indicates that crash dump analysis has detected executable code that exhibits behavior that is commonly performed by malicious payloads.</span><span class="sxs-lookup"><span data-stu-id="b854e-154">This alert indicates that crash dump analysis has detected executable code that exhibits behavior that is commonly performed by malicious payloads.</span></span> <span data-ttu-id="b854e-155">Although non-malicious software may perform this behavior, it is not typical of normal software development practices.</span><span class="sxs-lookup"><span data-stu-id="b854e-155">Although non-malicious software may perform this behavior, it is not typical of normal software development practices.</span></span>

<span data-ttu-id="b854e-156">The Shellcode alert example provides the following additional field:</span><span class="sxs-lookup"><span data-stu-id="b854e-156">The Shellcode alert example provides the following additional field:</span></span>

* <span data-ttu-id="b854e-157">ADDRESS: The location in memory of the shellcode.</span><span class="sxs-lookup"><span data-stu-id="b854e-157">ADDRESS: The location in memory of the shellcode.</span></span>

<span data-ttu-id="b854e-158">This is an example of this type of alert:</span><span class="sxs-lookup"><span data-stu-id="b854e-158">This is an example of this type of alert:</span></span>

![Shellcode alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-alerts-type/security-center-alerts-type-fig2.png)

### <a name="module-hijacking-discovered"></a><span data-ttu-id="b854e-160">Module hijacking discovered</span><span class="sxs-lookup"><span data-stu-id="b854e-160">Module hijacking discovered</span></span>
<span data-ttu-id="b854e-161">Windows uses dynamic-link libraries (DLLs) to allow software to utilize common Windows system functionality.</span><span class="sxs-lookup"><span data-stu-id="b854e-161">Windows uses dynamic-link libraries (DLLs) to allow software to utilize common Windows system functionality.</span></span> <span data-ttu-id="b854e-162">DLL Hijacking occurs when malware changes the DLL load order to load malicious payloads into memory, where arbitrary code can be executed.</span><span class="sxs-lookup"><span data-stu-id="b854e-162">DLL Hijacking occurs when malware changes the DLL load order to load malicious payloads into memory, where arbitrary code can be executed.</span></span> <span data-ttu-id="b854e-163">This alert indicates that the crash dump analysis detected a similarly named module that is loaded from two different paths.</span><span class="sxs-lookup"><span data-stu-id="b854e-163">This alert indicates that the crash dump analysis detected a similarly named module that is loaded from two different paths.</span></span> <span data-ttu-id="b854e-164">One of the loaded paths comes from a common Windows system binary location.</span><span class="sxs-lookup"><span data-stu-id="b854e-164">One of the loaded paths comes from a common Windows system binary location.</span></span>

<span data-ttu-id="b854e-165">Legitimate software developers occasionally change the DLL load order for non-malicious reasons, such as instrumenting, extending the Windows OS, or extending a Windows application.</span><span class="sxs-lookup"><span data-stu-id="b854e-165">Legitimate software developers occasionally change the DLL load order for non-malicious reasons, such as instrumenting, extending the Windows OS, or extending a Windows application.</span></span> <span data-ttu-id="b854e-166">To help differentiate between malicious and potentially benign changes to the DLL load order, Azure Security Center checks whether a loaded module conforms to a suspicious profile.</span><span class="sxs-lookup"><span data-stu-id="b854e-166">To help differentiate between malicious and potentially benign changes to the DLL load order, Azure Security Center checks whether a loaded module conforms to a suspicious profile.</span></span> <span data-ttu-id="b854e-167">The result of this check is indicated by the “SIGNATURE” field of the alert and is reflected in the severity of the alert, alert description, and alert remediation steps.</span><span class="sxs-lookup"><span data-stu-id="b854e-167">The result of this check is indicated by the “SIGNATURE” field of the alert and is reflected in the severity of the alert, alert description, and alert remediation steps.</span></span> <span data-ttu-id="b854e-168">To research whether the module is legitimate or malicious, analyze the on disk copy of the hijacking module.</span><span class="sxs-lookup"><span data-stu-id="b854e-168">To research whether the module is legitimate or malicious, analyze the on disk copy of the hijacking module.</span></span> <span data-ttu-id="b854e-169">For example, you can verify the file's digital signature, or run an antivirus scan.</span><span class="sxs-lookup"><span data-stu-id="b854e-169">For example, you can verify the file's digital signature, or run an antivirus scan.</span></span>

<span data-ttu-id="b854e-170">In addition to the common fields described in the earlier “Shellcode discovered” section, this alert provides the following fields:</span><span class="sxs-lookup"><span data-stu-id="b854e-170">In addition to the common fields described in the earlier “Shellcode discovered” section, this alert provides the following fields:</span></span>

* <span data-ttu-id="b854e-171">SIGNATURE: Indicates if the hijacking module conforms to a suspicious behavior profile.</span><span class="sxs-lookup"><span data-stu-id="b854e-171">SIGNATURE: Indicates if the hijacking module conforms to a suspicious behavior profile.</span></span>
* <span data-ttu-id="b854e-172">HIJACKEDMODULE: The name of the hijacked Windows system module.</span><span class="sxs-lookup"><span data-stu-id="b854e-172">HIJACKEDMODULE: The name of the hijacked Windows system module.</span></span>
* <span data-ttu-id="b854e-173">HIJACKEDMODULEPATH: The path of the hijacked Windows system module.</span><span class="sxs-lookup"><span data-stu-id="b854e-173">HIJACKEDMODULEPATH: The path of the hijacked Windows system module.</span></span>
* <span data-ttu-id="b854e-174">HIJACKINGMODULEPATH: The path of the hijacking module.</span><span class="sxs-lookup"><span data-stu-id="b854e-174">HIJACKINGMODULEPATH: The path of the hijacking module.</span></span>

<span data-ttu-id="b854e-175">This is an example of this type of alert:</span><span class="sxs-lookup"><span data-stu-id="b854e-175">This is an example of this type of alert:</span></span>

![Module hijacking alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-alerts-type/security-center-alerts-type-fig3.png)

### <a name="masquerading-windows-module-detected"></a><span data-ttu-id="b854e-177">Masquerading Windows module detected</span><span class="sxs-lookup"><span data-stu-id="b854e-177">Masquerading Windows module detected</span></span>
<span data-ttu-id="b854e-178">Malware may use common names of Windows system binaries (for example, SVCHOST.EXE) or modules (for example, NTDLL.DLL) to *blend in* and obscure the nature of the malicious software from system administrators.</span><span class="sxs-lookup"><span data-stu-id="b854e-178">Malware may use common names of Windows system binaries (for example, SVCHOST.EXE) or modules (for example, NTDLL.DLL) to *blend in* and obscure the nature of the malicious software from system administrators.</span></span> <span data-ttu-id="b854e-179">This alert indicates that the crash dump analysis detects that the crash dump file contains modules that use Windows system module names, but do not satisfy other criteria that are typical of Windows modules.</span><span class="sxs-lookup"><span data-stu-id="b854e-179">This alert indicates that the crash dump analysis detects that the crash dump file contains modules that use Windows system module names, but do not satisfy other criteria that are typical of Windows modules.</span></span> <span data-ttu-id="b854e-180">Analyzing the on disk copy of the masquerading module may provide more information about the legitimate or malicious nature of this module.</span><span class="sxs-lookup"><span data-stu-id="b854e-180">Analyzing the on disk copy of the masquerading module may provide more information about the legitimate or malicious nature of this module.</span></span> <span data-ttu-id="b854e-181">Analysis may include:</span><span class="sxs-lookup"><span data-stu-id="b854e-181">Analysis may include:</span></span>

* <span data-ttu-id="b854e-182">Confirm that the file in question is shipped as part of a legitimate software package.</span><span class="sxs-lookup"><span data-stu-id="b854e-182">Confirm that the file in question is shipped as part of a legitimate software package.</span></span>
* <span data-ttu-id="b854e-183">Verify the file’s digital signature.</span><span class="sxs-lookup"><span data-stu-id="b854e-183">Verify the file’s digital signature.</span></span>
* <span data-ttu-id="b854e-184">Run an antivirus scan on the file.</span><span class="sxs-lookup"><span data-stu-id="b854e-184">Run an antivirus scan on the file.</span></span>

<span data-ttu-id="b854e-185">In addition to the common fields described earlier in the “Shellcode discovered” section, this alert provides the following additional fields:</span><span class="sxs-lookup"><span data-stu-id="b854e-185">In addition to the common fields described earlier in the “Shellcode discovered” section, this alert provides the following additional fields:</span></span>

* <span data-ttu-id="b854e-186">DETAILS: Describes whether the module's metadata is valid, and whether the module was loaded from a system path.</span><span class="sxs-lookup"><span data-stu-id="b854e-186">DETAILS: Describes whether the module's metadata is valid, and whether the module was loaded from a system path.</span></span>
* <span data-ttu-id="b854e-187">NAME: The name of the masquerading Windows module.</span><span class="sxs-lookup"><span data-stu-id="b854e-187">NAME: The name of the masquerading Windows module.</span></span>
* <span data-ttu-id="b854e-188">PATH: The path to the masquerading Windows module.</span><span class="sxs-lookup"><span data-stu-id="b854e-188">PATH: The path to the masquerading Windows module.</span></span>

<span data-ttu-id="b854e-189">This alert also extracts and displays certain fields from the module’s PE header, such as “CHECKSUM” and “TIMESTAMP.”</span><span class="sxs-lookup"><span data-stu-id="b854e-189">This alert also extracts and displays certain fields from the module’s PE header, such as “CHECKSUM” and “TIMESTAMP.”</span></span> <span data-ttu-id="b854e-190">These fields are only displayed if the fields are present in the module.</span><span class="sxs-lookup"><span data-stu-id="b854e-190">These fields are only displayed if the fields are present in the module.</span></span> <span data-ttu-id="b854e-191">See the [Microsoft PE and COFF Specification](https://msdn.microsoft.com/windows/hardware/gg463119.aspx) for details on these fields.</span><span class="sxs-lookup"><span data-stu-id="b854e-191">See the [Microsoft PE and COFF Specification](https://msdn.microsoft.com/windows/hardware/gg463119.aspx) for details on these fields.</span></span>

<span data-ttu-id="b854e-192">This is an example of this type of alert:</span><span class="sxs-lookup"><span data-stu-id="b854e-192">This is an example of this type of alert:</span></span>

![Masquerading Windows alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-alerts-type/security-center-alerts-type-fig4.png)

### <a name="modified-system-binary-discovered"></a><span data-ttu-id="b854e-194">Modified system binary discovered</span><span class="sxs-lookup"><span data-stu-id="b854e-194">Modified system binary discovered</span></span>
<span data-ttu-id="b854e-195">Malware may modify core system binaries in order to covertly access data or surreptitiously persist on a compromised system.</span><span class="sxs-lookup"><span data-stu-id="b854e-195">Malware may modify core system binaries in order to covertly access data or surreptitiously persist on a compromised system.</span></span> <span data-ttu-id="b854e-196">This alert indicates that the crash dump analysis has detected that core Windows OS binaries have been modified in memory or on disk.</span><span class="sxs-lookup"><span data-stu-id="b854e-196">This alert indicates that the crash dump analysis has detected that core Windows OS binaries have been modified in memory or on disk.</span></span>

<span data-ttu-id="b854e-197">Legitimate software developers occasionally modify system modules in memory for non-malicious reasons, such as Detours or for application compatibility.</span><span class="sxs-lookup"><span data-stu-id="b854e-197">Legitimate software developers occasionally modify system modules in memory for non-malicious reasons, such as Detours or for application compatibility.</span></span> <span data-ttu-id="b854e-198">To help differentiate between malicious and potentially legitimate modules, Azure Security Center checks whether the modified module conforms to a suspicious profile.</span><span class="sxs-lookup"><span data-stu-id="b854e-198">To help differentiate between malicious and potentially legitimate modules, Azure Security Center checks whether the modified module conforms to a suspicious profile.</span></span> <span data-ttu-id="b854e-199">The result of this check is indicated by the severity of the alert, alert description, and alert remediation steps.</span><span class="sxs-lookup"><span data-stu-id="b854e-199">The result of this check is indicated by the severity of the alert, alert description, and alert remediation steps.</span></span>

<span data-ttu-id="b854e-200">In addition to the common fields described earlier in the “Shellcode discovered” section, this alert provides the following additional fields:</span><span class="sxs-lookup"><span data-stu-id="b854e-200">In addition to the common fields described earlier in the “Shellcode discovered” section, this alert provides the following additional fields:</span></span>

* <span data-ttu-id="b854e-201">MODULENAME: Name of the modified system binary.</span><span class="sxs-lookup"><span data-stu-id="b854e-201">MODULENAME: Name of the modified system binary.</span></span>
* <span data-ttu-id="b854e-202">MODULEVERSION: Version of the modified system binary.</span><span class="sxs-lookup"><span data-stu-id="b854e-202">MODULEVERSION: Version of the modified system binary.</span></span>

<span data-ttu-id="b854e-203">This is an example of this type of alert:</span><span class="sxs-lookup"><span data-stu-id="b854e-203">This is an example of this type of alert:</span></span>

![System binary alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-alerts-type/security-center-alerts-type-fig5.png)

### <a name="suspicious-process-executed"></a><span data-ttu-id="b854e-205">Suspicious process executed</span><span class="sxs-lookup"><span data-stu-id="b854e-205">Suspicious process executed</span></span>
<span data-ttu-id="b854e-206">Security Center identifies a suspicious process that runs on the target virtual machine, and then triggers an alert.</span><span class="sxs-lookup"><span data-stu-id="b854e-206">Security Center identifies a suspicious process that runs on the target virtual machine, and then triggers an alert.</span></span> <span data-ttu-id="b854e-207">The detection doesn’t look for the specific name, but does look for the executable file's parameter.</span><span class="sxs-lookup"><span data-stu-id="b854e-207">The detection doesn’t look for the specific name, but does look for the executable file's parameter.</span></span> <span data-ttu-id="b854e-208">Therefore, even if the attacker renames the executable, Security Center can still detect the suspicious process.</span><span class="sxs-lookup"><span data-stu-id="b854e-208">Therefore, even if the attacker renames the executable, Security Center can still detect the suspicious process.</span></span>

<span data-ttu-id="b854e-209">This is an example of this type of alert:</span><span class="sxs-lookup"><span data-stu-id="b854e-209">This is an example of this type of alert:</span></span>

![Suspicious process alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-alerts-type/security-center-alerts-type-fig6-new.png)

### <a name="multiple-domain-accounts-queried"></a><span data-ttu-id="b854e-211">Multiple domain accounts queried</span><span class="sxs-lookup"><span data-stu-id="b854e-211">Multiple domain accounts queried</span></span>
<span data-ttu-id="b854e-212">Security Center can detect multiple attempts to query Active Directory domain accounts, which is something usually performed by attackers during network reconnaissance.</span><span class="sxs-lookup"><span data-stu-id="b854e-212">Security Center can detect multiple attempts to query Active Directory domain accounts, which is something usually performed by attackers during network reconnaissance.</span></span> <span data-ttu-id="b854e-213">Attackers can leverage this technique to query the domain to identify the users, identify the domain admin accounts, identify the computers that are domain controllers, and also identify the potential domain trust relationship with other domains.</span><span class="sxs-lookup"><span data-stu-id="b854e-213">Attackers can leverage this technique to query the domain to identify the users, identify the domain admin accounts, identify the computers that are domain controllers, and also identify the potential domain trust relationship with other domains.</span></span>

<span data-ttu-id="b854e-214">This is an example of this type of alert:</span><span class="sxs-lookup"><span data-stu-id="b854e-214">This is an example of this type of alert:</span></span>

![Multiple domains account alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-alerts-type/security-center-alerts-type-fig7-new.png)

### <a name="local-administrators-group-members-were-enumerated"></a><span data-ttu-id="b854e-216">Local Administrators group members were enumerated</span><span class="sxs-lookup"><span data-stu-id="b854e-216">Local Administrators group members were enumerated</span></span>

<span data-ttu-id="b854e-217">Security Center is going to trigger an alert when the security event 4798, in Windows Server 2016 and Windows 10, is trigged.</span><span class="sxs-lookup"><span data-stu-id="b854e-217">Security Center is going to trigger an alert when the security event 4798, in Windows Server 2016 and Windows 10, is trigged.</span></span> <span data-ttu-id="b854e-218">This happens when local administrator groups are enumerated, which is something usually performed by attackers during network reconnaissance.</span><span class="sxs-lookup"><span data-stu-id="b854e-218">This happens when local administrator groups are enumerated, which is something usually performed by attackers during network reconnaissance.</span></span> <span data-ttu-id="b854e-219">Attackers can leverage this technique to query the identity of users with administrative privileges.</span><span class="sxs-lookup"><span data-stu-id="b854e-219">Attackers can leverage this technique to query the identity of users with administrative privileges.</span></span>

<span data-ttu-id="b854e-220">This is an example of this type of alert:</span><span class="sxs-lookup"><span data-stu-id="b854e-220">This is an example of this type of alert:</span></span>

![Local admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-alerts-type/security-center-alerts-type-fig14-new.png)

### <a name="anomalous-mix-of-upper-and-lower-case-characters"></a><span data-ttu-id="b854e-222">Anomalous mix of upper and lower case characters</span><span class="sxs-lookup"><span data-stu-id="b854e-222">Anomalous mix of upper and lower case characters</span></span>

<span data-ttu-id="b854e-223">Security Center will trigger an alert when it detects the use of a mix of upper and lower case characters at the command line.</span><span class="sxs-lookup"><span data-stu-id="b854e-223">Security Center will trigger an alert when it detects the use of a mix of upper and lower case characters at the command line.</span></span> <span data-ttu-id="b854e-224">Some attackers may use this technique to hide from case-sensitive or hash based machine rule.</span><span class="sxs-lookup"><span data-stu-id="b854e-224">Some attackers may use this technique to hide from case-sensitive or hash based machine rule.</span></span>

<span data-ttu-id="b854e-225">This is an example of this type of alert:</span><span class="sxs-lookup"><span data-stu-id="b854e-225">This is an example of this type of alert:</span></span>

![Anomalous mix](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-alerts-type/security-center-alerts-type-fig15-new.png)

### <a name="suspected-kerberos-golden-ticket-attack"></a><span data-ttu-id="b854e-227">Suspected Kerberos Golden Ticket attack</span><span class="sxs-lookup"><span data-stu-id="b854e-227">Suspected Kerberos Golden Ticket attack</span></span>

<span data-ttu-id="b854e-228">A compromised [krbtgt](https://technet.microsoft.com/library/dn745899.aspx) key can be used by an attacker to create Kerberos "Golden Tickets," allowing the attacker to impersonate any user they wish.</span><span class="sxs-lookup"><span data-stu-id="b854e-228">A compromised [krbtgt](https://technet.microsoft.com/library/dn745899.aspx) key can be used by an attacker to create Kerberos "Golden Tickets," allowing the attacker to impersonate any user they wish.</span></span> <span data-ttu-id="b854e-229">Security Center is going to trigger an alert when it detects this type of activity.</span><span class="sxs-lookup"><span data-stu-id="b854e-229">Security Center is going to trigger an alert when it detects this type of activity.</span></span>

> [!NOTE] 
> <span data-ttu-id="b854e-230">For more information about Kerberos Golden Ticket, read [Windows 10 credential theft mitigation guide](http://download.microsoft.com/download/C/1/4/C14579CA-E564-4743-8B51-61C0882662AC/Windows%2010%20credential%20theft%20mitigation%20guide.docx).</span><span class="sxs-lookup"><span data-stu-id="b854e-230">For more information about Kerberos Golden Ticket, read [Windows 10 credential theft mitigation guide](http://download.microsoft.com/download/C/1/4/C14579CA-E564-4743-8B51-61C0882662AC/Windows%2010%20credential%20theft%20mitigation%20guide.docx).</span></span>

<span data-ttu-id="b854e-231">This is an example of this type of alert:</span><span class="sxs-lookup"><span data-stu-id="b854e-231">This is an example of this type of alert:</span></span>

![Golden ticket](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-alerts-type/security-center-alerts-type-fig16-new.png)

### <a name="suspicious-account-created"></a><span data-ttu-id="b854e-233">Suspicious account created</span><span class="sxs-lookup"><span data-stu-id="b854e-233">Suspicious account created</span></span>

<span data-ttu-id="b854e-234">Security Center will trigger an alert when an account is created with close resemblance of an existing built in administrative privilege account.</span><span class="sxs-lookup"><span data-stu-id="b854e-234">Security Center will trigger an alert when an account is created with close resemblance of an existing built in administrative privilege account.</span></span> <span data-ttu-id="b854e-235">This technique can be used by attackers to create a rogue account to avoid being noticed by human verification.</span><span class="sxs-lookup"><span data-stu-id="b854e-235">This technique can be used by attackers to create a rogue account to avoid being noticed by human verification.</span></span>
 
<span data-ttu-id="b854e-236">This is an example of this type of alert:</span><span class="sxs-lookup"><span data-stu-id="b854e-236">This is an example of this type of alert:</span></span>

![Suspicious account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-alerts-type/security-center-alerts-type-fig17-new.png)

### <a name="suspicious-firewall-rule-created"></a><span data-ttu-id="b854e-238">Suspicious Firewall rule created</span><span class="sxs-lookup"><span data-stu-id="b854e-238">Suspicious Firewall rule created</span></span>

<span data-ttu-id="b854e-239">Attackers might try to circumvent host security by creating custom firewall rules to allow malicious applications to communicate with command and control, or to launch attacks through the network via the compromised host.</span><span class="sxs-lookup"><span data-stu-id="b854e-239">Attackers might try to circumvent host security by creating custom firewall rules to allow malicious applications to communicate with command and control, or to launch attacks through the network via the compromised host.</span></span> <span data-ttu-id="b854e-240">Security Center will trigger an alert when it detects that a new firewall rule was created from an executable file in a suspicious location.</span><span class="sxs-lookup"><span data-stu-id="b854e-240">Security Center will trigger an alert when it detects that a new firewall rule was created from an executable file in a suspicious location.</span></span>
 
<span data-ttu-id="b854e-241">This is an example of this type of alert:</span><span class="sxs-lookup"><span data-stu-id="b854e-241">This is an example of this type of alert:</span></span>

![Firewall rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-alerts-type/security-center-alerts-type-fig18-new.png)

### <a name="suspicious-combination-of-hta-and-powershell"></a><span data-ttu-id="b854e-243">Suspicious combination of HTA and PowerShell</span><span class="sxs-lookup"><span data-stu-id="b854e-243">Suspicious combination of HTA and PowerShell</span></span>

<span data-ttu-id="b854e-244">Security Center will trigger an alert when it detects that a Microsoft HTML Application Host (HTA) is launching PowerShell commands.</span><span class="sxs-lookup"><span data-stu-id="b854e-244">Security Center will trigger an alert when it detects that a Microsoft HTML Application Host (HTA) is launching PowerShell commands.</span></span> <span data-ttu-id="b854e-245">This is a technique used by attackers to launch malicious PowerShell scripts.</span><span class="sxs-lookup"><span data-stu-id="b854e-245">This is a technique used by attackers to launch malicious PowerShell scripts.</span></span>
 
<span data-ttu-id="b854e-246">This is an example of this type of alert:</span><span class="sxs-lookup"><span data-stu-id="b854e-246">This is an example of this type of alert:</span></span>

![HTA and PS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-alerts-type/security-center-alerts-type-fig19-new.png)


## <a name="network-analysis"></a><span data-ttu-id="b854e-248">Network analysis</span><span class="sxs-lookup"><span data-stu-id="b854e-248">Network analysis</span></span>
<span data-ttu-id="b854e-249">Security Center network threat detection works by automatically collecting security information from your Azure IPFIX (Internet Protocol Flow Information Export) traffic.</span><span class="sxs-lookup"><span data-stu-id="b854e-249">Security Center network threat detection works by automatically collecting security information from your Azure IPFIX (Internet Protocol Flow Information Export) traffic.</span></span> <span data-ttu-id="b854e-250">It analyzes this information, often correlating information from multiple sources, to identify threats.</span><span class="sxs-lookup"><span data-stu-id="b854e-250">It analyzes this information, often correlating information from multiple sources, to identify threats.</span></span>

### <a name="suspicious-outgoing-traffic-detected"></a><span data-ttu-id="b854e-251">Suspicious outgoing traffic detected</span><span class="sxs-lookup"><span data-stu-id="b854e-251">Suspicious outgoing traffic detected</span></span>
<span data-ttu-id="b854e-252">Network devices can be discovered and profiled in much the same way as other types of systems.</span><span class="sxs-lookup"><span data-stu-id="b854e-252">Network devices can be discovered and profiled in much the same way as other types of systems.</span></span> <span data-ttu-id="b854e-253">Attackers usually start with port scanning or port sweeping.</span><span class="sxs-lookup"><span data-stu-id="b854e-253">Attackers usually start with port scanning or port sweeping.</span></span> <span data-ttu-id="b854e-254">In the next example, you have suspicious Secure Shell (SSH) traffic from a VM.</span><span class="sxs-lookup"><span data-stu-id="b854e-254">In the next example, you have suspicious Secure Shell (SSH) traffic from a VM.</span></span> <span data-ttu-id="b854e-255">In this scenario, SSH brute force or a port sweeping attack against an external resource is possible.</span><span class="sxs-lookup"><span data-stu-id="b854e-255">In this scenario, SSH brute force or a port sweeping attack against an external resource is possible.</span></span>

![Suspicious outgoing traffic alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-alerts-type/security-center-alerts-type-fig8.png)

<span data-ttu-id="b854e-257">This alert gives information that you can use to identify the resource that was used to initiate this attack.</span><span class="sxs-lookup"><span data-stu-id="b854e-257">This alert gives information that you can use to identify the resource that was used to initiate this attack.</span></span> <span data-ttu-id="b854e-258">This alert also provides information to identify the compromised machine, the detection time, plus the protocol and port that was used.</span><span class="sxs-lookup"><span data-stu-id="b854e-258">This alert also provides information to identify the compromised machine, the detection time, plus the protocol and port that was used.</span></span> <span data-ttu-id="b854e-259">This blade also gives you a list of remediation steps that can be used to mitigate this issue.</span><span class="sxs-lookup"><span data-stu-id="b854e-259">This blade also gives you a list of remediation steps that can be used to mitigate this issue.</span></span>

### <a name="network-communication-with-a-malicious-machine"></a><span data-ttu-id="b854e-260">Network communication with a malicious machine</span><span class="sxs-lookup"><span data-stu-id="b854e-260">Network communication with a malicious machine</span></span>
<span data-ttu-id="b854e-261">By leveraging Microsoft threat intelligence feeds, Azure Security Center can detect compromised machines that communicate with malicious IP addresses.</span><span class="sxs-lookup"><span data-stu-id="b854e-261">By leveraging Microsoft threat intelligence feeds, Azure Security Center can detect compromised machines that communicate with malicious IP addresses.</span></span> <span data-ttu-id="b854e-262">In many cases, the malicious address is a command and control center.</span><span class="sxs-lookup"><span data-stu-id="b854e-262">In many cases, the malicious address is a command and control center.</span></span> <span data-ttu-id="b854e-263">In this case, Security Center detected that the communication was done by using Pony Loader malware (also known as [Fareit](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=PWS:Win32/Fareit.AF)).</span><span class="sxs-lookup"><span data-stu-id="b854e-263">In this case, Security Center detected that the communication was done by using Pony Loader malware (also known as [Fareit](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=PWS:Win32/Fareit.AF)).</span></span>

![network communication alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-alerts-type/security-center-alerts-type-fig9.png)

<span data-ttu-id="b854e-265">This alert gives information that enables you to identify the resource that was used to initiate this attack, the attacked resource, the victim IP, the attacker IP, and the detection time.</span><span class="sxs-lookup"><span data-stu-id="b854e-265">This alert gives information that enables you to identify the resource that was used to initiate this attack, the attacked resource, the victim IP, the attacker IP, and the detection time.</span></span>

> [!NOTE]
> <span data-ttu-id="b854e-266">Live IP addresses were removed from this screenshot for privacy purpose.</span><span class="sxs-lookup"><span data-stu-id="b854e-266">Live IP addresses were removed from this screenshot for privacy purpose.</span></span>
>
>

### <a name="possible-outgoing-denial-of-service-attack-detected"></a><span data-ttu-id="b854e-267">Possible outgoing denial-of-service attack detected</span><span class="sxs-lookup"><span data-stu-id="b854e-267">Possible outgoing denial-of-service attack detected</span></span>
<span data-ttu-id="b854e-268">Abnormal network traffic that originates from one virtual machine can cause Security Center to trigger a potential denial-of-service type of attack.</span><span class="sxs-lookup"><span data-stu-id="b854e-268">Abnormal network traffic that originates from one virtual machine can cause Security Center to trigger a potential denial-of-service type of attack.</span></span>

<span data-ttu-id="b854e-269">This is an example of this type of alert:</span><span class="sxs-lookup"><span data-stu-id="b854e-269">This is an example of this type of alert:</span></span>

![Outgoing DOS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-alerts-type/security-center-alerts-type-fig10-new.png)

## <a name="resource-analysis"></a><span data-ttu-id="b854e-271">Resource analysis</span><span class="sxs-lookup"><span data-stu-id="b854e-271">Resource analysis</span></span>
<span data-ttu-id="b854e-272">Security Center resource analysis focuses on platform as a service (PaaS) services, such as the integration with the [Azure SQL Database threat detection](../sql-database/sql-database-threat-detection.md) feature.</span><span class="sxs-lookup"><span data-stu-id="b854e-272">Security Center resource analysis focuses on platform as a service (PaaS) services, such as the integration with the [Azure SQL Database threat detection](../sql-database/sql-database-threat-detection.md) feature.</span></span> <span data-ttu-id="b854e-273">Based on the analysis’s results from these areas, Security Center triggers a resource-related alert.</span><span class="sxs-lookup"><span data-stu-id="b854e-273">Based on the analysis’s results from these areas, Security Center triggers a resource-related alert.</span></span>

### <a name="potential-sql-injection"></a><span data-ttu-id="b854e-274">Potential SQL injection</span><span class="sxs-lookup"><span data-stu-id="b854e-274">Potential SQL injection</span></span>
<span data-ttu-id="b854e-275">SQL injection is an attack where malicious code is inserted into strings that are later passed to an instance of SQL Server for parsing and execution.</span><span class="sxs-lookup"><span data-stu-id="b854e-275">SQL injection is an attack where malicious code is inserted into strings that are later passed to an instance of SQL Server for parsing and execution.</span></span> <span data-ttu-id="b854e-276">Because SQL Server executes all syntactically valid queries that it receives, any procedure that constructs SQL statements should be reviewed for injection vulnerabilities.</span><span class="sxs-lookup"><span data-stu-id="b854e-276">Because SQL Server executes all syntactically valid queries that it receives, any procedure that constructs SQL statements should be reviewed for injection vulnerabilities.</span></span> <span data-ttu-id="b854e-277">SQL Threat Detection uses machine learning, behavioral analysis, and anomaly detection to determine suspicious events that might be taking place in your Azure SQL databases.</span><span class="sxs-lookup"><span data-stu-id="b854e-277">SQL Threat Detection uses machine learning, behavioral analysis, and anomaly detection to determine suspicious events that might be taking place in your Azure SQL databases.</span></span> <span data-ttu-id="b854e-278">For example:</span><span class="sxs-lookup"><span data-stu-id="b854e-278">For example:</span></span>

* <span data-ttu-id="b854e-279">Attempted database access by a former employee</span><span class="sxs-lookup"><span data-stu-id="b854e-279">Attempted database access by a former employee</span></span>
* <span data-ttu-id="b854e-280">SQL injection attacks</span><span class="sxs-lookup"><span data-stu-id="b854e-280">SQL injection attacks</span></span>
* <span data-ttu-id="b854e-281">Unusual access to a production database from a user at home</span><span class="sxs-lookup"><span data-stu-id="b854e-281">Unusual access to a production database from a user at home</span></span>

![Potential SQL Injection alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-alerts-type/security-center-alerts-type-fig11.png)

<span data-ttu-id="b854e-283">The information in this alert can be used to identify the attacked resource, the detection time, and the state of the attack.</span><span class="sxs-lookup"><span data-stu-id="b854e-283">The information in this alert can be used to identify the attacked resource, the detection time, and the state of the attack.</span></span> <span data-ttu-id="b854e-284">It also provides a link to further investigation steps.</span><span class="sxs-lookup"><span data-stu-id="b854e-284">It also provides a link to further investigation steps.</span></span>

### <a name="vulnerability-to-sql-injection"></a><span data-ttu-id="b854e-285">Vulnerability to SQL Injection</span><span class="sxs-lookup"><span data-stu-id="b854e-285">Vulnerability to SQL Injection</span></span>
<span data-ttu-id="b854e-286">This alert is triggered when an application error is detected on a database.</span><span class="sxs-lookup"><span data-stu-id="b854e-286">This alert is triggered when an application error is detected on a database.</span></span> <span data-ttu-id="b854e-287">This alert may indicate a possible vulnerability to SQL injection attacks.</span><span class="sxs-lookup"><span data-stu-id="b854e-287">This alert may indicate a possible vulnerability to SQL injection attacks.</span></span>

![Potential SQL Injection alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-alerts-type/security-center-alerts-type-fig12-new.png)

### <a name="unusual-access-from-unfamiliar-location"></a><span data-ttu-id="b854e-289">Unusual access from unfamiliar location</span><span class="sxs-lookup"><span data-stu-id="b854e-289">Unusual access from unfamiliar location</span></span>
<span data-ttu-id="b854e-290">This alert is triggered when an access event from an unfamiliar IP address was detected on the server, which was not seen in the last period.</span><span class="sxs-lookup"><span data-stu-id="b854e-290">This alert is triggered when an access event from an unfamiliar IP address was detected on the server, which was not seen in the last period.</span></span>

![Unusual access alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-alerts-type/security-center-alerts-type-fig13-new.png)

## <a name="see-also"></a><span data-ttu-id="b854e-292">See also</span><span class="sxs-lookup"><span data-stu-id="b854e-292">See also</span></span>
<span data-ttu-id="b854e-293">In this article, you learned about the different types of security alerts in Security Center.</span><span class="sxs-lookup"><span data-stu-id="b854e-293">In this article, you learned about the different types of security alerts in Security Center.</span></span> <span data-ttu-id="b854e-294">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="b854e-294">To learn more about Security Center, see the following:</span></span>

* [<span data-ttu-id="b854e-295">Handling security incident in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="b854e-295">Handling security incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="b854e-296">Azure Security Center detection capabilities</span><span class="sxs-lookup"><span data-stu-id="b854e-296">Azure Security Center detection capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="b854e-297">Azure Security Center planning and operations guide</span><span class="sxs-lookup"><span data-stu-id="b854e-297">Azure Security Center planning and operations guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="b854e-298">[Azure Security Center FAQ](security-center-faq.md): Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="b854e-298">[Azure Security Center FAQ](security-center-faq.md): Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="b854e-299">[Azure security blog](http://blogs.msdn.com/b/azuresecurity/): Find blog posts about Azure security and compliance.</span><span class="sxs-lookup"><span data-stu-id="b854e-299">[Azure security blog](http://blogs.msdn.com/b/azuresecurity/): Find blog posts about Azure security and compliance.</span></span>



















