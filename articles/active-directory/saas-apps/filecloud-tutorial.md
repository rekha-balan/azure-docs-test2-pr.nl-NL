---
title: 'Tutorial: Azure Active Directory integration with FileCloud | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and FileCloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 2263e583-3eb2-4a06-982d-33f5f54858f4
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/27/2017
ms.author: jeedes
ms.openlocfilehash: 86e02fe51d4f461036d378f515746bddeb2d02a3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968911"
---
# <a name="tutorial-azure-active-directory-integration-with-filecloud"></a><span data-ttu-id="859c4-103">Tutorial: Azure Active Directory integration with FileCloud</span><span class="sxs-lookup"><span data-stu-id="859c4-103">Tutorial: Azure Active Directory integration with FileCloud</span></span>

<span data-ttu-id="859c4-104">In this tutorial, you learn how to integrate FileCloud with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="859c4-104">In this tutorial, you learn how to integrate FileCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="859c4-105">Integrating FileCloud with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="859c4-105">Integrating FileCloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="859c4-106">You can control in Azure AD who has access to FileCloud.</span><span class="sxs-lookup"><span data-stu-id="859c4-106">You can control in Azure AD who has access to FileCloud.</span></span>
- <span data-ttu-id="859c4-107">You can enable your users to automatically get signed-on to FileCloud (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="859c4-107">You can enable your users to automatically get signed-on to FileCloud (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="859c4-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="859c4-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="859c4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="859c4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="859c4-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="859c4-110">Prerequisites</span></span>

<span data-ttu-id="859c4-111">To configure Azure AD integration with FileCloud, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="859c4-111">To configure Azure AD integration with FileCloud, you need the following items:</span></span>

- <span data-ttu-id="859c4-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="859c4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="859c4-113">A FileCloud single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="859c4-113">A FileCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="859c4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="859c4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="859c4-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="859c4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="859c4-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="859c4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="859c4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="859c4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="859c4-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="859c4-118">Scenario description</span></span>
<span data-ttu-id="859c4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="859c4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="859c4-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="859c4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="859c4-121">Adding FileCloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="859c4-121">Adding FileCloud from the gallery</span></span>
1. <span data-ttu-id="859c4-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="859c4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-filecloud-from-the-gallery"></a><span data-ttu-id="859c4-123">Adding FileCloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="859c4-123">Adding FileCloud from the gallery</span></span>
<span data-ttu-id="859c4-124">To configure the integration of FileCloud into Azure AD, you need to add FileCloud from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="859c4-124">To configure the integration of FileCloud into Azure AD, you need to add FileCloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="859c4-125">**To add FileCloud from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="859c4-125">**To add FileCloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="859c4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="859c4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="859c4-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="859c4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="859c4-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="859c4-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="859c4-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="859c4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="859c4-133">In the search box, type **FileCloud**, select **FileCloud** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="859c4-133">In the search box, type **FileCloud**, select **FileCloud** from result panel then click **Add** button to add the application.</span></span>

    ![FileCloud in the results list](./media/filecloud-tutorial/tutorial_filecloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="859c4-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="859c4-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="859c4-136">In this section, you configure and test Azure AD single sign-on with FileCloud based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="859c4-136">In this section, you configure and test Azure AD single sign-on with FileCloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="859c4-137">For single sign-on to work, Azure AD needs to know what the counterpart user in FileCloud is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="859c4-137">For single sign-on to work, Azure AD needs to know what the counterpart user in FileCloud is to a user in Azure AD.</span></span> <span data-ttu-id="859c4-138">In other words, a link relationship between an Azure AD user and the related user in FileCloud needs to be established.</span><span class="sxs-lookup"><span data-stu-id="859c4-138">In other words, a link relationship between an Azure AD user and the related user in FileCloud needs to be established.</span></span>

<span data-ttu-id="859c4-139">In FileCloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="859c4-139">In FileCloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="859c4-140">To configure and test Azure AD single sign-on with FileCloud, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="859c4-140">To configure and test Azure AD single sign-on with FileCloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="859c4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="859c4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="859c4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="859c4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="859c4-143">**[Create a FileCloud test user](#create-a-filecloud-test-user)** - to have a counterpart of Britta Simon in FileCloud that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="859c4-143">**[Create a FileCloud test user](#create-a-filecloud-test-user)** - to have a counterpart of Britta Simon in FileCloud that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="859c4-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="859c4-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="859c4-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="859c4-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="859c4-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="859c4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="859c4-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FileCloud application.</span><span class="sxs-lookup"><span data-stu-id="859c4-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FileCloud application.</span></span>

<span data-ttu-id="859c4-148">**To configure Azure AD single sign-on with FileCloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="859c4-148">**To configure Azure AD single sign-on with FileCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="859c4-149">In the Azure portal, on the **FileCloud** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="859c4-149">In the Azure portal, on the **FileCloud** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="859c4-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="859c4-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/filecloud-tutorial/tutorial_filecloud_samlbase.png)

1. <span data-ttu-id="859c4-153">On the **FileCloud Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="859c4-153">On the **FileCloud Domain and URLs** section, perform the following steps:</span></span>

    ![FileCloud Domain and URLs single sign-on information](./media/filecloud-tutorial/tutorial_filecloud_url.png)

    <span data-ttu-id="859c4-155">a.</span><span class="sxs-lookup"><span data-stu-id="859c4-155">a.</span></span> <span data-ttu-id="859c4-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.filecloudonline.com`</span><span class="sxs-lookup"><span data-stu-id="859c4-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.filecloudonline.com`</span></span>

    <span data-ttu-id="859c4-157">b.</span><span class="sxs-lookup"><span data-stu-id="859c4-157">b.</span></span> <span data-ttu-id="859c4-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.filecloudonline.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span><span class="sxs-lookup"><span data-stu-id="859c4-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.filecloudonline.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="859c4-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="859c4-159">These values are not real.</span></span> <span data-ttu-id="859c4-160">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="859c4-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="859c4-161">Contact [FileCloud Client support team](mailto:support@codelathe.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="859c4-161">Contact [FileCloud Client support team](mailto:support@codelathe.com) to get these values.</span></span> 

1. <span data-ttu-id="859c4-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="859c4-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/filecloud-tutorial/tutorial_filecloud_certificate.png) 

1. <span data-ttu-id="859c4-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="859c4-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/filecloud-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="859c4-166">On the **FileCloud Configuration** section, click **Configure FileCloud** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="859c4-166">On the **FileCloud Configuration** section, click **Configure FileCloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="859c4-167">Copy the **SAML Entity ID** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="859c4-167">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![FileCloud Configuration](./media/filecloud-tutorial/tutorial_filecloud_configure.png) 

1. <span data-ttu-id="859c4-169">In a different web browser window, sign-on to your FileCloud tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="859c4-169">In a different web browser window, sign-on to your FileCloud tenant as an administrator.</span></span>

1. <span data-ttu-id="859c4-170">On the left navigation pane, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="859c4-170">On the left navigation pane, click **Settings**.</span></span> 
   
    ![Configure Single Sign-On On App side](./media/filecloud-tutorial/tutorial_filecloud_000.png)

1. <span data-ttu-id="859c4-172">Click **SSO** tab on Settings section.</span><span class="sxs-lookup"><span data-stu-id="859c4-172">Click **SSO** tab on Settings section.</span></span> 
   
    ![Configure Single Sign-On On App side](./media/filecloud-tutorial/tutorial_filecloud_001.png)

1. <span data-ttu-id="859c4-174">Select **SAML** as **Default SSO Type** on **Single Sign On (SSO) Settings** panel.</span><span class="sxs-lookup"><span data-stu-id="859c4-174">Select **SAML** as **Default SSO Type** on **Single Sign On (SSO) Settings** panel.</span></span>
   
    ![Configure Single Sign-On On App side](./media/filecloud-tutorial/tutorial_filecloud_002.png)

1. <span data-ttu-id="859c4-176">In the **IdP End Point URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="859c4-176">In the **IdP End Point URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    ![Configure Single Sign-On On App side](./media/filecloud-tutorial/tutorial_filecloud_003.png)

1. <span data-ttu-id="859c4-178">Open your downloaded metadata file in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Meta Data** textbox on **SAML Settings** panel.</span><span class="sxs-lookup"><span data-stu-id="859c4-178">Open your downloaded metadata file in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Meta Data** textbox on **SAML Settings** panel.</span></span>

    ![Configure Single Sign-On On App side](./media/filecloud-tutorial/tutorial_filecloud_004.png)

1. <span data-ttu-id="859c4-180">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="859c4-180">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="859c4-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="859c4-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="859c4-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="859c4-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="859c4-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="859c4-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="859c4-184">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="859c4-184">Create an Azure AD test user</span></span>

<span data-ttu-id="859c4-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="859c4-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="859c4-187">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="859c4-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="859c4-188">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="859c4-188">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/filecloud-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="859c4-190">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="859c4-190">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/filecloud-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="859c4-192">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="859c4-192">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/filecloud-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="859c4-194">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="859c4-194">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/filecloud-tutorial/create_aaduser_04.png)

    <span data-ttu-id="859c4-196">a.</span><span class="sxs-lookup"><span data-stu-id="859c4-196">a.</span></span> <span data-ttu-id="859c4-197">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="859c4-197">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="859c4-198">b.</span><span class="sxs-lookup"><span data-stu-id="859c4-198">b.</span></span> <span data-ttu-id="859c4-199">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="859c4-199">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="859c4-200">c.</span><span class="sxs-lookup"><span data-stu-id="859c4-200">c.</span></span> <span data-ttu-id="859c4-201">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="859c4-201">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="859c4-202">d.</span><span class="sxs-lookup"><span data-stu-id="859c4-202">d.</span></span> <span data-ttu-id="859c4-203">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="859c4-203">Click **Create**.</span></span>
 
### <a name="create-a-filecloud-test-user"></a><span data-ttu-id="859c4-204">Create a FileCloud test user</span><span class="sxs-lookup"><span data-stu-id="859c4-204">Create a FileCloud test user</span></span>

<span data-ttu-id="859c4-205">The objective of this section is to create a user called Britta Simon in FileCloud.</span><span class="sxs-lookup"><span data-stu-id="859c4-205">The objective of this section is to create a user called Britta Simon in FileCloud.</span></span> <span data-ttu-id="859c4-206">FileCloud supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="859c4-206">FileCloud supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="859c4-207">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="859c4-207">There is no action item for you in this section.</span></span> <span data-ttu-id="859c4-208">A new user is created during an attempt to access FileCloud if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="859c4-208">A new user is created during an attempt to access FileCloud if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="859c4-209">If you need to create a user manually, you need to contact the [FileCloud Client support team](mailto:support@codelathe.com).</span><span class="sxs-lookup"><span data-stu-id="859c4-209">If you need to create a user manually, you need to contact the [FileCloud Client support team](mailto:support@codelathe.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="859c4-210">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="859c4-210">Assign the Azure AD test user</span></span>

<span data-ttu-id="859c4-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FileCloud.</span><span class="sxs-lookup"><span data-stu-id="859c4-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FileCloud.</span></span>

![Assign the user role][200] 

<span data-ttu-id="859c4-213">**To assign Britta Simon to FileCloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="859c4-213">**To assign Britta Simon to FileCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="859c4-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="859c4-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="859c4-216">In the applications list, select **FileCloud**.</span><span class="sxs-lookup"><span data-stu-id="859c4-216">In the applications list, select **FileCloud**.</span></span>

    ![The FileCloud link in the Applications list](./media/filecloud-tutorial/tutorial_filecloud_app.png)  

1. <span data-ttu-id="859c4-218">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="859c4-218">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="859c4-220">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="859c4-220">Click **Add** button.</span></span> <span data-ttu-id="859c4-221">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="859c4-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="859c4-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="859c4-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="859c4-224">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="859c4-224">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="859c4-225">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="859c4-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="859c4-226">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="859c4-226">Test single sign-on</span></span>

<span data-ttu-id="859c4-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="859c4-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="859c4-228">When you click the FileCloud tile in the Access Panel, you should get automatically signed-on to your FileCloud application.</span><span class="sxs-lookup"><span data-stu-id="859c4-228">When you click the FileCloud tile in the Access Panel, you should get automatically signed-on to your FileCloud application.</span></span>
<span data-ttu-id="859c4-229">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="859c4-229">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="859c4-230">Additional resources</span><span class="sxs-lookup"><span data-stu-id="859c4-230">Additional resources</span></span>

* [<span data-ttu-id="859c4-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="859c4-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="859c4-232">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="859c4-232">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/filecloud-tutorial/tutorial_general_01.png
[2]: ./media/filecloud-tutorial/tutorial_general_02.png
[3]: ./media/filecloud-tutorial/tutorial_general_03.png
[4]: ./media/filecloud-tutorial/tutorial_general_04.png

[100]: ./media/filecloud-tutorial/tutorial_general_100.png

[200]: ./media/filecloud-tutorial/tutorial_general_200.png
[201]: ./media/filecloud-tutorial/tutorial_general_201.png
[202]: ./media/filecloud-tutorial/tutorial_general_202.png
[203]: ./media/filecloud-tutorial/tutorial_general_203.png

