---
title: Troubleshooting and logging in Azure AD password protection preview
description: Understand Azure AD password protection preview logging and common troubleshooting
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: jsimmons
ms.openlocfilehash: 1eea6380d4276644db0c7681f23a4b0c5e79ff09
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864443"
---
# <a name="preview-azure-ad-password-protection-monitoring-reporting-and-troubleshooting"></a><span data-ttu-id="b46b9-103">Preview: Azure AD password protection monitoring, reporting, and troubleshooting</span><span class="sxs-lookup"><span data-stu-id="b46b9-103">Preview: Azure AD password protection monitoring, reporting, and troubleshooting</span></span>

|     |
| --- |
| <span data-ttu-id="b46b9-104">Azure AD password protection and the custom banned password list are public preview features of Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b46b9-104">Azure AD password protection and the custom banned password list are public preview features of Azure Active Directory.</span></span> <span data-ttu-id="b46b9-105">For more information about previews, see  [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)</span><span class="sxs-lookup"><span data-stu-id="b46b9-105">For more information about previews, see  [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)</span></span>|
|     |

<span data-ttu-id="b46b9-106">After deployment of Azure AD password protection monitoring and reporting are essential tasks.</span><span class="sxs-lookup"><span data-stu-id="b46b9-106">After deployment of Azure AD password protection monitoring and reporting are essential tasks.</span></span> <span data-ttu-id="b46b9-107">This article goes into detail to help you understand where each service logs information and how to report on the use of Azure AD password protection.</span><span class="sxs-lookup"><span data-stu-id="b46b9-107">This article goes into detail to help you understand where each service logs information and how to report on the use of Azure AD password protection.</span></span>

## <a name="on-premises-logs-and-events"></a><span data-ttu-id="b46b9-108">On-premises logs and events</span><span class="sxs-lookup"><span data-stu-id="b46b9-108">On-premises logs and events</span></span>

### <a name="dc-agent-service"></a><span data-ttu-id="b46b9-109">DC agent service</span><span class="sxs-lookup"><span data-stu-id="b46b9-109">DC agent service</span></span>

<span data-ttu-id="b46b9-110">On each domain controller, the DC agent service software writes the results of its password validations (and other status) to a local event log: \Applications and Services Logs\Microsoft\AzureADPasswordProtection\DCAgent\Admin</span><span class="sxs-lookup"><span data-stu-id="b46b9-110">On each domain controller, the DC agent service software writes the results of its password validations (and other status) to a local event log: \Applications and Services Logs\Microsoft\AzureADPasswordProtection\DCAgent\Admin</span></span>

<span data-ttu-id="b46b9-111">Events are logged by the various DC agent components using the following ranges:</span><span class="sxs-lookup"><span data-stu-id="b46b9-111">Events are logged by the various DC agent components using the following ranges:</span></span>

|<span data-ttu-id="b46b9-112">Component</span><span class="sxs-lookup"><span data-stu-id="b46b9-112">Component</span></span> |<span data-ttu-id="b46b9-113">Event ID range</span><span class="sxs-lookup"><span data-stu-id="b46b9-113">Event ID range</span></span>|
| --- | --- |
|<span data-ttu-id="b46b9-114">DC Agent password filter dll</span><span class="sxs-lookup"><span data-stu-id="b46b9-114">DC Agent password filter dll</span></span>| <span data-ttu-id="b46b9-115">10000-19999</span><span class="sxs-lookup"><span data-stu-id="b46b9-115">10000-19999</span></span>|
|<span data-ttu-id="b46b9-116">DC agent service hosting process</span><span class="sxs-lookup"><span data-stu-id="b46b9-116">DC agent service hosting process</span></span>| <span data-ttu-id="b46b9-117">20000-29999</span><span class="sxs-lookup"><span data-stu-id="b46b9-117">20000-29999</span></span>|
|<span data-ttu-id="b46b9-118">DC agent service policy validation logic</span><span class="sxs-lookup"><span data-stu-id="b46b9-118">DC agent service policy validation logic</span></span>| <span data-ttu-id="b46b9-119">30000-39999</span><span class="sxs-lookup"><span data-stu-id="b46b9-119">30000-39999</span></span>|

<span data-ttu-id="b46b9-120">For a successful password validation operation, there is generally one event logged from the DC agent password filter dll.</span><span class="sxs-lookup"><span data-stu-id="b46b9-120">For a successful password validation operation, there is generally one event logged from the DC agent password filter dll.</span></span> <span data-ttu-id="b46b9-121">For a failing password validation operation, there are generally two events logged, one from the DC agent service, and one from the DC Agent password filter dll.</span><span class="sxs-lookup"><span data-stu-id="b46b9-121">For a failing password validation operation, there are generally two events logged, one from the DC agent service, and one from the DC Agent password filter dll.</span></span>

<span data-ttu-id="b46b9-122">Discrete events to capture these situations are logged, based around the following factors:</span><span class="sxs-lookup"><span data-stu-id="b46b9-122">Discrete events to capture these situations are logged, based around the following factors:</span></span>

