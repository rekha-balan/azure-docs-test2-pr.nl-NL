---
title: 'Tutorial: Azure Active Directory integration with Learningpool Act | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Learningpool Act.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 51e8695f-31e1-4d09-8eb3-13241999d99f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 6f3fab8398c8f32d4fa89f11c60fec57db516fcb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865428"
---
# <a name="tutorial-azure-active-directory-integration-with-learningpool-act"></a><span data-ttu-id="472df-103">Tutorial: Azure Active Directory integration with Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="472df-103">Tutorial: Azure Active Directory integration with Learningpool Act</span></span>

<span data-ttu-id="472df-104">In this tutorial, you learn how to integrate Learningpool Act with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="472df-104">In this tutorial, you learn how to integrate Learningpool Act with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="472df-105">Integrating Learningpool Act with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="472df-105">Integrating Learningpool Act with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="472df-106">You can control in Azure AD who has access to Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="472df-106">You can control in Azure AD who has access to Learningpool Act</span></span>
- <span data-ttu-id="472df-107">You can enable your users to automatically get signed-on to Learningpool Act (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="472df-107">You can enable your users to automatically get signed-on to Learningpool Act (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="472df-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="472df-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="472df-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="472df-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="472df-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="472df-110">Prerequisites</span></span>

<span data-ttu-id="472df-111">To configure Azure AD integration with Learningpool Act, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="472df-111">To configure Azure AD integration with Learningpool Act, you need the following items:</span></span>

- <span data-ttu-id="472df-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="472df-112">An Azure AD subscription</span></span>
- <span data-ttu-id="472df-113">A Learningpool Act single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="472df-113">A Learningpool Act single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="472df-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="472df-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="472df-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="472df-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="472df-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="472df-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="472df-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="472df-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="472df-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="472df-118">Scenario description</span></span>
<span data-ttu-id="472df-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="472df-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="472df-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="472df-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="472df-121">Adding Learningpool Act from the gallery</span><span class="sxs-lookup"><span data-stu-id="472df-121">Adding Learningpool Act from the gallery</span></span>
1. <span data-ttu-id="472df-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="472df-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learningpool-act-from-the-gallery"></a><span data-ttu-id="472df-123">Adding Learningpool Act from the gallery</span><span class="sxs-lookup"><span data-stu-id="472df-123">Adding Learningpool Act from the gallery</span></span>
<span data-ttu-id="472df-124">To configure the integration of Learningpool Act into Azure AD, you need to add Learningpool Act from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="472df-124">To configure the integration of Learningpool Act into Azure AD, you need to add Learningpool Act from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="472df-125">**To add Learningpool Act from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="472df-125">**To add Learningpool Act from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="472df-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="472df-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="472df-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="472df-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="472df-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="472df-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="472df-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="472df-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="472df-133">In the search box, type **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="472df-133">In the search box, type **Learningpool Act**.</span></span>

    ![Creating an Azure AD test user](./media/learningpool-tutorial/tutorial_Learningpoolact_search.png)

1. <span data-ttu-id="472df-135">In the results panel, select **Learningpool Act**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="472df-135">In the results panel, select **Learningpool Act**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/learningpool-tutorial/tutorial_Learningpoolact_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="472df-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="472df-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="472df-138">In this section, you configure and test Azure AD single sign-on with Learningpool Act based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="472df-138">In this section, you configure and test Azure AD single sign-on with Learningpool Act based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="472df-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learningpool Act is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="472df-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learningpool Act is to a user in Azure AD.</span></span> <span data-ttu-id="472df-140">In other words, a link relationship between an Azure AD user and the related user in Learningpool Act needs to be established.</span><span class="sxs-lookup"><span data-stu-id="472df-140">In other words, a link relationship between an Azure AD user and the related user in Learningpool Act needs to be established.</span></span>

<span data-ttu-id="472df-141">In Learningpool Act, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="472df-141">In Learningpool Act, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="472df-142">To configure and test Azure AD single sign-on with Learningpool Act, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="472df-142">To configure and test Azure AD single sign-on with Learningpool Act, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="472df-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="472df-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="472df-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="472df-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="472df-145">**[Creating a Learningpool Act test user](#creating-a-learningpool-act-test-user)** - to have a counterpart of Britta Simon in Learningpool Act that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="472df-145">**[Creating a Learningpool Act test user](#creating-a-learningpool-act-test-user)** - to have a counterpart of Britta Simon in Learningpool Act that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="472df-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="472df-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="472df-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="472df-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="472df-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="472df-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="472df-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learningpool Act application.</span><span class="sxs-lookup"><span data-stu-id="472df-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learningpool Act application.</span></span>

<span data-ttu-id="472df-150">**To configure Azure AD single sign-on with Learningpool Act, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="472df-150">**To configure Azure AD single sign-on with Learningpool Act, perform the following steps:**</span></span>

1. <span data-ttu-id="472df-151">In the Azure portal, on the **Learningpool Act** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="472df-151">In the Azure portal, on the **Learningpool Act** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="472df-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="472df-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/learningpool-tutorial/tutorial_Learningpoolact_samlbase.png)

1. <span data-ttu-id="472df-155">On the **Learningpool Act Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="472df-155">On the **Learningpool Act Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/learningpool-tutorial/tutorial_Learningpoolact_url.png)

    <span data-ttu-id="472df-157">a.</span><span class="sxs-lookup"><span data-stu-id="472df-157">a.</span></span> <span data-ttu-id="472df-158">In the **Sign-on URL** textbox, type the URL: `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span><span class="sxs-lookup"><span data-stu-id="472df-158">In the **Sign-on URL** textbox, type the URL: `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span></span>

    <span data-ttu-id="472df-159">b.</span><span class="sxs-lookup"><span data-stu-id="472df-159">b.</span></span> <span data-ttu-id="472df-160">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="472df-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.Learningpool.com/shibboleth` |
    | `https://<subdomain>.preview.Learningpool.com/shibboleth` |

    > [!NOTE] 
    > <span data-ttu-id="472df-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="472df-161">These values are not real.</span></span> <span data-ttu-id="472df-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="472df-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="472df-163">Contact [Learningpool Act Client support team](https://www.Learningpool.com/support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="472df-163">Contact [Learningpool Act Client support team](https://www.Learningpool.com/support) to get these values.</span></span> 
 
1. <span data-ttu-id="472df-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="472df-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/learningpool-tutorial/tutorial_Learningpoolact_certificate.png) 

