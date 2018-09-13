---
title: Azure log integration FAQ | Microsoft Docs
description: This FAQ answers questions about Azure log integration.
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
ms.workload: na
ms.date: 01/07/2017
ms.author: TomSh
ms.openlocfilehash: dba658d153ea5a8604811dfecc6cf0dabb4f9f24
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552583"
---
# <a name="azure-log-integration-frequently-asked-questions-faq"></a><span data-ttu-id="b7cba-103">Azure log integration frequently asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="b7cba-103">Azure log integration frequently asked questions (FAQ)</span></span>
<span data-ttu-id="b7cba-104">This FAQ answers questions about Azure log integration, a service that enables you to integrate raw logs from your Azure resources into your on-premises Security Information and Event Management (SIEM) systems.</span><span class="sxs-lookup"><span data-stu-id="b7cba-104">This FAQ answers questions about Azure log integration, a service that enables you to integrate raw logs from your Azure resources into your on-premises Security Information and Event Management (SIEM) systems.</span></span> <span data-ttu-id="b7cba-105">This integration provides a unified dashboard for all your assets, on-premises or in the cloud, so that you can aggregate, correlate, analyze, and alert for security events associated with your applications.</span><span class="sxs-lookup"><span data-stu-id="b7cba-105">This integration provides a unified dashboard for all your assets, on-premises or in the cloud, so that you can aggregate, correlate, analyze, and alert for security events associated with your applications.</span></span>

## <a name="is-the-azure-log-integration-software-free"></a><span data-ttu-id="b7cba-106">Is the Azure Log Integration software free?</span><span class="sxs-lookup"><span data-stu-id="b7cba-106">Is the Azure Log Integration software free?</span></span>
<span data-ttu-id="b7cba-107">Yes.</span><span class="sxs-lookup"><span data-stu-id="b7cba-107">Yes.</span></span> <span data-ttu-id="b7cba-108">There is no charge for the Azure Log Integration software.</span><span class="sxs-lookup"><span data-stu-id="b7cba-108">There is no charge for the Azure Log Integration software.</span></span>

## <a name="where-is-azure-log-integration-available"></a><span data-ttu-id="b7cba-109">Where is Azure Log Integration available?</span><span class="sxs-lookup"><span data-stu-id="b7cba-109">Where is Azure Log Integration available?</span></span>

<span data-ttu-id="b7cba-110">It is currently available in Azure commercial and Azure Government and not available in China, or Germany.</span><span class="sxs-lookup"><span data-stu-id="b7cba-110">It is currently available in Azure commercial and Azure Government and not available in China, or Germany.</span></span>

## <a name="how-can-i-see-the-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs-from"></a><span data-ttu-id="b7cba-111">How can I see the storage accounts from which Azure log integration is pulling Azure VM logs from?</span><span class="sxs-lookup"><span data-stu-id="b7cba-111">How can I see the storage accounts from which Azure log integration is pulling Azure VM logs from?</span></span>
<span data-ttu-id="b7cba-112">Run the command **azlog source list**.</span><span class="sxs-lookup"><span data-stu-id="b7cba-112">Run the command **azlog source list**.</span></span>

## <a name="how-can-i-update-the-proxy-configuration"></a><span data-ttu-id="b7cba-113">How can I update the proxy configuration?</span><span class="sxs-lookup"><span data-stu-id="b7cba-113">How can I update the proxy configuration?</span></span>
<span data-ttu-id="b7cba-114">If your proxy setting does not allow Azure storage access directly, open the **AZLOG.EXE.CONFIG** file in **c:\Program Files\Microsoft Azure Log Integration**.</span><span class="sxs-lookup"><span data-stu-id="b7cba-114">If your proxy setting does not allow Azure storage access directly, open the **AZLOG.EXE.CONFIG** file in **c:\Program Files\Microsoft Azure Log Integration**.</span></span> <span data-ttu-id="b7cba-115">Update the file to include the **defaultProxy** section with the proxy address of your organization.</span><span class="sxs-lookup"><span data-stu-id="b7cba-115">Update the file to include the **defaultProxy** section with the proxy address of your organization.</span></span> <span data-ttu-id="b7cba-116">After update is done, stop and start the service using commands **net stop azlog** and **net start azlog**.</span><span class="sxs-lookup"><span data-stu-id="b7cba-116">After update is done, stop and start the service using commands **net stop azlog** and **net start azlog**.</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.net>
        <connectionManagement>
          <add address="*" maxconnection="400" />
        </connectionManagement>
        <defaultProxy>
          <proxy usesystemdefault="true"
          proxyaddress=http://127.0.0.1:8888
          bypassonlocal="true" />
        </defaultProxy>
      </system.net>
      <system.diagnostics>
        <performanceCounters filemappingsize="20971520" />
      </system.diagnostics>   

