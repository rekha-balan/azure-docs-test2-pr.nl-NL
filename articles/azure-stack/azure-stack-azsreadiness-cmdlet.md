---
title: Start-AzsReadinessChecker cmdlet reference | Microsoft Docs
description: PowerShell cmdlet help for the Azure Stack Readiness Checker module.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/08/2018
ms.author: brenduns
ms.reviewer: ''
ms.openlocfilehash: 8481fbd6c7cb82b34070f9bc8cc6d7f3f4b2518c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871397"
---
# <a name="start-azsreadinesschecker-cmdlet-reference"></a><span data-ttu-id="acb78-103">Start-AzsReadinessChecker cmdlet reference</span><span class="sxs-lookup"><span data-stu-id="acb78-103">Start-AzsReadinessChecker cmdlet reference</span></span>

<span data-ttu-id="acb78-104">Module: Microsoft.AzureStack.ReadinessChecker</span><span class="sxs-lookup"><span data-stu-id="acb78-104">Module: Microsoft.AzureStack.ReadinessChecker</span></span>

<span data-ttu-id="acb78-105">This module only contains a single cmdlet.</span><span class="sxs-lookup"><span data-stu-id="acb78-105">This module only contains a single cmdlet.</span></span>  <span data-ttu-id="acb78-106">This cmdlet performs one or more pre-deployment or pre-servicing functions for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="acb78-106">This cmdlet performs one or more pre-deployment or pre-servicing functions for Azure Stack.</span></span>

## <a name="syntax"></a><span data-ttu-id="acb78-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="acb78-107">Syntax</span></span>
```PowerShell
Start-AzsReadinessChecker
       [-CertificatePath <String>]
       -PfxPassword <SecureString>
       -RegionName <String>
       -FQDN <String>
       -IdentitySystem <String>
       [-CleanReport]
       [-OutputPath <String>]
       [-WhatIf]
       [-Confirm]
       [<CommonParameters>]
```

```PowerShell
Start-AzsReadinessChecker
       [-CertificatePath <String>]
       -PfxPassword <SecureString>
       -DeploymentDataJSONPath <String>
       [-CleanReport]
       [-OutputPath <String>]
       [-WhatIf]
       [-Confirm]
       [<CommonParameters>]
```

```PowerShell
Start-AzsReadinessChecker
       -PaaSCertificates <Hashtable>
       -DeploymentDataJSONPath <String>
       [-OutputPath <String>]
       [-WhatIf]
       [-Confirm]
       [<CommonParameters>]
```

```PowerShell
Start-AzsReadinessChecker
       -PaaSCertificates <Hashtable>
       -RegionName <String>
       -FQDN <String>
       -IdentitySystem <String>
       [-OutputPath <String>]
       [-WhatIf]
       [-Confirm]
       [<CommonParameters>]
```

```PowerShell
Start-AzsReadinessChecker
       -RegionName <String>
       -FQDN <String>
       -IdentitySystem <String>
       -Subject <OrderedDictionary>
       -RequestType <String>
       [-IncludePaaS]
       -OutputRequestPath <String>
       [-OutputPath <String>]
       [-WhatIf]
       [-Confirm]
       [<CommonParameters>]
```

```PowerShell
Start-AzsReadinessChecker
       -PfxPassword <SecureString>
       -PfxPath <String>
       -ExportPFXPath <String>
       [-OutputPath <String>]
       [-WhatIf]
       [-Confirm]
       [<CommonParameters>]
```


```PowerShell
Start-AzsReadinessChecker
       -AADServiceAdministrator <PSCredential>
       -AADDirectoryTenantName <String>
       -IdentitySystem <String>
       -AzureEnvironment <String>
       [-CleanReport]
       [-OutputPath <String>]
       [-WhatIf]
       [-Confirm]
       [<CommonParameters>]
```

```PowerShell
Start-AzsReadinessChecker
       -AADServiceAdministrator <PSCredential>
       -DeploymentDataJSONPath <String>
       [-CleanReport]
       [-OutputPath <String>]
       [-WhatIf]
       [-Confirm]
       [<CommonParameters>]
```

```PowerShell
Start-AzsReadinessChecker
       -RegistrationAccount <PSCredential>
       -RegistrationSubscriptionID <Guid>
       -AzureEnvironment <String>
       [-CleanReport]
       [-OutputPath <String>]
       [-WhatIf]
       [-Confirm]
       [<CommonParameters>]
```

```PowerShell
Start-AzsReadinessChecker
       -RegistrationAccount <PSCredential>
       -RegistrationSubscriptionID <Guid>
       -DeploymentDataJSONPath <String>
       [-CleanReport]
       [-OutputPath <String>]
       [-WhatIf]
       [-Confirm]
       [<CommonParameters>]
```

```PowerShell
Start-AzsReadinessChecker
       -ReportPath <String>
       [-ReportSections <String>]
       [-Summary]
       [-OutputPath <String>]
       [-WhatIf]
       [-Confirm]
       [<CommonParameters>]
```





 ## <a name="description"></a><span data-ttu-id="acb78-108">Description</span><span class="sxs-lookup"><span data-stu-id="acb78-108">Description</span></span>
<span data-ttu-id="acb78-109">The **Start-AzsReadinessChecker** cmdlet validates certificates, Azure accounts, Azure subscriptions, and Azure Active Directories.</span><span class="sxs-lookup"><span data-stu-id="acb78-109">The **Start-AzsReadinessChecker** cmdlet validates certificates, Azure accounts, Azure subscriptions, and Azure Active Directories.</span></span> <span data-ttu-id="acb78-110">Run validation before deploying Azure Stack, or before Azure Stack servicing actions like Secret Rotation.</span><span class="sxs-lookup"><span data-stu-id="acb78-110">Run validation before deploying Azure Stack, or before Azure Stack servicing actions like Secret Rotation.</span></span> <span data-ttu-id="acb78-111">The cmdlet can also be used to generate Certificate Signing Requests for infrastructure certificates and optionally PaaS certificates.</span><span class="sxs-lookup"><span data-stu-id="acb78-111">The cmdlet can also be used to generate Certificate Signing Requests for infrastructure certificates and optionally PaaS certificates.</span></span>  <span data-ttu-id="acb78-112">Finally, the cmdlet can repackage PFX certificates to remediate common packaging issues.</span><span class="sxs-lookup"><span data-stu-id="acb78-112">Finally, the cmdlet can repackage PFX certificates to remediate common packaging issues.</span></span>

## <a name="examples"></a><span data-ttu-id="acb78-113">Examples</span><span class="sxs-lookup"><span data-stu-id="acb78-113">Examples</span></span>
<span data-ttu-id="acb78-114">**Example: Generate Certificate Signing Request**</span><span class="sxs-lookup"><span data-stu-id="acb78-114">**Example: Generate Certificate Signing Request**</span></span>

```PowerShell
$regionName = 'east'
$externalFQDN = 'azurestack.contoso.com'
$subjectHash = [ordered]@{"OU"="AzureStack";"O"="Microsoft";"L"="Redmond";"ST"="Washington";"C"="US"}
Start-AzsReadinessChecker -regionName $regionName -externalFQDN $externalFQDN -subjectName $subjectHash -IdentitySystem ADFS -requestType MultipleCSR
```

<span data-ttu-id="acb78-115">In this example, Start-AzsReadinessChecker generates multiple Certificate Signing Requests (CSR) for certificates suitable for an ADFS Azure Stack deployment with a region name of “east” and an external FQDN of “azurestack.contoso.com”</span><span class="sxs-lookup"><span data-stu-id="acb78-115">In this example, Start-AzsReadinessChecker generates multiple Certificate Signing Requests (CSR) for certificates suitable for an ADFS Azure Stack deployment with a region name of “east” and an external FQDN of “azurestack.contoso.com”</span></span>

