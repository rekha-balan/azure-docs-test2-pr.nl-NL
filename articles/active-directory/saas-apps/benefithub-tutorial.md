---
title: 'Tutorial: Azure Active Directory integration with BenefitHub | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and BenefitHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 4069fe32-a452-463f-973e-7aa0baa4c2fa
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 0a838e003fa4fde6c4a1d458cc6dadf6c6672842
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867966"
---
# <a name="tutorial-azure-active-directory-integration-with-benefithub"></a><span data-ttu-id="bb922-103">Tutorial: Azure Active Directory integration with BenefitHub</span><span class="sxs-lookup"><span data-stu-id="bb922-103">Tutorial: Azure Active Directory integration with BenefitHub</span></span>

<span data-ttu-id="bb922-104">In this tutorial, you learn how to integrate BenefitHub with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bb922-104">In this tutorial, you learn how to integrate BenefitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bb922-105">Integrating BenefitHub with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="bb922-105">Integrating BenefitHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bb922-106">You can control in Azure AD who has access to BenefitHub</span><span class="sxs-lookup"><span data-stu-id="bb922-106">You can control in Azure AD who has access to BenefitHub</span></span>
- <span data-ttu-id="bb922-107">You can enable your users to automatically get signed-on to BenefitHub (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="bb922-107">You can enable your users to automatically get signed-on to BenefitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bb922-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="bb922-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bb922-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="bb922-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb922-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bb922-110">Prerequisites</span></span>

<span data-ttu-id="bb922-111">To configure Azure AD integration with BenefitHub, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="bb922-111">To configure Azure AD integration with BenefitHub, you need the following items:</span></span>

- <span data-ttu-id="bb922-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="bb922-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bb922-113">A BenefitHub single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="bb922-113">A BenefitHub single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bb922-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="bb922-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bb922-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="bb922-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bb922-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="bb922-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bb922-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bb922-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bb922-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="bb922-118">Scenario description</span></span>
<span data-ttu-id="bb922-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="bb922-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bb922-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="bb922-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bb922-121">Adding BenefitHub from the gallery</span><span class="sxs-lookup"><span data-stu-id="bb922-121">Adding BenefitHub from the gallery</span></span>
1. <span data-ttu-id="bb922-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bb922-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benefithub-from-the-gallery"></a><span data-ttu-id="bb922-123">Adding BenefitHub from the gallery</span><span class="sxs-lookup"><span data-stu-id="bb922-123">Adding BenefitHub from the gallery</span></span>
<span data-ttu-id="bb922-124">To configure the integration of BenefitHub into Azure AD, you need to add BenefitHub from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="bb922-124">To configure the integration of BenefitHub into Azure AD, you need to add BenefitHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bb922-125">**To add BenefitHub from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bb922-125">**To add BenefitHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bb922-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="bb922-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="bb922-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="bb922-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bb922-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="bb922-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="bb922-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="bb922-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="bb922-133">In the search box, type **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="bb922-133">In the search box, type **BenefitHub**.</span></span>

    ![Creating an Azure AD test user](./media/benefithub-tutorial/tutorial_benefithub_search.png)

1. <span data-ttu-id="bb922-135">In the results panel, select **BenefitHub**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="bb922-135">In the results panel, select **BenefitHub**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/benefithub-tutorial/tutorial_benefithub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bb922-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bb922-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bb922-138">In this section, you configure and test Azure AD single sign-on with BenefitHub based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="bb922-138">In this section, you configure and test Azure AD single sign-on with BenefitHub based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bb922-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BenefitHub is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb922-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BenefitHub is to a user in Azure AD.</span></span> <span data-ttu-id="bb922-140">In other words, a link relationship between an Azure AD user and the related user in BenefitHub needs to be established.</span><span class="sxs-lookup"><span data-stu-id="bb922-140">In other words, a link relationship between an Azure AD user and the related user in BenefitHub needs to be established.</span></span>

<span data-ttu-id="bb922-141">In BenefitHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="bb922-141">In BenefitHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bb922-142">To configure and test Azure AD single sign-on with BenefitHub, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="bb922-142">To configure and test Azure AD single sign-on with BenefitHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bb922-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="bb922-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="bb922-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bb922-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="bb922-145">**[Creating a BenefitHub test user](#creating-a-benefithub-test-user)** - to have a counterpart of Britta Simon in BenefitHub that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="bb922-145">**[Creating a BenefitHub test user](#creating-a-benefithub-test-user)** - to have a counterpart of Britta Simon in BenefitHub that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="bb922-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bb922-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="bb922-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="bb922-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bb922-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bb922-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bb922-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BenefitHub application.</span><span class="sxs-lookup"><span data-stu-id="bb922-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BenefitHub application.</span></span>

<span data-ttu-id="bb922-150">**To configure Azure AD single sign-on with BenefitHub, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bb922-150">**To configure Azure AD single sign-on with BenefitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="bb922-151">In the Azure portal, on the **BenefitHub** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="bb922-151">In the Azure portal, on the **BenefitHub** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="bb922-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bb922-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/benefithub-tutorial/tutorial_benefithub_samlbase.png)

