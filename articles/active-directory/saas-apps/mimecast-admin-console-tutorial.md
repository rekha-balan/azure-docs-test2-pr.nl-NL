---
title: 'Tutorial: Azure Active Directory integration with Mimecast Admin Console | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Mimecast Admin Console.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: ce4142c5b4a20886a94c87699f262f7238fc2cb4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857694"
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a><span data-ttu-id="e5bb1-103">Tutorial: Azure Active Directory integration with Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="e5bb1-103">Tutorial: Azure Active Directory integration with Mimecast Admin Console</span></span>

<span data-ttu-id="e5bb1-104">In this tutorial, you learn how to integrate Mimecast Admin Console with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e5bb1-104">In this tutorial, you learn how to integrate Mimecast Admin Console with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e5bb1-105">Integrating Mimecast Admin Console with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="e5bb1-105">Integrating Mimecast Admin Console with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e5bb1-106">You can control in Azure AD who has access to Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-106">You can control in Azure AD who has access to Mimecast Admin Console.</span></span>
- <span data-ttu-id="e5bb1-107">You can enable your users to automatically get signed-on to Mimecast Admin Console (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-107">You can enable your users to automatically get signed-on to Mimecast Admin Console (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e5bb1-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="e5bb1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="e5bb1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5bb1-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e5bb1-110">Prerequisites</span></span>

<span data-ttu-id="e5bb1-111">To configure Azure AD integration with Mimecast Admin Console, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="e5bb1-111">To configure Azure AD integration with Mimecast Admin Console, you need the following items:</span></span>

- <span data-ttu-id="e5bb1-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="e5bb1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e5bb1-113">A Mimecast Admin Console single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="e5bb1-113">A Mimecast Admin Console single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e5bb1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e5bb1-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="e5bb1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e5bb1-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e5bb1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e5bb1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e5bb1-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="e5bb1-118">Scenario description</span></span>
<span data-ttu-id="e5bb1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e5bb1-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="e5bb1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e5bb1-121">Adding Mimecast Admin Console from the gallery</span><span class="sxs-lookup"><span data-stu-id="e5bb1-121">Adding Mimecast Admin Console from the gallery</span></span>
1. <span data-ttu-id="e5bb1-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e5bb1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-admin-console-from-the-gallery"></a><span data-ttu-id="e5bb1-123">Adding Mimecast Admin Console from the gallery</span><span class="sxs-lookup"><span data-stu-id="e5bb1-123">Adding Mimecast Admin Console from the gallery</span></span>
<span data-ttu-id="e5bb1-124">To configure the integration of Mimecast Admin Console into Azure AD, you need to add Mimecast Admin Console from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-124">To configure the integration of Mimecast Admin Console into Azure AD, you need to add Mimecast Admin Console from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e5bb1-125">**To add Mimecast Admin Console from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e5bb1-125">**To add Mimecast Admin Console from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e5bb1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="e5bb1-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e5bb1-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="e5bb1-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="e5bb1-133">In the search box, type **Mimecast Admin Console**, select **Mimecast Admin Console** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-133">In the search box, type **Mimecast Admin Console**, select **Mimecast Admin Console** from result panel then click **Add** button to add the application.</span></span>

    ![Mimecast Admin Console in the results list](./media/mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e5bb1-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e5bb1-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e5bb1-136">In this section, you configure and test Azure AD single sign-on with Mimecast Admin Console based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e5bb1-136">In this section, you configure and test Azure AD single sign-on with Mimecast Admin Console based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e5bb1-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Admin Console is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Admin Console is to a user in Azure AD.</span></span> <span data-ttu-id="e5bb1-138">In other words, a link relationship between an Azure AD user and the related user in Mimecast Admin Console needs to be established.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-138">In other words, a link relationship between an Azure AD user and the related user in Mimecast Admin Console needs to be established.</span></span>

<span data-ttu-id="e5bb1-139">In Mimecast Admin Console, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-139">In Mimecast Admin Console, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e5bb1-140">To configure and test Azure AD single sign-on with Mimecast Admin Console, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e5bb1-140">To configure and test Azure AD single sign-on with Mimecast Admin Console, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e5bb1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="e5bb1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="e5bb1-143">**[Create a Mimecast Admin Console test user](#create-a-mimecast-admin-console-test-user)** - to have a counterpart of Britta Simon in Mimecast Admin Console that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-143">**[Create a Mimecast Admin Console test user](#create-a-mimecast-admin-console-test-user)** - to have a counterpart of Britta Simon in Mimecast Admin Console that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="e5bb1-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="e5bb1-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e5bb1-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e5bb1-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e5bb1-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Admin Console application.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Admin Console application.</span></span>

<span data-ttu-id="e5bb1-148">**To configure Azure AD single sign-on with Mimecast Admin Console, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e5bb1-148">**To configure Azure AD single sign-on with Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="e5bb1-149">In the Azure portal, on the **Mimecast Admin Console** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-149">In the Azure portal, on the **Mimecast Admin Console** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="e5bb1-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

1. <span data-ttu-id="e5bb1-153">On the **Mimecast Admin Console Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e5bb1-153">On the **Mimecast Admin Console Domain and URLs** section, perform the following steps:</span></span>

    ![Mimecast Admin Console Domain and URLs single sign-on information](./media/mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    <span data-ttu-id="e5bb1-155">In the **Sign-on URL** textbox, type the URL:</span><span class="sxs-lookup"><span data-stu-id="e5bb1-155">In the **Sign-on URL** textbox, type the URL:</span></span>
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > <span data-ttu-id="e5bb1-156">The sign on URL is region specific.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-156">The sign on URL is region specific.</span></span>

1. <span data-ttu-id="e5bb1-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

1. <span data-ttu-id="e5bb1-159">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-159">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/mimecast-admin-console-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="e5bb1-161">On the **Mimecast Admin Console Configuration** section, click **Configure Mimecast Admin Console** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-161">On the **Mimecast Admin Console Configuration** section, click **Configure Mimecast Admin Console** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e5bb1-162">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="e5bb1-162">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Mimecast Admin Console Configuration](./media/mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

1. <span data-ttu-id="e5bb1-164">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-164">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span></span>

1. <span data-ttu-id="e5bb1-165">Go to **Services \> Application**.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-165">Go to **Services \> Application**.</span></span>

    <span data-ttu-id="e5bb1-166">![Services](./media/mimecast-admin-console-tutorial/ic794998.png "Services")</span><span class="sxs-lookup"><span data-stu-id="e5bb1-166">![Services](./media/mimecast-admin-console-tutorial/ic794998.png "Services")</span></span>

1. <span data-ttu-id="e5bb1-167">Click **Authentication Profiles**.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-167">Click **Authentication Profiles**.</span></span>

    <span data-ttu-id="e5bb1-168">![Authentication Profiles](./media/mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles")</span><span class="sxs-lookup"><span data-stu-id="e5bb1-168">![Authentication Profiles](./media/mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles")</span></span>
    
1. <span data-ttu-id="e5bb1-169">Click **New Authentication Profile**.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-169">Click **New Authentication Profile**.</span></span>

    <span data-ttu-id="e5bb1-170">![New Authentication Profiles](./media/mimecast-admin-console-tutorial/ic795000.png "New Authentication Profiles")</span><span class="sxs-lookup"><span data-stu-id="e5bb1-170">![New Authentication Profiles](./media/mimecast-admin-console-tutorial/ic795000.png "New Authentication Profiles")</span></span>

1. <span data-ttu-id="e5bb1-171">In the **Authentication Profile** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e5bb1-171">In the **Authentication Profile** section, perform the following steps:</span></span>

    <span data-ttu-id="e5bb1-172">![Authentication Profile](./media/mimecast-admin-console-tutorial/ic795015.png "Authentication Profile")</span><span class="sxs-lookup"><span data-stu-id="e5bb1-172">![Authentication Profile](./media/mimecast-admin-console-tutorial/ic795015.png "Authentication Profile")</span></span>
    
    <span data-ttu-id="e5bb1-173">a.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-173">a.</span></span> <span data-ttu-id="e5bb1-174">In the **Description** textbox, type a name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-174">In the **Description** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="e5bb1-175">b.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-175">b.</span></span> <span data-ttu-id="e5bb1-176">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-176">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span></span>
    
    <span data-ttu-id="e5bb1-177">c.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-177">c.</span></span> <span data-ttu-id="e5bb1-178">As **Provider**, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-178">As **Provider**, select **Azure Active Directory**.</span></span>
    
    <span data-ttu-id="e5bb1-179">d.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-179">d.</span></span> <span data-ttu-id="e5bb1-180">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **Issuer URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-180">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **Issuer URL** textbox.</span></span>
    
    <span data-ttu-id="e5bb1-181">e.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-181">e.</span></span> <span data-ttu-id="e5bb1-182">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-182">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Login URL** textbox.</span></span>

    <span data-ttu-id="e5bb1-183">f.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-183">f.</span></span> <span data-ttu-id="e5bb1-184">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-184">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Logout URL** textbox.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="e5bb1-185">The Login URL value and the Logout URL value are for the Mimecast Admin Console the same.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-185">The Login URL value and the Logout URL value are for the Mimecast Admin Console the same.</span></span>
    
    <span data-ttu-id="e5bb1-186">g.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-186">g.</span></span> <span data-ttu-id="e5bb1-187">Open your base-64 certificate downloaded from Azure portal in notepad, remove the first line (“*--*“) and the last line (“*--*“), copy the remaining content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-187">Open your base-64 certificate downloaded from Azure portal in notepad, remove the first line (“*--*“) and the last line (“*--*“), copy the remaining content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>
    
    <span data-ttu-id="e5bb1-188">h.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-188">h.</span></span> <span data-ttu-id="e5bb1-189">Select **Allow Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-189">Select **Allow Single Sign On**.</span></span>
    
    <span data-ttu-id="e5bb1-190">i.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-190">i.</span></span> <span data-ttu-id="e5bb1-191">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e5bb1-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="e5bb1-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e5bb1-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e5bb1-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e5bb1-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e5bb1-195">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e5bb1-195">Create an Azure AD test user</span></span>

<span data-ttu-id="e5bb1-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="e5bb1-198">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e5bb1-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e5bb1-199">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-199">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/mimecast-admin-console-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="e5bb1-201">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-201">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/mimecast-admin-console-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="e5bb1-203">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-203">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/mimecast-admin-console-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="e5bb1-205">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e5bb1-205">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/mimecast-admin-console-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e5bb1-207">a.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-207">a.</span></span> <span data-ttu-id="e5bb1-208">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-208">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e5bb1-209">b.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-209">b.</span></span> <span data-ttu-id="e5bb1-210">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-210">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="e5bb1-211">c.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-211">c.</span></span> <span data-ttu-id="e5bb1-212">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-212">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="e5bb1-213">d.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-213">d.</span></span> <span data-ttu-id="e5bb1-214">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-214">Click **Create**.</span></span>
 
### <a name="create-a-mimecast-admin-console-test-user"></a><span data-ttu-id="e5bb1-215">Create a Mimecast Admin Console test user</span><span class="sxs-lookup"><span data-stu-id="e5bb1-215">Create a Mimecast Admin Console test user</span></span>

<span data-ttu-id="e5bb1-216">In order to enable Azure AD users to log into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-216">In order to enable Azure AD users to log into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span></span> <span data-ttu-id="e5bb1-217">In the case of Mimecast Admin Console, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-217">In the case of Mimecast Admin Console, provisioning is a manual task.</span></span>

* <span data-ttu-id="e5bb1-218">You need to register a domain before you can create users.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-218">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="e5bb1-219">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e5bb1-219">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="e5bb1-220">Sign on to your **Mimecast Admin Console** as administrator.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-220">Sign on to your **Mimecast Admin Console** as administrator.</span></span>
1. <span data-ttu-id="e5bb1-221">Go to **Directories \> Internal**.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-221">Go to **Directories \> Internal**.</span></span>
   
   <span data-ttu-id="e5bb1-222">![Directories](./media/mimecast-admin-console-tutorial/ic795003.png "Directories")</span><span class="sxs-lookup"><span data-stu-id="e5bb1-222">![Directories](./media/mimecast-admin-console-tutorial/ic795003.png "Directories")</span></span>
1. <span data-ttu-id="e5bb1-223">Click **Register New Domain**.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-223">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="e5bb1-224">![Register New Domain](./media/mimecast-admin-console-tutorial/ic795004.png "Register New Domain")</span><span class="sxs-lookup"><span data-stu-id="e5bb1-224">![Register New Domain](./media/mimecast-admin-console-tutorial/ic795004.png "Register New Domain")</span></span>
1. <span data-ttu-id="e5bb1-225">After your new domain has been created, click **New Address**.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-225">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="e5bb1-226">![New Address](./media/mimecast-admin-console-tutorial/ic795005.png "New Address")</span><span class="sxs-lookup"><span data-stu-id="e5bb1-226">![New Address](./media/mimecast-admin-console-tutorial/ic795005.png "New Address")</span></span>
1. <span data-ttu-id="e5bb1-227">In the new address dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e5bb1-227">In the new address dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="e5bb1-228">![Save](./media/mimecast-admin-console-tutorial/ic795006.png "Save")</span><span class="sxs-lookup"><span data-stu-id="e5bb1-228">![Save](./media/mimecast-admin-console-tutorial/ic795006.png "Save")</span></span>
   
   <span data-ttu-id="e5bb1-229">a.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-229">a.</span></span> <span data-ttu-id="e5bb1-230">Type the **Email Address**, **Global Name**, **Password**, and **Confirm Password** attributes of a valid Azure AD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-230">Type the **Email Address**, **Global Name**, **Password**, and **Confirm Password** attributes of a valid Azure AD account you want to provision into the related textboxes.</span></span>

   <span data-ttu-id="e5bb1-231">b.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-231">b.</span></span> <span data-ttu-id="e5bb1-232">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-232">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="e5bb1-233">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-233">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console to provision Azure AD user accounts.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e5bb1-234">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e5bb1-234">Assign the Azure AD test user</span></span>

<span data-ttu-id="e5bb1-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Admin Console.</span></span>

![Assign the user role][200] 

<span data-ttu-id="e5bb1-237">**To assign Britta Simon to Mimecast Admin Console, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e5bb1-237">**To assign Britta Simon to Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="e5bb1-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="e5bb1-240">In the applications list, select **Mimecast Admin Console**.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-240">In the applications list, select **Mimecast Admin Console**.</span></span>

    ![The Mimecast Admin Console link in the Applications list](./media/mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

1. <span data-ttu-id="e5bb1-242">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-242">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="e5bb1-244">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-244">Click **Add** button.</span></span> <span data-ttu-id="e5bb1-245">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="e5bb1-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="e5bb1-248">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-248">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="e5bb1-249">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e5bb1-250">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="e5bb1-250">Test single sign-on</span></span>

<span data-ttu-id="e5bb1-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e5bb1-252">When you click the Mimecast Admin Console tile in the Access Panel, you should get automatically signed-on to your Mimecast Admin Console application.</span><span class="sxs-lookup"><span data-stu-id="e5bb1-252">When you click the Mimecast Admin Console tile in the Access Panel, you should get automatically signed-on to your Mimecast Admin Console application.</span></span>
<span data-ttu-id="e5bb1-253">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e5bb1-253">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e5bb1-254">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e5bb1-254">Additional resources</span></span>

* [<span data-ttu-id="e5bb1-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e5bb1-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="e5bb1-256">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e5bb1-256">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/mimecast-admin-console-tutorial/tutorial_general_203.png