<span data-ttu-id="acb78-116">**Example: Validate certificates**</span><span class="sxs-lookup"><span data-stu-id="acb78-116">**Example: Validate certificates**</span></span>
```PowerShell
$password = Read-Host -Prompt "Enter PFX Password" -AsSecureString
Start-AzsReadinessChecker -CertificatePath .\Certificates\ -PfxPassword $password -RegionName east -FQDN azurestack.contoso.com -IdentitySystem AAD
```

<span data-ttu-id="acb78-117">In this example, the PFX password is prompted for securely and Start-AzsReadinessChecker checks the relative folder “Certificates” for certificates valid for an AAD deployment with a region name of “east” and an external FQDN of “azurestack.contoso.com”</span><span class="sxs-lookup"><span data-stu-id="acb78-117">In this example, the PFX password is prompted for securely and Start-AzsReadinessChecker checks the relative folder “Certificates” for certificates valid for an AAD deployment with a region name of “east” and an external FQDN of “azurestack.contoso.com”</span></span> 

<span data-ttu-id="acb78-118">**Example: Validate certificates with deployment data (deployment and support)**</span><span class="sxs-lookup"><span data-stu-id="acb78-118">**Example: Validate certificates with deployment data (deployment and support)**</span></span>
```PowerShell
$password = Read-Host -Prompt "Enter PFX Password" -AsSecureString
Start-AzsReadinessChecker -CertificatePath .\Certificates\ -PfxPassword $password -DeploymentDataJSONPath .\deploymentdata.json
```
<span data-ttu-id="acb78-119">In this deployment and support example, the PFX password is prompted for securely and Start-AzsReadinessChecker checks the relative folder “Certificates” for certificates valid for a deployment where identity, region and external FQDN are read from the deployment data JSON file generated for deployment.</span><span class="sxs-lookup"><span data-stu-id="acb78-119">In this deployment and support example, the PFX password is prompted for securely and Start-AzsReadinessChecker checks the relative folder “Certificates” for certificates valid for a deployment where identity, region and external FQDN are read from the deployment data JSON file generated for deployment.</span></span> 

<span data-ttu-id="acb78-120">**Example: Validate PaaS certificates**</span><span class="sxs-lookup"><span data-stu-id="acb78-120">**Example: Validate PaaS certificates**</span></span>
```PowerShell
$PaaSCertificates = @{
    'PaaSDBCert' = @{'pfxPath' = '<Path to DBAdapter PFX>';'pfxPassword' = (ConvertTo-SecureString -String '<Password for PFX>' -AsPlainText -Force)}
    'PaaSDefaultCert' = @{'pfxPath' = '<Path to Default PFX>';'pfxPassword' = (ConvertTo-SecureString -String '<Password for PFX>' -AsPlainText -Force)}
    'PaaSAPICert' = @{'pfxPath' = '<Path to API PFX>';'pfxPassword' = (ConvertTo-SecureString -String '<Password for PFX>' -AsPlainText -Force)}
    'PaaSFTPCert' = @{'pfxPath' = '<Path to FTP PFX>';'pfxPassword' = (ConvertTo-SecureString -String '<Password for PFX>' -AsPlainText -Force)}
    'PaaSSSOCert' = @{'pfxPath' = '<Path to SSO PFX>';'pfxPassword' = (ConvertTo-SecureString -String '<Password for PFX>' -AsPlainText -Force)}
}
Start-AzsReadinessChecker -PaaSCertificates $PaaSCertificates – RegionName east -FQDN azurestack.contoso.com
```

<span data-ttu-id="acb78-121">In this example, a hashtable is constructed with paths and passwords to each PaaS certificate.</span><span class="sxs-lookup"><span data-stu-id="acb78-121">In this example, a hashtable is constructed with paths and passwords to each PaaS certificate.</span></span> <span data-ttu-id="acb78-122">Certificates can be omitted.</span><span class="sxs-lookup"><span data-stu-id="acb78-122">Certificates can be omitted.</span></span> <span data-ttu-id="acb78-123">Start-AzsReadinessChecker checks each PFX Path exists and validates them using the region ‘east’ and external FQDN ‘azurestack.contoso.com’.</span><span class="sxs-lookup"><span data-stu-id="acb78-123">Start-AzsReadinessChecker checks each PFX Path exists and validates them using the region ‘east’ and external FQDN ‘azurestack.contoso.com’.</span></span>

<span data-ttu-id="acb78-124">**Example: Validate PaaS certificates with deployment data**</span><span class="sxs-lookup"><span data-stu-id="acb78-124">**Example: Validate PaaS certificates with deployment data**</span></span>
```PowerShell
$PaaSCertificates = @{
    'PaaSDBCert' = @{'pfxPath' = '<Path to DBAdapter PFX>';'pfxPassword' = (ConvertTo-SecureString -String '<Password for PFX>' -AsPlainText -Force)}
    'PaaSDefaultCert' = @{'pfxPath' = '<Path to Default PFX>';'pfxPassword' = (ConvertTo-SecureString -String '<Password for PFX>' -AsPlainText -Force)}
    'PaaSAPICert' = @{'pfxPath' = '<Path to API PFX>';'pfxPassword' = (ConvertTo-SecureString -String '<Password for PFX>' -AsPlainText -Force)}
    'PaaSFTPCert' = @{'pfxPath' = '<Path to FTP PFX>';'pfxPassword' = (ConvertTo-SecureString -String '<Password for PFX>' -AsPlainText -Force)}
    'PaaSSSOCert' = @{'pfxPath' = '<Path to SSO PFX>';'pfxPassword' = (ConvertTo-SecureString -String '<Password for PFX>' -AsPlainText -Force)}
}
Start-AzsReadinessChecker -PaaSCertificates $PaaSCertificates -DeploymentDataJSONPath .\deploymentdata.json
```

<span data-ttu-id="acb78-125">In this example, a hashtable is constructed with paths and passwords to each PaaS certificate.</span><span class="sxs-lookup"><span data-stu-id="acb78-125">In this example, a hashtable is constructed with paths and passwords to each PaaS certificate.</span></span> <span data-ttu-id="acb78-126">Certificates can be omitted.</span><span class="sxs-lookup"><span data-stu-id="acb78-126">Certificates can be omitted.</span></span> <span data-ttu-id="acb78-127">Start-AzsReadinessChecker checks each PFX Path exists and validates them using the region and external FQDN read from the deployment data JSON file generated for deployment.</span><span class="sxs-lookup"><span data-stu-id="acb78-127">Start-AzsReadinessChecker checks each PFX Path exists and validates them using the region and external FQDN read from the deployment data JSON file generated for deployment.</span></span> 

<span data-ttu-id="acb78-128">**Example: Validate Azure identity**</span><span class="sxs-lookup"><span data-stu-id="acb78-128">**Example: Validate Azure identity**</span></span>
```PowerShell
$serviceAdminCredential = Get-Credential -Message "Enter Credentials for Service Administrator of Azure Active Directory Tenant e.g. serviceadmin@contoso.onmicrosoft.com"
Start-AzsReadinessChecker -AADServiceAdministrator $serviceAdminCredential -AzureEnvironment AzureCloud -AzureDirectoryTenantName azurestack.contoso.com
```

<span data-ttu-id="acb78-129">In this example, the Service Admin account credentials are prompted for securely and Start-AzsReadinessChecker checks the Azure account and Azure Active Directory are valid for an AAD deployment with a tenant directory name of “azurestack.contoso.com”</span><span class="sxs-lookup"><span data-stu-id="acb78-129">In this example, the Service Admin account credentials are prompted for securely and Start-AzsReadinessChecker checks the Azure account and Azure Active Directory are valid for an AAD deployment with a tenant directory name of “azurestack.contoso.com”</span></span>


