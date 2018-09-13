---
title: Integrate external monitoring solution with Azure Stack | Microsoft Docs
description: Learn how to integrate Azure Stack with an external monitoring solution in your datacenter.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PowerShell
ms.topic: article
ms.date: 05/10/2018
ms.author: jeffgilb
ms.reviewer: thoroet
ms.openlocfilehash: d7c8520602132722fd0c7138de4a276b9ac2208a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856008"
---
# <a name="integrate-external-monitoring-solution-with-azure-stack"></a><span data-ttu-id="7e7c3-103">Integrate external monitoring solution with Azure Stack</span><span class="sxs-lookup"><span data-stu-id="7e7c3-103">Integrate external monitoring solution with Azure Stack</span></span>

<span data-ttu-id="7e7c3-104">For external monitoring of the Azure Stack infrastructure, you need to monitor the Azure Stack software, the physical computers, and the physical network switches.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-104">For external monitoring of the Azure Stack infrastructure, you need to monitor the Azure Stack software, the physical computers, and the physical network switches.</span></span> <span data-ttu-id="7e7c3-105">Each of these areas offers a method to retrieve health and alert information:</span><span class="sxs-lookup"><span data-stu-id="7e7c3-105">Each of these areas offers a method to retrieve health and alert information:</span></span>

- <span data-ttu-id="7e7c3-106">Azure Stack software offers a REST-based API to retrieve health and alerts.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-106">Azure Stack software offers a REST-based API to retrieve health and alerts.</span></span> <span data-ttu-id="7e7c3-107">The use of software-defined technologies such as Storage Spaces Direct, storage health and alerts are part of software monitoring.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-107">The use of software-defined technologies such as Storage Spaces Direct, storage health and alerts are part of software monitoring.</span></span>
- <span data-ttu-id="7e7c3-108">Physical computers can make health and alert information available via the baseboard management controllers (BMCs).</span><span class="sxs-lookup"><span data-stu-id="7e7c3-108">Physical computers can make health and alert information available via the baseboard management controllers (BMCs).</span></span>
- <span data-ttu-id="7e7c3-109">Physical network devices can make health and alert information available via the SNMP protocol.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-109">Physical network devices can make health and alert information available via the SNMP protocol.</span></span>

<span data-ttu-id="7e7c3-110">Each Azure Stack solution ships with a hardware lifecycle host.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-110">Each Azure Stack solution ships with a hardware lifecycle host.</span></span> <span data-ttu-id="7e7c3-111">This host runs the Original Equipment Manufacturer (OEM) hardware vendor’s monitoring software for the physical servers and network devices.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-111">This host runs the Original Equipment Manufacturer (OEM) hardware vendor’s monitoring software for the physical servers and network devices.</span></span> <span data-ttu-id="7e7c3-112">If desired, you can bypass these monitoring solutions and directly integrate with existing monitoring solutions in your datacenter.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-112">If desired, you can bypass these monitoring solutions and directly integrate with existing monitoring solutions in your datacenter.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e7c3-113">The external monitoring solution you use must be agentless.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-113">The external monitoring solution you use must be agentless.</span></span> <span data-ttu-id="7e7c3-114">You can't install third-party agents inside Azure Stack components.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-114">You can't install third-party agents inside Azure Stack components.</span></span>

<span data-ttu-id="7e7c3-115">The following diagram shows traffic flow between an Azure Stack integrated system, the hardware lifecycle host, an external monitoring solution, and an external ticketing/data collection system.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-115">The following diagram shows traffic flow between an Azure Stack integrated system, the hardware lifecycle host, an external monitoring solution, and an external ticketing/data collection system.</span></span>

![Diagram showing traffic between Azure Stack, monitoring, and ticketing solution.](media/azure-stack-integrate-monitor/MonitoringIntegration.png)  

