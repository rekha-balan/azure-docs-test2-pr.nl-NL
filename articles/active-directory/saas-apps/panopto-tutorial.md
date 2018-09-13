---
title: 'Tutorial: Azure Active Directory integration with Panopto | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Panopto.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 89c88e23-93ce-4970-9baa-1104c4e8fe4a
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 60d4b9f5343aac978c1e32aad39f237d565b2176
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856562"
---
# <a name="tutorial-azure-active-directory-integration-with-panopto"></a><span data-ttu-id="365d5-103">Tutorial: Azure Active Directory integration with Panopto</span><span class="sxs-lookup"><span data-stu-id="365d5-103">Tutorial: Azure Active Directory integration with Panopto</span></span>

<span data-ttu-id="365d5-104">In this tutorial, you learn how to integrate Panopto with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="365d5-104">In this tutorial, you learn how to integrate Panopto with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="365d5-105">Integrating Panopto with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="365d5-105">Integrating Panopto with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="365d5-106">You can control in Azure AD who has access to Panopto</span><span class="sxs-lookup"><span data-stu-id="365d5-106">You can control in Azure AD who has access to Panopto</span></span>
- <span data-ttu-id="365d5-107">You can enable your users to automatically get signed-on to Panopto (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="365d5-107">You can enable your users to automatically get signed-on to Panopto (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="365d5-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="365d5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="365d5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="365d5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="365d5-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="365d5-110">Prerequisites</span></span>

<span data-ttu-id="365d5-111">To configure Azure AD integration with Panopto, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="365d5-111">To configure Azure AD integration with Panopto, you need the following items:</span></span>

- <span data-ttu-id="365d5-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="365d5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="365d5-113">A Panopto single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="365d5-113">A Panopto single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="365d5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="365d5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="365d5-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="365d5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="365d5-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="365d5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="365d5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="365d5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="365d5-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="365d5-118">Scenario description</span></span>
<span data-ttu-id="365d5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="365d5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="365d5-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="365d5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="365d5-121">Adding Panopto from the gallery</span><span class="sxs-lookup"><span data-stu-id="365d5-121">Adding Panopto from the gallery</span></span>
1. <span data-ttu-id="365d5-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="365d5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panopto-from-the-gallery"></a><span data-ttu-id="365d5-123">Adding Panopto from the gallery</span><span class="sxs-lookup"><span data-stu-id="365d5-123">Adding Panopto from the gallery</span></span>
<span data-ttu-id="365d5-124">To configure the integration of Panopto into Azure AD, you need to add Panopto from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="365d5-124">To configure the integration of Panopto into Azure AD, you need to add Panopto from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="365d5-125">**To add Panopto from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="365d5-125">**To add Panopto from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="365d5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="365d5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="365d5-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="365d5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="365d5-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="365d5-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="365d5-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="365d5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="365d5-133">In the search box, type **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="365d5-133">In the search box, type **Panopto**.</span></span>

    ![Creating an Azure AD test user](./media/panopto-tutorial/tutorial_panopto_search.png)

1. <span data-ttu-id="365d5-135">In the results panel, select **Panopto**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="365d5-135">In the results panel, select **Panopto**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/panopto-tutorial/tutorial_panopto_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="365d5-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="365d5-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="365d5-138">In this section, you configure and test Azure AD single sign-on with Panopto based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="365d5-138">In this section, you configure and test Azure AD single sign-on with Panopto based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="365d5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Panopto is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="365d5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Panopto is to a user in Azure AD.</span></span> <span data-ttu-id="365d5-140">In other words, a link relationship between an Azure AD user and the related user in Panopto needs to be established.</span><span class="sxs-lookup"><span data-stu-id="365d5-140">In other words, a link relationship between an Azure AD user and the related user in Panopto needs to be established.</span></span>

<span data-ttu-id="365d5-141">In Panopto, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="365d5-141">In Panopto, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="365d5-142">To configure and test Azure AD single sign-on with Panopto, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="365d5-142">To configure and test Azure AD single sign-on with Panopto, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="365d5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="365d5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="365d5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="365d5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="365d5-145">**[Creating a Panopto test user](#creating-a-panopto-test-user)** - to have a counterpart of Britta Simon in Panopto that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="365d5-145">**[Creating a Panopto test user](#creating-a-panopto-test-user)** - to have a counterpart of Britta Simon in Panopto that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="365d5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="365d5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="365d5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="365d5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="365d5-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="365d5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="365d5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Panopto application.</span><span class="sxs-lookup"><span data-stu-id="365d5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Panopto application.</span></span>

<span data-ttu-id="365d5-150">**To configure Azure AD single sign-on with Panopto, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="365d5-150">**To configure Azure AD single sign-on with Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="365d5-151">In the Azure portal, on the **Panopto** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="365d5-151">In the Azure portal, on the **Panopto** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="365d5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="365d5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/panopto-tutorial/tutorial_panopto_samlbase.png)

1. <span data-ttu-id="365d5-155">On the **Panopto Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="365d5-155">On the **Panopto Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/panopto-tutorial/tutorial_panopto_url.png)

    <span data-ttu-id="365d5-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.panopto.com`</span><span class="sxs-lookup"><span data-stu-id="365d5-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.panopto.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="365d5-158">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="365d5-158">This value is not real.</span></span> <span data-ttu-id="365d5-159">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="365d5-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="365d5-160">Contact [Panopto Client support team](mailto:support@panopto.com‎) to get this value.</span><span class="sxs-lookup"><span data-stu-id="365d5-160">Contact [Panopto Client support team](mailto:support@panopto.com‎) to get this value.</span></span> 
 
1. <span data-ttu-id="365d5-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="365d5-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/panopto-tutorial/tutorial_panopto_certificate.png) 

