---
title: 'Tutorial: Azure Active Directory integration with Origami | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Origami.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 9ec165253898ec77da2c7ae0e98cab578e773094
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856888"
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a><span data-ttu-id="347f8-103">Tutorial: Azure Active Directory integration with Origami</span><span class="sxs-lookup"><span data-stu-id="347f8-103">Tutorial: Azure Active Directory integration with Origami</span></span>

<span data-ttu-id="347f8-104">In this tutorial, you learn how to integrate Origami with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="347f8-104">In this tutorial, you learn how to integrate Origami with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="347f8-105">Integrating Origami with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="347f8-105">Integrating Origami with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="347f8-106">You can control in Azure AD who has access to Origami</span><span class="sxs-lookup"><span data-stu-id="347f8-106">You can control in Azure AD who has access to Origami</span></span>
- <span data-ttu-id="347f8-107">You can enable your users to automatically get signed-on to Origami (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="347f8-107">You can enable your users to automatically get signed-on to Origami (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="347f8-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="347f8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="347f8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="347f8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="347f8-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="347f8-110">Prerequisites</span></span>

<span data-ttu-id="347f8-111">To configure Azure AD integration with Origami, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="347f8-111">To configure Azure AD integration with Origami, you need the following items:</span></span>

- <span data-ttu-id="347f8-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="347f8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="347f8-113">An Origami single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="347f8-113">An Origami single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="347f8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="347f8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="347f8-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="347f8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="347f8-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="347f8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="347f8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="347f8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="347f8-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="347f8-118">Scenario description</span></span>
<span data-ttu-id="347f8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="347f8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="347f8-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="347f8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="347f8-121">Adding Origami from the gallery</span><span class="sxs-lookup"><span data-stu-id="347f8-121">Adding Origami from the gallery</span></span>
1. <span data-ttu-id="347f8-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="347f8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-origami-from-the-gallery"></a><span data-ttu-id="347f8-123">Adding Origami from the gallery</span><span class="sxs-lookup"><span data-stu-id="347f8-123">Adding Origami from the gallery</span></span>
<span data-ttu-id="347f8-124">To configure the integration of Origami into Azure AD, you need to add Origami from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="347f8-124">To configure the integration of Origami into Azure AD, you need to add Origami from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="347f8-125">**To add Origami from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="347f8-125">**To add Origami from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="347f8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="347f8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="347f8-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="347f8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="347f8-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="347f8-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="347f8-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="347f8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="347f8-133">In the search box, type **Origami**.</span><span class="sxs-lookup"><span data-stu-id="347f8-133">In the search box, type **Origami**.</span></span>

    ![Creating an Azure AD test user](./media/origami-tutorial/tutorial_origami_search.png)

1. <span data-ttu-id="347f8-135">In the results panel, select **Origami**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="347f8-135">In the results panel, select **Origami**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="347f8-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="347f8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="347f8-138">In this section, you configure and test Azure AD single sign-on with Origami based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="347f8-138">In this section, you configure and test Azure AD single sign-on with Origami based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="347f8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Origami is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="347f8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Origami is to a user in Azure AD.</span></span> <span data-ttu-id="347f8-140">In other words, a link relationship between an Azure AD user and the related user in Origami needs to be established.</span><span class="sxs-lookup"><span data-stu-id="347f8-140">In other words, a link relationship between an Azure AD user and the related user in Origami needs to be established.</span></span>

<span data-ttu-id="347f8-141">In Origami, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="347f8-141">In Origami, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="347f8-142">To configure and test Azure AD single sign-on with Origami, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="347f8-142">To configure and test Azure AD single sign-on with Origami, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="347f8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="347f8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="347f8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="347f8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="347f8-145">**[Creating an Origami test user](#creating-an-origami-test-user)** - to have a counterpart of Britta Simon in Origami that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="347f8-145">**[Creating an Origami test user](#creating-an-origami-test-user)** - to have a counterpart of Britta Simon in Origami that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="347f8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="347f8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="347f8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="347f8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="347f8-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="347f8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="347f8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Origami application.</span><span class="sxs-lookup"><span data-stu-id="347f8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Origami application.</span></span>

<span data-ttu-id="347f8-150">**To configure Azure AD single sign-on with Origami, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="347f8-150">**To configure Azure AD single sign-on with Origami, perform the following steps:**</span></span>

1. <span data-ttu-id="347f8-151">In the Azure portal, on the **Origami** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="347f8-151">In the Azure portal, on the **Origami** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="347f8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="347f8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/origami-tutorial/tutorial_origami_samlbase.png)

1. <span data-ttu-id="347f8-155">On the **Origami Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="347f8-155">On the **Origami Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/origami-tutorial/tutorial_origami_url.png)

    <span data-ttu-id="347f8-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span><span class="sxs-lookup"><span data-stu-id="347f8-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="347f8-158">The value is not real.</span><span class="sxs-lookup"><span data-stu-id="347f8-158">The value is not real.</span></span> <span data-ttu-id="347f8-159">Update the value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="347f8-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="347f8-160">Contact [Origami Client support team](https://wordpress.org/support/theme/origami) to get the value.</span><span class="sxs-lookup"><span data-stu-id="347f8-160">Contact [Origami Client support team](https://wordpress.org/support/theme/origami) to get the value.</span></span> 
 
1. <span data-ttu-id="347f8-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="347f8-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/origami-tutorial/tutorial_origami_certificate.png) 

