---
title: 'Tutorial: Azure Active Directory integration with Aravo | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Aravo.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 224939d8-2c9c-4561-968d-62722f5ab5ed
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: f9ada220a82a2cf9347f02960eeef9c211f37c67
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871034"
---
# <a name="tutorial-azure-active-directory-integration-with-aravo"></a><span data-ttu-id="17611-103">Tutorial: Azure Active Directory integration with Aravo</span><span class="sxs-lookup"><span data-stu-id="17611-103">Tutorial: Azure Active Directory integration with Aravo</span></span>

<span data-ttu-id="17611-104">In this tutorial, you learn how to integrate Aravo with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="17611-104">In this tutorial, you learn how to integrate Aravo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="17611-105">Integrating Aravo with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="17611-105">Integrating Aravo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="17611-106">You can control in Azure AD who has access to Aravo</span><span class="sxs-lookup"><span data-stu-id="17611-106">You can control in Azure AD who has access to Aravo</span></span>
- <span data-ttu-id="17611-107">You can enable your users to automatically get signed-on to Aravo (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="17611-107">You can enable your users to automatically get signed-on to Aravo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="17611-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="17611-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="17611-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="17611-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17611-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="17611-110">Prerequisites</span></span>

<span data-ttu-id="17611-111">To configure Azure AD integration with Aravo, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="17611-111">To configure Azure AD integration with Aravo, you need the following items:</span></span>

- <span data-ttu-id="17611-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="17611-112">An Azure AD subscription</span></span>
- <span data-ttu-id="17611-113">An Aravo single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="17611-113">An Aravo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17611-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="17611-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="17611-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="17611-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="17611-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="17611-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="17611-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17611-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="17611-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="17611-118">Scenario description</span></span>
<span data-ttu-id="17611-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="17611-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="17611-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="17611-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="17611-121">Adding Aravo from the gallery</span><span class="sxs-lookup"><span data-stu-id="17611-121">Adding Aravo from the gallery</span></span>
2. <span data-ttu-id="17611-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="17611-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aravo-from-the-gallery"></a><span data-ttu-id="17611-123">Adding Aravo from the gallery</span><span class="sxs-lookup"><span data-stu-id="17611-123">Adding Aravo from the gallery</span></span>
<span data-ttu-id="17611-124">To configure the integration of Aravo into Azure AD, you need to add Aravo from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="17611-124">To configure the integration of Aravo into Azure AD, you need to add Aravo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="17611-125">**To add Aravo from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="17611-125">**To add Aravo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="17611-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="17611-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="17611-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="17611-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="17611-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="17611-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="17611-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="17611-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="17611-133">In the search box, type **Aravo**.</span><span class="sxs-lookup"><span data-stu-id="17611-133">In the search box, type **Aravo**.</span></span>

    ![Creating an Azure AD test user](./media/aravo-tutorial/tutorial_aravo_search.png)

5. <span data-ttu-id="17611-135">In the results panel, select **Aravo**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="17611-135">In the results panel, select **Aravo**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/aravo-tutorial/tutorial_aravo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="17611-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="17611-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="17611-138">In this section, you configure and test Azure AD single sign-on with Aravo based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="17611-138">In this section, you configure and test Azure AD single sign-on with Aravo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="17611-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Aravo is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17611-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Aravo is to a user in Azure AD.</span></span> <span data-ttu-id="17611-140">In other words, a link relationship between an Azure AD user and the related user in Aravo needs to be established.</span><span class="sxs-lookup"><span data-stu-id="17611-140">In other words, a link relationship between an Azure AD user and the related user in Aravo needs to be established.</span></span>

<span data-ttu-id="17611-141">In Aravo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="17611-141">In Aravo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="17611-142">To configure and test Azure AD single sign-on with Aravo, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="17611-142">To configure and test Azure AD single sign-on with Aravo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="17611-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="17611-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="17611-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17611-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="17611-145">**[Creating an Aravo test user](#creating-an-aravo-test-user)** - to have a counterpart of Britta Simon in Aravo that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="17611-145">**[Creating an Aravo test user](#creating-an-aravo-test-user)** - to have a counterpart of Britta Simon in Aravo that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="17611-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="17611-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="17611-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="17611-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="17611-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="17611-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="17611-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Aravo application.</span><span class="sxs-lookup"><span data-stu-id="17611-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Aravo application.</span></span>

<span data-ttu-id="17611-150">**To configure Azure AD single sign-on with Aravo, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="17611-150">**To configure Azure AD single sign-on with Aravo, perform the following steps:**</span></span>

1. <span data-ttu-id="17611-151">In the Azure portal, on the **Aravo** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="17611-151">In the Azure portal, on the **Aravo** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="17611-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="17611-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/aravo-tutorial/tutorial_aravo_samlbase.png)

3. <span data-ttu-id="17611-155">On the **Aravo Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="17611-155">On the **Aravo Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/aravo-tutorial/tutorial_aravo_url.png)

    <span data-ttu-id="17611-157">a.</span><span class="sxs-lookup"><span data-stu-id="17611-157">a.</span></span> <span data-ttu-id="17611-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.aravo.com`</span><span class="sxs-lookup"><span data-stu-id="17611-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.aravo.com`</span></span>

    <span data-ttu-id="17611-159">b.</span><span class="sxs-lookup"><span data-stu-id="17611-159">b.</span></span> <span data-ttu-id="17611-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.aravo.com/aems/login.do`</span><span class="sxs-lookup"><span data-stu-id="17611-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.aravo.com/aems/login.do`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="17611-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="17611-161">These values are not real.</span></span> <span data-ttu-id="17611-162">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="17611-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="17611-163">Contact [Aravo support team](http://www.aravo.com/about-us/contact/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="17611-163">Contact [Aravo support team](http://www.aravo.com/about-us/contact/) to get these values.</span></span>
 
