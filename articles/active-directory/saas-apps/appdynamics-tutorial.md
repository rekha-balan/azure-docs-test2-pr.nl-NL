---
title: 'Tutorial: Azure Active Directory integration with AppDynamics | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and AppDynamics.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/09/2018
ms.author: jeedes
ms.openlocfilehash: 3600e83d18f8cabd03c46af2ef47445c588cbdb5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864776"
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a><span data-ttu-id="55fef-103">Tutorial: Azure Active Directory integration with AppDynamics</span><span class="sxs-lookup"><span data-stu-id="55fef-103">Tutorial: Azure Active Directory integration with AppDynamics</span></span>

<span data-ttu-id="55fef-104">In this tutorial, you learn how to integrate AppDynamics with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="55fef-104">In this tutorial, you learn how to integrate AppDynamics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="55fef-105">Integrating AppDynamics with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="55fef-105">Integrating AppDynamics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="55fef-106">You can control in Azure AD who has access to AppDynamics</span><span class="sxs-lookup"><span data-stu-id="55fef-106">You can control in Azure AD who has access to AppDynamics</span></span>
- <span data-ttu-id="55fef-107">You can enable your users to automatically get signed-on to AppDynamics (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="55fef-107">You can enable your users to automatically get signed-on to AppDynamics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="55fef-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="55fef-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="55fef-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="55fef-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55fef-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="55fef-110">Prerequisites</span></span>

<span data-ttu-id="55fef-111">To configure Azure AD integration with AppDynamics, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="55fef-111">To configure Azure AD integration with AppDynamics, you need the following items:</span></span>

- <span data-ttu-id="55fef-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="55fef-112">An Azure AD subscription</span></span>
- <span data-ttu-id="55fef-113">An AppDynamics single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="55fef-113">An AppDynamics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="55fef-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="55fef-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="55fef-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="55fef-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="55fef-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="55fef-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="55fef-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="55fef-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="55fef-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="55fef-118">Scenario description</span></span>
<span data-ttu-id="55fef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="55fef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>
<span data-ttu-id="55fef-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="55fef-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="55fef-121">Adding AppDynamics from the gallery</span><span class="sxs-lookup"><span data-stu-id="55fef-121">Adding AppDynamics from the gallery</span></span>
2. <span data-ttu-id="55fef-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="55fef-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appdynamics-from-the-gallery"></a><span data-ttu-id="55fef-123">Adding AppDynamics from the gallery</span><span class="sxs-lookup"><span data-stu-id="55fef-123">Adding AppDynamics from the gallery</span></span>
<span data-ttu-id="55fef-124">To configure the integration of AppDynamics into Azure AD, you need to add AppDynamics from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="55fef-124">To configure the integration of AppDynamics into Azure AD, you need to add AppDynamics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="55fef-125">**To add AppDynamics from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="55fef-125">**To add AppDynamics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="55fef-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="55fef-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="55fef-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="55fef-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="55fef-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="55fef-129">Then go to **All applications**.</span></span>

    ![Applications][2]

3. <span data-ttu-id="55fef-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="55fef-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="55fef-133">In the search box, type **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="55fef-133">In the search box, type **AppDynamics**.</span></span>

    ![Creating an Azure AD test user](./media/appdynamics-tutorial/tutorial_appdynamics_search.png)

5. <span data-ttu-id="55fef-135">In the results panel, select **AppDynamics**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="55fef-135">In the results panel, select **AppDynamics**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/appdynamics-tutorial/tutorial_appdynamics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="55fef-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="55fef-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="55fef-138">In this section, you configure and test Azure AD single sign-on with AppDynamics based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="55fef-138">In this section, you configure and test Azure AD single sign-on with AppDynamics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="55fef-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AppDynamics is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55fef-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AppDynamics is to a user in Azure AD.</span></span> <span data-ttu-id="55fef-140">In other words, a link relationship between an Azure AD user and the related user in AppDynamics needs to be established.</span><span class="sxs-lookup"><span data-stu-id="55fef-140">In other words, a link relationship between an Azure AD user and the related user in AppDynamics needs to be established.</span></span>

<span data-ttu-id="55fef-141">In AppDynamics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="55fef-141">In AppDynamics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="55fef-142">To configure and test Azure AD single sign-on with AppDynamics, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="55fef-142">To configure and test Azure AD single sign-on with AppDynamics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="55fef-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="55fef-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="55fef-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="55fef-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="55fef-145">**[Creating an AppDynamics test user](#creating-an-appdynamics-test-user)** - to have a counterpart of Britta Simon in AppDynamics that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="55fef-145">**[Creating an AppDynamics test user](#creating-an-appdynamics-test-user)** - to have a counterpart of Britta Simon in AppDynamics that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="55fef-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="55fef-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="55fef-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="55fef-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="55fef-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="55fef-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="55fef-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AppDynamics application.</span><span class="sxs-lookup"><span data-stu-id="55fef-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AppDynamics application.</span></span>

<span data-ttu-id="55fef-150">**To configure Azure AD single sign-on with AppDynamics, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="55fef-150">**To configure Azure AD single sign-on with AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="55fef-151">In the Azure portal, on the **AppDynamics** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="55fef-151">In the Azure portal, on the **AppDynamics** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="55fef-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="55fef-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configure Single Sign-On](./media/appdynamics-tutorial/tutorial_appdynamics_samlbase.png)

3. <span data-ttu-id="55fef-155">On the **AppDynamics Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="55fef-155">On the **AppDynamics Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/appdynamics-tutorial/tutorial_appdynamics_url.png)

    <span data-ttu-id="55fef-157">a.</span><span class="sxs-lookup"><span data-stu-id="55fef-157">a.</span></span> <span data-ttu-id="55fef-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com`</span><span class="sxs-lookup"><span data-stu-id="55fef-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com`</span></span>

    <span data-ttu-id="55fef-159">b.</span><span class="sxs-lookup"><span data-stu-id="55fef-159">b.</span></span> <span data-ttu-id="55fef-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com/controller`</span><span class="sxs-lookup"><span data-stu-id="55fef-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com/controller`</span></span>

    > [!NOTE]
    > <span data-ttu-id="55fef-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="55fef-161">These values are not real.</span></span> <span data-ttu-id="55fef-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="55fef-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="55fef-163">Contact [AppDynamics Client support team](https://www.appdynamics.com/support/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="55fef-163">Contact [AppDynamics Client support team](https://www.appdynamics.com/support/) to get these values.</span></span>