<span data-ttu-id="acb78-130">**Example: Validate Azure identity with deployment data (deployment support)**</span><span class="sxs-lookup"><span data-stu-id="acb78-130">**Example: Validate Azure identity with deployment data (deployment support)**</span></span>
```PowerSHell
$serviceAdminCredential = Get-Credential -Message "Enter Credentials for Service Administrator of Azure Active Directory Tenant e.g. serviceadmin@contoso.onmicrosoft.com"
Start-AzsReadinessChecker -AADServiceAdministrator $serviceAdminCredential -DeploymentDataJSONPath .\contoso-depploymentdata.json
```

<span data-ttu-id="acb78-131">In this example, the Service Admin account credentials are prompted for securely and Start-AzsReadinessChecker checks the Azure account and Azure Active Directory are valid for an AAD deployment where AzureCloud and TenantName are read from the deployment data JSON file generated for the deployment.</span><span class="sxs-lookup"><span data-stu-id="acb78-131">In this example, the Service Admin account credentials are prompted for securely and Start-AzsReadinessChecker checks the Azure account and Azure Active Directory are valid for an AAD deployment where AzureCloud and TenantName are read from the deployment data JSON file generated for the deployment.</span></span>


<span data-ttu-id="acb78-132">**Example: Validate Azure registration**</span><span class="sxs-lookup"><span data-stu-id="acb78-132">**Example: Validate Azure registration**</span></span>
```PowerShell
$registrationCredential = Get-Credential -Message "Enter Credentials for Subscription Owner"e.g. subscriptionowner@contoso.onmicrosoft.com"
$subscriptionID = "f7c26209-cd2d-4625-86ba-724ebeece794"
Start-AzsReadinessChecker -RegistrationAccount $registrationCredential -RegistrationSubscriptionID $subscriptionID -AzureEnvironment AzureCloud
```

<span data-ttu-id="acb78-133">In this example, the Subscription Owner credentials are prompted for securely and Start-AzsReadinessChecker then performs validation against the given account and subscription to ensure it can be used for Azure Stack registration.</span><span class="sxs-lookup"><span data-stu-id="acb78-133">In this example, the Subscription Owner credentials are prompted for securely and Start-AzsReadinessChecker then performs validation against the given account and subscription to ensure it can be used for Azure Stack registration.</span></span> 


<span data-ttu-id="acb78-134">**Example: Validate Azure registration with deployment data (deployment team)**</span><span class="sxs-lookup"><span data-stu-id="acb78-134">**Example: Validate Azure registration with deployment data (deployment team)**</span></span>
```PowerShell
$registrationCredential = Get-Credential -Message "Enter Credentials for Subscription Owner"e.g. subscriptionowner@contoso.onmicrosoft.com"
$subscriptionID = "f7c26209-cd2d-4625-86ba-724ebeece794"
Start-AzsReadinessChecker -RegistrationAccount $registrationCredential -RegistrationSubscriptionID $subscriptionID -DeploymentDataJSONPath .\contoso-deploymentdata.json
```

<span data-ttu-id="acb78-135">In this example, the Subscription Owner credentials are prompted for securely and Start-AzsReadinessChecker then performs validation against the given account and subscription to ensure it can be used for Azure Stack registration where additional details are read from the deployment data JSON file generated for the deployment.</span><span class="sxs-lookup"><span data-stu-id="acb78-135">In this example, the Subscription Owner credentials are prompted for securely and Start-AzsReadinessChecker then performs validation against the given account and subscription to ensure it can be used for Azure Stack registration where additional details are read from the deployment data JSON file generated for the deployment.</span></span>

<span data-ttu-id="acb78-136">**Example: Import/Export PFX package**</span><span class="sxs-lookup"><span data-stu-id="acb78-136">**Example: Import/Export PFX package**</span></span>
```PowerShell
$password = Read-Host -Prompt "Enter PFX Password" -AsSecureString
Start-AzsReadinessChecker -PfxPassword $password -PfxPath .\certificates\ssl.pfx -ExportPFXPath .\certificates\ssl_new.pfx
```

<span data-ttu-id="acb78-137">In this example, the PFX password is prompted for securely.</span><span class="sxs-lookup"><span data-stu-id="acb78-137">In this example, the PFX password is prompted for securely.</span></span> <span data-ttu-id="acb78-138">The ssl.pfx file will be imported into the local machine certificate store and re-exported with the same password and saved as ssl_new.pfx.</span><span class="sxs-lookup"><span data-stu-id="acb78-138">The ssl.pfx file will be imported into the local machine certificate store and re-exported with the same password and saved as ssl_new.pfx.</span></span>  <span data-ttu-id="acb78-139">This procedure is for use when certificate validation flagged that a private key does not have the Local Machine attribute set, the certificate chain is broken, irrelevant certificates are present in the PFX or the certificate chain is in the wrong order.</span><span class="sxs-lookup"><span data-stu-id="acb78-139">This procedure is for use when certificate validation flagged that a private key does not have the Local Machine attribute set, the certificate chain is broken, irrelevant certificates are present in the PFX or the certificate chain is in the wrong order.</span></span>


<span data-ttu-id="acb78-140">**Example: View validation report (deployment support)**</span><span class="sxs-lookup"><span data-stu-id="acb78-140">**Example: View validation report (deployment support)**</span></span>
```PowerShell
Start-AzsReadinessChecker -ReportPath Contoso-AzsReadinessReport.json
```

<span data-ttu-id="acb78-141">In this example, the deployment or support team receive the readiness report from the customer (Contoso) and use Start-AzsReadinessChecker to view the status of the validation executions Contoso performed.</span><span class="sxs-lookup"><span data-stu-id="acb78-141">In this example, the deployment or support team receive the readiness report from the customer (Contoso) and use Start-AzsReadinessChecker to view the status of the validation executions Contoso performed.</span></span>

<span data-ttu-id="acb78-142">**Example: View validation report summary for certificate validation only (deployment and support)**</span><span class="sxs-lookup"><span data-stu-id="acb78-142">**Example: View validation report summary for certificate validation only (deployment and support)**</span></span>
```PowerShell
Start-AzsReadinessChecker -ReportPath Contoso-AzsReadinessReport.json -ReportSections Certificate -Summary
```

<span data-ttu-id="acb78-143">In this example, the deployment or support team receive the readiness report from the customer Contoso and use Start-AzsReadinessChecker to view a summarized status of the certificate validation executions Contoso performed.</span><span class="sxs-lookup"><span data-stu-id="acb78-143">In this example, the deployment or support team receive the readiness report from the customer Contoso and use Start-AzsReadinessChecker to view a summarized status of the certificate validation executions Contoso performed.</span></span>



## <a name="required-parameters"></a><span data-ttu-id="acb78-144">Required parameters</span><span class="sxs-lookup"><span data-stu-id="acb78-144">Required parameters</span></span>
> <span data-ttu-id="acb78-145">-RegionName</span><span class="sxs-lookup"><span data-stu-id="acb78-145">-RegionName</span></span>

<span data-ttu-id="acb78-146">Specifies the Azure Stack deployment's region name.</span><span class="sxs-lookup"><span data-stu-id="acb78-146">Specifies the Azure Stack deployment's region name.</span></span>
|  |  |
|----------------------------|--------------|
|<span data-ttu-id="acb78-147">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-147">Type:</span></span>                       |<span data-ttu-id="acb78-148">String</span><span class="sxs-lookup"><span data-stu-id="acb78-148">String</span></span>        |
|<span data-ttu-id="acb78-149">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-149">Position:</span></span>                   |<span data-ttu-id="acb78-150">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-150">Named</span></span>         |
|<span data-ttu-id="acb78-151">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-151">Default value:</span></span>              |<span data-ttu-id="acb78-152">None</span><span class="sxs-lookup"><span data-stu-id="acb78-152">None</span></span>          |
|<span data-ttu-id="acb78-153">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-153">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-154">False</span><span class="sxs-lookup"><span data-stu-id="acb78-154">False</span></span>         |
|<span data-ttu-id="acb78-155">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-155">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-156">False</span><span class="sxs-lookup"><span data-stu-id="acb78-156">False</span></span>         |

