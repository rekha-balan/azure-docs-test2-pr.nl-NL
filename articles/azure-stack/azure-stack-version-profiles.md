---
title: Using API version profiles in Azure Stack | Microsoft Docs
description: Learn about API version profiles in Azure Stack.
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
ms.date: 03/21/2017
ms.author: sngun
ms.openlocfilehash: 4584323cb2f30b76b574ad0d8f131c37d0cf8d10
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550055"
---
# <a name="manage-api-version-profiles-in-azure-stack"></a><span data-ttu-id="af644-103">Manage API version profiles in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="af644-103">Manage API version profiles in Azure Stack</span></span>

<span data-ttu-id="af644-104">API version profiles provide a way to manage version differences between Azure and Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="af644-104">API version profiles provide a way to manage version differences between Azure and Azure Stack.</span></span> <span data-ttu-id="af644-105">An API version profile is a set of AzureRM PowerShell modules with specific API versions.</span><span class="sxs-lookup"><span data-stu-id="af644-105">An API version profile is a set of AzureRM PowerShell modules with specific API versions.</span></span> <span data-ttu-id="af644-106">Each cloud platform has a set of supported API version profiles.</span><span class="sxs-lookup"><span data-stu-id="af644-106">Each cloud platform has a set of supported API version profiles.</span></span> <span data-ttu-id="af644-107">For example, Azure Stack supports a specific dated profile version such as  **2017-03-09-profile**, and Azure supports the **latest** API version profile.</span><span class="sxs-lookup"><span data-stu-id="af644-107">For example, Azure Stack supports a specific dated profile version such as  **2017-03-09-profile**, and Azure supports the **latest** API version profile.</span></span> <span data-ttu-id="af644-108">When you install a profile, the AzureRM PowerShell modules that correspond to the specified profile are installed.</span><span class="sxs-lookup"><span data-stu-id="af644-108">When you install a profile, the AzureRM PowerShell modules that correspond to the specified profile are installed.</span></span>

## <a name="install-the-powershell-module-required-to-use-api-version-profiles"></a><span data-ttu-id="af644-109">Install the PowerShell module required to use API version profiles</span><span class="sxs-lookup"><span data-stu-id="af644-109">Install the PowerShell module required to use API version profiles</span></span>

<span data-ttu-id="af644-110">The **AzureRM.Bootstrapper** module that is available through the PowerShell Gallery provides PowerShell cmdlets that are required to work with API version profiles.</span><span class="sxs-lookup"><span data-stu-id="af644-110">The **AzureRM.Bootstrapper** module that is available through the PowerShell Gallery provides PowerShell cmdlets that are required to work with API version profiles.</span></span> <span data-ttu-id="af644-111">Use the following cmdlet to install the AzureRM.Bootstrapper module:</span><span class="sxs-lookup"><span data-stu-id="af644-111">Use the following cmdlet to install the AzureRM.Bootstrapper module:</span></span>

```PowerShell
Install-Module -Name AzureRm.BootStrapper
```
<span data-ttu-id="af644-112">The AzureRM.Bootstrapper module is in preview; details and functionality are subject to change.</span><span class="sxs-lookup"><span data-stu-id="af644-112">The AzureRM.Bootstrapper module is in preview; details and functionality are subject to change.</span></span> <span data-ttu-id="af644-113">To download and install the latest version of this module from the PowerShell Gallery, run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="af644-113">To download and install the latest version of this module from the PowerShell Gallery, run the following cmdlet:</span></span>

```PowerShell
Update-Module -Name "AzureRm.BootStrapper"
```

## <a name="install-a-profile"></a><span data-ttu-id="af644-114">Install a profile</span><span class="sxs-lookup"><span data-stu-id="af644-114">Install a profile</span></span>

<span data-ttu-id="af644-115">Use the **Install-AzureRmProfile** cmdlet with the **2017-03-09-profile** API version profile to install the AzureRM modules required by Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="af644-115">Use the **Install-AzureRmProfile** cmdlet with the **2017-03-09-profile** API version profile to install the AzureRM modules required by Azure Stack.</span></span> <span data-ttu-id="af644-116">Note that the Azure Stack administrator modules are not installed with this API version profile, and they should be installed separately as specified in the Step 3 of the [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) article.</span><span class="sxs-lookup"><span data-stu-id="af644-116">Note that the Azure Stack administrator modules are not installed with this API version profile, and they should be installed separately as specified in the Step 3 of the [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) article.</span></span>

