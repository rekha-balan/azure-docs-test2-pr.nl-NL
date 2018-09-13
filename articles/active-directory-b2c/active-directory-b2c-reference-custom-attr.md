---
title: 'Azure Active Directory B2C: Custom attributes | Microsoft Docs'
description: How to use custom attributes in Azure Active Directory B2C to collect information about your consumers
services: active-directory-b2c
documentationcenter: ''
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: f7b21cc941f17d0815316dfe7013e9f97a95c223
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555242"
---
# <a name="azure-active-directory-b2c-use-custom-attributes-to-collect-information-about-your-consumers"></a><span data-ttu-id="4c8ed-103">Azure Active Directory B2C: Use custom attributes to collect information about your consumers</span><span class="sxs-lookup"><span data-stu-id="4c8ed-103">Azure Active Directory B2C: Use custom attributes to collect information about your consumers</span></span>
<span data-ttu-id="4c8ed-104">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of information (attributes): Given Name, Surname, City, Postal Code, and other attributes.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-104">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of information (attributes): Given Name, Surname, City, Postal Code, and other attributes.</span></span> <span data-ttu-id="4c8ed-105">However, every consumer-facing application has unique requirements on what attributes to gather from consumers.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-105">However, every consumer-facing application has unique requirements on what attributes to gather from consumers.</span></span> <span data-ttu-id="4c8ed-106">With Azure AD B2C, you can extend the set of attributes stored on each consumer account.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-106">With Azure AD B2C, you can extend the set of attributes stored on each consumer account.</span></span> <span data-ttu-id="4c8ed-107">You can create custom attributes on the [Azure portal](https://portal.azure.com/) and use it in your sign-up policies, as shown below.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-107">You can create custom attributes on the [Azure portal](https://portal.azure.com/) and use it in your sign-up policies, as shown below.</span></span> <span data-ttu-id="4c8ed-108">You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="4c8ed-108">You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4c8ed-109">Custom attributes use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span><span class="sxs-lookup"><span data-stu-id="4c8ed-109">Custom attributes use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span></span>
> 
> 

## <a name="create-a-custom-attribute"></a><span data-ttu-id="4c8ed-110">Create a custom attribute</span><span class="sxs-lookup"><span data-stu-id="4c8ed-110">Create a custom attribute</span></span>
1. <span data-ttu-id="4c8ed-111">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade).</span><span class="sxs-lookup"><span data-stu-id="4c8ed-111">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade).</span></span>
2. <span data-ttu-id="4c8ed-112">Click **User attributes**.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-112">Click **User attributes**.</span></span>
3. <span data-ttu-id="4c8ed-113">Click **+Add** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-113">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="4c8ed-114">Provide a **Name** for the custom attribute (for example, "ShoeSize") and optionally, a **Description**.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-114">Provide a **Name** for the custom attribute (for example, "ShoeSize") and optionally, a **Description**.</span></span> <span data-ttu-id="4c8ed-115">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-115">Click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4c8ed-116">Only the "String" **Data Type** is currently available.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-116">Only the "String" **Data Type** is currently available.</span></span>
   > 
   > 

<span data-ttu-id="4c8ed-117">The custom attribute is now available in the list of **User attributes**, and for use in your sign-up policies.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-117">The custom attribute is now available in the list of **User attributes**, and for use in your sign-up policies.</span></span>

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a><span data-ttu-id="4c8ed-118">Use a custom attribute in your sign-up policy</span><span class="sxs-lookup"><span data-stu-id="4c8ed-118">Use a custom attribute in your sign-up policy</span></span>
1. <span data-ttu-id="4c8ed-119">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade).</span><span class="sxs-lookup"><span data-stu-id="4c8ed-119">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-the-b2c-features-blade).</span></span>
2. <span data-ttu-id="4c8ed-120">Click **Sign-up policies**.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-120">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="4c8ed-121">Click your sign-up policy (for example, "B2C_1_SiUp") to open it.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-121">Click your sign-up policy (for example, "B2C_1_SiUp") to open it.</span></span> <span data-ttu-id="4c8ed-122">Click **Edit** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-122">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="4c8ed-123">Click **Sign-up attributes** and select the custom attribute (for example, "ShoeSize").</span><span class="sxs-lookup"><span data-stu-id="4c8ed-123">Click **Sign-up attributes** and select the custom attribute (for example, "ShoeSize").</span></span> <span data-ttu-id="4c8ed-124">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-124">Click **OK**.</span></span>
5. <span data-ttu-id="4c8ed-125">Click **Application claims** and select the custom attribute.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-125">Click **Application claims** and select the custom attribute.</span></span> <span data-ttu-id="4c8ed-126">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-126">Click **OK**.</span></span>
6. <span data-ttu-id="4c8ed-127">Click **Save** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-127">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="4c8ed-128">You can use the "Run now" feature on the policy to verify the consumer experience.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-128">You can use the "Run now" feature on the policy to verify the consumer experience.</span></span> <span data-ttu-id="4c8ed-129">You should now see "ShoeSize" in the list of attributes collected during consumer sign-up, and see it in the token sent back to your application.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-129">You should now see "ShoeSize" in the list of attributes collected during consumer sign-up, and see it in the token sent back to your application.</span></span>

## <a name="notes"></a><span data-ttu-id="4c8ed-130">Notes</span><span class="sxs-lookup"><span data-stu-id="4c8ed-130">Notes</span></span>
* <span data-ttu-id="4c8ed-131">Along with sign-up policies, custom attributes can also be used in sign-up or sign-in policies and profile editing policies.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-131">Along with sign-up policies, custom attributes can also be used in sign-up or sign-in policies and profile editing policies.</span></span>
* <span data-ttu-id="4c8ed-132">There is a known limitation of custom attributes.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-132">There is a known limitation of custom attributes.</span></span> <span data-ttu-id="4c8ed-133">It is only created the first time it is used in any policy, and not when you add it to the list of **User attributes**.</span><span class="sxs-lookup"><span data-stu-id="4c8ed-133">It is only created the first time it is used in any policy, and not when you add it to the list of **User attributes**.</span></span>

