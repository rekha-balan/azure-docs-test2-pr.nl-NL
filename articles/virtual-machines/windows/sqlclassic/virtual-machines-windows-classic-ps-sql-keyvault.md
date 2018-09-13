---
title: Integrate Key Vault with SQL Server on Windows VMs in Azure (Classic) | Microsoft Docs
description: Learn how to automate the configuration of SQL Server encryption for use with Azure Key Vault. This topic explains how to use Azure Key Vault Integration with SQL Server virtual machines create in the classic deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: rothja
manager: jhubbard
editor: ''
tags: azure-service-management
ms.assetid: ab8d41a7-1971-4032-ab71-eb435c455dc1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 02/17/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2a9ac5763bb934bd0646e47c3936f7bdd0d603b1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549485"
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-classic"></a><span data-ttu-id="1367c-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Classic)</span><span class="sxs-lookup"><span data-stu-id="1367c-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-ps-sql-keyvault.md)
> * [Classic](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="1367c-107">Overview</span><span class="sxs-lookup"><span data-stu-id="1367c-107">Overview</span></span>
<span data-ttu-id="1367c-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span><span class="sxs-lookup"><span data-stu-id="1367c-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span></span> <span data-ttu-id="1367c-109">These forms of encryption require you to manage and store the cryptographic keys you use for encryption.</span><span class="sxs-lookup"><span data-stu-id="1367c-109">These forms of encryption require you to manage and store the cryptographic keys you use for encryption.</span></span> <span data-ttu-id="1367c-110">The Azure Key Vault (AKV) service is designed to improve the security and management of these keys in a secure and highly available location.</span><span class="sxs-lookup"><span data-stu-id="1367c-110">The Azure Key Vault (AKV) service is designed to improve the security and management of these keys in a secure and highly available location.</span></span> <span data-ttu-id="1367c-111">The [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server to use these keys from Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1367c-111">The [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server to use these keys from Azure Key Vault.</span></span>

> [!IMPORTANT] 
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model.

<span data-ttu-id="1367c-115">If you are running SQL Server with on-premises machines, there are [steps you can follow to access Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span><span class="sxs-lookup"><span data-stu-id="1367c-115">If you are running SQL Server with on-premises machines, there are [steps you can follow to access Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span></span> <span data-ttu-id="1367c-116">But for SQL Server in Azure VMs, you can save time by using the *Azure Key Vault Integration* feature.</span><span class="sxs-lookup"><span data-stu-id="1367c-116">But for SQL Server in Azure VMs, you can save time by using the *Azure Key Vault Integration* feature.</span></span> <span data-ttu-id="1367c-117">With a few Azure PowerShell cmdlets to enable this feature, you can automate the configuration necessary for a SQL VM to access your key vault.</span><span class="sxs-lookup"><span data-stu-id="1367c-117">With a few Azure PowerShell cmdlets to enable this feature, you can automate the configuration necessary for a SQL VM to access your key vault.</span></span>

<span data-ttu-id="1367c-118">When this feature is enabled, it automatically installs the SQL Server Connector, configures the EKM provider to access Azure Key Vault, and creates the credential to allow you to access your vault.</span><span class="sxs-lookup"><span data-stu-id="1367c-118">When this feature is enabled, it automatically installs the SQL Server Connector, configures the EKM provider to access Azure Key Vault, and creates the credential to allow you to access your vault.</span></span> <span data-ttu-id="1367c-119">If you looked at the steps in the previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span><span class="sxs-lookup"><span data-stu-id="1367c-119">If you looked at the steps in the previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span></span> <span data-ttu-id="1367c-120">The only thing you would still need to do manually is to create the key vault and keys.</span><span class="sxs-lookup"><span data-stu-id="1367c-120">The only thing you would still need to do manually is to create the key vault and keys.</span></span> <span data-ttu-id="1367c-121">From there, the entire setup of your SQL VM is automated.</span><span class="sxs-lookup"><span data-stu-id="1367c-121">From there, the entire setup of your SQL VM is automated.</span></span> <span data-ttu-id="1367c-122">Once this feature has completed this setup, you can execute T-SQL statements to begin encrypting your databases or backups as you normally would.</span><span class="sxs-lookup"><span data-stu-id="1367c-122">Once this feature has completed this setup, you can execute T-SQL statements to begin encrypting your databases or backups as you normally would.</span></span>

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="configure-akv-integration"></a><span data-ttu-id="1367c-123">Configure AKV Integration</span><span class="sxs-lookup"><span data-stu-id="1367c-123">Configure AKV Integration</span></span>
<span data-ttu-id="1367c-124">Use PowerShell to configure Azure Key Vault Integration.</span><span class="sxs-lookup"><span data-stu-id="1367c-124">Use PowerShell to configure Azure Key Vault Integration.</span></span> <span data-ttu-id="1367c-125">The following sections provide an overview of the required parameters and then a sample PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="1367c-125">The following sections provide an overview of the required parameters and then a sample PowerShell script.</span></span>

### <a name="install-the-sql-server-iaas-extension"></a><span data-ttu-id="1367c-126">Install the SQL Server IaaS Extension</span><span class="sxs-lookup"><span data-stu-id="1367c-126">Install the SQL Server IaaS Extension</span></span>
<span data-ttu-id="1367c-127">First, [install the SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="1367c-127">First, [install the SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

### <a name="understand-the-input-parameters"></a><span data-ttu-id="1367c-128">Understand the input parameters</span><span class="sxs-lookup"><span data-stu-id="1367c-128">Understand the input parameters</span></span>
<span data-ttu-id="1367c-129">The following table lists the parameters required to run the PowerShell script in the next section.</span><span class="sxs-lookup"><span data-stu-id="1367c-129">The following table lists the parameters required to run the PowerShell script in the next section.</span></span>

| <span data-ttu-id="1367c-130">Parameter</span><span class="sxs-lookup"><span data-stu-id="1367c-130">Parameter</span></span> | <span data-ttu-id="1367c-131">Description</span><span class="sxs-lookup"><span data-stu-id="1367c-131">Description</span></span> | <span data-ttu-id="1367c-132">Example</span><span class="sxs-lookup"><span data-stu-id="1367c-132">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1367c-133">**$akvURL**</span><span class="sxs-lookup"><span data-stu-id="1367c-133">**$akvURL**</span></span> |<span data-ttu-id="1367c-134">**The key vault URL**</span><span class="sxs-lookup"><span data-stu-id="1367c-134">**The key vault URL**</span></span> |<span data-ttu-id="1367c-135">"https://contosokeyvault.vault.azure.net/"</span><span class="sxs-lookup"><span data-stu-id="1367c-135">"https://contosokeyvault.vault.azure.net/"</span></span> |
| <span data-ttu-id="1367c-136">**$spName**</span><span class="sxs-lookup"><span data-stu-id="1367c-136">**$spName**</span></span> |<span data-ttu-id="1367c-137">**Service Principal name**</span><span class="sxs-lookup"><span data-stu-id="1367c-137">**Service Principal name**</span></span> |<span data-ttu-id="1367c-138">"fde2b411-33d5-4e11-af04eb07b669ccf2"</span><span class="sxs-lookup"><span data-stu-id="1367c-138">"fde2b411-33d5-4e11-af04eb07b669ccf2"</span></span> |
| <span data-ttu-id="1367c-139">**$spSecret**</span><span class="sxs-lookup"><span data-stu-id="1367c-139">**$spSecret**</span></span> |<span data-ttu-id="1367c-140">**Service Principal secret**</span><span class="sxs-lookup"><span data-stu-id="1367c-140">**Service Principal secret**</span></span> |<span data-ttu-id="1367c-141">"9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="</span><span class="sxs-lookup"><span data-stu-id="1367c-141">"9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="</span></span> |
| <span data-ttu-id="1367c-142">**$credName**</span><span class="sxs-lookup"><span data-stu-id="1367c-142">**$credName**</span></span> |<span data-ttu-id="1367c-143">**Credential name**: AKV Integration creates a credential within SQL Server, allowing the VM to have access to the key vault.</span><span class="sxs-lookup"><span data-stu-id="1367c-143">**Credential name**: AKV Integration creates a credential within SQL Server, allowing the VM to have access to the key vault.</span></span> <span data-ttu-id="1367c-144">Choose a name for this credential.</span><span class="sxs-lookup"><span data-stu-id="1367c-144">Choose a name for this credential.</span></span> |<span data-ttu-id="1367c-145">"mycred1"</span><span class="sxs-lookup"><span data-stu-id="1367c-145">"mycred1"</span></span> |
| <span data-ttu-id="1367c-146">**$vmName**</span><span class="sxs-lookup"><span data-stu-id="1367c-146">**$vmName**</span></span> |<span data-ttu-id="1367c-147">**Virtual machine name**: The name of a previously created SQL VM.</span><span class="sxs-lookup"><span data-stu-id="1367c-147">**Virtual machine name**: The name of a previously created SQL VM.</span></span> |<span data-ttu-id="1367c-148">"myvmname"</span><span class="sxs-lookup"><span data-stu-id="1367c-148">"myvmname"</span></span> |
| <span data-ttu-id="1367c-149">**$serviceName**</span><span class="sxs-lookup"><span data-stu-id="1367c-149">**$serviceName**</span></span> |<span data-ttu-id="1367c-150">**Service name**: The Cloud Service name that is associated with the SQL VM.</span><span class="sxs-lookup"><span data-stu-id="1367c-150">**Service name**: The Cloud Service name that is associated with the SQL VM.</span></span> |<span data-ttu-id="1367c-151">"mycloudservicename"</span><span class="sxs-lookup"><span data-stu-id="1367c-151">"mycloudservicename"</span></span> |

### <a name="enable-akv-integration-with-powershell"></a><span data-ttu-id="1367c-152">Enable AKV Integration with PowerShell</span><span class="sxs-lookup"><span data-stu-id="1367c-152">Enable AKV Integration with PowerShell</span></span>
<span data-ttu-id="1367c-153">The **New-AzureVMSqlServerKeyVaultCredentialConfig** cmdlet creates a configuration object for the Azure Key Vault Integration feature.</span><span class="sxs-lookup"><span data-stu-id="1367c-153">The **New-AzureVMSqlServerKeyVaultCredentialConfig** cmdlet creates a configuration object for the Azure Key Vault Integration feature.</span></span> <span data-ttu-id="1367c-154">The **Set-AzureVMSqlServerExtension** configures this integration with the **KeyVaultCredentialSettings** parameter.</span><span class="sxs-lookup"><span data-stu-id="1367c-154">The **Set-AzureVMSqlServerExtension** configures this integration with the **KeyVaultCredentialSettings** parameter.</span></span> <span data-ttu-id="1367c-155">The following steps show how to use these commands.</span><span class="sxs-lookup"><span data-stu-id="1367c-155">The following steps show how to use these commands.</span></span>

1. <span data-ttu-id="1367c-156">In Azure PowerShell, first configure the input parameters with your specific values as described in the previous sections of this topic.</span><span class="sxs-lookup"><span data-stu-id="1367c-156">In Azure PowerShell, first configure the input parameters with your specific values as described in the previous sections of this topic.</span></span> <span data-ttu-id="1367c-157">The following script is an example.</span><span class="sxs-lookup"><span data-stu-id="1367c-157">The following script is an example.</span></span>
   
        $akvURL = "https://contosokeyvault.vault.azure.net/"
        $spName = "fde2b411-33d5-4e11-af04eb07b669ccf2"
        $spSecret = "9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM="
        $credName = "mycred1"
        $vmName = "myvmname"
        $serviceName = "mycloudservicename"
2. <span data-ttu-id="1367c-158">Then use the following script to configure and enable AKV Integration.</span><span class="sxs-lookup"><span data-stu-id="1367c-158">Then use the following script to configure and enable AKV Integration.</span></span>
   
        $secureakv =  $spSecret | ConvertTo-SecureString -AsPlainText -Force
        $akvs = New-AzureVMSqlServerKeyVaultCredentialConfig -Enable -CredentialName $credname -AzureKeyVaultUrl $akvURL -ServicePrincipalName $spName -ServicePrincipalSecret $secureakv
        Get-AzureVM -ServiceName $serviceName -Name $vmName | Set-AzureVMSqlServerExtension -KeyVaultCredentialSettings $akvs | Update-AzureVM

<span data-ttu-id="1367c-159">The SQL IaaS Agent Extension will update the SQL VM with this new configuration.</span><span class="sxs-lookup"><span data-stu-id="1367c-159">The SQL IaaS Agent Extension will update the SQL VM with this new configuration.</span></span>

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