1. <span data-ttu-id="347f8-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="347f8-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/origami-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="347f8-165">On the **Origami Configuration** section, click **Configure Origami** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="347f8-165">On the **Origami Configuration** section, click **Configure Origami** to open **Configure sign-on** window.</span></span> <span data-ttu-id="347f8-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="347f8-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/origami-tutorial/tutorial_origami_configure.png) 

1. <span data-ttu-id="347f8-168">Log in to the Origami account with Admin rights.</span><span class="sxs-lookup"><span data-stu-id="347f8-168">Log in to the Origami account with Admin rights.</span></span>

1. <span data-ttu-id="347f8-169">In the menu on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="347f8-169">In the menu on the top, click **Admin**.</span></span>
   
    ![Configure Single Sign-On](./media/origami-tutorial/tutorial_origami_51.png)

1. <span data-ttu-id="347f8-171">On the Single Sign On Setup dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="347f8-171">On the Single Sign On Setup dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](./media/origami-tutorial/tutorial_origami_531.png)

    <span data-ttu-id="347f8-173">a.</span><span class="sxs-lookup"><span data-stu-id="347f8-173">a.</span></span> <span data-ttu-id="347f8-174">Select **Enable Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="347f8-174">Select **Enable Single Sign On**.</span></span>

    <span data-ttu-id="347f8-175">b.</span><span class="sxs-lookup"><span data-stu-id="347f8-175">b.</span></span> <span data-ttu-id="347f8-176">In the **Identity Provider's Sign-in Page URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="347f8-176">In the **Identity Provider's Sign-in Page URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="347f8-177">c.</span><span class="sxs-lookup"><span data-stu-id="347f8-177">c.</span></span> <span data-ttu-id="347f8-178">In the **Identity Provider's Sign-out Page URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="347f8-178">In the **Identity Provider's Sign-out Page URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="347f8-179">d.</span><span class="sxs-lookup"><span data-stu-id="347f8-179">d.</span></span> <span data-ttu-id="347f8-180">Click **Browse** to upload the certificate you have downloaded from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="347f8-180">Click **Browse** to upload the certificate you have downloaded from the Azure portal.</span></span>

    <span data-ttu-id="347f8-181">e.</span><span class="sxs-lookup"><span data-stu-id="347f8-181">e.</span></span> <span data-ttu-id="347f8-182">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="347f8-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="347f8-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="347f8-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="347f8-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="347f8-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="347f8-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="347f8-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="347f8-186">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="347f8-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="347f8-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="347f8-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="347f8-189">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="347f8-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="347f8-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="347f8-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/origami-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="347f8-192">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="347f8-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/origami-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="347f8-194">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="347f8-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/origami-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="347f8-196">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="347f8-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/origami-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="347f8-198">a.</span><span class="sxs-lookup"><span data-stu-id="347f8-198">a.</span></span> <span data-ttu-id="347f8-199">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="347f8-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="347f8-200">b.</span><span class="sxs-lookup"><span data-stu-id="347f8-200">b.</span></span> <span data-ttu-id="347f8-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="347f8-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="347f8-202">c.</span><span class="sxs-lookup"><span data-stu-id="347f8-202">c.</span></span> <span data-ttu-id="347f8-203">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="347f8-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="347f8-204">d.</span><span class="sxs-lookup"><span data-stu-id="347f8-204">d.</span></span> <span data-ttu-id="347f8-205">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="347f8-205">Click **Create**.</span></span>
 
### <a name="creating-an-origami-test-user"></a><span data-ttu-id="347f8-206">Creating an Origami test user</span><span class="sxs-lookup"><span data-stu-id="347f8-206">Creating an Origami test user</span></span>

<span data-ttu-id="347f8-207">In this section, you create a user called Britta Simon in Origami.</span><span class="sxs-lookup"><span data-stu-id="347f8-207">In this section, you create a user called Britta Simon in Origami.</span></span> 

1. <span data-ttu-id="347f8-208">Log in to the Origami account with Admin rights.</span><span class="sxs-lookup"><span data-stu-id="347f8-208">Log in to the Origami account with Admin rights.</span></span>

1. <span data-ttu-id="347f8-209">In the menu on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="347f8-209">In the menu on the top, click **Admin**.</span></span>
   
    ![Configure Single Sign-On](./media/origami-tutorial/tutorial_origami_51.png)

1. <span data-ttu-id="347f8-211">On the **Users and Security** dialog, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="347f8-211">On the **Users and Security** dialog, click **Users**.</span></span>
   
    ![Configure Single Sign-On](./media/origami-tutorial/tutorial_origami_54.png)

