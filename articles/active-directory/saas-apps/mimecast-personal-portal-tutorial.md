---
title: 'Tutorial: Azure Active Directory integration with Mimecast Personal Portal | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Mimecast Personal Portal.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2018
ms.author: jeedes
ms.openlocfilehash: 71ecffebe095fd325837aeb1d6e741a2f3321aea
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866670"
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a><span data-ttu-id="e9129-103">Tutorial: Azure Active Directory integration with Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="e9129-103">Tutorial: Azure Active Directory integration with Mimecast Personal Portal</span></span>

<span data-ttu-id="e9129-104">In this tutorial, you learn how to integrate Mimecast Personal Portal with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e9129-104">In this tutorial, you learn how to integrate Mimecast Personal Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e9129-105">Integrating Mimecast Personal Portal with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="e9129-105">Integrating Mimecast Personal Portal with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e9129-106">You can control in Azure AD who has access to Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="e9129-106">You can control in Azure AD who has access to Mimecast Personal Portal.</span></span>
- <span data-ttu-id="e9129-107">You can enable your users to automatically get signed-on to Mimecast Personal Portal (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="e9129-107">You can enable your users to automatically get signed-on to Mimecast Personal Portal (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e9129-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e9129-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="e9129-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="e9129-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9129-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e9129-110">Prerequisites</span></span>

<span data-ttu-id="e9129-111">To configure Azure AD integration with Mimecast Personal Portal, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="e9129-111">To configure Azure AD integration with Mimecast Personal Portal, you need the following items:</span></span>

- <span data-ttu-id="e9129-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="e9129-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e9129-113">A Mimecast Personal Portal single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="e9129-113">A Mimecast Personal Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e9129-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="e9129-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e9129-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="e9129-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e9129-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="e9129-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e9129-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e9129-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e9129-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="e9129-118">Scenario description</span></span>
<span data-ttu-id="e9129-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="e9129-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e9129-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="e9129-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e9129-121">Adding Mimecast Personal Portal from the gallery</span><span class="sxs-lookup"><span data-stu-id="e9129-121">Adding Mimecast Personal Portal from the gallery</span></span>
1. <span data-ttu-id="e9129-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e9129-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-personal-portal-from-the-gallery"></a><span data-ttu-id="e9129-123">Adding Mimecast Personal Portal from the gallery</span><span class="sxs-lookup"><span data-stu-id="e9129-123">Adding Mimecast Personal Portal from the gallery</span></span>
<span data-ttu-id="e9129-124">To configure the integration of Mimecast Personal Portal into Azure AD, you need to add Mimecast Personal Portal from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="e9129-124">To configure the integration of Mimecast Personal Portal into Azure AD, you need to add Mimecast Personal Portal from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e9129-125">**To add Mimecast Personal Portal from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e9129-125">**To add Mimecast Personal Portal from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e9129-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="e9129-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="e9129-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="e9129-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e9129-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e9129-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="e9129-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="e9129-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="e9129-133">In the search box, type **Mimecast Personal Portal**, select **Mimecast Personal Portal** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="e9129-133">In the search box, type **Mimecast Personal Portal**, select **Mimecast Personal Portal** from result panel then click **Add** button to add the application.</span></span>

    ![Mimecast Personal Portal in the results list](./media/mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e9129-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e9129-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e9129-136">In this section, you configure and test Azure AD single sign-on with Mimecast Personal Portal based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e9129-136">In this section, you configure and test Azure AD single sign-on with Mimecast Personal Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e9129-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Personal Portal is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9129-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Personal Portal is to a user in Azure AD.</span></span> <span data-ttu-id="e9129-138">In other words, a link relationship between an Azure AD user and the related user in Mimecast Personal Portal needs to be established.</span><span class="sxs-lookup"><span data-stu-id="e9129-138">In other words, a link relationship between an Azure AD user and the related user in Mimecast Personal Portal needs to be established.</span></span>

<span data-ttu-id="e9129-139">To configure and test Azure AD single sign-on with Mimecast Personal Portal, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e9129-139">To configure and test Azure AD single sign-on with Mimecast Personal Portal, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e9129-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="e9129-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="e9129-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e9129-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="e9129-142">**[Create a Mimecast Personal Portal test user](#create-a-mimecast-personal-portal-test-user)** - to have a counterpart of Britta Simon in Mimecast Personal Portal that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="e9129-142">**[Create a Mimecast Personal Portal test user](#create-a-mimecast-personal-portal-test-user)** - to have a counterpart of Britta Simon in Mimecast Personal Portal that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="e9129-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e9129-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="e9129-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="e9129-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e9129-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e9129-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e9129-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Personal Portal application.</span><span class="sxs-lookup"><span data-stu-id="e9129-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Personal Portal application.</span></span>

<span data-ttu-id="e9129-147">**To configure Azure AD single sign-on with Mimecast Personal Portal, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e9129-147">**To configure Azure AD single sign-on with Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="e9129-148">In the Azure portal, on the **Mimecast Personal Portal** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e9129-148">In the Azure portal, on the **Mimecast Personal Portal** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="e9129-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e9129-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

1. <span data-ttu-id="e9129-152">On the **Mimecast Personal Portal Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e9129-152">On the **Mimecast Personal Portal Domain and URLs** section, perform the following steps:</span></span>

    ![Mimecast Personal Portal Domain and URLs single sign-on information](./media/mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    <span data-ttu-id="e9129-154">a.</span><span class="sxs-lookup"><span data-stu-id="e9129-154">a.</span></span> <span data-ttu-id="e9129-155">In the **Sign-on URL** textbox, type a URL:</span><span class="sxs-lookup"><span data-stu-id="e9129-155">In the **Sign-on URL** textbox, type a URL:</span></span> 

    | <span data-ttu-id="e9129-156">Region</span><span class="sxs-lookup"><span data-stu-id="e9129-156">Region</span></span>  |  <span data-ttu-id="e9129-157">Value</span><span class="sxs-lookup"><span data-stu-id="e9129-157">Value</span></span> | 
    | --------------- | --------------- | 
    | <span data-ttu-id="e9129-158">Europe</span><span class="sxs-lookup"><span data-stu-id="e9129-158">Europe</span></span>          | `https://eu-api.mimecast.com/login/saml`|
    | <span data-ttu-id="e9129-159">United States</span><span class="sxs-lookup"><span data-stu-id="e9129-159">United States</span></span>   | `https://us-api.mimecast.com/login/saml`|
    | <span data-ttu-id="e9129-160">South Africa</span><span class="sxs-lookup"><span data-stu-id="e9129-160">South Africa</span></span>    | `https://za-api.mimecast.com/login/saml`|
    | <span data-ttu-id="e9129-161">Australia</span><span class="sxs-lookup"><span data-stu-id="e9129-161">Australia</span></span>       | `https://au-api.mimecast.com/login/saml`|
    | <span data-ttu-id="e9129-162">Offshore</span><span class="sxs-lookup"><span data-stu-id="e9129-162">Offshore</span></span>        | `https://jer-api.mimecast.com/login/saml`|

    <span data-ttu-id="e9129-163">b.</span><span class="sxs-lookup"><span data-stu-id="e9129-163">b.</span></span> <span data-ttu-id="e9129-164">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="e9129-164">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    | <span data-ttu-id="e9129-165">Region</span><span class="sxs-lookup"><span data-stu-id="e9129-165">Region</span></span>  |  <span data-ttu-id="e9129-166">Value</span><span class="sxs-lookup"><span data-stu-id="e9129-166">Value</span></span> | 
    | --------------- | --------------- |
    | <span data-ttu-id="e9129-167">Europe</span><span class="sxs-lookup"><span data-stu-id="e9129-167">Europe</span></span>          | `https://eu-api.mimecast.com/sso/<accountcode>`|
    | <span data-ttu-id="e9129-168">United States</span><span class="sxs-lookup"><span data-stu-id="e9129-168">United States</span></span>   | `https://us-api.mimecast.com/sso/<accountcode>`|    
    | <span data-ttu-id="e9129-169">South Africa</span><span class="sxs-lookup"><span data-stu-id="e9129-169">South Africa</span></span>    | `https://za-api.mimecast.com/sso/<accountcode>`|
    | <span data-ttu-id="e9129-170">Australia</span><span class="sxs-lookup"><span data-stu-id="e9129-170">Australia</span></span>       | `https://au-api.mimecast.com/sso/<accountcode>`|
    | <span data-ttu-id="e9129-171">Offshore</span><span class="sxs-lookup"><span data-stu-id="e9129-171">Offshore</span></span>        | `https://jer-api.mimecast.com/sso/<accountcode>`|

    <span data-ttu-id="e9129-172">c.</span><span class="sxs-lookup"><span data-stu-id="e9129-172">c.</span></span> <span data-ttu-id="e9129-173">In the **Reply URL** textbox, type a URL:</span><span class="sxs-lookup"><span data-stu-id="e9129-173">In the **Reply URL** textbox, type a URL:</span></span> 

    | <span data-ttu-id="e9129-174">Region</span><span class="sxs-lookup"><span data-stu-id="e9129-174">Region</span></span>  |  <span data-ttu-id="e9129-175">Value</span><span class="sxs-lookup"><span data-stu-id="e9129-175">Value</span></span> | 
    | --------------- | --------------- | 
    | <span data-ttu-id="e9129-176">Europe</span><span class="sxs-lookup"><span data-stu-id="e9129-176">Europe</span></span>          | `https://eu-api.mimecast.com/login/saml`|
    | <span data-ttu-id="e9129-177">United States</span><span class="sxs-lookup"><span data-stu-id="e9129-177">United States</span></span>   | `https://us-api.mimecast.com/login/saml`|
    | <span data-ttu-id="e9129-178">South Africa</span><span class="sxs-lookup"><span data-stu-id="e9129-178">South Africa</span></span>    | `https://za-api.mimecast.com/login/saml`|
    | <span data-ttu-id="e9129-179">Australia</span><span class="sxs-lookup"><span data-stu-id="e9129-179">Australia</span></span>       | `https://au-api.mimecast.com/login/saml`|
    | <span data-ttu-id="e9129-180">Offshore</span><span class="sxs-lookup"><span data-stu-id="e9129-180">Offshore</span></span>        | `https://jer-api.mimecast.com/login/saml`|
    
    > [!NOTE] 
    > <span data-ttu-id="e9129-181">The Identifier value is not real.</span><span class="sxs-lookup"><span data-stu-id="e9129-181">The Identifier value is not real.</span></span> <span data-ttu-id="e9129-182">Update the value with the actual Identifier.</span><span class="sxs-lookup"><span data-stu-id="e9129-182">Update the value with the actual Identifier.</span></span> <span data-ttu-id="e9129-183">Contact [Mimecast Personal Portal Client support team](http://www.mimecast.com/customer-success/technical-support/) to get the value.</span><span class="sxs-lookup"><span data-stu-id="e9129-183">Contact [Mimecast Personal Portal Client support team](http://www.mimecast.com/customer-success/technical-support/) to get the value.</span></span> 

1. <span data-ttu-id="e9129-184">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="e9129-184">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

1. <span data-ttu-id="e9129-186">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="e9129-186">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/mimecast-personal-portal-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="e9129-188">On the **Mimecast Personal Portal Configuration** section, click **Configure Mimecast Personal Portal** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="e9129-188">On the **Mimecast Personal Portal Configuration** section, click **Configure Mimecast Personal Portal** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e9129-189">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="e9129-189">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Mimecast Personal Portal Configuration](./media/mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

1. <span data-ttu-id="e9129-191">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span><span class="sxs-lookup"><span data-stu-id="e9129-191">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span></span>

1. <span data-ttu-id="e9129-192">Go to **Services \> Applications**.</span><span class="sxs-lookup"><span data-stu-id="e9129-192">Go to **Services \> Applications**.</span></span>
   
    <span data-ttu-id="e9129-193">![Applications](./media/mimecast-personal-portal-tutorial/ic794998.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="e9129-193">![Applications](./media/mimecast-personal-portal-tutorial/ic794998.png "Applications")</span></span>

1. <span data-ttu-id="e9129-194">Click **Authentication Profiles**.</span><span class="sxs-lookup"><span data-stu-id="e9129-194">Click **Authentication Profiles**.</span></span>
   
    <span data-ttu-id="e9129-195">![Authentication Profiles](./media/mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles")</span><span class="sxs-lookup"><span data-stu-id="e9129-195">![Authentication Profiles](./media/mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles")</span></span>

1. <span data-ttu-id="e9129-196">Click **New Authentication Profile**.</span><span class="sxs-lookup"><span data-stu-id="e9129-196">Click **New Authentication Profile**.</span></span>
   
    <span data-ttu-id="e9129-197">![New Authentication Profile](./media/mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span><span class="sxs-lookup"><span data-stu-id="e9129-197">![New Authentication Profile](./media/mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span></span>

1. <span data-ttu-id="e9129-198">In the **Authentication Profile** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e9129-198">In the **Authentication Profile** section, perform the following steps:</span></span>
   
    <span data-ttu-id="e9129-199">![Authentication Profile](./media/mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile")</span><span class="sxs-lookup"><span data-stu-id="e9129-199">![Authentication Profile](./media/mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile")</span></span>
   
    <span data-ttu-id="e9129-200">a.</span><span class="sxs-lookup"><span data-stu-id="e9129-200">a.</span></span> <span data-ttu-id="e9129-201">In the **Description** textbox, type a name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="e9129-201">In the **Description** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="e9129-202">b.</span><span class="sxs-lookup"><span data-stu-id="e9129-202">b.</span></span> <span data-ttu-id="e9129-203">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="e9129-203">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span></span>
   
    <span data-ttu-id="e9129-204">c.</span><span class="sxs-lookup"><span data-stu-id="e9129-204">c.</span></span> <span data-ttu-id="e9129-205">As **Provider**, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e9129-205">As **Provider**, select **Azure Active Directory**.</span></span>
   
    <span data-ttu-id="e9129-206">d.</span><span class="sxs-lookup"><span data-stu-id="e9129-206">d.</span></span> <span data-ttu-id="e9129-207">In **Issuer URL** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e9129-207">In **Issuer URL** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="e9129-208">e.</span><span class="sxs-lookup"><span data-stu-id="e9129-208">e.</span></span> <span data-ttu-id="e9129-209">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e9129-209">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="e9129-210">f.</span><span class="sxs-lookup"><span data-stu-id="e9129-210">f.</span></span> <span data-ttu-id="e9129-211">In **Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e9129-211">In **Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e9129-212">g.</span><span class="sxs-lookup"><span data-stu-id="e9129-212">g.</span></span> <span data-ttu-id="e9129-213">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span><span class="sxs-lookup"><span data-stu-id="e9129-213">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>

    <span data-ttu-id="e9129-214">h.</span><span class="sxs-lookup"><span data-stu-id="e9129-214">h.</span></span> <span data-ttu-id="e9129-215">Select **Allow Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="e9129-215">Select **Allow Single Sign On**.</span></span>
   
    <span data-ttu-id="e9129-216">i.</span><span class="sxs-lookup"><span data-stu-id="e9129-216">i.</span></span> <span data-ttu-id="e9129-217">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e9129-217">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e9129-218">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e9129-218">Create an Azure AD test user</span></span>

<span data-ttu-id="e9129-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e9129-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="e9129-221">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e9129-221">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e9129-222">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="e9129-222">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/mimecast-personal-portal-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="e9129-224">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="e9129-224">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/mimecast-personal-portal-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="e9129-226">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="e9129-226">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/mimecast-personal-portal-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="e9129-228">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e9129-228">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/mimecast-personal-portal-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e9129-230">a.</span><span class="sxs-lookup"><span data-stu-id="e9129-230">a.</span></span> <span data-ttu-id="e9129-231">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e9129-231">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e9129-232">b.</span><span class="sxs-lookup"><span data-stu-id="e9129-232">b.</span></span> <span data-ttu-id="e9129-233">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e9129-233">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="e9129-234">c.</span><span class="sxs-lookup"><span data-stu-id="e9129-234">c.</span></span> <span data-ttu-id="e9129-235">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="e9129-235">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="e9129-236">d.</span><span class="sxs-lookup"><span data-stu-id="e9129-236">d.</span></span> <span data-ttu-id="e9129-237">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e9129-237">Click **Create**.</span></span>
 
### <a name="create-a-mimecast-personal-portal-test-user"></a><span data-ttu-id="e9129-238">Create a Mimecast Personal Portal test user</span><span class="sxs-lookup"><span data-stu-id="e9129-238">Create a Mimecast Personal Portal test user</span></span>

<span data-ttu-id="e9129-239">In order to enable Azure AD users to log into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="e9129-239">In order to enable Azure AD users to log into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span></span> <span data-ttu-id="e9129-240">In the case of Mimecast Personal Portal, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="e9129-240">In the case of Mimecast Personal Portal, provisioning is a manual task.</span></span>

<span data-ttu-id="e9129-241">You need to register a domain before you can create users.</span><span class="sxs-lookup"><span data-stu-id="e9129-241">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="e9129-242">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e9129-242">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="e9129-243">Sign on to your **Mimecast Personal Portal** as administrator.</span><span class="sxs-lookup"><span data-stu-id="e9129-243">Sign on to your **Mimecast Personal Portal** as administrator.</span></span>

1. <span data-ttu-id="e9129-244">Go to **Directories \> Internal**.</span><span class="sxs-lookup"><span data-stu-id="e9129-244">Go to **Directories \> Internal**.</span></span>
   
    <span data-ttu-id="e9129-245">![Directories](./media/mimecast-personal-portal-tutorial/ic795003.png "Directories")</span><span class="sxs-lookup"><span data-stu-id="e9129-245">![Directories](./media/mimecast-personal-portal-tutorial/ic795003.png "Directories")</span></span>

1. <span data-ttu-id="e9129-246">Click **Register New Domain**.</span><span class="sxs-lookup"><span data-stu-id="e9129-246">Click **Register New Domain**.</span></span>
   
    <span data-ttu-id="e9129-247">![Register New Domain](./media/mimecast-personal-portal-tutorial/ic795004.png "Register New Domain")</span><span class="sxs-lookup"><span data-stu-id="e9129-247">![Register New Domain](./media/mimecast-personal-portal-tutorial/ic795004.png "Register New Domain")</span></span>

1. <span data-ttu-id="e9129-248">After your new domain has been created, click **New Address**.</span><span class="sxs-lookup"><span data-stu-id="e9129-248">After your new domain has been created, click **New Address**.</span></span>
   
    <span data-ttu-id="e9129-249">![New Address](./media/mimecast-personal-portal-tutorial/ic795005.png "New Address")</span><span class="sxs-lookup"><span data-stu-id="e9129-249">![New Address](./media/mimecast-personal-portal-tutorial/ic795005.png "New Address")</span></span>

1. <span data-ttu-id="e9129-250">In the new address dialog, perform the following steps of a valid Azure AD account you want to provision:</span><span class="sxs-lookup"><span data-stu-id="e9129-250">In the new address dialog, perform the following steps of a valid Azure AD account you want to provision:</span></span>
   
    <span data-ttu-id="e9129-251">![Save](./media/mimecast-personal-portal-tutorial/ic795006.png "Save")</span><span class="sxs-lookup"><span data-stu-id="e9129-251">![Save](./media/mimecast-personal-portal-tutorial/ic795006.png "Save")</span></span>
   
    <span data-ttu-id="e9129-252">a.</span><span class="sxs-lookup"><span data-stu-id="e9129-252">a.</span></span> <span data-ttu-id="e9129-253">In the **Email Address** textbox, type **Email Address** of the user as **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="e9129-253">In the **Email Address** textbox, type **Email Address** of the user as **BrittaSimon@contoso.com**.</span></span>
    
    <span data-ttu-id="e9129-254">b.</span><span class="sxs-lookup"><span data-stu-id="e9129-254">b.</span></span> <span data-ttu-id="e9129-255">In the **Global Name** textbox, type the **username** as **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e9129-255">In the **Global Name** textbox, type the **username** as **BrittaSimon**.</span></span>

    <span data-ttu-id="e9129-256">c.</span><span class="sxs-lookup"><span data-stu-id="e9129-256">c.</span></span> <span data-ttu-id="e9129-257">In the **Password**, and **Confirm Password** textboxes, type the **Password** of the user.</span><span class="sxs-lookup"><span data-stu-id="e9129-257">In the **Password**, and **Confirm Password** textboxes, type the **Password** of the user.</span></span>
   
    <span data-ttu-id="e9129-258">b.</span><span class="sxs-lookup"><span data-stu-id="e9129-258">b.</span></span> <span data-ttu-id="e9129-259">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e9129-259">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="e9129-260">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="e9129-260">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e9129-261">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e9129-261">Assign the Azure AD test user</span></span>

<span data-ttu-id="e9129-262">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="e9129-262">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Personal Portal.</span></span>

![Assign the user role][200] 

<span data-ttu-id="e9129-264">**To assign Britta Simon to Mimecast Personal Portal, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e9129-264">**To assign Britta Simon to Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="e9129-265">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e9129-265">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="e9129-267">In the applications list, select **Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="e9129-267">In the applications list, select **Mimecast Personal Portal**.</span></span>

    ![The Mimecast Personal Portal link in the Applications list](./media/mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png)  

1. <span data-ttu-id="e9129-269">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="e9129-269">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="e9129-271">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="e9129-271">Click **Add** button.</span></span> <span data-ttu-id="e9129-272">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e9129-272">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="e9129-274">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="e9129-274">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="e9129-275">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="e9129-275">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="e9129-276">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e9129-276">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e9129-277">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="e9129-277">Test single sign-on</span></span>

<span data-ttu-id="e9129-278">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="e9129-278">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e9129-279">When you click the Mimecast Personal Portal tile in the Access Panel, you should get automatically signed-on to your Mimecast Personal Portal application.</span><span class="sxs-lookup"><span data-stu-id="e9129-279">When you click the Mimecast Personal Portal tile in the Access Panel, you should get automatically signed-on to your Mimecast Personal Portal application.</span></span>
<span data-ttu-id="e9129-280">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e9129-280">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e9129-281">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e9129-281">Additional resources</span></span>

* [<span data-ttu-id="e9129-282">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e9129-282">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="e9129-283">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e9129-283">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/mimecast-personal-portal-tutorial/tutorial_general_203.png