* <span data-ttu-id="b46b9-123">Whether a given password is being set or changed.</span><span class="sxs-lookup"><span data-stu-id="b46b9-123">Whether a given password is being set or changed.</span></span>
* <span data-ttu-id="b46b9-124">Whether validation of a given password passed or failed.</span><span class="sxs-lookup"><span data-stu-id="b46b9-124">Whether validation of a given password passed or failed.</span></span>
* <span data-ttu-id="b46b9-125">Whether validation failed due to the Microsoft global policy vs the organizational policy.</span><span class="sxs-lookup"><span data-stu-id="b46b9-125">Whether validation failed due to the Microsoft global policy vs the organizational policy.</span></span>
* <span data-ttu-id="b46b9-126">Whether audit only mode is currently on or off for the current password policy.</span><span class="sxs-lookup"><span data-stu-id="b46b9-126">Whether audit only mode is currently on or off for the current password policy.</span></span>

<span data-ttu-id="b46b9-127">The key password-validation-related events are as follows:</span><span class="sxs-lookup"><span data-stu-id="b46b9-127">The key password-validation-related events are as follows:</span></span>

|   |<span data-ttu-id="b46b9-128">Password change</span><span class="sxs-lookup"><span data-stu-id="b46b9-128">Password change</span></span> |<span data-ttu-id="b46b9-129">Password set</span><span class="sxs-lookup"><span data-stu-id="b46b9-129">Password set</span></span>|
| --- | :---: | :---: |
|<span data-ttu-id="b46b9-130">Pass</span><span class="sxs-lookup"><span data-stu-id="b46b9-130">Pass</span></span> |<span data-ttu-id="b46b9-131">10014</span><span class="sxs-lookup"><span data-stu-id="b46b9-131">10014</span></span> |<span data-ttu-id="b46b9-132">10015</span><span class="sxs-lookup"><span data-stu-id="b46b9-132">10015</span></span>|
|<span data-ttu-id="b46b9-133">Fail (did not pass customer password policy)</span><span class="sxs-lookup"><span data-stu-id="b46b9-133">Fail (did not pass customer password policy)</span></span>| <span data-ttu-id="b46b9-134">10016, 30002</span><span class="sxs-lookup"><span data-stu-id="b46b9-134">10016, 30002</span></span>| <span data-ttu-id="b46b9-135">10017, 30003</span><span class="sxs-lookup"><span data-stu-id="b46b9-135">10017, 30003</span></span>|
|<span data-ttu-id="b46b9-136">Fail (did not pass Microsoft password policy)</span><span class="sxs-lookup"><span data-stu-id="b46b9-136">Fail (did not pass Microsoft password policy)</span></span>| <span data-ttu-id="b46b9-137">10016, 30004</span><span class="sxs-lookup"><span data-stu-id="b46b9-137">10016, 30004</span></span>| <span data-ttu-id="b46b9-138">10017, 30005</span><span class="sxs-lookup"><span data-stu-id="b46b9-138">10017, 30005</span></span>|
|<span data-ttu-id="b46b9-139">Audit-only Pass (would have failed customer password policy)</span><span class="sxs-lookup"><span data-stu-id="b46b9-139">Audit-only Pass (would have failed customer password policy)</span></span>| <span data-ttu-id="b46b9-140">10024, 30008</span><span class="sxs-lookup"><span data-stu-id="b46b9-140">10024, 30008</span></span>| <span data-ttu-id="b46b9-141">10025, 30007</span><span class="sxs-lookup"><span data-stu-id="b46b9-141">10025, 30007</span></span>|
|<span data-ttu-id="b46b9-142">Audit-only Pass (would have failed Microsoft password policy)</span><span class="sxs-lookup"><span data-stu-id="b46b9-142">Audit-only Pass (would have failed Microsoft password policy)</span></span>| <span data-ttu-id="b46b9-143">10024, 30010</span><span class="sxs-lookup"><span data-stu-id="b46b9-143">10024, 30010</span></span>| <span data-ttu-id="b46b9-144">10025, 30009</span><span class="sxs-lookup"><span data-stu-id="b46b9-144">10025, 30009</span></span>|

> [!TIP]
> <span data-ttu-id="b46b9-145">Incoming passwords are validated against the Microsoft global password list first; if that fails, no further processing is performed.</span><span class="sxs-lookup"><span data-stu-id="b46b9-145">Incoming passwords are validated against the Microsoft global password list first; if that fails, no further processing is performed.</span></span> <span data-ttu-id="b46b9-146">This is the same behavior as performed on password changes in Azure.</span><span class="sxs-lookup"><span data-stu-id="b46b9-146">This is the same behavior as performed on password changes in Azure.</span></span>

#### <a name="sample-event-log-message-for-event-id-10014-successful-password-set"></a><span data-ttu-id="b46b9-147">Sample event log message for Event ID 10014 successful password set</span><span class="sxs-lookup"><span data-stu-id="b46b9-147">Sample event log message for Event ID 10014 successful password set</span></span>

