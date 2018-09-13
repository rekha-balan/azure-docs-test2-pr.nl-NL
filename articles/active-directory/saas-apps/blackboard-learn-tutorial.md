---
title: 'Tutorial: Azure Active Directory integration with Blackboard Learn | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Blackboard Learn.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jeedes
ms.openlocfilehash: 9b7e7a84059f8393e8f900733602e32ca3ad833b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869487"
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="46906-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="46906-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>

<span data-ttu-id="46906-104">In this tutorial, you learn how to integrate Blackboard Learn with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="46906-104">In this tutorial, you learn how to integrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="46906-105">Integrating Blackboard Learn with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="46906-105">Integrating Blackboard Learn with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="46906-106">You can control in Azure AD who has access to Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="46906-106">You can control in Azure AD who has access to Blackboard Learn</span></span>
- <span data-ttu-id="46906-107">You can enable your users to automatically get signed-on to Blackboard Learn (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="46906-107">You can enable your users to automatically get signed-on to Blackboard Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="46906-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="46906-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="46906-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="46906-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46906-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="46906-110">Prerequisites</span></span>

<span data-ttu-id="46906-111">To configure Azure AD integration with Blackboard Learn, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="46906-111">To configure Azure AD integration with Blackboard Learn, you need the following items:</span></span>

- <span data-ttu-id="46906-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="46906-112">An Azure AD subscription</span></span>
- <span data-ttu-id="46906-113">A Blackboard Learn single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="46906-113">A Blackboard Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="46906-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="46906-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="46906-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="46906-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="46906-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="46906-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="46906-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="46906-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="46906-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="46906-118">Scenario description</span></span>
<span data-ttu-id="46906-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="46906-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="46906-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="46906-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="46906-121">Adding Blackboard Learn from the gallery</span><span class="sxs-lookup"><span data-stu-id="46906-121">Adding Blackboard Learn from the gallery</span></span>
1. <span data-ttu-id="46906-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="46906-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn-from-the-gallery"></a><span data-ttu-id="46906-123">Adding Blackboard Learn from the gallery</span><span class="sxs-lookup"><span data-stu-id="46906-123">Adding Blackboard Learn from the gallery</span></span>
<span data-ttu-id="46906-124">To configure the integration of Blackboard Learn into Azure AD, you need to add Blackboard Learn from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="46906-124">To configure the integration of Blackboard Learn into Azure AD, you need to add Blackboard Learn from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="46906-125">**To add Blackboard Learn from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="46906-125">**To add Blackboard Learn from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="46906-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="46906-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="46906-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="46906-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="46906-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="46906-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="46906-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="46906-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="46906-133">In the search box, type **Blackboard Learn**.</span><span class="sxs-lookup"><span data-stu-id="46906-133">In the search box, type **Blackboard Learn**.</span></span>

    ![Creating an Azure AD test user](./media/blackboard-learn-tutorial/tutorial_blackboardlearn_search.png)

1. <span data-ttu-id="46906-135">In the results panel, select **Blackboard Learn**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="46906-135">In the results panel, select **Blackboard Learn**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/blackboard-learn-tutorial/tutorial_blackboardlearn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="46906-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="46906-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="46906-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="46906-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="46906-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="46906-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn is to a user in Azure AD.</span></span> <span data-ttu-id="46906-140">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn needs to be established.</span><span class="sxs-lookup"><span data-stu-id="46906-140">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn needs to be established.</span></span>

<span data-ttu-id="46906-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="46906-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="46906-142">To configure and test Azure AD single sign-on with Blackboard Learn, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="46906-142">To configure and test Azure AD single sign-on with Blackboard Learn, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="46906-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="46906-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="46906-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="46906-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="46906-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="46906-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="46906-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="46906-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="46906-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="46906-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="46906-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="46906-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="46906-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Blackboard Learn application.</span><span class="sxs-lookup"><span data-stu-id="46906-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="46906-150">**To configure Azure AD single sign-on with Blackboard Learn, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="46906-150">**To configure Azure AD single sign-on with Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="46906-151">In the Azure portal, on the **Blackboard Learn** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="46906-151">In the Azure portal, on the **Blackboard Learn** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="46906-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="46906-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/blackboard-learn-tutorial/tutorial_blackboardlearn_samlbase.png)

