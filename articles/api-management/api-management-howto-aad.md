---
title: Authorize developer accounts by using Azure Active Directory - Azure API Management | Microsoft Docs
description: Learn how to authorize users by using Azure Active Directory in API Management.
services: api-management
documentationcenter: API Management
author: miaojiang
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2018
ms.author: apimpm
ms.openlocfilehash: 4c1696fc373975eb9857c40366829fbe6a535911
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44818641"
---
# <a name="authorize-developer-accounts-by-using-azure-active-directory-in-azure-api-management"></a><span data-ttu-id="a1ac3-103">Authorize developer accounts by using Azure Active Directory in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="a1ac3-103">Authorize developer accounts by using Azure Active Directory in Azure API Management</span></span>

<span data-ttu-id="a1ac3-104">This article shows you how to enable access to the developer portal for users from Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a1ac3-104">This article shows you how to enable access to the developer portal for users from Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="a1ac3-105">This guide also shows you how to manage groups of Azure AD users by adding external groups that contain the users.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-105">This guide also shows you how to manage groups of Azure AD users by adding external groups that contain the users.</span></span>

> [!NOTE]
> <span data-ttu-id="a1ac3-106">Azure AD integration is available in the [Developer, Standard, and Premium](https://azure.microsoft.com/pricing/details/api-management/) tiers only.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-106">Azure AD integration is available in the [Developer, Standard, and Premium](https://azure.microsoft.com/pricing/details/api-management/) tiers only.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1ac3-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a1ac3-107">Prerequisites</span></span>

- <span data-ttu-id="a1ac3-108">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md).</span><span class="sxs-lookup"><span data-stu-id="a1ac3-108">Complete the following quickstart: [Create an Azure API Management instance](get-started-create-service-instance.md).</span></span>
- <span data-ttu-id="a1ac3-109">Import and publish an Azure API Management instance.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-109">Import and publish an Azure API Management instance.</span></span> <span data-ttu-id="a1ac3-110">For more information, see [Import and publish](import-and-publish.md).</span><span class="sxs-lookup"><span data-stu-id="a1ac3-110">For more information, see [Import and publish](import-and-publish.md).</span></span>

## <a name="authorize-developer-accounts-by-using-azure-ad"></a><span data-ttu-id="a1ac3-111">Authorize developer accounts by using Azure AD</span><span class="sxs-lookup"><span data-stu-id="a1ac3-111">Authorize developer accounts by using Azure AD</span></span>

1. <span data-ttu-id="a1ac3-112">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a1ac3-112">Sign in to the [Azure portal](https://portal.azure.com).</span></span> 
1. <span data-ttu-id="a1ac3-113">Select</span><span class="sxs-lookup"><span data-stu-id="a1ac3-113">Select</span></span> ![arrow](./media/api-management-howto-aad/arrow.png)<span data-ttu-id="a1ac3-115">.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-115">.</span></span>
1. <span data-ttu-id="a1ac3-116">Type **api** in the search box.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-116">Type **api** in the search box.</span></span>
1. <span data-ttu-id="a1ac3-117">Select **API Management services**.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-117">Select **API Management services**.</span></span>
1. <span data-ttu-id="a1ac3-118">Select your API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-118">Select your API Management service instance.</span></span>
1. <span data-ttu-id="a1ac3-119">Under **SECURITY**, select **Identities**.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-119">Under **SECURITY**, select **Identities**.</span></span>

1. <span data-ttu-id="a1ac3-120">Select **+Add** from the top.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-120">Select **+Add** from the top.</span></span>

    <span data-ttu-id="a1ac3-121">The **Add identity provider** pane appears on the right.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-121">The **Add identity provider** pane appears on the right.</span></span>