<span data-ttu-id="b46b9-148">The changed password for the specified user was validated as compliant with the current Azure password policy.</span><span class="sxs-lookup"><span data-stu-id="b46b9-148">The changed password for the specified user was validated as compliant with the current Azure password policy.</span></span>

 <span data-ttu-id="b46b9-149">UserName: BPL_02885102771 FullName:</span><span class="sxs-lookup"><span data-stu-id="b46b9-149">UserName: BPL_02885102771 FullName:</span></span>

#### <a name="sample-event-log-message-for-event-id-10017-and-30003-failed-password-set"></a><span data-ttu-id="b46b9-150">Sample event log message for Event ID 10017 and 30003 failed password set</span><span class="sxs-lookup"><span data-stu-id="b46b9-150">Sample event log message for Event ID 10017 and 30003 failed password set</span></span>

<span data-ttu-id="b46b9-151">10017:</span><span class="sxs-lookup"><span data-stu-id="b46b9-151">10017:</span></span>

<span data-ttu-id="b46b9-152">The reset password for the specified user was rejected because it did not comply with the current Azure password policy.</span><span class="sxs-lookup"><span data-stu-id="b46b9-152">The reset password for the specified user was rejected because it did not comply with the current Azure password policy.</span></span> <span data-ttu-id="b46b9-153">Please see the correlated event log message for more details.</span><span class="sxs-lookup"><span data-stu-id="b46b9-153">Please see the correlated event log message for more details.</span></span>

 <span data-ttu-id="b46b9-154">UserName: BPL_03283841185 FullName:</span><span class="sxs-lookup"><span data-stu-id="b46b9-154">UserName: BPL_03283841185 FullName:</span></span>

<span data-ttu-id="b46b9-155">30003:</span><span class="sxs-lookup"><span data-stu-id="b46b9-155">30003:</span></span>

<span data-ttu-id="b46b9-156">The reset password for the specified user was rejected because it matched at least one of the tokens present in the per-tenant banned password list of the current Azure password policy.</span><span class="sxs-lookup"><span data-stu-id="b46b9-156">The reset password for the specified user was rejected because it matched at least one of the tokens present in the per-tenant banned password list of the current Azure password policy.</span></span>

 <span data-ttu-id="b46b9-157">UserName: BPL_03283841185 FullName:</span><span class="sxs-lookup"><span data-stu-id="b46b9-157">UserName: BPL_03283841185 FullName:</span></span>

<span data-ttu-id="b46b9-158">Some other key event log messages to be aware of are:</span><span class="sxs-lookup"><span data-stu-id="b46b9-158">Some other key event log messages to be aware of are:</span></span>

#### <a name="sample-event-log-message-for-event-id-30001"></a><span data-ttu-id="b46b9-159">Sample event log message for Event ID 30001</span><span class="sxs-lookup"><span data-stu-id="b46b9-159">Sample event log message for Event ID 30001</span></span>

<span data-ttu-id="b46b9-160">The password for the specified user was accepted because an Azure password policy is not available yet</span><span class="sxs-lookup"><span data-stu-id="b46b9-160">The password for the specified user was accepted because an Azure password policy is not available yet</span></span>

<span data-ttu-id="b46b9-161">UserName: <user> FullName: <user></span><span class="sxs-lookup"><span data-stu-id="b46b9-161">UserName: <user> FullName: <user></span></span>

<span data-ttu-id="b46b9-162">This condition may be caused by one or more of the following reasons:%n</span><span class="sxs-lookup"><span data-stu-id="b46b9-162">This condition may be caused by one or more of the following reasons:%n</span></span>

1. <span data-ttu-id="b46b9-163">The forest has not yet been registered with Azure.</span><span class="sxs-lookup"><span data-stu-id="b46b9-163">The forest has not yet been registered with Azure.</span></span>

   <span data-ttu-id="b46b9-164">Resolution steps: an administrator must register the forest using the Register-AzureADPasswordProtectionForest cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b46b9-164">Resolution steps: an administrator must register the forest using the Register-AzureADPasswordProtectionForest cmdlet.</span></span>

2. <span data-ttu-id="b46b9-165">An Azure AD password protection Proxy is not yet available on at least one machine in the current forest.</span><span class="sxs-lookup"><span data-stu-id="b46b9-165">An Azure AD password protection Proxy is not yet available on at least one machine in the current forest.</span></span>

   <span data-ttu-id="b46b9-166">Resolution steps: an administrator must install and register a proxy using the Register-AzureADPasswordProtectionProxy cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b46b9-166">Resolution steps: an administrator must install and register a proxy using the Register-AzureADPasswordProtectionProxy cmdlet.</span></span>

3. <span data-ttu-id="b46b9-167">This DC does not have network connectivity to any Azure AD password protection Proxy instances.</span><span class="sxs-lookup"><span data-stu-id="b46b9-167">This DC does not have network connectivity to any Azure AD password protection Proxy instances.</span></span>

   <span data-ttu-id="b46b9-168">Resolution steps: ensure network connectivity exists to at least one Azure AD password protection Proxy instance.</span><span class="sxs-lookup"><span data-stu-id="b46b9-168">Resolution steps: ensure network connectivity exists to at least one Azure AD password protection Proxy instance.</span></span>

