---
title: Configure PowerShell for use with Azure Stack | Microsoft Docs
description: Learn how to configure PowerShell for Azure Stack.
services: azure-stack
documentationcenter: ''
author: SnehaGunda
manager: byronr
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: sngun
ms.openlocfilehash: 181252126c8f0dc2379b1ce26c758da6a97b6c52
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554544"
---
# <a name="configure-powershell-for-use-with-azure-stack"></a><span data-ttu-id="3053f-103">Configure PowerShell for use with Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3053f-103">Configure PowerShell for use with Azure Stack</span></span> 

<span data-ttu-id="3053f-104">You can use PowerShell to connect to an Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="3053f-104">You can use PowerShell to connect to an Azure Stack environment.</span></span> <span data-ttu-id="3053f-105">After connecting, you can manage and deploy Azure Stack resources.</span><span class="sxs-lookup"><span data-stu-id="3053f-105">After connecting, you can manage and deploy Azure Stack resources.</span></span> <span data-ttu-id="3053f-106">You can use the steps described in this article either from MAS-CON01, the Azure Stack host computer, or a Windows-based external client if you are connected through VPN.</span><span class="sxs-lookup"><span data-stu-id="3053f-106">You can use the steps described in this article either from MAS-CON01, the Azure Stack host computer, or a Windows-based external client if you are connected through VPN.</span></span> <span data-ttu-id="3053f-107">The steps in this article are applicable for Azure Stack instances deployed through Azure Active Directory(AAD) or Active Directory Federation Services(ADFS).</span><span class="sxs-lookup"><span data-stu-id="3053f-107">The steps in this article are applicable for Azure Stack instances deployed through Azure Active Directory(AAD) or Active Directory Federation Services(ADFS).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3053f-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3053f-108">Prerequisites</span></span>
* [<span data-ttu-id="3053f-109">Install Azure Stack compatible Azure PowerShell on MAS-CON01 or on your local computer.</span><span class="sxs-lookup"><span data-stu-id="3053f-109">Install Azure Stack compatible Azure PowerShell on MAS-CON01 or on your local computer.</span></span>](azure-stack-powershell-install.md)  
* [<span data-ttu-id="3053f-110">Download tools required to work with Azure Stack to MAS-CON01 or to your local computer.</span><span class="sxs-lookup"><span data-stu-id="3053f-110">Download tools required to work with Azure Stack to MAS-CON01 or to your local computer.</span></span>](azure-stack-powershell-download.md)  

## <a name="import-the-connect-powershell-module"></a><span data-ttu-id="3053f-111">Import the Connect PowerShell module</span><span class="sxs-lookup"><span data-stu-id="3053f-111">Import the Connect PowerShell module</span></span>

<span data-ttu-id="3053f-112">After downloading the tools, navigate to the downloaded folder and import the **Connect** PowerShell module by using the following command:</span><span class="sxs-lookup"><span data-stu-id="3053f-112">After downloading the tools, navigate to the downloaded folder and import the **Connect** PowerShell module by using the following command:</span></span>  
```PowerShell
Import-Module .\Connect\AzureStack.Connect.psm1
```

> [!NOTE]
> <span data-ttu-id="3053f-113">When importing the module specified earlier, if you receive an error that “AzureStack.Connect.psm1 is not digitally signed and you cannot run this script on the current system”, you can resolve it by executing the following command in an elevated PowerShell window:</span><span class="sxs-lookup"><span data-stu-id="3053f-113">When importing the module specified earlier, if you receive an error that “AzureStack.Connect.psm1 is not digitally signed and you cannot run this script on the current system”, you can resolve it by executing the following command in an elevated PowerShell window:</span></span>  

```PowerShell
Set-ExecutionPolicy Unrestricted
```

## <a name="configure-the-powershell-environment"></a><span data-ttu-id="3053f-114">Configure the PowerShell Environment</span><span class="sxs-lookup"><span data-stu-id="3053f-114">Configure the PowerShell Environment</span></span>
<span data-ttu-id="3053f-115">Use the following steps to configure your Azure Stack environment:</span><span class="sxs-lookup"><span data-stu-id="3053f-115">Use the following steps to configure your Azure Stack environment:</span></span>

1. <span data-ttu-id="3053f-116">Register an AzureRM environment that targets your Azure Stack instance by using the following cmdlets:</span><span class="sxs-lookup"><span data-stu-id="3053f-116">Register an AzureRM environment that targets your Azure Stack instance by using the following cmdlets:</span></span>  
    ```PowerShell
    # Use this command to access the administrative portal.
    Add-AzureStackAzureRmEnvironment -Name "AzureStackAdmin" -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

    # Use this command to access the user portal.
    Add-AzureStackAzureRmEnvironment -Name "AzureStackUser" -ArmEndpoint "https://management.local.azurestack.external" 
    ```

    ![Get environment details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-powershell-configure/getenvdetails.png)

