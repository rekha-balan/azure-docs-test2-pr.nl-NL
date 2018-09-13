---
title: 'Tutorial: Azure Active Directory integration with DigiCert | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and DigiCert.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 646f3129-aa67-4875-9073-1d0b6a3173d9
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/09/2018
ms.author: jeedes
ms.openlocfilehash: f37ac37d80562a402d6891ffaa2a687e04c3a8c0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966673"
---
# <a name="tutorial-azure-active-directory-integration-with-digicert"></a><span data-ttu-id="c60c0-103">Tutorial: Azure Active Directory integration with DigiCert</span><span class="sxs-lookup"><span data-stu-id="c60c0-103">Tutorial: Azure Active Directory integration with DigiCert</span></span>

<span data-ttu-id="c60c0-104">In this tutorial, you learn how to integrate DigiCert with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c60c0-104">In this tutorial, you learn how to integrate DigiCert with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c60c0-105">Integrating DigiCert with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="c60c0-105">Integrating DigiCert with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c60c0-106">You can control in Azure AD who has access to DigiCert</span><span class="sxs-lookup"><span data-stu-id="c60c0-106">You can control in Azure AD who has access to DigiCert</span></span>
- <span data-ttu-id="c60c0-107">You can enable your users to automatically get signed-on to DigiCert (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="c60c0-107">You can enable your users to automatically get signed-on to DigiCert (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c60c0-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c60c0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c60c0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="c60c0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c60c0-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c60c0-110">Prerequisites</span></span>

<span data-ttu-id="c60c0-111">To configure Azure AD integration with DigiCert, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="c60c0-111">To configure Azure AD integration with DigiCert, you need the following items:</span></span>

- <span data-ttu-id="c60c0-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="c60c0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c60c0-113">A DigiCert single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="c60c0-113">A DigiCert single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c60c0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="c60c0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c60c0-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="c60c0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c60c0-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="c60c0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c60c0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c60c0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c60c0-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="c60c0-118">Scenario description</span></span>
<span data-ttu-id="c60c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="c60c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c60c0-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="c60c0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c60c0-121">Adding DigiCert from the gallery</span><span class="sxs-lookup"><span data-stu-id="c60c0-121">Adding DigiCert from the gallery</span></span>
1. <span data-ttu-id="c60c0-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c60c0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-digicert-from-the-gallery"></a><span data-ttu-id="c60c0-123">Adding DigiCert from the gallery</span><span class="sxs-lookup"><span data-stu-id="c60c0-123">Adding DigiCert from the gallery</span></span>
<span data-ttu-id="c60c0-124">To configure the integration of DigiCert into Azure AD, you need to add DigiCert from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="c60c0-124">To configure the integration of DigiCert into Azure AD, you need to add DigiCert from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c60c0-125">**To add DigiCert from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c60c0-125">**To add DigiCert from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c60c0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="c60c0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="c60c0-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="c60c0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c60c0-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c60c0-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="c60c0-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="c60c0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="c60c0-133">In the search box, type **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="c60c0-133">In the search box, type **DigiCert**.</span></span>

    ![Creating an Azure AD test user](./media/digicert-tutorial/tutorial_digicert_search.png)

1. <span data-ttu-id="c60c0-135">In the results panel, select **DigiCert**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="c60c0-135">In the results panel, select **DigiCert**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/digicert-tutorial/tutorial_digicert_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c60c0-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c60c0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c60c0-138">In this section, you configure and test Azure AD single sign-on with DigiCert based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="c60c0-138">In this section, you configure and test Azure AD single sign-on with DigiCert based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c60c0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in DigiCert is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c60c0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in DigiCert is to a user in Azure AD.</span></span> <span data-ttu-id="c60c0-140">In other words, a link relationship between an Azure AD user and the related user in DigiCert needs to be established.</span><span class="sxs-lookup"><span data-stu-id="c60c0-140">In other words, a link relationship between an Azure AD user and the related user in DigiCert needs to be established.</span></span>

<span data-ttu-id="c60c0-141">In DigiCert, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="c60c0-141">In DigiCert, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c60c0-142">To configure and test Azure AD single sign-on with DigiCert, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c60c0-142">To configure and test Azure AD single sign-on with DigiCert, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c60c0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="c60c0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="c60c0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c60c0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="c60c0-145">**[Creating a DigiCert test user](#creating-a-digicert-test-user)** - to have a counterpart of Britta Simon in DigiCert that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="c60c0-145">**[Creating a DigiCert test user](#creating-a-digicert-test-user)** - to have a counterpart of Britta Simon in DigiCert that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="c60c0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c60c0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="c60c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="c60c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c60c0-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c60c0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c60c0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DigiCert application.</span><span class="sxs-lookup"><span data-stu-id="c60c0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DigiCert application.</span></span>

<span data-ttu-id="c60c0-150">**To configure Azure AD single sign-on with DigiCert, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c60c0-150">**To configure Azure AD single sign-on with DigiCert, perform the following steps:**</span></span>

1. <span data-ttu-id="c60c0-151">In the Azure portal, on the **DigiCert** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c60c0-151">In the Azure portal, on the **DigiCert** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="c60c0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c60c0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/digicert-tutorial/tutorial_digicert_samlbase.png)

1. <span data-ttu-id="c60c0-155">On the **DigiCert Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c60c0-155">On the **DigiCert Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/digicert-tutorial/tutorial_digicert_url.png)
    
    <span data-ttu-id="c60c0-157">In the **Identifier** textbox, type the URL: `https://www.digicert.com/sso`</span><span class="sxs-lookup"><span data-stu-id="c60c0-157">In the **Identifier** textbox, type the URL: `https://www.digicert.com/sso`</span></span>

1. <span data-ttu-id="c60c0-158">DigiCert application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="c60c0-158">DigiCert application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="c60c0-159">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="c60c0-159">Configure the following claims for this application.</span></span> <span data-ttu-id="c60c0-160">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="c60c0-160">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="c60c0-161">The following screenshot shows an example for this configuration.</span><span class="sxs-lookup"><span data-stu-id="c60c0-161">The following screenshot shows an example for this configuration.</span></span> 

    ![Configure Single Sign-On](./media/digicert-tutorial/tutorial_digicert_attributes.png)
    
1. <span data-ttu-id="c60c0-163">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c60c0-163">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="c60c0-164">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="c60c0-164">Attribute Name</span></span> | <span data-ttu-id="c60c0-165">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="c60c0-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="c60c0-166">company</span><span class="sxs-lookup"><span data-stu-id="c60c0-166">company</span></span> | <span data-ttu-id="c60c0-167">< companycode ></span><span class="sxs-lookup"><span data-stu-id="c60c0-167">< companycode ></span></span> |
    | <span data-ttu-id="c60c0-168">digicertrole</span><span class="sxs-lookup"><span data-stu-id="c60c0-168">digicertrole</span></span> | <span data-ttu-id="c60c0-169">CanAccessCertCentral</span><span class="sxs-lookup"><span data-stu-id="c60c0-169">CanAccessCertCentral</span></span> |

    > [!Note]
    > <span data-ttu-id="c60c0-170">The value of **company** attribute is not real.</span><span class="sxs-lookup"><span data-stu-id="c60c0-170">The value of **company** attribute is not real.</span></span> <span data-ttu-id="c60c0-171">Update this value with actual company code.</span><span class="sxs-lookup"><span data-stu-id="c60c0-171">Update this value with actual company code.</span></span> <span data-ttu-id="c60c0-172">To get the value of **company** attribute contact [DigiCert support team](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="c60c0-172">To get the value of **company** attribute contact [DigiCert support team](mailto:support@digicert.com).</span></span>

    <span data-ttu-id="c60c0-173">a.</span><span class="sxs-lookup"><span data-stu-id="c60c0-173">a.</span></span> <span data-ttu-id="c60c0-174">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="c60c0-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/digicert-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/digicert-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="c60c0-177">b.</span><span class="sxs-lookup"><span data-stu-id="c60c0-177">b.</span></span> <span data-ttu-id="c60c0-178">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="c60c0-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="c60c0-179">c.</span><span class="sxs-lookup"><span data-stu-id="c60c0-179">c.</span></span> <span data-ttu-id="c60c0-180">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="c60c0-180">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="c60c0-181">d.</span><span class="sxs-lookup"><span data-stu-id="c60c0-181">d.</span></span> <span data-ttu-id="c60c0-182">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="c60c0-182">Click **Ok**.</span></span> 

1. <span data-ttu-id="c60c0-183">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="c60c0-183">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/digicert-tutorial/tutorial_digicert_certificate.png) 

1. <span data-ttu-id="c60c0-185">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="c60c0-185">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/digicert-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="c60c0-187">To configure single sign-on on **DigiCert** side, you need to send the downloaded **Metadata XML** to [DigiCert support team](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="c60c0-187">To configure single sign-on on **DigiCert** side, you need to send the downloaded **Metadata XML** to [DigiCert support team](mailto:support@digicert.com).</span></span> <span data-ttu-id="c60c0-188">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="c60c0-188">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c60c0-189">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c60c0-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="c60c0-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c60c0-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="c60c0-192">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c60c0-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c60c0-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="c60c0-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/digicert-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="c60c0-195">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="c60c0-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/digicert-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="c60c0-197">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="c60c0-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/digicert-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="c60c0-199">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c60c0-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/digicert-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c60c0-201">a.</span><span class="sxs-lookup"><span data-stu-id="c60c0-201">a.</span></span> <span data-ttu-id="c60c0-202">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c60c0-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c60c0-203">b.</span><span class="sxs-lookup"><span data-stu-id="c60c0-203">b.</span></span> <span data-ttu-id="c60c0-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c60c0-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c60c0-205">c.</span><span class="sxs-lookup"><span data-stu-id="c60c0-205">c.</span></span> <span data-ttu-id="c60c0-206">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="c60c0-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c60c0-207">d.</span><span class="sxs-lookup"><span data-stu-id="c60c0-207">d.</span></span> <span data-ttu-id="c60c0-208">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c60c0-208">Click **Create**.</span></span>
 
### <a name="creating-a-digicert-test-user"></a><span data-ttu-id="c60c0-209">Creating a DigiCert test user</span><span class="sxs-lookup"><span data-stu-id="c60c0-209">Creating a DigiCert test user</span></span>

<span data-ttu-id="c60c0-210">In this section, you create a user called Britta Simon in DigiCert.</span><span class="sxs-lookup"><span data-stu-id="c60c0-210">In this section, you create a user called Britta Simon in DigiCert.</span></span> <span data-ttu-id="c60c0-211">Please work with [DigiCert support team](mailto:support@digicert.com) to add the users in DigiCert.</span><span class="sxs-lookup"><span data-stu-id="c60c0-211">Please work with [DigiCert support team](mailto:support@digicert.com) to add the users in DigiCert.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c60c0-212">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c60c0-212">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c60c0-213">In this section, you enable Britta Simon to use Azure single sign-on by granting access to DigiCert.</span><span class="sxs-lookup"><span data-stu-id="c60c0-213">In this section, you enable Britta Simon to use Azure single sign-on by granting access to DigiCert.</span></span>

![Assign User][200] 

<span data-ttu-id="c60c0-215">**To assign Britta Simon to DigiCert, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c60c0-215">**To assign Britta Simon to DigiCert, perform the following steps:**</span></span>

1. <span data-ttu-id="c60c0-216">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c60c0-216">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="c60c0-218">In the applications list, select **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="c60c0-218">In the applications list, select **DigiCert**.</span></span>

    ![Configure Single Sign-On](./media/digicert-tutorial/tutorial_digicert_app.png) 

1. <span data-ttu-id="c60c0-220">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="c60c0-220">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="c60c0-222">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="c60c0-222">Click **Add** button.</span></span> <span data-ttu-id="c60c0-223">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c60c0-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="c60c0-225">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="c60c0-225">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="c60c0-226">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="c60c0-226">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="c60c0-227">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c60c0-227">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c60c0-228">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="c60c0-228">Testing single sign-on</span></span>

<span data-ttu-id="c60c0-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c60c0-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c60c0-230">When you click the DigiCert tile in the Access Panel, you should get automatically signed-on to your DeigiCert application.</span><span class="sxs-lookup"><span data-stu-id="c60c0-230">When you click the DigiCert tile in the Access Panel, you should get automatically signed-on to your DeigiCert application.</span></span>
<span data-ttu-id="c60c0-231">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c60c0-231">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c60c0-232">Additional resources</span><span class="sxs-lookup"><span data-stu-id="c60c0-232">Additional resources</span></span>

* [<span data-ttu-id="c60c0-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c60c0-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="c60c0-234">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c60c0-234">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/digicert-tutorial/tutorial_general_01.png
[2]: ./media/digicert-tutorial/tutorial_general_02.png
[3]: ./media/digicert-tutorial/tutorial_general_03.png
[4]: ./media/digicert-tutorial/tutorial_general_04.png

[100]: ./media/digicert-tutorial/tutorial_general_100.png

[200]: ./media/digicert-tutorial/tutorial_general_200.png
[201]: ./media/digicert-tutorial/tutorial_general_201.png
[202]: ./media/digicert-tutorial/tutorial_general_202.png
[203]: ./media/digicert-tutorial/tutorial_general_203.png

