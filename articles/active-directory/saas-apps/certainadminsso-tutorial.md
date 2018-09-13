---
title: 'Tutorial: Azure Active Directory integration with Certain Admin SSO | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Certain Admin SSO.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98ba0174-be02-408a-8634-c8113b12dedb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2018
ms.author: jeedes
ms.openlocfilehash: 40bdba8e7ce699f0fd6ca589c753f51b550fae05
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865588"
---
# <a name="tutorial-azure-active-directory-integration-with-certain-admin-sso"></a><span data-ttu-id="269b5-103">Tutorial: Azure Active Directory integration with Certain Admin SSO</span><span class="sxs-lookup"><span data-stu-id="269b5-103">Tutorial: Azure Active Directory integration with Certain Admin SSO</span></span>

<span data-ttu-id="269b5-104">In this tutorial, you learn how to integrate Certain Admin SSO with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="269b5-104">In this tutorial, you learn how to integrate Certain Admin SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="269b5-105">Integrating Certain Admin SSO with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="269b5-105">Integrating Certain Admin SSO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="269b5-106">You can control in Azure AD who has access to Certain Admin SSO.</span><span class="sxs-lookup"><span data-stu-id="269b5-106">You can control in Azure AD who has access to Certain Admin SSO.</span></span>
- <span data-ttu-id="269b5-107">You can enable your users to automatically get signed-on to Certain Admin SSO (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="269b5-107">You can enable your users to automatically get signed-on to Certain Admin SSO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="269b5-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="269b5-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="269b5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="269b5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="269b5-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="269b5-110">Prerequisites</span></span>

<span data-ttu-id="269b5-111">To configure Azure AD integration with Certain Admin SSO, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="269b5-111">To configure Azure AD integration with Certain Admin SSO, you need the following items:</span></span>

- <span data-ttu-id="269b5-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="269b5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="269b5-113">A Certain Admin SSO single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="269b5-113">A Certain Admin SSO single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="269b5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="269b5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="269b5-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="269b5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="269b5-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="269b5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="269b5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="269b5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="269b5-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="269b5-118">Scenario description</span></span>
<span data-ttu-id="269b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="269b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="269b5-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="269b5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="269b5-121">Adding Certain Admin SSO from the gallery</span><span class="sxs-lookup"><span data-stu-id="269b5-121">Adding Certain Admin SSO from the gallery</span></span>
1. <span data-ttu-id="269b5-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="269b5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-certain-admin-sso-from-the-gallery"></a><span data-ttu-id="269b5-123">Adding Certain Admin SSO from the gallery</span><span class="sxs-lookup"><span data-stu-id="269b5-123">Adding Certain Admin SSO from the gallery</span></span>
<span data-ttu-id="269b5-124">To configure the integration of Certain Admin SSO into Azure AD, you need to add Certain Admin SSO from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="269b5-124">To configure the integration of Certain Admin SSO into Azure AD, you need to add Certain Admin SSO from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="269b5-125">**To add Certain Admin SSO from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="269b5-125">**To add Certain Admin SSO from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="269b5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="269b5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="269b5-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="269b5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="269b5-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="269b5-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="269b5-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="269b5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="269b5-133">In the search box, type **Certain Admin SSO**, select **Certain Admin SSO** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="269b5-133">In the search box, type **Certain Admin SSO**, select **Certain Admin SSO** from result panel then click **Add** button to add the application.</span></span>

    ![Certain Admin SSO in the results list](./media/certainadminsso-tutorial/tutorial_certainadminsso_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="269b5-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="269b5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="269b5-136">In this section, you configure and test Azure AD single sign-on with Certain Admin SSO based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="269b5-136">In this section, you configure and test Azure AD single sign-on with Certain Admin SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="269b5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Certain Admin SSO is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="269b5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Certain Admin SSO is to a user in Azure AD.</span></span> <span data-ttu-id="269b5-138">In other words, a link relationship between an Azure AD user and the related user in Certain Admin SSO needs to be established.</span><span class="sxs-lookup"><span data-stu-id="269b5-138">In other words, a link relationship between an Azure AD user and the related user in Certain Admin SSO needs to be established.</span></span>

<span data-ttu-id="269b5-139">To configure and test Azure AD single sign-on with Certain Admin SSO, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="269b5-139">To configure and test Azure AD single sign-on with Certain Admin SSO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="269b5-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="269b5-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="269b5-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="269b5-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="269b5-142">**[Create a Certain Admin SSO test user](#create-a-certain-admin-sso-test-user)** - to have a counterpart of Britta Simon in Certain Admin SSO that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="269b5-142">**[Create a Certain Admin SSO test user](#create-a-certain-admin-sso-test-user)** - to have a counterpart of Britta Simon in Certain Admin SSO that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="269b5-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="269b5-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="269b5-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="269b5-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="269b5-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="269b5-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="269b5-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Certain Admin SSO application.</span><span class="sxs-lookup"><span data-stu-id="269b5-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Certain Admin SSO application.</span></span>

<span data-ttu-id="269b5-147">**To configure Azure AD single sign-on with Certain Admin SSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="269b5-147">**To configure Azure AD single sign-on with Certain Admin SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="269b5-148">In the Azure portal, on the **Certain Admin SSO** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="269b5-148">In the Azure portal, on the **Certain Admin SSO** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="269b5-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="269b5-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/certainadminsso-tutorial/tutorial_certainadminsso_samlbase.png)

1. <span data-ttu-id="269b5-152">On the **Certain Admin SSO Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="269b5-152">On the **Certain Admin SSO Domain and URLs** section, perform the following steps:</span></span>

    ![Certain Admin SSO Domain and URLs single sign-on information](./media/certainadminsso-tutorial/tutorial_certainadminsso_url.png)

    <span data-ttu-id="269b5-154">a.</span><span class="sxs-lookup"><span data-stu-id="269b5-154">a.</span></span> <span data-ttu-id="269b5-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<YOUR DOMAIN URL>/svcs/sso_admin_login/handleRequest/<ID>`</span><span class="sxs-lookup"><span data-stu-id="269b5-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<YOUR DOMAIN URL>/svcs/sso_admin_login/handleRequest/<ID>`</span></span>

    <span data-ttu-id="269b5-156">b.</span><span class="sxs-lookup"><span data-stu-id="269b5-156">b.</span></span> <span data-ttu-id="269b5-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.certain.com`</span><span class="sxs-lookup"><span data-stu-id="269b5-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.certain.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="269b5-158">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="269b5-158">These values are not real.</span></span> <span data-ttu-id="269b5-159">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="269b5-159">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="269b5-160">Contact [Certain Admin SSO Client support team](mailto:integrations@certain.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="269b5-160">Contact [Certain Admin SSO Client support team](mailto:integrations@certain.com) to get these values.</span></span> 
 
1. <span data-ttu-id="269b5-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="269b5-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/certainadminsso-tutorial/tutorial_certainadminsso_certificate.png) 

1. <span data-ttu-id="269b5-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="269b5-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/certainadminsso-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="269b5-165">On the **Certain Admin SSO Configuration** section, click **Configure Certain Admin SSO** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="269b5-165">On the **Certain Admin SSO Configuration** section, click **Configure Certain Admin SSO** to open **Configure sign-on** window.</span></span> <span data-ttu-id="269b5-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="269b5-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Certain Admin SSO Configuration](./media/certainadminsso-tutorial/tutorial_certainadminsso_configure.png) 

