---
title: 'Tutorial: Azure Active Directory integration with Fidelity NetBenefits | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Fidelity NetBenefits.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 77dc8a98-c0e7-4129-ab88-28e7643e432a
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2018
ms.author: jeedes
ms.openlocfilehash: a1308035a8b758a9e2f824de3a78c03103c19931
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869647"
---
# <a name="tutorial-azure-active-directory-integration-with-fidelity-netbenefits"></a><span data-ttu-id="ba45a-103">Tutorial: Azure Active Directory integration with Fidelity NetBenefits</span><span class="sxs-lookup"><span data-stu-id="ba45a-103">Tutorial: Azure Active Directory integration with Fidelity NetBenefits</span></span>

<span data-ttu-id="ba45a-104">In this tutorial, you learn how to integrate Fidelity NetBenefits with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ba45a-104">In this tutorial, you learn how to integrate Fidelity NetBenefits with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ba45a-105">Integrating Fidelity NetBenefits with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ba45a-105">Integrating Fidelity NetBenefits with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ba45a-106">You can control in Azure AD who has access to Fidelity NetBenefits.</span><span class="sxs-lookup"><span data-stu-id="ba45a-106">You can control in Azure AD who has access to Fidelity NetBenefits.</span></span>
- <span data-ttu-id="ba45a-107">You can enable your users to automatically get signed-on to Fidelity NetBenefits (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="ba45a-107">You can enable your users to automatically get signed-on to Fidelity NetBenefits (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ba45a-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ba45a-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="ba45a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="ba45a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba45a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ba45a-110">Prerequisites</span></span>

<span data-ttu-id="ba45a-111">To configure Azure AD integration with Fidelity NetBenefits, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="ba45a-111">To configure Azure AD integration with Fidelity NetBenefits, you need the following items:</span></span>

- <span data-ttu-id="ba45a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="ba45a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ba45a-113">A Fidelity NetBenefits single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ba45a-113">A Fidelity NetBenefits single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ba45a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="ba45a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ba45a-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="ba45a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ba45a-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="ba45a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ba45a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ba45a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ba45a-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="ba45a-118">Scenario description</span></span>

<span data-ttu-id="ba45a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="ba45a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>
<span data-ttu-id="ba45a-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="ba45a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ba45a-121">Adding Fidelity NetBenefits from the gallery</span><span class="sxs-lookup"><span data-stu-id="ba45a-121">Adding Fidelity NetBenefits from the gallery</span></span>
2. <span data-ttu-id="ba45a-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ba45a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fidelity-netbenefits-from-the-gallery"></a><span data-ttu-id="ba45a-123">Adding Fidelity NetBenefits from the gallery</span><span class="sxs-lookup"><span data-stu-id="ba45a-123">Adding Fidelity NetBenefits from the gallery</span></span>

<span data-ttu-id="ba45a-124">To configure the integration of Fidelity NetBenefits into Azure AD, you need to add Fidelity NetBenefits from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="ba45a-124">To configure the integration of Fidelity NetBenefits into Azure AD, you need to add Fidelity NetBenefits from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ba45a-125">**To add Fidelity NetBenefits from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ba45a-125">**To add Fidelity NetBenefits from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ba45a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ba45a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="ba45a-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="ba45a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ba45a-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ba45a-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="ba45a-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="ba45a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="ba45a-133">In the search box, type **Fidelity NetBenefits**, select **Fidelity NetBenefits** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="ba45a-133">In the search box, type **Fidelity NetBenefits**, select **Fidelity NetBenefits** from result panel then click **Add** button to add the application.</span></span>

    ![Fidelity NetBenefits in the results list](./media/fidelitynetbenefits-tutorial/tutorial_fidelitynetbenefits_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ba45a-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ba45a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ba45a-136">In this section, you configure and test Azure AD single sign-on with Fidelity NetBenefits based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ba45a-136">In this section, you configure and test Azure AD single sign-on with Fidelity NetBenefits based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ba45a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Fidelity NetBenefits is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba45a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Fidelity NetBenefits is to a user in Azure AD.</span></span> <span data-ttu-id="ba45a-138">In other words, a link relationship between an Azure AD user and the related user in Fidelity NetBenefits needs to be established.</span><span class="sxs-lookup"><span data-stu-id="ba45a-138">In other words, a link relationship between an Azure AD user and the related user in Fidelity NetBenefits needs to be established.</span></span>

<span data-ttu-id="ba45a-139">In Fidelity NetBenefits, **user** mapping should be done with **Azure AD user** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="ba45a-139">In Fidelity NetBenefits, **user** mapping should be done with **Azure AD user** to establish the link relationship.</span></span>

<span data-ttu-id="ba45a-140">To configure and test Azure AD single sign-on with Fidelity NetBenefits, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ba45a-140">To configure and test Azure AD single sign-on with Fidelity NetBenefits, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ba45a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="ba45a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ba45a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ba45a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ba45a-143">**[Create a Fidelity NetBenefits test user](#create-a-fidelity-netbenefits-test-user)** - to have a counterpart of Britta Simon in Fidelity NetBenefits that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="ba45a-143">**[Create a Fidelity NetBenefits test user](#create-a-fidelity-netbenefits-test-user)** - to have a counterpart of Britta Simon in Fidelity NetBenefits that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ba45a-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ba45a-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ba45a-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="ba45a-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ba45a-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ba45a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ba45a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Fidelity NetBenefits application.</span><span class="sxs-lookup"><span data-stu-id="ba45a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Fidelity NetBenefits application.</span></span>

<span data-ttu-id="ba45a-148">**To configure Azure AD single sign-on with Fidelity NetBenefits, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ba45a-148">**To configure Azure AD single sign-on with Fidelity NetBenefits, perform the following steps:**</span></span>

1. <span data-ttu-id="ba45a-149">In the Azure portal, on the **Fidelity NetBenefits** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ba45a-149">In the Azure portal, on the **Fidelity NetBenefits** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="ba45a-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ba45a-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/fidelitynetbenefits-tutorial/tutorial_fidelitynetbenefits_samlbase.png)

3. <span data-ttu-id="ba45a-153">On the **Fidelity NetBenefits Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ba45a-153">On the **Fidelity NetBenefits Domain and URLs** section, perform the following steps:</span></span>

    ![Fidelity NetBenefits Domain and URLs single sign-on information](./media/fidelitynetbenefits-tutorial/tutorial_fidelitynetbenefits_url.png)

    <span data-ttu-id="ba45a-155">a.</span><span class="sxs-lookup"><span data-stu-id="ba45a-155">a.</span></span> <span data-ttu-id="ba45a-156">In the **Identifier** textbox, type a URL:</span><span class="sxs-lookup"><span data-stu-id="ba45a-156">In the **Identifier** textbox, type a URL:</span></span>

    <span data-ttu-id="ba45a-157">For Testing Environment:  `urn:sp:fidelity:geninbndnbparts20:uat:xq1`</span><span class="sxs-lookup"><span data-stu-id="ba45a-157">For Testing Environment:  `urn:sp:fidelity:geninbndnbparts20:uat:xq1`</span></span>

    <span data-ttu-id="ba45a-158">For Production Environment:  `urn:sp:fidelity:geninbndnbparts20`</span><span class="sxs-lookup"><span data-stu-id="ba45a-158">For Production Environment:  `urn:sp:fidelity:geninbndnbparts20`</span></span>

    <span data-ttu-id="ba45a-159">b.</span><span class="sxs-lookup"><span data-stu-id="ba45a-159">b.</span></span> <span data-ttu-id="ba45a-160">In the **Reply URL** textbox, enter a URL that to be provided by Fidelity at time of implementation or contact your assigned Fidelity Client Service Manager.</span><span class="sxs-lookup"><span data-stu-id="ba45a-160">In the **Reply URL** textbox, enter a URL that to be provided by Fidelity at time of implementation or contact your assigned Fidelity Client Service Manager.</span></span>

4. <span data-ttu-id="ba45a-161">Fidelity NetBenefits application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="ba45a-161">Fidelity NetBenefits application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="ba45a-162">We have mapped the **User Identifier** with the **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="ba45a-162">We have mapped the **User Identifier** with the **user.userprincipalname**.</span></span> <span data-ttu-id="ba45a-163">You can map this with **employeeid** or any other claim which is applicable to your Organization as **User Identifier**.</span><span class="sxs-lookup"><span data-stu-id="ba45a-163">You can map this with **employeeid** or any other claim which is applicable to your Organization as **User Identifier**.</span></span> <span data-ttu-id="ba45a-164">The following screenshot shows just an example for this.</span><span class="sxs-lookup"><span data-stu-id="ba45a-164">The following screenshot shows just an example for this.</span></span>

    ![Fidelity NetBenefits attribute](./media/fidelitynetbenefits-tutorial/tutorial_fidelitynetbenefits_attribute.png)

    >[!Note]
    ><span data-ttu-id="ba45a-166">Fidelity NetBenefits support Static and Dynamic Federation.</span><span class="sxs-lookup"><span data-stu-id="ba45a-166">Fidelity NetBenefits support Static and Dynamic Federation.</span></span> <span data-ttu-id="ba45a-167">Static means it will not use SAML based just in time user provisioning and Dynamic means it supports just in time user provisioning.</span><span class="sxs-lookup"><span data-stu-id="ba45a-167">Static means it will not use SAML based just in time user provisioning and Dynamic means it supports just in time user provisioning.</span></span> <span data-ttu-id="ba45a-168">For using JIT based provisioning customers have to add some more claims in Azure AD like user's birthdate etc. These details are provided by the your assigned **Fidelity Client Service Manager** and they have to enable this dynamic federation for your instance.</span><span class="sxs-lookup"><span data-stu-id="ba45a-168">For using JIT based provisioning customers have to add some more claims in Azure AD like user's birthdate etc. These details are provided by the your assigned **Fidelity Client Service Manager** and they have to enable this dynamic federation for your instance.</span></span>

5. <span data-ttu-id="ba45a-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="ba45a-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/fidelitynetbenefits-tutorial/tutorial_fidelitynetbenefits_certificate.png)

6. <span data-ttu-id="ba45a-171">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="ba45a-171">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/fidelitynetbenefits-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="ba45a-173">On the **Fidelity NetBenefits Configuration** section, click **Configure Fidelity NetBenefits** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="ba45a-173">On the **Fidelity NetBenefits Configuration** section, click **Configure Fidelity NetBenefits** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ba45a-174">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="ba45a-174">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Fidelity NetBenefits Configuration](./media/fidelitynetbenefits-tutorial/tutorial_fidelitynetbenefits_configure.png)

8. <span data-ttu-id="ba45a-176">To configure single sign-on on **Fidelity NetBenefits** side, you need to send the downloaded **Metadata XML**, **SAML Single Sign-On Service URL** and **SAML Entity ID** to **your assigned Fidelity Client Service Manager**.</span><span class="sxs-lookup"><span data-stu-id="ba45a-176">To configure single sign-on on **Fidelity NetBenefits** side, you need to send the downloaded **Metadata XML**, **SAML Single Sign-On Service URL** and **SAML Entity ID** to **your assigned Fidelity Client Service Manager**.</span></span> <span data-ttu-id="ba45a-177">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="ba45a-177">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ba45a-178">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ba45a-178">Create an Azure AD test user</span></span>

<span data-ttu-id="ba45a-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ba45a-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="ba45a-181">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ba45a-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ba45a-182">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="ba45a-182">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/fidelitynetbenefits-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="ba45a-184">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="ba45a-184">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/fidelitynetbenefits-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="ba45a-186">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="ba45a-186">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/fidelitynetbenefits-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="ba45a-188">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ba45a-188">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/fidelitynetbenefits-tutorial/create_aaduser_04.png)

    <span data-ttu-id="ba45a-190">a.</span><span class="sxs-lookup"><span data-stu-id="ba45a-190">a.</span></span> <span data-ttu-id="ba45a-191">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ba45a-191">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ba45a-192">b.</span><span class="sxs-lookup"><span data-stu-id="ba45a-192">b.</span></span> <span data-ttu-id="ba45a-193">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ba45a-193">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="ba45a-194">c.</span><span class="sxs-lookup"><span data-stu-id="ba45a-194">c.</span></span> <span data-ttu-id="ba45a-195">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="ba45a-195">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="ba45a-196">d.</span><span class="sxs-lookup"><span data-stu-id="ba45a-196">d.</span></span> <span data-ttu-id="ba45a-197">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ba45a-197">Click **Create**.</span></span>
  
### <a name="create-a-fidelity-netbenefits-test-user"></a><span data-ttu-id="ba45a-198">Create a Fidelity NetBenefits test user</span><span class="sxs-lookup"><span data-stu-id="ba45a-198">Create a Fidelity NetBenefits test user</span></span>

<span data-ttu-id="ba45a-199">In this section, you create a user called Britta Simon in Fidelity NetBenefits.</span><span class="sxs-lookup"><span data-stu-id="ba45a-199">In this section, you create a user called Britta Simon in Fidelity NetBenefits.</span></span> <span data-ttu-id="ba45a-200">If you are creating Static federation, please work with your assigned **Fidelity Client Service Manager** to create users in Fidelity NetBenefits platform.</span><span class="sxs-lookup"><span data-stu-id="ba45a-200">If you are creating Static federation, please work with your assigned **Fidelity Client Service Manager** to create users in Fidelity NetBenefits platform.</span></span> <span data-ttu-id="ba45a-201">These users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ba45a-201">These users must be created and activated before you use single sign-on.</span></span>

<span data-ttu-id="ba45a-202">For Dynamic Federation, users are created using Just In Time user provisioning.</span><span class="sxs-lookup"><span data-stu-id="ba45a-202">For Dynamic Federation, users are created using Just In Time user provisioning.</span></span> <span data-ttu-id="ba45a-203">For using JIT based provisioning customers have to add some more claims in Azure AD like user's birthdate etc. These details are provided by the your assigned **Fidelity Client Service Manager** and they have to enable this dynamic federation for your instance.</span><span class="sxs-lookup"><span data-stu-id="ba45a-203">For using JIT based provisioning customers have to add some more claims in Azure AD like user's birthdate etc. These details are provided by the your assigned **Fidelity Client Service Manager** and they have to enable this dynamic federation for your instance.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ba45a-204">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ba45a-204">Assign the Azure AD test user</span></span>

<span data-ttu-id="ba45a-205">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Fidelity NetBenefits.</span><span class="sxs-lookup"><span data-stu-id="ba45a-205">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Fidelity NetBenefits.</span></span>

![Assign the user role][200]

<span data-ttu-id="ba45a-207">**To assign Britta Simon to Fidelity NetBenefits, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ba45a-207">**To assign Britta Simon to Fidelity NetBenefits, perform the following steps:**</span></span>

1. <span data-ttu-id="ba45a-208">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ba45a-208">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="ba45a-210">In the applications list, select **Fidelity NetBenefits**.</span><span class="sxs-lookup"><span data-stu-id="ba45a-210">In the applications list, select **Fidelity NetBenefits**.</span></span>

    ![The Fidelity NetBenefits link in the Applications list](./media/fidelitynetbenefits-tutorial/tutorial_fidelitynetbenefits_app.png)  

3. <span data-ttu-id="ba45a-212">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="ba45a-212">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="ba45a-214">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="ba45a-214">Click **Add** button.</span></span> <span data-ttu-id="ba45a-215">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ba45a-215">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="ba45a-217">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="ba45a-217">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ba45a-218">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="ba45a-218">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ba45a-219">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ba45a-219">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="ba45a-220">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="ba45a-220">Test single sign-on</span></span>

<span data-ttu-id="ba45a-221">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ba45a-221">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ba45a-222">When you click the Fidelity NetBenefits tile in the Access Panel, you should get automatically signed-on to your Fidelity NetBenefits application.</span><span class="sxs-lookup"><span data-stu-id="ba45a-222">When you click the Fidelity NetBenefits tile in the Access Panel, you should get automatically signed-on to your Fidelity NetBenefits application.</span></span>
<span data-ttu-id="ba45a-223">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ba45a-223">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ba45a-224">Additional resources</span><span class="sxs-lookup"><span data-stu-id="ba45a-224">Additional resources</span></span>

* [<span data-ttu-id="ba45a-225">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ba45a-225">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="ba45a-226">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ba45a-226">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/fidelitynetbenefits-tutorial/tutorial_general_01.png
[2]: ./media/fidelitynetbenefits-tutorial/tutorial_general_02.png
[3]: ./media/fidelitynetbenefits-tutorial/tutorial_general_03.png
[4]: ./media/fidelitynetbenefits-tutorial/tutorial_general_04.png

[100]: ./media/fidelitynetbenefits-tutorial/tutorial_general_100.png

[200]: ./media/fidelitynetbenefits-tutorial/tutorial_general_200.png
[201]: ./media/fidelitynetbenefits-tutorial/tutorial_general_201.png
[202]: ./media/fidelitynetbenefits-tutorial/tutorial_general_202.png
[203]: ./media/fidelitynetbenefits-tutorial/tutorial_general_203.png