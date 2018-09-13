---
title: 'Tutorial: Azure Active Directory integration with Fuze | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Fuze.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9780b4bf-1fd1-48c1-9ceb-f750225ae08a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 7a1bbe6f61a71e6fc05c9a9b626b8d1291c298ef
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548968"
---
# <a name="tutorial-azure-active-directory-integration-with-fuze"></a><span data-ttu-id="43375-103">Tutorial: Azure Active Directory integration with Fuze</span><span class="sxs-lookup"><span data-stu-id="43375-103">Tutorial: Azure Active Directory integration with Fuze</span></span>

<span data-ttu-id="43375-104">In this tutorial, you learn how to integrate Fuze with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="43375-104">In this tutorial, you learn how to integrate Fuze with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="43375-105">Integrating Fuze with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="43375-105">Integrating Fuze with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="43375-106">You can control in Azure AD who has access to Fuze</span><span class="sxs-lookup"><span data-stu-id="43375-106">You can control in Azure AD who has access to Fuze</span></span>
- <span data-ttu-id="43375-107">You can enable your users to automatically get signed-on to Fuze (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="43375-107">You can enable your users to automatically get signed-on to Fuze (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="43375-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="43375-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="43375-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="43375-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43375-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="43375-110">Prerequisites</span></span>

<span data-ttu-id="43375-111">To configure Azure AD integration with Fuze, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="43375-111">To configure Azure AD integration with Fuze, you need the following items:</span></span>

- <span data-ttu-id="43375-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="43375-112">An Azure AD subscription</span></span>
- <span data-ttu-id="43375-113">A Fuze single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="43375-113">A Fuze single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="43375-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="43375-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="43375-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="43375-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="43375-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="43375-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="43375-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="43375-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="43375-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="43375-118">Scenario description</span></span>
<span data-ttu-id="43375-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="43375-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="43375-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="43375-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="43375-121">Adding Fuze from the gallery</span><span class="sxs-lookup"><span data-stu-id="43375-121">Adding Fuze from the gallery</span></span>
2. <span data-ttu-id="43375-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="43375-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-fuze-from-the-gallery"></a><span data-ttu-id="43375-123">Adding Fuze from the gallery</span><span class="sxs-lookup"><span data-stu-id="43375-123">Adding Fuze from the gallery</span></span>
<span data-ttu-id="43375-124">To configure the integration of Fuze into Azure AD, you need to add Fuze from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="43375-124">To configure the integration of Fuze into Azure AD, you need to add Fuze from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="43375-125">**To add Fuze from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="43375-125">**To add Fuze from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="43375-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="43375-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="43375-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="43375-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="43375-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="43375-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="43375-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="43375-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="43375-133">In the search box, type **Fuze**.</span><span class="sxs-lookup"><span data-stu-id="43375-133">In the search box, type **Fuze**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuze-tutorial/tutorial_fuze_000.png)

5. <span data-ttu-id="43375-135">In the results panel, select **Fuze**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="43375-135">In the results panel, select **Fuze**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuze-tutorial/tutorial_fuze_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="43375-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="43375-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="43375-138">In this section, you configure and test Azure AD single sign-on with Fuze based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="43375-138">In this section, you configure and test Azure AD single sign-on with Fuze based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="43375-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Fuze is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43375-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Fuze is to a user in Azure AD.</span></span> <span data-ttu-id="43375-140">In other words, a link relationship between an Azure AD user and the related user in Fuze needs to be established.</span><span class="sxs-lookup"><span data-stu-id="43375-140">In other words, a link relationship between an Azure AD user and the related user in Fuze needs to be established.</span></span>

<span data-ttu-id="43375-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Fuze.</span><span class="sxs-lookup"><span data-stu-id="43375-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Fuze.</span></span>

<span data-ttu-id="43375-142">To configure and test Azure AD single sign-on with Fuze, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="43375-142">To configure and test Azure AD single sign-on with Fuze, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="43375-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="43375-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="43375-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="43375-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="43375-145">**[Creating a Fuze test user](#creating-a-fuze-test-user)** - to have a counterpart of Britta Simon in Fuze that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="43375-145">**[Creating a Fuze test user](#creating-a-fuze-test-user)** - to have a counterpart of Britta Simon in Fuze that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="43375-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="43375-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="43375-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="43375-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="43375-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="43375-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="43375-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Fuze application.</span><span class="sxs-lookup"><span data-stu-id="43375-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Fuze application.</span></span>

<span data-ttu-id="43375-150">**To configure Azure AD single sign-on with Fuze, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="43375-150">**To configure Azure AD single sign-on with Fuze, perform the following steps:**</span></span>

1. <span data-ttu-id="43375-151">In the Azure Management portal, on the **Fuze** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="43375-151">In the Azure Management portal, on the **Fuze** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="43375-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="43375-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuze-tutorial/tutorial_fuze_01.png)

3. <span data-ttu-id="43375-155">On the **Fuze Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="43375-155">On the **Fuze Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuze-tutorial/tutorial_fuze_020.png)
    
    <span data-ttu-id="43375-157">In the **Sign on URL** textbox, type the Sign-on URL as: `https://www.thinkingphones.com/jetspeed/portal/`</span><span class="sxs-lookup"><span data-stu-id="43375-157">In the **Sign on URL** textbox, type the Sign-on URL as: `https://www.thinkingphones.com/jetspeed/portal/`</span></span>

