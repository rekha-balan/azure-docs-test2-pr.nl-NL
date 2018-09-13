---
title: 'Tutorial: Azure Active Directory integration with Allocadia | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Allocadia.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: c415fc55-6dc1-49f2-a8a2-2fc6e3790d65
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: jeedes
ms.openlocfilehash: a25fbd4daaa4d1fb09d788ba7ab61392ffb100f2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869623"
---
# <a name="tutorial-azure-active-directory-integration-with-allocadia"></a><span data-ttu-id="840c5-103">Tutorial: Azure Active Directory integration with Allocadia</span><span class="sxs-lookup"><span data-stu-id="840c5-103">Tutorial: Azure Active Directory integration with Allocadia</span></span>

<span data-ttu-id="840c5-104">In this tutorial, you learn how to integrate Allocadia with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="840c5-104">In this tutorial, you learn how to integrate Allocadia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="840c5-105">Integrating Allocadia with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="840c5-105">Integrating Allocadia with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="840c5-106">You can control in Azure AD who has access to Allocadia</span><span class="sxs-lookup"><span data-stu-id="840c5-106">You can control in Azure AD who has access to Allocadia</span></span>
- <span data-ttu-id="840c5-107">You can enable your users to automatically get signed-on to Allocadia (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="840c5-107">You can enable your users to automatically get signed-on to Allocadia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="840c5-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="840c5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="840c5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="840c5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="840c5-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="840c5-110">Prerequisites</span></span>

<span data-ttu-id="840c5-111">To configure Azure AD integration with Allocadia, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="840c5-111">To configure Azure AD integration with Allocadia, you need the following items:</span></span>

- <span data-ttu-id="840c5-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="840c5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="840c5-113">An Allocadia single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="840c5-113">An Allocadia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="840c5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="840c5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="840c5-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="840c5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="840c5-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="840c5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="840c5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="840c5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="840c5-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="840c5-118">Scenario description</span></span>
<span data-ttu-id="840c5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="840c5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="840c5-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="840c5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="840c5-121">Adding Allocadia from the gallery</span><span class="sxs-lookup"><span data-stu-id="840c5-121">Adding Allocadia from the gallery</span></span>
2. <span data-ttu-id="840c5-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="840c5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-allocadia-from-the-gallery"></a><span data-ttu-id="840c5-123">Adding Allocadia from the gallery</span><span class="sxs-lookup"><span data-stu-id="840c5-123">Adding Allocadia from the gallery</span></span>
<span data-ttu-id="840c5-124">To configure the integration of Allocadia into Azure AD, you need to add Allocadia from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="840c5-124">To configure the integration of Allocadia into Azure AD, you need to add Allocadia from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="840c5-125">**To add Allocadia from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="840c5-125">**To add Allocadia from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="840c5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="840c5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="840c5-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="840c5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="840c5-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="840c5-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="840c5-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="840c5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="840c5-133">In the search box, type **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="840c5-133">In the search box, type **Allocadia**.</span></span>

    ![Creating an Azure AD test user](./media/allocadia-tutorial/tutorial_allocadia_search.png)

5. <span data-ttu-id="840c5-135">In the results panel, select **Allocadia**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="840c5-135">In the results panel, select **Allocadia**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/allocadia-tutorial/tutorial_allocadia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="840c5-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="840c5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="840c5-138">In this section, you configure and test Azure AD single sign-on with Allocadia based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="840c5-138">In this section, you configure and test Azure AD single sign-on with Allocadia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="840c5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Allocadia is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="840c5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Allocadia is to a user in Azure AD.</span></span> <span data-ttu-id="840c5-140">In other words, a link relationship between an Azure AD user and the related user in Allocadia needs to be established.</span><span class="sxs-lookup"><span data-stu-id="840c5-140">In other words, a link relationship between an Azure AD user and the related user in Allocadia needs to be established.</span></span>

<span data-ttu-id="840c5-141">In Allocadia, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="840c5-141">In Allocadia, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="840c5-142">To configure and test Azure AD single sign-on with Allocadia, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="840c5-142">To configure and test Azure AD single sign-on with Allocadia, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="840c5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="840c5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="840c5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="840c5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="840c5-145">**[Creating an Allocadia test user](#creating-an-allocadia-test-user)** - to have a counterpart of Britta Simon in Allocadia that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="840c5-145">**[Creating an Allocadia test user](#creating-an-allocadia-test-user)** - to have a counterpart of Britta Simon in Allocadia that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="840c5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="840c5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="840c5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="840c5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="840c5-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="840c5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="840c5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Allocadia application.</span><span class="sxs-lookup"><span data-stu-id="840c5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Allocadia application.</span></span>

<span data-ttu-id="840c5-150">**To configure Azure AD single sign-on with Allocadia, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="840c5-150">**To configure Azure AD single sign-on with Allocadia, perform the following steps:**</span></span>

1. <span data-ttu-id="840c5-151">In the Azure portal, on the **Allocadia** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="840c5-151">In the Azure portal, on the **Allocadia** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="840c5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="840c5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/allocadia-tutorial/tutorial_allocadia_samlbase.png)

3. <span data-ttu-id="840c5-155">On the **Allocadia Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="840c5-155">On the **Allocadia Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/allocadia-tutorial/tutorial_allocadia_url.png)

    <span data-ttu-id="840c5-157">a.</span><span class="sxs-lookup"><span data-stu-id="840c5-157">a.</span></span> <span data-ttu-id="840c5-158">In the **Identifier** textbox, type a URL using the following patterns:</span><span class="sxs-lookup"><span data-stu-id="840c5-158">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
       
     <span data-ttu-id="840c5-159">For test environment -  `https://na2standby.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="840c5-159">For test environment -  `https://na2standby.allocadia.com`</span></span>
    
     <span data-ttu-id="840c5-160">For production environment - `https://na2.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="840c5-160">For production environment - `https://na2.allocadia.com`</span></span>

    <span data-ttu-id="840c5-161">b.</span><span class="sxs-lookup"><span data-stu-id="840c5-161">b.</span></span> <span data-ttu-id="840c5-162">In the **Reply URL** textbox, type a URL using the following patterns:</span><span class="sxs-lookup"><span data-stu-id="840c5-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    
     <span data-ttu-id="840c5-163">For test environment - `https://na2standby.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="840c5-163">For test environment - `https://na2standby.allocadia.com/allocadia/saml/SSO`</span></span>
    
     <span data-ttu-id="840c5-164">For production environment - `https://na2.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="840c5-164">For production environment - `https://na2.allocadia.com/allocadia/saml/SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="840c5-165">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="840c5-165">These values are not real.</span></span> <span data-ttu-id="840c5-166">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="840c5-166">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="840c5-167">Contact [Allocadia support team](mailTo:support@allocadia.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="840c5-167">Contact [Allocadia support team](mailTo:support@allocadia.com) to get these values.</span></span>

