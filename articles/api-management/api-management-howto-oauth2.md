---
title: Authorize developer accounts using OAuth 2.0 in Azure API Management | Microsoft Docs
description: Learn how to authorize users using OAuth 2.0 in API Management.
services: api-management
documentationcenter: ''
author: steved0x
manager: erikre
editor: ''
ms.assetid: 78c48247-64f0-4708-b2d0-98b61a821283
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 608b7f693bafcfe4af80bdaf1caea235b71a8a2d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553413"
---
# <a name="how-to-authorize-developer-accounts-using-oauth-20-in-azure-api-management"></a><span data-ttu-id="15cba-103">How to authorize developer accounts using OAuth 2.0 in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="15cba-103">How to authorize developer accounts using OAuth 2.0 in Azure API Management</span></span>
<span data-ttu-id="15cba-104">Many APIs support [OAuth 2.0](http://oauth.net/2/) to secure the API and ensure that only valid users have access, and they can only access resources to which they're entitled.</span><span class="sxs-lookup"><span data-stu-id="15cba-104">Many APIs support [OAuth 2.0](http://oauth.net/2/) to secure the API and ensure that only valid users have access, and they can only access resources to which they're entitled.</span></span> <span data-ttu-id="15cba-105">In order to use Azure API Management's interactive Developer Console with such APIs, the service allows you to configure your service instance to work with your OAuth 2.0 enabled API.</span><span class="sxs-lookup"><span data-stu-id="15cba-105">In order to use Azure API Management's interactive Developer Console with such APIs, the service allows you to configure your service instance to work with your OAuth 2.0 enabled API.</span></span>

## <span data-ttu-id="15cba-106"><a name="prerequisites"> </a>Prerequisites</span><span class="sxs-lookup"><span data-stu-id="15cba-106"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="15cba-107">This guide shows you how to configure your API Management service instance to use OAuth 2.0 authorization for developer accounts, but does not show you how to configure an OAuth 2.0 provider.</span><span class="sxs-lookup"><span data-stu-id="15cba-107">This guide shows you how to configure your API Management service instance to use OAuth 2.0 authorization for developer accounts, but does not show you how to configure an OAuth 2.0 provider.</span></span> <span data-ttu-id="15cba-108">The configuration for each OAuth 2.0 provider is different, although the steps are similar, and the required pieces of information used in configuring OAuth 2.0 in your API Management service instance are the same.</span><span class="sxs-lookup"><span data-stu-id="15cba-108">The configuration for each OAuth 2.0 provider is different, although the steps are similar, and the required pieces of information used in configuring OAuth 2.0 in your API Management service instance are the same.</span></span> <span data-ttu-id="15cba-109">This topic shows examples using Azure Active Directory as an OAuth 2.0 provider.</span><span class="sxs-lookup"><span data-stu-id="15cba-109">This topic shows examples using Azure Active Directory as an OAuth 2.0 provider.</span></span>

> [!NOTE]
> <span data-ttu-id="15cba-110">For more information on configuring OAuth 2.0 using Azure Active Directory, see the [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet] sample.</span><span class="sxs-lookup"><span data-stu-id="15cba-110">For more information on configuring OAuth 2.0 using Azure Active Directory, see the [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet] sample.</span></span>
> 
> 

## <span data-ttu-id="15cba-111"><a name="step1"> </a>Configure an OAuth 2.0 authorization server in API Management</span><span class="sxs-lookup"><span data-stu-id="15cba-111"><a name="step1"> </a>Configure an OAuth 2.0 authorization server in API Management</span></span>
<span data-ttu-id="15cba-112">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span><span class="sxs-lookup"><span data-stu-id="15cba-112">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Publisher portal][api-management-management-console]

> [!NOTE]
> <span data-ttu-id="15cba-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="15cba-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="15cba-115">Click **Security** from the **API Management** menu on the left, click **OAuth 2.0**, and then click **Add authorization server**.</span><span class="sxs-lookup"><span data-stu-id="15cba-115">Click **Security** from the **API Management** menu on the left, click **OAuth 2.0**, and then click **Add authorization server**.</span></span>

![OAuth 2.0][api-management-oauth2]

<span data-ttu-id="15cba-117">After clicking **Add authorization server**, the new authorization server form is displayed.</span><span class="sxs-lookup"><span data-stu-id="15cba-117">After clicking **Add authorization server**, the new authorization server form is displayed.</span></span>

![New server][api-management-oauth2-server-1]

