---
title: Migrate a classic policy that requires multi-factor authentication in the Azure portal | Microsoft Docs
description: This article shows how to migrate a classic policy that requires multi-factor authentication in the Azure portal.
services: active-directory
keywords: conditional access to apps, conditional access with Azure AD, secure access to company resources, conditional access policies
documentationcenter: ''
author: MarkusVi
manager: mtillman
editor: ''
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.component: conditional-access
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/13/2018
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 20a15bf94826df0b058be59ff242c46878ea26dd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864799"
---
# <a name="migrate-a-classic-policy-that-requires-multi-factor-authentication-in-the-azure-portal"></a><span data-ttu-id="48583-104">Migrate a classic policy that requires multi-factor authentication in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="48583-104">Migrate a classic policy that requires multi-factor authentication in the Azure portal</span></span> 

<span data-ttu-id="48583-105">This article shows how to migrate a classic policy that requires **multi-factor authentication** for a cloud app.</span><span class="sxs-lookup"><span data-stu-id="48583-105">This article shows how to migrate a classic policy that requires **multi-factor authentication** for a cloud app.</span></span> <span data-ttu-id="48583-106">Although it is not a prerequisite, we recommend that you read [Migrate classic policies in the Azure portal](policy-migration.md) before you start migrating your classic policies.</span><span class="sxs-lookup"><span data-stu-id="48583-106">Although it is not a prerequisite, we recommend that you read [Migrate classic policies in the Azure portal](policy-migration.md) before you start migrating your classic policies.</span></span>


 
## <a name="overview"></a><span data-ttu-id="48583-107">Overview</span><span class="sxs-lookup"><span data-stu-id="48583-107">Overview</span></span> 

<span data-ttu-id="48583-108">The scenario in this article shows how to migrate a classic policy that requires **multi-factor authentication** for a cloud app.</span><span class="sxs-lookup"><span data-stu-id="48583-108">The scenario in this article shows how to migrate a classic policy that requires **multi-factor authentication** for a cloud app.</span></span> 

![Azure Active Directory](./media/policy-migration/33.png)


<span data-ttu-id="48583-110">The migration process consist of the following steps:</span><span class="sxs-lookup"><span data-stu-id="48583-110">The migration process consist of the following steps:</span></span>