## <a name="how-can-i-see-the-subscription-information-in-windows-events"></a><span data-ttu-id="b7cba-117">How can I see the subscription information in Windows events?</span><span class="sxs-lookup"><span data-stu-id="b7cba-117">How can I see the subscription information in Windows events?</span></span>
<span data-ttu-id="b7cba-118">Append the **subscriptionid** to the friendly name while adding the source.</span><span class="sxs-lookup"><span data-stu-id="b7cba-118">Append the **subscriptionid** to the friendly name while adding the source.</span></span>

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
<span data-ttu-id="b7cba-119">The event XML has the metadata as shown below, including the subscription id.</span><span class="sxs-lookup"><span data-stu-id="b7cba-119">The event XML has the metadata as shown below, including the subscription id.</span></span>

![Event XML][1]

## <a name="error-messages"></a><span data-ttu-id="b7cba-121">Error messages</span><span class="sxs-lookup"><span data-stu-id="b7cba-121">Error messages</span></span>
### <a name="when-running-command-azlog-createazureid-why-do-i-get-the-following-error"></a><span data-ttu-id="b7cba-122">When running command **azlog createazureid**, why do I get the following error?</span><span class="sxs-lookup"><span data-stu-id="b7cba-122">When running command **azlog createazureid**, why do I get the following error?</span></span>
<span data-ttu-id="b7cba-123">Error:</span><span class="sxs-lookup"><span data-stu-id="b7cba-123">Error:</span></span>

  <span data-ttu-id="b7cba-124">*Failed to create AAD Application - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - Reason = 'Forbidden' - Message = 'Insufficient privileges to complete the operation.'*</span><span class="sxs-lookup"><span data-stu-id="b7cba-124">*Failed to create AAD Application - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - Reason = 'Forbidden' - Message = 'Insufficient privileges to complete the operation.'*</span></span>

<span data-ttu-id="b7cba-125">**Azlog createazureid** attempts to create a service principal in all the Azure AD tenants for the subscriptions on which the Azure login has access to.</span><span class="sxs-lookup"><span data-stu-id="b7cba-125">**Azlog createazureid** attempts to create a service principal in all the Azure AD tenants for the subscriptions on which the Azure login has access to.</span></span> <span data-ttu-id="b7cba-126">If your Azure login is only a Guest user in that Azure AD tenant, then the command fails with ‘Insufficient privileges to complete the operation.’</span><span class="sxs-lookup"><span data-stu-id="b7cba-126">If your Azure login is only a Guest user in that Azure AD tenant, then the command fails with ‘Insufficient privileges to complete the operation.’</span></span> <span data-ttu-id="b7cba-127">Request Tenant admin to add your account as a user in the tenant.</span><span class="sxs-lookup"><span data-stu-id="b7cba-127">Request Tenant admin to add your account as a user in the tenant.</span></span>

### <a name="when-running-command-azlog-authorize-why-do-i-get-the-following-error"></a><span data-ttu-id="b7cba-128">When running command **azlog authorize**, why do I get the following error?</span><span class="sxs-lookup"><span data-stu-id="b7cba-128">When running command **azlog authorize**, why do I get the following error?</span></span>
<span data-ttu-id="b7cba-129">Error:</span><span class="sxs-lookup"><span data-stu-id="b7cba-129">Error:</span></span>

  <span data-ttu-id="b7cba-130">*Warning creating Role Assignment - AuthorizationFailed: The client janedo@microsoft.com' with object id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000'.*</span><span class="sxs-lookup"><span data-stu-id="b7cba-130">*Warning creating Role Assignment - AuthorizationFailed: The client janedo@microsoft.com' with object id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000'.*</span></span>

<span data-ttu-id="b7cba-131">**Azlog authorize** command assigns the role of Reader to the Azure AD service principal (created with **Azlog createazureid**) to the subscriptions provided.</span><span class="sxs-lookup"><span data-stu-id="b7cba-131">**Azlog authorize** command assigns the role of Reader to the Azure AD service principal (created with **Azlog createazureid**) to the subscriptions provided.</span></span> <span data-ttu-id="b7cba-132">If the Azure login is not a Co-Administrator or an Owner of the subscription, it fails with ‘Authorization Failed’ error message.</span><span class="sxs-lookup"><span data-stu-id="b7cba-132">If the Azure login is not a Co-Administrator or an Owner of the subscription, it fails with ‘Authorization Failed’ error message.</span></span> <span data-ttu-id="b7cba-133">Azure role-based access control (RBAC) of Co-Administrator or Owner is needed to complete this action.</span><span class="sxs-lookup"><span data-stu-id="b7cba-133">Azure role-based access control (RBAC) of Co-Administrator or Owner is needed to complete this action.</span></span>

