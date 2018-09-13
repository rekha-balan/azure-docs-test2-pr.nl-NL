---
title: 'Azure Active Directory B2C: Amazon configuration | Microsoft Docs'
description: Provide sign-up and sign-in to consumers with Amazon accounts in your applications that are secured by Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: ''
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 1534f5bf90114616fe73488023dece1293818509
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552445"
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-amazon-accounts"></a><span data-ttu-id="f33fa-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Amazon accounts</span><span class="sxs-lookup"><span data-stu-id="f33fa-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Amazon accounts</span></span>
## <a name="create-an-amazon-application"></a><span data-ttu-id="f33fa-104">Create an Amazon application</span><span class="sxs-lookup"><span data-stu-id="f33fa-104">Create an Amazon application</span></span>
<span data-ttu-id="f33fa-105">To use Amazon as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an Amazon application and supply it with the right parameters.</span><span class="sxs-lookup"><span data-stu-id="f33fa-105">To use Amazon as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an Amazon application and supply it with the right parameters.</span></span> <span data-ttu-id="f33fa-106">You need an Amazon account to do this.</span><span class="sxs-lookup"><span data-stu-id="f33fa-106">You need an Amazon account to do this.</span></span> <span data-ttu-id="f33fa-107">If you don’t have one, you can get it at [http://www.amazon.com/](http://www.amazon.com/).</span><span class="sxs-lookup"><span data-stu-id="f33fa-107">If you don’t have one, you can get it at [http://www.amazon.com/](http://www.amazon.com/).</span></span>

1. <span data-ttu-id="f33fa-108">Go to the [Amazon Developer Center](https://login.amazon.com/) and sign in with your Amazon account credentials.</span><span class="sxs-lookup"><span data-stu-id="f33fa-108">Go to the [Amazon Developer Center](https://login.amazon.com/) and sign in with your Amazon account credentials.</span></span>
2. <span data-ttu-id="f33fa-109">If you have not already done so, click **Sign Up**, follow the developer registration steps, and accept the policy.</span><span class="sxs-lookup"><span data-stu-id="f33fa-109">If you have not already done so, click **Sign Up**, follow the developer registration steps, and accept the policy.</span></span>
3. <span data-ttu-id="f33fa-110">Click **Register new application**.</span><span class="sxs-lookup"><span data-stu-id="f33fa-110">Click **Register new application**.</span></span>
   
    ![Registering a new application at the Amazon website](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. <span data-ttu-id="f33fa-112">Provide application information (**Name**, **Description**, and **Privacy Notice URL**) and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f33fa-112">Provide application information (**Name**, **Description**, and **Privacy Notice URL**) and click **Save**.</span></span>
   
    ![Providing application information for registering a new application at Amazon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. <span data-ttu-id="f33fa-114">In the **Web Settings** section, copy the values of **Client ID** and **Client Secret**.</span><span class="sxs-lookup"><span data-stu-id="f33fa-114">In the **Web Settings** section, copy the values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="f33fa-115">(You need to click the **Show Secret** button to see this.) You need both of them to configure Amazon as an identity provider in your tenant.</span><span class="sxs-lookup"><span data-stu-id="f33fa-115">(You need to click the **Show Secret** button to see this.) You need both of them to configure Amazon as an identity provider in your tenant.</span></span> <span data-ttu-id="f33fa-116">Click **Edit** at the bottom of the section.</span><span class="sxs-lookup"><span data-stu-id="f33fa-116">Click **Edit** at the bottom of the section.</span></span> <span data-ttu-id="f33fa-117">**Client Secret** is an important security credential.</span><span class="sxs-lookup"><span data-stu-id="f33fa-117">**Client Secret** is an important security credential.</span></span>
   
    ![Providing Client ID and Client Secret for your new application at Amazon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. <span data-ttu-id="f33fa-119">Enter `https://login.microsoftonline.com` in the **Allowed JavaScript Origins** field and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Allowed Return URLs** field.</span><span class="sxs-lookup"><span data-stu-id="f33fa-119">Enter `https://login.microsoftonline.com` in the **Allowed JavaScript Origins** field and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Allowed Return URLs** field.</span></span> <span data-ttu-id="f33fa-120">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="f33fa-120">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="f33fa-121">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f33fa-121">Click **Save**.</span></span> <span data-ttu-id="f33fa-122">The **{tenant}** value is case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="f33fa-122">The **{tenant}** value is case-sensitive.</span></span>
   
    ![Providing JavaScript Origins and Return URLs for your new application at Amazon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-b2c/media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="f33fa-124">Configure Amazon as an identity provider in your tenant</span><span class="sxs-lookup"><span data-stu-id="f33fa-124">Configure Amazon as an identity provider in your tenant</span></span>
1. <span data-ttu-id="f33fa-125">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade) on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f33fa-125">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade) on the Azure portal.</span></span>
2. <span data-ttu-id="f33fa-126">On the B2C features blade, click **Identity providers**.</span><span class="sxs-lookup"><span data-stu-id="f33fa-126">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="f33fa-127">Click **+Add** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="f33fa-127">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="f33fa-128">Provide a friendly **Name** for the identity provider configuration.</span><span class="sxs-lookup"><span data-stu-id="f33fa-128">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="f33fa-129">For example, enter "Amzn".</span><span class="sxs-lookup"><span data-stu-id="f33fa-129">For example, enter "Amzn".</span></span>
5. <span data-ttu-id="f33fa-130">Click **Identity provider type**, select **Amazon**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f33fa-130">Click **Identity provider type**, select **Amazon**, and click **OK**.</span></span>
6. <span data-ttu-id="f33fa-131">Click **Set up this identity provider** and enter the client ID and client secret of the Amazon application that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="f33fa-131">Click **Set up this identity provider** and enter the client ID and client secret of the Amazon application that you created earlier.</span></span>
7. <span data-ttu-id="f33fa-132">Click **OK** and then click **Create** to save your Amazon configuration.</span><span class="sxs-lookup"><span data-stu-id="f33fa-132">Click **OK** and then click **Create** to save your Amazon configuration.</span></span>





