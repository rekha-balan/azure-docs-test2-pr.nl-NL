---
title: 'Tutorial: Azure Active Directory integration with Andromeda | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Andromeda.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7a142c86-ca0c-4915-b1d8-124c08c3e3d8
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2018
ms.author: jeedes
ms.openlocfilehash: 047e1ea6a474d95c57ffc2bdff5ad8a5c45e0d36
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866728"
---
# <a name="tutorial-azure-active-directory-integration-with-andromeda"></a><span data-ttu-id="917e7-103">Tutorial: Azure Active Directory integration with Andromeda</span><span class="sxs-lookup"><span data-stu-id="917e7-103">Tutorial: Azure Active Directory integration with Andromeda</span></span>

<span data-ttu-id="917e7-104">In this tutorial, you learn how to integrate Andromeda with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="917e7-104">In this tutorial, you learn how to integrate Andromeda with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="917e7-105">Integrating Andromeda with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="917e7-105">Integrating Andromeda with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="917e7-106">You can control in Azure AD who has access to Andromeda.</span><span class="sxs-lookup"><span data-stu-id="917e7-106">You can control in Azure AD who has access to Andromeda.</span></span>
- <span data-ttu-id="917e7-107">You can enable your users to automatically get signed-on to Andromeda (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="917e7-107">You can enable your users to automatically get signed-on to Andromeda (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="917e7-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="917e7-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="917e7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="917e7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="917e7-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="917e7-110">Prerequisites</span></span>

<span data-ttu-id="917e7-111">To configure Azure AD integration with Andromeda, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="917e7-111">To configure Azure AD integration with Andromeda, you need the following items:</span></span>

- <span data-ttu-id="917e7-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="917e7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="917e7-113">An Andromeda single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="917e7-113">An Andromeda single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="917e7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="917e7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="917e7-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="917e7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="917e7-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="917e7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="917e7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="917e7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="917e7-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="917e7-118">Scenario description</span></span>
<span data-ttu-id="917e7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="917e7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="917e7-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="917e7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="917e7-121">Adding Andromeda from the gallery</span><span class="sxs-lookup"><span data-stu-id="917e7-121">Adding Andromeda from the gallery</span></span>
2. <span data-ttu-id="917e7-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="917e7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-andromeda-from-the-gallery"></a><span data-ttu-id="917e7-123">Adding Andromeda from the gallery</span><span class="sxs-lookup"><span data-stu-id="917e7-123">Adding Andromeda from the gallery</span></span>
<span data-ttu-id="917e7-124">To configure the integration of Andromeda into Azure AD, you need to add Andromeda from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="917e7-124">To configure the integration of Andromeda into Azure AD, you need to add Andromeda from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="917e7-125">**To add Andromeda from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="917e7-125">**To add Andromeda from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="917e7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="917e7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="917e7-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="917e7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="917e7-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="917e7-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="917e7-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="917e7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="917e7-133">In the search box, type **Andromeda**, select **Andromeda** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="917e7-133">In the search box, type **Andromeda**, select **Andromeda** from result panel then click **Add** button to add the application.</span></span>

    ![Andromeda in the results list](./media/andromedascm-tutorial/tutorial_andromedascm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="917e7-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="917e7-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="917e7-136">In this section, you configure and test Azure AD single sign-on with Andromeda based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="917e7-136">In this section, you configure and test Azure AD single sign-on with Andromeda based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="917e7-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Andromeda is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="917e7-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Andromeda is to a user in Azure AD.</span></span> <span data-ttu-id="917e7-138">In other words, a link relationship between an Azure AD user and the related user in Andromeda needs to be established.</span><span class="sxs-lookup"><span data-stu-id="917e7-138">In other words, a link relationship between an Azure AD user and the related user in Andromeda needs to be established.</span></span>

<span data-ttu-id="917e7-139">To configure and test Azure AD single sign-on with Andromeda, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="917e7-139">To configure and test Azure AD single sign-on with Andromeda, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="917e7-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="917e7-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="917e7-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="917e7-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="917e7-142">**[Create an Andromeda test user](#create-an-andromeda-test-user)** - to have a counterpart of Britta Simon in Andromeda that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="917e7-142">**[Create an Andromeda test user](#create-an-andromeda-test-user)** - to have a counterpart of Britta Simon in Andromeda that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="917e7-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="917e7-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="917e7-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="917e7-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="917e7-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="917e7-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="917e7-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Andromeda application.</span><span class="sxs-lookup"><span data-stu-id="917e7-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Andromeda application.</span></span>

<span data-ttu-id="917e7-147">**To configure Azure AD single sign-on with Andromeda, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="917e7-147">**To configure Azure AD single sign-on with Andromeda, perform the following steps:**</span></span>

1. <span data-ttu-id="917e7-148">In the Azure portal, on the **Andromeda** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="917e7-148">In the Azure portal, on the **Andromeda** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="917e7-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="917e7-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/andromedascm-tutorial/tutorial_andromedascm_samlbase.png)

3. <span data-ttu-id="917e7-152">On the **Andromeda Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="917e7-152">On the **Andromeda Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Andromeda Domain and URLs single sign-on information](./media/andromedascm-tutorial/tutorial_andromedascm_url.png)

    <span data-ttu-id="917e7-154">a.</span><span class="sxs-lookup"><span data-stu-id="917e7-154">a.</span></span> <span data-ttu-id="917e7-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantURL>.ngcxpress.com/`</span><span class="sxs-lookup"><span data-stu-id="917e7-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantURL>.ngcxpress.com/`</span></span>

    <span data-ttu-id="917e7-156">b.</span><span class="sxs-lookup"><span data-stu-id="917e7-156">b.</span></span> <span data-ttu-id="917e7-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<tenantURL>.ngcxpress.com/SAMLConsumer.aspx`</span><span class="sxs-lookup"><span data-stu-id="917e7-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<tenantURL>.ngcxpress.com/SAMLConsumer.aspx`</span></span>

4. <span data-ttu-id="917e7-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="917e7-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Andromeda Domain and URLs single sign-on information](./media/andromedascm-tutorial/tutorial_andromedascm_url1.png)

    <span data-ttu-id="917e7-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantURL>.ngcxpress.com/SAMLLogon.aspx`</span><span class="sxs-lookup"><span data-stu-id="917e7-160">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantURL>.ngcxpress.com/SAMLLogon.aspx`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="917e7-161">The preceding value is not real value.</span><span class="sxs-lookup"><span data-stu-id="917e7-161">The preceding value is not real value.</span></span> <span data-ttu-id="917e7-162">You will update the value with the actual Identifier, Reply URL, and Sign-On URL which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="917e7-162">You will update the value with the actual Identifier, Reply URL, and Sign-On URL which is explained later in the tutorial.</span></span>

5. <span data-ttu-id="917e7-163">Andromeda application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="917e7-163">Andromeda application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="917e7-164">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="917e7-164">Configure the following claims for this application.</span></span> <span data-ttu-id="917e7-165">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="917e7-165">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="917e7-166">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="917e7-166">The following screenshot shows an example for this.</span></span>
    
    ![Configure Single Sign-On attb](./media/andromedascm-tutorial/tutorial_andromedascm_attribute.png)

    > [!Important]
    > <span data-ttu-id="917e7-168">Clear out the NameSpace definitions while setting these up.</span><span class="sxs-lookup"><span data-stu-id="917e7-168">Clear out the NameSpace definitions while setting these up.</span></span>
    
6. <span data-ttu-id="917e7-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="917e7-169">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="917e7-170">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="917e7-170">Attribute Name</span></span> | <span data-ttu-id="917e7-171">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="917e7-171">Attribute Value</span></span> |
    | -------------- | -------------------- |    
    | <span data-ttu-id="917e7-172">role</span><span class="sxs-lookup"><span data-stu-id="917e7-172">role</span></span>        | <span data-ttu-id="917e7-173">App specific role</span><span class="sxs-lookup"><span data-stu-id="917e7-173">App specific role</span></span> |
    | <span data-ttu-id="917e7-174">type</span><span class="sxs-lookup"><span data-stu-id="917e7-174">type</span></span>        | <span data-ttu-id="917e7-175">App Type</span><span class="sxs-lookup"><span data-stu-id="917e7-175">App Type</span></span> |
    | <span data-ttu-id="917e7-176">company</span><span class="sxs-lookup"><span data-stu-id="917e7-176">company</span></span>       | <span data-ttu-id="917e7-177">CompanyName</span><span class="sxs-lookup"><span data-stu-id="917e7-177">CompanyName</span></span>    |

    > [!NOTE]
    > <span data-ttu-id="917e7-178">There are not real values.</span><span class="sxs-lookup"><span data-stu-id="917e7-178">There are not real values.</span></span> <span data-ttu-id="917e7-179">These values are only for demo purpose, please use your organization roles.</span><span class="sxs-lookup"><span data-stu-id="917e7-179">These values are only for demo purpose, please use your organization roles.</span></span>

    <span data-ttu-id="917e7-180">a.</span><span class="sxs-lookup"><span data-stu-id="917e7-180">a.</span></span> <span data-ttu-id="917e7-181">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="917e7-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On Add](./media/andromedascm-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On Addattb](./media/andromedascm-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="917e7-184">b.</span><span class="sxs-lookup"><span data-stu-id="917e7-184">b.</span></span> <span data-ttu-id="917e7-185">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="917e7-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="917e7-186">c.</span><span class="sxs-lookup"><span data-stu-id="917e7-186">c.</span></span> <span data-ttu-id="917e7-187">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="917e7-187">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="917e7-188">d.</span><span class="sxs-lookup"><span data-stu-id="917e7-188">d.</span></span> <span data-ttu-id="917e7-189">Leave the **Namespace** blank.</span><span class="sxs-lookup"><span data-stu-id="917e7-189">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="917e7-190">e.</span><span class="sxs-lookup"><span data-stu-id="917e7-190">e.</span></span> <span data-ttu-id="917e7-191">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="917e7-191">Click **Ok**.</span></span>

7. <span data-ttu-id="917e7-192">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="917e7-192">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/andromedascm-tutorial/tutorial_andromedascm_certificate.png) 

