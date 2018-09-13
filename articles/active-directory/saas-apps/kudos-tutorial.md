---
title: 'Tutorial: Azure Active Directory integration with Kudos | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Kudos.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 39c47ce6-4944-47ba-8f53-3afa95398034
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 878bbe16e2d33375c160c17d458654541e2f4174
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869997"
---
# <a name="tutorial-azure-active-directory-integration-with-kudos"></a><span data-ttu-id="f28d9-103">Tutorial: Azure Active Directory integration with Kudos</span><span class="sxs-lookup"><span data-stu-id="f28d9-103">Tutorial: Azure Active Directory integration with Kudos</span></span>

<span data-ttu-id="f28d9-104">In this tutorial, you learn how to integrate Kudos with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f28d9-104">In this tutorial, you learn how to integrate Kudos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f28d9-105">Integrating Kudos with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f28d9-105">Integrating Kudos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f28d9-106">You can control in Azure AD who has access to Kudos</span><span class="sxs-lookup"><span data-stu-id="f28d9-106">You can control in Azure AD who has access to Kudos</span></span>
- <span data-ttu-id="f28d9-107">You can enable your users to automatically get signed-on to Kudos (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="f28d9-107">You can enable your users to automatically get signed-on to Kudos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f28d9-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f28d9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f28d9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="f28d9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f28d9-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f28d9-110">Prerequisites</span></span>

<span data-ttu-id="f28d9-111">To configure Azure AD integration with Kudos, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f28d9-111">To configure Azure AD integration with Kudos, you need the following items:</span></span>

- <span data-ttu-id="f28d9-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f28d9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f28d9-113">A Kudos single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f28d9-113">A Kudos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f28d9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="f28d9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f28d9-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f28d9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f28d9-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="f28d9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f28d9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f28d9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f28d9-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="f28d9-118">Scenario description</span></span>
<span data-ttu-id="f28d9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f28d9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f28d9-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="f28d9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f28d9-121">Adding Kudos from the gallery</span><span class="sxs-lookup"><span data-stu-id="f28d9-121">Adding Kudos from the gallery</span></span>
1. <span data-ttu-id="f28d9-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f28d9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kudos-from-the-gallery"></a><span data-ttu-id="f28d9-123">Adding Kudos from the gallery</span><span class="sxs-lookup"><span data-stu-id="f28d9-123">Adding Kudos from the gallery</span></span>
<span data-ttu-id="f28d9-124">To configure the integration of Kudos into Azure AD, you need to add Kudos from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f28d9-124">To configure the integration of Kudos into Azure AD, you need to add Kudos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f28d9-125">**To add Kudos from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f28d9-125">**To add Kudos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f28d9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f28d9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="f28d9-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="f28d9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f28d9-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f28d9-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="f28d9-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="f28d9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="f28d9-133">In the search box, type **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="f28d9-133">In the search box, type **Kudos**.</span></span>

    ![Creating an Azure AD test user](./media/kudos-tutorial/tutorial_kudos_search.png)

1. <span data-ttu-id="f28d9-135">In the results panel, select **Kudos**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="f28d9-135">In the results panel, select **Kudos**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/kudos-tutorial/tutorial_kudos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f28d9-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f28d9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f28d9-138">In this section, you configure and test Azure AD single sign-on with Kudos based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f28d9-138">In this section, you configure and test Azure AD single sign-on with Kudos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f28d9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kudos is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f28d9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kudos is to a user in Azure AD.</span></span> <span data-ttu-id="f28d9-140">In other words, a link relationship between an Azure AD user and the related user in Kudos needs to be established.</span><span class="sxs-lookup"><span data-stu-id="f28d9-140">In other words, a link relationship between an Azure AD user and the related user in Kudos needs to be established.</span></span>

<span data-ttu-id="f28d9-141">In Kudos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="f28d9-141">In Kudos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f28d9-142">To configure and test Azure AD single sign-on with Kudos, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f28d9-142">To configure and test Azure AD single sign-on with Kudos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f28d9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f28d9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="f28d9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f28d9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="f28d9-145">**[Creating a Kudos test user](#creating-a-kudos-test-user)** - to have a counterpart of Britta Simon in Kudos that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="f28d9-145">**[Creating a Kudos test user](#creating-a-kudos-test-user)** - to have a counterpart of Britta Simon in Kudos that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="f28d9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f28d9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="f28d9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="f28d9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f28d9-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f28d9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f28d9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kudos application.</span><span class="sxs-lookup"><span data-stu-id="f28d9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kudos application.</span></span>

<span data-ttu-id="f28d9-150">**To configure Azure AD single sign-on with Kudos, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f28d9-150">**To configure Azure AD single sign-on with Kudos, perform the following steps:**</span></span>

1. <span data-ttu-id="f28d9-151">In the Azure portal, on the **Kudos** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f28d9-151">In the Azure portal, on the **Kudos** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="f28d9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f28d9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/kudos-tutorial/tutorial_kudos_samlbase.png)

