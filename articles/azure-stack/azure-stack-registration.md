---
title: Azure registration for Azure Stack integrated systems | Microsoft Docs
description: Describes the Azure registration process for multi-node Azure Stack Azure-connected deployments.
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
ms.date: 09/05/2018
ms.author: jeffgilb
ms.reviewer: brbartle
ms.openlocfilehash: 52d0706177482e162d1f4bc038c967a4596fd3b3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865244"
---
# <a name="register-azure-stack-with-azure"></a><span data-ttu-id="5cd78-103">Register Azure Stack with Azure</span><span class="sxs-lookup"><span data-stu-id="5cd78-103">Register Azure Stack with Azure</span></span>

<span data-ttu-id="5cd78-104">Registering Azure Stack with Azure allows you to download marketplace items from Azure and to set up commerce data reporting back to Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5cd78-104">Registering Azure Stack with Azure allows you to download marketplace items from Azure and to set up commerce data reporting back to Microsoft.</span></span> <span data-ttu-id="5cd78-105">After you register Azure Stack, usage is reported to Azure commerce and you can see it under the subscription used for registration.</span><span class="sxs-lookup"><span data-stu-id="5cd78-105">After you register Azure Stack, usage is reported to Azure commerce and you can see it under the subscription used for registration.</span></span>

<span data-ttu-id="5cd78-106">The information in this article describes registering Azure Stack integrated systems with Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd78-106">The information in this article describes registering Azure Stack integrated systems with Azure.</span></span> <span data-ttu-id="5cd78-107">For information about registering the ASDK with Azure, see [Azure Stack registration](.\asdk\asdk-register.md) in the ASDK documentation.</span><span class="sxs-lookup"><span data-stu-id="5cd78-107">For information about registering the ASDK with Azure, see [Azure Stack registration](.\asdk\asdk-register.md) in the ASDK documentation.</span></span>

