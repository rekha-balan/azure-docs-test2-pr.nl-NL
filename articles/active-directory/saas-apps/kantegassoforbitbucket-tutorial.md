---
title: 'Tutorial: Azure Active Directory integration with Kantega SSO for Bitbucket | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Kantega SSO for Bitbucket.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: c41cdaaf-0441-493c-94c7-569615b7b1ab
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: a81ea48937927e13141642d70093bc322196b2cc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868366"
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-bitbucket"></a><span data-ttu-id="bf129-103">Tutorial: Azure Active Directory integration with Kantega SSO for Bitbucket</span><span class="sxs-lookup"><span data-stu-id="bf129-103">Tutorial: Azure Active Directory integration with Kantega SSO for Bitbucket</span></span>

<span data-ttu-id="bf129-104">In this tutorial, you learn how to integrate Kantega SSO for Bitbucket with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bf129-104">In this tutorial, you learn how to integrate Kantega SSO for Bitbucket with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bf129-105">Integrating Kantega SSO for Bitbucket with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="bf129-105">Integrating Kantega SSO for Bitbucket with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bf129-106">You can control in Azure AD who has access to Kantega SSO for Bitbucket</span><span class="sxs-lookup"><span data-stu-id="bf129-106">You can control in Azure AD who has access to Kantega SSO for Bitbucket</span></span>
- <span data-ttu-id="bf129-107">You can enable your users to automatically get signed-on to Kantega SSO for Bitbucket (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="bf129-107">You can enable your users to automatically get signed-on to Kantega SSO for Bitbucket (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bf129-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="bf129-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bf129-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="bf129-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf129-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bf129-110">Prerequisites</span></span>

<span data-ttu-id="bf129-111">To configure Azure AD integration with Kantega SSO for Bitbucket, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="bf129-111">To configure Azure AD integration with Kantega SSO for Bitbucket, you need the following items:</span></span>

- <span data-ttu-id="bf129-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="bf129-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bf129-113">A Kantega SSO for Bitbucket single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="bf129-113">A Kantega SSO for Bitbucket single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bf129-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="bf129-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bf129-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="bf129-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bf129-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="bf129-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bf129-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bf129-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bf129-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="bf129-118">Scenario description</span></span>
<span data-ttu-id="bf129-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="bf129-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bf129-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="bf129-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bf129-121">Adding Kantega SSO for Bitbucket from the gallery</span><span class="sxs-lookup"><span data-stu-id="bf129-121">Adding Kantega SSO for Bitbucket from the gallery</span></span>
1. <span data-ttu-id="bf129-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bf129-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-bitbucket-from-the-gallery"></a><span data-ttu-id="bf129-123">Adding Kantega SSO for Bitbucket from the gallery</span><span class="sxs-lookup"><span data-stu-id="bf129-123">Adding Kantega SSO for Bitbucket from the gallery</span></span>
<span data-ttu-id="bf129-124">To configure the integration of Kantega SSO for Bitbucket into Azure AD, you need to add Kantega SSO for Bitbucket from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="bf129-124">To configure the integration of Kantega SSO for Bitbucket into Azure AD, you need to add Kantega SSO for Bitbucket from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bf129-125">**To add Kantega SSO for Bitbucket from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bf129-125">**To add Kantega SSO for Bitbucket from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bf129-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="bf129-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="bf129-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="bf129-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bf129-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="bf129-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="bf129-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="bf129-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="bf129-133">In the search box, type **Kantega SSO for Bitbucket**.</span><span class="sxs-lookup"><span data-stu-id="bf129-133">In the search box, type **Kantega SSO for Bitbucket**.</span></span>

    ![Creating an Azure AD test user](./media/kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_search.png)

1. <span data-ttu-id="bf129-135">In the results panel, select **Kantega SSO for Bitbucket**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="bf129-135">In the results panel, select **Kantega SSO for Bitbucket**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bf129-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bf129-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bf129-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Bitbucket based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bf129-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Bitbucket based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bf129-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for Bitbucket is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf129-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for Bitbucket is to a user in Azure AD.</span></span> <span data-ttu-id="bf129-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for Bitbucket needs to be established.</span><span class="sxs-lookup"><span data-stu-id="bf129-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for Bitbucket needs to be established.</span></span>

<span data-ttu-id="bf129-141">In Kantega SSO for Bitbucket, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="bf129-141">In Kantega SSO for Bitbucket, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bf129-142">To configure and test Azure AD single sign-on with Kantega SSO for Bitbucket, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="bf129-142">To configure and test Azure AD single sign-on with Kantega SSO for Bitbucket, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bf129-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="bf129-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="bf129-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bf129-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="bf129-145">**[Creating a Kantega SSO for Bitbucket test user](#creating-a-kantega-sso-for-bitbucket-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for Bitbucket that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="bf129-145">**[Creating a Kantega SSO for Bitbucket test user](#creating-a-kantega-sso-for-bitbucket-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for Bitbucket that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="bf129-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bf129-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="bf129-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="bf129-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bf129-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bf129-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bf129-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for Bitbucket application.</span><span class="sxs-lookup"><span data-stu-id="bf129-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for Bitbucket application.</span></span>

<span data-ttu-id="bf129-150">**To configure Azure AD single sign-on with Kantega SSO for Bitbucket, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bf129-150">**To configure Azure AD single sign-on with Kantega SSO for Bitbucket, perform the following steps:**</span></span>

1. <span data-ttu-id="bf129-151">In the Azure portal, on the **Kantega SSO for Bitbucket** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="bf129-151">In the Azure portal, on the **Kantega SSO for Bitbucket** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="bf129-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bf129-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_samlbase.png)

1. <span data-ttu-id="bf129-155">In **IDP** initiated mode, on the **Kantega SSO for Bitbucket Domain and URLs** section perform the following step:</span><span class="sxs-lookup"><span data-stu-id="bf129-155">In **IDP** initiated mode, on the **Kantega SSO for Bitbucket Domain and URLs** section perform the following step:</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_url1.png)

    <span data-ttu-id="bf129-157">a.</span><span class="sxs-lookup"><span data-stu-id="bf129-157">a.</span></span> <span data-ttu-id="bf129-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="bf129-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="bf129-159">b.</span><span class="sxs-lookup"><span data-stu-id="bf129-159">b.</span></span> <span data-ttu-id="bf129-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="bf129-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

1. <span data-ttu-id="bf129-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform the following step:</span><span class="sxs-lookup"><span data-stu-id="bf129-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform the following step:</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_url2.png)
    
    <span data-ttu-id="bf129-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="bf129-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bf129-164">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="bf129-164">These values are not real.</span></span> <span data-ttu-id="bf129-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="bf129-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="bf129-166">These values are recieved during the configuration of Bitbucket plugin which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="bf129-166">These values are recieved during the configuration of Bitbucket plugin which is explained later in the tutorial.</span></span>

