---
title: 'Tutorial: Azure Active Directory integration with Evidence.com | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Evidence.com.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 52f582f0cac55aaff90cf21097e679617a50ef0b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870364"
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a><span data-ttu-id="371c4-103">Tutorial: Azure Active Directory integration with Evidence.com</span><span class="sxs-lookup"><span data-stu-id="371c4-103">Tutorial: Azure Active Directory integration with Evidence.com</span></span>

<span data-ttu-id="371c4-104">In this tutorial, you learn how to integrate Evidence.com with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="371c4-104">In this tutorial, you learn how to integrate Evidence.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="371c4-105">Integrating Evidence.com with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="371c4-105">Integrating Evidence.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="371c4-106">You can control in Azure AD who has access to Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="371c4-106">You can control in Azure AD who has access to Evidence.com.</span></span>
- <span data-ttu-id="371c4-107">You can enable your users to automatically get signed-on to Evidence.com (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="371c4-107">You can enable your users to automatically get signed-on to Evidence.com (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="371c4-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="371c4-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="371c4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="371c4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="371c4-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="371c4-110">Prerequisites</span></span>

<span data-ttu-id="371c4-111">To configure Azure AD integration with Evidence.com, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="371c4-111">To configure Azure AD integration with Evidence.com, you need the following items:</span></span>

- <span data-ttu-id="371c4-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="371c4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="371c4-113">A Evidence.com single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="371c4-113">A Evidence.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="371c4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="371c4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="371c4-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="371c4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="371c4-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="371c4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="371c4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="371c4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="371c4-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="371c4-118">Scenario description</span></span>
<span data-ttu-id="371c4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="371c4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="371c4-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="371c4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="371c4-121">Adding Evidence.com from the gallery</span><span class="sxs-lookup"><span data-stu-id="371c4-121">Adding Evidence.com from the gallery</span></span>
1. <span data-ttu-id="371c4-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="371c4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evidencecom-from-the-gallery"></a><span data-ttu-id="371c4-123">Adding Evidence.com from the gallery</span><span class="sxs-lookup"><span data-stu-id="371c4-123">Adding Evidence.com from the gallery</span></span>
<span data-ttu-id="371c4-124">To configure the integration of Evidence.com into Azure AD, you need to add Evidence.com from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="371c4-124">To configure the integration of Evidence.com into Azure AD, you need to add Evidence.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="371c4-125">**To add Evidence.com from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="371c4-125">**To add Evidence.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="371c4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="371c4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="371c4-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="371c4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="371c4-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="371c4-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="371c4-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="371c4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="371c4-133">In the search box, type **Evidence.com**, select **Evidence.com** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="371c4-133">In the search box, type **Evidence.com**, select **Evidence.com** from result panel then click **Add** button to add the application.</span></span>

    ![Evidence.com in the results list](./media/evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="371c4-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="371c4-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="371c4-136">In this section, you configure and test Azure AD single sign-on with Evidence.com based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="371c4-136">In this section, you configure and test Azure AD single sign-on with Evidence.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="371c4-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Evidence.com is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="371c4-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Evidence.com is to a user in Azure AD.</span></span> <span data-ttu-id="371c4-138">In other words, a link relationship between an Azure AD user and the related user in Evidence.com needs to be established.</span><span class="sxs-lookup"><span data-stu-id="371c4-138">In other words, a link relationship between an Azure AD user and the related user in Evidence.com needs to be established.</span></span>

<span data-ttu-id="371c4-139">In Evidence.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="371c4-139">In Evidence.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="371c4-140">To configure and test Azure AD single sign-on with Evidence.com, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="371c4-140">To configure and test Azure AD single sign-on with Evidence.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="371c4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="371c4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="371c4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="371c4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="371c4-143">**[Create a Evidence.com test user](#create-a-evidencecom-test-user)** - to have a counterpart of Britta Simon in Evidence.com that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="371c4-143">**[Create a Evidence.com test user](#create-a-evidencecom-test-user)** - to have a counterpart of Britta Simon in Evidence.com that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="371c4-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="371c4-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="371c4-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="371c4-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="371c4-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="371c4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="371c4-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Evidence.com application.</span><span class="sxs-lookup"><span data-stu-id="371c4-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Evidence.com application.</span></span>

<span data-ttu-id="371c4-148">**To configure Azure AD single sign-on with Evidence.com, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="371c4-148">**To configure Azure AD single sign-on with Evidence.com, perform the following steps:**</span></span>

1. <span data-ttu-id="371c4-149">In the Azure portal, on the **Evidence.com** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="371c4-149">In the Azure portal, on the **Evidence.com** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="371c4-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="371c4-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/evidence-tutorial/tutorial_evidence.com_samlbase.png)

1. <span data-ttu-id="371c4-153">On the **Evidence.com Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="371c4-153">On the **Evidence.com Domain and URLs** section, perform the following steps:</span></span>

    ![Evidence.com Domain and URLs single sign-on information](./media/evidence-tutorial/tutorial_evidence.com_url.png)

    <span data-ttu-id="371c4-155">a.</span><span class="sxs-lookup"><span data-stu-id="371c4-155">a.</span></span> <span data-ttu-id="371c4-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="371c4-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<yourtenant>.evidence.com`</span></span>

    <span data-ttu-id="371c4-157">b.</span><span class="sxs-lookup"><span data-stu-id="371c4-157">b.</span></span> <span data-ttu-id="371c4-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="371c4-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<yourtenant>.evidence.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="371c4-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="371c4-159">These values are not real.</span></span> <span data-ttu-id="371c4-160">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="371c4-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="371c4-161">Contact [Evidence.com Client support team](https://communities.taser.com/support/SupportContactUs?typ=LE) to get these values.</span><span class="sxs-lookup"><span data-stu-id="371c4-161">Contact [Evidence.com Client support team](https://communities.taser.com/support/SupportContactUs?typ=LE) to get these values.</span></span> 

1. <span data-ttu-id="371c4-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="371c4-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/evidence-tutorial/tutorial_evidence.com_certificate.png) 

1. <span data-ttu-id="371c4-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="371c4-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/evidence-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="371c4-166">On the **Evidence.com Configuration** section, click **Configure Evidence.com** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="371c4-166">On the **Evidence.com Configuration** section, click **Configure Evidence.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="371c4-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="371c4-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Evidence.com Configuration](./media/evidence-tutorial/tutorial_evidence.com_configure.png) 

1. <span data-ttu-id="371c4-169">In a separate web browser window, login to your Evidence.com tenant as an administrator and navigate to **Admin** Tab</span><span class="sxs-lookup"><span data-stu-id="371c4-169">In a separate web browser window, login to your Evidence.com tenant as an administrator and navigate to **Admin** Tab</span></span>

1. <span data-ttu-id="371c4-170">Click on **Agency Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="371c4-170">Click on **Agency Single Sign On**</span></span>

1. <span data-ttu-id="371c4-171">Select **SAML Based Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="371c4-171">Select **SAML Based Single Sign On**</span></span>

1. <span data-ttu-id="371c4-172">Copy the **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** values shown in the Azure portal and to the corresponding fields in Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="371c4-172">Copy the **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** values shown in the Azure portal and to the corresponding fields in Evidence.com.</span></span>

1. <span data-ttu-id="371c4-173">Open your downloaded Certificate(Base64) file in notepad, copy the content of it into your clipboard, and then paste it to the **Security Certificate** box.</span><span class="sxs-lookup"><span data-stu-id="371c4-173">Open your downloaded Certificate(Base64) file in notepad, copy the content of it into your clipboard, and then paste it to the **Security Certificate** box.</span></span> 

1. <span data-ttu-id="371c4-174">Save the configuration in Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="371c4-174">Save the configuration in Evidence.com.</span></span>

> [!TIP]
> <span data-ttu-id="371c4-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="371c4-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="371c4-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="371c4-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="371c4-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="371c4-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="371c4-178">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="371c4-178">Create an Azure AD test user</span></span>

<span data-ttu-id="371c4-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="371c4-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="371c4-181">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="371c4-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="371c4-182">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="371c4-182">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/evidence-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="371c4-184">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="371c4-184">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/evidence-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="371c4-186">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="371c4-186">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/evidence-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="371c4-188">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="371c4-188">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/evidence-tutorial/create_aaduser_04.png)

    <span data-ttu-id="371c4-190">a.</span><span class="sxs-lookup"><span data-stu-id="371c4-190">a.</span></span> <span data-ttu-id="371c4-191">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="371c4-191">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="371c4-192">b.</span><span class="sxs-lookup"><span data-stu-id="371c4-192">b.</span></span> <span data-ttu-id="371c4-193">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="371c4-193">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="371c4-194">c.</span><span class="sxs-lookup"><span data-stu-id="371c4-194">c.</span></span> <span data-ttu-id="371c4-195">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="371c4-195">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="371c4-196">d.</span><span class="sxs-lookup"><span data-stu-id="371c4-196">d.</span></span> <span data-ttu-id="371c4-197">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="371c4-197">Click **Create**.</span></span>
 
### <a name="create-a-evidencecom-test-user"></a><span data-ttu-id="371c4-198">Create a Evidence.com test user</span><span class="sxs-lookup"><span data-stu-id="371c4-198">Create a Evidence.com test user</span></span>

<span data-ttu-id="371c4-199">For Azure AD users to be able to sign in, they must be provisioned for access inside the Evidence.com application.</span><span class="sxs-lookup"><span data-stu-id="371c4-199">For Azure AD users to be able to sign in, they must be provisioned for access inside the Evidence.com application.</span></span> <span data-ttu-id="371c4-200">This section describes how to create Azure AD user accounts inside Evidence.com</span><span class="sxs-lookup"><span data-stu-id="371c4-200">This section describes how to create Azure AD user accounts inside Evidence.com</span></span>

<span data-ttu-id="371c4-201">**To provision a user account in Evidence.com:**</span><span class="sxs-lookup"><span data-stu-id="371c4-201">**To provision a user account in Evidence.com:**</span></span>

1. <span data-ttu-id="371c4-202">In a web browser window, log into your Evidence.com company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="371c4-202">In a web browser window, log into your Evidence.com company site as an administrator.</span></span>

1. <span data-ttu-id="371c4-203">Navigate to **Admin** tab.</span><span class="sxs-lookup"><span data-stu-id="371c4-203">Navigate to **Admin** tab.</span></span>

1. <span data-ttu-id="371c4-204">Click on **Add User**.</span><span class="sxs-lookup"><span data-stu-id="371c4-204">Click on **Add User**.</span></span>

1. <span data-ttu-id="371c4-205">Click the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="371c4-205">Click the **Add** button.</span></span>

1. <span data-ttu-id="371c4-206">The **Email Address** of the added user must match the username of the users in Azure AD who you wish to give access.</span><span class="sxs-lookup"><span data-stu-id="371c4-206">The **Email Address** of the added user must match the username of the users in Azure AD who you wish to give access.</span></span> <span data-ttu-id="371c4-207">If the username and email address are not the same value in your organization, you can use the **Evidence.com > Attributes > Single Sign-On** section of the Azure portal to change the nameidenitifer sent to Evidence.com to be the email address.</span><span class="sxs-lookup"><span data-stu-id="371c4-207">If the username and email address are not the same value in your organization, you can use the **Evidence.com > Attributes > Single Sign-On** section of the Azure portal to change the nameidenitifer sent to Evidence.com to be the email address.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="371c4-208">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="371c4-208">Assign the Azure AD test user</span></span>

<span data-ttu-id="371c4-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="371c4-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Evidence.com.</span></span>

![Assign the user role][200] 

<span data-ttu-id="371c4-211">**To assign Britta Simon to Evidence.com, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="371c4-211">**To assign Britta Simon to Evidence.com, perform the following steps:**</span></span>

1. <span data-ttu-id="371c4-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="371c4-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="371c4-214">In the applications list, select **Evidence.com**.</span><span class="sxs-lookup"><span data-stu-id="371c4-214">In the applications list, select **Evidence.com**.</span></span>

    ![The Evidence.com link in the Applications list](./media/evidence-tutorial/tutorial_evidence.com_app.png)  

1. <span data-ttu-id="371c4-216">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="371c4-216">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="371c4-218">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="371c4-218">Click **Add** button.</span></span> <span data-ttu-id="371c4-219">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="371c4-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="371c4-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="371c4-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="371c4-222">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="371c4-222">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="371c4-223">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="371c4-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="371c4-224">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="371c4-224">Test single sign-on</span></span>

<span data-ttu-id="371c4-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="371c4-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="371c4-226">When you click the Evidence.com tile in the Access Panel, you should get automatically signed-on to your Evidence.com application.</span><span class="sxs-lookup"><span data-stu-id="371c4-226">When you click the Evidence.com tile in the Access Panel, you should get automatically signed-on to your Evidence.com application.</span></span>
<span data-ttu-id="371c4-227">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="371c4-227">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="371c4-228">Additional resources</span><span class="sxs-lookup"><span data-stu-id="371c4-228">Additional resources</span></span>

* [<span data-ttu-id="371c4-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="371c4-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="371c4-230">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="371c4-230">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/evidence-tutorial/tutorial_general_01.png
[2]: ./media/evidence-tutorial/tutorial_general_02.png
[3]: ./media/evidence-tutorial/tutorial_general_03.png
[4]: ./media/evidence-tutorial/tutorial_general_04.png

[100]: ./media/evidence-tutorial/tutorial_general_100.png

[200]: ./media/evidence-tutorial/tutorial_general_200.png
[201]: ./media/evidence-tutorial/tutorial_general_201.png
[202]: ./media/evidence-tutorial/tutorial_general_202.png
[203]: ./media/evidence-tutorial/tutorial_general_203.png