1. <span data-ttu-id="48583-111">[Open the classic policy](#open-a-classic-policy) to get the configuration settings.</span><span class="sxs-lookup"><span data-stu-id="48583-111">[Open the classic policy](#open-a-classic-policy) to get the configuration settings.</span></span>
2. <span data-ttu-id="48583-112">Create a new Azure AD conditional access policy to replace your classic policy.</span><span class="sxs-lookup"><span data-stu-id="48583-112">Create a new Azure AD conditional access policy to replace your classic policy.</span></span> 
3. <span data-ttu-id="48583-113">Disable the classic policy.</span><span class="sxs-lookup"><span data-stu-id="48583-113">Disable the classic policy.</span></span>



## <a name="open-a-classic-policy"></a><span data-ttu-id="48583-114">Open a classic policy</span><span class="sxs-lookup"><span data-stu-id="48583-114">Open a classic policy</span></span>

1. <span data-ttu-id="48583-115">In the [Azure portal](https://portal.azure.com), on the left navbar, click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="48583-115">In the [Azure portal](https://portal.azure.com), on the left navbar, click **Azure Active Directory**.</span></span>

    ![Azure Active Directory](./media/policy-migration-mfa/01.png)

2. <span data-ttu-id="48583-117">On the **Azure Active Directory** page, in the **Manage** section, click **Conditional access**.</span><span class="sxs-lookup"><span data-stu-id="48583-117">On the **Azure Active Directory** page, in the **Manage** section, click **Conditional access**.</span></span>

    ![Conditional access](./media/policy-migration-mfa/02.png)

3. <span data-ttu-id="48583-119">In the **Manage** section, click **Classic policies (preview)**.</span><span class="sxs-lookup"><span data-stu-id="48583-119">In the **Manage** section, click **Classic policies (preview)**.</span></span>

    ![Classic policies](./media/policy-migration-mfa/12.png)

4. <span data-ttu-id="48583-121">In the list of classic policies, click the policy that requires **multi-factor authentication** for a cloud app.</span><span class="sxs-lookup"><span data-stu-id="48583-121">In the list of classic policies, click the policy that requires **multi-factor authentication** for a cloud app.</span></span>

    ![Classic policies](./media/policy-migration-mfa/13.png)


## <a name="create-a-new-conditional-access-policy"></a><span data-ttu-id="48583-123">Create a new conditional access policy</span><span class="sxs-lookup"><span data-stu-id="48583-123">Create a new conditional access policy</span></span>


1. <span data-ttu-id="48583-124">In the [Azure portal](https://portal.azure.com), on the left navbar, click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="48583-124">In the [Azure portal](https://portal.azure.com), on the left navbar, click **Azure Active Directory**.</span></span>

    ![Azure Active Directory](./media/policy-migration/01.png)

2. <span data-ttu-id="48583-126">On the **Azure Active Directory** page, in the **Manage** section, click **Conditional access**.</span><span class="sxs-lookup"><span data-stu-id="48583-126">On the **Azure Active Directory** page, in the **Manage** section, click **Conditional access**.</span></span>

    ![Conditional access](./media/policy-migration/02.png)



3. <span data-ttu-id="48583-128">On the **Conditional Access** page, to open the **New** page, in the toolbar on the top, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="48583-128">On the **Conditional Access** page, to open the **New** page, in the toolbar on the top, click **Add**.</span></span>

    ![Conditional access](./media/policy-migration/03.png)

4. <span data-ttu-id="48583-130">On the **New** page, in the **Name** textbox, type a name for your policy.</span><span class="sxs-lookup"><span data-stu-id="48583-130">On the **New** page, in the **Name** textbox, type a name for your policy.</span></span>

    ![Conditional access](./media/policy-migration/29.png)

5. <span data-ttu-id="48583-132">In the **Assignments** section, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="48583-132">In the **Assignments** section, click **Users and groups**.</span></span>

    ![Conditional access](./media/policy-migration/05.png)

    <span data-ttu-id="48583-134">a.</span><span class="sxs-lookup"><span data-stu-id="48583-134">a.</span></span> <span data-ttu-id="48583-135">If you have all users selected in your classic policy, click **All users**.</span><span class="sxs-lookup"><span data-stu-id="48583-135">If you have all users selected in your classic policy, click **All users**.</span></span> 

    ![Conditional access](./media/policy-migration/35.png)

    <span data-ttu-id="48583-137">b.</span><span class="sxs-lookup"><span data-stu-id="48583-137">b.</span></span> <span data-ttu-id="48583-138">If you have groups selected in your classic policy, click **Select users and groups**, and then select the required users and groups.</span><span class="sxs-lookup"><span data-stu-id="48583-138">If you have groups selected in your classic policy, click **Select users and groups**, and then select the required users and groups.</span></span>

    ![Conditional access](./media/policy-migration/36.png)

    <span data-ttu-id="48583-140">c.</span><span class="sxs-lookup"><span data-stu-id="48583-140">c.</span></span> <span data-ttu-id="48583-141">If you have the excluded groups, click the **Exclude** tab, and then select the required users and groups.</span><span class="sxs-lookup"><span data-stu-id="48583-141">If you have the excluded groups, click the **Exclude** tab, and then select the required users and groups.</span></span> 

    ![Conditional access](./media/policy-migration/37.png)

6. <span data-ttu-id="48583-143">On the **New** page, to open the **Cloud apps** page, in the **Assignment** section, click **Cloud apps**.</span><span class="sxs-lookup"><span data-stu-id="48583-143">On the **New** page, to open the **Cloud apps** page, in the **Assignment** section, click **Cloud apps**.</span></span>

8. <span data-ttu-id="48583-144">On the **Cloud apps** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="48583-144">On the **Cloud apps** page, perform the following steps:</span></span>

    ![Conditional access](./media/policy-migration/08.png)

    <span data-ttu-id="48583-146">a.</span><span class="sxs-lookup"><span data-stu-id="48583-146">a.</span></span> <span data-ttu-id="48583-147">Click **Select apps**.</span><span class="sxs-lookup"><span data-stu-id="48583-147">Click **Select apps**.</span></span>

    <span data-ttu-id="48583-148">b.</span><span class="sxs-lookup"><span data-stu-id="48583-148">b.</span></span> <span data-ttu-id="48583-149">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="48583-149">Click **Select**.</span></span>

    <span data-ttu-id="48583-150">c.</span><span class="sxs-lookup"><span data-stu-id="48583-150">c.</span></span> <span data-ttu-id="48583-151">On the **Select** page, select your cloud app, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="48583-151">On the **Select** page, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="48583-152">d.</span><span class="sxs-lookup"><span data-stu-id="48583-152">d.</span></span> <span data-ttu-id="48583-153">On the **Cloud apps** page, click **Done**.</span><span class="sxs-lookup"><span data-stu-id="48583-153">On the **Cloud apps** page, click **Done**.</span></span>



9. <span data-ttu-id="48583-154">If you have **Require multi-factor authentication** selected:</span><span class="sxs-lookup"><span data-stu-id="48583-154">If you have **Require multi-factor authentication** selected:</span></span>

    ![Conditional access](./media/policy-migration/26.png)

    <span data-ttu-id="48583-156">a.</span><span class="sxs-lookup"><span data-stu-id="48583-156">a.</span></span> <span data-ttu-id="48583-157">In the **Access controls** section, click **Grant**.</span><span class="sxs-lookup"><span data-stu-id="48583-157">In the **Access controls** section, click **Grant**.</span></span>

    ![Conditional access](./media/policy-migration/27.png)

    <span data-ttu-id="48583-159">b.</span><span class="sxs-lookup"><span data-stu-id="48583-159">b.</span></span> <span data-ttu-id="48583-160">On the **Grant** page, click **Grant access**, and then click **Require multi-factor authentication**.</span><span class="sxs-lookup"><span data-stu-id="48583-160">On the **Grant** page, click **Grant access**, and then click **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="48583-161">c.</span><span class="sxs-lookup"><span data-stu-id="48583-161">c.</span></span> <span data-ttu-id="48583-162">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="48583-162">Click **Select**.</span></span>


10. <span data-ttu-id="48583-163">Click **On** to enable your policy.</span><span class="sxs-lookup"><span data-stu-id="48583-163">Click **On** to enable your policy.</span></span>

    ![Conditional access](./media/policy-migration/30.png)



## <a name="disable-the-classic-policy"></a><span data-ttu-id="48583-165">Disable the classic policy</span><span class="sxs-lookup"><span data-stu-id="48583-165">Disable the classic policy</span></span>

<span data-ttu-id="48583-166">To disable your classic policy, click **Disable** in the **Details** view.</span><span class="sxs-lookup"><span data-stu-id="48583-166">To disable your classic policy, click **Disable** in the **Details** view.</span></span>

![Classic policies](./media/policy-migration-mfa/14.png)



## <a name="next-steps"></a><span data-ttu-id="48583-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="48583-168">Next steps</span></span>

- <span data-ttu-id="48583-169">For more information about the classic policy migration, see [Migrate classic policies in the Azure portal](policy-migration.md).</span><span class="sxs-lookup"><span data-stu-id="48583-169">For more information about the classic policy migration, see [Migrate classic policies in the Azure portal](policy-migration.md).</span></span>


- <span data-ttu-id="48583-170">If you want to know how to configure a conditional access policy, see [Require MFA for specific apps with Azure Active Directory conditional access](app-based-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="48583-170">If you want to know how to configure a conditional access policy, see [Require MFA for specific apps with Azure Active Directory conditional access](app-based-mfa.md).</span></span>

- <span data-ttu-id="48583-171">If you are ready to configure conditional access policies for your environment, see the [best practices for conditional access in Azure Active Directory](best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="48583-171">If you are ready to configure conditional access policies for your environment, see the [best practices for conditional access in Azure Active Directory](best-practices.md).</span></span> 