> [!IMPORTANT]  
> <span data-ttu-id="5cd78-108">Registration is required to support full Azure Stack functionality, including offering items in the marketplace.</span><span class="sxs-lookup"><span data-stu-id="5cd78-108">Registration is required to support full Azure Stack functionality, including offering items in the marketplace.</span></span> <span data-ttu-id="5cd78-109">In addition, you will be in violation of Azure Stack licensing terms if you do not register when using the pay-as-you-use billing model.</span><span class="sxs-lookup"><span data-stu-id="5cd78-109">In addition, you will be in violation of Azure Stack licensing terms if you do not register when using the pay-as-you-use billing model.</span></span> <span data-ttu-id="5cd78-110">To learn more about Azure Stack licensing models, please see the [How to buy page](https://azure.microsoft.com/overview/azure-stack/how-to-buy/).</span><span class="sxs-lookup"><span data-stu-id="5cd78-110">To learn more about Azure Stack licensing models, please see the [How to buy page](https://azure.microsoft.com/overview/azure-stack/how-to-buy/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5cd78-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5cd78-111">Prerequisites</span></span>

<span data-ttu-id="5cd78-112">You will need the following in place before you register:</span><span class="sxs-lookup"><span data-stu-id="5cd78-112">You will need the following in place before you register:</span></span>

 - <span data-ttu-id="5cd78-113">Verify your credentials</span><span class="sxs-lookup"><span data-stu-id="5cd78-113">Verify your credentials</span></span>
 - <span data-ttu-id="5cd78-114">Set the PowerShell language mode</span><span class="sxs-lookup"><span data-stu-id="5cd78-114">Set the PowerShell language mode</span></span>
 - <span data-ttu-id="5cd78-115">Install PowerShell for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5cd78-115">Install PowerShell for Azure Stack</span></span>
 - <span data-ttu-id="5cd78-116">Download the Azure Stack tools</span><span class="sxs-lookup"><span data-stu-id="5cd78-116">Download the Azure Stack tools</span></span>
 - <span data-ttu-id="5cd78-117">Determine your registration scenario</span><span class="sxs-lookup"><span data-stu-id="5cd78-117">Determine your registration scenario</span></span>

### <a name="verify-your-credentials"></a><span data-ttu-id="5cd78-118">Verify your credentials</span><span class="sxs-lookup"><span data-stu-id="5cd78-118">Verify your credentials</span></span>

<span data-ttu-id="5cd78-119">Before registering Azure Stack with Azure, you must have:</span><span class="sxs-lookup"><span data-stu-id="5cd78-119">Before registering Azure Stack with Azure, you must have:</span></span>

- <span data-ttu-id="5cd78-120">The subscription ID for an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5cd78-120">The subscription ID for an Azure subscription.</span></span> <span data-ttu-id="5cd78-121">To get the ID, sign in to Azure, click **All services**.</span><span class="sxs-lookup"><span data-stu-id="5cd78-121">To get the ID, sign in to Azure, click **All services**.</span></span> <span data-ttu-id="5cd78-122">Then, under the **GENERAL** category, select **Subscriptions**, click the subscription you want to use, and under **Essentials** you can find the Subscription ID.</span><span class="sxs-lookup"><span data-stu-id="5cd78-122">Then, under the **GENERAL** category, select **Subscriptions**, click the subscription you want to use, and under **Essentials** you can find the Subscription ID.</span></span>

  > [!Note]  
  > <span data-ttu-id="5cd78-123">Germany cloud subscriptions are not currently supported.</span><span class="sxs-lookup"><span data-stu-id="5cd78-123">Germany cloud subscriptions are not currently supported.</span></span>

- <span data-ttu-id="5cd78-124">The username and password for an account that is an owner for the subscription (MSA/2FA accounts are supported).</span><span class="sxs-lookup"><span data-stu-id="5cd78-124">The username and password for an account that is an owner for the subscription (MSA/2FA accounts are supported).</span></span>

- <span data-ttu-id="5cd78-125">The user account needs to be an Admin in the Azure AD tenant to which Azure Stack is registered, for example, `yourazurestacktenant.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="5cd78-125">The user account needs to be an Admin in the Azure AD tenant to which Azure Stack is registered, for example, `yourazurestacktenant.onmicrosoft.com`.</span></span>

- <span data-ttu-id="5cd78-126">Registered the Azure Stack resource provider (see the Register Azure Stack Resource Provider section below for details).</span><span class="sxs-lookup"><span data-stu-id="5cd78-126">Registered the Azure Stack resource provider (see the Register Azure Stack Resource Provider section below for details).</span></span>

  <span data-ttu-id="5cd78-127">If you don’t have an Azure subscription that meets these requirements, you can [create a free Azure account here](https://azure.microsoft.com/free/?b=17.06).</span><span class="sxs-lookup"><span data-stu-id="5cd78-127">If you don’t have an Azure subscription that meets these requirements, you can [create a free Azure account here](https://azure.microsoft.com/free/?b=17.06).</span></span> <span data-ttu-id="5cd78-128">Registering Azure Stack incurs no cost on your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5cd78-128">Registering Azure Stack incurs no cost on your Azure subscription.</span></span>

### <a name="powershell-language-mode"></a><span data-ttu-id="5cd78-129">PowerShell language mode</span><span class="sxs-lookup"><span data-stu-id="5cd78-129">PowerShell language mode</span></span>

<span data-ttu-id="5cd78-130">To successfully register Azure Stack, the PowerShell language mode must be set to **FullLanguageMode**.</span><span class="sxs-lookup"><span data-stu-id="5cd78-130">To successfully register Azure Stack, the PowerShell language mode must be set to **FullLanguageMode**.</span></span>  <span data-ttu-id="5cd78-131">To verify that the current language mode is set to full, open an elevated PowerShell window and run the following PowerShell cmdlets:</span><span class="sxs-lookup"><span data-stu-id="5cd78-131">To verify that the current language mode is set to full, open an elevated PowerShell window and run the following PowerShell cmdlets:</span></span>

```PowerShell  
$ExecutionContext.SessionState.LanguageMode
```

<span data-ttu-id="5cd78-132">Ensure the output returns **FullLanguageMode**.</span><span class="sxs-lookup"><span data-stu-id="5cd78-132">Ensure the output returns **FullLanguageMode**.</span></span> <span data-ttu-id="5cd78-133">If any other language mode is returned, registration will need to be run on another machine or the language mode will need to be set to **FullLanguageMode** before continuing.</span><span class="sxs-lookup"><span data-stu-id="5cd78-133">If any other language mode is returned, registration will need to be run on another machine or the language mode will need to be set to **FullLanguageMode** before continuing.</span></span>

### <a name="install-powershell-for-azure-stack"></a><span data-ttu-id="5cd78-134">Install PowerShell for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5cd78-134">Install PowerShell for Azure Stack</span></span>

<span data-ttu-id="5cd78-135">You need to use the latest PowerShell for Azure Stack to register with Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd78-135">You need to use the latest PowerShell for Azure Stack to register with Azure.</span></span>

<span data-ttu-id="5cd78-136">If not the latest version is not already installed, see [install PowerShell for Azure Stack](https://docs.microsoft.com/azure/azure-stack/azure-stack-powershell-install).</span><span class="sxs-lookup"><span data-stu-id="5cd78-136">If not the latest version is not already installed, see [install PowerShell for Azure Stack](https://docs.microsoft.com/azure/azure-stack/azure-stack-powershell-install).</span></span>

### <a name="download-the-azure-stack-tools"></a><span data-ttu-id="5cd78-137">Download the Azure Stack tools</span><span class="sxs-lookup"><span data-stu-id="5cd78-137">Download the Azure Stack tools</span></span>

<span data-ttu-id="5cd78-138">The Azure Stack tools GitHub repository contains PowerShell modules that support Azure Stack functionality; including registration functionality.</span><span class="sxs-lookup"><span data-stu-id="5cd78-138">The Azure Stack tools GitHub repository contains PowerShell modules that support Azure Stack functionality; including registration functionality.</span></span> <span data-ttu-id="5cd78-139">During the registration process, you need to import and use the **RegisterWithAzure.psm1** PowerShell module, found in the Azure Stack tools repository, to register your Azure Stack instance with Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd78-139">During the registration process, you need to import and use the **RegisterWithAzure.psm1** PowerShell module, found in the Azure Stack tools repository, to register your Azure Stack instance with Azure.</span></span>

<span data-ttu-id="5cd78-140">To ensure you are using the latest version, you should delete any existing versions of the Azure Stack tools and [download the latest version from GitHub](azure-stack-powershell-download.md) before registering with Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd78-140">To ensure you are using the latest version, you should delete any existing versions of the Azure Stack tools and [download the latest version from GitHub](azure-stack-powershell-download.md) before registering with Azure.</span></span>

### <a name="determine-your-registration-scenario"></a><span data-ttu-id="5cd78-141">Determine your registration scenario</span><span class="sxs-lookup"><span data-stu-id="5cd78-141">Determine your registration scenario</span></span>

<span data-ttu-id="5cd78-142">Your Azure Stack deployment may be *connected* or *disconnected*.</span><span class="sxs-lookup"><span data-stu-id="5cd78-142">Your Azure Stack deployment may be *connected* or *disconnected*.</span></span>

 - <span data-ttu-id="5cd78-143">**Connected**</span><span class="sxs-lookup"><span data-stu-id="5cd78-143">**Connected**</span></span>  
 <span data-ttu-id="5cd78-144">Connected means you have deployed Azure Stack so that it can connect to the Internet and to Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd78-144">Connected means you have deployed Azure Stack so that it can connect to the Internet and to Azure.</span></span> <span data-ttu-id="5cd78-145">You either have Azure Active Directory (Azure AD) or Active Directory Federation Services (AD FS) for your identity store.</span><span class="sxs-lookup"><span data-stu-id="5cd78-145">You either have Azure Active Directory (Azure AD) or Active Directory Federation Services (AD FS) for your identity store.</span></span> <span data-ttu-id="5cd78-146">With a connected deployment, you can choose from two billing models: pay-as-you-use or capacity-based.</span><span class="sxs-lookup"><span data-stu-id="5cd78-146">With a connected deployment, you can choose from two billing models: pay-as-you-use or capacity-based.</span></span>
    - [<span data-ttu-id="5cd78-147">Register a connected Azure Stack with Azure using the **pay-as-you-use** billing model</span><span class="sxs-lookup"><span data-stu-id="5cd78-147">Register a connected Azure Stack with Azure using the **pay-as-you-use** billing model</span></span>](#register-connected-with-pay-as-you-go-billing)
    - [<span data-ttu-id="5cd78-148">Register a connected Azure Stack with Azure using the **capacity** billing model</span><span class="sxs-lookup"><span data-stu-id="5cd78-148">Register a connected Azure Stack with Azure using the **capacity** billing model</span></span>](#register-connected-with-capacity-billing)

 - <span data-ttu-id="5cd78-149">**Disconnected**</span><span class="sxs-lookup"><span data-stu-id="5cd78-149">**Disconnected**</span></span>  
 <span data-ttu-id="5cd78-150">With the disconnected from Azure deployment option, you can deploy and use Azure Stack without a connection to the Internet.</span><span class="sxs-lookup"><span data-stu-id="5cd78-150">With the disconnected from Azure deployment option, you can deploy and use Azure Stack without a connection to the Internet.</span></span> <span data-ttu-id="5cd78-151">However, with a disconnected deployment, you are limited to an AD FS identity store and the capacity-based billing model.</span><span class="sxs-lookup"><span data-stu-id="5cd78-151">However, with a disconnected deployment, you are limited to an AD FS identity store and the capacity-based billing model.</span></span>
    - [<span data-ttu-id="5cd78-152">Register a disconnected Azure Stack using the **capacity** billing model </span><span class="sxs-lookup"><span data-stu-id="5cd78-152">Register a disconnected Azure Stack using the **capacity** billing model </span></span>](#register-disconnected-with-capacity-billing)

## <a name="register-connected-with-pay-as-you-go-billing"></a><span data-ttu-id="5cd78-153">Register connected with pay-as-you-go billing</span><span class="sxs-lookup"><span data-stu-id="5cd78-153">Register connected with pay-as-you-go billing</span></span>

<span data-ttu-id="5cd78-154">Use these steps to register Azure Stack with Azure using the pay-as-you-use billing model.</span><span class="sxs-lookup"><span data-stu-id="5cd78-154">Use these steps to register Azure Stack with Azure using the pay-as-you-use billing model.</span></span>

> [!Note]  
> <span data-ttu-id="5cd78-155">All these steps must be run from a computer that has access to the privileged endpoint (PEP).</span><span class="sxs-lookup"><span data-stu-id="5cd78-155">All these steps must be run from a computer that has access to the privileged endpoint (PEP).</span></span> <span data-ttu-id="5cd78-156">For details about the PEP, see [Using the privileged endpoint in Azure Stack](azure-stack-privileged-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="5cd78-156">For details about the PEP, see [Using the privileged endpoint in Azure Stack](azure-stack-privileged-endpoint.md).</span></span>

<span data-ttu-id="5cd78-157">Connected environments can access the internet and Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd78-157">Connected environments can access the internet and Azure.</span></span> <span data-ttu-id="5cd78-158">For these environments, you need to register the Azure Stack resource provider with Azure and then configure your billing model.</span><span class="sxs-lookup"><span data-stu-id="5cd78-158">For these environments, you need to register the Azure Stack resource provider with Azure and then configure your billing model.</span></span>

1. <span data-ttu-id="5cd78-159">To register the Azure Stack resource provider with Azure, start PowerShell ISE as an administrator and use the following PowerShell cmdlets with the **EnvironmentName** parameter set to the appropriate Azure subscription type (see parameters below).</span><span class="sxs-lookup"><span data-stu-id="5cd78-159">To register the Azure Stack resource provider with Azure, start PowerShell ISE as an administrator and use the following PowerShell cmdlets with the **EnvironmentName** parameter set to the appropriate Azure subscription type (see parameters below).</span></span>

2. <span data-ttu-id="5cd78-160">Add the Azure account that you use to register Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5cd78-160">Add the Azure account that you use to register Azure Stack.</span></span> <span data-ttu-id="5cd78-161">To add the account, run the **Add-AzureRmAccount** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5cd78-161">To add the account, run the **Add-AzureRmAccount** cmdlet.</span></span> <span data-ttu-id="5cd78-162">You are prompted to enter your Azure global administrator account credentials and you may have to use 2-factor authentication based on your account’s configuration.</span><span class="sxs-lookup"><span data-stu-id="5cd78-162">You are prompted to enter your Azure global administrator account credentials and you may have to use 2-factor authentication based on your account’s configuration.</span></span>

   ```PowerShell  
      Add-AzureRmAccount -EnvironmentName "<AzureCloud, AzureChinaCloud, or AzureUSGovernment>"
   ```

   | <span data-ttu-id="5cd78-163">Parameter</span><span class="sxs-lookup"><span data-stu-id="5cd78-163">Parameter</span></span> | <span data-ttu-id="5cd78-164">Description</span><span class="sxs-lookup"><span data-stu-id="5cd78-164">Description</span></span> |  
   |-----|-----|
   | <span data-ttu-id="5cd78-165">EnvironmentName</span><span class="sxs-lookup"><span data-stu-id="5cd78-165">EnvironmentName</span></span> | <span data-ttu-id="5cd78-166">The Azure cloud subscription environment name.</span><span class="sxs-lookup"><span data-stu-id="5cd78-166">The Azure cloud subscription environment name.</span></span> <span data-ttu-id="5cd78-167">Supported environment names are **AzureCloud**, **AzureUSGovernment**, or if using a China Azure Subscription, **AzureChinaCloud**.</span><span class="sxs-lookup"><span data-stu-id="5cd78-167">Supported environment names are **AzureCloud**, **AzureUSGovernment**, or if using a China Azure Subscription, **AzureChinaCloud**.</span></span>  |

3. <span data-ttu-id="5cd78-168">If you have multiple subscriptions, run the following command to select the one you want to use:</span><span class="sxs-lookup"><span data-stu-id="5cd78-168">If you have multiple subscriptions, run the following command to select the one you want to use:</span></span>  

   ```PowerShell  
      Get-AzureRmSubscription -SubscriptionID '<Your Azure Subscription GUID>' | Select-AzureRmSubscription
   ```

4. <span data-ttu-id="5cd78-169">Run the following command to register the Azure Stack resource provider in your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="5cd78-169">Run the following command to register the Azure Stack resource provider in your Azure subscription:</span></span>

   ```PowerShell  
   Register-AzureRmResourceProvider -ProviderNamespace Microsoft.AzureStack
   ```

5. <span data-ttu-id="5cd78-170">Start PowerShell ISE as an administrator and navigate to the **Registration** folder in the **AzureStack-Tools-master** directory created when you [downloaded the Azure Stack tools](#bkmk_tools).</span><span class="sxs-lookup"><span data-stu-id="5cd78-170">Start PowerShell ISE as an administrator and navigate to the **Registration** folder in the **AzureStack-Tools-master** directory created when you [downloaded the Azure Stack tools](#bkmk_tools).</span></span> <span data-ttu-id="5cd78-171">Import the **RegisterWithAzure.psm1** module using PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5cd78-171">Import the **RegisterWithAzure.psm1** module using PowerShell:</span></span>

   ```PowerShell  
   Import-Module .\RegisterWithAzure.psm1
   ```

6. <span data-ttu-id="5cd78-172">Next, in the same PowerShell session, ensure you are logged in to the correct Azure PowerShell Context.</span><span class="sxs-lookup"><span data-stu-id="5cd78-172">Next, in the same PowerShell session, ensure you are logged in to the correct Azure PowerShell Context.</span></span> <span data-ttu-id="5cd78-173">This is the azure account that was used to register the Azure Stack resource provider above.</span><span class="sxs-lookup"><span data-stu-id="5cd78-173">This is the azure account that was used to register the Azure Stack resource provider above.</span></span> <span data-ttu-id="5cd78-174">Powershell to run:</span><span class="sxs-lookup"><span data-stu-id="5cd78-174">Powershell to run:</span></span>

   ```PowerShell  
   Add-AzureRmAccount -Environment "<AzureCloud, AzureChinaCloud, or AzureUSGovernment>"
   ```

7. <span data-ttu-id="5cd78-175">In the same PowerShell session, run the **Set-AzsRegistration** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5cd78-175">In the same PowerShell session, run the **Set-AzsRegistration** cmdlet.</span></span> <span data-ttu-id="5cd78-176">PowerShell to run:</span><span class="sxs-lookup"><span data-stu-id="5cd78-176">PowerShell to run:</span></span>  

   ```PowerShell  
   $CloudAdminCred = Get-Credential -UserName <Privileged endpoint credentials> -Message "Enter the cloud domain credentials to access the privileged endpoint."
   $RegistrationName = "<unique-registration-name>"
   Set-AzsRegistration `
      -PrivilegedEndpointCredential $CloudAdminCred `
      -PrivilegedEndpoint <PrivilegedEndPoint computer name> `
      -BillingModel PayAsYouUse `
      -RegistrationName $RegistrationName
   ```
   <span data-ttu-id="5cd78-177">For more information on the Set-AzsRegistration cmdlet, see [Registration reference](#registration-reference).</span><span class="sxs-lookup"><span data-stu-id="5cd78-177">For more information on the Set-AzsRegistration cmdlet, see [Registration reference](#registration-reference).</span></span>

  <span data-ttu-id="5cd78-178">The process will take between 10 and 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="5cd78-178">The process will take between 10 and 15 minutes.</span></span> <span data-ttu-id="5cd78-179">When the command completes, you will see the message **"Your environment is now registered and activated using the provided parameters."**</span><span class="sxs-lookup"><span data-stu-id="5cd78-179">When the command completes, you will see the message **"Your environment is now registered and activated using the provided parameters."**</span></span>

## <a name="register-connected-with-capacity-billing"></a><span data-ttu-id="5cd78-180">Register connected with capacity billing</span><span class="sxs-lookup"><span data-stu-id="5cd78-180">Register connected with capacity billing</span></span>

<span data-ttu-id="5cd78-181">Use these steps to register Azure Stack with Azure using the pay-as-you-use billing model.</span><span class="sxs-lookup"><span data-stu-id="5cd78-181">Use these steps to register Azure Stack with Azure using the pay-as-you-use billing model.</span></span>

> [!Note]  
> <span data-ttu-id="5cd78-182">All these steps must be run from a computer that has access to the privileged endpoint (PEP).</span><span class="sxs-lookup"><span data-stu-id="5cd78-182">All these steps must be run from a computer that has access to the privileged endpoint (PEP).</span></span> <span data-ttu-id="5cd78-183">For details about the PEP, see [Using the privileged endpoint in Azure Stack](azure-stack-privileged-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="5cd78-183">For details about the PEP, see [Using the privileged endpoint in Azure Stack](azure-stack-privileged-endpoint.md).</span></span>

<span data-ttu-id="5cd78-184">Connected environments can access the internet and Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd78-184">Connected environments can access the internet and Azure.</span></span> <span data-ttu-id="5cd78-185">For these environments, you need to register the Azure Stack resource provider with Azure and then configure your billing model.</span><span class="sxs-lookup"><span data-stu-id="5cd78-185">For these environments, you need to register the Azure Stack resource provider with Azure and then configure your billing model.</span></span>

1. <span data-ttu-id="5cd78-186">To register the Azure Stack resource provider with Azure, start PowerShell ISE as an administrator and use the following PowerShell cmdlets with the **EnvironmentName** parameter set to the appropriate Azure subscription type (see parameters below).</span><span class="sxs-lookup"><span data-stu-id="5cd78-186">To register the Azure Stack resource provider with Azure, start PowerShell ISE as an administrator and use the following PowerShell cmdlets with the **EnvironmentName** parameter set to the appropriate Azure subscription type (see parameters below).</span></span>

2. <span data-ttu-id="5cd78-187">Add the Azure account that you use to register Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5cd78-187">Add the Azure account that you use to register Azure Stack.</span></span> <span data-ttu-id="5cd78-188">To add the account, run the **Add-AzureRmAccount** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5cd78-188">To add the account, run the **Add-AzureRmAccount** cmdlet.</span></span> <span data-ttu-id="5cd78-189">You are prompted to enter your Azure global administrator account credentials and you may have to use 2-factor authentication based on your account’s configuration.</span><span class="sxs-lookup"><span data-stu-id="5cd78-189">You are prompted to enter your Azure global administrator account credentials and you may have to use 2-factor authentication based on your account’s configuration.</span></span>

   ```PowerShell  
      Add-AzureRmAccount -EnvironmentName "<AzureCloud, AzureChinaCloud, or AzureUSGovernment>"
   ```

   | <span data-ttu-id="5cd78-190">Parameter</span><span class="sxs-lookup"><span data-stu-id="5cd78-190">Parameter</span></span> | <span data-ttu-id="5cd78-191">Description</span><span class="sxs-lookup"><span data-stu-id="5cd78-191">Description</span></span> |  
   |-----|-----|
   | <span data-ttu-id="5cd78-192">EnvironmentName</span><span class="sxs-lookup"><span data-stu-id="5cd78-192">EnvironmentName</span></span> | <span data-ttu-id="5cd78-193">The Azure cloud subscription environment name.</span><span class="sxs-lookup"><span data-stu-id="5cd78-193">The Azure cloud subscription environment name.</span></span> <span data-ttu-id="5cd78-194">Supported environment names are **AzureCloud**, **AzureUSGovernment**, or if using a China Azure Subscription, **AzureChinaCloud**.</span><span class="sxs-lookup"><span data-stu-id="5cd78-194">Supported environment names are **AzureCloud**, **AzureUSGovernment**, or if using a China Azure Subscription, **AzureChinaCloud**.</span></span>  |

3. <span data-ttu-id="5cd78-195">If you have multiple subscriptions, run the following command to select the one you want to use:</span><span class="sxs-lookup"><span data-stu-id="5cd78-195">If you have multiple subscriptions, run the following command to select the one you want to use:</span></span>  

   ```PowerShell  
      Get-AzureRmSubscription -SubscriptionID '<Your Azure Subscription GUID>' | Select-AzureRmSubscription
   ```

4. <span data-ttu-id="5cd78-196">Run the following command to register the Azure Stack resource provider in your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="5cd78-196">Run the following command to register the Azure Stack resource provider in your Azure subscription:</span></span>

   ```PowerShell  
   Register-AzureRmResourceProvider -ProviderNamespace Microsoft.AzureStack
   ```

5. <span data-ttu-id="5cd78-197">Start PowerShell ISE as an administrator and navigate to the **Registration** folder in the **AzureStack-Tools-master** directory created when you [downloaded the Azure Stack tools](#bkmk_tools).</span><span class="sxs-lookup"><span data-stu-id="5cd78-197">Start PowerShell ISE as an administrator and navigate to the **Registration** folder in the **AzureStack-Tools-master** directory created when you [downloaded the Azure Stack tools](#bkmk_tools).</span></span> <span data-ttu-id="5cd78-198">Import the **RegisterWithAzure.psm1** module using PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5cd78-198">Import the **RegisterWithAzure.psm1** module using PowerShell:</span></span>

  ```PowerShell  
  $CloudAdminCred = Get-Credential -UserName <Privileged endpoint credentials> -Message "Enter the cloud domain credentials to access the privileged endpoint."
  $RegistrationName = "<unique-registration-name>"
  Set-AzsRegistration `
      -PrivilegedEndpointCredential $CloudAdminCred `
      -PrivilegedEndpoint <PrivilegedEndPoint computer name> `
      -AgreementNumber <EA agreement number> `
      -BillingModel Capacity
      -RegistrationName $RegistrationName
  ```
   > [!Note]  
   > <span data-ttu-id="5cd78-199">You can disable usage reporting with the UsageReportingEnabled parameter for the **Set-AzsRegistration** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5cd78-199">You can disable usage reporting with the UsageReportingEnabled parameter for the **Set-AzsRegistration** cmdlet.</span></span> <span data-ttu-id="5cd78-200">Set the parameter to false.</span><span class="sxs-lookup"><span data-stu-id="5cd78-200">Set the parameter to false.</span></span> <span data-ttu-id="5cd78-201">For example: \`UsageReportingEnabled</span><span class="sxs-lookup"><span data-stu-id="5cd78-201">For example: \`UsageReportingEnabled</span></span>
   
  <span data-ttu-id="5cd78-202">For more information on the Set-AzsRegistration cmdlet, see [Registration reference](#registration-reference).</span><span class="sxs-lookup"><span data-stu-id="5cd78-202">For more information on the Set-AzsRegistration cmdlet, see [Registration reference](#registration-reference).</span></span>

## <a name="register-disconnected-with-capacity-billing"></a><span data-ttu-id="5cd78-203">Register disconnected with capacity billing</span><span class="sxs-lookup"><span data-stu-id="5cd78-203">Register disconnected with capacity billing</span></span>

<span data-ttu-id="5cd78-204">If you are registering Azure Stack in a disconnected environment (with no internet connectivity), you need to get a registration token from the Azure Stack environment and then use that token on a computer that can connect to Azure and has [PowerShell for Azure Stack installed](#bkmk_powershell).</span><span class="sxs-lookup"><span data-stu-id="5cd78-204">If you are registering Azure Stack in a disconnected environment (with no internet connectivity), you need to get a registration token from the Azure Stack environment and then use that token on a computer that can connect to Azure and has [PowerShell for Azure Stack installed](#bkmk_powershell).</span></span>  

### <a name="get-a-registration-token-from-the-azure-stack-environment"></a><span data-ttu-id="5cd78-205">Get a registration token from the Azure Stack environment</span><span class="sxs-lookup"><span data-stu-id="5cd78-205">Get a registration token from the Azure Stack environment</span></span>

1. <span data-ttu-id="5cd78-206">Start PowerShell ISE as an administrator and navigate to the **Registration** folder in the **AzureStack-Tools-master** directory created when you [downloaded the Azure Stack tools](#bkmk_tools).</span><span class="sxs-lookup"><span data-stu-id="5cd78-206">Start PowerShell ISE as an administrator and navigate to the **Registration** folder in the **AzureStack-Tools-master** directory created when you [downloaded the Azure Stack tools](#bkmk_tools).</span></span> <span data-ttu-id="5cd78-207">Import the **RegisterWithAzure.psm1** module:</span><span class="sxs-lookup"><span data-stu-id="5cd78-207">Import the **RegisterWithAzure.psm1** module:</span></span>  

   ```PowerShell  
   Import-Module .\RegisterWithAzure.psm1
   ```

2. <span data-ttu-id="5cd78-208">To get the registration token, run the following PowerShell cmdlets:</span><span class="sxs-lookup"><span data-stu-id="5cd78-208">To get the registration token, run the following PowerShell cmdlets:</span></span>  

   ```Powershell
   $FilePathForRegistrationToken = $env:SystemDrive\RegistrationToken.txt
   $RegistrationToken = Get-AzsRegistrationToken -PrivilegedEndpointCredential -UsageReportingEnabled:$False $YourCloudAdminCredential -PrivilegedEndpoint $YourPrivilegedEndpoint -BillingModel Capacity -AgreementNumber '<EA agreement number>' -TokenOutputFilePath $FilePathForRegistrationToken
   ```
   <span data-ttu-id="5cd78-209">For more information on the Get-AzsRegistrationToken cmdlet, see [Registration reference](#registration-reference).</span><span class="sxs-lookup"><span data-stu-id="5cd78-209">For more information on the Get-AzsRegistrationToken cmdlet, see [Registration reference](#registration-reference).</span></span>

   > [!Tip]  
   > <span data-ttu-id="5cd78-210">The registration token is saved in the file specified for *$FilePathForRegistrationToken*.</span><span class="sxs-lookup"><span data-stu-id="5cd78-210">The registration token is saved in the file specified for *$FilePathForRegistrationToken*.</span></span> <span data-ttu-id="5cd78-211">You can change the filepath or filename at your discretion.</span><span class="sxs-lookup"><span data-stu-id="5cd78-211">You can change the filepath or filename at your discretion.</span></span>

3. <span data-ttu-id="5cd78-212">Save this registration token for use on the Azure connected machine.</span><span class="sxs-lookup"><span data-stu-id="5cd78-212">Save this registration token for use on the Azure connected machine.</span></span> <span data-ttu-id="5cd78-213">You can copy the file or the text from $FilePathForRegistrationToken.</span><span class="sxs-lookup"><span data-stu-id="5cd78-213">You can copy the file or the text from $FilePathForRegistrationToken.</span></span>

### <a name="connect-to-azure-and-register"></a><span data-ttu-id="5cd78-214">Connect to Azure and register</span><span class="sxs-lookup"><span data-stu-id="5cd78-214">Connect to Azure and register</span></span>

<span data-ttu-id="5cd78-215">On the computer that is connected to the Internet, perform the same steps to import the RegisterWithAzure.psm1 module and sign in to the correct Azure Powershell context.</span><span class="sxs-lookup"><span data-stu-id="5cd78-215">On the computer that is connected to the Internet, perform the same steps to import the RegisterWithAzure.psm1 module and sign in to the correct Azure Powershell context.</span></span> <span data-ttu-id="5cd78-216">Then call Register-AzsEnvironment.</span><span class="sxs-lookup"><span data-stu-id="5cd78-216">Then call Register-AzsEnvironment.</span></span> <span data-ttu-id="5cd78-217">Specify the registration token to register with Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd78-217">Specify the registration token to register with Azure.</span></span> <span data-ttu-id="5cd78-218">If you are registering more than one instance of Azure Stack using the same Azure Subscription ID, specify a unique registration name.</span><span class="sxs-lookup"><span data-stu-id="5cd78-218">If you are registering more than one instance of Azure Stack using the same Azure Subscription ID, specify a unique registration name.</span></span> <span data-ttu-id="5cd78-219">Run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5cd78-219">Run the following cmdlet:</span></span>

  ```PowerShell  
  $registrationToken = "<Your Registration Token>"
  $RegistrationName = "<unique-registration-name>"
  Register-AzsEnvironment -RegistrationToken $registrationToken  -RegistrationName $RegistrationName
  ```

<span data-ttu-id="5cd78-220">Optionally, you can use the Get-Content cmdlet to point to a file that contains your registration token:</span><span class="sxs-lookup"><span data-stu-id="5cd78-220">Optionally, you can use the Get-Content cmdlet to point to a file that contains your registration token:</span></span>

  ```PowerShell  
  $registrationToken = Get-Content -Path '<Path>\<Registration Token File>'
  Register-AzsEnvironment -RegistrationToken $registrationToken -RegistrationName $RegistrationName
  ```

  > [!Note]  
  > <span data-ttu-id="5cd78-221">Save the registration resource name and the registration token for future reference.</span><span class="sxs-lookup"><span data-stu-id="5cd78-221">Save the registration resource name and the registration token for future reference.</span></span>

### <a name="retrieve-an-activation-key-from-azure-registration-resource"></a><span data-ttu-id="5cd78-222">Retrieve an Activation Key from Azure Registration Resource</span><span class="sxs-lookup"><span data-stu-id="5cd78-222">Retrieve an Activation Key from Azure Registration Resource</span></span>

<span data-ttu-id="5cd78-223">Next, you need to retrieve an activation key from the registration resource created in Azure during Register-AzsEnvironment.</span><span class="sxs-lookup"><span data-stu-id="5cd78-223">Next, you need to retrieve an activation key from the registration resource created in Azure during Register-AzsEnvironment.</span></span>

<span data-ttu-id="5cd78-224">To get the activation key, run the following PowerShell cmdlets:</span><span class="sxs-lookup"><span data-stu-id="5cd78-224">To get the activation key, run the following PowerShell cmdlets:</span></span>  

  ```Powershell
  $RegistrationResourceName = "AzureStack-<Cloud Id for the Environment to register>"
  $KeyOutputFilePath = "$env:SystemDrive\ActivationKey.txt"
  $ActivationKey = Get-AzsActivationKey -RegistrationName $RegistrationResourceName -KeyOutputFilePath $KeyOutputFilePath
  ```

  > [!Tip]  
  > <span data-ttu-id="5cd78-225">The activation key is saved in the file specified for *$KeyOutputFilePath*.</span><span class="sxs-lookup"><span data-stu-id="5cd78-225">The activation key is saved in the file specified for *$KeyOutputFilePath*.</span></span> <span data-ttu-id="5cd78-226">You can change the filepath or filename at your discretion.</span><span class="sxs-lookup"><span data-stu-id="5cd78-226">You can change the filepath or filename at your discretion.</span></span>

### <a name="create-an-activation-resource-in-azure-stack"></a><span data-ttu-id="5cd78-227">Create an Activation Resource in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5cd78-227">Create an Activation Resource in Azure Stack</span></span>

<span data-ttu-id="5cd78-228">Return to the Azure Stack environment with the file or text from the activation key created from Get-AzsActivationKey.</span><span class="sxs-lookup"><span data-stu-id="5cd78-228">Return to the Azure Stack environment with the file or text from the activation key created from Get-AzsActivationKey.</span></span> <span data-ttu-id="5cd78-229">Next you will create an activation resource in Azure Stack using that activation key.</span><span class="sxs-lookup"><span data-stu-id="5cd78-229">Next you will create an activation resource in Azure Stack using that activation key.</span></span> <span data-ttu-id="5cd78-230">To create an activation resource, run the following PowerShell cmdlets:</span><span class="sxs-lookup"><span data-stu-id="5cd78-230">To create an activation resource, run the following PowerShell cmdlets:</span></span>  

  ```Powershell
  $ActivationKey = "<activation key>"
  New-AzsActivationResource -PrivilegedEndpointCredential $YourCloudAdminCredential -PrivilegedEndpoint $YourPrivilegedEndpoint -ActivationKey $ActivationKey
  ```

<span data-ttu-id="5cd78-231">Optionally, you can use the Get-Content cmdlet to point to a file that contains your registration token:</span><span class="sxs-lookup"><span data-stu-id="5cd78-231">Optionally, you can use the Get-Content cmdlet to point to a file that contains your registration token:</span></span>

  ```Powershell
  $ActivationKey = Get-Content -Path '<Path>\<Activation Key File>'
  New-AzsActivationResource -PrivilegedEndpointCredential $YourCloudAdminCredential -PrivilegedEndpoint $YourPrivilegedEndpoint -ActivationKey $ActivationKey
  ```

## <a name="verify-azure-stack-registration"></a><span data-ttu-id="5cd78-232">Verify Azure Stack registration</span><span class="sxs-lookup"><span data-stu-id="5cd78-232">Verify Azure Stack registration</span></span>

<span data-ttu-id="5cd78-233">Use these steps to verify that Azure Stack is successfully registered with Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd78-233">Use these steps to verify that Azure Stack is successfully registered with Azure.</span></span>

1. <span data-ttu-id="5cd78-234">Sign in to the Azure Stack [administrator portal](https://docs.microsoft.com/azure/azure-stack/azure-stack-manage-portals#access-the-administrator-portal): https&#58;//adminportal.*&lt;region>.&lt;fqdn>*.</span><span class="sxs-lookup"><span data-stu-id="5cd78-234">Sign in to the Azure Stack [administrator portal](https://docs.microsoft.com/azure/azure-stack/azure-stack-manage-portals#access-the-administrator-portal): https&#58;//adminportal.*&lt;region>.&lt;fqdn>*.</span></span>
2. <span data-ttu-id="5cd78-235">Select **All Services**, and then under the **ADMINISTRATION** category, select **Marketplace management** > **Add from Azure**.</span><span class="sxs-lookup"><span data-stu-id="5cd78-235">Select **All Services**, and then under the **ADMINISTRATION** category, select **Marketplace management** > **Add from Azure**.</span></span>

<span data-ttu-id="5cd78-236">If you see a list of items available from Azure (such as WordPress), your activation was successful.</span><span class="sxs-lookup"><span data-stu-id="5cd78-236">If you see a list of items available from Azure (such as WordPress), your activation was successful.</span></span> <span data-ttu-id="5cd78-237">However, in disconnected environments you will not see Azure marketplace items in the Azure Stack marketplace.</span><span class="sxs-lookup"><span data-stu-id="5cd78-237">However, in disconnected environments you will not see Azure marketplace items in the Azure Stack marketplace.</span></span>

> [!Note]  
> <span data-ttu-id="5cd78-238">After registration is complete, the active warning for not registering will no longer appear.</span><span class="sxs-lookup"><span data-stu-id="5cd78-238">After registration is complete, the active warning for not registering will no longer appear.</span></span>

## <a name="renew-or-change-registration"></a><span data-ttu-id="5cd78-239">Renew or change registration</span><span class="sxs-lookup"><span data-stu-id="5cd78-239">Renew or change registration</span></span>

### <a name="renew-or-change-registration-in-connected-environments"></a><span data-ttu-id="5cd78-240">Renew or change registration in connected environments</span><span class="sxs-lookup"><span data-stu-id="5cd78-240">Renew or change registration in connected environments</span></span>

<span data-ttu-id="5cd78-241">You’ll need to update or renew your registration in the following circumstances:</span><span class="sxs-lookup"><span data-stu-id="5cd78-241">You’ll need to update or renew your registration in the following circumstances:</span></span>

- <span data-ttu-id="5cd78-242">After you renew your capacity-based yearly subscription.</span><span class="sxs-lookup"><span data-stu-id="5cd78-242">After you renew your capacity-based yearly subscription.</span></span>
- <span data-ttu-id="5cd78-243">When you change your billing model.</span><span class="sxs-lookup"><span data-stu-id="5cd78-243">When you change your billing model.</span></span>
- <span data-ttu-id="5cd78-244">When you scale changes (add/remove nodes) for capacity-based billing.</span><span class="sxs-lookup"><span data-stu-id="5cd78-244">When you scale changes (add/remove nodes) for capacity-based billing.</span></span>

#### <a name="change-the-subscription-you-use"></a><span data-ttu-id="5cd78-245">Change the subscription you use</span><span class="sxs-lookup"><span data-stu-id="5cd78-245">Change the subscription you use</span></span>

<span data-ttu-id="5cd78-246">If you would like to change the subscription you use, you must first run the **Remove-AzsRegistration** cmdlet, then ensure you are logged in to the correct Azure PowerShell context, and finally run **Set-AzsRegistration** with any changed parameters:</span><span class="sxs-lookup"><span data-stu-id="5cd78-246">If you would like to change the subscription you use, you must first run the **Remove-AzsRegistration** cmdlet, then ensure you are logged in to the correct Azure PowerShell context, and finally run **Set-AzsRegistration** with any changed parameters:</span></span>

  ```PowerShell  
  Remove-AzsRegistration -PrivilegedEndpointCredential $YourCloudAdminCredential -PrivilegedEndpoint $YourPrivilegedEndpoint
  Set-AzureRmContext -SubscriptionId $NewSubscriptionId
  Set-AzsRegistration -PrivilegedEndpointCredential $YourCloudAdminCredential -PrivilegedEndpoint $YourPrivilegedEndpoint -BillingModel PayAsYouUse -RegistrationName $RegistrationName
  ```

#### <a name="change-the-billing-model-or-how-to-offer-features"></a><span data-ttu-id="5cd78-247">Change the billing model or how to offer features</span><span class="sxs-lookup"><span data-stu-id="5cd78-247">Change the billing model or how to offer features</span></span>

<span data-ttu-id="5cd78-248">If you would like to change the billing model or how to offer features for your installation, you can call the registration function to set the new values.</span><span class="sxs-lookup"><span data-stu-id="5cd78-248">If you would like to change the billing model or how to offer features for your installation, you can call the registration function to set the new values.</span></span> <span data-ttu-id="5cd78-249">You do not need to first remove the current registration:</span><span class="sxs-lookup"><span data-stu-id="5cd78-249">You do not need to first remove the current registration:</span></span>

  ```PowerShell  
  Set-AzsRegistration -PrivilegedEndpointCredential $YourCloudAdminCredential -PrivilegedEndpoint $YourPrivilegedEndpoint -BillingModel PayAsYouUse -RegistrationName $RegistrationName
  ```

### <a name="renew-or-change-registration-in-disconnected-environments"></a><span data-ttu-id="5cd78-250">Renew or change registration in disconnected environments</span><span class="sxs-lookup"><span data-stu-id="5cd78-250">Renew or change registration in disconnected environments</span></span>

<span data-ttu-id="5cd78-251">You’ll need to update or renew your registration in the following circumstances:</span><span class="sxs-lookup"><span data-stu-id="5cd78-251">You’ll need to update or renew your registration in the following circumstances:</span></span>

- <span data-ttu-id="5cd78-252">After you renew your capacity-based yearly subscription.</span><span class="sxs-lookup"><span data-stu-id="5cd78-252">After you renew your capacity-based yearly subscription.</span></span>
- <span data-ttu-id="5cd78-253">When you change your billing model.</span><span class="sxs-lookup"><span data-stu-id="5cd78-253">When you change your billing model.</span></span>
- <span data-ttu-id="5cd78-254">When you scale changes (add/remove nodes) for capacity-based billing.</span><span class="sxs-lookup"><span data-stu-id="5cd78-254">When you scale changes (add/remove nodes) for capacity-based billing.</span></span>

#### <a name="remove-the-activation-resource-from-azure-stack"></a><span data-ttu-id="5cd78-255">Remove the activation resource from Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5cd78-255">Remove the activation resource from Azure Stack</span></span>

<span data-ttu-id="5cd78-256">You will first need to remove the activation resource from Azure Stack, and then the registration resource in Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd78-256">You will first need to remove the activation resource from Azure Stack, and then the registration resource in Azure.</span></span>  

<span data-ttu-id="5cd78-257">To remove the activation resource in Azure Stack, run the following PowerShell cmdlets in your Azure Stack environment:</span><span class="sxs-lookup"><span data-stu-id="5cd78-257">To remove the activation resource in Azure Stack, run the following PowerShell cmdlets in your Azure Stack environment:</span></span>  

  ```Powershell
  Remove-AzsActivationResource -PrivilegedEndpointCredential $YourCloudAdminCredential -PrivilegedEndpoint $YourPrivilegedEndpoint
  ```

<span data-ttu-id="5cd78-258">Next, to remove the registration resource in Azure, ensure you are on an Azure connected computer, sign in to the correct Azure PowerShell context, and run the appropriate PowerShell cmdlets as described below.</span><span class="sxs-lookup"><span data-stu-id="5cd78-258">Next, to remove the registration resource in Azure, ensure you are on an Azure connected computer, sign in to the correct Azure PowerShell context, and run the appropriate PowerShell cmdlets as described below.</span></span>

<span data-ttu-id="5cd78-259">You can use the registration token used to create the resource:</span><span class="sxs-lookup"><span data-stu-id="5cd78-259">You can use the registration token used to create the resource:</span></span>  

  ```Powershell
  $registrationToken = "<registration token>"
  Unregister-AzsEnvironment -RegistrationToken $registrationToken
  ```

<span data-ttu-id="5cd78-260">Or you can use the registration name:</span><span class="sxs-lookup"><span data-stu-id="5cd78-260">Or you can use the registration name:</span></span>

  ```Powershell
  $registrationName = "AzureStack-<Cloud ID of Azure Stack Environment>"
  Unregister-AzsEnvironment -RegistrationName $registrationName
  ```

### <a name="re-register-using-disconnected-steps"></a><span data-ttu-id="5cd78-261">Re-register using disconnected steps</span><span class="sxs-lookup"><span data-stu-id="5cd78-261">Re-register using disconnected steps</span></span>

<span data-ttu-id="5cd78-262">You have now completely unregistered in a disconnected scenario and must repeat the steps for registering an Azure Stack environment in a disconnected scenario.</span><span class="sxs-lookup"><span data-stu-id="5cd78-262">You have now completely unregistered in a disconnected scenario and must repeat the steps for registering an Azure Stack environment in a disconnected scenario.</span></span>

### <a name="disable-or-enable-usage-reporting"></a><span data-ttu-id="5cd78-263">Disable or enable usage reporting</span><span class="sxs-lookup"><span data-stu-id="5cd78-263">Disable or enable usage reporting</span></span>

<span data-ttu-id="5cd78-264">For Azure Stack environments that use a capacity billing model, turn off usage reporting with the **UsageReportingEnabled** parameter using either the **Set-AzsRegistration** or the **Get-AzsRegistrationToken** cmdlets.</span><span class="sxs-lookup"><span data-stu-id="5cd78-264">For Azure Stack environments that use a capacity billing model, turn off usage reporting with the **UsageReportingEnabled** parameter using either the **Set-AzsRegistration** or the **Get-AzsRegistrationToken** cmdlets.</span></span> <span data-ttu-id="5cd78-265">Azure Stack reports usage metrics by default.</span><span class="sxs-lookup"><span data-stu-id="5cd78-265">Azure Stack reports usage metrics by default.</span></span> <span data-ttu-id="5cd78-266">Operators with capacity uses or supporting a disconnected environment will need to turn off usage reporting.</span><span class="sxs-lookup"><span data-stu-id="5cd78-266">Operators with capacity uses or supporting a disconnected environment will need to turn off usage reporting.</span></span>

#### <a name="with-a-connected-azure-stack"></a><span data-ttu-id="5cd78-267">With a connected Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5cd78-267">With a connected Azure Stack</span></span>

   ```PowerShell  
   $CloudAdminCred = Get-Credential -UserName <Privileged endpoint credentials> -Message "Enter the cloud domain credentials to access the privileged endpoint."
   $RegistrationName = "<unique-registration-name>"
   Set-AzsRegistration `
      -PrivilegedEndpointCredential $CloudAdminCred `
      -PrivilegedEndpoint <PrivilegedEndPoint computer name> `
      -BillingModel Capacity
      -RegistrationName $RegistrationName
   ```

#### <a name="with-a-disconnected-azure-stack"></a><span data-ttu-id="5cd78-268">With a disconnected Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5cd78-268">With a disconnected Azure Stack</span></span>

1. <span data-ttu-id="5cd78-269">To change the registration token, run the following PowerShell cmdlets:</span><span class="sxs-lookup"><span data-stu-id="5cd78-269">To change the registration token, run the following PowerShell cmdlets:</span></span>  

   ```Powershell
   $FilePathForRegistrationToken = $env:SystemDrive\RegistrationToken.txt
   $RegistrationToken = Get-AzsRegistrationToken -PrivilegedEndpointCredential -UsageReportingEnabled:$False
   $YourCloudAdminCredential -PrivilegedEndpoint $YourPrivilegedEndpoint -BillingModel Capacity -AgreementNumber '<EA agreement number>' -TokenOutputFilePath $FilePathForRegistrationToken
   ```

   > [!Tip]  
   > <span data-ttu-id="5cd78-270">The registration token is saved in the file specified for *$FilePathForRegistrationToken*.</span><span class="sxs-lookup"><span data-stu-id="5cd78-270">The registration token is saved in the file specified for *$FilePathForRegistrationToken*.</span></span> <span data-ttu-id="5cd78-271">You can change the filepath or filename at your discretion.</span><span class="sxs-lookup"><span data-stu-id="5cd78-271">You can change the filepath or filename at your discretion.</span></span>

2. <span data-ttu-id="5cd78-272">Save this registration token for use on the Azure connected machine.</span><span class="sxs-lookup"><span data-stu-id="5cd78-272">Save this registration token for use on the Azure connected machine.</span></span> <span data-ttu-id="5cd78-273">You can copy the file or the text from $FilePathForRegistrationToken.</span><span class="sxs-lookup"><span data-stu-id="5cd78-273">You can copy the file or the text from $FilePathForRegistrationToken.</span></span>

## <a name="move-a-registration-resource"></a><span data-ttu-id="5cd78-274">Move a registration resource</span><span class="sxs-lookup"><span data-stu-id="5cd78-274">Move a registration resource</span></span>
<span data-ttu-id="5cd78-275">Moving a registration resource between resource groups under the same subscription **is** supported for all environments.</span><span class="sxs-lookup"><span data-stu-id="5cd78-275">Moving a registration resource between resource groups under the same subscription **is** supported for all environments.</span></span> <span data-ttu-id="5cd78-276">However, moving a registration resource between subscriptions is only supported for CSPs when both subscriptions resolve to the same Partner ID.</span><span class="sxs-lookup"><span data-stu-id="5cd78-276">However, moving a registration resource between subscriptions is only supported for CSPs when both subscriptions resolve to the same Partner ID.</span></span> <span data-ttu-id="5cd78-277">For more information about moving resources to a new resource group, see [Move resources to new resource group or subscription](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-move-resources).</span><span class="sxs-lookup"><span data-stu-id="5cd78-277">For more information about moving resources to a new resource group, see [Move resources to new resource group or subscription](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-move-resources).</span></span>

## <a name="registration-reference"></a><span data-ttu-id="5cd78-278">Registration reference</span><span class="sxs-lookup"><span data-stu-id="5cd78-278">Registration reference</span></span>

### <a name="set-azsregistration"></a><span data-ttu-id="5cd78-279">Set-AzsRegistration</span><span class="sxs-lookup"><span data-stu-id="5cd78-279">Set-AzsRegistration</span></span>

<span data-ttu-id="5cd78-280">You can use Set-AzsRegistration to register Azure Stack with Azure and enable or disable the offer of items in the marketplace and usage reporting.</span><span class="sxs-lookup"><span data-stu-id="5cd78-280">You can use Set-AzsRegistration to register Azure Stack with Azure and enable or disable the offer of items in the marketplace and usage reporting.</span></span>

<span data-ttu-id="5cd78-281">To run the cmdlet, you need:</span><span class="sxs-lookup"><span data-stu-id="5cd78-281">To run the cmdlet, you need:</span></span>
- <span data-ttu-id="5cd78-282">A global Azure subscription of any type.</span><span class="sxs-lookup"><span data-stu-id="5cd78-282">A global Azure subscription of any type.</span></span>
- <span data-ttu-id="5cd78-283">You must also be logged in to Azure PowerShell with an account that is an owner or contributor to that subscription.</span><span class="sxs-lookup"><span data-stu-id="5cd78-283">You must also be logged in to Azure PowerShell with an account that is an owner or contributor to that subscription.</span></span>

```PowerShell
    Set-AzsRegistration [-PrivilegedEndpointCredential] <PSCredential> [-PrivilegedEndpoint] <String> [[-AzureContext]
    <PSObject>] [[-ResourceGroupName] <String>] [[-ResourceGroupLocation] <String>] [[-BillingModel] <String>]
    [-MarketplaceSyndicationEnabled] [-UsageReportingEnabled] [[-AgreementNumber] <String>] [[-RegistrationName]
    <String>] [<CommonParameters>]
   ```

| <span data-ttu-id="5cd78-284">Parameter</span><span class="sxs-lookup"><span data-stu-id="5cd78-284">Parameter</span></span> | <span data-ttu-id="5cd78-285">Type</span><span class="sxs-lookup"><span data-stu-id="5cd78-285">Type</span></span> | <span data-ttu-id="5cd78-286">Description</span><span class="sxs-lookup"><span data-stu-id="5cd78-286">Description</span></span> |
|-------------------------------|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5cd78-287">PrivilegedEndpointCredential</span><span class="sxs-lookup"><span data-stu-id="5cd78-287">PrivilegedEndpointCredential</span></span> | <span data-ttu-id="5cd78-288">PSCredential</span><span class="sxs-lookup"><span data-stu-id="5cd78-288">PSCredential</span></span> | <span data-ttu-id="5cd78-289">The credentials used to [access the privileged endpoint](azure-stack-privileged-endpoint.md#access-the-privileged-endpoint).</span><span class="sxs-lookup"><span data-stu-id="5cd78-289">The credentials used to [access the privileged endpoint](azure-stack-privileged-endpoint.md#access-the-privileged-endpoint).</span></span> <span data-ttu-id="5cd78-290">The username is in the format **AzureStackDomain\CloudAdmin**.</span><span class="sxs-lookup"><span data-stu-id="5cd78-290">The username is in the format **AzureStackDomain\CloudAdmin**.</span></span> |
| <span data-ttu-id="5cd78-291">PrivilegedEndpoint</span><span class="sxs-lookup"><span data-stu-id="5cd78-291">PrivilegedEndpoint</span></span> | <span data-ttu-id="5cd78-292">String</span><span class="sxs-lookup"><span data-stu-id="5cd78-292">String</span></span> | <span data-ttu-id="5cd78-293">A pre-configured remote PowerShell console that provides you with capabilities like log collection and other post deployment tasks.</span><span class="sxs-lookup"><span data-stu-id="5cd78-293">A pre-configured remote PowerShell console that provides you with capabilities like log collection and other post deployment tasks.</span></span> <span data-ttu-id="5cd78-294">To learn more, refer to the [using the privileged endpoint](azure-stack-privileged-endpoint.md#access-the-privileged-endpoint) article.</span><span class="sxs-lookup"><span data-stu-id="5cd78-294">To learn more, refer to the [using the privileged endpoint](azure-stack-privileged-endpoint.md#access-the-privileged-endpoint) article.</span></span> |
| <span data-ttu-id="5cd78-295">AzureContext</span><span class="sxs-lookup"><span data-stu-id="5cd78-295">AzureContext</span></span> | <span data-ttu-id="5cd78-296">PSObject</span><span class="sxs-lookup"><span data-stu-id="5cd78-296">PSObject</span></span> |  |
| <span data-ttu-id="5cd78-297">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="5cd78-297">ResourceGroupName</span></span> | <span data-ttu-id="5cd78-298">String</span><span class="sxs-lookup"><span data-stu-id="5cd78-298">String</span></span> |  |
| <span data-ttu-id="5cd78-299">ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="5cd78-299">ResourceGroupLocation</span></span> | <span data-ttu-id="5cd78-300">String</span><span class="sxs-lookup"><span data-stu-id="5cd78-300">String</span></span> |  |
| <span data-ttu-id="5cd78-301">BillingModel</span><span class="sxs-lookup"><span data-stu-id="5cd78-301">BillingModel</span></span> | <span data-ttu-id="5cd78-302">String</span><span class="sxs-lookup"><span data-stu-id="5cd78-302">String</span></span> | <span data-ttu-id="5cd78-303">The billing model that your subscription uses.</span><span class="sxs-lookup"><span data-stu-id="5cd78-303">The billing model that your subscription uses.</span></span> <span data-ttu-id="5cd78-304">Allowed values for this parameter are: Capacity, PayAsYouUse, and Development.</span><span class="sxs-lookup"><span data-stu-id="5cd78-304">Allowed values for this parameter are: Capacity, PayAsYouUse, and Development.</span></span> |
| <span data-ttu-id="5cd78-305">MarketplaceSyndicationEnabled</span><span class="sxs-lookup"><span data-stu-id="5cd78-305">MarketplaceSyndicationEnabled</span></span> |  |  |
| <span data-ttu-id="5cd78-306">UsageReportingEnabled</span><span class="sxs-lookup"><span data-stu-id="5cd78-306">UsageReportingEnabled</span></span> | <span data-ttu-id="5cd78-307">True/False</span><span class="sxs-lookup"><span data-stu-id="5cd78-307">True/False</span></span> | <span data-ttu-id="5cd78-308">Azure Stack reports usage metrics by default.</span><span class="sxs-lookup"><span data-stu-id="5cd78-308">Azure Stack reports usage metrics by default.</span></span> <span data-ttu-id="5cd78-309">Operators with capacity uses or supporting a disconnected environment will need to turn off usage reporting.</span><span class="sxs-lookup"><span data-stu-id="5cd78-309">Operators with capacity uses or supporting a disconnected environment will need to turn off usage reporting.</span></span> <span data-ttu-id="5cd78-310">Allowed values for this parameter are: True, False.</span><span class="sxs-lookup"><span data-stu-id="5cd78-310">Allowed values for this parameter are: True, False.</span></span> |
| <span data-ttu-id="5cd78-311">AgreementNumber</span><span class="sxs-lookup"><span data-stu-id="5cd78-311">AgreementNumber</span></span> | <span data-ttu-id="5cd78-312">String</span><span class="sxs-lookup"><span data-stu-id="5cd78-312">String</span></span> |  |
| <span data-ttu-id="5cd78-313">RegistrationName</span><span class="sxs-lookup"><span data-stu-id="5cd78-313">RegistrationName</span></span> | <span data-ttu-id="5cd78-314">String</span><span class="sxs-lookup"><span data-stu-id="5cd78-314">String</span></span> | <span data-ttu-id="5cd78-315">Set a unique name for the registration if you are running the registration script on more than one instance of Azure Stack using the same Azure Subscription ID.</span><span class="sxs-lookup"><span data-stu-id="5cd78-315">Set a unique name for the registration if you are running the registration script on more than one instance of Azure Stack using the same Azure Subscription ID.</span></span> <span data-ttu-id="5cd78-316">The parameter has a default value of **AzureStackRegistration**.</span><span class="sxs-lookup"><span data-stu-id="5cd78-316">The parameter has a default value of **AzureStackRegistration**.</span></span> <span data-ttu-id="5cd78-317">However, if you use the same name on more than one instance of Azure Stack, the script will fail.</span><span class="sxs-lookup"><span data-stu-id="5cd78-317">However, if you use the same name on more than one instance of Azure Stack, the script will fail.</span></span> |

### <a name="get-azsregistrationtoken"></a><span data-ttu-id="5cd78-318">Get-AzsRegistrationToken</span><span class="sxs-lookup"><span data-stu-id="5cd78-318">Get-AzsRegistrationToken</span></span>

<span data-ttu-id="5cd78-319">Get-AzsRegistrationToken will generate a registration token from the input parameters.</span><span class="sxs-lookup"><span data-stu-id="5cd78-319">Get-AzsRegistrationToken will generate a registration token from the input parameters.</span></span>

```PowerShell  
    Get-AzsRegistrationToken [-PrivilegedEndpointCredential] <PSCredential> [-PrivilegedEndpoint] <String>
    [-BillingModel] <String> [[-TokenOutputFilePath] <String>] [-UsageReportingEnabled] [[-AgreementNumber] <String>]
    [<CommonParameters>]
```
| <span data-ttu-id="5cd78-320">Parameter</span><span class="sxs-lookup"><span data-stu-id="5cd78-320">Parameter</span></span> | <span data-ttu-id="5cd78-321">Type</span><span class="sxs-lookup"><span data-stu-id="5cd78-321">Type</span></span> | <span data-ttu-id="5cd78-322">Description</span><span class="sxs-lookup"><span data-stu-id="5cd78-322">Description</span></span> |
|-------------------------------|--------------|-------------|
| <span data-ttu-id="5cd78-323">PrivilegedEndpointCredential</span><span class="sxs-lookup"><span data-stu-id="5cd78-323">PrivilegedEndpointCredential</span></span> | <span data-ttu-id="5cd78-324">PSCredential</span><span class="sxs-lookup"><span data-stu-id="5cd78-324">PSCredential</span></span> | <span data-ttu-id="5cd78-325">The credentials used to [access the privileged endpoint](azure-stack-privileged-endpoint.md#access-the-privileged-endpoint).</span><span class="sxs-lookup"><span data-stu-id="5cd78-325">The credentials used to [access the privileged endpoint](azure-stack-privileged-endpoint.md#access-the-privileged-endpoint).</span></span> <span data-ttu-id="5cd78-326">The username is in the format **AzureStackDomain\CloudAdmin**.</span><span class="sxs-lookup"><span data-stu-id="5cd78-326">The username is in the format **AzureStackDomain\CloudAdmin**.</span></span> |
| <span data-ttu-id="5cd78-327">PrivilegedEndpoint</span><span class="sxs-lookup"><span data-stu-id="5cd78-327">PrivilegedEndpoint</span></span> | <span data-ttu-id="5cd78-328">String</span><span class="sxs-lookup"><span data-stu-id="5cd78-328">String</span></span> |  <span data-ttu-id="5cd78-329">A pre-configured remote PowerShell console that provides you with capabilities like log collection and other post deployment tasks.</span><span class="sxs-lookup"><span data-stu-id="5cd78-329">A pre-configured remote PowerShell console that provides you with capabilities like log collection and other post deployment tasks.</span></span> <span data-ttu-id="5cd78-330">To learn more, refer to the [using the privileged endpoint](azure-stack-privileged-endpoint.md#access-the-privileged-endpoint) article.</span><span class="sxs-lookup"><span data-stu-id="5cd78-330">To learn more, refer to the [using the privileged endpoint](azure-stack-privileged-endpoint.md#access-the-privileged-endpoint) article.</span></span> |
| <span data-ttu-id="5cd78-331">AzureContext</span><span class="sxs-lookup"><span data-stu-id="5cd78-331">AzureContext</span></span> | <span data-ttu-id="5cd78-332">PSObject</span><span class="sxs-lookup"><span data-stu-id="5cd78-332">PSObject</span></span> |  |
| <span data-ttu-id="5cd78-333">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="5cd78-333">ResourceGroupName</span></span> | <span data-ttu-id="5cd78-334">String</span><span class="sxs-lookup"><span data-stu-id="5cd78-334">String</span></span> |  |
| <span data-ttu-id="5cd78-335">ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="5cd78-335">ResourceGroupLocation</span></span> | <span data-ttu-id="5cd78-336">String</span><span class="sxs-lookup"><span data-stu-id="5cd78-336">String</span></span> |  |
| <span data-ttu-id="5cd78-337">BillingModel</span><span class="sxs-lookup"><span data-stu-id="5cd78-337">BillingModel</span></span> | <span data-ttu-id="5cd78-338">String</span><span class="sxs-lookup"><span data-stu-id="5cd78-338">String</span></span> | <span data-ttu-id="5cd78-339">The billing model that your subscription uses.</span><span class="sxs-lookup"><span data-stu-id="5cd78-339">The billing model that your subscription uses.</span></span> <span data-ttu-id="5cd78-340">Allowed values for this parameter are: Capacity, PayAsYouUse, and Development.</span><span class="sxs-lookup"><span data-stu-id="5cd78-340">Allowed values for this parameter are: Capacity, PayAsYouUse, and Development.</span></span> |
| <span data-ttu-id="5cd78-341">MarketplaceSyndicationEnabled</span><span class="sxs-lookup"><span data-stu-id="5cd78-341">MarketplaceSyndicationEnabled</span></span> | <span data-ttu-id="5cd78-342">True/False</span><span class="sxs-lookup"><span data-stu-id="5cd78-342">True/False</span></span> |  |
| <span data-ttu-id="5cd78-343">UsageReportingEnabled</span><span class="sxs-lookup"><span data-stu-id="5cd78-343">UsageReportingEnabled</span></span> | <span data-ttu-id="5cd78-344">True/False</span><span class="sxs-lookup"><span data-stu-id="5cd78-344">True/False</span></span> | <span data-ttu-id="5cd78-345">Azure Stack reports usage metrics by default.</span><span class="sxs-lookup"><span data-stu-id="5cd78-345">Azure Stack reports usage metrics by default.</span></span> <span data-ttu-id="5cd78-346">Operators with capacity uses or supporting a disconnected environment will need to turn off usage reporting.</span><span class="sxs-lookup"><span data-stu-id="5cd78-346">Operators with capacity uses or supporting a disconnected environment will need to turn off usage reporting.</span></span> <span data-ttu-id="5cd78-347">Allowed values for this parameter are: True, False.</span><span class="sxs-lookup"><span data-stu-id="5cd78-347">Allowed values for this parameter are: True, False.</span></span> |
| <span data-ttu-id="5cd78-348">AgreementNumber</span><span class="sxs-lookup"><span data-stu-id="5cd78-348">AgreementNumber</span></span> | <span data-ttu-id="5cd78-349">String</span><span class="sxs-lookup"><span data-stu-id="5cd78-349">String</span></span> |  |


## <a name="next-steps"></a><span data-ttu-id="5cd78-350">Next steps</span><span class="sxs-lookup"><span data-stu-id="5cd78-350">Next steps</span></span>

[<span data-ttu-id="5cd78-351">Download marketplace items from Azure</span><span class="sxs-lookup"><span data-stu-id="5cd78-351">Download marketplace items from Azure</span></span>](azure-stack-download-azure-marketplace-item.md)
