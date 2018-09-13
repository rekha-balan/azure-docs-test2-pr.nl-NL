---
title: 'Tutorial: Azure Active Directory integration with TimeLive | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and TimeLive.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 34123629-4ad5-465c-a4c1-8299f857e720
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2017
ms.author: jeedes
ms.openlocfilehash: 26e70abc336b7cb13342873784aa2cb4048a47d9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870425"
---
# <a name="tutorial-azure-active-directory-integration-with-timelive"></a><span data-ttu-id="a2209-103">Tutorial: Azure Active Directory integration with TimeLive</span><span class="sxs-lookup"><span data-stu-id="a2209-103">Tutorial: Azure Active Directory integration with TimeLive</span></span>

<span data-ttu-id="a2209-104">In this tutorial, you learn how to integrate TimeLive with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a2209-104">In this tutorial, you learn how to integrate TimeLive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a2209-105">Integrating TimeLive with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a2209-105">Integrating TimeLive with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a2209-106">You can control in Azure AD who has access to TimeLive.</span><span class="sxs-lookup"><span data-stu-id="a2209-106">You can control in Azure AD who has access to TimeLive.</span></span>
- <span data-ttu-id="a2209-107">You can enable your users to automatically get signed-on to TimeLive (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="a2209-107">You can enable your users to automatically get signed-on to TimeLive (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a2209-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a2209-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="a2209-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a2209-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2209-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a2209-110">Prerequisites</span></span>

<span data-ttu-id="a2209-111">To configure Azure AD integration with TimeLive, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a2209-111">To configure Azure AD integration with TimeLive, you need the following items:</span></span>

- <span data-ttu-id="a2209-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a2209-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a2209-113">A TimeLive single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a2209-113">A TimeLive single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a2209-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a2209-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a2209-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a2209-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a2209-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a2209-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a2209-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2209-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a2209-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a2209-118">Scenario description</span></span>
<span data-ttu-id="a2209-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a2209-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a2209-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a2209-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a2209-121">Adding TimeLive from the gallery</span><span class="sxs-lookup"><span data-stu-id="a2209-121">Adding TimeLive from the gallery</span></span>
1. <span data-ttu-id="a2209-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a2209-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-timelive-from-the-gallery"></a><span data-ttu-id="a2209-123">Adding TimeLive from the gallery</span><span class="sxs-lookup"><span data-stu-id="a2209-123">Adding TimeLive from the gallery</span></span>
<span data-ttu-id="a2209-124">To configure the integration of TimeLive into Azure AD, you need to add TimeLive from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a2209-124">To configure the integration of TimeLive into Azure AD, you need to add TimeLive from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a2209-125">**To add TimeLive from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a2209-125">**To add TimeLive from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a2209-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a2209-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="a2209-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a2209-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a2209-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a2209-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="a2209-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a2209-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="a2209-133">In the search box, type **TimeLive**, select **TimeLive** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a2209-133">In the search box, type **TimeLive**, select **TimeLive** from result panel then click **Add** button to add the application.</span></span>

    ![TimeLive in the results list](./media/timelive-tutorial/tutorial_timelive_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a2209-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a2209-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="a2209-136">In this section, you configure and test Azure AD single sign-on with TimeLive based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a2209-136">In this section, you configure and test Azure AD single sign-on with TimeLive based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a2209-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TimeLive is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2209-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TimeLive is to a user in Azure AD.</span></span> <span data-ttu-id="a2209-138">In other words, a link relationship between an Azure AD user and the related user in TimeLive needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a2209-138">In other words, a link relationship between an Azure AD user and the related user in TimeLive needs to be established.</span></span>

<span data-ttu-id="a2209-139">In TimeLive, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="a2209-139">In TimeLive, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a2209-140">To configure and test Azure AD single sign-on with TimeLive, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a2209-140">To configure and test Azure AD single sign-on with TimeLive, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a2209-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a2209-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="a2209-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a2209-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="a2209-143">**[Create a TimeLive test user](#create-a-timelive-test-user)** - to have a counterpart of Britta Simon in TimeLive that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a2209-143">**[Create a TimeLive test user](#create-a-timelive-test-user)** - to have a counterpart of Britta Simon in TimeLive that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="a2209-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a2209-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="a2209-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a2209-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a2209-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a2209-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="a2209-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TimeLive application.</span><span class="sxs-lookup"><span data-stu-id="a2209-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TimeLive application.</span></span>

<span data-ttu-id="a2209-148">**To configure Azure AD single sign-on with TimeLive, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a2209-148">**To configure Azure AD single sign-on with TimeLive, perform the following steps:**</span></span>

1. <span data-ttu-id="a2209-149">In the Azure portal, on the **TimeLive** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a2209-149">In the Azure portal, on the **TimeLive** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="a2209-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a2209-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/timelive-tutorial/tutorial_timelive_samlbase.png)

1. <span data-ttu-id="a2209-153">On the **TimeLive Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a2209-153">On the **TimeLive Domain and URLs** section, perform the following steps:</span></span>

    ![TimeLive Domain and URLs single sign-on information](./media/timelive-tutorial/tutorial_timelive_url.png)

    <span data-ttu-id="a2209-155">a.</span><span class="sxs-lookup"><span data-stu-id="a2209-155">a.</span></span> <span data-ttu-id="a2209-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://domainname.livetecs.com/`</span><span class="sxs-lookup"><span data-stu-id="a2209-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://domainname.livetecs.com/`</span></span>

    <span data-ttu-id="a2209-157">b.</span><span class="sxs-lookup"><span data-stu-id="a2209-157">b.</span></span> <span data-ttu-id="a2209-158">In the **Identifier** textbox, type a URL using the following pattern: `https://domainname.livetecs.com/`</span><span class="sxs-lookup"><span data-stu-id="a2209-158">In the **Identifier** textbox, type a URL using the following pattern: `https://domainname.livetecs.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a2209-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="a2209-159">These values are not real.</span></span> <span data-ttu-id="a2209-160">Update these values with the actual Identifier and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="a2209-160">Update these values with the actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="a2209-161">Contact [TimeLive Client support team](mailto:support@livetecs.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="a2209-161">Contact [TimeLive Client support team](mailto:support@livetecs.com) to get these values.</span></span> 

1. <span data-ttu-id="a2209-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a2209-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/timelive-tutorial/tutorial_timelive_certificate.png) 

1. <span data-ttu-id="a2209-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a2209-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/timelive-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="a2209-166">On the **TimeLive Configuration** section, click **Configure TimeLive** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="a2209-166">On the **TimeLive Configuration** section, click **Configure TimeLive** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a2209-167">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="a2209-167">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![TimeLive Configuration](./media/timelive-tutorial/tutorial_timelive_configure.png)

1. <span data-ttu-id="a2209-169">In a different web browser window, log in to your TimeLive company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="a2209-169">In a different web browser window, log in to your TimeLive company site as an administrator.</span></span>

1. <span data-ttu-id="a2209-170">Select **Preferences** under **Admin Options**.</span><span class="sxs-lookup"><span data-stu-id="a2209-170">Select **Preferences** under **Admin Options**.</span></span>

    ![TimeLive Configuration](./media/timelive-tutorial/configure1.png)

1. <span data-ttu-id="a2209-172">In the **Application Preference** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a2209-172">In the **Application Preference** section, perform the following steps:</span></span>
    
    ![TimeLive Configuration](./media/timelive-tutorial/configure2.png)

    <span data-ttu-id="a2209-174">a.</span><span class="sxs-lookup"><span data-stu-id="a2209-174">a.</span></span> <span data-ttu-id="a2209-175">Select **Security** tab.</span><span class="sxs-lookup"><span data-stu-id="a2209-175">Select **Security** tab.</span></span>

    <span data-ttu-id="a2209-176">b.</span><span class="sxs-lookup"><span data-stu-id="a2209-176">b.</span></span> <span data-ttu-id="a2209-177">Check **Enable Single Sign On (SSO)** checkbox.</span><span class="sxs-lookup"><span data-stu-id="a2209-177">Check **Enable Single Sign On (SSO)** checkbox.</span></span>

    <span data-ttu-id="a2209-178">c.</span><span class="sxs-lookup"><span data-stu-id="a2209-178">c.</span></span> <span data-ttu-id="a2209-179">Select **SAML** from the drop down menu with heading **Sign in using Single Sign-On (SSO) with**.</span><span class="sxs-lookup"><span data-stu-id="a2209-179">Select **SAML** from the drop down menu with heading **Sign in using Single Sign-On (SSO) with**.</span></span>

    <span data-ttu-id="a2209-180">d.</span><span class="sxs-lookup"><span data-stu-id="a2209-180">d.</span></span> <span data-ttu-id="a2209-181">In the **SAML SSO URL**, Paste **SAML Single Sign-On Service URL** value which you have copied form the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a2209-181">In the **SAML SSO URL**, Paste **SAML Single Sign-On Service URL** value which you have copied form the Azure portal.</span></span>

    <span data-ttu-id="a2209-182">e.</span><span class="sxs-lookup"><span data-stu-id="a2209-182">e.</span></span> <span data-ttu-id="a2209-183">In the **Remote logout URL**, Paste **Sign-Out URL** value which you have copied form the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a2209-183">In the **Remote logout URL**, Paste **Sign-Out URL** value which you have copied form the Azure portal.</span></span>

    <span data-ttu-id="a2209-184">f.</span><span class="sxs-lookup"><span data-stu-id="a2209-184">f.</span></span> <span data-ttu-id="a2209-185">Open the downloaded **base-64 encoded certificate** from Azure portal in Notepad, copy the content, and then paste it into the **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="a2209-185">Open the downloaded **base-64 encoded certificate** from Azure portal in Notepad, copy the content, and then paste it into the **X.509 Certificate** textbox.</span></span>

    <span data-ttu-id="a2209-186">g.</span><span class="sxs-lookup"><span data-stu-id="a2209-186">g.</span></span> <span data-ttu-id="a2209-187">Click **Update**.</span><span class="sxs-lookup"><span data-stu-id="a2209-187">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="a2209-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="a2209-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a2209-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="a2209-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a2209-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a2209-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a2209-191">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a2209-191">Create an Azure AD test user</span></span>

<span data-ttu-id="a2209-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a2209-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="a2209-194">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a2209-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a2209-195">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="a2209-195">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/timelive-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="a2209-197">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a2209-197">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/timelive-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="a2209-199">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="a2209-199">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/timelive-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="a2209-201">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a2209-201">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/timelive-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a2209-203">a.</span><span class="sxs-lookup"><span data-stu-id="a2209-203">a.</span></span> <span data-ttu-id="a2209-204">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a2209-204">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a2209-205">b.</span><span class="sxs-lookup"><span data-stu-id="a2209-205">b.</span></span> <span data-ttu-id="a2209-206">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a2209-206">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="a2209-207">c.</span><span class="sxs-lookup"><span data-stu-id="a2209-207">c.</span></span> <span data-ttu-id="a2209-208">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="a2209-208">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="a2209-209">d.</span><span class="sxs-lookup"><span data-stu-id="a2209-209">d.</span></span> <span data-ttu-id="a2209-210">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a2209-210">Click **Create**.</span></span>
 
### <a name="create-a-timelive-test-user"></a><span data-ttu-id="a2209-211">Create a TimeLive test user</span><span class="sxs-lookup"><span data-stu-id="a2209-211">Create a TimeLive test user</span></span>

<span data-ttu-id="a2209-212">The objective of this section is to create a user called Britta Simon in TimeLive.</span><span class="sxs-lookup"><span data-stu-id="a2209-212">The objective of this section is to create a user called Britta Simon in TimeLive.</span></span> <span data-ttu-id="a2209-213">TimeLive supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="a2209-213">TimeLive supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="a2209-214">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="a2209-214">There is no action item for you in this section.</span></span> <span data-ttu-id="a2209-215">A new user is created during an attempt to access TimeLive if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="a2209-215">A new user is created during an attempt to access TimeLive if it doesn't exist yet.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a2209-216">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a2209-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="a2209-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TimeLive.</span><span class="sxs-lookup"><span data-stu-id="a2209-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TimeLive.</span></span>

![Assign the user role][200] 

<span data-ttu-id="a2209-219">**To assign Britta Simon to TimeLive, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a2209-219">**To assign Britta Simon to TimeLive, perform the following steps:**</span></span>

1. <span data-ttu-id="a2209-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a2209-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="a2209-222">In the applications list, select **TimeLive**.</span><span class="sxs-lookup"><span data-stu-id="a2209-222">In the applications list, select **TimeLive**.</span></span>

    ![The TimeLive link in the Applications list](./media/timelive-tutorial/tutorial_timelive_app.png)  

1. <span data-ttu-id="a2209-224">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a2209-224">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="a2209-226">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a2209-226">Click **Add** button.</span></span> <span data-ttu-id="a2209-227">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a2209-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="a2209-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a2209-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="a2209-230">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a2209-230">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="a2209-231">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a2209-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="a2209-232">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="a2209-232">Test single sign-on</span></span>

<span data-ttu-id="a2209-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a2209-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a2209-234">When you click the TimeLive tile in the Access Panel, you should get automatically signed-on to your TimeLive application.</span><span class="sxs-lookup"><span data-stu-id="a2209-234">When you click the TimeLive tile in the Access Panel, you should get automatically signed-on to your TimeLive application.</span></span>
<span data-ttu-id="a2209-235">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a2209-235">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a2209-236">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a2209-236">Additional resources</span></span>

* [<span data-ttu-id="a2209-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2209-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a2209-238">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a2209-238">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/timelive-tutorial/tutorial_general_01.png
[2]: ./media/timelive-tutorial/tutorial_general_02.png
[3]: ./media/timelive-tutorial/tutorial_general_03.png
[4]: ./media/timelive-tutorial/tutorial_general_04.png

[100]: ./media/timelive-tutorial/tutorial_general_100.png

[200]: ./media/timelive-tutorial/tutorial_general_200.png
[201]: ./media/timelive-tutorial/tutorial_general_201.png
[202]: ./media/timelive-tutorial/tutorial_general_202.png
[203]: ./media/timelive-tutorial/tutorial_general_203.png

