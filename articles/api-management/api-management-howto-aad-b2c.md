---
title: Authorize developer accounts by using Azure Active Directory B2C - Azure API Management | Microsoft Docs
description: Learn how to authorize users by using Azure Active Directory B2C in API Management.
services: api-management
documentationcenter: API Management
author: miaojiang
manager: erikre
editor: ''
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 8722be9e58dc6b0450d3334340f43b236da66a86
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554033"
---
# <a name="how-to-authorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a><span data-ttu-id="cbcaf-103">How to authorize developer accounts by using Azure Active Directory B2C in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="cbcaf-103">How to authorize developer accounts by using Azure Active Directory B2C in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="cbcaf-104">Overview</span><span class="sxs-lookup"><span data-stu-id="cbcaf-104">Overview</span></span>
<span data-ttu-id="cbcaf-105">Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-105">Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications.</span></span> <span data-ttu-id="cbcaf-106">You can use it to manage access to your developer portal.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-106">You can use it to manage access to your developer portal.</span></span> <span data-ttu-id="cbcaf-107">This guide shows you the configuration that's required in your API Management service to integrate with Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-107">This guide shows you the configuration that's required in your API Management service to integrate with Azure Active Directory B2C.</span></span> <span data-ttu-id="cbcaf-108">For information about enabling access to the developer portal by using classic Azure Active Directory, see [How to authorize developer accounts using Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="cbcaf-108">For information about enabling access to the developer portal by using classic Azure Active Directory, see [How to authorize developer accounts using Azure Active Directory].</span></span>

> [!NOTE]
> <span data-ttu-id="cbcaf-109">To complete the steps in this guide, you must first have an Azure Active Directory B2C tenant to create an application in.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-109">To complete the steps in this guide, you must first have an Azure Active Directory B2C tenant to create an application in.</span></span> <span data-ttu-id="cbcaf-110">Also, you need to have signup and signin policies ready.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-110">Also, you need to have signup and signin policies ready.</span></span> <span data-ttu-id="cbcaf-111">For more information, see [Azure Active Directory B2C overview].</span><span class="sxs-lookup"><span data-stu-id="cbcaf-111">For more information, see [Azure Active Directory B2C overview].</span></span>

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a><span data-ttu-id="cbcaf-112">Authorize developer accounts by using Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="cbcaf-112">Authorize developer accounts by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="cbcaf-113">To get started, click **Publisher portal** in the Azure portal for your API Management service.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-113">To get started, click **Publisher portal** in the Azure portal for your API Management service.</span></span> <span data-ttu-id="cbcaf-114">This takes you to the API Management publisher portal.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-114">This takes you to the API Management publisher portal.</span></span>

   ![Publisher portal][api-management-management-console]

   > [!NOTE]
   > <span data-ttu-id="cbcaf-116">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management tutorial][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="cbcaf-116">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management tutorial][Get started with Azure API Management].</span></span>

2. <span data-ttu-id="cbcaf-117">On the **API Management** menu, click **Security**.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-117">On the **API Management** menu, click **Security**.</span></span> <span data-ttu-id="cbcaf-118">On the **Identities** tab, choose **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-118">On the **Identities** tab, choose **Azure Active Directory B2C**.</span></span>

  ![External identities 1][api-management-howto-aad-b2c-security-tab]