1. <span data-ttu-id="a1ac3-122">Under **Provider type**, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-122">Under **Provider type**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="a1ac3-123">Controls that enable you to enter other necessary information appear in the pane.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-123">Controls that enable you to enter other necessary information appear in the pane.</span></span> <span data-ttu-id="a1ac3-124">The controls include **Client ID** and **Client secret**.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-124">The controls include **Client ID** and **Client secret**.</span></span> <span data-ttu-id="a1ac3-125">(You get information about these controls later in the article.)</span><span class="sxs-lookup"><span data-stu-id="a1ac3-125">(You get information about these controls later in the article.)</span></span>
1. <span data-ttu-id="a1ac3-126">Make a note of the contents of **Redirect URL**.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-126">Make a note of the contents of **Redirect URL**.</span></span>
    
   ![Steps for adding an identity provider in the Azure portal](./media/api-management-howto-aad/api-management-with-aad001.png)  
1. <span data-ttu-id="a1ac3-128">In your browser, open a different tab.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-128">In your browser, open a different tab.</span></span> 
1. <span data-ttu-id="a1ac3-129">Go to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a1ac3-129">Go to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="a1ac3-130">Select</span><span class="sxs-lookup"><span data-stu-id="a1ac3-130">Select</span></span> ![arrow](./media/api-management-howto-aad/arrow.png)<span data-ttu-id="a1ac3-132">.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-132">.</span></span>
1. <span data-ttu-id="a1ac3-133">Type **active**.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-133">Type **active**.</span></span> <span data-ttu-id="a1ac3-134">The **Azure Active Directory** pane appears.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-134">The **Azure Active Directory** pane appears.</span></span>
1. <span data-ttu-id="a1ac3-135">Select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-135">Select **Azure Active Directory**.</span></span>
1. <span data-ttu-id="a1ac3-136">Under **MANAGE**, select **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-136">Under **MANAGE**, select **App registrations**.</span></span>
1. <span data-ttu-id="a1ac3-137">Select **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-137">Select **New application registration**.</span></span>

    ![Selections for creating a new app registration](./media/api-management-howto-aad/api-management-with-aad002.png)

    <span data-ttu-id="a1ac3-139">The **Create** pane appears on the right.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-139">The **Create** pane appears on the right.</span></span> <span data-ttu-id="a1ac3-140">That's where you enter the Azure AD app-relevant information.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-140">That's where you enter the Azure AD app-relevant information.</span></span>
1. <span data-ttu-id="a1ac3-141">Enter a name for the application.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-141">Enter a name for the application.</span></span>
1. <span data-ttu-id="a1ac3-142">For the application type, select **Web app/API**.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-142">For the application type, select **Web app/API**.</span></span>
1. <span data-ttu-id="a1ac3-143">For the sign-in URL, enter the sign-in URL of your developer portal.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-143">For the sign-in URL, enter the sign-in URL of your developer portal.</span></span> <span data-ttu-id="a1ac3-144">In this example, the sign-in URL is `https://apimwithaad.portal.azure-api.net/signin`.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-144">In this example, the sign-in URL is `https://apimwithaad.portal.azure-api.net/signin`.</span></span>
1. <span data-ttu-id="a1ac3-145">Select **Create** to create the application.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-145">Select **Create** to create the application.</span></span>
1. <span data-ttu-id="a1ac3-146">To find your app, select **App registrations** and search by name.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-146">To find your app, select **App registrations** and search by name.</span></span>

    ![Box where you search for an app](./media/api-management-howto-aad/find-your-app.png)
1. <span data-ttu-id="a1ac3-148">After the application is registered, go to **Reply URL** and make sure **Redirect URL** is set to the value that you got from step 9.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-148">After the application is registered, go to **Reply URL** and make sure **Redirect URL** is set to the value that you got from step 9.</span></span> 
1. <span data-ttu-id="a1ac3-149">If you want to configure your application (for example, change **App ID URL**), select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-149">If you want to configure your application (for example, change **App ID URL**), select **Properties**.</span></span>

    ![Opening the "Properties" pane](./media/api-management-howto-aad/api-management-with-aad004.png)

    <span data-ttu-id="a1ac3-151">If multiple Azure AD instances will be used for this application, select **Yes** for **Multi-tenanted**.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-151">If multiple Azure AD instances will be used for this application, select **Yes** for **Multi-tenanted**.</span></span> <span data-ttu-id="a1ac3-152">The default is **No**.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-152">The default is **No**.</span></span>
