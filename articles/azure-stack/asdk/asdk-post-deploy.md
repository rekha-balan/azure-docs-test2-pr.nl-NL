---
title: Post deployment configurations for the Azure Stack Development Kit (ASDK) | Microsoft Docs
description: Describes the recommended configuration changes to make after installing the Azure Stack Development Kit (ASDK).
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/11/2018
ms.author: jeffgilb
ms.reviewer: misainat
ms.openlocfilehash: 4eadbe38eede505a3339d4b6090d0a34c12a5fc2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856566"
---
# <a name="post-asdk-installation-configuration-tasks"></a><span data-ttu-id="8774f-103">Post ASDK installation configuration tasks</span><span class="sxs-lookup"><span data-stu-id="8774f-103">Post ASDK installation configuration tasks</span></span>

<span data-ttu-id="8774f-104">After [installing the Azure Stack Development Kit (ASDK)](asdk-install.md), you will need to make a some recommended post-installation configuration changes.</span><span class="sxs-lookup"><span data-stu-id="8774f-104">After [installing the Azure Stack Development Kit (ASDK)](asdk-install.md), you will need to make a some recommended post-installation configuration changes.</span></span>

## <a name="install-azure-stack-powershell"></a><span data-ttu-id="8774f-105">Install Azure Stack PowerShell</span><span class="sxs-lookup"><span data-stu-id="8774f-105">Install Azure Stack PowerShell</span></span>

<span data-ttu-id="8774f-106">Azure Stack compatible Azure PowerShell modules are required to work with Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8774f-106">Azure Stack compatible Azure PowerShell modules are required to work with Azure Stack.</span></span>

<span data-ttu-id="8774f-107">PowerShell commands for Azure Stack are installed through the PowerShell Gallery.</span><span class="sxs-lookup"><span data-stu-id="8774f-107">PowerShell commands for Azure Stack are installed through the PowerShell Gallery.</span></span> <span data-ttu-id="8774f-108">To register the PSGallery repository, open an elevated PowerShell session and run the following command:</span><span class="sxs-lookup"><span data-stu-id="8774f-108">To register the PSGallery repository, open an elevated PowerShell session and run the following command:</span></span>

``` Powershell
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted
```

<span data-ttu-id="8774f-109">You can use API version profiles  to specify Azure Stack compatible AzureRM modules.</span><span class="sxs-lookup"><span data-stu-id="8774f-109">You can use API version profiles  to specify Azure Stack compatible AzureRM modules.</span></span>  <span data-ttu-id="8774f-110">API version profiles provide a way to manage version differences between Azure and Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8774f-110">API version profiles provide a way to manage version differences between Azure and Azure Stack.</span></span> <span data-ttu-id="8774f-111">An API version profile is a set of AzureRM PowerShell modules with specific API versions.</span><span class="sxs-lookup"><span data-stu-id="8774f-111">An API version profile is a set of AzureRM PowerShell modules with specific API versions.</span></span> <span data-ttu-id="8774f-112">The **AzureRM.Bootstrapper** module that is available through the PowerShell Gallery provides PowerShell cmdlets that are required to work with API version profiles.</span><span class="sxs-lookup"><span data-stu-id="8774f-112">The **AzureRM.Bootstrapper** module that is available through the PowerShell Gallery provides PowerShell cmdlets that are required to work with API version profiles.</span></span>

 

<span data-ttu-id="8774f-113">You can install the latest Azure Stack PowerShell module with or without Internet connectivity to the ASDK host computer:</span><span class="sxs-lookup"><span data-stu-id="8774f-113">You can install the latest Azure Stack PowerShell module with or without Internet connectivity to the ASDK host computer:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8774f-114">Before installing the required version, make sure that you [uninstall any existing Azure PowerShell modules](.\.\azure-stack-powershell-install.md#3-uninstall-existing-versions-of-the-azure-stack-powershell-modules).</span><span class="sxs-lookup"><span data-stu-id="8774f-114">Before installing the required version, make sure that you [uninstall any existing Azure PowerShell modules](.\.\azure-stack-powershell-install.md#3-uninstall-existing-versions-of-the-azure-stack-powershell-modules).</span></span>