1. <span data-ttu-id="269b5-168">To configure single sign-on on **Certain Admin SSO** side, you need to send the downloaded **Certificate (Raw)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Certain Admin SSO support team](mailto:integrations@certain.com).</span><span class="sxs-lookup"><span data-stu-id="269b5-168">To configure single sign-on on **Certain Admin SSO** side, you need to send the downloaded **Certificate (Raw)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Certain Admin SSO support team](mailto:integrations@certain.com).</span></span> <span data-ttu-id="269b5-169">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="269b5-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="269b5-170">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="269b5-170">Create an Azure AD test user</span></span>

<span data-ttu-id="269b5-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="269b5-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="269b5-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="269b5-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="269b5-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="269b5-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/certainadminsso-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="269b5-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="269b5-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/certainadminsso-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="269b5-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="269b5-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/certainadminsso-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="269b5-180">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="269b5-180">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/certainadminsso-tutorial/create_aaduser_04.png)

    <span data-ttu-id="269b5-182">a.</span><span class="sxs-lookup"><span data-stu-id="269b5-182">a.</span></span> <span data-ttu-id="269b5-183">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="269b5-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="269b5-184">b.</span><span class="sxs-lookup"><span data-stu-id="269b5-184">b.</span></span> <span data-ttu-id="269b5-185">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="269b5-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="269b5-186">c.</span><span class="sxs-lookup"><span data-stu-id="269b5-186">c.</span></span> <span data-ttu-id="269b5-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="269b5-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="269b5-188">d.</span><span class="sxs-lookup"><span data-stu-id="269b5-188">d.</span></span> <span data-ttu-id="269b5-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="269b5-189">Click **Create**.</span></span>
 
