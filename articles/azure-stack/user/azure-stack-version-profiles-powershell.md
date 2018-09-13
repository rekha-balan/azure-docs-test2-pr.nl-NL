---
title: Using API version profiles with PowerShell in Azure Stack | Microsoft Docs
description: Learn about using API version profiles with PowerShell in Azure Stack.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: EBAEA4D2-098B-4B5A-A197-2CEA631A1882
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2018
ms.author: sethm
ms.reviewer: sijuman
ms.openlocfilehash: 994893eb73356fde9acc593569dc5fb1c5a0106f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968683"
---
# <a name="use-api-version-profiles-for-powershell-in-azure-stack"></a><span data-ttu-id="79d71-103">Use API version profiles for PowerShell in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="79d71-103">Use API version profiles for PowerShell in Azure Stack</span></span>

<span data-ttu-id="79d71-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="79d71-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="79d71-105">API version profiles provide a way to manage version differences between Azure and Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="79d71-105">API version profiles provide a way to manage version differences between Azure and Azure Stack.</span></span> <span data-ttu-id="79d71-106">An API version profile is a set of AzureRM PowerShell modules with specific API versions.</span><span class="sxs-lookup"><span data-stu-id="79d71-106">An API version profile is a set of AzureRM PowerShell modules with specific API versions.</span></span> <span data-ttu-id="79d71-107">Each cloud platform has a set of supported API version profiles.</span><span class="sxs-lookup"><span data-stu-id="79d71-107">Each cloud platform has a set of supported API version profiles.</span></span> <span data-ttu-id="79d71-108">For example, Azure Stack supports a specific dated profile version such as  **2017-03-09-profile**, and Azure supports the **latest** API version profile.</span><span class="sxs-lookup"><span data-stu-id="79d71-108">For example, Azure Stack supports a specific dated profile version such as  **2017-03-09-profile**, and Azure supports the **latest** API version profile.</span></span> <span data-ttu-id="79d71-109">When you install a profile, the AzureRM PowerShell modules that correspond to the specified profile are installed.</span><span class="sxs-lookup"><span data-stu-id="79d71-109">When you install a profile, the AzureRM PowerShell modules that correspond to the specified profile are installed.</span></span>

 

## <a name="install-the-powershell-module-required-to-use-api-version-profiles"></a><span data-ttu-id="79d71-110">Install the PowerShell module required to use API version profiles</span><span class="sxs-lookup"><span data-stu-id="79d71-110">Install the PowerShell module required to use API version profiles</span></span>

<span data-ttu-id="79d71-111">The **AzureRM.Bootstrapper** module that is available through the PowerShell Gallery provides PowerShell cmdlets that are required to work with API version profiles.</span><span class="sxs-lookup"><span data-stu-id="79d71-111">The **AzureRM.Bootstrapper** module that is available through the PowerShell Gallery provides PowerShell cmdlets that are required to work with API version profiles.</span></span> <span data-ttu-id="79d71-112">Use the following cmdlet to install the AzureRM.Bootstrapper module:</span><span class="sxs-lookup"><span data-stu-id="79d71-112">Use the following cmdlet to install the AzureRM.Bootstrapper module:</span></span>

```PowerShell
Install-Module -Name AzureRm.BootStrapper
```

## <a name="install-a-profile"></a><span data-ttu-id="79d71-113">Install a profile</span><span class="sxs-lookup"><span data-stu-id="79d71-113">Install a profile</span></span>

<span data-ttu-id="79d71-114">Use the **Install-AzureRmProfile** cmdlet with the **2017-03-09-profile** API version profile to install the AzureRM modules required by Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="79d71-114">Use the **Install-AzureRmProfile** cmdlet with the **2017-03-09-profile** API version profile to install the AzureRM modules required by Azure Stack.</span></span> <span data-ttu-id="79d71-115">The Azure Stack operator modules are not installed with this API version profile.</span><span class="sxs-lookup"><span data-stu-id="79d71-115">The Azure Stack operator modules are not installed with this API version profile.</span></span> <span data-ttu-id="79d71-116">They should be installed separately as specified in the Step 3 of the [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) article.</span><span class="sxs-lookup"><span data-stu-id="79d71-116">They should be installed separately as specified in the Step 3 of the [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) article.</span></span>

