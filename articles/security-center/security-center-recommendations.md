---
title: Managing security recommendations in Azure Security Center  | Microsoft Docs
description: This document walks you through how recommendations in Azure Security Center help you protect your Azure resources and stay in compliance with security policies.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 86c50c9f-eb6b-4d97-acb3-6d599c06133e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/03/2017
ms.author: terrylan
ms.openlocfilehash: 9d4ec8e0be7747d786d1a9a2531e0591f4a5647a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556732"
---
# <a name="managing-security-recommendations-in-azure-security-center"></a><span data-ttu-id="a4099-103">Managing security recommendations in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="a4099-103">Managing security recommendations in Azure Security Center</span></span>
<span data-ttu-id="a4099-104">This document walks you through how to use recommendations in Azure Security Center to help you protect your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="a4099-104">This document walks you through how to use recommendations in Azure Security Center to help you protect your Azure resources.</span></span>

> [!NOTE]
> <span data-ttu-id="a4099-105">This document introduces the service by using an example deployment.</span><span class="sxs-lookup"><span data-stu-id="a4099-105">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="a4099-106">This document is not a step-by-step guide.</span><span class="sxs-lookup"><span data-stu-id="a4099-106">This document is not a step-by-step guide.</span></span>
>
>

## <a name="what-are-security-recommendations"></a><span data-ttu-id="a4099-107">What are security recommendations?</span><span class="sxs-lookup"><span data-stu-id="a4099-107">What are security recommendations?</span></span>
<span data-ttu-id="a4099-108">Security Center periodically analyzes the security state of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="a4099-108">Security Center periodically analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="a4099-109">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span><span class="sxs-lookup"><span data-stu-id="a4099-109">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="a4099-110">The recommendations guide you through the process of configuring the needed controls.</span><span class="sxs-lookup"><span data-stu-id="a4099-110">The recommendations guide you through the process of configuring the needed controls.</span></span>

## <a name="implementing-security-recommendations"></a><span data-ttu-id="a4099-111">Implementing security recommendations</span><span class="sxs-lookup"><span data-stu-id="a4099-111">Implementing security recommendations</span></span>
### <a name="set-recommendations"></a><span data-ttu-id="a4099-112">Set recommendations</span><span class="sxs-lookup"><span data-stu-id="a4099-112">Set recommendations</span></span>
<span data-ttu-id="a4099-113">In [Setting security policies in Azure Security Center](security-center-policies.md), you learn to:</span><span class="sxs-lookup"><span data-stu-id="a4099-113">In [Setting security policies in Azure Security Center](security-center-policies.md), you learn to:</span></span>

* <span data-ttu-id="a4099-114">Configure security policies.</span><span class="sxs-lookup"><span data-stu-id="a4099-114">Configure security policies.</span></span>
* <span data-ttu-id="a4099-115">Turn on data collection.</span><span class="sxs-lookup"><span data-stu-id="a4099-115">Turn on data collection.</span></span>
* <span data-ttu-id="a4099-116">Choose which recommendations to see as part of your security policy.</span><span class="sxs-lookup"><span data-stu-id="a4099-116">Choose which recommendations to see as part of your security policy.</span></span>

<span data-ttu-id="a4099-117">Current policy recommendations center around system updates, baseline rules, antimalware programs, [network security groups](../virtual-network/virtual-networks-nsg.md) on subnets and network interfaces, SQL database auditing, SQL database transparent data encryption, and web application firewalls.</span><span class="sxs-lookup"><span data-stu-id="a4099-117">Current policy recommendations center around system updates, baseline rules, antimalware programs, [network security groups](../virtual-network/virtual-networks-nsg.md) on subnets and network interfaces, SQL database auditing, SQL database transparent data encryption, and web application firewalls.</span></span>  <span data-ttu-id="a4099-118">[Setting security policies](security-center-policies.md) provides a description of each recommendation option.</span><span class="sxs-lookup"><span data-stu-id="a4099-118">[Setting security policies](security-center-policies.md) provides a description of each recommendation option.</span></span>