1. <span data-ttu-id="f28d9-155">On the **Kudos Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f28d9-155">On the **Kudos Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/kudos-tutorial/tutorial_kudos_url.png)

    <span data-ttu-id="f28d9-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.kudosnow.com`</span><span class="sxs-lookup"><span data-stu-id="f28d9-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.kudosnow.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="f28d9-158">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="f28d9-158">This value is not real.</span></span> <span data-ttu-id="f28d9-159">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="f28d9-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="f28d9-160">Contact [Kudos Client support team](http://success.kudosnow.com/home) to get this value.</span><span class="sxs-lookup"><span data-stu-id="f28d9-160">Contact [Kudos Client support team](http://success.kudosnow.com/home) to get this value.</span></span> 
 
1. <span data-ttu-id="f28d9-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="f28d9-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/kudos-tutorial/tutorial_kudos_certificate.png) 

1. <span data-ttu-id="f28d9-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="f28d9-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/kudos-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="f28d9-165">On the **Kudos Configuration** section, click **Configure Kudos** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="f28d9-165">On the **Kudos Configuration** section, click **Configure Kudos** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f28d9-166">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="f28d9-166">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/kudos-tutorial/tutorial_kudos_configure.png) 

1. <span data-ttu-id="f28d9-168">In a different web browser window, log into your Kudos company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="f28d9-168">In a different web browser window, log into your Kudos company site as an administrator.</span></span>