4. <span data-ttu-id="b46b9-169">This DC does not have connectivity to other domain controllers in the domain.</span><span class="sxs-lookup"><span data-stu-id="b46b9-169">This DC does not have connectivity to other domain controllers in the domain.</span></span>

   <span data-ttu-id="b46b9-170">Resolution steps: ensure network connectivity exists to the domain.</span><span class="sxs-lookup"><span data-stu-id="b46b9-170">Resolution steps: ensure network connectivity exists to the domain.</span></span>

#### <a name="sample-event-log-message-for-event-id-30006"></a><span data-ttu-id="b46b9-171">Sample event log message for Event ID 30006</span><span class="sxs-lookup"><span data-stu-id="b46b9-171">Sample event log message for Event ID 30006</span></span>

<span data-ttu-id="b46b9-172">The service is now enforcing the following Azure password policy.</span><span class="sxs-lookup"><span data-stu-id="b46b9-172">The service is now enforcing the following Azure password policy.</span></span>

 <span data-ttu-id="b46b9-173">AuditOnly: 1</span><span class="sxs-lookup"><span data-stu-id="b46b9-173">AuditOnly: 1</span></span>

 <span data-ttu-id="b46b9-174">Global policy date: ‎2018‎-‎05‎-‎15T00:00:00.000000000Z</span><span class="sxs-lookup"><span data-stu-id="b46b9-174">Global policy date: ‎2018‎-‎05‎-‎15T00:00:00.000000000Z</span></span>

 <span data-ttu-id="b46b9-175">Tenant policy date: ‎2018‎-‎06‎-‎10T20:15:24.432457600Z</span><span class="sxs-lookup"><span data-stu-id="b46b9-175">Tenant policy date: ‎2018‎-‎06‎-‎10T20:15:24.432457600Z</span></span>

 <span data-ttu-id="b46b9-176">Enforce tenant policy: 1</span><span class="sxs-lookup"><span data-stu-id="b46b9-176">Enforce tenant policy: 1</span></span>

#### <a name="dc-agent-log-locations"></a><span data-ttu-id="b46b9-177">DC Agent log locations</span><span class="sxs-lookup"><span data-stu-id="b46b9-177">DC Agent log locations</span></span>

<span data-ttu-id="b46b9-178">The DC agent service will also log operational-related events to the following log: \Applications and Services Logs\Microsoft\AzureADPasswordProtection\DCAgent\Operational</span><span class="sxs-lookup"><span data-stu-id="b46b9-178">The DC agent service will also log operational-related events to the following log: \Applications and Services Logs\Microsoft\AzureADPasswordProtection\DCAgent\Operational</span></span>

<span data-ttu-id="b46b9-179">The DC agent service can also log verbose debug-level trace events to the following log: \Applications and Services Logs\Microsoft\AzureADPasswordProtection\DCAgent\Trace</span><span class="sxs-lookup"><span data-stu-id="b46b9-179">The DC agent service can also log verbose debug-level trace events to the following log: \Applications and Services Logs\Microsoft\AzureADPasswordProtection\DCAgent\Trace</span></span>

> [!WARNING]
> <span data-ttu-id="b46b9-180">The Trace log is disabled by default.</span><span class="sxs-lookup"><span data-stu-id="b46b9-180">The Trace log is disabled by default.</span></span> <span data-ttu-id="b46b9-181">When enabled, this log receives a high volume of events and may impact domain controller performance.</span><span class="sxs-lookup"><span data-stu-id="b46b9-181">When enabled, this log receives a high volume of events and may impact domain controller performance.</span></span> <span data-ttu-id="b46b9-182">Therefore, this enhanced log should only be enabled when a problem requires deeper investigation, and then only for a minimal amount of time.</span><span class="sxs-lookup"><span data-stu-id="b46b9-182">Therefore, this enhanced log should only be enabled when a problem requires deeper investigation, and then only for a minimal amount of time.</span></span>

### <a name="azure-ad-password-protection-proxy-service"></a><span data-ttu-id="b46b9-183">Azure AD password protection proxy service</span><span class="sxs-lookup"><span data-stu-id="b46b9-183">Azure AD password protection proxy service</span></span>

<span data-ttu-id="b46b9-184">The password protection Proxy service emits a minimal set of events to the following event log: \Applications and Services Logs\Microsoft\AzureADPasswordProtection\ProxyService\Operational</span><span class="sxs-lookup"><span data-stu-id="b46b9-184">The password protection Proxy service emits a minimal set of events to the following event log: \Applications and Services Logs\Microsoft\AzureADPasswordProtection\ProxyService\Operational</span></span>

<span data-ttu-id="b46b9-185">The password protection Proxy service can also log verbose debug-level trace events to the following log: \Applications and Services Logs\Microsoft\AzureADPasswordProtection\ProxyService\Trace</span><span class="sxs-lookup"><span data-stu-id="b46b9-185">The password protection Proxy service can also log verbose debug-level trace events to the following log: \Applications and Services Logs\Microsoft\AzureADPasswordProtection\ProxyService\Trace</span></span>