1. <span data-ttu-id="a1ac3-153">Set application permissions by selecting **Required permissions**.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-153">Set application permissions by selecting **Required permissions**.</span></span>
1. <span data-ttu-id="a1ac3-154">Select your application, and then select the **Read directory data** and **Sign in and read user profile** check boxes.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-154">Select your application, and then select the **Read directory data** and **Sign in and read user profile** check boxes.</span></span>

    ![Check boxes for permissions](./media/api-management-howto-aad/api-management-with-aad005.png)

1. <span data-ttu-id="a1ac3-156">Select **Grant permissions** to consent application permissions.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-156">Select **Grant permissions** to consent application permissions.</span></span>

    <span data-ttu-id="a1ac3-157">For more information about application permissions and delegated permissions, see [Accessing the Graph API][Accessing the Graph API].</span><span class="sxs-lookup"><span data-stu-id="a1ac3-157">For more information about application permissions and delegated permissions, see [Accessing the Graph API][Accessing the Graph API].</span></span>
    
1. <span data-ttu-id="a1ac3-158">In the left pane, copy the **Application ID** value.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-158">In the left pane, copy the **Application ID** value.</span></span>

    !["Application ID" value](./media/api-management-howto-aad/application-id.png)
1. <span data-ttu-id="a1ac3-160">Switch back to your API Management application.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-160">Switch back to your API Management application.</span></span> 

    <span data-ttu-id="a1ac3-161">In the **Add identity provider** window, paste the **Application ID** value in the **Client ID** box.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-161">In the **Add identity provider** window, paste the **Application ID** value in the **Client ID** box.</span></span>
1. <span data-ttu-id="a1ac3-162">Switch back to the Azure AD configuration, and select **Keys**.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-162">Switch back to the Azure AD configuration, and select **Keys**.</span></span>
1. <span data-ttu-id="a1ac3-163">Create a new key by specifying a name and duration.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-163">Create a new key by specifying a name and duration.</span></span> 
1. <span data-ttu-id="a1ac3-164">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-164">Select **Save**.</span></span> <span data-ttu-id="a1ac3-165">The key is generated.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-165">The key is generated.</span></span>

    <span data-ttu-id="a1ac3-166">Copy the key to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-166">Copy the key to the clipboard.</span></span>

    ![Selections for creating a key](./media/api-management-howto-aad/api-management-with-aad006.png)

    > [!NOTE]
    > <span data-ttu-id="a1ac3-168">Make a note of this key.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-168">Make a note of this key.</span></span> <span data-ttu-id="a1ac3-169">After you close the Azure AD configuration pane, the key cannot be displayed again.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-169">After you close the Azure AD configuration pane, the key cannot be displayed again.</span></span>
    > 
    > 

1. <span data-ttu-id="a1ac3-170">Switch back to your API Management application.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-170">Switch back to your API Management application.</span></span> 

    <span data-ttu-id="a1ac3-171">In the **Add identity provider** window, paste the key in the **Client secret** text box.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-171">In the **Add identity provider** window, paste the key in the **Client secret** text box.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a1ac3-172">Please make sure to update the **Client secret** before the key expires.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-172">Please make sure to update the **Client secret** before the key expires.</span></span> 
    >  
    >

