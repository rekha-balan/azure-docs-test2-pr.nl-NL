---
title: 'Tutorial: Azure Active Directory integration with Canvas Lms | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Canvas LMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: af2c997f0842da751eb93f0788a7402fc7d144ae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867199"
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a><span data-ttu-id="2f15e-103">Tutorial: Azure Active Directory integration with Canvas LMS</span><span class="sxs-lookup"><span data-stu-id="2f15e-103">Tutorial: Azure Active Directory integration with Canvas LMS</span></span>

<span data-ttu-id="2f15e-104">In this tutorial, you learn how to integrate Canvas with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2f15e-104">In this tutorial, you learn how to integrate Canvas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2f15e-105">Integrating Canvas with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="2f15e-105">Integrating Canvas with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2f15e-106">You can control in Azure AD who has access to Canvas</span><span class="sxs-lookup"><span data-stu-id="2f15e-106">You can control in Azure AD who has access to Canvas</span></span>
- <span data-ttu-id="2f15e-107">You can enable your users to automatically get signed-on to Canvas (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="2f15e-107">You can enable your users to automatically get signed-on to Canvas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2f15e-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="2f15e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2f15e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="2f15e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f15e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2f15e-110">Prerequisites</span></span>

<span data-ttu-id="2f15e-111">To configure Azure AD integration with Canvas, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="2f15e-111">To configure Azure AD integration with Canvas, you need the following items:</span></span>

- <span data-ttu-id="2f15e-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="2f15e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2f15e-113">A Canvas single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="2f15e-113">A Canvas single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2f15e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="2f15e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2f15e-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="2f15e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2f15e-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="2f15e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2f15e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f15e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2f15e-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="2f15e-118">Scenario description</span></span>
<span data-ttu-id="2f15e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="2f15e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2f15e-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="2f15e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2f15e-121">Adding Canvas from the gallery</span><span class="sxs-lookup"><span data-stu-id="2f15e-121">Adding Canvas from the gallery</span></span>
1. <span data-ttu-id="2f15e-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2f15e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-canvas-from-the-gallery"></a><span data-ttu-id="2f15e-123">Adding Canvas from the gallery</span><span class="sxs-lookup"><span data-stu-id="2f15e-123">Adding Canvas from the gallery</span></span>
<span data-ttu-id="2f15e-124">To configure the integration of Canvas into Azure AD, you need to add Canvas from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="2f15e-124">To configure the integration of Canvas into Azure AD, you need to add Canvas from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2f15e-125">**To add Canvas from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2f15e-125">**To add Canvas from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2f15e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="2f15e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="2f15e-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2f15e-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="2f15e-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="2f15e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="2f15e-133">In the search box, type **Canvas**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-133">In the search box, type **Canvas**.</span></span>

    ![Creating an Azure AD test user](./media/canvas-lms-tutorial/tutorial_canvaslms_search.png)

1. <span data-ttu-id="2f15e-135">In the results panel, select **Canvas**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="2f15e-135">In the results panel, select **Canvas**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2f15e-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2f15e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2f15e-138">In this section, you configure and test Azure AD single sign-on with Canvas based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="2f15e-138">In this section, you configure and test Azure AD single sign-on with Canvas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2f15e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Canvas is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f15e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Canvas is to a user in Azure AD.</span></span> <span data-ttu-id="2f15e-140">In other words, a link relationship between an Azure AD user and the related user in Canvas needs to be established.</span><span class="sxs-lookup"><span data-stu-id="2f15e-140">In other words, a link relationship between an Azure AD user and the related user in Canvas needs to be established.</span></span>

<span data-ttu-id="2f15e-141">In Canvas, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="2f15e-141">In Canvas, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2f15e-142">To configure and test Azure AD single sign-on with Canvas, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="2f15e-142">To configure and test Azure AD single sign-on with Canvas, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2f15e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="2f15e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="2f15e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2f15e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="2f15e-145">**[Creating a Canvas test user](#creating-a-canvas-test-user)** - to have a counterpart of Britta Simon in Canvas that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="2f15e-145">**[Creating a Canvas test user](#creating-a-canvas-test-user)** - to have a counterpart of Britta Simon in Canvas that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="2f15e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2f15e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="2f15e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="2f15e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2f15e-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2f15e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2f15e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Canvas application.</span><span class="sxs-lookup"><span data-stu-id="2f15e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Canvas application.</span></span>

<span data-ttu-id="2f15e-150">**To configure Azure AD single sign-on with Canvas, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2f15e-150">**To configure Azure AD single sign-on with Canvas, perform the following steps:**</span></span>

1. <span data-ttu-id="2f15e-151">In the Azure portal, on the **Canvas** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-151">In the Azure portal, on the **Canvas** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="2f15e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2f15e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

1. <span data-ttu-id="2f15e-155">On the **Canvas Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2f15e-155">On the **Canvas Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/canvas-lms-tutorial/tutorial_canvaslms_url.png)

    <span data-ttu-id="2f15e-157">a.</span><span class="sxs-lookup"><span data-stu-id="2f15e-157">a.</span></span> <span data-ttu-id="2f15e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.instructure.com`</span><span class="sxs-lookup"><span data-stu-id="2f15e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.instructure.com`</span></span>

    <span data-ttu-id="2f15e-159">b.</span><span class="sxs-lookup"><span data-stu-id="2f15e-159">b.</span></span> <span data-ttu-id="2f15e-160">In the **Identifier** textbox, type the value using the following pattern: `https://<tenant-name>.instructure.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="2f15e-160">In the **Identifier** textbox, type the value using the following pattern: `https://<tenant-name>.instructure.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2f15e-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="2f15e-161">These values are not real.</span></span> <span data-ttu-id="2f15e-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="2f15e-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2f15e-163">Contact [Canvas Client support team](https://community.canvaslms.com/community/help) to get these values.</span><span class="sxs-lookup"><span data-stu-id="2f15e-163">Contact [Canvas Client support team](https://community.canvaslms.com/community/help) to get these values.</span></span> 
 
1. <span data-ttu-id="2f15e-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span><span class="sxs-lookup"><span data-stu-id="2f15e-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Configure Single Sign-On](./media/canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

1. <span data-ttu-id="2f15e-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="2f15e-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/canvas-lms-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="2f15e-168">On the **Canvas Configuration** section, click **Configure Canvas** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="2f15e-168">On the **Canvas Configuration** section, click **Configure Canvas** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2f15e-169">Copy the **Change Password URL, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="2f15e-169">Copy the **Change Password URL, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
1. <span data-ttu-id="2f15e-171">In a different web browser window, log in to your Canvas company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="2f15e-171">In a different web browser window, log in to your Canvas company site as an administrator.</span></span>

1. <span data-ttu-id="2f15e-172">Go to **Courses \> Managed Accounts \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-172">Go to **Courses \> Managed Accounts \> Microsoft**.</span></span>
   
    <span data-ttu-id="2f15e-173">![Canvas](./media/canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="2f15e-173">![Canvas](./media/canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

1. <span data-ttu-id="2f15e-174">In the navigation pane on the left, select **Authentication**, and then click **Add New SAML Config**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-174">In the navigation pane on the left, select **Authentication**, and then click **Add New SAML Config**.</span></span>
   
    <span data-ttu-id="2f15e-175">![Authentication](./media/canvas-lms-tutorial/IC775991.png "Authentication")</span><span class="sxs-lookup"><span data-stu-id="2f15e-175">![Authentication](./media/canvas-lms-tutorial/IC775991.png "Authentication")</span></span>

1. <span data-ttu-id="2f15e-176">On the Current Integration page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2f15e-176">On the Current Integration page, perform the following steps:</span></span>
   
    <span data-ttu-id="2f15e-177">![Current Integration](./media/canvas-lms-tutorial/IC775992.png "Current Integration")</span><span class="sxs-lookup"><span data-stu-id="2f15e-177">![Current Integration](./media/canvas-lms-tutorial/IC775992.png "Current Integration")</span></span>

    <span data-ttu-id="2f15e-178">a.</span><span class="sxs-lookup"><span data-stu-id="2f15e-178">a.</span></span> <span data-ttu-id="2f15e-179">In **IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2f15e-179">In **IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2f15e-180">b.</span><span class="sxs-lookup"><span data-stu-id="2f15e-180">b.</span></span> <span data-ttu-id="2f15e-181">In **Log On URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal .</span><span class="sxs-lookup"><span data-stu-id="2f15e-181">In **Log On URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal .</span></span>

    <span data-ttu-id="2f15e-182">c.</span><span class="sxs-lookup"><span data-stu-id="2f15e-182">c.</span></span> <span data-ttu-id="2f15e-183">In **Log Out URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2f15e-183">In **Log Out URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2f15e-184">d.</span><span class="sxs-lookup"><span data-stu-id="2f15e-184">d.</span></span> <span data-ttu-id="2f15e-185">In **Change Password Link** textbox, paste the value of **Change Password URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2f15e-185">In **Change Password Link** textbox, paste the value of **Change Password URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="2f15e-186">e.</span><span class="sxs-lookup"><span data-stu-id="2f15e-186">e.</span></span> <span data-ttu-id="2f15e-187">In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2f15e-187">In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>      
        
    <span data-ttu-id="2f15e-188">f.</span><span class="sxs-lookup"><span data-stu-id="2f15e-188">f.</span></span> <span data-ttu-id="2f15e-189">From the **Login Attribute** list, select **NameID**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-189">From the **Login Attribute** list, select **NameID**.</span></span>

    <span data-ttu-id="2f15e-190">g.</span><span class="sxs-lookup"><span data-stu-id="2f15e-190">g.</span></span> <span data-ttu-id="2f15e-191">From the **Identifier Format** list, select **emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-191">From the **Identifier Format** list, select **emailAddress**.</span></span>

    <span data-ttu-id="2f15e-192">h.</span><span class="sxs-lookup"><span data-stu-id="2f15e-192">h.</span></span> <span data-ttu-id="2f15e-193">Click **Save Authentication Settings**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-193">Click **Save Authentication Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="2f15e-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="2f15e-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2f15e-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="2f15e-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2f15e-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2f15e-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2f15e-197">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2f15e-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="2f15e-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2f15e-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="2f15e-200">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2f15e-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2f15e-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="2f15e-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/canvas-lms-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="2f15e-203">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/canvas-lms-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="2f15e-205">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="2f15e-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/canvas-lms-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="2f15e-207">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2f15e-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/canvas-lms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2f15e-209">a.</span><span class="sxs-lookup"><span data-stu-id="2f15e-209">a.</span></span> <span data-ttu-id="2f15e-210">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2f15e-211">b.</span><span class="sxs-lookup"><span data-stu-id="2f15e-211">b.</span></span> <span data-ttu-id="2f15e-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2f15e-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2f15e-213">c.</span><span class="sxs-lookup"><span data-stu-id="2f15e-213">c.</span></span> <span data-ttu-id="2f15e-214">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2f15e-215">d.</span><span class="sxs-lookup"><span data-stu-id="2f15e-215">d.</span></span> <span data-ttu-id="2f15e-216">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-216">Click **Create**.</span></span>
 
### <a name="creating-a-canvas-test-user"></a><span data-ttu-id="2f15e-217">Creating a Canvas test user</span><span class="sxs-lookup"><span data-stu-id="2f15e-217">Creating a Canvas test user</span></span>

<span data-ttu-id="2f15e-218">To enable Azure AD users to log in to Canvas, they must be provisioned into Canvas.</span><span class="sxs-lookup"><span data-stu-id="2f15e-218">To enable Azure AD users to log in to Canvas, they must be provisioned into Canvas.</span></span>

<span data-ttu-id="2f15e-219">In case of Canvas, user provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="2f15e-219">In case of Canvas, user provisioning is a manual task.</span></span>

<span data-ttu-id="2f15e-220">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2f15e-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="2f15e-221">Log in to your **Canvas** tenant.</span><span class="sxs-lookup"><span data-stu-id="2f15e-221">Log in to your **Canvas** tenant.</span></span>

1. <span data-ttu-id="2f15e-222">Go to **Courses \> Managed Accounts \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-222">Go to **Courses \> Managed Accounts \> Microsoft**.</span></span>
   
   <span data-ttu-id="2f15e-223">![Canvas](./media/canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="2f15e-223">![Canvas](./media/canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

1. <span data-ttu-id="2f15e-224">Click **Users**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-224">Click **Users**.</span></span>
   
   <span data-ttu-id="2f15e-225">![Users](./media/canvas-lms-tutorial/IC775995.png "Users")</span><span class="sxs-lookup"><span data-stu-id="2f15e-225">![Users](./media/canvas-lms-tutorial/IC775995.png "Users")</span></span>

1. <span data-ttu-id="2f15e-226">Click **Add New User**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-226">Click **Add New User**.</span></span>
   
   <span data-ttu-id="2f15e-227">![Users](./media/canvas-lms-tutorial/IC775996.png "Users")</span><span class="sxs-lookup"><span data-stu-id="2f15e-227">![Users](./media/canvas-lms-tutorial/IC775996.png "Users")</span></span>

1. <span data-ttu-id="2f15e-228">On the Add a New User dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2f15e-228">On the Add a New User dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="2f15e-229">![Add User](./media/canvas-lms-tutorial/IC775997.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="2f15e-229">![Add User](./media/canvas-lms-tutorial/IC775997.png "Add User")</span></span>
   
   <span data-ttu-id="2f15e-230">a.</span><span class="sxs-lookup"><span data-stu-id="2f15e-230">a.</span></span> <span data-ttu-id="2f15e-231">In the **Full Name** textbox, enter the name of user like **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-231">In the **Full Name** textbox, enter the name of user like **BrittaSimon**.</span></span>

   <span data-ttu-id="2f15e-232">b.</span><span class="sxs-lookup"><span data-stu-id="2f15e-232">b.</span></span> <span data-ttu-id="2f15e-233">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-233">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="2f15e-234">c.</span><span class="sxs-lookup"><span data-stu-id="2f15e-234">c.</span></span> <span data-ttu-id="2f15e-235">In the **Login** textbox, enter the user’s Azure AD email address like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-235">In the **Login** textbox, enter the user’s Azure AD email address like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="2f15e-236">d.</span><span class="sxs-lookup"><span data-stu-id="2f15e-236">d.</span></span> <span data-ttu-id="2f15e-237">Select **Email the user about this account creation**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-237">Select **Email the user about this account creation**.</span></span>

   <span data-ttu-id="2f15e-238">e.</span><span class="sxs-lookup"><span data-stu-id="2f15e-238">e.</span></span> <span data-ttu-id="2f15e-239">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-239">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="2f15e-240">You can use any other Canvas user account creation tools or APIs provided by Canvas to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="2f15e-240">You can use any other Canvas user account creation tools or APIs provided by Canvas to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2f15e-241">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2f15e-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2f15e-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Canvas.</span><span class="sxs-lookup"><span data-stu-id="2f15e-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Canvas.</span></span>

![Assign User][200] 

<span data-ttu-id="2f15e-244">**To assign Britta Simon to Canvas, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2f15e-244">**To assign Britta Simon to Canvas, perform the following steps:**</span></span>

1. <span data-ttu-id="2f15e-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="2f15e-247">In the applications list, select **Canvas**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-247">In the applications list, select **Canvas**.</span></span>

    ![Configure Single Sign-On](./media/canvas-lms-tutorial/tutorial_canvaslms_app.png) 

1. <span data-ttu-id="2f15e-249">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="2f15e-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="2f15e-251">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="2f15e-251">Click **Add** button.</span></span> <span data-ttu-id="2f15e-252">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2f15e-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="2f15e-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="2f15e-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="2f15e-255">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="2f15e-255">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="2f15e-256">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2f15e-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2f15e-257">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="2f15e-257">Testing single sign-on</span></span>

<span data-ttu-id="2f15e-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="2f15e-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2f15e-259">When you click the Canvas tile in the Access Panel, you should get automatically signed-on to your Canvas application.</span><span class="sxs-lookup"><span data-stu-id="2f15e-259">When you click the Canvas tile in the Access Panel, you should get automatically signed-on to your Canvas application.</span></span>
<span data-ttu-id="2f15e-260">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2f15e-260">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2f15e-261">Additional resources</span><span class="sxs-lookup"><span data-stu-id="2f15e-261">Additional resources</span></span>

* [<span data-ttu-id="2f15e-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2f15e-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="2f15e-263">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2f15e-263">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/canvas-lms-tutorial/tutorial_general_203.png