> <span data-ttu-id="acb78-157">-FQDN</span><span class="sxs-lookup"><span data-stu-id="acb78-157">-FQDN</span></span>    

<span data-ttu-id="acb78-158">Specifies the Azure Stack deployment's external FQDN, also aliased as ExternalFQDN and ExternalDomainName.</span><span class="sxs-lookup"><span data-stu-id="acb78-158">Specifies the Azure Stack deployment's external FQDN, also aliased as ExternalFQDN and ExternalDomainName.</span></span>
|  |  |
|----------------------------|--------------|
|<span data-ttu-id="acb78-159">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-159">Type:</span></span>                       |<span data-ttu-id="acb78-160">String</span><span class="sxs-lookup"><span data-stu-id="acb78-160">String</span></span>        |
|<span data-ttu-id="acb78-161">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-161">Position:</span></span>                   |<span data-ttu-id="acb78-162">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-162">Named</span></span>         |
|<span data-ttu-id="acb78-163">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-163">Default value:</span></span>              |<span data-ttu-id="acb78-164">ExternalFQDN, ExternalDomainName</span><span class="sxs-lookup"><span data-stu-id="acb78-164">ExternalFQDN, ExternalDomainName</span></span> |
|<span data-ttu-id="acb78-165">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-165">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-166">False</span><span class="sxs-lookup"><span data-stu-id="acb78-166">False</span></span>         |
|<span data-ttu-id="acb78-167">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-167">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-168">False</span><span class="sxs-lookup"><span data-stu-id="acb78-168">False</span></span>         |

 

> <span data-ttu-id="acb78-169">-IdentitySystem</span><span class="sxs-lookup"><span data-stu-id="acb78-169">-IdentitySystem</span></span>    

<span data-ttu-id="acb78-170">Specifies the Azure Stack deployment's Identity System valid values, AAD or ADFS, for Azure Active Directory and Active Directory Federated Services respectively.</span><span class="sxs-lookup"><span data-stu-id="acb78-170">Specifies the Azure Stack deployment's Identity System valid values, AAD or ADFS, for Azure Active Directory and Active Directory Federated Services respectively.</span></span>
|  |  |
|----------------------------|--------------|
|<span data-ttu-id="acb78-171">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-171">Type:</span></span>                       |<span data-ttu-id="acb78-172">String</span><span class="sxs-lookup"><span data-stu-id="acb78-172">String</span></span>        |
|<span data-ttu-id="acb78-173">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-173">Position:</span></span>                   |<span data-ttu-id="acb78-174">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-174">Named</span></span>         |
|<span data-ttu-id="acb78-175">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-175">Default value:</span></span>              |<span data-ttu-id="acb78-176">None</span><span class="sxs-lookup"><span data-stu-id="acb78-176">None</span></span>          |
|<span data-ttu-id="acb78-177">Valid values:</span><span class="sxs-lookup"><span data-stu-id="acb78-177">Valid values:</span></span>               |<span data-ttu-id="acb78-178">'AAD','ADFS'</span><span class="sxs-lookup"><span data-stu-id="acb78-178">'AAD','ADFS'</span></span>  |
|<span data-ttu-id="acb78-179">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-179">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-180">False</span><span class="sxs-lookup"><span data-stu-id="acb78-180">False</span></span>         |
|<span data-ttu-id="acb78-181">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-181">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-182">False</span><span class="sxs-lookup"><span data-stu-id="acb78-182">False</span></span>         |

> <span data-ttu-id="acb78-183">-PfxPassword</span><span class="sxs-lookup"><span data-stu-id="acb78-183">-PfxPassword</span></span>    

<span data-ttu-id="acb78-184">Specifies the password associated with PFX certificate files.</span><span class="sxs-lookup"><span data-stu-id="acb78-184">Specifies the password associated with PFX certificate files.</span></span>
|  |  |
|----------------------------|---------|
|<span data-ttu-id="acb78-185">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-185">Type:</span></span>                       |<span data-ttu-id="acb78-186">SecureString</span><span class="sxs-lookup"><span data-stu-id="acb78-186">SecureString</span></span> |
|<span data-ttu-id="acb78-187">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-187">Position:</span></span>                   |<span data-ttu-id="acb78-188">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-188">Named</span></span>    |
|<span data-ttu-id="acb78-189">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-189">Default value:</span></span>              |<span data-ttu-id="acb78-190">None</span><span class="sxs-lookup"><span data-stu-id="acb78-190">None</span></span>     |
|<span data-ttu-id="acb78-191">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-191">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-192">False</span><span class="sxs-lookup"><span data-stu-id="acb78-192">False</span></span>    |
|<span data-ttu-id="acb78-193">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-193">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-194">False</span><span class="sxs-lookup"><span data-stu-id="acb78-194">False</span></span>    |

> <span data-ttu-id="acb78-195">-PaaSCertificates</span><span class="sxs-lookup"><span data-stu-id="acb78-195">-PaaSCertificates</span></span>

<span data-ttu-id="acb78-196">Specifies the hashtable containing paths and passwords to PaaS Certificates.</span><span class="sxs-lookup"><span data-stu-id="acb78-196">Specifies the hashtable containing paths and passwords to PaaS Certificates.</span></span>
|  |  |
|----------------------------|---------|
|<span data-ttu-id="acb78-197">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-197">Type:</span></span>                       |<span data-ttu-id="acb78-198">Hashtable</span><span class="sxs-lookup"><span data-stu-id="acb78-198">Hashtable</span></span> |
|<span data-ttu-id="acb78-199">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-199">Position:</span></span>                   |<span data-ttu-id="acb78-200">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-200">Named</span></span>    |
|<span data-ttu-id="acb78-201">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-201">Default value:</span></span>              |<span data-ttu-id="acb78-202">None</span><span class="sxs-lookup"><span data-stu-id="acb78-202">None</span></span>     |
|<span data-ttu-id="acb78-203">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-203">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-204">False</span><span class="sxs-lookup"><span data-stu-id="acb78-204">False</span></span>    |
|<span data-ttu-id="acb78-205">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-205">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-206">False</span><span class="sxs-lookup"><span data-stu-id="acb78-206">False</span></span>    |

> <span data-ttu-id="acb78-207">-DeploymentDataJSONPath</span><span class="sxs-lookup"><span data-stu-id="acb78-207">-DeploymentDataJSONPath</span></span>

<span data-ttu-id="acb78-208">Specifies the Azure Stack deployment data JSON configuration file.</span><span class="sxs-lookup"><span data-stu-id="acb78-208">Specifies the Azure Stack deployment data JSON configuration file.</span></span> <span data-ttu-id="acb78-209">This file is generated for deployment.</span><span class="sxs-lookup"><span data-stu-id="acb78-209">This file is generated for deployment.</span></span>
|  |  |
|----------------------------|---------|
|<span data-ttu-id="acb78-210">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-210">Type:</span></span>                       |<span data-ttu-id="acb78-211">String</span><span class="sxs-lookup"><span data-stu-id="acb78-211">String</span></span>   |
|<span data-ttu-id="acb78-212">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-212">Position:</span></span>                   |<span data-ttu-id="acb78-213">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-213">Named</span></span>    |
|<span data-ttu-id="acb78-214">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-214">Default value:</span></span>              |<span data-ttu-id="acb78-215">None</span><span class="sxs-lookup"><span data-stu-id="acb78-215">None</span></span>     |
|<span data-ttu-id="acb78-216">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-216">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-217">False</span><span class="sxs-lookup"><span data-stu-id="acb78-217">False</span></span>    |
|<span data-ttu-id="acb78-218">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-218">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-219">False</span><span class="sxs-lookup"><span data-stu-id="acb78-219">False</span></span>    |

