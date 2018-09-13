---
title: Get data using the Azure AD Reporting API with certificates | Microsoft Docs
description: Explains how to use the Azure AD Reporting API with certificate credentials to get data from directories without user intervention.
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.component: report-monitor
ms.date: 05/07/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 7e2dd4c50a1d6995302c5a2a6f9b4877253d0a41
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864920"
---
# <a name="get-data-using-the-azure-active-directory-reporting-api-with-certificates"></a><span data-ttu-id="eae0c-103">Get data using the Azure Active Directory reporting API with certificates</span><span class="sxs-lookup"><span data-stu-id="eae0c-103">Get data using the Azure Active Directory reporting API with certificates</span></span>

<span data-ttu-id="eae0c-104">The [Azure Active Directory (Azure AD) reporting APIs](concept-reporting-api.md) provide you with programmatic access to the data through a set of REST-based APIs.</span><span class="sxs-lookup"><span data-stu-id="eae0c-104">The [Azure Active Directory (Azure AD) reporting APIs](concept-reporting-api.md) provide you with programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="eae0c-105">You can call these APIs from a variety of programming languages and tools.</span><span class="sxs-lookup"><span data-stu-id="eae0c-105">You can call these APIs from a variety of programming languages and tools.</span></span> <span data-ttu-id="eae0c-106">If you want to access the Azure AD Reporting API without user intervention, you can configure your access to use certificates.</span><span class="sxs-lookup"><span data-stu-id="eae0c-106">If you want to access the Azure AD Reporting API without user intervention, you can configure your access to use certificates.</span></span>

<span data-ttu-id="eae0c-107">This involves the following steps:</span><span class="sxs-lookup"><span data-stu-id="eae0c-107">This involves the following steps:</span></span>