<span data-ttu-id="15cba-119">Enter a name and an optional description in the **Name** and **Description** fields.</span><span class="sxs-lookup"><span data-stu-id="15cba-119">Enter a name and an optional description in the **Name** and **Description** fields.</span></span> 

> [!NOTE]
> <span data-ttu-id="15cba-120">These fields are used to identify the OAuth 2.0 authorization server within the current API Management service instance and their values do not come from the OAuth 2.0 server.</span><span class="sxs-lookup"><span data-stu-id="15cba-120">These fields are used to identify the OAuth 2.0 authorization server within the current API Management service instance and their values do not come from the OAuth 2.0 server.</span></span>
> 
> 

<span data-ttu-id="15cba-121">Enter the **Client registration page URL**.</span><span class="sxs-lookup"><span data-stu-id="15cba-121">Enter the **Client registration page URL**.</span></span> <span data-ttu-id="15cba-122">This page is where users can create and manage their accounts, and varies depending on the OAuth 2.0 provider used.</span><span class="sxs-lookup"><span data-stu-id="15cba-122">This page is where users can create and manage their accounts, and varies depending on the OAuth 2.0 provider used.</span></span> <span data-ttu-id="15cba-123">The **Client registration page URL** points to the page that users can use to create and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span><span class="sxs-lookup"><span data-stu-id="15cba-123">The **Client registration page URL** points to the page that users can use to create and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="15cba-124">Some organizations do not configure or use this functionality even if the OAuth 2.0 provider supports it.</span><span class="sxs-lookup"><span data-stu-id="15cba-124">Some organizations do not configure or use this functionality even if the OAuth 2.0 provider supports it.</span></span> <span data-ttu-id="15cba-125">If your OAuth 2.0 provider does not have user management of accounts configured, enter a placeholder URL here such as the URL of your company, or a URL such as `https://placeholder.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="15cba-125">If your OAuth 2.0 provider does not have user management of accounts configured, enter a placeholder URL here such as the URL of your company, or a URL such as `https://placeholder.contoso.com`.</span></span>

<span data-ttu-id="15cba-126">The next section of the form contains the **Authorization code grant types**, **Authorization endpoint URL**, and **Authorization request method** settings.</span><span class="sxs-lookup"><span data-stu-id="15cba-126">The next section of the form contains the **Authorization code grant types**, **Authorization endpoint URL**, and **Authorization request method** settings.</span></span>

![New server][api-management-oauth2-server-2]

<span data-ttu-id="15cba-128">Specify the **Authorization code grant types** by checking the desired types.</span><span class="sxs-lookup"><span data-stu-id="15cba-128">Specify the **Authorization code grant types** by checking the desired types.</span></span> <span data-ttu-id="15cba-129">**Authorization code** is specified by default.</span><span class="sxs-lookup"><span data-stu-id="15cba-129">**Authorization code** is specified by default.</span></span>

<span data-ttu-id="15cba-130">Enter the **Authorization endpoint URL**.</span><span class="sxs-lookup"><span data-stu-id="15cba-130">Enter the **Authorization endpoint URL**.</span></span> <span data-ttu-id="15cba-131">For Azure Active Directory, this URL will be similar to the following URL, where `<client_id>` is replaced with the client id that identifies your application to the OAuth 2.0 server.</span><span class="sxs-lookup"><span data-stu-id="15cba-131">For Azure Active Directory, this URL will be similar to the following URL, where `<client_id>` is replaced with the client id that identifies your application to the OAuth 2.0 server.</span></span>

`https://login.windows.net/<client_id>/oauth2/authorize`

<span data-ttu-id="15cba-132">The **Authorization request method** specifies how the authorization request is sent to the OAuth 2.0 server.</span><span class="sxs-lookup"><span data-stu-id="15cba-132">The **Authorization request method** specifies how the authorization request is sent to the OAuth 2.0 server.</span></span> <span data-ttu-id="15cba-133">By default **GET** is selected.</span><span class="sxs-lookup"><span data-stu-id="15cba-133">By default **GET** is selected.</span></span>

<span data-ttu-id="15cba-134">The next section is where the **Token endpoint URL**, **Client authentication methods**, **Access token sending method**, and **Default scope** are specified.</span><span class="sxs-lookup"><span data-stu-id="15cba-134">The next section is where the **Token endpoint URL**, **Client authentication methods**, **Access token sending method**, and **Default scope** are specified.</span></span>

![New server][api-management-oauth2-server-3]

