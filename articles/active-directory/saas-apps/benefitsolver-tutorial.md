---
title: 'Tutorial: Azure Active Directory integration with Benefitsolver | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Benefitsolver.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 333394c1-b5a7-489c-8f7b-d1a5b4e782ea
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2017
ms.author: jeedes
ms.openlocfilehash: a14ac0d0b7cae515c2daad055e542fda93986392
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869350"
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="692f5-103">Tutorial: Azure Active Directory integration with Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="692f5-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>

<span data-ttu-id="692f5-104">In this tutorial, you learn how to integrate Benefitsolver with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="692f5-104">In this tutorial, you learn how to integrate Benefitsolver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="692f5-105">Integrating Benefitsolver with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="692f5-105">Integrating Benefitsolver with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="692f5-106">You can control in Azure AD who has access to Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="692f5-106">You can control in Azure AD who has access to Benefitsolver.</span></span>
- <span data-ttu-id="692f5-107">You can enable your users to automatically get signed-on to Benefitsolver (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="692f5-107">You can enable your users to automatically get signed-on to Benefitsolver (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="692f5-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="692f5-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="692f5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="692f5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="692f5-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="692f5-110">Prerequisites</span></span>

<span data-ttu-id="692f5-111">To configure Azure AD integration with Benefitsolver, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="692f5-111">To configure Azure AD integration with Benefitsolver, you need the following items:</span></span>

- <span data-ttu-id="692f5-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="692f5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="692f5-113">A Benefitsolver single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="692f5-113">A Benefitsolver single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="692f5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="692f5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="692f5-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="692f5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="692f5-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="692f5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="692f5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="692f5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="692f5-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="692f5-118">Scenario description</span></span>
<span data-ttu-id="692f5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="692f5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="692f5-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="692f5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="692f5-121">Adding Benefitsolver from the gallery</span><span class="sxs-lookup"><span data-stu-id="692f5-121">Adding Benefitsolver from the gallery</span></span>
1. <span data-ttu-id="692f5-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="692f5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benefitsolver-from-the-gallery"></a><span data-ttu-id="692f5-123">Adding Benefitsolver from the gallery</span><span class="sxs-lookup"><span data-stu-id="692f5-123">Adding Benefitsolver from the gallery</span></span>
<span data-ttu-id="692f5-124">To configure the integration of Benefitsolver into Azure AD, you need to add Benefitsolver from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="692f5-124">To configure the integration of Benefitsolver into Azure AD, you need to add Benefitsolver from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="692f5-125">**To add Benefitsolver from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="692f5-125">**To add Benefitsolver from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="692f5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="692f5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="692f5-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="692f5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="692f5-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="692f5-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="692f5-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="692f5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="692f5-133">In the search box, type **Benefitsolver**, select **Benefitsolver** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="692f5-133">In the search box, type **Benefitsolver**, select **Benefitsolver** from result panel then click **Add** button to add the application.</span></span>

    ![Benefitsolver in the results list](./media/benefitsolver-tutorial/tutorial_benefitsolver_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="692f5-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="692f5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="692f5-136">In this section, you configure and test Azure AD single sign-on with Benefitsolver based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="692f5-136">In this section, you configure and test Azure AD single sign-on with Benefitsolver based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="692f5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Benefitsolver is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="692f5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Benefitsolver is to a user in Azure AD.</span></span> <span data-ttu-id="692f5-138">In other words, a link relationship between an Azure AD user and the related user in Benefitsolver needs to be established.</span><span class="sxs-lookup"><span data-stu-id="692f5-138">In other words, a link relationship between an Azure AD user and the related user in Benefitsolver needs to be established.</span></span>

<span data-ttu-id="692f5-139">In Benefitsolver, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="692f5-139">In Benefitsolver, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="692f5-140">To configure and test Azure AD single sign-on with Benefitsolver, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="692f5-140">To configure and test Azure AD single sign-on with Benefitsolver, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="692f5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="692f5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="692f5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="692f5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="692f5-143">**[Create a Benefitsolver test user](#create-a-benefitsolver-test-user)** - to have a counterpart of Britta Simon in Benefitsolver that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="692f5-143">**[Create a Benefitsolver test user](#create-a-benefitsolver-test-user)** - to have a counterpart of Britta Simon in Benefitsolver that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="692f5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="692f5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="692f5-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="692f5-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="692f5-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="692f5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="692f5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Benefitsolver application.</span><span class="sxs-lookup"><span data-stu-id="692f5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Benefitsolver application.</span></span>

<span data-ttu-id="692f5-148">**To configure Azure AD single sign-on with Benefitsolver, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="692f5-148">**To configure Azure AD single sign-on with Benefitsolver, perform the following steps:**</span></span>

1. <span data-ttu-id="692f5-149">In the Azure portal, on the **Benefitsolver** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="692f5-149">In the Azure portal, on the **Benefitsolver** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="692f5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="692f5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/benefitsolver-tutorial/tutorial_benefitsolver_samlbase.png)

1. <span data-ttu-id="692f5-153">On the **Benefitsolver Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="692f5-153">On the **Benefitsolver Domain and URLs** section, perform the following steps:</span></span>

    ![Benefitsolver Domain and URLs single sign-on information](./media/benefitsolver-tutorial/tutorial_benefitsolver_url.png)

    <span data-ttu-id="692f5-155">a.</span><span class="sxs-lookup"><span data-stu-id="692f5-155">a.</span></span> <span data-ttu-id="692f5-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.benefitsolver.com`</span><span class="sxs-lookup"><span data-stu-id="692f5-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.benefitsolver.com`</span></span>

    <span data-ttu-id="692f5-157">b.</span><span class="sxs-lookup"><span data-stu-id="692f5-157">b.</span></span> <span data-ttu-id="692f5-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.benefitsolver.com/saml20`</span><span class="sxs-lookup"><span data-stu-id="692f5-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.benefitsolver.com/saml20`</span></span>

    <span data-ttu-id="692f5-159">c.</span><span class="sxs-lookup"><span data-stu-id="692f5-159">c.</span></span> <span data-ttu-id="692f5-160">In the **Reply URL** textbox, type the URL: `https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml`</span><span class="sxs-lookup"><span data-stu-id="692f5-160">In the **Reply URL** textbox, type the URL: `https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="692f5-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="692f5-161">These values are not real.</span></span> <span data-ttu-id="692f5-162">Update these values with the actual Sign-On URL,Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="692f5-162">Update these values with the actual Sign-On URL,Identifier and Reply URL.</span></span> <span data-ttu-id="692f5-163">Contact [Benefitsolver Client support team](https://www.businessolver.com/contact) to get these values.</span><span class="sxs-lookup"><span data-stu-id="692f5-163">Contact [Benefitsolver Client support team](https://www.businessolver.com/contact) to get these values.</span></span>

1. <span data-ttu-id="692f5-164">Your Benefitsolver application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span><span class="sxs-lookup"><span data-stu-id="692f5-164">Your Benefitsolver application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span>

    ![Benefitsolver attribute section](./media/benefitsolver-tutorial/tutorial_attribute.png)

1. <span data-ttu-id="692f5-166">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="692f5-166">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="692f5-167">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="692f5-167">Attribute Name</span></span>| <span data-ttu-id="692f5-168">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="692f5-168">Attribute Value</span></span>|
    |---------------|----------------|
    | <span data-ttu-id="692f5-169">ClientID</span><span class="sxs-lookup"><span data-stu-id="692f5-169">ClientID</span></span> | <span data-ttu-id="692f5-170">You need to get this value from your [Benefitsolver Client support team](https://www.businessolver.com/contact).</span><span class="sxs-lookup"><span data-stu-id="692f5-170">You need to get this value from your [Benefitsolver Client support team](https://www.businessolver.com/contact).</span></span>|
    | <span data-ttu-id="692f5-171">ClientKey</span><span class="sxs-lookup"><span data-stu-id="692f5-171">ClientKey</span></span> | <span data-ttu-id="692f5-172">You need to get this value from your [Benefitsolver Client support team](https://www.businessolver.com/contact).</span><span class="sxs-lookup"><span data-stu-id="692f5-172">You need to get this value from your [Benefitsolver Client support team](https://www.businessolver.com/contact).</span></span>|
    | <span data-ttu-id="692f5-173">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="692f5-173">LogoutURL</span></span> | <span data-ttu-id="692f5-174">You need to get this value from your [Benefitsolver Client support team](https://www.businessolver.com/contact).</span><span class="sxs-lookup"><span data-stu-id="692f5-174">You need to get this value from your [Benefitsolver Client support team](https://www.businessolver.com/contact).</span></span>|
    | <span data-ttu-id="692f5-175">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="692f5-175">EmployeeID</span></span> | <span data-ttu-id="692f5-176">You need to get this value from your [Benefitsolver Client support team](https://www.businessolver.com/contact).</span><span class="sxs-lookup"><span data-stu-id="692f5-176">You need to get this value from your [Benefitsolver Client support team](https://www.businessolver.com/contact).</span></span>|

    <span data-ttu-id="692f5-177">a.</span><span class="sxs-lookup"><span data-stu-id="692f5-177">a.</span></span> <span data-ttu-id="692f5-178">Click Add attribute to open the Add Attribute dialog.</span><span class="sxs-lookup"><span data-stu-id="692f5-178">Click Add attribute to open the Add Attribute dialog.</span></span>

    ![Benefitsolver attribute section](./media/benefitsolver-tutorial/tutorial_attribute_04.png)
    
    ![Benefitsolver attribute section](./media/benefitsolver-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="692f5-181">b.</span><span class="sxs-lookup"><span data-stu-id="692f5-181">b.</span></span> <span data-ttu-id="692f5-182">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="692f5-182">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="692f5-183">c.</span><span class="sxs-lookup"><span data-stu-id="692f5-183">c.</span></span> <span data-ttu-id="692f5-184">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="692f5-184">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="692f5-185">d.</span><span class="sxs-lookup"><span data-stu-id="692f5-185">d.</span></span> <span data-ttu-id="692f5-186">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="692f5-186">Click **Ok**.</span></span>

1. <span data-ttu-id="692f5-187">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="692f5-187">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/benefitsolver-tutorial/tutorial_benefitsolver_certificate.png) 

1. <span data-ttu-id="692f5-189">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="692f5-189">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/benefitsolver-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="692f5-191">To configure single sign-on on **Benefitsolver** side, you need to send the downloaded **Metadata XML** to [Benefitsolver support team](https://www.businessolver.com/contact).</span><span class="sxs-lookup"><span data-stu-id="692f5-191">To configure single sign-on on **Benefitsolver** side, you need to send the downloaded **Metadata XML** to [Benefitsolver support team](https://www.businessolver.com/contact).</span></span>

    > [!NOTE]
    > <span data-ttu-id="692f5-192">Your Benefitsolver support team has to do the actual SSO configuration.</span><span class="sxs-lookup"><span data-stu-id="692f5-192">Your Benefitsolver support team has to do the actual SSO configuration.</span></span> <span data-ttu-id="692f5-193">You will get a notification when SSO has been enabled for your subscription.</span><span class="sxs-lookup"><span data-stu-id="692f5-193">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="692f5-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="692f5-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="692f5-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="692f5-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="692f5-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="692f5-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="692f5-197">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="692f5-197">Create an Azure AD test user</span></span>

<span data-ttu-id="692f5-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="692f5-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="692f5-200">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="692f5-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="692f5-201">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="692f5-201">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/benefitsolver-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="692f5-203">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="692f5-203">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/benefitsolver-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="692f5-205">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="692f5-205">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/benefitsolver-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="692f5-207">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="692f5-207">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/benefitsolver-tutorial/create_aaduser_04.png)

    <span data-ttu-id="692f5-209">a.</span><span class="sxs-lookup"><span data-stu-id="692f5-209">a.</span></span> <span data-ttu-id="692f5-210">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="692f5-210">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="692f5-211">b.</span><span class="sxs-lookup"><span data-stu-id="692f5-211">b.</span></span> <span data-ttu-id="692f5-212">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="692f5-212">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="692f5-213">c.</span><span class="sxs-lookup"><span data-stu-id="692f5-213">c.</span></span> <span data-ttu-id="692f5-214">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="692f5-214">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="692f5-215">d.</span><span class="sxs-lookup"><span data-stu-id="692f5-215">d.</span></span> <span data-ttu-id="692f5-216">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="692f5-216">Click **Create**.</span></span>
 
### <a name="create-a-benefitsolver-test-user"></a><span data-ttu-id="692f5-217">Create a Benefitsolver test user</span><span class="sxs-lookup"><span data-stu-id="692f5-217">Create a Benefitsolver test user</span></span>

<span data-ttu-id="692f5-218">In order to enable Azure AD users to log into Benefitsolver, they must be provisioned into Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="692f5-218">In order to enable Azure AD users to log into Benefitsolver, they must be provisioned into Benefitsolver.</span></span> <span data-ttu-id="692f5-219">In the case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span><span class="sxs-lookup"><span data-stu-id="692f5-219">In the case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>

> [!NOTE]
> <span data-ttu-id="692f5-220">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="692f5-220">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver to provision AAD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="692f5-221">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="692f5-221">Assign the Azure AD test user</span></span>

<span data-ttu-id="692f5-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="692f5-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Benefitsolver.</span></span>

![Assign the user role][200] 

<span data-ttu-id="692f5-224">**To assign Britta Simon to Benefitsolver, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="692f5-224">**To assign Britta Simon to Benefitsolver, perform the following steps:**</span></span>

1. <span data-ttu-id="692f5-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="692f5-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="692f5-227">In the applications list, select **Benefitsolver**.</span><span class="sxs-lookup"><span data-stu-id="692f5-227">In the applications list, select **Benefitsolver**.</span></span>

    ![The Benefitsolver link in the Applications list](./media/benefitsolver-tutorial/tutorial_benefitsolver_app.png)  

1. <span data-ttu-id="692f5-229">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="692f5-229">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="692f5-231">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="692f5-231">Click **Add** button.</span></span> <span data-ttu-id="692f5-232">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="692f5-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="692f5-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="692f5-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="692f5-235">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="692f5-235">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="692f5-236">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="692f5-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="692f5-237">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="692f5-237">Test single sign-on</span></span>

<span data-ttu-id="692f5-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="692f5-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="692f5-239">When you click the Benefitsolver tile in the Access Panel, you should get automatically signed-on to your Benefitsolver application.</span><span class="sxs-lookup"><span data-stu-id="692f5-239">When you click the Benefitsolver tile in the Access Panel, you should get automatically signed-on to your Benefitsolver application.</span></span>
<span data-ttu-id="692f5-240">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="692f5-240">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="692f5-241">Additional resources</span><span class="sxs-lookup"><span data-stu-id="692f5-241">Additional resources</span></span>

* [<span data-ttu-id="692f5-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="692f5-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="692f5-243">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="692f5-243">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/benefitsolver-tutorial/tutorial_general_01.png
[2]: ./media/benefitsolver-tutorial/tutorial_general_02.png
[3]: ./media/benefitsolver-tutorial/tutorial_general_03.png
[4]: ./media/benefitsolver-tutorial/tutorial_general_04.png

[100]: ./media/benefitsolver-tutorial/tutorial_general_100.png

[200]: ./media/benefitsolver-tutorial/tutorial_general_200.png
[201]: ./media/benefitsolver-tutorial/tutorial_general_201.png
[202]: ./media/benefitsolver-tutorial/tutorial_general_202.png
[203]: ./media/benefitsolver-tutorial/tutorial_general_203.png