8. <span data-ttu-id="917e7-194">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="917e7-194">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/andromedascm-tutorial/tutorial_general_400.png)
    
9. <span data-ttu-id="917e7-196">On the **Andromeda Configuration** section, click **Configure Andromeda** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="917e7-196">On the **Andromeda Configuration** section, click **Configure Andromeda** to open **Configure sign-on** window.</span></span> <span data-ttu-id="917e7-197">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="917e7-197">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Andromeda Configuration](./media/andromedascm-tutorial/tutorial_andromedascm_configure.png)

10. <span data-ttu-id="917e7-199">Sign-on to your Andromeda company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="917e7-199">Sign-on to your Andromeda company site as administrator.</span></span>

11. <span data-ttu-id="917e7-200">On the top of the menubar click **Admin** and navigate to **Administration**.</span><span class="sxs-lookup"><span data-stu-id="917e7-200">On the top of the menubar click **Admin** and navigate to **Administration**.</span></span>

    ![Andromeda admin](./media/andromedascm-tutorial/tutorial_andromedascm_admin.png)

12. <span data-ttu-id="917e7-202">On the left side of tool bar under **Interfaces** section, click **SAML Configuration**.</span><span class="sxs-lookup"><span data-stu-id="917e7-202">On the left side of tool bar under **Interfaces** section, click **SAML Configuration**.</span></span>

    ![Andromeda saml](./media/andromedascm-tutorial/tutorial_andromedascm_saml.png)

