---
title: 'Tutorial: Azure Active Directory integration with IriusRisk | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and IriusRisk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d2c854d5-101d-4d67-80e0-87749e1a0352
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2017
ms.author: jeedes
ms.openlocfilehash: b7e026d9a27edeec3c48bbc9360992f80099230d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864434"
---
# <a name="tutorial-azure-active-directory-integration-with-iriusrisk"></a><span data-ttu-id="87feb-103">Tutorial: Azure Active Directory integration with IriusRisk</span><span class="sxs-lookup"><span data-stu-id="87feb-103">Tutorial: Azure Active Directory integration with IriusRisk</span></span>

<span data-ttu-id="87feb-104">In this tutorial, you learn how to integrate IriusRisk with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="87feb-104">In this tutorial, you learn how to integrate IriusRisk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="87feb-105">Integrating IriusRisk with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="87feb-105">Integrating IriusRisk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="87feb-106">You can control in Azure AD who has access to IriusRisk.</span><span class="sxs-lookup"><span data-stu-id="87feb-106">You can control in Azure AD who has access to IriusRisk.</span></span>
- <span data-ttu-id="87feb-107">You can enable your users to automatically get signed-on to IriusRisk (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="87feb-107">You can enable your users to automatically get signed-on to IriusRisk (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="87feb-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="87feb-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="87feb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="87feb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87feb-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="87feb-110">Prerequisites</span></span>

<span data-ttu-id="87feb-111">To configure Azure AD integration with IriusRisk, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="87feb-111">To configure Azure AD integration with IriusRisk, you need the following items:</span></span>

- <span data-ttu-id="87feb-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="87feb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="87feb-113">A IriusRisk single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="87feb-113">A IriusRisk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="87feb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="87feb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="87feb-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="87feb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="87feb-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="87feb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="87feb-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="87feb-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="87feb-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="87feb-118">Scenario description</span></span>
<span data-ttu-id="87feb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="87feb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="87feb-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="87feb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="87feb-121">Adding IriusRisk from the gallery</span><span class="sxs-lookup"><span data-stu-id="87feb-121">Adding IriusRisk from the gallery</span></span>
1. <span data-ttu-id="87feb-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="87feb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-iriusrisk-from-the-gallery"></a><span data-ttu-id="87feb-123">Adding IriusRisk from the gallery</span><span class="sxs-lookup"><span data-stu-id="87feb-123">Adding IriusRisk from the gallery</span></span>
<span data-ttu-id="87feb-124">To configure the integration of IriusRisk into Azure AD, you need to add IriusRisk from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="87feb-124">To configure the integration of IriusRisk into Azure AD, you need to add IriusRisk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="87feb-125">**To add IriusRisk from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="87feb-125">**To add IriusRisk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="87feb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="87feb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="87feb-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="87feb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="87feb-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="87feb-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="87feb-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="87feb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="87feb-133">In the search box, type **IriusRisk**, select **IriusRisk** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="87feb-133">In the search box, type **IriusRisk**, select **IriusRisk** from result panel then click **Add** button to add the application.</span></span>

    ![IriusRisk in the results list](./media/iriusrisk-tutorial/tutorial_iriusrisk_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="87feb-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="87feb-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="87feb-136">In this section, you configure and test Azure AD single sign-on with IriusRisk based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="87feb-136">In this section, you configure and test Azure AD single sign-on with IriusRisk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="87feb-137">For single sign-on to work, Azure AD needs to know what the counterpart user in IriusRisk is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87feb-137">For single sign-on to work, Azure AD needs to know what the counterpart user in IriusRisk is to a user in Azure AD.</span></span> <span data-ttu-id="87feb-138">In other words, a link relationship between an Azure AD user and the related user in IriusRisk needs to be established.</span><span class="sxs-lookup"><span data-stu-id="87feb-138">In other words, a link relationship between an Azure AD user and the related user in IriusRisk needs to be established.</span></span>

<span data-ttu-id="87feb-139">In IriusRisk, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="87feb-139">In IriusRisk, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="87feb-140">To configure and test Azure AD single sign-on with IriusRisk, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="87feb-140">To configure and test Azure AD single sign-on with IriusRisk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="87feb-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="87feb-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="87feb-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="87feb-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="87feb-143">**[Create a IriusRisk test user](#create-a-iriusrisk-test-user)** - to have a counterpart of Britta Simon in IriusRisk that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="87feb-143">**[Create a IriusRisk test user](#create-a-iriusrisk-test-user)** - to have a counterpart of Britta Simon in IriusRisk that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="87feb-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="87feb-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="87feb-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="87feb-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="87feb-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="87feb-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="87feb-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your IriusRisk application.</span><span class="sxs-lookup"><span data-stu-id="87feb-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your IriusRisk application.</span></span>

<span data-ttu-id="87feb-148">**To configure Azure AD single sign-on with IriusRisk, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="87feb-148">**To configure Azure AD single sign-on with IriusRisk, perform the following steps:**</span></span>

1. <span data-ttu-id="87feb-149">In the Azure portal, on the **IriusRisk** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="87feb-149">In the Azure portal, on the **IriusRisk** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="87feb-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="87feb-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/iriusrisk-tutorial/tutorial_iriusrisk_samlbase.png)

1. <span data-ttu-id="87feb-153">On the **IriusRisk Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="87feb-153">On the **IriusRisk Domain and URLs** section, perform the following steps:</span></span>

    ![IriusRisk Domain and URLs single sign-on information](./media/iriusrisk-tutorial/tutorial_iriusrisk_url.png)

    <span data-ttu-id="87feb-155">a.</span><span class="sxs-lookup"><span data-stu-id="87feb-155">a.</span></span> <span data-ttu-id="87feb-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.iriusrisk.com/ui#!login`</span><span class="sxs-lookup"><span data-stu-id="87feb-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.iriusrisk.com/ui#!login`</span></span>

    <span data-ttu-id="87feb-157">b.</span><span class="sxs-lookup"><span data-stu-id="87feb-157">b.</span></span> <span data-ttu-id="87feb-158">In the **Identifier** textbox, type the value: `iriusrisk-sp`</span><span class="sxs-lookup"><span data-stu-id="87feb-158">In the **Identifier** textbox, type the value: `iriusrisk-sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="87feb-159">The Sign-on URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="87feb-159">The Sign-on URL value is not real.</span></span> <span data-ttu-id="87feb-160">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="87feb-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="87feb-161">Contact [IriusRisk Client support team](mailto:info@continuumsecurity.net) to get this value.</span><span class="sxs-lookup"><span data-stu-id="87feb-161">Contact [IriusRisk Client support team](mailto:info@continuumsecurity.net) to get this value.</span></span> 

1. <span data-ttu-id="87feb-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="87feb-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/iriusrisk-tutorial/tutorial_iriusrisk_certificate.png) 

1. <span data-ttu-id="87feb-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="87feb-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/iriusrisk-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="87feb-166">To configure single sign-on on **IriusRisk** side, you need to send the downloaded **Metadata XML** to [IriusRisk support team](mailto:info@continuumsecurity.net).</span><span class="sxs-lookup"><span data-stu-id="87feb-166">To configure single sign-on on **IriusRisk** side, you need to send the downloaded **Metadata XML** to [IriusRisk support team](mailto:info@continuumsecurity.net).</span></span> <span data-ttu-id="87feb-167">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="87feb-167">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="87feb-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="87feb-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="87feb-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="87feb-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="87feb-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="87feb-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="87feb-171">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="87feb-171">Create an Azure AD test user</span></span>

<span data-ttu-id="87feb-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="87feb-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="87feb-174">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="87feb-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="87feb-175">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="87feb-175">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/iriusrisk-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="87feb-177">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="87feb-177">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/iriusrisk-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="87feb-179">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="87feb-179">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/iriusrisk-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="87feb-181">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="87feb-181">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/iriusrisk-tutorial/create_aaduser_04.png)

    <span data-ttu-id="87feb-183">a.</span><span class="sxs-lookup"><span data-stu-id="87feb-183">a.</span></span> <span data-ttu-id="87feb-184">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="87feb-184">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="87feb-185">b.</span><span class="sxs-lookup"><span data-stu-id="87feb-185">b.</span></span> <span data-ttu-id="87feb-186">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="87feb-186">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="87feb-187">c.</span><span class="sxs-lookup"><span data-stu-id="87feb-187">c.</span></span> <span data-ttu-id="87feb-188">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="87feb-188">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="87feb-189">d.</span><span class="sxs-lookup"><span data-stu-id="87feb-189">d.</span></span> <span data-ttu-id="87feb-190">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="87feb-190">Click **Create**.</span></span>
 
### <a name="create-a-iriusrisk-test-user"></a><span data-ttu-id="87feb-191">Create a IriusRisk test user</span><span class="sxs-lookup"><span data-stu-id="87feb-191">Create a IriusRisk test user</span></span>

<span data-ttu-id="87feb-192">The objective of this section is to create a user called Britta Simon in IriusRisk.</span><span class="sxs-lookup"><span data-stu-id="87feb-192">The objective of this section is to create a user called Britta Simon in IriusRisk.</span></span> <span data-ttu-id="87feb-193">IriusRisk supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="87feb-193">IriusRisk supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="87feb-194">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="87feb-194">There is no action item for you in this section.</span></span> <span data-ttu-id="87feb-195">A new user is created during an attempt to access IriusRisk if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="87feb-195">A new user is created during an attempt to access IriusRisk if it doesn't exist yet.</span></span>

> [!Note]
> <span data-ttu-id="87feb-196">If you need to create a user manually, contact [IriusRisk support team](mailto:info@continuumsecurity.net).</span><span class="sxs-lookup"><span data-stu-id="87feb-196">If you need to create a user manually, contact [IriusRisk support team](mailto:info@continuumsecurity.net).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="87feb-197">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="87feb-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="87feb-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to IriusRisk.</span><span class="sxs-lookup"><span data-stu-id="87feb-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to IriusRisk.</span></span>

![Assign the user role][200] 

<span data-ttu-id="87feb-200">**To assign Britta Simon to IriusRisk, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="87feb-200">**To assign Britta Simon to IriusRisk, perform the following steps:**</span></span>

1. <span data-ttu-id="87feb-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="87feb-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="87feb-203">In the applications list, select **IriusRisk**.</span><span class="sxs-lookup"><span data-stu-id="87feb-203">In the applications list, select **IriusRisk**.</span></span>

    ![The IriusRisk link in the Applications list](./media/iriusrisk-tutorial/tutorial_iriusrisk_app.png)  

1. <span data-ttu-id="87feb-205">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="87feb-205">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="87feb-207">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="87feb-207">Click **Add** button.</span></span> <span data-ttu-id="87feb-208">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="87feb-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="87feb-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="87feb-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="87feb-211">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="87feb-211">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="87feb-212">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="87feb-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="87feb-213">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="87feb-213">Test single sign-on</span></span>

<span data-ttu-id="87feb-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="87feb-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="87feb-215">When you click the IriusRisk tile in the Access Panel, you should get automatically signed-on to your IriusRisk application.</span><span class="sxs-lookup"><span data-stu-id="87feb-215">When you click the IriusRisk tile in the Access Panel, you should get automatically signed-on to your IriusRisk application.</span></span>
<span data-ttu-id="87feb-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="87feb-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="87feb-217">Additional resources</span><span class="sxs-lookup"><span data-stu-id="87feb-217">Additional resources</span></span>

* [<span data-ttu-id="87feb-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="87feb-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="87feb-219">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="87feb-219">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/iriusrisk-tutorial/tutorial_general_01.png
[2]: ./media/iriusrisk-tutorial/tutorial_general_02.png
[3]: ./media/iriusrisk-tutorial/tutorial_general_03.png
[4]: ./media/iriusrisk-tutorial/tutorial_general_04.png

[100]: ./media/iriusrisk-tutorial/tutorial_general_100.png

[200]: ./media/iriusrisk-tutorial/tutorial_general_200.png
[201]: ./media/iriusrisk-tutorial/tutorial_general_201.png
[202]: ./media/iriusrisk-tutorial/tutorial_general_202.png
[203]: ./media/iriusrisk-tutorial/tutorial_general_203.png

