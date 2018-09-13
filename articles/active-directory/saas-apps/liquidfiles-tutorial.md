---
title: 'Tutorial: Azure Active Directory integration with LiquidFiles | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and LiquidFiles.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: cb517134-0b34-4a74-b40c-5a3223ca81b6
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: f1fc9be81cb5ada628c253351746dbaf11fe3b84
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868091"
---
# <a name="tutorial-azure-active-directory-integration-with-liquidfiles"></a><span data-ttu-id="8e60f-103">Tutorial: Azure Active Directory integration with LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="8e60f-103">Tutorial: Azure Active Directory integration with LiquidFiles</span></span>

<span data-ttu-id="8e60f-104">In this tutorial, you learn how to integrate LiquidFiles with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8e60f-104">In this tutorial, you learn how to integrate LiquidFiles with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8e60f-105">Integrating LiquidFiles with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8e60f-105">Integrating LiquidFiles with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8e60f-106">You can control in Azure AD who has access to LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="8e60f-106">You can control in Azure AD who has access to LiquidFiles</span></span>
- <span data-ttu-id="8e60f-107">You can enable your users to automatically get signed-on to LiquidFiles (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="8e60f-107">You can enable your users to automatically get signed-on to LiquidFiles (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8e60f-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8e60f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8e60f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="8e60f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e60f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8e60f-110">Prerequisites</span></span>

<span data-ttu-id="8e60f-111">To configure Azure AD integration with LiquidFiles, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8e60f-111">To configure Azure AD integration with LiquidFiles, you need the following items:</span></span>

- <span data-ttu-id="8e60f-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8e60f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8e60f-113">A LiquidFiles single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8e60f-113">A LiquidFiles single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8e60f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8e60f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8e60f-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8e60f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8e60f-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="8e60f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8e60f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8e60f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8e60f-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="8e60f-118">Scenario description</span></span>
<span data-ttu-id="8e60f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8e60f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8e60f-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8e60f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8e60f-121">Adding LiquidFiles from the gallery</span><span class="sxs-lookup"><span data-stu-id="8e60f-121">Adding LiquidFiles from the gallery</span></span>
1. <span data-ttu-id="8e60f-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8e60f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-liquidfiles-from-the-gallery"></a><span data-ttu-id="8e60f-123">Adding LiquidFiles from the gallery</span><span class="sxs-lookup"><span data-stu-id="8e60f-123">Adding LiquidFiles from the gallery</span></span>
<span data-ttu-id="8e60f-124">To configure the integration of LiquidFiles into Azure AD, you need to add LiquidFiles from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8e60f-124">To configure the integration of LiquidFiles into Azure AD, you need to add LiquidFiles from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8e60f-125">**To add LiquidFiles from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8e60f-125">**To add LiquidFiles from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8e60f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8e60f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="8e60f-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="8e60f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8e60f-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8e60f-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="8e60f-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="8e60f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="8e60f-133">In the search box, type **LiquidFiles**.</span><span class="sxs-lookup"><span data-stu-id="8e60f-133">In the search box, type **LiquidFiles**.</span></span>

    ![Creating an Azure AD test user](./media/liquidfiles-tutorial/tutorial_liquidfiles_search.png)

1. <span data-ttu-id="8e60f-135">In the results panel, select **LiquidFiles**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="8e60f-135">In the results panel, select **LiquidFiles**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/liquidfiles-tutorial/tutorial_liquidfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8e60f-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8e60f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8e60f-138">In this section, you configure and test Azure AD single sign-on with LiquidFiles based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8e60f-138">In this section, you configure and test Azure AD single sign-on with LiquidFiles based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8e60f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LiquidFiles is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e60f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LiquidFiles is to a user in Azure AD.</span></span> <span data-ttu-id="8e60f-140">In other words, a link relationship between an Azure AD user and the related user in LiquidFiles needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8e60f-140">In other words, a link relationship between an Azure AD user and the related user in LiquidFiles needs to be established.</span></span>

<span data-ttu-id="8e60f-141">In LiquidFiles, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="8e60f-141">In LiquidFiles, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8e60f-142">To configure and test Azure AD single sign-on with LiquidFiles, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8e60f-142">To configure and test Azure AD single sign-on with LiquidFiles, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8e60f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8e60f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="8e60f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e60f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="8e60f-145">**[Creating a LiquidFiles test user](#creating-a-liquidfiles-test-user)** - to have a counterpart of Britta Simon in LiquidFiles that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="8e60f-145">**[Creating a LiquidFiles test user](#creating-a-liquidfiles-test-user)** - to have a counterpart of Britta Simon in LiquidFiles that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="8e60f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8e60f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="8e60f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8e60f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8e60f-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8e60f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8e60f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LiquidFiles application.</span><span class="sxs-lookup"><span data-stu-id="8e60f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LiquidFiles application.</span></span>

<span data-ttu-id="8e60f-150">**To configure Azure AD single sign-on with LiquidFiles, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8e60f-150">**To configure Azure AD single sign-on with LiquidFiles, perform the following steps:**</span></span>

1. <span data-ttu-id="8e60f-151">In the Azure portal, on the **LiquidFiles** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8e60f-151">In the Azure portal, on the **LiquidFiles** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="8e60f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8e60f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/liquidfiles-tutorial/tutorial_liquidfiles_samlbase.png)

1. <span data-ttu-id="8e60f-155">On the **LiquidFiles Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8e60f-155">On the **LiquidFiles Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/liquidfiles-tutorial/tutorial_liquidfiles_url.png)

    <span data-ttu-id="8e60f-157">a.</span><span class="sxs-lookup"><span data-stu-id="8e60f-157">a.</span></span> <span data-ttu-id="8e60f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<YOUR_SERVER_URL>/saml/init`</span><span class="sxs-lookup"><span data-stu-id="8e60f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<YOUR_SERVER_URL>/saml/init`</span></span>

    <span data-ttu-id="8e60f-159">b.</span><span class="sxs-lookup"><span data-stu-id="8e60f-159">b.</span></span> <span data-ttu-id="8e60f-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<YOUR_SERVER_URL>`</span><span class="sxs-lookup"><span data-stu-id="8e60f-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<YOUR_SERVER_URL>`</span></span>

    <span data-ttu-id="8e60f-161">c.</span><span class="sxs-lookup"><span data-stu-id="8e60f-161">c.</span></span> <span data-ttu-id="8e60f-162">b.</span><span class="sxs-lookup"><span data-stu-id="8e60f-162">b.</span></span> <span data-ttu-id="8e60f-163">In the **Reply URL** textbox, type a URL using the following pattern: `https://<YOUR_SERVER_URL>/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="8e60f-163">In the **Reply URL** textbox, type a URL using the following pattern: `https://<YOUR_SERVER_URL>/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8e60f-164">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="8e60f-164">These values are not real.</span></span> <span data-ttu-id="8e60f-165">Update these values with the actual Sign-On URL, Identifier and, Reply URL.</span><span class="sxs-lookup"><span data-stu-id="8e60f-165">Update these values with the actual Sign-On URL, Identifier and, Reply URL.</span></span> <span data-ttu-id="8e60f-166">Contact [LiquidFiles Client support team](https://www.liquidfiles.com/support.html) to get these values.</span><span class="sxs-lookup"><span data-stu-id="8e60f-166">Contact [LiquidFiles Client support team](https://www.liquidfiles.com/support.html) to get these values.</span></span> 
 
1. <span data-ttu-id="8e60f-167">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span><span class="sxs-lookup"><span data-stu-id="8e60f-167">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Configure Single Sign-On](./media/liquidfiles-tutorial/tutorial_liquidfiles_certificate.png) 

