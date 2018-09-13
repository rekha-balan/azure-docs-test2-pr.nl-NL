---
title: 'Tutorial: Azure Active Directory integration with StatusPage | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and StatusPage.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: f6ee8bb3-df43-4c0d-bf84-89f18deac4b9
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: e79eb2473760fd1eb7ccc3816ac73cce7c801f3e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866960"
---
# <a name="tutorial-azure-active-directory-integration-with-statuspage"></a><span data-ttu-id="4022f-103">Tutorial: Azure Active Directory integration with StatusPage</span><span class="sxs-lookup"><span data-stu-id="4022f-103">Tutorial: Azure Active Directory integration with StatusPage</span></span>

<span data-ttu-id="4022f-104">In this tutorial, you learn how to integrate StatusPage with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4022f-104">In this tutorial, you learn how to integrate StatusPage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4022f-105">Integrating StatusPage with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4022f-105">Integrating StatusPage with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4022f-106">You can control in Azure AD who has access to StatusPage</span><span class="sxs-lookup"><span data-stu-id="4022f-106">You can control in Azure AD who has access to StatusPage</span></span>
- <span data-ttu-id="4022f-107">You can enable your users to automatically get signed-on to StatusPage (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="4022f-107">You can enable your users to automatically get signed-on to StatusPage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4022f-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4022f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4022f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="4022f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4022f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4022f-110">Prerequisites</span></span>

<span data-ttu-id="4022f-111">To configure Azure AD integration with StatusPage, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4022f-111">To configure Azure AD integration with StatusPage, you need the following items:</span></span>

- <span data-ttu-id="4022f-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4022f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4022f-113">A StatusPage single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4022f-113">A StatusPage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4022f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4022f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4022f-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4022f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4022f-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="4022f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4022f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4022f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4022f-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="4022f-118">Scenario description</span></span>
<span data-ttu-id="4022f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4022f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4022f-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4022f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4022f-121">Adding StatusPage from the gallery</span><span class="sxs-lookup"><span data-stu-id="4022f-121">Adding StatusPage from the gallery</span></span>
1. <span data-ttu-id="4022f-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4022f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-statuspage-from-the-gallery"></a><span data-ttu-id="4022f-123">Adding StatusPage from the gallery</span><span class="sxs-lookup"><span data-stu-id="4022f-123">Adding StatusPage from the gallery</span></span>
<span data-ttu-id="4022f-124">To configure the integration of StatusPage into Azure AD, you need to add StatusPage from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4022f-124">To configure the integration of StatusPage into Azure AD, you need to add StatusPage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4022f-125">**To add StatusPage from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4022f-125">**To add StatusPage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4022f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4022f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="4022f-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="4022f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4022f-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4022f-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="4022f-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="4022f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="4022f-133">In the search box, type **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="4022f-133">In the search box, type **StatusPage**.</span></span>

    ![Creating an Azure AD test user](./media/statuspage-tutorial/tutorial_statuspage_search.png)

1. <span data-ttu-id="4022f-135">In the results panel, select **StatusPage**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="4022f-135">In the results panel, select **StatusPage**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/statuspage-tutorial/tutorial_statuspage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4022f-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4022f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4022f-138">In this section, you configure and test Azure AD single sign-on with StatusPage based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4022f-138">In this section, you configure and test Azure AD single sign-on with StatusPage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4022f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in StatusPage is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4022f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in StatusPage is to a user in Azure AD.</span></span> <span data-ttu-id="4022f-140">In other words, a link relationship between an Azure AD user and the related user in StatusPage needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4022f-140">In other words, a link relationship between an Azure AD user and the related user in StatusPage needs to be established.</span></span>

<span data-ttu-id="4022f-141">In StatusPage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="4022f-141">In StatusPage, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4022f-142">To configure and test Azure AD single sign-on with StatusPage, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4022f-142">To configure and test Azure AD single sign-on with StatusPage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4022f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4022f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="4022f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4022f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="4022f-145">**[Creating a StatusPage test user](#creating-a-statuspage-test-user)** - to have a counterpart of Britta Simon in StatusPage that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="4022f-145">**[Creating a StatusPage test user](#creating-a-statuspage-test-user)** - to have a counterpart of Britta Simon in StatusPage that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="4022f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4022f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="4022f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4022f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4022f-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4022f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4022f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your StatusPage application.</span><span class="sxs-lookup"><span data-stu-id="4022f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your StatusPage application.</span></span>

<span data-ttu-id="4022f-150">**To configure Azure AD single sign-on with StatusPage, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4022f-150">**To configure Azure AD single sign-on with StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="4022f-151">In the Azure portal, on the **StatusPage** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4022f-151">In the Azure portal, on the **StatusPage** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="4022f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4022f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/statuspage-tutorial/tutorial_statuspage_samlbase.png)

1. <span data-ttu-id="4022f-155">On the **StatusPage Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4022f-155">On the **StatusPage Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/statuspage-tutorial/tutorial_statuspage_url.png)

    <span data-ttu-id="4022f-157">a.</span><span class="sxs-lookup"><span data-stu-id="4022f-157">a.</span></span> <span data-ttu-id="4022f-158">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="4022f-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |

    <span data-ttu-id="4022f-159">b.</span><span class="sxs-lookup"><span data-stu-id="4022f-159">b.</span></span> <span data-ttu-id="4022f-160">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="4022f-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span> 
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |

    > [!NOTE]
    > <span data-ttu-id="4022f-161">Contact the StatusPage support team at [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)to request metadata necessary to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4022f-161">Contact the StatusPage support team at [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)to request metadata necessary to configure single sign-on.</span></span> 
    >
    ><span data-ttu-id="4022f-162">a.</span><span class="sxs-lookup"><span data-stu-id="4022f-162">a.</span></span> <span data-ttu-id="4022f-163">From the metadata, copy the Issuer value, and then paste it into the **Identifier** textbox.</span><span class="sxs-lookup"><span data-stu-id="4022f-163">From the metadata, copy the Issuer value, and then paste it into the **Identifier** textbox.</span></span>
    >
    ><span data-ttu-id="4022f-164">b.</span><span class="sxs-lookup"><span data-stu-id="4022f-164">b.</span></span> <span data-ttu-id="4022f-165">From the metadata, copy the Reply URL, and then paste it into the **Reply URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="4022f-165">From the metadata, copy the Reply URL, and then paste it into the **Reply URL** textbox.</span></span>

1. <span data-ttu-id="4022f-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4022f-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/statuspage-tutorial/tutorial_statuspage_certificate.png) 

1. <span data-ttu-id="4022f-168">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4022f-168">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/statuspage-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="4022f-170">On the **StatusPage Configuration** section, click **Configure StatusPage** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="4022f-170">On the **StatusPage Configuration** section, click **Configure StatusPage** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4022f-171">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="4022f-171">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/statuspage-tutorial/tutorial_statuspage_configure.png) 

