---
title: 'Tutorial: Azure Active Directory integration with Kintone | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Kintone.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 693211245ee98849548bee4a52f7e424dd8b4cc6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866548"
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a><span data-ttu-id="1c24a-103">Tutorial: Azure Active Directory integration with Kintone</span><span class="sxs-lookup"><span data-stu-id="1c24a-103">Tutorial: Azure Active Directory integration with Kintone</span></span>

<span data-ttu-id="1c24a-104">In this tutorial, you learn how to integrate Kintone with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1c24a-104">In this tutorial, you learn how to integrate Kintone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1c24a-105">Integrating Kintone with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1c24a-105">Integrating Kintone with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1c24a-106">You can control in Azure AD who has access to Kintone</span><span class="sxs-lookup"><span data-stu-id="1c24a-106">You can control in Azure AD who has access to Kintone</span></span>
- <span data-ttu-id="1c24a-107">You can enable your users to automatically get signed-on to Kintone (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="1c24a-107">You can enable your users to automatically get signed-on to Kintone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1c24a-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1c24a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1c24a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="1c24a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c24a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1c24a-110">Prerequisites</span></span>

<span data-ttu-id="1c24a-111">To configure Azure AD integration with Kintone, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1c24a-111">To configure Azure AD integration with Kintone, you need the following items:</span></span>

- <span data-ttu-id="1c24a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="1c24a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1c24a-113">A Kintone single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1c24a-113">A Kintone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1c24a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1c24a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1c24a-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1c24a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1c24a-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="1c24a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1c24a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1c24a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1c24a-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="1c24a-118">Scenario description</span></span>
<span data-ttu-id="1c24a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1c24a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1c24a-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1c24a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1c24a-121">Adding Kintone from the gallery</span><span class="sxs-lookup"><span data-stu-id="1c24a-121">Adding Kintone from the gallery</span></span>
1. <span data-ttu-id="1c24a-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1c24a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kintone-from-the-gallery"></a><span data-ttu-id="1c24a-123">Adding Kintone from the gallery</span><span class="sxs-lookup"><span data-stu-id="1c24a-123">Adding Kintone from the gallery</span></span>
<span data-ttu-id="1c24a-124">To configure the integration of Kintone into Azure AD, you need to add Kintone from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1c24a-124">To configure the integration of Kintone into Azure AD, you need to add Kintone from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1c24a-125">**To add Kintone from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1c24a-125">**To add Kintone from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1c24a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="1c24a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="1c24a-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="1c24a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1c24a-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1c24a-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="1c24a-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="1c24a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="1c24a-133">In the search box, type **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="1c24a-133">In the search box, type **Kintone**.</span></span>

    ![Creating an Azure AD test user](./media/kintone-tutorial/tutorial_kintone_search.png)

1. <span data-ttu-id="1c24a-135">In the results panel, select **Kintone**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="1c24a-135">In the results panel, select **Kintone**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1c24a-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1c24a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1c24a-138">In this section, you configure and test Azure AD single sign-on with Kintone based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1c24a-138">In this section, you configure and test Azure AD single sign-on with Kintone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1c24a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kintone is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c24a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kintone is to a user in Azure AD.</span></span> <span data-ttu-id="1c24a-140">In other words, a link relationship between an Azure AD user and the related user in Kintone needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1c24a-140">In other words, a link relationship between an Azure AD user and the related user in Kintone needs to be established.</span></span>

<span data-ttu-id="1c24a-141">In Kintone, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="1c24a-141">In Kintone, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1c24a-142">To configure and test Azure AD single sign-on with Kintone, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1c24a-142">To configure and test Azure AD single sign-on with Kintone, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1c24a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1c24a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="1c24a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1c24a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="1c24a-145">**[Creating a Kintone test user](#creating-a-kintone-test-user)** - to have a counterpart of Britta Simon in Kintone that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="1c24a-145">**[Creating a Kintone test user](#creating-a-kintone-test-user)** - to have a counterpart of Britta Simon in Kintone that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="1c24a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1c24a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="1c24a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1c24a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1c24a-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1c24a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1c24a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kintone application.</span><span class="sxs-lookup"><span data-stu-id="1c24a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kintone application.</span></span>

<span data-ttu-id="1c24a-150">**To configure Azure AD single sign-on with Kintone, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1c24a-150">**To configure Azure AD single sign-on with Kintone, perform the following steps:**</span></span>

1. <span data-ttu-id="1c24a-151">In the Azure portal, on the **Kintone** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1c24a-151">In the Azure portal, on the **Kintone** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="1c24a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1c24a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/kintone-tutorial/tutorial_kintone_samlbase.png)

