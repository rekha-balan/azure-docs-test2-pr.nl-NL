---
title: Register Azure Stack | Microsoft Docs
description: Register Azure Stack with your Azure subscription.
services: azure-stack
documentationcenter: ''
author: ErikjeMS
manager: byronr
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: erikje
ms.openlocfilehash: da6c3a013b8d7539160f05a692655bfcdd72312f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554644"
---
# <a name="register-azure-stack-with-your-azure-subscription"></a><span data-ttu-id="f114b-103">Register Azure Stack with your Azure Subscription</span><span class="sxs-lookup"><span data-stu-id="f114b-103">Register Azure Stack with your Azure Subscription</span></span>

<span data-ttu-id="f114b-104">For Azure Active Directory deployments, you can register Azure Stack with Azure to download marketplace items from Azure and to set up commerce data reporting back to Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f114b-104">For Azure Active Directory deployments, you can register Azure Stack with Azure to download marketplace items from Azure and to set up commerce data reporting back to Microsoft.</span></span> 

> [!NOTE]
><span data-ttu-id="f114b-105">In TP3, registering Azure Stack is not required because you don't have to select a business model or connection option.</span><span class="sxs-lookup"><span data-stu-id="f114b-105">In TP3, registering Azure Stack is not required because you don't have to select a business model or connection option.</span></span> <span data-ttu-id="f114b-106">However, you can test the process and provide feedback about it.</span><span class="sxs-lookup"><span data-stu-id="f114b-106">However, you can test the process and provide feedback about it.</span></span>
>


## <a name="get-azure-subscription"></a><span data-ttu-id="f114b-107">Get Azure subscription</span><span class="sxs-lookup"><span data-stu-id="f114b-107">Get Azure subscription</span></span>

<span data-ttu-id="f114b-108">Before registering Azure Stack with Azure, you must have:</span><span class="sxs-lookup"><span data-stu-id="f114b-108">Before registering Azure Stack with Azure, you must have:</span></span>

- <span data-ttu-id="f114b-109">The subscription ID for an Azure subscription (China, Germany, government cloud, and CSP subscriptions are not supported in TP3)</span><span class="sxs-lookup"><span data-stu-id="f114b-109">The subscription ID for an Azure subscription (China, Germany, government cloud, and CSP subscriptions are not supported in TP3)</span></span>
- <span data-ttu-id="f114b-110">The username and password for an account that is an owner for the subscription (Hotmail.com, live.com domains and 2FA accounts are not supported)</span><span class="sxs-lookup"><span data-stu-id="f114b-110">The username and password for an account that is an owner for the subscription (Hotmail.com, live.com domains and 2FA accounts are not supported)</span></span>
- <span data-ttu-id="f114b-111">The AAD directory for the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f114b-111">The AAD directory for the Azure subscription.</span></span> <span data-ttu-id="f114b-112">You can find this directory in Azure by hovering over your avatar at the top right corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f114b-112">You can find this directory in Azure by hovering over your avatar at the top right corner of the Azure portal.</span></span> 

