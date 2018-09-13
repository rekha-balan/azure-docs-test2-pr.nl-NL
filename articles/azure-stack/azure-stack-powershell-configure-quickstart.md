---
title: Install and configure PowerShell for Azure Stack quickstart  | Microsoft Docs
description: Learn about installing and configuring PowerShell for Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/10/2018
ms.author: mabrigg
ms.openlocfilehash: 5d988e8a8a32924b8424a07cf20c75f0e8f8cf4d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855993"
---
# <a name="get-up-and-running-with-powershell-in-azure-stack"></a><span data-ttu-id="816b3-103">Get up and running with PowerShell in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="816b3-103">Get up and running with PowerShell in Azure Stack</span></span>

<span data-ttu-id="816b3-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="816b3-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="816b3-105">This quickstart helps you to install and configure an Azure Stack environment with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="816b3-105">This quickstart helps you to install and configure an Azure Stack environment with PowerShell.</span></span> <span data-ttu-id="816b3-106">The script that we provide in this article is scoped to the **Azure Stack operator** only.</span><span class="sxs-lookup"><span data-stu-id="816b3-106">The script that we provide in this article is scoped to the **Azure Stack operator** only.</span></span>

<span data-ttu-id="816b3-107">This article is a condensed version of the steps that are described in the [Install PowerShell]( azure-stack-powershell-install.md), [Download tools]( azure-stack-powershell-download.md), and [Configure the Azure Stack operator's PowerShell environment]( azure-stack-powershell-configure-admin.md) articles.</span><span class="sxs-lookup"><span data-stu-id="816b3-107">This article is a condensed version of the steps that are described in the [Install PowerShell]( azure-stack-powershell-install.md), [Download tools]( azure-stack-powershell-download.md), and [Configure the Azure Stack operator's PowerShell environment]( azure-stack-powershell-configure-admin.md) articles.</span></span> <span data-ttu-id="816b3-108">By using the scripts in this article, you can set up PowerShell for Azure Stack environments that are deployed with Azure Active Directory or Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="816b3-108">By using the scripts in this article, you can set up PowerShell for Azure Stack environments that are deployed with Azure Active Directory or Active Directory Federation Services (AD FS).</span></span>  


## <a name="set-up-powershell-for-azure-active-directory-based-deployments"></a><span data-ttu-id="816b3-109">Set up PowerShell for Azure Active Directory-based deployments</span><span class="sxs-lookup"><span data-stu-id="816b3-109">Set up PowerShell for Azure Active Directory-based deployments</span></span>

<a name="sign-in-to-your-azure-stack-development-kit-or-a-windows-based-external-client-if-you-are-connected-through-vpn-open-an-elevated-powershell-ise-session-and-then-run-the-following-script"></a><span data-ttu-id="816b3-110">Sign in to your Azure Stack Development Kit, or a Windows-based external client if you are connected through VPN.</span><span class="sxs-lookup"><span data-stu-id="816b3-110">Sign in to your Azure Stack Development Kit, or a Windows-based external client if you are connected through VPN.</span></span> <span data-ttu-id="816b3-111">Open an elevated PowerShell ISE session, and then run the following script.</span><span class="sxs-lookup"><span data-stu-id="816b3-111">Open an elevated PowerShell ISE session, and then run the following script.</span></span> 
-  
- <span data-ttu-id="816b3-112">Make sure to update the **TenantName**, **ArmEndpoint**, and **GraphAudience** variables as necessary for your environment configuration:</span><span class="sxs-lookup"><span data-stu-id="816b3-112">Make sure to update the **TenantName**, **ArmEndpoint**, and **GraphAudience** variables as necessary for your environment configuration:</span></span>

```powershell
# Specify Azure Active Directory tenant name.
$TenantName = "<mydirectory>.onmicrosoft.com"

# Set the module repository and the execution policy.
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted

Set-ExecutionPolicy RemoteSigned `
  -force

# Uninstall any existing Azure PowerShell modules. To uninstall, close all the active PowerShell sessions, and then run the following command:
Get-Module -ListAvailable -Name Azure* | `
  Uninstall-Module

# Install PowerShell for Azure Stack.
Install-Module `
  -Name AzureRm.BootStrapper `
  -Force

Use-AzureRmProfile `
  -Profile 2017-03-09-profile `
  -Force

Install-Module `
  -Name AzureStack `
  -RequiredVersion 1.2.11 `
  -Force 

# Download Azure Stack tools from GitHub and import the connect module.
cd \
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12 
invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

expand-archive master.zip `
  -DestinationPath . `
  -Force

cd AzureStack-Tools-master

Import-Module .\Connect\AzureStack.Connect.psm1

# For Azure Stack development kit, this value is set to https://adminmanagement.local.azurestack.external. To get this value for Azure Stack integrated systems, contact your service provider.
  $ArmEndpoint = "<Resource Manager endpoint for your environment>"

# Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackAdmin" `
    -ArmEndpoint $ArmEndpoint

# Get the Active Directory tenantId that is used to deploy Azure Stack
  $TenantID = Get-AzsDirectoryTenantId `
    -AADTenantName $TenantName `
    -EnvironmentName "AzureStackAdmin"

# Sign in to your environment
  Add-AzureRmAccount `
    -EnvironmentName "AzureStackAdmin" `
    -TenantId $TenantID 