<span data-ttu-id="7e7c3-117">This article explains how to integrate Azure Stack with external monitoring solutions such as System Center Operations Manager and Nagios.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-117">This article explains how to integrate Azure Stack with external monitoring solutions such as System Center Operations Manager and Nagios.</span></span> <span data-ttu-id="7e7c3-118">It also includes how to work with alerts programmatically by using PowerShell or through REST API calls.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-118">It also includes how to work with alerts programmatically by using PowerShell or through REST API calls.</span></span>

## <a name="integrate-with-operations-manager"></a><span data-ttu-id="7e7c3-119">Integrate with Operations Manager</span><span class="sxs-lookup"><span data-stu-id="7e7c3-119">Integrate with Operations Manager</span></span>

<span data-ttu-id="7e7c3-120">You can use Operations Manager for external monitoring of Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-120">You can use Operations Manager for external monitoring of Azure Stack.</span></span> <span data-ttu-id="7e7c3-121">The System Center Management Pack for Microsoft Azure Stack enables you to monitor multiple Azure Stack deployments with a single Operations Manager instance.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-121">The System Center Management Pack for Microsoft Azure Stack enables you to monitor multiple Azure Stack deployments with a single Operations Manager instance.</span></span> <span data-ttu-id="7e7c3-122">The management pack uses the Health resource provider and Update resource provider REST APIs to communicate with Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-122">The management pack uses the Health resource provider and Update resource provider REST APIs to communicate with Azure Stack.</span></span> <span data-ttu-id="7e7c3-123">If you plan to bypass the OEM monitoring software that's running on the hardware lifecycle host, you can install vendor management packs to monitor physical servers.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-123">If you plan to bypass the OEM monitoring software that's running on the hardware lifecycle host, you can install vendor management packs to monitor physical servers.</span></span> <span data-ttu-id="7e7c3-124">You can also use Operations Manager network device discovery to monitor network switches.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-124">You can also use Operations Manager network device discovery to monitor network switches.</span></span>

<span data-ttu-id="7e7c3-125">The management pack for Azure Stack provides the following capabilities:</span><span class="sxs-lookup"><span data-stu-id="7e7c3-125">The management pack for Azure Stack provides the following capabilities:</span></span>

- <span data-ttu-id="7e7c3-126">You can manage multiple Azure Stack deployments</span><span class="sxs-lookup"><span data-stu-id="7e7c3-126">You can manage multiple Azure Stack deployments</span></span>
- <span data-ttu-id="7e7c3-127">There's support for Azure Active Directory (Azure AD) and Active Directory Federation Services (AD FS)</span><span class="sxs-lookup"><span data-stu-id="7e7c3-127">There's support for Azure Active Directory (Azure AD) and Active Directory Federation Services (AD FS)</span></span>
- <span data-ttu-id="7e7c3-128">You can retrieve and close alerts</span><span class="sxs-lookup"><span data-stu-id="7e7c3-128">You can retrieve and close alerts</span></span>
- <span data-ttu-id="7e7c3-129">There's a Health and a Capacity dashboard</span><span class="sxs-lookup"><span data-stu-id="7e7c3-129">There's a Health and a Capacity dashboard</span></span>
- <span data-ttu-id="7e7c3-130">Includes Auto Maintenance Mode detection for when patch and update (P&U) is in progress</span><span class="sxs-lookup"><span data-stu-id="7e7c3-130">Includes Auto Maintenance Mode detection for when patch and update (P&U) is in progress</span></span>
- <span data-ttu-id="7e7c3-131">Includes Force Update tasks for deployment and region</span><span class="sxs-lookup"><span data-stu-id="7e7c3-131">Includes Force Update tasks for deployment and region</span></span>
- <span data-ttu-id="7e7c3-132">You can add custom information to a region</span><span class="sxs-lookup"><span data-stu-id="7e7c3-132">You can add custom information to a region</span></span>
- <span data-ttu-id="7e7c3-133">Supports notification and reporting</span><span class="sxs-lookup"><span data-stu-id="7e7c3-133">Supports notification and reporting</span></span>