```PowerShell 
Install-AzureRMProfile -Profile 2017-03-09-profile
```
## <a name="install-and-import-modules-in-a-profile"></a><span data-ttu-id="79d71-117">Install and import modules in a profile</span><span class="sxs-lookup"><span data-stu-id="79d71-117">Install and import modules in a profile</span></span>

<span data-ttu-id="79d71-118">Use the **Use-AzureRmProfile** cmdlet to install and import modules that are associated with an API version profile.</span><span class="sxs-lookup"><span data-stu-id="79d71-118">Use the **Use-AzureRmProfile** cmdlet to install and import modules that are associated with an API version profile.</span></span> <span data-ttu-id="79d71-119">You can import only one API version profile in a PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="79d71-119">You can import only one API version profile in a PowerShell session.</span></span> <span data-ttu-id="79d71-120">To import a different API version profile, you must open a new PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="79d71-120">To import a different API version profile, you must open a new PowerShell session.</span></span> <span data-ttu-id="79d71-121">The Use-AzureRMProfile cmdlet runs the following tasks:</span><span class="sxs-lookup"><span data-stu-id="79d71-121">The Use-AzureRMProfile cmdlet runs the following tasks:</span></span>  
1. <span data-ttu-id="79d71-122">Checks if the PowerShell modules associated with the specified API version profile are installed in the current scope.</span><span class="sxs-lookup"><span data-stu-id="79d71-122">Checks if the PowerShell modules associated with the specified API version profile are installed in the current scope.</span></span>  
2. <span data-ttu-id="79d71-123">Downloads and installs the modules if they are not already installed.</span><span class="sxs-lookup"><span data-stu-id="79d71-123">Downloads and installs the modules if they are not already installed.</span></span>   
3. <span data-ttu-id="79d71-124">Imports the modules into the current PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="79d71-124">Imports the modules into the current PowerShell session.</span></span> 

```PowerShell
# Installs and imports the specified API version profile into the current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser

# Installs and imports the specified API version profile into the current PowerShell session without any prompts
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser -Force
```

<span data-ttu-id="79d71-125">To install and import selected AzureRM modules from an API version profile, run the Use-AzureRMProfile cmdlet with the **Module** parameter:</span><span class="sxs-lookup"><span data-stu-id="79d71-125">To install and import selected AzureRM modules from an API version profile, run the Use-AzureRMProfile cmdlet with the **Module** parameter:</span></span>

```PowerShell
# Installs and imports the compute, Storage and Network modules from the specified API version profile into your current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Module AzureRM.Compute, AzureRM.Storage, AzureRM.Network
```

## <a name="get-the-installed-profiles"></a><span data-ttu-id="79d71-126">Get the installed profiles</span><span class="sxs-lookup"><span data-stu-id="79d71-126">Get the installed profiles</span></span>

<span data-ttu-id="79d71-127">Use the **Get-AzureRmProfile** cmdlet to get the list of available API version profiles:</span><span class="sxs-lookup"><span data-stu-id="79d71-127">Use the **Get-AzureRmProfile** cmdlet to get the list of available API version profiles:</span></span> 

```PowerShell
# lists all API version profiles provided by the AzureRM.BootStrapper module.
Get-AzureRmProfile -ListAvailable 

# lists the API version profiles which are installed on your machine
Get-AzureRmProfile
```
## <a name="update-profiles"></a><span data-ttu-id="79d71-128">Update profiles</span><span class="sxs-lookup"><span data-stu-id="79d71-128">Update profiles</span></span>