```

## <a name="set-up-powershell-for-ad-fs-based-deployments"></a><span data-ttu-id="816b3-113">Set up PowerShell for AD FS-based deployments</span><span class="sxs-lookup"><span data-stu-id="816b3-113">Set up PowerShell for AD FS-based deployments</span></span>

<span data-ttu-id="816b3-114">You can use the following script if you are operating Azure Stack when connected to internet.</span><span class="sxs-lookup"><span data-stu-id="816b3-114">You can use the following script if you are operating Azure Stack when connected to internet.</span></span> <span data-ttu-id="816b3-115">However if you are operating Azure Stack without internet connectivity, use the [disconnected way of installing PowerShell](azure-stack-powershell-install.md) and the cmdlets to configure PowerShell will remain same as shown in this script.</span><span class="sxs-lookup"><span data-stu-id="816b3-115">However if you are operating Azure Stack without internet connectivity, use the [disconnected way of installing PowerShell](azure-stack-powershell-install.md) and the cmdlets to configure PowerShell will remain same as shown in this script.</span></span> <span data-ttu-id="816b3-116">Sign in to your Azure Stack Development Kit, or a Windows-based external client if you are connected through VPN.</span><span class="sxs-lookup"><span data-stu-id="816b3-116">Sign in to your Azure Stack Development Kit, or a Windows-based external client if you are connected through VPN.</span></span> <span data-ttu-id="816b3-117">Open an elevated PowerShell ISE session, and then run the following script.</span><span class="sxs-lookup"><span data-stu-id="816b3-117">Open an elevated PowerShell ISE session, and then run the following script.</span></span> <span data-ttu-id="816b3-118">Make sure to update the **ArmEndpoint** and **GraphAudience** variables as necessary for your environment configuration:</span><span class="sxs-lookup"><span data-stu-id="816b3-118">Make sure to update the **ArmEndpoint** and **GraphAudience** variables as necessary for your environment configuration:</span></span>

```powershell

# Set the module repository and the execution policy.
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted

Set-ExecutionPolicy RemoteSigned `
  -force

# Uninstall any existing Azure PowerShell modules. To uninstall, close all the active PowerShell sessions and run the following command:
Get-Module -ListAvailable -Name Azure* | `
  Uninstall-Module

# Install PowerShell for Azure Stack.
Install-Module `
  -Name AzureRm.BootStrapper `
  -Force

Use-AzureRmProfile `
  -Profile 2017-03-09-profile `
  -Force

Install-Module `
  -Name AzureStack `
  -RequiredVersion 1.2.11 `
  -Force 

# Download Azure Stack tools from GitHub and import the connect module.
cd \
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

expand-archive master.zip `
  -DestinationPath . `
  -Force

cd AzureStack-Tools-master

Import-Module .\Connect\AzureStack.Connect.psm1

# For Azure Stack development kit, this value is set to https://adminmanagement.local.azurestack.external. To get this value for Azure Stack integrated systems, contact your service provider.
$ArmEndpoint = "<Resource Manager endpoint for your environment>"

# Register an AzureRM environment that targets your Azure Stack instance
Add-AzureRMEnvironment `
    -Name "AzureStackAdmin" `
    -ArmEndpoint $ArmEndpoint

# Get the Active Directory tenantId that is used to deploy Azure Stack     
$TenantID = Get-AzsDirectoryTenantId `
    -ADFS `
    -EnvironmentName "AzureStackAdmin"

# Sign in to your environment
Add-AzureRmAccount `
    -EnvironmentName "AzureStackAdmin" `
    -TenantId $TenantID
```

## <a name="test-the-connectivity"></a><span data-ttu-id="816b3-119">Test the connectivity</span><span class="sxs-lookup"><span data-stu-id="816b3-119">Test the connectivity</span></span>

<span data-ttu-id="816b3-120">Now that you’ve configured PowerShell, you can test the configuration by creating a resource group:</span><span class="sxs-lookup"><span data-stu-id="816b3-120">Now that you’ve configured PowerShell, you can test the configuration by creating a resource group:</span></span>

```powershell
New-AzureRMResourceGroup -Name "ContosoVMRG" -Location Local
```

> [!note]  
> <span data-ttu-id="816b3-121">To specify a resource group, you will need to have a resource group in your subscription.</span><span class="sxs-lookup"><span data-stu-id="816b3-121">To specify a resource group, you will need to have a resource group in your subscription.</span></span> <span data-ttu-id="816b3-122">For more information about subscriptions, see [Plan, offer, quota, and subscription overview](azure-stack-plan-offer-quota-overview.md)</span><span class="sxs-lookup"><span data-stu-id="816b3-122">For more information about subscriptions, see [Plan, offer, quota, and subscription overview](azure-stack-plan-offer-quota-overview.md)</span></span>

<span data-ttu-id="816b3-123">After the resource group is created, the **Provisioning state** property is set to **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="816b3-123">After the resource group is created, the **Provisioning state** property is set to **Succeeded**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="816b3-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="816b3-124">Next steps</span></span>

* [<span data-ttu-id="816b3-125">Install and configure CLI</span><span class="sxs-lookup"><span data-stu-id="816b3-125">Install and configure CLI</span></span>](azure-stack-connect-cli.md)

* [<span data-ttu-id="816b3-126">Develop templates</span><span class="sxs-lookup"><span data-stu-id="816b3-126">Develop templates</span></span>](user/azure-stack-develop-templates.md)
