---
title: 'Tutorial: Azure Active Directory integration with Trello | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Trello.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/04/2017
ms.author: jeedes
ms.openlocfilehash: 163d7faa99d362f400581c42974eeb4a466641d9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868712"
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a><span data-ttu-id="a9771-103">Tutorial: Azure Active Directory integration with Trello</span><span class="sxs-lookup"><span data-stu-id="a9771-103">Tutorial: Azure Active Directory integration with Trello</span></span>

<span data-ttu-id="a9771-104">In this tutorial, you learn how to integrate Trello with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a9771-104">In this tutorial, you learn how to integrate Trello with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a9771-105">Integrating Trello with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a9771-105">Integrating Trello with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a9771-106">You can control in Azure AD who has access to Trello.</span><span class="sxs-lookup"><span data-stu-id="a9771-106">You can control in Azure AD who has access to Trello.</span></span>
- <span data-ttu-id="a9771-107">You can enable your users to automatically get signed-on to Trello (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="a9771-107">You can enable your users to automatically get signed-on to Trello (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a9771-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a9771-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="a9771-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a9771-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9771-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a9771-110">Prerequisites</span></span>

<span data-ttu-id="a9771-111">To configure Azure AD integration with Trello, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a9771-111">To configure Azure AD integration with Trello, you need the following items:</span></span>

- <span data-ttu-id="a9771-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a9771-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a9771-113">A Trello single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a9771-113">A Trello single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a9771-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a9771-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a9771-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a9771-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a9771-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a9771-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a9771-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a9771-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a9771-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a9771-118">Scenario description</span></span>
<span data-ttu-id="a9771-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a9771-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a9771-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a9771-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a9771-121">Adding Trello from the gallery</span><span class="sxs-lookup"><span data-stu-id="a9771-121">Adding Trello from the gallery</span></span>
1. <span data-ttu-id="a9771-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a9771-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trello-from-the-gallery"></a><span data-ttu-id="a9771-123">Adding Trello from the gallery</span><span class="sxs-lookup"><span data-stu-id="a9771-123">Adding Trello from the gallery</span></span>
<span data-ttu-id="a9771-124">To configure the integration of Trello into Azure AD, you need to add Trello from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a9771-124">To configure the integration of Trello into Azure AD, you need to add Trello from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a9771-125">**To add Trello from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a9771-125">**To add Trello from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a9771-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a9771-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="a9771-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a9771-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a9771-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a9771-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="a9771-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a9771-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="a9771-133">In the search box, type **Trello**, select **Trello** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a9771-133">In the search box, type **Trello**, select **Trello** from result panel then click **Add** button to add the application.</span></span>

    ![Trello in the results list](./media/trello-tutorial/tutorial_trello_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a9771-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a9771-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a9771-136">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a9771-136">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a9771-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Trello is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9771-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Trello is to a user in Azure AD.</span></span> <span data-ttu-id="a9771-138">In other words, a link relationship between an Azure AD user and the related user in Trello needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a9771-138">In other words, a link relationship between an Azure AD user and the related user in Trello needs to be established.</span></span>

<span data-ttu-id="a9771-139">In Trello, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="a9771-139">In Trello, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a9771-140">To configure and test Azure AD single sign-on with Trello, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a9771-140">To configure and test Azure AD single sign-on with Trello, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a9771-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a9771-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="a9771-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9771-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="a9771-143">**[Create a Trello test user](#create-a-trello-test-user)** - to have a counterpart of Britta Simon in Trello that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a9771-143">**[Create a Trello test user](#create-a-trello-test-user)** - to have a counterpart of Britta Simon in Trello that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="a9771-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a9771-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="a9771-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a9771-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a9771-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a9771-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a9771-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trello application.</span><span class="sxs-lookup"><span data-stu-id="a9771-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Trello application.</span></span>

>[!NOTE]
><span data-ttu-id="a9771-148">You should get the **\<enterprise\>** slug from Trello.</span><span class="sxs-lookup"><span data-stu-id="a9771-148">You should get the **\<enterprise\>** slug from Trello.</span></span> <span data-ttu-id="a9771-149">If you don't have the slug value, contact [Trello support team](mailto:support@trello.com) to get the slug for you enterprise.</span><span class="sxs-lookup"><span data-stu-id="a9771-149">If you don't have the slug value, contact [Trello support team](mailto:support@trello.com) to get the slug for you enterprise.</span></span>
    > 

<span data-ttu-id="a9771-150">**To configure Azure AD single sign-on with Trello, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a9771-150">**To configure Azure AD single sign-on with Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="a9771-151">In the Azure portal, on the **Trello** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a9771-151">In the Azure portal, on the **Trello** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="a9771-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a9771-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/trello-tutorial/tutorial_trello_samlbase.png)

1. <span data-ttu-id="a9771-155">On the **Trello Domain and URLs** section, if you wish to configure the application in **IDP initiated mode**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a9771-155">On the **Trello Domain and URLs** section, if you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Trello Domain and URLs single sign-on information](./media/trello-tutorial/tutorial_trello_url.png)
    
    <span data-ttu-id="a9771-157">a.</span><span class="sxs-lookup"><span data-stu-id="a9771-157">a.</span></span> <span data-ttu-id="a9771-158">In the **Identifier** textbox, type the following URL: `https://trello.com/auth/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="a9771-158">In the **Identifier** textbox, type the following URL: `https://trello.com/auth/saml/metadata`</span></span>
    
    <span data-ttu-id="a9771-159">b.</span><span class="sxs-lookup"><span data-stu-id="a9771-159">b.</span></span> <span data-ttu-id="a9771-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="a9771-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

1. <span data-ttu-id="a9771-161">If you wish to configure the application in **SP initiated mode**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a9771-161">If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>

    ![Trello Domain and URLs single sign-on information](./media/trello-tutorial/tutorial_trello_url1.png)

    <span data-ttu-id="a9771-163">a.</span><span class="sxs-lookup"><span data-stu-id="a9771-163">a.</span></span> <span data-ttu-id="a9771-164">Check **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="a9771-164">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="a9771-165">b.</span><span class="sxs-lookup"><span data-stu-id="a9771-165">b.</span></span> <span data-ttu-id="a9771-166">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/login/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="a9771-166">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://trello.com/auth/saml/login/<enterprise>`</span></span> 

1. <span data-ttu-id="a9771-167">Trello application expects the SAML assertions to contain specific attributes.</span><span class="sxs-lookup"><span data-stu-id="a9771-167">Trello application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="a9771-168">Configure the following attributes  for this application.</span><span class="sxs-lookup"><span data-stu-id="a9771-168">Configure the following attributes  for this application.</span></span> <span data-ttu-id="a9771-169">You can manage the values of these attributes from the **"User Attributes"** of the application.</span><span class="sxs-lookup"><span data-stu-id="a9771-169">You can manage the values of these attributes from the **"User Attributes"** of the application.</span></span> <span data-ttu-id="a9771-170">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="a9771-170">The following screenshot shows an example for this.</span></span>

    ![Configure Single Sign-On](./media/trello-tutorial/tutorial_trello_attribute.png)

1. <span data-ttu-id="a9771-172">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a9771-172">On the **SAML token attributes** dialog, for each row shown in the table below, perform the following steps:</span></span>
 
    | <span data-ttu-id="a9771-173">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="a9771-173">Attribute Name</span></span> | <span data-ttu-id="a9771-174">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="a9771-174">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="a9771-175">User.Email</span><span class="sxs-lookup"><span data-stu-id="a9771-175">User.Email</span></span> | <span data-ttu-id="a9771-176">user.mail</span><span class="sxs-lookup"><span data-stu-id="a9771-176">user.mail</span></span> |
    | <span data-ttu-id="a9771-177">User.FirstName</span><span class="sxs-lookup"><span data-stu-id="a9771-177">User.FirstName</span></span> | <span data-ttu-id="a9771-178">user.givenname</span><span class="sxs-lookup"><span data-stu-id="a9771-178">user.givenname</span></span> |
    | <span data-ttu-id="a9771-179">User.LastName</span><span class="sxs-lookup"><span data-stu-id="a9771-179">User.LastName</span></span> | <span data-ttu-id="a9771-180">user.surname</span><span class="sxs-lookup"><span data-stu-id="a9771-180">user.surname</span></span> |

    <span data-ttu-id="a9771-181">a.</span><span class="sxs-lookup"><span data-stu-id="a9771-181">a.</span></span> <span data-ttu-id="a9771-182">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="a9771-182">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/trello-tutorial/tutorial_officespace_04.png)

    ![Configure Single Sign-On](./media/trello-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="a9771-185">b.</span><span class="sxs-lookup"><span data-stu-id="a9771-185">b.</span></span> <span data-ttu-id="a9771-186">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="a9771-186">In the **Name** textbox, type the attribute name shown for that row.</span></span> 

    <span data-ttu-id="a9771-187">c.</span><span class="sxs-lookup"><span data-stu-id="a9771-187">c.</span></span> <span data-ttu-id="a9771-188">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="a9771-188">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="a9771-189">d.</span><span class="sxs-lookup"><span data-stu-id="a9771-189">d.</span></span> <span data-ttu-id="a9771-190">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="a9771-190">Click **Ok**.</span></span> 

1. <span data-ttu-id="a9771-191">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a9771-191">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/trello-tutorial/tutorial_trello_certificate.png) 

1. <span data-ttu-id="a9771-193">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a9771-193">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/trello-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="a9771-195">On the **Trello Configuration** section, click **Configure Trello** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="a9771-195">On the **Trello Configuration** section, click **Configure Trello** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a9771-196">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="a9771-196">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Trello Configuration](./media/trello-tutorial/tutorial_trello_configure.png) 

1. <span data-ttu-id="a9771-198">To configure single sign-on on **Trello** side, you need to go to the [Trello enterprise SSO configuration](https://trello.com/sso-configuration) page to send the downloaded **Certificate (Base64)** and **SAML Single Sign-On Service URL** to [Trello support team](mailto:support@trello.com).</span><span class="sxs-lookup"><span data-stu-id="a9771-198">To configure single sign-on on **Trello** side, you need to go to the [Trello enterprise SSO configuration](https://trello.com/sso-configuration) page to send the downloaded **Certificate (Base64)** and **SAML Single Sign-On Service URL** to [Trello support team](mailto:support@trello.com).</span></span> <span data-ttu-id="a9771-199">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="a9771-199">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a9771-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="a9771-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a9771-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="a9771-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a9771-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a9771-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a9771-203">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a9771-203">Create an Azure AD test user</span></span>

<span data-ttu-id="a9771-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9771-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="a9771-206">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a9771-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a9771-207">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="a9771-207">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/trello-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="a9771-209">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a9771-209">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/trello-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="a9771-211">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="a9771-211">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/trello-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="a9771-213">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a9771-213">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/trello-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a9771-215">a.</span><span class="sxs-lookup"><span data-stu-id="a9771-215">a.</span></span> <span data-ttu-id="a9771-216">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a9771-216">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a9771-217">b.</span><span class="sxs-lookup"><span data-stu-id="a9771-217">b.</span></span> <span data-ttu-id="a9771-218">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9771-218">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="a9771-219">c.</span><span class="sxs-lookup"><span data-stu-id="a9771-219">c.</span></span> <span data-ttu-id="a9771-220">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="a9771-220">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="a9771-221">d.</span><span class="sxs-lookup"><span data-stu-id="a9771-221">d.</span></span> <span data-ttu-id="a9771-222">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a9771-222">Click **Create**.</span></span>
 
### <a name="create-a-trello-test-user"></a><span data-ttu-id="a9771-223">Create a Trello test user</span><span class="sxs-lookup"><span data-stu-id="a9771-223">Create a Trello test user</span></span>

<span data-ttu-id="a9771-224">The objective of this section is to create a user called Britta Simon in Trello.</span><span class="sxs-lookup"><span data-stu-id="a9771-224">The objective of this section is to create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="a9771-225">Trello supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="a9771-225">Trello supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="a9771-226">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="a9771-226">There is no action item for you in this section.</span></span> <span data-ttu-id="a9771-227">A new user is created during an attempt to access Trello if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="a9771-227">A new user is created during an attempt to access Trello if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="a9771-228">If you need to create a user manually, Contact [Trello support team](mailto:support@trello.com).</span><span class="sxs-lookup"><span data-stu-id="a9771-228">If you need to create a user manually, Contact [Trello support team](mailto:support@trello.com).</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a9771-229">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a9771-229">Assign the Azure AD test user</span></span>

<span data-ttu-id="a9771-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trello.</span><span class="sxs-lookup"><span data-stu-id="a9771-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Trello.</span></span>

![Assign the user role][200] 

<span data-ttu-id="a9771-232">**To assign Britta Simon to Trello, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a9771-232">**To assign Britta Simon to Trello, perform the following steps:**</span></span>

1. <span data-ttu-id="a9771-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a9771-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="a9771-235">In the applications list, select **Trello**.</span><span class="sxs-lookup"><span data-stu-id="a9771-235">In the applications list, select **Trello**.</span></span>

    ![The Trello link in the Applications list](./media/trello-tutorial/tutorial_trello_app.png)  

1. <span data-ttu-id="a9771-237">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a9771-237">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="a9771-239">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a9771-239">Click **Add** button.</span></span> <span data-ttu-id="a9771-240">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a9771-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="a9771-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a9771-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="a9771-243">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a9771-243">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="a9771-244">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a9771-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a9771-245">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="a9771-245">Test single sign-on</span></span>

<span data-ttu-id="a9771-246">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a9771-246">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a9771-247">When you click the Trello tile in the Access Panel, you should get automatically signed-on to your Trello application.</span><span class="sxs-lookup"><span data-stu-id="a9771-247">When you click the Trello tile in the Access Panel, you should get automatically signed-on to your Trello application.</span></span>
<span data-ttu-id="a9771-248">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a9771-248">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a9771-249">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a9771-249">Additional resources</span></span>

* [<span data-ttu-id="a9771-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a9771-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a9771-251">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a9771-251">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/trello-tutorial/tutorial_general_01.png
[2]: ./media/trello-tutorial/tutorial_general_02.png
[3]: ./media/trello-tutorial/tutorial_general_03.png
[4]: ./media/trello-tutorial/tutorial_general_04.png

[100]: ./media/trello-tutorial/tutorial_general_100.png

[200]: ./media/trello-tutorial/tutorial_general_200.png
[201]: ./media/trello-tutorial/tutorial_general_201.png
[202]: ./media/trello-tutorial/tutorial_general_202.png
[203]: ./media/trello-tutorial/tutorial_general_203.png