- <span data-ttu-id="8774f-115">**With an internet connection** from the ASDK host computer.</span><span class="sxs-lookup"><span data-stu-id="8774f-115">**With an internet connection** from the ASDK host computer.</span></span> <span data-ttu-id="8774f-116">Run the following PowerShell script to install these modules on your development kit installation:</span><span class="sxs-lookup"><span data-stu-id="8774f-116">Run the following PowerShell script to install these modules on your development kit installation:</span></span>

  ``` PowerShell
  # Install the AzureRM.Bootstrapper module. Select Yes when prompted to install NuGet. 
  Install-Module `
    -Name AzureRm.BootStrapper

  # Install and import the API Version Profile required by Azure Stack into the current PowerShell session.
  Use-AzureRmProfile `
    -Profile 2017-03-09-profile -Force

  # Install Azure Stack Module Version 1.4.0. If running a pre-1804 version of Azure Stack, change the -RequiredVersion value to 1.2.11.
  Install-Module -Name AzureStack -RequiredVersion 1.4.0 

  ```

  <span data-ttu-id="8774f-117">If the installation is successful, the AzureRM and AzureStack modules are displayed in the output.</span><span class="sxs-lookup"><span data-stu-id="8774f-117">If the installation is successful, the AzureRM and AzureStack modules are displayed in the output.</span></span>

