---
title: Get started with conditional access in Azure Active Directory - preview | Microsoft Docs
description: Test conditional access using a location condition.
services: active-directory
keywords: conditional access to apps, conditional access with Azure AD, secure access to company resources, conditional access policies
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/23/2017
ms.author: markvi
ms.openlocfilehash: 749e96826d3b0cd9bbe4a4765bee05e41dd49e2a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549405"
---
# <a name="get-started-with-conditional-access-in-azure-active-directory---preview"></a><span data-ttu-id="727bf-104">Get started with conditional access in Azure Active Directory - preview</span><span class="sxs-lookup"><span data-stu-id="727bf-104">Get started with conditional access in Azure Active Directory - preview</span></span>

<span data-ttu-id="727bf-105">The behavior outlined in this topic is currently in [preview](active-directory-preview-explainer.md).</span><span class="sxs-lookup"><span data-stu-id="727bf-105">The behavior outlined in this topic is currently in [preview](active-directory-preview-explainer.md).</span></span>

<span data-ttu-id="727bf-106">Conditional access is a capability of Azure Active Directory that enables you to define conditions under which authorized users can access your apps.</span><span class="sxs-lookup"><span data-stu-id="727bf-106">Conditional access is a capability of Azure Active Directory that enables you to define conditions under which authorized users can access your apps.</span></span> 

<span data-ttu-id="727bf-107">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span><span class="sxs-lookup"><span data-stu-id="727bf-107">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span></span>  


## <a name="scenario-description"></a><span data-ttu-id="727bf-108">Scenario description</span><span class="sxs-lookup"><span data-stu-id="727bf-108">Scenario description</span></span>

<span data-ttu-id="727bf-109">One common requirement in many organizations is to only require multi-factor authentication for access to apps that is not performed from the corporate intranet.</span><span class="sxs-lookup"><span data-stu-id="727bf-109">One common requirement in many organizations is to only require multi-factor authentication for access to apps that is not performed from the corporate intranet.</span></span> <span data-ttu-id="727bf-110">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="727bf-110">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span></span> <span data-ttu-id="727bf-111">This topic provides you with detailed instructions for configuring a related policy.</span><span class="sxs-lookup"><span data-stu-id="727bf-111">This topic provides you with detailed instructions for configuring a related policy.</span></span> <span data-ttu-id="727bf-112">The policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) to distinguish between access attempts made from the corporate's intranet and all other locations.</span><span class="sxs-lookup"><span data-stu-id="727bf-112">The policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) to distinguish between access attempts made from the corporate's intranet and all other locations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="727bf-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="727bf-113">Prerequisites</span></span>

<span data-ttu-id="727bf-114">The scenario outlined in this topic assumes that you are familiar with the concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="727bf-114">The scenario outlined in this topic assumes that you are familiar with the concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="727bf-115">To test this scenario, you need to:</span><span class="sxs-lookup"><span data-stu-id="727bf-115">To test this scenario, you need to:</span></span>

- <span data-ttu-id="727bf-116">Create a test user</span><span class="sxs-lookup"><span data-stu-id="727bf-116">Create a test user</span></span> 

- <span data-ttu-id="727bf-117">Assign an Azure AD Premium license to the test user</span><span class="sxs-lookup"><span data-stu-id="727bf-117">Assign an Azure AD Premium license to the test user</span></span>

- <span data-ttu-id="727bf-118">Configure a managed app and assign your test user to it</span><span class="sxs-lookup"><span data-stu-id="727bf-118">Configure a managed app and assign your test user to it</span></span>

- <span data-ttu-id="727bf-119">Configure trusted IPs</span><span class="sxs-lookup"><span data-stu-id="727bf-119">Configure trusted IPs</span></span>

<span data-ttu-id="727bf-120">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="727bf-120">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="policy-configuration-steps"></a><span data-ttu-id="727bf-121">Policy configuration steps</span><span class="sxs-lookup"><span data-stu-id="727bf-121">Policy configuration steps</span></span>

<span data-ttu-id="727bf-122">**To configure your conditional access policy, do:**</span><span class="sxs-lookup"><span data-stu-id="727bf-122">**To configure your conditional access policy, do:**</span></span>

