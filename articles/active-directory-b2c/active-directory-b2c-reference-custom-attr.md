---
title: Define custom attributes in Azure Active Directory B2C | Microsoft Docs
description: Define custom attributes for your application in Azure Active Directory B2C to collect information about your customers.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 07/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: d5ef77ab0bbf00d4ddbb05b7a38516e3c3e7d800
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44774936"
---
# <a name="define-custom-attributes-in-azure-active-directory-b2c"></a><span data-ttu-id="81893-103">Define custom attributes in Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="81893-103">Define custom attributes in Azure Active Directory B2C</span></span>

 <span data-ttu-id="81893-104">Every customer-facing application has unique requirements for the information that needs to be collected.</span><span class="sxs-lookup"><span data-stu-id="81893-104">Every customer-facing application has unique requirements for the information that needs to be collected.</span></span> <span data-ttu-id="81893-105">Your Azure Active Directory (Azure AD) B2C tenant comes with a built-in set of information stored in attributes, such as Given Name, Surname, City, and Postal Code.</span><span class="sxs-lookup"><span data-stu-id="81893-105">Your Azure Active Directory (Azure AD) B2C tenant comes with a built-in set of information stored in attributes, such as Given Name, Surname, City, and Postal Code.</span></span> <span data-ttu-id="81893-106">With Azure AD B2C, you can extend the set of attributes stored on each customer account.</span><span class="sxs-lookup"><span data-stu-id="81893-106">With Azure AD B2C, you can extend the set of attributes stored on each customer account.</span></span> 
 
 <span data-ttu-id="81893-107">You can create custom attributes in the [Azure portal](https://portal.azure.com/) and use them in your sign-up policies, sign-up or sign-in policies, or profile editing policies.</span><span class="sxs-lookup"><span data-stu-id="81893-107">You can create custom attributes in the [Azure portal](https://portal.azure.com/) and use them in your sign-up policies, sign-up or sign-in policies, or profile editing policies.</span></span> <span data-ttu-id="81893-108">You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="81893-108">You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span> <span data-ttu-id="81893-109">Custom attributes in Azure AD B2C use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-directory-schema-extensions).</span><span class="sxs-lookup"><span data-stu-id="81893-109">Custom attributes in Azure AD B2C use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-directory-schema-extensions).</span></span>

## <a name="create-a-custom-attribute"></a><span data-ttu-id="81893-110">Create a custom attribute</span><span class="sxs-lookup"><span data-stu-id="81893-110">Create a custom attribute</span></span>

1. <span data-ttu-id="81893-111">Sign in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="81893-111">Sign in to the [Azure portal](https://portal.azure.com/) as the global administrator of your Azure AD B2C tenant.</span></span>
2. <span data-ttu-id="81893-112">Make sure you're using the directory that contains your Azure AD B2C tenant by switching to it in the top-right corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="81893-112">Make sure you're using the directory that contains your Azure AD B2C tenant by switching to it in the top-right corner of the Azure portal.</span></span> <span data-ttu-id="81893-113">Select your subscription information, and then select **Switch Directory**.</span><span class="sxs-lookup"><span data-stu-id="81893-113">Select your subscription information, and then select **Switch Directory**.</span></span> 

    ![Switch to your Azure AD B2C tenant](./media/active-directory-b2c-reference-custom-attr/switch-directories.png)

    <span data-ttu-id="81893-115">Choose the directory that contains your tenant.</span><span class="sxs-lookup"><span data-stu-id="81893-115">Choose the directory that contains your tenant.</span></span>

    ![Select directory](./media/active-directory-b2c-reference-custom-attr/select-directory.png)

3. <span data-ttu-id="81893-117">Choose **All services** in the top-left corner of the Azure portal, search for and select **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="81893-117">Choose **All services** in the top-left corner of the Azure portal, search for and select **Azure AD B2C**.</span></span>
4. <span data-ttu-id="81893-118">Select **User attributes**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="81893-118">Select **User attributes**, and then select **Add**.</span></span>
5. <span data-ttu-id="81893-119">Provide a **Name** for the custom attribute (for example, "ShoeSize")</span><span class="sxs-lookup"><span data-stu-id="81893-119">Provide a **Name** for the custom attribute (for example, "ShoeSize")</span></span>
6. <span data-ttu-id="81893-120">Choose a **Data Type**.</span><span class="sxs-lookup"><span data-stu-id="81893-120">Choose a **Data Type**.</span></span> <span data-ttu-id="81893-121">Only **String**, **Boolean**, and **Int** are available.</span><span class="sxs-lookup"><span data-stu-id="81893-121">Only **String**, **Boolean**, and **Int** are available.</span></span>
7. <span data-ttu-id="81893-122">Optionally, enter a **Description** for informational purposes.</span><span class="sxs-lookup"><span data-stu-id="81893-122">Optionally, enter a **Description** for informational purposes.</span></span> 
8. <span data-ttu-id="81893-123">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="81893-123">Click **Create**.</span></span>

<span data-ttu-id="81893-124">The custom attribute is now available in the list of **User attributes** and for use in your policies.</span><span class="sxs-lookup"><span data-stu-id="81893-124">The custom attribute is now available in the list of **User attributes** and for use in your policies.</span></span> <span data-ttu-id="81893-125">A custom attribute is only created the first time it is used in any policy, and not when you add it to the list of **User attributes**.</span><span class="sxs-lookup"><span data-stu-id="81893-125">A custom attribute is only created the first time it is used in any policy, and not when you add it to the list of **User attributes**.</span></span>

## <a name="use-a-custom-attribute-in-your-policy"></a><span data-ttu-id="81893-126">Use a custom attribute in your policy</span><span class="sxs-lookup"><span data-stu-id="81893-126">Use a custom attribute in your policy</span></span>

1. <span data-ttu-id="81893-127">In your Azure AD B2C tenant, select **Sign-up or sign-in policies**.</span><span class="sxs-lookup"><span data-stu-id="81893-127">In your Azure AD B2C tenant, select **Sign-up or sign-in policies**.</span></span>
2. <span data-ttu-id="81893-128">Select your policy (for example, "B2C_1_SignupSignin") to open it.</span><span class="sxs-lookup"><span data-stu-id="81893-128">Select your policy (for example, "B2C_1_SignupSignin") to open it.</span></span> 
3. <span data-ttu-id="81893-129">Click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="81893-129">Click **Edit**.</span></span>
4. <span data-ttu-id="81893-130">Select **Sign-up attributes** and then select the custom attribute (for example, "ShoeSize").</span><span class="sxs-lookup"><span data-stu-id="81893-130">Select **Sign-up attributes** and then select the custom attribute (for example, "ShoeSize").</span></span> <span data-ttu-id="81893-131">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="81893-131">Click **OK**.</span></span>
5. <span data-ttu-id="81893-132">Select **Application claims** and then select the custom attribute.</span><span class="sxs-lookup"><span data-stu-id="81893-132">Select **Application claims** and then select the custom attribute.</span></span> <span data-ttu-id="81893-133">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="81893-133">Click **OK**.</span></span>
6. <span data-ttu-id="81893-134">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="81893-134">Click **Save**.</span></span>

<span data-ttu-id="81893-135">You can use the **Run now** feature on the policy to verify the customer experience.</span><span class="sxs-lookup"><span data-stu-id="81893-135">You can use the **Run now** feature on the policy to verify the customer experience.</span></span> <span data-ttu-id="81893-136">You should now see **ShoeSize** in the list of attributes collected during the sign-up journey, and see it in the token sent back to your application.</span><span class="sxs-lookup"><span data-stu-id="81893-136">You should now see **ShoeSize** in the list of attributes collected during the sign-up journey, and see it in the token sent back to your application.</span></span>