```PowerShell 
Install-AzureRMProfile -Profile 2017-03-09-profile
```
## <a name="install-and-import-modules-in-a-profile"></a><span data-ttu-id="af644-117">Install and import modules in a profile</span><span class="sxs-lookup"><span data-stu-id="af644-117">Install and import modules in a profile</span></span>

<span data-ttu-id="af644-118">Use the **Use-AzureRmProfile** cmdlet to install and import modules that are associated with an API version profile.</span><span class="sxs-lookup"><span data-stu-id="af644-118">Use the **Use-AzureRmProfile** cmdlet to install and import modules that are associated with an API version profile.</span></span> <span data-ttu-id="af644-119">You can import only one API version profile in a PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="af644-119">You can import only one API version profile in a PowerShell session.</span></span> <span data-ttu-id="af644-120">To import a different API version profile, you must open a new PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="af644-120">To import a different API version profile, you must open a new PowerShell session.</span></span> <span data-ttu-id="af644-121">The Use-AzureRMProfile cmdlet runs the following tasks:</span><span class="sxs-lookup"><span data-stu-id="af644-121">The Use-AzureRMProfile cmdlet runs the following tasks:</span></span>  
1. <span data-ttu-id="af644-122">Checks if the PowerShell modules associated with the specified API version profile are installed in the current scope.</span><span class="sxs-lookup"><span data-stu-id="af644-122">Checks if the PowerShell modules associated with the specified API version profile are installed in the current scope.</span></span>  
2. <span data-ttu-id="af644-123">Downloads and installs the modules if they are not already installed.</span><span class="sxs-lookup"><span data-stu-id="af644-123">Downloads and installs the modules if they are not already installed.</span></span>   
3. <span data-ttu-id="af644-124">Imports the modules into the current PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="af644-124">Imports the modules into the current PowerShell session.</span></span> 

```PowerShell
# Installs and imports the specified API version profile into the current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser

# Installs and imports the specified API version profile into the current PowerShell session without any prompts
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser -Force
```

<span data-ttu-id="af644-125">To install and import selected AzureRM modules from an API version profile, run the Use-AzureRMProfile cmdlet with the **Module** parameter:</span><span class="sxs-lookup"><span data-stu-id="af644-125">To install and import selected AzureRM modules from an API version profile, run the Use-AzureRMProfile cmdlet with the **Module** parameter:</span></span>

```PowerShell
# Installs and imports the compute, Storage and Network modules from the specified API version profile into your current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Module AzureRM.Compute, AzureRM.Storage, AzureRM.Network
```

## <a name="get-the-installed-profiles"></a><span data-ttu-id="af644-126">Get the installed profiles</span><span class="sxs-lookup"><span data-stu-id="af644-126">Get the installed profiles</span></span>

<span data-ttu-id="af644-127">Use the **Get-AzureRmProfile** cmdlet to get the list of available API version profiles:</span><span class="sxs-lookup"><span data-stu-id="af644-127">Use the **Get-AzureRmProfile** cmdlet to get the list of available API version profiles:</span></span> 

```PowerShell
# lists all API version profiles provided by the AzureRM.BootStrapper module.
Get-AzureRmProfile -ListAvailable 

# lists the API version profiles which are installed on your machine
Get-AzureRmProfile
```
## <a name="update-profiles"></a><span data-ttu-id="af644-128">Update profiles</span><span class="sxs-lookup"><span data-stu-id="af644-128">Update profiles</span></span>

