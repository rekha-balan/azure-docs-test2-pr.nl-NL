---
title: 'Tutorial: Azure Active Directory integration with Workfront | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Workfront.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 155aa8ac1ee01ba46297e66763e0c0501ead32e2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866160"
---
# <a name="tutorial-azure-active-directory-integration-with-workfront"></a><span data-ttu-id="88992-103">Tutorial: Azure Active Directory integration with Workfront</span><span class="sxs-lookup"><span data-stu-id="88992-103">Tutorial: Azure Active Directory integration with Workfront</span></span>

<span data-ttu-id="88992-104">In this tutorial, you learn how to integrate Workfront with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88992-104">In this tutorial, you learn how to integrate Workfront with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="88992-105">Integrating Workfront with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="88992-105">Integrating Workfront with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="88992-106">You can control in Azure AD who has access to Workfront</span><span class="sxs-lookup"><span data-stu-id="88992-106">You can control in Azure AD who has access to Workfront</span></span>
- <span data-ttu-id="88992-107">You can enable your users to automatically get signed-on to Workfront (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="88992-107">You can enable your users to automatically get signed-on to Workfront (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="88992-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="88992-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="88992-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="88992-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88992-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="88992-110">Prerequisites</span></span>

<span data-ttu-id="88992-111">To configure Azure AD integration with Workfront, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="88992-111">To configure Azure AD integration with Workfront, you need the following items:</span></span>

- <span data-ttu-id="88992-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="88992-112">An Azure AD subscription</span></span>
- <span data-ttu-id="88992-113">A Workfront single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="88992-113">A Workfront single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="88992-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="88992-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="88992-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="88992-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="88992-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="88992-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="88992-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88992-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="88992-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="88992-118">Scenario description</span></span>
<span data-ttu-id="88992-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="88992-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="88992-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="88992-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="88992-121">Adding Workfront from the gallery</span><span class="sxs-lookup"><span data-stu-id="88992-121">Adding Workfront from the gallery</span></span>
1. <span data-ttu-id="88992-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="88992-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workfront-from-the-gallery"></a><span data-ttu-id="88992-123">Adding Workfront from the gallery</span><span class="sxs-lookup"><span data-stu-id="88992-123">Adding Workfront from the gallery</span></span>
<span data-ttu-id="88992-124">To configure the integration of Workfront into Azure AD, you need to add Workfront from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="88992-124">To configure the integration of Workfront into Azure AD, you need to add Workfront from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="88992-125">**To add Workfront from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="88992-125">**To add Workfront from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="88992-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="88992-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="88992-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="88992-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="88992-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="88992-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="88992-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="88992-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="88992-133">In the search box, type **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="88992-133">In the search box, type **Workfront**.</span></span>

    ![Creating an Azure AD test user](./media/workfront-tutorial/tutorial_workfront_search.png)

1. <span data-ttu-id="88992-135">In the results panel, select **Workfront**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="88992-135">In the results panel, select **Workfront**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/workfront-tutorial/tutorial_workfront_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="88992-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="88992-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="88992-138">In this section, you configure and test Azure AD single sign-on with Workfront based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="88992-138">In this section, you configure and test Azure AD single sign-on with Workfront based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="88992-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workfront is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88992-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workfront is to a user in Azure AD.</span></span> <span data-ttu-id="88992-140">In other words, a link relationship between an Azure AD user and the related user in Workfront needs to be established.</span><span class="sxs-lookup"><span data-stu-id="88992-140">In other words, a link relationship between an Azure AD user and the related user in Workfront needs to be established.</span></span>

<span data-ttu-id="88992-141">In Workfront, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="88992-141">In Workfront, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="88992-142">To configure and test Azure AD single sign-on with Workfront, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="88992-142">To configure and test Azure AD single sign-on with Workfront, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="88992-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="88992-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="88992-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="88992-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="88992-145">**[Creating a Workfront test user](#creating-a-workfront-test-user)** - to have a counterpart of Britta Simon in Workfront that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="88992-145">**[Creating a Workfront test user](#creating-a-workfront-test-user)** - to have a counterpart of Britta Simon in Workfront that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="88992-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="88992-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="88992-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="88992-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="88992-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="88992-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="88992-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workfront application.</span><span class="sxs-lookup"><span data-stu-id="88992-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workfront application.</span></span>

<span data-ttu-id="88992-150">**To configure Azure AD single sign-on with Workfront, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="88992-150">**To configure Azure AD single sign-on with Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="88992-151">In the Azure portal, on the **Workfront** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="88992-151">In the Azure portal, on the **Workfront** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="88992-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="88992-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/workfront-tutorial/tutorial_workfront_samlbase.png)

1. <span data-ttu-id="88992-155">On the **Workfront Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="88992-155">On the **Workfront Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/workfront-tutorial/tutorial_workfront_url.png)

    <span data-ttu-id="88992-157">a.</span><span class="sxs-lookup"><span data-stu-id="88992-157">a.</span></span> <span data-ttu-id="88992-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.attask-ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="88992-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.attask-ondemand.com`</span></span>

    <span data-ttu-id="88992-159">b.</span><span class="sxs-lookup"><span data-stu-id="88992-159">b.</span></span> <span data-ttu-id="88992-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.attasksandbox.com/SAML2`</span><span class="sxs-lookup"><span data-stu-id="88992-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.attasksandbox.com/SAML2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="88992-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="88992-161">These values are not real.</span></span> <span data-ttu-id="88992-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="88992-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="88992-163">Contact [Workfront Client support team](https://www.workfront.com/services-and-support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="88992-163">Contact [Workfront Client support team](https://www.workfront.com/services-and-support) to get these values.</span></span> 
 
1. <span data-ttu-id="88992-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the Certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="88992-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the Certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/workfront-tutorial/tutorial_workfront_certificate.png) 

1. <span data-ttu-id="88992-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="88992-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/workfront-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="88992-168">On the **Workfront Configuration** section, click **Configure Workfront** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="88992-168">On the **Workfront Configuration** section, click **Configure Workfront** to open **Configure sign-on** window.</span></span> <span data-ttu-id="88992-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="88992-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/workfront-tutorial/tutorial_workfront_configure.png) 

