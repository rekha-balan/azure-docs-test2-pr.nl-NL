---
title: Set up sign-up and sign-in with a Twitter account using Azure Active Directory B2C | Microsoft Docs
description: Provide sign-up and sign-in to customers with Twitter accounts in your applications using Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 07/09/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 6d8e9245e95c08aad69cd05f338b6260e554469b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867329"
---
# <a name="set-up-sign-up-and-sign-in-with-a-twitter-account-using-azure-active-directory-b2c"></a><span data-ttu-id="69256-103">Set up sign-up and sign-in with a Twitter account using Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="69256-103">Set up sign-up and sign-in with a Twitter account using Azure Active Directory B2C</span></span>

## <a name="create-a-twitter-application"></a><span data-ttu-id="69256-104">Create a Twitter application</span><span class="sxs-lookup"><span data-stu-id="69256-104">Create a Twitter application</span></span>

<span data-ttu-id="69256-105">To use a Twitter account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an application in your tenant that represents it.</span><span class="sxs-lookup"><span data-stu-id="69256-105">To use a Twitter account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an application in your tenant that represents it.</span></span> <span data-ttu-id="69256-106">If you don’t already have a Twitter account, you can get it at [https://twitter.com/signup](https://twitter.com/signup).</span><span class="sxs-lookup"><span data-stu-id="69256-106">If you don’t already have a Twitter account, you can get it at [https://twitter.com/signup](https://twitter.com/signup).</span></span>

1. <span data-ttu-id="69256-107">Sign in to the [Twitter Apps](https://apps.twitter.com/) with your Twitter credentials.</span><span class="sxs-lookup"><span data-stu-id="69256-107">Sign in to the [Twitter Apps](https://apps.twitter.com/) with your Twitter credentials.</span></span>
2. <span data-ttu-id="69256-108">Select **Create New App**.</span><span class="sxs-lookup"><span data-stu-id="69256-108">Select **Create New App**.</span></span>
3. <span data-ttu-id="69256-109">Enter the **Name**, **Description**, and **Website**.</span><span class="sxs-lookup"><span data-stu-id="69256-109">Enter the **Name**, **Description**, and **Website**.</span></span>
4. <span data-ttu-id="69256-110">Enter `https://{tenant}.b2clogin.com/te/{tenant}.onmicrosoft.com/{policyId}/oauth1/authresp` in **Callback URLs**.</span><span class="sxs-lookup"><span data-stu-id="69256-110">Enter `https://{tenant}.b2clogin.com/te/{tenant}.onmicrosoft.com/{policyId}/oauth1/authresp` in **Callback URLs**.</span></span> <span data-ttu-id="69256-111">Replace **{tenant}** with your tenant's name (for example, contosob2c) and **{policyId}** with your policy ID (for example, b2c_1_policy).</span><span class="sxs-lookup"><span data-stu-id="69256-111">Replace **{tenant}** with your tenant's name (for example, contosob2c) and **{policyId}** with your policy ID (for example, b2c_1_policy).</span></span> <span data-ttu-id="69256-112">You should add a callback URL for all policies that use the Twitter account.</span><span class="sxs-lookup"><span data-stu-id="69256-112">You should add a callback URL for all policies that use the Twitter account.</span></span> 
5. <span data-ttu-id="69256-113">Agree to the **Developer Agreement** and select **Create your Twitter application**.</span><span class="sxs-lookup"><span data-stu-id="69256-113">Agree to the **Developer Agreement** and select **Create your Twitter application**.</span></span>
7. <span data-ttu-id="69256-114">Select the **Keys and Access Tokens** tab.</span><span class="sxs-lookup"><span data-stu-id="69256-114">Select the **Keys and Access Tokens** tab.</span></span>
8. <span data-ttu-id="69256-115">Copy the value of **Consumer Key** and **Consumer Secret**.</span><span class="sxs-lookup"><span data-stu-id="69256-115">Copy the value of **Consumer Key** and **Consumer Secret**.</span></span> <span data-ttu-id="69256-116">You need both of them to configure a Twitter account as an identity provider in your tenant.</span><span class="sxs-lookup"><span data-stu-id="69256-116">You need both of them to configure a Twitter account as an identity provider in your tenant.</span></span>

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="69256-117">Configure Twitter as an identity provider in your tenant</span><span class="sxs-lookup"><span data-stu-id="69256-117">Configure Twitter as an identity provider in your tenant</span></span>

1. <span data-ttu-id="69256-118">Sign in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="69256-118">Sign in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span></span>
2. <span data-ttu-id="69256-119">Make sure you're using the directory that contains your Azure AD B2C tenant by switching to it in the top-right corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="69256-119">Make sure you're using the directory that contains your Azure AD B2C tenant by switching to it in the top-right corner of the Azure portal.</span></span> <span data-ttu-id="69256-120">Select your subscription information, and then select **Switch Directory**.</span><span class="sxs-lookup"><span data-stu-id="69256-120">Select your subscription information, and then select **Switch Directory**.</span></span> 

    ![Switch to your Azure AD B2C tenant](./media/active-directory-b2c-setup-twitter-app/switch-directories.png)

    <span data-ttu-id="69256-122">Choose the directory that contains your tenant.</span><span class="sxs-lookup"><span data-stu-id="69256-122">Choose the directory that contains your tenant.</span></span>

    ![Select directory](./media/active-directory-b2c-setup-twitter-app/select-directory.png)

3. <span data-ttu-id="69256-124">Choose **All services** in the top-left corner of the Azure portal, search for and select **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="69256-124">Choose **All services** in the top-left corner of the Azure portal, search for and select **Azure AD B2C**.</span></span>
4. <span data-ttu-id="69256-125">Select **Identity providers**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="69256-125">Select **Identity providers**, and then select **Add**.</span></span>
5. <span data-ttu-id="69256-126">Provide a **Name**.</span><span class="sxs-lookup"><span data-stu-id="69256-126">Provide a **Name**.</span></span> <span data-ttu-id="69256-127">For example, enter *Twitter*.</span><span class="sxs-lookup"><span data-stu-id="69256-127">For example, enter *Twitter*.</span></span>
6. <span data-ttu-id="69256-128">Select **Identity provider type**, select **Twitter**, and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="69256-128">Select **Identity provider type**, select **Twitter**, and click **OK**.</span></span>
7. <span data-ttu-id="69256-129">Select **Set up this identity provider** and enter the Consumer Key for the **Client ID** and the **Consumer Secret** for the **Client secret**.</span><span class="sxs-lookup"><span data-stu-id="69256-129">Select **Set up this identity provider** and enter the Consumer Key for the **Client ID** and the **Consumer Secret** for the **Client secret**.</span></span>
8. <span data-ttu-id="69256-130">Click **OK**, and then click **Create** to save your Twitter configuration.</span><span class="sxs-lookup"><span data-stu-id="69256-130">Click **OK**, and then click **Create** to save your Twitter configuration.</span></span>