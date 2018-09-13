---
title: 'Tutorial: Azure Active Directory integration with Central Desktop | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Central Desktop.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2017
ms.author: jeedes
ms.openlocfilehash: 82a6911c85dd1438aa8f60cb36194a2916bc91e7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856336"
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a><span data-ttu-id="a8fd2-103">Tutorial: Azure Active Directory integration with Central Desktop</span><span class="sxs-lookup"><span data-stu-id="a8fd2-103">Tutorial: Azure Active Directory integration with Central Desktop</span></span>

<span data-ttu-id="a8fd2-104">In this tutorial, you learn how to integrate Central Desktop with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a8fd2-104">In this tutorial, you learn how to integrate Central Desktop with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a8fd2-105">Integrating Central Desktop with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a8fd2-105">Integrating Central Desktop with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a8fd2-106">You can control in Azure AD who has access to Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-106">You can control in Azure AD who has access to Central Desktop.</span></span>
- <span data-ttu-id="a8fd2-107">You can enable your users to automatically get signed in to Central Desktop with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-107">You can enable your users to automatically get signed in to Central Desktop with their Azure AD accounts.</span></span>
- <span data-ttu-id="a8fd2-108">You can manage your accounts in one central location--the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="a8fd2-109">For more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a8fd2-109">For more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8fd2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a8fd2-110">Prerequisites</span></span>

<span data-ttu-id="a8fd2-111">To configure Azure AD integration with Central Desktop, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a8fd2-111">To configure Azure AD integration with Central Desktop, you need the following items:</span></span>

