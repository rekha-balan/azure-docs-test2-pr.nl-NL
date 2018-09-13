---
title: Authorize developer accounts using Azure Active Directory - Azure API Management | Microsoft Docs
description: Learn how to authorize users using Azure Active Directory in API Management.
services: api-management
documentationcenter: API Management
author: steved0x
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
ms.openlocfilehash: ee50940a2c1e19c41aac620d6e4142cc1851547f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562936"
---
# <a name="how-to-authorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a><span data-ttu-id="46102-103">How to authorize developer accounts using Azure Active Directory in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="46102-103">How to authorize developer accounts using Azure Active Directory in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="46102-104">Overview</span><span class="sxs-lookup"><span data-stu-id="46102-104">Overview</span></span>
<span data-ttu-id="46102-105">This guide shows you how to enable access to the developer portal for users from Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46102-105">This guide shows you how to enable access to the developer portal for users from Azure Active Directory.</span></span> <span data-ttu-id="46102-106">This guide also shows you how to manage groups of Azure Active Directory users by adding external groups that contain the users of an Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46102-106">This guide also shows you how to manage groups of Azure Active Directory users by adding external groups that contain the users of an Azure Active Directory.</span></span>

> <span data-ttu-id="46102-107">To complete the steps in this guide you must first have an Azure Active Directory in which to create an application.</span><span class="sxs-lookup"><span data-stu-id="46102-107">To complete the steps in this guide you must first have an Azure Active Directory in which to create an application.</span></span>
> 
> 

## <a name="how-to-authorize-developer-accounts-using-azure-active-directory"></a><span data-ttu-id="46102-108">How to authorize developer accounts using Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="46102-108">How to authorize developer accounts using Azure Active Directory</span></span>
<span data-ttu-id="46102-109">To get started, click **Publisher portal** in the Azure portal for your API Management service.</span><span class="sxs-lookup"><span data-stu-id="46102-109">To get started, click **Publisher portal** in the Azure portal for your API Management service.</span></span> <span data-ttu-id="46102-110">This takes you to the API Management publisher portal.</span><span class="sxs-lookup"><span data-stu-id="46102-110">This takes you to the API Management publisher portal.</span></span>

![Publisher portal][api-management-management-console]

> <span data-ttu-id="46102-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="46102-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="46102-113">Click **Security** from the **API Management** menu on the left and click **External Identities**.</span><span class="sxs-lookup"><span data-stu-id="46102-113">Click **Security** from the **API Management** menu on the left and click **External Identities**.</span></span>

![External Identities][api-management-security-external-identities]

<span data-ttu-id="46102-115">Click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46102-115">Click **Azure Active Directory**.</span></span> <span data-ttu-id="46102-116">Make a note of the **Redirect URL** and switch over to your Azure Active Directory in the Azure Classic Portal.</span><span class="sxs-lookup"><span data-stu-id="46102-116">Make a note of the **Redirect URL** and switch over to your Azure Active Directory in the Azure Classic Portal.</span></span>

![External Identities][api-management-security-aad-new]

<span data-ttu-id="46102-118">Click the **Add** button to create a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span><span class="sxs-lookup"><span data-stu-id="46102-118">Click the **Add** button to create a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Add new Azure Active Directory application][api-management-new-aad-application-menu]

<span data-ttu-id="46102-120">Enter a name for the application, select **Web application and/or Web API**, and click the next button.</span><span class="sxs-lookup"><span data-stu-id="46102-120">Enter a name for the application, select **Web application and/or Web API**, and click the next button.</span></span>

![New Azure Active Directory application][api-management-new-aad-application-1]

<span data-ttu-id="46102-122">For **Sign-on URL**, enter the sign-on URL of your developer portal.</span><span class="sxs-lookup"><span data-stu-id="46102-122">For **Sign-on URL**, enter the sign-on URL of your developer portal.</span></span> <span data-ttu-id="46102-123">In this example, the **Sign-on URL** is `https://aad03.portal.current.int-azure-api.net/signin`.</span><span class="sxs-lookup"><span data-stu-id="46102-123">In this example, the **Sign-on URL** is `https://aad03.portal.current.int-azure-api.net/signin`.</span></span> 