<span data-ttu-id="15cba-136">For an Azure Active Directory OAuth 2.0 server, the **Token endpoint URL** will have the following format, where `<APPID>`  has the format of `yourapp.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="15cba-136">For an Azure Active Directory OAuth 2.0 server, the **Token endpoint URL** will have the following format, where `<APPID>`  has the format of `yourapp.onmicrosoft.com`.</span></span>

`https://login.windows.net/<APPID>/oauth2/token`

<span data-ttu-id="15cba-137">The default setting for **Client authentication methods** is **Basic**, and  **Access token sending method** is **Authorization header**.</span><span class="sxs-lookup"><span data-stu-id="15cba-137">The default setting for **Client authentication methods** is **Basic**, and  **Access token sending method** is **Authorization header**.</span></span> <span data-ttu-id="15cba-138">These values are configured on this section of the form, along with the **Default scope**.</span><span class="sxs-lookup"><span data-stu-id="15cba-138">These values are configured on this section of the form, along with the **Default scope**.</span></span>

<span data-ttu-id="15cba-139">The **Client credentials** section contains the **Client ID** and **Client secret**, which are obtained during the creation and configuration process of your OAuth 2.0 server.</span><span class="sxs-lookup"><span data-stu-id="15cba-139">The **Client credentials** section contains the **Client ID** and **Client secret**, which are obtained during the creation and configuration process of your OAuth 2.0 server.</span></span> <span data-ttu-id="15cba-140">Once the **Client ID** and **Client secret** are specified, the **redirect_uri** for the **authorization code** is generated.</span><span class="sxs-lookup"><span data-stu-id="15cba-140">Once the **Client ID** and **Client secret** are specified, the **redirect_uri** for the **authorization code** is generated.</span></span> <span data-ttu-id="15cba-141">This URI is used to configure the reply URL in your OAuth 2.0 server configuration.</span><span class="sxs-lookup"><span data-stu-id="15cba-141">This URI is used to configure the reply URL in your OAuth 2.0 server configuration.</span></span>

![New server][api-management-oauth2-server-4]

<span data-ttu-id="15cba-143">If **Authorization code grant types** is set to **Resource owner password**, the **Resource owner password credentials** section is used to specify those credentials; otherwise you can leave it blank.</span><span class="sxs-lookup"><span data-stu-id="15cba-143">If **Authorization code grant types** is set to **Resource owner password**, the **Resource owner password credentials** section is used to specify those credentials; otherwise you can leave it blank.</span></span>

![New server][api-management-oauth2-server-5]

<span data-ttu-id="15cba-145">Once the form is complete, click **Save** to save the API Management OAuth 2.0 authorization server configuration.</span><span class="sxs-lookup"><span data-stu-id="15cba-145">Once the form is complete, click **Save** to save the API Management OAuth 2.0 authorization server configuration.</span></span> <span data-ttu-id="15cba-146">Once the server configuration is saved, you can configure APIs to use this configuration, as shown in the next section.</span><span class="sxs-lookup"><span data-stu-id="15cba-146">Once the server configuration is saved, you can configure APIs to use this configuration, as shown in the next section.</span></span>

## <span data-ttu-id="15cba-147"><a name="step2"> </a>Configure an API to use OAuth 2.0 user authorization</span><span class="sxs-lookup"><span data-stu-id="15cba-147"><a name="step2"> </a>Configure an API to use OAuth 2.0 user authorization</span></span>
<span data-ttu-id="15cba-148">Click **APIs** from the **API Management** menu on the left, click the name of the desired API, click **Security**, and then check the box for **OAuth 2.0**.</span><span class="sxs-lookup"><span data-stu-id="15cba-148">Click **APIs** from the **API Management** menu on the left, click the name of the desired API, click **Security**, and then check the box for **OAuth 2.0**.</span></span>

![User authorization][api-management-user-authorization]

<span data-ttu-id="15cba-150">Select the desired **Authorization server** from the drop-down list, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="15cba-150">Select the desired **Authorization server** from the drop-down list, and click **Save**.</span></span>

![User authorization][api-management-user-authorization-save]

## <span data-ttu-id="15cba-152"><a name="step3"> </a>Test the OAuth 2.0 user authorization in the Developer Portal</span><span class="sxs-lookup"><span data-stu-id="15cba-152"><a name="step3"> </a>Test the OAuth 2.0 user authorization in the Developer Portal</span></span>
<span data-ttu-id="15cba-153">Once you have configured your OAuth 2.0 authorization server and configured your API to use that server, you can test it by going to the Developer Portal and calling an API.</span><span class="sxs-lookup"><span data-stu-id="15cba-153">Once you have configured your OAuth 2.0 authorization server and configured your API to use that server, you can test it by going to the Developer Portal and calling an API.</span></span>  <span data-ttu-id="15cba-154">Click **Developer portal** in the top right menu.</span><span class="sxs-lookup"><span data-stu-id="15cba-154">Click **Developer portal** in the top right menu.</span></span>

