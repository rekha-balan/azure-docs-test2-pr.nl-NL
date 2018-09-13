---
title: Register the ASDK with Azure | Microsoft Docs
description: Describes how to register Azure Stack with Azure to enable marketplace syndication and usage reporting.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/11/2018
ms.author: jeffgilb
ms.reviewer: misainat
ms.openlocfilehash: eacf8fc9335af2dacffa3e13da47ea39a2776f2b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869048"
---
# <a name="azure-stack-registration"></a><span data-ttu-id="1b210-103">Azure Stack registration</span><span class="sxs-lookup"><span data-stu-id="1b210-103">Azure Stack registration</span></span>
<span data-ttu-id="1b210-104">You can register your Azure Stack Development Kit (ASDK) installation with Azure to download marketplace items from Azure and to set up commerce data reporting back to Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1b210-104">You can register your Azure Stack Development Kit (ASDK) installation with Azure to download marketplace items from Azure and to set up commerce data reporting back to Microsoft.</span></span> <span data-ttu-id="1b210-105">Registration is required to support full Azure Stack functionality, including marketplace syndication.</span><span class="sxs-lookup"><span data-stu-id="1b210-105">Registration is required to support full Azure Stack functionality, including marketplace syndication.</span></span> <span data-ttu-id="1b210-106">Registration is recommended because it enables you to test important Azure Stack functionality like marketplace syndication and usage reporting.</span><span class="sxs-lookup"><span data-stu-id="1b210-106">Registration is recommended because it enables you to test important Azure Stack functionality like marketplace syndication and usage reporting.</span></span> <span data-ttu-id="1b210-107">After you register Azure Stack, usage is reported to Azure commerce.</span><span class="sxs-lookup"><span data-stu-id="1b210-107">After you register Azure Stack, usage is reported to Azure commerce.</span></span> <span data-ttu-id="1b210-108">You can see it under the subscription you used for registration.</span><span class="sxs-lookup"><span data-stu-id="1b210-108">You can see it under the subscription you used for registration.</span></span> <span data-ttu-id="1b210-109">However, ASDK users aren't charged for any usage they report.</span><span class="sxs-lookup"><span data-stu-id="1b210-109">However, ASDK users aren't charged for any usage they report.</span></span>

<span data-ttu-id="1b210-110">If you do not register your ASDK, you might see an **Activation Required** warning alert that advises you to register your Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="1b210-110">If you do not register your ASDK, you might see an **Activation Required** warning alert that advises you to register your Azure Stack Development Kit.</span></span> <span data-ttu-id="1b210-111">This behavior is expected.</span><span class="sxs-lookup"><span data-stu-id="1b210-111">This behavior is expected.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b210-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1b210-112">Prerequisites</span></span>
<span data-ttu-id="1b210-113">Before using these instructions to register the ASDK with Azure, ensure that you have installed the Azure Stack PowerShell and downloaded the Azure Stack tools as described in the [post-deployment configuration](asdk-post-deploy.md) article.</span><span class="sxs-lookup"><span data-stu-id="1b210-113">Before using these instructions to register the ASDK with Azure, ensure that you have installed the Azure Stack PowerShell and downloaded the Azure Stack tools as described in the [post-deployment configuration](asdk-post-deploy.md) article.</span></span>

<span data-ttu-id="1b210-114">In addition, the PowerShell language mode must be set to **FullLanguageMode** on the computer used to register the ASDK with Azure.</span><span class="sxs-lookup"><span data-stu-id="1b210-114">In addition, the PowerShell language mode must be set to **FullLanguageMode** on the computer used to register the ASDK with Azure.</span></span> <span data-ttu-id="1b210-115">To verify that the current language mode is set to full, open an elevated PowerShell window and run the following PowerShell commands:</span><span class="sxs-lookup"><span data-stu-id="1b210-115">To verify that the current language mode is set to full, open an elevated PowerShell window and run the following PowerShell commands:</span></span>

```PowerShell  
$ExecutionContext.SessionState.LanguageMode
```

<span data-ttu-id="1b210-116">Ensure the output returns **FullLanguageMode**.</span><span class="sxs-lookup"><span data-stu-id="1b210-116">Ensure the output returns **FullLanguageMode**.</span></span> <span data-ttu-id="1b210-117">If any other language mode is returned, registration will need to be run on another computer or the language mode will need to be set to **FullLanguageMode** before continuing.</span><span class="sxs-lookup"><span data-stu-id="1b210-117">If any other language mode is returned, registration will need to be run on another computer or the language mode will need to be set to **FullLanguageMode** before continuing.</span></span>

## <a name="register-azure-stack-with-azure"></a><span data-ttu-id="1b210-118">Register Azure Stack with Azure</span><span class="sxs-lookup"><span data-stu-id="1b210-118">Register Azure Stack with Azure</span></span>
<span data-ttu-id="1b210-119">Follow these steps to register the ASDK with Azure.</span><span class="sxs-lookup"><span data-stu-id="1b210-119">Follow these steps to register the ASDK with Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="1b210-120">All these steps must be run from a computer that has access to the privileged endpoint.</span><span class="sxs-lookup"><span data-stu-id="1b210-120">All these steps must be run from a computer that has access to the privileged endpoint.</span></span> <span data-ttu-id="1b210-121">For the ASDK, that's the development kit host computer.</span><span class="sxs-lookup"><span data-stu-id="1b210-121">For the ASDK, that's the development kit host computer.</span></span>

1. <span data-ttu-id="1b210-122">Open a PowerShell console as an administrator.</span><span class="sxs-lookup"><span data-stu-id="1b210-122">Open a PowerShell console as an administrator.</span></span>  