<span data-ttu-id="46102-124">For the **App ID URL**, enter either the default domain or a custom domain for the Azure Active Directory, and append a unique string to it.</span><span class="sxs-lookup"><span data-stu-id="46102-124">For the **App ID URL**, enter either the default domain or a custom domain for the Azure Active Directory, and append a unique string to it.</span></span> <span data-ttu-id="46102-125">In this example, the default domain of **https://contoso5api.onmicrosoft.com** is used with the suffix of **/api** specified.</span><span class="sxs-lookup"><span data-stu-id="46102-125">In this example, the default domain of **https://contoso5api.onmicrosoft.com** is used with the suffix of **/api** specified.</span></span>

![New Azure Active Directory application properties][api-management-new-aad-application-2]

<span data-ttu-id="46102-127">Click the check button to save and create the application, and switch to the **Configure** tab to configure the new application.</span><span class="sxs-lookup"><span data-stu-id="46102-127">Click the check button to save and create the application, and switch to the **Configure** tab to configure the new application.</span></span>

![New Azure Active Directory application created][api-management-new-aad-app-created]

<span data-ttu-id="46102-129">If multiple Azure Active Directories are going to be used for this application, click **Yes** for **Application is multi-tenant**.</span><span class="sxs-lookup"><span data-stu-id="46102-129">If multiple Azure Active Directories are going to be used for this application, click **Yes** for **Application is multi-tenant**.</span></span> <span data-ttu-id="46102-130">The default is **No**.</span><span class="sxs-lookup"><span data-stu-id="46102-130">The default is **No**.</span></span>

![Application is multi-tenant][api-management-aad-app-multi-tenant]

<span data-ttu-id="46102-132">Copy the **Redirect URL** from the **Azure Active Directory** section of the **External Identities** tab in the publisher portal and paste it into the **Reply URL** text box.</span><span class="sxs-lookup"><span data-stu-id="46102-132">Copy the **Redirect URL** from the **Azure Active Directory** section of the **External Identities** tab in the publisher portal and paste it into the **Reply URL** text box.</span></span> 

![Reply URL][api-management-aad-reply-url]

<span data-ttu-id="46102-134">Scroll to the bottom of the configure tab, select the **Application Permissions** drop-down, and check **Read directory data**.</span><span class="sxs-lookup"><span data-stu-id="46102-134">Scroll to the bottom of the configure tab, select the **Application Permissions** drop-down, and check **Read directory data**.</span></span>

![Application Permissions][api-management-aad-app-permissions]

<span data-ttu-id="46102-136">Select the **Delegate Permissions** drop-down, and check **Enable sign-on and read users' profiles**.</span><span class="sxs-lookup"><span data-stu-id="46102-136">Select the **Delegate Permissions** drop-down, and check **Enable sign-on and read users' profiles**.</span></span>

![Delegated Permissions][api-management-aad-delegated-permissions]

> <span data-ttu-id="46102-138">For more information about application and delegated permissions, see [Accessing the Graph API][Accessing the Graph API].</span><span class="sxs-lookup"><span data-stu-id="46102-138">For more information about application and delegated permissions, see [Accessing the Graph API][Accessing the Graph API].</span></span>
> 
> 

<span data-ttu-id="46102-139">Copy the **Client Id** to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="46102-139">Copy the **Client Id** to the clipboard.</span></span>

![Client Id][api-management-aad-app-client-id]

<span data-ttu-id="46102-141">Switch back to the publisher portal and paste in the **Client Id** copied from the Azure Active Directory application configuration.</span><span class="sxs-lookup"><span data-stu-id="46102-141">Switch back to the publisher portal and paste in the **Client Id** copied from the Azure Active Directory application configuration.</span></span>

![Client Id][api-management-client-id]

