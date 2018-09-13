---
title: 'Tutorial: Azure Active Directory integration with SumoLogic | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SumoLogic.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: dbebf2605fb214a167a276ec8dc344ff450ae5c0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969203"
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a><span data-ttu-id="91064-103">Tutorial: Azure Active Directory integration with SumoLogic</span><span class="sxs-lookup"><span data-stu-id="91064-103">Tutorial: Azure Active Directory integration with SumoLogic</span></span>

<span data-ttu-id="91064-104">In this tutorial, you learn how to integrate SumoLogic with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="91064-104">In this tutorial, you learn how to integrate SumoLogic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="91064-105">Integrating SumoLogic with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="91064-105">Integrating SumoLogic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="91064-106">You can control in Azure AD who has access to SumoLogic</span><span class="sxs-lookup"><span data-stu-id="91064-106">You can control in Azure AD who has access to SumoLogic</span></span>
- <span data-ttu-id="91064-107">You can enable your users to automatically get signed-on to SumoLogic (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="91064-107">You can enable your users to automatically get signed-on to SumoLogic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="91064-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="91064-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="91064-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="91064-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91064-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="91064-110">Prerequisites</span></span>

<span data-ttu-id="91064-111">To configure Azure AD integration with SumoLogic, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="91064-111">To configure Azure AD integration with SumoLogic, you need the following items:</span></span>

- <span data-ttu-id="91064-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="91064-112">An Azure AD subscription</span></span>
- <span data-ttu-id="91064-113">A SumoLogic single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="91064-113">A SumoLogic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="91064-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="91064-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="91064-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="91064-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="91064-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="91064-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="91064-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="91064-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="91064-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="91064-118">Scenario description</span></span>
<span data-ttu-id="91064-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="91064-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="91064-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="91064-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="91064-121">Adding SumoLogic from the gallery</span><span class="sxs-lookup"><span data-stu-id="91064-121">Adding SumoLogic from the gallery</span></span>
1. <span data-ttu-id="91064-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="91064-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sumologic-from-the-gallery"></a><span data-ttu-id="91064-123">Adding SumoLogic from the gallery</span><span class="sxs-lookup"><span data-stu-id="91064-123">Adding SumoLogic from the gallery</span></span>
<span data-ttu-id="91064-124">To configure the integration of SumoLogic into Azure AD, you need to add SumoLogic from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="91064-124">To configure the integration of SumoLogic into Azure AD, you need to add SumoLogic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="91064-125">**To add SumoLogic from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91064-125">**To add SumoLogic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="91064-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="91064-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="91064-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="91064-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="91064-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="91064-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="91064-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="91064-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="91064-133">In the search box, type **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="91064-133">In the search box, type **SumoLogic**.</span></span>

    ![Creating an Azure AD test user](./media/sumologic-tutorial/tutorial_sumologic_search.png)

1. <span data-ttu-id="91064-135">In the results panel, select **SumoLogic**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="91064-135">In the results panel, select **SumoLogic**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="91064-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="91064-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="91064-138">In this section, you configure and test Azure AD single sign-on with SumoLogic based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="91064-138">In this section, you configure and test Azure AD single sign-on with SumoLogic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="91064-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SumoLogic is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91064-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SumoLogic is to a user in Azure AD.</span></span> <span data-ttu-id="91064-140">In other words, a link relationship between an Azure AD user and the related user in SumoLogic needs to be established.</span><span class="sxs-lookup"><span data-stu-id="91064-140">In other words, a link relationship between an Azure AD user and the related user in SumoLogic needs to be established.</span></span>

<span data-ttu-id="91064-141">In SumoLogic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="91064-141">In SumoLogic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="91064-142">To configure and test Azure AD single sign-on with SumoLogic, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="91064-142">To configure and test Azure AD single sign-on with SumoLogic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="91064-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="91064-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="91064-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91064-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="91064-145">**[Creating a SumoLogic test user](#creating-a-sumologic-test-user)** - to have a counterpart of Britta Simon in SumoLogic that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="91064-145">**[Creating a SumoLogic test user](#creating-a-sumologic-test-user)** - to have a counterpart of Britta Simon in SumoLogic that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="91064-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="91064-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="91064-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="91064-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="91064-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="91064-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="91064-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SumoLogic application.</span><span class="sxs-lookup"><span data-stu-id="91064-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SumoLogic application.</span></span>

<span data-ttu-id="91064-150">**To configure Azure AD single sign-on with SumoLogic, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91064-150">**To configure Azure AD single sign-on with SumoLogic, perform the following steps:**</span></span>

1. <span data-ttu-id="91064-151">In the Azure portal, on the **SumoLogic** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="91064-151">In the Azure portal, on the **SumoLogic** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="91064-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="91064-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/sumologic-tutorial/tutorial_sumologic_samlbase.png)