1. <span data-ttu-id="4022f-173">In another browser window, sign on to your StatusPage company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="4022f-173">In another browser window, sign on to your StatusPage company site as an administrator.</span></span>

1. <span data-ttu-id="4022f-174">In the main toolbar, click **Manage Account**.</span><span class="sxs-lookup"><span data-stu-id="4022f-174">In the main toolbar, click **Manage Account**.</span></span>
   
    ![Configure Single Sign-On](./media/statuspage-tutorial/tutorial_statuspage_06.png) 

1. <span data-ttu-id="4022f-176">Click the **Single Sign-on** tab.</span><span class="sxs-lookup"><span data-stu-id="4022f-176">Click the **Single Sign-on** tab.</span></span> 
   
    ![Configure Single Sign-On](./media/statuspage-tutorial/tutorial_statuspage_07.png) 

1. <span data-ttu-id="4022f-178">On the SSO Setup page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4022f-178">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](./media/statuspage-tutorial/tutorial_statuspage_08.png) 

    ![Configure Single Sign-On](./media/statuspage-tutorial/tutorial_statuspage_09.png) 
 
    <span data-ttu-id="4022f-181">a.</span><span class="sxs-lookup"><span data-stu-id="4022f-181">a.</span></span> <span data-ttu-id="4022f-182">In the **SSO Target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4022f-182">In the **SSO Target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4022f-183">b.</span><span class="sxs-lookup"><span data-stu-id="4022f-183">b.</span></span> <span data-ttu-id="4022f-184">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="4022f-184">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span> 

    <span data-ttu-id="4022f-185">c.</span><span class="sxs-lookup"><span data-stu-id="4022f-185">c.</span></span> <span data-ttu-id="4022f-186">Click **SAVE CONFIGURATION**.</span><span class="sxs-lookup"><span data-stu-id="4022f-186">Click **SAVE CONFIGURATION**.</span></span>

> [!TIP]
> <span data-ttu-id="4022f-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="4022f-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4022f-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="4022f-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4022f-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4022f-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4022f-190">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4022f-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="4022f-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4022f-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="4022f-193">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4022f-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4022f-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4022f-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/statuspage-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="4022f-196">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4022f-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/statuspage-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="4022f-198">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="4022f-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/statuspage-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="4022f-200">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4022f-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/statuspage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4022f-202">a.</span><span class="sxs-lookup"><span data-stu-id="4022f-202">a.</span></span> <span data-ttu-id="4022f-203">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4022f-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4022f-204">b.</span><span class="sxs-lookup"><span data-stu-id="4022f-204">b.</span></span> <span data-ttu-id="4022f-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4022f-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4022f-206">c.</span><span class="sxs-lookup"><span data-stu-id="4022f-206">c.</span></span> <span data-ttu-id="4022f-207">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="4022f-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4022f-208">d.</span><span class="sxs-lookup"><span data-stu-id="4022f-208">d.</span></span> <span data-ttu-id="4022f-209">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4022f-209">Click **Create**.</span></span>
 