4.  <span data-ttu-id="43375-158">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="43375-158">Click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuze-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="43375-160">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the xml file on your computer.</span><span class="sxs-lookup"><span data-stu-id="43375-160">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the xml file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuze-tutorial/tutorial_fuze_05.png) 

6. <span data-ttu-id="43375-162">To configure single sign-on on **Fuze** side, you need to send the downloaded **Metadata XML** to [Fuze support team](https://www.fuze.com/support).</span><span class="sxs-lookup"><span data-stu-id="43375-162">To configure single sign-on on **Fuze** side, you need to send the downloaded **Metadata XML** to [Fuze support team](https://www.fuze.com/support).</span></span> <span data-ttu-id="43375-163">They will set this up in order to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="43375-163">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="43375-164">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="43375-164">Creating an Azure AD test user</span></span>
<span data-ttu-id="43375-165">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="43375-165">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="43375-167">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="43375-167">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="43375-168">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="43375-168">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuze-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="43375-170">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="43375-170">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuze-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="43375-172">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="43375-172">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuze-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="43375-174">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="43375-174">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuze-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="43375-176">a.</span><span class="sxs-lookup"><span data-stu-id="43375-176">a.</span></span> <span data-ttu-id="43375-177">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="43375-177">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="43375-178">b.</span><span class="sxs-lookup"><span data-stu-id="43375-178">b.</span></span> <span data-ttu-id="43375-179">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="43375-179">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="43375-180">c.</span><span class="sxs-lookup"><span data-stu-id="43375-180">c.</span></span> <span data-ttu-id="43375-181">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="43375-181">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="43375-182">d.</span><span class="sxs-lookup"><span data-stu-id="43375-182">d.</span></span> <span data-ttu-id="43375-183">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="43375-183">Click **Create**.</span></span> 


### <a name="creating-a-fuze-test-user"></a><span data-ttu-id="43375-184">Creating a Fuze test user</span><span class="sxs-lookup"><span data-stu-id="43375-184">Creating a Fuze test user</span></span>

<span data-ttu-id="43375-185">Fuze application supports full Just in time user provision, so users will get created automatically when they sign-in.</span><span class="sxs-lookup"><span data-stu-id="43375-185">Fuze application supports full Just in time user provision, so users will get created automatically when they sign-in.</span></span> <span data-ttu-id="43375-186">For any other clarification, please contact Fuze [support](https://www.fuze.com/support).</span><span class="sxs-lookup"><span data-stu-id="43375-186">For any other clarification, please contact Fuze [support](https://www.fuze.com/support).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="43375-187">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="43375-187">Assigning the Azure AD test user</span></span>

<span data-ttu-id="43375-188">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Fuze.</span><span class="sxs-lookup"><span data-stu-id="43375-188">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Fuze.</span></span>

![Assign User][200] 

<span data-ttu-id="43375-190">**To assign Britta Simon to Fuze, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="43375-190">**To assign Britta Simon to Fuze, perform the following steps:**</span></span>

1. <span data-ttu-id="43375-191">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="43375-191">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="43375-193">In the applications list, select **Fuze**.</span><span class="sxs-lookup"><span data-stu-id="43375-193">In the applications list, select **Fuze**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuze-tutorial/tutorial_fuze_50.png) 

3. <span data-ttu-id="43375-195">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="43375-195">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="43375-197">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="43375-197">Click **Add** button.</span></span> <span data-ttu-id="43375-198">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="43375-198">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="43375-200">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="43375-200">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="43375-201">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="43375-201">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="43375-202">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="43375-202">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="testing-single-sign-on"></a><span data-ttu-id="43375-203">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="43375-203">Testing single sign-on</span></span>

<span data-ttu-id="43375-204">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="43375-204">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="43375-205">When you click the Fuze tile in the Access Panel, you should get automatically signed-on to your Fuze application.</span><span class="sxs-lookup"><span data-stu-id="43375-205">When you click the Fuze tile in the Access Panel, you should get automatically signed-on to your Fuze application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="43375-206">Additional resources</span><span class="sxs-lookup"><span data-stu-id="43375-206">Additional resources</span></span>

* [<span data-ttu-id="43375-207">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="43375-207">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="43375-208">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="43375-208">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuze-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuze-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuze-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuze-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuze-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuze-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuze-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuze-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-fuze-tutorial/tutorial_general_203.png



















