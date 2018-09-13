---
title: 'Tutorial: Azure Active Directory integration with 360 Online | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and 360 Online.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: cda8eba6-843f-4a09-8c55-0aaf6e593d75
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: b45906c8ca22965865bc4bce5132677113bfb6db
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865315"
---
# <a name="tutorial-azure-active-directory-integration-with-360-online"></a><span data-ttu-id="a351f-103">Tutorial: Azure Active Directory integration with 360 Online</span><span class="sxs-lookup"><span data-stu-id="a351f-103">Tutorial: Azure Active Directory integration with 360 Online</span></span>

<span data-ttu-id="a351f-104">In this tutorial, you learn how to integrate 360 Online with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a351f-104">In this tutorial, you learn how to integrate 360 Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a351f-105">Integrating 360 Online with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a351f-105">Integrating 360 Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a351f-106">You can control in Azure AD who has access to 360 Online</span><span class="sxs-lookup"><span data-stu-id="a351f-106">You can control in Azure AD who has access to 360 Online</span></span>
- <span data-ttu-id="a351f-107">You can enable your users to automatically get signed-on to 360 Online (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="a351f-107">You can enable your users to automatically get signed-on to 360 Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a351f-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a351f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a351f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a351f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a351f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a351f-110">Prerequisites</span></span>

<span data-ttu-id="a351f-111">To configure Azure AD integration with 360 Online, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a351f-111">To configure Azure AD integration with 360 Online, you need the following items:</span></span>

- <span data-ttu-id="a351f-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a351f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a351f-113">A 360 Online single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a351f-113">A 360 Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a351f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a351f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a351f-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a351f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a351f-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a351f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a351f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a351f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a351f-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a351f-118">Scenario description</span></span>
<span data-ttu-id="a351f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a351f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a351f-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a351f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a351f-121">Adding 360 Online from the gallery</span><span class="sxs-lookup"><span data-stu-id="a351f-121">Adding 360 Online from the gallery</span></span>
2. <span data-ttu-id="a351f-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a351f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-360-online-from-the-gallery"></a><span data-ttu-id="a351f-123">Adding 360 Online from the gallery</span><span class="sxs-lookup"><span data-stu-id="a351f-123">Adding 360 Online from the gallery</span></span>
<span data-ttu-id="a351f-124">To configure the integration of 360 Online into Azure AD, you need to add 360 Online from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a351f-124">To configure the integration of 360 Online into Azure AD, you need to add 360 Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a351f-125">**To add 360 Online from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a351f-125">**To add 360 Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a351f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a351f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a351f-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a351f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a351f-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a351f-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a351f-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a351f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a351f-133">In the search box, type **360 Online**.</span><span class="sxs-lookup"><span data-stu-id="a351f-133">In the search box, type **360 Online**.</span></span>

    ![Creating an Azure AD test user](./media/360online-tutorial/tutorial_360online_search.png)

5. <span data-ttu-id="a351f-135">In the results panel, select **360 Online**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a351f-135">In the results panel, select **360 Online**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/360online-tutorial/tutorial_360online_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a351f-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a351f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a351f-138">In this section, you configure and test Azure AD single sign-on with 360 Online based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a351f-138">In this section, you configure and test Azure AD single sign-on with 360 Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a351f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 360 Online is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a351f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 360 Online is to a user in Azure AD.</span></span> <span data-ttu-id="a351f-140">In other words, a link relationship between an Azure AD user and the related user in 360 Online needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a351f-140">In other words, a link relationship between an Azure AD user and the related user in 360 Online needs to be established.</span></span>

<span data-ttu-id="a351f-141">In 360 Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="a351f-141">In 360 Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a351f-142">To configure and test Azure AD single sign-on with 360 Online, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a351f-142">To configure and test Azure AD single sign-on with 360 Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a351f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a351f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a351f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a351f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a351f-145">**[Creating a 360 Online test user](#creating-a-360-online-test-user)** - to have a counterpart of Britta Simon in 360 Online that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a351f-145">**[Creating a 360 Online test user](#creating-a-360-online-test-user)** - to have a counterpart of Britta Simon in 360 Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a351f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a351f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a351f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a351f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a351f-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a351f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a351f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 360 Online application.</span><span class="sxs-lookup"><span data-stu-id="a351f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 360 Online application.</span></span>

<span data-ttu-id="a351f-150">**To configure Azure AD single sign-on with 360 Online, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a351f-150">**To configure Azure AD single sign-on with 360 Online, perform the following steps:**</span></span>

1. <span data-ttu-id="a351f-151">In the Azure portal, on the **360 Online** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a351f-151">In the Azure portal, on the **360 Online** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="a351f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a351f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/360online-tutorial/tutorial_360online_samlbase.png)

3. <span data-ttu-id="a351f-155">On the **360 Online Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a351f-155">On the **360 Online Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/360online-tutorial/tutorial_360online_url.png)

    <span data-ttu-id="a351f-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.public360online.com`</span><span class="sxs-lookup"><span data-stu-id="a351f-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.public360online.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a351f-158">The value is not real.</span><span class="sxs-lookup"><span data-stu-id="a351f-158">The value is not real.</span></span> <span data-ttu-id="a351f-159">Update the value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="a351f-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="a351f-160">Contact [360 Online Client support team](mailto:360online@software-innovation.com) to get the value.</span><span class="sxs-lookup"><span data-stu-id="a351f-160">Contact [360 Online Client support team](mailto:360online@software-innovation.com) to get the value.</span></span> 
 
4. <span data-ttu-id="a351f-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a351f-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/360online-tutorial/tutorial_360online_certificate.png) 

5. <span data-ttu-id="a351f-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a351f-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/360online-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a351f-165">To configure single sign-on on **360 Online** side, you need to send the downloaded **Metadata XML** to [360 Online support team](mailto:360online@software-innovation.com).</span><span class="sxs-lookup"><span data-stu-id="a351f-165">To configure single sign-on on **360 Online** side, you need to send the downloaded **Metadata XML** to [360 Online support team](mailto:360online@software-innovation.com).</span></span> 

> [!TIP]
> <span data-ttu-id="a351f-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="a351f-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a351f-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="a351f-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a351f-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a351f-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a351f-169">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a351f-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="a351f-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a351f-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="a351f-172">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a351f-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a351f-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a351f-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/360online-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a351f-175">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a351f-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/360online-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a351f-177">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="a351f-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/360online-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a351f-179">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a351f-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/360online-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a351f-181">a.</span><span class="sxs-lookup"><span data-stu-id="a351f-181">a.</span></span> <span data-ttu-id="a351f-182">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a351f-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a351f-183">b.</span><span class="sxs-lookup"><span data-stu-id="a351f-183">b.</span></span> <span data-ttu-id="a351f-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a351f-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a351f-185">c.</span><span class="sxs-lookup"><span data-stu-id="a351f-185">c.</span></span> <span data-ttu-id="a351f-186">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="a351f-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a351f-187">d.</span><span class="sxs-lookup"><span data-stu-id="a351f-187">d.</span></span> <span data-ttu-id="a351f-188">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a351f-188">Click **Create**.</span></span>
 
### <a name="creating-a-360-online-test-user"></a><span data-ttu-id="a351f-189">Creating a 360 Online test user</span><span class="sxs-lookup"><span data-stu-id="a351f-189">Creating a 360 Online test user</span></span>

<span data-ttu-id="a351f-190">In this section, you create a user called Britta Simon in 360 Online.</span><span class="sxs-lookup"><span data-stu-id="a351f-190">In this section, you create a user called Britta Simon in 360 Online.</span></span> <span data-ttu-id="a351f-191">you need to contact [360 Online support team](mailto:360online@software-innovation.com).</span><span class="sxs-lookup"><span data-stu-id="a351f-191">you need to contact [360 Online support team](mailto:360online@software-innovation.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a351f-192">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a351f-192">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a351f-193">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 360 Online.</span><span class="sxs-lookup"><span data-stu-id="a351f-193">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 360 Online.</span></span>

![Assign User][200] 

<span data-ttu-id="a351f-195">**To assign Britta Simon to 360 Online, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a351f-195">**To assign Britta Simon to 360 Online, perform the following steps:**</span></span>

1. <span data-ttu-id="a351f-196">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a351f-196">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="a351f-198">In the applications list, select **360 Online**.</span><span class="sxs-lookup"><span data-stu-id="a351f-198">In the applications list, select **360 Online**.</span></span>

    ![Configure Single Sign-On](./media/360online-tutorial/tutorial_360online_app.png) 

3. <span data-ttu-id="a351f-200">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a351f-200">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="a351f-202">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a351f-202">Click **Add** button.</span></span> <span data-ttu-id="a351f-203">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a351f-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="a351f-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a351f-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a351f-206">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a351f-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a351f-207">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a351f-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a351f-208">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="a351f-208">Testing single sign-on</span></span>

<span data-ttu-id="a351f-209">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a351f-209">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a351f-210">When you click the 360 Online tile in the Access Panel, you should get automatically signed-on to your 360 Online application.</span><span class="sxs-lookup"><span data-stu-id="a351f-210">When you click the 360 Online tile in the Access Panel, you should get automatically signed-on to your 360 Online application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a351f-211">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a351f-211">Additional resources</span></span>

* [<span data-ttu-id="a351f-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a351f-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a351f-213">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a351f-213">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/360online-tutorial/tutorial_general_01.png
[2]: ./media/360online-tutorial/tutorial_general_02.png
[3]: ./media/360online-tutorial/tutorial_general_03.png
[4]: ./media/360online-tutorial/tutorial_general_04.png

[100]: ./media/360online-tutorial/tutorial_general_100.png

[200]: ./media/360online-tutorial/tutorial_general_200.png
[201]: ./media/360online-tutorial/tutorial_general_201.png
[202]: ./media/360online-tutorial/tutorial_general_202.png
[203]: ./media/360online-tutorial/tutorial_general_203.png