1. <span data-ttu-id="bf129-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="bf129-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_certificate.png) 

1. <span data-ttu-id="bf129-169">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="bf129-169">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbitbucket-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="bf129-171">In a different web browser window, log in to your Bitbucket admin portal as an administrator.</span><span class="sxs-lookup"><span data-stu-id="bf129-171">In a different web browser window, log in to your Bitbucket admin portal as an administrator.</span></span>

1. <span data-ttu-id="bf129-172">Click cog and click the **Find new add-ons**.</span><span class="sxs-lookup"><span data-stu-id="bf129-172">Click cog and click the **Find new add-ons**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbitbucket-tutorial/addon1.png)

1. <span data-ttu-id="bf129-174">Search **Kantega SSO for Bitbucket SAML & Kerberos** and click **Install** button to install the new SAML plugin.</span><span class="sxs-lookup"><span data-stu-id="bf129-174">Search **Kantega SSO for Bitbucket SAML & Kerberos** and click **Install** button to install the new SAML plugin.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbitbucket-tutorial/addon2.png)

1. <span data-ttu-id="bf129-176">The plugin installation starts.</span><span class="sxs-lookup"><span data-stu-id="bf129-176">The plugin installation starts.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbitbucket-tutorial/addon31.png)

1. <span data-ttu-id="bf129-178">Once the installation is complete.</span><span class="sxs-lookup"><span data-stu-id="bf129-178">Once the installation is complete.</span></span> <span data-ttu-id="bf129-179">Click **Close**.</span><span class="sxs-lookup"><span data-stu-id="bf129-179">Click **Close**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbitbucket-tutorial/addon33.png)