> <span data-ttu-id="acb78-220">-PfxPath</span><span class="sxs-lookup"><span data-stu-id="acb78-220">-PfxPath</span></span>

<span data-ttu-id="acb78-221">Specifies the path to a problematic certificate that requires import/export routine to fix, as indicated by certificate validation in this tool.</span><span class="sxs-lookup"><span data-stu-id="acb78-221">Specifies the path to a problematic certificate that requires import/export routine to fix, as indicated by certificate validation in this tool.</span></span>
|  |  |
|----------------------------|---------|
|<span data-ttu-id="acb78-222">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-222">Type:</span></span>                       |<span data-ttu-id="acb78-223">String</span><span class="sxs-lookup"><span data-stu-id="acb78-223">String</span></span>   |
|<span data-ttu-id="acb78-224">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-224">Position:</span></span>                   |<span data-ttu-id="acb78-225">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-225">Named</span></span>    |
|<span data-ttu-id="acb78-226">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-226">Default value:</span></span>              |<span data-ttu-id="acb78-227">None</span><span class="sxs-lookup"><span data-stu-id="acb78-227">None</span></span>     |
|<span data-ttu-id="acb78-228">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-228">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-229">False</span><span class="sxs-lookup"><span data-stu-id="acb78-229">False</span></span>    |
|<span data-ttu-id="acb78-230">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-230">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-231">False</span><span class="sxs-lookup"><span data-stu-id="acb78-231">False</span></span>    |

> <span data-ttu-id="acb78-232">-ExportPFXPath</span><span class="sxs-lookup"><span data-stu-id="acb78-232">-ExportPFXPath</span></span>  

<span data-ttu-id="acb78-233">Specifies the destination path for the resultant PFX file from import/export routine.</span><span class="sxs-lookup"><span data-stu-id="acb78-233">Specifies the destination path for the resultant PFX file from import/export routine.</span></span>  
|  |  |
|----------------------------|---------|
|<span data-ttu-id="acb78-234">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-234">Type:</span></span>                       |<span data-ttu-id="acb78-235">String</span><span class="sxs-lookup"><span data-stu-id="acb78-235">String</span></span>   |
|<span data-ttu-id="acb78-236">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-236">Position:</span></span>                   |<span data-ttu-id="acb78-237">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-237">Named</span></span>    |
|<span data-ttu-id="acb78-238">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-238">Default value:</span></span>              |<span data-ttu-id="acb78-239">None</span><span class="sxs-lookup"><span data-stu-id="acb78-239">None</span></span>     |
|<span data-ttu-id="acb78-240">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-240">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-241">False</span><span class="sxs-lookup"><span data-stu-id="acb78-241">False</span></span>    |
|<span data-ttu-id="acb78-242">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-242">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-243">False</span><span class="sxs-lookup"><span data-stu-id="acb78-243">False</span></span>    |

> <span data-ttu-id="acb78-244">-Subject</span><span class="sxs-lookup"><span data-stu-id="acb78-244">-Subject</span></span>

<span data-ttu-id="acb78-245">Specifies an ordered dictionary of the subject for the certificate request generation.</span><span class="sxs-lookup"><span data-stu-id="acb78-245">Specifies an ordered dictionary of the subject for the certificate request generation.</span></span>
|  |  |
|----------------------------|---------|
|<span data-ttu-id="acb78-246">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-246">Type:</span></span>                       |<span data-ttu-id="acb78-247">OrderedDictionary</span><span class="sxs-lookup"><span data-stu-id="acb78-247">OrderedDictionary</span></span>   |
|<span data-ttu-id="acb78-248">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-248">Position:</span></span>                   |<span data-ttu-id="acb78-249">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-249">Named</span></span>    |
|<span data-ttu-id="acb78-250">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-250">Default value:</span></span>              |<span data-ttu-id="acb78-251">None</span><span class="sxs-lookup"><span data-stu-id="acb78-251">None</span></span>     |
|<span data-ttu-id="acb78-252">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-252">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-253">False</span><span class="sxs-lookup"><span data-stu-id="acb78-253">False</span></span>    |
|<span data-ttu-id="acb78-254">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-254">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-255">False</span><span class="sxs-lookup"><span data-stu-id="acb78-255">False</span></span>    |

> <span data-ttu-id="acb78-256">-RequestType</span><span class="sxs-lookup"><span data-stu-id="acb78-256">-RequestType</span></span>

<span data-ttu-id="acb78-257">Specifies the SAN type of the certificate request.</span><span class="sxs-lookup"><span data-stu-id="acb78-257">Specifies the SAN type of the certificate request.</span></span> <span data-ttu-id="acb78-258">Valid values MultipleCSR, SingleCSR.</span><span class="sxs-lookup"><span data-stu-id="acb78-258">Valid values MultipleCSR, SingleCSR.</span></span>
- <span data-ttu-id="acb78-259">*MultipleCSR* generates multiple certificate requests, one for each service.</span><span class="sxs-lookup"><span data-stu-id="acb78-259">*MultipleCSR* generates multiple certificate requests, one for each service.</span></span>
- <span data-ttu-id="acb78-260">*SingleCSR* generates one certificate request for all services.</span><span class="sxs-lookup"><span data-stu-id="acb78-260">*SingleCSR* generates one certificate request for all services.</span></span>   

|  |  |
|----------------------------|---------|
|<span data-ttu-id="acb78-261">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-261">Type:</span></span>                       |<span data-ttu-id="acb78-262">String</span><span class="sxs-lookup"><span data-stu-id="acb78-262">String</span></span>   |
|<span data-ttu-id="acb78-263">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-263">Position:</span></span>                   |<span data-ttu-id="acb78-264">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-264">Named</span></span>    |
|<span data-ttu-id="acb78-265">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-265">Default value:</span></span>              |<span data-ttu-id="acb78-266">None</span><span class="sxs-lookup"><span data-stu-id="acb78-266">None</span></span>     |
|<span data-ttu-id="acb78-267">Valid values:</span><span class="sxs-lookup"><span data-stu-id="acb78-267">Valid values:</span></span>               |<span data-ttu-id="acb78-268">'MultipleCSR','SingleCSR'</span><span class="sxs-lookup"><span data-stu-id="acb78-268">'MultipleCSR','SingleCSR'</span></span> |
|<span data-ttu-id="acb78-269">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-269">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-270">False</span><span class="sxs-lookup"><span data-stu-id="acb78-270">False</span></span>    |
|<span data-ttu-id="acb78-271">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-271">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-272">False</span><span class="sxs-lookup"><span data-stu-id="acb78-272">False</span></span>    |

> <span data-ttu-id="acb78-273">-OutputRequestPath</span><span class="sxs-lookup"><span data-stu-id="acb78-273">-OutputRequestPath</span></span>

<span data-ttu-id="acb78-274">Specifies the destination path for certificate request files, directory must already exist.</span><span class="sxs-lookup"><span data-stu-id="acb78-274">Specifies the destination path for certificate request files, directory must already exist.</span></span>
|  |  |
|----------------------------|---------|
|<span data-ttu-id="acb78-275">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-275">Type:</span></span>                       |<span data-ttu-id="acb78-276">String</span><span class="sxs-lookup"><span data-stu-id="acb78-276">String</span></span>   |
|<span data-ttu-id="acb78-277">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-277">Position:</span></span>                   |<span data-ttu-id="acb78-278">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-278">Named</span></span>    |
|<span data-ttu-id="acb78-279">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-279">Default value:</span></span>              |<span data-ttu-id="acb78-280">None</span><span class="sxs-lookup"><span data-stu-id="acb78-280">None</span></span>     |
|<span data-ttu-id="acb78-281">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-281">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-282">False</span><span class="sxs-lookup"><span data-stu-id="acb78-282">False</span></span>    |
|<span data-ttu-id="acb78-283">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-283">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-284">False</span><span class="sxs-lookup"><span data-stu-id="acb78-284">False</span></span>    |