3. <span data-ttu-id="cbcaf-120">Make a note of the **Redirect URL** and switch over to Azure Active Directory B2C in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-120">Make a note of the **Redirect URL** and switch over to Azure Active Directory B2C in the Azure portal.</span></span>

  ![External identities 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. <span data-ttu-id="cbcaf-122">Click the **Applications** button.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-122">Click the **Applications** button.</span></span>

  ![Register a new application 1][api-management-howto-aad-b2c-portal-menu]

5. <span data-ttu-id="cbcaf-124">Click the **Add** button to create a new Azure Active Directory B2C application.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-124">Click the **Add** button to create a new Azure Active Directory B2C application.</span></span>

  ![Register a new application 2][api-management-howto-aad-b2c-add-button]

6. <span data-ttu-id="cbcaf-126">In the **New application** blade, enter a name for the application.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-126">In the **New application** blade, enter a name for the application.</span></span> <span data-ttu-id="cbcaf-127">Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-127">Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**.</span></span> <span data-ttu-id="cbcaf-128">Then copy the **Redirect URL** from the **Azure Active Directory B2C** section of the **Identities** tab in the publisher portal, and paste it into the **Reply URL** text box.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-128">Then copy the **Redirect URL** from the **Azure Active Directory B2C** section of the **Identities** tab in the publisher portal, and paste it into the **Reply URL** text box.</span></span>

  ![Register a new application 3][api-management-howto-aad-b2c-app-details]

7. <span data-ttu-id="cbcaf-130">Click the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-130">Click the **Create** button.</span></span> <span data-ttu-id="cbcaf-131">When the application is created, it appears in the **Applications** blade.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-131">When the application is created, it appears in the **Applications** blade.</span></span> <span data-ttu-id="cbcaf-132">Click the application name to see its details.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-132">Click the application name to see its details.</span></span>

  ![Register a new application 4][api-management-howto-aad-b2c-app-created]

8. <span data-ttu-id="cbcaf-134">From the **Properties** blade, copy the **Application ID** to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-134">From the **Properties** blade, copy the **Application ID** to the clipboard.</span></span>

  ![Application ID 1][api-management-howto-aad-b2c-app-id]

9. <span data-ttu-id="cbcaf-136">Switch back to the publisher portal and paste the ID into the **Client Id** text box.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-136">Switch back to the publisher portal and paste the ID into the **Client Id** text box.</span></span>

  ![Application ID 2][api-management-howto-aad-b2c-client-id]

10. <span data-ttu-id="cbcaf-138">Switch back to the Azure portal, click the **Keys** button, and then click **Generate key**.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-138">Switch back to the Azure portal, click the **Keys** button, and then click **Generate key**.</span></span> <span data-ttu-id="cbcaf-139">Click **Save** to save the configuration and display the **App key**.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-139">Click **Save** to save the configuration and display the **App key**.</span></span> <span data-ttu-id="cbcaf-140">Copy the key to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-140">Copy the key to the clipboard.</span></span>

  ![App key 1][api-management-howto-aad-b2c-app-key]

11. <span data-ttu-id="cbcaf-142">Switch back to the publisher portal and paste the key into the **Client Secret** text box.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-142">Switch back to the publisher portal and paste the key into the **Client Secret** text box.</span></span>

  ![App key 2][api-management-howto-aad-b2c-client-secret]

12. <span data-ttu-id="cbcaf-144">Specify the domain name of the Azure Active Directory B2C tenant in **Allowed Tenant**.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-144">Specify the domain name of the Azure Active Directory B2C tenant in **Allowed Tenant**.</span></span>

  ![Allowed tenant][api-management-howto-aad-b2c-allowed-tenant]

13. <span data-ttu-id="cbcaf-146">Specify the **Signup Policy** and **Signin Policy**.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-146">Specify the **Signup Policy** and **Signin Policy**.</span></span> <span data-ttu-id="cbcaf-147">Optionally, you can also provide the **Profile Editing Policy** and **Password Reset Policy**.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-147">Optionally, you can also provide the **Profile Editing Policy** and **Password Reset Policy**.</span></span>

  ![Policies][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > <span data-ttu-id="cbcaf-149">For more information on policies, see [Azure Active Directory B2C: Extensible policy framework].</span><span class="sxs-lookup"><span data-stu-id="cbcaf-149">For more information on policies, see [Azure Active Directory B2C: Extensible policy framework].</span></span>

14. <span data-ttu-id="cbcaf-150">After you've specified the desired configuration, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-150">After you've specified the desired configuration, click **Save**.</span></span>

  <span data-ttu-id="cbcaf-151">After the changes are saved, developers will be able to create new accounts and sign in to the developer portal by using Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-151">After the changes are saved, developers will be able to create new accounts and sign in to the developer portal by using Azure Active Directory B2C.</span></span>

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a><span data-ttu-id="cbcaf-152">Sign up for a developer account by using Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="cbcaf-152">Sign up for a developer account by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="cbcaf-153">To sign up for a developer account by using Azure Active Directory B2C, open a new browser window and go to the developer portal.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-153">To sign up for a developer account by using Azure Active Directory B2C, open a new browser window and go to the developer portal.</span></span> <span data-ttu-id="cbcaf-154">Click the **Sign up** button.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-154">Click the **Sign up** button.</span></span>

   ![Developer portal 1][api-management-howto-aad-b2c-dev-portal]

2. <span data-ttu-id="cbcaf-156">Choose to sign up with **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-156">Choose to sign up with **Azure Active Directory B2C**.</span></span>

   ![Developer portal 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. <span data-ttu-id="cbcaf-158">You're redirected to the signup policy that you configured in the previous section.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-158">You're redirected to the signup policy that you configured in the previous section.</span></span> <span data-ttu-id="cbcaf-159">Choose to sign up by using your email address or one of your existing social accounts.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-159">Choose to sign up by using your email address or one of your existing social accounts.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cbcaf-160">If Azure Active Directory B2C is the only option that's enabled on the **Identities** tab in the publisher portal, you'll be redirected to the signup policy directly.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-160">If Azure Active Directory B2C is the only option that's enabled on the **Identities** tab in the publisher portal, you'll be redirected to the signup policy directly.</span></span>

   ![Developer portal][api-management-howto-aad-b2c-dev-portal-b2c-options]

   <span data-ttu-id="cbcaf-162">When the signup is complete, you're redirected back to the developer portal.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-162">When the signup is complete, you're redirected back to the developer portal.</span></span> <span data-ttu-id="cbcaf-163">You're now signed in to the developer portal for your API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="cbcaf-163">You're now signed in to the developer portal for your API Management service instance.</span></span>

    ![Registration complete][api-management-registration-complete]

## <a name="next-steps"></a><span data-ttu-id="cbcaf-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="cbcaf-165">Next steps</span></span>

*  <span data-ttu-id="cbcaf-166">[Azure Active Directory B2C overview]</span><span class="sxs-lookup"><span data-stu-id="cbcaf-166">[Azure Active Directory B2C overview]</span></span>
*  <span data-ttu-id="cbcaf-167">[Azure Active Directory B2C: Extensible policy framework]</span><span class="sxs-lookup"><span data-stu-id="cbcaf-167">[Azure Active Directory B2C: Extensible policy framework]</span></span>
*  <span data-ttu-id="cbcaf-168">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="cbcaf-168">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="cbcaf-169">[Use a Google account as an identity provider in Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="cbcaf-169">[Use a Google account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="cbcaf-170">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="cbcaf-170">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="cbcaf-171">[Use a Facebook account as an identity provider in Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="cbcaf-171">[Use a Facebook account as an identity provider in Azure Active Directory B2C]</span></span>




[api-management-howto-aad-b2c-security-tab]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad-b2c/api-management-b2c-security-tab.PNG
[api-management-howto-aad-b2c-security-tab-reply-url]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad-b2c/api-management-b2c-security-tab-reply-url.PNG
[api-management-howto-aad-b2c-portal-menu]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad-b2c/api-management-b2c-portal-menu.PNG
[api-management-howto-aad-b2c-add-button]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad-b2c/api-management-b2c-add-button.PNG
[api-management-howto-aad-b2c-app-details]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad-b2c/api-management-b2c-app-details.PNG
[api-management-howto-aad-b2c-app-created]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad-b2c/api-management-b2c-app-created.PNG
[api-management-howto-aad-b2c-app-id]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad-b2c/api-management-b2c-app-id.PNG
[api-management-howto-aad-b2c-client-id]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad-b2c/api-management-b2c-client-id.PNG
[api-management-howto-aad-b2c-app-key]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad-b2c/api-management-b2c-app-key.PNG
[api-management-howto-aad-b2c-app-key-saved]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad-b2c/api-management-b2c-app-key-saved.PNG
[api-management-howto-aad-b2c-client-secret]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad-b2c/api-management-b2c-client-secret.PNG
[api-management-howto-aad-b2c-allowed-tenant]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad-b2c/api-management-b2c-allowed-tenant.PNG
[api-management-howto-aad-b2c-policies]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad-b2c/api-management-b2c-policies.PNG
[api-management-howto-aad-b2c-dev-portal]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad-b2c/api-management-b2c-dev-portal.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-button]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-button.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-options]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-options.PNG
[api-management-complete-registration]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-registration-complete.png

[api-management-management-console]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-b2c-security-tab.png
[api-management-security-aad-new]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-aad-signin.png
[api-management-aad-app-multi-tenant]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-permissions-form]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-edit-group.png

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
[Accessing the Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph
[Azure Active Directory B2C overview]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview
[How to authorize developer accounts using Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad
[Azure Active Directory B2C: Extensible policy framework]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies
[Use a Microsoft account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app
[Use a Google account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app
[Use a Facebook account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app
[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

[Log in to the Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account













































