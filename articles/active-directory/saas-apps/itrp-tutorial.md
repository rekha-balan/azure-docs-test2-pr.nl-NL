---
title: 'Tutorial: Azure Active Directory integration with ITRP | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ITRP.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: e09716a3-4200-4853-9414-2390e6c10d98
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 0af96b750c7e316d1d394a00781f727358f2c4e8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867383"
---
# <a name="tutorial-azure-active-directory-integration-with-itrp"></a><span data-ttu-id="60036-103">Tutorial: Azure Active Directory integration with ITRP</span><span class="sxs-lookup"><span data-stu-id="60036-103">Tutorial: Azure Active Directory integration with ITRP</span></span>

<span data-ttu-id="60036-104">In this tutorial, you learn how to integrate ITRP with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="60036-104">In this tutorial, you learn how to integrate ITRP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="60036-105">Integrating ITRP with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="60036-105">Integrating ITRP with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="60036-106">You can control in Azure AD who has access to ITRP</span><span class="sxs-lookup"><span data-stu-id="60036-106">You can control in Azure AD who has access to ITRP</span></span>
- <span data-ttu-id="60036-107">You can enable your users to automatically get signed-on to ITRP (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="60036-107">You can enable your users to automatically get signed-on to ITRP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="60036-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="60036-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="60036-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="60036-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60036-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="60036-110">Prerequisites</span></span>

<span data-ttu-id="60036-111">To configure Azure AD integration with ITRP, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="60036-111">To configure Azure AD integration with ITRP, you need the following items:</span></span>

- <span data-ttu-id="60036-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="60036-112">An Azure AD subscription</span></span>
- <span data-ttu-id="60036-113">An ITRP single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="60036-113">An ITRP single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="60036-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="60036-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="60036-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="60036-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="60036-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="60036-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="60036-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="60036-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="60036-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="60036-118">Scenario description</span></span>
<span data-ttu-id="60036-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="60036-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="60036-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="60036-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="60036-121">Adding ITRP from the gallery</span><span class="sxs-lookup"><span data-stu-id="60036-121">Adding ITRP from the gallery</span></span>
1. <span data-ttu-id="60036-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="60036-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itrp-from-the-gallery"></a><span data-ttu-id="60036-123">Adding ITRP from the gallery</span><span class="sxs-lookup"><span data-stu-id="60036-123">Adding ITRP from the gallery</span></span>
<span data-ttu-id="60036-124">To configure the integration of ITRP in to Azure AD, you need to add ITRP from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="60036-124">To configure the integration of ITRP in to Azure AD, you need to add ITRP from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="60036-125">**To add ITRP from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="60036-125">**To add ITRP from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="60036-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="60036-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="60036-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="60036-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="60036-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="60036-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="60036-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="60036-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="60036-133">In the search box, type **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="60036-133">In the search box, type **ITRP**.</span></span>

    ![Creating an Azure AD test user](./media/itrp-tutorial/tutorial_itrp_search.png)

1. <span data-ttu-id="60036-135">In the results panel, select **ITRP**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="60036-135">In the results panel, select **ITRP**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/itrp-tutorial/tutorial_itrp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="60036-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="60036-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="60036-138">In this section, you configure and test Azure AD single sign-on with ITRP based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="60036-138">In this section, you configure and test Azure AD single sign-on with ITRP based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="60036-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ITRP is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60036-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ITRP is to a user in Azure AD.</span></span> <span data-ttu-id="60036-140">In other words, a link relationship between an Azure AD user and the related user in ITRP needs to be established.</span><span class="sxs-lookup"><span data-stu-id="60036-140">In other words, a link relationship between an Azure AD user and the related user in ITRP needs to be established.</span></span>

<span data-ttu-id="60036-141">In ITRP, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="60036-141">In ITRP, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="60036-142">To configure and test Azure AD single sign-on with ITRP, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="60036-142">To configure and test Azure AD single sign-on with ITRP, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="60036-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="60036-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="60036-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="60036-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="60036-145">**[Creating an ITRP test user](#creating-an-itrp-test-user)** - to have a counterpart of Britta Simon in ITRP that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="60036-145">**[Creating an ITRP test user](#creating-an-itrp-test-user)** - to have a counterpart of Britta Simon in ITRP that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="60036-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="60036-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="60036-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="60036-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="60036-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="60036-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="60036-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ITRP application.</span><span class="sxs-lookup"><span data-stu-id="60036-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ITRP application.</span></span>

<span data-ttu-id="60036-150">**To configure Azure AD single sign-on with ITRP, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="60036-150">**To configure Azure AD single sign-on with ITRP, perform the following steps:**</span></span>

1. <span data-ttu-id="60036-151">In the Azure portal, on the **ITRP** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="60036-151">In the Azure portal, on the **ITRP** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="60036-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="60036-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/itrp-tutorial/tutorial_itrp_samlbase.png)

1. <span data-ttu-id="60036-155">On the **ITRP Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="60036-155">On the **ITRP Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/itrp-tutorial/tutorial_itrp_url.png)

    <span data-ttu-id="60036-157">a.</span><span class="sxs-lookup"><span data-stu-id="60036-157">a.</span></span> <span data-ttu-id="60036-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="60036-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.itrp.com`</span></span>

    <span data-ttu-id="60036-159">b.</span><span class="sxs-lookup"><span data-stu-id="60036-159">b.</span></span> <span data-ttu-id="60036-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="60036-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.itrp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="60036-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="60036-161">These values are not real.</span></span> <span data-ttu-id="60036-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="60036-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="60036-163">Contact [ITRP Client support team](https://www.itrp.com/support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="60036-163">Contact [ITRP Client support team](https://www.itrp.com/support) to get these values.</span></span> 
 
1. <span data-ttu-id="60036-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span><span class="sxs-lookup"><span data-stu-id="60036-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Configure Single Sign-On](./media/itrp-tutorial/tutorial_itrp_certificate.png) 

1. <span data-ttu-id="60036-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="60036-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/itrp-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="60036-168">On the **ITRP Configuration** section, click **Configure ITRP** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="60036-168">On the **ITRP Configuration** section, click **Configure ITRP** to open **Configure sign-on** window.</span></span> <span data-ttu-id="60036-169">Copy the **SAML Single Sign-On Service URL and Sign-Out URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="60036-169">Copy the **SAML Single Sign-On Service URL and Sign-Out URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/itrp-tutorial/tutorial_itrp_configure.png) 

1. <span data-ttu-id="60036-171">In a different web browser window, log in to your ITRP company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="60036-171">In a different web browser window, log in to your ITRP company site as an administrator.</span></span>

1. <span data-ttu-id="60036-172">In the toolbar on the top, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="60036-172">In the toolbar on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="60036-173">![ITRP](./media/itrp-tutorial/ic775570.png "ITRP")</span><span class="sxs-lookup"><span data-stu-id="60036-173">![ITRP](./media/itrp-tutorial/ic775570.png "ITRP")</span></span>

1. <span data-ttu-id="60036-174">In the left navigation pane, select **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="60036-174">In the left navigation pane, select **Single Sign-On**.</span></span>
   
    <span data-ttu-id="60036-175">![Single Sign-On](./media/itrp-tutorial/ic775571.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="60036-175">![Single Sign-On](./media/itrp-tutorial/ic775571.png "Single Sign-On")</span></span>

1. <span data-ttu-id="60036-176">In the Single Sign-On configuration section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="60036-176">In the Single Sign-On configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="60036-177">![Single Sign-On](./media/itrp-tutorial/ic775572.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="60036-177">![Single Sign-On](./media/itrp-tutorial/ic775572.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="60036-178">![Single Sign-On](./media/itrp-tutorial/ic775573.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="60036-178">![Single Sign-On](./media/itrp-tutorial/ic775573.png "Single Sign-On")</span></span>   

    <span data-ttu-id="60036-179">a.</span><span class="sxs-lookup"><span data-stu-id="60036-179">a.</span></span> <span data-ttu-id="60036-180">Click **Enable**.</span><span class="sxs-lookup"><span data-stu-id="60036-180">Click **Enable**.</span></span>

    <span data-ttu-id="60036-181">b.</span><span class="sxs-lookup"><span data-stu-id="60036-181">b.</span></span> <span data-ttu-id="60036-182">In **Remote Log Out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="60036-182">In **Remote Log Out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="60036-183">c.</span><span class="sxs-lookup"><span data-stu-id="60036-183">c.</span></span> <span data-ttu-id="60036-184">In **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="60036-184">In **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="60036-185">d.In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="60036-185">d.In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span> 
      
1. <span data-ttu-id="60036-186">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="60036-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="60036-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="60036-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="60036-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="60036-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="60036-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="60036-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="60036-190">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="60036-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="60036-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="60036-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="60036-193">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="60036-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="60036-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="60036-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/itrp-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="60036-196">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="60036-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/itrp-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="60036-198">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="60036-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/itrp-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="60036-200">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="60036-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/itrp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="60036-202">a.</span><span class="sxs-lookup"><span data-stu-id="60036-202">a.</span></span> <span data-ttu-id="60036-203">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="60036-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="60036-204">b.</span><span class="sxs-lookup"><span data-stu-id="60036-204">b.</span></span> <span data-ttu-id="60036-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="60036-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="60036-206">c.</span><span class="sxs-lookup"><span data-stu-id="60036-206">c.</span></span> <span data-ttu-id="60036-207">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="60036-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="60036-208">d.</span><span class="sxs-lookup"><span data-stu-id="60036-208">d.</span></span> <span data-ttu-id="60036-209">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="60036-209">Click **Create**.</span></span>
 
### <a name="creating-an-itrp-test-user"></a><span data-ttu-id="60036-210">Creating an ITRP test user</span><span class="sxs-lookup"><span data-stu-id="60036-210">Creating an ITRP test user</span></span>

<span data-ttu-id="60036-211">To enable Azure AD users to log in to ITRP, they must be provisioned in to ITRP.</span><span class="sxs-lookup"><span data-stu-id="60036-211">To enable Azure AD users to log in to ITRP, they must be provisioned in to ITRP.</span></span>  

<span data-ttu-id="60036-212">In the case of ITRP, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="60036-212">In the case of ITRP, provisioning is a manual task.</span></span>

<span data-ttu-id="60036-213">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="60036-213">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="60036-214">Log in to your **ITRP** tenant.</span><span class="sxs-lookup"><span data-stu-id="60036-214">Log in to your **ITRP** tenant.</span></span>

1. <span data-ttu-id="60036-215">In the toolbar on the top, click **Records**.</span><span class="sxs-lookup"><span data-stu-id="60036-215">In the toolbar on the top, click **Records**.</span></span>
   
    <span data-ttu-id="60036-216">![Admin](./media/itrp-tutorial/ic775575.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="60036-216">![Admin](./media/itrp-tutorial/ic775575.png "Admin")</span></span>

1. <span data-ttu-id="60036-217">From the popup menu, select **People**.</span><span class="sxs-lookup"><span data-stu-id="60036-217">From the popup menu, select **People**.</span></span>
   
    <span data-ttu-id="60036-218">![People](./media/itrp-tutorial/ic775587.png "People")</span><span class="sxs-lookup"><span data-stu-id="60036-218">![People](./media/itrp-tutorial/ic775587.png "People")</span></span>

1. <span data-ttu-id="60036-219">Click **Add New Person** (“+”).</span><span class="sxs-lookup"><span data-stu-id="60036-219">Click **Add New Person** (“+”).</span></span>
   
    <span data-ttu-id="60036-220">![Admin](./media/itrp-tutorial/ic775576.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="60036-220">![Admin](./media/itrp-tutorial/ic775576.png "Admin")</span></span>

1. <span data-ttu-id="60036-221">On the Add New Person dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="60036-221">On the Add New Person dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="60036-222">![User](./media/itrp-tutorial/ic775577.png "User")</span><span class="sxs-lookup"><span data-stu-id="60036-222">![User](./media/itrp-tutorial/ic775577.png "User")</span></span> 
      
    <span data-ttu-id="60036-223">a.</span><span class="sxs-lookup"><span data-stu-id="60036-223">a.</span></span> <span data-ttu-id="60036-224">Type the **Name**, **Email** of a valid AAD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="60036-224">Type the **Name**, **Email** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="60036-225">b.</span><span class="sxs-lookup"><span data-stu-id="60036-225">b.</span></span> <span data-ttu-id="60036-226">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="60036-226">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="60036-227">You can use any other ITRP user account creation tools or APIs provided by ITRP to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="60036-227">You can use any other ITRP user account creation tools or APIs provided by ITRP to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="60036-228">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="60036-228">Assigning the Azure AD test user</span></span>

<span data-ttu-id="60036-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ITRP.</span><span class="sxs-lookup"><span data-stu-id="60036-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ITRP.</span></span>

![Assign User][200] 

<span data-ttu-id="60036-231">**To assign Britta Simon to ITRP, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="60036-231">**To assign Britta Simon to ITRP, perform the following steps:**</span></span>

1. <span data-ttu-id="60036-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="60036-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="60036-234">In the applications list, select **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="60036-234">In the applications list, select **ITRP**.</span></span>

    ![Configure Single Sign-On](./media/itrp-tutorial/tutorial_itrp_app.png) 

1. <span data-ttu-id="60036-236">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="60036-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="60036-238">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="60036-238">Click **Add** button.</span></span> <span data-ttu-id="60036-239">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="60036-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="60036-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="60036-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="60036-242">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="60036-242">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="60036-243">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="60036-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="60036-244">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="60036-244">Testing single sign-on</span></span>

<span data-ttu-id="60036-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="60036-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="60036-246">When you click the ITRP tile in the Access Panel, you should get automatically signed-on to your ITRP application.</span><span class="sxs-lookup"><span data-stu-id="60036-246">When you click the ITRP tile in the Access Panel, you should get automatically signed-on to your ITRP application.</span></span>
<span data-ttu-id="60036-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="60036-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="60036-248">Additional resources</span><span class="sxs-lookup"><span data-stu-id="60036-248">Additional resources</span></span>

* [<span data-ttu-id="60036-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="60036-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="60036-250">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="60036-250">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/itrp-tutorial/tutorial_general_01.png
[2]: ./media/itrp-tutorial/tutorial_general_02.png
[3]: ./media/itrp-tutorial/tutorial_general_03.png
[4]: ./media/itrp-tutorial/tutorial_general_04.png

[100]: ./media/itrp-tutorial/tutorial_general_100.png

[200]: ./media/itrp-tutorial/tutorial_general_200.png
[201]: ./media/itrp-tutorial/tutorial_general_201.png
[202]: ./media/itrp-tutorial/tutorial_general_202.png
[203]: ./media/itrp-tutorial/tutorial_general_203.png

