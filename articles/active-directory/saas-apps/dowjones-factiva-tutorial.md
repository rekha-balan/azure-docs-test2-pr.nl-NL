---
title: 'Tutorial: Azure Active Directory integration with Dow Jones Factiva | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Dow Jones Factiva.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: b36e97e8-37a6-4096-a894-530427ee1331
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: 117ca9b5dc617ec982823e7653f67fc5e64ea003
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867715"
---
# <a name="tutorial-azure-active-directory-integration-with-dow-jones-factiva"></a><span data-ttu-id="352d1-103">Tutorial: Azure Active Directory integration with Dow Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="352d1-103">Tutorial: Azure Active Directory integration with Dow Jones Factiva</span></span>

<span data-ttu-id="352d1-104">In this tutorial, you learn how to integrate Dow Jones Factiva with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="352d1-104">In this tutorial, you learn how to integrate Dow Jones Factiva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="352d1-105">Integrating Dow Jones Factiva with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="352d1-105">Integrating Dow Jones Factiva with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="352d1-106">You can control in Azure AD who has access to Dow Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="352d1-106">You can control in Azure AD who has access to Dow Jones Factiva</span></span>
- <span data-ttu-id="352d1-107">You can enable your users to automatically get signed-on to Dow Jones Factiva (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="352d1-107">You can enable your users to automatically get signed-on to Dow Jones Factiva (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="352d1-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="352d1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="352d1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="352d1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="352d1-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="352d1-110">Prerequisites</span></span>

<span data-ttu-id="352d1-111">To configure Azure AD integration with Dow Jones Factiva, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="352d1-111">To configure Azure AD integration with Dow Jones Factiva, you need the following items:</span></span>

- <span data-ttu-id="352d1-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="352d1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="352d1-113">A Dow Jones Factiva single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="352d1-113">A Dow Jones Factiva single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="352d1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="352d1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="352d1-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="352d1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="352d1-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="352d1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="352d1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="352d1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="352d1-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="352d1-118">Scenario description</span></span>
<span data-ttu-id="352d1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="352d1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="352d1-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="352d1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="352d1-121">Adding Dow Jones Factiva from the gallery</span><span class="sxs-lookup"><span data-stu-id="352d1-121">Adding Dow Jones Factiva from the gallery</span></span>
1. <span data-ttu-id="352d1-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="352d1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dow-jones-factiva-from-the-gallery"></a><span data-ttu-id="352d1-123">Adding Dow Jones Factiva from the gallery</span><span class="sxs-lookup"><span data-stu-id="352d1-123">Adding Dow Jones Factiva from the gallery</span></span>
<span data-ttu-id="352d1-124">To configure the integration of Dow Jones Factiva into Azure AD, you need to add Dow Jones Factiva from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="352d1-124">To configure the integration of Dow Jones Factiva into Azure AD, you need to add Dow Jones Factiva from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="352d1-125">**To add Dow Jones Factiva from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="352d1-125">**To add Dow Jones Factiva from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="352d1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="352d1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="352d1-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="352d1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="352d1-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="352d1-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="352d1-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="352d1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="352d1-133">In the search box, type **Dow Jones Factiva**.</span><span class="sxs-lookup"><span data-stu-id="352d1-133">In the search box, type **Dow Jones Factiva**.</span></span>

    ![Creating an Azure AD test user](./media/dowjones-factiva-tutorial/tutorial_dowjonesfactiva_search.png)

1. <span data-ttu-id="352d1-135">In the results panel, select **Dow Jones Factiva**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="352d1-135">In the results panel, select **Dow Jones Factiva**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/dowjones-factiva-tutorial/tutorial_dowjonesfactiva_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="352d1-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="352d1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="352d1-138">In this section, you configure and test Azure AD single sign-on with Dow Jones Factiva based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="352d1-138">In this section, you configure and test Azure AD single sign-on with Dow Jones Factiva based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="352d1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Dow Jones Factiva is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="352d1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Dow Jones Factiva is to a user in Azure AD.</span></span> <span data-ttu-id="352d1-140">In other words, a link relationship between an Azure AD user and the related user in Dow Jones Factiva needs to be established.</span><span class="sxs-lookup"><span data-stu-id="352d1-140">In other words, a link relationship between an Azure AD user and the related user in Dow Jones Factiva needs to be established.</span></span>

<span data-ttu-id="352d1-141">In Dow Jones Factiva, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="352d1-141">In Dow Jones Factiva, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="352d1-142">To configure and test Azure AD single sign-on with Dow Jones Factiva, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="352d1-142">To configure and test Azure AD single sign-on with Dow Jones Factiva, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="352d1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="352d1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="352d1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="352d1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="352d1-145">**[Creating a Dow Jones Factiva test user](#creating-a-dow-jones-factiva-test-user)** - to have a counterpart of Britta Simon in Dow Jones Factiva that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="352d1-145">**[Creating a Dow Jones Factiva test user](#creating-a-dow-jones-factiva-test-user)** - to have a counterpart of Britta Simon in Dow Jones Factiva that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="352d1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="352d1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="352d1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="352d1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="352d1-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="352d1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="352d1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dow Jones Factiva application.</span><span class="sxs-lookup"><span data-stu-id="352d1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dow Jones Factiva application.</span></span>

<span data-ttu-id="352d1-150">**To configure Azure AD single sign-on with Dow Jones Factiva, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="352d1-150">**To configure Azure AD single sign-on with Dow Jones Factiva, perform the following steps:**</span></span>

1. <span data-ttu-id="352d1-151">In the Azure portal, on the **Dow Jones Factiva** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="352d1-151">In the Azure portal, on the **Dow Jones Factiva** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="352d1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="352d1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/dowjones-factiva-tutorial/tutorial_dowjonesfactiva_samlbase.png)

1. <span data-ttu-id="352d1-155">On the **Dow Jones Factiva Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span><span class="sxs-lookup"><span data-stu-id="352d1-155">On the **Dow Jones Factiva Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configure Single Sign-On](./media/dowjones-factiva-tutorial/tutorial_dowjonesfactiva_url.png)

1. <span data-ttu-id="352d1-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="352d1-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/dowjones-factiva-tutorial/tutorial_dowjonesfactiva_certificate.png) 