1. <span data-ttu-id="8e60f-169">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="8e60f-169">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/liquidfiles-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="8e60f-171">On the **LiquidFiles Configuration** section, click **Configure LiquidFiles** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="8e60f-171">On the **LiquidFiles Configuration** section, click **Configure LiquidFiles** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8e60f-172">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="8e60f-172">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/liquidfiles-tutorial/tutorial_liquidfiles_configure.png)
 
1. <span data-ttu-id="8e60f-174">Sign-on to your LiquidFiles company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="8e60f-174">Sign-on to your LiquidFiles company site as administrator.</span></span>

1. <span data-ttu-id="8e60f-175">Click **Single Sign-On** in the **Admin > Configuration** from the menu.</span><span class="sxs-lookup"><span data-stu-id="8e60f-175">Click **Single Sign-On** in the **Admin > Configuration** from the menu.</span></span>

1. <span data-ttu-id="8e60f-176">On the **Single Sign-On Configuration** page, perform the following steps</span><span class="sxs-lookup"><span data-stu-id="8e60f-176">On the **Single Sign-On Configuration** page, perform the following steps</span></span>

    ![Configure Single Sign-On](./media/liquidfiles-tutorial/tutorial_single_01.png)

    <span data-ttu-id="8e60f-178">a.</span><span class="sxs-lookup"><span data-stu-id="8e60f-178">a.</span></span> <span data-ttu-id="8e60f-179">As **Single Sign On Method**, select **SAML 2**.</span><span class="sxs-lookup"><span data-stu-id="8e60f-179">As **Single Sign On Method**, select **SAML 2**.</span></span>

    <span data-ttu-id="8e60f-180">b.</span><span class="sxs-lookup"><span data-stu-id="8e60f-180">b.</span></span> <span data-ttu-id="8e60f-181">In the **IDP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8e60f-181">In the **IDP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8e60f-182">c.</span><span class="sxs-lookup"><span data-stu-id="8e60f-182">c.</span></span> <span data-ttu-id="8e60f-183">In the **IDP Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8e60f-183">In the **IDP Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8e60f-184">d.</span><span class="sxs-lookup"><span data-stu-id="8e60f-184">d.</span></span> <span data-ttu-id="8e60f-185">In the **IDP Cert Fingerprint** textbox, paste the **THUMBPRINT** value which you have copied from Azure portal..</span><span class="sxs-lookup"><span data-stu-id="8e60f-185">In the **IDP Cert Fingerprint** textbox, paste the **THUMBPRINT** value which you have copied from Azure portal..</span></span>

    <span data-ttu-id="8e60f-186">e.</span><span class="sxs-lookup"><span data-stu-id="8e60f-186">e.</span></span> <span data-ttu-id="8e60f-187">In the Name Identifier Format textbox, type the value **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="8e60f-187">In the Name Identifier Format textbox, type the value **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="8e60f-188">f.</span><span class="sxs-lookup"><span data-stu-id="8e60f-188">f.</span></span> <span data-ttu-id="8e60f-189">In the Authn Context textbox, type the value **urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport**.</span><span class="sxs-lookup"><span data-stu-id="8e60f-189">In the Authn Context textbox, type the value **urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport**.</span></span>

    <span data-ttu-id="8e60f-190">g.</span><span class="sxs-lookup"><span data-stu-id="8e60f-190">g.</span></span> <span data-ttu-id="8e60f-191">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="8e60f-191">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="8e60f-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="8e60f-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8e60f-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="8e60f-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8e60f-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8e60f-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8e60f-195">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8e60f-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="8e60f-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e60f-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="8e60f-198">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8e60f-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8e60f-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8e60f-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/liquidfiles-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="8e60f-201">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="8e60f-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/liquidfiles-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="8e60f-203">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="8e60f-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/liquidfiles-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="8e60f-205">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8e60f-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/liquidfiles-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8e60f-207">a.</span><span class="sxs-lookup"><span data-stu-id="8e60f-207">a.</span></span> <span data-ttu-id="8e60f-208">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8e60f-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8e60f-209">b.</span><span class="sxs-lookup"><span data-stu-id="8e60f-209">b.</span></span> <span data-ttu-id="8e60f-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8e60f-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8e60f-211">c.</span><span class="sxs-lookup"><span data-stu-id="8e60f-211">c.</span></span> <span data-ttu-id="8e60f-212">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="8e60f-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8e60f-213">d.</span><span class="sxs-lookup"><span data-stu-id="8e60f-213">d.</span></span> <span data-ttu-id="8e60f-214">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8e60f-214">Click **Create**.</span></span>
 