### <a name="monitor-recommendations"></a><span data-ttu-id="a4099-119">Monitor recommendations</span><span class="sxs-lookup"><span data-stu-id="a4099-119">Monitor recommendations</span></span>
<span data-ttu-id="a4099-120">After setting a security policy, Security Center analyzes the security state of your resources to identify potential vulnerabilities.</span><span class="sxs-lookup"><span data-stu-id="a4099-120">After setting a security policy, Security Center analyzes the security state of your resources to identify potential vulnerabilities.</span></span> <span data-ttu-id="a4099-121">The **Recommendations** tile on the **Security Center** blade lets you know the total number of recommendations identified by Security Center.</span><span class="sxs-lookup"><span data-stu-id="a4099-121">The **Recommendations** tile on the **Security Center** blade lets you know the total number of recommendations identified by Security Center.</span></span>

![Recommendations tile][1]

<span data-ttu-id="a4099-123">To see the details of each recommendation:</span><span class="sxs-lookup"><span data-stu-id="a4099-123">To see the details of each recommendation:</span></span>

1. <span data-ttu-id="a4099-124">Click the **Recommendations tile** on the **Security Center** blade.</span><span class="sxs-lookup"><span data-stu-id="a4099-124">Click the **Recommendations tile** on the **Security Center** blade.</span></span> <span data-ttu-id="a4099-125">The **Recommendations** blade opens.</span><span class="sxs-lookup"><span data-stu-id="a4099-125">The **Recommendations** blade opens.</span></span>

<span data-ttu-id="a4099-126">The recommendations are shown in a table format where each line represents one particular recommendation.</span><span class="sxs-lookup"><span data-stu-id="a4099-126">The recommendations are shown in a table format where each line represents one particular recommendation.</span></span> <span data-ttu-id="a4099-127">The columns of this table are:</span><span class="sxs-lookup"><span data-stu-id="a4099-127">The columns of this table are:</span></span>

* <span data-ttu-id="a4099-128">**DESCRIPTION**: Explains the recommendation and what needs to be done to address it.</span><span class="sxs-lookup"><span data-stu-id="a4099-128">**DESCRIPTION**: Explains the recommendation and what needs to be done to address it.</span></span>
* <span data-ttu-id="a4099-129">**RESOURCE**: Lists the resources to which this recommendation applies.</span><span class="sxs-lookup"><span data-stu-id="a4099-129">**RESOURCE**: Lists the resources to which this recommendation applies.</span></span>
* <span data-ttu-id="a4099-130">**STATE**: Describes the current state of the recommendation:</span><span class="sxs-lookup"><span data-stu-id="a4099-130">**STATE**: Describes the current state of the recommendation:</span></span>
  * <span data-ttu-id="a4099-131">**Open**: The recommendation hasn't been addressed yet.</span><span class="sxs-lookup"><span data-stu-id="a4099-131">**Open**: The recommendation hasn't been addressed yet.</span></span>
  * <span data-ttu-id="a4099-132">**In Progress**: The recommendation is currently being applied to the resources, and no action is required by you.</span><span class="sxs-lookup"><span data-stu-id="a4099-132">**In Progress**: The recommendation is currently being applied to the resources, and no action is required by you.</span></span>
  * <span data-ttu-id="a4099-133">**Resolved**: The recommendation has already been completed (in this case, the line is grayed out).</span><span class="sxs-lookup"><span data-stu-id="a4099-133">**Resolved**: The recommendation has already been completed (in this case, the line is grayed out).</span></span>
* <span data-ttu-id="a4099-134">**SEVERITY**: Describes the severity of that particular recommendation:</span><span class="sxs-lookup"><span data-stu-id="a4099-134">**SEVERITY**: Describes the severity of that particular recommendation:</span></span>
  * <span data-ttu-id="a4099-135">**High**: A vulnerability exists with a meaningful resource (such as an application, a VM, or a network security group) and requires attention.</span><span class="sxs-lookup"><span data-stu-id="a4099-135">**High**: A vulnerability exists with a meaningful resource (such as an application, a VM, or a network security group) and requires attention.</span></span>
  * <span data-ttu-id="a4099-136">**Medium**: A vulnerability exists and non-critical or additional steps are required to eliminate it or to complete a process.</span><span class="sxs-lookup"><span data-stu-id="a4099-136">**Medium**: A vulnerability exists and non-critical or additional steps are required to eliminate it or to complete a process.</span></span>
  * <span data-ttu-id="a4099-137">**Low**: A vulnerability exists that should be addressed but does not require immediate attention.</span><span class="sxs-lookup"><span data-stu-id="a4099-137">**Low**: A vulnerability exists that should be addressed but does not require immediate attention.</span></span> <span data-ttu-id="a4099-138">(By default, low recommendations aren't presented, but you can filter on low recommendations if you want to see them.)</span><span class="sxs-lookup"><span data-stu-id="a4099-138">(By default, low recommendations aren't presented, but you can filter on low recommendations if you want to see them.)</span></span>

