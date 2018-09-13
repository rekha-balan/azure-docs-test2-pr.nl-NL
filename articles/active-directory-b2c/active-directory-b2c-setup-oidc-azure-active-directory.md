---
title: Add an Azure AD provider using built-in policies in Azure Active Directory B2C | Microsoft Docs
description: Learn how to add an Open ID Connect identity provider (Azure AD).
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 04/27/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: e09ad89f3225af9de40781fafc022c8326f80619
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866997"
---
# <a name="azure-active-directory-b2c-sign-in-using-azure-ad-accounts-through-a-built-in-policy"></a><span data-ttu-id="3d5a0-103">Azure Active Directory B2C: Sign in using Azure AD accounts through a built-in policy</span><span class="sxs-lookup"><span data-stu-id="3d5a0-103">Azure Active Directory B2C: Sign in using Azure AD accounts through a built-in policy</span></span>

>[!NOTE]
> <span data-ttu-id="3d5a0-104">This feature is in public preview.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-104">This feature is in public preview.</span></span> <span data-ttu-id="3d5a0-105">Do not use the feature in production environments.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-105">Do not use the feature in production environments.</span></span>

<span data-ttu-id="3d5a0-106">This article shows you how to enable sign-in for users from a specific Azure Active Directory (Azure AD) organization built-in policies.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-106">This article shows you how to enable sign-in for users from a specific Azure Active Directory (Azure AD) organization built-in policies.</span></span>

## <a name="create-an-azure-ad-app"></a><span data-ttu-id="3d5a0-107">Create an Azure AD app</span><span class="sxs-lookup"><span data-stu-id="3d5a0-107">Create an Azure AD app</span></span>

<span data-ttu-id="3d5a0-108">To enable sign-in for users from a specific Azure AD organization, you need to register an application within the organizational Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-108">To enable sign-in for users from a specific Azure AD organization, you need to register an application within the organizational Azure AD tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="3d5a0-109">We use "contoso.com" for the organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as the Azure AD B2C tenant in the following instructions.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-109">We use "contoso.com" for the organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as the Azure AD B2C tenant in the following instructions.</span></span>