1. <span data-ttu-id="365d5-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="365d5-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/panopto-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="365d5-165">On the **Panopto Configuration** section, click **Configure Panopto** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="365d5-165">On the **Panopto Configuration** section, click **Configure Panopto** to open **Configure sign-on** window.</span></span> <span data-ttu-id="365d5-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="365d5-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/panopto-tutorial/tutorial_panopto_configure.png) 

1. <span data-ttu-id="365d5-168">In a different web browser window, log in to your Panopto company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="365d5-168">In a different web browser window, log in to your Panopto company site as an administrator.</span></span>

1. <span data-ttu-id="365d5-169">In the toolbar on the left, click **System**, and then click **Identity Providers**.</span><span class="sxs-lookup"><span data-stu-id="365d5-169">In the toolbar on the left, click **System**, and then click **Identity Providers**.</span></span>
   
   <span data-ttu-id="365d5-170">![System](./media/panopto-tutorial/ic777670.png "System")</span><span class="sxs-lookup"><span data-stu-id="365d5-170">![System](./media/panopto-tutorial/ic777670.png "System")</span></span>
1. <span data-ttu-id="365d5-171">Click **Add Provider**.</span><span class="sxs-lookup"><span data-stu-id="365d5-171">Click **Add Provider**.</span></span>
   
   <span data-ttu-id="365d5-172">![Identity Providers](./media/panopto-tutorial/ic777671.png "Identity Providers")</span><span class="sxs-lookup"><span data-stu-id="365d5-172">![Identity Providers](./media/panopto-tutorial/ic777671.png "Identity Providers")</span></span>
   
1. <span data-ttu-id="365d5-173">In the SAML provider section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="365d5-173">In the SAML provider section, perform the following steps:</span></span>
   
    <span data-ttu-id="365d5-174">![SaaS configuration](./media/panopto-tutorial/ic777672.png "SaaS configuration")</span><span class="sxs-lookup"><span data-stu-id="365d5-174">![SaaS configuration](./media/panopto-tutorial/ic777672.png "SaaS configuration")</span></span>
    
    <span data-ttu-id="365d5-175">a.</span><span class="sxs-lookup"><span data-stu-id="365d5-175">a.</span></span> <span data-ttu-id="365d5-176">From the **Provider Type** list, select **SAML20**.</span><span class="sxs-lookup"><span data-stu-id="365d5-176">From the **Provider Type** list, select **SAML20**.</span></span>    
    
    <span data-ttu-id="365d5-177">b.</span><span class="sxs-lookup"><span data-stu-id="365d5-177">b.</span></span> <span data-ttu-id="365d5-178">In the **Instance Name** textbox, type a name for the instance.</span><span class="sxs-lookup"><span data-stu-id="365d5-178">In the **Instance Name** textbox, type a name for the instance.</span></span>

    <span data-ttu-id="365d5-179">c.</span><span class="sxs-lookup"><span data-stu-id="365d5-179">c.</span></span> <span data-ttu-id="365d5-180">In the **Friendly Description** textbox, type a friendly description.</span><span class="sxs-lookup"><span data-stu-id="365d5-180">In the **Friendly Description** textbox, type a friendly description.</span></span>
    
    <span data-ttu-id="365d5-181">d.</span><span class="sxs-lookup"><span data-stu-id="365d5-181">d.</span></span> <span data-ttu-id="365d5-182">In **Bounce Page Url** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="365d5-182">In **Bounce Page Url** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="365d5-183">e.</span><span class="sxs-lookup"><span data-stu-id="365d5-183">e.</span></span> <span data-ttu-id="365d5-184">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="365d5-184">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="365d5-185">f.</span><span class="sxs-lookup"><span data-stu-id="365d5-185">f.</span></span> <span data-ttu-id="365d5-186">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy the content of it in to your clipboard, and then paste it to the **Public Key**  textbox.</span><span class="sxs-lookup"><span data-stu-id="365d5-186">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy the content of it in to your clipboard, and then paste it to the **Public Key**  textbox.</span></span>

1. <span data-ttu-id="365d5-187">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="365d5-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="365d5-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="365d5-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="365d5-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="365d5-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="365d5-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="365d5-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="365d5-191">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="365d5-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="365d5-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="365d5-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="365d5-194">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="365d5-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="365d5-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="365d5-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/panopto-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="365d5-197">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="365d5-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/panopto-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="365d5-199">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="365d5-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/panopto-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="365d5-201">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="365d5-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/panopto-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="365d5-203">a.</span><span class="sxs-lookup"><span data-stu-id="365d5-203">a.</span></span> <span data-ttu-id="365d5-204">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="365d5-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="365d5-205">b.</span><span class="sxs-lookup"><span data-stu-id="365d5-205">b.</span></span> <span data-ttu-id="365d5-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="365d5-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="365d5-207">c.</span><span class="sxs-lookup"><span data-stu-id="365d5-207">c.</span></span> <span data-ttu-id="365d5-208">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="365d5-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="365d5-209">d.</span><span class="sxs-lookup"><span data-stu-id="365d5-209">d.</span></span> <span data-ttu-id="365d5-210">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="365d5-210">Click **Create**.</span></span>
 
### <a name="creating-a-panopto-test-user"></a><span data-ttu-id="365d5-211">Creating a Panopto test user</span><span class="sxs-lookup"><span data-stu-id="365d5-211">Creating a Panopto test user</span></span>

<span data-ttu-id="365d5-212">There is no action item for you to configure user provisioning to Panopto.</span><span class="sxs-lookup"><span data-stu-id="365d5-212">There is no action item for you to configure user provisioning to Panopto.</span></span>  
<span data-ttu-id="365d5-213">When an assigned user tries to log in to Panopto using the access panel, Panopto checks whether the user exists.</span><span class="sxs-lookup"><span data-stu-id="365d5-213">When an assigned user tries to log in to Panopto using the access panel, Panopto checks whether the user exists.</span></span>  

<span data-ttu-id="365d5-214">If there is no user account available yet, it is automatically created by Panopto.</span><span class="sxs-lookup"><span data-stu-id="365d5-214">If there is no user account available yet, it is automatically created by Panopto.</span></span>

>[!NOTE]
><span data-ttu-id="365d5-215">You can use any other Panopto user account creation tools or APIs provided by Panopto to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="365d5-215">You can use any other Panopto user account creation tools or APIs provided by Panopto to provision Azure AD user accounts.</span></span>
>
>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="365d5-216">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="365d5-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="365d5-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Panopto.</span><span class="sxs-lookup"><span data-stu-id="365d5-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Panopto.</span></span>

![Assign User][200] 

<span data-ttu-id="365d5-219">**To assign Britta Simon to Panopto, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="365d5-219">**To assign Britta Simon to Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="365d5-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="365d5-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="365d5-222">In the applications list, select **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="365d5-222">In the applications list, select **Panopto**.</span></span>

    ![Configure Single Sign-On](./media/panopto-tutorial/tutorial_panopto_app.png) 

1. <span data-ttu-id="365d5-224">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="365d5-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="365d5-226">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="365d5-226">Click **Add** button.</span></span> <span data-ttu-id="365d5-227">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="365d5-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="365d5-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="365d5-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="365d5-230">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="365d5-230">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="365d5-231">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="365d5-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="365d5-232">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="365d5-232">Testing single sign-on</span></span>

<span data-ttu-id="365d5-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="365d5-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="365d5-234">When you click the Panopto tile in the Access Panel, you should get automatically login page of Panopto application.</span><span class="sxs-lookup"><span data-stu-id="365d5-234">When you click the Panopto tile in the Access Panel, you should get automatically login page of Panopto application.</span></span>
<span data-ttu-id="365d5-235">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="365d5-235">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="365d5-236">Additional resources</span><span class="sxs-lookup"><span data-stu-id="365d5-236">Additional resources</span></span>

* [<span data-ttu-id="365d5-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="365d5-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="365d5-238">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="365d5-238">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/panopto-tutorial/tutorial_general_01.png
[2]: ./media/panopto-tutorial/tutorial_general_02.png
[3]: ./media/panopto-tutorial/tutorial_general_03.png
[4]: ./media/panopto-tutorial/tutorial_general_04.png

[100]: ./media/panopto-tutorial/tutorial_general_100.png

[200]: ./media/panopto-tutorial/tutorial_general_200.png
[201]: ./media/panopto-tutorial/tutorial_general_201.png
[202]: ./media/panopto-tutorial/tutorial_general_202.png
[203]: ./media/panopto-tutorial/tutorial_general_203.png