4. <span data-ttu-id="840c5-168">Allocadia application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="840c5-168">Allocadia application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="840c5-169">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="840c5-169">Configure the following claims for this application.</span></span> <span data-ttu-id="840c5-170">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="840c5-170">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="840c5-171">The following screenshot shows an example for this configuration.</span><span class="sxs-lookup"><span data-stu-id="840c5-171">The following screenshot shows an example for this configuration.</span></span> 

    ![Configure Single Sign-On](./media/allocadia-tutorial/tutorial_allocadia_attributes.png)
    
5. <span data-ttu-id="840c5-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="840c5-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="840c5-174">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="840c5-174">Attribute Name</span></span> | <span data-ttu-id="840c5-175">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="840c5-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="840c5-176">firstname</span><span class="sxs-lookup"><span data-stu-id="840c5-176">firstname</span></span> | <span data-ttu-id="840c5-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="840c5-177">user.givenname</span></span> |
    | <span data-ttu-id="840c5-178">lastname</span><span class="sxs-lookup"><span data-stu-id="840c5-178">lastname</span></span> | <span data-ttu-id="840c5-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="840c5-179">user.surname</span></span> |
    | <span data-ttu-id="840c5-180">email</span><span class="sxs-lookup"><span data-stu-id="840c5-180">email</span></span> | <span data-ttu-id="840c5-181">user.mail</span><span class="sxs-lookup"><span data-stu-id="840c5-181">user.mail</span></span> |
    
    <span data-ttu-id="840c5-182">a.</span><span class="sxs-lookup"><span data-stu-id="840c5-182">a.</span></span> <span data-ttu-id="840c5-183">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="840c5-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/allocadia-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="840c5-185">b.</span><span class="sxs-lookup"><span data-stu-id="840c5-185">b.</span></span> <span data-ttu-id="840c5-186">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="840c5-186">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Configure Single Sign-On](./media/allocadia-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="840c5-188">c.</span><span class="sxs-lookup"><span data-stu-id="840c5-188">c.</span></span> <span data-ttu-id="840c5-189">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="840c5-189">From the **Value** list, type the attribute value shown for that row.</span></span>
 
    <span data-ttu-id="840c5-190">d.</span><span class="sxs-lookup"><span data-stu-id="840c5-190">d.</span></span> <span data-ttu-id="840c5-191">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="840c5-191">Click **Ok**.</span></span>