1. <span data-ttu-id="472df-166">Learningpool Act application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="472df-166">Learningpool Act application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="472df-167">Please configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="472df-167">Please configure the following claims for this application.</span></span> <span data-ttu-id="472df-168">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span><span class="sxs-lookup"><span data-stu-id="472df-168">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="472df-169">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="472df-169">The following screenshot shows an example for this.</span></span> 

    ![Configure Single Sign-On](./media/learningpool-tutorial/tutorial_Learningpoolact_attribute.png) 

1. <span data-ttu-id="472df-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="472df-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="472df-172">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="472df-172">Attribute Name</span></span> | <span data-ttu-id="472df-173">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="472df-173">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="472df-174">urn:oid:1.2.840.113556.1.4.221</span><span class="sxs-lookup"><span data-stu-id="472df-174">urn:oid:1.2.840.113556.1.4.221</span></span> | <span data-ttu-id="472df-175">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="472df-175">user.userprincipalname</span></span> |
    | <span data-ttu-id="472df-176">urn:oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="472df-176">urn:oid:2.5.4.42</span></span> | <span data-ttu-id="472df-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="472df-177">user.givenname</span></span> |
    | <span data-ttu-id="472df-178">urn:oid:0.9.2342.19200300.100.1.3</span><span class="sxs-lookup"><span data-stu-id="472df-178">urn:oid:0.9.2342.19200300.100.1.3</span></span> | <span data-ttu-id="472df-179">user.mail</span><span class="sxs-lookup"><span data-stu-id="472df-179">user.mail</span></span> |    
    | <span data-ttu-id="472df-180">urn:oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="472df-180">urn:oid:2.5.4.4</span></span> | <span data-ttu-id="472df-181">user.surname</span><span class="sxs-lookup"><span data-stu-id="472df-181">user.surname</span></span> |
    
    <span data-ttu-id="472df-182">a.</span><span class="sxs-lookup"><span data-stu-id="472df-182">a.</span></span> <span data-ttu-id="472df-183">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="472df-183">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/learningpool-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/learningpool-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="472df-186">b.</span><span class="sxs-lookup"><span data-stu-id="472df-186">b.</span></span> <span data-ttu-id="472df-187">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="472df-187">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="472df-188">c.</span><span class="sxs-lookup"><span data-stu-id="472df-188">c.</span></span> <span data-ttu-id="472df-189">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="472df-189">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="472df-190">d.</span><span class="sxs-lookup"><span data-stu-id="472df-190">d.</span></span> <span data-ttu-id="472df-191">Leave the **Namespace** blank.</span><span class="sxs-lookup"><span data-stu-id="472df-191">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="472df-192">e.</span><span class="sxs-lookup"><span data-stu-id="472df-192">e.</span></span> <span data-ttu-id="472df-193">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="472df-193">Click **Ok**.</span></span>

