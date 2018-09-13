---
title: 'Tutorial: Azure Active Directory integration with G Suite | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and G Suite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2018
ms.author: jeedes
ms.openlocfilehash: 8001f2d38ac80bb6c67419faa54bf834531f0332
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855929"
---
# <a name="tutorial-azure-active-directory-integration-with-g-suite"></a><span data-ttu-id="1b539-103">Tutorial: Azure Active Directory integration with G Suite</span><span class="sxs-lookup"><span data-stu-id="1b539-103">Tutorial: Azure Active Directory integration with G Suite</span></span>

<span data-ttu-id="1b539-104">In this tutorial, you learn how to integrate G Suite with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1b539-104">In this tutorial, you learn how to integrate G Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1b539-105">Integrating G Suite with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1b539-105">Integrating G Suite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1b539-106">You can control in Azure AD who has access to G Suite.</span><span class="sxs-lookup"><span data-stu-id="1b539-106">You can control in Azure AD who has access to G Suite.</span></span>
- <span data-ttu-id="1b539-107">You can enable your users to automatically get signed-on to G Suite (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="1b539-107">You can enable your users to automatically get signed-on to G Suite (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="1b539-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1b539-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="1b539-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="1b539-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b539-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1b539-110">Prerequisites</span></span>

<span data-ttu-id="1b539-111">To configure Azure AD integration with G Suite, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1b539-111">To configure Azure AD integration with G Suite, you need the following items:</span></span>

- <span data-ttu-id="1b539-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="1b539-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1b539-113">A G Suite single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1b539-113">A G Suite single sign-on enabled subscription</span></span>
- <span data-ttu-id="1b539-114">A Google Apps subscription or Google Cloud Platform subscription.</span><span class="sxs-lookup"><span data-stu-id="1b539-114">A Google Apps subscription or Google Cloud Platform subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="1b539-115">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1b539-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1b539-116">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1b539-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1b539-117">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="1b539-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1b539-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1b539-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="1b539-119">Frequently Asked Questions</span><span class="sxs-lookup"><span data-stu-id="1b539-119">Frequently Asked Questions</span></span>
1.  <span data-ttu-id="1b539-120">**Q: Does this integration support Google Cloud Platform SSO integration with Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="1b539-120">**Q: Does this integration support Google Cloud Platform SSO integration with Azure AD?**</span></span>
    
    <span data-ttu-id="1b539-121">A: Yes.</span><span class="sxs-lookup"><span data-stu-id="1b539-121">A: Yes.</span></span> <span data-ttu-id="1b539-122">Google Cloud Platform and Google Apps share the same authentication platform.</span><span class="sxs-lookup"><span data-stu-id="1b539-122">Google Cloud Platform and Google Apps share the same authentication platform.</span></span> <span data-ttu-id="1b539-123">So to do the GCP integration you need to configure the SSO with Google Apps.</span><span class="sxs-lookup"><span data-stu-id="1b539-123">So to do the GCP integration you need to configure the SSO with Google Apps.</span></span>


1. <span data-ttu-id="1b539-124">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span><span class="sxs-lookup"><span data-stu-id="1b539-124">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span></span>
   
    <span data-ttu-id="1b539-125">A: Yes, users are able to sign into their Chromebook devices using their Azure AD credentials.</span><span class="sxs-lookup"><span data-stu-id="1b539-125">A: Yes, users are able to sign into their Chromebook devices using their Azure AD credentials.</span></span> <span data-ttu-id="1b539-126">See this [G Suite support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span><span class="sxs-lookup"><span data-stu-id="1b539-126">See this [G Suite support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span></span>

1. <span data-ttu-id="1b539-127">**Q: If I enable single sign-on, will users be able to use their Azure AD credentials to sign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, and so on?**</span><span class="sxs-lookup"><span data-stu-id="1b539-127">**Q: If I enable single sign-on, will users be able to use their Azure AD credentials to sign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, and so on?**</span></span>
   
    <span data-ttu-id="1b539-128">A: Yes, depending on [which G Suite](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose to enable or disable for your organization.</span><span class="sxs-lookup"><span data-stu-id="1b539-128">A: Yes, depending on [which G Suite](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose to enable or disable for your organization.</span></span>

1. <span data-ttu-id="1b539-129">**Q: Can I enable single sign-on for only a subset of my G Suite users?**</span><span class="sxs-lookup"><span data-stu-id="1b539-129">**Q: Can I enable single sign-on for only a subset of my G Suite users?**</span></span>
   
    <span data-ttu-id="1b539-130">A: No, turning on single sign-on immediately requires all your G Suite users to authenticate with their Azure AD credentials.</span><span class="sxs-lookup"><span data-stu-id="1b539-130">A: No, turning on single sign-on immediately requires all your G Suite users to authenticate with their Azure AD credentials.</span></span> <span data-ttu-id="1b539-131">Because G Suite doesn't support having multiple identity providers, the identity provider for your G Suite environment can either be Azure AD or Google -- but not both at the same time.</span><span class="sxs-lookup"><span data-stu-id="1b539-131">Because G Suite doesn't support having multiple identity providers, the identity provider for your G Suite environment can either be Azure AD or Google -- but not both at the same time.</span></span>

1. <span data-ttu-id="1b539-132">**Q: If a user is signed in through Windows, are they automatically authenticate to G Suite without getting prompted for a password?**</span><span class="sxs-lookup"><span data-stu-id="1b539-132">**Q: If a user is signed in through Windows, are they automatically authenticate to G Suite without getting prompted for a password?**</span></span>
   
    <span data-ttu-id="1b539-133">A: There are two options for enabling this scenario.</span><span class="sxs-lookup"><span data-stu-id="1b539-133">A: There are two options for enabling this scenario.</span></span> <span data-ttu-id="1b539-134">First, users could sign into Windows 10 devices via [Azure Active Directory Join](../device-management-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1b539-134">First, users could sign into Windows 10 devices via [Azure Active Directory Join](../device-management-introduction.md).</span></span> <span data-ttu-id="1b539-135">Alternatively, users could sign into Windows devices that are domain-joined to an on-premises Active Directory that has been enabled for single sign-on to Azure AD via an [Active Directory Federation Services (AD FS)](../connect/active-directory-aadconnect-user-signin.md) deployment.</span><span class="sxs-lookup"><span data-stu-id="1b539-135">Alternatively, users could sign into Windows devices that are domain-joined to an on-premises Active Directory that has been enabled for single sign-on to Azure AD via an [Active Directory Federation Services (AD FS)](../connect/active-directory-aadconnect-user-signin.md) deployment.</span></span> <span data-ttu-id="1b539-136">Both options require you to perform the steps in the following tutorial to enable single sign-on between Azure AD and G Suite.</span><span class="sxs-lookup"><span data-stu-id="1b539-136">Both options require you to perform the steps in the following tutorial to enable single sign-on between Azure AD and G Suite.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1b539-137">Scenario description</span><span class="sxs-lookup"><span data-stu-id="1b539-137">Scenario description</span></span>
<span data-ttu-id="1b539-138">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1b539-138">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1b539-139">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1b539-139">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1b539-140">Adding G Suite from the gallery</span><span class="sxs-lookup"><span data-stu-id="1b539-140">Adding G Suite from the gallery</span></span>
1. <span data-ttu-id="1b539-141">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1b539-141">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-g-suite-from-the-gallery"></a><span data-ttu-id="1b539-142">Adding G Suite from the gallery</span><span class="sxs-lookup"><span data-stu-id="1b539-142">Adding G Suite from the gallery</span></span>
<span data-ttu-id="1b539-143">To configure the integration of G Suite into Azure AD, you need to add G Suite from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1b539-143">To configure the integration of G Suite into Azure AD, you need to add G Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1b539-144">**To add G Suite from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1b539-144">**To add G Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1b539-145">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="1b539-145">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="1b539-147">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="1b539-147">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1b539-148">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1b539-148">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="1b539-150">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="1b539-150">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="1b539-152">In the search box, type **G Suite**, select **G Suite** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="1b539-152">In the search box, type **G Suite**, select **G Suite** from result panel then click **Add** button to add the application.</span></span>

    ![G Suite in the results list](./media/google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1b539-154">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1b539-154">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1b539-155">In this section, you configure and test Azure AD single sign-on with G Suite based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1b539-155">In this section, you configure and test Azure AD single sign-on with G Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1b539-156">For single sign-on to work, Azure AD needs to know what the counterpart user in G Suite is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b539-156">For single sign-on to work, Azure AD needs to know what the counterpart user in G Suite is to a user in Azure AD.</span></span> <span data-ttu-id="1b539-157">In other words, a link relationship between an Azure AD user and the related user in G Suite needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1b539-157">In other words, a link relationship between an Azure AD user and the related user in G Suite needs to be established.</span></span>

<span data-ttu-id="1b539-158">In G Suite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="1b539-158">In G Suite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1b539-159">To configure and test Azure AD single sign-on with G Suite, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1b539-159">To configure and test Azure AD single sign-on with G Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1b539-160">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1b539-160">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="1b539-161">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b539-161">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="1b539-162">**[Create a G Suite test user](#create-a-g-suite-test-user)** - to have a counterpart of Britta Simon in G Suite that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="1b539-162">**[Create a G Suite test user](#create-a-g-suite-test-user)** - to have a counterpart of Britta Simon in G Suite that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="1b539-163">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1b539-163">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="1b539-164">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1b539-164">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1b539-165">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="1b539-165">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1b539-166">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your G Suite application.</span><span class="sxs-lookup"><span data-stu-id="1b539-166">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your G Suite application.</span></span>

<span data-ttu-id="1b539-167">**To configure Azure AD single sign-on with G Suite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1b539-167">**To configure Azure AD single sign-on with G Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="1b539-168">In the Azure portal, on the **G Suite** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="1b539-168">In the Azure portal, on the **G Suite** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="1b539-170">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1b539-170">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/google-apps-tutorial/tutorial_googleapps_samlbase.png)

1. <span data-ttu-id="1b539-172">On the **G Suite Domain and URLs** section, if you want to configure for the **Gmail** perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1b539-172">On the **G Suite Domain and URLs** section, if you want to configure for the **Gmail** perform the following steps:</span></span>

    ![G Suite Domain and URLs single sign-on information](./media/google-apps-tutorial/tutorial_googleapps_urlgmail.png)

    <span data-ttu-id="1b539-174">a.</span><span class="sxs-lookup"><span data-stu-id="1b539-174">a.</span></span> <span data-ttu-id="1b539-175">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.google.com/a/<yourdomain.com>/ServiceLogin?continue=https://mail.google.com`</span><span class="sxs-lookup"><span data-stu-id="1b539-175">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.google.com/a/<yourdomain.com>/ServiceLogin?continue=https://mail.google.com`</span></span>

    <span data-ttu-id="1b539-176">b.</span><span class="sxs-lookup"><span data-stu-id="1b539-176">b.</span></span> <span data-ttu-id="1b539-177">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="1b539-177">In the **Identifier** textbox, type a URL using the following pattern:</span></span> 
    | |
    |--|
    | `google.com/a/<yourdomain.com>` |
    | `google.com` |
    | `http://google.com` |
    | `http://google.com/a/<yourdomain.com>` |
 
    > [!NOTE] 
    > <span data-ttu-id="1b539-178">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="1b539-178">These values are not real.</span></span> <span data-ttu-id="1b539-179">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="1b539-179">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1b539-180">Contact [G Suite Client support team](https://www.google.com/contact/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="1b539-180">Contact [G Suite Client support team](https://www.google.com/contact/) to get these values.</span></span>

1. <span data-ttu-id="1b539-181">On the **G Suite Domain and URLs** section, if you want to configure for the **Google Cloud Platform** perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1b539-181">On the **G Suite Domain and URLs** section, if you want to configure for the **Google Cloud Platform** perform the following steps:</span></span>

    ![G Suite Domain and URLs single sign-on information](./media/google-apps-tutorial/tutorial_googleapps_url1.png)

    <span data-ttu-id="1b539-183">a.</span><span class="sxs-lookup"><span data-stu-id="1b539-183">a.</span></span> <span data-ttu-id="1b539-184">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.google.com/a/<yourdomain.com>/ServiceLogin?continue=https://console.cloud.google.com `</span><span class="sxs-lookup"><span data-stu-id="1b539-184">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.google.com/a/<yourdomain.com>/ServiceLogin?continue=https://console.cloud.google.com `</span></span>

    <span data-ttu-id="1b539-185">b.</span><span class="sxs-lookup"><span data-stu-id="1b539-185">b.</span></span> <span data-ttu-id="1b539-186">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="1b539-186">In the **Identifier** textbox, type a URL using the following pattern:</span></span> 
    | |
    |--|
    | `google.com/a/<yourdomain.com>` |
    | `google.com` |
    | `http://google.com` |
    | `http://google.com/a/<yourdomain.com>` |
    
    > [!NOTE] 
    > <span data-ttu-id="1b539-187">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="1b539-187">These values are not real.</span></span> <span data-ttu-id="1b539-188">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="1b539-188">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1b539-189">Contact [G Suite Client support team](https://www.google.com/contact/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="1b539-189">Contact [G Suite Client support team](https://www.google.com/contact/) to get these values.</span></span> 

1. <span data-ttu-id="1b539-190">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="1b539-190">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/google-apps-tutorial/tutorial_googleapps_certificate.png) 

1. <span data-ttu-id="1b539-192">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="1b539-192">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/google-apps-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="1b539-194">On the **G Suite Configuration** section, click **Configure G Suite** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="1b539-194">On the **G Suite Configuration** section, click **Configure G Suite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1b539-195">Copy the **Sign-Out URL, SAML Single Sign-On Service URL and Change password URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="1b539-195">Copy the **Sign-Out URL, SAML Single Sign-On Service URL and Change password URL** from the **Quick Reference section.**</span></span>

    ![G Suite Configuration](./media/google-apps-tutorial/tutorial_googleapps_configure.png) 

1. <span data-ttu-id="1b539-197">Open a new tab in your browser, and sign into the [G Suite Admin Console](http://admin.google.com/) using your administrator account.</span><span class="sxs-lookup"><span data-stu-id="1b539-197">Open a new tab in your browser, and sign into the [G Suite Admin Console](http://admin.google.com/) using your administrator account.</span></span>

1. <span data-ttu-id="1b539-198">Click **Security**.</span><span class="sxs-lookup"><span data-stu-id="1b539-198">Click **Security**.</span></span> <span data-ttu-id="1b539-199">If you don't see the link, it may be hidden under the **More Controls** menu at the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="1b539-199">If you don't see the link, it may be hidden under the **More Controls** menu at the bottom of the screen.</span></span>
   
    ![Click Security.][10]

1. <span data-ttu-id="1b539-201">On the **Security** page, click **Set up single sign-on (SSO).**</span><span class="sxs-lookup"><span data-stu-id="1b539-201">On the **Security** page, click **Set up single sign-on (SSO).**</span></span>
   
    ![Click SSO.][11]

1. <span data-ttu-id="1b539-203">Perform the following configuration changes:</span><span class="sxs-lookup"><span data-stu-id="1b539-203">Perform the following configuration changes:</span></span>
   
    ![Configure SSO][12]
   
    <span data-ttu-id="1b539-205">a.</span><span class="sxs-lookup"><span data-stu-id="1b539-205">a.</span></span> <span data-ttu-id="1b539-206">Select **Setup SSO with third-party identity provider**.</span><span class="sxs-lookup"><span data-stu-id="1b539-206">Select **Setup SSO with third-party identity provider**.</span></span>

    <span data-ttu-id="1b539-207">b.</span><span class="sxs-lookup"><span data-stu-id="1b539-207">b.</span></span> <span data-ttu-id="1b539-208">In the **Sign-in page URL** field in G Suite, paste the value of **Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1b539-208">In the **Sign-in page URL** field in G Suite, paste the value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1b539-209">c.</span><span class="sxs-lookup"><span data-stu-id="1b539-209">c.</span></span> <span data-ttu-id="1b539-210">In the **Sign-out page URL** field in G Suite, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1b539-210">In the **Sign-out page URL** field in G Suite, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="1b539-211">d.</span><span class="sxs-lookup"><span data-stu-id="1b539-211">d.</span></span> <span data-ttu-id="1b539-212">In the **Change password URL** field in G Suite, paste the value of **Change password URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1b539-212">In the **Change password URL** field in G Suite, paste the value of **Change password URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="1b539-213">e.</span><span class="sxs-lookup"><span data-stu-id="1b539-213">e.</span></span> <span data-ttu-id="1b539-214">In G Suite, for the **Verification certificate**, upload the certificate that you have downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1b539-214">In G Suite, for the **Verification certificate**, upload the certificate that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="1b539-215">f.</span><span class="sxs-lookup"><span data-stu-id="1b539-215">f.</span></span> <span data-ttu-id="1b539-216">Select **Use a domain specific issuer**.</span><span class="sxs-lookup"><span data-stu-id="1b539-216">Select **Use a domain specific issuer**.</span></span>

    <span data-ttu-id="1b539-217">g.</span><span class="sxs-lookup"><span data-stu-id="1b539-217">g.</span></span> <span data-ttu-id="1b539-218">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="1b539-218">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="1b539-219">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="1b539-219">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1b539-220">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="1b539-220">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1b539-221">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1b539-221">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1b539-222">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1b539-222">Create an Azure AD test user</span></span>

<span data-ttu-id="1b539-223">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b539-223">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="1b539-225">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1b539-225">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1b539-226">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="1b539-226">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/google-apps-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="1b539-228">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="1b539-228">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/google-apps-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="1b539-230">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="1b539-230">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/google-apps-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="1b539-232">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1b539-232">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/google-apps-tutorial/create_aaduser_04.png)

    <span data-ttu-id="1b539-234">a.</span><span class="sxs-lookup"><span data-stu-id="1b539-234">a.</span></span> <span data-ttu-id="1b539-235">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1b539-235">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1b539-236">b.</span><span class="sxs-lookup"><span data-stu-id="1b539-236">b.</span></span> <span data-ttu-id="1b539-237">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1b539-237">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="1b539-238">c.</span><span class="sxs-lookup"><span data-stu-id="1b539-238">c.</span></span> <span data-ttu-id="1b539-239">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="1b539-239">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="1b539-240">d.</span><span class="sxs-lookup"><span data-stu-id="1b539-240">d.</span></span> <span data-ttu-id="1b539-241">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1b539-241">Click **Create**.</span></span>
 
### <a name="create-a-g-suite-test-user"></a><span data-ttu-id="1b539-242">Create a G Suite test user</span><span class="sxs-lookup"><span data-stu-id="1b539-242">Create a G Suite test user</span></span>

<span data-ttu-id="1b539-243">The objective of this section is to create a user called Britta Simon in G Suite Software.</span><span class="sxs-lookup"><span data-stu-id="1b539-243">The objective of this section is to create a user called Britta Simon in G Suite Software.</span></span> <span data-ttu-id="1b539-244">G Suite supports auto provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="1b539-244">G Suite supports auto provisioning, which is by default enabled.</span></span> <span data-ttu-id="1b539-245">There is no action for you in this section.</span><span class="sxs-lookup"><span data-stu-id="1b539-245">There is no action for you in this section.</span></span> <span data-ttu-id="1b539-246">If a user doesn't already exist in G Suite Software, a new one is created when you attempt to access G Suite Software.</span><span class="sxs-lookup"><span data-stu-id="1b539-246">If a user doesn't already exist in G Suite Software, a new one is created when you attempt to access G Suite Software.</span></span>

>[!NOTE] 
><span data-ttu-id="1b539-247">If you need to create a user manually, contact the [Google support team](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="1b539-247">If you need to create a user manually, contact the [Google support team](https://www.google.com/contact/).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1b539-248">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1b539-248">Assign the Azure AD test user</span></span>

<span data-ttu-id="1b539-249">In this section, you enable Britta Simon to use Azure single sign-on by granting access to G Suite.</span><span class="sxs-lookup"><span data-stu-id="1b539-249">In this section, you enable Britta Simon to use Azure single sign-on by granting access to G Suite.</span></span>

![Assign the user role][200] 

<span data-ttu-id="1b539-251">**To assign Britta Simon to G Suite, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1b539-251">**To assign Britta Simon to G Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="1b539-252">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="1b539-252">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="1b539-254">In the applications list, select **G Suite**.</span><span class="sxs-lookup"><span data-stu-id="1b539-254">In the applications list, select **G Suite**.</span></span>

    ![The G Suite link in the Applications list](./media/google-apps-tutorial/tutorial_googleapps_app.png)  

1. <span data-ttu-id="1b539-256">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="1b539-256">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="1b539-258">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="1b539-258">Click **Add** button.</span></span> <span data-ttu-id="1b539-259">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1b539-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="1b539-261">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="1b539-261">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="1b539-262">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="1b539-262">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="1b539-263">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="1b539-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1b539-264">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="1b539-264">Test single sign-on</span></span>

<span data-ttu-id="1b539-265">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1b539-265">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1b539-266">When you click the G Suite tile in the Access Panel, you should get automatically signed-on to your G Suite application.</span><span class="sxs-lookup"><span data-stu-id="1b539-266">When you click the G Suite tile in the Access Panel, you should get automatically signed-on to your G Suite application.</span></span>
<span data-ttu-id="1b539-267">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1b539-267">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1b539-268">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1b539-268">Additional resources</span></span>

* [<span data-ttu-id="1b539-269">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b539-269">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="1b539-270">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1b539-270">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/googleapps-tutorial/tutorial_general_01.png
[2]: ./media/googleapps-tutorial/tutorial_general_02.png
[3]: ./media/googleapps-tutorial/tutorial_general_03.png
[4]: ./media/googleapps-tutorial/tutorial_general_04.png

[100]: ./media/googleapps-tutorial/tutorial_general_100.png

[200]: ./media/googleapps-tutorial/tutorial_general_200.png
[201]: ./media/googleapps-tutorial/tutorial_general_201.png
[202]: ./media/googleapps-tutorial/tutorial_general_202.png
[203]: ./media/googleapps-tutorial/tutorial_general_203.png
[10]: ./media/googleapps-tutorial/gapps-security.png
[11]: ./media/googleapps-tutorial/security-gapps.png
[12]: ./media/googleapps-tutorial/gapps-sso-config.png