4. <span data-ttu-id="55fef-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="55fef-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/appdynamics-tutorial/tutorial_appdynamics_certificate.png)

5. <span data-ttu-id="55fef-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="55fef-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/appdynamics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="55fef-168">On the **AppDynamics Configuration** section, click **Configure AppDynamics** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="55fef-168">On the **AppDynamics Configuration** section, click **Configure AppDynamics** to open **Configure sign-on** window.</span></span> <span data-ttu-id="55fef-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="55fef-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/appdynamics-tutorial/tutorial_appdynamics_configure.png)

7. <span data-ttu-id="55fef-171">In a different web browser window, log in to your AppDynamics company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="55fef-171">In a different web browser window, log in to your AppDynamics company site as an administrator.</span></span>

8. <span data-ttu-id="55fef-172">In the toolbar on the top, click **Settings**, and then click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="55fef-172">In the toolbar on the top, click **Settings**, and then click **Administration**.</span></span>

    <span data-ttu-id="55fef-173">![Administration](./media/appdynamics-tutorial/ic790216.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="55fef-173">![Administration](./media/appdynamics-tutorial/ic790216.png "Administration")</span></span>

9. <span data-ttu-id="55fef-174">Click the **Authentication Provider** tab.</span><span class="sxs-lookup"><span data-stu-id="55fef-174">Click the **Authentication Provider** tab.</span></span>

    <span data-ttu-id="55fef-175">![Authentication Provider](./media/appdynamics-tutorial/ic790224.png "Authentication Provider")</span><span class="sxs-lookup"><span data-stu-id="55fef-175">![Authentication Provider](./media/appdynamics-tutorial/ic790224.png "Authentication Provider")</span></span>

10. <span data-ttu-id="55fef-176">In the **Authentication Provider** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="55fef-176">In the **Authentication Provider** section, perform the following steps:</span></span>

    <span data-ttu-id="55fef-177">![SAML Configuration](./media/appdynamics-tutorial/ic790225.png "SAML Configuration")</span><span class="sxs-lookup"><span data-stu-id="55fef-177">![SAML Configuration](./media/appdynamics-tutorial/ic790225.png "SAML Configuration")</span></span>

    <span data-ttu-id="55fef-178">a.</span><span class="sxs-lookup"><span data-stu-id="55fef-178">a.</span></span> <span data-ttu-id="55fef-179">As **Authentication Provider**, select **SAML**.</span><span class="sxs-lookup"><span data-stu-id="55fef-179">As **Authentication Provider**, select **SAML**.</span></span>

    <span data-ttu-id="55fef-180">b.</span><span class="sxs-lookup"><span data-stu-id="55fef-180">b.</span></span> <span data-ttu-id="55fef-181">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="55fef-181">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="55fef-182">c.</span><span class="sxs-lookup"><span data-stu-id="55fef-182">c.</span></span> <span data-ttu-id="55fef-183">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="55fef-183">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="55fef-184">d.</span><span class="sxs-lookup"><span data-stu-id="55fef-184">d.</span></span> <span data-ttu-id="55fef-185">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox</span><span class="sxs-lookup"><span data-stu-id="55fef-185">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox</span></span>

    <span data-ttu-id="55fef-186">e.</span><span class="sxs-lookup"><span data-stu-id="55fef-186">e.</span></span> <span data-ttu-id="55fef-187">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="55fef-187">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="55fef-188">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="55fef-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="55fef-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="55fef-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="55fef-191">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="55fef-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="55fef-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="55fef-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/appdynamics-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="55fef-194">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="55fef-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>

    ![Creating an Azure AD test user](./media/appdynamics-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="55fef-196">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="55fef-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>

    ![Creating an Azure AD test user](./media/appdynamics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="55fef-198">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="55fef-198">On the **User** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](./media/appdynamics-tutorial/create_aaduser_04.png)

    <span data-ttu-id="55fef-200">a.</span><span class="sxs-lookup"><span data-stu-id="55fef-200">a.</span></span> <span data-ttu-id="55fef-201">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="55fef-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="55fef-202">b.</span><span class="sxs-lookup"><span data-stu-id="55fef-202">b.</span></span> <span data-ttu-id="55fef-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="55fef-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="55fef-204">c.</span><span class="sxs-lookup"><span data-stu-id="55fef-204">c.</span></span> <span data-ttu-id="55fef-205">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="55fef-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="55fef-206">d.</span><span class="sxs-lookup"><span data-stu-id="55fef-206">d.</span></span> <span data-ttu-id="55fef-207">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="55fef-207">Click **Create**.</span></span>

### <a name="creating-an-appdynamics-test-user"></a><span data-ttu-id="55fef-208">Creating an AppDynamics test user</span><span class="sxs-lookup"><span data-stu-id="55fef-208">Creating an AppDynamics test user</span></span>

<span data-ttu-id="55fef-209">The objective of this section is to create a user called Britta Simon in AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="55fef-209">The objective of this section is to create a user called Britta Simon in AppDynamics.</span></span> <span data-ttu-id="55fef-210">AppDynamics supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="55fef-210">AppDynamics supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="55fef-211">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="55fef-211">There is no action item for you in this section.</span></span> <span data-ttu-id="55fef-212">A new user is created during an attempt to access AppDynamics if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="55fef-212">A new user is created during an attempt to access AppDynamics if it doesn't exist yet.</span></span>
>[!Note]
><span data-ttu-id="55fef-213">If you need to create a user manually, contact [AppDynamics Client support team](https://www.appdynamics.com/support/).</span><span class="sxs-lookup"><span data-stu-id="55fef-213">If you need to create a user manually, contact [AppDynamics Client support team](https://www.appdynamics.com/support/).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="55fef-214">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="55fef-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="55fef-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="55fef-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AppDynamics.</span></span>

![Assign User][200]

<span data-ttu-id="55fef-217">**To assign Britta Simon to AppDynamics, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="55fef-217">**To assign Britta Simon to AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="55fef-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="55fef-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="55fef-220">In the applications list, select **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="55fef-220">In the applications list, select **AppDynamics**.</span></span>

    ![Configure Single Sign-On](./media/appdynamics-tutorial/tutorial_appdynamics_app.png)

3. <span data-ttu-id="55fef-222">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="55fef-222">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202]

4. <span data-ttu-id="55fef-224">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="55fef-224">Click **Add** button.</span></span> <span data-ttu-id="55fef-225">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="55fef-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="55fef-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="55fef-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="55fef-228">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="55fef-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="55fef-229">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="55fef-229">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="55fef-230">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="55fef-230">Testing single sign-on</span></span>

<span data-ttu-id="55fef-231">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="55fef-231">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="55fef-232">When you click the AppDynamics tile in the Access Panel, you should get automatically signed-on to your AppDynamics application.</span><span class="sxs-lookup"><span data-stu-id="55fef-232">When you click the AppDynamics tile in the Access Panel, you should get automatically signed-on to your AppDynamics application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="55fef-233">Additional resources</span><span class="sxs-lookup"><span data-stu-id="55fef-233">Additional resources</span></span>

* [<span data-ttu-id="55fef-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="55fef-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="55fef-235">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="55fef-235">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/appdynamics-tutorial/tutorial_general_01.png
[2]: ./media/appdynamics-tutorial/tutorial_general_02.png
[3]: ./media/appdynamics-tutorial/tutorial_general_03.png
[4]: ./media/appdynamics-tutorial/tutorial_general_04.png

[100]: ./media/appdynamics-tutorial/tutorial_general_100.png

[200]: ./media/appdynamics-tutorial/tutorial_general_200.png
[201]: ./media/appdynamics-tutorial/tutorial_general_201.png
[202]: ./media/appdynamics-tutorial/tutorial_general_202.png
[203]: ./media/appdynamics-tutorial/tutorial_general_203.png
