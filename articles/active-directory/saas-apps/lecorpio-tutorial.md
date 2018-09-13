---
title: 'Tutorial: Azure Active Directory integration with Lecorpio | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Lecorpio.
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
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 2dff30709fae08ffc17908f3ea9d1f540f5e79ed
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855777"
---
# <a name="tutorial-azure-active-directory-integration-with-lecorpio"></a><span data-ttu-id="7a071-103">Tutorial: Azure Active Directory integration with Lecorpio</span><span class="sxs-lookup"><span data-stu-id="7a071-103">Tutorial: Azure Active Directory integration with Lecorpio</span></span>

<span data-ttu-id="7a071-104">In this tutorial, you learn how to integrate Lecorpio with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7a071-104">In this tutorial, you learn how to integrate Lecorpio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7a071-105">Integrating Lecorpio with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7a071-105">Integrating Lecorpio with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7a071-106">You can control in Azure AD who has access to Lecorpio</span><span class="sxs-lookup"><span data-stu-id="7a071-106">You can control in Azure AD who has access to Lecorpio</span></span>
- <span data-ttu-id="7a071-107">You can enable your users to automatically get signed-on to Lecorpio (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="7a071-107">You can enable your users to automatically get signed-on to Lecorpio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7a071-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7a071-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7a071-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="7a071-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a071-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7a071-110">Prerequisites</span></span>

<span data-ttu-id="7a071-111">To configure Azure AD integration with Lecorpio, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7a071-111">To configure Azure AD integration with Lecorpio, you need the following items:</span></span>

- <span data-ttu-id="7a071-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7a071-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7a071-113">A Lecorpio single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7a071-113">A Lecorpio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7a071-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7a071-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7a071-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7a071-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7a071-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="7a071-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7a071-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7a071-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7a071-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7a071-118">Scenario description</span></span>
<span data-ttu-id="7a071-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7a071-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7a071-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7a071-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7a071-121">Adding Lecorpio from the gallery</span><span class="sxs-lookup"><span data-stu-id="7a071-121">Adding Lecorpio from the gallery</span></span>
1. <span data-ttu-id="7a071-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7a071-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lecorpio-from-the-gallery"></a><span data-ttu-id="7a071-123">Adding Lecorpio from the gallery</span><span class="sxs-lookup"><span data-stu-id="7a071-123">Adding Lecorpio from the gallery</span></span>
<span data-ttu-id="7a071-124">To configure the integration of Lecorpio into Azure AD, you need to add Lecorpio from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7a071-124">To configure the integration of Lecorpio into Azure AD, you need to add Lecorpio from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7a071-125">**To add Lecorpio from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7a071-125">**To add Lecorpio from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7a071-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7a071-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="7a071-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="7a071-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7a071-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7a071-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="7a071-131">Click **New application** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="7a071-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="7a071-133">In the search box, type **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="7a071-133">In the search box, type **Lecorpio**.</span></span>

    ![Creating an Azure AD test user](./media/lecorpio-tutorial/tutorial_lecorpio_search.png)

1. <span data-ttu-id="7a071-135">In the results panel, select **Lecorpio**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="7a071-135">In the results panel, select **Lecorpio**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/lecorpio-tutorial/tutorial_lecorpio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7a071-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7a071-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7a071-138">In this section, you configure and test Azure AD single sign-on with Lecorpio based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="7a071-138">In this section, you configure and test Azure AD single sign-on with Lecorpio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7a071-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lecorpio is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a071-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lecorpio is to a user in Azure AD.</span></span> <span data-ttu-id="7a071-140">In other words, a link relationship between an Azure AD user and the related user in Lecorpio needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7a071-140">In other words, a link relationship between an Azure AD user and the related user in Lecorpio needs to be established.</span></span>

<span data-ttu-id="7a071-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="7a071-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lecorpio.</span></span>

<span data-ttu-id="7a071-142">To configure and test Azure AD single sign-on with Lecorpio, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7a071-142">To configure and test Azure AD single sign-on with Lecorpio, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7a071-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7a071-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="7a071-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7a071-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="7a071-145">**[Creating a Lecorpio test user](#creating-a-lecorpio-test-user)** - to have a counterpart of Britta Simon in Lecorpio that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="7a071-145">**[Creating a Lecorpio test user](#creating-a-lecorpio-test-user)** - to have a counterpart of Britta Simon in Lecorpio that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="7a071-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7a071-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="7a071-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7a071-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7a071-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7a071-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7a071-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lecorpio application.</span><span class="sxs-lookup"><span data-stu-id="7a071-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lecorpio application.</span></span>

<span data-ttu-id="7a071-150">**To configure Azure AD single sign-on with Lecorpio, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7a071-150">**To configure Azure AD single sign-on with Lecorpio, perform the following steps:**</span></span>

1. <span data-ttu-id="7a071-151">In the Azure portal, on the **Lecorpio** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7a071-151">In the Azure portal, on the **Lecorpio** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="7a071-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7a071-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/lecorpio-tutorial/tutorial_lecorpio_samlbase.png)

1. <span data-ttu-id="7a071-155">On the **Lecorpio Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7a071-155">On the **Lecorpio Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/lecorpio-tutorial/tutorial_lecorpio_url.png)

    <span data-ttu-id="7a071-157">a.</span><span class="sxs-lookup"><span data-stu-id="7a071-157">a.</span></span> <span data-ttu-id="7a071-158">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="7a071-158">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    <span data-ttu-id="7a071-159">b.</span><span class="sxs-lookup"><span data-stu-id="7a071-159">b.</span></span> <span data-ttu-id="7a071-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="7a071-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7a071-161">These values are not the real.</span><span class="sxs-lookup"><span data-stu-id="7a071-161">These values are not the real.</span></span> <span data-ttu-id="7a071-162">Update these values with the actual Sign-on URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="7a071-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="7a071-163">Here we suggest you to use the unique value of string in the Identifier.</span><span class="sxs-lookup"><span data-stu-id="7a071-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="7a071-164">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="7a071-164">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) to get these values.</span></span> 
 
1. <span data-ttu-id="7a071-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="7a071-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/lecorpio-tutorial/tutorial_lecorpio_certificate.png) 

