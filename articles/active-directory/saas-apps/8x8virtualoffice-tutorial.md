---
title: 'Tutorial: Azure Active Directory integration with 8x8 Virtual Office | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and 8x8 Virtual Office.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: b34a6edf-e745-4aec-b0b2-7337473d64c5
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 3a33f9ba0ca744709e21e9e55acc22b657c2adc2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857536"
---
# <a name="tutorial-azure-active-directory-integration-with-8x8-virtual-office"></a><span data-ttu-id="a2903-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="a2903-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span></span>

<span data-ttu-id="a2903-104">In this tutorial, you learn how to integrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a2903-104">In this tutorial, you learn how to integrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a2903-105">Integrating 8x8 Virtual Office with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a2903-105">Integrating 8x8 Virtual Office with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a2903-106">You can control in Azure AD who has access to 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="a2903-106">You can control in Azure AD who has access to 8x8 Virtual Office</span></span>
- <span data-ttu-id="a2903-107">You can enable your users to automatically get signed-on to 8x8 Virtual Office (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="a2903-107">You can enable your users to automatically get signed-on to 8x8 Virtual Office (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a2903-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a2903-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a2903-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a2903-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2903-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a2903-110">Prerequisites</span></span>

<span data-ttu-id="a2903-111">To configure Azure AD integration with 8x8 Virtual Office, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a2903-111">To configure Azure AD integration with 8x8 Virtual Office, you need the following items:</span></span>

- <span data-ttu-id="a2903-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a2903-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a2903-113">A 8x8 Virtual Office single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a2903-113">A 8x8 Virtual Office single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a2903-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a2903-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a2903-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a2903-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a2903-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a2903-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a2903-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2903-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a2903-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a2903-118">Scenario description</span></span>
<span data-ttu-id="a2903-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a2903-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a2903-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a2903-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a2903-121">Adding 8x8 Virtual Office from the gallery</span><span class="sxs-lookup"><span data-stu-id="a2903-121">Adding 8x8 Virtual Office from the gallery</span></span>
2. <span data-ttu-id="a2903-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a2903-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-8x8-virtual-office-from-the-gallery"></a><span data-ttu-id="a2903-123">Adding 8x8 Virtual Office from the gallery</span><span class="sxs-lookup"><span data-stu-id="a2903-123">Adding 8x8 Virtual Office from the gallery</span></span>
<span data-ttu-id="a2903-124">To configure the integration of 8x8 Virtual Office into Azure AD, you need to add 8x8 Virtual Office from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a2903-124">To configure the integration of 8x8 Virtual Office into Azure AD, you need to add 8x8 Virtual Office from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a2903-125">**To add 8x8 Virtual Office from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a2903-125">**To add 8x8 Virtual Office from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a2903-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a2903-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a2903-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a2903-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a2903-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a2903-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a2903-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a2903-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a2903-133">In the search box, type **8x8 Virtual Office**.</span><span class="sxs-lookup"><span data-stu-id="a2903-133">In the search box, type **8x8 Virtual Office**.</span></span>

    ![Creating an Azure AD test user](./media/8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_search.png)

5. <span data-ttu-id="a2903-135">In the results panel, select **8x8 Virtual Office**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a2903-135">In the results panel, select **8x8 Virtual Office**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a2903-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a2903-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a2903-138">In this section, you configure and test Azure AD single sign-on with 8x8 Virtual Office based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a2903-138">In this section, you configure and test Azure AD single sign-on with 8x8 Virtual Office based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a2903-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 8x8 Virtual Office is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2903-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 8x8 Virtual Office is to a user in Azure AD.</span></span> <span data-ttu-id="a2903-140">In other words, a link relationship between an Azure AD user and the related user in 8x8 Virtual Office needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a2903-140">In other words, a link relationship between an Azure AD user and the related user in 8x8 Virtual Office needs to be established.</span></span>

<span data-ttu-id="a2903-141">In 8x8 Virtual Office, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="a2903-141">In 8x8 Virtual Office, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a2903-142">To configure and test Azure AD single sign-on with 8x8 Virtual Office, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a2903-142">To configure and test Azure AD single sign-on with 8x8 Virtual Office, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a2903-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a2903-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a2903-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a2903-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a2903-145">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - to have a counterpart of Britta Simon in 8x8 Virtual Office that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a2903-145">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - to have a counterpart of Britta Simon in 8x8 Virtual Office that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a2903-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a2903-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a2903-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a2903-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a2903-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a2903-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a2903-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 8x8 Virtual Office application.</span><span class="sxs-lookup"><span data-stu-id="a2903-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 8x8 Virtual Office application.</span></span>

<span data-ttu-id="a2903-150">**To configure Azure AD single sign-on with 8x8 Virtual Office, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a2903-150">**To configure Azure AD single sign-on with 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="a2903-151">In the Azure portal, on the **8x8 Virtual Office** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a2903-151">In the Azure portal, on the **8x8 Virtual Office** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="a2903-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a2903-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_samlbase.png)

3. <span data-ttu-id="a2903-155">On the **8x8 Virtual Office Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a2903-155">On the **8x8 Virtual Office Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_url.png)

    <span data-ttu-id="a2903-157">a.</span><span class="sxs-lookup"><span data-stu-id="a2903-157">a.</span></span> <span data-ttu-id="a2903-158">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="a2903-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="a2903-159">| `https://sso.8x8.com/<companyname>` |
    | `https://www.8x8.com/<companyname>` |
    | `https://sso.8x8pilot.com/<companyname>` |</span><span class="sxs-lookup"><span data-stu-id="a2903-159">| `https://sso.8x8.com/<companyname>` |
 | `https://www.8x8.com/<companyname>` |
 | `https://sso.8x8pilot.com/<companyname>` |</span></span>

    <span data-ttu-id="a2903-160">b.</span><span class="sxs-lookup"><span data-stu-id="a2903-160">b.</span></span> <span data-ttu-id="a2903-161">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="a2903-161">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="a2903-162">| `https://<subdomain>.8x8.com/saml2` |
    | `https://<subdomain>.8x8pilot.com/saml2`|</span><span class="sxs-lookup"><span data-stu-id="a2903-162">| `https://<subdomain>.8x8.com/saml2` |
 | `https://<subdomain>.8x8pilot.com/saml2`|</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a2903-163">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="a2903-163">These values are not real.</span></span> <span data-ttu-id="a2903-164">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="a2903-164">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="a2903-165">Contact [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us) to get these values.</span><span class="sxs-lookup"><span data-stu-id="a2903-165">Contact [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us) to get these values.</span></span>
 


4. <span data-ttu-id="a2903-166">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a2903-166">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_certificate.png) 

5. <span data-ttu-id="a2903-168">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a2903-168">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/8x8virtualoffice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a2903-170">On the **8x8 Virtual Office Configuration** section, click **Configure 8x8 Virtual Office** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="a2903-170">On the **8x8 Virtual Office Configuration** section, click **Configure 8x8 Virtual Office** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a2903-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="a2903-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_configure.png) 

7. <span data-ttu-id="a2903-173">Sign-on to your 8x8 Virtual Office tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="a2903-173">Sign-on to your 8x8 Virtual Office tenant as an administrator.</span></span>

8. <span data-ttu-id="a2903-174">Select **Virtual Office Account Mgr** on Application Panel.</span><span class="sxs-lookup"><span data-stu-id="a2903-174">Select **Virtual Office Account Mgr** on Application Panel.</span></span>
   
    ![Configure On App Side](./media/8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_001.png)

9. <span data-ttu-id="a2903-176">Select **Business** account to manage and click **Sign In** button.</span><span class="sxs-lookup"><span data-stu-id="a2903-176">Select **Business** account to manage and click **Sign In** button.</span></span>
   
    ![Configure On App Side](./media/8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_002.png)

10. <span data-ttu-id="a2903-178">Click **Accounts** tab in the menu list.</span><span class="sxs-lookup"><span data-stu-id="a2903-178">Click **Accounts** tab in the menu list.</span></span>
   
    ![Configure On App Side](./media/8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_003.png)

11. <span data-ttu-id="a2903-180">Click **Single Sign On** in the list of Accounts.</span><span class="sxs-lookup"><span data-stu-id="a2903-180">Click **Single Sign On** in the list of Accounts.</span></span>
   
    ![Configure On App Side](./media/8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_004.png)

12. <span data-ttu-id="a2903-182">Select **Single Sign On** under Authentication method and click **SAML**.</span><span class="sxs-lookup"><span data-stu-id="a2903-182">Select **Single Sign On** under Authentication method and click **SAML**.</span></span>
    
    ![Configure On App Side](./media/8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_005.png)

13. <span data-ttu-id="a2903-184">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD to **Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="a2903-184">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD to **Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span></span> 
    
    ![Configure On App Side](./media/8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_006.png)
    
14. <span data-ttu-id="a2903-186">Click **Browser** button to upload the certificate which you downloaded from Azure AD, and click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a2903-186">Click **Browser** button to upload the certificate which you downloaded from Azure AD, and click the **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="a2903-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="a2903-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a2903-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="a2903-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a2903-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a2903-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a2903-190">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a2903-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="a2903-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a2903-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="a2903-193">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a2903-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a2903-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a2903-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/8x8virtualoffice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a2903-196">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a2903-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/8x8virtualoffice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a2903-198">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="a2903-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/8x8virtualoffice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a2903-200">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a2903-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/8x8virtualoffice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a2903-202">a.</span><span class="sxs-lookup"><span data-stu-id="a2903-202">a.</span></span> <span data-ttu-id="a2903-203">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a2903-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a2903-204">b.</span><span class="sxs-lookup"><span data-stu-id="a2903-204">b.</span></span> <span data-ttu-id="a2903-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a2903-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a2903-206">c.</span><span class="sxs-lookup"><span data-stu-id="a2903-206">c.</span></span> <span data-ttu-id="a2903-207">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="a2903-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a2903-208">d.</span><span class="sxs-lookup"><span data-stu-id="a2903-208">d.</span></span> <span data-ttu-id="a2903-209">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a2903-209">Click **Create**.</span></span>
 
### <a name="creating-a-8x8-virtual-office-test-user"></a><span data-ttu-id="a2903-210">Creating a 8x8 Virtual Office test user</span><span class="sxs-lookup"><span data-stu-id="a2903-210">Creating a 8x8 Virtual Office test user</span></span>

<span data-ttu-id="a2903-211">The objective of this section is to create a user called Britta Simon in 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="a2903-211">The objective of this section is to create a user called Britta Simon in 8x8 Virtual Office.</span></span> <span data-ttu-id="a2903-212">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="a2903-212">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="a2903-213">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="a2903-213">There is no action item for you in this section.</span></span> <span data-ttu-id="a2903-214">A new user is created during an attempt to access 8x8 Virtual Office if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="a2903-214">A new user is created during an attempt to access 8x8 Virtual Office if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="a2903-215">If you need to create a user manually, you need to contact the [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us).</span><span class="sxs-lookup"><span data-stu-id="a2903-215">If you need to create a user manually, you need to contact the [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a2903-216">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a2903-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a2903-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="a2903-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 8x8 Virtual Office.</span></span>

![Assign User][200] 

<span data-ttu-id="a2903-219">**To assign Britta Simon to 8x8 Virtual Office, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a2903-219">**To assign Britta Simon to 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="a2903-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a2903-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="a2903-222">In the applications list, select **8x8 Virtual Office**.</span><span class="sxs-lookup"><span data-stu-id="a2903-222">In the applications list, select **8x8 Virtual Office**.</span></span>

    ![Configure Single Sign-On](./media/8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_app.png) 

3. <span data-ttu-id="a2903-224">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a2903-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="a2903-226">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a2903-226">Click **Add** button.</span></span> <span data-ttu-id="a2903-227">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a2903-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="a2903-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a2903-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a2903-230">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a2903-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a2903-231">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a2903-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a2903-232">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="a2903-232">Testing single sign-on</span></span>

<span data-ttu-id="a2903-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a2903-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a2903-234">When you click the 8x8 Virtual Office tile in the Access Panel, you should get automatically signed-on to your 8x8 Virtual Office application.</span><span class="sxs-lookup"><span data-stu-id="a2903-234">When you click the 8x8 Virtual Office tile in the Access Panel, you should get automatically signed-on to your 8x8 Virtual Office application.</span></span>
<span data-ttu-id="a2903-235">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="a2903-235">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a2903-236">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a2903-236">Additional resources</span></span>

* [<span data-ttu-id="a2903-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2903-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a2903-238">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a2903-238">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/8x8virtualoffice-tutorial/tutorial_general_01.png
[2]: ./media/8x8virtualoffice-tutorial/tutorial_general_02.png
[3]: ./media/8x8virtualoffice-tutorial/tutorial_general_03.png
[4]: ./media/8x8virtualoffice-tutorial/tutorial_general_04.png

[100]: ./media/8x8virtualoffice-tutorial/tutorial_general_100.png

[200]: ./media/8x8virtualoffice-tutorial/tutorial_general_200.png
[201]: ./media/8x8virtualoffice-tutorial/tutorial_general_201.png
[202]: ./media/8x8virtualoffice-tutorial/tutorial_general_202.png
[203]: ./media/8x8virtualoffice-tutorial/tutorial_general_203.png

