---
title: Azure Log Integration FAQ | Microsoft Docs
description: This article answers questions about Azure Log Integration.
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: d06d1ac5-5c3b-49de-800e-4d54b3064c64
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload8: na
ms.date: 06/07/2018
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: bec62b8c6b70706fa6519cbc2fd59bf69f119e9d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44810419"
---
# <a name="azure-log-integration-faq"></a><span data-ttu-id="57da5-103">Azure Log Integration FAQ</span><span class="sxs-lookup"><span data-stu-id="57da5-103">Azure Log Integration FAQ</span></span>

<span data-ttu-id="57da5-104">This article answers frequently asked questions (FAQ) about Azure Log Integration.</span><span class="sxs-lookup"><span data-stu-id="57da5-104">This article answers frequently asked questions (FAQ) about Azure Log Integration.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="57da5-105">The Azure Log integration feature will be deprecated by 06/01/2019.</span><span class="sxs-lookup"><span data-stu-id="57da5-105">The Azure Log integration feature will be deprecated by 06/01/2019.</span></span> <span data-ttu-id="57da5-106">AzLog downloads will be disabled by Jun 27, 2018.</span><span class="sxs-lookup"><span data-stu-id="57da5-106">AzLog downloads will be disabled by Jun 27, 2018.</span></span> <span data-ttu-id="57da5-107">For guidance on what to do moving forward review the post [Use Azure monitor to integrate with SIEM tools](https://azure.microsoft.com/blog/use-azure-monitor-to-integrate-with-siem-tools/)</span><span class="sxs-lookup"><span data-stu-id="57da5-107">For guidance on what to do moving forward review the post [Use Azure monitor to integrate with SIEM tools](https://azure.microsoft.com/blog/use-azure-monitor-to-integrate-with-siem-tools/)</span></span> 

<span data-ttu-id="57da5-108">Azure Log Integration is a Windows operating system service that you can use to integrate raw logs from your Azure resources into your on-premises security information and event management (SIEM) systems.</span><span class="sxs-lookup"><span data-stu-id="57da5-108">Azure Log Integration is a Windows operating system service that you can use to integrate raw logs from your Azure resources into your on-premises security information and event management (SIEM) systems.</span></span> <span data-ttu-id="57da5-109">This integration provides a unified dashboard for all your assets, on-premises or in the cloud.</span><span class="sxs-lookup"><span data-stu-id="57da5-109">This integration provides a unified dashboard for all your assets, on-premises or in the cloud.</span></span> <span data-ttu-id="57da5-110">You can then aggregate, correlate, analyze, and alert for security events associated with your applications.</span><span class="sxs-lookup"><span data-stu-id="57da5-110">You can then aggregate, correlate, analyze, and alert for security events associated with your applications.</span></span>

<span data-ttu-id="57da5-111">The preferred method for integrating Azure logs is by using your SIEM vendor’s Azure Monitor connector and following these [instructions](../monitoring-and-diagnostics/monitor-stream-monitoring-data-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="57da5-111">The preferred method for integrating Azure logs is by using your SIEM vendor’s Azure Monitor connector and following these [instructions](../monitoring-and-diagnostics/monitor-stream-monitoring-data-event-hubs.md).</span></span> <span data-ttu-id="57da5-112">However, if your SIEM vendor doesn’t provide a connector to Azure Monitor, you may be able to use Azure Log Integration as a temporary solution (if your SIEM is supported by Azure Log Integration) until such a connector is available.</span><span class="sxs-lookup"><span data-stu-id="57da5-112">However, if your SIEM vendor doesn’t provide a connector to Azure Monitor, you may be able to use Azure Log Integration as a temporary solution (if your SIEM is supported by Azure Log Integration) until such a connector is available.</span></span>

## <a name="is-the-azure-log-integration-software-free"></a><span data-ttu-id="57da5-113">Is the Azure Log Integration software free?</span><span class="sxs-lookup"><span data-stu-id="57da5-113">Is the Azure Log Integration software free?</span></span>

<span data-ttu-id="57da5-114">Yes.</span><span class="sxs-lookup"><span data-stu-id="57da5-114">Yes.</span></span> <span data-ttu-id="57da5-115">There is no charge for the Azure Log Integration software.</span><span class="sxs-lookup"><span data-stu-id="57da5-115">There is no charge for the Azure Log Integration software.</span></span>

## <a name="where-is-azure-log-integration-available"></a><span data-ttu-id="57da5-116">Where is Azure Log Integration available?</span><span class="sxs-lookup"><span data-stu-id="57da5-116">Where is Azure Log Integration available?</span></span>

<span data-ttu-id="57da5-117">It is currently available in Azure Commercial and Azure Government and is not available in China or Germany.</span><span class="sxs-lookup"><span data-stu-id="57da5-117">It is currently available in Azure Commercial and Azure Government and is not available in China or Germany.</span></span>

## <a name="how-can-i-see-the-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a><span data-ttu-id="57da5-118">How can I see the storage accounts from which Azure Log Integration is pulling Azure VM logs?</span><span class="sxs-lookup"><span data-stu-id="57da5-118">How can I see the storage accounts from which Azure Log Integration is pulling Azure VM logs?</span></span>

<span data-ttu-id="57da5-119">Run the command **AzLog source list**.</span><span class="sxs-lookup"><span data-stu-id="57da5-119">Run the command **AzLog source list**.</span></span>

## <a name="how-can-i-tell-which-subscription-the-azure-log-integration-logs-are-from"></a><span data-ttu-id="57da5-120">How can I tell which subscription the Azure Log Integration logs are from?</span><span class="sxs-lookup"><span data-stu-id="57da5-120">How can I tell which subscription the Azure Log Integration logs are from?</span></span>

<span data-ttu-id="57da5-121">In the case of audit logs that are placed in the **AzureResourcemanagerJson** directories, the subscription ID is in the log file name.</span><span class="sxs-lookup"><span data-stu-id="57da5-121">In the case of audit logs that are placed in the **AzureResourcemanagerJson** directories, the subscription ID is in the log file name.</span></span> <span data-ttu-id="57da5-122">This is also true for logs in the **AzureSecurityCenterJson** folder.</span><span class="sxs-lookup"><span data-stu-id="57da5-122">This is also true for logs in the **AzureSecurityCenterJson** folder.</span></span> <span data-ttu-id="57da5-123">For example:</span><span class="sxs-lookup"><span data-stu-id="57da5-123">For example:</span></span>

<span data-ttu-id="57da5-124">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span><span class="sxs-lookup"><span data-stu-id="57da5-124">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span></span>

<span data-ttu-id="57da5-125">Azure Active Directory audit logs include the tenant ID as part of the name.</span><span class="sxs-lookup"><span data-stu-id="57da5-125">Azure Active Directory audit logs include the tenant ID as part of the name.</span></span>

<span data-ttu-id="57da5-126">Diagnostic logs that are read from an event hub do not include the subscription ID as part of the name.</span><span class="sxs-lookup"><span data-stu-id="57da5-126">Diagnostic logs that are read from an event hub do not include the subscription ID as part of the name.</span></span> <span data-ttu-id="57da5-127">Instead, they include the friendly name specified as part of the creation of the event hub source.</span><span class="sxs-lookup"><span data-stu-id="57da5-127">Instead, they include the friendly name specified as part of the creation of the event hub source.</span></span> 

## <a name="how-can-i-update-the-proxy-configuration"></a><span data-ttu-id="57da5-128">How can I update the proxy configuration?</span><span class="sxs-lookup"><span data-stu-id="57da5-128">How can I update the proxy configuration?</span></span>

<span data-ttu-id="57da5-129">If your proxy setting does not allow Azure storage access directly, open the **AZLOG.EXE.CONFIG** file in **c:\Program Files\Microsoft Azure Log Integration**.</span><span class="sxs-lookup"><span data-stu-id="57da5-129">If your proxy setting does not allow Azure storage access directly, open the **AZLOG.EXE.CONFIG** file in **c:\Program Files\Microsoft Azure Log Integration**.</span></span> <span data-ttu-id="57da5-130">Update the file to include the **defaultProxy** section with the proxy address of your organization.</span><span class="sxs-lookup"><span data-stu-id="57da5-130">Update the file to include the **defaultProxy** section with the proxy address of your organization.</span></span> <span data-ttu-id="57da5-131">After the update is done, stop and start the service by using the commands **net stop AzLog** and **net start AzLog**.</span><span class="sxs-lookup"><span data-stu-id="57da5-131">After the update is done, stop and start the service by using the commands **net stop AzLog** and **net start AzLog**.</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.net>
        <connectionManagement>
          <add address="*" maxconnection="400" />
        </connectionManagement>
        <defaultProxy>
          <proxy usesystemdefault="true"
          proxyaddress="http://127.0.0.1:8888"
          bypassonlocal="true" />
        </defaultProxy>
      </system.net>
      <system.diagnostics>
        <performanceCounters filemappingsize="20971520" />
      </system.diagnostics>   

## <a name="how-can-i-see-the-subscription-information-in-windows-events"></a><span data-ttu-id="57da5-132">How can I see the subscription information in Windows events?</span><span class="sxs-lookup"><span data-stu-id="57da5-132">How can I see the subscription information in Windows events?</span></span>

<span data-ttu-id="57da5-133">Append the subscription ID to the friendly name while adding the source:</span><span class="sxs-lookup"><span data-stu-id="57da5-133">Append the subscription ID to the friendly name while adding the source:</span></span>

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
<span data-ttu-id="57da5-134">The event XML has the following metadata, including the subscription ID:</span><span class="sxs-lookup"><span data-stu-id="57da5-134">The event XML has the following metadata, including the subscription ID:</span></span>

![Event XML][1]

## <a name="error-messages"></a><span data-ttu-id="57da5-136">Error messages</span><span class="sxs-lookup"><span data-stu-id="57da5-136">Error messages</span></span>
### <a name="when-i-run-the-command-azlog-createazureid-why-do-i-get-the-following-error"></a><span data-ttu-id="57da5-137">When I run the command ```AzLog createazureid```, why do I get the following error?</span><span class="sxs-lookup"><span data-stu-id="57da5-137">When I run the command ```AzLog createazureid```, why do I get the following error?</span></span>

<span data-ttu-id="57da5-138">Error:</span><span class="sxs-lookup"><span data-stu-id="57da5-138">Error:</span></span>

  <span data-ttu-id="57da5-139">*Failed to create AAD Application - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - Reason = 'Forbidden' - Message = 'Insufficient privileges to complete the operation.'*</span><span class="sxs-lookup"><span data-stu-id="57da5-139">*Failed to create AAD Application - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - Reason = 'Forbidden' - Message = 'Insufficient privileges to complete the operation.'*</span></span>

<span data-ttu-id="57da5-140">The **azlog createazureid** command attempts to create a service principal in all the Azure AD tenants for the subscriptions that the Azure login has access to.</span><span class="sxs-lookup"><span data-stu-id="57da5-140">The **azlog createazureid** command attempts to create a service principal in all the Azure AD tenants for the subscriptions that the Azure login has access to.</span></span> <span data-ttu-id="57da5-141">If your Azure login is only a guest user in that Azure AD tenant, the command fails with "Insufficient privileges to complete the operation."</span><span class="sxs-lookup"><span data-stu-id="57da5-141">If your Azure login is only a guest user in that Azure AD tenant, the command fails with "Insufficient privileges to complete the operation."</span></span> <span data-ttu-id="57da5-142">Ask the tenant admin to add your account as a user in the tenant.</span><span class="sxs-lookup"><span data-stu-id="57da5-142">Ask the tenant admin to add your account as a user in the tenant.</span></span>

### <a name="when-i-run-the-command-azlog-authorize-why-do-i-get-the-following-error"></a><span data-ttu-id="57da5-143">When I run the command **azlog authorize**, why do I get the following error?</span><span class="sxs-lookup"><span data-stu-id="57da5-143">When I run the command **azlog authorize**, why do I get the following error?</span></span>

<span data-ttu-id="57da5-144">Error:</span><span class="sxs-lookup"><span data-stu-id="57da5-144">Error:</span></span>

  <span data-ttu-id="57da5-145">*Warning creating Role Assignment - AuthorizationFailed: The client janedo@microsoft.com' with object id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000'.*</span><span class="sxs-lookup"><span data-stu-id="57da5-145">*Warning creating Role Assignment - AuthorizationFailed: The client janedo@microsoft.com' with object id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000'.*</span></span>

<span data-ttu-id="57da5-146">The **azlog authorize** command assigns the role of reader to the Azure AD service principal (created with **azlog createazureid**) to the provided subscriptions.</span><span class="sxs-lookup"><span data-stu-id="57da5-146">The **azlog authorize** command assigns the role of reader to the Azure AD service principal (created with **azlog createazureid**) to the provided subscriptions.</span></span> <span data-ttu-id="57da5-147">If the Azure login is not a co-administrator or an owner of the subscription, it fails with an "Authorization Failed" error message.</span><span class="sxs-lookup"><span data-stu-id="57da5-147">If the Azure login is not a co-administrator or an owner of the subscription, it fails with an "Authorization Failed" error message.</span></span> <span data-ttu-id="57da5-148">Azure Role-Based Access Control (RBAC) of co-administrator or owner is needed to complete this action.</span><span class="sxs-lookup"><span data-stu-id="57da5-148">Azure Role-Based Access Control (RBAC) of co-administrator or owner is needed to complete this action.</span></span>

## <a name="where-can-i-find-the-definition-of-the-properties-in-the-audit-log"></a><span data-ttu-id="57da5-149">Where can I find the definition of the properties in the audit log?</span><span class="sxs-lookup"><span data-stu-id="57da5-149">Where can I find the definition of the properties in the audit log?</span></span>

<span data-ttu-id="57da5-150">See:</span><span class="sxs-lookup"><span data-stu-id="57da5-150">See:</span></span>

* [<span data-ttu-id="57da5-151">Audit operations with Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="57da5-151">Audit operations with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-audit.md)
* [<span data-ttu-id="57da5-152">List the management events in a subscription in the Azure Monitor REST API</span><span class="sxs-lookup"><span data-stu-id="57da5-152">List the management events in a subscription in the Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a><span data-ttu-id="57da5-153">Where can I find details on Azure Security Center alerts?</span><span class="sxs-lookup"><span data-stu-id="57da5-153">Where can I find details on Azure Security Center alerts?</span></span>

<span data-ttu-id="57da5-154">See [Managing and responding to security alerts in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="57da5-154">See [Managing and responding to security alerts in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span></span>

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a><span data-ttu-id="57da5-155">How can I modify what is collected with VM diagnostics?</span><span class="sxs-lookup"><span data-stu-id="57da5-155">How can I modify what is collected with VM diagnostics?</span></span>

<span data-ttu-id="57da5-156">For details on how to get, modify, and set the Azure Diagnostics configuration, see [Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="57da5-156">For details on how to get, modify, and set the Azure Diagnostics configuration, see [Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="57da5-157">The following example gets the Azure Diagnostics configuration:</span><span class="sxs-lookup"><span data-stu-id="57da5-157">The following example gets the Azure Diagnostics configuration:</span></span>

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

<span data-ttu-id="57da5-158">The following example modifies the Azure Diagnostics configuration.</span><span class="sxs-lookup"><span data-stu-id="57da5-158">The following example modifies the Azure Diagnostics configuration.</span></span> <span data-ttu-id="57da5-159">In this configuration, only event ID 4624 and event ID 4625 are collected from the security event log.</span><span class="sxs-lookup"><span data-stu-id="57da5-159">In this configuration, only event ID 4624 and event ID 4625 are collected from the security event log.</span></span> <span data-ttu-id="57da5-160">Microsoft Antimalware for Azure events are collected from the system event log.</span><span class="sxs-lookup"><span data-stu-id="57da5-160">Microsoft Antimalware for Azure events are collected from the system event log.</span></span> <span data-ttu-id="57da5-161">For details on the use of XPath expressions, see [Consuming Events](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="57da5-161">For details on the use of XPath expressions, see [Consuming Events](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span></span>

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

<span data-ttu-id="57da5-162">The following example sets the Azure Diagnostics configuration:</span><span class="sxs-lookup"><span data-stu-id="57da5-162">The following example sets the Azure Diagnostics configuration:</span></span>

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

<span data-ttu-id="57da5-163">After you make changes, check the storage account to ensure that the correct events are collected.</span><span class="sxs-lookup"><span data-stu-id="57da5-163">After you make changes, check the storage account to ensure that the correct events are collected.</span></span>

<span data-ttu-id="57da5-164">If you have any issues during the installation and configuration, please open a [support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span><span class="sxs-lookup"><span data-stu-id="57da5-164">If you have any issues during the installation and configuration, please open a [support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span></span> <span data-ttu-id="57da5-165">Select **Log Integration** as the service for which you are requesting support.</span><span class="sxs-lookup"><span data-stu-id="57da5-165">Select **Log Integration** as the service for which you are requesting support.</span></span>

## <a name="can-i-use-azure-log-integration-to-integrate-network-watcher-logs-into-my-siem"></a><span data-ttu-id="57da5-166">Can I use Azure Log Integration to integrate Network Watcher logs into my SIEM?</span><span class="sxs-lookup"><span data-stu-id="57da5-166">Can I use Azure Log Integration to integrate Network Watcher logs into my SIEM?</span></span>

<span data-ttu-id="57da5-167">Azure Network Watcher generates large quantities of logging information.</span><span class="sxs-lookup"><span data-stu-id="57da5-167">Azure Network Watcher generates large quantities of logging information.</span></span> <span data-ttu-id="57da5-168">These logs are not meant to be sent to a SIEM.</span><span class="sxs-lookup"><span data-stu-id="57da5-168">These logs are not meant to be sent to a SIEM.</span></span> <span data-ttu-id="57da5-169">The only supported destination for Network Watcher logs is a storage account.</span><span class="sxs-lookup"><span data-stu-id="57da5-169">The only supported destination for Network Watcher logs is a storage account.</span></span> <span data-ttu-id="57da5-170">Azure Log Integration does not support reading these logs and making them available to a SIEM.</span><span class="sxs-lookup"><span data-stu-id="57da5-170">Azure Log Integration does not support reading these logs and making them available to a SIEM.</span></span>

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
