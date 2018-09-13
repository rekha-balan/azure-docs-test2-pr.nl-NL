---
title: 'Tutorial: Azure Active Directory integration with TonicDM | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and TonicDM.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 19ea9a07-9ecf-43dc-91ba-593ce3c00b01
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2018
ms.author: jeedes
ms.openlocfilehash: b582af22707b7bff187ed93fb48ba96d15634ab3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867457"
---
# <a name="tutorial-azure-active-directory-integration-with-tonicdm"></a><span data-ttu-id="d09b7-103">Tutorial: Azure Active Directory integration with TonicDM</span><span class="sxs-lookup"><span data-stu-id="d09b7-103">Tutorial: Azure Active Directory integration with TonicDM</span></span>

<span data-ttu-id="d09b7-104">In this tutorial, you learn how to integrate TonicDM with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d09b7-104">In this tutorial, you learn how to integrate TonicDM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d09b7-105">Integrating TonicDM with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d09b7-105">Integrating TonicDM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d09b7-106">You can control in Azure AD who has access to TonicDM.</span><span class="sxs-lookup"><span data-stu-id="d09b7-106">You can control in Azure AD who has access to TonicDM.</span></span>
- <span data-ttu-id="d09b7-107">You can enable your users to automatically get signed-on to TonicDM (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="d09b7-107">You can enable your users to automatically get signed-on to TonicDM (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d09b7-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d09b7-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="d09b7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="d09b7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d09b7-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d09b7-110">Prerequisites</span></span>

<span data-ttu-id="d09b7-111">To configure Azure AD integration with TonicDM, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d09b7-111">To configure Azure AD integration with TonicDM, you need the following items:</span></span>

- <span data-ttu-id="d09b7-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d09b7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d09b7-113">A TonicDM single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d09b7-113">A TonicDM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d09b7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d09b7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d09b7-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d09b7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d09b7-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="d09b7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d09b7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d09b7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d09b7-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="d09b7-118">Scenario description</span></span>
<span data-ttu-id="d09b7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d09b7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d09b7-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d09b7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d09b7-121">Adding TonicDM from the gallery</span><span class="sxs-lookup"><span data-stu-id="d09b7-121">Adding TonicDM from the gallery</span></span>
1. <span data-ttu-id="d09b7-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d09b7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tonicdm-from-the-gallery"></a><span data-ttu-id="d09b7-123">Adding TonicDM from the gallery</span><span class="sxs-lookup"><span data-stu-id="d09b7-123">Adding TonicDM from the gallery</span></span>
<span data-ttu-id="d09b7-124">To configure the integration of TonicDM into Azure AD, you need to add TonicDM from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d09b7-124">To configure the integration of TonicDM into Azure AD, you need to add TonicDM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d09b7-125">**To add TonicDM from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d09b7-125">**To add TonicDM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d09b7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d09b7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="d09b7-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="d09b7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d09b7-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d09b7-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="d09b7-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="d09b7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="d09b7-133">In the search box, type **TonicDM**, select **TonicDM** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="d09b7-133">In the search box, type **TonicDM**, select **TonicDM** from result panel then click **Add** button to add the application.</span></span>

    ![TonicDM in the results list](./media/tonicdm-tutorial/tutorial_tonicdm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d09b7-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d09b7-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d09b7-136">In this section, you configure and test Azure AD single sign-on with TonicDM based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d09b7-136">In this section, you configure and test Azure AD single sign-on with TonicDM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d09b7-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TonicDM is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d09b7-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TonicDM is to a user in Azure AD.</span></span> <span data-ttu-id="d09b7-138">In other words, a link relationship between an Azure AD user and the related user in TonicDM needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d09b7-138">In other words, a link relationship between an Azure AD user and the related user in TonicDM needs to be established.</span></span>

<span data-ttu-id="d09b7-139">To configure and test Azure AD single sign-on with TonicDM, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d09b7-139">To configure and test Azure AD single sign-on with TonicDM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d09b7-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d09b7-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="d09b7-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d09b7-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="d09b7-142">**[Create a TonicDM test user](#create-a-tonicdm-test-user)** - to have a counterpart of Britta Simon in TonicDM that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="d09b7-142">**[Create a TonicDM test user](#create-a-tonicdm-test-user)** - to have a counterpart of Britta Simon in TonicDM that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="d09b7-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d09b7-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="d09b7-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d09b7-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d09b7-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d09b7-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d09b7-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TonicDM application.</span><span class="sxs-lookup"><span data-stu-id="d09b7-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TonicDM application.</span></span>

<span data-ttu-id="d09b7-147">**To configure Azure AD single sign-on with TonicDM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d09b7-147">**To configure Azure AD single sign-on with TonicDM, perform the following steps:**</span></span>

1. <span data-ttu-id="d09b7-148">In the Azure portal, on the **TonicDM** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d09b7-148">In the Azure portal, on the **TonicDM** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="d09b7-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d09b7-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/tonicdm-tutorial/tutorial_tonicdm_samlbase.png)

1. <span data-ttu-id="d09b7-152">On the **TonicDM Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d09b7-152">On the **TonicDM Domain and URLs** section, perform the following steps:</span></span>

    ![TonicDM Domain and URLs single sign-on information](./media/tonicdm-tutorial/tutorial_tonicdm_url.png)

    <span data-ttu-id="d09b7-154">a.</span><span class="sxs-lookup"><span data-stu-id="d09b7-154">a.</span></span> <span data-ttu-id="d09b7-155">In the **Sign-on URL** textbox, type a URL: `https://tonicdm.com/`</span><span class="sxs-lookup"><span data-stu-id="d09b7-155">In the **Sign-on URL** textbox, type a URL: `https://tonicdm.com/`</span></span>

    <span data-ttu-id="d09b7-156">b.</span><span class="sxs-lookup"><span data-stu-id="d09b7-156">b.</span></span> <span data-ttu-id="d09b7-157">In the **Identifier** textbox, type a URL: `https://tonicdm.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="d09b7-157">In the **Identifier** textbox, type a URL: `https://tonicdm.com/saml/metadata`</span></span>

1. <span data-ttu-id="d09b7-158">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d09b7-158">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/tonicdm-tutorial/tutorial_tonicdm_certificate.png) 

1. <span data-ttu-id="d09b7-160">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="d09b7-160">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/tonicdm-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="d09b7-162">On the **TonicDM Configuration** section, click **Configure TonicDM** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="d09b7-162">On the **TonicDM Configuration** section, click **Configure TonicDM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d09b7-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="d09b7-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![TonicDM Configuration](./media/tonicdm-tutorial/tutorial_tonicdm_configure.png) 

1. <span data-ttu-id="d09b7-165">To configure single sign-on on **TonicDM** side, you need to send the downloaded **Certificate (Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [TonicDM support team](mailto:support@tonicdm.com).</span><span class="sxs-lookup"><span data-stu-id="d09b7-165">To configure single sign-on on **TonicDM** side, you need to send the downloaded **Certificate (Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [TonicDM support team](mailto:support@tonicdm.com).</span></span> <span data-ttu-id="d09b7-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="d09b7-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d09b7-167">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d09b7-167">Create an Azure AD test user</span></span>

<span data-ttu-id="d09b7-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d09b7-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="d09b7-170">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d09b7-170">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d09b7-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="d09b7-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/tonicdm-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="d09b7-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="d09b7-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/tonicdm-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="d09b7-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="d09b7-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/tonicdm-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="d09b7-177">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d09b7-177">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/tonicdm-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d09b7-179">a.</span><span class="sxs-lookup"><span data-stu-id="d09b7-179">a.</span></span> <span data-ttu-id="d09b7-180">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d09b7-180">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d09b7-181">b.</span><span class="sxs-lookup"><span data-stu-id="d09b7-181">b.</span></span> <span data-ttu-id="d09b7-182">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d09b7-182">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="d09b7-183">c.</span><span class="sxs-lookup"><span data-stu-id="d09b7-183">c.</span></span> <span data-ttu-id="d09b7-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="d09b7-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="d09b7-185">d.</span><span class="sxs-lookup"><span data-stu-id="d09b7-185">d.</span></span> <span data-ttu-id="d09b7-186">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d09b7-186">Click **Create**.</span></span>
 
### <a name="create-a-tonicdm-test-user"></a><span data-ttu-id="d09b7-187">Create a TonicDM test user</span><span class="sxs-lookup"><span data-stu-id="d09b7-187">Create a TonicDM test user</span></span>

<span data-ttu-id="d09b7-188">In this section, you create a user called Britta Simon in TonicDM.</span><span class="sxs-lookup"><span data-stu-id="d09b7-188">In this section, you create a user called Britta Simon in TonicDM.</span></span> <span data-ttu-id="d09b7-189">Work with [TonicDM support team](mailto:support@tonicdm.com) to add the users in the TonicDM platform.</span><span class="sxs-lookup"><span data-stu-id="d09b7-189">Work with [TonicDM support team](mailto:support@tonicdm.com) to add the users in the TonicDM platform.</span></span> <span data-ttu-id="d09b7-190">Users must be created and activated before you use single sign-on</span><span class="sxs-lookup"><span data-stu-id="d09b7-190">Users must be created and activated before you use single sign-on</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d09b7-191">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d09b7-191">Assign the Azure AD test user</span></span>

<span data-ttu-id="d09b7-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TonicDM.</span><span class="sxs-lookup"><span data-stu-id="d09b7-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TonicDM.</span></span>

![Assign the user role][200] 

<span data-ttu-id="d09b7-194">**To assign Britta Simon to TonicDM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d09b7-194">**To assign Britta Simon to TonicDM, perform the following steps:**</span></span>

1. <span data-ttu-id="d09b7-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d09b7-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="d09b7-197">In the applications list, select **TonicDM**.</span><span class="sxs-lookup"><span data-stu-id="d09b7-197">In the applications list, select **TonicDM**.</span></span>

    ![The TonicDM link in the Applications list](./media/tonicdm-tutorial/tutorial_tonicdm_app.png)  

1. <span data-ttu-id="d09b7-199">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="d09b7-199">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="d09b7-201">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="d09b7-201">Click **Add** button.</span></span> <span data-ttu-id="d09b7-202">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d09b7-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="d09b7-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="d09b7-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="d09b7-205">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="d09b7-205">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="d09b7-206">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d09b7-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d09b7-207">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="d09b7-207">Test single sign-on</span></span>

<span data-ttu-id="d09b7-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d09b7-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d09b7-209">When you click the TonicDM tile in the Access Panel, you should get automatically signed-on to your TonicDM application.</span><span class="sxs-lookup"><span data-stu-id="d09b7-209">When you click the TonicDM tile in the Access Panel, you should get automatically signed-on to your TonicDM application.</span></span>
<span data-ttu-id="d09b7-210">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d09b7-210">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d09b7-211">Additional resources</span><span class="sxs-lookup"><span data-stu-id="d09b7-211">Additional resources</span></span>

* [<span data-ttu-id="d09b7-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d09b7-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="d09b7-213">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d09b7-213">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/tonicdm-tutorial/tutorial_general_01.png
[2]: ./media/tonicdm-tutorial/tutorial_general_02.png
[3]: ./media/tonicdm-tutorial/tutorial_general_03.png
[4]: ./media/tonicdm-tutorial/tutorial_general_04.png

[100]: ./media/tonicdm-tutorial/tutorial_general_100.png

[200]: ./media/tonicdm-tutorial/tutorial_general_200.png
[201]: ./media/tonicdm-tutorial/tutorial_general_201.png
[202]: ./media/tonicdm-tutorial/tutorial_general_202.png
[203]: ./media/tonicdm-tutorial/tutorial_general_203.png