1. <span data-ttu-id="bb922-155">On the **BenefitHub Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bb922-155">On the **BenefitHub Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/benefithub-tutorial/tutorial_benefithub_url1.png)
  
    <span data-ttu-id="bb922-157">a.</span><span class="sxs-lookup"><span data-stu-id="bb922-157">a.</span></span> <span data-ttu-id="bb922-158">In the **Identifier** textbox, type: `urn:benefithub:passport`</span><span class="sxs-lookup"><span data-stu-id="bb922-158">In the **Identifier** textbox, type: `urn:benefithub:passport`</span></span>
    
    <span data-ttu-id="bb922-159">b.</span><span class="sxs-lookup"><span data-stu-id="bb922-159">b.</span></span> <span data-ttu-id="bb922-160">In the **Reply URL** textbox, type: `https://passport.benefithub.info/saml/post/ac`</span><span class="sxs-lookup"><span data-stu-id="bb922-160">In the **Reply URL** textbox, type: `https://passport.benefithub.info/saml/post/ac`</span></span>

1. <span data-ttu-id="bb922-161">The BenefitHub application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="bb922-161">The BenefitHub application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="bb922-162">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="bb922-162">Configure the following claims for this application.</span></span> <span data-ttu-id="bb922-163">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="bb922-163">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> 

    ![Configure Single Sign-On](./media/benefithub-tutorial/tutorial_benefithub_attribute.png)

