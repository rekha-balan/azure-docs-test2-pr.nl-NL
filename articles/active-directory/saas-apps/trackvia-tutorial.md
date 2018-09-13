---
title: 'Tutorial: Azure Active Directory integration with TrackVia | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and TrackVia.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e7010023-bdda-4a19-a335-19904e75b813
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2018
ms.author: jeedes
ms.openlocfilehash: fd17282783f9701f7365a5fb1d37f4a2263134e9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866791"
---
# <a name="tutorial-azure-active-directory-integration-with-trackvia"></a><span data-ttu-id="c2595-103">Tutorial: Azure Active Directory integration with TrackVia</span><span class="sxs-lookup"><span data-stu-id="c2595-103">Tutorial: Azure Active Directory integration with TrackVia</span></span>

<span data-ttu-id="c2595-104">In this tutorial, you learn how to integrate TrackVia with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c2595-104">In this tutorial, you learn how to integrate TrackVia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c2595-105">Integrating TrackVia with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="c2595-105">Integrating TrackVia with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c2595-106">You can control in Azure AD who has access to TrackVia.</span><span class="sxs-lookup"><span data-stu-id="c2595-106">You can control in Azure AD who has access to TrackVia.</span></span>
- <span data-ttu-id="c2595-107">You can enable your users to automatically get signed-on to TrackVia (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="c2595-107">You can enable your users to automatically get signed-on to TrackVia (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c2595-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c2595-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="c2595-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="c2595-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2595-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c2595-110">Prerequisites</span></span>

<span data-ttu-id="c2595-111">To configure Azure AD integration with TrackVia, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="c2595-111">To configure Azure AD integration with TrackVia, you need the following items:</span></span>

- <span data-ttu-id="c2595-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="c2595-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c2595-113">A TrackVia single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="c2595-113">A TrackVia single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c2595-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="c2595-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c2595-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="c2595-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c2595-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="c2595-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c2595-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c2595-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c2595-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="c2595-118">Scenario description</span></span>
<span data-ttu-id="c2595-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="c2595-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c2595-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="c2595-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c2595-121">Adding TrackVia from the gallery</span><span class="sxs-lookup"><span data-stu-id="c2595-121">Adding TrackVia from the gallery</span></span>
1. <span data-ttu-id="c2595-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c2595-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trackvia-from-the-gallery"></a><span data-ttu-id="c2595-123">Adding TrackVia from the gallery</span><span class="sxs-lookup"><span data-stu-id="c2595-123">Adding TrackVia from the gallery</span></span>
<span data-ttu-id="c2595-124">To configure the integration of TrackVia into Azure AD, you need to add TrackVia from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="c2595-124">To configure the integration of TrackVia into Azure AD, you need to add TrackVia from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c2595-125">**To add TrackVia from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c2595-125">**To add TrackVia from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c2595-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="c2595-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="c2595-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="c2595-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c2595-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c2595-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="c2595-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="c2595-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="c2595-133">In the search box, type **TrackVia**, select **TrackVia** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="c2595-133">In the search box, type **TrackVia**, select **TrackVia** from result panel then click **Add** button to add the application.</span></span>

    ![TrackVia in the results list](./media/trackvia-tutorial/tutorial_trackvia_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c2595-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c2595-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c2595-136">In this section, you configure and test Azure AD single sign-on with TrackVia based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c2595-136">In this section, you configure and test Azure AD single sign-on with TrackVia based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c2595-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TrackVia is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c2595-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TrackVia is to a user in Azure AD.</span></span> <span data-ttu-id="c2595-138">In other words, a link relationship between an Azure AD user and the related user in TrackVia needs to be established.</span><span class="sxs-lookup"><span data-stu-id="c2595-138">In other words, a link relationship between an Azure AD user and the related user in TrackVia needs to be established.</span></span>

<span data-ttu-id="c2595-139">In TrackVia, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="c2595-139">In TrackVia, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c2595-140">To configure and test Azure AD single sign-on with TrackVia, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c2595-140">To configure and test Azure AD single sign-on with TrackVia, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c2595-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="c2595-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="c2595-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c2595-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="c2595-143">**[Create a TrackVia test user](#create-a-trackvia-test-user)** - to have a counterpart of Britta Simon in TrackVia that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="c2595-143">**[Create a TrackVia test user](#create-a-trackvia-test-user)** - to have a counterpart of Britta Simon in TrackVia that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="c2595-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c2595-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="c2595-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="c2595-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c2595-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c2595-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c2595-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TrackVia application.</span><span class="sxs-lookup"><span data-stu-id="c2595-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TrackVia application.</span></span>

<span data-ttu-id="c2595-148">**To configure Azure AD single sign-on with TrackVia, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c2595-148">**To configure Azure AD single sign-on with TrackVia, perform the following steps:**</span></span>

1. <span data-ttu-id="c2595-149">In the Azure portal, on the **TrackVia** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c2595-149">In the Azure portal, on the **TrackVia** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="c2595-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c2595-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/trackvia-tutorial/tutorial_trackvia_samlbase.png)

1. <span data-ttu-id="c2595-153">On the **TrackVia Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="c2595-153">On the **TrackVia Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![TrackVia Domain and URLs single sign-on information](./media/trackvia-tutorial/tutorial_trackvia_url.png)

    <span data-ttu-id="c2595-155">In the **Identifier** textbox, type the value: `TrackVia`</span><span class="sxs-lookup"><span data-stu-id="c2595-155">In the **Identifier** textbox, type the value: `TrackVia`</span></span>

1. <span data-ttu-id="c2595-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="c2595-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![TrackVia Domain and URLs single sign-on information](./media/trackvia-tutorial/tutorial_trackvia_url1.png)

    <span data-ttu-id="c2595-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://companyname.trackvia.com`</span><span class="sxs-lookup"><span data-stu-id="c2595-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://companyname.trackvia.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="c2595-159">Sign-on URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="c2595-159">Sign-on URL value is not real.</span></span> <span data-ttu-id="c2595-160">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="c2595-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="c2595-161">Contact [TrackVia Client support team](mailto:support@trackvia.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="c2595-161">Contact [TrackVia Client support team](mailto:support@trackvia.com) to get this value.</span></span>

1. <span data-ttu-id="c2595-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="c2595-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/trackvia-tutorial/tutorial_trackvia_certificate.png) 

1. <span data-ttu-id="c2595-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="c2595-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/trackvia-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="c2595-166">On the **TrackVia Configuration** section, click **Configure TrackVia** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="c2595-166">On the **TrackVia Configuration** section, click **Configure TrackVia** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c2595-167">Copy the **SAML Entity ID** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="c2595-167">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![TrackVia configuration](./media/trackvia-tutorial/tutorial_trackvia_configure.png)
    
1. <span data-ttu-id="c2595-169">In different browser window, sign on to your TrackVia company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="c2595-169">In different browser window, sign on to your TrackVia company site as an administrator.</span></span>

1. <span data-ttu-id="c2595-170">Click on Trackvia **My Account** settings and then select **Single Sign On** tab, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c2595-170">Click on Trackvia **My Account** settings and then select **Single Sign On** tab, perform the following steps:</span></span>

    ![TrackVia configuration](./media/trackvia-tutorial/configure1.png)

    <span data-ttu-id="c2595-172">a.</span><span class="sxs-lookup"><span data-stu-id="c2595-172">a.</span></span> <span data-ttu-id="c2595-173">In the **Identity Provider Entity ID** textbox, paste **SAML Entity ID** value, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c2595-173">In the **Identity Provider Entity ID** textbox, paste **SAML Entity ID** value, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="c2595-174">b.</span><span class="sxs-lookup"><span data-stu-id="c2595-174">b.</span></span> <span data-ttu-id="c2595-175">Select the **Choose File** to upload the metadata file that you downloaded from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c2595-175">Select the **Choose File** to upload the metadata file that you downloaded from the Azure portal.</span></span>

    <span data-ttu-id="c2595-176">c.</span><span class="sxs-lookup"><span data-stu-id="c2595-176">c.</span></span> <span data-ttu-id="c2595-177">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="c2595-177">Click **Save**</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c2595-178">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c2595-178">Create an Azure AD test user</span></span>

<span data-ttu-id="c2595-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c2595-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="c2595-181">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c2595-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c2595-182">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="c2595-182">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/trackvia-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="c2595-184">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="c2595-184">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/trackvia-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="c2595-186">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="c2595-186">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/trackvia-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="c2595-188">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c2595-188">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/trackvia-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c2595-190">a.</span><span class="sxs-lookup"><span data-stu-id="c2595-190">a.</span></span> <span data-ttu-id="c2595-191">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c2595-191">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c2595-192">b.</span><span class="sxs-lookup"><span data-stu-id="c2595-192">b.</span></span> <span data-ttu-id="c2595-193">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c2595-193">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="c2595-194">c.</span><span class="sxs-lookup"><span data-stu-id="c2595-194">c.</span></span> <span data-ttu-id="c2595-195">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="c2595-195">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="c2595-196">d.</span><span class="sxs-lookup"><span data-stu-id="c2595-196">d.</span></span> <span data-ttu-id="c2595-197">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c2595-197">Click **Create**.</span></span>
 
### <a name="create-a-trackvia-test-user"></a><span data-ttu-id="c2595-198">Create a TrackVia test user</span><span class="sxs-lookup"><span data-stu-id="c2595-198">Create a TrackVia test user</span></span>

<span data-ttu-id="c2595-199">The objective of this section is to create a user called Britta Simon in TrackVia.</span><span class="sxs-lookup"><span data-stu-id="c2595-199">The objective of this section is to create a user called Britta Simon in TrackVia.</span></span> <span data-ttu-id="c2595-200">TrackVia supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="c2595-200">TrackVia supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="c2595-201">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="c2595-201">There is no action item for you in this section.</span></span> <span data-ttu-id="c2595-202">A new user is created during an attempt to access TrackVia if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="c2595-202">A new user is created during an attempt to access TrackVia if it doesn't exist yet.</span></span>
>[!Note]
><span data-ttu-id="c2595-203">If you need to create a user manually, contact [TrackVia support team](mailto:support@trackvia.com).</span><span class="sxs-lookup"><span data-stu-id="c2595-203">If you need to create a user manually, contact [TrackVia support team](mailto:support@trackvia.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c2595-204">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c2595-204">Assign the Azure AD test user</span></span>

<span data-ttu-id="c2595-205">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TrackVia.</span><span class="sxs-lookup"><span data-stu-id="c2595-205">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TrackVia.</span></span>

![Assign the user role][200] 

<span data-ttu-id="c2595-207">**To assign Britta Simon to TrackVia, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c2595-207">**To assign Britta Simon to TrackVia, perform the following steps:**</span></span>

1. <span data-ttu-id="c2595-208">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c2595-208">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="c2595-210">In the applications list, select **TrackVia**.</span><span class="sxs-lookup"><span data-stu-id="c2595-210">In the applications list, select **TrackVia**.</span></span>

    ![The TrackVia link in the Applications list](./media/trackvia-tutorial/tutorial_trackvia_app.png)  

1. <span data-ttu-id="c2595-212">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="c2595-212">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="c2595-214">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="c2595-214">Click **Add** button.</span></span> <span data-ttu-id="c2595-215">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c2595-215">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="c2595-217">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="c2595-217">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="c2595-218">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="c2595-218">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="c2595-219">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c2595-219">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c2595-220">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="c2595-220">Test single sign-on</span></span>

<span data-ttu-id="c2595-221">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c2595-221">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c2595-222">When you click the TrackVia tile in the Access Panel, you should get automatically signed-on to your TrackVia application.</span><span class="sxs-lookup"><span data-stu-id="c2595-222">When you click the TrackVia tile in the Access Panel, you should get automatically signed-on to your TrackVia application.</span></span>
<span data-ttu-id="c2595-223">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c2595-223">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c2595-224">Additional resources</span><span class="sxs-lookup"><span data-stu-id="c2595-224">Additional resources</span></span>

* [<span data-ttu-id="c2595-225">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2595-225">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="c2595-226">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c2595-226">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/trackvia-tutorial/tutorial_general_01.png
[2]: ./media/trackvia-tutorial/tutorial_general_02.png
[3]: ./media/trackvia-tutorial/tutorial_general_03.png
[4]: ./media/trackvia-tutorial/tutorial_general_04.png

[100]: ./media/trackvia-tutorial/tutorial_general_100.png

[200]: ./media/trackvia-tutorial/tutorial_general_200.png
[201]: ./media/trackvia-tutorial/tutorial_general_201.png
[202]: ./media/trackvia-tutorial/tutorial_general_202.png
[203]: ./media/trackvia-tutorial/tutorial_general_203.png