<span data-ttu-id="46102-143">Switch back to the Azure Active Directory configuration, and click the **Select duration** drop-down in the **Keys** section and specify an interval.</span><span class="sxs-lookup"><span data-stu-id="46102-143">Switch back to the Azure Active Directory configuration, and click the **Select duration** drop-down in the **Keys** section and specify an interval.</span></span> <span data-ttu-id="46102-144">In this example, **1 year** is used.</span><span class="sxs-lookup"><span data-stu-id="46102-144">In this example, **1 year** is used.</span></span>

![Key][api-management-aad-key-before-save]

<span data-ttu-id="46102-146">Click **Save** to save the configuration and display the key.</span><span class="sxs-lookup"><span data-stu-id="46102-146">Click **Save** to save the configuration and display the key.</span></span> <span data-ttu-id="46102-147">Copy the key to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="46102-147">Copy the key to the clipboard.</span></span>

> <span data-ttu-id="46102-148">Make a note of this key.</span><span class="sxs-lookup"><span data-stu-id="46102-148">Make a note of this key.</span></span> <span data-ttu-id="46102-149">Once you close the Azure Active Directory configuration window, the key cannot be displayed again.</span><span class="sxs-lookup"><span data-stu-id="46102-149">Once you close the Azure Active Directory configuration window, the key cannot be displayed again.</span></span>
> 
> 

![Key][api-management-aad-key-after-save]

<span data-ttu-id="46102-151">Switch back to the publisher portal and paste the key into the **Client Secret** text box.</span><span class="sxs-lookup"><span data-stu-id="46102-151">Switch back to the publisher portal and paste the key into the **Client Secret** text box.</span></span>

![Client Secret][api-management-client-secret]

<span data-ttu-id="46102-153">**Allowed Tenants** specifies which directories have access to the APIs of the API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="46102-153">**Allowed Tenants** specifies which directories have access to the APIs of the API Management service instance.</span></span> <span data-ttu-id="46102-154">Specify the domains of the Azure Active Directory instances to which you want to grant access.</span><span class="sxs-lookup"><span data-stu-id="46102-154">Specify the domains of the Azure Active Directory instances to which you want to grant access.</span></span> <span data-ttu-id="46102-155">You can separate multiple domains with newlines, spaces, or commas.</span><span class="sxs-lookup"><span data-stu-id="46102-155">You can separate multiple domains with newlines, spaces, or commas.</span></span>

![Allowed tenants][api-management-client-allowed-tenants]


<span data-ttu-id="46102-157">Once the desired configuration is specified, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="46102-157">Once the desired configuration is specified, click **Save**.</span></span>

![Save][api-management-client-allowed-tenants-save]

<span data-ttu-id="46102-159">Once the changes are saved, the users in the specified Azure Active Directory can sign in to the Developer portal by following the steps in [Log in to the Developer portal using an Azure Active Directory account][Log in to the Developer portal using an Azure Active Directory account].</span><span class="sxs-lookup"><span data-stu-id="46102-159">Once the changes are saved, the users in the specified Azure Active Directory can sign in to the Developer portal by following the steps in [Log in to the Developer portal using an Azure Active Directory account][Log in to the Developer portal using an Azure Active Directory account].</span></span>