<span data-ttu-id="a4099-139">Use the table below as a reference to help you understand the available recommendations and what each one does if you apply it.</span><span class="sxs-lookup"><span data-stu-id="a4099-139">Use the table below as a reference to help you understand the available recommendations and what each one does if you apply it.</span></span>

> [!NOTE]
> <span data-ttu-id="a4099-140">You will want to understand the [classic and Resource Manager deployment models](../azure-classic-rm.md) for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="a4099-140">You will want to understand the [classic and Resource Manager deployment models](../azure-classic-rm.md) for Azure resources.</span></span>
>
>

| <span data-ttu-id="a4099-141">Recommendation</span><span class="sxs-lookup"><span data-stu-id="a4099-141">Recommendation</span></span> | <span data-ttu-id="a4099-142">Description</span><span class="sxs-lookup"><span data-stu-id="a4099-142">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="a4099-143">Enable data collection for subscriptions</span><span class="sxs-lookup"><span data-stu-id="a4099-143">Enable data collection for subscriptions</span></span>](security-center-enable-data-collection.md) |<span data-ttu-id="a4099-144">Recommends that you turn on data collection in the security policy for each of your subscriptions and all virtual machines (VMs) in your subscriptions.</span><span class="sxs-lookup"><span data-stu-id="a4099-144">Recommends that you turn on data collection in the security policy for each of your subscriptions and all virtual machines (VMs) in your subscriptions.</span></span> |
| [<span data-ttu-id="a4099-145">Remediate OS vulnerabilities</span><span class="sxs-lookup"><span data-stu-id="a4099-145">Remediate OS vulnerabilities</span></span>](security-center-remediate-os-vulnerabilities.md) |<span data-ttu-id="a4099-146">Recommends that you align your OS configurations with the recommended configuration rules, for example, do not allow passwords to be saved.</span><span class="sxs-lookup"><span data-stu-id="a4099-146">Recommends that you align your OS configurations with the recommended configuration rules, for example, do not allow passwords to be saved.</span></span> |
| [<span data-ttu-id="a4099-147">Apply system updates</span><span class="sxs-lookup"><span data-stu-id="a4099-147">Apply system updates</span></span>](security-center-apply-system-updates.md) |<span data-ttu-id="a4099-148">Recommends that you deploy missing system security and critical updates to VMs.</span><span class="sxs-lookup"><span data-stu-id="a4099-148">Recommends that you deploy missing system security and critical updates to VMs.</span></span> |
| [<span data-ttu-id="a4099-149">Reboot after system updates</span><span class="sxs-lookup"><span data-stu-id="a4099-149">Reboot after system updates</span></span>](security-center-apply-system-updates.md#reboot-after-system-updates) |<span data-ttu-id="a4099-150">Recommends that you reboot a VM to complete the process of applying system updates.</span><span class="sxs-lookup"><span data-stu-id="a4099-150">Recommends that you reboot a VM to complete the process of applying system updates.</span></span> |
| [<span data-ttu-id="a4099-151">Add a web application firewall</span><span class="sxs-lookup"><span data-stu-id="a4099-151">Add a web application firewall</span></span>](security-center-add-web-application-firewall.md) |<span data-ttu-id="a4099-152">Recommends that you deploy a web application firewall (WAF) for web endpoints.</span><span class="sxs-lookup"><span data-stu-id="a4099-152">Recommends that you deploy a web application firewall (WAF) for web endpoints.</span></span> <span data-ttu-id="a4099-153">A WAF recommendation is shown for any public facing IP (either Instance Level IP or Load Balanced IP) that has an associated network security group with open inbound web ports (80,443).</span><span class="sxs-lookup"><span data-stu-id="a4099-153">A WAF recommendation is shown for any public facing IP (either Instance Level IP or Load Balanced IP) that has an associated network security group with open inbound web ports (80,443).</span></span> </br><span data-ttu-id="a4099-154">Security Center recommends that you provision a WAF to help defend against attacks targeting your web applications on virtual machines and on App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="a4099-154">Security Center recommends that you provision a WAF to help defend against attacks targeting your web applications on virtual machines and on App Service Environment.</span></span> <span data-ttu-id="a4099-155">An App Service Environment (ASE) is a [Premium](https://azure.microsoft.com/pricing/details/app-service/) service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps.</span><span class="sxs-lookup"><span data-stu-id="a4099-155">An App Service Environment (ASE) is a [Premium](https://azure.microsoft.com/pricing/details/app-service/) service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps.</span></span> <span data-ttu-id="a4099-156">To learn more about ASE, see the [App Service Environment Documentation](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="a4099-156">To learn more about ASE, see the [App Service Environment Documentation](../app-service/app-service-app-service-environments-readme.md).</span></span></br><span data-ttu-id="a4099-157">You can protect multiple web applications in Security Center by adding these applications to your existing WAF deployments.</span><span class="sxs-lookup"><span data-stu-id="a4099-157">You can protect multiple web applications in Security Center by adding these applications to your existing WAF deployments.</span></span> |
| [<span data-ttu-id="a4099-158">Finalize application protection</span><span class="sxs-lookup"><span data-stu-id="a4099-158">Finalize application protection</span></span>](security-center-add-web-application-firewall.md#finalize-application-protection) |<span data-ttu-id="a4099-159">To complete the configuration of a WAF, traffic must be rerouted to the WAF appliance.</span><span class="sxs-lookup"><span data-stu-id="a4099-159">To complete the configuration of a WAF, traffic must be rerouted to the WAF appliance.</span></span> <span data-ttu-id="a4099-160">Following this recommendation completes the necessary setup changes.</span><span class="sxs-lookup"><span data-stu-id="a4099-160">Following this recommendation completes the necessary setup changes.</span></span> |
| [<span data-ttu-id="a4099-161">Add a Next Generation Firewall</span><span class="sxs-lookup"><span data-stu-id="a4099-161">Add a Next Generation Firewall</span></span>](security-center-add-next-generation-firewall.md) |<span data-ttu-id="a4099-162">Recommends that you add a Next Generation Firewall (NGFW) from a Microsoft partner to increase your security protections.</span><span class="sxs-lookup"><span data-stu-id="a4099-162">Recommends that you add a Next Generation Firewall (NGFW) from a Microsoft partner to increase your security protections.</span></span> |
| [<span data-ttu-id="a4099-163">Route traffic through NGFW only</span><span class="sxs-lookup"><span data-stu-id="a4099-163">Route traffic through NGFW only</span></span>](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |<span data-ttu-id="a4099-164">Recommends that you configure network security group (NSG) rules that force inbound traffic to your VM through your NGFW.</span><span class="sxs-lookup"><span data-stu-id="a4099-164">Recommends that you configure network security group (NSG) rules that force inbound traffic to your VM through your NGFW.</span></span> |
| [<span data-ttu-id="a4099-165">Install Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="a4099-165">Install Endpoint Protection</span></span>](security-center-install-endpoint-protection.md) |<span data-ttu-id="a4099-166">Recommends that you provision antimalware programs to VMs (Windows VMs only).</span><span class="sxs-lookup"><span data-stu-id="a4099-166">Recommends that you provision antimalware programs to VMs (Windows VMs only).</span></span> |
| [<span data-ttu-id="a4099-167">Resolve Endpoint Protection health alerts</span><span class="sxs-lookup"><span data-stu-id="a4099-167">Resolve Endpoint Protection health alerts</span></span>](security-center-resolve-endpoint-protection-health-alerts.md) |<span data-ttu-id="a4099-168">Recommends that you resolve endpoint protection failures.</span><span class="sxs-lookup"><span data-stu-id="a4099-168">Recommends that you resolve endpoint protection failures.</span></span> |
| [<span data-ttu-id="a4099-169">Enable Network Security Groups on subnets or virtual machines</span><span class="sxs-lookup"><span data-stu-id="a4099-169">Enable Network Security Groups on subnets or virtual machines</span></span>](security-center-enable-network-security-groups.md) |<span data-ttu-id="a4099-170">Recommends that you enable NSGs on subnets or VMs.</span><span class="sxs-lookup"><span data-stu-id="a4099-170">Recommends that you enable NSGs on subnets or VMs.</span></span> |
| [<span data-ttu-id="a4099-171">Restrict access through Internet facing endpoint</span><span class="sxs-lookup"><span data-stu-id="a4099-171">Restrict access through Internet facing endpoint</span></span>](security-center-restrict-access-through-internet-facing-endpoints.md) |<span data-ttu-id="a4099-172">Recommends that you configure inbound traffic rules for NSGs.</span><span class="sxs-lookup"><span data-stu-id="a4099-172">Recommends that you configure inbound traffic rules for NSGs.</span></span> |
| [<span data-ttu-id="a4099-173">Enable auditing and threat detection on SQL servers</span><span class="sxs-lookup"><span data-stu-id="a4099-173">Enable auditing and threat detection on SQL servers</span></span>](security-center-enable-auditing-on-sql-servers.md) |<span data-ttu-id="a4099-174">Recommends that you turn on auditing and threat detection for Azure SQL servers.</span><span class="sxs-lookup"><span data-stu-id="a4099-174">Recommends that you turn on auditing and threat detection for Azure SQL servers.</span></span> <span data-ttu-id="a4099-175">(Azure SQL service only.</span><span class="sxs-lookup"><span data-stu-id="a4099-175">(Azure SQL service only.</span></span> <span data-ttu-id="a4099-176">Doesn't include SQL running on your virtual machines.)</span><span class="sxs-lookup"><span data-stu-id="a4099-176">Doesn't include SQL running on your virtual machines.)</span></span> |
| [<span data-ttu-id="a4099-177">Enable auditing and threat detection on SQL databases</span><span class="sxs-lookup"><span data-stu-id="a4099-177">Enable auditing and threat detection on SQL databases</span></span>](security-center-enable-auditing-on-sql-databases.md) |<span data-ttu-id="a4099-178">Recommends that you turn on auditing and threat detection for Azure SQL databases.</span><span class="sxs-lookup"><span data-stu-id="a4099-178">Recommends that you turn on auditing and threat detection for Azure SQL databases.</span></span> <span data-ttu-id="a4099-179">(Azure SQL service only.</span><span class="sxs-lookup"><span data-stu-id="a4099-179">(Azure SQL service only.</span></span> <span data-ttu-id="a4099-180">Doesn't include SQL running on your virtual machines.)</span><span class="sxs-lookup"><span data-stu-id="a4099-180">Doesn't include SQL running on your virtual machines.)</span></span> |
| [<span data-ttu-id="a4099-181">Enable Transparent Data Encryption on SQL databases</span><span class="sxs-lookup"><span data-stu-id="a4099-181">Enable Transparent Data Encryption on SQL databases</span></span>](security-center-enable-transparent-data-encryption.md) |<span data-ttu-id="a4099-182">Recommends that you enable encryption for SQL databases.</span><span class="sxs-lookup"><span data-stu-id="a4099-182">Recommends that you enable encryption for SQL databases.</span></span> <span data-ttu-id="a4099-183">(Azure SQL service only.)</span><span class="sxs-lookup"><span data-stu-id="a4099-183">(Azure SQL service only.)</span></span> |
| [<span data-ttu-id="a4099-184">Enable VM Agent</span><span class="sxs-lookup"><span data-stu-id="a4099-184">Enable VM Agent</span></span>](security-center-enable-vm-agent.md) |<span data-ttu-id="a4099-185">Enables you to see which VMs require the VM Agent.</span><span class="sxs-lookup"><span data-stu-id="a4099-185">Enables you to see which VMs require the VM Agent.</span></span> <span data-ttu-id="a4099-186">The VM Agent must be installed on VMs to provision patch scanning, baseline scanning, and antimalware programs.</span><span class="sxs-lookup"><span data-stu-id="a4099-186">The VM Agent must be installed on VMs to provision patch scanning, baseline scanning, and antimalware programs.</span></span> <span data-ttu-id="a4099-187">The VM Agent is installed by default for VMs that are deployed from the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a4099-187">The VM Agent is installed by default for VMs that are deployed from the Azure Marketplace.</span></span> <span data-ttu-id="a4099-188">The article [VM Agent and Extensions – Part 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) provides information on how to install the VM Agent.</span><span class="sxs-lookup"><span data-stu-id="a4099-188">The article [VM Agent and Extensions – Part 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) provides information on how to install the VM Agent.</span></span> |
| [<span data-ttu-id="a4099-189">Apply disk encryption</span><span class="sxs-lookup"><span data-stu-id="a4099-189">Apply disk encryption</span></span>](security-center-apply-disk-encryption.md) |<span data-ttu-id="a4099-190">Recommends that you encrypt your VM disks using Azure Disk Encryption (Windows and Linux VMs).</span><span class="sxs-lookup"><span data-stu-id="a4099-190">Recommends that you encrypt your VM disks using Azure Disk Encryption (Windows and Linux VMs).</span></span> <span data-ttu-id="a4099-191">Encryption is recommended for both the OS and data volumes on your VM.</span><span class="sxs-lookup"><span data-stu-id="a4099-191">Encryption is recommended for both the OS and data volumes on your VM.</span></span> |
| [<span data-ttu-id="a4099-192">Provide security contact details</span><span class="sxs-lookup"><span data-stu-id="a4099-192">Provide security contact details</span></span>](security-center-provide-security-contact-details.md) |<span data-ttu-id="a4099-193">Recommends that you provide security contact information for each of your subscriptions.</span><span class="sxs-lookup"><span data-stu-id="a4099-193">Recommends that you provide security contact information for each of your subscriptions.</span></span> <span data-ttu-id="a4099-194">Contact information is an email address and phone number.</span><span class="sxs-lookup"><span data-stu-id="a4099-194">Contact information is an email address and phone number.</span></span> <span data-ttu-id="a4099-195">The information is used to contact you if our security team finds that your resources are compromised.</span><span class="sxs-lookup"><span data-stu-id="a4099-195">The information is used to contact you if our security team finds that your resources are compromised.</span></span> |
| [<span data-ttu-id="a4099-196">Update OS version</span><span class="sxs-lookup"><span data-stu-id="a4099-196">Update OS version</span></span>](security-center-update-os-version.md) |<span data-ttu-id="a4099-197">Recommends that you update the operating system (OS) version for your Cloud Service to the most recent version available for your OS family.</span><span class="sxs-lookup"><span data-stu-id="a4099-197">Recommends that you update the operating system (OS) version for your Cloud Service to the most recent version available for your OS family.</span></span>  <span data-ttu-id="a4099-198">To learn more about Cloud Services, see the [Cloud Services overview](../cloud-services/cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="a4099-198">To learn more about Cloud Services, see the [Cloud Services overview](../cloud-services/cloud-services-choose-me.md).</span></span> |
| [<span data-ttu-id="a4099-199">Vulnerability assessment not installed</span><span class="sxs-lookup"><span data-stu-id="a4099-199">Vulnerability assessment not installed</span></span>](security-center-vulnerability-assessment-recommendations.md) |<span data-ttu-id="a4099-200">Recommends that you install a vulnerability assessment solution on your VM.</span><span class="sxs-lookup"><span data-stu-id="a4099-200">Recommends that you install a vulnerability assessment solution on your VM.</span></span> |
| [<span data-ttu-id="a4099-201">Remediate vulnerabilities</span><span class="sxs-lookup"><span data-stu-id="a4099-201">Remediate vulnerabilities</span></span>](security-center-vulnerability-assessment-recommendations.md#review-recommendation) |<span data-ttu-id="a4099-202">Enables you to see system and application vulnerabilities detected by the vulnerability assessment solution installed on your VM.</span><span class="sxs-lookup"><span data-stu-id="a4099-202">Enables you to see system and application vulnerabilities detected by the vulnerability assessment solution installed on your VM.</span></span> |
| [<span data-ttu-id="a4099-203">Enable encryption for Azure Storage Account</span><span class="sxs-lookup"><span data-stu-id="a4099-203">Enable encryption for Azure Storage Account</span></span>](security-center-enable-encryption-for-storage-account.md) | <span data-ttu-id="a4099-204">Recommends that you enable Azure Storage Service Encryption for data at rest.</span><span class="sxs-lookup"><span data-stu-id="a4099-204">Recommends that you enable Azure Storage Service Encryption for data at rest.</span></span> <span data-ttu-id="a4099-205">Storage Service Encryption (SSE) works by encrypting the data when it is written to Azure storage and decrypts before retrieval.</span><span class="sxs-lookup"><span data-stu-id="a4099-205">Storage Service Encryption (SSE) works by encrypting the data when it is written to Azure storage and decrypts before retrieval.</span></span> <span data-ttu-id="a4099-206">SSE is currently available only for the Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span><span class="sxs-lookup"><span data-stu-id="a4099-206">SSE is currently available only for the Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span> <span data-ttu-id="a4099-207">To learn more, see [Storage Service Encryption for data at rest](../storage/storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="a4099-207">To learn more, see [Storage Service Encryption for data at rest](../storage/storage-service-encryption.md).</span></span></br><span data-ttu-id="a4099-208">SSE is only supported on Resource Manager storage accounts.</span><span class="sxs-lookup"><span data-stu-id="a4099-208">SSE is only supported on Resource Manager storage accounts.</span></span> |

<span data-ttu-id="a4099-209">You can filter and dismiss recommendations.</span><span class="sxs-lookup"><span data-stu-id="a4099-209">You can filter and dismiss recommendations.</span></span>

1. <span data-ttu-id="a4099-210">Click **Filter** on the **Recommendations** blade.</span><span class="sxs-lookup"><span data-stu-id="a4099-210">Click **Filter** on the **Recommendations** blade.</span></span> <span data-ttu-id="a4099-211">The **Filter** blade opens and you select the severity and state values you wish to see.</span><span class="sxs-lookup"><span data-stu-id="a4099-211">The **Filter** blade opens and you select the severity and state values you wish to see.</span></span>

    ![Filter recommendations][2]
2. <span data-ttu-id="a4099-213">If you determine that a recommendation is not applicable, you can dismiss the recommendation and then filter it out of your view.</span><span class="sxs-lookup"><span data-stu-id="a4099-213">If you determine that a recommendation is not applicable, you can dismiss the recommendation and then filter it out of your view.</span></span> <span data-ttu-id="a4099-214">There are two ways to dismiss a recommendation.</span><span class="sxs-lookup"><span data-stu-id="a4099-214">There are two ways to dismiss a recommendation.</span></span> <span data-ttu-id="a4099-215">One way is to right click an item, and then select **Dismiss**.</span><span class="sxs-lookup"><span data-stu-id="a4099-215">One way is to right click an item, and then select **Dismiss**.</span></span> <span data-ttu-id="a4099-216">The other is to hover over an item, click the three dots that appear to the right, and then select **Dismiss**.</span><span class="sxs-lookup"><span data-stu-id="a4099-216">The other is to hover over an item, click the three dots that appear to the right, and then select **Dismiss**.</span></span> <span data-ttu-id="a4099-217">You can view dismissed recommendations by clicking **Filter**, and then selecting **Dismissed**.</span><span class="sxs-lookup"><span data-stu-id="a4099-217">You can view dismissed recommendations by clicking **Filter**, and then selecting **Dismissed**.</span></span>

    ![Dismiss recommendation][3]

### <a name="apply-recommendations"></a><span data-ttu-id="a4099-219">Apply recommendations</span><span class="sxs-lookup"><span data-stu-id="a4099-219">Apply recommendations</span></span>
<span data-ttu-id="a4099-220">After reviewing all recommendations, decide which one you should apply first.</span><span class="sxs-lookup"><span data-stu-id="a4099-220">After reviewing all recommendations, decide which one you should apply first.</span></span> <span data-ttu-id="a4099-221">We recommend that you use the severity rating as the main parameter to evaluate which recommendations should be applied first.</span><span class="sxs-lookup"><span data-stu-id="a4099-221">We recommend that you use the severity rating as the main parameter to evaluate which recommendations should be applied first.</span></span>

<span data-ttu-id="a4099-222">In the table of recommendations above, select a recommendation and walk through it as an example of how to apply a recommendation.</span><span class="sxs-lookup"><span data-stu-id="a4099-222">In the table of recommendations above, select a recommendation and walk through it as an example of how to apply a recommendation.</span></span>

## <a name="see-also"></a><span data-ttu-id="a4099-223">See also</span><span class="sxs-lookup"><span data-stu-id="a4099-223">See also</span></span>
<span data-ttu-id="a4099-224">In this document, you were introduced to security recommendations in Security Center.</span><span class="sxs-lookup"><span data-stu-id="a4099-224">In this document, you were introduced to security recommendations in Security Center.</span></span> <span data-ttu-id="a4099-225">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="a4099-225">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="a4099-226">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span><span class="sxs-lookup"><span data-stu-id="a4099-226">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="a4099-227">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="a4099-227">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="a4099-228">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="a4099-228">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="a4099-229">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span><span class="sxs-lookup"><span data-stu-id="a4099-229">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="a4099-230">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="a4099-230">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="a4099-231">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span><span class="sxs-lookup"><span data-stu-id="a4099-231">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-recommendations/recommendations-tile.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-recommendations/filter-recommendations.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-recommendations/dismiss-recommendations.png