1. <span data-ttu-id="a1ac3-173">The **Add identity provider** window also contains the **Allowed Tenants** text box.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-173">The **Add identity provider** window also contains the **Allowed Tenants** text box.</span></span> <span data-ttu-id="a1ac3-174">There, specify the domains of the Azure AD instances to which you want to grant access to the APIs of the API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-174">There, specify the domains of the Azure AD instances to which you want to grant access to the APIs of the API Management service instance.</span></span> <span data-ttu-id="a1ac3-175">You can separate multiple domains with newlines, spaces, or commas.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-175">You can separate multiple domains with newlines, spaces, or commas.</span></span>

    <span data-ttu-id="a1ac3-176">You can specify multiple domains in the **Allowed Tenants** section.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-176">You can specify multiple domains in the **Allowed Tenants** section.</span></span> <span data-ttu-id="a1ac3-177">Before any user can sign in from a different domain than the original domain where the application was registered, a global administrator of the different domain must grant permission for the application to access directory data.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-177">Before any user can sign in from a different domain than the original domain where the application was registered, a global administrator of the different domain must grant permission for the application to access directory data.</span></span> <span data-ttu-id="a1ac3-178">To grant permission, the global administrator should:</span><span class="sxs-lookup"><span data-stu-id="a1ac3-178">To grant permission, the global administrator should:</span></span>
    
    <span data-ttu-id="a1ac3-179">a.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-179">a.</span></span> <span data-ttu-id="a1ac3-180">Go to `https://<URL of your developer portal>/aadadminconsent` (for example, https://contoso.portal.azure-api.net/aadadminconsent).</span><span class="sxs-lookup"><span data-stu-id="a1ac3-180">Go to `https://<URL of your developer portal>/aadadminconsent` (for example, https://contoso.portal.azure-api.net/aadadminconsent).</span></span>
    
    <span data-ttu-id="a1ac3-181">b.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-181">b.</span></span> <span data-ttu-id="a1ac3-182">Type in the domain name of the Azure AD tenant that they want to give access to.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-182">Type in the domain name of the Azure AD tenant that they want to give access to.</span></span>
    
    <span data-ttu-id="a1ac3-183">c.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-183">c.</span></span> <span data-ttu-id="a1ac3-184">Select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-184">Select **Submit**.</span></span> 
    
    <span data-ttu-id="a1ac3-185">In the following example, a global administrator from miaoaad.onmicrosoft.com is trying to give permission to this particular developer portal.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-185">In the following example, a global administrator from miaoaad.onmicrosoft.com is trying to give permission to this particular developer portal.</span></span> 

1. <span data-ttu-id="a1ac3-186">After you specify the desired configuration, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-186">After you specify the desired configuration, select **Add**.</span></span>

    !["Add" button in "Add identity provider" pane](./media/api-management-howto-aad/api-management-with-aad007.png)

