---
title: Get data using the Azure AD Reporting API with certificates | Microsoft Docs
description: Explains how to use the Azure AD Reporting API with certificate credentials to get data from directories without user intervention.
services: active-directory
documentationcenter: ''
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: ''
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: fa434e5076036b4c34b6ec8a478958f3591a0b6f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554401"
---
# <a name="get-data-using-the-azure-ad-reporting-api-with-certificates"></a><span data-ttu-id="b8348-103">Get data using the Azure AD Reporting API with certificates</span><span class="sxs-lookup"><span data-stu-id="b8348-103">Get data using the Azure AD Reporting API with certificates</span></span>
<span data-ttu-id="b8348-104">This article discusses how to use the Azure AD Reporting API with certificate credentials to get data from directories without user intervention.</span><span class="sxs-lookup"><span data-stu-id="b8348-104">This article discusses how to use the Azure AD Reporting API with certificate credentials to get data from directories without user intervention.</span></span> 

## <a name="use-the-azure-ad-reporting-api"></a><span data-ttu-id="b8348-105">Use the Azure AD Reporting API</span><span class="sxs-lookup"><span data-stu-id="b8348-105">Use the Azure AD Reporting API</span></span> 
<span data-ttu-id="b8348-106">Azure AD Reporting API requires that you complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="b8348-106">Azure AD Reporting API requires that you complete the following steps:</span></span>
 *  <span data-ttu-id="b8348-107">Install prerequisites</span><span class="sxs-lookup"><span data-stu-id="b8348-107">Install prerequisites</span></span>
 *  <span data-ttu-id="b8348-108">Set the certificate in your app</span><span class="sxs-lookup"><span data-stu-id="b8348-108">Set the certificate in your app</span></span>
 *  <span data-ttu-id="b8348-109">Get an access token</span><span class="sxs-lookup"><span data-stu-id="b8348-109">Get an access token</span></span>
 *  <span data-ttu-id="b8348-110">Use the access token to call the Graph API</span><span class="sxs-lookup"><span data-stu-id="b8348-110">Use the access token to call the Graph API</span></span>