1. <span data-ttu-id="727bf-123">In the Azure portal, on the left navbar, click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="727bf-123">In the Azure portal, on the left navbar, click **Azure Active Directory**.</span></span> 

    ![Conditional access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. <span data-ttu-id="727bf-125">On the **Azure Active Directory** blade, in the **Manage** section, click **Conditional access**.</span><span class="sxs-lookup"><span data-stu-id="727bf-125">On the **Azure Active Directory** blade, in the **Manage** section, click **Conditional access**.</span></span>

    ![Conditional access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. <span data-ttu-id="727bf-127">On the **Conditional Access** blade, to open the **New** blade, in the toolbar on the top, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="727bf-127">On the **Conditional Access** blade, to open the **New** blade, in the toolbar on the top, click **Add**.</span></span>

    ![Conditional access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. <span data-ttu-id="727bf-129">On the **New** blade, in the **Name** textbox, type a name for your policy.</span><span class="sxs-lookup"><span data-stu-id="727bf-129">On the **New** blade, in the **Name** textbox, type a name for your policy.</span></span>

    ![Conditional access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. <span data-ttu-id="727bf-131">In the **Assignment** section, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="727bf-131">In the **Assignment** section, click **Users and groups**.</span></span>

    ![Conditional access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. <span data-ttu-id="727bf-133">On the **Users and groups** blade, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="727bf-133">On the **Users and groups** blade, perform the following steps:</span></span>

    ![Conditional access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal-get-started/06.png)

    <span data-ttu-id="727bf-135">a.</span><span class="sxs-lookup"><span data-stu-id="727bf-135">a.</span></span> <span data-ttu-id="727bf-136">Click **Select users and groups**.</span><span class="sxs-lookup"><span data-stu-id="727bf-136">Click **Select users and groups**.</span></span>

    <span data-ttu-id="727bf-137">b.</span><span class="sxs-lookup"><span data-stu-id="727bf-137">b.</span></span> <span data-ttu-id="727bf-138">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="727bf-138">Click **Select**.</span></span>

    <span data-ttu-id="727bf-139">c.</span><span class="sxs-lookup"><span data-stu-id="727bf-139">c.</span></span> <span data-ttu-id="727bf-140">On the **Select** blade, select your test user, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="727bf-140">On the **Select** blade, select your test user, and then click **Select**.</span></span>

    <span data-ttu-id="727bf-141">d.</span><span class="sxs-lookup"><span data-stu-id="727bf-141">d.</span></span> <span data-ttu-id="727bf-142">On the **Users and groups** blade, click **Done**.</span><span class="sxs-lookup"><span data-stu-id="727bf-142">On the **Users and groups** blade, click **Done**.</span></span>

7. <span data-ttu-id="727bf-143">On the **New** blade, to open the **Cloud apps** blade, in the **Assignment** section, click **Cloud apps**.</span><span class="sxs-lookup"><span data-stu-id="727bf-143">On the **New** blade, to open the **Cloud apps** blade, in the **Assignment** section, click **Cloud apps**.</span></span>

    ![Conditional access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. <span data-ttu-id="727bf-145">On the **Cloud apps** blade, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="727bf-145">On the **Cloud apps** blade, perform the following steps:</span></span>

    ![Conditional access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal-get-started/08.png)

    <span data-ttu-id="727bf-147">a.</span><span class="sxs-lookup"><span data-stu-id="727bf-147">a.</span></span> <span data-ttu-id="727bf-148">Click **Select apps**.</span><span class="sxs-lookup"><span data-stu-id="727bf-148">Click **Select apps**.</span></span>

    <span data-ttu-id="727bf-149">b.</span><span class="sxs-lookup"><span data-stu-id="727bf-149">b.</span></span> <span data-ttu-id="727bf-150">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="727bf-150">Click **Select**.</span></span>

    <span data-ttu-id="727bf-151">c.</span><span class="sxs-lookup"><span data-stu-id="727bf-151">c.</span></span> <span data-ttu-id="727bf-152">On the **Select** blade, select your cloud app, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="727bf-152">On the **Select** blade, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="727bf-153">d.</span><span class="sxs-lookup"><span data-stu-id="727bf-153">d.</span></span> <span data-ttu-id="727bf-154">On the **Cloud apps** blade, click **Done**.</span><span class="sxs-lookup"><span data-stu-id="727bf-154">On the **Cloud apps** blade, click **Done**.</span></span>

9. <span data-ttu-id="727bf-155">On the **New** blade, to open the **Conditions** blade, in the **Assignment** section, click **Conditions**.</span><span class="sxs-lookup"><span data-stu-id="727bf-155">On the **New** blade, to open the **Conditions** blade, in the **Assignment** section, click **Conditions**.</span></span>

    ![Conditional access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. <span data-ttu-id="727bf-157">On the **Conditions** blade, to open the **Locations** blade, click **Locations**.</span><span class="sxs-lookup"><span data-stu-id="727bf-157">On the **Conditions** blade, to open the **Locations** blade, click **Locations**.</span></span>

    ![Conditional access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. <span data-ttu-id="727bf-159">On the **Locations** blade, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="727bf-159">On the **Locations** blade, perform the following steps:</span></span>

    ![Conditional access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal-get-started/11.png)

    <span data-ttu-id="727bf-161">a.</span><span class="sxs-lookup"><span data-stu-id="727bf-161">a.</span></span> <span data-ttu-id="727bf-162">Under **Configure**, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="727bf-162">Under **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="727bf-163">b.</span><span class="sxs-lookup"><span data-stu-id="727bf-163">b.</span></span> <span data-ttu-id="727bf-164">Under **Include**, click **All locations**.</span><span class="sxs-lookup"><span data-stu-id="727bf-164">Under **Include**, click **All locations**.</span></span>

    <span data-ttu-id="727bf-165">c.</span><span class="sxs-lookup"><span data-stu-id="727bf-165">c.</span></span> <span data-ttu-id="727bf-166">Click **Exclude**, and then click **All trusted IPs**.</span><span class="sxs-lookup"><span data-stu-id="727bf-166">Click **Exclude**, and then click **All trusted IPs**.</span></span>

    ![Conditional access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal-get-started/12.png)

    <span data-ttu-id="727bf-168">d.</span><span class="sxs-lookup"><span data-stu-id="727bf-168">d.</span></span> <span data-ttu-id="727bf-169">Click **Done**.</span><span class="sxs-lookup"><span data-stu-id="727bf-169">Click **Done**.</span></span>

12. <span data-ttu-id="727bf-170">On the **Conditions** blade, click **Done**.</span><span class="sxs-lookup"><span data-stu-id="727bf-170">On the **Conditions** blade, click **Done**.</span></span>

13. <span data-ttu-id="727bf-171">On the **New** blade, to open the **Grant** blade, in the **Controls** section, click **Grant**.</span><span class="sxs-lookup"><span data-stu-id="727bf-171">On the **New** blade, to open the **Grant** blade, in the **Controls** section, click **Grant**.</span></span>

    ![Conditional access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. <span data-ttu-id="727bf-173">On the **Grant** blade, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="727bf-173">On the **Grant** blade, perform the following steps:</span></span>

    ![Conditional access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal-get-started/14.png)

    <span data-ttu-id="727bf-175">a.</span><span class="sxs-lookup"><span data-stu-id="727bf-175">a.</span></span> <span data-ttu-id="727bf-176">Select **Require multi-factor authentication**.</span><span class="sxs-lookup"><span data-stu-id="727bf-176">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="727bf-177">b.</span><span class="sxs-lookup"><span data-stu-id="727bf-177">b.</span></span> <span data-ttu-id="727bf-178">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="727bf-178">Click **Select**.</span></span>

15. <span data-ttu-id="727bf-179">On the **New** blade, under **Enable policy**, click **On**.</span><span class="sxs-lookup"><span data-stu-id="727bf-179">On the **New** blade, under **Enable policy**, click **On**.</span></span>

    ![Conditional access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. <span data-ttu-id="727bf-181">On the **New** blade, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="727bf-181">On the **New** blade, click **Create**.</span></span>


## <a name="testing-the-policy"></a><span data-ttu-id="727bf-182">Testing the policy</span><span class="sxs-lookup"><span data-stu-id="727bf-182">Testing the policy</span></span>

<span data-ttu-id="727bf-183">To test your policy, you should access your app from a device that:</span><span class="sxs-lookup"><span data-stu-id="727bf-183">To test your policy, you should access your app from a device that:</span></span> 

1. <span data-ttu-id="727bf-184">Has an IP address that is within your configured Trusted IPs</span><span class="sxs-lookup"><span data-stu-id="727bf-184">Has an IP address that is within your configured Trusted IPs</span></span> 

1. <span data-ttu-id="727bf-185">Has an IP address that is not within your configured Trusted IPs</span><span class="sxs-lookup"><span data-stu-id="727bf-185">Has an IP address that is not within your configured Trusted IPs</span></span>

<span data-ttu-id="727bf-186">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span><span class="sxs-lookup"><span data-stu-id="727bf-186">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="727bf-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="727bf-187">Next steps</span></span>

<span data-ttu-id="727bf-188">If you would like to learn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="727bf-188">If you would like to learn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>
