1.  <span data-ttu-id="bf129-181">Click **Manage**.</span><span class="sxs-lookup"><span data-stu-id="bf129-181">Click **Manage**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbitbucket-tutorial/addon34.png)
    
1. <span data-ttu-id="bf129-183">Click **Configure** to configure the new plugin.</span><span class="sxs-lookup"><span data-stu-id="bf129-183">Click **Configure** to configure the new plugin.</span></span> 

    ![Configure Single Sign-On](./media/kantegassoforbitbucket-tutorial/addon35.png)

1. <span data-ttu-id="bf129-185">In the **SAML** section.</span><span class="sxs-lookup"><span data-stu-id="bf129-185">In the **SAML** section.</span></span> <span data-ttu-id="bf129-186">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span><span class="sxs-lookup"><span data-stu-id="bf129-186">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbitbucket-tutorial/addon4.png)

1. <span data-ttu-id="bf129-188">Select subscription level as **Basic**.</span><span class="sxs-lookup"><span data-stu-id="bf129-188">Select subscription level as **Basic**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbitbucket-tutorial/addon5.png)

1. <span data-ttu-id="bf129-190">On the **App properties** section, perform following steps:</span><span class="sxs-lookup"><span data-stu-id="bf129-190">On the **App properties** section, perform following steps:</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbitbucket-tutorial/addon6.png)

    <span data-ttu-id="bf129-192">a.</span><span class="sxs-lookup"><span data-stu-id="bf129-192">a.</span></span> <span data-ttu-id="bf129-193">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for Bitbucket Domain and URLs** section in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bf129-193">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for Bitbucket Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="bf129-194">b.</span><span class="sxs-lookup"><span data-stu-id="bf129-194">b.</span></span> <span data-ttu-id="bf129-195">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bf129-195">Click **Next**.</span></span>

1. <span data-ttu-id="bf129-196">On the **Metadata import** section, perform following steps:</span><span class="sxs-lookup"><span data-stu-id="bf129-196">On the **Metadata import** section, perform following steps:</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbitbucket-tutorial/addon7.png)

    <span data-ttu-id="bf129-198">a.</span><span class="sxs-lookup"><span data-stu-id="bf129-198">a.</span></span> <span data-ttu-id="bf129-199">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bf129-199">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="bf129-200">b.</span><span class="sxs-lookup"><span data-stu-id="bf129-200">b.</span></span> <span data-ttu-id="bf129-201">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bf129-201">Click **Next**.</span></span>

1. <span data-ttu-id="bf129-202">On the **Name and SSO location** section, perform following steps:</span><span class="sxs-lookup"><span data-stu-id="bf129-202">On the **Name and SSO location** section, perform following steps:</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbitbucket-tutorial/addon8.png)

    <span data-ttu-id="bf129-204">a.</span><span class="sxs-lookup"><span data-stu-id="bf129-204">a.</span></span> <span data-ttu-id="bf129-205">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bf129-205">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="bf129-206">b.</span><span class="sxs-lookup"><span data-stu-id="bf129-206">b.</span></span> <span data-ttu-id="bf129-207">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bf129-207">Click **Next**.</span></span>

1. <span data-ttu-id="bf129-208">Verify the Signing certificate and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bf129-208">Verify the Signing certificate and click **Next**.</span></span>   

    ![Configure Single Sign-On](./media/kantegassoforbitbucket-tutorial/addon9.png)

1. <span data-ttu-id="bf129-210">On the **Bitbucket user accounts** section, perform following steps:</span><span class="sxs-lookup"><span data-stu-id="bf129-210">On the **Bitbucket user accounts** section, perform following steps:</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbitbucket-tutorial/addon10.png)

    <span data-ttu-id="bf129-212">a.</span><span class="sxs-lookup"><span data-stu-id="bf129-212">a.</span></span> <span data-ttu-id="bf129-213">Select **Create users in Bitbucket's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span><span class="sxs-lookup"><span data-stu-id="bf129-213">Select **Create users in Bitbucket's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span></span> <span data-ttu-id="bf129-214">of groups separated by comma).</span><span class="sxs-lookup"><span data-stu-id="bf129-214">of groups separated by comma).</span></span>

    <span data-ttu-id="bf129-215">b.</span><span class="sxs-lookup"><span data-stu-id="bf129-215">b.</span></span> <span data-ttu-id="bf129-216">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bf129-216">Click **Next**.</span></span>