1. <span data-ttu-id="88992-171">Sign-on to your Workfront company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="88992-171">Sign-on to your Workfront company site as administrator.</span></span>

1. <span data-ttu-id="88992-172">Go to **Single Sign On Configuration**.</span><span class="sxs-lookup"><span data-stu-id="88992-172">Go to **Single Sign On Configuration**.</span></span>

1. <span data-ttu-id="88992-173">On the **Single Sign-On** dialog, perform the following steps</span><span class="sxs-lookup"><span data-stu-id="88992-173">On the **Single Sign-On** dialog, perform the following steps</span></span>
    
    ![Configure Single Sign-On][23]
   
    <span data-ttu-id="88992-175">a.</span><span class="sxs-lookup"><span data-stu-id="88992-175">a.</span></span> <span data-ttu-id="88992-176">As **Type**, select **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="88992-176">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="88992-177">b.</span><span class="sxs-lookup"><span data-stu-id="88992-177">b.</span></span> <span data-ttu-id="88992-178">Select **Service Provider ID**.</span><span class="sxs-lookup"><span data-stu-id="88992-178">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="88992-179">c.</span><span class="sxs-lookup"><span data-stu-id="88992-179">c.</span></span> <span data-ttu-id="88992-180">Paste the **SAML Single Sign-On Service URL** into the **Login Portal URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="88992-180">Paste the **SAML Single Sign-On Service URL** into the **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="88992-181">d.</span><span class="sxs-lookup"><span data-stu-id="88992-181">d.</span></span> <span data-ttu-id="88992-182">Paste **Single Sign-Out Service URL** into the **Sign-Out URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="88992-182">Paste **Single Sign-Out Service URL** into the **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="88992-183">e.</span><span class="sxs-lookup"><span data-stu-id="88992-183">e.</span></span> <span data-ttu-id="88992-184">Paste **Change Password URL** into the **Change Password URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="88992-184">Paste **Change Password URL** into the **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="88992-185">f.</span><span class="sxs-lookup"><span data-stu-id="88992-185">f.</span></span> <span data-ttu-id="88992-186">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="88992-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="88992-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="88992-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="88992-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="88992-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="88992-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="88992-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="88992-190">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="88992-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="88992-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="88992-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="88992-193">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="88992-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="88992-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="88992-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/workfront-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="88992-196">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="88992-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/workfront-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="88992-198">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="88992-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/workfront-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="88992-200">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="88992-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/workfront-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="88992-202">a.</span><span class="sxs-lookup"><span data-stu-id="88992-202">a.</span></span> <span data-ttu-id="88992-203">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="88992-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="88992-204">b.</span><span class="sxs-lookup"><span data-stu-id="88992-204">b.</span></span> <span data-ttu-id="88992-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="88992-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="88992-206">c.</span><span class="sxs-lookup"><span data-stu-id="88992-206">c.</span></span> <span data-ttu-id="88992-207">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="88992-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="88992-208">d.</span><span class="sxs-lookup"><span data-stu-id="88992-208">d.</span></span> <span data-ttu-id="88992-209">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="88992-209">Click **Create**.</span></span>
 