> [!WARNING]
> <span data-ttu-id="b46b9-186">The Trace log is disabled by default.</span><span class="sxs-lookup"><span data-stu-id="b46b9-186">The Trace log is disabled by default.</span></span> <span data-ttu-id="b46b9-187">When enabled, this log receives a high volume of events and this may impact performance of the proxy host.</span><span class="sxs-lookup"><span data-stu-id="b46b9-187">When enabled, this log receives a high volume of events and this may impact performance of the proxy host.</span></span> <span data-ttu-id="b46b9-188">Therefore, this log should only be enabled when a problem requires deeper investigation, and then only for a minimal amount of time.</span><span class="sxs-lookup"><span data-stu-id="b46b9-188">Therefore, this log should only be enabled when a problem requires deeper investigation, and then only for a minimal amount of time.</span></span>

### <a name="dc-agent-discovery"></a><span data-ttu-id="b46b9-189">DC Agent discovery</span><span class="sxs-lookup"><span data-stu-id="b46b9-189">DC Agent discovery</span></span>

<span data-ttu-id="b46b9-190">The `Get-AzureADPasswordProtectionDCAgent` cmdlet may be used to display basic information about the various DC agents running in a domain or forest.</span><span class="sxs-lookup"><span data-stu-id="b46b9-190">The `Get-AzureADPasswordProtectionDCAgent` cmdlet may be used to display basic information about the various DC agents running in a domain or forest.</span></span> <span data-ttu-id="b46b9-191">This information is retrieved from the serviceConnectionPoint object(s) registered by the running DC agent service(s).</span><span class="sxs-lookup"><span data-stu-id="b46b9-191">This information is retrieved from the serviceConnectionPoint object(s) registered by the running DC agent service(s).</span></span> <span data-ttu-id="b46b9-192">An example output of this cmdlet is as follows:</span><span class="sxs-lookup"><span data-stu-id="b46b9-192">An example output of this cmdlet is as follows:</span></span>

```
PS C:\> Get-AzureADPasswordProtectionDCAgent
ServerFQDN            : bplChildDC2.bplchild.bplRootDomain.com
Domain                : bplchild.bplRootDomain.com
Forest                : bplRootDomain.com
Heartbeat             : 2/16/2018 8:35:01 AM
```

<span data-ttu-id="b46b9-193">The various properties are updated by each DC agent service on an approximate hourly basis.</span><span class="sxs-lookup"><span data-stu-id="b46b9-193">The various properties are updated by each DC agent service on an approximate hourly basis.</span></span> <span data-ttu-id="b46b9-194">The data is still subject to Active Directory replication latency.</span><span class="sxs-lookup"><span data-stu-id="b46b9-194">The data is still subject to Active Directory replication latency.</span></span>

<span data-ttu-id="b46b9-195">The scope of the cmdlet’s query may be influenced using either the –Forest or –Domain parameters.</span><span class="sxs-lookup"><span data-stu-id="b46b9-195">The scope of the cmdlet’s query may be influenced using either the –Forest or –Domain parameters.</span></span>

### <a name="emergency-remediation"></a><span data-ttu-id="b46b9-196">Emergency remediation</span><span class="sxs-lookup"><span data-stu-id="b46b9-196">Emergency remediation</span></span>

<span data-ttu-id="b46b9-197">If an unfortunate situation occurs where the DC agent service is causing problems, the DC agent service may be immediately shut down.</span><span class="sxs-lookup"><span data-stu-id="b46b9-197">If an unfortunate situation occurs where the DC agent service is causing problems, the DC agent service may be immediately shut down.</span></span> <span data-ttu-id="b46b9-198">The DC agent password filter dll attempts to call the non-running service and will log warning events (10012, 10013), but all incoming passwords are accepted during that time.</span><span class="sxs-lookup"><span data-stu-id="b46b9-198">The DC agent password filter dll attempts to call the non-running service and will log warning events (10012, 10013), but all incoming passwords are accepted during that time.</span></span> <span data-ttu-id="b46b9-199">The DC agent service may then also be configured via the Windows Service Control Manager with a startup type of “Disabled” as needed.</span><span class="sxs-lookup"><span data-stu-id="b46b9-199">The DC agent service may then also be configured via the Windows Service Control Manager with a startup type of “Disabled” as needed.</span></span>

### <a name="performance-monitoring"></a><span data-ttu-id="b46b9-200">Performance monitoring</span><span class="sxs-lookup"><span data-stu-id="b46b9-200">Performance monitoring</span></span>

<span data-ttu-id="b46b9-201">The DC agent service software installs a performance counter object named **Azure AD password protection**.</span><span class="sxs-lookup"><span data-stu-id="b46b9-201">The DC agent service software installs a performance counter object named **Azure AD password protection**.</span></span> <span data-ttu-id="b46b9-202">The following perf counters are currently available:</span><span class="sxs-lookup"><span data-stu-id="b46b9-202">The following perf counters are currently available:</span></span>