<span data-ttu-id="f114b-113">If you don’t have an Azure subscription that meets these requirements, you can [create a free Azure account here](https://azure.microsoft.com/en-us/free/?b=17.06).</span><span class="sxs-lookup"><span data-stu-id="f114b-113">If you don’t have an Azure subscription that meets these requirements, you can [create a free Azure account here](https://azure.microsoft.com/en-us/free/?b=17.06).</span></span> <span data-ttu-id="f114b-114">Registering Azure Stack incurs no cost on your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f114b-114">Registering Azure Stack incurs no cost on your Azure subscription.</span></span>




## <a name="register"></a><span data-ttu-id="f114b-115">Register</span><span class="sxs-lookup"><span data-stu-id="f114b-115">Register</span></span>

> [!NOTE]
><span data-ttu-id="f114b-116">All these steps must be completed on the host computer, not the console computer.</span><span class="sxs-lookup"><span data-stu-id="f114b-116">All these steps must be completed on the host computer, not the console computer.</span></span>
>

1. <span data-ttu-id="f114b-117">Sign in to the Azure Stack POC host computer as an Azure Stack administrator.</span><span class="sxs-lookup"><span data-stu-id="f114b-117">Sign in to the Azure Stack POC host computer as an Azure Stack administrator.</span></span>
2. <span data-ttu-id="f114b-118">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="f114b-118">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span> 
3. <span data-ttu-id="f114b-119">Copy the [RegisterWithAzure.ps1 script](https://go.microsoft.com/fwlink/?linkid=842959) to a folder (such as C:\Temp).</span><span class="sxs-lookup"><span data-stu-id="f114b-119">Copy the [RegisterWithAzure.ps1 script](https://go.microsoft.com/fwlink/?linkid=842959) to a folder (such as C:\Temp).</span></span>
4. <span data-ttu-id="f114b-120">Start PowerShell ISE as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f114b-120">Start PowerShell ISE as an administrator.</span></span>
5. <span data-ttu-id="f114b-121">Run the RegisterWithAzure.ps1 script.</span><span class="sxs-lookup"><span data-stu-id="f114b-121">Run the RegisterWithAzure.ps1 script.</span></span> <span data-ttu-id="f114b-122">Make sure to change the values for *YourAccountName* (the owner of the Azure subscription), *YourID*, and *YourDirectory* to match your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f114b-122">Make sure to change the values for *YourAccountName* (the owner of the Azure subscription), *YourID*, and *YourDirectory* to match your Azure subscription.</span></span>

    ```powershell
    RegisterWithAzure.ps1 -azureDirectory YourDirectory -azureSubscriptionId YourID -azureSubscriptionOwner YourAccountName
    ```
    
    <span data-ttu-id="f114b-123">For example:</span><span class="sxs-lookup"><span data-stu-id="f114b-123">For example:</span></span>
    
    ```powershell
    C:\temp\RegisterWithAzure.ps1 -azureDirectory contoso.onmicrosoft.com ` 
    -azureSubscriptionId 5c15413c-1135-479b-a046-857e1ef9fbeb ` 
    -azureSubscriptionOwner serviceadmin@contoso.onmicrosoft.com     
    ```
    
6. <span data-ttu-id="f114b-124">At the two prompts, press Enter.</span><span class="sxs-lookup"><span data-stu-id="f114b-124">At the two prompts, press Enter.</span></span>
7. <span data-ttu-id="f114b-125">In the pop-up log in window, enter your Azure subscription credentials</span><span class="sxs-lookup"><span data-stu-id="f114b-125">In the pop-up log in window, enter your Azure subscription credentials</span></span>

## <a name="verify-the-registration"></a><span data-ttu-id="f114b-126">Verify the registration</span><span class="sxs-lookup"><span data-stu-id="f114b-126">Verify the registration</span></span>

1. <span data-ttu-id="f114b-127">Sign in to the Azure Stack portal as a service administrator.</span><span class="sxs-lookup"><span data-stu-id="f114b-127">Sign in to the Azure Stack portal as a service administrator.</span></span>
2. <span data-ttu-id="f114b-128">Click **More Services** > **Marketplace Management** > **Add from Azure**.</span><span class="sxs-lookup"><span data-stu-id="f114b-128">Click **More Services** > **Marketplace Management** > **Add from Azure**.</span></span>
3. <span data-ttu-id="f114b-129">If you see a list of items available from Azure (such as WordPress), your activation was successful.</span><span class="sxs-lookup"><span data-stu-id="f114b-129">If you see a list of items available from Azure (such as WordPress), your activation was successful.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f114b-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="f114b-130">Next steps</span></span>

[<span data-ttu-id="f114b-131">Connect to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="f114b-131">Connect to Azure Stack</span></span>](azure-stack-connect-azure-stack.md)