### <a name="create-a-certain-admin-sso-test-user"></a><span data-ttu-id="269b5-190">Create a Certain Admin SSO test user</span><span class="sxs-lookup"><span data-stu-id="269b5-190">Create a Certain Admin SSO test user</span></span>

<span data-ttu-id="269b5-191">In this section, you create a user called Britta Simon in Certain Admin SSO.</span><span class="sxs-lookup"><span data-stu-id="269b5-191">In this section, you create a user called Britta Simon in Certain Admin SSO.</span></span> <span data-ttu-id="269b5-192">Work with [Certain Admin SSO support team](mailto:integrations@certain.com) to add the users in the Certain Admin SSO platform.</span><span class="sxs-lookup"><span data-stu-id="269b5-192">Work with [Certain Admin SSO support team](mailto:integrations@certain.com) to add the users in the Certain Admin SSO platform.</span></span> <span data-ttu-id="269b5-193">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="269b5-193">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="269b5-194">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="269b5-194">Assign the Azure AD test user</span></span>

<span data-ttu-id="269b5-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Certain Admin SSO.</span><span class="sxs-lookup"><span data-stu-id="269b5-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Certain Admin SSO.</span></span>

![Assign the user role][200] 

<span data-ttu-id="269b5-197">**To assign Britta Simon to Certain Admin SSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="269b5-197">**To assign Britta Simon to Certain Admin SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="269b5-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="269b5-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="269b5-200">In the applications list, select **Certain Admin SSO**.</span><span class="sxs-lookup"><span data-stu-id="269b5-200">In the applications list, select **Certain Admin SSO**.</span></span>

    ![The Certain Admin SSO link in the Applications list](./media/certainadminsso-tutorial/tutorial_certainadminsso_app.png)  

1. <span data-ttu-id="269b5-202">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="269b5-202">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="269b5-204">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="269b5-204">Click **Add** button.</span></span> <span data-ttu-id="269b5-205">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="269b5-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="269b5-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="269b5-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="269b5-208">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="269b5-208">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="269b5-209">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="269b5-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="269b5-210">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="269b5-210">Test single sign-on</span></span>

<span data-ttu-id="269b5-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="269b5-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="269b5-212">When you click the Certain Admin SSO tile in the Access Panel, you should get automatically signed-on to your Certain Admin SSO application.</span><span class="sxs-lookup"><span data-stu-id="269b5-212">When you click the Certain Admin SSO tile in the Access Panel, you should get automatically signed-on to your Certain Admin SSO application.</span></span>
<span data-ttu-id="269b5-213">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="269b5-213">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="269b5-214">Additional resources</span><span class="sxs-lookup"><span data-stu-id="269b5-214">Additional resources</span></span>

* [<span data-ttu-id="269b5-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="269b5-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="269b5-216">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="269b5-216">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/certainadminsso-tutorial/tutorial_general_01.png
[2]: ./media/certainadminsso-tutorial/tutorial_general_02.png
[3]: ./media/certainadminsso-tutorial/tutorial_general_03.png
[4]: ./media/certainadminsso-tutorial/tutorial_general_04.png

[100]: ./media/certainadminsso-tutorial/tutorial_general_100.png

[200]: ./media/certainadminsso-tutorial/tutorial_general_200.png
[201]: ./media/certainadminsso-tutorial/tutorial_general_201.png
[202]: ./media/certainadminsso-tutorial/tutorial_general_202.png
[203]: ./media/certainadminsso-tutorial/tutorial_general_203.png