|<span data-ttu-id="b46b9-203">Perf counter name</span><span class="sxs-lookup"><span data-stu-id="b46b9-203">Perf counter name</span></span> | <span data-ttu-id="b46b9-204">Description</span><span class="sxs-lookup"><span data-stu-id="b46b9-204">Description</span></span>|
| --- | --- |
|<span data-ttu-id="b46b9-205">Passwords processed</span><span class="sxs-lookup"><span data-stu-id="b46b9-205">Passwords processed</span></span> |<span data-ttu-id="b46b9-206">This counter displays the total number of passwords processed (accepted or rejected) since last restart.</span><span class="sxs-lookup"><span data-stu-id="b46b9-206">This counter displays the total number of passwords processed (accepted or rejected) since last restart.</span></span>|
|<span data-ttu-id="b46b9-207">Passwords accepted</span><span class="sxs-lookup"><span data-stu-id="b46b9-207">Passwords accepted</span></span> |<span data-ttu-id="b46b9-208">This counter displays the total number of passwords that were accepted since last restart.</span><span class="sxs-lookup"><span data-stu-id="b46b9-208">This counter displays the total number of passwords that were accepted since last restart.</span></span>|
|<span data-ttu-id="b46b9-209">Passwords rejected</span><span class="sxs-lookup"><span data-stu-id="b46b9-209">Passwords rejected</span></span> |<span data-ttu-id="b46b9-210">This counter displays the total number of passwords that were rejected since last restart.</span><span class="sxs-lookup"><span data-stu-id="b46b9-210">This counter displays the total number of passwords that were rejected since last restart.</span></span>|
|<span data-ttu-id="b46b9-211">Password filter requests in progress</span><span class="sxs-lookup"><span data-stu-id="b46b9-211">Password filter requests in progress</span></span> |<span data-ttu-id="b46b9-212">This counter displays the number of password filter requests currently in progress.</span><span class="sxs-lookup"><span data-stu-id="b46b9-212">This counter displays the number of password filter requests currently in progress.</span></span>|
|<span data-ttu-id="b46b9-213">Peak password filter requests</span><span class="sxs-lookup"><span data-stu-id="b46b9-213">Peak password filter requests</span></span> |<span data-ttu-id="b46b9-214">This counter displays the peak number of concurrent password filter requests since the last restart.</span><span class="sxs-lookup"><span data-stu-id="b46b9-214">This counter displays the peak number of concurrent password filter requests since the last restart.</span></span>|
|<span data-ttu-id="b46b9-215">Password filter request errors</span><span class="sxs-lookup"><span data-stu-id="b46b9-215">Password filter request errors</span></span> |<span data-ttu-id="b46b9-216">This counter displays the total number of password filter requests that failed due to an error since last restart.</span><span class="sxs-lookup"><span data-stu-id="b46b9-216">This counter displays the total number of password filter requests that failed due to an error since last restart.</span></span> <span data-ttu-id="b46b9-217">Errors can occur when the Azure AD password protection DC agent service is not running.</span><span class="sxs-lookup"><span data-stu-id="b46b9-217">Errors can occur when the Azure AD password protection DC agent service is not running.</span></span>|
|<span data-ttu-id="b46b9-218">Password filter requests/sec</span><span class="sxs-lookup"><span data-stu-id="b46b9-218">Password filter requests/sec</span></span> |<span data-ttu-id="b46b9-219">This counter displays the rate at which passwords are being processed.</span><span class="sxs-lookup"><span data-stu-id="b46b9-219">This counter displays the rate at which passwords are being processed.</span></span>|
|<span data-ttu-id="b46b9-220">Password filter request processing time</span><span class="sxs-lookup"><span data-stu-id="b46b9-220">Password filter request processing time</span></span> |<span data-ttu-id="b46b9-221">This counter displays the average time required to process a password filter request.</span><span class="sxs-lookup"><span data-stu-id="b46b9-221">This counter displays the average time required to process a password filter request.</span></span>|
|<span data-ttu-id="b46b9-222">Peak password filter request processing time</span><span class="sxs-lookup"><span data-stu-id="b46b9-222">Peak password filter request processing time</span></span> |<span data-ttu-id="b46b9-223">This counter displays the peak password filter request processing time since the last restart.</span><span class="sxs-lookup"><span data-stu-id="b46b9-223">This counter displays the peak password filter request processing time since the last restart.</span></span>|
|<span data-ttu-id="b46b9-224">Passwords accepted due to audit mode</span><span class="sxs-lookup"><span data-stu-id="b46b9-224">Passwords accepted due to audit mode</span></span> |<span data-ttu-id="b46b9-225">This counter displays the total number of passwords that would normally have been rejected, but were accepted because the password policy was configured to be in audit-mode (since last restart).</span><span class="sxs-lookup"><span data-stu-id="b46b9-225">This counter displays the total number of passwords that would normally have been rejected, but were accepted because the password policy was configured to be in audit-mode (since last restart).</span></span>|

