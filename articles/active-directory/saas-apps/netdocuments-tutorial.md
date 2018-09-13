---
title: 'Tutorial: Azure Active Directory integration with NetDocuments | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and NetDocuments.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 2da548b0d3a13dfac5d3928d8d692ac8e083bf58
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870111"
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a><span data-ttu-id="b233c-103">Tutorial: Azure Active Directory integration with NetDocuments</span><span class="sxs-lookup"><span data-stu-id="b233c-103">Tutorial: Azure Active Directory integration with NetDocuments</span></span>

<span data-ttu-id="b233c-104">In this tutorial, you learn how to integrate NetDocuments with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b233c-104">In this tutorial, you learn how to integrate NetDocuments with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b233c-105">Integrating NetDocuments with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="b233c-105">Integrating NetDocuments with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b233c-106">You can control in Azure AD who has access to NetDocuments</span><span class="sxs-lookup"><span data-stu-id="b233c-106">You can control in Azure AD who has access to NetDocuments</span></span>
- <span data-ttu-id="b233c-107">You can enable your users to automatically get signed-on to NetDocuments (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="b233c-107">You can enable your users to automatically get signed-on to NetDocuments (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b233c-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b233c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b233c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="b233c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b233c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b233c-110">Prerequisites</span></span>

<span data-ttu-id="b233c-111">To configure Azure AD integration with NetDocuments, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="b233c-111">To configure Azure AD integration with NetDocuments, you need the following items:</span></span>

- <span data-ttu-id="b233c-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="b233c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b233c-113">A NetDocuments single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="b233c-113">A NetDocuments single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b233c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="b233c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b233c-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="b233c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b233c-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="b233c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b233c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b233c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b233c-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="b233c-118">Scenario description</span></span>
<span data-ttu-id="b233c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="b233c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b233c-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="b233c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b233c-121">Adding NetDocuments from the gallery</span><span class="sxs-lookup"><span data-stu-id="b233c-121">Adding NetDocuments from the gallery</span></span>
1. <span data-ttu-id="b233c-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b233c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netdocuments-from-the-gallery"></a><span data-ttu-id="b233c-123">Adding NetDocuments from the gallery</span><span class="sxs-lookup"><span data-stu-id="b233c-123">Adding NetDocuments from the gallery</span></span>
<span data-ttu-id="b233c-124">To configure the integration of NetDocuments into Azure AD, you need to add NetDocuments from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="b233c-124">To configure the integration of NetDocuments into Azure AD, you need to add NetDocuments from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b233c-125">**To add NetDocuments from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b233c-125">**To add NetDocuments from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b233c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="b233c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="b233c-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="b233c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b233c-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b233c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="b233c-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="b233c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="b233c-133">In the search box, type **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="b233c-133">In the search box, type **NetDocuments**.</span></span>

    ![Creating an Azure AD test user](./media/netdocuments-tutorial/tutorial_netdocuments_search.png)

1. <span data-ttu-id="b233c-135">In the results panel, select **NetDocuments**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="b233c-135">In the results panel, select **NetDocuments**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/netdocuments-tutorial/tutorial_netdocuments_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b233c-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b233c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b233c-138">In this section, you configure and test Azure AD single sign-on with NetDocuments based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b233c-138">In this section, you configure and test Azure AD single sign-on with NetDocuments based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b233c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in NetDocuments is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b233c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in NetDocuments is to a user in Azure AD.</span></span> <span data-ttu-id="b233c-140">In other words, a link relationship between an Azure AD user and the related user in NetDocuments needs to be established.</span><span class="sxs-lookup"><span data-stu-id="b233c-140">In other words, a link relationship between an Azure AD user and the related user in NetDocuments needs to be established.</span></span>

<span data-ttu-id="b233c-141">In NetDocuments, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="b233c-141">In NetDocuments, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b233c-142">To configure and test Azure AD single sign-on with NetDocuments, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b233c-142">To configure and test Azure AD single sign-on with NetDocuments, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b233c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="b233c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="b233c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b233c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="b233c-145">**[Creating a NetDocuments test user](#creating-a-netdocuments-test-user)** - to have a counterpart of Britta Simon in NetDocuments that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="b233c-145">**[Creating a NetDocuments test user](#creating-a-netdocuments-test-user)** - to have a counterpart of Britta Simon in NetDocuments that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="b233c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b233c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="b233c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="b233c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b233c-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b233c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b233c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your NetDocuments application.</span><span class="sxs-lookup"><span data-stu-id="b233c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your NetDocuments application.</span></span>

<span data-ttu-id="b233c-150">**To configure Azure AD single sign-on with NetDocuments, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b233c-150">**To configure Azure AD single sign-on with NetDocuments, perform the following steps:**</span></span>

1. <span data-ttu-id="b233c-151">In the Azure portal, on the **NetDocuments** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b233c-151">In the Azure portal, on the **NetDocuments** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="b233c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b233c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/netdocuments-tutorial/tutorial_netdocuments_samlbase.png)

1. <span data-ttu-id="b233c-155">On the **NetDocuments Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b233c-155">On the **NetDocuments Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/netdocuments-tutorial/tutorial_netdocuments_url.png)

    <span data-ttu-id="b233c-157">a.</span><span class="sxs-lookup"><span data-stu-id="b233c-157">a.</span></span> <span data-ttu-id="b233c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="b233c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    <span data-ttu-id="b233c-159">b.</span><span class="sxs-lookup"><span data-stu-id="b233c-159">b.</span></span> <span data-ttu-id="b233c-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="b233c-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b233c-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="b233c-161">These values are not real.</span></span> <span data-ttu-id="b233c-162">Update these values with the actual Sign-on URL and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="b233c-162">Update these values with the actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="b233c-163">Contact [NetDocuments support team](https://support.netdocuments.com/hc/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="b233c-163">Contact [NetDocuments support team](https://support.netdocuments.com/hc/) to get these values.</span></span>
 
1. <span data-ttu-id="b233c-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="b233c-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/netdocuments-tutorial/tutorial_netdocuments_certificate.png) 

1. <span data-ttu-id="b233c-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="b233c-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/netdocuments-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="b233c-168">In a different web browser window, log into your NetDocuments company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="b233c-168">In a different web browser window, log into your NetDocuments company site as an administrator.</span></span>

1. <span data-ttu-id="b233c-169">Go to **Admin**.</span><span class="sxs-lookup"><span data-stu-id="b233c-169">Go to **Admin**.</span></span>

1. <span data-ttu-id="b233c-170">Click **Add and remove users and groups**.</span><span class="sxs-lookup"><span data-stu-id="b233c-170">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="b233c-171">![Repository](./media/netdocuments-tutorial/ic795047.png "Repository")</span><span class="sxs-lookup"><span data-stu-id="b233c-171">![Repository](./media/netdocuments-tutorial/ic795047.png "Repository")</span></span>

1. <span data-ttu-id="b233c-172">Click **Configure advanced authentication options**.</span><span class="sxs-lookup"><span data-stu-id="b233c-172">Click **Configure advanced authentication options**.</span></span>
    
    <span data-ttu-id="b233c-173">![Configure advanced authentication options](./media/netdocuments-tutorial/ic795048.png "Configure advanced authentication options")</span><span class="sxs-lookup"><span data-stu-id="b233c-173">![Configure advanced authentication options](./media/netdocuments-tutorial/ic795048.png "Configure advanced authentication options")</span></span>

1. <span data-ttu-id="b233c-174">On the **Federated Identity** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b233c-174">On the **Federated Identity** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="b233c-175">![Federated Identitty](./media/netdocuments-tutorial/ic795049.png "Federated Identitty")</span><span class="sxs-lookup"><span data-stu-id="b233c-175">![Federated Identitty](./media/netdocuments-tutorial/ic795049.png "Federated Identitty")</span></span>
   
    <span data-ttu-id="b233c-176">a.</span><span class="sxs-lookup"><span data-stu-id="b233c-176">a.</span></span> <span data-ttu-id="b233c-177">As **Federated identity server type**, select **Active Directory Federation Services**.</span><span class="sxs-lookup"><span data-stu-id="b233c-177">As **Federated identity server type**, select **Active Directory Federation Services**.</span></span>
   
    <span data-ttu-id="b233c-178">b.</span><span class="sxs-lookup"><span data-stu-id="b233c-178">b.</span></span> <span data-ttu-id="b233c-179">Click **Choose file**, to upload the downloaded metadata file which you have downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b233c-179">Click **Choose file**, to upload the downloaded metadata file which you have downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="b233c-180">c.</span><span class="sxs-lookup"><span data-stu-id="b233c-180">c.</span></span> <span data-ttu-id="b233c-181">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="b233c-181">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="b233c-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="b233c-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b233c-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="b233c-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b233c-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b233c-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b233c-185">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b233c-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="b233c-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b233c-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="b233c-188">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b233c-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b233c-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="b233c-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/netdocuments-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="b233c-191">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="b233c-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/netdocuments-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="b233c-193">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="b233c-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/netdocuments-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="b233c-195">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b233c-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/netdocuments-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b233c-197">a.</span><span class="sxs-lookup"><span data-stu-id="b233c-197">a.</span></span> <span data-ttu-id="b233c-198">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b233c-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b233c-199">b.</span><span class="sxs-lookup"><span data-stu-id="b233c-199">b.</span></span> <span data-ttu-id="b233c-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b233c-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b233c-201">c.</span><span class="sxs-lookup"><span data-stu-id="b233c-201">c.</span></span> <span data-ttu-id="b233c-202">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="b233c-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b233c-203">d.</span><span class="sxs-lookup"><span data-stu-id="b233c-203">d.</span></span> <span data-ttu-id="b233c-204">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b233c-204">Click **Create**.</span></span>
 
### <a name="creating-a-netdocuments-test-user"></a><span data-ttu-id="b233c-205">Creating a NetDocuments test user</span><span class="sxs-lookup"><span data-stu-id="b233c-205">Creating a NetDocuments test user</span></span>

<span data-ttu-id="b233c-206">To enable Azure AD users to log in to NetDocuments, they must be provisioned into NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="b233c-206">To enable Azure AD users to log in to NetDocuments, they must be provisioned into NetDocuments.</span></span>  
<span data-ttu-id="b233c-207">In the case of NetDocuments, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="b233c-207">In the case of NetDocuments, provisioning is a manual task.</span></span>

<span data-ttu-id="b233c-208">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b233c-208">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="b233c-209">Sing on to your **NetDocuments** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="b233c-209">Sing on to your **NetDocuments** company site as administrator.</span></span>

1. <span data-ttu-id="b233c-210">In the menu on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="b233c-210">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="b233c-211">![Admin](./media/netdocuments-tutorial/ic795051.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="b233c-211">![Admin](./media/netdocuments-tutorial/ic795051.png "Admin")</span></span>

1. <span data-ttu-id="b233c-212">Click **Add and remove users and groups**.</span><span class="sxs-lookup"><span data-stu-id="b233c-212">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="b233c-213">![Repository](./media/netdocuments-tutorial/ic795047.png "Repository")</span><span class="sxs-lookup"><span data-stu-id="b233c-213">![Repository](./media/netdocuments-tutorial/ic795047.png "Repository")</span></span>

1. <span data-ttu-id="b233c-214">In the **Email Address** textbox, type the email address of a valid Azure Active Directory account you want to provision, and then click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="b233c-214">In the **Email Address** textbox, type the email address of a valid Azure Active Directory account you want to provision, and then click **Add User**.</span></span>
   
    <span data-ttu-id="b233c-215">![Email Address](./media/netdocuments-tutorial/ic795053.png "Email Address")</span><span class="sxs-lookup"><span data-stu-id="b233c-215">![Email Address](./media/netdocuments-tutorial/ic795053.png "Email Address")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="b233c-216">The Azure Active Directory account holder will get an email that includes a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="b233c-216">The Azure Active Directory account holder will get an email that includes a link to confirm the account before it becomes active.</span></span> <span data-ttu-id="b233c-217">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments to provision Azure Active Directory user accounts.</span><span class="sxs-lookup"><span data-stu-id="b233c-217">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b233c-218">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b233c-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b233c-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="b233c-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to NetDocuments.</span></span>

![Assign User][200] 

<span data-ttu-id="b233c-221">**To assign Britta Simon to NetDocuments, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b233c-221">**To assign Britta Simon to NetDocuments, perform the following steps:**</span></span>

1. <span data-ttu-id="b233c-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b233c-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="b233c-224">In the applications list, select **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="b233c-224">In the applications list, select **NetDocuments**.</span></span>

    ![Configure Single Sign-On](./media/netdocuments-tutorial/tutorial_netdocuments_app.png) 

1. <span data-ttu-id="b233c-226">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="b233c-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="b233c-228">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="b233c-228">Click **Add** button.</span></span> <span data-ttu-id="b233c-229">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b233c-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="b233c-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="b233c-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="b233c-232">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="b233c-232">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="b233c-233">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b233c-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b233c-234">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="b233c-234">Testing single sign-on</span></span>

<span data-ttu-id="b233c-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b233c-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b233c-236">When you click the NetDocuments tile in the Access Panel, you should get automatically signed-on to your NetDocuments application.</span><span class="sxs-lookup"><span data-stu-id="b233c-236">When you click the NetDocuments tile in the Access Panel, you should get automatically signed-on to your NetDocuments application.</span></span>
<span data-ttu-id="b233c-237">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b233c-237">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b233c-238">Additional resources</span><span class="sxs-lookup"><span data-stu-id="b233c-238">Additional resources</span></span>

* [<span data-ttu-id="b233c-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b233c-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="b233c-240">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b233c-240">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/netdocuments-tutorial/tutorial_general_01.png
[2]: ./media/netdocuments-tutorial/tutorial_general_02.png
[3]: ./media/netdocuments-tutorial/tutorial_general_03.png
[4]: ./media/netdocuments-tutorial/tutorial_general_04.png

[100]: ./media/netdocuments-tutorial/tutorial_general_100.png

[200]: ./media/netdocuments-tutorial/tutorial_general_200.png
[201]: ./media/netdocuments-tutorial/tutorial_general_201.png
[202]: ./media/netdocuments-tutorial/tutorial_general_202.png
[203]: ./media/netdocuments-tutorial/tutorial_general_203.png