1. <span data-ttu-id="f28d9-169">In the menu on the top, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="f28d9-169">In the menu on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="f28d9-170">![Settings](./media/kudos-tutorial/ic787806.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="f28d9-170">![Settings](./media/kudos-tutorial/ic787806.png "Settings")</span></span>

1. <span data-ttu-id="f28d9-171">Click **Integrations \> SSO**.</span><span class="sxs-lookup"><span data-stu-id="f28d9-171">Click **Integrations \> SSO**.</span></span>

1. <span data-ttu-id="f28d9-172">In the **SSO** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f28d9-172">In the **SSO** section, perform the following steps:</span></span>
   
    <span data-ttu-id="f28d9-173">![SSO](./media/kudos-tutorial/ic787807.png "SSO")</span><span class="sxs-lookup"><span data-stu-id="f28d9-173">![SSO](./media/kudos-tutorial/ic787807.png "SSO")</span></span>
   
    <span data-ttu-id="f28d9-174">a.</span><span class="sxs-lookup"><span data-stu-id="f28d9-174">a.</span></span> <span data-ttu-id="f28d9-175">In **Sign on URL** textbox, paste the value of  **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f28d9-175">In **Sign on URL** textbox, paste the value of  **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="f28d9-176">b.</span><span class="sxs-lookup"><span data-stu-id="f28d9-176">b.</span></span> <span data-ttu-id="f28d9-177">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 certificate** textbox</span><span class="sxs-lookup"><span data-stu-id="f28d9-177">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 certificate** textbox</span></span>
   
    <span data-ttu-id="f28d9-178">c.</span><span class="sxs-lookup"><span data-stu-id="f28d9-178">c.</span></span> <span data-ttu-id="f28d9-179">In **Logout To URL**, paste the value of  **Sign-Out URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f28d9-179">In **Logout To URL**, paste the value of  **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="f28d9-180">d.</span><span class="sxs-lookup"><span data-stu-id="f28d9-180">d.</span></span> <span data-ttu-id="f28d9-181">In the **Your Kudos URL** textbox, type your company name.</span><span class="sxs-lookup"><span data-stu-id="f28d9-181">In the **Your Kudos URL** textbox, type your company name.</span></span>
   
    <span data-ttu-id="f28d9-182">e.</span><span class="sxs-lookup"><span data-stu-id="f28d9-182">e.</span></span> <span data-ttu-id="f28d9-183">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f28d9-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f28d9-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="f28d9-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f28d9-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="f28d9-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f28d9-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f28d9-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f28d9-187">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f28d9-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="f28d9-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f28d9-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="f28d9-190">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f28d9-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f28d9-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f28d9-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/kudos-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="f28d9-193">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="f28d9-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/kudos-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="f28d9-195">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="f28d9-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/kudos-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="f28d9-197">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f28d9-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/kudos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f28d9-199">a.</span><span class="sxs-lookup"><span data-stu-id="f28d9-199">a.</span></span> <span data-ttu-id="f28d9-200">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f28d9-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f28d9-201">b.</span><span class="sxs-lookup"><span data-stu-id="f28d9-201">b.</span></span> <span data-ttu-id="f28d9-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f28d9-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f28d9-203">c.</span><span class="sxs-lookup"><span data-stu-id="f28d9-203">c.</span></span> <span data-ttu-id="f28d9-204">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="f28d9-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f28d9-205">d.</span><span class="sxs-lookup"><span data-stu-id="f28d9-205">d.</span></span> <span data-ttu-id="f28d9-206">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f28d9-206">Click **Create**.</span></span>
 
### <a name="creating-a-kudos-test-user"></a><span data-ttu-id="f28d9-207">Creating a Kudos test user</span><span class="sxs-lookup"><span data-stu-id="f28d9-207">Creating a Kudos test user</span></span>

<span data-ttu-id="f28d9-208">In order to enable Azure AD users to log into Kudos, they must be provisioned into Kudos.</span><span class="sxs-lookup"><span data-stu-id="f28d9-208">In order to enable Azure AD users to log into Kudos, they must be provisioned into Kudos.</span></span> 

<span data-ttu-id="f28d9-209">In the case of Kudos, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="f28d9-209">In the case of Kudos, provisioning is a manual task.</span></span>

<span data-ttu-id="f28d9-210">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f28d9-210">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="f28d9-211">Log in to your **Kudos** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="f28d9-211">Log in to your **Kudos** company site as administrator.</span></span>

1. <span data-ttu-id="f28d9-212">In the menu on the top, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="f28d9-212">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="f28d9-213">![Settings](./media/kudos-tutorial/ic787806.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="f28d9-213">![Settings](./media/kudos-tutorial/ic787806.png "Settings")</span></span>

1. <span data-ttu-id="f28d9-214">Click **User Admin**.</span><span class="sxs-lookup"><span data-stu-id="f28d9-214">Click **User Admin**.</span></span>

1. <span data-ttu-id="f28d9-215">Click the **Users** tab, and then click **Add a User**.</span><span class="sxs-lookup"><span data-stu-id="f28d9-215">Click the **Users** tab, and then click **Add a User**.</span></span>
   
   <span data-ttu-id="f28d9-216">![User Admin](./media/kudos-tutorial/ic787809.png "User Admin")</span><span class="sxs-lookup"><span data-stu-id="f28d9-216">![User Admin](./media/kudos-tutorial/ic787809.png "User Admin")</span></span>

1. <span data-ttu-id="f28d9-217">In the **Add a User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f28d9-217">In the **Add a User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="f28d9-218">![Add a User](./media/kudos-tutorial/ic787810.png "Add a User")</span><span class="sxs-lookup"><span data-stu-id="f28d9-218">![Add a User](./media/kudos-tutorial/ic787810.png "Add a User")</span></span>
   
    <span data-ttu-id="f28d9-219">a.</span><span class="sxs-lookup"><span data-stu-id="f28d9-219">a.</span></span> <span data-ttu-id="f28d9-220">Type the **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="f28d9-220">Type the **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="f28d9-221">b.</span><span class="sxs-lookup"><span data-stu-id="f28d9-221">b.</span></span> <span data-ttu-id="f28d9-222">Click **Create User**.</span><span class="sxs-lookup"><span data-stu-id="f28d9-222">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="f28d9-223">You can use any other Kudos user account creation tools or APIs provided by Kudos to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="f28d9-223">You can use any other Kudos user account creation tools or APIs provided by Kudos to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f28d9-224">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f28d9-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f28d9-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kudos.</span><span class="sxs-lookup"><span data-stu-id="f28d9-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kudos.</span></span>

![Assign User][200] 

<span data-ttu-id="f28d9-227">**To assign Britta Simon to Kudos, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f28d9-227">**To assign Britta Simon to Kudos, perform the following steps:**</span></span>

1. <span data-ttu-id="f28d9-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f28d9-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="f28d9-230">In the applications list, select **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="f28d9-230">In the applications list, select **Kudos**.</span></span>

    ![Configure Single Sign-On](./media/kudos-tutorial/tutorial_kudos_app.png) 

1. <span data-ttu-id="f28d9-232">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="f28d9-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="f28d9-234">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="f28d9-234">Click **Add** button.</span></span> <span data-ttu-id="f28d9-235">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f28d9-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="f28d9-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="f28d9-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="f28d9-238">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="f28d9-238">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="f28d9-239">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f28d9-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f28d9-240">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="f28d9-240">Testing single sign-on</span></span>

<span data-ttu-id="f28d9-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f28d9-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f28d9-242">When you click the Kudos tile in the Access Panel, you should get automatically signed-on to your Kudos application.</span><span class="sxs-lookup"><span data-stu-id="f28d9-242">When you click the Kudos tile in the Access Panel, you should get automatically signed-on to your Kudos application.</span></span> <span data-ttu-id="f28d9-243">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f28d9-243">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f28d9-244">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f28d9-244">Additional resources</span></span>

* [<span data-ttu-id="f28d9-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f28d9-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="f28d9-246">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f28d9-246">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/kudos-tutorial/tutorial_general_01.png
[2]: ./media/kudos-tutorial/tutorial_general_02.png
[3]: ./media/kudos-tutorial/tutorial_general_03.png
[4]: ./media/kudos-tutorial/tutorial_general_04.png

[100]: ./media/kudos-tutorial/tutorial_general_100.png

[200]: ./media/kudos-tutorial/tutorial_general_200.png
[201]: ./media/kudos-tutorial/tutorial_general_201.png
[202]: ./media/kudos-tutorial/tutorial_general_202.png
[203]: ./media/kudos-tutorial/tutorial_general_203.png