## <a name="directory-services-repair-mode"></a><span data-ttu-id="b46b9-226">Directory Services Repair Mode</span><span class="sxs-lookup"><span data-stu-id="b46b9-226">Directory Services Repair Mode</span></span>

<span data-ttu-id="b46b9-227">If the domain controller is booted into Directory Services Repair Mode, the DC agent service detects this causing all password validation or enforcement activities to be disabled, regardless of the currently active policy configuration.</span><span class="sxs-lookup"><span data-stu-id="b46b9-227">If the domain controller is booted into Directory Services Repair Mode, the DC agent service detects this causing all password validation or enforcement activities to be disabled, regardless of the currently active policy configuration.</span></span>

## <a name="domain-controller-demotion"></a><span data-ttu-id="b46b9-228">Domain controller demotion</span><span class="sxs-lookup"><span data-stu-id="b46b9-228">Domain controller demotion</span></span>

<span data-ttu-id="b46b9-229">It is supported to demote a domain controller that is still running the DC agent software.</span><span class="sxs-lookup"><span data-stu-id="b46b9-229">It is supported to demote a domain controller that is still running the DC agent software.</span></span> <span data-ttu-id="b46b9-230">Administrators should be aware however that the DC agent software keeps running and continues enforcing the current password policy during the demotion procedure.</span><span class="sxs-lookup"><span data-stu-id="b46b9-230">Administrators should be aware however that the DC agent software keeps running and continues enforcing the current password policy during the demotion procedure.</span></span> <span data-ttu-id="b46b9-231">The new local Administrator account password (specified as part of the demotion operation) is validated like any other password.</span><span class="sxs-lookup"><span data-stu-id="b46b9-231">The new local Administrator account password (specified as part of the demotion operation) is validated like any other password.</span></span> <span data-ttu-id="b46b9-232">Microsoft recommends that secure passwords be chosen for local Administrator accounts as part of a DC demotion procedure; however the validation of the new local Administrator account password by the DC agent software may be disruptive to pre-existing demotion operational procedures.</span><span class="sxs-lookup"><span data-stu-id="b46b9-232">Microsoft recommends that secure passwords be chosen for local Administrator accounts as part of a DC demotion procedure; however the validation of the new local Administrator account password by the DC agent software may be disruptive to pre-existing demotion operational procedures.</span></span>
<span data-ttu-id="b46b9-233">Once the demotion has succeeded, and the domain controller has been rebooted and is again running as a normal member server, the DC agent software reverts to running in a passive mode.</span><span class="sxs-lookup"><span data-stu-id="b46b9-233">Once the demotion has succeeded, and the domain controller has been rebooted and is again running as a normal member server, the DC agent software reverts to running in a passive mode.</span></span> <span data-ttu-id="b46b9-234">It may then be uninstalled at any time.</span><span class="sxs-lookup"><span data-stu-id="b46b9-234">It may then be uninstalled at any time.</span></span>

## <a name="removal"></a><span data-ttu-id="b46b9-235">Removal</span><span class="sxs-lookup"><span data-stu-id="b46b9-235">Removal</span></span>

<span data-ttu-id="b46b9-236">If it is decided to uninstall the public preview software and cleanup all related state from the domain(s) and forest, this task can be accomplished using the following steps:</span><span class="sxs-lookup"><span data-stu-id="b46b9-236">If it is decided to uninstall the public preview software and cleanup all related state from the domain(s) and forest, this task can be accomplished using the following steps:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b46b9-237">It is important to perform these steps in order.</span><span class="sxs-lookup"><span data-stu-id="b46b9-237">It is important to perform these steps in order.</span></span> <span data-ttu-id="b46b9-238">If any instance of the password protection Proxy service is left running it will periodically re-create its serviceConnectionPoint object as well as periodically re-create the sysvol state.</span><span class="sxs-lookup"><span data-stu-id="b46b9-238">If any instance of the password protection Proxy service is left running it will periodically re-create its serviceConnectionPoint object as well as periodically re-create the sysvol state.</span></span>

