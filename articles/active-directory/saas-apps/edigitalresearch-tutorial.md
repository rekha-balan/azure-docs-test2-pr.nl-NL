---
title: 'Tutorial: Azure Active Directory integration with eDigitalResearch | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and eDigitalResearch.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: c6b66ea0-16ba-45b4-b550-e81c56262b1f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: ca42d6c8ca1333f2ffba77b79584b7092b26f03e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967592"
---
# <a name="tutorial-azure-active-directory-integration-with-edigitalresearch"></a><span data-ttu-id="acf3e-103">Tutorial: Azure Active Directory integration with eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="acf3e-103">Tutorial: Azure Active Directory integration with eDigitalResearch</span></span>

<span data-ttu-id="acf3e-104">In this tutorial, you learn how to integrate eDigitalResearch with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="acf3e-104">In this tutorial, you learn how to integrate eDigitalResearch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="acf3e-105">Integrating eDigitalResearch with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="acf3e-105">Integrating eDigitalResearch with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="acf3e-106">You can control in Azure AD who has access to eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="acf3e-106">You can control in Azure AD who has access to eDigitalResearch.</span></span>
- <span data-ttu-id="acf3e-107">You can enable your users to automatically get signed-on to eDigitalResearch (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="acf3e-107">You can enable your users to automatically get signed-on to eDigitalResearch (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="acf3e-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="acf3e-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="acf3e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="acf3e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acf3e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="acf3e-110">Prerequisites</span></span>

<span data-ttu-id="acf3e-111">To configure Azure AD integration with eDigitalResearch, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="acf3e-111">To configure Azure AD integration with eDigitalResearch, you need the following items:</span></span>

- <span data-ttu-id="acf3e-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="acf3e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="acf3e-113">A eDigitalResearch single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="acf3e-113">A eDigitalResearch single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="acf3e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="acf3e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="acf3e-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="acf3e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="acf3e-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="acf3e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="acf3e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="acf3e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="acf3e-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="acf3e-118">Scenario description</span></span>
<span data-ttu-id="acf3e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="acf3e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="acf3e-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="acf3e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="acf3e-121">Adding eDigitalResearch from the gallery</span><span class="sxs-lookup"><span data-stu-id="acf3e-121">Adding eDigitalResearch from the gallery</span></span>
1. <span data-ttu-id="acf3e-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="acf3e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-edigitalresearch-from-the-gallery"></a><span data-ttu-id="acf3e-123">Adding eDigitalResearch from the gallery</span><span class="sxs-lookup"><span data-stu-id="acf3e-123">Adding eDigitalResearch from the gallery</span></span>
<span data-ttu-id="acf3e-124">To configure the integration of eDigitalResearch into Azure AD, you need to add eDigitalResearch from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="acf3e-124">To configure the integration of eDigitalResearch into Azure AD, you need to add eDigitalResearch from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="acf3e-125">**To add eDigitalResearch from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="acf3e-125">**To add eDigitalResearch from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="acf3e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="acf3e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="acf3e-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="acf3e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="acf3e-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="acf3e-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="acf3e-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="acf3e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="acf3e-133">In the search box, type **eDigitalResearch**, select **eDigitalResearch** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="acf3e-133">In the search box, type **eDigitalResearch**, select **eDigitalResearch** from result panel then click **Add** button to add the application.</span></span>

    ![eDigitalResearch in the results list](./media/edigitalresearch-tutorial/tutorial_edigitalresearch_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="acf3e-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="acf3e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="acf3e-136">In this section, you configure and test Azure AD single sign-on with eDigitalResearch based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="acf3e-136">In this section, you configure and test Azure AD single sign-on with eDigitalResearch based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="acf3e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in eDigitalResearch is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="acf3e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in eDigitalResearch is to a user in Azure AD.</span></span> <span data-ttu-id="acf3e-138">In other words, a link relationship between an Azure AD user and the related user in eDigitalResearch needs to be established.</span><span class="sxs-lookup"><span data-stu-id="acf3e-138">In other words, a link relationship between an Azure AD user and the related user in eDigitalResearch needs to be established.</span></span>

<span data-ttu-id="acf3e-139">In eDigitalResearch, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="acf3e-139">In eDigitalResearch, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="acf3e-140">To configure and test Azure AD single sign-on with eDigitalResearch, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="acf3e-140">To configure and test Azure AD single sign-on with eDigitalResearch, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="acf3e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="acf3e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="acf3e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="acf3e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="acf3e-143">**[Create a eDigitalResearch test user](#create-a-edigitalresearch-test-user)** - to have a counterpart of Britta Simon in eDigitalResearch that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="acf3e-143">**[Create a eDigitalResearch test user](#create-a-edigitalresearch-test-user)** - to have a counterpart of Britta Simon in eDigitalResearch that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="acf3e-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="acf3e-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="acf3e-145">**[Test single sign-on](#test-single-sign-on)**  to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="acf3e-145">**[Test single sign-on](#test-single-sign-on)**  to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="acf3e-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="acf3e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="acf3e-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your eDigitalResearch application.</span><span class="sxs-lookup"><span data-stu-id="acf3e-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your eDigitalResearch application.</span></span>

<span data-ttu-id="acf3e-148">**To configure Azure AD single sign-on with eDigitalResearch, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="acf3e-148">**To configure Azure AD single sign-on with eDigitalResearch, perform the following steps:**</span></span>

1. <span data-ttu-id="acf3e-149">In the Azure portal, on the **eDigitalResearch** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="acf3e-149">In the Azure portal, on the **eDigitalResearch** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="acf3e-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="acf3e-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/edigitalresearch-tutorial/tutorial_edigitalresearch_samlbase.png)

1. <span data-ttu-id="acf3e-153">On the **eDigitalResearch Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="acf3e-153">On the **eDigitalResearch Domain and URLs** section, perform the following steps:</span></span>

    ![eDigitalResearch Domain and URLs single sign-on information](./media/edigitalresearch-tutorial/tutorial_edigitalresearch_url.png)

    <span data-ttu-id="acf3e-155">a.</span><span class="sxs-lookup"><span data-stu-id="acf3e-155">a.</span></span> <span data-ttu-id="acf3e-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<company-name>.edigitalresearch.com`</span><span class="sxs-lookup"><span data-stu-id="acf3e-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<company-name>.edigitalresearch.com`</span></span>

    <span data-ttu-id="acf3e-157">b.</span><span class="sxs-lookup"><span data-stu-id="acf3e-157">b.</span></span> <span data-ttu-id="acf3e-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company-name>.edigitalresearch.com/login/consume`</span><span class="sxs-lookup"><span data-stu-id="acf3e-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company-name>.edigitalresearch.com/login/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="acf3e-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="acf3e-159">These values are not real.</span></span> <span data-ttu-id="acf3e-160">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="acf3e-160">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="acf3e-161">Contact [eDigitalResearch support team](http://www.maruedr.com/contact) to get these values.</span><span class="sxs-lookup"><span data-stu-id="acf3e-161">Contact [eDigitalResearch support team](http://www.maruedr.com/contact) to get these values.</span></span>
 


1. <span data-ttu-id="acf3e-162">On the **SAML Signing Certificate** section, click **Certificate Base(64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="acf3e-162">On the **SAML Signing Certificate** section, click **Certificate Base(64)** and then save the certificate file on your computer.</span></span>

    <span data-ttu-id="acf3e-163">!</span><span class="sxs-lookup"><span data-stu-id="acf3e-163">!</span></span>![The Certificate download link](./media/edigitalresearch-tutorial/tutorial_edigitalresearch_certificate.png) 

1. <span data-ttu-id="acf3e-165">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="acf3e-165">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/edigitalresearch-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="acf3e-167">On the **eDigitalResearch Configuration** section, click **Configure eDigitalResearch** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="acf3e-167">On the **eDigitalResearch Configuration** section, click **Configure eDigitalResearch** to open **Configure sign-on** window.</span></span> <span data-ttu-id="acf3e-168">Copy the **Sign-Out URL, SAML Entity ID** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="acf3e-168">Copy the **Sign-Out URL, SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![eDigitalResearch Configuration](./media/edigitalresearch-tutorial/tutorial_edigitalresearch_configure.png) 

1. <span data-ttu-id="acf3e-170">To configure single sign-on on **eDigitalResearch** side, you need to send the downloaded **Certificate (Base64) File**, **SAML Entity ID**, and **Sign-Out URL** to [eDigitalResearch support team](http://www.maruedr.com/contact).</span><span class="sxs-lookup"><span data-stu-id="acf3e-170">To configure single sign-on on **eDigitalResearch** side, you need to send the downloaded **Certificate (Base64) File**, **SAML Entity ID**, and **Sign-Out URL** to [eDigitalResearch support team](http://www.maruedr.com/contact).</span></span> <span data-ttu-id="acf3e-171">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="acf3e-171">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="acf3e-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="acf3e-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="acf3e-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="acf3e-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="acf3e-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="acf3e-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="acf3e-175">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="acf3e-175">Create an Azure AD test user</span></span>

<span data-ttu-id="acf3e-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="acf3e-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="acf3e-178">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="acf3e-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="acf3e-179">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="acf3e-179">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/edigitalresearch-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="acf3e-181">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="acf3e-181">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/edigitalresearch-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="acf3e-183">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="acf3e-183">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/edigitalresearch-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="acf3e-185">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="acf3e-185">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/edigitalresearch-tutorial/create_aaduser_04.png)

    <span data-ttu-id="acf3e-187">a.</span><span class="sxs-lookup"><span data-stu-id="acf3e-187">a.</span></span> <span data-ttu-id="acf3e-188">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="acf3e-188">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="acf3e-189">b.</span><span class="sxs-lookup"><span data-stu-id="acf3e-189">b.</span></span> <span data-ttu-id="acf3e-190">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="acf3e-190">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="acf3e-191">c.</span><span class="sxs-lookup"><span data-stu-id="acf3e-191">c.</span></span> <span data-ttu-id="acf3e-192">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="acf3e-192">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="acf3e-193">d.</span><span class="sxs-lookup"><span data-stu-id="acf3e-193">d.</span></span> <span data-ttu-id="acf3e-194">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="acf3e-194">Click **Create**.</span></span>
  
### <a name="create-a-edigitalresearch-test-user"></a><span data-ttu-id="acf3e-195">Create a eDigitalResearch test user</span><span class="sxs-lookup"><span data-stu-id="acf3e-195">Create a eDigitalResearch test user</span></span>

<span data-ttu-id="acf3e-196">The objective of this section is to create a user called Britta Simon in eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="acf3e-196">The objective of this section is to create a user called Britta Simon in eDigitalResearch.</span></span> 

<span data-ttu-id="acf3e-197">Work with the [eDigitalResearch support team](http://www.maruedr.com/contact) to get users created.</span><span class="sxs-lookup"><span data-stu-id="acf3e-197">Work with the [eDigitalResearch support team](http://www.maruedr.com/contact) to get users created.</span></span>     
    
 > [!NOTE]
 > <span data-ttu-id="acf3e-198">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="acf3e-198">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="acf3e-199">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="acf3e-199">Assign the Azure AD test user</span></span>

<span data-ttu-id="acf3e-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="acf3e-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to eDigitalResearch.</span></span>

![Assign the user role][200] 

<span data-ttu-id="acf3e-202">**To assign Britta Simon to eDigitalResearch, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="acf3e-202">**To assign Britta Simon to eDigitalResearch, perform the following steps:**</span></span>

1. <span data-ttu-id="acf3e-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="acf3e-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="acf3e-205">In the applications list, select **eDigitalResearch**.</span><span class="sxs-lookup"><span data-stu-id="acf3e-205">In the applications list, select **eDigitalResearch**.</span></span>

    ![The eDigitalResearch link in the Applications list](./media/edigitalresearch-tutorial/tutorial_edigitalresearch_app.png)  

1. <span data-ttu-id="acf3e-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="acf3e-207">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="acf3e-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="acf3e-209">Click **Add** button.</span></span> <span data-ttu-id="acf3e-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="acf3e-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="acf3e-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="acf3e-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="acf3e-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="acf3e-213">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="acf3e-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="acf3e-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="acf3e-215">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="acf3e-215">Test single sign-on</span></span>

<span data-ttu-id="acf3e-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="acf3e-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="acf3e-217">When you click the eDigitalResearch tile in the Access Panel, you should get automatically signed-on to your eDigitalResearch application.</span><span class="sxs-lookup"><span data-stu-id="acf3e-217">When you click the eDigitalResearch tile in the Access Panel, you should get automatically signed-on to your eDigitalResearch application.</span></span>
<span data-ttu-id="acf3e-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="acf3e-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="acf3e-219">Additional resources</span><span class="sxs-lookup"><span data-stu-id="acf3e-219">Additional resources</span></span>

* [<span data-ttu-id="acf3e-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="acf3e-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="acf3e-221">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="acf3e-221">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/edigitalresearch-tutorial/tutorial_general_01.png
[2]: ./media/edigitalresearch-tutorial/tutorial_general_02.png
[3]: ./media/edigitalresearch-tutorial/tutorial_general_03.png
[4]: ./media/edigitalresearch-tutorial/tutorial_general_04.png

[100]: ./media/edigitalresearch-tutorial/tutorial_general_100.png

[200]: ./media/edigitalresearch-tutorial/tutorial_general_200.png
[201]: ./media/edigitalresearch-tutorial/tutorial_general_201.png
[202]: ./media/edigitalresearch-tutorial/tutorial_general_202.png
[203]: ./media/edigitalresearch-tutorial/tutorial_general_203.png

