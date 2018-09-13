---
title: 'Tutorial: Azure Active Directory integration with Dovetale | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Dovetale.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81da50c3-df94-458a-8b6a-a30827ee6358
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2018
ms.author: jeedes
ms.openlocfilehash: dd2aa699c22518ebbe7f29ba8dfd296da7385476
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967159"
---
# <a name="tutorial-azure-active-directory-integration-with-dovetale"></a><span data-ttu-id="41253-103">Tutorial: Azure Active Directory integration with Dovetale</span><span class="sxs-lookup"><span data-stu-id="41253-103">Tutorial: Azure Active Directory integration with Dovetale</span></span>

<span data-ttu-id="41253-104">In this tutorial, you learn how to integrate Dovetale with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="41253-104">In this tutorial, you learn how to integrate Dovetale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="41253-105">Integrating Dovetale with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="41253-105">Integrating Dovetale with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="41253-106">You can control in Azure AD who has access to Dovetale.</span><span class="sxs-lookup"><span data-stu-id="41253-106">You can control in Azure AD who has access to Dovetale.</span></span>
- <span data-ttu-id="41253-107">You can enable your users to automatically get signed-on to Dovetale (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="41253-107">You can enable your users to automatically get signed-on to Dovetale (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="41253-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="41253-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="41253-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span><span class="sxs-lookup"><span data-stu-id="41253-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41253-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="41253-110">Prerequisites</span></span>

<span data-ttu-id="41253-111">To configure Azure AD integration with Dovetale, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="41253-111">To configure Azure AD integration with Dovetale, you need the following items:</span></span>

- <span data-ttu-id="41253-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="41253-112">An Azure AD subscription</span></span>
- <span data-ttu-id="41253-113">A Dovetale single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="41253-113">A Dovetale single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="41253-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="41253-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="41253-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="41253-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="41253-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="41253-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="41253-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="41253-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="41253-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="41253-118">Scenario description</span></span>

<span data-ttu-id="41253-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="41253-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="41253-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="41253-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="41253-121">Adding Dovetale from the gallery</span><span class="sxs-lookup"><span data-stu-id="41253-121">Adding Dovetale from the gallery</span></span>
2. <span data-ttu-id="41253-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="41253-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dovetale-from-the-gallery"></a><span data-ttu-id="41253-123">Adding Dovetale from the gallery</span><span class="sxs-lookup"><span data-stu-id="41253-123">Adding Dovetale from the gallery</span></span>

<span data-ttu-id="41253-124">To configure the integration of Dovetale into Azure AD, you need to add Dovetale from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="41253-124">To configure the integration of Dovetale into Azure AD, you need to add Dovetale from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="41253-125">**To add Dovetale from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="41253-125">**To add Dovetale from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="41253-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="41253-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="41253-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="41253-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="41253-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="41253-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="41253-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="41253-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="41253-133">In the search box, type **Dovetale**, select **Dovetale** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="41253-133">In the search box, type **Dovetale**, select **Dovetale** from result panel then click **Add** button to add the application.</span></span>

    ![Dovetale in the results list](./media/dovetale-tutorial/tutorial_dovetale_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="41253-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="41253-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="41253-136">In this section, you configure and test Azure AD single sign-on with Dovetale based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="41253-136">In this section, you configure and test Azure AD single sign-on with Dovetale based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="41253-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Dovetale is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="41253-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Dovetale is to a user in Azure AD.</span></span> <span data-ttu-id="41253-138">In other words, a link relationship between an Azure AD user and the related user in Dovetale needs to be established.</span><span class="sxs-lookup"><span data-stu-id="41253-138">In other words, a link relationship between an Azure AD user and the related user in Dovetale needs to be established.</span></span>

<span data-ttu-id="41253-139">To configure and test Azure AD single sign-on with Dovetale, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="41253-139">To configure and test Azure AD single sign-on with Dovetale, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="41253-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="41253-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="41253-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="41253-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="41253-142">**[Create a Dovetale test user](#create-a-dovetale-test-user)** - to have a counterpart of Britta Simon in Dovetale that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="41253-142">**[Create a Dovetale test user](#create-a-dovetale-test-user)** - to have a counterpart of Britta Simon in Dovetale that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="41253-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="41253-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="41253-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="41253-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="41253-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="41253-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="41253-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dovetale application.</span><span class="sxs-lookup"><span data-stu-id="41253-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dovetale application.</span></span>

<span data-ttu-id="41253-147">**To configure Azure AD single sign-on with Dovetale, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="41253-147">**To configure Azure AD single sign-on with Dovetale, perform the following steps:**</span></span>

1. <span data-ttu-id="41253-148">In the Azure portal, on the **Dovetale** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="41253-148">In the Azure portal, on the **Dovetale** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="41253-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="41253-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/dovetale-tutorial/tutorial_dovetale_samlbase.png)

3. <span data-ttu-id="41253-152">On the **Dovetale Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode, the user does not have to perform any steps as the app is already pre-integrated with Azure:</span><span class="sxs-lookup"><span data-stu-id="41253-152">On the **Dovetale Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode, the user does not have to perform any steps as the app is already pre-integrated with Azure:</span></span>

    ![Dovetale Domain and URLs single sign-on information](./media/dovetale-tutorial/tutorial_dovetale_url1.png)

4. <span data-ttu-id="41253-154">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="41253-154">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Dovetale Domain and URLs single sign-on information](./media/dovetale-tutorial/tutorial_dovetale_url2.png)

    <span data-ttu-id="41253-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `<COMPANYNAME>.dovetale.com`</span><span class="sxs-lookup"><span data-stu-id="41253-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `<COMPANYNAME>.dovetale.com`</span></span>

    > [!NOTE]
    > <span data-ttu-id="41253-157">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="41253-157">This value is not real.</span></span> <span data-ttu-id="41253-158">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="41253-158">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="41253-159">Contact [Dovetale Client support team](mailto:support@dovetale.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="41253-159">Contact [Dovetale Client support team](mailto:support@dovetale.com) to get this value.</span></span>

5. <span data-ttu-id="41253-160">Dovetale application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="41253-160">Dovetale application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="41253-161">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="41253-161">Please configure the following claims for this application.</span></span> <span data-ttu-id="41253-162">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="41253-162">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="41253-163">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="41253-163">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On](./media/dovetale-tutorial/tutorial_attribute.png)

6. <span data-ttu-id="41253-165">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span><span class="sxs-lookup"><span data-stu-id="41253-165">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="41253-166">Perform the following steps on each of the displayed attributes-</span><span class="sxs-lookup"><span data-stu-id="41253-166">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="41253-167">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="41253-167">Attribute Name</span></span> | <span data-ttu-id="41253-168">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="41253-168">Attribute Value</span></span> |
    | ---------------| --------------- |
    | <span data-ttu-id="41253-169">email</span><span class="sxs-lookup"><span data-stu-id="41253-169">email</span></span> | <span data-ttu-id="41253-170">user.mail</span><span class="sxs-lookup"><span data-stu-id="41253-170">user.mail</span></span> |
    | <span data-ttu-id="41253-171">first_name</span><span class="sxs-lookup"><span data-stu-id="41253-171">first_name</span></span> | <span data-ttu-id="41253-172">user.givenname</span><span class="sxs-lookup"><span data-stu-id="41253-172">user.givenname</span></span> |
    | <span data-ttu-id="41253-173">name</span><span class="sxs-lookup"><span data-stu-id="41253-173">name</span></span> | <span data-ttu-id="41253-174">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="41253-174">user.userprincipalname</span></span> |
    | <span data-ttu-id="41253-175">last_name</span><span class="sxs-lookup"><span data-stu-id="41253-175">last_name</span></span> | <span data-ttu-id="41253-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="41253-176">user.surname</span></span> |

    <span data-ttu-id="41253-177">a.</span><span class="sxs-lookup"><span data-stu-id="41253-177">a.</span></span> <span data-ttu-id="41253-178">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="41253-178">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/dovetale-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/dovetale-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="41253-181">b.</span><span class="sxs-lookup"><span data-stu-id="41253-181">b.</span></span> <span data-ttu-id="41253-182">In the **Name** textbox, type the **attribute name** shown for that row.</span><span class="sxs-lookup"><span data-stu-id="41253-182">In the **Name** textbox, type the **attribute name** shown for that row.</span></span>

    <span data-ttu-id="41253-183">c.</span><span class="sxs-lookup"><span data-stu-id="41253-183">c.</span></span> <span data-ttu-id="41253-184">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="41253-184">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="41253-185">d.</span><span class="sxs-lookup"><span data-stu-id="41253-185">d.</span></span> <span data-ttu-id="41253-186">Leave **NAMESPACE** value blank.</span><span class="sxs-lookup"><span data-stu-id="41253-186">Leave **NAMESPACE** value blank.</span></span>

    <span data-ttu-id="41253-187">e.</span><span class="sxs-lookup"><span data-stu-id="41253-187">e.</span></span> <span data-ttu-id="41253-188">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="41253-188">Click **Ok**.</span></span>

7. <span data-ttu-id="41253-189">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="41253-189">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>

    ![The Certificate download link](./media/dovetale-tutorial/tutorial_dovetale_certificate.png) 

8. <span data-ttu-id="41253-191">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="41253-191">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/dovetale-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="41253-193">On the **Dovetale Configuration** section, click **Configure Dovetale** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="41253-193">On the **Dovetale Configuration** section, click **Configure Dovetale** to open **Configure sign-on** window.</span></span> <span data-ttu-id="41253-194">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="41253-194">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Dovetale Configuration](./media/dovetale-tutorial/tutorial_dovetale_configure.png)

10. <span data-ttu-id="41253-196">To configure single sign-on on **Dovetale** side, you need to send the **App Federation Metadata Url, SAML Entity ID, and SAML Single Sign-On Service URL** to [Dovetale support team](mailto:support@dovetale.com).</span><span class="sxs-lookup"><span data-stu-id="41253-196">To configure single sign-on on **Dovetale** side, you need to send the **App Federation Metadata Url, SAML Entity ID, and SAML Single Sign-On Service URL** to [Dovetale support team](mailto:support@dovetale.com).</span></span> <span data-ttu-id="41253-197">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="41253-197">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="41253-198">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="41253-198">Create an Azure AD test user</span></span>

<span data-ttu-id="41253-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="41253-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="41253-201">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="41253-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="41253-202">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="41253-202">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/dovetale-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="41253-204">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="41253-204">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/dovetale-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="41253-206">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="41253-206">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/dovetale-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="41253-208">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="41253-208">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/dovetale-tutorial/create_aaduser_04.png)

    <span data-ttu-id="41253-210">a.</span><span class="sxs-lookup"><span data-stu-id="41253-210">a.</span></span> <span data-ttu-id="41253-211">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="41253-211">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="41253-212">b.</span><span class="sxs-lookup"><span data-stu-id="41253-212">b.</span></span> <span data-ttu-id="41253-213">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="41253-213">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="41253-214">c.</span><span class="sxs-lookup"><span data-stu-id="41253-214">c.</span></span> <span data-ttu-id="41253-215">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="41253-215">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="41253-216">d.</span><span class="sxs-lookup"><span data-stu-id="41253-216">d.</span></span> <span data-ttu-id="41253-217">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="41253-217">Click **Create**.</span></span>

### <a name="create-a-dovetale-test-user"></a><span data-ttu-id="41253-218">Create a Dovetale test user</span><span class="sxs-lookup"><span data-stu-id="41253-218">Create a Dovetale test user</span></span>

<span data-ttu-id="41253-219">The objective of this section is to create a user called Britta Simon in Dovetale.</span><span class="sxs-lookup"><span data-stu-id="41253-219">The objective of this section is to create a user called Britta Simon in Dovetale.</span></span> <span data-ttu-id="41253-220">Dovetale supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="41253-220">Dovetale supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="41253-221">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="41253-221">There is no action item for you in this section.</span></span> <span data-ttu-id="41253-222">A new user is created during an attempt to access Dovetale if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="41253-222">A new user is created during an attempt to access Dovetale if it doesn't exist yet.</span></span>

> [!Note]
> <span data-ttu-id="41253-223">If you need to create a user manually, contact [Dovetale support team](mailto:support@dovetale.com).</span><span class="sxs-lookup"><span data-stu-id="41253-223">If you need to create a user manually, contact [Dovetale support team](mailto:support@dovetale.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="41253-224">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="41253-224">Assign the Azure AD test user</span></span>

<span data-ttu-id="41253-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dovetale.</span><span class="sxs-lookup"><span data-stu-id="41253-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dovetale.</span></span>

![Assign the user role][200]

<span data-ttu-id="41253-227">**To assign Britta Simon to Dovetale, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="41253-227">**To assign Britta Simon to Dovetale, perform the following steps:**</span></span>

1. <span data-ttu-id="41253-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="41253-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="41253-230">In the applications list, select **Dovetale**.</span><span class="sxs-lookup"><span data-stu-id="41253-230">In the applications list, select **Dovetale**.</span></span>

    ![The Dovetale link in the Applications list](./media/dovetale-tutorial/tutorial_dovetale_app.png)  

3. <span data-ttu-id="41253-232">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="41253-232">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="41253-234">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="41253-234">Click **Add** button.</span></span> <span data-ttu-id="41253-235">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="41253-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="41253-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="41253-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="41253-238">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="41253-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="41253-239">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="41253-239">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="41253-240">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="41253-240">Test single sign-on</span></span>

<span data-ttu-id="41253-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="41253-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="41253-242">When you click the Dovetale tile in the Access Panel, you should get automatically signed-on to your Dovetale application.</span><span class="sxs-lookup"><span data-stu-id="41253-242">When you click the Dovetale tile in the Access Panel, you should get automatically signed-on to your Dovetale application.</span></span>
<span data-ttu-id="41253-243">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="41253-243">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="41253-244">Additional resources</span><span class="sxs-lookup"><span data-stu-id="41253-244">Additional resources</span></span>

* [<span data-ttu-id="41253-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="41253-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="41253-246">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="41253-246">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/dovetale-tutorial/tutorial_general_01.png
[2]: ./media/dovetale-tutorial/tutorial_general_02.png
[3]: ./media/dovetale-tutorial/tutorial_general_03.png
[4]: ./media/dovetale-tutorial/tutorial_general_04.png

[100]: ./media/dovetale-tutorial/tutorial_general_100.png

[200]: ./media/dovetale-tutorial/tutorial_general_200.png
[201]: ./media/dovetale-tutorial/tutorial_general_201.png
[202]: ./media/dovetale-tutorial/tutorial_general_202.png
[203]: ./media/dovetale-tutorial/tutorial_general_203.png