<span data-ttu-id="46102-160">Multiple domains can be specified in the **Allowed Tenants** section.</span><span class="sxs-lookup"><span data-stu-id="46102-160">Multiple domains can be specified in the **Allowed Tenants** section.</span></span> <span data-ttu-id="46102-161">Before any user can log in from a different domain than the original domain where the application was registered, a global administrator of the different domain must grant permission for the application to access directory data.</span><span class="sxs-lookup"><span data-stu-id="46102-161">Before any user can log in from a different domain than the original domain where the application was registered, a global administrator of the different domain must grant permission for the application to access directory data.</span></span> <span data-ttu-id="46102-162">To grant permission, the global administrator should go to `https://<URL of your developer portal>/aadadminconsent` (for example, https://contoso.portal.azure-api.net/aadadminconsent), type in the domain name of the Active Directory tenant they want to give access to and click Submit.</span><span class="sxs-lookup"><span data-stu-id="46102-162">To grant permission, the global administrator should go to `https://<URL of your developer portal>/aadadminconsent` (for example, https://contoso.portal.azure-api.net/aadadminconsent), type in the domain name of the Active Directory tenant they want to give access to and click Submit.</span></span> <span data-ttu-id="46102-163">In the following example, a global administrator from `miaoaad.onmicrosoft.com` is trying to give permission to this particular developer portal.</span><span class="sxs-lookup"><span data-stu-id="46102-163">In the following example, a global administrator from `miaoaad.onmicrosoft.com` is trying to give permission to this particular developer portal.</span></span> 

![Permissions][api-management-aad-consent]

<span data-ttu-id="46102-165">In the next screen, the global administrator will be prompted to confirm giving the permission.</span><span class="sxs-lookup"><span data-stu-id="46102-165">In the next screen, the global administrator will be prompted to confirm giving the permission.</span></span> 

![Permissions][api-management-permissions-form]

> <span data-ttu-id="46102-167">If a non-global administrator tries to log in before permissions are granted by a global administrator, the login attempt fails and an error screen is displayed.</span><span class="sxs-lookup"><span data-stu-id="46102-167">If a non-global administrator tries to log in before permissions are granted by a global administrator, the login attempt fails and an error screen is displayed.</span></span>
> 
> 

## <a name="how-to-add-an-external-azure-active-directory-group"></a><span data-ttu-id="46102-168">How to add an external Azure Active Directory Group</span><span class="sxs-lookup"><span data-stu-id="46102-168">How to add an external Azure Active Directory Group</span></span>
<span data-ttu-id="46102-169">After enabling access for users in an Azure Active Directory, you can add Azure Active Directory groups into API Management to more easily manage the association of the developers in the group with the desired products.</span><span class="sxs-lookup"><span data-stu-id="46102-169">After enabling access for users in an Azure Active Directory, you can add Azure Active Directory groups into API Management to more easily manage the association of the developers in the group with the desired products.</span></span>

> <span data-ttu-id="46102-170">To configure an external Azure Active Directory group, the Azure Active Directory must first be configured in the Identities tab by following the procedure in the previous section.</span><span class="sxs-lookup"><span data-stu-id="46102-170">To configure an external Azure Active Directory group, the Azure Active Directory must first be configured in the Identities tab by following the procedure in the previous section.</span></span> 
> 
> 

<span data-ttu-id="46102-171">External Azure Active Directory groups are added from the **Visibility** tab of the product for which you wish to grant access to the group.</span><span class="sxs-lookup"><span data-stu-id="46102-171">External Azure Active Directory groups are added from the **Visibility** tab of the product for which you wish to grant access to the group.</span></span> <span data-ttu-id="46102-172">Click **Products**, and then click the name of the desired product.</span><span class="sxs-lookup"><span data-stu-id="46102-172">Click **Products**, and then click the name of the desired product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="46102-174">Switch to the **Visibility** tab, and click **Add Groups from Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46102-174">Switch to the **Visibility** tab, and click **Add Groups from Azure Active Directory**.</span></span>

![Add groups][api-management-add-groups]

<span data-ttu-id="46102-176">Select the **Azure Active Directory Tenant** from the drop-down list, and then type the name of the desired group in the **Groups** to be added text box.</span><span class="sxs-lookup"><span data-stu-id="46102-176">Select the **Azure Active Directory Tenant** from the drop-down list, and then type the name of the desired group in the **Groups** to be added text box.</span></span>

![Select group][api-management-select-group]

<span data-ttu-id="46102-178">This group name can be found in the **Groups** list for your Azure Active Directory, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="46102-178">This group name can be found in the **Groups** list for your Azure Active Directory, as shown in the following example.</span></span>

![Azure Active Directory Groups List][api-management-aad-groups-list]

<span data-ttu-id="46102-180">Click **Add** to validate the group name and add the group.</span><span class="sxs-lookup"><span data-stu-id="46102-180">Click **Add** to validate the group name and add the group.</span></span> <span data-ttu-id="46102-181">In this example, the **Contoso 5 Developers** external group is added.</span><span class="sxs-lookup"><span data-stu-id="46102-181">In this example, the **Contoso 5 Developers** external group is added.</span></span> 

![Group added][api-management-aad-group-added]

<span data-ttu-id="46102-183">Click **Save** to save the new group selection.</span><span class="sxs-lookup"><span data-stu-id="46102-183">Click **Save** to save the new group selection.</span></span>

<span data-ttu-id="46102-184">Once an Azure Active Directory group has been configured from one product, it is available to be checked on the **Visibility** tab for the other products in the API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="46102-184">Once an Azure Active Directory group has been configured from one product, it is available to be checked on the **Visibility** tab for the other products in the API Management service instance.</span></span>

<span data-ttu-id="46102-185">To review and configure the properties for external groups once they have been added, click the name of the group from the **Groups** tab.</span><span class="sxs-lookup"><span data-stu-id="46102-185">To review and configure the properties for external groups once they have been added, click the name of the group from the **Groups** tab.</span></span>

![Manage groups][api-management-groups]

<span data-ttu-id="46102-187">From here you can edit the **Name** and the **Description** of the group.</span><span class="sxs-lookup"><span data-stu-id="46102-187">From here you can edit the **Name** and the **Description** of the group.</span></span>

![Edit group][api-management-edit-group]

<span data-ttu-id="46102-189">Users from the configured Azure Active Directory can sign in to the Developer portal and view and subscribe to any groups for which they have visibility by following the instructions in the following section.</span><span class="sxs-lookup"><span data-stu-id="46102-189">Users from the configured Azure Active Directory can sign in to the Developer portal and view and subscribe to any groups for which they have visibility by following the instructions in the following section.</span></span>

## <a name="how-to-log-in-to-the-developer-portal-using-an-azure-active-directory-account"></a><span data-ttu-id="46102-190">How to log in to the Developer portal using an Azure Active Directory account</span><span class="sxs-lookup"><span data-stu-id="46102-190">How to log in to the Developer portal using an Azure Active Directory account</span></span>
<span data-ttu-id="46102-191">To log into the Developer portal using an Azure Active Directory account configured in the previous sections, open a new browser window using the **Sign-on URL** from the Active Directory application configuration, and click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46102-191">To log into the Developer portal using an Azure Active Directory account configured in the previous sections, open a new browser window using the **Sign-on URL** from the Active Directory application configuration, and click **Azure Active Directory**.</span></span>

![Developer Portal][api-management-dev-portal-signin]

<span data-ttu-id="46102-193">Enter the credentials of one of the users in your Azure Active Directory, and click **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="46102-193">Enter the credentials of one of the users in your Azure Active Directory, and click **Sign in**.</span></span>

![Sign in][api-management-aad-signin]

<span data-ttu-id="46102-195">You may be prompted with a registration form if any additional information is required.</span><span class="sxs-lookup"><span data-stu-id="46102-195">You may be prompted with a registration form if any additional information is required.</span></span> <span data-ttu-id="46102-196">Complete the registration form and click **Sign up**.</span><span class="sxs-lookup"><span data-stu-id="46102-196">Complete the registration form and click **Sign up**.</span></span>

![Registration][api-management-complete-registration]

<span data-ttu-id="46102-198">Your user is now logged into the developer portal for your API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="46102-198">Your user is now logged into the developer portal for your API Management service instance.</span></span>

![Registration Complete][api-management-registration-complete]

[api-management-management-console]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-security-external-identities.png
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
[api-management-complete-registration]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-registration-complete.png
[api-management-aad-app-multi-tenant]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-aad-consent]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-aad/api-management-aad-consent.png
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

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

[Log in to the Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
