## <a name="where-can-i-find-the-definition-of-the-properties-in-audit-log"></a><span data-ttu-id="b7cba-134">Where can I find the definition of the properties in audit log?</span><span class="sxs-lookup"><span data-stu-id="b7cba-134">Where can I find the definition of the properties in audit log?</span></span>
<span data-ttu-id="b7cba-135">See:</span><span class="sxs-lookup"><span data-stu-id="b7cba-135">See:</span></span>

* [<span data-ttu-id="b7cba-136">Audit operations with Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b7cba-136">Audit operations with Resource Manager</span></span>](../azure-resource-manager/resource-group-audit.md)
* [<span data-ttu-id="b7cba-137">List the management events in a subscription in Azure Monitor REST API</span><span class="sxs-lookup"><span data-stu-id="b7cba-137">List the management events in a subscription in Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a><span data-ttu-id="b7cba-138">Where can I find details on Azure Security Center alerts?</span><span class="sxs-lookup"><span data-stu-id="b7cba-138">Where can I find details on Azure Security Center alerts?</span></span>
<span data-ttu-id="b7cba-139">See [Managing and responding to security alerts in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="b7cba-139">See [Managing and responding to security alerts in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span></span>

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a><span data-ttu-id="b7cba-140">How can I modify what is collected with VM diagnostics?</span><span class="sxs-lookup"><span data-stu-id="b7cba-140">How can I modify what is collected with VM diagnostics?</span></span>
<span data-ttu-id="b7cba-141">See [Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for details on how to Get, Modify, and Set the Azure Diagnostics in Windows *(WAD)* configuration.</span><span class="sxs-lookup"><span data-stu-id="b7cba-141">See [Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for details on how to Get, Modify, and Set the Azure Diagnostics in Windows *(WAD)* configuration.</span></span> <span data-ttu-id="b7cba-142">Following is a sample:</span><span class="sxs-lookup"><span data-stu-id="b7cba-142">Following is a sample:</span></span>

### <a name="get-the-wad-config"></a><span data-ttu-id="b7cba-143">Get the WAD config</span><span class="sxs-lookup"><span data-stu-id="b7cba-143">Get the WAD config</span></span>
    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

### <a name="modify-the-wad-config"></a><span data-ttu-id="b7cba-144">Modify the WAD Config</span><span class="sxs-lookup"><span data-stu-id="b7cba-144">Modify the WAD Config</span></span>
<span data-ttu-id="b7cba-145">The following example is a configuration where only EventID 4624 and EventId 4625 are collected from the security event log.</span><span class="sxs-lookup"><span data-stu-id="b7cba-145">The following example is a configuration where only EventID 4624 and EventId 4625 are collected from the security event log.</span></span> <span data-ttu-id="b7cba-146">Microsoft Antimalware events are collected from the System event log.</span><span class="sxs-lookup"><span data-stu-id="b7cba-146">Microsoft Antimalware events are collected from the System event log.</span></span> <span data-ttu-id="b7cba-147">See [Consuming Events](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85) for details on the use of XPath expressions.</span><span class="sxs-lookup"><span data-stu-id="b7cba-147">See [Consuming Events](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85) for details on the use of XPath expressions.</span></span>

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

### <a name="set-the-wad-configuration"></a><span data-ttu-id="b7cba-148">Set the WAD configuration</span><span class="sxs-lookup"><span data-stu-id="b7cba-148">Set the WAD configuration</span></span>
    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

<span data-ttu-id="b7cba-149">After making changes, check the storage account to ensure that the correct events are collected.</span><span class="sxs-lookup"><span data-stu-id="b7cba-149">After making changes, check the storage account to ensure that the correct events are collected.</span></span>

<span data-ttu-id="b7cba-150">If you run into any issues during the installation and configuration, please open a [support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request), select **Log Integration** as the service for which you are requesting support.</span><span class="sxs-lookup"><span data-stu-id="b7cba-150">If you run into any issues during the installation and configuration, please open a [support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request), select **Log Integration** as the service for which you are requesting support.</span></span>


<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security/media/security-azure-log-integration-faq/event-xml.png

