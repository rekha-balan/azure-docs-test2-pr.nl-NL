---
title: 'Tutorial: Azure Active Directory integration with Citrix ShareFile | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Citrix ShareFile.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2018
ms.author: jeedes
ms.openlocfilehash: 9919be128ae651b589a37f957cc59ce6d171143f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968963"
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="d0c68-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="d0c68-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="d0c68-104">In this tutorial, you learn how to integrate Citrix ShareFile with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d0c68-104">In this tutorial, you learn how to integrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d0c68-105">Integrating Citrix ShareFile with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d0c68-105">Integrating Citrix ShareFile with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d0c68-106">You can control in Azure AD who has access to Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="d0c68-106">You can control in Azure AD who has access to Citrix ShareFile.</span></span>
- <span data-ttu-id="d0c68-107">You can enable your users to automatically get signed-on to Citrix ShareFile (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="d0c68-107">You can enable your users to automatically get signed-on to Citrix ShareFile (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d0c68-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d0c68-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="d0c68-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="d0c68-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0c68-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d0c68-110">Prerequisites</span></span>

<span data-ttu-id="d0c68-111">To configure Azure AD integration with Citrix ShareFile, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d0c68-111">To configure Azure AD integration with Citrix ShareFile, you need the following items:</span></span>

- <span data-ttu-id="d0c68-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d0c68-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d0c68-113">A Citrix ShareFile single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d0c68-113">A Citrix ShareFile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d0c68-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d0c68-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d0c68-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d0c68-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d0c68-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="d0c68-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d0c68-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0c68-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d0c68-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="d0c68-118">Scenario description</span></span>
<span data-ttu-id="d0c68-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d0c68-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d0c68-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d0c68-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d0c68-121">Add Citrix ShareFile from the gallery</span><span class="sxs-lookup"><span data-stu-id="d0c68-121">Add Citrix ShareFile from the gallery</span></span>
1. <span data-ttu-id="d0c68-122">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d0c68-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-citrix-sharefile-from-the-gallery"></a><span data-ttu-id="d0c68-123">Add Citrix ShareFile from the gallery</span><span class="sxs-lookup"><span data-stu-id="d0c68-123">Add Citrix ShareFile from the gallery</span></span>
<span data-ttu-id="d0c68-124">To configure the integration of Citrix ShareFile into Azure AD, you need to add Citrix ShareFile from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d0c68-124">To configure the integration of Citrix ShareFile into Azure AD, you need to add Citrix ShareFile from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d0c68-125">**To add Citrix ShareFile from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d0c68-125">**To add Citrix ShareFile from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d0c68-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d0c68-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="d0c68-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="d0c68-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d0c68-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d0c68-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="d0c68-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="d0c68-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="d0c68-133">In the search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="d0c68-133">In the search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button to add the application.</span></span>

    ![Citrix ShareFile in the results list](./media/sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d0c68-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d0c68-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d0c68-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d0c68-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d0c68-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix ShareFile is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0c68-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix ShareFile is to a user in Azure AD.</span></span> <span data-ttu-id="d0c68-138">In other words, a link relationship between an Azure AD user and the related user in Citrix ShareFile needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d0c68-138">In other words, a link relationship between an Azure AD user and the related user in Citrix ShareFile needs to be established.</span></span>

<span data-ttu-id="d0c68-139">In Citrix ShareFile, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="d0c68-139">In Citrix ShareFile, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d0c68-140">To configure and test Azure AD single sign-on with Citrix ShareFile, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d0c68-140">To configure and test Azure AD single sign-on with Citrix ShareFile, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d0c68-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d0c68-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="d0c68-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d0c68-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="d0c68-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - to have a counterpart of Britta Simon in Citrix ShareFile that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="d0c68-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - to have a counterpart of Britta Simon in Citrix ShareFile that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="d0c68-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d0c68-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="d0c68-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d0c68-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d0c68-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d0c68-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d0c68-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Citrix ShareFile application.</span><span class="sxs-lookup"><span data-stu-id="d0c68-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="d0c68-148">**To configure Azure AD single sign-on with Citrix ShareFile, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d0c68-148">**To configure Azure AD single sign-on with Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="d0c68-149">In the Azure portal, on the **Citrix ShareFile** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d0c68-149">In the Azure portal, on the **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="d0c68-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d0c68-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/sharefile-tutorial/tutorial_sharefile_samlbase.png)

1. <span data-ttu-id="d0c68-153">On the **Citrix ShareFile Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d0c68-153">On the **Citrix ShareFile Domain and URLs** section, perform the following steps:</span></span>

    ![Citrix ShareFile Domain and URLs single sign-on information](./media/sharefile-tutorial/tutorial_sharefile_url.png)
    
    <span data-ttu-id="d0c68-155">a.</span><span class="sxs-lookup"><span data-stu-id="d0c68-155">a.</span></span> <span data-ttu-id="d0c68-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span><span class="sxs-lookup"><span data-stu-id="d0c68-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span>

    <span data-ttu-id="d0c68-157">b.</span><span class="sxs-lookup"><span data-stu-id="d0c68-157">b.</span></span> <span data-ttu-id="d0c68-158">In the **Identifier (Entity ID)** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="d0c68-158">In the **Identifier (Entity ID)** textbox, type a URL using the following pattern:</span></span>

    | |
    |---|
    | `https://<tenant-name>.sharefile.com`|
    | `https://<tenant-name>.sharefile.com/saml/info`|
    | `https://<tenant-name>.sharefile1.com/saml/info`|
    | `https://<tenant-name>.sharefile1.eu/saml/info`|
    | `https://<tenant-name>.sharefile.eu/saml/info`|
    | |
    
    <span data-ttu-id="d0c68-159">c.</span><span class="sxs-lookup"><span data-stu-id="d0c68-159">c.</span></span> <span data-ttu-id="d0c68-160">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="d0c68-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |---|
    | `https://<tenant-name>.sharefile.com/saml/acs`|
    | `https://<tenant-name>.sharefile.eu/saml/<URL path>`|
    | `https://<tenant-name>.sharefile.com/saml/<URL path>`|
    | |

    > [!NOTE]
    > <span data-ttu-id="d0c68-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="d0c68-161">These values are not real.</span></span> <span data-ttu-id="d0c68-162">Update these values with the actual Sign-On URL, Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="d0c68-162">Update these values with the actual Sign-On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="d0c68-163">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) to get these values.</span><span class="sxs-lookup"><span data-stu-id="d0c68-163">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) to get these values.</span></span>

1. <span data-ttu-id="d0c68-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d0c68-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/sharefile-tutorial/tutorial_sharefile_certificate.png)

1. <span data-ttu-id="d0c68-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="d0c68-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/sharefile-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="d0c68-168">On the **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="d0c68-168">On the **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d0c68-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="d0c68-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Citrix ShareFile Configuration](./media/sharefile-tutorial/tutorial_sharefile_configure.png)

1. <span data-ttu-id="d0c68-171">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="d0c68-171">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>

1. <span data-ttu-id="d0c68-172">In the toolbar on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="d0c68-172">In the toolbar on the top, click **Admin**.</span></span>

1. <span data-ttu-id="d0c68-173">In the left navigation pane, select **Configure Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="d0c68-173">In the left navigation pane, select **Configure Single Sign-On**.</span></span>
   
    <span data-ttu-id="d0c68-174">![Account Administration](./media/sharefile-tutorial/ic773627.png "Account Administration")</span><span class="sxs-lookup"><span data-stu-id="d0c68-174">![Account Administration](./media/sharefile-tutorial/ic773627.png "Account Administration")</span></span>

1. <span data-ttu-id="d0c68-175">On the **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d0c68-175">On the **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform the following steps:</span></span>
   
    <span data-ttu-id="d0c68-176">![Single sign-on](./media/sharefile-tutorial/ic773628.png "Single sign-on")</span><span class="sxs-lookup"><span data-stu-id="d0c68-176">![Single sign-on](./media/sharefile-tutorial/ic773628.png "Single sign-on")</span></span>
   
    <span data-ttu-id="d0c68-177">a.</span><span class="sxs-lookup"><span data-stu-id="d0c68-177">a.</span></span> <span data-ttu-id="d0c68-178">Click **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="d0c68-178">Click **Enable SAML**.</span></span>
    
    <span data-ttu-id="d0c68-179">b.</span><span class="sxs-lookup"><span data-stu-id="d0c68-179">b.</span></span> <span data-ttu-id="d0c68-180">In **Your IDP Issuer/ Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d0c68-180">In **Your IDP Issuer/ Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d0c68-181">c.</span><span class="sxs-lookup"><span data-stu-id="d0c68-181">c.</span></span> <span data-ttu-id="d0c68-182">Click **Change** next to the **X.509 Certificate** field and then upload the certificate you downloaded from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d0c68-182">Click **Change** next to the **X.509 Certificate** field and then upload the certificate you downloaded from the Azure portal.</span></span>
    
    <span data-ttu-id="d0c68-183">d.</span><span class="sxs-lookup"><span data-stu-id="d0c68-183">d.</span></span> <span data-ttu-id="d0c68-184">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d0c68-184">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="d0c68-185">e.</span><span class="sxs-lookup"><span data-stu-id="d0c68-185">e.</span></span> <span data-ttu-id="d0c68-186">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d0c68-186">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

1. <span data-ttu-id="d0c68-187">Click **Save** on the Citrix ShareFile management portal.</span><span class="sxs-lookup"><span data-stu-id="d0c68-187">Click **Save** on the Citrix ShareFile management portal.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d0c68-188">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d0c68-188">Create an Azure AD test user</span></span>

<span data-ttu-id="d0c68-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d0c68-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="d0c68-191">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d0c68-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d0c68-192">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="d0c68-192">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/sharefile-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="d0c68-194">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="d0c68-194">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/sharefile-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="d0c68-196">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="d0c68-196">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/sharefile-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="d0c68-198">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d0c68-198">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/sharefile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d0c68-200">a.</span><span class="sxs-lookup"><span data-stu-id="d0c68-200">a.</span></span> <span data-ttu-id="d0c68-201">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d0c68-201">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d0c68-202">b.</span><span class="sxs-lookup"><span data-stu-id="d0c68-202">b.</span></span> <span data-ttu-id="d0c68-203">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d0c68-203">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="d0c68-204">c.</span><span class="sxs-lookup"><span data-stu-id="d0c68-204">c.</span></span> <span data-ttu-id="d0c68-205">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="d0c68-205">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="d0c68-206">d.</span><span class="sxs-lookup"><span data-stu-id="d0c68-206">d.</span></span> <span data-ttu-id="d0c68-207">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d0c68-207">Click **Create**.</span></span>
 
### <a name="create-a-citrix-sharefile-test-user"></a><span data-ttu-id="d0c68-208">Create a Citrix ShareFile test user</span><span class="sxs-lookup"><span data-stu-id="d0c68-208">Create a Citrix ShareFile test user</span></span>

<span data-ttu-id="d0c68-209">In order to enable Azure AD users to log into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="d0c68-209">In order to enable Azure AD users to log into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="d0c68-210">In the case of Citrix ShareFile, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="d0c68-210">In the case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="d0c68-211">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d0c68-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="d0c68-212">Log in to your **Citrix ShareFile** tenant.</span><span class="sxs-lookup"><span data-stu-id="d0c68-212">Log in to your **Citrix ShareFile** tenant.</span></span>

1. <span data-ttu-id="d0c68-213">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span><span class="sxs-lookup"><span data-stu-id="d0c68-213">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="d0c68-214">![Create Employee](./media/sharefile-tutorial/IC781050.png "Create Employee")</span><span class="sxs-lookup"><span data-stu-id="d0c68-214">![Create Employee](./media/sharefile-tutorial/IC781050.png "Create Employee")</span></span>

1. <span data-ttu-id="d0c68-215">On the **Basic Information** section, perform below steps:</span><span class="sxs-lookup"><span data-stu-id="d0c68-215">On the **Basic Information** section, perform below steps:</span></span>
   
   <span data-ttu-id="d0c68-216">![Basic Information](./media/sharefile-tutorial/IC799951.png "Basic Information")</span><span class="sxs-lookup"><span data-stu-id="d0c68-216">![Basic Information](./media/sharefile-tutorial/IC799951.png "Basic Information")</span></span>
   
   <span data-ttu-id="d0c68-217">a.</span><span class="sxs-lookup"><span data-stu-id="d0c68-217">a.</span></span> <span data-ttu-id="d0c68-218">In the **Email Address** textbox, type the email address of Britta Simon as **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="d0c68-218">In the **Email Address** textbox, type the email address of Britta Simon as **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="d0c68-219">b.</span><span class="sxs-lookup"><span data-stu-id="d0c68-219">b.</span></span> <span data-ttu-id="d0c68-220">In the **First Name** textbox, type **first name** of user as **Britta**.</span><span class="sxs-lookup"><span data-stu-id="d0c68-220">In the **First Name** textbox, type **first name** of user as **Britta**.</span></span>
   
   <span data-ttu-id="d0c68-221">c.</span><span class="sxs-lookup"><span data-stu-id="d0c68-221">c.</span></span> <span data-ttu-id="d0c68-222">In the **Last Name** textbox, type **last name** of user as **Simon**.</span><span class="sxs-lookup"><span data-stu-id="d0c68-222">In the **Last Name** textbox, type **last name** of user as **Simon**.</span></span>

1. <span data-ttu-id="d0c68-223">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="d0c68-223">Click **Add User**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="d0c68-224">The Azure AD account holder will receive an email and follow a link to confirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="d0c68-224">The Azure AD account holder will receive an email and follow a link to confirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d0c68-225">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d0c68-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="d0c68-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="d0c68-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Citrix ShareFile.</span></span>

![Assign the user role][200] 

<span data-ttu-id="d0c68-228">**To assign Britta Simon to Citrix ShareFile, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d0c68-228">**To assign Britta Simon to Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="d0c68-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d0c68-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="d0c68-231">In the applications list, select **Citrix ShareFile**.</span><span class="sxs-lookup"><span data-stu-id="d0c68-231">In the applications list, select **Citrix ShareFile**.</span></span>

    ![The Citrix ShareFile link in the Applications list](./media/sharefile-tutorial/tutorial_sharefile_app.png)  

1. <span data-ttu-id="d0c68-233">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="d0c68-233">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="d0c68-235">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="d0c68-235">Click **Add** button.</span></span> <span data-ttu-id="d0c68-236">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d0c68-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="d0c68-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="d0c68-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="d0c68-239">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="d0c68-239">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="d0c68-240">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d0c68-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d0c68-241">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="d0c68-241">Test single sign-on</span></span>

<span data-ttu-id="d0c68-242">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d0c68-242">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d0c68-243">When you click the Citrix ShareFile tile in the Access Panel, you should get automatically signed-on to your Citrix ShareFile application.</span><span class="sxs-lookup"><span data-stu-id="d0c68-243">When you click the Citrix ShareFile tile in the Access Panel, you should get automatically signed-on to your Citrix ShareFile application.</span></span>
<span data-ttu-id="d0c68-244">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d0c68-244">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d0c68-245">Additional resources</span><span class="sxs-lookup"><span data-stu-id="d0c68-245">Additional resources</span></span>

* [<span data-ttu-id="d0c68-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0c68-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="d0c68-247">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d0c68-247">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/sharefile-tutorial/tutorial_general_01.png
[2]: ./media/sharefile-tutorial/tutorial_general_02.png
[3]: ./media/sharefile-tutorial/tutorial_general_03.png
[4]: ./media/sharefile-tutorial/tutorial_general_04.png

[100]: ./media/sharefile-tutorial/tutorial_general_100.png

[200]: ./media/sharefile-tutorial/tutorial_general_200.png
[201]: ./media/sharefile-tutorial/tutorial_general_201.png
[202]: ./media/sharefile-tutorial/tutorial_general_202.png
[203]: ./media/sharefile-tutorial/tutorial_general_203.png
