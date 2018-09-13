---
title: Set up sign-up and sign-in with a GitHub account using Azure Active Directory B2C | Microsoft Docs
description: Provide sign-up and sign-in to customers with GitHub accounts in your applications using Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 07/09/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 11f3f190c0f55e45c549a8bd1de35f78eb7b752d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871345"
---
# <a name="set-up-sign-up-and-sign-in-with-a-github-account-using-azure-active-directory-b2c"></a><span data-ttu-id="20814-103">Set up sign-up and sign-in with a GitHub account using Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="20814-103">Set up sign-up and sign-in with a GitHub account using Azure Active Directory B2C</span></span>

> [!NOTE]
> <span data-ttu-id="20814-104">This feature is in preview.</span><span class="sxs-lookup"><span data-stu-id="20814-104">This feature is in preview.</span></span>
> 

<span data-ttu-id="20814-105">To use a Github account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an application in your tenant that represents it.</span><span class="sxs-lookup"><span data-stu-id="20814-105">To use a Github account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an application in your tenant that represents it.</span></span> <span data-ttu-id="20814-106">If you don’t already have a Github account, you can get it at [https://www.github.com/](https://www.github.com/).</span><span class="sxs-lookup"><span data-stu-id="20814-106">If you don’t already have a Github account, you can get it at [https://www.github.com/](https://www.github.com/).</span></span>

## <a name="create-a-github-oauth-application"></a><span data-ttu-id="20814-107">Create a GitHub OAuth application</span><span class="sxs-lookup"><span data-stu-id="20814-107">Create a GitHub OAuth application</span></span>

1. <span data-ttu-id="20814-108">Sign in to the [GitHub Developer](https://github.com/settings/developers) website with your GitHub credentials.</span><span class="sxs-lookup"><span data-stu-id="20814-108">Sign in to the [GitHub Developer](https://github.com/settings/developers) website with your GitHub credentials.</span></span>
2. <span data-ttu-id="20814-109">Select **OAuth Apps** and then select **Register a new application**.</span><span class="sxs-lookup"><span data-stu-id="20814-109">Select **OAuth Apps** and then select **Register a new application**.</span></span>
3. <span data-ttu-id="20814-110">Enter an **Application name** and your **Homepage URL**.</span><span class="sxs-lookup"><span data-stu-id="20814-110">Enter an **Application name** and your **Homepage URL**.</span></span>
4. <span data-ttu-id="20814-111">Enter `https://{tenant}.b2clogin.com/te/{tenant}.onmicrosoft.com/oauth2/authresp` in **Authorization callback URL**.</span><span class="sxs-lookup"><span data-stu-id="20814-111">Enter `https://{tenant}.b2clogin.com/te/{tenant}.onmicrosoft.com/oauth2/authresp` in **Authorization callback URL**.</span></span> <span data-ttu-id="20814-112">Replace **{tenant}** with your Azure AD B2C tenant's name (for example, contosob2c).</span><span class="sxs-lookup"><span data-stu-id="20814-112">Replace **{tenant}** with your Azure AD B2C tenant's name (for example, contosob2c).</span></span>
5. <span data-ttu-id="20814-113">Click **Register application**.</span><span class="sxs-lookup"><span data-stu-id="20814-113">Click **Register application**.</span></span>
6. <span data-ttu-id="20814-114">Copy the values of **Client ID** and **Client Secret**.</span><span class="sxs-lookup"><span data-stu-id="20814-114">Copy the values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="20814-115">You need both to add the identity provider to your tenant.</span><span class="sxs-lookup"><span data-stu-id="20814-115">You need both to add the identity provider to your tenant.</span></span>

## <a name="configure-a-github-account-as-an-identity-provider"></a><span data-ttu-id="20814-116">Configure a GitHub account as an identity provider</span><span class="sxs-lookup"><span data-stu-id="20814-116">Configure a GitHub account as an identity provider</span></span>

1. <span data-ttu-id="20814-117">Sign in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="20814-117">Sign in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span></span>
2. <span data-ttu-id="20814-118">Make sure you're using the directory that contains your Azure AD B2C tenant by switching to it in the top-right corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="20814-118">Make sure you're using the directory that contains your Azure AD B2C tenant by switching to it in the top-right corner of the Azure portal.</span></span> <span data-ttu-id="20814-119">Select your subscription information, and then select **Switch Directory**.</span><span class="sxs-lookup"><span data-stu-id="20814-119">Select your subscription information, and then select **Switch Directory**.</span></span> 

    ![Switch to your Azure AD B2C tenant](./media/active-directory-b2c-setup-github-app/switch-directories.png)

    <span data-ttu-id="20814-121">Choose the directory that contains your tenant.</span><span class="sxs-lookup"><span data-stu-id="20814-121">Choose the directory that contains your tenant.</span></span>

    ![Select directory](./media/active-directory-b2c-setup-github-app/select-directory.png)

3. <span data-ttu-id="20814-123">Choose **All services** in the top-left corner of the Azure portal, search for and select **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="20814-123">Choose **All services** in the top-left corner of the Azure portal, search for and select **Azure AD B2C**.</span></span>
4. <span data-ttu-id="20814-124">Select **Identity providers**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="20814-124">Select **Identity providers**, and then select **Add**.</span></span>
5. <span data-ttu-id="20814-125">Provide a **Name**.</span><span class="sxs-lookup"><span data-stu-id="20814-125">Provide a **Name**.</span></span> <span data-ttu-id="20814-126">For example, enter *Github*.</span><span class="sxs-lookup"><span data-stu-id="20814-126">For example, enter *Github*.</span></span>
6. <span data-ttu-id="20814-127">Select **Identity provider type**, select **Github (Preview)**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="20814-127">Select **Identity provider type**, select **Github (Preview)**, and click **OK**.</span></span>
7. <span data-ttu-id="20814-128">Select **Set up this identity provider** and enter the Client Id that you recorded earlier as the **Client ID** and enter the Client Secret that you recorded as the **Client secret** of the Github account application that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="20814-128">Select **Set up this identity provider** and enter the Client Id that you recorded earlier as the **Client ID** and enter the Client Secret that you recorded as the **Client secret** of the Github account application that you created earlier.</span></span>
8. <span data-ttu-id="20814-129">Click **OK** and then click **Create** to save your Github account configuration.</span><span class="sxs-lookup"><span data-stu-id="20814-129">Click **OK** and then click **Create** to save your Github account configuration.</span></span>