<span data-ttu-id="b8348-111">For information about source code, see [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span><span class="sxs-lookup"><span data-stu-id="b8348-111">For information about source code, see [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span></span> 

### <a name="install-prerequisites"></a><span data-ttu-id="b8348-112">Install prerequisites</span><span class="sxs-lookup"><span data-stu-id="b8348-112">Install prerequisites</span></span>
<span data-ttu-id="b8348-113">You will need to have Azure AD PowerShell V2 and AzureADUtils module installed.</span><span class="sxs-lookup"><span data-stu-id="b8348-113">You will need to have Azure AD PowerShell V2 and AzureADUtils module installed.</span></span>

1. <span data-ttu-id="b8348-114">Download and install Azure AD Powershell V2, following the instructions at [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="b8348-114">Download and install Azure AD Powershell V2, following the instructions at [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span></span>
2. <span data-ttu-id="b8348-115">Download the Azure AD Utils module from [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span><span class="sxs-lookup"><span data-stu-id="b8348-115">Download the Azure AD Utils module from [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span></span> 
  <span data-ttu-id="b8348-116">This module provides several utility cmdlets including:</span><span class="sxs-lookup"><span data-stu-id="b8348-116">This module provides several utility cmdlets including:</span></span>
   * <span data-ttu-id="b8348-117">The latest version of ADAL using Nuget</span><span class="sxs-lookup"><span data-stu-id="b8348-117">The latest version of ADAL using Nuget</span></span>
   * <span data-ttu-id="b8348-118">Access tokens from user, application keys, and certificates using ADAL</span><span class="sxs-lookup"><span data-stu-id="b8348-118">Access tokens from user, application keys, and certificates using ADAL</span></span>
   * <span data-ttu-id="b8348-119">Graph API handling paged results</span><span class="sxs-lookup"><span data-stu-id="b8348-119">Graph API handling paged results</span></span>

<span data-ttu-id="b8348-120">**To install the Azure AD Utils module:**</span><span class="sxs-lookup"><span data-stu-id="b8348-120">**To install the Azure AD Utils module:**</span></span>

1. <span data-ttu-id="b8348-121">Create a directory to save the utilities module (for example, c:\azureAD) and download the module from GitHub.</span><span class="sxs-lookup"><span data-stu-id="b8348-121">Create a directory to save the utilities module (for example, c:\azureAD) and download the module from GitHub.</span></span>
2. <span data-ttu-id="b8348-122">Open a PowerShell session, and go to the directory you just created.</span><span class="sxs-lookup"><span data-stu-id="b8348-122">Open a PowerShell session, and go to the directory you just created.</span></span> 
3. <span data-ttu-id="b8348-123">Import the module, and install it in the PowerShell module path using the Install-AzureADUtilsModule cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b8348-123">Import the module, and install it in the PowerShell module path using the Install-AzureADUtilsModule cmdlet.</span></span> 

<span data-ttu-id="b8348-124">The session should look similar to this screen:</span><span class="sxs-lookup"><span data-stu-id="b8348-124">The session should look similar to this screen:</span></span>

  ![Windows Powershell](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-the-certificate-in-your-app"></a><span data-ttu-id="b8348-126">Set the certificate in your app</span><span class="sxs-lookup"><span data-stu-id="b8348-126">Set the certificate in your app</span></span>
1. <span data-ttu-id="b8348-127">If you already have an app, get its Object ID from the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b8348-127">If you already have an app, get its Object ID from the Azure Portal.</span></span> 

  ![Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-report-api-with-certificates/azure-portal.png)

2. <span data-ttu-id="b8348-129">Open a PowerShell session and connect to Azure AD using the Connect-AzureAD cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b8348-129">Open a PowerShell session and connect to Azure AD using the Connect-AzureAD cmdlet.</span></span>

  ![Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. <span data-ttu-id="b8348-131">Use the New-AzureADApplicationCertificateCredential cmdlet from AzureADUtils to add a certificate credential to it.</span><span class="sxs-lookup"><span data-stu-id="b8348-131">Use the New-AzureADApplicationCertificateCredential cmdlet from AzureADUtils to add a certificate credential to it.</span></span> 

>[!Note]
><span data-ttu-id="b8348-132">You need to provide the application Object ID that you captured earlier, as well as the certificate object (get this using the Cert: drive).</span><span class="sxs-lookup"><span data-stu-id="b8348-132">You need to provide the application Object ID that you captured earlier, as well as the certificate object (get this using the Cert: drive).</span></span>
>


  ![Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a><span data-ttu-id="b8348-134">Get an access token</span><span class="sxs-lookup"><span data-stu-id="b8348-134">Get an access token</span></span>

<span data-ttu-id="b8348-135">To get an access token, use the Get-AzureADGraphAPIAccessTokenFromCert cmdlet from AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="b8348-135">To get an access token, use the Get-AzureADGraphAPIAccessTokenFromCert cmdlet from AzureADUtils.</span></span> 

>[!NOTE]
><span data-ttu-id="b8348-136">You need to use the Application ID instead of the Object ID that you used in the last section.</span><span class="sxs-lookup"><span data-stu-id="b8348-136">You need to use the Application ID instead of the Object ID that you used in the last section.</span></span>
>

 ![Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-the-access-token-to-call-the-graph-api"></a><span data-ttu-id="b8348-138">Use the access token to call the Graph API</span><span class="sxs-lookup"><span data-stu-id="b8348-138">Use the access token to call the Graph API</span></span>

<span data-ttu-id="b8348-139">Now you can create the script.</span><span class="sxs-lookup"><span data-stu-id="b8348-139">Now you can create the script.</span></span> <span data-ttu-id="b8348-140">Below is an example using the Invoke-AzureADGraphAPIQuery cmdlet from the AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="b8348-140">Below is an example using the Invoke-AzureADGraphAPIQuery cmdlet from the AzureADUtils.</span></span> <span data-ttu-id="b8348-141">This cmdlet handles multi-paged results, and then sends those results to the PowerShell pipeline.</span><span class="sxs-lookup"><span data-stu-id="b8348-141">This cmdlet handles multi-paged results, and then sends those results to the PowerShell pipeline.</span></span> 

 ![Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-report-api-with-certificates/script-completed.png)

<span data-ttu-id="b8348-143">You are now ready to export to a CSV and save to a SIEM system.</span><span class="sxs-lookup"><span data-stu-id="b8348-143">You are now ready to export to a CSV and save to a SIEM system.</span></span> <span data-ttu-id="b8348-144">You can also wrap your script in a scheduled task to get Azure AD data from your tenant periodically without having to store application keys in the source code.</span><span class="sxs-lookup"><span data-stu-id="b8348-144">You can also wrap your script in a scheduled task to get Azure AD data from your tenant periodically without having to store application keys in the source code.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b8348-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="b8348-145">Next steps</span></span>
[<span data-ttu-id="b8348-146">The fundamentals of Azure identity management</span><span class="sxs-lookup"><span data-stu-id="b8348-146">The fundamentals of Azure identity management</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>