<span data-ttu-id="79d71-129">Use the **Update-AzureRmProfile** cmdlet to update the modules in an API version profile to the latest version of modules that are available in the PSGallery.</span><span class="sxs-lookup"><span data-stu-id="79d71-129">Use the **Update-AzureRmProfile** cmdlet to update the modules in an API version profile to the latest version of modules that are available in the PSGallery.</span></span> <span data-ttu-id="79d71-130">It's recommended to always run the **Update-AzureRmProfile** cmdlet in a new PowerShell session to avoid conflicts when importing modules.</span><span class="sxs-lookup"><span data-stu-id="79d71-130">It's recommended to always run the **Update-AzureRmProfile** cmdlet in a new PowerShell session to avoid conflicts when importing modules.</span></span> <span data-ttu-id="79d71-131">The Update-AzureRmProfile cmdlet runs the following tasks:</span><span class="sxs-lookup"><span data-stu-id="79d71-131">The Update-AzureRmProfile cmdlet runs the following tasks:</span></span>

1. <span data-ttu-id="79d71-132">Checks if the latest versions of modules are installed in the given API version profile for the current scope.</span><span class="sxs-lookup"><span data-stu-id="79d71-132">Checks if the latest versions of modules are installed in the given API version profile for the current scope.</span></span>  
2. <span data-ttu-id="79d71-133">Prompts you to install if they are not already installed.</span><span class="sxs-lookup"><span data-stu-id="79d71-133">Prompts you to install if they are not already installed.</span></span>  
3. <span data-ttu-id="79d71-134">Installs and imports the updated modules into the current PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="79d71-134">Installs and imports the updated modules into the current PowerShell session.</span></span>  

```PowerShell
Update-AzureRmProfile -Profile 2017-03-09-profile
```

<span data-ttu-id="79d71-135">To remove the previously installed versions of the modules before updating to the latest available version, use the Update-AzureRmProfile cmdlet along with the **-RemovePreviousVersions** parameter:</span><span class="sxs-lookup"><span data-stu-id="79d71-135">To remove the previously installed versions of the modules before updating to the latest available version, use the Update-AzureRmProfile cmdlet along with the **-RemovePreviousVersions** parameter:</span></span>

```PowerShell 
Update-AzureRmProfile -Profile 2017-03-09-profile -RemovePreviousVersions
```

<span data-ttu-id="79d71-136">This cmdlet runs the following tasks:</span><span class="sxs-lookup"><span data-stu-id="79d71-136">This cmdlet runs the following tasks:</span></span>  

1. <span data-ttu-id="79d71-137">Checks if the latest versions of modules are installed in the given API version profile for the current scope.</span><span class="sxs-lookup"><span data-stu-id="79d71-137">Checks if the latest versions of modules are installed in the given API version profile for the current scope.</span></span>  
2. <span data-ttu-id="79d71-138">Removes the older versions of modules from the current API version profile and in the current PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="79d71-138">Removes the older versions of modules from the current API version profile and in the current PowerShell session.</span></span>  
4. <span data-ttu-id="79d71-139">prompts you to install the latest version.</span><span class="sxs-lookup"><span data-stu-id="79d71-139">prompts you to install the latest version.</span></span>  
5. <span data-ttu-id="79d71-140">Installs and imports the updated modules into the current PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="79d71-140">Installs and imports the updated modules into the current PowerShell session.</span></span>  
 
## <a name="uninstall-profiles"></a><span data-ttu-id="79d71-141">Uninstall profiles</span><span class="sxs-lookup"><span data-stu-id="79d71-141">Uninstall profiles</span></span>

<span data-ttu-id="79d71-142">Use the **Uninstall-AzureRmProfile** cmdlet to uninstall the specified API version profile.</span><span class="sxs-lookup"><span data-stu-id="79d71-142">Use the **Uninstall-AzureRmProfile** cmdlet to uninstall the specified API version profile.</span></span>

```PowerShell 
Uninstall-AzureRmProfile -Profile 2017-03-09-profile
```

## <a name="next-steps"></a><span data-ttu-id="79d71-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="79d71-143">Next steps</span></span>
* [<span data-ttu-id="79d71-144">Install PowerShell for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="79d71-144">Install PowerShell for Azure Stack</span></span>](azure-stack-powershell-install.md)
* [<span data-ttu-id="79d71-145">Configure the Azure Stack user's PowerShell environment</span><span class="sxs-lookup"><span data-stu-id="79d71-145">Configure the Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)  