2. <span data-ttu-id="1b210-123">Run the following PowerShell commands to register your ASDK installation with Azure.</span><span class="sxs-lookup"><span data-stu-id="1b210-123">Run the following PowerShell commands to register your ASDK installation with Azure.</span></span> <span data-ttu-id="1b210-124">You will need to sign in to both your Azure subscription and the local ASDK installation.</span><span class="sxs-lookup"><span data-stu-id="1b210-124">You will need to sign in to both your Azure subscription and the local ASDK installation.</span></span> <span data-ttu-id="1b210-125">If you don’t have an Azure subscription yet, you can [create a free Azure account here](https://azure.microsoft.com/free/?b=17.06).</span><span class="sxs-lookup"><span data-stu-id="1b210-125">If you don’t have an Azure subscription yet, you can [create a free Azure account here](https://azure.microsoft.com/free/?b=17.06).</span></span> <span data-ttu-id="1b210-126">Registering Azure Stack incurs no cost on your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="1b210-126">Registering Azure Stack incurs no cost on your Azure subscription.</span></span><br><br><span data-ttu-id="1b210-127">If you are running the registration script on more than one instance of Azure Stack using the same Azure Subscription ID, set a unique name for the registration when you run the **Set-AzsRegistration** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1b210-127">If you are running the registration script on more than one instance of Azure Stack using the same Azure Subscription ID, set a unique name for the registration when you run the **Set-AzsRegistration** cmdlet.</span></span> <span data-ttu-id="1b210-128">The **RegistrationName** parameter has a default value of **AzureStackRegistration**.</span><span class="sxs-lookup"><span data-stu-id="1b210-128">The **RegistrationName** parameter has a default value of **AzureStackRegistration**.</span></span> <span data-ttu-id="1b210-129">However, if you use the same name on more than one instance of Azure Stack, the script will fail.</span><span class="sxs-lookup"><span data-stu-id="1b210-129">However, if you use the same name on more than one instance of Azure Stack, the script will fail.</span></span>

    ```PowerShell  
    # Add the Azure cloud subscription environment name. 
    # Supported environment names are AzureCloud, AzureChinaCloud or AzureUSGovernment depending which Azure subscription you are using.
    Add-AzureRmAccount -EnvironmentName "AzureCloud"

    # Register the Azure Stack resource provider in your Azure subscription
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.AzureStack

    #Import the registration module that was downloaded with the GitHub tools
    Import-Module C:\AzureStack-Tools-master\Registration\RegisterWithAzure.psm1

    #Register Azure Stack
    $AzureContext = Get-AzureRmContext
    $CloudAdminCred = Get-Credential -UserName AZURESTACK\CloudAdmin -Message "Enter the credentials to access the privileged endpoint."
    Set-AzsRegistration `
    -PrivilegedEndpointCredential $CloudAdminCred `
    -PrivilegedEndpoint AzS-ERCS01 `
    -BillingModel Development `
    -RegistrationName "<Unique-name>"
    ```
3. <span data-ttu-id="1b210-130">When the script completes, you should see this message: **Your environment is now registered and activated using the provided parameters.**</span><span class="sxs-lookup"><span data-stu-id="1b210-130">When the script completes, you should see this message: **Your environment is now registered and activated using the provided parameters.**</span></span>

    ![Your environment is now registered](media/asdk-register/1.PNG)

## <a name="verify-the-registration-was-successful"></a><span data-ttu-id="1b210-132">Verify the registration was successful</span><span class="sxs-lookup"><span data-stu-id="1b210-132">Verify the registration was successful</span></span>
<span data-ttu-id="1b210-133">Follow these steps to verify that the ASDK registration with Azure was successful.</span><span class="sxs-lookup"><span data-stu-id="1b210-133">Follow these steps to verify that the ASDK registration with Azure was successful.</span></span>

1. <span data-ttu-id="1b210-134">Sign in to the [Azure Stack administration portal](https://adminportal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="1b210-134">Sign in to the [Azure Stack administration portal](https://adminportal.local.azurestack.external).</span></span>

2. <span data-ttu-id="1b210-135">Click **Marketplace Management** > **Add from Azure**.</span><span class="sxs-lookup"><span data-stu-id="1b210-135">Click **Marketplace Management** > **Add from Azure**.</span></span>

    ![](media/asdk-register/2.PNG)

3. <span data-ttu-id="1b210-136">If you see a list of items available from Azure, your activation was successful.</span><span class="sxs-lookup"><span data-stu-id="1b210-136">If you see a list of items available from Azure, your activation was successful.</span></span>

    ![](media/asdk-register/3.PNG)

## <a name="move-a-registration-resource"></a><span data-ttu-id="1b210-137">Move a registration resource</span><span class="sxs-lookup"><span data-stu-id="1b210-137">Move a registration resource</span></span>
<span data-ttu-id="1b210-138">Moving a registration resource between resource groups under the same subscription **is** supported.</span><span class="sxs-lookup"><span data-stu-id="1b210-138">Moving a registration resource between resource groups under the same subscription **is** supported.</span></span> <span data-ttu-id="1b210-139">For more information about moving resources to a new resource group, see [Move resources to new resource group or subscription](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-move-resources).</span><span class="sxs-lookup"><span data-stu-id="1b210-139">For more information about moving resources to a new resource group, see [Move resources to new resource group or subscription](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-move-resources).</span></span>


## <a name="next-steps"></a><span data-ttu-id="1b210-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="1b210-140">Next steps</span></span>
[<span data-ttu-id="1b210-141">Add an Azure Stack marketplace item</span><span class="sxs-lookup"><span data-stu-id="1b210-141">Add an Azure Stack marketplace item</span></span>](.\.\azure-stack-marketplace.md)