1. <span data-ttu-id="bf129-217">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="bf129-217">Click **Finish**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbitbucket-tutorial/addon11.png)

1. <span data-ttu-id="bf129-219">On the **Known domains for Azure AD** section, perform following steps:</span><span class="sxs-lookup"><span data-stu-id="bf129-219">On the **Known domains for Azure AD** section, perform following steps:</span></span>  

    ![Configure Single Sign-On](./media/kantegassoforbitbucket-tutorial/addon12.png)

    <span data-ttu-id="bf129-221">a.</span><span class="sxs-lookup"><span data-stu-id="bf129-221">a.</span></span> <span data-ttu-id="bf129-222">Select **Known domains** from the left panel of the page.</span><span class="sxs-lookup"><span data-stu-id="bf129-222">Select **Known domains** from the left panel of the page.</span></span>

    <span data-ttu-id="bf129-223">b.</span><span class="sxs-lookup"><span data-stu-id="bf129-223">b.</span></span> <span data-ttu-id="bf129-224">Enter domain name in the **Known domains** textbox.</span><span class="sxs-lookup"><span data-stu-id="bf129-224">Enter domain name in the **Known domains** textbox.</span></span>

    <span data-ttu-id="bf129-225">c.</span><span class="sxs-lookup"><span data-stu-id="bf129-225">c.</span></span> <span data-ttu-id="bf129-226">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="bf129-226">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="bf129-227">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="bf129-227">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bf129-228">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="bf129-228">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bf129-229">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bf129-229">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bf129-230">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="bf129-230">Creating an Azure AD test user</span></span>
<span data-ttu-id="bf129-231">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bf129-231">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="bf129-233">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bf129-233">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bf129-234">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="bf129-234">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/kantegassoforbitbucket-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="bf129-236">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="bf129-236">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/kantegassoforbitbucket-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="bf129-238">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="bf129-238">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/kantegassoforbitbucket-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="bf129-240">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bf129-240">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/kantegassoforbitbucket-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bf129-242">a.</span><span class="sxs-lookup"><span data-stu-id="bf129-242">a.</span></span> <span data-ttu-id="bf129-243">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bf129-243">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bf129-244">b.</span><span class="sxs-lookup"><span data-stu-id="bf129-244">b.</span></span> <span data-ttu-id="bf129-245">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bf129-245">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bf129-246">c.</span><span class="sxs-lookup"><span data-stu-id="bf129-246">c.</span></span> <span data-ttu-id="bf129-247">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="bf129-247">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bf129-248">d.</span><span class="sxs-lookup"><span data-stu-id="bf129-248">d.</span></span> <span data-ttu-id="bf129-249">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="bf129-249">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-bitbucket-test-user"></a><span data-ttu-id="bf129-250">Creating a Kantega SSO for Bitbucket test user</span><span class="sxs-lookup"><span data-stu-id="bf129-250">Creating a Kantega SSO for Bitbucket test user</span></span>

<span data-ttu-id="bf129-251">To enable Azure AD users to log in to Bitbucket, they must be provisioned into Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="bf129-251">To enable Azure AD users to log in to Bitbucket, they must be provisioned into Bitbucket.</span></span> <span data-ttu-id="bf129-252">In Kantega SSO for Bitbucket, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="bf129-252">In Kantega SSO for Bitbucket, provisioning is a manual task.</span></span>

<span data-ttu-id="bf129-253">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bf129-253">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="bf129-254">Log in to your Bitbucket company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="bf129-254">Log in to your Bitbucket company site as an administrator.</span></span>

1. <span data-ttu-id="bf129-255">Click on settings icon.</span><span class="sxs-lookup"><span data-stu-id="bf129-255">Click on settings icon.</span></span>

    ![Add Employee](./media/kantegassoforbitbucket-tutorial/user1.png) 

1. <span data-ttu-id="bf129-257">Under **Administration** tab section, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="bf129-257">Under **Administration** tab section, click **Users**.</span></span>

    ![Add Employee](./media/kantegassoforbitbucket-tutorial/user2.png)

1. <span data-ttu-id="bf129-259">Click **Create user**.</span><span class="sxs-lookup"><span data-stu-id="bf129-259">Click **Create user**.</span></span>

    ![Add Employee](./media/kantegassoforbitbucket-tutorial/user3.png)   