1. <span data-ttu-id="1c24a-155">On the **Kintone Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1c24a-155">On the **Kintone Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/kintone-tutorial/tutorial_kintone_url.png)

    <span data-ttu-id="1c24a-157">a.</span><span class="sxs-lookup"><span data-stu-id="1c24a-157">a.</span></span> <span data-ttu-id="1c24a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.kintone.com`</span><span class="sxs-lookup"><span data-stu-id="1c24a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.kintone.com`</span></span>

    <span data-ttu-id="1c24a-159">b.</span><span class="sxs-lookup"><span data-stu-id="1c24a-159">b.</span></span> <span data-ttu-id="1c24a-160">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="1c24a-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > <span data-ttu-id="1c24a-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="1c24a-161">These values are not real.</span></span> <span data-ttu-id="1c24a-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="1c24a-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1c24a-163">Contact [Kintone Client support team](https://www.kintone.com/contact/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="1c24a-163">Contact [Kintone Client support team](https://www.kintone.com/contact/) to get these values.</span></span> 
 
1. <span data-ttu-id="1c24a-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="1c24a-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/kintone-tutorial/tutorial_kintone_certificate.png) 

1. <span data-ttu-id="1c24a-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="1c24a-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/kintone-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="1c24a-168">On the **Kintone Configuration** section, click **Configure Kintone** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="1c24a-168">On the **Kintone Configuration** section, click **Configure Kintone** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1c24a-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="1c24a-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/kintone-tutorial/tutorial_kintone_configure.png) 

1. <span data-ttu-id="1c24a-171">In a different web browser window, log into your **Kintone** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="1c24a-171">In a different web browser window, log into your **Kintone** company site as an administrator.</span></span>

1. <span data-ttu-id="1c24a-172">Click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="1c24a-172">Click **Settings**.</span></span>
   
    <span data-ttu-id="1c24a-173">![Settings](./media/kintone-tutorial/ic785879.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="1c24a-173">![Settings](./media/kintone-tutorial/ic785879.png "Settings")</span></span>

1. <span data-ttu-id="1c24a-174">Click **Users & System Administration**.</span><span class="sxs-lookup"><span data-stu-id="1c24a-174">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="1c24a-175">![Users & System Administration](./media/kintone-tutorial/ic785880.png "Users & System Administration")</span><span class="sxs-lookup"><span data-stu-id="1c24a-175">![Users & System Administration](./media/kintone-tutorial/ic785880.png "Users & System Administration")</span></span>

1. <span data-ttu-id="1c24a-176">Under **System Administration \> Security** click **Login**.</span><span class="sxs-lookup"><span data-stu-id="1c24a-176">Under **System Administration \> Security** click **Login**.</span></span>
   
    <span data-ttu-id="1c24a-177">![Login](./media/kintone-tutorial/ic785881.png "Login")</span><span class="sxs-lookup"><span data-stu-id="1c24a-177">![Login](./media/kintone-tutorial/ic785881.png "Login")</span></span>

1. <span data-ttu-id="1c24a-178">Click **Enable SAML authentication**.</span><span class="sxs-lookup"><span data-stu-id="1c24a-178">Click **Enable SAML authentication**.</span></span>
   
    <span data-ttu-id="1c24a-179">![SAML Authentication](./media/kintone-tutorial/ic785882.png "SAML Authentication")</span><span class="sxs-lookup"><span data-stu-id="1c24a-179">![SAML Authentication](./media/kintone-tutorial/ic785882.png "SAML Authentication")</span></span>

1. <span data-ttu-id="1c24a-180">In the SAML Authentication section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1c24a-180">In the SAML Authentication section, perform the following steps:</span></span>
    
    <span data-ttu-id="1c24a-181">![SAML Authentication](./media/kintone-tutorial/ic785883.png "SAML Authentication")</span><span class="sxs-lookup"><span data-stu-id="1c24a-181">![SAML Authentication](./media/kintone-tutorial/ic785883.png "SAML Authentication")</span></span>
    
    <span data-ttu-id="1c24a-182">a.</span><span class="sxs-lookup"><span data-stu-id="1c24a-182">a.</span></span> <span data-ttu-id="1c24a-183">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1c24a-183">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="1c24a-184">b.</span><span class="sxs-lookup"><span data-stu-id="1c24a-184">b.</span></span> <span data-ttu-id="1c24a-185">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1c24a-185">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="1c24a-186">c.</span><span class="sxs-lookup"><span data-stu-id="1c24a-186">c.</span></span> <span data-ttu-id="1c24a-187">Click **Browse** to upload your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="1c24a-187">Click **Browse** to upload your downloaded certificate.</span></span>
    
    <span data-ttu-id="1c24a-188">d.</span><span class="sxs-lookup"><span data-stu-id="1c24a-188">d.</span></span> <span data-ttu-id="1c24a-189">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1c24a-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="1c24a-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="1c24a-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1c24a-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="1c24a-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1c24a-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1c24a-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1c24a-193">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1c24a-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="1c24a-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1c24a-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="1c24a-196">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1c24a-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1c24a-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="1c24a-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/kintone-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="1c24a-199">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="1c24a-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/kintone-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="1c24a-201">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="1c24a-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/kintone-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="1c24a-203">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1c24a-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/kintone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1c24a-205">a.</span><span class="sxs-lookup"><span data-stu-id="1c24a-205">a.</span></span> <span data-ttu-id="1c24a-206">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1c24a-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1c24a-207">b.</span><span class="sxs-lookup"><span data-stu-id="1c24a-207">b.</span></span> <span data-ttu-id="1c24a-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1c24a-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1c24a-209">c.</span><span class="sxs-lookup"><span data-stu-id="1c24a-209">c.</span></span> <span data-ttu-id="1c24a-210">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="1c24a-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1c24a-211">d.</span><span class="sxs-lookup"><span data-stu-id="1c24a-211">d.</span></span> <span data-ttu-id="1c24a-212">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1c24a-212">Click **Create**.</span></span>
 
### <a name="creating-a-kintone-test-user"></a><span data-ttu-id="1c24a-213">Creating a Kintone test user</span><span class="sxs-lookup"><span data-stu-id="1c24a-213">Creating a Kintone test user</span></span>

<span data-ttu-id="1c24a-214">To enable Azure AD users to log in to Kintone, they must be provisioned into Kintone.</span><span class="sxs-lookup"><span data-stu-id="1c24a-214">To enable Azure AD users to log in to Kintone, they must be provisioned into Kintone.</span></span>  
<span data-ttu-id="1c24a-215">In the case of Kintone, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="1c24a-215">In the case of Kintone, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="1c24a-216">To provision a user account, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1c24a-216">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="1c24a-217">Log in to your **Kintone** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="1c24a-217">Log in to your **Kintone** company site as an administrator.</span></span>

1. <span data-ttu-id="1c24a-218">Click **Setting**.</span><span class="sxs-lookup"><span data-stu-id="1c24a-218">Click **Setting**.</span></span>
   
    <span data-ttu-id="1c24a-219">![Settings](./media/kintone-tutorial/ic785879.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="1c24a-219">![Settings](./media/kintone-tutorial/ic785879.png "Settings")</span></span>

1. <span data-ttu-id="1c24a-220">Click **Users & System Administration**.</span><span class="sxs-lookup"><span data-stu-id="1c24a-220">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="1c24a-221">![User & System Administration](./media/kintone-tutorial/ic785880.png "User & System Administration")</span><span class="sxs-lookup"><span data-stu-id="1c24a-221">![User & System Administration](./media/kintone-tutorial/ic785880.png "User & System Administration")</span></span>

1. <span data-ttu-id="1c24a-222">Under **User Administration**, click **Departments & Users**.</span><span class="sxs-lookup"><span data-stu-id="1c24a-222">Under **User Administration**, click **Departments & Users**.</span></span>
   
    <span data-ttu-id="1c24a-223">![Department & Users](./media/kintone-tutorial/ic785888.png "Department & Users")</span><span class="sxs-lookup"><span data-stu-id="1c24a-223">![Department & Users](./media/kintone-tutorial/ic785888.png "Department & Users")</span></span>

1. <span data-ttu-id="1c24a-224">Click **New User**.</span><span class="sxs-lookup"><span data-stu-id="1c24a-224">Click **New User**.</span></span>
   
    <span data-ttu-id="1c24a-225">![New Users](./media/kintone-tutorial/ic785889.png "New Users")</span><span class="sxs-lookup"><span data-stu-id="1c24a-225">![New Users](./media/kintone-tutorial/ic785889.png "New Users")</span></span>

1. <span data-ttu-id="1c24a-226">In the **New User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1c24a-226">In the **New User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="1c24a-227">![New Users](./media/kintone-tutorial/ic785890.png "New Users")</span><span class="sxs-lookup"><span data-stu-id="1c24a-227">![New Users](./media/kintone-tutorial/ic785890.png "New Users")</span></span>
   
    <span data-ttu-id="1c24a-228">a.</span><span class="sxs-lookup"><span data-stu-id="1c24a-228">a.</span></span> <span data-ttu-id="1c24a-229">Type a **Display Name**, **Login Name**, **New Password**, **Confirm Password**, **E-mail Address**, and other details of a valid AAD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="1c24a-229">Type a **Display Name**, **Login Name**, **New Password**, **Confirm Password**, **E-mail Address**, and other details of a valid AAD account you want to provision into the related textboxes.</span></span>
 
    <span data-ttu-id="1c24a-230">b.</span><span class="sxs-lookup"><span data-stu-id="1c24a-230">b.</span></span> <span data-ttu-id="1c24a-231">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="1c24a-231">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="1c24a-232">You can use any other Kintone user account creation tools or APIs provided by Kintone to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="1c24a-232">You can use any other Kintone user account creation tools or APIs provided by Kintone to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1c24a-233">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1c24a-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1c24a-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kintone.</span><span class="sxs-lookup"><span data-stu-id="1c24a-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kintone.</span></span>

![Assign User][200] 

<span data-ttu-id="1c24a-236">**To assign Britta Simon to Kintone, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1c24a-236">**To assign Britta Simon to Kintone, perform the following steps:**</span></span>

1. <span data-ttu-id="1c24a-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1c24a-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="1c24a-239">In the applications list, select **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="1c24a-239">In the applications list, select **Kintone**.</span></span>

    ![Configure Single Sign-On](./media/kintone-tutorial/tutorial_kintone_app.png) 

1. <span data-ttu-id="1c24a-241">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="1c24a-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="1c24a-243">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="1c24a-243">Click **Add** button.</span></span> <span data-ttu-id="1c24a-244">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1c24a-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="1c24a-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="1c24a-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="1c24a-247">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="1c24a-247">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="1c24a-248">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1c24a-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1c24a-249">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="1c24a-249">Testing single sign-on</span></span>

<span data-ttu-id="1c24a-250">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1c24a-250">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1c24a-251">When you click the Kintone tile in the Access Panel, you should get automatically signed-on to your Kintone application.</span><span class="sxs-lookup"><span data-stu-id="1c24a-251">When you click the Kintone tile in the Access Panel, you should get automatically signed-on to your Kintone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1c24a-252">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1c24a-252">Additional resources</span></span>

* [<span data-ttu-id="1c24a-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c24a-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="1c24a-254">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1c24a-254">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/kintone-tutorial/tutorial_general_01.png
[2]: ./media/kintone-tutorial/tutorial_general_02.png
[3]: ./media/kintone-tutorial/tutorial_general_03.png
[4]: ./media/kintone-tutorial/tutorial_general_04.png

[100]: ./media/kintone-tutorial/tutorial_general_100.png

[200]: ./media/kintone-tutorial/tutorial_general_200.png
[201]: ./media/kintone-tutorial/tutorial_general_201.png
[202]: ./media/kintone-tutorial/tutorial_general_202.png
[203]: ./media/kintone-tutorial/tutorial_general_203.png

