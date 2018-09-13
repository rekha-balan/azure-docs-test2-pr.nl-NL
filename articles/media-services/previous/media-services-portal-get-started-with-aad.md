---
title: Get started with Azure AD authentication by using the Azure portal| Microsoft Docs
description: Learn how to use the Azure portal to access Azure Active Directory (Azure AD) authentication to consume the Azure Media Services API.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 6267dd8dca4c932d4a4d96b34a8eaa26f6a59c20
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856303"
---
# <a name="get-started-with-azure-ad-authentication-by-using-the-azure-portal"></a><span data-ttu-id="81cf7-103">Get started with Azure AD authentication by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="81cf7-103">Get started with Azure AD authentication by using the Azure portal</span></span>

<span data-ttu-id="81cf7-104">Learn how to use the Azure portal to access Azure Active Directory (Azure AD) authentication to access the Azure Media Services API.</span><span class="sxs-lookup"><span data-stu-id="81cf7-104">Learn how to use the Azure portal to access Azure Active Directory (Azure AD) authentication to access the Azure Media Services API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81cf7-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="81cf7-105">Prerequisites</span></span>

- <span data-ttu-id="81cf7-106">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="81cf7-106">An Azure account.</span></span> <span data-ttu-id="81cf7-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="81cf7-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="81cf7-108">A Media Services account.</span><span class="sxs-lookup"><span data-stu-id="81cf7-108">A Media Services account.</span></span> <span data-ttu-id="81cf7-109">For more information, see [Create an Azure Media Services account by using the Azure portal](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="81cf7-109">For more information, see [Create an Azure Media Services account by using the Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="81cf7-110">Make sure you review the [Accessing Azure Media Services API with Azure AD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="81cf7-110">Make sure you review the [Accessing Azure Media Services API with Azure AD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="81cf7-111">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span><span class="sxs-lookup"><span data-stu-id="81cf7-111">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span></span>

- <span data-ttu-id="81cf7-112">**User authentication**.</span><span class="sxs-lookup"><span data-stu-id="81cf7-112">**User authentication**.</span></span> <span data-ttu-id="81cf7-113">Authenticate a person who is using the app to interact with Media Services resources.</span><span class="sxs-lookup"><span data-stu-id="81cf7-113">Authenticate a person who is using the app to interact with Media Services resources.</span></span> <span data-ttu-id="81cf7-114">The interactive application should first prompt the user for credentials.</span><span class="sxs-lookup"><span data-stu-id="81cf7-114">The interactive application should first prompt the user for credentials.</span></span> <span data-ttu-id="81cf7-115">An example is a management console app used by authorized users to monitor encoding jobs or live streaming.</span><span class="sxs-lookup"><span data-stu-id="81cf7-115">An example is a management console app used by authorized users to monitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="81cf7-116">**Service principal authentication**.</span><span class="sxs-lookup"><span data-stu-id="81cf7-116">**Service principal authentication**.</span></span> <span data-ttu-id="81cf7-117">Authenticate a service.</span><span class="sxs-lookup"><span data-stu-id="81cf7-117">Authenticate a service.</span></span> <span data-ttu-id="81cf7-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs: web apps, function apps, logic apps, APIs, or a microservice.</span><span class="sxs-lookup"><span data-stu-id="81cf7-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs: web apps, function apps, logic apps, APIs, or a microservice.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="81cf7-119">Currently, Media Services supports the Azure Access Control service authentication model.</span><span class="sxs-lookup"><span data-stu-id="81cf7-119">Currently, Media Services supports the Azure Access Control service authentication model.</span></span> <span data-ttu-id="81cf7-120">However, Access Control authorization will be deprecated on June 1, 2018.</span><span class="sxs-lookup"><span data-stu-id="81cf7-120">However, Access Control authorization will be deprecated on June 1, 2018.</span></span> <span data-ttu-id="81cf7-121">We recommend that you migrate to the Azure AD authentication model as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="81cf7-121">We recommend that you migrate to the Azure AD authentication model as soon as possible.</span></span>

## <a name="select-the-authentication-method"></a><span data-ttu-id="81cf7-122">Select the authentication method</span><span class="sxs-lookup"><span data-stu-id="81cf7-122">Select the authentication method</span></span>

1. <span data-ttu-id="81cf7-123">In the [Azure portal](https://portal.azure.com/), select your Media Services account.</span><span class="sxs-lookup"><span data-stu-id="81cf7-123">In the [Azure portal](https://portal.azure.com/), select your Media Services account.</span></span>
2. <span data-ttu-id="81cf7-124">Select how to connect to the Media Services API.</span><span class="sxs-lookup"><span data-stu-id="81cf7-124">Select how to connect to the Media Services API.</span></span>

    ![Select connection method page](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a><span data-ttu-id="81cf7-126">User authentication</span><span class="sxs-lookup"><span data-stu-id="81cf7-126">User authentication</span></span>

<span data-ttu-id="81cf7-127">To connect to the Media Services API by using the user authentication option, the client app needs to request an Azure AD token that has the following parameters:</span><span class="sxs-lookup"><span data-stu-id="81cf7-127">To connect to the Media Services API by using the user authentication option, the client app needs to request an Azure AD token that has the following parameters:</span></span>  

* <span data-ttu-id="81cf7-128">Azure AD tenant endpoint</span><span class="sxs-lookup"><span data-stu-id="81cf7-128">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="81cf7-129">Media Services resource URI</span><span class="sxs-lookup"><span data-stu-id="81cf7-129">Media Services resource URI</span></span>
* <span data-ttu-id="81cf7-130">Media Services (native) application client ID</span><span class="sxs-lookup"><span data-stu-id="81cf7-130">Media Services (native) application client ID</span></span> 
* <span data-ttu-id="81cf7-131">Media Services (native) application redirect URI</span><span class="sxs-lookup"><span data-stu-id="81cf7-131">Media Services (native) application redirect URI</span></span> 
* <span data-ttu-id="81cf7-132">Resource URI for REST Media Services</span><span class="sxs-lookup"><span data-stu-id="81cf7-132">Resource URI for REST Media Services</span></span>

<span data-ttu-id="81cf7-133">You can get the values for these parameters on the **Media Services API with user authentication** page.</span><span class="sxs-lookup"><span data-stu-id="81cf7-133">You can get the values for these parameters on the **Media Services API with user authentication** page.</span></span> 

![Connect with user authentication page](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

<span data-ttu-id="81cf7-135">If you connect to the Media Services API by using the Media Services Microsoft .NET SDK, the required values are available to you as part of the SDK.</span><span class="sxs-lookup"><span data-stu-id="81cf7-135">If you connect to the Media Services API by using the Media Services Microsoft .NET SDK, the required values are available to you as part of the SDK.</span></span> <span data-ttu-id="81cf7-136">For more information, see [Use Azure AD authentication to access the Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="81cf7-136">For more information, see [Use Azure AD authentication to access the Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="81cf7-137">If you're not using the Media Services .NET client SDK, you must manually create an Azure AD token request by using the parameters discussed earlier.</span><span class="sxs-lookup"><span data-stu-id="81cf7-137">If you're not using the Media Services .NET client SDK, you must manually create an Azure AD token request by using the parameters discussed earlier.</span></span> <span data-ttu-id="81cf7-138">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="81cf7-138">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

## <a name="service-principal-authentication"></a><span data-ttu-id="81cf7-139">Service principal authentication</span><span class="sxs-lookup"><span data-stu-id="81cf7-139">Service principal authentication</span></span>

<span data-ttu-id="81cf7-140">To connect to the Media Services API by using the service principal option, your middle-tier app (web API or web application) needs to request an Azure AD token that has the following parameters:</span><span class="sxs-lookup"><span data-stu-id="81cf7-140">To connect to the Media Services API by using the service principal option, your middle-tier app (web API or web application) needs to request an Azure AD token that has the following parameters:</span></span>  

* <span data-ttu-id="81cf7-141">Azure AD tenant endpoint</span><span class="sxs-lookup"><span data-stu-id="81cf7-141">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="81cf7-142">Media Services resource URI</span><span class="sxs-lookup"><span data-stu-id="81cf7-142">Media Services resource URI</span></span> 
* <span data-ttu-id="81cf7-143">Resource URI for REST Media Services</span><span class="sxs-lookup"><span data-stu-id="81cf7-143">Resource URI for REST Media Services</span></span>
* <span data-ttu-id="81cf7-144">Azure AD application values: the **client ID** and **client secret**</span><span class="sxs-lookup"><span data-stu-id="81cf7-144">Azure AD application values: the **client ID** and **client secret**</span></span>

<span data-ttu-id="81cf7-145">You can get the values for these parameters on the **Connect to Media Services API with service principal** page.</span><span class="sxs-lookup"><span data-stu-id="81cf7-145">You can get the values for these parameters on the **Connect to Media Services API with service principal** page.</span></span> <span data-ttu-id="81cf7-146">Use this page to create a new Azure AD application or to select an existing one.</span><span class="sxs-lookup"><span data-stu-id="81cf7-146">Use this page to create a new Azure AD application or to select an existing one.</span></span> <span data-ttu-id="81cf7-147">After you select the Azure AD app, you can get the client ID (Application ID) and generate the client secret (key) values.</span><span class="sxs-lookup"><span data-stu-id="81cf7-147">After you select the Azure AD app, you can get the client ID (Application ID) and generate the client secret (key) values.</span></span> 

![Connect with service principal page](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

<span data-ttu-id="81cf7-149">When the **Service Principal** blade opens, the first Azure AD application that meets the following criteria is selected:</span><span class="sxs-lookup"><span data-stu-id="81cf7-149">When the **Service Principal** blade opens, the first Azure AD application that meets the following criteria is selected:</span></span>

- <span data-ttu-id="81cf7-150">It is a registered Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="81cf7-150">It is a registered Azure AD application.</span></span>
- <span data-ttu-id="81cf7-151">It has Contributor or Owner Role-Based Access Control permissions on the account.</span><span class="sxs-lookup"><span data-stu-id="81cf7-151">It has Contributor or Owner Role-Based Access Control permissions on the account.</span></span>

<span data-ttu-id="81cf7-152">After you create or select an Azure AD app, you can create and copy a client secret (key) and the client ID (Application ID).</span><span class="sxs-lookup"><span data-stu-id="81cf7-152">After you create or select an Azure AD app, you can create and copy a client secret (key) and the client ID (Application ID).</span></span> <span data-ttu-id="81cf7-153">The client secret and client ID are required to get the access token in this scenario.</span><span class="sxs-lookup"><span data-stu-id="81cf7-153">The client secret and client ID are required to get the access token in this scenario.</span></span>

<span data-ttu-id="81cf7-154">If you don't have permissions to create Azure AD apps in your domain, the Azure AD app controls of the blade are not shown, and a warning message is displayed.</span><span class="sxs-lookup"><span data-stu-id="81cf7-154">If you don't have permissions to create Azure AD apps in your domain, the Azure AD app controls of the blade are not shown, and a warning message is displayed.</span></span>

<span data-ttu-id="81cf7-155">If you connect to the Media Services API by using the Media Services .NET SDK, see [Use Azure AD authentication to access the Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="81cf7-155">If you connect to the Media Services API by using the Media Services .NET SDK, see [Use Azure AD authentication to access the Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="81cf7-156">If you are not using the Media Services .NET client SDK, you must manually create an Azure AD token request using the parameters discussed earlier.</span><span class="sxs-lookup"><span data-stu-id="81cf7-156">If you are not using the Media Services .NET client SDK, you must manually create an Azure AD token request using the parameters discussed earlier.</span></span> <span data-ttu-id="81cf7-157">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="81cf7-157">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

### <a name="get-the-client-id-and-client-secret"></a><span data-ttu-id="81cf7-158">Get the client ID and client secret</span><span class="sxs-lookup"><span data-stu-id="81cf7-158">Get the client ID and client secret</span></span>

<span data-ttu-id="81cf7-159">After you select an existing Azure AD app or select the option to create a new one, the following buttons appear:</span><span class="sxs-lookup"><span data-stu-id="81cf7-159">After you select an existing Azure AD app or select the option to create a new one, the following buttons appear:</span></span>

![Manage permissions button and Manage application button](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

<span data-ttu-id="81cf7-161">To open the Azure AD application blade, click **Manage application**.</span><span class="sxs-lookup"><span data-stu-id="81cf7-161">To open the Azure AD application blade, click **Manage application**.</span></span> <span data-ttu-id="81cf7-162">On the **Manage application** blade, you can get the app's client ID (Application ID).</span><span class="sxs-lookup"><span data-stu-id="81cf7-162">On the **Manage application** blade, you can get the app's client ID (Application ID).</span></span> <span data-ttu-id="81cf7-163">To generate a client secret (key), select **Keys**.</span><span class="sxs-lookup"><span data-stu-id="81cf7-163">To generate a client secret (key), select **Keys**.</span></span>

![Manage application blade Keys option](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-the-application"></a><span data-ttu-id="81cf7-165">Manage permissions and the application</span><span class="sxs-lookup"><span data-stu-id="81cf7-165">Manage permissions and the application</span></span>

<span data-ttu-id="81cf7-166">After you select the Azure AD application, you can manage the application and permissions.</span><span class="sxs-lookup"><span data-stu-id="81cf7-166">After you select the Azure AD application, you can manage the application and permissions.</span></span> <span data-ttu-id="81cf7-167">To set up your Azure AD application to access other applications, click **Manage permissions**.</span><span class="sxs-lookup"><span data-stu-id="81cf7-167">To set up your Azure AD application to access other applications, click **Manage permissions**.</span></span> <span data-ttu-id="81cf7-168">For management tasks, such as changing keys and reply URLs, or to edit the application’s manifest, click **Manage application**.</span><span class="sxs-lookup"><span data-stu-id="81cf7-168">For management tasks, such as changing keys and reply URLs, or to edit the application’s manifest, click **Manage application**.</span></span>

### <a name="edit-the-apps-settings-or-manifest"></a><span data-ttu-id="81cf7-169">Edit the app's settings or manifest</span><span class="sxs-lookup"><span data-stu-id="81cf7-169">Edit the app's settings or manifest</span></span>

<span data-ttu-id="81cf7-170">To edit the app's settings or manifest, click **Manage application**.</span><span class="sxs-lookup"><span data-stu-id="81cf7-170">To edit the app's settings or manifest, click **Manage application**.</span></span>

![Manage application page](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a><span data-ttu-id="81cf7-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="81cf7-172">Next steps</span></span>

<span data-ttu-id="81cf7-173">Get started with [uploading files to your account](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="81cf7-173">Get started with [uploading files to your account](media-services-portal-upload-files.md).</span></span>
