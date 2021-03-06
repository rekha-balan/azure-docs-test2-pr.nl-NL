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
# <a name="use-api-version-profiles-for-powershell-in-azure-stack"></a>Use API version profiles for PowerShell in Azure Stack

*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*

API version profiles provide a way to manage version differences between Azure and Azure Stack. An API version profile is a set of AzureRM PowerShell modules with specific API versions. Each cloud platform has a set of supported API version profiles. For example, Azure Stack supports a specific dated profile version such as  **2017-03-09-profile**, and Azure supports the **latest** API version profile. When you install a profile, the AzureRM PowerShell modules that correspond to the specified profile are installed.

 

## <a name="install-the-powershell-module-required-to-use-api-version-profiles"></a>Install the PowerShell module required to use API version profiles

The **AzureRM.Bootstrapper** module that is available through the PowerShell Gallery provides PowerShell cmdlets that are required to work with API version profiles. Use the following cmdlet to install the AzureRM.Bootstrapper module:

```PowerShell
Install-Module -Name AzureRm.BootStrapper
```

## <a name="install-a-profile"></a>Install a profile

Use the **Install-AzureRmProfile** cmdlet with the **2017-03-09-profile** API version profile to install the AzureRM modules required by Azure Stack. The Azure Stack operator modules are not installed with this API version profile. They should be installed separately as specified in the Step 3 of the [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) article.

```PowerShell 
Install-AzureRMProfile -Profile 2017-03-09-profile
```
## <a name="install-and-import-modules-in-a-profile"></a>Install and import modules in a profile

Use the **Use-AzureRmProfile** cmdlet to install and import modules that are associated with an API version profile. You can import only one API version profile in a PowerShell session. To import a different API version profile, you must open a new PowerShell session. The Use-AzureRMProfile cmdlet runs the following tasks:  
1. Checks if the PowerShell modules associated with the specified API version profile are installed in the current scope.  
2. Downloads and installs the modules if they are not already installed.   
3. Imports the modules into the current PowerShell session. 

```PowerShell
# Installs and imports the specified API version profile into the current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser

# Installs and imports the specified API version profile into the current PowerShell session without any prompts
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser -Force
```

To install and import selected AzureRM modules from an API version profile, run the Use-AzureRMProfile cmdlet with the **Module** parameter:

```PowerShell
# Installs and imports the compute, Storage and Network modules from the specified API version profile into your current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Module AzureRM.Compute, AzureRM.Storage, AzureRM.Network
```

## <a name="get-the-installed-profiles"></a>Get the installed profiles

Use the **Get-AzureRmProfile** cmdlet to get the list of available API version profiles: 

```PowerShell
# lists all API version profiles provided by the AzureRM.BootStrapper module.
Get-AzureRmProfile -ListAvailable 

# lists the API version profiles which are installed on your machine
Get-AzureRmProfile
```
## <a name="update-profiles"></a>Update profiles

Use the **Update-AzureRmProfile** cmdlet to update the modules in an API version profile to the latest version of modules that are available in the PSGallery. It's recommended to always run the **Update-AzureRmProfile** cmdlet in a new PowerShell session to avoid conflicts when importing modules. The Update-AzureRmProfile cmdlet runs the following tasks:

1. Checks if the latest versions of modules are installed in the given API version profile for the current scope.  
2. Prompts you to install if they are not already installed.  
3. Installs and imports the updated modules into the current PowerShell session.  

```PowerShell
Update-AzureRmProfile -Profile 2017-03-09-profile
```

To remove the previously installed versions of the modules before updating to the latest available version, use the Update-AzureRmProfile cmdlet along with the **-RemovePreviousVersions** parameter:

```PowerShell 
Update-AzureRmProfile -Profile 2017-03-09-profile -RemovePreviousVersions
```

This cmdlet runs the following tasks:  

1. Checks if the latest versions of modules are installed in the given API version profile for the current scope.  
2. Removes the older versions of modules from the current API version profile and in the current PowerShell session.  
4. prompts you to install the latest version.  
5. Installs and imports the updated modules into the current PowerShell session.  
 
## <a name="uninstall-profiles"></a>Uninstall profiles

Use the **Uninstall-AzureRmProfile** cmdlet to uninstall the specified API version profile.

```PowerShell 
Uninstall-AzureRmProfile -Profile 2017-03-09-profile
```

## <a name="next-steps"></a>Next steps
* [Install PowerShell for Azure Stack](azure-stack-powershell-install.md)
* [Configure the Azure Stack user's PowerShell environment](azure-stack-powershell-configure-user.md)  