1. <span data-ttu-id="bf129-261">On the **Create User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bf129-261">On the **Create User** dialog page, perform the following steps:</span></span>

    ![Add Employee](./media/kantegassoforbitbucket-tutorial/user4.png) 

    <span data-ttu-id="bf129-263">a.</span><span class="sxs-lookup"><span data-stu-id="bf129-263">a.</span></span> <span data-ttu-id="bf129-264">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="bf129-264">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="bf129-265">b.</span><span class="sxs-lookup"><span data-stu-id="bf129-265">b.</span></span> <span data-ttu-id="bf129-266">In the **Full Name** textbox, type full name of the user like Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bf129-266">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>
    
    <span data-ttu-id="bf129-267">c.</span><span class="sxs-lookup"><span data-stu-id="bf129-267">c.</span></span> <span data-ttu-id="bf129-268">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="bf129-268">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="bf129-269">d.</span><span class="sxs-lookup"><span data-stu-id="bf129-269">d.</span></span> <span data-ttu-id="bf129-270">In the **Password** textbox, type the password of user.</span><span class="sxs-lookup"><span data-stu-id="bf129-270">In the **Password** textbox, type the password of user.</span></span>  

    <span data-ttu-id="bf129-271">e.</span><span class="sxs-lookup"><span data-stu-id="bf129-271">e.</span></span> <span data-ttu-id="bf129-272">In the **Confirm Password** textbox, reenter the password of user.</span><span class="sxs-lookup"><span data-stu-id="bf129-272">In the **Confirm Password** textbox, reenter the password of user.</span></span>

    <span data-ttu-id="bf129-273">f.</span><span class="sxs-lookup"><span data-stu-id="bf129-273">f.</span></span> <span data-ttu-id="bf129-274">Click **Create user**.</span><span class="sxs-lookup"><span data-stu-id="bf129-274">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bf129-275">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="bf129-275">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bf129-276">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="bf129-276">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for Bitbucket.</span></span>

![Assign User][200] 

<span data-ttu-id="bf129-278">**To assign Britta Simon to Kantega SSO for Bitbucket, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bf129-278">**To assign Britta Simon to Kantega SSO for Bitbucket, perform the following steps:**</span></span>

1. <span data-ttu-id="bf129-279">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="bf129-279">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="bf129-281">In the applications list, select **Kantega SSO for Bitbucket**.</span><span class="sxs-lookup"><span data-stu-id="bf129-281">In the applications list, select **Kantega SSO for Bitbucket**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbitbucket-tutorial/tutorial_kantegassoforbitbucket_app.png) 

1. <span data-ttu-id="bf129-283">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="bf129-283">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="bf129-285">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="bf129-285">Click **Add** button.</span></span> <span data-ttu-id="bf129-286">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="bf129-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="bf129-288">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="bf129-288">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="bf129-289">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="bf129-289">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="bf129-290">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="bf129-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bf129-291">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="bf129-291">Testing single sign-on</span></span>

<span data-ttu-id="bf129-292">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="bf129-292">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bf129-293">When you click the Kantega SSO for Bitbucket tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for Bitbucket application.</span><span class="sxs-lookup"><span data-stu-id="bf129-293">When you click the Kantega SSO for Bitbucket tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for Bitbucket application.</span></span>
<span data-ttu-id="bf129-294">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bf129-294">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bf129-295">Additional resources</span><span class="sxs-lookup"><span data-stu-id="bf129-295">Additional resources</span></span>

* [<span data-ttu-id="bf129-296">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bf129-296">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="bf129-297">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bf129-297">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/kantegassoforbitbucket-tutorial/tutorial_general_01.png
[2]: ./media/kantegassoforbitbucket-tutorial/tutorial_general_02.png
[3]: ./media/kantegassoforbitbucket-tutorial/tutorial_general_03.png
[4]: ./media/kantegassoforbitbucket-tutorial/tutorial_general_04.png

[100]: ./media/kantegassoforbitbucket-tutorial/tutorial_general_100.png

[200]: ./media/kantegassoforbitbucket-tutorial/tutorial_general_200.png
[201]: ./media/kantegassoforbitbucket-tutorial/tutorial_general_201.png
[202]: ./media/kantegassoforbitbucket-tutorial/tutorial_general_202.png
[203]: ./media/kantegassoforbitbucket-tutorial/tutorial_general_203.png