> <span data-ttu-id="acb78-285">-AADServiceAdministrator</span><span class="sxs-lookup"><span data-stu-id="acb78-285">-AADServiceAdministrator</span></span>

<span data-ttu-id="acb78-286">Specifies Azure Active Directory Service Administrator to be used for Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="acb78-286">Specifies Azure Active Directory Service Administrator to be used for Azure Stack deployment.</span></span>
|  |  |
|----------------------------|---------|
|<span data-ttu-id="acb78-287">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-287">Type:</span></span>                       |<span data-ttu-id="acb78-288">PSCredential</span><span class="sxs-lookup"><span data-stu-id="acb78-288">PSCredential</span></span>   |
|<span data-ttu-id="acb78-289">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-289">Position:</span></span>                   |<span data-ttu-id="acb78-290">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-290">Named</span></span>    |
|<span data-ttu-id="acb78-291">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-291">Default value:</span></span>              |<span data-ttu-id="acb78-292">None</span><span class="sxs-lookup"><span data-stu-id="acb78-292">None</span></span>     |
|<span data-ttu-id="acb78-293">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-293">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-294">False</span><span class="sxs-lookup"><span data-stu-id="acb78-294">False</span></span>    |
|<span data-ttu-id="acb78-295">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-295">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-296">False</span><span class="sxs-lookup"><span data-stu-id="acb78-296">False</span></span>    |

> <span data-ttu-id="acb78-297">-AADDirectoryTenantName</span><span class="sxs-lookup"><span data-stu-id="acb78-297">-AADDirectoryTenantName</span></span>

<span data-ttu-id="acb78-298">Specifies the Azure Active Directory name to be used for Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="acb78-298">Specifies the Azure Active Directory name to be used for Azure Stack deployment.</span></span>
|  |  |
|----------------------------|---------|
|<span data-ttu-id="acb78-299">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-299">Type:</span></span>                       |<span data-ttu-id="acb78-300">String</span><span class="sxs-lookup"><span data-stu-id="acb78-300">String</span></span>   |
|<span data-ttu-id="acb78-301">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-301">Position:</span></span>                   |<span data-ttu-id="acb78-302">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-302">Named</span></span>    |
|<span data-ttu-id="acb78-303">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-303">Default value:</span></span>              |<span data-ttu-id="acb78-304">None</span><span class="sxs-lookup"><span data-stu-id="acb78-304">None</span></span>     |
|<span data-ttu-id="acb78-305">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-305">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-306">False</span><span class="sxs-lookup"><span data-stu-id="acb78-306">False</span></span>    |
|<span data-ttu-id="acb78-307">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-307">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-308">False</span><span class="sxs-lookup"><span data-stu-id="acb78-308">False</span></span>    |

> <span data-ttu-id="acb78-309">-AzureEnvironment</span><span class="sxs-lookup"><span data-stu-id="acb78-309">-AzureEnvironment</span></span>

<span data-ttu-id="acb78-310">Specifies the instance of Azure Services containing the accounts, directories, and subscriptions to be used for Azure Stack deployment and registration.</span><span class="sxs-lookup"><span data-stu-id="acb78-310">Specifies the instance of Azure Services containing the accounts, directories, and subscriptions to be used for Azure Stack deployment and registration.</span></span>
|  |  |
|----------------------------|---------|
|<span data-ttu-id="acb78-311">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-311">Type:</span></span>                       |<span data-ttu-id="acb78-312">String</span><span class="sxs-lookup"><span data-stu-id="acb78-312">String</span></span>   |
|<span data-ttu-id="acb78-313">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-313">Position:</span></span>                   |<span data-ttu-id="acb78-314">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-314">Named</span></span>    |
|<span data-ttu-id="acb78-315">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-315">Default value:</span></span>              |<span data-ttu-id="acb78-316">None</span><span class="sxs-lookup"><span data-stu-id="acb78-316">None</span></span>     |
|<span data-ttu-id="acb78-317">Valid values:</span><span class="sxs-lookup"><span data-stu-id="acb78-317">Valid values:</span></span>               |<span data-ttu-id="acb78-318">'AzureCloud','AzureChinaCloud','AzureGermanCloud'</span><span class="sxs-lookup"><span data-stu-id="acb78-318">'AzureCloud','AzureChinaCloud','AzureGermanCloud'</span></span> |
|<span data-ttu-id="acb78-319">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-319">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-320">False</span><span class="sxs-lookup"><span data-stu-id="acb78-320">False</span></span>    |
|<span data-ttu-id="acb78-321">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-321">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-322">False</span><span class="sxs-lookup"><span data-stu-id="acb78-322">False</span></span>    |

> <span data-ttu-id="acb78-323">-RegistrationAccount</span><span class="sxs-lookup"><span data-stu-id="acb78-323">-RegistrationAccount</span></span>

<span data-ttu-id="acb78-324">Specifies the Registration Account to be used for Azure Stack registration.</span><span class="sxs-lookup"><span data-stu-id="acb78-324">Specifies the Registration Account to be used for Azure Stack registration.</span></span>
|  |  |
|----------------------------|---------|
|<span data-ttu-id="acb78-325">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-325">Type:</span></span>                       |<span data-ttu-id="acb78-326">String</span><span class="sxs-lookup"><span data-stu-id="acb78-326">String</span></span>   |
|<span data-ttu-id="acb78-327">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-327">Position:</span></span>                   |<span data-ttu-id="acb78-328">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-328">Named</span></span>    |
|<span data-ttu-id="acb78-329">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-329">Default value:</span></span>              |<span data-ttu-id="acb78-330">None</span><span class="sxs-lookup"><span data-stu-id="acb78-330">None</span></span>     |
|<span data-ttu-id="acb78-331">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-331">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-332">False</span><span class="sxs-lookup"><span data-stu-id="acb78-332">False</span></span>    |
|<span data-ttu-id="acb78-333">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-333">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-334">False</span><span class="sxs-lookup"><span data-stu-id="acb78-334">False</span></span>    |

> <span data-ttu-id="acb78-335">-RegistrationSubscriptionID</span><span class="sxs-lookup"><span data-stu-id="acb78-335">-RegistrationSubscriptionID</span></span>

<span data-ttu-id="acb78-336">Specifies the Registration Subscription ID to be used for Azure Stack registration.</span><span class="sxs-lookup"><span data-stu-id="acb78-336">Specifies the Registration Subscription ID to be used for Azure Stack registration.</span></span>
|  |  |
|----------------------------|---------|
|<span data-ttu-id="acb78-337">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-337">Type:</span></span>                       |<span data-ttu-id="acb78-338">Guid</span><span class="sxs-lookup"><span data-stu-id="acb78-338">Guid</span></span>     |
|<span data-ttu-id="acb78-339">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-339">Position:</span></span>                   |<span data-ttu-id="acb78-340">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-340">Named</span></span>    |
|<span data-ttu-id="acb78-341">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-341">Default value:</span></span>              |<span data-ttu-id="acb78-342">None</span><span class="sxs-lookup"><span data-stu-id="acb78-342">None</span></span>     |
|<span data-ttu-id="acb78-343">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-343">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-344">False</span><span class="sxs-lookup"><span data-stu-id="acb78-344">False</span></span>    |
|<span data-ttu-id="acb78-345">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-345">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-346">False</span><span class="sxs-lookup"><span data-stu-id="acb78-346">False</span></span>    |

> <span data-ttu-id="acb78-347">-ReportPath</span><span class="sxs-lookup"><span data-stu-id="acb78-347">-ReportPath</span></span>