1. <span data-ttu-id="7a071-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="7a071-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/lecorpio-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="7a071-169">To configure single sign-on on **Lecorpio** side, you need to send the downloaded **Metadata XML** to [Lecorpio support team](mailto:info@lecorpio.com).</span><span class="sxs-lookup"><span data-stu-id="7a071-169">To configure single sign-on on **Lecorpio** side, you need to send the downloaded **Metadata XML** to [Lecorpio support team](mailto:info@lecorpio.com).</span></span>

> [!TIP]
> <span data-ttu-id="7a071-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="7a071-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7a071-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="7a071-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7a071-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7a071-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7a071-173">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7a071-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="7a071-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7a071-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="7a071-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7a071-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7a071-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7a071-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/lecorpio-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="7a071-179">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="7a071-179">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](./media/lecorpio-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="7a071-181">At the top of the dialog, click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="7a071-181">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/lecorpio-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="7a071-183">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7a071-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/lecorpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7a071-185">a.</span><span class="sxs-lookup"><span data-stu-id="7a071-185">a.</span></span> <span data-ttu-id="7a071-186">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7a071-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7a071-187">b.</span><span class="sxs-lookup"><span data-stu-id="7a071-187">b.</span></span> <span data-ttu-id="7a071-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7a071-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7a071-189">c.</span><span class="sxs-lookup"><span data-stu-id="7a071-189">c.</span></span> <span data-ttu-id="7a071-190">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="7a071-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7a071-191">d.</span><span class="sxs-lookup"><span data-stu-id="7a071-191">d.</span></span> <span data-ttu-id="7a071-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7a071-192">Click **Create**.</span></span>
 
### <a name="creating-a-lecorpio-test-user"></a><span data-ttu-id="7a071-193">Creating a Lecorpio test user</span><span class="sxs-lookup"><span data-stu-id="7a071-193">Creating a Lecorpio test user</span></span>

<span data-ttu-id="7a071-194">In this section, you create a user called Britta Simon in Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="7a071-194">In this section, you create a user called Britta Simon in Lecorpio.</span></span> 

<span data-ttu-id="7a071-195">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) to add the users in the Lecorpio application.</span><span class="sxs-lookup"><span data-stu-id="7a071-195">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) to add the users in the Lecorpio application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7a071-196">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7a071-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7a071-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="7a071-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lecorpio.</span></span>

![Assign User][200] 

<span data-ttu-id="7a071-199">**To assign Britta Simon to Lecorpio, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7a071-199">**To assign Britta Simon to Lecorpio, perform the following steps:**</span></span>

1. <span data-ttu-id="7a071-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7a071-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="7a071-202">In the applications list, select **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="7a071-202">In the applications list, select **Lecorpio**.</span></span>

    ![Configure Single Sign-On](./media/lecorpio-tutorial/tutorial_lecorpio_app.png) 

1. <span data-ttu-id="7a071-204">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="7a071-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="7a071-206">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="7a071-206">Click **Add** button.</span></span> <span data-ttu-id="7a071-207">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7a071-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="7a071-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="7a071-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="7a071-210">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="7a071-210">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="7a071-211">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7a071-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7a071-212">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="7a071-212">Testing single sign-on</span></span>

<span data-ttu-id="7a071-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7a071-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7a071-214">When you click the Lecorpio tile in the Access Panel, you should get automatically signed-on to your Lecorpio application.</span><span class="sxs-lookup"><span data-stu-id="7a071-214">When you click the Lecorpio tile in the Access Panel, you should get automatically signed-on to your Lecorpio application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7a071-215">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7a071-215">Additional resources</span></span>

* [<span data-ttu-id="7a071-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a071-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="7a071-217">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7a071-217">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/lecorpio-tutorial/tutorial_general_01.png
[2]: ./media/lecorpio-tutorial/tutorial_general_02.png
[3]: ./media/lecorpio-tutorial/tutorial_general_03.png
[4]: ./media/lecorpio-tutorial/tutorial_general_04.png

[100]: ./media/lecorpio-tutorial/tutorial_general_100.png

[200]: ./media/lecorpio-tutorial/tutorial_general_200.png
[201]: ./media/lecorpio-tutorial/tutorial_general_201.png
[202]: ./media/lecorpio-tutorial/tutorial_general_202.png
[203]: ./media/lecorpio-tutorial/tutorial_general_203.png