1. <span data-ttu-id="472df-194">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="472df-194">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/learningpool-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="472df-196">To configure single sign-on on **Learningpool Act** side, you need to send the downloaded **Metadata XML** to [Learningpool Act support team](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="472df-196">To configure single sign-on on **Learningpool Act** side, you need to send the downloaded **Metadata XML** to [Learningpool Act support team](https://www.Learningpool.com/support).</span></span> <span data-ttu-id="472df-197">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="472df-197">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="472df-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="472df-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="472df-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="472df-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="472df-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="472df-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="472df-201">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="472df-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="472df-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="472df-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="472df-204">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="472df-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="472df-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="472df-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/learningpool-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="472df-207">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="472df-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/learningpool-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="472df-209">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="472df-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/learningpool-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="472df-211">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="472df-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/learningpool-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="472df-213">a.</span><span class="sxs-lookup"><span data-stu-id="472df-213">a.</span></span> <span data-ttu-id="472df-214">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="472df-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="472df-215">b.</span><span class="sxs-lookup"><span data-stu-id="472df-215">b.</span></span> <span data-ttu-id="472df-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="472df-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="472df-217">c.</span><span class="sxs-lookup"><span data-stu-id="472df-217">c.</span></span> <span data-ttu-id="472df-218">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="472df-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="472df-219">d.</span><span class="sxs-lookup"><span data-stu-id="472df-219">d.</span></span> <span data-ttu-id="472df-220">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="472df-220">Click **Create**.</span></span>
 
### <a name="creating-a-learningpool-act-test-user"></a><span data-ttu-id="472df-221">Creating a Learningpool Act test user</span><span class="sxs-lookup"><span data-stu-id="472df-221">Creating a Learningpool Act test user</span></span>

<span data-ttu-id="472df-222">To enable Azure AD users to log in to Learningpool Act, they must be provisioned into Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="472df-222">To enable Azure AD users to log in to Learningpool Act, they must be provisioned into Learningpool Act.</span></span>

<span data-ttu-id="472df-223">There is no action item for you to configure user provisioning to Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="472df-223">There is no action item for you to configure user provisioning to Learningpool Act.</span></span>  
<span data-ttu-id="472df-224">Users need to be created by your [Learningpool Act support team](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="472df-224">Users need to be created by your [Learningpool Act support team](https://www.Learningpool.com/support).</span></span>

>[!NOTE]
><span data-ttu-id="472df-225">You can use any other Learningpool Act user account creation tools or APIs provided by Learningpool Act to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="472df-225">You can use any other Learningpool Act user account creation tools or APIs provided by Learningpool Act to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="472df-226">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="472df-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="472df-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="472df-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learningpool Act.</span></span>

![Assign User][200] 

<span data-ttu-id="472df-229">**To assign Britta Simon to Learningpool Act, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="472df-229">**To assign Britta Simon to Learningpool Act, perform the following steps:**</span></span>

1. <span data-ttu-id="472df-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="472df-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="472df-232">In the applications list, select **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="472df-232">In the applications list, select **Learningpool Act**.</span></span>

    ![Configure Single Sign-On](./media/learningpool-tutorial/tutorial_Learningpoolact_app.png) 

1. <span data-ttu-id="472df-234">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="472df-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="472df-236">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="472df-236">Click **Add** button.</span></span> <span data-ttu-id="472df-237">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="472df-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="472df-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="472df-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="472df-240">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="472df-240">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="472df-241">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="472df-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="472df-242">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="472df-242">Testing single sign-on</span></span>

<span data-ttu-id="472df-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="472df-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="472df-244">When you click the Learningpool Act tile in the Access Panel, you should get automatically signed-on to your Learningpool Act application.</span><span class="sxs-lookup"><span data-stu-id="472df-244">When you click the Learningpool Act tile in the Access Panel, you should get automatically signed-on to your Learningpool Act application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="472df-245">Additional resources</span><span class="sxs-lookup"><span data-stu-id="472df-245">Additional resources</span></span>

* [<span data-ttu-id="472df-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="472df-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="472df-247">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="472df-247">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/Learningpool-tutorial/tutorial_general_01.png
[2]: ./media/Learningpool-tutorial/tutorial_general_02.png
[3]: ./media/Learningpool-tutorial/tutorial_general_03.png
[4]: ./media/Learningpool-tutorial/tutorial_general_04.png

[100]: ./media/Learningpool-tutorial/tutorial_general_100.png

[200]: ./media/Learningpool-tutorial/tutorial_general_200.png
[201]: ./media/Learningpool-tutorial/tutorial_general_201.png
[202]: ./media/Learningpool-tutorial/tutorial_general_202.png
[203]: ./media/Learningpool-tutorial/tutorial_general_203.png

