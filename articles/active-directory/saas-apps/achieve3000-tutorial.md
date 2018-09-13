---
title: 'Tutorial: Azure Active Directory integration with Achieve3000 | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Achieve3000.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 83a83d07-ff9c-46c4-b5ba-25fe2b2cd003
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/19/2017
ms.author: jeedes
ms.openlocfilehash: 72e327f3cfa81b1ff27fcad743f5bb9a98737ed9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864323"
---
# <a name="tutorial-azure-active-directory-integration-with-achieve3000"></a><span data-ttu-id="48767-103">Tutorial: Azure Active Directory integration with Achieve3000</span><span class="sxs-lookup"><span data-stu-id="48767-103">Tutorial: Azure Active Directory integration with Achieve3000</span></span>

<span data-ttu-id="48767-104">In this tutorial, you learn how to integrate Achieve3000 with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="48767-104">In this tutorial, you learn how to integrate Achieve3000 with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="48767-105">Integrating Achieve3000 with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="48767-105">Integrating Achieve3000 with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="48767-106">You can control in Azure AD who has access to Achieve3000.</span><span class="sxs-lookup"><span data-stu-id="48767-106">You can control in Azure AD who has access to Achieve3000.</span></span>
- <span data-ttu-id="48767-107">You can enable your users to automatically get signed-on to Achieve3000 (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="48767-107">You can enable your users to automatically get signed-on to Achieve3000 (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="48767-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="48767-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="48767-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="48767-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48767-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="48767-110">Prerequisites</span></span>

<span data-ttu-id="48767-111">To configure Azure AD integration with Achieve3000, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="48767-111">To configure Azure AD integration with Achieve3000, you need the following items:</span></span>

- <span data-ttu-id="48767-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="48767-112">An Azure AD subscription</span></span>
- <span data-ttu-id="48767-113">An Achieve3000 single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="48767-113">An Achieve3000 single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="48767-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="48767-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="48767-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="48767-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="48767-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="48767-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="48767-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48767-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="48767-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="48767-118">Scenario description</span></span>
<span data-ttu-id="48767-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="48767-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="48767-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="48767-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="48767-121">Adding Achieve3000 from the gallery</span><span class="sxs-lookup"><span data-stu-id="48767-121">Adding Achieve3000 from the gallery</span></span>
2. <span data-ttu-id="48767-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="48767-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-achieve3000-from-the-gallery"></a><span data-ttu-id="48767-123">Adding Achieve3000 from the gallery</span><span class="sxs-lookup"><span data-stu-id="48767-123">Adding Achieve3000 from the gallery</span></span>
<span data-ttu-id="48767-124">To configure the integration of Achieve3000 into Azure AD, you need to add Achieve3000 from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="48767-124">To configure the integration of Achieve3000 into Azure AD, you need to add Achieve3000 from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="48767-125">**To add Achieve3000 from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="48767-125">**To add Achieve3000 from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="48767-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="48767-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="48767-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="48767-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="48767-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="48767-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="48767-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="48767-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="48767-133">In the search box, type **Achieve3000**, select **Achieve3000** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="48767-133">In the search box, type **Achieve3000**, select **Achieve3000** from result panel then click **Add** button to add the application.</span></span>

    ![Achieve3000 in the results list](./media/achieve3000-tutorial/tutorial_achieve3000_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="48767-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="48767-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="48767-136">In this section, you configure and test Azure AD single sign-on with Achieve3000 based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="48767-136">In this section, you configure and test Azure AD single sign-on with Achieve3000 based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="48767-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Achieve3000 is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48767-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Achieve3000 is to a user in Azure AD.</span></span> <span data-ttu-id="48767-138">In other words, a link relationship between an Azure AD user and the related user in Achieve3000 needs to be established.</span><span class="sxs-lookup"><span data-stu-id="48767-138">In other words, a link relationship between an Azure AD user and the related user in Achieve3000 needs to be established.</span></span>

<span data-ttu-id="48767-139">In Achieve3000, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="48767-139">In Achieve3000, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="48767-140">To configure and test Azure AD single sign-on with Achieve3000, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="48767-140">To configure and test Azure AD single sign-on with Achieve3000, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="48767-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="48767-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="48767-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48767-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="48767-143">**[Create an Achieve3000 test user](#create-an-achieve3000-test-user)** - to have a counterpart of Britta Simon in Achieve3000 that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="48767-143">**[Create an Achieve3000 test user](#create-an-achieve3000-test-user)** - to have a counterpart of Britta Simon in Achieve3000 that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="48767-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="48767-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="48767-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="48767-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="48767-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="48767-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="48767-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Achieve3000 application.</span><span class="sxs-lookup"><span data-stu-id="48767-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Achieve3000 application.</span></span>

<span data-ttu-id="48767-148">**To configure Azure AD single sign-on with Achieve3000, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="48767-148">**To configure Azure AD single sign-on with Achieve3000, perform the following steps:**</span></span>

1. <span data-ttu-id="48767-149">In the Azure portal, on the **Achieve3000** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="48767-149">In the Azure portal, on the **Achieve3000** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="48767-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="48767-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/achieve3000-tutorial/tutorial_achieve3000_samlbase.png)

3. <span data-ttu-id="48767-153">On the **Achieve3000 Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="48767-153">On the **Achieve3000 Domain and URLs** section, perform the following steps:</span></span>

    ![Achieve3000 Domain and URLs single sign-on information](./media/achieve3000-tutorial/tutorial_achieve3000_url.png)

    <span data-ttu-id="48767-155">a.</span><span class="sxs-lookup"><span data-stu-id="48767-155">a.</span></span> <span data-ttu-id="48767-156">In the **Sign-on URL** textbox, type a URL using the following: pattern: `https://saml.achieve3000.com/district/<District Identifier>`</span><span class="sxs-lookup"><span data-stu-id="48767-156">In the **Sign-on URL** textbox, type a URL using the following: pattern: `https://saml.achieve3000.com/district/<District Identifier>`</span></span>

    <span data-ttu-id="48767-157">b.</span><span class="sxs-lookup"><span data-stu-id="48767-157">b.</span></span> <span data-ttu-id="48767-158">In the **Identifier** textbox, type the value: `achieve3000-saml`</span><span class="sxs-lookup"><span data-stu-id="48767-158">In the **Identifier** textbox, type the value: `achieve3000-saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="48767-159">The Sign-On URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="48767-159">The Sign-On URL value is not real.</span></span> <span data-ttu-id="48767-160">Update the value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="48767-160">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="48767-161">Contact [Achieve3000 Client support team](https://www.achieve3000.com/contact-us/) to get the value.</span><span class="sxs-lookup"><span data-stu-id="48767-161">Contact [Achieve3000 Client support team](https://www.achieve3000.com/contact-us/) to get the value.</span></span> 

4. <span data-ttu-id="48767-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="48767-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/achieve3000-tutorial/tutorial_achieve3000_certificate.png) 

5. <span data-ttu-id="48767-164">Achieve3000 application expects the unique **studentID** value in the Name Identifier claim.</span><span class="sxs-lookup"><span data-stu-id="48767-164">Achieve3000 application expects the unique **studentID** value in the Name Identifier claim.</span></span> <span data-ttu-id="48767-165">Customer can map the correct value for the Name Identifier claim.</span><span class="sxs-lookup"><span data-stu-id="48767-165">Customer can map the correct value for the Name Identifier claim.</span></span> <span data-ttu-id="48767-166">In this case, we have mapped the **user.mail** for the demo purpose.</span><span class="sxs-lookup"><span data-stu-id="48767-166">In this case, we have mapped the **user.mail** for the demo purpose.</span></span> <span data-ttu-id="48767-167">But according to your unique identifier, you should map the correct value for it.</span><span class="sxs-lookup"><span data-stu-id="48767-167">But according to your unique identifier, you should map the correct value for it.</span></span>   

    ![Configure Single Sign-On attb](./media/achieve3000-tutorial/tutorial_achieve3000_attribute.png)

6. <span data-ttu-id="48767-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="48767-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="48767-170">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="48767-170">Attribute Name</span></span> | <span data-ttu-id="48767-171">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="48767-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="48767-172">studentID</span><span class="sxs-lookup"><span data-stu-id="48767-172">studentID</span></span>               | <span data-ttu-id="48767-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="48767-173">user.mail</span></span> |

    <span data-ttu-id="48767-174">a.</span><span class="sxs-lookup"><span data-stu-id="48767-174">a.</span></span> <span data-ttu-id="48767-175">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="48767-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On Add](./media/achieve3000-tutorial/tutorial_officespace_04.png)

    ![Configure Single Sign-On Addattb](./media/achieve3000-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="48767-178">b.</span><span class="sxs-lookup"><span data-stu-id="48767-178">b.</span></span> <span data-ttu-id="48767-179">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="48767-179">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="48767-180">c.</span><span class="sxs-lookup"><span data-stu-id="48767-180">c.</span></span> <span data-ttu-id="48767-181">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="48767-181">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="48767-182">d.</span><span class="sxs-lookup"><span data-stu-id="48767-182">d.</span></span> <span data-ttu-id="48767-183">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="48767-183">Click **Ok**.</span></span>

7. <span data-ttu-id="48767-184">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="48767-184">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/achieve3000-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="48767-186">To configure single sign-on on **Achieve3000** side, you need to send the downloaded **Metadata XML** to [Achieve3000 support team](https://www.achieve3000.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="48767-186">To configure single sign-on on **Achieve3000** side, you need to send the downloaded **Metadata XML** to [Achieve3000 support team](https://www.achieve3000.com/contact-us/).</span></span> <span data-ttu-id="48767-187">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="48767-187">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="48767-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="48767-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="48767-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="48767-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="48767-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="48767-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="48767-191">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="48767-191">Create an Azure AD test user</span></span>

<span data-ttu-id="48767-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48767-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="48767-194">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="48767-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="48767-195">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="48767-195">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/achieve3000-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="48767-197">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="48767-197">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/achieve3000-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="48767-199">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="48767-199">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/achieve3000-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="48767-201">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="48767-201">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/achieve3000-tutorial/create_aaduser_04.png)

    <span data-ttu-id="48767-203">a.</span><span class="sxs-lookup"><span data-stu-id="48767-203">a.</span></span> <span data-ttu-id="48767-204">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="48767-204">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="48767-205">b.</span><span class="sxs-lookup"><span data-stu-id="48767-205">b.</span></span> <span data-ttu-id="48767-206">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48767-206">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="48767-207">c.</span><span class="sxs-lookup"><span data-stu-id="48767-207">c.</span></span> <span data-ttu-id="48767-208">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="48767-208">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="48767-209">d.</span><span class="sxs-lookup"><span data-stu-id="48767-209">d.</span></span> <span data-ttu-id="48767-210">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="48767-210">Click **Create**.</span></span>
 
### <a name="create-an-achieve3000-test-user"></a><span data-ttu-id="48767-211">Create an Achieve3000 test user</span><span class="sxs-lookup"><span data-stu-id="48767-211">Create an Achieve3000 test user</span></span>

<span data-ttu-id="48767-212">In this section, you create a user called Britta Simon in Achieve3000.</span><span class="sxs-lookup"><span data-stu-id="48767-212">In this section, you create a user called Britta Simon in Achieve3000.</span></span> <span data-ttu-id="48767-213">Work with [Achieve3000 support team](https://www.achieve3000.com/contact-us/) to add the users in the Achieve3000 platform.</span><span class="sxs-lookup"><span data-stu-id="48767-213">Work with [Achieve3000 support team](https://www.achieve3000.com/contact-us/) to add the users in the Achieve3000 platform.</span></span> <span data-ttu-id="48767-214">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="48767-214">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="48767-215">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="48767-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="48767-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Achieve3000.</span><span class="sxs-lookup"><span data-stu-id="48767-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Achieve3000.</span></span>

![Assign the user role][200] 

<span data-ttu-id="48767-218">**To assign Britta Simon to Achieve3000, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="48767-218">**To assign Britta Simon to Achieve3000, perform the following steps:**</span></span>

1. <span data-ttu-id="48767-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="48767-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="48767-221">In the applications list, select **Achieve3000**.</span><span class="sxs-lookup"><span data-stu-id="48767-221">In the applications list, select **Achieve3000**.</span></span>

    ![The Achieve3000 link in the Applications list](./media/achieve3000-tutorial/tutorial_achieve3000_app.png)  

3. <span data-ttu-id="48767-223">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="48767-223">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="48767-225">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="48767-225">Click **Add** button.</span></span> <span data-ttu-id="48767-226">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="48767-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="48767-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="48767-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="48767-229">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="48767-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="48767-230">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="48767-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="48767-231">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="48767-231">Test single sign-on</span></span>

<span data-ttu-id="48767-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="48767-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="48767-233">When you click the Achieve3000 tile in the Access Panel, you should get automatically signed-on to your Achieve3000 application.</span><span class="sxs-lookup"><span data-stu-id="48767-233">When you click the Achieve3000 tile in the Access Panel, you should get automatically signed-on to your Achieve3000 application.</span></span>
<span data-ttu-id="48767-234">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="48767-234">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="48767-235">Additional resources</span><span class="sxs-lookup"><span data-stu-id="48767-235">Additional resources</span></span>

* [<span data-ttu-id="48767-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48767-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="48767-237">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="48767-237">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/achieve3000-tutorial/tutorial_general_01.png
[2]: ./media/achieve3000-tutorial/tutorial_general_02.png
[3]: ./media/achieve3000-tutorial/tutorial_general_03.png
[4]: ./media/achieve3000-tutorial/tutorial_general_04.png

[100]: ./media/achieve3000-tutorial/tutorial_general_100.png

[200]: ./media/achieve3000-tutorial/tutorial_general_200.png
[201]: ./media/achieve3000-tutorial/tutorial_general_201.png
[202]: ./media/achieve3000-tutorial/tutorial_general_202.png
[203]: ./media/achieve3000-tutorial/tutorial_general_203.png

