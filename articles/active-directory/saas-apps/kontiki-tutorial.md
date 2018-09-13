---
title: 'Tutorial: Azure Active Directory integration with Kontiki | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Kontiki.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 8d5e5413-da4c-40d8-b1d0-f03ecfef030b
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: e5f29a12de5f82fa13c0c61462db00b2906fdca7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856315"
---
# <a name="tutorial-azure-active-directory-integration-with-kontiki"></a><span data-ttu-id="48e14-103">Tutorial: Azure Active Directory integration with Kontiki</span><span class="sxs-lookup"><span data-stu-id="48e14-103">Tutorial: Azure Active Directory integration with Kontiki</span></span>

<span data-ttu-id="48e14-104">In this tutorial, you learn how to integrate Kontiki with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="48e14-104">In this tutorial, you learn how to integrate Kontiki with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="48e14-105">Integrating Kontiki with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="48e14-105">Integrating Kontiki with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="48e14-106">You can control in Azure AD who has access to Kontiki</span><span class="sxs-lookup"><span data-stu-id="48e14-106">You can control in Azure AD who has access to Kontiki</span></span>
- <span data-ttu-id="48e14-107">You can enable your users to automatically get signed-on to Kontiki (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="48e14-107">You can enable your users to automatically get signed-on to Kontiki (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="48e14-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="48e14-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="48e14-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="48e14-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48e14-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="48e14-110">Prerequisites</span></span>

<span data-ttu-id="48e14-111">To configure Azure AD integration with Kontiki, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="48e14-111">To configure Azure AD integration with Kontiki, you need the following items:</span></span>

- <span data-ttu-id="48e14-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="48e14-112">An Azure AD subscription</span></span>
- <span data-ttu-id="48e14-113">A Kontiki single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="48e14-113">A Kontiki single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="48e14-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="48e14-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="48e14-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="48e14-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="48e14-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="48e14-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="48e14-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48e14-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="48e14-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="48e14-118">Scenario description</span></span>
<span data-ttu-id="48e14-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="48e14-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="48e14-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="48e14-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="48e14-121">Adding Kontiki from the gallery</span><span class="sxs-lookup"><span data-stu-id="48e14-121">Adding Kontiki from the gallery</span></span>
1. <span data-ttu-id="48e14-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="48e14-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kontiki-from-the-gallery"></a><span data-ttu-id="48e14-123">Adding Kontiki from the gallery</span><span class="sxs-lookup"><span data-stu-id="48e14-123">Adding Kontiki from the gallery</span></span>
<span data-ttu-id="48e14-124">To configure the integration of Kontiki into Azure AD, you need to add Kontiki from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="48e14-124">To configure the integration of Kontiki into Azure AD, you need to add Kontiki from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="48e14-125">**To add Kontiki from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="48e14-125">**To add Kontiki from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="48e14-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="48e14-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="48e14-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="48e14-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="48e14-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="48e14-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="48e14-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="48e14-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="48e14-133">In the search box, type **Kontiki**.</span><span class="sxs-lookup"><span data-stu-id="48e14-133">In the search box, type **Kontiki**.</span></span>

    ![Creating an Azure AD test user](./media/kontiki-tutorial/tutorial_kontiki_search.png)

1. <span data-ttu-id="48e14-135">In the results panel, select **Kontiki**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="48e14-135">In the results panel, select **Kontiki**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/kontiki-tutorial/tutorial_kontiki_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="48e14-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="48e14-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="48e14-138">In this section, you configure and test Azure AD single sign-on with Kontiki based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="48e14-138">In this section, you configure and test Azure AD single sign-on with Kontiki based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="48e14-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kontiki is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48e14-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kontiki is to a user in Azure AD.</span></span> <span data-ttu-id="48e14-140">In other words, a link relationship between an Azure AD user and the related user in Kontiki needs to be established.</span><span class="sxs-lookup"><span data-stu-id="48e14-140">In other words, a link relationship between an Azure AD user and the related user in Kontiki needs to be established.</span></span>

<span data-ttu-id="48e14-141">In Kontiki, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="48e14-141">In Kontiki, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="48e14-142">To configure and test Azure AD single sign-on with Kontiki, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="48e14-142">To configure and test Azure AD single sign-on with Kontiki, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="48e14-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="48e14-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="48e14-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48e14-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="48e14-145">**[Creating a Kontiki test user](#creating-a-kontiki-test-user)** - to have a counterpart of Britta Simon in Kontiki that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="48e14-145">**[Creating a Kontiki test user](#creating-a-kontiki-test-user)** - to have a counterpart of Britta Simon in Kontiki that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="48e14-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="48e14-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="48e14-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="48e14-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="48e14-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="48e14-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="48e14-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kontiki application.</span><span class="sxs-lookup"><span data-stu-id="48e14-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kontiki application.</span></span>

<span data-ttu-id="48e14-150">**To configure Azure AD single sign-on with Kontiki, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="48e14-150">**To configure Azure AD single sign-on with Kontiki, perform the following steps:**</span></span>

1. <span data-ttu-id="48e14-151">In the Azure portal, on the **Kontiki** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="48e14-151">In the Azure portal, on the **Kontiki** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="48e14-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="48e14-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/kontiki-tutorial/tutorial_kontiki_samlbase.png)

1. <span data-ttu-id="48e14-155">On the **Kontiki Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="48e14-155">On the **Kontiki Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/kontiki-tutorial/tutorial_kontiki_url.png)

     <span data-ttu-id="48e14-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.mc.eval.kontiki.com`</span><span class="sxs-lookup"><span data-stu-id="48e14-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.mc.eval.kontiki.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="48e14-158">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="48e14-158">This value is not real.</span></span> <span data-ttu-id="48e14-159">Update the value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="48e14-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="48e14-160">Contact [Kontiki Client support team](http://customersupport.kontiki.com/enterprise/contactsupport.html) to get the value.</span><span class="sxs-lookup"><span data-stu-id="48e14-160">Contact [Kontiki Client support team](http://customersupport.kontiki.com/enterprise/contactsupport.html) to get the value.</span></span> 
 
