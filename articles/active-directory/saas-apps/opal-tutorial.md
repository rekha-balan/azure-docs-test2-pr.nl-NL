---
title: 'Tutorial: Azure Active Directory integration with Opal | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Opal.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 434fc204-e9f9-4678-ad5f-054d621bb2f9
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2018
ms.author: jeedes
ms.openlocfilehash: a20818fc03117b3e6a6cdb882c7323d6b9aec533
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866849"
---
# <a name="tutorial-azure-active-directory-integration-with-opal"></a><span data-ttu-id="54244-103">Tutorial: Azure Active Directory integration with Opal</span><span class="sxs-lookup"><span data-stu-id="54244-103">Tutorial: Azure Active Directory integration with Opal</span></span>

<span data-ttu-id="54244-104">In this tutorial, you learn how to integrate Opal with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="54244-104">In this tutorial, you learn how to integrate Opal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="54244-105">Integrating Opal with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="54244-105">Integrating Opal with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="54244-106">You can control in Azure AD who has access to Opal.</span><span class="sxs-lookup"><span data-stu-id="54244-106">You can control in Azure AD who has access to Opal.</span></span>
- <span data-ttu-id="54244-107">You can enable your users to automatically get signed-on to Opal (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="54244-107">You can enable your users to automatically get signed-on to Opal (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="54244-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="54244-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="54244-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="54244-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54244-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="54244-110">Prerequisites</span></span>

<span data-ttu-id="54244-111">To configure Azure AD integration with Opal, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="54244-111">To configure Azure AD integration with Opal, you need the following items:</span></span>

- <span data-ttu-id="54244-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="54244-112">An Azure AD subscription</span></span>
- <span data-ttu-id="54244-113">An Opal single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="54244-113">An Opal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="54244-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="54244-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="54244-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="54244-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="54244-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="54244-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="54244-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="54244-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="54244-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="54244-118">Scenario description</span></span>
<span data-ttu-id="54244-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="54244-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="54244-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="54244-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="54244-121">Adding Opal from the gallery</span><span class="sxs-lookup"><span data-stu-id="54244-121">Adding Opal from the gallery</span></span>
1. <span data-ttu-id="54244-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="54244-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-opal-from-the-gallery"></a><span data-ttu-id="54244-123">Adding Opal from the gallery</span><span class="sxs-lookup"><span data-stu-id="54244-123">Adding Opal from the gallery</span></span>
<span data-ttu-id="54244-124">To configure the integration of Opal into Azure AD, you need to add Opal from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="54244-124">To configure the integration of Opal into Azure AD, you need to add Opal from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="54244-125">**To add Opal from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54244-125">**To add Opal from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="54244-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="54244-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="54244-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="54244-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="54244-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="54244-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="54244-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="54244-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="54244-133">In the search box, type **Opal**, select **Opal** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="54244-133">In the search box, type **Opal**, select **Opal** from result panel then click **Add** button to add the application.</span></span>

    ![Opal in the results list](./media/opal-tutorial/tutorial_opal_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="54244-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="54244-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="54244-136">In this section, you configure and test Azure AD single sign-on with Opal based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="54244-136">In this section, you configure and test Azure AD single sign-on with Opal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="54244-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Opal is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54244-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Opal is to a user in Azure AD.</span></span> <span data-ttu-id="54244-138">In other words, a link relationship between an Azure AD user and the related user in Opal needs to be established.</span><span class="sxs-lookup"><span data-stu-id="54244-138">In other words, a link relationship between an Azure AD user and the related user in Opal needs to be established.</span></span>

<span data-ttu-id="54244-139">In Opal, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="54244-139">In Opal, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="54244-140">To configure and test Azure AD single sign-on with Opal, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="54244-140">To configure and test Azure AD single sign-on with Opal, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="54244-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="54244-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="54244-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54244-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="54244-143">**[Create an Opal test user](#create-an-opal-test-user)** - to have a counterpart of Britta Simon in Opal that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="54244-143">**[Create an Opal test user](#create-an-opal-test-user)** - to have a counterpart of Britta Simon in Opal that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="54244-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="54244-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="54244-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="54244-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="54244-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="54244-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="54244-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Opal application.</span><span class="sxs-lookup"><span data-stu-id="54244-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Opal application.</span></span>

<span data-ttu-id="54244-148">**To configure Azure AD single sign-on with Opal, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54244-148">**To configure Azure AD single sign-on with Opal, perform the following steps:**</span></span>

1. <span data-ttu-id="54244-149">In the Azure portal, on the **Opal** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="54244-149">In the Azure portal, on the **Opal** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="54244-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="54244-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/opal-tutorial/tutorial_opal_samlbase.png)

1. <span data-ttu-id="54244-153">On the **Opal Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="54244-153">On the **Opal Domain and URLs** section, perform the following steps:</span></span>

    ![Opal Domain and URLs single sign-on information](./media/opal-tutorial/tutorial_opal_url.png)

    <span data-ttu-id="54244-155">a.</span><span class="sxs-lookup"><span data-stu-id="54244-155">a.</span></span> <span data-ttu-id="54244-156">In the **Identifier** textbox, type a value: `Opal`</span><span class="sxs-lookup"><span data-stu-id="54244-156">In the **Identifier** textbox, type a value: `Opal`</span></span>

    <span data-ttu-id="54244-157">b.</span><span class="sxs-lookup"><span data-stu-id="54244-157">b.</span></span> <span data-ttu-id="54244-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.ouropal.com/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="54244-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.ouropal.com/auth/saml/callback`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="54244-159">The Reply URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="54244-159">The Reply URL value is not real.</span></span> <span data-ttu-id="54244-160">Update the value with the actual Reply URL.</span><span class="sxs-lookup"><span data-stu-id="54244-160">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="54244-161">Contact [Opal support team](mailto:support@workwithopal.com) to get the value.</span><span class="sxs-lookup"><span data-stu-id="54244-161">Contact [Opal support team](mailto:support@workwithopal.com) to get the value.</span></span>

1. <span data-ttu-id="54244-162">Opal application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="54244-162">Opal application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="54244-163">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="54244-163">Configure the following claims for this application.</span></span> <span data-ttu-id="54244-164">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="54244-164">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="54244-165">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="54244-165">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On attb](./media/opal-tutorial/tutorial_opal_attribute.png)
    
1. <span data-ttu-id="54244-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="54244-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="54244-168">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="54244-168">Attribute Name</span></span> | <span data-ttu-id="54244-169">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="54244-169">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="54244-170">firstname</span><span class="sxs-lookup"><span data-stu-id="54244-170">firstname</span></span>           | <span data-ttu-id="54244-171">user.givenname</span><span class="sxs-lookup"><span data-stu-id="54244-171">user.givenname</span></span> |
    | <span data-ttu-id="54244-172">lastname</span><span class="sxs-lookup"><span data-stu-id="54244-172">lastname</span></span>        | <span data-ttu-id="54244-173">user.surname</span><span class="sxs-lookup"><span data-stu-id="54244-173">user.surname</span></span> |

    <span data-ttu-id="54244-174">a.</span><span class="sxs-lookup"><span data-stu-id="54244-174">a.</span></span> <span data-ttu-id="54244-175">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="54244-175">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On Add](./media/opal-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On Addattb](./media/opal-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="54244-178">b.</span><span class="sxs-lookup"><span data-stu-id="54244-178">b.</span></span> <span data-ttu-id="54244-179">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="54244-179">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="54244-180">c.</span><span class="sxs-lookup"><span data-stu-id="54244-180">c.</span></span> <span data-ttu-id="54244-181">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="54244-181">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="54244-182">d.</span><span class="sxs-lookup"><span data-stu-id="54244-182">d.</span></span> <span data-ttu-id="54244-183">Leave the **Namespace** blank.</span><span class="sxs-lookup"><span data-stu-id="54244-183">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="54244-184">e.</span><span class="sxs-lookup"><span data-stu-id="54244-184">e.</span></span> <span data-ttu-id="54244-185">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="54244-185">Click **Ok**.</span></span>
 
1. <span data-ttu-id="54244-186">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="54244-186">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/opal-tutorial/tutorial_opal_certificate.png) 

1. <span data-ttu-id="54244-188">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="54244-188">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/opal-tutorial/tutorial_general_400.png) 

1. <span data-ttu-id="54244-190">To configure single sign-on on **Opal** side, you need to send the downloaded **Metadata XML** to [Opal support team](mailto:support@workwithopal.com).</span><span class="sxs-lookup"><span data-stu-id="54244-190">To configure single sign-on on **Opal** side, you need to send the downloaded **Metadata XML** to [Opal support team](mailto:support@workwithopal.com).</span></span> <span data-ttu-id="54244-191">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="54244-191">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="54244-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="54244-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="54244-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="54244-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="54244-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="54244-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="54244-195">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="54244-195">Create an Azure AD test user</span></span>

<span data-ttu-id="54244-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54244-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="54244-198">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54244-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="54244-199">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="54244-199">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/opal-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="54244-201">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="54244-201">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/opal-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="54244-203">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="54244-203">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/opal-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="54244-205">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="54244-205">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/opal-tutorial/create_aaduser_04.png)

    <span data-ttu-id="54244-207">a.</span><span class="sxs-lookup"><span data-stu-id="54244-207">a.</span></span> <span data-ttu-id="54244-208">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="54244-208">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="54244-209">b.</span><span class="sxs-lookup"><span data-stu-id="54244-209">b.</span></span> <span data-ttu-id="54244-210">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54244-210">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="54244-211">c.</span><span class="sxs-lookup"><span data-stu-id="54244-211">c.</span></span> <span data-ttu-id="54244-212">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="54244-212">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="54244-213">d.</span><span class="sxs-lookup"><span data-stu-id="54244-213">d.</span></span> <span data-ttu-id="54244-214">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="54244-214">Click **Create**.</span></span>
  
### <a name="create-an-opal-test-user"></a><span data-ttu-id="54244-215">Create an Opal test user</span><span class="sxs-lookup"><span data-stu-id="54244-215">Create an Opal test user</span></span>

<span data-ttu-id="54244-216">In this section, you create a user called Britta Simon in Opal.</span><span class="sxs-lookup"><span data-stu-id="54244-216">In this section, you create a user called Britta Simon in Opal.</span></span> <span data-ttu-id="54244-217">Work with [Opal support team](mailto:support@workwithopal.com) to add the users in the Opal platform.</span><span class="sxs-lookup"><span data-stu-id="54244-217">Work with [Opal support team](mailto:support@workwithopal.com) to add the users in the Opal platform.</span></span> <span data-ttu-id="54244-218">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="54244-218">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="54244-219">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="54244-219">Assign the Azure AD test user</span></span>

<span data-ttu-id="54244-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Opal.</span><span class="sxs-lookup"><span data-stu-id="54244-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Opal.</span></span>

![Assign the user role][200] 

<span data-ttu-id="54244-222">**To assign Britta Simon to Opal, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54244-222">**To assign Britta Simon to Opal, perform the following steps:**</span></span>

1. <span data-ttu-id="54244-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="54244-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="54244-225">In the applications list, select **Opal**.</span><span class="sxs-lookup"><span data-stu-id="54244-225">In the applications list, select **Opal**.</span></span>

    ![The Opal link in the Applications list](./media/opal-tutorial/tutorial_opal_app.png)  

1. <span data-ttu-id="54244-227">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="54244-227">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="54244-229">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="54244-229">Click **Add** button.</span></span> <span data-ttu-id="54244-230">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="54244-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="54244-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="54244-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="54244-233">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="54244-233">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="54244-234">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="54244-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="54244-235">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="54244-235">Test single sign-on</span></span>

<span data-ttu-id="54244-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="54244-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="54244-237">When you click the Opal tile in the Access Panel, you should get automatically signed-on to your Opal application.</span><span class="sxs-lookup"><span data-stu-id="54244-237">When you click the Opal tile in the Access Panel, you should get automatically signed-on to your Opal application.</span></span>
<span data-ttu-id="54244-238">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="54244-238">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="54244-239">Additional resources</span><span class="sxs-lookup"><span data-stu-id="54244-239">Additional resources</span></span>

* [<span data-ttu-id="54244-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="54244-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="54244-241">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="54244-241">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/opal-tutorial/tutorial_general_01.png
[2]: ./media/opal-tutorial/tutorial_general_02.png
[3]: ./media/opal-tutorial/tutorial_general_03.png
[4]: ./media/opal-tutorial/tutorial_general_04.png

[100]: ./media/opal-tutorial/tutorial_general_100.png

[200]: ./media/opal-tutorial/tutorial_general_200.png
[201]: ./media/opal-tutorial/tutorial_general_201.png
[202]: ./media/opal-tutorial/tutorial_general_202.png
[203]: ./media/opal-tutorial/tutorial_general_203.png