### <a name="creating-a-liquidfiles-test-user"></a><span data-ttu-id="8e60f-215">Creating a LiquidFiles test user</span><span class="sxs-lookup"><span data-stu-id="8e60f-215">Creating a LiquidFiles test user</span></span>

<span data-ttu-id="8e60f-216">The objective of this section is to create a user called Britta Simon in LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="8e60f-216">The objective of this section is to create a user called Britta Simon in LiquidFiles.</span></span> <span data-ttu-id="8e60f-217">Work with your LiquidFiles server administrator to get yourself added as a user before logging in to your LiquidFiles application.</span><span class="sxs-lookup"><span data-stu-id="8e60f-217">Work with your LiquidFiles server administrator to get yourself added as a user before logging in to your LiquidFiles application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8e60f-218">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8e60f-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8e60f-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LiquidFiles.</span><span class="sxs-lookup"><span data-stu-id="8e60f-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LiquidFiles.</span></span>

![Assign User][200] 

<span data-ttu-id="8e60f-221">**To assign Britta Simon to LiquidFiles, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8e60f-221">**To assign Britta Simon to LiquidFiles, perform the following steps:**</span></span>

1. <span data-ttu-id="8e60f-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8e60f-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="8e60f-224">In the applications list, select **LiquidFiles**.</span><span class="sxs-lookup"><span data-stu-id="8e60f-224">In the applications list, select **LiquidFiles**.</span></span>

    ![Configure Single Sign-On](./media/liquidfiles-tutorial/tutorial_liquidfiles_app.png) 