1. <span data-ttu-id="48e14-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="48e14-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/kontiki-tutorial/tutorial_kontiki_certificate.png) 

1. <span data-ttu-id="48e14-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="48e14-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/kontiki-tutorial/tutorial_general_400.png) 

1. <span data-ttu-id="48e14-165">To configure single sign-on on **Kontiki** side, you need to send the downloaded **Metadata XML** to [Kontiki support team](http://customersupport.kontiki.com/enterprise/contactsupport.html).</span><span class="sxs-lookup"><span data-stu-id="48e14-165">To configure single sign-on on **Kontiki** side, you need to send the downloaded **Metadata XML** to [Kontiki support team](http://customersupport.kontiki.com/enterprise/contactsupport.html).</span></span> <span data-ttu-id="48e14-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="48e14-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="48e14-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="48e14-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="48e14-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="48e14-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="48e14-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="48e14-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="48e14-170">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="48e14-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="48e14-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48e14-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="48e14-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="48e14-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="48e14-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="48e14-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/kontiki-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="48e14-176">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="48e14-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/kontiki-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="48e14-178">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="48e14-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/kontiki-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="48e14-180">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="48e14-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/kontiki-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="48e14-182">a.</span><span class="sxs-lookup"><span data-stu-id="48e14-182">a.</span></span> <span data-ttu-id="48e14-183">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="48e14-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="48e14-184">b.</span><span class="sxs-lookup"><span data-stu-id="48e14-184">b.</span></span> <span data-ttu-id="48e14-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="48e14-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="48e14-186">c.</span><span class="sxs-lookup"><span data-stu-id="48e14-186">c.</span></span> <span data-ttu-id="48e14-187">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="48e14-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="48e14-188">d.</span><span class="sxs-lookup"><span data-stu-id="48e14-188">d.</span></span> <span data-ttu-id="48e14-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="48e14-189">Click **Create**.</span></span>
 
### <a name="creating-a-kontiki-test-user"></a><span data-ttu-id="48e14-190">Creating a Kontiki test user</span><span class="sxs-lookup"><span data-stu-id="48e14-190">Creating a Kontiki test user</span></span>

<span data-ttu-id="48e14-191">There is no action item for you to configure user provisioning to Kontiki.</span><span class="sxs-lookup"><span data-stu-id="48e14-191">There is no action item for you to configure user provisioning to Kontiki.</span></span> <span data-ttu-id="48e14-192">When an assigned user tries to log in to Kontiki using the access panel, Kontiki checks whether the user exists.</span><span class="sxs-lookup"><span data-stu-id="48e14-192">When an assigned user tries to log in to Kontiki using the access panel, Kontiki checks whether the user exists.</span></span>  

>[!NOTE]
><span data-ttu-id="48e14-193">If there is no user account available yet, it is automatically created by Kontiki.</span><span class="sxs-lookup"><span data-stu-id="48e14-193">If there is no user account available yet, it is automatically created by Kontiki.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="48e14-194">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="48e14-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="48e14-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kontiki.</span><span class="sxs-lookup"><span data-stu-id="48e14-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kontiki.</span></span>

![Assign User][200] 

<span data-ttu-id="48e14-197">**To assign Britta Simon to Kontiki, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="48e14-197">**To assign Britta Simon to Kontiki, perform the following steps:**</span></span>

1. <span data-ttu-id="48e14-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="48e14-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="48e14-200">In the applications list, select **Kontiki**.</span><span class="sxs-lookup"><span data-stu-id="48e14-200">In the applications list, select **Kontiki**.</span></span>

    ![Configure Single Sign-On](./media/kontiki-tutorial/tutorial_kontiki_app.png) 

1. <span data-ttu-id="48e14-202">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="48e14-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="48e14-204">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="48e14-204">Click **Add** button.</span></span> <span data-ttu-id="48e14-205">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="48e14-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="48e14-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="48e14-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="48e14-208">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="48e14-208">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="48e14-209">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="48e14-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="48e14-210">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="48e14-210">Testing single sign-on</span></span>

<span data-ttu-id="48e14-211">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="48e14-211">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="48e14-212">When you click the Kontiki tile in the Access Panel, you should get automatically signed-on to your Kontiki application.</span><span class="sxs-lookup"><span data-stu-id="48e14-212">When you click the Kontiki tile in the Access Panel, you should get automatically signed-on to your Kontiki application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="48e14-213">Additional resources</span><span class="sxs-lookup"><span data-stu-id="48e14-213">Additional resources</span></span>

* [<span data-ttu-id="48e14-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48e14-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="48e14-215">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="48e14-215">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/kontiki-tutorial/tutorial_general_01.png
[2]: ./media/kontiki-tutorial/tutorial_general_02.png
[3]: ./media/kontiki-tutorial/tutorial_general_03.png
[4]: ./media/kontiki-tutorial/tutorial_general_04.png

[100]: ./media/kontiki-tutorial/tutorial_general_100.png

[200]: ./media/kontiki-tutorial/tutorial_general_200.png
[201]: ./media/kontiki-tutorial/tutorial_general_201.png
[202]: ./media/kontiki-tutorial/tutorial_general_202.png
[203]: ./media/kontiki-tutorial/tutorial_general_203.png