<span data-ttu-id="af644-129">Use the **Update-AzureRmProfile** cmdlet to update the modules in an API version profile to the latest version of modules that are available in the PSGallery.</span><span class="sxs-lookup"><span data-stu-id="af644-129">Use the **Update-AzureRmProfile** cmdlet to update the modules in an API version profile to the latest version of modules that are available in the PSGallery.</span></span> <span data-ttu-id="af644-130">It's recommended to always run the **Update-AzureRmProfile** cmdlet in a new PowerShell session to avoid conflicts when importing modules.</span><span class="sxs-lookup"><span data-stu-id="af644-130">It's recommended to always run the **Update-AzureRmProfile** cmdlet in a new PowerShell session to avoid conflicts when importing modules.</span></span> <span data-ttu-id="af644-131">The Update-AzureRmProfile cmdlet runs the following tasks:</span><span class="sxs-lookup"><span data-stu-id="af644-131">The Update-AzureRmProfile cmdlet runs the following tasks:</span></span>

1. <span data-ttu-id="af644-132">Checks if the latest versions of modules are installed in the given API version profile for the current scope.</span><span class="sxs-lookup"><span data-stu-id="af644-132">Checks if the latest versions of modules are installed in the given API version profile for the current scope.</span></span>  
2. <span data-ttu-id="af644-133">Prompts you to install if they are not already installed.</span><span class="sxs-lookup"><span data-stu-id="af644-133">Prompts you to install if they are not already installed.</span></span>  
3. <span data-ttu-id="af644-134">Installs and imports the updated modules into the current PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="af644-134">Installs and imports the updated modules into the current PowerShell session.</span></span>  

```PowerShell
Update-AzureRmProfile -Profile 2017-03-09-profile
```

<span data-ttu-id="af644-135">To remove the previously installed versions of the modules before updating to the latest available version, use the Update-AzureRmProfile cmdlet along with the **-RemovePreviousVersions** parameter:</span><span class="sxs-lookup"><span data-stu-id="af644-135">To remove the previously installed versions of the modules before updating to the latest available version, use the Update-AzureRmProfile cmdlet along with the **-RemovePreviousVersions** parameter:</span></span>

```PowerShell 
Update-AzureRmProfile -Profile 2017-03-09-profile -RemovePreviousVersions
```

<span data-ttu-id="af644-136">This cmdlet runs the following tasks:</span><span class="sxs-lookup"><span data-stu-id="af644-136">This cmdlet runs the following tasks:</span></span>  

1. <span data-ttu-id="af644-137">Checks if the latest versions of modules are installed in the given API version profile for the current scope.</span><span class="sxs-lookup"><span data-stu-id="af644-137">Checks if the latest versions of modules are installed in the given API version profile for the current scope.</span></span>  
2. <span data-ttu-id="af644-138">Removes the older versions of modules from the current API version profile and in the current PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="af644-138">Removes the older versions of modules from the current API version profile and in the current PowerShell session.</span></span>  
4. <span data-ttu-id="af644-139">prompts you to install the latest version.</span><span class="sxs-lookup"><span data-stu-id="af644-139">prompts you to install the latest version.</span></span>  
5. <span data-ttu-id="af644-140">Installs and imports the updated modules into the current PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="af644-140">Installs and imports the updated modules into the current PowerShell session.</span></span>  
 
## <a name="uninstall-profiles"></a><span data-ttu-id="af644-141">Uninstall profiles</span><span class="sxs-lookup"><span data-stu-id="af644-141">Uninstall profiles</span></span>

<span data-ttu-id="af644-142">Use the **Uninstall-AzureRmProfile** cmdlet to uninstall the specified API version profile.</span><span class="sxs-lookup"><span data-stu-id="af644-142">Use the **Uninstall-AzureRmProfile** cmdlet to uninstall the specified API version profile.</span></span>

```PowerShell 
Uninstall-AzureRmProfile -Profile 2017-03-09-profile
```

## <a name="next-steps"></a><span data-ttu-id="af644-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="af644-143">Next steps</span></span>
* [<span data-ttu-id="af644-144">Install PowerShell for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="af644-144">Install PowerShell for Azure Stack</span></span>](azure-stack-powershell-install.md)
* [<span data-ttu-id="af644-145">Configure PowerShell for use with Azure Stack</span><span class="sxs-lookup"><span data-stu-id="af644-145">Configure PowerShell for use with Azure Stack</span></span>](azure-stack-powershell-configure.md)  
