---
title: 'Tutorial: Azure Active Directory integration with Intralinks | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Intralinks.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 44cae95cfd01f8d6fbd6ddb4a11e9af290042ffa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867644"
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a><span data-ttu-id="a7cee-103">Tutorial: Azure Active Directory integration with Intralinks</span><span class="sxs-lookup"><span data-stu-id="a7cee-103">Tutorial: Azure Active Directory integration with Intralinks</span></span>

<span data-ttu-id="a7cee-104">In this tutorial, you learn how to integrate Intralinks with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a7cee-104">In this tutorial, you learn how to integrate Intralinks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a7cee-105">Integrating Intralinks with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a7cee-105">Integrating Intralinks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a7cee-106">You can control in Azure AD who has access to Intralinks</span><span class="sxs-lookup"><span data-stu-id="a7cee-106">You can control in Azure AD who has access to Intralinks</span></span>
- <span data-ttu-id="a7cee-107">You can enable your users to automatically get signed-on to Intralinks (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="a7cee-107">You can enable your users to automatically get signed-on to Intralinks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a7cee-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a7cee-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a7cee-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a7cee-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7cee-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a7cee-110">Prerequisites</span></span>

<span data-ttu-id="a7cee-111">To configure Azure AD integration with Intralinks, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a7cee-111">To configure Azure AD integration with Intralinks, you need the following items:</span></span>

- <span data-ttu-id="a7cee-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a7cee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a7cee-113">An Intralinks single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a7cee-113">An Intralinks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a7cee-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a7cee-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a7cee-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a7cee-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a7cee-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a7cee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a7cee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a7cee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a7cee-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a7cee-118">Scenario description</span></span>
<span data-ttu-id="a7cee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a7cee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a7cee-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a7cee-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a7cee-121">Adding Intralinks from the gallery</span><span class="sxs-lookup"><span data-stu-id="a7cee-121">Adding Intralinks from the gallery</span></span>
1. <span data-ttu-id="a7cee-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a7cee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intralinks-from-the-gallery"></a><span data-ttu-id="a7cee-123">Adding Intralinks from the gallery</span><span class="sxs-lookup"><span data-stu-id="a7cee-123">Adding Intralinks from the gallery</span></span>
<span data-ttu-id="a7cee-124">To configure the integration of Intralinks into Azure AD, you need to add Intralinks from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a7cee-124">To configure the integration of Intralinks into Azure AD, you need to add Intralinks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a7cee-125">**To add Intralinks from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a7cee-125">**To add Intralinks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a7cee-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a7cee-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="a7cee-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a7cee-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a7cee-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a7cee-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="a7cee-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a7cee-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="a7cee-133">In the search box, type **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="a7cee-133">In the search box, type **Intralinks**.</span></span>

    ![Creating an Azure AD test user](./media/intralinks-tutorial/tutorial_intralinks_search.png)

1. <span data-ttu-id="a7cee-135">In the results panel, select **Intralinks**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a7cee-135">In the results panel, select **Intralinks**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a7cee-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a7cee-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a7cee-138">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a7cee-138">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a7cee-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Intralinks is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7cee-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Intralinks is to a user in Azure AD.</span></span> <span data-ttu-id="a7cee-140">In other words, a link relationship between an Azure AD user and the related user in Intralinks needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a7cee-140">In other words, a link relationship between an Azure AD user and the related user in Intralinks needs to be established.</span></span>

<span data-ttu-id="a7cee-141">In Intralinks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="a7cee-141">In Intralinks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a7cee-142">To configure and test Azure AD single sign-on with Intralinks, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a7cee-142">To configure and test Azure AD single sign-on with Intralinks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a7cee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a7cee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="a7cee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7cee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="a7cee-145">**[Creating an Intralinks test user](#creating-an-intralinks-test-user)** - to have a counterpart of Britta Simon in Intralinks that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a7cee-145">**[Creating an Intralinks test user](#creating-an-intralinks-test-user)** - to have a counterpart of Britta Simon in Intralinks that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="a7cee-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a7cee-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="a7cee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a7cee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a7cee-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a7cee-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a7cee-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Intralinks application.</span><span class="sxs-lookup"><span data-stu-id="a7cee-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Intralinks application.</span></span>

<span data-ttu-id="a7cee-150">**To configure Azure AD single sign-on with Intralinks, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a7cee-150">**To configure Azure AD single sign-on with Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="a7cee-151">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a7cee-151">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="a7cee-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a7cee-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/intralinks-tutorial/tutorial_intralinks_samlbase.png)

1. <span data-ttu-id="a7cee-155">On the **Intralinks Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a7cee-155">On the **Intralinks Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/intralinks-tutorial/tutorial_intralinks_url.png)

    <span data-ttu-id="a7cee-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span><span class="sxs-lookup"><span data-stu-id="a7cee-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a7cee-158">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="a7cee-158">This value is not real.</span></span> <span data-ttu-id="a7cee-159">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="a7cee-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="a7cee-160">Contact [Intralinks Client support team](https://www.intralinks.com/contact) to get this value.</span><span class="sxs-lookup"><span data-stu-id="a7cee-160">Contact [Intralinks Client support team](https://www.intralinks.com/contact) to get this value.</span></span> 
 
1. <span data-ttu-id="a7cee-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a7cee-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/intralinks-tutorial/tutorial_intralinks_certificate.png) 

1. <span data-ttu-id="a7cee-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a7cee-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/intralinks-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="a7cee-165">To configure single sign-on on **Intralinks** side, you need to send the downloaded **Metadata XML** [Intralinks support team](https://www.intralinks.com/contact).</span><span class="sxs-lookup"><span data-stu-id="a7cee-165">To configure single sign-on on **Intralinks** side, you need to send the downloaded **Metadata XML** [Intralinks support team](https://www.intralinks.com/contact).</span></span> <span data-ttu-id="a7cee-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="a7cee-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a7cee-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="a7cee-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a7cee-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="a7cee-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a7cee-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a7cee-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a7cee-170">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a7cee-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="a7cee-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7cee-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="a7cee-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a7cee-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a7cee-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a7cee-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/intralinks-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="a7cee-176">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a7cee-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/intralinks-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="a7cee-178">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="a7cee-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/intralinks-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="a7cee-180">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a7cee-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/intralinks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a7cee-182">a.</span><span class="sxs-lookup"><span data-stu-id="a7cee-182">a.</span></span> <span data-ttu-id="a7cee-183">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a7cee-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a7cee-184">b.</span><span class="sxs-lookup"><span data-stu-id="a7cee-184">b.</span></span> <span data-ttu-id="a7cee-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a7cee-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a7cee-186">c.</span><span class="sxs-lookup"><span data-stu-id="a7cee-186">c.</span></span> <span data-ttu-id="a7cee-187">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="a7cee-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a7cee-188">d.</span><span class="sxs-lookup"><span data-stu-id="a7cee-188">d.</span></span> <span data-ttu-id="a7cee-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a7cee-189">Click **Create**.</span></span>
 
### <a name="creating-an-intralinks-test-user"></a><span data-ttu-id="a7cee-190">Creating an Intralinks test user</span><span class="sxs-lookup"><span data-stu-id="a7cee-190">Creating an Intralinks test user</span></span>

<span data-ttu-id="a7cee-191">In this section, you create a user called Britta Simon in Intralinks.</span><span class="sxs-lookup"><span data-stu-id="a7cee-191">In this section, you create a user called Britta Simon in Intralinks.</span></span> <span data-ttu-id="a7cee-192">Please work with [Intralinks support team](https://www.intralinks.com/contact) to add the users in the Intralinks platform.</span><span class="sxs-lookup"><span data-stu-id="a7cee-192">Please work with [Intralinks support team](https://www.intralinks.com/contact) to add the users in the Intralinks platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a7cee-193">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a7cee-193">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a7cee-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Intralinks.</span><span class="sxs-lookup"><span data-stu-id="a7cee-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Intralinks.</span></span>

![Assign User][200] 

<span data-ttu-id="a7cee-196">**To assign Britta Simon to Intralinks, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a7cee-196">**To assign Britta Simon to Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="a7cee-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a7cee-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="a7cee-199">In the applications list, select **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="a7cee-199">In the applications list, select **Intralinks**.</span></span>

    ![Configure Single Sign-On](./media/intralinks-tutorial/tutorial_intralinks_app.png) 

1. <span data-ttu-id="a7cee-201">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a7cee-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="a7cee-203">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a7cee-203">Click **Add** button.</span></span> <span data-ttu-id="a7cee-204">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a7cee-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="a7cee-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a7cee-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="a7cee-207">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a7cee-207">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="a7cee-208">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a7cee-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="add-intralinks-via-or-elite-application"></a><span data-ttu-id="a7cee-209">Add Intralinks VIA or Elite application</span><span class="sxs-lookup"><span data-stu-id="a7cee-209">Add Intralinks VIA or Elite application</span></span>

<span data-ttu-id="a7cee-210">Intralinks uses the same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span><span class="sxs-lookup"><span data-stu-id="a7cee-210">Intralinks uses the same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span></span> <span data-ttu-id="a7cee-211">So if you plan to use any other Intralinks application then first you have to configure SSO for one Primary Intralinks application using the procedure described above.</span><span class="sxs-lookup"><span data-stu-id="a7cee-211">So if you plan to use any other Intralinks application then first you have to configure SSO for one Primary Intralinks application using the procedure described above.</span></span>

<span data-ttu-id="a7cee-212">After that you can follow the below procedure to add another Intralinks application in your tenant which can leverage this primary application for SSO.</span><span class="sxs-lookup"><span data-stu-id="a7cee-212">After that you can follow the below procedure to add another Intralinks application in your tenant which can leverage this primary application for SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="a7cee-213">This feature is available only to Azure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span><span class="sxs-lookup"><span data-stu-id="a7cee-213">This feature is available only to Azure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span></span>

1. <span data-ttu-id="a7cee-214">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a7cee-214">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]


1. <span data-ttu-id="a7cee-216">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a7cee-216">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a7cee-217">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a7cee-217">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="a7cee-219">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a7cee-219">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="a7cee-221">In the search box, type **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="a7cee-221">In the search box, type **Intralinks**.</span></span>

    ![Creating an Azure AD test user](./media/intralinks-tutorial/tutorial_intralinks_search.png)

1. <span data-ttu-id="a7cee-223">On **Intralinks Add app** perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a7cee-223">On **Intralinks Add app** perform the following steps:</span></span>

    ![Adding Intralinks VIA or Elite application](./media/intralinks-tutorial/tutorial_intralinks_addapp.png)

    <span data-ttu-id="a7cee-225">a.</span><span class="sxs-lookup"><span data-stu-id="a7cee-225">a.</span></span> <span data-ttu-id="a7cee-226">In **Name** textbox, enter appropriate name of the application e.g. **Intralinks Elite**.</span><span class="sxs-lookup"><span data-stu-id="a7cee-226">In **Name** textbox, enter appropriate name of the application e.g. **Intralinks Elite**.</span></span>

    <span data-ttu-id="a7cee-227">b.</span><span class="sxs-lookup"><span data-stu-id="a7cee-227">b.</span></span> <span data-ttu-id="a7cee-228">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a7cee-228">Click **Add** button.</span></span>

1.  <span data-ttu-id="a7cee-229">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a7cee-229">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="a7cee-231">On the **Single sign-on** dialog, select **Mode** as **Linked Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a7cee-231">On the **Single sign-on** dialog, select **Mode** as **Linked Sign-on**.</span></span>
 
    ![Configure Single Sign-On](./media/intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

1. <span data-ttu-id="a7cee-233">Get the SP Initiated SSO URL from [Intralinks team](https://www.intralinks.com/contact) for the other Intralinks application and enter it in **Configure Sign-on URL** as shown below.</span><span class="sxs-lookup"><span data-stu-id="a7cee-233">Get the SP Initiated SSO URL from [Intralinks team](https://www.intralinks.com/contact) for the other Intralinks application and enter it in **Configure Sign-on URL** as shown below.</span></span> 
    
     ![Configure Single Sign-On](./media/intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     <span data-ttu-id="a7cee-235">In the Sign On URL textbox, type the URL used by your users to sign-on to your Intralinks application using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="a7cee-235">In the Sign On URL textbox, type the URL used by your users to sign-on to your Intralinks application using the following pattern:</span></span>
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

1. <span data-ttu-id="a7cee-236">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a7cee-236">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/intralinks-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="a7cee-238">Assign the application to user or groups as shown in the section **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)**.</span><span class="sxs-lookup"><span data-stu-id="a7cee-238">Assign the application to user or groups as shown in the section **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)**.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="a7cee-239">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="a7cee-239">Testing single sign-on</span></span>

<span data-ttu-id="a7cee-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a7cee-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a7cee-241">When you click the Intralinks tile in the Access Panel, you should get automatically signed-on to your Intralinks application.</span><span class="sxs-lookup"><span data-stu-id="a7cee-241">When you click the Intralinks tile in the Access Panel, you should get automatically signed-on to your Intralinks application.</span></span>
<span data-ttu-id="a7cee-242">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a7cee-242">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a7cee-243">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a7cee-243">Additional resources</span></span>

* [<span data-ttu-id="a7cee-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7cee-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a7cee-245">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a7cee-245">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)


<!--Image references-->

[1]: ./media/intralinks-tutorial/tutorial_general_01.png
[2]: ./media/intralinks-tutorial/tutorial_general_02.png
[3]: ./media/intralinks-tutorial/tutorial_general_03.png
[4]: ./media/intralinks-tutorial/tutorial_general_04.png

[100]: ./media/intralinks-tutorial/tutorial_general_100.png

[200]: ./media/intralinks-tutorial/tutorial_general_200.png
[201]: ./media/intralinks-tutorial/tutorial_general_201.png
[202]: ./media/intralinks-tutorial/tutorial_general_202.png
[203]: ./media/intralinks-tutorial/tutorial_general_203.png

