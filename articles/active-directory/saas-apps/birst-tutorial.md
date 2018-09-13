---
title: 'Tutorial: Azure Active Directory integration with Birst Agile Business Analytics | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Birst Agile Business Analytics.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 677183b1-5348-4302-88cc-5c8ab63a3c6c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: f3c9ff07b0cbb7b3f7aa6a23887ef86a0b53af0e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968528"
---
# <a name="tutorial-azure-active-directory-integration-with-birst-agile-business-analytics"></a><span data-ttu-id="084d8-103">Tutorial: Azure Active Directory integration with Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="084d8-103">Tutorial: Azure Active Directory integration with Birst Agile Business Analytics</span></span>

<span data-ttu-id="084d8-104">In this tutorial, you learn how to integrate Birst Agile Business Analytics with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="084d8-104">In this tutorial, you learn how to integrate Birst Agile Business Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="084d8-105">Integrating Birst Agile Business Analytics with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="084d8-105">Integrating Birst Agile Business Analytics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="084d8-106">You can control in Azure AD who has access to Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="084d8-106">You can control in Azure AD who has access to Birst Agile Business Analytics</span></span>
- <span data-ttu-id="084d8-107">You can enable your users to automatically get signed-on to Birst Agile Business Analytics (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="084d8-107">You can enable your users to automatically get signed-on to Birst Agile Business Analytics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="084d8-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="084d8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="084d8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="084d8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="084d8-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="084d8-110">Prerequisites</span></span>

<span data-ttu-id="084d8-111">To configure Azure AD integration with Birst Agile Business Analytics, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="084d8-111">To configure Azure AD integration with Birst Agile Business Analytics, you need the following items:</span></span>

- <span data-ttu-id="084d8-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="084d8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="084d8-113">A Birst Agile Business Analytics single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="084d8-113">A Birst Agile Business Analytics single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="084d8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="084d8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="084d8-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="084d8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="084d8-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="084d8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="084d8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="084d8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="084d8-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="084d8-118">Scenario description</span></span>
<span data-ttu-id="084d8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="084d8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="084d8-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="084d8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="084d8-121">Adding Birst Agile Business Analytics from the gallery</span><span class="sxs-lookup"><span data-stu-id="084d8-121">Adding Birst Agile Business Analytics from the gallery</span></span>
1. <span data-ttu-id="084d8-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="084d8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-birst-agile-business-analytics-from-the-gallery"></a><span data-ttu-id="084d8-123">Adding Birst Agile Business Analytics from the gallery</span><span class="sxs-lookup"><span data-stu-id="084d8-123">Adding Birst Agile Business Analytics from the gallery</span></span>
<span data-ttu-id="084d8-124">To configure the integration of Birst Agile Business Analytics into Azure AD, you need to add Birst Agile Business Analytics from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="084d8-124">To configure the integration of Birst Agile Business Analytics into Azure AD, you need to add Birst Agile Business Analytics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="084d8-125">**To add Birst Agile Business Analytics from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="084d8-125">**To add Birst Agile Business Analytics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="084d8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="084d8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="084d8-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="084d8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="084d8-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="084d8-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="084d8-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="084d8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="084d8-133">In the search box, type **Birst Agile Business Analytics**.</span><span class="sxs-lookup"><span data-stu-id="084d8-133">In the search box, type **Birst Agile Business Analytics**.</span></span>

    ![Creating an Azure AD test user](./media/birst-tutorial/tutorial_birst_search.png)

1. <span data-ttu-id="084d8-135">In the results panel, select **Birst Agile Business Analytics**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="084d8-135">In the results panel, select **Birst Agile Business Analytics**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/birst-tutorial/tutorial_birst_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="084d8-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="084d8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="084d8-138">In this section, you configure and test Azure AD single sign-on with Birst Agile Business Analytics based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="084d8-138">In this section, you configure and test Azure AD single sign-on with Birst Agile Business Analytics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="084d8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Birst Agile Business Analytics is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="084d8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Birst Agile Business Analytics is to a user in Azure AD.</span></span> <span data-ttu-id="084d8-140">In other words, a link relationship between an Azure AD user and the related user in Birst Agile Business Analytics needs to be established.</span><span class="sxs-lookup"><span data-stu-id="084d8-140">In other words, a link relationship between an Azure AD user and the related user in Birst Agile Business Analytics needs to be established.</span></span>

<span data-ttu-id="084d8-141">In Birst Agile Business Analytics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="084d8-141">In Birst Agile Business Analytics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="084d8-142">To configure and test Azure AD single sign-on with Birst Agile Business Analytics, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="084d8-142">To configure and test Azure AD single sign-on with Birst Agile Business Analytics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="084d8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="084d8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="084d8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="084d8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="084d8-145">**[Creating a Birst Agile Business Analytics test user](#creating-a-birst-agile-business-analytics-test-user)** - to have a counterpart of Britta Simon in Birst Agile Business Analytics that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="084d8-145">**[Creating a Birst Agile Business Analytics test user](#creating-a-birst-agile-business-analytics-test-user)** - to have a counterpart of Britta Simon in Birst Agile Business Analytics that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="084d8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="084d8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="084d8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="084d8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="084d8-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="084d8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="084d8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Birst Agile Business Analytics application.</span><span class="sxs-lookup"><span data-stu-id="084d8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Birst Agile Business Analytics application.</span></span>

<span data-ttu-id="084d8-150">**To configure Azure AD single sign-on with Birst Agile Business Analytics, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="084d8-150">**To configure Azure AD single sign-on with Birst Agile Business Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="084d8-151">In the Azure portal, on the **Birst Agile Business Analytics** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="084d8-151">In the Azure portal, on the **Birst Agile Business Analytics** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="084d8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="084d8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/birst-tutorial/tutorial_birst_samlbase.png)

1. <span data-ttu-id="084d8-155">On the **Birst Agile Business Analytics Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="084d8-155">On the **Birst Agile Business Analytics Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/birst-tutorial/tutorial_birst_url.png)

     <span data-ttu-id="084d8-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="084d8-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

     <span data-ttu-id="084d8-158">The URL depends on the datacenter that your Birst account is located:</span><span class="sxs-lookup"><span data-stu-id="084d8-158">The URL depends on the datacenter that your Birst account is located:</span></span> 

     * <span data-ttu-id="084d8-159">For US datacenter use following the pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="084d8-159">For US datacenter use following the pattern: `https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span> 

     * <span data-ttu-id="084d8-160">For Europe datacenter use the following pattern: `https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span><span class="sxs-lookup"><span data-stu-id="084d8-160">For Europe datacenter use the following pattern: `https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="084d8-161">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="084d8-161">This value is not real.</span></span> <span data-ttu-id="084d8-162">Update the value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="084d8-162">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="084d8-163">Contact [Birst Agile Business Analytics Client support team](mailto:info@birst.com) to get the value.</span><span class="sxs-lookup"><span data-stu-id="084d8-163">Contact [Birst Agile Business Analytics Client support team](mailto:info@birst.com) to get the value.</span></span> 
 
1. <span data-ttu-id="084d8-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="084d8-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/birst-tutorial/tutorial_birst_certificate.png) 

1. <span data-ttu-id="084d8-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="084d8-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/birst-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="084d8-168">On the **Birst Agile Business Analytics Configuration** section, click **Configure Birst Agile Business Analytics** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="084d8-168">On the **Birst Agile Business Analytics Configuration** section, click **Configure Birst Agile Business Analytics** to open **Configure sign-on** window.</span></span> <span data-ttu-id="084d8-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="084d8-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/birst-tutorial/tutorial_birst_configure.png) 

1. <span data-ttu-id="084d8-171">To configure single sign-on on **Birst Agile Business Analytics** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Birst Agile Business Analytics support team](mailto:info@birst.com).</span><span class="sxs-lookup"><span data-stu-id="084d8-171">To configure single sign-on on **Birst Agile Business Analytics** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Birst Agile Business Analytics support team](mailto:info@birst.com).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="084d8-172">Mention to Birst team that this integration needs SHA256 Algorithm (SHA1 will not be supported) so that they can set the SSO on the appropriate server like **app2101** etc.</span><span class="sxs-lookup"><span data-stu-id="084d8-172">Mention to Birst team that this integration needs SHA256 Algorithm (SHA1 will not be supported) so that they can set the SSO on the appropriate server like **app2101** etc.</span></span>
  

> [!TIP]
> <span data-ttu-id="084d8-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="084d8-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="084d8-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="084d8-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="084d8-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="084d8-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="084d8-176">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="084d8-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="084d8-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="084d8-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="084d8-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="084d8-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="084d8-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="084d8-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/birst-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="084d8-182">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="084d8-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/birst-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="084d8-184">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="084d8-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/birst-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="084d8-186">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="084d8-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/birst-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="084d8-188">a.</span><span class="sxs-lookup"><span data-stu-id="084d8-188">a.</span></span> <span data-ttu-id="084d8-189">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="084d8-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="084d8-190">b.</span><span class="sxs-lookup"><span data-stu-id="084d8-190">b.</span></span> <span data-ttu-id="084d8-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="084d8-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="084d8-192">c.</span><span class="sxs-lookup"><span data-stu-id="084d8-192">c.</span></span> <span data-ttu-id="084d8-193">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="084d8-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="084d8-194">d.</span><span class="sxs-lookup"><span data-stu-id="084d8-194">d.</span></span> <span data-ttu-id="084d8-195">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="084d8-195">Click **Create**.</span></span>
 
### <a name="creating-a-birst-agile-business-analytics-test-user"></a><span data-ttu-id="084d8-196">Creating a Birst Agile Business Analytics test user</span><span class="sxs-lookup"><span data-stu-id="084d8-196">Creating a Birst Agile Business Analytics test user</span></span>

<span data-ttu-id="084d8-197">The objective of this section is to create a user called Britta Simon in Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="084d8-197">The objective of this section is to create a user called Britta Simon in Birst Agile Business Analytics.</span></span> <span data-ttu-id="084d8-198">Work with [Birst Agile Business Analytics support team](mailto:info@birst.com) to add the users in the Birst account.</span><span class="sxs-lookup"><span data-stu-id="084d8-198">Work with [Birst Agile Business Analytics support team](mailto:info@birst.com) to add the users in the Birst account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="084d8-199">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="084d8-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="084d8-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="084d8-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Birst Agile Business Analytics.</span></span>

![Assign User][200] 

<span data-ttu-id="084d8-202">**To assign Britta Simon to Birst Agile Business Analytics, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="084d8-202">**To assign Britta Simon to Birst Agile Business Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="084d8-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="084d8-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="084d8-205">In the applications list, select **Birst Agile Business Analytics**.</span><span class="sxs-lookup"><span data-stu-id="084d8-205">In the applications list, select **Birst Agile Business Analytics**.</span></span>

    ![Configure Single Sign-On](./media/birst-tutorial/tutorial_birst_app.png) 

1. <span data-ttu-id="084d8-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="084d8-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="084d8-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="084d8-209">Click **Add** button.</span></span> <span data-ttu-id="084d8-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="084d8-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="084d8-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="084d8-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="084d8-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="084d8-213">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="084d8-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="084d8-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="084d8-215">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="084d8-215">Testing single sign-on</span></span>

<span data-ttu-id="084d8-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="084d8-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="084d8-217">When you click the Birst Agile Business Analytics tile in the Access Panel, you should get automatically signed-on to your Birst Agile Business Analytics application.</span><span class="sxs-lookup"><span data-stu-id="084d8-217">When you click the Birst Agile Business Analytics tile in the Access Panel, you should get automatically signed-on to your Birst Agile Business Analytics application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="084d8-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="084d8-218">Additional resources</span></span>

* [<span data-ttu-id="084d8-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="084d8-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="084d8-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="084d8-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/birst-tutorial/tutorial_general_01.png
[2]: ./media/birst-tutorial/tutorial_general_02.png
[3]: ./media/birst-tutorial/tutorial_general_03.png
[4]: ./media/birst-tutorial/tutorial_general_04.png

[100]: ./media/birst-tutorial/tutorial_general_100.png

[200]: ./media/birst-tutorial/tutorial_general_200.png
[201]: ./media/birst-tutorial/tutorial_general_201.png
[202]: ./media/birst-tutorial/tutorial_general_202.png
[203]: ./media/birst-tutorial/tutorial_general_203.png