1. [<span data-ttu-id="eae0c-108">Install the prerequisites</span><span class="sxs-lookup"><span data-stu-id="eae0c-108">Install the prerequisites</span></span>](#install-prerequisites)
2. [<span data-ttu-id="eae0c-109">Register the certificate in your app</span><span class="sxs-lookup"><span data-stu-id="eae0c-109">Register the certificate in your app</span></span>](#register-the-certificate-in-your-app)
3. [<span data-ttu-id="eae0c-110">Get an access token for MS Graph API</span><span class="sxs-lookup"><span data-stu-id="eae0c-110">Get an access token for MS Graph API</span></span>](#get-an-access-token-for-ms-graph-api)
4. [<span data-ttu-id="eae0c-111">Query the MS Graph API endpoints</span><span class="sxs-lookup"><span data-stu-id="eae0c-111">Query the MS Graph API endpoints</span></span>](#query-the-ms-graph-api-endpoints)


## <a name="install-prerequisites"></a><span data-ttu-id="eae0c-112">Install prerequisites</span><span class="sxs-lookup"><span data-stu-id="eae0c-112">Install prerequisites</span></span>

1. <span data-ttu-id="eae0c-113">First, make sure that you have completed the [prerequisites to access the Azure Active Directory reporting API](howto-configure-prerequisites-for-reporting-api.md).</span><span class="sxs-lookup"><span data-stu-id="eae0c-113">First, make sure that you have completed the [prerequisites to access the Azure Active Directory reporting API](howto-configure-prerequisites-for-reporting-api.md).</span></span> 

2. <span data-ttu-id="eae0c-114">Download and install Azure AD Powershell V2, following the instructions at [Azure Active Directory PowerShell(https://github.com/Azure/azure-docs-powershell-azuread/blob/master/docs-conceptual/azureadps-2.0/install-adv2.md)</span><span class="sxs-lookup"><span data-stu-id="eae0c-114">Download and install Azure AD Powershell V2, following the instructions at [Azure Active Directory PowerShell(https://github.com/Azure/azure-docs-powershell-azuread/blob/master/docs-conceptual/azureadps-2.0/install-adv2.md)</span></span>

3. <span data-ttu-id="eae0c-115">Install the MSCloudIDUtils from the [PowerShellGallery - MSCloudIdUtils](https://www.powershellgallery.com/packages/MSCloudIdUtils/).</span><span class="sxs-lookup"><span data-stu-id="eae0c-115">Install the MSCloudIDUtils from the [PowerShellGallery - MSCloudIdUtils](https://www.powershellgallery.com/packages/MSCloudIdUtils/).</span></span> <span data-ttu-id="eae0c-116">This module provides several utility cmdlets including:</span><span class="sxs-lookup"><span data-stu-id="eae0c-116">This module provides several utility cmdlets including:</span></span>
    - <span data-ttu-id="eae0c-117">The ADAL libraries needed for authentication</span><span class="sxs-lookup"><span data-stu-id="eae0c-117">The ADAL libraries needed for authentication</span></span>
    - <span data-ttu-id="eae0c-118">Access tokens from user, application keys, and certificates using ADAL</span><span class="sxs-lookup"><span data-stu-id="eae0c-118">Access tokens from user, application keys, and certificates using ADAL</span></span>
    - <span data-ttu-id="eae0c-119">Graph API handling paged results</span><span class="sxs-lookup"><span data-stu-id="eae0c-119">Graph API handling paged results</span></span>

4. <span data-ttu-id="eae0c-120">If it's your first time using the module run **Install-MSCloudIdUtilsModule** to complete setup, otherwise you can simply import it using the **Import-Module** Powershell command.</span><span class="sxs-lookup"><span data-stu-id="eae0c-120">If it's your first time using the module run **Install-MSCloudIdUtilsModule** to complete setup, otherwise you can simply import it using the **Import-Module** Powershell command.</span></span>

<span data-ttu-id="eae0c-121">Your session should look similar to this screen:</span><span class="sxs-lookup"><span data-stu-id="eae0c-121">Your session should look similar to this screen:</span></span>

  ![Windows Powershell](./media/tutorial-access-api-with-certificates/module-install.png)

## <a name="register-the-certificate-in-your-app"></a><span data-ttu-id="eae0c-123">Register the certificate in your app</span><span class="sxs-lookup"><span data-stu-id="eae0c-123">Register the certificate in your app</span></span>

1. <span data-ttu-id="eae0c-124">First, go to your application registration page.</span><span class="sxs-lookup"><span data-stu-id="eae0c-124">First, go to your application registration page.</span></span> <span data-ttu-id="eae0c-125">You can do this by navigating to the [Azure portal](https://portal.azure.com), clicking **Azure Active Directory**, then clicking **App registrations** and choosing your application from the list.</span><span class="sxs-lookup"><span data-stu-id="eae0c-125">You can do this by navigating to the [Azure portal](https://portal.azure.com), clicking **Azure Active Directory**, then clicking **App registrations** and choosing your application from the list.</span></span> 

2. <span data-ttu-id="eae0c-126">Then, follow the steps to [register your certificate with Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-certificate-credentials#register-your-certificate-with-azure-ad) for the application.</span><span class="sxs-lookup"><span data-stu-id="eae0c-126">Then, follow the steps to [register your certificate with Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-certificate-credentials#register-your-certificate-with-azure-ad) for the application.</span></span> 

3. <span data-ttu-id="eae0c-127">Note the Application ID, and the thumbprint of the certificate you just registered with your application.</span><span class="sxs-lookup"><span data-stu-id="eae0c-127">Note the Application ID, and the thumbprint of the certificate you just registered with your application.</span></span> <span data-ttu-id="eae0c-128">To find the thumbprint, from your application page in the portal, go to **Settings** and click **Keys**.</span><span class="sxs-lookup"><span data-stu-id="eae0c-128">To find the thumbprint, from your application page in the portal, go to **Settings** and click **Keys**.</span></span> <span data-ttu-id="eae0c-129">The thumbprint will be under the **Public Keys** list.</span><span class="sxs-lookup"><span data-stu-id="eae0c-129">The thumbprint will be under the **Public Keys** list.</span></span>

  
## <a name="get-an-access-token-for-ms-graph-api"></a><span data-ttu-id="eae0c-130">Get an access token for MS Graph API</span><span class="sxs-lookup"><span data-stu-id="eae0c-130">Get an access token for MS Graph API</span></span>

<span data-ttu-id="eae0c-131">To get an access token for the MS Graph API, use the **Get-MSCloudIdMSGraphAccessTokenFromCert** cmdlet from the MSCloudIdUtils PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="eae0c-131">To get an access token for the MS Graph API, use the **Get-MSCloudIdMSGraphAccessTokenFromCert** cmdlet from the MSCloudIdUtils PowerShell module.</span></span> 

>[!NOTE]
><span data-ttu-id="eae0c-132">You need to use the Application ID (also known as ClientID), and the certificate thumbprint of the certificate with the private key installed in your computer's certificate store (CurrentUser or LocalMachine certificate store).</span><span class="sxs-lookup"><span data-stu-id="eae0c-132">You need to use the Application ID (also known as ClientID), and the certificate thumbprint of the certificate with the private key installed in your computer's certificate store (CurrentUser or LocalMachine certificate store).</span></span>
>

 ![Azure portal](./media/tutorial-access-api-with-certificates/getaccesstoken.png)

## <a name="use-the-access-token-to-call-the-graph-api"></a><span data-ttu-id="eae0c-134">Use the access token to call the Graph API</span><span class="sxs-lookup"><span data-stu-id="eae0c-134">Use the access token to call the Graph API</span></span>

<span data-ttu-id="eae0c-135">Now, you can use the access token in your Powershell script to query the Graph API.</span><span class="sxs-lookup"><span data-stu-id="eae0c-135">Now, you can use the access token in your Powershell script to query the Graph API.</span></span> <span data-ttu-id="eae0c-136">Below is an example using the **Invoke-MSCloudIdMSGraphQuery** cmdlet from the MSCloudIDUtils to enumerate the signins or diectoryAudits endpoint.</span><span class="sxs-lookup"><span data-stu-id="eae0c-136">Below is an example using the **Invoke-MSCloudIdMSGraphQuery** cmdlet from the MSCloudIDUtils to enumerate the signins or diectoryAudits endpoint.</span></span> <span data-ttu-id="eae0c-137">This cmdlet handles multi-paged results, and then sends those results to the PowerShell pipeline.</span><span class="sxs-lookup"><span data-stu-id="eae0c-137">This cmdlet handles multi-paged results, and then sends those results to the PowerShell pipeline.</span></span>

### <a name="query-the-directoryaudits-endpoint"></a><span data-ttu-id="eae0c-138">Query the DirectoryAudits endpoint</span><span class="sxs-lookup"><span data-stu-id="eae0c-138">Query the DirectoryAudits endpoint</span></span>
 ![Azure portal](./media/tutorial-access-api-with-certificates/query-directoryAudits.png)

 ### <a name="query-the-signins-endpoint"></a><span data-ttu-id="eae0c-140">Query the SignIns endpoint</span><span class="sxs-lookup"><span data-stu-id="eae0c-140">Query the SignIns endpoint</span></span>
 ![Azure portal](./media/tutorial-access-api-with-certificates/query-signins.png)

<span data-ttu-id="eae0c-142">You can now choose to export this data to a CSV and save to a SIEM system.</span><span class="sxs-lookup"><span data-stu-id="eae0c-142">You can now choose to export this data to a CSV and save to a SIEM system.</span></span> <span data-ttu-id="eae0c-143">You can also wrap your script in a scheduled task to get Azure AD data from your tenant periodically without having to store application keys in the source code.</span><span class="sxs-lookup"><span data-stu-id="eae0c-143">You can also wrap your script in a scheduled task to get Azure AD data from your tenant periodically without having to store application keys in the source code.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="eae0c-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="eae0c-144">Next steps</span></span>

* [<span data-ttu-id="eae0c-145">Get a first impression of the reporting APIs</span><span class="sxs-lookup"><span data-stu-id="eae0c-145">Get a first impression of the reporting APIs</span></span>](concept-reporting-api.md)
* [<span data-ttu-id="eae0c-146">Audit API reference</span><span class="sxs-lookup"><span data-stu-id="eae0c-146">Audit API reference</span></span>](https://developer.microsoft.com/graph/docs/api-reference/beta/resources/directoryaudit) 
* [<span data-ttu-id="eae0c-147">Sign-in activity report API reference</span><span class="sxs-lookup"><span data-stu-id="eae0c-147">Sign-in activity report API reference</span></span>](https://developer.microsoft.com/graph/docs/api-reference/beta/resources/signin)



