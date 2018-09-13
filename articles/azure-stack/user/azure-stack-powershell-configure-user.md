---
title: Connect to Azure Stack with PowerShell as a user | Microsoft Docs
description: Steps to connect to the user's Azure Stack instance.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: F4ED2238-AAF2-4930-AA7F-7C140311E10F
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2018
ms.author: sethm
ms.reviewer: Balsu.G
ms.openlocfilehash: acdad9788737f4f552cedc1b5f42e03e2288dba8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969474"
---
# <a name="connect-to-azure-stack-with-powershell-as-a-user"></a><span data-ttu-id="007f0-103">Connect to Azure Stack with PowerShell as a user</span><span class="sxs-lookup"><span data-stu-id="007f0-103">Connect to Azure Stack with PowerShell as a user</span></span>

<span data-ttu-id="007f0-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="007f0-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="007f0-105">This article provides you with the steps to connect to your Azure Stack instance.</span><span class="sxs-lookup"><span data-stu-id="007f0-105">This article provides you with the steps to connect to your Azure Stack instance.</span></span> <span data-ttu-id="007f0-106">You must connect to manage Azure Stack resources with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="007f0-106">You must connect to manage Azure Stack resources with PowerShell.</span></span> <span data-ttu-id="007f0-107">For example, you can use PowerShell to subscribe to offers, create virtual machines, and deploy Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="007f0-107">For example, you can use PowerShell to subscribe to offers, create virtual machines, and deploy Azure Resource Manager templates.</span></span> <span data-ttu-id="007f0-108">in order to execute PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="007f0-108">in order to execute PowerShell cmdlets.</span></span>

<span data-ttu-id="007f0-109">To get set up:</span><span class="sxs-lookup"><span data-stu-id="007f0-109">To get set up:</span></span>
  - <span data-ttu-id="007f0-110">Make sure you have the requirements.</span><span class="sxs-lookup"><span data-stu-id="007f0-110">Make sure you have the requirements.</span></span>
  - <span data-ttu-id="007f0-111">Connect with Azure Active Directory (Azure AD) or Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="007f0-111">Connect with Azure Active Directory (Azure AD) or Active Directory Federation Services (AD FS).</span></span> 
  - <span data-ttu-id="007f0-112">Register resource providers.</span><span class="sxs-lookup"><span data-stu-id="007f0-112">Register resource providers.</span></span>
  - <span data-ttu-id="007f0-113">Test your connectivity.</span><span class="sxs-lookup"><span data-stu-id="007f0-113">Test your connectivity.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="007f0-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="007f0-114">Prerequisites</span></span>