13. <span data-ttu-id="917e7-204">On the **SAML Configuration** section page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="917e7-204">On the **SAML Configuration** section page, perform the following steps:</span></span>

    ![Andromeda config](./media/andromedascm-tutorial/tutorial_andromedascm_config.png)

    <span data-ttu-id="917e7-206">a.</span><span class="sxs-lookup"><span data-stu-id="917e7-206">a.</span></span> <span data-ttu-id="917e7-207">Check **Enable SSO with SAML**.</span><span class="sxs-lookup"><span data-stu-id="917e7-207">Check **Enable SSO with SAML**.</span></span>

    <span data-ttu-id="917e7-208">b.</span><span class="sxs-lookup"><span data-stu-id="917e7-208">b.</span></span> <span data-ttu-id="917e7-209">Under **Andromeda Information** section, copy the **SP Identity** value and paste it into the **Identifier** textbox of **Andromeda Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="917e7-209">Under **Andromeda Information** section, copy the **SP Identity** value and paste it into the **Identifier** textbox of **Andromeda Domain and URLs** section.</span></span>

    <span data-ttu-id="917e7-210">c.</span><span class="sxs-lookup"><span data-stu-id="917e7-210">c.</span></span> <span data-ttu-id="917e7-211">Copy the **Consumer URL** value and paste it into the **Reply URL** textbox of **Andromeda Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="917e7-211">Copy the **Consumer URL** value and paste it into the **Reply URL** textbox of **Andromeda Domain and URLs** section.</span></span>

    <span data-ttu-id="917e7-212">d.</span><span class="sxs-lookup"><span data-stu-id="917e7-212">d.</span></span> <span data-ttu-id="917e7-213">Copy the **Logon URL** value and paste it into the **Sign-on URL** textbox of **Andromeda Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="917e7-213">Copy the **Logon URL** value and paste it into the **Sign-on URL** textbox of **Andromeda Domain and URLs** section.</span></span>

    <span data-ttu-id="917e7-214">e.</span><span class="sxs-lookup"><span data-stu-id="917e7-214">e.</span></span> <span data-ttu-id="917e7-215">Under **SAML Identity Provider** section, type your IDP Name.</span><span class="sxs-lookup"><span data-stu-id="917e7-215">Under **SAML Identity Provider** section, type your IDP Name.</span></span>

    <span data-ttu-id="917e7-216">f.</span><span class="sxs-lookup"><span data-stu-id="917e7-216">f.</span></span> <span data-ttu-id="917e7-217">In the **Single Sign On End Point** textbox, paste the value of **SAML Single Sign-On Service URL** which, you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="917e7-217">In the **Single Sign On End Point** textbox, paste the value of **SAML Single Sign-On Service URL** which, you have copied from the Azure portal.</span></span>

    <span data-ttu-id="917e7-218">g.</span><span class="sxs-lookup"><span data-stu-id="917e7-218">g.</span></span> <span data-ttu-id="917e7-219">Open the downloaded **Base64 encoded certificate** from Azure portal in notepad, paste it into the **X 509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="917e7-219">Open the downloaded **Base64 encoded certificate** from Azure portal in notepad, paste it into the **X 509 Certificate** textbox.</span></span>
    
    <span data-ttu-id="917e7-220">h.</span><span class="sxs-lookup"><span data-stu-id="917e7-220">h.</span></span> <span data-ttu-id="917e7-221">Map the following attributes with the respective value to facilitate SSO login from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="917e7-221">Map the following attributes with the respective value to facilitate SSO login from Azure AD.</span></span> <span data-ttu-id="917e7-222">The **User ID** attribute is required for logging in.</span><span class="sxs-lookup"><span data-stu-id="917e7-222">The **User ID** attribute is required for logging in.</span></span> <span data-ttu-id="917e7-223">For provisioning, **Email**, **Company**, **UserType**, and **Role** are required.</span><span class="sxs-lookup"><span data-stu-id="917e7-223">For provisioning, **Email**, **Company**, **UserType**, and **Role** are required.</span></span> <span data-ttu-id="917e7-224">In this section, we define attributes mapping (name and values) which correlate to those defined within Azure portal</span><span class="sxs-lookup"><span data-stu-id="917e7-224">In this section, we define attributes mapping (name and values) which correlate to those defined within Azure portal</span></span>

    ![Andromeda attbmap](./media/andromedascm-tutorial/tutorial_andromedascm_attbmap.png)

    <span data-ttu-id="917e7-226">i.</span><span class="sxs-lookup"><span data-stu-id="917e7-226">i.</span></span> <span data-ttu-id="917e7-227">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="917e7-227">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="917e7-228">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="917e7-228">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="917e7-229">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="917e7-229">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="917e7-230">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="917e7-230">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="917e7-231">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="917e7-231">Create an Azure AD test user</span></span>