6. <span data-ttu-id="840c5-192">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="840c5-192">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/allocadia-tutorial/tutorial_allocadia_certificate.png) 


7. <span data-ttu-id="840c5-194">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="840c5-194">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/allocadia-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="840c5-196">To configure single sign-on on **Allocadia** side, you need to send the downloaded **Metadata XML** to [Allocadia support team](mailTo:support@allocadia.com).</span><span class="sxs-lookup"><span data-stu-id="840c5-196">To configure single sign-on on **Allocadia** side, you need to send the downloaded **Metadata XML** to [Allocadia support team](mailTo:support@allocadia.com).</span></span> <span data-ttu-id="840c5-197">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="840c5-197">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="840c5-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="840c5-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="840c5-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="840c5-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="840c5-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="840c5-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="840c5-201">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="840c5-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="840c5-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="840c5-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="840c5-204">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="840c5-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="840c5-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="840c5-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/allocadia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="840c5-207">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="840c5-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/allocadia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="840c5-209">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="840c5-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/allocadia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="840c5-211">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="840c5-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/allocadia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="840c5-213">a.</span><span class="sxs-lookup"><span data-stu-id="840c5-213">a.</span></span> <span data-ttu-id="840c5-214">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="840c5-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="840c5-215">b.</span><span class="sxs-lookup"><span data-stu-id="840c5-215">b.</span></span> <span data-ttu-id="840c5-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="840c5-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="840c5-217">c.</span><span class="sxs-lookup"><span data-stu-id="840c5-217">c.</span></span> <span data-ttu-id="840c5-218">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="840c5-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="840c5-219">d.</span><span class="sxs-lookup"><span data-stu-id="840c5-219">d.</span></span> <span data-ttu-id="840c5-220">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="840c5-220">Click **Create**.</span></span>
 
### <a name="creating-an-allocadia-test-user"></a><span data-ttu-id="840c5-221">Creating an Allocadia test user</span><span class="sxs-lookup"><span data-stu-id="840c5-221">Creating an Allocadia test user</span></span>

<span data-ttu-id="840c5-222">Application supports Just in time user provisioning.</span><span class="sxs-lookup"><span data-stu-id="840c5-222">Application supports Just in time user provisioning.</span></span> <span data-ttu-id="840c5-223">After authentication users are created in the application automatically.</span><span class="sxs-lookup"><span data-stu-id="840c5-223">After authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="840c5-224">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="840c5-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="840c5-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Allocadia.</span><span class="sxs-lookup"><span data-stu-id="840c5-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Allocadia.</span></span>

![Assign User][200] 

<span data-ttu-id="840c5-227">**To assign Britta Simon to Allocadia, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="840c5-227">**To assign Britta Simon to Allocadia, perform the following steps:**</span></span>

1. <span data-ttu-id="840c5-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="840c5-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="840c5-230">In the applications list, select **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="840c5-230">In the applications list, select **Allocadia**.</span></span>

    ![Configure Single Sign-On](./media/allocadia-tutorial/tutorial_allocadia_app.png) 

3. <span data-ttu-id="840c5-232">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="840c5-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="840c5-234">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="840c5-234">Click **Add** button.</span></span> <span data-ttu-id="840c5-235">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="840c5-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="840c5-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="840c5-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="840c5-238">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="840c5-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="840c5-239">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="840c5-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="840c5-240">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="840c5-240">Testing single sign-on</span></span>

<span data-ttu-id="840c5-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="840c5-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="840c5-242">When you click the Allocadia tile in the Access Panel, you should get automatically signed-on to your Allocadia application.</span><span class="sxs-lookup"><span data-stu-id="840c5-242">When you click the Allocadia tile in the Access Panel, you should get automatically signed-on to your Allocadia application.</span></span>
<span data-ttu-id="840c5-243">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="840c5-243">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="840c5-244">Additional resources</span><span class="sxs-lookup"><span data-stu-id="840c5-244">Additional resources</span></span>

* [<span data-ttu-id="840c5-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="840c5-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="840c5-246">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="840c5-246">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/allocadia-tutorial/tutorial_general_01.png
[2]: ./media/allocadia-tutorial/tutorial_general_02.png
[3]: ./media/allocadia-tutorial/tutorial_general_03.png
[4]: ./media/allocadia-tutorial/tutorial_general_04.png

[100]: ./media/allocadia-tutorial/tutorial_general_100.png

[200]: ./media/allocadia-tutorial/tutorial_general_200.png
[201]: ./media/allocadia-tutorial/tutorial_general_201.png
[202]: ./media/allocadia-tutorial/tutorial_general_202.png
[203]: ./media/allocadia-tutorial/tutorial_general_203.png

