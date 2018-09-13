---
title: 'Tutorial: Azure Active Directory integration with Moxi Engage | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Moxi Engage.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 1135a879-8f00-43b0-ac8a-831593d9586d
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jeedes
ms.openlocfilehash: 200382578d7cf2cce96b9cb73097bce632c88767
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869603"
---
# <a name="tutorial-azure-active-directory-integration-with-moxi-engage"></a><span data-ttu-id="61146-103">Tutorial: Azure Active Directory integration with Moxi Engage</span><span class="sxs-lookup"><span data-stu-id="61146-103">Tutorial: Azure Active Directory integration with Moxi Engage</span></span>

<span data-ttu-id="61146-104">In this tutorial, you learn how to integrate Moxi Engage with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="61146-104">In this tutorial, you learn how to integrate Moxi Engage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="61146-105">Integrating Moxi Engage with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="61146-105">Integrating Moxi Engage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="61146-106">You can control in Azure AD who has access to Moxi Engage</span><span class="sxs-lookup"><span data-stu-id="61146-106">You can control in Azure AD who has access to Moxi Engage</span></span>
- <span data-ttu-id="61146-107">You can enable your users to automatically get signed-on to Moxi Engage (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="61146-107">You can enable your users to automatically get signed-on to Moxi Engage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="61146-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="61146-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="61146-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="61146-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61146-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="61146-110">Prerequisites</span></span>

<span data-ttu-id="61146-111">To configure Azure AD integration with Moxi Engage, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="61146-111">To configure Azure AD integration with Moxi Engage, you need the following items:</span></span>

- <span data-ttu-id="61146-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="61146-112">An Azure AD subscription</span></span>
- <span data-ttu-id="61146-113">A Moxi Engage single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="61146-113">A Moxi Engage single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="61146-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="61146-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="61146-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="61146-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="61146-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="61146-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="61146-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="61146-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="61146-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="61146-118">Scenario description</span></span>
<span data-ttu-id="61146-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="61146-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="61146-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="61146-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="61146-121">Adding Moxi Engage from the gallery</span><span class="sxs-lookup"><span data-stu-id="61146-121">Adding Moxi Engage from the gallery</span></span>
1. <span data-ttu-id="61146-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="61146-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxi-engage-from-the-gallery"></a><span data-ttu-id="61146-123">Adding Moxi Engage from the gallery</span><span class="sxs-lookup"><span data-stu-id="61146-123">Adding Moxi Engage from the gallery</span></span>
<span data-ttu-id="61146-124">To configure the integration of Moxi Engage into Azure AD, you need to add Moxi Engage from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="61146-124">To configure the integration of Moxi Engage into Azure AD, you need to add Moxi Engage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="61146-125">**To add Moxi Engage from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61146-125">**To add Moxi Engage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="61146-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="61146-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="61146-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="61146-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="61146-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="61146-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="61146-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="61146-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="61146-133">In the search box, type **Moxi Engage**.</span><span class="sxs-lookup"><span data-stu-id="61146-133">In the search box, type **Moxi Engage**.</span></span>

    ![Creating an Azure AD test user](./media/moxiengage-tutorial/tutorial_moxiengage_search.png)

1. <span data-ttu-id="61146-135">In the results panel, select **Moxi Engage**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="61146-135">In the results panel, select **Moxi Engage**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/moxiengage-tutorial/tutorial_moxiengage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="61146-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="61146-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="61146-138">In this section, you configure and test Azure AD single sign-on with Moxi Engage based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="61146-138">In this section, you configure and test Azure AD single sign-on with Moxi Engage based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="61146-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Moxi Engage is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61146-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Moxi Engage is to a user in Azure AD.</span></span> <span data-ttu-id="61146-140">In other words, a link relationship between an Azure AD user and the related user in Moxi Engage needs to be established.</span><span class="sxs-lookup"><span data-stu-id="61146-140">In other words, a link relationship between an Azure AD user and the related user in Moxi Engage needs to be established.</span></span>

<span data-ttu-id="61146-141">In Moxi Engage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="61146-141">In Moxi Engage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="61146-142">To configure and test Azure AD single sign-on with Moxi Engage, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="61146-142">To configure and test Azure AD single sign-on with Moxi Engage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="61146-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="61146-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="61146-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="61146-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="61146-145">**[Creating a Moxi Engage test user](#creating-a-moxi-engage-test-user)** - to have a counterpart of Britta Simon in Moxi Engage that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="61146-145">**[Creating a Moxi Engage test user](#creating-a-moxi-engage-test-user)** - to have a counterpart of Britta Simon in Moxi Engage that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="61146-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="61146-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="61146-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="61146-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="61146-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="61146-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="61146-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Moxi Engage application.</span><span class="sxs-lookup"><span data-stu-id="61146-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Moxi Engage application.</span></span>

<span data-ttu-id="61146-150">**To configure Azure AD single sign-on with Moxi Engage, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61146-150">**To configure Azure AD single sign-on with Moxi Engage, perform the following steps:**</span></span>

1. <span data-ttu-id="61146-151">In the Azure portal, on the **Moxi Engage** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="61146-151">In the Azure portal, on the **Moxi Engage** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="61146-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="61146-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/moxiengage-tutorial/tutorial_moxiengage_samlbase.png)

1. <span data-ttu-id="61146-155">On the **Moxi Engage Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="61146-155">On the **Moxi Engage Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/moxiengage-tutorial/tutorial_moxiengage_url.png)

    <span data-ttu-id="61146-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://svc.<moxiworks-integration-domain>/service/v1/auth/inbound/saml/aad`</span><span class="sxs-lookup"><span data-stu-id="61146-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://svc.<moxiworks-integration-domain>/service/v1/auth/inbound/saml/aad`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="61146-158">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="61146-158">This value is not real.</span></span> <span data-ttu-id="61146-159">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="61146-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="61146-160">Contact [Moxi Engage Client support team](mailto:support@moxiworks.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="61146-160">Contact [Moxi Engage Client support team](mailto:support@moxiworks.com) to get this value.</span></span> 
 
