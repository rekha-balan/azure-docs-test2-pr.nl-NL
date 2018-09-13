---
title: Install PowerShell for Azure Stack | Microsoft Docs
description: Learn how to install PowerShell for Azure Stack.
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
ms.openlocfilehash: 0cd19509ab6ab62bd54dfcbae6caa7303c3e4e10
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556168"
---
# <a name="install-powershell-for-azure-stack"></a><span data-ttu-id="0c5a2-103">Install PowerShell for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="0c5a2-103">Install PowerShell for Azure Stack</span></span>  

<span data-ttu-id="0c5a2-104">Azure Stack compatible Azure PowerShell modules are required to work with Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="0c5a2-104">Azure Stack compatible Azure PowerShell modules are required to work with Azure Stack.</span></span> <span data-ttu-id="0c5a2-105">In this guide, we walk you through the steps required to install PowerShell in Azure Stack by using the PowerShell commands.</span><span class="sxs-lookup"><span data-stu-id="0c5a2-105">In this guide, we walk you through the steps required to install PowerShell in Azure Stack by using the PowerShell commands.</span></span> <span data-ttu-id="0c5a2-106">You can use the steps described in this article either from MAS-CON01, Azure Stack host computer, or from a Windows-based external client if you are connected through VPN.</span><span class="sxs-lookup"><span data-stu-id="0c5a2-106">You can use the steps described in this article either from MAS-CON01, Azure Stack host computer, or from a Windows-based external client if you are connected through VPN.</span></span>

> [!NOTE]
> <span data-ttu-id="0c5a2-107">The following steps require PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="0c5a2-107">The following steps require PowerShell 5.0.</span></span>  <span data-ttu-id="0c5a2-108">To check your version, run $PSVersionTable.PSVersion and compare the "Major" version.</span><span class="sxs-lookup"><span data-stu-id="0c5a2-108">To check your version, run $PSVersionTable.PSVersion and compare the "Major" version.</span></span>

<span data-ttu-id="0c5a2-109">PowerShell commands for Azure Stack are installed from the PowerShell Gallery.</span><span class="sxs-lookup"><span data-stu-id="0c5a2-109">PowerShell commands for Azure Stack are installed from the PowerShell Gallery.</span></span> <span data-ttu-id="0c5a2-110">To verify if PowerShell Gallery is available, open a PowerShell session on the MAS-CON01 computer or on your local computer if you are connected through VPN and run the following command:</span><span class="sxs-lookup"><span data-stu-id="0c5a2-110">To verify if PowerShell Gallery is available, open a PowerShell session on the MAS-CON01 computer or on your local computer if you are connected through VPN and run the following command:</span></span>

```powershell
# Returns a list of PowerShell module repositories that are registered for the current user.
Get-PSRepository
```
![GetPSrepository](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-powershell-install/getpsrepository.png)

## <a name="install-the-required-version-of-powershell-modules"></a><span data-ttu-id="0c5a2-112">Install the required version of PowerShell modules</span><span class="sxs-lookup"><span data-stu-id="0c5a2-112">Install the required version of PowerShell modules</span></span>

<span data-ttu-id="0c5a2-113">Use the following steps to install PowerShell for Azure Stack:</span><span class="sxs-lookup"><span data-stu-id="0c5a2-113">Use the following steps to install PowerShell for Azure Stack:</span></span>  

1. <span data-ttu-id="0c5a2-114">Azure Stack compatible AzureRM modules are installed through API version profiles.</span><span class="sxs-lookup"><span data-stu-id="0c5a2-114">Azure Stack compatible AzureRM modules are installed through API version profiles.</span></span>
<span data-ttu-id="0c5a2-115">To learn about API version profiles and the cmdlets provided by them, refer to the [manage API version profiles](azure-stack-version-profiles.md) article.</span><span class="sxs-lookup"><span data-stu-id="0c5a2-115">To learn about API version profiles and the cmdlets provided by them, refer to the [manage API version profiles](azure-stack-version-profiles.md) article.</span></span> <span data-ttu-id="0c5a2-116">The AzureRM.Bootstrapper module provides PowerShell commands that are required to work with API version profiles.</span><span class="sxs-lookup"><span data-stu-id="0c5a2-116">The AzureRM.Bootstrapper module provides PowerShell commands that are required to work with API version profiles.</span></span> <span data-ttu-id="0c5a2-117">Use the following command to install the AzureRM.Bootstrapper module:</span><span class="sxs-lookup"><span data-stu-id="0c5a2-117">Use the following command to install the AzureRM.Bootstrapper module:</span></span>  

  ```powershell
  # Install the AzureRM.Bootstrapper module
  Install-Module -Name AzureRm.BootStrapper
  ```
2. <span data-ttu-id="0c5a2-118">Run the following command to install the **2017-03-09-profile** version of the AzureRM modules for Compute, Storage, Network, Key Vault etc.</span><span class="sxs-lookup"><span data-stu-id="0c5a2-118">Run the following command to install the **2017-03-09-profile** version of the AzureRM modules for Compute, Storage, Network, Key Vault etc.</span></span>  

  ```powershell
  # Installs and imports the API Version Profile required by Azure Stack into the current PowerShell session.
  Use-AzureRmProfile -Profile 2017-03-09-profile
  ```
3. <span data-ttu-id="0c5a2-119">In addition to the AzureRM modules, you should also install the Azure Stack-specific PowerShell modules such as AzureStackAdmin, and AzureStackStorage by running the following command:</span><span class="sxs-lookup"><span data-stu-id="0c5a2-119">In addition to the AzureRM modules, you should also install the Azure Stack-specific PowerShell modules such as AzureStackAdmin, and AzureStackStorage by running the following command:</span></span>  

  ```powershell
  Install-Module -Name AzureStack -RequiredVersion 1.2.9
  ```
4. <span data-ttu-id="0c5a2-120">To confirm the installation, run the following command:</span><span class="sxs-lookup"><span data-stu-id="0c5a2-120">To confirm the installation, run the following command:</span></span>  

  ```powershell
  Get-Module -ListAvailable | where-Object {$_.Name -like “Azure*”}
  ```
  <span data-ttu-id="0c5a2-121">If the installation is successful, the AzureRM and AzureStack modules are displayed in the output.</span><span class="sxs-lookup"><span data-stu-id="0c5a2-121">If the installation is successful, the AzureRM and AzureStack modules are displayed in the output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c5a2-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="0c5a2-122">Next steps</span></span>

* [<span data-ttu-id="0c5a2-123">Download Azure Stack tools from GitHub</span><span class="sxs-lookup"><span data-stu-id="0c5a2-123">Download Azure Stack tools from GitHub</span></span>](azure-stack-powershell-download.md)
* [<span data-ttu-id="0c5a2-124">Configure PowerShell for use with Azure Stack</span><span class="sxs-lookup"><span data-stu-id="0c5a2-124">Configure PowerShell for use with Azure Stack</span></span>](azure-stack-powershell-configure.md)  
* [<span data-ttu-id="0c5a2-125">Manage API version profiles in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="0c5a2-125">Manage API version profiles in Azure Stack</span></span>](azure-stack-version-profiles.md)  