<span data-ttu-id="7e7c3-134">You can download the System Center Management Pack for Microsoft Azure Stack and the associated [user guide](https://www.microsoft.com/en-us/download/details.aspx?id=55184), or directly from Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-134">You can download the System Center Management Pack for Microsoft Azure Stack and the associated [user guide](https://www.microsoft.com/en-us/download/details.aspx?id=55184), or directly from Operations Manager.</span></span>

<span data-ttu-id="7e7c3-135">For a ticketing solution, you can integrate Operations Manager with System Center Service Manager.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-135">For a ticketing solution, you can integrate Operations Manager with System Center Service Manager.</span></span> <span data-ttu-id="7e7c3-136">The integrated product connector enables bi-directional communication that allows you to close an alert in Azure Stack and Operations Manager after you resolve a service request in Service Manager.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-136">The integrated product connector enables bi-directional communication that allows you to close an alert in Azure Stack and Operations Manager after you resolve a service request in Service Manager.</span></span>

<span data-ttu-id="7e7c3-137">The following diagram shows integration of Azure Stack with an existing System Center deployment.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-137">The following diagram shows integration of Azure Stack with an existing System Center deployment.</span></span> <span data-ttu-id="7e7c3-138">You can automate Service Manager further with System Center Orchestrator or Service Management Automation (SMA) to run operations in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-138">You can automate Service Manager further with System Center Orchestrator or Service Management Automation (SMA) to run operations in Azure Stack.</span></span>

![Diagram showing integration with OM, Service Manager, and SMA.](media/azure-stack-integrate-monitor/SystemCenterIntegration.png)

## <a name="integrate-with-nagios"></a><span data-ttu-id="7e7c3-140">Integrate with Nagios</span><span class="sxs-lookup"><span data-stu-id="7e7c3-140">Integrate with Nagios</span></span>

<span data-ttu-id="7e7c3-141">A Nagios monitoring plugin was developed together with the partner Cloudbase solutions, which is available under the permissive free software license – MIT (Massachusetts Institute of Technology).</span><span class="sxs-lookup"><span data-stu-id="7e7c3-141">A Nagios monitoring plugin was developed together with the partner Cloudbase solutions, which is available under the permissive free software license – MIT (Massachusetts Institute of Technology).</span></span>

<span data-ttu-id="7e7c3-142">The plugin is written in Python and leverages the health resource provider REST API.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-142">The plugin is written in Python and leverages the health resource provider REST API.</span></span> <span data-ttu-id="7e7c3-143">It offers basic functionality to retrieve and close alerts in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-143">It offers basic functionality to retrieve and close alerts in Azure Stack.</span></span> <span data-ttu-id="7e7c3-144">Like the System Center management pack, it enables you to add multiple Azure Stack deployments and to send notifications.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-144">Like the System Center management pack, it enables you to add multiple Azure Stack deployments and to send notifications.</span></span>

<span data-ttu-id="7e7c3-145">The plugin works with Nagios Enterprise and Nagios Core.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-145">The plugin works with Nagios Enterprise and Nagios Core.</span></span> <span data-ttu-id="7e7c3-146">You can download it [here](https://exchange.nagios.org/directory/Plugins/Cloud/Monitoring-AzureStack-Alerts/details).</span><span class="sxs-lookup"><span data-stu-id="7e7c3-146">You can download it [here](https://exchange.nagios.org/directory/Plugins/Cloud/Monitoring-AzureStack-Alerts/details).</span></span> <span data-ttu-id="7e7c3-147">The download site also includes installation and configuration details.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-147">The download site also includes installation and configuration details.</span></span>

### <a name="plugin-parameters"></a><span data-ttu-id="7e7c3-148">Plugin parameters</span><span class="sxs-lookup"><span data-stu-id="7e7c3-148">Plugin parameters</span></span>

<span data-ttu-id="7e7c3-149">Configure the plugin file “Azurestack_plugin.py” with the following parameters:</span><span class="sxs-lookup"><span data-stu-id="7e7c3-149">Configure the plugin file “Azurestack_plugin.py” with the following parameters:</span></span>

| <span data-ttu-id="7e7c3-150">Parameter</span><span class="sxs-lookup"><span data-stu-id="7e7c3-150">Parameter</span></span> | <span data-ttu-id="7e7c3-151">Description</span><span class="sxs-lookup"><span data-stu-id="7e7c3-151">Description</span></span> | <span data-ttu-id="7e7c3-152">Example</span><span class="sxs-lookup"><span data-stu-id="7e7c3-152">Example</span></span> |
|---------|---------|---------|
| <span data-ttu-id="7e7c3-153">*arm_endpoint*</span><span class="sxs-lookup"><span data-stu-id="7e7c3-153">*arm_endpoint*</span></span> | <span data-ttu-id="7e7c3-154">Azure Resource Manager (administrator) endpoint</span><span class="sxs-lookup"><span data-stu-id="7e7c3-154">Azure Resource Manager (administrator) endpoint</span></span> |https://adminmanagement.local.azurestack.external |
| <span data-ttu-id="7e7c3-155">*api_endpoint*</span><span class="sxs-lookup"><span data-stu-id="7e7c3-155">*api_endpoint*</span></span> | <span data-ttu-id="7e7c3-156">Azure Resource Manager (administrator) endpoint</span><span class="sxs-lookup"><span data-stu-id="7e7c3-156">Azure Resource Manager (administrator) endpoint</span></span>  | https://adminmanagement.local.azurestack.external |
| <span data-ttu-id="7e7c3-157">*Tenant_id*</span><span class="sxs-lookup"><span data-stu-id="7e7c3-157">*Tenant_id*</span></span> | <span data-ttu-id="7e7c3-158">Admin subscription ID</span><span class="sxs-lookup"><span data-stu-id="7e7c3-158">Admin subscription ID</span></span> | <span data-ttu-id="7e7c3-159">Retrieve via the administrator portal or PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e7c3-159">Retrieve via the administrator portal or PowerShell</span></span> |
| <span data-ttu-id="7e7c3-160">*User_name*</span><span class="sxs-lookup"><span data-stu-id="7e7c3-160">*User_name*</span></span> | <span data-ttu-id="7e7c3-161">Operator subscription username</span><span class="sxs-lookup"><span data-stu-id="7e7c3-161">Operator subscription username</span></span> | operator@myazuredirectory.onmicrosoft.com |
| <span data-ttu-id="7e7c3-162">*User_password*</span><span class="sxs-lookup"><span data-stu-id="7e7c3-162">*User_password*</span></span> | <span data-ttu-id="7e7c3-163">Operator subscription password</span><span class="sxs-lookup"><span data-stu-id="7e7c3-163">Operator subscription password</span></span> | <span data-ttu-id="7e7c3-164">mypassword</span><span class="sxs-lookup"><span data-stu-id="7e7c3-164">mypassword</span></span> |
| <span data-ttu-id="7e7c3-165">*Client_id*</span><span class="sxs-lookup"><span data-stu-id="7e7c3-165">*Client_id*</span></span> | <span data-ttu-id="7e7c3-166">Client</span><span class="sxs-lookup"><span data-stu-id="7e7c3-166">Client</span></span> | <span data-ttu-id="7e7c3-167">0a7bdc5c-7b57-40be-9939-d4c5fc7cd417\*</span><span class="sxs-lookup"><span data-stu-id="7e7c3-167">0a7bdc5c-7b57-40be-9939-d4c5fc7cd417\*</span></span> |
| <span data-ttu-id="7e7c3-168">*region*</span><span class="sxs-lookup"><span data-stu-id="7e7c3-168">*region*</span></span> |  <span data-ttu-id="7e7c3-169">Azure Stack region name</span><span class="sxs-lookup"><span data-stu-id="7e7c3-169">Azure Stack region name</span></span> | <span data-ttu-id="7e7c3-170">local</span><span class="sxs-lookup"><span data-stu-id="7e7c3-170">local</span></span> |
|  |  |

<span data-ttu-id="7e7c3-171">\*The PowerShell GUID that’s provided is universal.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-171">\*The PowerShell GUID that’s provided is universal.</span></span> <span data-ttu-id="7e7c3-172">You can use it for each deployment.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-172">You can use it for each deployment.</span></span>

## <a name="use-powershell-to-monitor-health-and-alerts"></a><span data-ttu-id="7e7c3-173">Use PowerShell to monitor health and alerts</span><span class="sxs-lookup"><span data-stu-id="7e7c3-173">Use PowerShell to monitor health and alerts</span></span>

<span data-ttu-id="7e7c3-174">If you're not using Operations Manager, Nagios, or a Nagios-based solution, you can use PowerShell to enable a broad range of monitoring solutions to integrate with Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-174">If you're not using Operations Manager, Nagios, or a Nagios-based solution, you can use PowerShell to enable a broad range of monitoring solutions to integrate with Azure Stack.</span></span>

1. <span data-ttu-id="7e7c3-175">To use PowerShell, make sure that you have [PowerShell installed and configured](azure-stack-powershell-configure-quickstart.md) for an Azure Stack operator environment.</span><span class="sxs-lookup"><span data-stu-id="7e7c3-175">To use PowerShell, make sure that you have [PowerShell installed and configured](azure-stack-powershell-configure-quickstart.md) for an Azure Stack operator environment.</span></span> <span data-ttu-id="7e7c3-176">Install PowerShell on a local computer that can reach the Resource Manager (administrator) endpoint (https://adminmanagement.[region].[External_FQDN]).</span><span class="sxs-lookup"><span data-stu-id="7e7c3-176">Install PowerShell on a local computer that can reach the Resource Manager (administrator) endpoint (https://adminmanagement.[region].[External_FQDN]).</span></span>

2. <span data-ttu-id="7e7c3-177">Run the following commands to connect to the Azure Stack environment as an Azure Stack operator:</span><span class="sxs-lookup"><span data-stu-id="7e7c3-177">Run the following commands to connect to the Azure Stack environment as an Azure Stack operator:</span></span>

   ```PowerShell  
    Add-AzureRMEnvironment -Name "AzureStackAdmin" -ArmEndpoint https://adminmanagement.[Region].[External_FQDN]

   Add-AzureRmAccount -EnvironmentName "AzureStackAdmin"
   ```

3. <span data-ttu-id="7e7c3-178">Use commands such as the following examples to work with alerts:</span><span class="sxs-lookup"><span data-stu-id="7e7c3-178">Use commands such as the following examples to work with alerts:</span></span>
   ```PowerShell
    #Retrieve all alerts
    Get-AzsAlert

    #Filter for active alerts
    $Active=Get-AzsAlert | Where {$_.State -eq "active"}
    $Active

    #Close alert
    Close-AzsAlert -AlertID "ID"

    #Retrieve resource provider health
    Get-AzsRPHealth

    #Retrieve infrastructure role instance health
    $FRPID=Get-AzsRPHealth|Where-Object {$_.DisplayName -eq "Capacity"}
    Get-AzsRegistrationHealth -ServiceRegistrationId $FRPID.RegistrationId

    ```

## <a name="learn-more"></a><span data-ttu-id="7e7c3-179">Learn more</span><span class="sxs-lookup"><span data-stu-id="7e7c3-179">Learn more</span></span>

<span data-ttu-id="7e7c3-180">For information about built-in health monitoring, see [Monitor health and alerts in Azure Stack](azure-stack-monitor-health.md).</span><span class="sxs-lookup"><span data-stu-id="7e7c3-180">For information about built-in health monitoring, see [Monitor health and alerts in Azure Stack](azure-stack-monitor-health.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e7c3-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="7e7c3-181">Next steps</span></span>

[<span data-ttu-id="7e7c3-182">Security integration</span><span class="sxs-lookup"><span data-stu-id="7e7c3-182">Security integration</span></span>](azure-stack-integrate-security.md)