### <a name="creating-a-statuspage-test-user"></a><span data-ttu-id="4022f-210">Creating a StatusPage test user</span><span class="sxs-lookup"><span data-stu-id="4022f-210">Creating a StatusPage test user</span></span>

<span data-ttu-id="4022f-211">The objective of this section is to create a user called Britta Simon in StatusPage.</span><span class="sxs-lookup"><span data-stu-id="4022f-211">The objective of this section is to create a user called Britta Simon in StatusPage.</span></span>

<span data-ttu-id="4022f-212">StatusPage supports just-in-time provisioning.</span><span class="sxs-lookup"><span data-stu-id="4022f-212">StatusPage supports just-in-time provisioning.</span></span> <span data-ttu-id="4022f-213">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="4022f-213">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="4022f-214">**To create a user called Britta Simon in StatusPage, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4022f-214">**To create a user called Britta Simon in StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="4022f-215">Sign-on to your StatusPage company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="4022f-215">Sign-on to your StatusPage company site as an administrator.</span></span>

1. <span data-ttu-id="4022f-216">In the menu on the top, click **Manage Account**.</span><span class="sxs-lookup"><span data-stu-id="4022f-216">In the menu on the top, click **Manage Account**.</span></span>

    ![Configure Single Sign-On](./media/statuspage-tutorial/tutorial_statuspage_06.png)

1. <span data-ttu-id="4022f-218">Click the **Team Members** tab.</span><span class="sxs-lookup"><span data-stu-id="4022f-218">Click the **Team Members** tab.</span></span> 
   
    ![Creating an Azure AD test user](./media/statuspage-tutorial/tutorial_statuspage_10.png) 

1. <span data-ttu-id="4022f-220">Click **ADD TEAM MEMBER**.</span><span class="sxs-lookup"><span data-stu-id="4022f-220">Click **ADD TEAM MEMBER**.</span></span> 
   
    ![Creating an Azure AD test user](./media/statuspage-tutorial/tutorial_statuspage_11.png) 

1. <span data-ttu-id="4022f-222">Type the **Email Address**, **First Name**, and **Sur Name** of a valid user you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="4022f-222">Type the **Email Address**, **First Name**, and **Sur Name** of a valid user you want to provision into the related textboxes.</span></span> 
   
    ![Creating an Azure AD test user](./media/statuspage-tutorial/tutorial_statuspage_12.png) 

1. <span data-ttu-id="4022f-224">As **Role**, choose **Client Administrator**.</span><span class="sxs-lookup"><span data-stu-id="4022f-224">As **Role**, choose **Client Administrator**.</span></span>

1. <span data-ttu-id="4022f-225">Click **CREATE ACCOUNT**.</span><span class="sxs-lookup"><span data-stu-id="4022f-225">Click **CREATE ACCOUNT**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4022f-226">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4022f-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4022f-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to StatusPage.</span><span class="sxs-lookup"><span data-stu-id="4022f-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to StatusPage.</span></span>

![Assign User][200] 

<span data-ttu-id="4022f-229">**To assign Britta Simon to StatusPage, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4022f-229">**To assign Britta Simon to StatusPage, perform the following steps:**</span></span>

1. <span data-ttu-id="4022f-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4022f-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="4022f-232">In the applications list, select **StatusPage**.</span><span class="sxs-lookup"><span data-stu-id="4022f-232">In the applications list, select **StatusPage**.</span></span>

    ![Configure Single Sign-On](./media/statuspage-tutorial/tutorial_statuspage_app.png) 

1. <span data-ttu-id="4022f-234">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="4022f-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="4022f-236">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="4022f-236">Click **Add** button.</span></span> <span data-ttu-id="4022f-237">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4022f-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="4022f-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="4022f-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="4022f-240">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="4022f-240">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="4022f-241">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4022f-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4022f-242">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="4022f-242">Testing single sign-on</span></span>

<span data-ttu-id="4022f-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4022f-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4022f-244">When you click the StatusPage tile in the Access Panel, you should get automatically signed-on to your StatusPage application.</span><span class="sxs-lookup"><span data-stu-id="4022f-244">When you click the StatusPage tile in the Access Panel, you should get automatically signed-on to your StatusPage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4022f-245">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4022f-245">Additional resources</span></span>

* [<span data-ttu-id="4022f-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4022f-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="4022f-247">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4022f-247">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/statuspage-tutorial/tutorial_general_01.png
[2]: ./media/statuspage-tutorial/tutorial_general_02.png
[3]: ./media/statuspage-tutorial/tutorial_general_03.png
[4]: ./media/statuspage-tutorial/tutorial_general_04.png

[100]: ./media/statuspage-tutorial/tutorial_general_100.png

[200]: ./media/statuspage-tutorial/tutorial_general_200.png
[201]: ./media/statuspage-tutorial/tutorial_general_201.png
[202]: ./media/statuspage-tutorial/tutorial_general_202.png
[203]: ./media/statuspage-tutorial/tutorial_general_203.png