- <span data-ttu-id="8774f-118">**Without an internet connection** from the ASDK host computer.</span><span class="sxs-lookup"><span data-stu-id="8774f-118">**Without an internet connection** from the ASDK host computer.</span></span> <span data-ttu-id="8774f-119">In a disconnected scenario, you must first download the PowerShell modules to a machine that has internet connectivity using the following PowerShell commands:</span><span class="sxs-lookup"><span data-stu-id="8774f-119">In a disconnected scenario, you must first download the PowerShell modules to a machine that has internet connectivity using the following PowerShell commands:</span></span>

  ```PowerShell
  $Path = "<Path that is used to save the packages>"

  Save-Package `
    -ProviderName NuGet `
    -Source https://www.powershellgallery.com/api/v2 `
    -Name AzureRM `
    -Path $Path `
    -Force `
    -RequiredVersion 1.2.11

  Save-Package `
    -ProviderName NuGet `
    -Source https://www.powershellgallery.com/api/v2 `
    -Name AzureStack `
    -Path $Path `
    -Force `
  # Install Azure Stack Module Version 1.4.0. If running a pre-1804 version of Azure Stack, change the -RequiredVersion value to 1.2.11.  
    -RequiredVersion 1.4.0
  ```

  <span data-ttu-id="8774f-120">Next, copy the downloaded packages to the ASDK computer and register the location as the default repository and install the AzureRM and AzureStack modules from this repository:</span><span class="sxs-lookup"><span data-stu-id="8774f-120">Next, copy the downloaded packages to the ASDK computer and register the location as the default repository and install the AzureRM and AzureStack modules from this repository:</span></span>

    ```PowerShell  
    $SourceLocation = "<Location on the development kit that contains the PowerShell packages>"
    $RepoName = "MyNuGetSource"

    Register-PSRepository `
      -Name $RepoName `
      -SourceLocation $SourceLocation `
      -InstallationPolicy Trusted

    Install-Module AzureRM `
      -Repository $RepoName

    Install-Module AzureStack `
      -Repository $RepoName
    ```

## <a name="download-the-azure-stack-tools"></a><span data-ttu-id="8774f-121">Download the Azure Stack tools</span><span class="sxs-lookup"><span data-stu-id="8774f-121">Download the Azure Stack tools</span></span>

<span data-ttu-id="8774f-122">[AzureStack-Tools](https://github.com/Azure/AzureStack-Tools) is a GitHub repository that hosts PowerShell modules for managing and deploying resources to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8774f-122">[AzureStack-Tools](https://github.com/Azure/AzureStack-Tools) is a GitHub repository that hosts PowerShell modules for managing and deploying resources to Azure Stack.</span></span> <span data-ttu-id="8774f-123">To obtain these tools, clone the GitHub repository or download the AzureStack-Tools folder by running the following script:</span><span class="sxs-lookup"><span data-stu-id="8774f-123">To obtain these tools, clone the GitHub repository or download the AzureStack-Tools folder by running the following script:</span></span>

  ```PowerShell
  # Change directory to the root directory. 
  cd \

  # Enforce usage of TLSv1.2 to download the Azure Stack tools archive from GitHub
  [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
  invoke-webrequest `
    https://github.com/Azure/AzureStack-Tools/archive/master.zip `
    -OutFile master.zip

  # Expand the downloaded files.
  expand-archive master.zip `
    -DestinationPath . `
    -Force

  # Change to the tools directory.
  cd AzureStack-Tools-master
  ```

## <a name="validate-the-asdk-installation"></a><span data-ttu-id="8774f-124">Validate the ASDK installation</span><span class="sxs-lookup"><span data-stu-id="8774f-124">Validate the ASDK installation</span></span>
<span data-ttu-id="8774f-125">To ensure that your ASDK deployment was successful, you can use the Test-AzureStack cmdlet by following these steps:</span><span class="sxs-lookup"><span data-stu-id="8774f-125">To ensure that your ASDK deployment was successful, you can use the Test-AzureStack cmdlet by following these steps:</span></span>

1. <span data-ttu-id="8774f-126">Log in as AzureStack\AzureStackAdmin on the ASDK host computer.</span><span class="sxs-lookup"><span data-stu-id="8774f-126">Log in as AzureStack\AzureStackAdmin on the ASDK host computer.</span></span>
2. <span data-ttu-id="8774f-127">Open PowerShell as an administrator (not PowerShell ISE).</span><span class="sxs-lookup"><span data-stu-id="8774f-127">Open PowerShell as an administrator (not PowerShell ISE).</span></span>
3. <span data-ttu-id="8774f-128">Run: `Enter-PSSession -ComputerName AzS-ERCS01 -ConfigurationName PrivilegedEndpoint`</span><span class="sxs-lookup"><span data-stu-id="8774f-128">Run: `Enter-PSSession -ComputerName AzS-ERCS01 -ConfigurationName PrivilegedEndpoint`</span></span>
4. <span data-ttu-id="8774f-129">Run: `Test-AzureStack`</span><span class="sxs-lookup"><span data-stu-id="8774f-129">Run: `Test-AzureStack`</span></span>

<span data-ttu-id="8774f-130">The tests take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="8774f-130">The tests take a few minutes to complete.</span></span> <span data-ttu-id="8774f-131">If the installation was successful, the output looks something like:</span><span class="sxs-lookup"><span data-stu-id="8774f-131">If the installation was successful, the output looks something like:</span></span>

![test-azurestack](media/asdk-post-deploy/test-azurestack.png)

<span data-ttu-id="8774f-133">If there was a failure, follow the troubleshooting steps to get help.</span><span class="sxs-lookup"><span data-stu-id="8774f-133">If there was a failure, follow the troubleshooting steps to get help.</span></span>

## <a name="reset-the-password-expiration-policy"></a><span data-ttu-id="8774f-134">Reset the password expiration policy</span><span class="sxs-lookup"><span data-stu-id="8774f-134">Reset the password expiration policy</span></span> 
<span data-ttu-id="8774f-135">To make sure that the password for the development kit host doesn't expire before your evaluation period ends, follow these steps after you deploy the ASDK.</span><span class="sxs-lookup"><span data-stu-id="8774f-135">To make sure that the password for the development kit host doesn't expire before your evaluation period ends, follow these steps after you deploy the ASDK.</span></span>

### <a name="to-change-the-password-expiration-policy-from-powershell"></a><span data-ttu-id="8774f-136">To change the password expiration policy from Powershell:</span><span class="sxs-lookup"><span data-stu-id="8774f-136">To change the password expiration policy from Powershell:</span></span>
<span data-ttu-id="8774f-137">From an elevated Powershell console, run the command:</span><span class="sxs-lookup"><span data-stu-id="8774f-137">From an elevated Powershell console, run the command:</span></span>

```powershell
Set-ADDefaultDomainPasswordPolicy -MaxPasswordAge 180.00:00:00 -Identity azurestack.local
```

### <a name="to-change-the-password-expiration-policy-manually"></a><span data-ttu-id="8774f-138">To change the password expiration policy manually:</span><span class="sxs-lookup"><span data-stu-id="8774f-138">To change the password expiration policy manually:</span></span>
1. <span data-ttu-id="8774f-139">On the development kit host, open **Group Policy Management** (GPMC.MMC) and navigate to **Group Policy Management** – **Forest: azurestack.local** – **Domains** – **azurestack.local**.</span><span class="sxs-lookup"><span data-stu-id="8774f-139">On the development kit host, open **Group Policy Management** (GPMC.MMC) and navigate to **Group Policy Management** – **Forest: azurestack.local** – **Domains** – **azurestack.local**.</span></span>
2. <span data-ttu-id="8774f-140">Right-click **Default Domain Policy** and click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="8774f-140">Right-click **Default Domain Policy** and click **Edit**.</span></span>
3. <span data-ttu-id="8774f-141">In the Group Policy Management Editor, navigate to **Computer Configuration** – **Policies** – **Windows Settings** – **Security Settings** – **Account Policies** – **Password Policy**.</span><span class="sxs-lookup"><span data-stu-id="8774f-141">In the Group Policy Management Editor, navigate to **Computer Configuration** – **Policies** – **Windows Settings** – **Security Settings** – **Account Policies** – **Password Policy**.</span></span>
4. <span data-ttu-id="8774f-142">In the right pane, double-click **Maximum password age**.</span><span class="sxs-lookup"><span data-stu-id="8774f-142">In the right pane, double-click **Maximum password age**.</span></span>
5. <span data-ttu-id="8774f-143">In the **Maximum password age Properties** dialog box, change the **Password will expire in** value to **180**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8774f-143">In the **Maximum password age Properties** dialog box, change the **Password will expire in** value to **180**, and then click **OK**.</span></span>

![Group policy management console](media/asdk-post-deploy/gpmc.png)

## <a name="enable-multi-tenancy"></a><span data-ttu-id="8774f-145">Enable multi-tenancy</span><span class="sxs-lookup"><span data-stu-id="8774f-145">Enable multi-tenancy</span></span>
<span data-ttu-id="8774f-146">For deployments using Azure AD, you need to [enable multi-tenancy](.\.\azure-stack-enable-multitenancy.md#enable-multi-tenancy) for your ASDK installation.</span><span class="sxs-lookup"><span data-stu-id="8774f-146">For deployments using Azure AD, you need to [enable multi-tenancy](.\.\azure-stack-enable-multitenancy.md#enable-multi-tenancy) for your ASDK installation.</span></span>

> [!NOTE]
> <span data-ttu-id="8774f-147">When administrator or user accounts from domains other than the one used to register Azure Stack are used to log in to an Azure Stack portal, the domain name used to register Azure Stack must be appended to the portal url.</span><span class="sxs-lookup"><span data-stu-id="8774f-147">When administrator or user accounts from domains other than the one used to register Azure Stack are used to log in to an Azure Stack portal, the domain name used to register Azure Stack must be appended to the portal url.</span></span> <span data-ttu-id="8774f-148">For example, if Azure Stack has been registered with fabrikam.onmicrosoft.com and the user account logging in is admin@contoso.com, the url to use to log into the user portal would be: https://portal.local.azurestack.external/fabrikam.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="8774f-148">For example, if Azure Stack has been registered with fabrikam.onmicrosoft.com and the user account logging in is admin@contoso.com, the url to use to log into the user portal would be: https://portal.local.azurestack.external/fabrikam.onmicrosoft.com.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8774f-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="8774f-149">Next steps</span></span>
[<span data-ttu-id="8774f-150">Register the ASDK with Azure</span><span class="sxs-lookup"><span data-stu-id="8774f-150">Register the ASDK with Azure</span></span>](asdk-register.md)
