---
title: 'Tutorial: Azure Active Directory integration with LearnUpon | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and LearnUpon.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 27d7949be97dc9f64f3c0855f4f7b936312bf7a8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867596"
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a><span data-ttu-id="dc978-103">Tutorial: Azure Active Directory integration with LearnUpon</span><span class="sxs-lookup"><span data-stu-id="dc978-103">Tutorial: Azure Active Directory integration with LearnUpon</span></span>

<span data-ttu-id="dc978-104">In this tutorial, you learn how to integrate LearnUpon with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dc978-104">In this tutorial, you learn how to integrate LearnUpon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dc978-105">Integrating LearnUpon with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="dc978-105">Integrating LearnUpon with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dc978-106">You can control in Azure AD who has access to LearnUpon</span><span class="sxs-lookup"><span data-stu-id="dc978-106">You can control in Azure AD who has access to LearnUpon</span></span>
- <span data-ttu-id="dc978-107">You can enable your users to automatically get signed-on to LearnUpon (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="dc978-107">You can enable your users to automatically get signed-on to LearnUpon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dc978-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="dc978-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dc978-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="dc978-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc978-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dc978-110">Prerequisites</span></span>

<span data-ttu-id="dc978-111">To configure Azure AD integration with LearnUpon, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="dc978-111">To configure Azure AD integration with LearnUpon, you need the following items:</span></span>

- <span data-ttu-id="dc978-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="dc978-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dc978-113">A LearnUpon single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="dc978-113">A LearnUpon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dc978-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="dc978-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dc978-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="dc978-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dc978-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="dc978-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dc978-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dc978-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dc978-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="dc978-118">Scenario description</span></span>
<span data-ttu-id="dc978-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="dc978-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dc978-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="dc978-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dc978-121">Adding LearnUpon from the gallery</span><span class="sxs-lookup"><span data-stu-id="dc978-121">Adding LearnUpon from the gallery</span></span>
1. <span data-ttu-id="dc978-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dc978-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learnupon-from-the-gallery"></a><span data-ttu-id="dc978-123">Adding LearnUpon from the gallery</span><span class="sxs-lookup"><span data-stu-id="dc978-123">Adding LearnUpon from the gallery</span></span>
<span data-ttu-id="dc978-124">To configure the integration of LearnUpon into Azure AD, you need to add LearnUpon from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="dc978-124">To configure the integration of LearnUpon into Azure AD, you need to add LearnUpon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dc978-125">**To add LearnUpon from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dc978-125">**To add LearnUpon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dc978-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="dc978-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="dc978-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="dc978-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dc978-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="dc978-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="dc978-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="dc978-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="dc978-133">In the search box, type **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="dc978-133">In the search box, type **LearnUpon**.</span></span>

    ![Creating an Azure AD test user](./media/learnupon-tutorial/tutorial_learnupon_search.png)

1. <span data-ttu-id="dc978-135">In the results panel, select **LearnUpon**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="dc978-135">In the results panel, select **LearnUpon**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dc978-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dc978-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dc978-138">In this section, you configure and test Azure AD single sign-on with LearnUpon based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dc978-138">In this section, you configure and test Azure AD single sign-on with LearnUpon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dc978-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LearnUpon is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc978-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LearnUpon is to a user in Azure AD.</span></span> <span data-ttu-id="dc978-140">In other words, a link relationship between an Azure AD user and the related user in LearnUpon needs to be established.</span><span class="sxs-lookup"><span data-stu-id="dc978-140">In other words, a link relationship between an Azure AD user and the related user in LearnUpon needs to be established.</span></span>

<span data-ttu-id="dc978-141">In LearnUpon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="dc978-141">In LearnUpon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dc978-142">To configure and test Azure AD single sign-on with LearnUpon, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="dc978-142">To configure and test Azure AD single sign-on with LearnUpon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dc978-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="dc978-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="dc978-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc978-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="dc978-145">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - to have a counterpart of Britta Simon in LearnUpon that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="dc978-145">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - to have a counterpart of Britta Simon in LearnUpon that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="dc978-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="dc978-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="dc978-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="dc978-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dc978-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dc978-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dc978-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LearnUpon application.</span><span class="sxs-lookup"><span data-stu-id="dc978-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LearnUpon application.</span></span>

<span data-ttu-id="dc978-150">**To configure Azure AD single sign-on with LearnUpon, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dc978-150">**To configure Azure AD single sign-on with LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="dc978-151">In the Azure portal, on the **LearnUpon** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="dc978-151">In the Azure portal, on the **LearnUpon** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="dc978-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="dc978-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/learnupon-tutorial/tutorial_learnupon_samlbase.png)

1. <span data-ttu-id="dc978-155">On the **LearnUpon Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dc978-155">On the **LearnUpon Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/learnupon-tutorial/tutorial_learnupon_url.png)

    <span data-ttu-id="dc978-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.learnupon.com/saml/consumer`</span><span class="sxs-lookup"><span data-stu-id="dc978-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.learnupon.com/saml/consumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dc978-158">Please note that this is not the real value.</span><span class="sxs-lookup"><span data-stu-id="dc978-158">Please note that this is not the real value.</span></span> <span data-ttu-id="dc978-159">you have to update this value with the actual Reply URL.</span><span class="sxs-lookup"><span data-stu-id="dc978-159">you have to update this value with the actual Reply URL.</span></span> <span data-ttu-id="dc978-160">To get this value Contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="dc978-160">To get this value Contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span>



1. <span data-ttu-id="dc978-161">On the **SAML Signing Certificate** section, locate the **Thumbprint** - This will be added to your LearnUpon SAML Settings.</span><span class="sxs-lookup"><span data-stu-id="dc978-161">On the **SAML Signing Certificate** section, locate the **Thumbprint** - This will be added to your LearnUpon SAML Settings.</span></span>

    ![Configure Single Sign-On](./media/learnupon-tutorial/tutorial_learnupon_certificate.png) 

1. <span data-ttu-id="dc978-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="dc978-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/learnupon-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="dc978-165">On the **LearnUpon Configuration** section, click **Configure LearnUpon** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="dc978-165">On the **LearnUpon Configuration** section, click **Configure LearnUpon** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dc978-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="dc978-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/learnupon-tutorial/tutorial_learnupon_configure.png) 

1. <span data-ttu-id="dc978-168">Open another browser instance and login into LearnUpon with an administrator account.</span><span class="sxs-lookup"><span data-stu-id="dc978-168">Open another browser instance and login into LearnUpon with an administrator account.</span></span> 

1. <span data-ttu-id="dc978-169">Click the **settings** tab.</span><span class="sxs-lookup"><span data-stu-id="dc978-169">Click the **settings** tab.</span></span>
   
    ![Configure Single Sign-On](./media/learnupon-tutorial/tutorial_learnupon_06.png)

1. <span data-ttu-id="dc978-171">Click **Single Sign On - SAML**, and then click **General Settings** to configure SAML settings.</span><span class="sxs-lookup"><span data-stu-id="dc978-171">Click **Single Sign On - SAML**, and then click **General Settings** to configure SAML settings.</span></span>
   
    ![Configure Single Sign-On](./media/learnupon-tutorial/tutorial_learnupon_07.png) 

1. <span data-ttu-id="dc978-173">In the **General Settings** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dc978-173">In the **General Settings** section, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](./media/learnupon-tutorial/tutorial_learnupon_08.png)  
  
    <span data-ttu-id="dc978-175">a.</span><span class="sxs-lookup"><span data-stu-id="dc978-175">a.</span></span> <span data-ttu-id="dc978-176">Select **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="dc978-176">Select **Enabled**.</span></span>

    <span data-ttu-id="dc978-177">b.</span><span class="sxs-lookup"><span data-stu-id="dc978-177">b.</span></span> <span data-ttu-id="dc978-178">Select **Version** as **2.0**.</span><span class="sxs-lookup"><span data-stu-id="dc978-178">Select **Version** as **2.0**.</span></span>

    <span data-ttu-id="dc978-179">c.</span><span class="sxs-lookup"><span data-stu-id="dc978-179">c.</span></span> <span data-ttu-id="dc978-180">Select **Skip conditions** as **No**.</span><span class="sxs-lookup"><span data-stu-id="dc978-180">Select **Skip conditions** as **No**.</span></span>

    <span data-ttu-id="dc978-181">d.</span><span class="sxs-lookup"><span data-stu-id="dc978-181">d.</span></span> <span data-ttu-id="dc978-182">In the **SAML Token Post param name** textbox, type the name of request post parameter to the SAML consumer URL indicated above that contains the SAML Assertion to be verified and authenticated - for example **SAMLResponse**.</span><span class="sxs-lookup"><span data-stu-id="dc978-182">In the **SAML Token Post param name** textbox, type the name of request post parameter to the SAML consumer URL indicated above that contains the SAML Assertion to be verified and authenticated - for example **SAMLResponse**.</span></span>

    <span data-ttu-id="dc978-183">e.</span><span class="sxs-lookup"><span data-stu-id="dc978-183">e.</span></span> <span data-ttu-id="dc978-184">In the **Name Identifier Format** textbox, type the value that indicates where in your SAML Assertion the users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="dc978-184">In the **Name Identifier Format** textbox, type the value that indicates where in your SAML Assertion the users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>
  
    <span data-ttu-id="dc978-185">f.</span><span class="sxs-lookup"><span data-stu-id="dc978-185">f.</span></span> <span data-ttu-id="dc978-186">In the **Identify Provider Location** textbox, type the value that indicates where the users are sent to if they click on your uploaded icon from your Azure portal login screen.</span><span class="sxs-lookup"><span data-stu-id="dc978-186">In the **Identify Provider Location** textbox, type the value that indicates where the users are sent to if they click on your uploaded icon from your Azure portal login screen.</span></span>
  
    <span data-ttu-id="dc978-187">g.</span><span class="sxs-lookup"><span data-stu-id="dc978-187">g.</span></span> <span data-ttu-id="dc978-188">In the **Sign out URL** textbox, paste the **Sign-Out URL** which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="dc978-188">In the **Sign out URL** textbox, paste the **Sign-Out URL** which you have copied from the Azure portal.</span></span>
    
    <span data-ttu-id="dc978-189">h.</span><span class="sxs-lookup"><span data-stu-id="dc978-189">h.</span></span> <span data-ttu-id="dc978-190">Click **Manage finger prints**, and then upload the finger print of your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="dc978-190">Click **Manage finger prints**, and then upload the finger print of your downloaded certificate.</span></span>

1. <span data-ttu-id="dc978-191">Click **User Settings**, and then perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dc978-191">Click **User Settings**, and then perform the following steps:</span></span>
   
     ![Configure Single Sign-On](./media/learnupon-tutorial/tutorial_learnupon_11.png)  
 
    <span data-ttu-id="dc978-193">a.</span><span class="sxs-lookup"><span data-stu-id="dc978-193">a.</span></span> <span data-ttu-id="dc978-194">In the **First Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users firstname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="dc978-194">In the **First Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users firstname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
  
    <span data-ttu-id="dc978-195">b.</span><span class="sxs-lookup"><span data-stu-id="dc978-195">b.</span></span> <span data-ttu-id="dc978-196">In the **Last Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users lastname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="dc978-196">In the **Last Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users lastname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

> [!TIP]
> <span data-ttu-id="dc978-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="dc978-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dc978-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="dc978-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dc978-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dc978-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dc978-200">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="dc978-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="dc978-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc978-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="dc978-203">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dc978-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dc978-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="dc978-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/learnupon-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="dc978-206">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="dc978-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/learnupon-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="dc978-208">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="dc978-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/learnupon-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="dc978-210">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dc978-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/learnupon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dc978-212">a.</span><span class="sxs-lookup"><span data-stu-id="dc978-212">a.</span></span> <span data-ttu-id="dc978-213">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dc978-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dc978-214">b.</span><span class="sxs-lookup"><span data-stu-id="dc978-214">b.</span></span> <span data-ttu-id="dc978-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dc978-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dc978-216">c.</span><span class="sxs-lookup"><span data-stu-id="dc978-216">c.</span></span> <span data-ttu-id="dc978-217">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="dc978-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dc978-218">d.</span><span class="sxs-lookup"><span data-stu-id="dc978-218">d.</span></span> <span data-ttu-id="dc978-219">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="dc978-219">Click **Create**.</span></span>
 
### <a name="creating-a-learnupon-test-user"></a><span data-ttu-id="dc978-220">Creating a LearnUpon test user</span><span class="sxs-lookup"><span data-stu-id="dc978-220">Creating a LearnUpon test user</span></span>

<span data-ttu-id="dc978-221">The objective of this section is to create a user called Britta Simon in LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="dc978-221">The objective of this section is to create a user called Britta Simon in LearnUpon.</span></span> <span data-ttu-id="dc978-222">LearnUpon supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="dc978-222">LearnUpon supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="dc978-223">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="dc978-223">There is no action item for you in this section.</span></span> <span data-ttu-id="dc978-224">A new user will be created during an attempt to access LearnUpon if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="dc978-224">A new user will be created during an attempt to access LearnUpon if it doesn't exist yet.</span></span> <span data-ttu-id="dc978-225">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="dc978-225">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="dc978-226">If you need to create an user manually, you need to contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="dc978-226">If you need to create an user manually, you need to contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dc978-227">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="dc978-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dc978-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="dc978-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LearnUpon.</span></span>

![Assign User][200] 

<span data-ttu-id="dc978-230">**To assign Britta Simon to LearnUpon, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dc978-230">**To assign Britta Simon to LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="dc978-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="dc978-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="dc978-233">In the applications list, select **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="dc978-233">In the applications list, select **LearnUpon**.</span></span>

    ![Configure Single Sign-On](./media/learnupon-tutorial/tutorial_learnupon_app.png) 

1. <span data-ttu-id="dc978-235">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="dc978-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="dc978-237">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="dc978-237">Click **Add** button.</span></span> <span data-ttu-id="dc978-238">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="dc978-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="dc978-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="dc978-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="dc978-241">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="dc978-241">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="dc978-242">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="dc978-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dc978-243">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="dc978-243">Testing single sign-on</span></span>

<span data-ttu-id="dc978-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="dc978-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dc978-245">When you click the LearnUpon tile in the Access Panel, you should get automatically signed-on to your LearnUpon application.</span><span class="sxs-lookup"><span data-stu-id="dc978-245">When you click the LearnUpon tile in the Access Panel, you should get automatically signed-on to your LearnUpon application.</span></span>
<span data-ttu-id="dc978-246">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dc978-246">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dc978-247">Additional resources</span><span class="sxs-lookup"><span data-stu-id="dc978-247">Additional resources</span></span>

* [<span data-ttu-id="dc978-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc978-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="dc978-249">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dc978-249">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/learnupon-tutorial/tutorial_general_01.png
[2]: ./media/learnupon-tutorial/tutorial_general_02.png
[3]: ./media/learnupon-tutorial/tutorial_general_03.png
[4]: ./media/learnupon-tutorial/tutorial_general_04.png

[100]: ./media/learnupon-tutorial/tutorial_general_100.png

[200]: ./media/learnupon-tutorial/tutorial_general_200.png
[201]: ./media/learnupon-tutorial/tutorial_general_201.png
[202]: ./media/learnupon-tutorial/tutorial_general_202.png
[203]: ./media/learnupon-tutorial/tutorial_general_203.png

