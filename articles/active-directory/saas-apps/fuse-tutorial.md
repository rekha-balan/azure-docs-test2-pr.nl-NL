---
title: 'Tutorial: Azure Active Directory integration with Fuse | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Fuse.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ef34f58-863a-4b37-875c-e8efa3e18bb3
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: jeedes
ms.openlocfilehash: 5ac9db26bc73d7b97507cca0db36ca10024422cd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867583"
---
# <a name="tutorial-azure-active-directory-integration-with-fuse"></a><span data-ttu-id="c5732-103">Tutorial: Azure Active Directory integration with Fuse</span><span class="sxs-lookup"><span data-stu-id="c5732-103">Tutorial: Azure Active Directory integration with Fuse</span></span>

<span data-ttu-id="c5732-104">In this tutorial, you learn how to integrate Fuse with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c5732-104">In this tutorial, you learn how to integrate Fuse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5732-105">Integrating Fuse with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="c5732-105">Integrating Fuse with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c5732-106">You can control in Azure AD who has access to Fuse.</span><span class="sxs-lookup"><span data-stu-id="c5732-106">You can control in Azure AD who has access to Fuse.</span></span>
- <span data-ttu-id="c5732-107">You can enable your users to automatically get signed-on to Fuse (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="c5732-107">You can enable your users to automatically get signed-on to Fuse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c5732-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c5732-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="c5732-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="c5732-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5732-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c5732-110">Prerequisites</span></span>

<span data-ttu-id="c5732-111">To configure Azure AD integration with Fuse, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="c5732-111">To configure Azure AD integration with Fuse, you need the following items:</span></span>

- <span data-ttu-id="c5732-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="c5732-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c5732-113">A Fuse single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="c5732-113">A Fuse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c5732-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="c5732-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c5732-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="c5732-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c5732-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="c5732-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c5732-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c5732-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5732-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="c5732-118">Scenario description</span></span>
<span data-ttu-id="c5732-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="c5732-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c5732-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="c5732-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5732-121">Add Fuse from the gallery</span><span class="sxs-lookup"><span data-stu-id="c5732-121">Add Fuse from the gallery</span></span>
2. <span data-ttu-id="c5732-122">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c5732-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-fuse-from-the-gallery"></a><span data-ttu-id="c5732-123">Add Fuse from the gallery</span><span class="sxs-lookup"><span data-stu-id="c5732-123">Add Fuse from the gallery</span></span>
<span data-ttu-id="c5732-124">To configure the integration of Fuse into Azure AD, you need to add Fuse from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="c5732-124">To configure the integration of Fuse into Azure AD, you need to add Fuse from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c5732-125">**To add Fuse from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c5732-125">**To add Fuse from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c5732-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="c5732-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="c5732-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="c5732-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c5732-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c5732-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="c5732-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="c5732-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="c5732-133">In the search box, type **Fuse**, select **Fuse** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="c5732-133">In the search box, type **Fuse**, select **Fuse** from result panel then click **Add** button to add the application.</span></span>

    ![Fuse in the results list](./media/fuse-tutorial/tutorial_fuse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c5732-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c5732-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c5732-136">In this section, you configure and test Azure AD single sign-on with Fuse based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c5732-136">In this section, you configure and test Azure AD single sign-on with Fuse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c5732-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Fuse is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5732-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Fuse is to a user in Azure AD.</span></span> <span data-ttu-id="c5732-138">In other words, a link relationship between an Azure AD user and the related user in Fuse needs to be established.</span><span class="sxs-lookup"><span data-stu-id="c5732-138">In other words, a link relationship between an Azure AD user and the related user in Fuse needs to be established.</span></span>

<span data-ttu-id="c5732-139">In Fuse, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="c5732-139">In Fuse, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c5732-140">To configure and test Azure AD single sign-on with Fuse, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c5732-140">To configure and test Azure AD single sign-on with Fuse, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c5732-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="c5732-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c5732-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c5732-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c5732-143">**[Create a Fuse test user](#create-a-fuse-test-user)** - to have a counterpart of Britta Simon in Fuse that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="c5732-143">**[Create a Fuse test user](#create-a-fuse-test-user)** - to have a counterpart of Britta Simon in Fuse that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c5732-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c5732-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c5732-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="c5732-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c5732-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c5732-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c5732-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Fuse application.</span><span class="sxs-lookup"><span data-stu-id="c5732-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Fuse application.</span></span>

<span data-ttu-id="c5732-148">**To configure Azure AD single sign-on with Fuse, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c5732-148">**To configure Azure AD single sign-on with Fuse, perform the following steps:**</span></span>

1. <span data-ttu-id="c5732-149">In the Azure portal, on the **Fuse** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c5732-149">In the Azure portal, on the **Fuse** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="c5732-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c5732-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/fuse-tutorial/tutorial_fuse_samlbase.png)

3. <span data-ttu-id="c5732-153">On the **Fuse Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c5732-153">On the **Fuse Domain and URLs** section, perform the following steps:</span></span>

    ![Fuse Domain and URLs single sign-on information](./media/fuse-tutorial/tutorial_fuse_url.png)
    
    <span data-ttu-id="c5732-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant name>.fusionuniversal.com/`</span><span class="sxs-lookup"><span data-stu-id="c5732-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant name>.fusionuniversal.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c5732-156">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="c5732-156">This value is not real.</span></span> <span data-ttu-id="c5732-157">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="c5732-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="c5732-158">Contact [Fuse Client support team](mailto:support@fusion-universal.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="c5732-158">Contact [Fuse Client support team](mailto:support@fusion-universal.com) to get this value.</span></span> 
 
4. <span data-ttu-id="c5732-159">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="c5732-159">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/fuse-tutorial/tutorial_fuse_certificate.png) 

5. <span data-ttu-id="c5732-161">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="c5732-161">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/fuse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c5732-163">On the **Fuse Configuration** section, click **Configure Fuse** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="c5732-163">On the **Fuse Configuration** section, click **Configure Fuse** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c5732-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="c5732-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Fuse Configuration](./media/fuse-tutorial/tutorial_fuse_configure.png) 

7. <span data-ttu-id="c5732-166">To get SSO configured for your application, contact [Fuse support team](mailto:support@fusion-universal.com) and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="c5732-166">To get SSO configured for your application, contact [Fuse support team](mailto:support@fusion-universal.com) and provide them with the following:</span></span>

    * <span data-ttu-id="c5732-167">The downloaded **Certificate (Raw) file**</span><span class="sxs-lookup"><span data-stu-id="c5732-167">The downloaded **Certificate (Raw) file**</span></span>
    * <span data-ttu-id="c5732-168">The **SAML Single Sign-On Service URL**</span><span class="sxs-lookup"><span data-stu-id="c5732-168">The **SAML Single Sign-On Service URL**</span></span>
    * <span data-ttu-id="c5732-169">The **SAML Entity ID**</span><span class="sxs-lookup"><span data-stu-id="c5732-169">The **SAML Entity ID**</span></span>
    * <span data-ttu-id="c5732-170">The **Sign-Out URL**</span><span class="sxs-lookup"><span data-stu-id="c5732-170">The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="c5732-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="c5732-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c5732-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="c5732-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c5732-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c5732-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c5732-174">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c5732-174">Create an Azure AD test user</span></span>

<span data-ttu-id="c5732-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c5732-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="c5732-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c5732-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c5732-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="c5732-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/fuse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c5732-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="c5732-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/fuse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c5732-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="c5732-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/fuse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c5732-184">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c5732-184">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/fuse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c5732-186">a.</span><span class="sxs-lookup"><span data-stu-id="c5732-186">a.</span></span> <span data-ttu-id="c5732-187">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c5732-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c5732-188">b.</span><span class="sxs-lookup"><span data-stu-id="c5732-188">b.</span></span> <span data-ttu-id="c5732-189">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c5732-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="c5732-190">c.</span><span class="sxs-lookup"><span data-stu-id="c5732-190">c.</span></span> <span data-ttu-id="c5732-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="c5732-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="c5732-192">d.</span><span class="sxs-lookup"><span data-stu-id="c5732-192">d.</span></span> <span data-ttu-id="c5732-193">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c5732-193">Click **Create**.</span></span>
 
### <a name="create-a-fuse-test-user"></a><span data-ttu-id="c5732-194">Create a Fuse test user</span><span class="sxs-lookup"><span data-stu-id="c5732-194">Create a Fuse test user</span></span>

<span data-ttu-id="c5732-195">In this section, you create a user called Britta Simon in Fuse.</span><span class="sxs-lookup"><span data-stu-id="c5732-195">In this section, you create a user called Britta Simon in Fuse.</span></span> <span data-ttu-id="c5732-196">Please work with [Fuse support team](mailto:support@fusion-universal.com) to add the users in the Fuse platform.</span><span class="sxs-lookup"><span data-stu-id="c5732-196">Please work with [Fuse support team](mailto:support@fusion-universal.com) to add the users in the Fuse platform.</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c5732-197">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c5732-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="c5732-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Fuse.</span><span class="sxs-lookup"><span data-stu-id="c5732-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Fuse.</span></span>

![Assign the user role][200] 

<span data-ttu-id="c5732-200">**To assign Britta Simon to Fuse, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c5732-200">**To assign Britta Simon to Fuse, perform the following steps:**</span></span>

1. <span data-ttu-id="c5732-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c5732-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="c5732-203">In the applications list, select **Fuse**.</span><span class="sxs-lookup"><span data-stu-id="c5732-203">In the applications list, select **Fuse**.</span></span>

    ![The Fuse link in the Applications list](./media/fuse-tutorial/tutorial_fuse_app.png)  

3. <span data-ttu-id="c5732-205">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="c5732-205">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="c5732-207">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="c5732-207">Click **Add** button.</span></span> <span data-ttu-id="c5732-208">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c5732-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="c5732-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="c5732-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c5732-211">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="c5732-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c5732-212">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c5732-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c5732-213">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="c5732-213">Test single sign-on</span></span>

<span data-ttu-id="c5732-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c5732-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c5732-215">When you click the Fuse tile in the Access Panel, you should get automatically signed-on to your Fuse application.</span><span class="sxs-lookup"><span data-stu-id="c5732-215">When you click the Fuse tile in the Access Panel, you should get automatically signed-on to your Fuse application.</span></span>
<span data-ttu-id="c5732-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c5732-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c5732-217">Additional resources</span><span class="sxs-lookup"><span data-stu-id="c5732-217">Additional resources</span></span>

* [<span data-ttu-id="c5732-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5732-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="c5732-219">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c5732-219">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/fuse-tutorial/tutorial_general_01.png
[2]: ./media/fuse-tutorial/tutorial_general_02.png
[3]: ./media/fuse-tutorial/tutorial_general_03.png
[4]: ./media/fuse-tutorial/tutorial_general_04.png

[100]: ./media/fuse-tutorial/tutorial_general_100.png

[200]: ./media/fuse-tutorial/tutorial_general_200.png
[201]: ./media/fuse-tutorial/tutorial_general_201.png
[202]: ./media/fuse-tutorial/tutorial_general_202.png
[203]: ./media/fuse-tutorial/tutorial_general_203.png