<span data-ttu-id="917e7-232">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="917e7-232">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="917e7-234">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="917e7-234">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="917e7-235">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="917e7-235">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/andromedascm-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="917e7-237">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="917e7-237">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/andromedascm-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="917e7-239">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="917e7-239">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/andromedascm-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="917e7-241">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="917e7-241">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/andromedascm-tutorial/create_aaduser_04.png)

    <span data-ttu-id="917e7-243">a.</span><span class="sxs-lookup"><span data-stu-id="917e7-243">a.</span></span> <span data-ttu-id="917e7-244">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="917e7-244">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="917e7-245">b.</span><span class="sxs-lookup"><span data-stu-id="917e7-245">b.</span></span> <span data-ttu-id="917e7-246">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="917e7-246">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="917e7-247">c.</span><span class="sxs-lookup"><span data-stu-id="917e7-247">c.</span></span> <span data-ttu-id="917e7-248">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="917e7-248">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="917e7-249">d.</span><span class="sxs-lookup"><span data-stu-id="917e7-249">d.</span></span> <span data-ttu-id="917e7-250">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="917e7-250">Click **Create**.</span></span>
 
### <a name="create-an-andromeda-test-user"></a><span data-ttu-id="917e7-251">Create an Andromeda test user</span><span class="sxs-lookup"><span data-stu-id="917e7-251">Create an Andromeda test user</span></span>