### <a name="creating-a-workfront-test-user"></a><span data-ttu-id="88992-210">Creating a Workfront test user</span><span class="sxs-lookup"><span data-stu-id="88992-210">Creating a Workfront test user</span></span>

<span data-ttu-id="88992-211">The objective of this section is to create a user called Britta Simon in Workfront.</span><span class="sxs-lookup"><span data-stu-id="88992-211">The objective of this section is to create a user called Britta Simon in Workfront.</span></span>

<span data-ttu-id="88992-212">**To create a user called Britta Simon in Workfront, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="88992-212">**To create a user called Britta Simon in Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="88992-213">Sign on to your Workfront company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="88992-213">Sign on to your Workfront company site as administrator.</span></span>
1. <span data-ttu-id="88992-214">In the menu on the top, click **People**.</span><span class="sxs-lookup"><span data-stu-id="88992-214">In the menu on the top, click **People**.</span></span>
1. <span data-ttu-id="88992-215">Click **New Person**.</span><span class="sxs-lookup"><span data-stu-id="88992-215">Click **New Person**.</span></span> 
1. <span data-ttu-id="88992-216">On the New Person dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="88992-216">On the New Person dialog, perform the following steps:</span></span>
   
    ![Create an Workfront test user][21] 
   
    <span data-ttu-id="88992-218">a.</span><span class="sxs-lookup"><span data-stu-id="88992-218">a.</span></span> <span data-ttu-id="88992-219">In the **First Name** textbox, type "Britta."</span><span class="sxs-lookup"><span data-stu-id="88992-219">In the **First Name** textbox, type "Britta."</span></span>
   
    <span data-ttu-id="88992-220">b.</span><span class="sxs-lookup"><span data-stu-id="88992-220">b.</span></span> <span data-ttu-id="88992-221">In the **Last Name** textbox, type "Simon."</span><span class="sxs-lookup"><span data-stu-id="88992-221">In the **Last Name** textbox, type "Simon."</span></span>
   
    <span data-ttu-id="88992-222">c.</span><span class="sxs-lookup"><span data-stu-id="88992-222">c.</span></span> <span data-ttu-id="88992-223">In the **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="88992-223">In the **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="88992-224">d.</span><span class="sxs-lookup"><span data-stu-id="88992-224">d.</span></span> <span data-ttu-id="88992-225">Click **Add Person**.</span><span class="sxs-lookup"><span data-stu-id="88992-225">Click **Add Person**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="88992-226">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="88992-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="88992-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workfront.</span><span class="sxs-lookup"><span data-stu-id="88992-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workfront.</span></span>

![Assign User][200] 

<span data-ttu-id="88992-229">**To assign Britta Simon to Workfront, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="88992-229">**To assign Britta Simon to Workfront, perform the following steps:**</span></span>

1. <span data-ttu-id="88992-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="88992-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="88992-232">In the applications list, select **Workfront**.</span><span class="sxs-lookup"><span data-stu-id="88992-232">In the applications list, select **Workfront**.</span></span>

    ![Configure Single Sign-On](./media/workfront-tutorial/tutorial_workfront_app.png) 

1. <span data-ttu-id="88992-234">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="88992-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="88992-236">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="88992-236">Click **Add** button.</span></span> <span data-ttu-id="88992-237">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="88992-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="88992-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="88992-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="88992-240">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="88992-240">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="88992-241">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="88992-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="88992-242">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="88992-242">Testing single sign-on</span></span>

<span data-ttu-id="88992-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="88992-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="88992-244">When you click the Workfront tile in the Access Panel, you should get login page of Workfront application.</span><span class="sxs-lookup"><span data-stu-id="88992-244">When you click the Workfront tile in the Access Panel, you should get login page of Workfront application.</span></span>
<span data-ttu-id="88992-245">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="88992-245">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="88992-246">Additional resources</span><span class="sxs-lookup"><span data-stu-id="88992-246">Additional resources</span></span>

* [<span data-ttu-id="88992-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88992-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="88992-248">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="88992-248">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/workfront-tutorial/tutorial_general_01.png
[2]: ./media/workfront-tutorial/tutorial_general_02.png
[3]: ./media/workfront-tutorial/tutorial_general_03.png
[4]: ./media/workfront-tutorial/tutorial_general_04.png
[21]:./media/workfront-tutorial/tutorial_attask_08.png
[23]:./media/workfront-tutorial/tutorial_attask_06.png
[100]: ./media/workfront-tutorial/tutorial_general_100.png

[200]: ./media/workfront-tutorial/tutorial_general_200.png
[201]: ./media/workfront-tutorial/tutorial_general_201.png
[202]: ./media/workfront-tutorial/tutorial_general_202.png
[203]: ./media/workfront-tutorial/tutorial_general_203.png

