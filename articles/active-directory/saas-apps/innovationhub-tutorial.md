---
title: 'Tutorial: Azure Active Directory integration with Innovation Hub | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Innovation Hub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d72e4da0-0123-409b-96c2-e613f3f83fb1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2018
ms.author: jeedes
ms.openlocfilehash: 6486c43ed9eaf1e829598cfc9177a96e0bed9fe1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871591"
---
# <a name="tutorial-azure-active-directory-integration-with-innovation-hub"></a><span data-ttu-id="893dc-103">Tutorial: Azure Active Directory integration with Innovation Hub</span><span class="sxs-lookup"><span data-stu-id="893dc-103">Tutorial: Azure Active Directory integration with Innovation Hub</span></span>

<span data-ttu-id="893dc-104">In this tutorial, you learn how to integrate Innovation Hub with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="893dc-104">In this tutorial, you learn how to integrate Innovation Hub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="893dc-105">Integrating Innovation Hub with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="893dc-105">Integrating Innovation Hub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="893dc-106">You can control in Azure AD who has access to Innovation Hub.</span><span class="sxs-lookup"><span data-stu-id="893dc-106">You can control in Azure AD who has access to Innovation Hub.</span></span>
- <span data-ttu-id="893dc-107">You can enable your users to automatically get signed-on to Innovation Hub (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="893dc-107">You can enable your users to automatically get signed-on to Innovation Hub (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="893dc-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="893dc-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="893dc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="893dc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="893dc-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="893dc-110">Prerequisites</span></span>

<span data-ttu-id="893dc-111">To configure Azure AD integration with Innovation Hub, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="893dc-111">To configure Azure AD integration with Innovation Hub, you need the following items:</span></span>

- <span data-ttu-id="893dc-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="893dc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="893dc-113">An Innovation Hub single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="893dc-113">An Innovation Hub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="893dc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="893dc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="893dc-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="893dc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="893dc-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="893dc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="893dc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="893dc-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="893dc-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="893dc-118">Scenario description</span></span>
<span data-ttu-id="893dc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="893dc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="893dc-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="893dc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="893dc-121">Adding Innovation Hub from the gallery</span><span class="sxs-lookup"><span data-stu-id="893dc-121">Adding Innovation Hub from the gallery</span></span>
1. <span data-ttu-id="893dc-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="893dc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-innovation-hub-from-the-gallery"></a><span data-ttu-id="893dc-123">Adding Innovation Hub from the gallery</span><span class="sxs-lookup"><span data-stu-id="893dc-123">Adding Innovation Hub from the gallery</span></span>
<span data-ttu-id="893dc-124">To configure the integration of Innovation Hub into Azure AD, you need to add Innovation Hub from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="893dc-124">To configure the integration of Innovation Hub into Azure AD, you need to add Innovation Hub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="893dc-125">**To add Innovation Hub from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="893dc-125">**To add Innovation Hub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="893dc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="893dc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="893dc-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="893dc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="893dc-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="893dc-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="893dc-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="893dc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="893dc-133">In the search box, type **Innovation Hub**, select **Innovation Hub** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="893dc-133">In the search box, type **Innovation Hub**, select **Innovation Hub** from result panel then click **Add** button to add the application.</span></span>

    ![Innovation Hub in the results list](./media/innovationhub-tutorial/tutorial_innovationhub_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="893dc-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="893dc-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="893dc-136">In this section, you configure and test Azure AD single sign-on with Innovation Hub based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="893dc-136">In this section, you configure and test Azure AD single sign-on with Innovation Hub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="893dc-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Innovation Hub is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="893dc-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Innovation Hub is to a user in Azure AD.</span></span> <span data-ttu-id="893dc-138">In other words, a link relationship between an Azure AD user and the related user in Innovation Hub needs to be established.</span><span class="sxs-lookup"><span data-stu-id="893dc-138">In other words, a link relationship between an Azure AD user and the related user in Innovation Hub needs to be established.</span></span>

<span data-ttu-id="893dc-139">To configure and test Azure AD single sign-on with Innovation Hub, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="893dc-139">To configure and test Azure AD single sign-on with Innovation Hub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="893dc-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="893dc-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="893dc-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="893dc-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="893dc-142">**[Create an Innovation Hub test user](#create-an-innovation-hub-test-user)** - to have a counterpart of Britta Simon in Innovation Hub that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="893dc-142">**[Create an Innovation Hub test user](#create-an-innovation-hub-test-user)** - to have a counterpart of Britta Simon in Innovation Hub that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="893dc-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="893dc-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="893dc-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="893dc-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="893dc-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="893dc-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="893dc-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Innovation Hub application.</span><span class="sxs-lookup"><span data-stu-id="893dc-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Innovation Hub application.</span></span>

<span data-ttu-id="893dc-147">**To configure Azure AD single sign-on with Innovation Hub, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="893dc-147">**To configure Azure AD single sign-on with Innovation Hub, perform the following steps:**</span></span>

1. <span data-ttu-id="893dc-148">In the Azure portal, on the **Innovation Hub** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="893dc-148">In the Azure portal, on the **Innovation Hub** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="893dc-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="893dc-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/innovationhub-tutorial/tutorial_innovationhub_samlbase.png)

1. <span data-ttu-id="893dc-152">On the **Innovation Hub Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="893dc-152">On the **Innovation Hub Domain and URLs** section, perform the following steps:</span></span>

    ![Innovation Hub Domain and URLs single sign-on information](./media/innovationhub-tutorial/tutorial_innovationhub_url.png)

    <span data-ttu-id="893dc-154">a.</span><span class="sxs-lookup"><span data-stu-id="893dc-154">a.</span></span> <span data-ttu-id="893dc-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<domainname>.innohb.com/auth/saml2/login`</span><span class="sxs-lookup"><span data-stu-id="893dc-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<domainname>.innohb.com/auth/saml2/login`</span></span>

    <span data-ttu-id="893dc-156">b.</span><span class="sxs-lookup"><span data-stu-id="893dc-156">b.</span></span> <span data-ttu-id="893dc-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<domainname>.innohb.com`</span><span class="sxs-lookup"><span data-stu-id="893dc-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<domainname>.innohb.com`</span></span>

    > [!NOTE]
    > <span data-ttu-id="893dc-158">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="893dc-158">These values are not real.</span></span> <span data-ttu-id="893dc-159">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="893dc-159">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="893dc-160">Contact [Innovation Hub Client support team](mailto:support@readify.net) to get these values.</span><span class="sxs-lookup"><span data-stu-id="893dc-160">Contact [Innovation Hub Client support team](mailto:support@readify.net) to get these values.</span></span>

1. <span data-ttu-id="893dc-161">Innovation Hub application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="893dc-161">Innovation Hub application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="893dc-162">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="893dc-162">Please configure the following claims for this application.</span></span> <span data-ttu-id="893dc-163">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="893dc-163">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="893dc-164">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="893dc-164">The following screenshot shows an example for this.</span></span>

    ![Configure Single Sign-On](./media/innovationhub-tutorial/attribute.png)

1. <span data-ttu-id="893dc-166">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span><span class="sxs-lookup"><span data-stu-id="893dc-166">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="893dc-167">Perform the following steps on each of the displayed attributes-</span><span class="sxs-lookup"><span data-stu-id="893dc-167">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="893dc-168">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="893dc-168">Attribute Name</span></span> | <span data-ttu-id="893dc-169">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="893dc-169">Attribute Value</span></span> | <span data-ttu-id="893dc-170">Namespace Value</span><span class="sxs-lookup"><span data-stu-id="893dc-170">Namespace Value</span></span>|
    | ---------------| --------------- |----------------|
    | <span data-ttu-id="893dc-171">displayname</span><span class="sxs-lookup"><span data-stu-id="893dc-171">displayname</span></span> | <span data-ttu-id="893dc-172">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="893dc-172">user.userprincipalname</span></span> | `http://schemas.xmlsoap.org/ws/2005/05/identity/claims`|
    | | |

    <span data-ttu-id="893dc-173">a.</span><span class="sxs-lookup"><span data-stu-id="893dc-173">a.</span></span> <span data-ttu-id="893dc-174">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="893dc-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/innovationhub-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/innovationhub-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="893dc-177">b.</span><span class="sxs-lookup"><span data-stu-id="893dc-177">b.</span></span> <span data-ttu-id="893dc-178">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="893dc-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="893dc-179">c.</span><span class="sxs-lookup"><span data-stu-id="893dc-179">c.</span></span> <span data-ttu-id="893dc-180">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="893dc-180">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="893dc-181">d.</span><span class="sxs-lookup"><span data-stu-id="893dc-181">d.</span></span> <span data-ttu-id="893dc-182">From the **Namespace Value** list, type the namespace value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="893dc-182">From the **Namespace Value** list, type the namespace value shown for that row.</span></span>

    <span data-ttu-id="893dc-183">e.</span><span class="sxs-lookup"><span data-stu-id="893dc-183">e.</span></span> <span data-ttu-id="893dc-184">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="893dc-184">Click **Ok**.</span></span>

1. <span data-ttu-id="893dc-185">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="893dc-185">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>

    ![The Certificate download link](./media/innovationhub-tutorial/tutorial_innovationhub_certificate.png)

1. <span data-ttu-id="893dc-187">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="893dc-187">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/innovationhub-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="893dc-189">To configure single sign-on on **Innovation Hub** side, you need to send the copied **Federation Metadata Url** to [Innovation Hub support team](mailto:support@readify.net).</span><span class="sxs-lookup"><span data-stu-id="893dc-189">To configure single sign-on on **Innovation Hub** side, you need to send the copied **Federation Metadata Url** to [Innovation Hub support team](mailto:support@readify.net).</span></span> <span data-ttu-id="893dc-190">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="893dc-190">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="893dc-191">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="893dc-191">Create an Azure AD test user</span></span>

<span data-ttu-id="893dc-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="893dc-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="893dc-194">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="893dc-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="893dc-195">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="893dc-195">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/innovationhub-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="893dc-197">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="893dc-197">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/innovationhub-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="893dc-199">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="893dc-199">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/innovationhub-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="893dc-201">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="893dc-201">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/innovationhub-tutorial/create_aaduser_04.png)

    <span data-ttu-id="893dc-203">a.</span><span class="sxs-lookup"><span data-stu-id="893dc-203">a.</span></span> <span data-ttu-id="893dc-204">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="893dc-204">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="893dc-205">b.</span><span class="sxs-lookup"><span data-stu-id="893dc-205">b.</span></span> <span data-ttu-id="893dc-206">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="893dc-206">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="893dc-207">c.</span><span class="sxs-lookup"><span data-stu-id="893dc-207">c.</span></span> <span data-ttu-id="893dc-208">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="893dc-208">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="893dc-209">d.</span><span class="sxs-lookup"><span data-stu-id="893dc-209">d.</span></span> <span data-ttu-id="893dc-210">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="893dc-210">Click **Create**.</span></span>
 
### <a name="create-an-innovation-hub-test-user"></a><span data-ttu-id="893dc-211">Create an Innovation Hub test user</span><span class="sxs-lookup"><span data-stu-id="893dc-211">Create an Innovation Hub test user</span></span>

<span data-ttu-id="893dc-212">The objective of this section is to create a user called Britta Simon in Innovation Hub.</span><span class="sxs-lookup"><span data-stu-id="893dc-212">The objective of this section is to create a user called Britta Simon in Innovation Hub.</span></span> <span data-ttu-id="893dc-213">Innovation Hub supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="893dc-213">Innovation Hub supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="893dc-214">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="893dc-214">There is no action item for you in this section.</span></span> <span data-ttu-id="893dc-215">A new user is created during an attempt to access Innovation Hub if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="893dc-215">A new user is created during an attempt to access Innovation Hub if it doesn't exist yet.</span></span>
>[!Note]
><span data-ttu-id="893dc-216">If you need to create a user manually, contact [Innovation Hub support team](mailto:support@readify.net).</span><span class="sxs-lookup"><span data-stu-id="893dc-216">If you need to create a user manually, contact [Innovation Hub support team](mailto:support@readify.net).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="893dc-217">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="893dc-217">Assign the Azure AD test user</span></span>

<span data-ttu-id="893dc-218">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Innovation Hub.</span><span class="sxs-lookup"><span data-stu-id="893dc-218">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Innovation Hub.</span></span>

![Assign the user role][200] 

<span data-ttu-id="893dc-220">**To assign Britta Simon to Innovation Hub, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="893dc-220">**To assign Britta Simon to Innovation Hub, perform the following steps:**</span></span>

1. <span data-ttu-id="893dc-221">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="893dc-221">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="893dc-223">In the applications list, select **Innovation Hub**.</span><span class="sxs-lookup"><span data-stu-id="893dc-223">In the applications list, select **Innovation Hub**.</span></span>

    ![The Innovation Hub link in the Applications list](./media/innovationhub-tutorial/tutorial_innovationhub_app.png)  

1. <span data-ttu-id="893dc-225">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="893dc-225">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="893dc-227">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="893dc-227">Click **Add** button.</span></span> <span data-ttu-id="893dc-228">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="893dc-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="893dc-230">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="893dc-230">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="893dc-231">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="893dc-231">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="893dc-232">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="893dc-232">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="893dc-233">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="893dc-233">Test single sign-on</span></span>

<span data-ttu-id="893dc-234">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="893dc-234">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="893dc-235">When you click the Innovation Hub tile in the Access Panel, you should get automatically signed-on to your Innovation Hub application.</span><span class="sxs-lookup"><span data-stu-id="893dc-235">When you click the Innovation Hub tile in the Access Panel, you should get automatically signed-on to your Innovation Hub application.</span></span>
<span data-ttu-id="893dc-236">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="893dc-236">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="893dc-237">Additional resources</span><span class="sxs-lookup"><span data-stu-id="893dc-237">Additional resources</span></span>

* [<span data-ttu-id="893dc-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="893dc-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* <span data-ttu-id="893dc-239">[What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)
<!--Image references--></span><span class="sxs-lookup"><span data-stu-id="893dc-239">[What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)
<!--Image references--></span></span>

[1]: ./media/innovationhub-tutorial/tutorial_general_01.png
[2]: ./media/innovationhub-tutorial/tutorial_general_02.png
[3]: ./media/innovationhub-tutorial/tutorial_general_03.png
[4]: ./media/innovationhub-tutorial/tutorial_general_04.png

[100]: ./media/innovationhub-tutorial/tutorial_general_100.png

[200]: ./media/innovationhub-tutorial/tutorial_general_200.png
[201]: ./media/innovationhub-tutorial/tutorial_general_201.png
[202]: ./media/innovationhub-tutorial/tutorial_general_202.png
[203]: ./media/innovationhub-tutorial/tutorial_general_203.png

