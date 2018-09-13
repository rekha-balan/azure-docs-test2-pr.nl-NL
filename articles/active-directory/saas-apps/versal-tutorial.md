---
title: 'Tutorial: Azure Active Directory integration with Versal | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Versal.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 5b2e53c0-61a3-4954-ae46-8c28c6368bfd
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeedes
ms.openlocfilehash: a6e1f73218efb11da475f3e67188863c3b99de97
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869995"
---
# <a name="tutorial-azure-active-directory-integration-with-versal"></a><span data-ttu-id="27efb-103">Tutorial: Azure Active Directory integration with Versal</span><span class="sxs-lookup"><span data-stu-id="27efb-103">Tutorial: Azure Active Directory integration with Versal</span></span>

<span data-ttu-id="27efb-104">In this tutorial, you learn how to integrate Versal with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="27efb-104">In this tutorial, you learn how to integrate Versal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="27efb-105">Integrating Versal with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="27efb-105">Integrating Versal with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="27efb-106">You can control in Azure AD who has access to Versal.</span><span class="sxs-lookup"><span data-stu-id="27efb-106">You can control in Azure AD who has access to Versal.</span></span>
- <span data-ttu-id="27efb-107">You can enable your users to automatically get signed-on to Versal (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="27efb-107">You can enable your users to automatically get signed-on to Versal (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="27efb-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="27efb-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="27efb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="27efb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27efb-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="27efb-110">Prerequisites</span></span>

<span data-ttu-id="27efb-111">To configure Azure AD integration with Versal, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="27efb-111">To configure Azure AD integration with Versal, you need the following items:</span></span>

- <span data-ttu-id="27efb-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="27efb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="27efb-113">A Versal single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="27efb-113">A Versal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="27efb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="27efb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="27efb-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="27efb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="27efb-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="27efb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="27efb-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="27efb-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="27efb-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="27efb-118">Scenario description</span></span>
<span data-ttu-id="27efb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="27efb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="27efb-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="27efb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="27efb-121">Adding Versal from the gallery</span><span class="sxs-lookup"><span data-stu-id="27efb-121">Adding Versal from the gallery</span></span>
1. <span data-ttu-id="27efb-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="27efb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-versal-from-the-gallery"></a><span data-ttu-id="27efb-123">Adding Versal from the gallery</span><span class="sxs-lookup"><span data-stu-id="27efb-123">Adding Versal from the gallery</span></span>
<span data-ttu-id="27efb-124">To configure the integration of Versal into Azure AD, you need to add Versal from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="27efb-124">To configure the integration of Versal into Azure AD, you need to add Versal from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="27efb-125">**To add Versal from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="27efb-125">**To add Versal from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="27efb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="27efb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="27efb-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="27efb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="27efb-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="27efb-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="27efb-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="27efb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="27efb-133">In the search box, type **Versal**, select **Versal** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="27efb-133">In the search box, type **Versal**, select **Versal** from result panel then click **Add** button to add the application.</span></span>

    ![Versal in the results list](./media/versal-tutorial/tutorial_versal_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="27efb-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="27efb-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="27efb-136">In this section, you configure and test Azure AD single sign-on with Versal based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="27efb-136">In this section, you configure and test Azure AD single sign-on with Versal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="27efb-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Versal is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="27efb-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Versal is to a user in Azure AD.</span></span> <span data-ttu-id="27efb-138">In other words, a link relationship between an Azure AD user and the related user in Versal needs to be established.</span><span class="sxs-lookup"><span data-stu-id="27efb-138">In other words, a link relationship between an Azure AD user and the related user in Versal needs to be established.</span></span>

<span data-ttu-id="27efb-139">In Versal, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="27efb-139">In Versal, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="27efb-140">To configure and test Azure AD single sign-on with Versal, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="27efb-140">To configure and test Azure AD single sign-on with Versal, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="27efb-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="27efb-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="27efb-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="27efb-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="27efb-143">**[Create a Versal test user](#create-a-versal-test-user)** - to have a counterpart of Britta Simon in Versal that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="27efb-143">**[Create a Versal test user](#create-a-versal-test-user)** - to have a counterpart of Britta Simon in Versal that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="27efb-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="27efb-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="27efb-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="27efb-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="27efb-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="27efb-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="27efb-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Versal application.</span><span class="sxs-lookup"><span data-stu-id="27efb-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Versal application.</span></span>

<span data-ttu-id="27efb-148">**To configure Azure AD single sign-on with Versal, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="27efb-148">**To configure Azure AD single sign-on with Versal, perform the following steps:**</span></span>

1. <span data-ttu-id="27efb-149">In the Azure portal, on the **Versal** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="27efb-149">In the Azure portal, on the **Versal** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="27efb-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="27efb-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/versal-tutorial/tutorial_versal_samlbase.png)

1. <span data-ttu-id="27efb-153">On the **Versal Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="27efb-153">On the **Versal Domain and URLs** section, perform the following steps:</span></span>

    ![Versal Domain and URLs single sign-on information](./media/versal-tutorial/tutorial_versal_url.png)

    <span data-ttu-id="27efb-155">a.</span><span class="sxs-lookup"><span data-stu-id="27efb-155">a.</span></span> <span data-ttu-id="27efb-156">In the **Identifier** textbox, type the value: `VERSAL`</span><span class="sxs-lookup"><span data-stu-id="27efb-156">In the **Identifier** textbox, type the value: `VERSAL`</span></span>

    <span data-ttu-id="27efb-157">b.</span><span class="sxs-lookup"><span data-stu-id="27efb-157">b.</span></span> <span data-ttu-id="27efb-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://versal.com/sso/saml/orgs/<organization_id>`</span><span class="sxs-lookup"><span data-stu-id="27efb-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://versal.com/sso/saml/orgs/<organization_id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="27efb-159">Reply URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="27efb-159">Reply URL value is not real.</span></span> <span data-ttu-id="27efb-160">Update this value with the actual Reply URL.</span><span class="sxs-lookup"><span data-stu-id="27efb-160">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="27efb-161">Contact [Versal support team](https://support.versal.com/hc/) to get this value.</span><span class="sxs-lookup"><span data-stu-id="27efb-161">Contact [Versal support team](https://support.versal.com/hc/) to get this value.</span></span>
    
1. <span data-ttu-id="27efb-162">Your application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="27efb-162">Your application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="27efb-163">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="27efb-163">The following screenshot shows an example for this.</span></span> <span data-ttu-id="27efb-164">The default value of **User Identifier** is **user.userprincipalname** but **Versal** expects this to be mapped with the user's email address.</span><span class="sxs-lookup"><span data-stu-id="27efb-164">The default value of **User Identifier** is **user.userprincipalname** but **Versal** expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="27efb-165">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span><span class="sxs-lookup"><span data-stu-id="27efb-165">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration.</span></span>
    
    ![User Identifier dropdown menu](./media/versal-tutorial/tutorial_versal_attribute.png)

1. <span data-ttu-id="27efb-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="27efb-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/versal-tutorial/tutorial_versal_certificate.png) 

1. <span data-ttu-id="27efb-169">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="27efb-169">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/versal-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="27efb-171">To configure single sign-on on **Versal** side, you need to send the downloaded **Metadata XML**  and **SAML Signing Certificate** to [Versal support team](https://support.versal.com/hc/).</span><span class="sxs-lookup"><span data-stu-id="27efb-171">To configure single sign-on on **Versal** side, you need to send the downloaded **Metadata XML**  and **SAML Signing Certificate** to [Versal support team](https://support.versal.com/hc/).</span></span> <span data-ttu-id="27efb-172">They will configure your Versal organization to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="27efb-172">They will configure your Versal organization to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="27efb-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="27efb-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="27efb-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="27efb-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="27efb-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="27efb-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="27efb-176">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="27efb-176">Create an Azure AD test user</span></span>

<span data-ttu-id="27efb-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="27efb-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="27efb-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="27efb-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="27efb-180">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="27efb-180">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/versal-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="27efb-182">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="27efb-182">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/versal-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="27efb-184">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="27efb-184">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/versal-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="27efb-186">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="27efb-186">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/versal-tutorial/create_aaduser_04.png)

    <span data-ttu-id="27efb-188">a.</span><span class="sxs-lookup"><span data-stu-id="27efb-188">a.</span></span> <span data-ttu-id="27efb-189">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="27efb-189">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="27efb-190">b.</span><span class="sxs-lookup"><span data-stu-id="27efb-190">b.</span></span> <span data-ttu-id="27efb-191">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="27efb-191">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="27efb-192">c.</span><span class="sxs-lookup"><span data-stu-id="27efb-192">c.</span></span> <span data-ttu-id="27efb-193">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="27efb-193">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="27efb-194">d.</span><span class="sxs-lookup"><span data-stu-id="27efb-194">d.</span></span> <span data-ttu-id="27efb-195">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="27efb-195">Click **Create**.</span></span>
  
### <a name="create-a-versal-test-user"></a><span data-ttu-id="27efb-196">Create a Versal test user</span><span class="sxs-lookup"><span data-stu-id="27efb-196">Create a Versal test user</span></span>

<span data-ttu-id="27efb-197">In this section, you create a user called Britta Simon in Versal.</span><span class="sxs-lookup"><span data-stu-id="27efb-197">In this section, you create a user called Britta Simon in Versal.</span></span> <span data-ttu-id="27efb-198">Please follow the [Creating a SAML test user](https://support.versal.com/hc/en-us/articles/115011672887-Creating-a-SAML-test-user) support guide to create the user Britta Simon within your organization.</span><span class="sxs-lookup"><span data-stu-id="27efb-198">Please follow the [Creating a SAML test user](https://support.versal.com/hc/en-us/articles/115011672887-Creating-a-SAML-test-user) support guide to create the user Britta Simon within your organization.</span></span> <span data-ttu-id="27efb-199">Users must be created and activated in Versal before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="27efb-199">Users must be created and activated in Versal before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="27efb-200">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="27efb-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="27efb-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Versal.</span><span class="sxs-lookup"><span data-stu-id="27efb-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Versal.</span></span>

![Assign the user role][200] 

<span data-ttu-id="27efb-203">**To assign Britta Simon to Versal, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="27efb-203">**To assign Britta Simon to Versal, perform the following steps:**</span></span>

1. <span data-ttu-id="27efb-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="27efb-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="27efb-206">In the applications list, select **Versal**.</span><span class="sxs-lookup"><span data-stu-id="27efb-206">In the applications list, select **Versal**.</span></span>

    ![The Versal link in the Applications list](./media/versal-tutorial/tutorial_versal_app.png)  

1. <span data-ttu-id="27efb-208">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="27efb-208">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="27efb-210">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="27efb-210">Click **Add** button.</span></span> <span data-ttu-id="27efb-211">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="27efb-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="27efb-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="27efb-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="27efb-214">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="27efb-214">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="27efb-215">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="27efb-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="27efb-216">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="27efb-216">Test single sign-on</span></span>

<span data-ttu-id="27efb-217">In this section, you test your Azure AD single sign-on configuration using a Versal course embedded within your website.</span><span class="sxs-lookup"><span data-stu-id="27efb-217">In this section, you test your Azure AD single sign-on configuration using a Versal course embedded within your website.</span></span>
<span data-ttu-id="27efb-218">Please see the [Embedding Organizational Courses](https://support.versal.com/hc/en-us/articles/203271866-Embedding-organizational-courses) **SAML Single Sign-On** support guide for instructions on how to embed a Versal course with support for Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="27efb-218">Please see the [Embedding Organizational Courses](https://support.versal.com/hc/en-us/articles/203271866-Embedding-organizational-courses) **SAML Single Sign-On** support guide for instructions on how to embed a Versal course with support for Azure AD single sign-on.</span></span> 

<span data-ttu-id="27efb-219">You will need to create a course, share it with your organization, and publish it in order to test course embedding.</span><span class="sxs-lookup"><span data-stu-id="27efb-219">You will need to create a course, share it with your organization, and publish it in order to test course embedding.</span></span> <span data-ttu-id="27efb-220">Please see [Creating a course](https://support.versal.com/hc/en-us/articles/203722528-Create-a-course), [Publishing a course](https://support.versal.com/hc/en-us/articles/203753398-Publishing-a-course), and [Course and learner management](https://support.versal.com/hc/en-us/articles/206029467-Course-and-learner-management) for more information.</span><span class="sxs-lookup"><span data-stu-id="27efb-220">Please see [Creating a course](https://support.versal.com/hc/en-us/articles/203722528-Create-a-course), [Publishing a course](https://support.versal.com/hc/en-us/articles/203753398-Publishing-a-course), and [Course and learner management](https://support.versal.com/hc/en-us/articles/206029467-Course-and-learner-management) for more information.</span></span>  
                     

## <a name="additional-resources"></a><span data-ttu-id="27efb-221">Additional resources</span><span class="sxs-lookup"><span data-stu-id="27efb-221">Additional resources</span></span>

* [<span data-ttu-id="27efb-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="27efb-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="27efb-223">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="27efb-223">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/versal-tutorial/tutorial_general_01.png
[2]: ./media/versal-tutorial/tutorial_general_02.png
[3]: ./media/versal-tutorial/tutorial_general_03.png
[4]: ./media/versal-tutorial/tutorial_general_04.png

[100]: ./media/versal-tutorial/tutorial_general_100.png

[200]: ./media/versal-tutorial/tutorial_general_200.png
[201]: ./media/versal-tutorial/tutorial_general_201.png
[202]: ./media/versal-tutorial/tutorial_general_202.png
[203]: ./media/versal-tutorial/tutorial_general_203.png