1. <span data-ttu-id="61146-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="61146-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/moxiengage-tutorial/tutorial_moxiengage_certificate.png) 

1. <span data-ttu-id="61146-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="61146-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/moxiengage-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="61146-165">To configure single sign-on on **Moxi Engage** side, you need to send the downloaded **Metadata XML** to [Moxi Engage support team](mailto:support@moxiworks.com).</span><span class="sxs-lookup"><span data-stu-id="61146-165">To configure single sign-on on **Moxi Engage** side, you need to send the downloaded **Metadata XML** to [Moxi Engage support team](mailto:support@moxiworks.com).</span></span> <span data-ttu-id="61146-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="61146-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="61146-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="61146-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="61146-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="61146-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="61146-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="61146-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="61146-170">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="61146-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="61146-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="61146-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="61146-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61146-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="61146-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="61146-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/moxiengage-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="61146-176">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="61146-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/moxiengage-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="61146-178">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="61146-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/moxiengage-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="61146-180">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="61146-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/moxiengage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="61146-182">a.</span><span class="sxs-lookup"><span data-stu-id="61146-182">a.</span></span> <span data-ttu-id="61146-183">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="61146-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="61146-184">b.</span><span class="sxs-lookup"><span data-stu-id="61146-184">b.</span></span> <span data-ttu-id="61146-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="61146-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="61146-186">c.</span><span class="sxs-lookup"><span data-stu-id="61146-186">c.</span></span> <span data-ttu-id="61146-187">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="61146-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="61146-188">d.</span><span class="sxs-lookup"><span data-stu-id="61146-188">d.</span></span> <span data-ttu-id="61146-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="61146-189">Click **Create**.</span></span>
 
### <a name="creating-a-moxi-engage-test-user"></a><span data-ttu-id="61146-190">Creating a Moxi Engage test user</span><span class="sxs-lookup"><span data-stu-id="61146-190">Creating a Moxi Engage test user</span></span>

<span data-ttu-id="61146-191">In this section, you create a user called Britta Simon in Moxi Engage.</span><span class="sxs-lookup"><span data-stu-id="61146-191">In this section, you create a user called Britta Simon in Moxi Engage.</span></span> <span data-ttu-id="61146-192">Work with [Moxi Engage support team](mailto:support@moxiworks.com) to add the users in the Moxi Engage platform.</span><span class="sxs-lookup"><span data-stu-id="61146-192">Work with [Moxi Engage support team](mailto:support@moxiworks.com) to add the users in the Moxi Engage platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="61146-193">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="61146-193">Assigning the Azure AD test user</span></span>

<span data-ttu-id="61146-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Moxi Engage.</span><span class="sxs-lookup"><span data-stu-id="61146-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Moxi Engage.</span></span>

![Assign User][200] 

<span data-ttu-id="61146-196">**To assign Britta Simon to Moxi Engage, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61146-196">**To assign Britta Simon to Moxi Engage, perform the following steps:**</span></span>

1. <span data-ttu-id="61146-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="61146-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="61146-199">In the applications list, select **Moxi Engage**.</span><span class="sxs-lookup"><span data-stu-id="61146-199">In the applications list, select **Moxi Engage**.</span></span>

    ![Configure Single Sign-On](./media/moxiengage-tutorial/tutorial_moxiengage_app.png) 

1. <span data-ttu-id="61146-201">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="61146-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="61146-203">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="61146-203">Click **Add** button.</span></span> <span data-ttu-id="61146-204">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="61146-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="61146-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="61146-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="61146-207">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="61146-207">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="61146-208">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="61146-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="61146-209">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="61146-209">Testing single sign-on</span></span>

<span data-ttu-id="61146-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="61146-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="61146-211">When you click the Moxi Engage tile in the Access Panel, you should get automatic login to Moxi Engage application.</span><span class="sxs-lookup"><span data-stu-id="61146-211">When you click the Moxi Engage tile in the Access Panel, you should get automatic login to Moxi Engage application.</span></span>
<span data-ttu-id="61146-212">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="61146-212">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="61146-213">Additional resources</span><span class="sxs-lookup"><span data-stu-id="61146-213">Additional resources</span></span>

* [<span data-ttu-id="61146-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="61146-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="61146-215">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="61146-215">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/moxiengage-tutorial/tutorial_general_01.png
[2]: ./media/moxiengage-tutorial/tutorial_general_02.png
[3]: ./media/moxiengage-tutorial/tutorial_general_03.png
[4]: ./media/moxiengage-tutorial/tutorial_general_04.png

[100]: ./media/moxiengage-tutorial/tutorial_general_100.png

[200]: ./media/moxiengage-tutorial/tutorial_general_200.png
[201]: ./media/moxiengage-tutorial/tutorial_general_201.png
[202]: ./media/moxiengage-tutorial/tutorial_general_202.png
[203]: ./media/moxiengage-tutorial/tutorial_general_203.png