1. <span data-ttu-id="46906-155">On the **Blackboard Learn Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="46906-155">On the **Blackboard Learn Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/blackboard-learn-tutorial/tutorial_blackboardlearn_url.png)

    <span data-ttu-id="46906-157">a.</span><span class="sxs-lookup"><span data-stu-id="46906-157">a.</span></span> <span data-ttu-id="46906-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/`</span><span class="sxs-lookup"><span data-stu-id="46906-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/`</span></span>

    <span data-ttu-id="46906-159">b.</span><span class="sxs-lookup"><span data-stu-id="46906-159">b.</span></span> <span data-ttu-id="46906-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span><span class="sxs-lookup"><span data-stu-id="46906-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="46906-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="46906-161">These values are not real.</span></span> <span data-ttu-id="46906-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="46906-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="46906-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) to get these values.</span><span class="sxs-lookup"><span data-stu-id="46906-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) to get these values.</span></span> 

1. <span data-ttu-id="46906-164">Blackboard Learn application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="46906-164">Blackboard Learn application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="46906-165">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="46906-165">Configure the following claims for this application.</span></span> <span data-ttu-id="46906-166">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="46906-166">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="46906-167">The following screenshot shows an example about it.</span><span class="sxs-lookup"><span data-stu-id="46906-167">The following screenshot shows an example about it.</span></span>

    ![Configure Single Sign-On](./media/blackboard-learn-tutorial/tutorial_attribute.png)

1. <span data-ttu-id="46906-169">In the **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in the image and perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="46906-169">In the **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in the image and perform the following steps.</span></span> <span data-ttu-id="46906-170">We have mapped the Userprincipalname as the unique user attribute here but you can map it to the appropriate value, which uniquely distinguishes the user in the organization and that maps to Blackboard Learn username field.</span><span class="sxs-lookup"><span data-stu-id="46906-170">We have mapped the Userprincipalname as the unique user attribute here but you can map it to the appropriate value, which uniquely distinguishes the user in the organization and that maps to Blackboard Learn username field.</span></span>
           
    | <span data-ttu-id="46906-171">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="46906-171">Attribute Name</span></span> | <span data-ttu-id="46906-172">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="46906-172">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="46906-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="46906-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="46906-174">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="46906-174">user.userprincipalname</span></span> |

    <span data-ttu-id="46906-175">a.</span><span class="sxs-lookup"><span data-stu-id="46906-175">a.</span></span> <span data-ttu-id="46906-176">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="46906-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/blackboard-learn-tutorial/tutorial_attribute_04.png)
    
    ![Configure Single Sign-On](./media/blackboard-learn-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="46906-179">b.</span><span class="sxs-lookup"><span data-stu-id="46906-179">b.</span></span> <span data-ttu-id="46906-180">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="46906-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="46906-181">c.</span><span class="sxs-lookup"><span data-stu-id="46906-181">c.</span></span> <span data-ttu-id="46906-182">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="46906-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="46906-183">d.</span><span class="sxs-lookup"><span data-stu-id="46906-183">d.</span></span> <span data-ttu-id="46906-184">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="46906-184">Click **Ok**.</span></span>

1. <span data-ttu-id="46906-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="46906-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](./media/blackboard-learn-tutorial/tutorial_blackboardlearn_certificate.png)

1. <span data-ttu-id="46906-187">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="46906-187">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/blackboard-learn-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="46906-189">On the **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="46906-189">On the **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** to open **Configure sign-on** window.</span></span> <span data-ttu-id="46906-190">Copy the **SAML Entity ID** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="46906-190">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/blackboard-learn-tutorial/tutorial_blackboardlearn_configure.png) 

1. <span data-ttu-id="46906-192">To configure single sign-on on **Blackboard Learn** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID** to [Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span><span class="sxs-lookup"><span data-stu-id="46906-192">To configure single sign-on on **Blackboard Learn** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID** to [Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="46906-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="46906-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="46906-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="46906-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="46906-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="46906-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="46906-196">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="46906-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="46906-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="46906-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="46906-199">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="46906-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="46906-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="46906-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/blackboard-learn-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="46906-202">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="46906-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/blackboard-learn-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="46906-204">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="46906-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/blackboard-learn-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="46906-206">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="46906-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/blackboard-learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="46906-208">a.</span><span class="sxs-lookup"><span data-stu-id="46906-208">a.</span></span> <span data-ttu-id="46906-209">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="46906-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="46906-210">b.</span><span class="sxs-lookup"><span data-stu-id="46906-210">b.</span></span> <span data-ttu-id="46906-211">In the **User name** textbox, type the **email address** of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="46906-211">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="46906-212">c.</span><span class="sxs-lookup"><span data-stu-id="46906-212">c.</span></span> <span data-ttu-id="46906-213">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="46906-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="46906-214">d.</span><span class="sxs-lookup"><span data-stu-id="46906-214">d.</span></span> <span data-ttu-id="46906-215">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="46906-215">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn-test-user"></a><span data-ttu-id="46906-216">Creating a Blackboard Learn test user</span><span class="sxs-lookup"><span data-stu-id="46906-216">Creating a Blackboard Learn test user</span></span>
<span data-ttu-id="46906-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="46906-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="46906-218">Blackboard Learn application support just in time user provisioning.</span><span class="sxs-lookup"><span data-stu-id="46906-218">Blackboard Learn application support just in time user provisioning.</span></span> <span data-ttu-id="46906-219">Make sure that you have configured the claims as described in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span><span class="sxs-lookup"><span data-stu-id="46906-219">Make sure that you have configured the claims as described in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="46906-220">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="46906-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="46906-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="46906-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Blackboard Learn.</span></span>

![Assign User][200] 

<span data-ttu-id="46906-223">**To assign Britta Simon to Blackboard Learn, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="46906-223">**To assign Britta Simon to Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="46906-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="46906-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="46906-226">In the applications list, select **Blackboard Learn**.</span><span class="sxs-lookup"><span data-stu-id="46906-226">In the applications list, select **Blackboard Learn**.</span></span>

    ![Configure Single Sign-On](./media/blackboard-learn-tutorial/tutorial_blackboardlearn_app.png) 

1. <span data-ttu-id="46906-228">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="46906-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="46906-230">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="46906-230">Click **Add** button.</span></span> <span data-ttu-id="46906-231">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="46906-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="46906-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="46906-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="46906-234">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="46906-234">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="46906-235">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="46906-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="46906-236">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="46906-236">Testing single sign-on</span></span>

<span data-ttu-id="46906-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="46906-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="46906-238">When you click the Blackboard Learn tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn application.</span><span class="sxs-lookup"><span data-stu-id="46906-238">When you click the Blackboard Learn tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn application.</span></span> <span data-ttu-id="46906-239">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="46906-239">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="46906-240">Additional resources</span><span class="sxs-lookup"><span data-stu-id="46906-240">Additional resources</span></span>

* [<span data-ttu-id="46906-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="46906-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="46906-242">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="46906-242">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/blackboard-learn-tutorial/tutorial_general_01.png
[2]: ./media/blackboard-learn-tutorial/tutorial_general_02.png
[3]: ./media/blackboard-learn-tutorial/tutorial_general_03.png
[4]: ./media/blackboard-learn-tutorial/tutorial_general_04.png

[100]: ./media/blackboard-learn-tutorial/tutorial_general_100.png

[200]: ./media/blackboard-learn-tutorial/tutorial_general_200.png
[201]: ./media/blackboard-learn-tutorial/tutorial_general_201.png
[202]: ./media/blackboard-learn-tutorial/tutorial_general_202.png
[203]: ./media/blackboard-learn-tutorial/tutorial_general_203.png