4. <span data-ttu-id="17611-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="17611-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/aravo-tutorial/tutorial_aravo_certificate.png) 

5. <span data-ttu-id="17611-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="17611-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/aravo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="17611-168">On the **Aravo Configuration** section, click **Configure Aravo** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="17611-168">On the **Aravo Configuration** section, click **Configure Aravo** to open **Configure sign-on** window.</span></span> <span data-ttu-id="17611-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="17611-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/aravo-tutorial/tutorial_aravo_configure.png) 

7. <span data-ttu-id="17611-171">To configure single sign-on on **Aravo** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Aravo support team](http://www.aravo.com/about-us/contact/).</span><span class="sxs-lookup"><span data-stu-id="17611-171">To configure single sign-on on **Aravo** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Aravo support team](http://www.aravo.com/about-us/contact/).</span></span> 


> [!TIP]
> <span data-ttu-id="17611-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="17611-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="17611-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="17611-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="17611-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="17611-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="17611-175">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="17611-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="17611-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17611-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="17611-178">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="17611-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="17611-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="17611-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/aravo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="17611-181">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="17611-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/aravo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="17611-183">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="17611-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/aravo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="17611-185">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="17611-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/aravo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="17611-187">a.</span><span class="sxs-lookup"><span data-stu-id="17611-187">a.</span></span> <span data-ttu-id="17611-188">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="17611-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="17611-189">b.</span><span class="sxs-lookup"><span data-stu-id="17611-189">b.</span></span> <span data-ttu-id="17611-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="17611-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="17611-191">c.</span><span class="sxs-lookup"><span data-stu-id="17611-191">c.</span></span> <span data-ttu-id="17611-192">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="17611-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="17611-193">d.</span><span class="sxs-lookup"><span data-stu-id="17611-193">d.</span></span> <span data-ttu-id="17611-194">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="17611-194">Click **Create**.</span></span>
 
### <a name="creating-an-aravo-test-user"></a><span data-ttu-id="17611-195">Creating an Aravo test user</span><span class="sxs-lookup"><span data-stu-id="17611-195">Creating an Aravo test user</span></span>

<span data-ttu-id="17611-196">The objective of this section is to create a user called Britta Simon in Aravo.</span><span class="sxs-lookup"><span data-stu-id="17611-196">The objective of this section is to create a user called Britta Simon in Aravo.</span></span> <span data-ttu-id="17611-197">Work with [Aravo support team](http://www.aravo.com/about-us/contact/) to add the users in the Aravo account.</span><span class="sxs-lookup"><span data-stu-id="17611-197">Work with [Aravo support team](http://www.aravo.com/about-us/contact/) to add the users in the Aravo account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="17611-198">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="17611-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="17611-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Aravo.</span><span class="sxs-lookup"><span data-stu-id="17611-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Aravo.</span></span>

![Assign User][200] 

<span data-ttu-id="17611-201">**To assign Britta Simon to Aravo, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="17611-201">**To assign Britta Simon to Aravo, perform the following steps:**</span></span>

1. <span data-ttu-id="17611-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="17611-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="17611-204">In the applications list, select **Aravo**.</span><span class="sxs-lookup"><span data-stu-id="17611-204">In the applications list, select **Aravo**.</span></span>

    ![Configure Single Sign-On](./media/aravo-tutorial/tutorial_aravo_app.png) 

3. <span data-ttu-id="17611-206">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="17611-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="17611-208">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="17611-208">Click **Add** button.</span></span> <span data-ttu-id="17611-209">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="17611-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="17611-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="17611-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="17611-212">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="17611-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="17611-213">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="17611-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="17611-214">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="17611-214">Testing single sign-on</span></span>

<span data-ttu-id="17611-215">The objective of this section is to test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="17611-215">The objective of this section is to test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.</span></span>

<span data-ttu-id="17611-216">When you click the Aravo tile in the Access Panel, you should get automatically signed-on to your Aravo application.</span><span class="sxs-lookup"><span data-stu-id="17611-216">When you click the Aravo tile in the Access Panel, you should get automatically signed-on to your Aravo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="17611-217">Additional resources</span><span class="sxs-lookup"><span data-stu-id="17611-217">Additional resources</span></span>

* [<span data-ttu-id="17611-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17611-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="17611-219">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="17611-219">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/aravo-tutorial/tutorial_general_01.png
[2]: ./media/aravo-tutorial/tutorial_general_02.png
[3]: ./media/aravo-tutorial/tutorial_general_03.png
[4]: ./media/aravo-tutorial/tutorial_general_04.png

[100]: ./media/aravo-tutorial/tutorial_general_100.png

[200]: ./media/aravo-tutorial/tutorial_general_200.png
[201]: ./media/aravo-tutorial/tutorial_general_201.png
[202]: ./media/aravo-tutorial/tutorial_general_202.png
[203]: ./media/aravo-tutorial/tutorial_general_203.png