1. <span data-ttu-id="8e60f-226">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="8e60f-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="8e60f-228">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="8e60f-228">Click **Add** button.</span></span> <span data-ttu-id="8e60f-229">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8e60f-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="8e60f-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="8e60f-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="8e60f-232">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="8e60f-232">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="8e60f-233">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8e60f-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8e60f-234">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="8e60f-234">Testing single sign-on</span></span>

<span data-ttu-id="8e60f-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8e60f-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8e60f-236">When you click the LiquidFiles tile in the Access Panel, you should get automatically signed-on to your LiquidFiles application.</span><span class="sxs-lookup"><span data-stu-id="8e60f-236">When you click the LiquidFiles tile in the Access Panel, you should get automatically signed-on to your LiquidFiles application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8e60f-237">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8e60f-237">Additional resources</span></span>

* [<span data-ttu-id="8e60f-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e60f-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="8e60f-239">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8e60f-239">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/liquidfiles-tutorial/tutorial_general_01.png
[2]: ./media/liquidfiles-tutorial/tutorial_general_02.png
[3]: ./media/liquidfiles-tutorial/tutorial_general_03.png
[4]: ./media/liquidfiles-tutorial/tutorial_general_04.png

[100]: ./media/liquidfiles-tutorial/tutorial_general_100.png

[200]: ./media/liquidfiles-tutorial/tutorial_general_200.png
[201]: ./media/liquidfiles-tutorial/tutorial_general_201.png
[202]: ./media/liquidfiles-tutorial/tutorial_general_202.png
[203]: ./media/liquidfiles-tutorial/tutorial_general_203.png

