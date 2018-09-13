---
title: 'Azure Active Directory B2C: Facebook configuration | Microsoft Docs'
description: Provide sign-up and sign-in to consumers with Facebook accounts in your applications that are secured by Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: ''
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: b875f235-a1d2-4abb-b9f0-b89beac38a32
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 0aee82ed47ecce21e3506e25898c08a84d0afa29
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550083"
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-facebook-accounts"></a><span data-ttu-id="4efd1-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Facebook accounts</span><span class="sxs-lookup"><span data-stu-id="4efd1-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Facebook accounts</span></span>
## <a name="create-a-facebook-application"></a><span data-ttu-id="4efd1-104">Create a Facebook application</span><span class="sxs-lookup"><span data-stu-id="4efd1-104">Create a Facebook application</span></span>
<span data-ttu-id="4efd1-105">To use Facebook as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Facebook application and supply it with the right parameters.</span><span class="sxs-lookup"><span data-stu-id="4efd1-105">To use Facebook as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Facebook application and supply it with the right parameters.</span></span> <span data-ttu-id="4efd1-106">You need a Facebook account to do this.</span><span class="sxs-lookup"><span data-stu-id="4efd1-106">You need a Facebook account to do this.</span></span> <span data-ttu-id="4efd1-107">If you don’t have one, you can get it at [https://www.facebook.com/](https://www.facebook.com/).</span><span class="sxs-lookup"><span data-stu-id="4efd1-107">If you don’t have one, you can get it at [https://www.facebook.com/](https://www.facebook.com/).</span></span>

1. <span data-ttu-id="4efd1-108">Go to the [Facebook for developers](https://developers.facebook.com/) website and sign in with your Facebook account credentials.</span><span class="sxs-lookup"><span data-stu-id="4efd1-108">Go to the [Facebook for developers](https://developers.facebook.com/) website and sign in with your Facebook account credentials.</span></span>
2. <span data-ttu-id="4efd1-109">If you have not already done so, you need to register as a Facebook developer.</span><span class="sxs-lookup"><span data-stu-id="4efd1-109">If you have not already done so, you need to register as a Facebook developer.</span></span> <span data-ttu-id="4efd1-110">To do this, click **Register** (on the upper-right corner of the page), accept Facebook's policies, and complete the registration steps.</span><span class="sxs-lookup"><span data-stu-id="4efd1-110">To do this, click **Register** (on the upper-right corner of the page), accept Facebook's policies, and complete the registration steps.</span></span>
3. <span data-ttu-id="4efd1-111">Click **My Apps** and then click **Add a New App**.</span><span class="sxs-lookup"><span data-stu-id="4efd1-111">Click **My Apps** and then click **Add a New App**.</span></span> 
4. <span data-ttu-id="4efd1-112">In the form, provide a **Display Name** and a valid **Contact Email**.</span><span class="sxs-lookup"><span data-stu-id="4efd1-112">In the form, provide a **Display Name** and a valid **Contact Email**.</span></span>
5. <span data-ttu-id="4efd1-113">Click **Create App ID**.</span><span class="sxs-lookup"><span data-stu-id="4efd1-113">Click **Create App ID**.</span></span> <span data-ttu-id="4efd1-114">This may require you to accept Facebook platform policies and complete an online security check.</span><span class="sxs-lookup"><span data-stu-id="4efd1-114">This may require you to accept Facebook platform policies and complete an online security check.</span></span>
6. <span data-ttu-id="4efd1-115">In the left column, click **Settings** and then select **Basic** if not selected already.</span><span class="sxs-lookup"><span data-stu-id="4efd1-115">In the left column, click **Settings** and then select **Basic** if not selected already.</span></span>
7. <span data-ttu-id="4efd1-116">Select a **Category**.</span><span class="sxs-lookup"><span data-stu-id="4efd1-116">Select a **Category**.</span></span> 
8. <span data-ttu-id="4efd1-117">Click **+ Add Platform** and select **Website**.</span><span class="sxs-lookup"><span data-stu-id="4efd1-117">Click **+ Add Platform** and select **Website**.</span></span>
   
    ![Facebook - Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - Settings - Website](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-fb-app/fb-website.png)
9. <span data-ttu-id="4efd1-120">Enter `https://login.microsoftonline.com/` in the **Site URL** field and then click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="4efd1-120">Enter `https://login.microsoftonline.com/` in the **Site URL** field and then click **Save Changes**.</span></span>
   
    ![Facebook - Site URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. <span data-ttu-id="4efd1-122">Copy the value of **App ID**.</span><span class="sxs-lookup"><span data-stu-id="4efd1-122">Copy the value of **App ID**.</span></span> <span data-ttu-id="4efd1-123">Click **Show** and copy the value of **App Secret**.</span><span class="sxs-lookup"><span data-stu-id="4efd1-123">Click **Show** and copy the value of **App Secret**.</span></span> <span data-ttu-id="4efd1-124">You will need both of them to configure Facebook as an identity provider in your tenant.</span><span class="sxs-lookup"><span data-stu-id="4efd1-124">You will need both of them to configure Facebook as an identity provider in your tenant.</span></span> <span data-ttu-id="4efd1-125">**App Secret** is an important security credential.</span><span class="sxs-lookup"><span data-stu-id="4efd1-125">**App Secret** is an important security credential.</span></span>
   
    ![Facebook - App ID & App Secret](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. <span data-ttu-id="4efd1-127">Click **+ Add Product** on the left navigation and then the **Get Started** button next to **Facebook Login**.</span><span class="sxs-lookup"><span data-stu-id="4efd1-127">Click **+ Add Product** on the left navigation and then the **Get Started** button next to **Facebook Login**.</span></span>
   
    ![Facebook - Facebook Login](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-fb-app/fb-login.png)
12. <span data-ttu-id="4efd1-129">Select **Website** and then enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Valid OAuth redirect URIs** field in the **Client OAuth Settings** section.</span><span class="sxs-lookup"><span data-stu-id="4efd1-129">Select **Website** and then enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Valid OAuth redirect URIs** field in the **Client OAuth Settings** section.</span></span> <span data-ttu-id="4efd1-130">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="4efd1-130">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="4efd1-131">Click **Save Changes** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="4efd1-131">Click **Save Changes** at the bottom of the page.</span></span>
    
    ![Facebook - OAuth Redirect URI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
13. <span data-ttu-id="4efd1-133">To make your Facebook application usable by Azure AD B2C, you need to make it publicly available.</span><span class="sxs-lookup"><span data-stu-id="4efd1-133">To make your Facebook application usable by Azure AD B2C, you need to make it publicly available.</span></span> <span data-ttu-id="4efd1-134">You can do this by clicking **App Review** on the left navigation and by turning the switch at the top of the page to **YES** and clicking **Confirm**.</span><span class="sxs-lookup"><span data-stu-id="4efd1-134">You can do this by clicking **App Review** on the left navigation and by turning the switch at the top of the page to **YES** and clicking **Confirm**.</span></span>
    
    ![Facebook - App public](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="4efd1-136">Configure Facebook as an identity provider in your tenant</span><span class="sxs-lookup"><span data-stu-id="4efd1-136">Configure Facebook as an identity provider in your tenant</span></span>
1. <span data-ttu-id="4efd1-137">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade) on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4efd1-137">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade) on the Azure portal.</span></span>
2. <span data-ttu-id="4efd1-138">On the B2C features blade, click **Identity providers**.</span><span class="sxs-lookup"><span data-stu-id="4efd1-138">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="4efd1-139">Click **+Add** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="4efd1-139">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="4efd1-140">Provide a friendly **Name** for the identity provider configuration.</span><span class="sxs-lookup"><span data-stu-id="4efd1-140">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="4efd1-141">For example, enter "FB".</span><span class="sxs-lookup"><span data-stu-id="4efd1-141">For example, enter "FB".</span></span>
5. <span data-ttu-id="4efd1-142">Click **Identity provider type**, select **Facebook**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4efd1-142">Click **Identity provider type**, select **Facebook**, and click **OK**.</span></span>
6. <span data-ttu-id="4efd1-143">Click **Set up this identity provider** and enter the app ID and app secret (of the Facebook application that you created earlier) in the **Client ID** and **Client secret** fields respectively.</span><span class="sxs-lookup"><span data-stu-id="4efd1-143">Click **Set up this identity provider** and enter the app ID and app secret (of the Facebook application that you created earlier) in the **Client ID** and **Client secret** fields respectively.</span></span>
7. <span data-ttu-id="4efd1-144">Click **OK**, and then click **Create** to save your Facebook configuration.</span><span class="sxs-lookup"><span data-stu-id="4efd1-144">Click **OK**, and then click **Create** to save your Facebook configuration.</span></span>








