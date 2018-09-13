---
title: 'Tutorial: Azure Active Directory integration with Land Gorilla Client | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Land Gorilla.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: jeedes
ms.openlocfilehash: 6712ecbc81abdf4756cb72f4949f51d2ffca4142
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870894"
---
# <a name="tutorial-azure-active-directory-integration-with-land-gorilla-client"></a><span data-ttu-id="f8159-103">Tutorial: Azure Active Directory integration with Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="f8159-103">Tutorial: Azure Active Directory integration with Land Gorilla Client</span></span>

<span data-ttu-id="f8159-104">In this tutorial, you learn how to integrate Land Gorilla Client with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f8159-104">In this tutorial, you learn how to integrate Land Gorilla Client with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f8159-105">Integrating Land Gorilla Client with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f8159-105">Integrating Land Gorilla Client with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f8159-106">You can control in Azure AD who has access to Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="f8159-106">You can control in Azure AD who has access to Land Gorilla Client</span></span>
- <span data-ttu-id="f8159-107">You can enable your users to automatically get signed-on to Land Gorilla Client (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="f8159-107">You can enable your users to automatically get signed-on to Land Gorilla Client (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f8159-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="f8159-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="f8159-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="f8159-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="f8159-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f8159-110">Prerequisites</span></span>

<span data-ttu-id="f8159-111">To configure Azure AD integration with Land Gorilla Client, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f8159-111">To configure Azure AD integration with Land Gorilla Client, you need the following items:</span></span>

- <span data-ttu-id="f8159-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f8159-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f8159-113">A Land Gorilla Client single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f8159-113">A Land Gorilla Client single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="f8159-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="f8159-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="f8159-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f8159-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f8159-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="f8159-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f8159-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f8159-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="f8159-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="f8159-118">Scenario description</span></span>
<span data-ttu-id="f8159-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f8159-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f8159-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="f8159-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f8159-121">Adding Land Gorilla Client from the gallery</span><span class="sxs-lookup"><span data-stu-id="f8159-121">Adding Land Gorilla Client from the gallery</span></span>
1. <span data-ttu-id="f8159-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f8159-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-land-gorilla-client-from-the-gallery"></a><span data-ttu-id="f8159-123">Adding Land Gorilla Client from the gallery</span><span class="sxs-lookup"><span data-stu-id="f8159-123">Adding Land Gorilla Client from the gallery</span></span>
<span data-ttu-id="f8159-124">To configure the integration of Land Gorilla Client into Azure AD, you need to add Land Gorilla Client from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f8159-124">To configure the integration of Land Gorilla Client into Azure AD, you need to add Land Gorilla Client from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f8159-125">**To add Land Gorilla Client from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f8159-125">**To add Land Gorilla Client from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f8159-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f8159-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="f8159-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="f8159-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f8159-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f8159-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="f8159-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="f8159-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="f8159-133">In the search box, type **Land Gorilla Client**.</span><span class="sxs-lookup"><span data-stu-id="f8159-133">In the search box, type **Land Gorilla Client**.</span></span>

    ![Creating an Azure AD test user](./media/landgorilla-tutorial/tutorial_landgorilla_search.png)

1. <span data-ttu-id="f8159-135">In the results panel, select **Land Gorilla Client**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="f8159-135">In the results panel, select **Land Gorilla Client**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/landgorilla-tutorial/tutorial_landgorilla_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f8159-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f8159-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f8159-138">In this section, you configure and test Azure AD single sign-on with Land Gorilla Client based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f8159-138">In this section, you configure and test Azure AD single sign-on with Land Gorilla Client based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f8159-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Land Gorilla Client is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8159-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Land Gorilla Client is to a user in Azure AD.</span></span> <span data-ttu-id="f8159-140">In other words, a link relationship between an Azure AD user and the related user in Land Gorilla Client needs to be established.</span><span class="sxs-lookup"><span data-stu-id="f8159-140">In other words, a link relationship between an Azure AD user and the related user in Land Gorilla Client needs to be established.</span></span>

<span data-ttu-id="f8159-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="f8159-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Land Gorilla Client.</span></span>

<span data-ttu-id="f8159-142">To configure and test Azure AD single sign-on with Land Gorilla Client, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f8159-142">To configure and test Azure AD single sign-on with Land Gorilla Client, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f8159-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f8159-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="f8159-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with limited group.</span><span class="sxs-lookup"><span data-stu-id="f8159-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with limited group.</span></span>
1. <span data-ttu-id="f8159-145">**[Creating a Land Gorilla test user](#creating-a-land-gorilla-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f8159-145">**[Creating a Land Gorilla test user](#creating-a-land-gorilla-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="f8159-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f8159-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="f8159-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="f8159-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f8159-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f8159-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f8159-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Land Gorilla Client application.</span><span class="sxs-lookup"><span data-stu-id="f8159-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Land Gorilla Client application.</span></span>

<span data-ttu-id="f8159-150">**To configure Azure AD single sign-on with Land Gorilla Client, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f8159-150">**To configure Azure AD single sign-on with Land Gorilla Client, perform the following steps:**</span></span>

1. <span data-ttu-id="f8159-151">In the Azure Management portal, on the **Land Gorilla Client** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f8159-151">In the Azure Management portal, on the **Land Gorilla Client** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="f8159-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="f8159-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](./media/landgorilla-tutorial/tutorial_landgorilla_samlbase.png)

1. <span data-ttu-id="f8159-155">On the **Land Gorilla Client Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f8159-155">On the **Land Gorilla Client Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/landgorilla-tutorial/tutorial_landgorilla_url_02.png)

    <span data-ttu-id="f8159-157">a.</span><span class="sxs-lookup"><span data-stu-id="f8159-157">a.</span></span> <span data-ttu-id="f8159-158">In the **Identifier** textbox, type the value using one of the following pattern:</span><span class="sxs-lookup"><span data-stu-id="f8159-158">In the **Identifier** textbox, type the value using one of the following pattern:</span></span> 
    
    `https://<customer domain>.landgorilla.com/` 
    
    `https://www.<customer domain>.landgorilla.com`

    <span data-ttu-id="f8159-159">b.</span><span class="sxs-lookup"><span data-stu-id="f8159-159">b.</span></span> <span data-ttu-id="f8159-160">In the **Reply URL** textbox, type a URL using one of the following pattern:</span><span class="sxs-lookup"><span data-stu-id="f8159-160">In the **Reply URL** textbox, type a URL using one of the following pattern:</span></span>

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`
    
    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`

    > [!NOTE] 
    > <span data-ttu-id="f8159-161">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="f8159-161">Please note that these are not the real values.</span></span> <span data-ttu-id="f8159-162">You have to update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="f8159-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="f8159-163">Here we suggest you to use the unique value of string in the Identifier.</span><span class="sxs-lookup"><span data-stu-id="f8159-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="f8159-164">Contact [Land Gorilla Client team](https://www.landgorilla.com/support/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="f8159-164">Contact [Land Gorilla Client team](https://www.landgorilla.com/support/) to get these values.</span></span> 

1. <span data-ttu-id="f8159-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="f8159-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](./media/landgorilla-tutorial/tutorial_landgorilla_certificate.png) 

1. <span data-ttu-id="f8159-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="f8159-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/landgorilla-tutorial/tutorial_general_400.png) 

1. <span data-ttu-id="f8159-169">To get SSO configuration complete for your application at Land Gorilla end, Contact [Land Gorilla Client support team](https://www.landgorilla.com/support/) and provide them with the downloaded **“Metadata XML** file.</span><span class="sxs-lookup"><span data-stu-id="f8159-169">To get SSO configuration complete for your application at Land Gorilla end, Contact [Land Gorilla Client support team](https://www.landgorilla.com/support/) and provide them with the downloaded **“Metadata XML** file.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f8159-170">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f8159-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="f8159-171">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f8159-171">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="f8159-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f8159-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f8159-174">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f8159-174">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/landgorilla-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="f8159-176">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="f8159-176">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](./media/landgorilla-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="f8159-178">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="f8159-178">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/landgorilla-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="f8159-180">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f8159-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/landgorilla-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f8159-182">a.</span><span class="sxs-lookup"><span data-stu-id="f8159-182">a.</span></span> <span data-ttu-id="f8159-183">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f8159-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f8159-184">b.</span><span class="sxs-lookup"><span data-stu-id="f8159-184">b.</span></span> <span data-ttu-id="f8159-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f8159-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f8159-186">c.</span><span class="sxs-lookup"><span data-stu-id="f8159-186">c.</span></span> <span data-ttu-id="f8159-187">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="f8159-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f8159-188">d.</span><span class="sxs-lookup"><span data-stu-id="f8159-188">d.</span></span> <span data-ttu-id="f8159-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f8159-189">Click **Create**.</span></span> 

### <a name="creating-a-land-gorilla-test-user"></a><span data-ttu-id="f8159-190">Creating a Land Gorilla test user</span><span class="sxs-lookup"><span data-stu-id="f8159-190">Creating a Land Gorilla test user</span></span>

<span data-ttu-id="f8159-191">Please work with [Land Gorilla support team](https://www.landgorilla.com/support/) to add the users in the Land Gorilla platform.</span><span class="sxs-lookup"><span data-stu-id="f8159-191">Please work with [Land Gorilla support team](https://www.landgorilla.com/support/) to add the users in the Land Gorilla platform.</span></span>
    
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f8159-192">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f8159-192">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f8159-193">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Land Gorilla Client.</span><span class="sxs-lookup"><span data-stu-id="f8159-193">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Land Gorilla Client.</span></span>

![Assign User][200] 

<span data-ttu-id="f8159-195">**To assign Britta Simon to Land Gorilla Client, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f8159-195">**To assign Britta Simon to Land Gorilla Client, perform the following steps:**</span></span>

1. <span data-ttu-id="f8159-196">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f8159-196">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="f8159-198">In the applications list, select **Land Gorilla Client**.</span><span class="sxs-lookup"><span data-stu-id="f8159-198">In the applications list, select **Land Gorilla Client**.</span></span>

    ![Configure Single Sign-On](./media/landgorilla-tutorial/tutorial_landgorilla_app.png) 

1. <span data-ttu-id="f8159-200">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="f8159-200">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="f8159-202">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="f8159-202">Click **Add** button.</span></span> <span data-ttu-id="f8159-203">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f8159-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="f8159-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="f8159-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="f8159-206">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="f8159-206">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="f8159-207">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f8159-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="f8159-208">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="f8159-208">Testing single sign-on</span></span>

<span data-ttu-id="f8159-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f8159-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f8159-210">When you click the Land Gorilla Client tile in the Access Panel, you should get automatically signed-on to your Land Gorilla Client application.</span><span class="sxs-lookup"><span data-stu-id="f8159-210">When you click the Land Gorilla Client tile in the Access Panel, you should get automatically signed-on to your Land Gorilla Client application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f8159-211">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f8159-211">Additional resources</span></span>

* [<span data-ttu-id="f8159-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f8159-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="f8159-213">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f8159-213">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/landgorilla-tutorial/tutorial_general_01.png
[2]: ./media/landgorilla-tutorial/tutorial_general_02.png
[3]: ./media/landgorilla-tutorial/tutorial_general_03.png
[4]: ./media/landgorilla-tutorial/tutorial_general_04.png

[100]: ./media/landgorilla-tutorial/tutorial_general_100.png
[200]: ./media/landgorilla-tutorial/tutorial_general_200.png
[201]: ./media/landgorilla-tutorial/tutorial_general_201.png
[202]: ./media/landgorilla-tutorial/tutorial_general_202.png
[203]: ./media/landgorilla-tutorial/tutorial_general_203.png