- <span data-ttu-id="a8fd2-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a8fd2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a8fd2-113">A Central Desktop single sign-on-enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a8fd2-113">A Central Desktop single sign-on-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a8fd2-114">We don't recommend using a production environment to test the steps in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-114">We don't recommend using a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="a8fd2-115">To test the steps in this tutorial, follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a8fd2-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="a8fd2-116">Don't use your production environment unless it's necessary.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="a8fd2-117">If you don't already have an Azure AD trial environment, [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a8fd2-117">If you don't already have an Azure AD trial environment, [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a8fd2-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a8fd2-118">Scenario description</span></span>
<span data-ttu-id="a8fd2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a8fd2-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a8fd2-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a8fd2-121">Adding Central Desktop from the gallery</span><span class="sxs-lookup"><span data-stu-id="a8fd2-121">Adding Central Desktop from the gallery</span></span>
1. <span data-ttu-id="a8fd2-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a8fd2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-central-desktop-from-the-gallery"></a><span data-ttu-id="a8fd2-123">Add Central Desktop from the gallery</span><span class="sxs-lookup"><span data-stu-id="a8fd2-123">Add Central Desktop from the gallery</span></span>
<span data-ttu-id="a8fd2-124">To configure the integration of Central Desktop into Azure AD, you need to add Central Desktop from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-124">To configure the integration of Central Desktop into Azure AD, you need to add Central Desktop from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a8fd2-125">**To add Central Desktop from the gallery, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a8fd2-125">**To add Central Desktop from the gallery, take the following steps:**</span></span>

1. <span data-ttu-id="a8fd2-126">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-126">In the [Azure portal](https://portal.azure.com), in the left pane, select the **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="a8fd2-128">Go to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-128">Go to **Enterprise applications**.</span></span> <span data-ttu-id="a8fd2-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="a8fd2-131">To add new applications, select the **New application** button on the top of the dialog box.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-131">To add new applications, select the **New application** button on the top of the dialog box.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="a8fd2-133">In the search box, type **Central Desktop**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-133">In the search box, type **Central Desktop**.</span></span> <span data-ttu-id="a8fd2-134">Select **Central Desktop** from the results panel, and then select the **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-134">Select **Central Desktop** from the results panel, and then select the **Add** button to add the application.</span></span>

    ![Central Desktop in the results list](./media/central-desktop-tutorial/tutorial_centraldesktop_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a8fd2-136">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a8fd2-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a8fd2-137">In this section, you configure and test Azure AD single sign-on with Central Desktop based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a8fd2-137">In this section, you configure and test Azure AD single sign-on with Central Desktop based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a8fd2-138">For single sign-on to work, Azure AD needs to know who the counterpart user in Central Desktop is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-138">For single sign-on to work, Azure AD needs to know who the counterpart user in Central Desktop is to a user in Azure AD.</span></span> <span data-ttu-id="a8fd2-139">In other words, you need to establish a link between an Azure AD user and a related user in Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-139">In other words, you need to establish a link between an Azure AD user and a related user in Central Desktop.</span></span>

<span data-ttu-id="a8fd2-140">In Central Desktop, give **Username** the same value as **user name** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-140">In Central Desktop, give **Username** the same value as **user name** in Azure AD.</span></span> <span data-ttu-id="a8fd2-141">Now you have established the link between the two users.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-141">Now you have established the link between the two users.</span></span>

<span data-ttu-id="a8fd2-142">To configure and test Azure AD single sign-on with Central Desktop, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a8fd2-142">To configure and test Azure AD single sign-on with Central Desktop, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a8fd2-143">[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on) to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-143">[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on) to enable your users to use this feature.</span></span>
1. <span data-ttu-id="a8fd2-144">[Create an Azure AD test user](#create-an-azure-ad-test-user) to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-144">[Create an Azure AD test user](#create-an-azure-ad-test-user) to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="a8fd2-145">[Create a Central Desktop test user](#create-a-central-desktop-test-user) to have a counterpart of Britta Simon in Central Desktop that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-145">[Create a Central Desktop test user](#create-a-central-desktop-test-user) to have a counterpart of Britta Simon in Central Desktop that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="a8fd2-146">[Assign the Azure AD test user](#assign-the-azure-ad-test-user) to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-146">[Assign the Azure AD test user](#assign-the-azure-ad-test-user) to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="a8fd2-147">[Test single sign-on](#test-single-sign-on) to verify that the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-147">[Test single sign-on](#test-single-sign-on) to verify that the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a8fd2-148">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a8fd2-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a8fd2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Central Desktop application.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Central Desktop application.</span></span>

<span data-ttu-id="a8fd2-150">**To configure Azure AD single sign-on with Central Desktop, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a8fd2-150">**To configure Azure AD single sign-on with Central Desktop, take the following steps:**</span></span>

1. <span data-ttu-id="a8fd2-151">In the Azure portal, on the **Central Desktop** application integration page, select **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-151">In the Azure portal, on the **Central Desktop** application integration page, select **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="a8fd2-153">To enable single sign-on, in the **Single sign-on** dialog box, in the **Mode** drop-down list, select **SAML-based Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-153">To enable single sign-on, in the **Single sign-on** dialog box, in the **Mode** drop-down list, select **SAML-based Sign-on**.</span></span>
 
    ![Single sign-on dialog box](./media/central-desktop-tutorial/tutorial_centraldesktop_samlbase.png)

1. <span data-ttu-id="a8fd2-155">In the **Central Desktop Domain and URLs** section, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="a8fd2-155">In the **Central Desktop Domain and URLs** section, take the following steps:</span></span>

    ![Central Desktop domain and URLs single sign-on information](./media/central-desktop-tutorial/tutorial_centraldesktop_url.png)

    <span data-ttu-id="a8fd2-157">a.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-157">a.</span></span> <span data-ttu-id="a8fd2-158">In the **Sign-on URL** box, type a URL with the following pattern: `https://<companyname>.centraldesktop.com`</span><span class="sxs-lookup"><span data-stu-id="a8fd2-158">In the **Sign-on URL** box, type a URL with the following pattern: `https://<companyname>.centraldesktop.com`</span></span>

    <span data-ttu-id="a8fd2-159">b.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-159">b.</span></span> <span data-ttu-id="a8fd2-160">In the **Identifier** box, type a URL with the following pattern:</span><span class="sxs-lookup"><span data-stu-id="a8fd2-160">In the **Identifier** box, type a URL with the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.centraldesktop.com/saml2-metadata.php`|
    | `https://<companyname>.imeetcentral.com/saml2-metadata.php`|

    <span data-ttu-id="a8fd2-161">c.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-161">c.</span></span> <span data-ttu-id="a8fd2-162">In the **Reply URL** box, type a URL with the following pattern: `https://<companyname>.centraldesktop.com/saml2-assertion.php`</span><span class="sxs-lookup"><span data-stu-id="a8fd2-162">In the **Reply URL** box, type a URL with the following pattern: `https://<companyname>.centraldesktop.com/saml2-assertion.php`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="a8fd2-163">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-163">These values are not real.</span></span> <span data-ttu-id="a8fd2-164">Update these values with the actual identifier, reply URL, and sign-on URL.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-164">Update these values with the actual identifier, reply URL, and sign-on URL.</span></span> <span data-ttu-id="a8fd2-165">Contact the [Central Desktop client support team](https://imeetcentral.com/contact-us) to get these values.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-165">Contact the [Central Desktop client support team](https://imeetcentral.com/contact-us) to get these values.</span></span> 

1. <span data-ttu-id="a8fd2-166">In the **SAML Signing Certificate** section, select **Certificate**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-166">In the **SAML Signing Certificate** section, select **Certificate**.</span></span> <span data-ttu-id="a8fd2-167">Then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-167">Then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/central-desktop-tutorial/tutorial_centraldesktop_certificate.png) 

1. <span data-ttu-id="a8fd2-169">Select the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-169">Select the **Save** button.</span></span>

    ![Configure the single sign-on Save button](./media/central-desktop-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="a8fd2-171">In the **Central Desktop Configuration** section, select **Configure Central Desktop** to open the **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-171">In the **Central Desktop Configuration** section, select **Configure Central Desktop** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="a8fd2-172">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference** section.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-172">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference** section.</span></span>

    ![Central Desktop configuration](./media/central-desktop-tutorial/tutorial_centraldesktop_configure.png) 

1. <span data-ttu-id="a8fd2-174">Sign in to your **Central Desktop** tenant.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-174">Sign in to your **Central Desktop** tenant.</span></span>

1. <span data-ttu-id="a8fd2-175">Go to **Settings**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-175">Go to **Settings**.</span></span> <span data-ttu-id="a8fd2-176">Select **Advanced**, and then select **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-176">Select **Advanced**, and then select **Single Sign On**.</span></span>

    <span data-ttu-id="a8fd2-177">![Setup - Advanced](./media/central-desktop-tutorial/ic769563.png "Setup - Advanced")</span><span class="sxs-lookup"><span data-stu-id="a8fd2-177">![Setup - Advanced](./media/central-desktop-tutorial/ic769563.png "Setup - Advanced")</span></span>

1. <span data-ttu-id="a8fd2-178">On the **Single Sign On Settings** page, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="a8fd2-178">On the **Single Sign On Settings** page, take the following steps:</span></span>

    <span data-ttu-id="a8fd2-179">![Single sign-on settings](./media/central-desktop-tutorial/ic769564.png "Single Sign On Settings")</span><span class="sxs-lookup"><span data-stu-id="a8fd2-179">![Single sign-on settings](./media/central-desktop-tutorial/ic769564.png "Single Sign On Settings")</span></span>
    
    <span data-ttu-id="a8fd2-180">a.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-180">a.</span></span> <span data-ttu-id="a8fd2-181">Select **Enable SAML v2 Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-181">Select **Enable SAML v2 Single Sign On**.</span></span>
    
    <span data-ttu-id="a8fd2-182">b.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-182">b.</span></span> <span data-ttu-id="a8fd2-183">In the **SSO URL** box, paste the **SAML Entity ID** value that you copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-183">In the **SSO URL** box, paste the **SAML Entity ID** value that you copied from the Azure portal.</span></span>
    
    <span data-ttu-id="a8fd2-184">c.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-184">c.</span></span> <span data-ttu-id="a8fd2-185">In the **SSO Login URL** box, paste the **SAML Single Sign-On Service URL** value that you copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-185">In the **SSO Login URL** box, paste the **SAML Single Sign-On Service URL** value that you copied from the Azure portal.</span></span>
    
    <span data-ttu-id="a8fd2-186">d.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-186">d.</span></span> <span data-ttu-id="a8fd2-187">In the **SSO Logout URL** box, paste the **Sign-Out URL** value that you copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-187">In the **SSO Logout URL** box, paste the **Sign-Out URL** value that you copied from the Azure portal.</span></span>

1. <span data-ttu-id="a8fd2-188">In the **Message Signature Verification Method** section, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="a8fd2-188">In the **Message Signature Verification Method** section, take the following steps:</span></span>

    <span data-ttu-id="a8fd2-189">![Message signature verification method](./media/central-desktop-tutorial/ic769565.png "Message Signature Verification Method") a.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-189">![Message signature verification method](./media/central-desktop-tutorial/ic769565.png "Message Signature Verification Method") a.</span></span> <span data-ttu-id="a8fd2-190">Select **Certificate**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-190">Select **Certificate**.</span></span>
    
    <span data-ttu-id="a8fd2-191">b.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-191">b.</span></span> <span data-ttu-id="a8fd2-192">In the **SSO Certificate** list, select **RSH SHA256**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-192">In the **SSO Certificate** list, select **RSH SHA256**.</span></span>
    
    <span data-ttu-id="a8fd2-193">c.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-193">c.</span></span> <span data-ttu-id="a8fd2-194">Open your downloaded certificate in Notepad.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-194">Open your downloaded certificate in Notepad.</span></span> <span data-ttu-id="a8fd2-195">Then copy the content of certificate and paste it into the **SSO Certificate** field.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-195">Then copy the content of certificate and paste it into the **SSO Certificate** field.</span></span>
        
    <span data-ttu-id="a8fd2-196">d.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-196">d.</span></span> <span data-ttu-id="a8fd2-197">Select **Display a link to your SAMLv2 login page**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-197">Select **Display a link to your SAMLv2 login page**.</span></span>
    
    <span data-ttu-id="a8fd2-198">e.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-198">e.</span></span> <span data-ttu-id="a8fd2-199">Select **Update**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-199">Select **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="a8fd2-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com) while you are setting up the app.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com) while you are setting up the app.</span></span> <span data-ttu-id="a8fd2-201">After you add this app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab, and then access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-201">After you add this app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab, and then access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a8fd2-202">You can read more about the embedded documentation feature at [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="a8fd2-202">You can read more about the embedded documentation feature at [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a8fd2-203">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a8fd2-203">Create an Azure AD test user</span></span>

<span data-ttu-id="a8fd2-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="a8fd2-206">**To create a test user in Azure AD, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a8fd2-206">**To create a test user in Azure AD, take the following steps:**</span></span>

1. <span data-ttu-id="a8fd2-207">In the Azure portal, in the left pane, select the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-207">In the Azure portal, in the left pane, select the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/central-desktop-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="a8fd2-209">To display the list of users, go to **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-209">To display the list of users, go to **Users and groups**.</span></span> <span data-ttu-id="a8fd2-210">Then select **All users**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-210">Then select **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/central-desktop-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="a8fd2-212">To open the **User** dialog box, select **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-212">To open the **User** dialog box, select **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/central-desktop-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="a8fd2-214">In the **User** dialog box, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="a8fd2-214">In the **User** dialog box, take the following steps:</span></span>

    ![The User dialog box](./media/central-desktop-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a8fd2-216">a.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-216">a.</span></span> <span data-ttu-id="a8fd2-217">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-217">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a8fd2-218">b.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-218">b.</span></span> <span data-ttu-id="a8fd2-219">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-219">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="a8fd2-220">c.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-220">c.</span></span> <span data-ttu-id="a8fd2-221">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-221">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="a8fd2-222">d.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-222">d.</span></span> <span data-ttu-id="a8fd2-223">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-223">Select **Create**.</span></span>
 
### <a name="create-a-central-desktop-test-user"></a><span data-ttu-id="a8fd2-224">Create a Central Desktop test user</span><span class="sxs-lookup"><span data-stu-id="a8fd2-224">Create a Central Desktop test user</span></span>

<span data-ttu-id="a8fd2-225">For Azure AD users to be able to sign in, they must be provisioned in the Central Desktop application.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-225">For Azure AD users to be able to sign in, they must be provisioned in the Central Desktop application.</span></span> <span data-ttu-id="a8fd2-226">This section describes how to create Azure AD user accounts in Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-226">This section describes how to create Azure AD user accounts in Central Desktop.</span></span>

> [!NOTE]
> <span data-ttu-id="a8fd2-227">To provision Azure AD user accounts, you can use any other Central Desktop user account creation tools or APIs that are provided by Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-227">To provision Azure AD user accounts, you can use any other Central Desktop user account creation tools or APIs that are provided by Central Desktop.</span></span>

<span data-ttu-id="a8fd2-228">**To provision user accounts to Central Desktop:**</span><span class="sxs-lookup"><span data-stu-id="a8fd2-228">**To provision user accounts to Central Desktop:**</span></span>

1. <span data-ttu-id="a8fd2-229">Sign in to your Central Desktop tenant.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-229">Sign in to your Central Desktop tenant.</span></span>

1. <span data-ttu-id="a8fd2-230">Go to **People** > **Internal Members**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-230">Go to **People** > **Internal Members**.</span></span>

1. <span data-ttu-id="a8fd2-231">Select **Add Internal Members**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-231">Select **Add Internal Members**.</span></span>

    <span data-ttu-id="a8fd2-232">![People](./media/central-desktop-tutorial/ic781051.png "People")</span><span class="sxs-lookup"><span data-stu-id="a8fd2-232">![People](./media/central-desktop-tutorial/ic781051.png "People")</span></span>
    
1. <span data-ttu-id="a8fd2-233">In the **Email Address of New Members** box, type an Azure AD account that you want to provision, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-233">In the **Email Address of New Members** box, type an Azure AD account that you want to provision, and then select **Next**.</span></span>

    <span data-ttu-id="a8fd2-234">![Email addresses of new members](./media/central-desktop-tutorial/ic781052.png "Email addresses of new members")</span><span class="sxs-lookup"><span data-stu-id="a8fd2-234">![Email addresses of new members](./media/central-desktop-tutorial/ic781052.png "Email addresses of new members")</span></span>

1. <span data-ttu-id="a8fd2-235">Select **Add Internal member(s)**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-235">Select **Add Internal member(s)**.</span></span>

    <span data-ttu-id="a8fd2-236">![Add internal member](./media/central-desktop-tutorial/ic781053.png "Add internal member")</span><span class="sxs-lookup"><span data-stu-id="a8fd2-236">![Add internal member](./media/central-desktop-tutorial/ic781053.png "Add internal member")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="a8fd2-237">The users that you add receive an email that includes a confirmation link for activating their accounts.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-237">The users that you add receive an email that includes a confirmation link for activating their accounts.</span></span>
   
### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a8fd2-238">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a8fd2-238">Assign the Azure AD test user</span></span>

<span data-ttu-id="a8fd2-239">In this section, you enable user Britta Simon to use Azure single sign-on by granting them access to Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-239">In this section, you enable user Britta Simon to use Azure single sign-on by granting them access to Central Desktop.</span></span>

![Assign the user role][200] 

<span data-ttu-id="a8fd2-241">**To assign Britta Simon to Central Desktop, take the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a8fd2-241">**To assign Britta Simon to Central Desktop, take the following steps:**</span></span>

1. <span data-ttu-id="a8fd2-242">In the Azure portal, open the applications view.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-242">In the Azure portal, open the applications view.</span></span> <span data-ttu-id="a8fd2-243">Go to the directory view, and then go to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-243">Go to the directory view, and then go to **Enterprise applications**.</span></span>

1. <span data-ttu-id="a8fd2-244">Select **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-244">Select **All applications**.</span></span>

    ![Assign user][201] 

1. <span data-ttu-id="a8fd2-246">In the applications list, select **Central Desktop**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-246">In the applications list, select **Central Desktop**.</span></span>

    ![The Central Desktop link in the applications list](./media/central-desktop-tutorial/tutorial_centraldesktop_app.png)  

1. <span data-ttu-id="a8fd2-248">In the menu on the left, select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-248">In the menu on the left, select **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="a8fd2-250">Select the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-250">Select the **Add** button.</span></span> <span data-ttu-id="a8fd2-251">Then select **Users and groups** in the **Add Assignment** dialog box.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-251">Then select **Users and groups** in the **Add Assignment** dialog box.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="a8fd2-253">In the **Users and groups** dialog box, select **Britta Simon** in the **Users** list.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-253">In the **Users and groups** dialog box, select **Britta Simon** in the **Users** list.</span></span>

1. <span data-ttu-id="a8fd2-254">In the **Users and groups** dialog box, click the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-254">In the **Users and groups** dialog box, click the **Select** button.</span></span>

1. <span data-ttu-id="a8fd2-255">In the  **Add Assignment** dialog box, select the **Assign** button.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-255">In the  **Add Assignment** dialog box, select the **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a8fd2-256">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="a8fd2-256">Test single sign-on</span></span>

<span data-ttu-id="a8fd2-257">In this section, test your Azure AD single sign-on configuration by using the access panel.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-257">In this section, test your Azure AD single sign-on configuration by using the access panel.</span></span>

<span data-ttu-id="a8fd2-258">When you select the Central Desktop tile in the access panel, you automatically get signed in to your Central Desktop application.</span><span class="sxs-lookup"><span data-stu-id="a8fd2-258">When you select the Central Desktop tile in the access panel, you automatically get signed in to your Central Desktop application.</span></span>
<span data-ttu-id="a8fd2-259">For more information about the access panel, see [Introduction to the access panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a8fd2-259">For more information about the access panel, see [Introduction to the access panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a8fd2-260">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a8fd2-260">Additional resources</span></span>

* [<span data-ttu-id="a8fd2-261">List of tutorials on how to integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8fd2-261">List of tutorials on how to integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a8fd2-262">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a8fd2-262">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/central-desktop-tutorial/tutorial_general_01.png
[2]: ./media/central-desktop-tutorial/tutorial_general_02.png
[3]: ./media/central-desktop-tutorial/tutorial_general_03.png
[4]: ./media/central-desktop-tutorial/tutorial_general_04.png

[100]: ./media/central-desktop-tutorial/tutorial_general_100.png

[200]: ./media/central-desktop-tutorial/tutorial_general_200.png
[201]: ./media/central-desktop-tutorial/tutorial_general_201.png
[202]: ./media/central-desktop-tutorial/tutorial_general_202.png
[203]: ./media/central-desktop-tutorial/tutorial_general_203.png