<span data-ttu-id="a1ac3-188">After the changes are saved, users in the specified Azure AD instance can sign in to the developer portal by following the steps in [Sign in to the developer portal by using an Azure AD account](#log_in_to_dev_portal).</span><span class="sxs-lookup"><span data-stu-id="a1ac3-188">After the changes are saved, users in the specified Azure AD instance can sign in to the developer portal by following the steps in [Sign in to the developer portal by using an Azure AD account](#log_in_to_dev_portal).</span></span>

![Entering the name of an Azure AD tenant](./media/api-management-howto-aad/api-management-aad-consent.png)

<span data-ttu-id="a1ac3-190">On the next screen, the global administrator is prompted to confirm giving the permission.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-190">On the next screen, the global administrator is prompted to confirm giving the permission.</span></span> 

![Confirmation of assigning permissions](./media/api-management-howto-aad/api-management-permissions-form.png)

<span data-ttu-id="a1ac3-192">If a non-global administrator tries to sign in before a global administrator grants permissions, the sign-in attempt fails and an error screen is displayed.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-192">If a non-global administrator tries to sign in before a global administrator grants permissions, the sign-in attempt fails and an error screen is displayed.</span></span>

## <a name="add-an-external-azure-ad-group"></a><span data-ttu-id="a1ac3-193">Add an external Azure AD group</span><span class="sxs-lookup"><span data-stu-id="a1ac3-193">Add an external Azure AD group</span></span>

<span data-ttu-id="a1ac3-194">After you enable access for users in an Azure AD instance, you can add Azure AD groups in API Management.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-194">After you enable access for users in an Azure AD instance, you can add Azure AD groups in API Management.</span></span> <span data-ttu-id="a1ac3-195">Then, you can more easily manage the association of the developers in the group with the desired products.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-195">Then, you can more easily manage the association of the developers in the group with the desired products.</span></span>

<span data-ttu-id="a1ac3-196">To configure an external Azure AD group, you must first configure the Azure AD instance on the **Identities** tab by following the procedure in the previous section.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-196">To configure an external Azure AD group, you must first configure the Azure AD instance on the **Identities** tab by following the procedure in the previous section.</span></span> 

<span data-ttu-id="a1ac3-197">You add external Azure AD groups from the **Groups** tab of your API Management instance.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-197">You add external Azure AD groups from the **Groups** tab of your API Management instance.</span></span>

1. <span data-ttu-id="a1ac3-198">Select the **Groups** tab.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-198">Select the **Groups** tab.</span></span>
1. <span data-ttu-id="a1ac3-199">Select the **Add AAD group** button.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-199">Select the **Add AAD group** button.</span></span>
   <span data-ttu-id="a1ac3-200">!["Add AAD group" button](./media/api-management-howto-aad/api-management-with-aad008.png)</span><span class="sxs-lookup"><span data-stu-id="a1ac3-200">!["Add AAD group" button](./media/api-management-howto-aad/api-management-with-aad008.png)</span></span>
1. <span data-ttu-id="a1ac3-201">Select the group that you want to add.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-201">Select the group that you want to add.</span></span>
1. <span data-ttu-id="a1ac3-202">Press the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-202">Press the **Select** button.</span></span>

<span data-ttu-id="a1ac3-203">After you add an external Azure AD group, you can review and configure its properties.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-203">After you add an external Azure AD group, you can review and configure its properties.</span></span> <span data-ttu-id="a1ac3-204">Select the name of the group from the **Groups** tab. From here, you can edit **Name** and **Description** information for the group.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-204">Select the name of the group from the **Groups** tab. From here, you can edit **Name** and **Description** information for the group.</span></span>
 
<span data-ttu-id="a1ac3-205">Users from the configured Azure AD instance can now sign in to the developer portal.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-205">Users from the configured Azure AD instance can now sign in to the developer portal.</span></span> <span data-ttu-id="a1ac3-206">They can view and subscribe to any groups for which they have visibility.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-206">They can view and subscribe to any groups for which they have visibility.</span></span>

## <a name="a-idlogintodevportalsign-in-to-the-developer-portal-by-using-an-azure-ad-account"></a><span data-ttu-id="a1ac3-207"><a id="log_in_to_dev_portal"/>Sign in to the developer portal by using an Azure AD account</span><span class="sxs-lookup"><span data-stu-id="a1ac3-207"><a id="log_in_to_dev_portal"/>Sign in to the developer portal by using an Azure AD account</span></span>

<span data-ttu-id="a1ac3-208">To sign in to the developer portal by using an Azure AD account that you configured in the previous sections:</span><span class="sxs-lookup"><span data-stu-id="a1ac3-208">To sign in to the developer portal by using an Azure AD account that you configured in the previous sections:</span></span>

1. <span data-ttu-id="a1ac3-209">Open a new browser window by using the sign-in URL from the Active Directory application configuration, and select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-209">Open a new browser window by using the sign-in URL from the Active Directory application configuration, and select **Azure Active Directory**.</span></span>

   ![Sign-in page][api-management-dev-portal-signin]

1. <span data-ttu-id="a1ac3-211">Enter the credentials of one of the users in Azure AD, and select **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-211">Enter the credentials of one of the users in Azure AD, and select **Sign in**.</span></span>

   ![Signing in with username and password][api-management-aad-signin]

1. <span data-ttu-id="a1ac3-213">You might be prompted with a registration form if any additional information is required.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-213">You might be prompted with a registration form if any additional information is required.</span></span> <span data-ttu-id="a1ac3-214">Complete the registration form, and select **Sign up**.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-214">Complete the registration form, and select **Sign up**.</span></span>

   !["Sign up" button on registration form][api-management-complete-registration]

<span data-ttu-id="a1ac3-216">Your user is now signed in to the developer portal for your API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="a1ac3-216">Your user is now signed in to the developer portal for your API Management service instance.</span></span>

![Developer portal after registration is complete][api-management-registration-complete]

[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png

[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: get-started-create-service-instance.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: get-started-create-service-instance.md

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing the Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

[Sign in to the developer portal by using an Azure AD account]: #Sign-in-to-the-developer-portal-by-using-an-Azure-AD-account