![Developer portal][api-management-developer-portal-menu]

<span data-ttu-id="15cba-156">Click **APIs** in the top menu and select **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="15cba-156">Click **APIs** in the top menu and select **Echo API**.</span></span>

![Echo API][api-management-apis-echo-api]

> [!NOTE]
> <span data-ttu-id="15cba-158">If you have only one API configured or visible to your account, then clicking APIs takes you directly to the operations for that API.</span><span class="sxs-lookup"><span data-stu-id="15cba-158">If you have only one API configured or visible to your account, then clicking APIs takes you directly to the operations for that API.</span></span>
> 
> 

<span data-ttu-id="15cba-159">Select the **GET Resource** operation, click **Open Console**, and then select **Authorization code** from the drop-down.</span><span class="sxs-lookup"><span data-stu-id="15cba-159">Select the **GET Resource** operation, click **Open Console**, and then select **Authorization code** from the drop-down.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="15cba-161">When **Authorization code** is selected, a pop-up window is displayed with the sign-in form of the OAuth 2.0 provider.</span><span class="sxs-lookup"><span data-stu-id="15cba-161">When **Authorization code** is selected, a pop-up window is displayed with the sign-in form of the OAuth 2.0 provider.</span></span> <span data-ttu-id="15cba-162">In this example the sign-in form is provided by Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="15cba-162">In this example the sign-in form is provided by Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="15cba-163">If you have pop-ups disabled you will be prompted to enable them by the browser.</span><span class="sxs-lookup"><span data-stu-id="15cba-163">If you have pop-ups disabled you will be prompted to enable them by the browser.</span></span> <span data-ttu-id="15cba-164">After you enable them, select **Authorization code** again and the sign-in form will be displayed.</span><span class="sxs-lookup"><span data-stu-id="15cba-164">After you enable them, select **Authorization code** again and the sign-in form will be displayed.</span></span>
> 
> 

![Sign in][api-management-oauth2-signin]

<span data-ttu-id="15cba-166">Once you have signed in, the **Request headers** are populated with an `Authorization : Bearer` header that authorizes the request.</span><span class="sxs-lookup"><span data-stu-id="15cba-166">Once you have signed in, the **Request headers** are populated with an `Authorization : Bearer` header that authorizes the request.</span></span>

![Request header token][api-management-request-header-token]

<span data-ttu-id="15cba-168">At this point you can configure the desired values for the remaining parameters, and submit the request.</span><span class="sxs-lookup"><span data-stu-id="15cba-168">At this point you can configure the desired values for the remaining parameters, and submit the request.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="15cba-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="15cba-169">Next steps</span></span>
<span data-ttu-id="15cba-170">For more information about using OAuth 2.0 and API Management, see the following video and accompanying [article](api-management-howto-protect-backend-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="15cba-170">For more information about using OAuth 2.0 and API Management, see the following video and accompanying [article](api-management-howto-protect-backend-with-aad.md).</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

[api-management-management-console]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-oauth2/api-management-management-console.png
[api-management-oauth2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-oauth2/api-management-oauth2.png
[api-management-user-authorization]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-oauth2/api-management-user-authorization.png
[api-management-user-authorization-save]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-oauth2/api-management-user-authorization-save.png
[api-management-oauth2-signin]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-oauth2/api-management-oauth2-signin.png
[api-management-request-header-token]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-oauth2/api-management-request-header-token.png
[api-management-developer-portal-menu]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-oauth2/api-management-developer-portal-menu.png
[api-management-open-console]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-oauth2/api-management-open-console.png
[api-management-oauth2-server-1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-oauth2/api-management-oauth2-server-1.png
[api-management-oauth2-server-2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-oauth2/api-management-oauth2-server-2.png
[api-management-oauth2-server-3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-oauth2/api-management-oauth2-server-3.png
[api-management-oauth2-server-4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-oauth2/api-management-oauth2-server-4.png
[api-management-oauth2-server-5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-oauth2/api-management-oauth2-server-5.png
[api-management-apis-echo-api]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-oauth2/api-management-apis-echo-api.png


[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps















