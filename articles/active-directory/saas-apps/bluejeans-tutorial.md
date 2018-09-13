---
title: 'Tutorial: Azure Active Directory integration with BlueJeans | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and BlueJeans.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2018
ms.author: jeedes
ms.openlocfilehash: 2ec94217a8df2efaa23eb3cc2c9d5a80e8037615
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966913"
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a><span data-ttu-id="0cca3-103">Tutorial: Azure Active Directory integration with BlueJeans</span><span class="sxs-lookup"><span data-stu-id="0cca3-103">Tutorial: Azure Active Directory integration with BlueJeans</span></span>

<span data-ttu-id="0cca3-104">In this tutorial, you learn how to integrate BlueJeans with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0cca3-104">In this tutorial, you learn how to integrate BlueJeans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0cca3-105">Integrating BlueJeans with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="0cca3-105">Integrating BlueJeans with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0cca3-106">You can control in Azure AD who has access to BlueJeans</span><span class="sxs-lookup"><span data-stu-id="0cca3-106">You can control in Azure AD who has access to BlueJeans</span></span>
- <span data-ttu-id="0cca3-107">You can enable your users to automatically get signed-on to BlueJeans (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="0cca3-107">You can enable your users to automatically get signed-on to BlueJeans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0cca3-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="0cca3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0cca3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="0cca3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0cca3-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0cca3-110">Prerequisites</span></span>

<span data-ttu-id="0cca3-111">To configure Azure AD integration with BlueJeans, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="0cca3-111">To configure Azure AD integration with BlueJeans, you need the following items:</span></span>

- <span data-ttu-id="0cca3-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="0cca3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0cca3-113">A BlueJeans single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="0cca3-113">A BlueJeans single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0cca3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="0cca3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0cca3-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="0cca3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0cca3-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="0cca3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0cca3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0cca3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0cca3-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="0cca3-118">Scenario description</span></span>
<span data-ttu-id="0cca3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="0cca3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0cca3-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="0cca3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0cca3-121">Adding BlueJeans from the gallery</span><span class="sxs-lookup"><span data-stu-id="0cca3-121">Adding BlueJeans from the gallery</span></span>
1. <span data-ttu-id="0cca3-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0cca3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bluejeans-from-the-gallery"></a><span data-ttu-id="0cca3-123">Adding BlueJeans from the gallery</span><span class="sxs-lookup"><span data-stu-id="0cca3-123">Adding BlueJeans from the gallery</span></span>
<span data-ttu-id="0cca3-124">To configure the integration of BlueJeans into Azure AD, you need to add BlueJeans from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="0cca3-124">To configure the integration of BlueJeans into Azure AD, you need to add BlueJeans from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0cca3-125">**To add BlueJeans from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0cca3-125">**To add BlueJeans from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0cca3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="0cca3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span>

    ![Active Directory][1]

1. <span data-ttu-id="0cca3-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="0cca3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0cca3-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0cca3-129">Then go to **All applications**.</span></span>

    ![Applications][2]

1. <span data-ttu-id="0cca3-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="0cca3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="0cca3-133">In the search box, type **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="0cca3-133">In the search box, type **BlueJeans**.</span></span>

    ![Creating an Azure AD test user](./media/bluejeans-tutorial/tutorial_bluejeans_search.png)

1. <span data-ttu-id="0cca3-135">In the results panel, select **BlueJeans**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="0cca3-135">In the results panel, select **BlueJeans**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0cca3-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0cca3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0cca3-138">In this section, you configure and test Azure AD single sign-on with BlueJeans based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="0cca3-138">In this section, you configure and test Azure AD single sign-on with BlueJeans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0cca3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BlueJeans is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0cca3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BlueJeans is to a user in Azure AD.</span></span> <span data-ttu-id="0cca3-140">In other words, a link relationship between an Azure AD user and the related user in BlueJeans needs to be established.</span><span class="sxs-lookup"><span data-stu-id="0cca3-140">In other words, a link relationship between an Azure AD user and the related user in BlueJeans needs to be established.</span></span>

<span data-ttu-id="0cca3-141">In BlueJeans, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="0cca3-141">In BlueJeans, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0cca3-142">To configure and test Azure AD single sign-on with BlueJeans, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="0cca3-142">To configure and test Azure AD single sign-on with BlueJeans, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0cca3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="0cca3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="0cca3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0cca3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="0cca3-145">**[Creating a BlueJeans test user](#creating-a-bluejeans-test-user)** - to have a counterpart of Britta Simon in BlueJeans that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="0cca3-145">**[Creating a BlueJeans test user](#creating-a-bluejeans-test-user)** - to have a counterpart of Britta Simon in BlueJeans that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="0cca3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0cca3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="0cca3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="0cca3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0cca3-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0cca3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0cca3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BlueJeans application.</span><span class="sxs-lookup"><span data-stu-id="0cca3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BlueJeans application.</span></span>

<span data-ttu-id="0cca3-150">**To configure Azure AD single sign-on with BlueJeans, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0cca3-150">**To configure Azure AD single sign-on with BlueJeans, perform the following steps:**</span></span>

1. <span data-ttu-id="0cca3-151">In the Azure portal, on the **BlueJeans** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="0cca3-151">In the Azure portal, on the **BlueJeans** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="0cca3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0cca3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configure Single Sign-On](./media/bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

1. <span data-ttu-id="0cca3-155">On the **BlueJeans Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0cca3-155">On the **BlueJeans Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/bluejeans-tutorial/tutorial_bluejeans_url.png)

    <span data-ttu-id="0cca3-157">a.</span><span class="sxs-lookup"><span data-stu-id="0cca3-157">a.</span></span> <span data-ttu-id="0cca3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="0cca3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    <span data-ttu-id="0cca3-159">b.</span><span class="sxs-lookup"><span data-stu-id="0cca3-159">b.</span></span> <span data-ttu-id="0cca3-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.BlueJeans.com`</span><span class="sxs-lookup"><span data-stu-id="0cca3-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.BlueJeans.com`</span></span>

    > [!NOTE]
    > <span data-ttu-id="0cca3-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="0cca3-161">These values are not real.</span></span> <span data-ttu-id="0cca3-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="0cca3-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0cca3-163">Contact [BlueJeans Client support team](https://support.bluejeans.com/contact) to get these values.</span><span class="sxs-lookup"><span data-stu-id="0cca3-163">Contact [BlueJeans Client support team](https://support.bluejeans.com/contact) to get these values.</span></span>

1. <span data-ttu-id="0cca3-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="0cca3-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

1. <span data-ttu-id="0cca3-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="0cca3-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/bluejeans-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="0cca3-168">On the **BlueJeans Configuration** section, click **Configure BlueJeans** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="0cca3-168">On the **BlueJeans Configuration** section, click **Configure BlueJeans** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0cca3-169">Copy the **Sign-Out URL, Change Password URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="0cca3-169">Copy the **Sign-Out URL, Change Password URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/bluejeans-tutorial/tutorial_bluejeans_configure.png) 

1. <span data-ttu-id="0cca3-171">In a different web browser window, log in to your **BlueJeans** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="0cca3-171">In a different web browser window, log in to your **BlueJeans** company site as an administrator.</span></span>

1. <span data-ttu-id="0cca3-172">Go to **ADMIN \> Group Settings \> Security**.</span><span class="sxs-lookup"><span data-stu-id="0cca3-172">Go to **ADMIN \> Group Settings \> Security**.</span></span>

   <span data-ttu-id="0cca3-173">![Admin](./media/bluejeans-tutorial/IC785868.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="0cca3-173">![Admin](./media/bluejeans-tutorial/IC785868.png "Admin")</span></span>

1. <span data-ttu-id="0cca3-174">In the **Security** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0cca3-174">In the **Security** section, perform the following steps:</span></span>

   <span data-ttu-id="0cca3-175">![SAML Single Sign On](./media/bluejeans-tutorial/IC785869.png "SAML Single Sign On")</span><span class="sxs-lookup"><span data-stu-id="0cca3-175">![SAML Single Sign On](./media/bluejeans-tutorial/IC785869.png "SAML Single Sign On")</span></span>

   <span data-ttu-id="0cca3-176">a.</span><span class="sxs-lookup"><span data-stu-id="0cca3-176">a.</span></span> <span data-ttu-id="0cca3-177">Select **SAML Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="0cca3-177">Select **SAML Single Sign On**.</span></span>

   <span data-ttu-id="0cca3-178">b.</span><span class="sxs-lookup"><span data-stu-id="0cca3-178">b.</span></span> <span data-ttu-id="0cca3-179">Select **Enable automatic provisioning**.</span><span class="sxs-lookup"><span data-stu-id="0cca3-179">Select **Enable automatic provisioning**.</span></span>

1. <span data-ttu-id="0cca3-180">Move on with the following steps:</span><span class="sxs-lookup"><span data-stu-id="0cca3-180">Move on with the following steps:</span></span>

    <span data-ttu-id="0cca3-181">![Certificate Path](./media/bluejeans-tutorial/IC785870.png "Certificate Path")</span><span class="sxs-lookup"><span data-stu-id="0cca3-181">![Certificate Path](./media/bluejeans-tutorial/IC785870.png "Certificate Path")</span></span>

    <span data-ttu-id="0cca3-182">a.</span><span class="sxs-lookup"><span data-stu-id="0cca3-182">a.</span></span> <span data-ttu-id="0cca3-183">Click **Choose File**, and then upload the downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="0cca3-183">Click **Choose File**, and then upload the downloaded certificate.</span></span>

    <span data-ttu-id="0cca3-184">b.</span><span class="sxs-lookup"><span data-stu-id="0cca3-184">b.</span></span> <span data-ttu-id="0cca3-185">Paste **SAML Single Sign-On Service URL** into the **Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="0cca3-185">Paste **SAML Single Sign-On Service URL** into the **Login URL** textbox.</span></span>

    <span data-ttu-id="0cca3-186">c.</span><span class="sxs-lookup"><span data-stu-id="0cca3-186">c.</span></span> <span data-ttu-id="0cca3-187">Paste **Change Password URL** into the **Password Change URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="0cca3-187">Paste **Change Password URL** into the **Password Change URL** textbox.</span></span>

    <span data-ttu-id="0cca3-188">d.</span><span class="sxs-lookup"><span data-stu-id="0cca3-188">d.</span></span> <span data-ttu-id="0cca3-189">Paste **Sign-Out URL** into the **Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="0cca3-189">Paste **Sign-Out URL** into the **Logout URL** textbox.</span></span>

1. <span data-ttu-id="0cca3-190">Move on with the following steps:</span><span class="sxs-lookup"><span data-stu-id="0cca3-190">Move on with the following steps:</span></span>

    <span data-ttu-id="0cca3-191">![Save Changes](./media/bluejeans-tutorial/IC785874.png "Save Changes")</span><span class="sxs-lookup"><span data-stu-id="0cca3-191">![Save Changes](./media/bluejeans-tutorial/IC785874.png "Save Changes")</span></span>

    <span data-ttu-id="0cca3-192">a.</span><span class="sxs-lookup"><span data-stu-id="0cca3-192">a.</span></span> <span data-ttu-id="0cca3-193">In the **User id** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="0cca3-193">In the **User id** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="0cca3-194">b.</span><span class="sxs-lookup"><span data-stu-id="0cca3-194">b.</span></span> <span data-ttu-id="0cca3-195">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="0cca3-195">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="0cca3-196">c.</span><span class="sxs-lookup"><span data-stu-id="0cca3-196">c.</span></span> <span data-ttu-id="0cca3-197">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="0cca3-197">Click **Save Changes**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0cca3-198">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0cca3-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="0cca3-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0cca3-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="0cca3-201">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0cca3-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0cca3-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="0cca3-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/bluejeans-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="0cca3-204">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="0cca3-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>

    ![Creating an Azure AD test user](./media/bluejeans-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="0cca3-206">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="0cca3-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>

    ![Creating an Azure AD test user](./media/bluejeans-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="0cca3-208">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0cca3-208">On the **User** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](./media/bluejeans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0cca3-210">a.</span><span class="sxs-lookup"><span data-stu-id="0cca3-210">a.</span></span> <span data-ttu-id="0cca3-211">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0cca3-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0cca3-212">b.</span><span class="sxs-lookup"><span data-stu-id="0cca3-212">b.</span></span> <span data-ttu-id="0cca3-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0cca3-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0cca3-214">c.</span><span class="sxs-lookup"><span data-stu-id="0cca3-214">c.</span></span> <span data-ttu-id="0cca3-215">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="0cca3-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0cca3-216">d.</span><span class="sxs-lookup"><span data-stu-id="0cca3-216">d.</span></span> <span data-ttu-id="0cca3-217">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0cca3-217">Click **Create**.</span></span>

### <a name="creating-a-bluejeans-test-user"></a><span data-ttu-id="0cca3-218">Creating a BlueJeans test user</span><span class="sxs-lookup"><span data-stu-id="0cca3-218">Creating a BlueJeans test user</span></span>

<span data-ttu-id="0cca3-219">The objective of this section is to create a user called Britta Simon in BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="0cca3-219">The objective of this section is to create a user called Britta Simon in BlueJeans.</span></span> <span data-ttu-id="0cca3-220">BlueJeans supports automatic user provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="0cca3-220">BlueJeans supports automatic user provisioning, which is by default enabled.</span></span> <span data-ttu-id="0cca3-221">You can find more details [here](bluejeans-provisioning-tutorial.md) on how to configure automatic user provisioning.</span><span class="sxs-lookup"><span data-stu-id="0cca3-221">You can find more details [here](bluejeans-provisioning-tutorial.md) on how to configure automatic user provisioning.</span></span>

<span data-ttu-id="0cca3-222">**If you need to create user manually, perform following steps:**</span><span class="sxs-lookup"><span data-stu-id="0cca3-222">**If you need to create user manually, perform following steps:**</span></span>

1. <span data-ttu-id="0cca3-223">Log in to your **BlueJeans** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="0cca3-223">Log in to your **BlueJeans** company site as an administrator.</span></span>

1. <span data-ttu-id="0cca3-224">Go to **ADMIN \> Manage Users \> Add User**.</span><span class="sxs-lookup"><span data-stu-id="0cca3-224">Go to **ADMIN \> Manage Users \> Add User**.</span></span>

   <span data-ttu-id="0cca3-225">![Admin](./media/bluejeans-tutorial/IC785877.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="0cca3-225">![Admin](./media/bluejeans-tutorial/IC785877.png "Admin")</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="0cca3-226">The **Add User** tab is only available if, in the **Security tab**, **Enable automatic provisioning** is unchecked.</span><span class="sxs-lookup"><span data-stu-id="0cca3-226">The **Add User** tab is only available if, in the **Security tab**, **Enable automatic provisioning** is unchecked.</span></span> 

1. <span data-ttu-id="0cca3-227">In the **Add User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0cca3-227">In the **Add User** section, perform the following steps:</span></span>

    <span data-ttu-id="0cca3-228">![Add User](./media/bluejeans-tutorial/IC785886.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="0cca3-228">![Add User](./media/bluejeans-tutorial/IC785886.png "Add User")</span></span>

    <span data-ttu-id="0cca3-229">a.</span><span class="sxs-lookup"><span data-stu-id="0cca3-229">a.</span></span> <span data-ttu-id="0cca3-230">Type a **BlueJeans Username**, an **Email address**, a **BlueJeans Meeting ID**, a **Moderator Passcode**, a **Full Name**, the **Company** of a valid AAD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="0cca3-230">Type a **BlueJeans Username**, an **Email address**, a **BlueJeans Meeting ID**, a **Moderator Passcode**, a **Full Name**, the **Company** of a valid AAD account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="0cca3-231">b.</span><span class="sxs-lookup"><span data-stu-id="0cca3-231">b.</span></span> <span data-ttu-id="0cca3-232">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="0cca3-232">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="0cca3-233">You can use any other BlueJeans user account creation tools or APIs provided by BlueJeans to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="0cca3-233">You can use any other BlueJeans user account creation tools or APIs provided by BlueJeans to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0cca3-234">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0cca3-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0cca3-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BlueJeans.</span><span class="sxs-lookup"><span data-stu-id="0cca3-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BlueJeans.</span></span>

![Assign User][200]

<span data-ttu-id="0cca3-237">**To assign Britta Simon to BlueJeans, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0cca3-237">**To assign Britta Simon to BlueJeans, perform the following steps:**</span></span>

1. <span data-ttu-id="0cca3-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0cca3-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

1. <span data-ttu-id="0cca3-240">In the applications list, select **BlueJeans**.</span><span class="sxs-lookup"><span data-stu-id="0cca3-240">In the applications list, select **BlueJeans**.</span></span>

    ![Configure Single Sign-On](./media/bluejeans-tutorial/tutorial_bluejeans_app.png)

1. <span data-ttu-id="0cca3-242">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="0cca3-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202]

1. <span data-ttu-id="0cca3-244">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="0cca3-244">Click **Add** button.</span></span> <span data-ttu-id="0cca3-245">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0cca3-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="0cca3-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="0cca3-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="0cca3-248">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="0cca3-248">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="0cca3-249">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0cca3-249">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="0cca3-250">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="0cca3-250">Testing single sign-on</span></span>

<span data-ttu-id="0cca3-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="0cca3-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0cca3-252">When you click the BlueJeans tile in the Access Panel, you should get login page of BlueJeans application.</span><span class="sxs-lookup"><span data-stu-id="0cca3-252">When you click the BlueJeans tile in the Access Panel, you should get login page of BlueJeans application.</span></span>
<span data-ttu-id="0cca3-253">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0cca3-253">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0cca3-254">Additional resources</span><span class="sxs-lookup"><span data-stu-id="0cca3-254">Additional resources</span></span>

* [<span data-ttu-id="0cca3-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0cca3-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="0cca3-256">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0cca3-256">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="0cca3-257">Configure User Provisioning</span><span class="sxs-lookup"><span data-stu-id="0cca3-257">Configure User Provisioning</span></span>](bluejeans-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/bluejeans-tutorial/tutorial_general_203.png
