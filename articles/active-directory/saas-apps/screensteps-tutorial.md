---
title: 'Tutorial: Azure Active Directory integration with ScreenSteps | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ScreenSteps.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: 105ec895635a882d562de48203222702a2c6bfed
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869124"
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a><span data-ttu-id="33ea8-103">Tutorial: Azure Active Directory integration with ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="33ea8-103">Tutorial: Azure Active Directory integration with ScreenSteps</span></span>

<span data-ttu-id="33ea8-104">In this tutorial, you learn how to integrate ScreenSteps with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="33ea8-104">In this tutorial, you learn how to integrate ScreenSteps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="33ea8-105">Integrating ScreenSteps with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="33ea8-105">Integrating ScreenSteps with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="33ea8-106">You can control in Azure AD who has access to ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="33ea8-106">You can control in Azure AD who has access to ScreenSteps.</span></span>
- <span data-ttu-id="33ea8-107">You can enable your users to automatically get signed-on to ScreenSteps (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="33ea8-107">You can enable your users to automatically get signed-on to ScreenSteps (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="33ea8-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="33ea8-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="33ea8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="33ea8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33ea8-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="33ea8-110">Prerequisites</span></span>

<span data-ttu-id="33ea8-111">To configure Azure AD integration with ScreenSteps, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="33ea8-111">To configure Azure AD integration with ScreenSteps, you need the following items:</span></span>

- <span data-ttu-id="33ea8-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="33ea8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="33ea8-113">A ScreenSteps single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="33ea8-113">A ScreenSteps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="33ea8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="33ea8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="33ea8-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="33ea8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="33ea8-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="33ea8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="33ea8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="33ea8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="33ea8-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="33ea8-118">Scenario description</span></span>
<span data-ttu-id="33ea8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="33ea8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="33ea8-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="33ea8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="33ea8-121">Adding ScreenSteps from the gallery</span><span class="sxs-lookup"><span data-stu-id="33ea8-121">Adding ScreenSteps from the gallery</span></span>
1. <span data-ttu-id="33ea8-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="33ea8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-screensteps-from-the-gallery"></a><span data-ttu-id="33ea8-123">Adding ScreenSteps from the gallery</span><span class="sxs-lookup"><span data-stu-id="33ea8-123">Adding ScreenSteps from the gallery</span></span>
<span data-ttu-id="33ea8-124">To configure the integration of ScreenSteps into Azure AD, you need to add ScreenSteps from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="33ea8-124">To configure the integration of ScreenSteps into Azure AD, you need to add ScreenSteps from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="33ea8-125">**To add ScreenSteps from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="33ea8-125">**To add ScreenSteps from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="33ea8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="33ea8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="33ea8-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="33ea8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="33ea8-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="33ea8-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="33ea8-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="33ea8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="33ea8-133">In the search box, type **ScreenSteps**, select **ScreenSteps** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="33ea8-133">In the search box, type **ScreenSteps**, select **ScreenSteps** from result panel then click **Add** button to add the application.</span></span>

    ![ScreenSteps in the results list](./media/screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="33ea8-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="33ea8-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="33ea8-136">In this section, you configure and test Azure AD single sign-on with ScreenSteps based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="33ea8-136">In this section, you configure and test Azure AD single sign-on with ScreenSteps based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="33ea8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ScreenSteps is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33ea8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ScreenSteps is to a user in Azure AD.</span></span> <span data-ttu-id="33ea8-138">In other words, a link relationship between an Azure AD user and the related user in ScreenSteps needs to be established.</span><span class="sxs-lookup"><span data-stu-id="33ea8-138">In other words, a link relationship between an Azure AD user and the related user in ScreenSteps needs to be established.</span></span>

<span data-ttu-id="33ea8-139">In ScreenSteps, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="33ea8-139">In ScreenSteps, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="33ea8-140">To configure and test Azure AD single sign-on with ScreenSteps, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="33ea8-140">To configure and test Azure AD single sign-on with ScreenSteps, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="33ea8-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="33ea8-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="33ea8-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="33ea8-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="33ea8-143">**[Create a ScreenSteps test user](#create-a-screensteps-test-user)** - to have a counterpart of Britta Simon in ScreenSteps that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="33ea8-143">**[Create a ScreenSteps test user](#create-a-screensteps-test-user)** - to have a counterpart of Britta Simon in ScreenSteps that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="33ea8-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="33ea8-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="33ea8-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="33ea8-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="33ea8-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="33ea8-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="33ea8-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScreenSteps application.</span><span class="sxs-lookup"><span data-stu-id="33ea8-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ScreenSteps application.</span></span>

<span data-ttu-id="33ea8-148">**To configure Azure AD single sign-on with ScreenSteps, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="33ea8-148">**To configure Azure AD single sign-on with ScreenSteps, perform the following steps:**</span></span>

1. <span data-ttu-id="33ea8-149">In the Azure portal, on the **ScreenSteps** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="33ea8-149">In the Azure portal, on the **ScreenSteps** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="33ea8-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="33ea8-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/screensteps-tutorial/tutorial_screensteps_samlbase.png)

1. <span data-ttu-id="33ea8-153">On the **ScreenSteps Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="33ea8-153">On the **ScreenSteps Domain and URLs** section, perform the following steps:</span></span>

    ![ScreenSteps Domain and URLs single sign-on information](./media/screensteps-tutorial/tutorial_screensteps_url.png)

    <span data-ttu-id="33ea8-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.ScreenSteps.com`</span><span class="sxs-lookup"><span data-stu-id="33ea8-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.ScreenSteps.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="33ea8-156">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="33ea8-156">This value is not real.</span></span> <span data-ttu-id="33ea8-157">Update this value with the actual Sign-On URL, which is explained later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="33ea8-157">Update this value with the actual Sign-On URL, which is explained later in this tutorial.</span></span> 

1. <span data-ttu-id="33ea8-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="33ea8-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/screensteps-tutorial/tutorial_screensteps_certificate.png) 

1. <span data-ttu-id="33ea8-160">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="33ea8-160">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/screensteps-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="33ea8-162">On the **ScreenSteps Configuration** section, click **Configure ScreenSteps** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="33ea8-162">On the **ScreenSteps Configuration** section, click **Configure ScreenSteps** to open **Configure sign-on** window.</span></span> <span data-ttu-id="33ea8-163">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="33ea8-163">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![ScreenSteps Configuration](./media/screensteps-tutorial/tutorial_screensteps_configure.png) 

1. <span data-ttu-id="33ea8-165">In a different web browser window, log into your ScreenSteps company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="33ea8-165">In a different web browser window, log into your ScreenSteps company site as an administrator.</span></span>

1. <span data-ttu-id="33ea8-166">Click **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="33ea8-166">Click **Account Settings**.</span></span>

    <span data-ttu-id="33ea8-167">![Account management](./media/screensteps-tutorial/ic778523.png "Account management")</span><span class="sxs-lookup"><span data-stu-id="33ea8-167">![Account management](./media/screensteps-tutorial/ic778523.png "Account management")</span></span>

1. <span data-ttu-id="33ea8-168">Click **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="33ea8-168">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="33ea8-169">![Remote authentication](./media/screensteps-tutorial/ic778524.png "Remote authentication")</span><span class="sxs-lookup"><span data-stu-id="33ea8-169">![Remote authentication](./media/screensteps-tutorial/ic778524.png "Remote authentication")</span></span>

1. <span data-ttu-id="33ea8-170">Click **Create Single Sign-on Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="33ea8-170">Click **Create Single Sign-on Endpoint**.</span></span>

    <span data-ttu-id="33ea8-171">![Remote authentication](./media/screensteps-tutorial/ic778525.png "Remote authentication")</span><span class="sxs-lookup"><span data-stu-id="33ea8-171">![Remote authentication](./media/screensteps-tutorial/ic778525.png "Remote authentication")</span></span>

1. <span data-ttu-id="33ea8-172">In the **Create Single Sign-on Endpoint** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="33ea8-172">In the **Create Single Sign-on Endpoint** section, perform the following steps:</span></span>

    <span data-ttu-id="33ea8-173">![Create an authentication endpoint](./media/screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span><span class="sxs-lookup"><span data-stu-id="33ea8-173">![Create an authentication endpoint](./media/screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span></span>
    
    <span data-ttu-id="33ea8-174">a.</span><span class="sxs-lookup"><span data-stu-id="33ea8-174">a.</span></span> <span data-ttu-id="33ea8-175">In the **Title** textbox, type a title.</span><span class="sxs-lookup"><span data-stu-id="33ea8-175">In the **Title** textbox, type a title.</span></span>
    
    <span data-ttu-id="33ea8-176">b.</span><span class="sxs-lookup"><span data-stu-id="33ea8-176">b.</span></span> <span data-ttu-id="33ea8-177">From the **Mode** list, select **SAML**.</span><span class="sxs-lookup"><span data-stu-id="33ea8-177">From the **Mode** list, select **SAML**.</span></span>
    
    <span data-ttu-id="33ea8-178">c.</span><span class="sxs-lookup"><span data-stu-id="33ea8-178">c.</span></span> <span data-ttu-id="33ea8-179">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="33ea8-179">Click **Create**.</span></span>

1. <span data-ttu-id="33ea8-180">**Edit** the new endpoint.</span><span class="sxs-lookup"><span data-stu-id="33ea8-180">**Edit** the new endpoint.</span></span>

    <span data-ttu-id="33ea8-181">![Edit endpoint](./media/screensteps-tutorial/ic778528.png "Edit endpoint")</span><span class="sxs-lookup"><span data-stu-id="33ea8-181">![Edit endpoint](./media/screensteps-tutorial/ic778528.png "Edit endpoint")</span></span>

1. <span data-ttu-id="33ea8-182">In the **Edit Single Sign-on Endpoint** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="33ea8-182">In the **Edit Single Sign-on Endpoint** section, perform the following steps:</span></span>

    <span data-ttu-id="33ea8-183">![Remote authentication endpoint](./media/screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span><span class="sxs-lookup"><span data-stu-id="33ea8-183">![Remote authentication endpoint](./media/screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span></span>

    <span data-ttu-id="33ea8-184">a.</span><span class="sxs-lookup"><span data-stu-id="33ea8-184">a.</span></span> <span data-ttu-id="33ea8-185">Click **Upload new SAML Certificate file**, and then upload the certificate, which you have downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="33ea8-185">Click **Upload new SAML Certificate file**, and then upload the certificate, which you have downloaded from Azure portal.</span></span>
    
    <span data-ttu-id="33ea8-186">b.</span><span class="sxs-lookup"><span data-stu-id="33ea8-186">b.</span></span> <span data-ttu-id="33ea8-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **Remote Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="33ea8-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **Remote Login URL** textbox.</span></span>
    
    <span data-ttu-id="33ea8-188">c.</span><span class="sxs-lookup"><span data-stu-id="33ea8-188">c.</span></span> <span data-ttu-id="33ea8-189">Paste **Sign-Out URL** value, which you have copied from the Azure portal into the **Log out URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="33ea8-189">Paste **Sign-Out URL** value, which you have copied from the Azure portal into the **Log out URL** textbox.</span></span>
    
    <span data-ttu-id="33ea8-190">d.</span><span class="sxs-lookup"><span data-stu-id="33ea8-190">d.</span></span> <span data-ttu-id="33ea8-191">Select a **Group** to assign users to when they are provisioned.</span><span class="sxs-lookup"><span data-stu-id="33ea8-191">Select a **Group** to assign users to when they are provisioned.</span></span>
    
    <span data-ttu-id="33ea8-192">e.</span><span class="sxs-lookup"><span data-stu-id="33ea8-192">e.</span></span> <span data-ttu-id="33ea8-193">Click **Update**.</span><span class="sxs-lookup"><span data-stu-id="33ea8-193">Click **Update**.</span></span>

    <span data-ttu-id="33ea8-194">f.</span><span class="sxs-lookup"><span data-stu-id="33ea8-194">f.</span></span> <span data-ttu-id="33ea8-195">Copy the **SAML Consumer URL** to the clipboard and paste in to the **Sign-on URL** textbox in **ScreenSteps Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="33ea8-195">Copy the **SAML Consumer URL** to the clipboard and paste in to the **Sign-on URL** textbox in **ScreenSteps Domain and URLs** section.</span></span>
    
    <span data-ttu-id="33ea8-196">g.</span><span class="sxs-lookup"><span data-stu-id="33ea8-196">g.</span></span> <span data-ttu-id="33ea8-197">Return to the **Edit Single Sign-on Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="33ea8-197">Return to the **Edit Single Sign-on Endpoint**.</span></span>
    
    <span data-ttu-id="33ea8-198">h.</span><span class="sxs-lookup"><span data-stu-id="33ea8-198">h.</span></span> <span data-ttu-id="33ea8-199">Click the **Make default for account** button to use this endpoint for all users who log into ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="33ea8-199">Click the **Make default for account** button to use this endpoint for all users who log into ScreenSteps.</span></span> <span data-ttu-id="33ea8-200">Alternatively you can click the **Add to Site** button to use this endpoint for specific sites in **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="33ea8-200">Alternatively you can click the **Add to Site** button to use this endpoint for specific sites in **ScreenSteps**.</span></span>

> [!TIP]
> <span data-ttu-id="33ea8-201">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="33ea8-201">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="33ea8-202">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="33ea8-202">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="33ea8-203">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="33ea8-203">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="33ea8-204">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="33ea8-204">Create an Azure AD test user</span></span>

<span data-ttu-id="33ea8-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="33ea8-205">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="33ea8-207">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="33ea8-207">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="33ea8-208">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="33ea8-208">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/screensteps-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="33ea8-210">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="33ea8-210">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/screensteps-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="33ea8-212">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="33ea8-212">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/screensteps-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="33ea8-214">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="33ea8-214">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/screensteps-tutorial/create_aaduser_04.png)

    <span data-ttu-id="33ea8-216">a.</span><span class="sxs-lookup"><span data-stu-id="33ea8-216">a.</span></span> <span data-ttu-id="33ea8-217">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="33ea8-217">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="33ea8-218">b.</span><span class="sxs-lookup"><span data-stu-id="33ea8-218">b.</span></span> <span data-ttu-id="33ea8-219">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="33ea8-219">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="33ea8-220">c.</span><span class="sxs-lookup"><span data-stu-id="33ea8-220">c.</span></span> <span data-ttu-id="33ea8-221">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="33ea8-221">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="33ea8-222">d.</span><span class="sxs-lookup"><span data-stu-id="33ea8-222">d.</span></span> <span data-ttu-id="33ea8-223">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="33ea8-223">Click **Create**.</span></span>
 
### <a name="create-a-screensteps-test-user"></a><span data-ttu-id="33ea8-224">Create a ScreenSteps test user</span><span class="sxs-lookup"><span data-stu-id="33ea8-224">Create a ScreenSteps test user</span></span>

<span data-ttu-id="33ea8-225">In this section, you create a user called Britta Simon in ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="33ea8-225">In this section, you create a user called Britta Simon in ScreenSteps.</span></span> <span data-ttu-id="33ea8-226">Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add the users in the ScreenSteps platform.</span><span class="sxs-lookup"><span data-stu-id="33ea8-226">Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add the users in the ScreenSteps platform.</span></span> <span data-ttu-id="33ea8-227">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="33ea8-227">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="33ea8-228">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="33ea8-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="33ea8-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="33ea8-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ScreenSteps.</span></span>

![Assign the user role][200] 

<span data-ttu-id="33ea8-231">**To assign Britta Simon to ScreenSteps, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="33ea8-231">**To assign Britta Simon to ScreenSteps, perform the following steps:**</span></span>

1. <span data-ttu-id="33ea8-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="33ea8-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="33ea8-234">In the applications list, select **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="33ea8-234">In the applications list, select **ScreenSteps**.</span></span>

    ![The ScreenSteps link in the Applications list](./media/screensteps-tutorial/tutorial_screensteps_app.png)  

1. <span data-ttu-id="33ea8-236">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="33ea8-236">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="33ea8-238">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="33ea8-238">Click **Add** button.</span></span> <span data-ttu-id="33ea8-239">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="33ea8-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="33ea8-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="33ea8-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="33ea8-242">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="33ea8-242">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="33ea8-243">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="33ea8-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="33ea8-244">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="33ea8-244">Test single sign-on</span></span>

<span data-ttu-id="33ea8-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="33ea8-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="33ea8-246">When you click the ScreenSteps tile in the Access Panel, you should get automatically signed-on to your ScreenSteps application.</span><span class="sxs-lookup"><span data-stu-id="33ea8-246">When you click the ScreenSteps tile in the Access Panel, you should get automatically signed-on to your ScreenSteps application.</span></span>
<span data-ttu-id="33ea8-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="33ea8-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="33ea8-248">Additional resources</span><span class="sxs-lookup"><span data-stu-id="33ea8-248">Additional resources</span></span>

* [<span data-ttu-id="33ea8-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="33ea8-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="33ea8-250">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="33ea8-250">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/screensteps-tutorial/tutorial_general_01.png
[2]: ./media/screensteps-tutorial/tutorial_general_02.png
[3]: ./media/screensteps-tutorial/tutorial_general_03.png
[4]: ./media/screensteps-tutorial/tutorial_general_04.png

[100]: ./media/screensteps-tutorial/tutorial_general_100.png

[200]: ./media/screensteps-tutorial/tutorial_general_200.png
[201]: ./media/screensteps-tutorial/tutorial_general_201.png
[202]: ./media/screensteps-tutorial/tutorial_general_202.png
[203]: ./media/screensteps-tutorial/tutorial_general_203.png

