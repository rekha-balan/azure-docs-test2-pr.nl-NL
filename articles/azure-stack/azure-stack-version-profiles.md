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
# <a name="manage-api-version-profiles-in-azure-stack"></a>Manage API version profiles in Azure Stack

API version profiles provide a way to manage version differences between Azure and Azure Stack. An API version profile is a set of AzureRM PowerShell modules with specific API versions. Each cloud platform has a set of supported API version profiles. For example, Azure Stack supports a specific dated profile version such as  **2017-03-09-profile**, and Azure supports the **latest** API version profile. When you install a profile, the AzureRM PowerShell modules that correspond to the specified profile are installed.

## <a name="install-the-powershell-module-required-to-use-api-version-profiles"></a>Install the PowerShell module required to use API version profiles

The **AzureRM.Bootstrapper** module that is available through the PowerShell Gallery provides PowerShell cmdlets that are required to work with API version profiles. Use the following cmdlet to install the AzureRM.Bootstrapper module:

```PowerShell
Install-Module -Name AzureRm.BootStrapper
```
The AzureRM.Bootstrapper module is in preview; details and functionality are subject to change. To download and install the latest version of this module from the PowerShell Gallery, run the following cmdlet:

```PowerShell
Update-Module -Name "AzureRm.BootStrapper"
```

## <a name="install-a-profile"></a>Install a profile

Use the **Install-AzureRmProfile** cmdlet with the **2017-03-09-profile** API version profile to install the AzureRM modules required by Azure Stack. Note that the Azure Stack administrator modules are not installed with this API version profile, and they should be installed separately as specified in the Step 3 of the [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) article.

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
* [Configure PowerShell for use with Azure Stack](azure-stack-powershell-configure.md)  