<span data-ttu-id="007f0-115">You can configure these prerequisites from the [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span><span class="sxs-lookup"><span data-stu-id="007f0-115">You can configure these prerequisites from the [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="007f0-116">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="007f0-116">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>
* <span data-ttu-id="007f0-117">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="007f0-117">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span>

<span data-ttu-id="007f0-118">Make sure you replace the following script variables with values from your Azure Stack configuration:</span><span class="sxs-lookup"><span data-stu-id="007f0-118">Make sure you replace the following script variables with values from your Azure Stack configuration:</span></span>

- <span data-ttu-id="007f0-119">**Azure AD tenant name**</span><span class="sxs-lookup"><span data-stu-id="007f0-119">**Azure AD tenant name**</span></span>  
  <span data-ttu-id="007f0-120">The name of your Azure AD tenant used to manage Azure Stack, for example, yourdirectory.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="007f0-120">The name of your Azure AD tenant used to manage Azure Stack, for example, yourdirectory.onmicrosoft.com.</span></span>
- <span data-ttu-id="007f0-121">**Azure Resource Manager endpoint**</span><span class="sxs-lookup"><span data-stu-id="007f0-121">**Azure Resource Manager endpoint**</span></span>  
  <span data-ttu-id="007f0-122">For Azure Stack development kit, this value is set to https://management.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="007f0-122">For Azure Stack development kit, this value is set to https://management.local.azurestack.external.</span></span> <span data-ttu-id="007f0-123">To get this value for Azure Stack integrated systems, contact your service provider.</span><span class="sxs-lookup"><span data-stu-id="007f0-123">To get this value for Azure Stack integrated systems, contact your service provider.</span></span>

## <a name="connect-with-azure-ad"></a><span data-ttu-id="007f0-124">Connect with Azure AD</span><span class="sxs-lookup"><span data-stu-id="007f0-124">Connect with Azure AD</span></span>

  ```PowerShell
  $AADTenantName = "yourdirectory.onmicrosoft.com"
  $ArmEndpoint = "https://management.local.azurestack.external"

  # Register an Azure Resource Manager environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackUser" `
    -ArmEndpoint $ArmEndpoint

  $AuthEndpoint = (Get-AzureRmEnvironment -Name "AzureStackUser").ActiveDirectoryAuthority.TrimEnd('/')
  $TenantId = (invoke-restmethod "$($AuthEndpoint)/$($AADTenantName)/.well-known/openid-configuration").issuer.TrimEnd('/').Split('/')[-1]

  # Sign in to your environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackUser" `
    -TenantId $TenantId
   ```

## <a name="connect-with-ad-fs"></a><span data-ttu-id="007f0-125">Connect with AD FS</span><span class="sxs-lookup"><span data-stu-id="007f0-125">Connect with AD FS</span></span>

  ```PowerShell  
  $ArmEndpoint = "https://management.local.azurestack.external"

  # Register an Azure Resource Manager environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackUser" `
    -ArmEndpoint $ArmEndpoint

  $AuthEndpoint = (Get-AzureRmEnvironment -Name "AzureStackUser").ActiveDirectoryAuthority.TrimEnd('/')
  $tenantId = (invoke-restmethod "$($AuthEndpoint)/.well-known/openid-configuration").issuer.TrimEnd('/').Split('/')[-1]

  # Sign in to your environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackUser" `
    -TenantId $tenantId
  ```

## <a name="register-resource-providers"></a><span data-ttu-id="007f0-126">Register resource providers</span><span class="sxs-lookup"><span data-stu-id="007f0-126">Register resource providers</span></span>

<span data-ttu-id="007f0-127">Resource providers aren’t automatically registered for new user subscriptions that don’t have any resources deployed through the portal.</span><span class="sxs-lookup"><span data-stu-id="007f0-127">Resource providers aren’t automatically registered for new user subscriptions that don’t have any resources deployed through the portal.</span></span> <span data-ttu-id="007f0-128">You can explicitly register a resource provider by running the following script:</span><span class="sxs-lookup"><span data-stu-id="007f0-128">You can explicitly register a resource provider by running the following script:</span></span>

```PowerShell  
foreach($s in (Get-AzureRmSubscription)) {
        Select-AzureRmSubscription -SubscriptionId $s.SubscriptionId | Out-Null
        Write-Progress $($s.SubscriptionId + " : " + $s.SubscriptionName)
Get-AzureRmResourceProvider -ListAvailable | Register-AzureRmResourceProvider -Force
    }
```

## <a name="test-the-connectivity"></a><span data-ttu-id="007f0-129">Test the connectivity</span><span class="sxs-lookup"><span data-stu-id="007f0-129">Test the connectivity</span></span>

<span data-ttu-id="007f0-130">When you've got everything set up, test connectivity by using PowerShell to create resources in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="007f0-130">When you've got everything set up, test connectivity by using PowerShell to create resources in Azure Stack.</span></span> <span data-ttu-id="007f0-131">As a test, create a resource group for an application and add a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="007f0-131">As a test, create a resource group for an application and add a virtual machine.</span></span> <span data-ttu-id="007f0-132">Run the following command to create a resource group named "MyResourceGroup":</span><span class="sxs-lookup"><span data-stu-id="007f0-132">Run the following command to create a resource group named "MyResourceGroup":</span></span>

```PowerShell  
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a><span data-ttu-id="007f0-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="007f0-133">Next steps</span></span>

- [<span data-ttu-id="007f0-134">Develop templates for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="007f0-134">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
- [<span data-ttu-id="007f0-135">Deploy templates with PowerShell</span><span class="sxs-lookup"><span data-stu-id="007f0-135">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)
- <span data-ttu-id="007f0-136">If you want to set up PowerShell for the cloud operator environment, refer to the [Configure the Azure Stack operator's PowerShell environment](../azure-stack-powershell-configure-admin.md) article.</span><span class="sxs-lookup"><span data-stu-id="007f0-136">If you want to set up PowerShell for the cloud operator environment, refer to the [Configure the Azure Stack operator's PowerShell environment](../azure-stack-powershell-configure-admin.md) article.</span></span>