1. <span data-ttu-id="bb922-165">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bb922-165">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
    
    | <span data-ttu-id="bb922-166">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="bb922-166">Attribute Name</span></span> | <span data-ttu-id="bb922-167">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="bb922-167">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="bb922-168">organizationid</span><span class="sxs-lookup"><span data-stu-id="bb922-168">organizationid</span></span> | <span data-ttu-id="bb922-169">< organizationid ></span><span class="sxs-lookup"><span data-stu-id="bb922-169">< organizationid ></span></span> |

    > [!NOTE]
    > <span data-ttu-id="bb922-170">This attribute value is not real.</span><span class="sxs-lookup"><span data-stu-id="bb922-170">This attribute value is not real.</span></span> <span data-ttu-id="bb922-171">Update this value with actual organizationid.</span><span class="sxs-lookup"><span data-stu-id="bb922-171">Update this value with actual organizationid.</span></span> <span data-ttu-id="bb922-172">Contact [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to get the actual organizationid.</span><span class="sxs-lookup"><span data-stu-id="bb922-172">Contact [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to get the actual organizationid.</span></span>
    
    <span data-ttu-id="bb922-173">a.</span><span class="sxs-lookup"><span data-stu-id="bb922-173">a.</span></span> <span data-ttu-id="bb922-174">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="bb922-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/benefithub-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/benefithub-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="bb922-177">b.</span><span class="sxs-lookup"><span data-stu-id="bb922-177">b.</span></span> <span data-ttu-id="bb922-178">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="bb922-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="bb922-179">c.</span><span class="sxs-lookup"><span data-stu-id="bb922-179">c.</span></span> <span data-ttu-id="bb922-180">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="bb922-180">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="bb922-181">d.</span><span class="sxs-lookup"><span data-stu-id="bb922-181">d.</span></span> <span data-ttu-id="bb922-182">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="bb922-182">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bb922-183">Before you can configure the SAML assertion, you need to contact your [BenefitHub support](https://www.benefithub.com/Home/ContactUs) and request the value of the unique identifier attribute for your tenant.</span><span class="sxs-lookup"><span data-stu-id="bb922-183">Before you can configure the SAML assertion, you need to contact your [BenefitHub support](https://www.benefithub.com/Home/ContactUs) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="bb922-184">You need this value to configure the custom claim for your application.</span><span class="sxs-lookup"><span data-stu-id="bb922-184">You need this value to configure the custom claim for your application.</span></span>

1. <span data-ttu-id="bb922-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="bb922-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/benefithub-tutorial/tutorial_benefithub_certificate.png) 

1. <span data-ttu-id="bb922-187">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="bb922-187">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/benefithub-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="bb922-189">To configure single sign-on on **BenefitHub** side, you need to send the downloaded **Metadata XML** to [BenefitHub support team](https://www.benefithub.com/Home/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="bb922-189">To configure single sign-on on **BenefitHub** side, you need to send the downloaded **Metadata XML** to [BenefitHub support team](https://www.benefithub.com/Home/ContactUs).</span></span> <span data-ttu-id="bb922-190">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="bb922-190">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="bb922-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="bb922-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bb922-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="bb922-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bb922-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bb922-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bb922-194">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="bb922-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="bb922-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bb922-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="bb922-197">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bb922-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bb922-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="bb922-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/benefithub-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="bb922-200">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="bb922-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/benefithub-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="bb922-202">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="bb922-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/benefithub-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="bb922-204">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bb922-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/benefithub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bb922-206">a.</span><span class="sxs-lookup"><span data-stu-id="bb922-206">a.</span></span> <span data-ttu-id="bb922-207">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bb922-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bb922-208">b.</span><span class="sxs-lookup"><span data-stu-id="bb922-208">b.</span></span> <span data-ttu-id="bb922-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bb922-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bb922-210">c.</span><span class="sxs-lookup"><span data-stu-id="bb922-210">c.</span></span> <span data-ttu-id="bb922-211">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="bb922-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bb922-212">d.</span><span class="sxs-lookup"><span data-stu-id="bb922-212">d.</span></span> <span data-ttu-id="bb922-213">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="bb922-213">Click **Create**.</span></span>
 
### <a name="creating-a-benefithub-test-user"></a><span data-ttu-id="bb922-214">Creating a BenefitHub test user</span><span class="sxs-lookup"><span data-stu-id="bb922-214">Creating a BenefitHub test user</span></span>

<span data-ttu-id="bb922-215">In this section, you create a user called Britta Simon in BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="bb922-215">In this section, you create a user called Britta Simon in BenefitHub.</span></span> <span data-ttu-id="bb922-216">Work with [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to add the users in the BenefitHub platform.</span><span class="sxs-lookup"><span data-stu-id="bb922-216">Work with [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to add the users in the BenefitHub platform.</span></span> <span data-ttu-id="bb922-217">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bb922-217">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bb922-218">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="bb922-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bb922-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="bb922-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BenefitHub.</span></span>

![Assign User][200] 

<span data-ttu-id="bb922-221">**To assign Britta Simon to BenefitHub, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bb922-221">**To assign Britta Simon to BenefitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="bb922-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="bb922-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="bb922-224">In the applications list, select **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="bb922-224">In the applications list, select **BenefitHub**.</span></span>

    ![Configure Single Sign-On](./media/benefithub-tutorial/tutorial_benefithub_app.png) 

1. <span data-ttu-id="bb922-226">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="bb922-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="bb922-228">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="bb922-228">Click **Add** button.</span></span> <span data-ttu-id="bb922-229">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="bb922-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="bb922-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="bb922-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="bb922-232">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="bb922-232">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="bb922-233">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="bb922-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bb922-234">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="bb922-234">Testing single sign-on</span></span>

<span data-ttu-id="bb922-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="bb922-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bb922-236">When you click the BenefitHub tile in the Access Panel, you should get automatically signed-on to your BenefitHub application.</span><span class="sxs-lookup"><span data-stu-id="bb922-236">When you click the BenefitHub tile in the Access Panel, you should get automatically signed-on to your BenefitHub application.</span></span>
<span data-ttu-id="bb922-237">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bb922-237">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bb922-238">Additional resources</span><span class="sxs-lookup"><span data-stu-id="bb922-238">Additional resources</span></span>

* [<span data-ttu-id="bb922-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bb922-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="bb922-240">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bb922-240">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/benefithub-tutorial/tutorial_general_01.png
[2]: ./media/benefithub-tutorial/tutorial_general_02.png
[3]: ./media/benefithub-tutorial/tutorial_general_03.png
[4]: ./media/benefithub-tutorial/tutorial_general_04.png

[100]: ./media/benefithub-tutorial/tutorial_general_100.png

[200]: ./media/benefithub-tutorial/tutorial_general_200.png
[201]: ./media/benefithub-tutorial/tutorial_general_201.png
[202]: ./media/benefithub-tutorial/tutorial_general_202.png
[203]: ./media/benefithub-tutorial/tutorial_general_203.png
