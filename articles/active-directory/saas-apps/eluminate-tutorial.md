---
title: 'Tutorial: Azure Active Directory integration with eLuminate | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and eLuminate.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 94c28db4-dbca-446b-8eef-9b728f18ca9a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2018
ms.author: jeedes
ms.openlocfilehash: d2798f3638192604d0912f50a8b1c43f4a1939fb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864770"
---
# <a name="tutorial-azure-active-directory-integration-with-eluminate"></a><span data-ttu-id="b36a0-103">Tutorial: Azure Active Directory integration with eLuminate</span><span class="sxs-lookup"><span data-stu-id="b36a0-103">Tutorial: Azure Active Directory integration with eLuminate</span></span>

<span data-ttu-id="b36a0-104">In this tutorial, you learn how to integrate eLuminate with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b36a0-104">In this tutorial, you learn how to integrate eLuminate with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b36a0-105">Integrating eLuminate with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="b36a0-105">Integrating eLuminate with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b36a0-106">You can control in Azure AD who has access to eLuminate.</span><span class="sxs-lookup"><span data-stu-id="b36a0-106">You can control in Azure AD who has access to eLuminate.</span></span>
- <span data-ttu-id="b36a0-107">You can enable your users to automatically get signed-on to eLuminate (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="b36a0-107">You can enable your users to automatically get signed-on to eLuminate (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b36a0-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b36a0-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b36a0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span><span class="sxs-lookup"><span data-stu-id="b36a0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b36a0-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b36a0-110">Prerequisites</span></span>

<span data-ttu-id="b36a0-111">To configure Azure AD integration with eLuminate, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="b36a0-111">To configure Azure AD integration with eLuminate, you need the following items:</span></span>

- <span data-ttu-id="b36a0-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="b36a0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b36a0-113">A eLuminate single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="b36a0-113">A eLuminate single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b36a0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="b36a0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b36a0-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="b36a0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b36a0-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="b36a0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b36a0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b36a0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b36a0-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="b36a0-118">Scenario description</span></span>

<span data-ttu-id="b36a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="b36a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b36a0-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="b36a0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b36a0-121">Adding eLuminate from the gallery</span><span class="sxs-lookup"><span data-stu-id="b36a0-121">Adding eLuminate from the gallery</span></span>
2. <span data-ttu-id="b36a0-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b36a0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-eluminate-from-the-gallery"></a><span data-ttu-id="b36a0-123">Adding eLuminate from the gallery</span><span class="sxs-lookup"><span data-stu-id="b36a0-123">Adding eLuminate from the gallery</span></span>

<span data-ttu-id="b36a0-124">To configure the integration of eLuminate into Azure AD, you need to add eLuminate from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="b36a0-124">To configure the integration of eLuminate into Azure AD, you need to add eLuminate from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b36a0-125">**To add eLuminate from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b36a0-125">**To add eLuminate from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b36a0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="b36a0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="b36a0-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="b36a0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b36a0-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b36a0-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="b36a0-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="b36a0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="b36a0-133">In the search box, type **eLuminate**, select **eLuminate** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="b36a0-133">In the search box, type **eLuminate**, select **eLuminate** from result panel then click **Add** button to add the application.</span></span>

    ![eLuminate in the results list](./media/eluminate-tutorial/tutorial_eluminate_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b36a0-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b36a0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b36a0-136">In this section, you configure and test Azure AD single sign-on with eLuminate based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b36a0-136">In this section, you configure and test Azure AD single sign-on with eLuminate based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b36a0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in eLuminate is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b36a0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in eLuminate is to a user in Azure AD.</span></span> <span data-ttu-id="b36a0-138">In other words, a link relationship between an Azure AD user and the related user in eLuminate needs to be established.</span><span class="sxs-lookup"><span data-stu-id="b36a0-138">In other words, a link relationship between an Azure AD user and the related user in eLuminate needs to be established.</span></span>

<span data-ttu-id="b36a0-139">To configure and test Azure AD single sign-on with eLuminate, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b36a0-139">To configure and test Azure AD single sign-on with eLuminate, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b36a0-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="b36a0-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b36a0-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b36a0-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b36a0-142">**[Create a eLuminate test user](#create-a-eluminate-test-user)** - to have a counterpart of Britta Simon in eLuminate that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="b36a0-142">**[Create a eLuminate test user](#create-a-eluminate-test-user)** - to have a counterpart of Britta Simon in eLuminate that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b36a0-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b36a0-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b36a0-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="b36a0-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b36a0-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b36a0-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b36a0-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your eLuminate application.</span><span class="sxs-lookup"><span data-stu-id="b36a0-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your eLuminate application.</span></span>

<span data-ttu-id="b36a0-147">**To configure Azure AD single sign-on with eLuminate, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b36a0-147">**To configure Azure AD single sign-on with eLuminate, perform the following steps:**</span></span>

1. <span data-ttu-id="b36a0-148">In the Azure portal, on the **eLuminate** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b36a0-148">In the Azure portal, on the **eLuminate** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="b36a0-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b36a0-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/eluminate-tutorial/tutorial_eluminate_samlbase.png)

3. <span data-ttu-id="b36a0-152">On the **eLuminate Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b36a0-152">On the **eLuminate Domain and URLs** section, perform the following steps:</span></span>

    ![eLuminate Domain and URLs single sign-on information](./media/eluminate-tutorial/tutorial_eluminate_url.png)

    <span data-ttu-id="b36a0-154">a.</span><span class="sxs-lookup"><span data-stu-id="b36a0-154">a.</span></span> <span data-ttu-id="b36a0-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://ClientShortName.eluminate.ca/azuresso/account/SignIn`</span><span class="sxs-lookup"><span data-stu-id="b36a0-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://ClientShortName.eluminate.ca/azuresso/account/SignIn`</span></span>

    <span data-ttu-id="b36a0-156">b.</span><span class="sxs-lookup"><span data-stu-id="b36a0-156">b.</span></span> <span data-ttu-id="b36a0-157">In the **Identifier** textbox, type a URL using the following pattern: `Eluminate/ClientShortName`</span><span class="sxs-lookup"><span data-stu-id="b36a0-157">In the **Identifier** textbox, type a URL using the following pattern: `Eluminate/ClientShortName`</span></span>

    > [!NOTE]
    > <span data-ttu-id="b36a0-158">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="b36a0-158">These values are not real.</span></span> <span data-ttu-id="b36a0-159">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="b36a0-159">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b36a0-160">Contact [eLuminate Client support team](mailto:support@intellimedia.ca) to get these values.</span><span class="sxs-lookup"><span data-stu-id="b36a0-160">Contact [eLuminate Client support team](mailto:support@intellimedia.ca) to get these values.</span></span>

4. <span data-ttu-id="b36a0-161">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="b36a0-161">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>

    ![The Certificate download link](./media/eluminate-tutorial/tutorial_eluminate_certificate.png) 

5. <span data-ttu-id="b36a0-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="b36a0-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/eluminate-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b36a0-165">To configure single sign-on on **eLuminate** side, you need to send the **App Federation Metadata Url** to [eLuminate support team](mailto:support@intellimedia.ca).</span><span class="sxs-lookup"><span data-stu-id="b36a0-165">To configure single sign-on on **eLuminate** side, you need to send the **App Federation Metadata Url** to [eLuminate support team](mailto:support@intellimedia.ca).</span></span> <span data-ttu-id="b36a0-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="b36a0-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b36a0-167">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b36a0-167">Create an Azure AD test user</span></span>

<span data-ttu-id="b36a0-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b36a0-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="b36a0-170">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b36a0-170">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b36a0-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="b36a0-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/eluminate-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b36a0-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="b36a0-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/eluminate-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b36a0-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="b36a0-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/eluminate-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b36a0-177">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b36a0-177">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/eluminate-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b36a0-179">a.</span><span class="sxs-lookup"><span data-stu-id="b36a0-179">a.</span></span> <span data-ttu-id="b36a0-180">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b36a0-180">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b36a0-181">b.</span><span class="sxs-lookup"><span data-stu-id="b36a0-181">b.</span></span> <span data-ttu-id="b36a0-182">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b36a0-182">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b36a0-183">c.</span><span class="sxs-lookup"><span data-stu-id="b36a0-183">c.</span></span> <span data-ttu-id="b36a0-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="b36a0-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b36a0-185">d.</span><span class="sxs-lookup"><span data-stu-id="b36a0-185">d.</span></span> <span data-ttu-id="b36a0-186">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b36a0-186">Click **Create**.</span></span>

### <a name="create-a-eluminate-test-user"></a><span data-ttu-id="b36a0-187">Create a eLuminate test user</span><span class="sxs-lookup"><span data-stu-id="b36a0-187">Create a eLuminate test user</span></span>

<span data-ttu-id="b36a0-188">In this section, you create a user called Britta Simon in eLuminate.</span><span class="sxs-lookup"><span data-stu-id="b36a0-188">In this section, you create a user called Britta Simon in eLuminate.</span></span> <span data-ttu-id="b36a0-189">Work with [eLuminate support team](mailto:support@intellimedia.ca) to add the users in the eLuminate platform.</span><span class="sxs-lookup"><span data-stu-id="b36a0-189">Work with [eLuminate support team](mailto:support@intellimedia.ca) to add the users in the eLuminate platform.</span></span> <span data-ttu-id="b36a0-190">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b36a0-190">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b36a0-191">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b36a0-191">Assign the Azure AD test user</span></span>

<span data-ttu-id="b36a0-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to eLuminate.</span><span class="sxs-lookup"><span data-stu-id="b36a0-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to eLuminate.</span></span>

![Assign the user role][200]

<span data-ttu-id="b36a0-194">**To assign Britta Simon to eLuminate, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b36a0-194">**To assign Britta Simon to eLuminate, perform the following steps:**</span></span>

1. <span data-ttu-id="b36a0-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b36a0-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="b36a0-197">In the applications list, select **eLuminate**.</span><span class="sxs-lookup"><span data-stu-id="b36a0-197">In the applications list, select **eLuminate**.</span></span>

    ![The eLuminate link in the Applications list](./media/eluminate-tutorial/tutorial_eluminate_app.png)  

3. <span data-ttu-id="b36a0-199">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="b36a0-199">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="b36a0-201">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="b36a0-201">Click **Add** button.</span></span> <span data-ttu-id="b36a0-202">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b36a0-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="b36a0-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="b36a0-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b36a0-205">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="b36a0-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b36a0-206">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b36a0-206">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="b36a0-207">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="b36a0-207">Test single sign-on</span></span>

<span data-ttu-id="b36a0-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b36a0-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b36a0-209">When you click the eLuminate tile in the Access Panel, you should get automatically signed-on to your eLuminate application.</span><span class="sxs-lookup"><span data-stu-id="b36a0-209">When you click the eLuminate tile in the Access Panel, you should get automatically signed-on to your eLuminate application.</span></span>
<span data-ttu-id="b36a0-210">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b36a0-210">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b36a0-211">Additional resources</span><span class="sxs-lookup"><span data-stu-id="b36a0-211">Additional resources</span></span>

* [<span data-ttu-id="b36a0-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b36a0-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="b36a0-213">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b36a0-213">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/eluminate-tutorial/tutorial_general_01.png
[2]: ./media/eluminate-tutorial/tutorial_general_02.png
[3]: ./media/eluminate-tutorial/tutorial_general_03.png
[4]: ./media/eluminate-tutorial/tutorial_general_04.png

[100]: ./media/eluminate-tutorial/tutorial_general_100.png

[200]: ./media/eluminate-tutorial/tutorial_general_200.png
[201]: ./media/eluminate-tutorial/tutorial_general_201.png
[202]: ./media/eluminate-tutorial/tutorial_general_202.png
[203]: ./media/eluminate-tutorial/tutorial_general_203.png