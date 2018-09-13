---
title: 'Tutorial: Azure Active Directory integration with Jitbit Helpdesk | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Jitbit Helpdesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 94ded0ef1bf77de20973a87a1ca2d6d1dd3fdf3f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865446"
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a><span data-ttu-id="bbf9e-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="bbf9e-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span></span>

<span data-ttu-id="bbf9e-104">In this tutorial, you learn how to integrate Jitbit Helpdesk with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bbf9e-104">In this tutorial, you learn how to integrate Jitbit Helpdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bbf9e-105">Integrating Jitbit Helpdesk with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="bbf9e-105">Integrating Jitbit Helpdesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bbf9e-106">You can control in Azure AD who has access to Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="bbf9e-106">You can control in Azure AD who has access to Jitbit Helpdesk</span></span>
- <span data-ttu-id="bbf9e-107">You can enable your users to automatically get signed-on to Jitbit Helpdesk (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="bbf9e-107">You can enable your users to automatically get signed-on to Jitbit Helpdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bbf9e-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="bbf9e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bbf9e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="bbf9e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bbf9e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bbf9e-110">Prerequisites</span></span>

<span data-ttu-id="bbf9e-111">To configure Azure AD integration with Jitbit Helpdesk, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="bbf9e-111">To configure Azure AD integration with Jitbit Helpdesk, you need the following items:</span></span>

- <span data-ttu-id="bbf9e-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="bbf9e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bbf9e-113">A Jitbit Helpdesk single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="bbf9e-113">A Jitbit Helpdesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bbf9e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bbf9e-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="bbf9e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bbf9e-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bbf9e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bbf9e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bbf9e-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="bbf9e-118">Scenario description</span></span>
<span data-ttu-id="bbf9e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bbf9e-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="bbf9e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bbf9e-121">Adding Jitbit Helpdesk from the gallery</span><span class="sxs-lookup"><span data-stu-id="bbf9e-121">Adding Jitbit Helpdesk from the gallery</span></span>
1. <span data-ttu-id="bbf9e-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bbf9e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jitbit-helpdesk-from-the-gallery"></a><span data-ttu-id="bbf9e-123">Adding Jitbit Helpdesk from the gallery</span><span class="sxs-lookup"><span data-stu-id="bbf9e-123">Adding Jitbit Helpdesk from the gallery</span></span>
<span data-ttu-id="bbf9e-124">To configure the integration of Jitbit Helpdesk into Azure AD, you need to add Jitbit Helpdesk from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-124">To configure the integration of Jitbit Helpdesk into Azure AD, you need to add Jitbit Helpdesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bbf9e-125">**To add Jitbit Helpdesk from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bbf9e-125">**To add Jitbit Helpdesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bbf9e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="bbf9e-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bbf9e-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="bbf9e-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="bbf9e-133">In the search box, type **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-133">In the search box, type **Jitbit Helpdesk**.</span></span>

    ![Creating an Azure AD test user](./media/jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

1. <span data-ttu-id="bbf9e-135">In the results panel, select **Jitbit Helpdesk**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-135">In the results panel, select **Jitbit Helpdesk**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bbf9e-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bbf9e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bbf9e-138">In this section, you configure and test Azure AD single sign-on with Jitbit Helpdesk based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bbf9e-138">In this section, you configure and test Azure AD single sign-on with Jitbit Helpdesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bbf9e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jitbit Helpdesk is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jitbit Helpdesk is to a user in Azure AD.</span></span> <span data-ttu-id="bbf9e-140">In other words, a link relationship between an Azure AD user and the related user in Jitbit Helpdesk needs to be established.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-140">In other words, a link relationship between an Azure AD user and the related user in Jitbit Helpdesk needs to be established.</span></span>

<span data-ttu-id="bbf9e-141">In Jitbit Helpdesk, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-141">In Jitbit Helpdesk, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bbf9e-142">To configure and test Azure AD single sign-on with Jitbit Helpdesk, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="bbf9e-142">To configure and test Azure AD single sign-on with Jitbit Helpdesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bbf9e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="bbf9e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="bbf9e-145">**[Creating a Jitbit Helpdesk test user](#creating-a-jitbit-helpdesk-test-user)** - to have a counterpart of Britta Simon in Jitbit Helpdesk that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-145">**[Creating a Jitbit Helpdesk test user](#creating-a-jitbit-helpdesk-test-user)** - to have a counterpart of Britta Simon in Jitbit Helpdesk that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="bbf9e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="bbf9e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bbf9e-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bbf9e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bbf9e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jitbit Helpdesk application.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jitbit Helpdesk application.</span></span>

<span data-ttu-id="bbf9e-150">**To configure Azure AD single sign-on with Jitbit Helpdesk, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bbf9e-150">**To configure Azure AD single sign-on with Jitbit Helpdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="bbf9e-151">In the Azure portal, on the **Jitbit Helpdesk** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-151">In the Azure portal, on the **Jitbit Helpdesk** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="bbf9e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

1. <span data-ttu-id="bbf9e-155">On the **Jitbit Helpdesk Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bbf9e-155">On the **Jitbit Helpdesk Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    <span data-ttu-id="bbf9e-157">a.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-157">a.</span></span> <span data-ttu-id="bbf9e-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="bbf9e-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > <span data-ttu-id="bbf9e-159">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-159">This value is not real.</span></span> <span data-ttu-id="bbf9e-160">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="bbf9e-161">Contact [Jitbit Helpdesk Client support team](https://www.jitbit.com/support/) to get this value.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-161">Contact [Jitbit Helpdesk Client support team](https://www.jitbit.com/support/) to get this value.</span></span> 
    
    <span data-ttu-id="bbf9e-162">b.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-162">b.</span></span>  <span data-ttu-id="bbf9e-163">In the **Identifier** textbox, type a URL as following: `https://www.jitbit.com/web-helpdesk/`</span><span class="sxs-lookup"><span data-stu-id="bbf9e-163">In the **Identifier** textbox, type a URL as following: `https://www.jitbit.com/web-helpdesk/`</span></span>

    
 


1. <span data-ttu-id="bbf9e-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

1. <span data-ttu-id="bbf9e-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/jitbit-helpdesk-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="bbf9e-168">On the **Jitbit Helpdesk Configuration** section, click **Configure Jitbit Helpdesk** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-168">On the **Jitbit Helpdesk Configuration** section, click **Configure Jitbit Helpdesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bbf9e-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="bbf9e-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

1. <span data-ttu-id="bbf9e-171">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-171">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span></span>

1. <span data-ttu-id="bbf9e-172">In the toolbar on the top, click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-172">In the toolbar on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="bbf9e-173">![Administration](./media/jitbit-helpdesk-tutorial/ic777681.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="bbf9e-173">![Administration](./media/jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

1. <span data-ttu-id="bbf9e-174">Click **General settings**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-174">Click **General settings**.</span></span>
   
    <span data-ttu-id="bbf9e-175">![Users, companies, and permissions](./media/jitbit-helpdesk-tutorial/ic777680.png "Users, companies, and permissions")</span><span class="sxs-lookup"><span data-stu-id="bbf9e-175">![Users, companies, and permissions](./media/jitbit-helpdesk-tutorial/ic777680.png "Users, companies, and permissions")</span></span>

1. <span data-ttu-id="bbf9e-176">In the **Authentication settings** configuration section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bbf9e-176">In the **Authentication settings** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="bbf9e-177">![Authentication settings](./media/jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span><span class="sxs-lookup"><span data-stu-id="bbf9e-177">![Authentication settings](./media/jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span></span>
    
    <span data-ttu-id="bbf9e-178">a.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-178">a.</span></span> <span data-ttu-id="bbf9e-179">Select **Enable SAML 2.0 single sign on**, to sign in using Single Sign-On (SSO), with **OneLogin**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-179">Select **Enable SAML 2.0 single sign on**, to sign in using Single Sign-On (SSO), with **OneLogin**.</span></span>

    <span data-ttu-id="bbf9e-180">b.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-180">b.</span></span> <span data-ttu-id="bbf9e-181">In the **EndPoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-181">In the **EndPoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bbf9e-182">c.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-182">c.</span></span> <span data-ttu-id="bbf9e-183">Open your **base-64** encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span><span class="sxs-lookup"><span data-stu-id="bbf9e-183">Open your **base-64** encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>

    <span data-ttu-id="bbf9e-184">d.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-184">d.</span></span> <span data-ttu-id="bbf9e-185">Click **Save changes**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-185">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="bbf9e-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="bbf9e-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bbf9e-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bbf9e-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bbf9e-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bbf9e-189">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="bbf9e-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="bbf9e-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="bbf9e-192">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bbf9e-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bbf9e-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/jitbit-helpdesk-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="bbf9e-195">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/jitbit-helpdesk-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="bbf9e-197">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/jitbit-helpdesk-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="bbf9e-199">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bbf9e-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bbf9e-201">a.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-201">a.</span></span> <span data-ttu-id="bbf9e-202">In the **Name** textbox, type name as **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-202">In the **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="bbf9e-203">b.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-203">b.</span></span> <span data-ttu-id="bbf9e-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bbf9e-205">c.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-205">c.</span></span> <span data-ttu-id="bbf9e-206">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bbf9e-207">d.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-207">d.</span></span> <span data-ttu-id="bbf9e-208">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-208">Click **Create**.</span></span>
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a><span data-ttu-id="bbf9e-209">Creating a Jitbit Helpdesk test user</span><span class="sxs-lookup"><span data-stu-id="bbf9e-209">Creating a Jitbit Helpdesk test user</span></span>

<span data-ttu-id="bbf9e-210">In order to enable Azure AD users to log into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-210">In order to enable Azure AD users to log into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span></span>  <span data-ttu-id="bbf9e-211">In the case of Jitbit Helpdesk, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-211">In the case of Jitbit Helpdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="bbf9e-212">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bbf9e-212">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="bbf9e-213">Log in to your **Jitbit Helpdesk** tenant.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-213">Log in to your **Jitbit Helpdesk** tenant.</span></span>

1. <span data-ttu-id="bbf9e-214">In the menu on the top, click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-214">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="bbf9e-215">![Administration](./media/jitbit-helpdesk-tutorial/ic777681.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="bbf9e-215">![Administration](./media/jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

1. <span data-ttu-id="bbf9e-216">Click **Users, companies and permissions**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-216">Click **Users, companies and permissions**.</span></span>
   
    <span data-ttu-id="bbf9e-217">![Users, companies, and permissions](./media/jitbit-helpdesk-tutorial/ic777682.png "Users, companies, and permissions")</span><span class="sxs-lookup"><span data-stu-id="bbf9e-217">![Users, companies, and permissions](./media/jitbit-helpdesk-tutorial/ic777682.png "Users, companies, and permissions")</span></span>

1. <span data-ttu-id="bbf9e-218">Click **Add user**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-218">Click **Add user**.</span></span>
   
    <span data-ttu-id="bbf9e-219">![Add user](./media/jitbit-helpdesk-tutorial/ic777685.png "Add user")</span><span class="sxs-lookup"><span data-stu-id="bbf9e-219">![Add user](./media/jitbit-helpdesk-tutorial/ic777685.png "Add user")</span></span>
   
1. <span data-ttu-id="bbf9e-220">In the Create section, type the data of the Azure AD account you want to provision as follows:</span><span class="sxs-lookup"><span data-stu-id="bbf9e-220">In the Create section, type the data of the Azure AD account you want to provision as follows:</span></span>

    <span data-ttu-id="bbf9e-221">![Create](./media/jitbit-helpdesk-tutorial/ic777686.png "Create")</span><span class="sxs-lookup"><span data-stu-id="bbf9e-221">![Create](./media/jitbit-helpdesk-tutorial/ic777686.png "Create")</span></span>
   
   <span data-ttu-id="bbf9e-222">a.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-222">a.</span></span> <span data-ttu-id="bbf9e-223">In the **Username** textbox, type **BrittaSimon**, the user name as in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-223">In the **Username** textbox, type **BrittaSimon**, the user name as in the Azure portal.</span></span>

   <span data-ttu-id="bbf9e-224">b.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-224">b.</span></span> <span data-ttu-id="bbf9e-225">In the **Email** textbox, type email of the user like **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-225">In the **Email** textbox, type email of the user like **BrittaSimon@contoso.com**.</span></span>

   <span data-ttu-id="bbf9e-226">c.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-226">c.</span></span> <span data-ttu-id="bbf9e-227">In the **First Name** textbox, type first name of the user like **Britta**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-227">In the **First Name** textbox, type first name of the user like **Britta**.</span></span>

   <span data-ttu-id="bbf9e-228">d.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-228">d.</span></span> <span data-ttu-id="bbf9e-229">In the **Last Name** textbox, type last name of the user like **Simon**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-229">In the **Last Name** textbox, type last name of the user like **Simon**.</span></span>
   
   <span data-ttu-id="bbf9e-230">e.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-230">e.</span></span> <span data-ttu-id="bbf9e-231">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-231">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="bbf9e-232">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-232">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk to provision Azure AD user accounts.</span></span>
> 
        

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bbf9e-233">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="bbf9e-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bbf9e-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jitbit Helpdesk.</span></span>

![Assign User][200] 

<span data-ttu-id="bbf9e-236">**To assign Britta Simon to Jitbit Helpdesk, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bbf9e-236">**To assign Britta Simon to Jitbit Helpdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="bbf9e-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="bbf9e-239">In the applications list, select **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-239">In the applications list, select **Jitbit Helpdesk**.</span></span>

    ![Configure Single Sign-On](./media/jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

1. <span data-ttu-id="bbf9e-241">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="bbf9e-243">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-243">Click **Add** button.</span></span> <span data-ttu-id="bbf9e-244">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="bbf9e-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="bbf9e-247">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-247">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="bbf9e-248">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bbf9e-249">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="bbf9e-249">Testing single sign-on</span></span>

<span data-ttu-id="bbf9e-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bbf9e-251">When you click the Jitbit Helpdesk tile in the Access Panel, you should get login page of Jitbit Helpdesk application.</span><span class="sxs-lookup"><span data-stu-id="bbf9e-251">When you click the Jitbit Helpdesk tile in the Access Panel, you should get login page of Jitbit Helpdesk application.</span></span>
<span data-ttu-id="bbf9e-252">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bbf9e-252">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bbf9e-253">Additional resources</span><span class="sxs-lookup"><span data-stu-id="bbf9e-253">Additional resources</span></span>

* [<span data-ttu-id="bbf9e-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bbf9e-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="bbf9e-255">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bbf9e-255">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/jitbit-helpdesk-tutorial/tutorial_general_203.png