1. <span data-ttu-id="91064-155">On the **SumoLogic Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="91064-155">On the **SumoLogic Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/sumologic-tutorial/tutorial_sumologic_url.png)

    <span data-ttu-id="91064-157">a.</span><span class="sxs-lookup"><span data-stu-id="91064-157">a.</span></span> <span data-ttu-id="91064-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.SumoLogic.com`</span><span class="sxs-lookup"><span data-stu-id="91064-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.SumoLogic.com`</span></span>

    <span data-ttu-id="91064-159">b.</span><span class="sxs-lookup"><span data-stu-id="91064-159">b.</span></span> <span data-ttu-id="91064-160">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="91064-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > <span data-ttu-id="91064-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="91064-161">These values are not real.</span></span> <span data-ttu-id="91064-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="91064-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="91064-163">Contact [SumoLogic Client support team](https://www.sumologic.com/contact-us/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="91064-163">Contact [SumoLogic Client support team](https://www.sumologic.com/contact-us/) to get these values.</span></span> 
 
1. <span data-ttu-id="91064-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="91064-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/sumologic-tutorial/tutorial_sumologic_certificate.png) 

1. <span data-ttu-id="91064-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="91064-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/sumologic-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="91064-168">On the **SumoLogic Configuration** section, click **Configure SumoLogic** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="91064-168">On the **SumoLogic Configuration** section, click **Configure SumoLogic** to open **Configure sign-on** window.</span></span> <span data-ttu-id="91064-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="91064-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/sumologic-tutorial/tutorial_sumologic_configure.png) 

1. <span data-ttu-id="91064-171">In a different web browser window, log in to your SumoLogic company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="91064-171">In a different web browser window, log in to your SumoLogic company site as an administrator.</span></span>

1. <span data-ttu-id="91064-172">Go to **Manage \> Security**.</span><span class="sxs-lookup"><span data-stu-id="91064-172">Go to **Manage \> Security**.</span></span>
   
    <span data-ttu-id="91064-173">![Manage](./media/sumologic-tutorial/ic778556.png "Manage")</span><span class="sxs-lookup"><span data-stu-id="91064-173">![Manage](./media/sumologic-tutorial/ic778556.png "Manage")</span></span>

1. <span data-ttu-id="91064-174">Click **SAML**.</span><span class="sxs-lookup"><span data-stu-id="91064-174">Click **SAML**.</span></span>
   
    <span data-ttu-id="91064-175">![Global security settings](./media/sumologic-tutorial/ic778557.png "Global security settings")</span><span class="sxs-lookup"><span data-stu-id="91064-175">![Global security settings](./media/sumologic-tutorial/ic778557.png "Global security settings")</span></span>

1. <span data-ttu-id="91064-176">From the **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="91064-176">From the **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span></span>
   
    <span data-ttu-id="91064-177">![Configure SAML 2.0](./media/sumologic-tutorial/ic778558.png "Configure SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="91064-177">![Configure SAML 2.0](./media/sumologic-tutorial/ic778558.png "Configure SAML 2.0")</span></span>

1. <span data-ttu-id="91064-178">On the **Configure SAML 2.0** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="91064-178">On the **Configure SAML 2.0** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="91064-179">![Configure SAML 2.0](./media/sumologic-tutorial/ic778559.png "Configure SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="91064-179">![Configure SAML 2.0](./media/sumologic-tutorial/ic778559.png "Configure SAML 2.0")</span></span>
   
    <span data-ttu-id="91064-180">a.</span><span class="sxs-lookup"><span data-stu-id="91064-180">a.</span></span> <span data-ttu-id="91064-181">In the **Configuration Name** textbox, type **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="91064-181">In the **Configuration Name** textbox, type **Azure AD**.</span></span> 

    <span data-ttu-id="91064-182">b.</span><span class="sxs-lookup"><span data-stu-id="91064-182">b.</span></span> <span data-ttu-id="91064-183">Select **Debug Mode**.</span><span class="sxs-lookup"><span data-stu-id="91064-183">Select **Debug Mode**.</span></span>

    <span data-ttu-id="91064-184">c.</span><span class="sxs-lookup"><span data-stu-id="91064-184">c.</span></span> <span data-ttu-id="91064-185">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="91064-185">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="91064-186">d.</span><span class="sxs-lookup"><span data-stu-id="91064-186">d.</span></span> <span data-ttu-id="91064-187">In the **Authn Request URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="91064-187">In the **Authn Request URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="91064-188">e.</span><span class="sxs-lookup"><span data-stu-id="91064-188">e.</span></span> <span data-ttu-id="91064-189">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="91064-189">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>

    <span data-ttu-id="91064-190">f.</span><span class="sxs-lookup"><span data-stu-id="91064-190">f.</span></span> <span data-ttu-id="91064-191">As **Email Attribute**, select **Use SAML subject**.</span><span class="sxs-lookup"><span data-stu-id="91064-191">As **Email Attribute**, select **Use SAML subject**.</span></span>  

    <span data-ttu-id="91064-192">g.</span><span class="sxs-lookup"><span data-stu-id="91064-192">g.</span></span> <span data-ttu-id="91064-193">Select **SP initiated Login Configuration**.</span><span class="sxs-lookup"><span data-stu-id="91064-193">Select **SP initiated Login Configuration**.</span></span>

    <span data-ttu-id="91064-194">h.</span><span class="sxs-lookup"><span data-stu-id="91064-194">h.</span></span> <span data-ttu-id="91064-195">In the **Login Path** textbox, type **Azure** and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="91064-195">In the **Login Path** textbox, type **Azure** and click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="91064-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="91064-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="91064-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="91064-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="91064-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="91064-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="91064-199">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="91064-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="91064-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91064-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="91064-202">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91064-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="91064-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="91064-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/sumologic-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="91064-205">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="91064-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/sumologic-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="91064-207">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="91064-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/sumologic-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="91064-209">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="91064-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/sumologic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="91064-211">a.</span><span class="sxs-lookup"><span data-stu-id="91064-211">a.</span></span> <span data-ttu-id="91064-212">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="91064-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="91064-213">b.</span><span class="sxs-lookup"><span data-stu-id="91064-213">b.</span></span> <span data-ttu-id="91064-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="91064-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="91064-215">c.</span><span class="sxs-lookup"><span data-stu-id="91064-215">c.</span></span> <span data-ttu-id="91064-216">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="91064-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="91064-217">d.</span><span class="sxs-lookup"><span data-stu-id="91064-217">d.</span></span> <span data-ttu-id="91064-218">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="91064-218">Click **Create**.</span></span>
 
### <a name="creating-a-sumologic-test-user"></a><span data-ttu-id="91064-219">Creating a SumoLogic test user</span><span class="sxs-lookup"><span data-stu-id="91064-219">Creating a SumoLogic test user</span></span>

<span data-ttu-id="91064-220">In order to enable Azure AD users to log in to SumoLogic, they must be provisioned to SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="91064-220">In order to enable Azure AD users to log in to SumoLogic, they must be provisioned to SumoLogic.</span></span>  

* <span data-ttu-id="91064-221">In the case of SumoLogic, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="91064-221">In the case of SumoLogic, provisioning is a manual task.</span></span>

<span data-ttu-id="91064-222">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91064-222">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="91064-223">Log in to your **SumoLogic** tenant.</span><span class="sxs-lookup"><span data-stu-id="91064-223">Log in to your **SumoLogic** tenant.</span></span>

1. <span data-ttu-id="91064-224">Go to **Manage \> Users**.</span><span class="sxs-lookup"><span data-stu-id="91064-224">Go to **Manage \> Users**.</span></span>
   
    <span data-ttu-id="91064-225">![Users](./media/sumologic-tutorial/ic778561.png "Users")</span><span class="sxs-lookup"><span data-stu-id="91064-225">![Users](./media/sumologic-tutorial/ic778561.png "Users")</span></span>

1. <span data-ttu-id="91064-226">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="91064-226">Click **Add**.</span></span>
   
    <span data-ttu-id="91064-227">![Users](./media/sumologic-tutorial/ic778562.png "Users")</span><span class="sxs-lookup"><span data-stu-id="91064-227">![Users](./media/sumologic-tutorial/ic778562.png "Users")</span></span>

1. <span data-ttu-id="91064-228">On the **New User** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="91064-228">On the **New User** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="91064-229">![New User](./media/sumologic-tutorial/ic778563.png "New User")</span><span class="sxs-lookup"><span data-stu-id="91064-229">![New User](./media/sumologic-tutorial/ic778563.png "New User")</span></span> 
 
    <span data-ttu-id="91064-230">a.</span><span class="sxs-lookup"><span data-stu-id="91064-230">a.</span></span> <span data-ttu-id="91064-231">Type the related information of the Azure AD account you want to provision into the **First Name**, **Last Name**, and **Email** textboxes.</span><span class="sxs-lookup"><span data-stu-id="91064-231">Type the related information of the Azure AD account you want to provision into the **First Name**, **Last Name**, and **Email** textboxes.</span></span>
  
    <span data-ttu-id="91064-232">b.</span><span class="sxs-lookup"><span data-stu-id="91064-232">b.</span></span> <span data-ttu-id="91064-233">Select a role.</span><span class="sxs-lookup"><span data-stu-id="91064-233">Select a role.</span></span>
  
    <span data-ttu-id="91064-234">c.</span><span class="sxs-lookup"><span data-stu-id="91064-234">c.</span></span> <span data-ttu-id="91064-235">As **Status**, select **Active**.</span><span class="sxs-lookup"><span data-stu-id="91064-235">As **Status**, select **Active**.</span></span>
  
    <span data-ttu-id="91064-236">d.</span><span class="sxs-lookup"><span data-stu-id="91064-236">d.</span></span> <span data-ttu-id="91064-237">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="91064-237">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="91064-238">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="91064-238">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="91064-239">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="91064-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="91064-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="91064-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SumoLogic.</span></span>

![Assign User][200] 

<span data-ttu-id="91064-242">**To assign Britta Simon to SumoLogic, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91064-242">**To assign Britta Simon to SumoLogic, perform the following steps:**</span></span>

1. <span data-ttu-id="91064-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="91064-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="91064-245">In the applications list, select **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="91064-245">In the applications list, select **SumoLogic**.</span></span>

    ![Configure Single Sign-On](./media/sumologic-tutorial/tutorial_sumologic_app.png) 

1. <span data-ttu-id="91064-247">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="91064-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="91064-249">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="91064-249">Click **Add** button.</span></span> <span data-ttu-id="91064-250">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="91064-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="91064-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="91064-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="91064-253">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="91064-253">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="91064-254">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="91064-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="91064-255">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="91064-255">Testing single sign-on</span></span>

<span data-ttu-id="91064-256">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="91064-256">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="91064-257">When you click the SumoLogic tile in the Access Panel, you should get automatically signed-on to your SumoLogic application.</span><span class="sxs-lookup"><span data-stu-id="91064-257">When you click the SumoLogic tile in the Access Panel, you should get automatically signed-on to your SumoLogic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="91064-258">Additional resources</span><span class="sxs-lookup"><span data-stu-id="91064-258">Additional resources</span></span>

* [<span data-ttu-id="91064-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="91064-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="91064-260">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="91064-260">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/sumologic-tutorial/tutorial_general_01.png
[2]: ./media/sumologic-tutorial/tutorial_general_02.png
[3]: ./media/sumologic-tutorial/tutorial_general_03.png
[4]: ./media/sumologic-tutorial/tutorial_general_04.png

[100]: ./media/sumologic-tutorial/tutorial_general_100.png

[200]: ./media/sumologic-tutorial/tutorial_general_200.png
[201]: ./media/sumologic-tutorial/tutorial_general_201.png
[202]: ./media/sumologic-tutorial/tutorial_general_202.png
[203]: ./media/sumologic-tutorial/tutorial_general_203.png