<span data-ttu-id="acb78-348">Specifies path for Readiness Report, defaults to current directory and default report name.</span><span class="sxs-lookup"><span data-stu-id="acb78-348">Specifies path for Readiness Report, defaults to current directory and default report name.</span></span>
|  |  |
|----------------------------|---------|
|<span data-ttu-id="acb78-349">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-349">Type:</span></span>                       |<span data-ttu-id="acb78-350">String</span><span class="sxs-lookup"><span data-stu-id="acb78-350">String</span></span>   |
|<span data-ttu-id="acb78-351">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-351">Position:</span></span>                   |<span data-ttu-id="acb78-352">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-352">Named</span></span>    |
|<span data-ttu-id="acb78-353">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-353">Default value:</span></span>              |<span data-ttu-id="acb78-354">All</span><span class="sxs-lookup"><span data-stu-id="acb78-354">All</span></span>      |
|<span data-ttu-id="acb78-355">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-355">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-356">False</span><span class="sxs-lookup"><span data-stu-id="acb78-356">False</span></span>    |
|<span data-ttu-id="acb78-357">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-357">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-358">False</span><span class="sxs-lookup"><span data-stu-id="acb78-358">False</span></span>    |



## <a name="optional-parameters"></a><span data-ttu-id="acb78-359">Optional parameters</span><span class="sxs-lookup"><span data-stu-id="acb78-359">Optional parameters</span></span>
> <span data-ttu-id="acb78-360">-CertificatePath</span><span class="sxs-lookup"><span data-stu-id="acb78-360">-CertificatePath</span></span>     

<span data-ttu-id="acb78-361">Specifies the path under which only the certificate required certificate folders are present.</span><span class="sxs-lookup"><span data-stu-id="acb78-361">Specifies the path under which only the certificate required certificate folders are present.</span></span>

<span data-ttu-id="acb78-362">Required folders for Azure Stack deployment with Azure Active Directory identity system are:</span><span class="sxs-lookup"><span data-stu-id="acb78-362">Required folders for Azure Stack deployment with Azure Active Directory identity system are:</span></span>

<span data-ttu-id="acb78-363">ACSBlob, ACSQueue, ACSTable, Admin Portal, ARM Admin, ARM Public, KeyVault, KeyVaultInternal, Public Portal</span><span class="sxs-lookup"><span data-stu-id="acb78-363">ACSBlob, ACSQueue, ACSTable, Admin Portal, ARM Admin, ARM Public, KeyVault, KeyVaultInternal, Public Portal</span></span>

<span data-ttu-id="acb78-364">Required folder for Azure Stack deployment with Active Directory Federation Services identity system are:</span><span class="sxs-lookup"><span data-stu-id="acb78-364">Required folder for Azure Stack deployment with Active Directory Federation Services identity system are:</span></span>

<span data-ttu-id="acb78-365">ACSBlob, ACSQueue, ACSTable, ADFS, Admin Portal, ARM Admin, ARM Public, Graph, KeyVault, KeyVaultInternal, Public Portal</span><span class="sxs-lookup"><span data-stu-id="acb78-365">ACSBlob, ACSQueue, ACSTable, ADFS, Admin Portal, ARM Admin, ARM Public, Graph, KeyVault, KeyVaultInternal, Public Portal</span></span>


|  |  |
|----------------------------|---------|
|<span data-ttu-id="acb78-366">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-366">Type:</span></span>                       |<span data-ttu-id="acb78-367">String</span><span class="sxs-lookup"><span data-stu-id="acb78-367">String</span></span>   |
|<span data-ttu-id="acb78-368">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-368">Position:</span></span>                   |<span data-ttu-id="acb78-369">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-369">Named</span></span>    |
|<span data-ttu-id="acb78-370">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-370">Default value:</span></span>              |<span data-ttu-id="acb78-371">.\Certificates</span><span class="sxs-lookup"><span data-stu-id="acb78-371">.\Certificates</span></span> |
|<span data-ttu-id="acb78-372">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-372">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-373">False</span><span class="sxs-lookup"><span data-stu-id="acb78-373">False</span></span>    |
|<span data-ttu-id="acb78-374">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-374">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-375">False</span><span class="sxs-lookup"><span data-stu-id="acb78-375">False</span></span>    |


> <span data-ttu-id="acb78-376">-IncludePaaS</span><span class="sxs-lookup"><span data-stu-id="acb78-376">-IncludePaaS</span></span>  

<span data-ttu-id="acb78-377">Specifies if PaaS services/hostnames should be added to the certificate request(s).</span><span class="sxs-lookup"><span data-stu-id="acb78-377">Specifies if PaaS services/hostnames should be added to the certificate request(s).</span></span>


|  |  |
|----------------------------|------------------|
|<span data-ttu-id="acb78-378">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-378">Type:</span></span>                       |<span data-ttu-id="acb78-379">SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="acb78-379">SwitchParameter</span></span>   |
|<span data-ttu-id="acb78-380">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-380">Position:</span></span>                   |<span data-ttu-id="acb78-381">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-381">Named</span></span>             |
|<span data-ttu-id="acb78-382">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-382">Default value:</span></span>              |<span data-ttu-id="acb78-383">False</span><span class="sxs-lookup"><span data-stu-id="acb78-383">False</span></span>             |
|<span data-ttu-id="acb78-384">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-384">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-385">False</span><span class="sxs-lookup"><span data-stu-id="acb78-385">False</span></span>             |
|<span data-ttu-id="acb78-386">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-386">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-387">False</span><span class="sxs-lookup"><span data-stu-id="acb78-387">False</span></span>             |


> <span data-ttu-id="acb78-388">-ReportSections</span><span class="sxs-lookup"><span data-stu-id="acb78-388">-ReportSections</span></span>        

<span data-ttu-id="acb78-389">Specifies whether to only show report summary, omits detail.</span><span class="sxs-lookup"><span data-stu-id="acb78-389">Specifies whether to only show report summary, omits detail.</span></span>
|  |  |
|----------------------------|---------|
|<span data-ttu-id="acb78-390">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-390">Type:</span></span>                       |<span data-ttu-id="acb78-391">String</span><span class="sxs-lookup"><span data-stu-id="acb78-391">String</span></span>   |
|<span data-ttu-id="acb78-392">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-392">Position:</span></span>                   |<span data-ttu-id="acb78-393">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-393">Named</span></span>    |
|<span data-ttu-id="acb78-394">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-394">Default value:</span></span>              |<span data-ttu-id="acb78-395">All</span><span class="sxs-lookup"><span data-stu-id="acb78-395">All</span></span>      |
|<span data-ttu-id="acb78-396">Valid values:</span><span class="sxs-lookup"><span data-stu-id="acb78-396">Valid values:</span></span>               |<span data-ttu-id="acb78-397">'Certificate','AzureRegistration','AzureIdentity','Jobs','All'</span><span class="sxs-lookup"><span data-stu-id="acb78-397">'Certificate','AzureRegistration','AzureIdentity','Jobs','All'</span></span> |
|<span data-ttu-id="acb78-398">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-398">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-399">False</span><span class="sxs-lookup"><span data-stu-id="acb78-399">False</span></span>    |
|<span data-ttu-id="acb78-400">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-400">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-401">False</span><span class="sxs-lookup"><span data-stu-id="acb78-401">False</span></span>    |


> <span data-ttu-id="acb78-402">-Summary</span><span class="sxs-lookup"><span data-stu-id="acb78-402">-Summary</span></span> 