<span data-ttu-id="917e7-252">The objective of this section is to create a user called Britta Simon in Andromeda.</span><span class="sxs-lookup"><span data-stu-id="917e7-252">The objective of this section is to create a user called Britta Simon in Andromeda.</span></span> <span data-ttu-id="917e7-253">Andromeda supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="917e7-253">Andromeda supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="917e7-254">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="917e7-254">There is no action item for you in this section.</span></span> <span data-ttu-id="917e7-255">A new user is created during an attempt to access Andromeda if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="917e7-255">A new user is created during an attempt to access Andromeda if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="917e7-256">If you need to create a user manually, contact [Andromeda Client support team](https://www.ngcsoftware.com/support/).</span><span class="sxs-lookup"><span data-stu-id="917e7-256">If you need to create a user manually, contact [Andromeda Client support team](https://www.ngcsoftware.com/support/).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="917e7-257">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="917e7-257">Assign the Azure AD test user</span></span>

<span data-ttu-id="917e7-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Andromeda.</span><span class="sxs-lookup"><span data-stu-id="917e7-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Andromeda.</span></span>

![Assign the user role][200] 

<span data-ttu-id="917e7-260">**To assign Britta Simon to Andromeda, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="917e7-260">**To assign Britta Simon to Andromeda, perform the following steps:**</span></span>

1. <span data-ttu-id="917e7-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="917e7-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="917e7-263">In the applications list, select **Andromeda**.</span><span class="sxs-lookup"><span data-stu-id="917e7-263">In the applications list, select **Andromeda**.</span></span>

    ![The Andromeda link in the Applications list](./media/andromedascm-tutorial/tutorial_andromedascm_app.png)  

3. <span data-ttu-id="917e7-265">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="917e7-265">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="917e7-267">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="917e7-267">Click **Add** button.</span></span> <span data-ttu-id="917e7-268">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="917e7-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="917e7-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="917e7-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="917e7-271">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="917e7-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="917e7-272">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="917e7-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="917e7-273">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="917e7-273">Test single sign-on</span></span>

<span data-ttu-id="917e7-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="917e7-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="917e7-275">When you click the Andromeda tile in the Access Panel, you should get automatically signed-on to your Andromeda application.</span><span class="sxs-lookup"><span data-stu-id="917e7-275">When you click the Andromeda tile in the Access Panel, you should get automatically signed-on to your Andromeda application.</span></span>
<span data-ttu-id="917e7-276">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="917e7-276">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="917e7-277">Additional resources</span><span class="sxs-lookup"><span data-stu-id="917e7-277">Additional resources</span></span>

* [<span data-ttu-id="917e7-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="917e7-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="917e7-279">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="917e7-279">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/andromedascm-tutorial/tutorial_general_01.png
[2]: ./media/andromedascm-tutorial/tutorial_general_02.png
[3]: ./media/andromedascm-tutorial/tutorial_general_03.png
[4]: ./media/andromedascm-tutorial/tutorial_general_04.png

[100]: ./media/andromedascm-tutorial/tutorial_general_100.png

[200]: ./media/andromedascm-tutorial/tutorial_general_200.png
[201]: ./media/andromedascm-tutorial/tutorial_general_201.png
[202]: ./media/andromedascm-tutorial/tutorial_general_202.png
[203]: ./media/andromedascm-tutorial/tutorial_general_203.png