1. <span data-ttu-id="b46b9-239">Uninstall the password protection Proxy software from all machines.</span><span class="sxs-lookup"><span data-stu-id="b46b9-239">Uninstall the password protection Proxy software from all machines.</span></span> <span data-ttu-id="b46b9-240">This step does **not** require a reboot.</span><span class="sxs-lookup"><span data-stu-id="b46b9-240">This step does **not** require a reboot.</span></span>
2. <span data-ttu-id="b46b9-241">Uninstall the DC Agent software from all domain controllers.</span><span class="sxs-lookup"><span data-stu-id="b46b9-241">Uninstall the DC Agent software from all domain controllers.</span></span> <span data-ttu-id="b46b9-242">This step **requires** a reboot.</span><span class="sxs-lookup"><span data-stu-id="b46b9-242">This step **requires** a reboot.</span></span>
3. <span data-ttu-id="b46b9-243">Manually remove all proxy service connection points in each domain naming context.</span><span class="sxs-lookup"><span data-stu-id="b46b9-243">Manually remove all proxy service connection points in each domain naming context.</span></span> <span data-ttu-id="b46b9-244">The location of these objects may be discovered with the following Active Directory Powershell command:</span><span class="sxs-lookup"><span data-stu-id="b46b9-244">The location of these objects may be discovered with the following Active Directory Powershell command:</span></span>
   ```
   $scp = “serviceConnectionPoint”
   $keywords = “{EBEFB703-6113-413D-9167-9F8DD4D24468}*”
   Get-ADObject -SearchScope Subtree -Filter { objectClass -eq $scp -and keywords -like $keywords }
   ```

   <span data-ttu-id="b46b9-245">Do not omit the asterisk (“\*”) at the end of the $keywords variable value.</span><span class="sxs-lookup"><span data-stu-id="b46b9-245">Do not omit the asterisk (“\*”) at the end of the $keywords variable value.</span></span>

   <span data-ttu-id="b46b9-246">The resulting object found via the `Get-ADObject` command can then be piped to `Remove-ADObject`, or deleted manually.</span><span class="sxs-lookup"><span data-stu-id="b46b9-246">The resulting object found via the `Get-ADObject` command can then be piped to `Remove-ADObject`, or deleted manually.</span></span> 

4. <span data-ttu-id="b46b9-247">Manually remove all DC agent connection points in each domain naming context.</span><span class="sxs-lookup"><span data-stu-id="b46b9-247">Manually remove all DC agent connection points in each domain naming context.</span></span> <span data-ttu-id="b46b9-248">There may be one these objects per domain controller in the forest, depending on how widely the public preview software was deployed.</span><span class="sxs-lookup"><span data-stu-id="b46b9-248">There may be one these objects per domain controller in the forest, depending on how widely the public preview software was deployed.</span></span> <span data-ttu-id="b46b9-249">The location of that object may be discovered with the following Active Directory Powershell command:</span><span class="sxs-lookup"><span data-stu-id="b46b9-249">The location of that object may be discovered with the following Active Directory Powershell command:</span></span>

   ```
   $scp = “serviceConnectionPoint”
   $keywords = “{B11BB10A-3E7D-4D37-A4C3-51DE9D0F77C9}*”
   Get-ADObject -SearchScope Subtree -Filter { objectClass -eq $scp -and keywords -like $keywords }
   ```

   <span data-ttu-id="b46b9-250">The resulting object found via the `Get-ADObject` command can then be piped to `Remove-ADObject`, or deleted manually.</span><span class="sxs-lookup"><span data-stu-id="b46b9-250">The resulting object found via the `Get-ADObject` command can then be piped to `Remove-ADObject`, or deleted manually.</span></span>

5. <span data-ttu-id="b46b9-251">Manually remove the forest-level configuration state.</span><span class="sxs-lookup"><span data-stu-id="b46b9-251">Manually remove the forest-level configuration state.</span></span> <span data-ttu-id="b46b9-252">The forest configuration state is maintained in a container in the Active Directory configuration naming context.</span><span class="sxs-lookup"><span data-stu-id="b46b9-252">The forest configuration state is maintained in a container in the Active Directory configuration naming context.</span></span> <span data-ttu-id="b46b9-253">It can be discovered and deleted as follows:</span><span class="sxs-lookup"><span data-stu-id="b46b9-253">It can be discovered and deleted as follows:</span></span>

   ```
   $passwordProtectonConfigContainer = "CN=Azure AD password protection,CN=Services," + (Get-ADRootDSE).configurationNamingContext
   Remove-ADObject $passwordProtectonConfigContainer
   ```

6. <span data-ttu-id="b46b9-254">Manually remove all sysvol related state by manually deleting the following folder and all of its contents:</span><span class="sxs-lookup"><span data-stu-id="b46b9-254">Manually remove all sysvol related state by manually deleting the following folder and all of its contents:</span></span>

   `\\<domain>\sysvol\<domain fqdn>\Policies\{4A9AB66B-4365-4C2A-996C-58ED9927332D}`

   <span data-ttu-id="b46b9-255">If necessary, this path may also be accessed locally on a given domain controller; the default location would be something like the following path:</span><span class="sxs-lookup"><span data-stu-id="b46b9-255">If necessary, this path may also be accessed locally on a given domain controller; the default location would be something like the following path:</span></span>

   `%windir%\sysvol\domain\Policies\{4A9AB66B-4365-4C2A-996C-58ED9927332D}`

   <span data-ttu-id="b46b9-256">This path is different if the sysvol share has been configured in a non-default location.</span><span class="sxs-lookup"><span data-stu-id="b46b9-256">This path is different if the sysvol share has been configured in a non-default location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b46b9-257">Next steps</span><span class="sxs-lookup"><span data-stu-id="b46b9-257">Next steps</span></span>

<span data-ttu-id="b46b9-258">For more information on the global and custom banned password lists, see the article [Ban bad passwords](concept-password-ban-bad.md)</span><span class="sxs-lookup"><span data-stu-id="b46b9-258">For more information on the global and custom banned password lists, see the article [Ban bad passwords](concept-password-ban-bad.md)</span></span>
