---
title: 'Tutorial: Azure Active Directory integration with SuccessFactors | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SuccessFactors.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2017
ms.author: jeedes
ms.openlocfilehash: 870a753a8f10255a602616ab54234b295f4d6e13
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866302"
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a><span data-ttu-id="7dbf4-103">Tutorial: Azure Active Directory integration with SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="7dbf4-103">Tutorial: Azure Active Directory integration with SuccessFactors</span></span>

<span data-ttu-id="7dbf4-104">In this tutorial, you learn how to integrate SuccessFactors with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7dbf4-104">In this tutorial, you learn how to integrate SuccessFactors with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7dbf4-105">Integrating SuccessFactors with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7dbf4-105">Integrating SuccessFactors with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7dbf4-106">You can control in Azure AD who has access to SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-106">You can control in Azure AD who has access to SuccessFactors.</span></span>
- <span data-ttu-id="7dbf4-107">You can enable your users to automatically get signed-on to SuccessFactors (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-107">You can enable your users to automatically get signed-on to SuccessFactors (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7dbf4-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="7dbf4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="7dbf4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7dbf4-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7dbf4-110">Prerequisites</span></span>

<span data-ttu-id="7dbf4-111">To configure Azure AD integration with SuccessFactors, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7dbf4-111">To configure Azure AD integration with SuccessFactors, you need the following items:</span></span>

- <span data-ttu-id="7dbf4-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7dbf4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7dbf4-113">A SuccessFactors single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7dbf4-113">A SuccessFactors single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7dbf4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7dbf4-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7dbf4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7dbf4-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7dbf4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7dbf4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7dbf4-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7dbf4-118">Scenario description</span></span>
<span data-ttu-id="7dbf4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7dbf4-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7dbf4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7dbf4-121">Adding SuccessFactors from the gallery</span><span class="sxs-lookup"><span data-stu-id="7dbf4-121">Adding SuccessFactors from the gallery</span></span>
1. <span data-ttu-id="7dbf4-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7dbf4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-successfactors-from-the-gallery"></a><span data-ttu-id="7dbf4-123">Adding SuccessFactors from the gallery</span><span class="sxs-lookup"><span data-stu-id="7dbf4-123">Adding SuccessFactors from the gallery</span></span>
<span data-ttu-id="7dbf4-124">To configure the integration of SuccessFactors into Azure AD, you need to add SuccessFactors from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-124">To configure the integration of SuccessFactors into Azure AD, you need to add SuccessFactors from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7dbf4-125">**To add SuccessFactors from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7dbf4-125">**To add SuccessFactors from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7dbf4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="7dbf4-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7dbf4-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="7dbf4-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="7dbf4-133">In the search box, type **SuccessFactors**, select **SuccessFactors** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-133">In the search box, type **SuccessFactors**, select **SuccessFactors** from result panel then click **Add** button to add the application.</span></span>

    ![SuccessFactors in the results list](./media/successfactors-tutorial/tutorial_successfactors_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7dbf4-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7dbf4-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7dbf4-136">In this section, you configure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7dbf4-136">In this section, you configure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7dbf4-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SuccessFactors is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SuccessFactors is to a user in Azure AD.</span></span> <span data-ttu-id="7dbf4-138">In other words, a link relationship between an Azure AD user and the related user in SuccessFactors needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-138">In other words, a link relationship between an Azure AD user and the related user in SuccessFactors needs to be established.</span></span>

<span data-ttu-id="7dbf4-139">In SuccessFactors, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-139">In SuccessFactors, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7dbf4-140">To configure and test Azure AD single sign-on with SuccessFactors, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7dbf4-140">To configure and test Azure AD single sign-on with SuccessFactors, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7dbf4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="7dbf4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="7dbf4-143">**[Create a SuccessFactors test user](#create-a-successfactors-test-user)** - to have a counterpart of Britta Simon in SuccessFactors that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-143">**[Create a SuccessFactors test user](#create-a-successfactors-test-user)** - to have a counterpart of Britta Simon in SuccessFactors that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="7dbf4-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="7dbf4-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7dbf4-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7dbf4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7dbf4-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SuccessFactors application.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SuccessFactors application.</span></span>

<span data-ttu-id="7dbf4-148">**To configure Azure AD single sign-on with SuccessFactors, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7dbf4-148">**To configure Azure AD single sign-on with SuccessFactors, perform the following steps:**</span></span>

1. <span data-ttu-id="7dbf4-149">In the Azure portal, on the **SuccessFactors** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-149">In the Azure portal, on the **SuccessFactors** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="7dbf4-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/successfactors-tutorial/tutorial_successfactors_samlbase.png)

1. <span data-ttu-id="7dbf4-153">On the **SuccessFactors Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7dbf4-153">On the **SuccessFactors Domain and URLs** section, perform the following steps:</span></span>

    ![SuccessFactors Domain and URLs single sign-on information](./media/successfactors-tutorial/tutorial_successfactors_url.png)

    <span data-ttu-id="7dbf4-155">a.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-155">a.</span></span> <span data-ttu-id="7dbf4-156">In the **Sign-on URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="7dbf4-156">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.successfactors.com/<companyname>`|
    | `https://<companyname>.sapsf.com/<companyname>`|
    | `https://<companyname>.successfactors.eu/<companyname>`|
    | `https://<companyname>.sapsf.eu`|

    <span data-ttu-id="7dbf4-157">b.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-157">b.</span></span> <span data-ttu-id="7dbf4-158">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="7dbf4-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://www.successfactors.com/<companyname>`|
    | `https://www.successfactors.com`|
    | `https://<companyname>.successfactors.eu`|
    | `https://www.successfactors.eu/<companyname>`|
    | `https://<companyname>.sapsf.com`|
    | `https://hcm4preview.sapsf.com/<companyname>`|
    | `https://<companyname>.sapsf.eu`|
    | `https://www.successfactors.cn`|
    | `https://www.successfactors.cn/<companyname>`|

    <span data-ttu-id="7dbf4-159">c.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-159">c.</span></span> <span data-ttu-id="7dbf4-160">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="7dbf4-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.successfactors.com/<companyname>`|
    | `https://<companyname>.successfactors.com`|
    | `https://<companyname>.sapsf.com/<companyname>`|
    | `https://<companyname>.sapsf.com`|
    | `https://<companyname>.successfactors.eu/<companyname>`|
    | `https://<companyname>.successfactors.eu`|
    | `https://<companyname>.sapsf.eu`|
    | `https://<companyname>.sapsf.eu/<companyname>`|
    | `https://<companyname>.sapsf.cn`|
    | `https://<companyname>.sapsf.cn/<companyname>`|
         
    > [!NOTE] 
    > <span data-ttu-id="7dbf4-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-161">These values are not real.</span></span> <span data-ttu-id="7dbf4-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="7dbf4-163">Contact [SuccessFactors Client support team](https://www.successfactors.com/en_us/support.html) to get these values.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-163">Contact [SuccessFactors Client support team](https://www.successfactors.com/en_us/support.html) to get these values.</span></span> 

1. <span data-ttu-id="7dbf4-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/successfactors-tutorial/tutorial_successfactors_certificate.png) 

1. <span data-ttu-id="7dbf4-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/successfactors-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="7dbf4-168">On the **SuccessFactors Configuration** section, click **Configure SuccessFactors** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-168">On the **SuccessFactors Configuration** section, click **Configure SuccessFactors** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7dbf4-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="7dbf4-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/successfactors-tutorial/tutorial_successfactors_configure.png) 

1. <span data-ttu-id="7dbf4-171">In a different web browser window, log in to your **SuccessFactors admin portal** as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-171">In a different web browser window, log in to your **SuccessFactors admin portal** as an administrator.</span></span>
    
1. <span data-ttu-id="7dbf4-172">Visit **Application Security** and native to **Single Sign On Feature**.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-172">Visit **Application Security** and native to **Single Sign On Feature**.</span></span> 

1. <span data-ttu-id="7dbf4-173">Place any value in the **Reset Token** and click **Save Token** to enable SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-173">Place any value in the **Reset Token** and click **Save Token** to enable SAML SSO.</span></span>
   
    ![Configuring single sign-on on app side][11]

    > [!NOTE] 
    > <span data-ttu-id="7dbf4-175">This value is used as the on/off switch.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-175">This value is used as the on/off switch.</span></span> <span data-ttu-id="7dbf4-176">If any value is saved, the SAML SSO is ON.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-176">If any value is saved, the SAML SSO is ON.</span></span> <span data-ttu-id="7dbf4-177">If a blank value is saved the SAML SSO is OFF.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-177">If a blank value is saved the SAML SSO is OFF.</span></span>

1. <span data-ttu-id="7dbf4-178">Native to below screenshot and perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="7dbf4-178">Native to below screenshot and perform the following actions:</span></span>
   
    ![Configuring single sign-on on app side][12]
   
    <span data-ttu-id="7dbf4-180">a.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-180">a.</span></span> <span data-ttu-id="7dbf4-181">Select the **SAML v2 SSO** Radio Button</span><span class="sxs-lookup"><span data-stu-id="7dbf4-181">Select the **SAML v2 SSO** Radio Button</span></span>
   
    <span data-ttu-id="7dbf4-182">b.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-182">b.</span></span> <span data-ttu-id="7dbf4-183">Set the **SAML Asserting Party Name**(for example, SAML issuer + company name).</span><span class="sxs-lookup"><span data-stu-id="7dbf4-183">Set the **SAML Asserting Party Name**(for example, SAML issuer + company name).</span></span>
   
    <span data-ttu-id="7dbf4-184">c.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-184">c.</span></span> <span data-ttu-id="7dbf4-185">In the **Issuer URL** textbox, paste the **SAML Entity ID** value which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-185">In the **Issuer URL** textbox, paste the **SAML Entity ID** value which you have copied from the Azure portal.</span></span>
   
    <span data-ttu-id="7dbf4-186">d.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-186">d.</span></span> <span data-ttu-id="7dbf4-187">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-187">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span></span>
   
    <span data-ttu-id="7dbf4-188">e.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-188">e.</span></span> <span data-ttu-id="7dbf4-189">Select **Enabled** as **Enable SAML Flag**.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-189">Select **Enabled** as **Enable SAML Flag**.</span></span>
   
    <span data-ttu-id="7dbf4-190">f.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-190">f.</span></span> <span data-ttu-id="7dbf4-191">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-191">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span></span>
   
    <span data-ttu-id="7dbf4-192">g.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-192">g.</span></span> <span data-ttu-id="7dbf4-193">Select **Browser/Post Profile** as **SAML Profile**.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-193">Select **Browser/Post Profile** as **SAML Profile**.</span></span>
   
    <span data-ttu-id="7dbf4-194">h.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-194">h.</span></span> <span data-ttu-id="7dbf4-195">Select **No** as **Enforce Certificate Valid Period**.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-195">Select **No** as **Enforce Certificate Valid Period**.</span></span>
   
    <span data-ttu-id="7dbf4-196">i.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-196">i.</span></span> <span data-ttu-id="7dbf4-197">Copy the content of the downloaded certificate file from Azure portal, and then paste it into the **SAML Verifying Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-197">Copy the content of the downloaded certificate file from Azure portal, and then paste it into the **SAML Verifying Certificate** textbox.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7dbf4-198">The certificate content must have begin certificate and end certificate tags.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-198">The certificate content must have begin certificate and end certificate tags.</span></span>

1. <span data-ttu-id="7dbf4-199">Navigate to SAML V2, and then perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7dbf4-199">Navigate to SAML V2, and then perform the following steps:</span></span>
   
    ![Configuring single sign-on on app side][13]
   
    <span data-ttu-id="7dbf4-201">a.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-201">a.</span></span> <span data-ttu-id="7dbf4-202">Select **Yes** as **Support SP-initiated Global Logout**.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-202">Select **Yes** as **Support SP-initiated Global Logout**.</span></span>
   
    <span data-ttu-id="7dbf4-203">b.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-203">b.</span></span> <span data-ttu-id="7dbf4-204">In the **Global Logout Service URL (LogoutRequest destination)** textbox, paste the **Sign-Out URL** value which you have copied form the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-204">In the **Global Logout Service URL (LogoutRequest destination)** textbox, paste the **Sign-Out URL** value which you have copied form the Azure portal.</span></span>
   
    <span data-ttu-id="7dbf4-205">c.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-205">c.</span></span> <span data-ttu-id="7dbf4-206">Select **No** as **Require sp must encrypt all NameID element**.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-206">Select **No** as **Require sp must encrypt all NameID element**.</span></span>
   
    <span data-ttu-id="7dbf4-207">d.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-207">d.</span></span> <span data-ttu-id="7dbf4-208">Select **unspecified** as **NameID Format**.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-208">Select **unspecified** as **NameID Format**.</span></span>
   
    <span data-ttu-id="7dbf4-209">e.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-209">e.</span></span> <span data-ttu-id="7dbf4-210">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-210">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span></span>
   
    <span data-ttu-id="7dbf4-211">f.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-211">f.</span></span> <span data-ttu-id="7dbf4-212">In the **Send request as Company-Wide issuer** textbox, paste **SAML Single Sign-On Service URL** value which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-212">In the **Send request as Company-Wide issuer** textbox, paste **SAML Single Sign-On Service URL** value which you have copied from the Azure portal.</span></span>

1. <span data-ttu-id="7dbf4-213">Perform these steps if you want to make the login usernames Case Insensitive.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-213">Perform these steps if you want to make the login usernames Case Insensitive.</span></span>
   
    ![Configure Single Sign-On][29]
    
    <span data-ttu-id="7dbf4-215">a.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-215">a.</span></span> <span data-ttu-id="7dbf4-216">Visit **Company Settings**(near the bottom).</span><span class="sxs-lookup"><span data-stu-id="7dbf4-216">Visit **Company Settings**(near the bottom).</span></span>
   
    <span data-ttu-id="7dbf4-217">b.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-217">b.</span></span> <span data-ttu-id="7dbf4-218">select checkbox near **Enable Non-Case-Sensitive Username**.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-218">select checkbox near **Enable Non-Case-Sensitive Username**.</span></span>
   
    <span data-ttu-id="7dbf4-219">c.Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-219">c.Click **Save**.</span></span>
   
    > [!NOTE] 
    > <span data-ttu-id="7dbf4-220">If you try to enable this, the system checks if it creates a duplicate SAML login name.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-220">If you try to enable this, the system checks if it creates a duplicate SAML login name.</span></span> <span data-ttu-id="7dbf4-221">For example if the customer has usernames User1 and user1.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-221">For example if the customer has usernames User1 and user1.</span></span> <span data-ttu-id="7dbf4-222">Taking away case sensitivity makes these duplicates.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-222">Taking away case sensitivity makes these duplicates.</span></span> <span data-ttu-id="7dbf4-223">The system gives you an error message and does not enable the feature.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-223">The system gives you an error message and does not enable the feature.</span></span> <span data-ttu-id="7dbf4-224">The customer needs to change one of the usernames so it’s spelled different.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-224">The customer needs to change one of the usernames so it’s spelled different.</span></span>

> [!TIP]
> <span data-ttu-id="7dbf4-225">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="7dbf4-225">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7dbf4-226">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-226">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7dbf4-227">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7dbf4-227">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7dbf4-228">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7dbf4-228">Create an Azure AD test user</span></span>

<span data-ttu-id="7dbf4-229">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-229">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="7dbf4-231">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7dbf4-231">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7dbf4-232">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-232">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/successfactors-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="7dbf4-234">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-234">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/successfactors-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="7dbf4-236">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-236">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/successfactors-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="7dbf4-238">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7dbf4-238">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/successfactors-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7dbf4-240">a.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-240">a.</span></span> <span data-ttu-id="7dbf4-241">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-241">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7dbf4-242">b.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-242">b.</span></span> <span data-ttu-id="7dbf4-243">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-243">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="7dbf4-244">c.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-244">c.</span></span> <span data-ttu-id="7dbf4-245">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-245">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="7dbf4-246">d.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-246">d.</span></span> <span data-ttu-id="7dbf4-247">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-247">Click **Create**.</span></span>
 
### <a name="create-a-successfactors-test-user"></a><span data-ttu-id="7dbf4-248">Create a SuccessFactors test user</span><span class="sxs-lookup"><span data-stu-id="7dbf4-248">Create a SuccessFactors test user</span></span>

<span data-ttu-id="7dbf4-249">To enable Azure AD users to log in to SuccessFactors, they must be provisioned into SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-249">To enable Azure AD users to log in to SuccessFactors, they must be provisioned into SuccessFactors.</span></span>  
<span data-ttu-id="7dbf4-250">In the case of SuccessFactors, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-250">In the case of SuccessFactors, provisioning is a manual task.</span></span>

<span data-ttu-id="7dbf4-251">To get users created in SuccessFactors, you need to contact the [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="7dbf4-251">To get users created in SuccessFactors, you need to contact the [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7dbf4-252">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7dbf4-252">Assign the Azure AD test user</span></span>

<span data-ttu-id="7dbf4-253">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-253">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SuccessFactors.</span></span>

![Assign the user role][200] 

<span data-ttu-id="7dbf4-255">**To assign Britta Simon to SuccessFactors, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7dbf4-255">**To assign Britta Simon to SuccessFactors, perform the following steps:**</span></span>

1. <span data-ttu-id="7dbf4-256">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-256">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="7dbf4-258">In the applications list, select **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-258">In the applications list, select **SuccessFactors**.</span></span>

    ![The SuccessFactors link in the Applications list](./media/successfactors-tutorial/tutorial_successfactors_app.png)  

1. <span data-ttu-id="7dbf4-260">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-260">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="7dbf4-262">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-262">Click **Add** button.</span></span> <span data-ttu-id="7dbf4-263">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="7dbf4-265">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-265">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="7dbf4-266">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-266">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="7dbf4-267">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7dbf4-268">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="7dbf4-268">Test single sign-on</span></span>

<span data-ttu-id="7dbf4-269">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-269">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7dbf4-270">When you click the SuccessFactors tile in the Access Panel, you should get automatically signed-on to your SuccessFactors application.</span><span class="sxs-lookup"><span data-stu-id="7dbf4-270">When you click the SuccessFactors tile in the Access Panel, you should get automatically signed-on to your SuccessFactors application.</span></span>
<span data-ttu-id="7dbf4-271">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7dbf4-271">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7dbf4-272">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7dbf4-272">Additional resources</span></span>

* [<span data-ttu-id="7dbf4-273">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7dbf4-273">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="7dbf4-274">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7dbf4-274">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/successfactors-tutorial/tutorial_general_01.png
[2]: ./media/successfactors-tutorial/tutorial_general_02.png
[3]: ./media/successfactors-tutorial/tutorial_general_03.png
[4]: ./media/successfactors-tutorial/tutorial_general_04.png

[11]: ./media/successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/successfactors-tutorial/tutorial_general_05.png
[15]: ./media/successfactors-tutorial/tutorial_general_06.png
[29]: ./media/successfactors-tutorial/tutorial_successfactors_10.png

[100]: ./media/successfactors-tutorial/tutorial_general_100.png

[200]: ./media/successfactors-tutorial/tutorial_general_200.png
[201]: ./media/successfactors-tutorial/tutorial_general_201.png
[202]: ./media/successfactors-tutorial/tutorial_general_202.png
[203]: ./media/successfactors-tutorial/tutorial_general_203.png