1. <span data-ttu-id="347f8-213">Click **Add New User**.</span><span class="sxs-lookup"><span data-stu-id="347f8-213">Click **Add New User**.</span></span>
   
    ![Configure Single Sign-On](./media/origami-tutorial/tutorial_origami_55.png)

1. <span data-ttu-id="347f8-215">On the Add New User dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="347f8-215">On the Add New User dialog, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](./media/origami-tutorial/tutorial_origami_56.png)

    <span data-ttu-id="347f8-217">a.</span><span class="sxs-lookup"><span data-stu-id="347f8-217">a.</span></span> <span data-ttu-id="347f8-218">In the **User Name** textbox, enter the email of user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="347f8-218">In the **User Name** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="347f8-219">b.</span><span class="sxs-lookup"><span data-stu-id="347f8-219">b.</span></span> <span data-ttu-id="347f8-220">In the **Password** textbox, type a password.</span><span class="sxs-lookup"><span data-stu-id="347f8-220">In the **Password** textbox, type a password.</span></span>

    <span data-ttu-id="347f8-221">c.</span><span class="sxs-lookup"><span data-stu-id="347f8-221">c.</span></span> <span data-ttu-id="347f8-222">In the **Confirm Password** textbox, type the password again.</span><span class="sxs-lookup"><span data-stu-id="347f8-222">In the **Confirm Password** textbox, type the password again.</span></span>

    <span data-ttu-id="347f8-223">d.</span><span class="sxs-lookup"><span data-stu-id="347f8-223">d.</span></span> <span data-ttu-id="347f8-224">In the **First Name** textbox, enter the first name of user like **Britta**.</span><span class="sxs-lookup"><span data-stu-id="347f8-224">In the **First Name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="347f8-225">e.</span><span class="sxs-lookup"><span data-stu-id="347f8-225">e.</span></span> <span data-ttu-id="347f8-226">In the **Last Name** textbox, enter the last name of user like **Simon**.</span><span class="sxs-lookup"><span data-stu-id="347f8-226">In the **Last Name** textbox, enter the last name of user like **Simon**.</span></span>

    <span data-ttu-id="347f8-227">f.</span><span class="sxs-lookup"><span data-stu-id="347f8-227">f.</span></span> <span data-ttu-id="347f8-228">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="347f8-228">Click **Save**.</span></span>
   
    ![Configure Single Sign-On](./media/origami-tutorial/tutorial_origami_57.png)

1. <span data-ttu-id="347f8-230">Assign **User Roles** and **Client Access** to the user.</span><span class="sxs-lookup"><span data-stu-id="347f8-230">Assign **User Roles** and **Client Access** to the user.</span></span> 
   
    ![Configure Single Sign-On](./media/origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="347f8-232">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="347f8-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="347f8-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Origami.</span><span class="sxs-lookup"><span data-stu-id="347f8-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Origami.</span></span>

![Assign User][200] 

<span data-ttu-id="347f8-235">**To assign Britta Simon to Origami, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="347f8-235">**To assign Britta Simon to Origami, perform the following steps:**</span></span>

1. <span data-ttu-id="347f8-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="347f8-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="347f8-238">In the applications list, select **Origami**.</span><span class="sxs-lookup"><span data-stu-id="347f8-238">In the applications list, select **Origami**.</span></span>

    ![Configure Single Sign-On](./media/origami-tutorial/tutorial_origami_app.png) 

1. <span data-ttu-id="347f8-240">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="347f8-240">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="347f8-242">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="347f8-242">Click **Add** button.</span></span> <span data-ttu-id="347f8-243">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="347f8-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="347f8-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="347f8-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="347f8-246">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="347f8-246">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="347f8-247">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="347f8-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="347f8-248">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="347f8-248">Testing single sign-on</span></span>

<span data-ttu-id="347f8-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="347f8-249">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="347f8-250">When you click the Origami tile in the Access Panel, you should get automatically signed-on to your Origami application.</span><span class="sxs-lookup"><span data-stu-id="347f8-250">When you click the Origami tile in the Access Panel, you should get automatically signed-on to your Origami application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="347f8-251">Additional resources</span><span class="sxs-lookup"><span data-stu-id="347f8-251">Additional resources</span></span>

* [<span data-ttu-id="347f8-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="347f8-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="347f8-253">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="347f8-253">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/origami-tutorial/tutorial_general_01.png
[2]: ./media/origami-tutorial/tutorial_general_02.png
[3]: ./media/origami-tutorial/tutorial_general_03.png
[4]: ./media/origami-tutorial/tutorial_general_04.png

[100]: ./media/origami-tutorial/tutorial_general_100.png

[200]: ./media/origami-tutorial/tutorial_general_200.png
[201]: ./media/origami-tutorial/tutorial_general_201.png
[202]: ./media/origami-tutorial/tutorial_general_202.png
[203]: ./media/origami-tutorial/tutorial_general_203.png