1. <span data-ttu-id="3d5a0-110">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3d5a0-110">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="3d5a0-111">On the top bar, select your account.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-111">On the top bar, select your account.</span></span> <span data-ttu-id="3d5a0-112">From the **Directory** list, choose the organizational Azure AD tenant where you will register your application (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="3d5a0-112">From the **Directory** list, choose the organizational Azure AD tenant where you will register your application (contoso.com).</span></span>
1. <span data-ttu-id="3d5a0-113">Select **All services** in the left pane, and search for "App registrations."</span><span class="sxs-lookup"><span data-stu-id="3d5a0-113">Select **All services** in the left pane, and search for "App registrations."</span></span>
1. <span data-ttu-id="3d5a0-114">Select **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-114">Select **New application registration**.</span></span>
1. <span data-ttu-id="3d5a0-115">Enter a name for your application (for example, `Azure AD B2C App`).</span><span class="sxs-lookup"><span data-stu-id="3d5a0-115">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
1. <span data-ttu-id="3d5a0-116">Select **Web app / API** for the application type.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-116">Select **Web app / API** for the application type.</span></span>
1. <span data-ttu-id="3d5a0-117">For **Sign-on URL**, enter the following URL, where `yourtenant` is replaced by the name of your Azure AD B2C tenant (`fabrikamb2c`):</span><span class="sxs-lookup"><span data-stu-id="3d5a0-117">For **Sign-on URL**, enter the following URL, where `yourtenant` is replaced by the name of your Azure AD B2C tenant (`fabrikamb2c`):</span></span>

    >[!NOTE]
    ><span data-ttu-id="3d5a0-118">The value for "yourtenant" must be all lowercase in the **Sign-on URL**.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-118">The value for "yourtenant" must be all lowercase in the **Sign-on URL**.</span></span>

    ```Console
    https://yourtenant.b2clogin.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. <span data-ttu-id="3d5a0-119">Save the application ID, which you will use in the next section as the client ID.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-119">Save the application ID, which you will use in the next section as the client ID.</span></span>
1. <span data-ttu-id="3d5a0-120">Under the **Settings** blade, select **Keys**.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-120">Under the **Settings** blade, select **Keys**.</span></span>
1. <span data-ttu-id="3d5a0-121">Enter a **Key description** under the **Passwords** section and set the **Duration** to "Never expires".</span><span class="sxs-lookup"><span data-stu-id="3d5a0-121">Enter a **Key description** under the **Passwords** section and set the **Duration** to "Never expires".</span></span> 
1. <span data-ttu-id="3d5a0-122">Click **Save**, and note down the resulting key **Value**, which you will use in the next section as the client secret.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-122">Click **Save**, and note down the resulting key **Value**, which you will use in the next section as the client secret.</span></span>

## <a name="configure-azure-ad-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="3d5a0-123">Configure Azure AD as an identity provider in your tenant</span><span class="sxs-lookup"><span data-stu-id="3d5a0-123">Configure Azure AD as an identity provider in your tenant</span></span>

1. <span data-ttu-id="3d5a0-124">On the top bar, select your account.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-124">On the top bar, select your account.</span></span> <span data-ttu-id="3d5a0-125">From the **Directory** list, choose the Azure AD B2C tenant (fabrikamb2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="3d5a0-125">From the **Directory** list, choose the Azure AD B2C tenant (fabrikamb2c.onmicrosoft.com).</span></span>
1. <span data-ttu-id="3d5a0-126">[Navigate to the Azure AD B2C settings menu](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-126">[Navigate to the Azure AD B2C settings menu](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) in the Azure portal.</span></span>
1. <span data-ttu-id="3d5a0-127">In the Azure AD B2C settings menu, click on **Identity providers**.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-127">In the Azure AD B2C settings menu, click on **Identity providers**.</span></span>
1. <span data-ttu-id="3d5a0-128">Click **+Add** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-128">Click **+Add** at the top of the blade.</span></span>
1. <span data-ttu-id="3d5a0-129">Provide a friendly **Name** for the identity provider configuration.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-129">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="3d5a0-130">For example, enter "Contoso Azure AD".</span><span class="sxs-lookup"><span data-stu-id="3d5a0-130">For example, enter "Contoso Azure AD".</span></span>
1. <span data-ttu-id="3d5a0-131">Click **Identity provider type**, select **Open ID Connect**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-131">Click **Identity provider type**, select **Open ID Connect**, and click **OK**.</span></span>
1. <span data-ttu-id="3d5a0-132">Click **Set up this identity provider**</span><span class="sxs-lookup"><span data-stu-id="3d5a0-132">Click **Set up this identity provider**</span></span>
1. <span data-ttu-id="3d5a0-133">For **Metadata url**, enter the following URL, where `yourtenant` is replaced by the name of your Azure AD tenant (e.g. `contoso.com`):</span><span class="sxs-lookup"><span data-stu-id="3d5a0-133">For **Metadata url**, enter the following URL, where `yourtenant` is replaced by the name of your Azure AD tenant (e.g. `contoso.com`):</span></span>

    ```Console
    https://login.microsoftonline.com/yourtenant/.well-known/openid-configuration
    ```
1. <span data-ttu-id="3d5a0-134">For the **Client ID** and **Client secret**, enter the Application ID and Key from the previous section.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-134">For the **Client ID** and **Client secret**, enter the Application ID and Key from the previous section.</span></span>
1. <span data-ttu-id="3d5a0-135">Keep the default value for **Scope**, which should be set to `openid`.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-135">Keep the default value for **Scope**, which should be set to `openid`.</span></span>
1. <span data-ttu-id="3d5a0-136">Keep the default value for **Response type**, which should be set to `code`.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-136">Keep the default value for **Response type**, which should be set to `code`.</span></span>
1. <span data-ttu-id="3d5a0-137">Keep the default value for **Response mode**, which should be set to `form_post`.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-137">Keep the default value for **Response mode**, which should be set to `form_post`.</span></span>
1. <span data-ttu-id="3d5a0-138">Optionally, enter a value for **Domain** (e.g. `ContosoAD`).</span><span class="sxs-lookup"><span data-stu-id="3d5a0-138">Optionally, enter a value for **Domain** (e.g. `ContosoAD`).</span></span> <span data-ttu-id="3d5a0-139">This is the value to use when referring to this identity provider using *domain_hint* in the request.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-139">This is the value to use when referring to this identity provider using *domain_hint* in the request.</span></span> 
1. <span data-ttu-id="3d5a0-140">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-140">Click **OK**.</span></span>
1. <span data-ttu-id="3d5a0-141">Click on **Map this identity provider's claims**.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-141">Click on **Map this identity provider's claims**.</span></span>
1. <span data-ttu-id="3d5a0-142">For **User ID**, enter `oid`.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-142">For **User ID**, enter `oid`.</span></span>
1. <span data-ttu-id="3d5a0-143">For **Display Name**, enter `name`.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-143">For **Display Name**, enter `name`.</span></span>
1. <span data-ttu-id="3d5a0-144">For **Given name**, enter `given_name`.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-144">For **Given name**, enter `given_name`.</span></span>
1. <span data-ttu-id="3d5a0-145">For **Surname**, enter `family_name`.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-145">For **Surname**, enter `family_name`.</span></span>
1. <span data-ttu-id="3d5a0-146">For **Email**, enter `unique_name`</span><span class="sxs-lookup"><span data-stu-id="3d5a0-146">For **Email**, enter `unique_name`</span></span>
1. <span data-ttu-id="3d5a0-147">Click **OK**, and then **Create** to save your configuration.</span><span class="sxs-lookup"><span data-stu-id="3d5a0-147">Click **OK**, and then **Create** to save your configuration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d5a0-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="3d5a0-148">Next steps</span></span>

<span data-ttu-id="3d5a0-149">Add the newly created Azure AD identity provider to a built-in policy and provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="3d5a0-149">Add the newly created Azure AD identity provider to a built-in policy and provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
