---
title: 'Tutorial: Azure Active Directory integration with Aha! | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Aha!.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 30f0f316727cfcf20daa58c35d0ba11c25311898
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865880"
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a><span data-ttu-id="03a50-104">Tutorial: Azure Active Directory integration with Aha!</span><span class="sxs-lookup"><span data-stu-id="03a50-104">Tutorial: Azure Active Directory integration with Aha!</span></span>

<span data-ttu-id="03a50-105">In this tutorial, you learn how to integrate Aha!</span><span class="sxs-lookup"><span data-stu-id="03a50-105">In this tutorial, you learn how to integrate Aha!</span></span> <span data-ttu-id="03a50-106">with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="03a50-106">with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="03a50-107">Integrating Aha!</span><span class="sxs-lookup"><span data-stu-id="03a50-107">Integrating Aha!</span></span> <span data-ttu-id="03a50-108">with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="03a50-108">with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="03a50-109">You can control in Azure AD who has access to Aha!</span><span class="sxs-lookup"><span data-stu-id="03a50-109">You can control in Azure AD who has access to Aha!</span></span>
- <span data-ttu-id="03a50-110">You can enable your users to automatically get signed-on to Aha!</span><span class="sxs-lookup"><span data-stu-id="03a50-110">You can enable your users to automatically get signed-on to Aha!</span></span> <span data-ttu-id="03a50-111">(Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="03a50-111">(Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="03a50-112">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="03a50-112">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="03a50-113">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="03a50-113">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03a50-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="03a50-114">Prerequisites</span></span>

<span data-ttu-id="03a50-115">To configure Azure AD integration with Aha!, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="03a50-115">To configure Azure AD integration with Aha!, you need the following items:</span></span>

- <span data-ttu-id="03a50-116">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="03a50-116">An Azure AD subscription</span></span>
- <span data-ttu-id="03a50-117">An Aha!</span><span class="sxs-lookup"><span data-stu-id="03a50-117">An Aha!</span></span> <span data-ttu-id="03a50-118">single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="03a50-118">single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="03a50-119">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="03a50-119">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="03a50-120">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="03a50-120">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="03a50-121">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="03a50-121">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="03a50-122">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="03a50-122">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="03a50-123">Scenario description</span><span class="sxs-lookup"><span data-stu-id="03a50-123">Scenario description</span></span>
<span data-ttu-id="03a50-124">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="03a50-124">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="03a50-125">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="03a50-125">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="03a50-126">Adding Aha!</span><span class="sxs-lookup"><span data-stu-id="03a50-126">Adding Aha!</span></span> <span data-ttu-id="03a50-127">from the gallery</span><span class="sxs-lookup"><span data-stu-id="03a50-127">from the gallery</span></span>
2. <span data-ttu-id="03a50-128">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="03a50-128">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aha-from-the-gallery"></a><span data-ttu-id="03a50-129">Adding Aha!</span><span class="sxs-lookup"><span data-stu-id="03a50-129">Adding Aha!</span></span> <span data-ttu-id="03a50-130">from the gallery</span><span class="sxs-lookup"><span data-stu-id="03a50-130">from the gallery</span></span>
<span data-ttu-id="03a50-131">To configure the integration of Aha!</span><span class="sxs-lookup"><span data-stu-id="03a50-131">To configure the integration of Aha!</span></span> <span data-ttu-id="03a50-132">into Azure AD, you need to add Aha!</span><span class="sxs-lookup"><span data-stu-id="03a50-132">into Azure AD, you need to add Aha!</span></span> <span data-ttu-id="03a50-133">from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="03a50-133">from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="03a50-134">**To add Aha! from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="03a50-134">**To add Aha! from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="03a50-135">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="03a50-135">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="03a50-137">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="03a50-137">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="03a50-138">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="03a50-138">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="03a50-140">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="03a50-140">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="03a50-142">In the search box, type **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="03a50-142">In the search box, type **Aha!**.</span></span>

    ![Creating an Azure AD test user](./media/aha-tutorial/tutorial_aha_search.png)

5. <span data-ttu-id="03a50-144">In the results panel, select **Aha!**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="03a50-144">In the results panel, select **Aha!**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="03a50-146">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="03a50-146">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="03a50-147">In this section, you configure and test Azure AD single sign-on with Aha!</span><span class="sxs-lookup"><span data-stu-id="03a50-147">In this section, you configure and test Azure AD single sign-on with Aha!</span></span> <span data-ttu-id="03a50-148">based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="03a50-148">based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="03a50-149">For single sign-on to work, Azure AD needs to know what the counterpart user in Aha!</span><span class="sxs-lookup"><span data-stu-id="03a50-149">For single sign-on to work, Azure AD needs to know what the counterpart user in Aha!</span></span> <span data-ttu-id="03a50-150">is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03a50-150">is to a user in Azure AD.</span></span> <span data-ttu-id="03a50-151">In other words, a link relationship between an Azure AD user and the related user in Aha!</span><span class="sxs-lookup"><span data-stu-id="03a50-151">In other words, a link relationship between an Azure AD user and the related user in Aha!</span></span> <span data-ttu-id="03a50-152">needs to be established.</span><span class="sxs-lookup"><span data-stu-id="03a50-152">needs to be established.</span></span>

<span data-ttu-id="03a50-153">In Aha!, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="03a50-153">In Aha!, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="03a50-154">To configure and test Azure AD single sign-on with Aha!, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="03a50-154">To configure and test Azure AD single sign-on with Aha!, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="03a50-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="03a50-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="03a50-156">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="03a50-156">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="03a50-157">**[Creating an Aha! test user](#creating-an-aha-test-user)** - to have a counterpart of Britta Simon in Aha!</span><span class="sxs-lookup"><span data-stu-id="03a50-157">**[Creating an Aha! test user](#creating-an-aha-test-user)** - to have a counterpart of Britta Simon in Aha!</span></span> <span data-ttu-id="03a50-158">that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="03a50-158">that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="03a50-159">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="03a50-159">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="03a50-160">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="03a50-160">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="03a50-161">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="03a50-161">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="03a50-162">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Aha!</span><span class="sxs-lookup"><span data-stu-id="03a50-162">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Aha!</span></span> <span data-ttu-id="03a50-163">application.</span><span class="sxs-lookup"><span data-stu-id="03a50-163">application.</span></span>

<span data-ttu-id="03a50-164">**To configure Azure AD single sign-on with Aha!, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="03a50-164">**To configure Azure AD single sign-on with Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="03a50-165">In the Azure portal, on the **Aha!**</span><span class="sxs-lookup"><span data-stu-id="03a50-165">In the Azure portal, on the **Aha!**</span></span> <span data-ttu-id="03a50-166">application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="03a50-166">application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="03a50-168">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="03a50-168">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/aha-tutorial/tutorial_aha_samlbase.png)

3. <span data-ttu-id="03a50-170">On the **Aha! Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="03a50-170">On the **Aha! Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/aha-tutorial/tutorial_aha_url.png)

    <span data-ttu-id="03a50-172">a.</span><span class="sxs-lookup"><span data-stu-id="03a50-172">a.</span></span> <span data-ttu-id="03a50-173">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.aha.io/session/new`</span><span class="sxs-lookup"><span data-stu-id="03a50-173">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.aha.io/session/new`</span></span>

    <span data-ttu-id="03a50-174">b.</span><span class="sxs-lookup"><span data-stu-id="03a50-174">b.</span></span> <span data-ttu-id="03a50-175">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.aha.io`</span><span class="sxs-lookup"><span data-stu-id="03a50-175">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.aha.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="03a50-176">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="03a50-176">These values are not real.</span></span> <span data-ttu-id="03a50-177">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="03a50-177">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="03a50-178">Contact [Aha! Client support team](https://www.aha.io/company/contact) to get these values.</span><span class="sxs-lookup"><span data-stu-id="03a50-178">Contact [Aha! Client support team](https://www.aha.io/company/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="03a50-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="03a50-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/aha-tutorial/tutorial_aha_certificate.png) 

5. <span data-ttu-id="03a50-181">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="03a50-181">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/aha-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="03a50-183">In a different web browser window, log in to your Aha!</span><span class="sxs-lookup"><span data-stu-id="03a50-183">In a different web browser window, log in to your Aha!</span></span> <span data-ttu-id="03a50-184">company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="03a50-184">company site as an administrator.</span></span>

7. <span data-ttu-id="03a50-185">In the menu on the top, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="03a50-185">In the menu on the top, click **Settings**.</span></span>

    <span data-ttu-id="03a50-186">![Settings](./media/aha-tutorial/IC798950.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="03a50-186">![Settings](./media/aha-tutorial/IC798950.png "Settings")</span></span>

8. <span data-ttu-id="03a50-187">Click **Account**.</span><span class="sxs-lookup"><span data-stu-id="03a50-187">Click **Account**.</span></span>
   
    <span data-ttu-id="03a50-188">![Profile](./media/aha-tutorial/IC798951.png "Profile")</span><span class="sxs-lookup"><span data-stu-id="03a50-188">![Profile](./media/aha-tutorial/IC798951.png "Profile")</span></span>

9. <span data-ttu-id="03a50-189">Click **Security and single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="03a50-189">Click **Security and single sign-on**.</span></span>
   
    <span data-ttu-id="03a50-190">![Security and single sign-on](./media/aha-tutorial/IC798952.png "Security and single sign-on")</span><span class="sxs-lookup"><span data-stu-id="03a50-190">![Security and single sign-on](./media/aha-tutorial/IC798952.png "Security and single sign-on")</span></span>

10. <span data-ttu-id="03a50-191">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span><span class="sxs-lookup"><span data-stu-id="03a50-191">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span></span>
   
    <span data-ttu-id="03a50-192">![Security and single sign-on](./media/aha-tutorial/IC798953.png "Security and single sign-on")</span><span class="sxs-lookup"><span data-stu-id="03a50-192">![Security and single sign-on](./media/aha-tutorial/IC798953.png "Security and single sign-on")</span></span>

11. <span data-ttu-id="03a50-193">On the **Single Sign-On** configuration page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="03a50-193">On the **Single Sign-On** configuration page, perform the following steps:</span></span>
    
    <span data-ttu-id="03a50-194">![Single Sign-On](./media/aha-tutorial/IC798954.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="03a50-194">![Single Sign-On](./media/aha-tutorial/IC798954.png "Single Sign-On")</span></span>
    
       <span data-ttu-id="03a50-195">a.</span><span class="sxs-lookup"><span data-stu-id="03a50-195">a.</span></span> <span data-ttu-id="03a50-196">In the **Name** textbox, type a name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="03a50-196">In the **Name** textbox, type a name for your configuration.</span></span>

       <span data-ttu-id="03a50-197">b.</span><span class="sxs-lookup"><span data-stu-id="03a50-197">b.</span></span> <span data-ttu-id="03a50-198">For **Configure using**, select **Metadata File**.</span><span class="sxs-lookup"><span data-stu-id="03a50-198">For **Configure using**, select **Metadata File**.</span></span>
   
       <span data-ttu-id="03a50-199">c.</span><span class="sxs-lookup"><span data-stu-id="03a50-199">c.</span></span> <span data-ttu-id="03a50-200">To upload your downloaded metadata file, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="03a50-200">To upload your downloaded metadata file, click **Browse**.</span></span>
   
       <span data-ttu-id="03a50-201">d.</span><span class="sxs-lookup"><span data-stu-id="03a50-201">d.</span></span> <span data-ttu-id="03a50-202">Click **Update**.</span><span class="sxs-lookup"><span data-stu-id="03a50-202">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="03a50-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="03a50-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="03a50-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="03a50-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="03a50-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="03a50-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="03a50-206">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="03a50-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="03a50-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="03a50-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="03a50-209">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="03a50-209">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="03a50-210">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="03a50-210">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/aha-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="03a50-212">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="03a50-212">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/aha-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="03a50-214">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="03a50-214">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/aha-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="03a50-216">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="03a50-216">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/aha-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="03a50-218">a.</span><span class="sxs-lookup"><span data-stu-id="03a50-218">a.</span></span> <span data-ttu-id="03a50-219">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="03a50-219">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="03a50-220">b.</span><span class="sxs-lookup"><span data-stu-id="03a50-220">b.</span></span> <span data-ttu-id="03a50-221">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="03a50-221">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="03a50-222">c.</span><span class="sxs-lookup"><span data-stu-id="03a50-222">c.</span></span> <span data-ttu-id="03a50-223">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="03a50-223">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="03a50-224">d.</span><span class="sxs-lookup"><span data-stu-id="03a50-224">d.</span></span> <span data-ttu-id="03a50-225">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="03a50-225">Click **Create**.</span></span>
 
### <a name="creating-an-aha-test-user"></a><span data-ttu-id="03a50-226">Creating an Aha!</span><span class="sxs-lookup"><span data-stu-id="03a50-226">Creating an Aha!</span></span> <span data-ttu-id="03a50-227">test user</span><span class="sxs-lookup"><span data-stu-id="03a50-227">test user</span></span>

<span data-ttu-id="03a50-228">To enable Azure AD users to log in to Aha!, they must be provisioned into Aha!.</span><span class="sxs-lookup"><span data-stu-id="03a50-228">To enable Azure AD users to log in to Aha!, they must be provisioned into Aha!.</span></span>  

<span data-ttu-id="03a50-229">In the case of Aha!, provisioning is an automated task.</span><span class="sxs-lookup"><span data-stu-id="03a50-229">In the case of Aha!, provisioning is an automated task.</span></span> <span data-ttu-id="03a50-230">There is no action item for you.</span><span class="sxs-lookup"><span data-stu-id="03a50-230">There is no action item for you.</span></span>

<span data-ttu-id="03a50-231">Users are automatically created if necessary during the first single sign-on attempt.</span><span class="sxs-lookup"><span data-stu-id="03a50-231">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="03a50-232">You can use any other Aha!</span><span class="sxs-lookup"><span data-stu-id="03a50-232">You can use any other Aha!</span></span> <span data-ttu-id="03a50-233">user account creation tools or APIs provided by Aha!</span><span class="sxs-lookup"><span data-stu-id="03a50-233">user account creation tools or APIs provided by Aha!</span></span> <span data-ttu-id="03a50-234">to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="03a50-234">to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="03a50-235">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="03a50-235">Assigning the Azure AD test user</span></span>

<span data-ttu-id="03a50-236">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Aha!.</span><span class="sxs-lookup"><span data-stu-id="03a50-236">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Aha!.</span></span>

![Assign User][200] 

<span data-ttu-id="03a50-238">**To assign Britta Simon to Aha!, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="03a50-238">**To assign Britta Simon to Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="03a50-239">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="03a50-239">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="03a50-241">In the applications list, select **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="03a50-241">In the applications list, select **Aha!**.</span></span>

    ![Configure Single Sign-On](./media/aha-tutorial/tutorial_aha_app.png) 

3. <span data-ttu-id="03a50-243">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="03a50-243">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="03a50-245">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="03a50-245">Click **Add** button.</span></span> <span data-ttu-id="03a50-246">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="03a50-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="03a50-248">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="03a50-248">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="03a50-249">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="03a50-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="03a50-250">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="03a50-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="03a50-251">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="03a50-251">Testing single sign-on</span></span>

<span data-ttu-id="03a50-252">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="03a50-252">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="03a50-253">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="03a50-253">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="03a50-254">Additional resources</span><span class="sxs-lookup"><span data-stu-id="03a50-254">Additional resources</span></span>

* [<span data-ttu-id="03a50-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="03a50-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="03a50-256">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="03a50-256">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/aha-tutorial/tutorial_general_01.png
[2]: ./media/aha-tutorial/tutorial_general_02.png
[3]: ./media/aha-tutorial/tutorial_general_03.png
[4]: ./media/aha-tutorial/tutorial_general_04.png

[100]: ./media/aha-tutorial/tutorial_general_100.png

[200]: ./media/aha-tutorial/tutorial_general_200.png
[201]: ./media/aha-tutorial/tutorial_general_201.png
[202]: ./media/aha-tutorial/tutorial_general_202.png
[203]: ./media/aha-tutorial/tutorial_general_203.png