1. <span data-ttu-id="352d1-159">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="352d1-159">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/dowjones-factiva-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="352d1-161">To configure single sign-on on **Dow Jones Factiva** side, you need to send the downloaded **Metadata XML** to [Dow Jones Factiva support team](https://www.dowjones.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="352d1-161">To configure single sign-on on **Dow Jones Factiva** side, you need to send the downloaded **Metadata XML** to [Dow Jones Factiva support team](https://www.dowjones.com/contact/).</span></span> <span data-ttu-id="352d1-162">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="352d1-162">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="352d1-163">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="352d1-163">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="352d1-164">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="352d1-164">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="352d1-165">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="352d1-165">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="352d1-166">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="352d1-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="352d1-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="352d1-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="352d1-169">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="352d1-169">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="352d1-170">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="352d1-170">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/dowjones-factiva-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="352d1-172">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="352d1-172">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/dowjones-factiva-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="352d1-174">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="352d1-174">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/dowjones-factiva-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="352d1-176">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="352d1-176">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/dowjones-factiva-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="352d1-178">a.</span><span class="sxs-lookup"><span data-stu-id="352d1-178">a.</span></span> <span data-ttu-id="352d1-179">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="352d1-179">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="352d1-180">b.</span><span class="sxs-lookup"><span data-stu-id="352d1-180">b.</span></span> <span data-ttu-id="352d1-181">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="352d1-181">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="352d1-182">c.</span><span class="sxs-lookup"><span data-stu-id="352d1-182">c.</span></span> <span data-ttu-id="352d1-183">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="352d1-183">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="352d1-184">d.</span><span class="sxs-lookup"><span data-stu-id="352d1-184">d.</span></span> <span data-ttu-id="352d1-185">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="352d1-185">Click **Create**.</span></span>
 
### <a name="creating-a-dow-jones-factiva-test-user"></a><span data-ttu-id="352d1-186">Creating a Dow Jones Factiva test user</span><span class="sxs-lookup"><span data-stu-id="352d1-186">Creating a Dow Jones Factiva test user</span></span>

<span data-ttu-id="352d1-187">In this section, you create a user called Britta Simon in Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="352d1-187">In this section, you create a user called Britta Simon in Dow Jones Factiva.</span></span> <span data-ttu-id="352d1-188">Please work with Dow [Jones Factiva support team](https://www.dowjones.com/contact/) to add the users in the Dow Jones Factiva platform.</span><span class="sxs-lookup"><span data-stu-id="352d1-188">Please work with Dow [Jones Factiva support team](https://www.dowjones.com/contact/) to add the users in the Dow Jones Factiva platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="352d1-189">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="352d1-189">Assigning the Azure AD test user</span></span>

<span data-ttu-id="352d1-190">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="352d1-190">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dow Jones Factiva.</span></span>

![Assign User][200] 

<span data-ttu-id="352d1-192">**To assign Britta Simon to Dow Jones Factiva, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="352d1-192">**To assign Britta Simon to Dow Jones Factiva, perform the following steps:**</span></span>

1. <span data-ttu-id="352d1-193">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="352d1-193">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="352d1-195">In the applications list, select **Dow Jones Factiva**.</span><span class="sxs-lookup"><span data-stu-id="352d1-195">In the applications list, select **Dow Jones Factiva**.</span></span>

    ![Configure Single Sign-On](./media/dowjones-factiva-tutorial/tutorial_dowjonesfactiva_app.png) 

1. <span data-ttu-id="352d1-197">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="352d1-197">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="352d1-199">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="352d1-199">Click **Add** button.</span></span> <span data-ttu-id="352d1-200">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="352d1-200">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="352d1-202">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="352d1-202">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="352d1-203">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="352d1-203">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="352d1-204">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="352d1-204">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="352d1-205">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="352d1-205">Testing single sign-on</span></span>

<span data-ttu-id="352d1-206">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="352d1-206">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="352d1-207">When you click the Dow Jones Factiva tile in the Access Panel, you should get automatically signed-on to your Dow Jones Factiva application.</span><span class="sxs-lookup"><span data-stu-id="352d1-207">When you click the Dow Jones Factiva tile in the Access Panel, you should get automatically signed-on to your Dow Jones Factiva application.</span></span>
<span data-ttu-id="352d1-208">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="352d1-208">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="352d1-209">Additional resources</span><span class="sxs-lookup"><span data-stu-id="352d1-209">Additional resources</span></span>

* [<span data-ttu-id="352d1-210">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="352d1-210">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="352d1-211">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="352d1-211">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/dowjones-factiva-tutorial/tutorial_general_01.png
[2]: ./media/dowjones-factiva-tutorial/tutorial_general_02.png
[3]: ./media/dowjones-factiva-tutorial/tutorial_general_03.png
[4]: ./media/dowjones-factiva-tutorial/tutorial_general_04.png

[100]: ./media/dowjones-factiva-tutorial/tutorial_general_100.png

[200]: ./media/dowjones-factiva-tutorial/tutorial_general_200.png
[201]: ./media/dowjones-factiva-tutorial/tutorial_general_201.png
[202]: ./media/dowjones-factiva-tutorial/tutorial_general_202.png
[203]: ./media/dowjones-factiva-tutorial/tutorial_general_203.png

