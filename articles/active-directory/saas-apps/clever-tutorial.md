---
title: 'Tutorial: Azure Active Directory integration with Clever | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Clever.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2018
ms.author: jeedes
ms.openlocfilehash: 483d03fcc72e0a93111d10b0221164459de27d12
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869752"
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a><span data-ttu-id="2e792-103">Tutorial: Azure Active Directory integration with Clever</span><span class="sxs-lookup"><span data-stu-id="2e792-103">Tutorial: Azure Active Directory integration with Clever</span></span>

<span data-ttu-id="2e792-104">In this tutorial, you learn how to integrate Clever with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2e792-104">In this tutorial, you learn how to integrate Clever with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2e792-105">Integrating Clever with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="2e792-105">Integrating Clever with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2e792-106">You can control in Azure AD who has access to Clever.</span><span class="sxs-lookup"><span data-stu-id="2e792-106">You can control in Azure AD who has access to Clever.</span></span>
- <span data-ttu-id="2e792-107">You can enable your users to automatically get signed-on to Clever (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="2e792-107">You can enable your users to automatically get signed-on to Clever (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="2e792-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2e792-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="2e792-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="2e792-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e792-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2e792-110">Prerequisites</span></span>

<span data-ttu-id="2e792-111">To configure Azure AD integration with Clever, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="2e792-111">To configure Azure AD integration with Clever, you need the following items:</span></span>

- <span data-ttu-id="2e792-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="2e792-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2e792-113">A Clever single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="2e792-113">A Clever single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2e792-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="2e792-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2e792-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="2e792-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2e792-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="2e792-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2e792-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2e792-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2e792-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="2e792-118">Scenario description</span></span>
<span data-ttu-id="2e792-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="2e792-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2e792-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="2e792-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2e792-121">Adding Clever from the gallery</span><span class="sxs-lookup"><span data-stu-id="2e792-121">Adding Clever from the gallery</span></span>
1. <span data-ttu-id="2e792-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2e792-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clever-from-the-gallery"></a><span data-ttu-id="2e792-123">Adding Clever from the gallery</span><span class="sxs-lookup"><span data-stu-id="2e792-123">Adding Clever from the gallery</span></span>
<span data-ttu-id="2e792-124">To configure the integration of Clever into Azure AD, you need to add Clever from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="2e792-124">To configure the integration of Clever into Azure AD, you need to add Clever from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2e792-125">**To add Clever from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2e792-125">**To add Clever from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2e792-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="2e792-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="2e792-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="2e792-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2e792-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2e792-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="2e792-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="2e792-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="2e792-133">In the search box, type **Clever**, select **Clever** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="2e792-133">In the search box, type **Clever**, select **Clever** from result panel then click **Add** button to add the application.</span></span>

    ![Clever in the results list](./media/clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2e792-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2e792-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2e792-136">In this section, you configure and test Azure AD single sign-on with Clever based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2e792-136">In this section, you configure and test Azure AD single sign-on with Clever based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2e792-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Clever is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e792-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Clever is to a user in Azure AD.</span></span> <span data-ttu-id="2e792-138">In other words, a link relationship between an Azure AD user and the related user in Clever needs to be established.</span><span class="sxs-lookup"><span data-stu-id="2e792-138">In other words, a link relationship between an Azure AD user and the related user in Clever needs to be established.</span></span>

<span data-ttu-id="2e792-139">In Clever, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="2e792-139">In Clever, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2e792-140">To configure and test Azure AD single sign-on with Clever, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="2e792-140">To configure and test Azure AD single sign-on with Clever, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2e792-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="2e792-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="2e792-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e792-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="2e792-143">**[Create a Clever test user](#create-a-clever-test-user)** - to have a counterpart of Britta Simon in Clever that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="2e792-143">**[Create a Clever test user](#create-a-clever-test-user)** - to have a counterpart of Britta Simon in Clever that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="2e792-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2e792-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="2e792-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="2e792-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2e792-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2e792-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2e792-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clever application.</span><span class="sxs-lookup"><span data-stu-id="2e792-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clever application.</span></span>

<span data-ttu-id="2e792-148">**To configure Azure AD single sign-on with Clever, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2e792-148">**To configure Azure AD single sign-on with Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="2e792-149">In the Azure portal, on the **Clever** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2e792-149">In the Azure portal, on the **Clever** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="2e792-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2e792-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/clever-tutorial/tutorial_clever_samlbase.png)

1. <span data-ttu-id="2e792-153">On the **Clever Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2e792-153">On the **Clever Domain and URLs** section, perform the following steps:</span></span>

    ![Clever Domain and URLs single sign-on information](./media/clever-tutorial/tutorial_clever_url.png)

    <span data-ttu-id="2e792-155">a.</span><span class="sxs-lookup"><span data-stu-id="2e792-155">a.</span></span> <span data-ttu-id="2e792-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://clever.com/in/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="2e792-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://clever.com/in/<companyname>`</span></span>

    <span data-ttu-id="2e792-157">b.</span><span class="sxs-lookup"><span data-stu-id="2e792-157">b.</span></span> <span data-ttu-id="2e792-158">In the **Identifier** textbox, type the URL: `https://clever.com/oauth/saml/metadata.xml`</span><span class="sxs-lookup"><span data-stu-id="2e792-158">In the **Identifier** textbox, type the URL: `https://clever.com/oauth/saml/metadata.xml`</span></span>

    > [!NOTE]
    > <span data-ttu-id="2e792-159">Sign-on URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="2e792-159">Sign-on URL value is not real.</span></span> <span data-ttu-id="2e792-160">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="2e792-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="2e792-161">Contact [Clever Client support team](https://clever.com/about/contact/) to get this value.</span><span class="sxs-lookup"><span data-stu-id="2e792-161">Contact [Clever Client support team](https://clever.com/about/contact/) to get this value.</span></span>

1. <span data-ttu-id="2e792-162">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into Notepad.</span><span class="sxs-lookup"><span data-stu-id="2e792-162">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into Notepad.</span></span>
    
    ![Configure Single Sign-On](./media/clever-tutorial/tutorial_metadataurl.png)

1. <span data-ttu-id="2e792-164">The Clever application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span><span class="sxs-lookup"><span data-stu-id="2e792-164">The Clever application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span>

    <span data-ttu-id="2e792-165">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="2e792-165">The following screenshot shows an example for this.</span></span>

    ![Configure Single Sign-On](./media/clever-tutorial/tutorial_clever_07.png)

1. <span data-ttu-id="2e792-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2e792-167">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="2e792-168">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="2e792-168">Attribute Name</span></span>  | <span data-ttu-id="2e792-169">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="2e792-169">Attribute Value</span></span> |
    | --------------- | -------------------- |
    | <span data-ttu-id="2e792-170">clever.teacher.credentials.district_username</span><span class="sxs-lookup"><span data-stu-id="2e792-170">clever.teacher.credentials.district_username</span></span>|<span data-ttu-id="2e792-171">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="2e792-171">user.userprincipalname</span></span>|
    | <span data-ttu-id="2e792-172">clever.student.credentials.district_username</span><span class="sxs-lookup"><span data-stu-id="2e792-172">clever.student.credentials.district_username</span></span>| <span data-ttu-id="2e792-173">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="2e792-173">user.userprincipalname</span></span> |
    | <span data-ttu-id="2e792-174">Firstname</span><span class="sxs-lookup"><span data-stu-id="2e792-174">Firstname</span></span>  | <span data-ttu-id="2e792-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="2e792-175">user.givenname</span></span> |
    | <span data-ttu-id="2e792-176">Lastname</span><span class="sxs-lookup"><span data-stu-id="2e792-176">Lastname</span></span>  | <span data-ttu-id="2e792-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="2e792-177">user.surname</span></span> |

    <span data-ttu-id="2e792-178">a.</span><span class="sxs-lookup"><span data-stu-id="2e792-178">a.</span></span> <span data-ttu-id="2e792-179">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="2e792-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/clever-tutorial/tutorial_attribute_04.png)
    
    ![Configure Single Sign-On](./media/clever-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="2e792-182">b.</span><span class="sxs-lookup"><span data-stu-id="2e792-182">b.</span></span> <span data-ttu-id="2e792-183">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="2e792-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="2e792-184">c.</span><span class="sxs-lookup"><span data-stu-id="2e792-184">c.</span></span> <span data-ttu-id="2e792-185">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="2e792-185">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="2e792-186">d.</span><span class="sxs-lookup"><span data-stu-id="2e792-186">d.</span></span> <span data-ttu-id="2e792-187">Leave the **Namespace** textbox blank.</span><span class="sxs-lookup"><span data-stu-id="2e792-187">Leave the **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="2e792-188">d.</span><span class="sxs-lookup"><span data-stu-id="2e792-188">d.</span></span> <span data-ttu-id="2e792-189">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="2e792-189">Click **Ok**.</span></span>
    
1. <span data-ttu-id="2e792-190">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="2e792-190">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/clever-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="2e792-192">In a different web browser window, log in to your Clever company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="2e792-192">In a different web browser window, log in to your Clever company site as an administrator.</span></span>

1. <span data-ttu-id="2e792-193">In the toolbar, click **Instant Login**.</span><span class="sxs-lookup"><span data-stu-id="2e792-193">In the toolbar, click **Instant Login**.</span></span>

    <span data-ttu-id="2e792-194">![Instant Login](./media/clever-tutorial/ic798984.png "Instant Login")</span><span class="sxs-lookup"><span data-stu-id="2e792-194">![Instant Login](./media/clever-tutorial/ic798984.png "Instant Login")</span></span>

    > [!NOTE]
    > <span data-ttu-id="2e792-195">Before you can Test single sign-on, You have to contact [Clever Client support team](https://clever.com/about/contact/) to enable Office 365 SSO in the back end.</span><span class="sxs-lookup"><span data-stu-id="2e792-195">Before you can Test single sign-on, You have to contact [Clever Client support team](https://clever.com/about/contact/) to enable Office 365 SSO in the back end.</span></span>

1. <span data-ttu-id="2e792-196">On the **Instant Login** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2e792-196">On the **Instant Login** page, perform the following steps:</span></span>
    
      <span data-ttu-id="2e792-197">![Instant Login](./media/clever-tutorial/ic798985.png "Instant Login")</span><span class="sxs-lookup"><span data-stu-id="2e792-197">![Instant Login](./media/clever-tutorial/ic798985.png "Instant Login")</span></span>
    
      <span data-ttu-id="2e792-198">a.</span><span class="sxs-lookup"><span data-stu-id="2e792-198">a.</span></span> <span data-ttu-id="2e792-199">Type the **Login URL**.</span><span class="sxs-lookup"><span data-stu-id="2e792-199">Type the **Login URL**.</span></span>
    
      >[!NOTE]
      ><span data-ttu-id="2e792-200">The **Login URL** is a custom value.</span><span class="sxs-lookup"><span data-stu-id="2e792-200">The **Login URL** is a custom value.</span></span> <span data-ttu-id="2e792-201">Contact [Clever Client support team](https://clever.com/about/contact/) to get this value.</span><span class="sxs-lookup"><span data-stu-id="2e792-201">Contact [Clever Client support team](https://clever.com/about/contact/) to get this value.</span></span>
    
      <span data-ttu-id="2e792-202">b.</span><span class="sxs-lookup"><span data-stu-id="2e792-202">b.</span></span> <span data-ttu-id="2e792-203">As **Identity System**, select **ADFS**.</span><span class="sxs-lookup"><span data-stu-id="2e792-203">As **Identity System**, select **ADFS**.</span></span>

      <span data-ttu-id="2e792-204">c.</span><span class="sxs-lookup"><span data-stu-id="2e792-204">c.</span></span> <span data-ttu-id="2e792-205">In the **Metadata URL** textbox, paste **App Federation Metadata Url** value which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2e792-205">In the **Metadata URL** textbox, paste **App Federation Metadata Url** value which you have copied from the Azure portal.</span></span>
    
      <span data-ttu-id="2e792-206">d.</span><span class="sxs-lookup"><span data-stu-id="2e792-206">d.</span></span> <span data-ttu-id="2e792-207">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="2e792-207">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2e792-208">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2e792-208">Create an Azure AD test user</span></span>

<span data-ttu-id="2e792-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e792-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="2e792-211">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2e792-211">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2e792-212">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="2e792-212">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/clever-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="2e792-214">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="2e792-214">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/clever-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="2e792-216">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="2e792-216">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/clever-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="2e792-218">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2e792-218">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/clever-tutorial/create_aaduser_04.png)

    <span data-ttu-id="2e792-220">a.</span><span class="sxs-lookup"><span data-stu-id="2e792-220">a.</span></span> <span data-ttu-id="2e792-221">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2e792-221">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2e792-222">b.</span><span class="sxs-lookup"><span data-stu-id="2e792-222">b.</span></span> <span data-ttu-id="2e792-223">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e792-223">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="2e792-224">c.</span><span class="sxs-lookup"><span data-stu-id="2e792-224">c.</span></span> <span data-ttu-id="2e792-225">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="2e792-225">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="2e792-226">d.</span><span class="sxs-lookup"><span data-stu-id="2e792-226">d.</span></span> <span data-ttu-id="2e792-227">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="2e792-227">Click **Create**.</span></span>

### <a name="create-a-clever-test-user"></a><span data-ttu-id="2e792-228">Create a Clever test user</span><span class="sxs-lookup"><span data-stu-id="2e792-228">Create a Clever test user</span></span>

<span data-ttu-id="2e792-229">To enable Azure AD users to log in to Clever, they must be provisioned into Clever.</span><span class="sxs-lookup"><span data-stu-id="2e792-229">To enable Azure AD users to log in to Clever, they must be provisioned into Clever.</span></span>

<span data-ttu-id="2e792-230">In case of Clever, Work with [Clever Client support team](https://clever.com/about/contact/) to add the users in the Clever platform.</span><span class="sxs-lookup"><span data-stu-id="2e792-230">In case of Clever, Work with [Clever Client support team](https://clever.com/about/contact/) to add the users in the Clever platform.</span></span> <span data-ttu-id="2e792-231">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2e792-231">Users must be created and activated before you use single sign-on.</span></span>

>[!NOTE]
><span data-ttu-id="2e792-232">You can use any other Clever user account creation tools or APIs provided by Clever to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="2e792-232">You can use any other Clever user account creation tools or APIs provided by Clever to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="2e792-233">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2e792-233">Assign the Azure AD test user</span></span>

<span data-ttu-id="2e792-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Clever.</span><span class="sxs-lookup"><span data-stu-id="2e792-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Clever.</span></span>

![Assign the user role][200]

<span data-ttu-id="2e792-236">**To assign Britta Simon to Clever, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2e792-236">**To assign Britta Simon to Clever, perform the following steps:**</span></span>

1. <span data-ttu-id="2e792-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2e792-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

1. <span data-ttu-id="2e792-239">In the applications list, select **Clever**.</span><span class="sxs-lookup"><span data-stu-id="2e792-239">In the applications list, select **Clever**.</span></span>

    ![The Clever link in the Applications list](./media/clever-tutorial/tutorial_clever_app.png)

1. <span data-ttu-id="2e792-241">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="2e792-241">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="2e792-243">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="2e792-243">Click **Add** button.</span></span> <span data-ttu-id="2e792-244">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2e792-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="2e792-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="2e792-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="2e792-247">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="2e792-247">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="2e792-248">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2e792-248">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="2e792-249">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="2e792-249">Test single sign-on</span></span>

<span data-ttu-id="2e792-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="2e792-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2e792-251">When you click the Clever tile in the Access Panel, you should get automatically signed-on to your Clever application.</span><span class="sxs-lookup"><span data-stu-id="2e792-251">When you click the Clever tile in the Access Panel, you should get automatically signed-on to your Clever application.</span></span>
<span data-ttu-id="2e792-252">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2e792-252">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2e792-253">Additional resources</span><span class="sxs-lookup"><span data-stu-id="2e792-253">Additional resources</span></span>

* [<span data-ttu-id="2e792-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2e792-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="2e792-255">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2e792-255">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/clever-tutorial/tutorial_general_01.png
[2]: ./media/clever-tutorial/tutorial_general_02.png
[3]: ./media/clever-tutorial/tutorial_general_03.png
[4]: ./media/clever-tutorial/tutorial_general_04.png

[100]: ./media/clever-tutorial/tutorial_general_100.png

[200]: ./media/clever-tutorial/tutorial_general_200.png
[201]: ./media/clever-tutorial/tutorial_general_201.png
[202]: ./media/clever-tutorial/tutorial_general_202.png
[203]: ./media/clever-tutorial/tutorial_general_203.png