2. <span data-ttu-id="3053f-118">Get the GUID value of the Azure Active Directory(AAD) tenant that is used to deploy the Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3053f-118">Get the GUID value of the Azure Active Directory(AAD) tenant that is used to deploy the Azure Stack.</span></span> <span data-ttu-id="3053f-119">If your Azure Stack environment is deployed by using:</span><span class="sxs-lookup"><span data-stu-id="3053f-119">If your Azure Stack environment is deployed by using:</span></span>  

    <span data-ttu-id="3053f-120">a.</span><span class="sxs-lookup"><span data-stu-id="3053f-120">a.</span></span> <span data-ttu-id="3053f-121">**Azure Active Directory**, use the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3053f-121">**Azure Active Directory**, use the following cmdlet:</span></span>
    
    ```PowerShell
    # Use this command to get the GUID value in the administrator's environment. 
    $TenantID = Get-DirectoryTenantID -AADTenantName "<myaadtenant>.onmicrosoft.com" -EnvironmentName AzureStackAdmin
    
    # Use this command to get the GUID value in the user's environment. 
    $TenantID = Get-DirectoryTenantID -AADTenantName "<myaadtenant>.onmicrosoft.com" -EnvironmentName AzureStackUser
    ```
    <span data-ttu-id="3053f-122">b.</span><span class="sxs-lookup"><span data-stu-id="3053f-122">b.</span></span> <span data-ttu-id="3053f-123">**Active Directory Federation Services**, use the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3053f-123">**Active Directory Federation Services**, use the following cmdlet:</span></span>
    
    ```PowerShell
    # This command gets the GUID value in the administrator's environment.
    $TenantID = Get-DirectoryTenantID -ADFS -EnvironmentName AzureStackAdmin 
    
    # This command gets the GUID value in the user's environment. 
    $TenantID = Get-DirectoryTenantID -ADFS -EnvironmentName AzureStackUser 
    ```

## <a name="sign-in-to-azure-stack"></a><span data-ttu-id="3053f-124">Sign in to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3053f-124">Sign in to Azure Stack</span></span> 
<span data-ttu-id="3053f-125">After the AzureRM environment is registered to target the Azure Stack instance, you can use all the AzureRM commands in your Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="3053f-125">After the AzureRM environment is registered to target the Azure Stack instance, you can use all the AzureRM commands in your Azure Stack environment.</span></span> <span data-ttu-id="3053f-126">Use the following command to sign in to your Azure Stack administrator or user account:</span><span class="sxs-lookup"><span data-stu-id="3053f-126">Use the following command to sign in to your Azure Stack administrator or user account:</span></span>

```PowerShell
# Store the AAD service administrator or user account credentials in a variable. 
$UserName='<Username of the service administrator or user account>'
$Password='<administrator or user password>'| ConvertTo-SecureString -Force -AsPlainText
$Credential=New-Object PSCredential($UserName,$Password)

# Use this command to sign-in to the administrative portal.
Login-AzureRmAccount -EnvironmentName "AzureStackAdmin" -TenantId $TenantID -Credential $Credential

# Use this command to sign-in to the user portal.
Login-AzureRmAccount -EnvironmentName "AzureStackUser" -TenantId $TenantID -Credential $Credential
```
![Get subscription details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-powershell-configure/subscriptiondetails.png)

## <a name="register-resource-providers"></a><span data-ttu-id="3053f-128">Register resource providers</span><span class="sxs-lookup"><span data-stu-id="3053f-128">Register resource providers</span></span> 

<span data-ttu-id="3053f-129">After you sign in to the administrator or user portal, you can issue operations against resource providers registered in that subscription.</span><span class="sxs-lookup"><span data-stu-id="3053f-129">After you sign in to the administrator or user portal, you can issue operations against resource providers registered in that subscription.</span></span> <span data-ttu-id="3053f-130">By default, all the foundational resource providers are registered in the **Default Provider Subscription(administrator subscription)**.</span><span class="sxs-lookup"><span data-stu-id="3053f-130">By default, all the foundational resource providers are registered in the **Default Provider Subscription(administrator subscription)**.</span></span> <span data-ttu-id="3053f-131">When operating on a newly created user subscription, and if these subscription doesn’t have any resources deployed through the portal, you should register the resource providers for this subscription by using the following command:</span><span class="sxs-lookup"><span data-stu-id="3053f-131">When operating on a newly created user subscription, and if these subscription doesn’t have any resources deployed through the portal, you should register the resource providers for this subscription by using the following command:</span></span>

```PowerShell
  Get-AzureRmResourceProvider -ListAvailable 
```

![unregistered PowerShell](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-powershell-configure/unregisteredrps.png)  

<span data-ttu-id="3053f-133">In the user subscriptions, you should manually register these resource providers before you use them.</span><span class="sxs-lookup"><span data-stu-id="3053f-133">In the user subscriptions, you should manually register these resource providers before you use them.</span></span> <span data-ttu-id="3053f-134">To register providers on the current subscription, use the following command:</span><span class="sxs-lookup"><span data-stu-id="3053f-134">To register providers on the current subscription, use the following command:</span></span>

```PowerShell
Register-AllAzureRmProviders
```

![registering PowerShell](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-powershell-configure/registeringrps.png)  

<span data-ttu-id="3053f-136">To register all resource providers on all your subscriptions, use the following command:</span><span class="sxs-lookup"><span data-stu-id="3053f-136">To register all resource providers on all your subscriptions, use the following command:</span></span>

```PowerShell
Register-AllAzureRmProvidersOnAllSubscriptions
```

## <a name="next-steps"></a><span data-ttu-id="3053f-137">Next Steps</span><span class="sxs-lookup"><span data-stu-id="3053f-137">Next Steps</span></span>
* [<span data-ttu-id="3053f-138">Develop templates for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3053f-138">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)
* [<span data-ttu-id="3053f-139">Deploy templates with PowerShell</span><span class="sxs-lookup"><span data-stu-id="3053f-139">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)