<span data-ttu-id="acb78-403">Specifies whether to only show report summary, omits detail.</span><span class="sxs-lookup"><span data-stu-id="acb78-403">Specifies whether to only show report summary, omits detail.</span></span>
|  |  |
|----------------------------|------------------|
|<span data-ttu-id="acb78-404">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-404">Type:</span></span>                       |<span data-ttu-id="acb78-405">SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="acb78-405">SwitchParameter</span></span>   |
|<span data-ttu-id="acb78-406">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-406">Position:</span></span>                   |<span data-ttu-id="acb78-407">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-407">Named</span></span>             |
|<span data-ttu-id="acb78-408">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-408">Default value:</span></span>              |<span data-ttu-id="acb78-409">False</span><span class="sxs-lookup"><span data-stu-id="acb78-409">False</span></span>             |
|<span data-ttu-id="acb78-410">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-410">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-411">False</span><span class="sxs-lookup"><span data-stu-id="acb78-411">False</span></span>             |
|<span data-ttu-id="acb78-412">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-412">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-413">False</span><span class="sxs-lookup"><span data-stu-id="acb78-413">False</span></span>             |


> <span data-ttu-id="acb78-414">-CleanReport</span><span class="sxs-lookup"><span data-stu-id="acb78-414">-CleanReport</span></span>  

<span data-ttu-id="acb78-415">Removes previous execution and validation history and writes validations to a new report.</span><span class="sxs-lookup"><span data-stu-id="acb78-415">Removes previous execution and validation history and writes validations to a new report.</span></span>
|  |  |
|----------------------------|------------------|
|<span data-ttu-id="acb78-416">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-416">Type:</span></span>                       |<span data-ttu-id="acb78-417">SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="acb78-417">SwitchParameter</span></span>   |
|<span data-ttu-id="acb78-418">Aliases:</span><span class="sxs-lookup"><span data-stu-id="acb78-418">Aliases:</span></span>                    |<span data-ttu-id="acb78-419">cf</span><span class="sxs-lookup"><span data-stu-id="acb78-419">cf</span></span>                |
|<span data-ttu-id="acb78-420">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-420">Position:</span></span>                   |<span data-ttu-id="acb78-421">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-421">Named</span></span>             |
|<span data-ttu-id="acb78-422">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-422">Default value:</span></span>              |<span data-ttu-id="acb78-423">False</span><span class="sxs-lookup"><span data-stu-id="acb78-423">False</span></span>             |
|<span data-ttu-id="acb78-424">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-424">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-425">False</span><span class="sxs-lookup"><span data-stu-id="acb78-425">False</span></span>             |
|<span data-ttu-id="acb78-426">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-426">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-427">False</span><span class="sxs-lookup"><span data-stu-id="acb78-427">False</span></span>             |


> <span data-ttu-id="acb78-428">-OutputPath</span><span class="sxs-lookup"><span data-stu-id="acb78-428">-OutputPath</span></span>    

<span data-ttu-id="acb78-429">Specifies custom path to save Readiness JSON report and verbose log file.</span><span class="sxs-lookup"><span data-stu-id="acb78-429">Specifies custom path to save Readiness JSON report and verbose log file.</span></span>  <span data-ttu-id="acb78-430">If the path does not already exist, the tool will attempt to create the directory.</span><span class="sxs-lookup"><span data-stu-id="acb78-430">If the path does not already exist, the tool will attempt to create the directory.</span></span>
|  |  |
|----------------------------|------------------|
|<span data-ttu-id="acb78-431">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-431">Type:</span></span>                       |<span data-ttu-id="acb78-432">String</span><span class="sxs-lookup"><span data-stu-id="acb78-432">String</span></span>            |
|<span data-ttu-id="acb78-433">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-433">Position:</span></span>                   |<span data-ttu-id="acb78-434">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-434">Named</span></span>             |
|<span data-ttu-id="acb78-435">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-435">Default value:</span></span>              |<span data-ttu-id="acb78-436">$ENV:TEMP\AzsReadinessChecker</span><span class="sxs-lookup"><span data-stu-id="acb78-436">$ENV:TEMP\AzsReadinessChecker</span></span>  |
|<span data-ttu-id="acb78-437">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-437">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-438">False</span><span class="sxs-lookup"><span data-stu-id="acb78-438">False</span></span>             |
|<span data-ttu-id="acb78-439">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-439">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-440">False</span><span class="sxs-lookup"><span data-stu-id="acb78-440">False</span></span>             |


> <span data-ttu-id="acb78-441">-Confirm</span><span class="sxs-lookup"><span data-stu-id="acb78-441">-Confirm</span></span>  

<span data-ttu-id="acb78-442">Prompts for confirmation before running the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="acb78-442">Prompts for confirmation before running the cmdlet.</span></span>
|  |  |
|----------------------------|------------------|
|<span data-ttu-id="acb78-443">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-443">Type:</span></span>                       |<span data-ttu-id="acb78-444">SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="acb78-444">SwitchParameter</span></span>   |
|<span data-ttu-id="acb78-445">Aliases:</span><span class="sxs-lookup"><span data-stu-id="acb78-445">Aliases:</span></span>                    |<span data-ttu-id="acb78-446">cf</span><span class="sxs-lookup"><span data-stu-id="acb78-446">cf</span></span>                |
|<span data-ttu-id="acb78-447">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-447">Position:</span></span>                   |<span data-ttu-id="acb78-448">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-448">Named</span></span>             |
|<span data-ttu-id="acb78-449">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-449">Default value:</span></span>              |<span data-ttu-id="acb78-450">False</span><span class="sxs-lookup"><span data-stu-id="acb78-450">False</span></span>             |
|<span data-ttu-id="acb78-451">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-451">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-452">False</span><span class="sxs-lookup"><span data-stu-id="acb78-452">False</span></span>             |
|<span data-ttu-id="acb78-453">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-453">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-454">False</span><span class="sxs-lookup"><span data-stu-id="acb78-454">False</span></span>             |


> <span data-ttu-id="acb78-455">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="acb78-455">-WhatIf</span></span>  

<span data-ttu-id="acb78-456">Shows what would happen if the cmdlet runs.</span><span class="sxs-lookup"><span data-stu-id="acb78-456">Shows what would happen if the cmdlet runs.</span></span> <span data-ttu-id="acb78-457">The cmdlet is not run.</span><span class="sxs-lookup"><span data-stu-id="acb78-457">The cmdlet is not run.</span></span>
|  |  |
|----------------------------|------------------|
|<span data-ttu-id="acb78-458">Type:</span><span class="sxs-lookup"><span data-stu-id="acb78-458">Type:</span></span>                       |<span data-ttu-id="acb78-459">SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="acb78-459">SwitchParameter</span></span>   |
|<span data-ttu-id="acb78-460">Aliases:</span><span class="sxs-lookup"><span data-stu-id="acb78-460">Aliases:</span></span>                    |<span data-ttu-id="acb78-461">wi</span><span class="sxs-lookup"><span data-stu-id="acb78-461">wi</span></span>                |
|<span data-ttu-id="acb78-462">Position:</span><span class="sxs-lookup"><span data-stu-id="acb78-462">Position:</span></span>                   |<span data-ttu-id="acb78-463">Named</span><span class="sxs-lookup"><span data-stu-id="acb78-463">Named</span></span>             |
|<span data-ttu-id="acb78-464">Default value:</span><span class="sxs-lookup"><span data-stu-id="acb78-464">Default value:</span></span>              |<span data-ttu-id="acb78-465">False</span><span class="sxs-lookup"><span data-stu-id="acb78-465">False</span></span>             |
|<span data-ttu-id="acb78-466">Accept pipeline input:</span><span class="sxs-lookup"><span data-stu-id="acb78-466">Accept pipeline input:</span></span>      |<span data-ttu-id="acb78-467">False</span><span class="sxs-lookup"><span data-stu-id="acb78-467">False</span></span>             |
|<span data-ttu-id="acb78-468">Accept wildcard characters:</span><span class="sxs-lookup"><span data-stu-id="acb78-468">Accept wildcard characters:</span></span> |<span data-ttu-id="acb78-469">False</span><span class="sxs-lookup"><span data-stu-id="acb78-469">False</span></span>             |

 
