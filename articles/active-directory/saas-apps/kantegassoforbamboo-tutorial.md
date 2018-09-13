---
title: 'Tutorial: Azure Active Directory integration with Kantega SSO for Bamboo | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Kantega SSO for Bamboo.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: e238b574-9e9b-43b7-ab98-d2a87ff89d48
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: ceab1293b5bd1fbae9088783651d0effa8c5a78a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857882"
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-bamboo"></a><span data-ttu-id="76c93-103">Tutorial: Azure Active Directory integration with Kantega SSO for Bamboo</span><span class="sxs-lookup"><span data-stu-id="76c93-103">Tutorial: Azure Active Directory integration with Kantega SSO for Bamboo</span></span>

<span data-ttu-id="76c93-104">In this tutorial, you learn how to integrate Kantega SSO for Bamboo with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="76c93-104">In this tutorial, you learn how to integrate Kantega SSO for Bamboo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="76c93-105">Integrating Kantega SSO for Bamboo with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="76c93-105">Integrating Kantega SSO for Bamboo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="76c93-106">You can control in Azure AD who has access to Kantega SSO for Bamboo</span><span class="sxs-lookup"><span data-stu-id="76c93-106">You can control in Azure AD who has access to Kantega SSO for Bamboo</span></span>
- <span data-ttu-id="76c93-107">You can enable your users to automatically get signed-on to Kantega SSO for Bamboo (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="76c93-107">You can enable your users to automatically get signed-on to Kantega SSO for Bamboo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="76c93-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="76c93-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="76c93-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="76c93-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76c93-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="76c93-110">Prerequisites</span></span>

<span data-ttu-id="76c93-111">To configure Azure AD integration with Kantega SSO for Bamboo, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="76c93-111">To configure Azure AD integration with Kantega SSO for Bamboo, you need the following items:</span></span>

- <span data-ttu-id="76c93-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="76c93-112">An Azure AD subscription</span></span>
- <span data-ttu-id="76c93-113">A Kantega SSO for Bamboo single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="76c93-113">A Kantega SSO for Bamboo single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="76c93-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="76c93-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="76c93-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="76c93-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="76c93-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="76c93-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="76c93-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="76c93-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="76c93-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="76c93-118">Scenario description</span></span>
<span data-ttu-id="76c93-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="76c93-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="76c93-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="76c93-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="76c93-121">Adding Kantega SSO for Bamboo from the gallery</span><span class="sxs-lookup"><span data-stu-id="76c93-121">Adding Kantega SSO for Bamboo from the gallery</span></span>
1. <span data-ttu-id="76c93-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="76c93-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-bamboo-from-the-gallery"></a><span data-ttu-id="76c93-123">Adding Kantega SSO for Bamboo from the gallery</span><span class="sxs-lookup"><span data-stu-id="76c93-123">Adding Kantega SSO for Bamboo from the gallery</span></span>
<span data-ttu-id="76c93-124">To configure the integration of Kantega SSO for Bamboo into Azure AD, you need to add Kantega SSO for Bamboo from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="76c93-124">To configure the integration of Kantega SSO for Bamboo into Azure AD, you need to add Kantega SSO for Bamboo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="76c93-125">**To add Kantega SSO for Bamboo from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="76c93-125">**To add Kantega SSO for Bamboo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="76c93-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="76c93-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="76c93-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="76c93-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="76c93-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="76c93-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="76c93-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="76c93-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="76c93-133">In the search box, type **Kantega SSO for Bamboo**.</span><span class="sxs-lookup"><span data-stu-id="76c93-133">In the search box, type **Kantega SSO for Bamboo**.</span></span>

    ![Creating an Azure AD test user](./media/kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_search.png)

1. <span data-ttu-id="76c93-135">In the results panel, select **Kantega SSO for Bamboo**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="76c93-135">In the results panel, select **Kantega SSO for Bamboo**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="76c93-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="76c93-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="76c93-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Bamboo based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="76c93-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Bamboo based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="76c93-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for Bamboo is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76c93-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for Bamboo is to a user in Azure AD.</span></span> <span data-ttu-id="76c93-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for Bamboo needs to be established.</span><span class="sxs-lookup"><span data-stu-id="76c93-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for Bamboo needs to be established.</span></span>

<span data-ttu-id="76c93-141">In Kantega SSO for Bamboo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="76c93-141">In Kantega SSO for Bamboo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="76c93-142">To configure and test Azure AD single sign-on with Kantega SSO for Bamboo, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="76c93-142">To configure and test Azure AD single sign-on with Kantega SSO for Bamboo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="76c93-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="76c93-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="76c93-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="76c93-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="76c93-145">**[Creating a Kantega SSO for Bamboo test user](#creating-a-kantega-sso-for-bamboo-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for Bamboo that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="76c93-145">**[Creating a Kantega SSO for Bamboo test user](#creating-a-kantega-sso-for-bamboo-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for Bamboo that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="76c93-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="76c93-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="76c93-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="76c93-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="76c93-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="76c93-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="76c93-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for Bamboo application.</span><span class="sxs-lookup"><span data-stu-id="76c93-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for Bamboo application.</span></span>

<span data-ttu-id="76c93-150">**To configure Azure AD single sign-on with Kantega SSO for Bamboo, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="76c93-150">**To configure Azure AD single sign-on with Kantega SSO for Bamboo, perform the following steps:**</span></span>

1. <span data-ttu-id="76c93-151">In the Azure portal, on the **Kantega SSO for Bamboo** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="76c93-151">In the Azure portal, on the **Kantega SSO for Bamboo** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="76c93-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="76c93-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_samlbase.png)

1. <span data-ttu-id="76c93-155">In **IDP** initiated mode, on the **Kantega SSO for Bamboo Domain and URLs** section perform the following step :</span><span class="sxs-lookup"><span data-stu-id="76c93-155">In **IDP** initiated mode, on the **Kantega SSO for Bamboo Domain and URLs** section perform the following step :</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url1.png)
    
    <span data-ttu-id="76c93-157">a.</span><span class="sxs-lookup"><span data-stu-id="76c93-157">a.</span></span> <span data-ttu-id="76c93-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="76c93-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="76c93-159">b.</span><span class="sxs-lookup"><span data-stu-id="76c93-159">b.</span></span> <span data-ttu-id="76c93-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="76c93-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

1. <span data-ttu-id="76c93-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform the following step :</span><span class="sxs-lookup"><span data-stu-id="76c93-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform the following step :</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url2.png)
    
    <span data-ttu-id="76c93-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="76c93-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="76c93-164">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="76c93-164">These values are not real.</span></span> <span data-ttu-id="76c93-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="76c93-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="76c93-166">These values are recieved during the configuration of Bamboo plugin which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="76c93-166">These values are recieved during the configuration of Bamboo plugin which is explained later in the tutorial.</span></span>

1. <span data-ttu-id="76c93-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="76c93-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_certificate.png) 

1. <span data-ttu-id="76c93-169">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="76c93-169">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbamboo-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="76c93-171">In a different web browser window, log in to your Bamboo  on-premises server as an administrator.</span><span class="sxs-lookup"><span data-stu-id="76c93-171">In a different web browser window, log in to your Bamboo  on-premises server as an administrator.</span></span>

1. <span data-ttu-id="76c93-172">Hover on cog and click the **Add-ons**.</span><span class="sxs-lookup"><span data-stu-id="76c93-172">Hover on cog and click the **Add-ons**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbamboo-tutorial/addon1.png)

1. <span data-ttu-id="76c93-174">Under Add-ons tab section, click **Find new add-ons**.</span><span class="sxs-lookup"><span data-stu-id="76c93-174">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="76c93-175">Search **Kantega SSO for Bamboo (SAML & Kerberos)** and click **Install** button to install the new SAML plugin.</span><span class="sxs-lookup"><span data-stu-id="76c93-175">Search **Kantega SSO for Bamboo (SAML & Kerberos)** and click **Install** button to install the new SAML plugin.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbamboo-tutorial/addon2.png)

1. <span data-ttu-id="76c93-177">The plugin installation will start.</span><span class="sxs-lookup"><span data-stu-id="76c93-177">The plugin installation will start.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbamboo-tutorial/addon21.png)

1. <span data-ttu-id="76c93-179">Once the installation is complete.</span><span class="sxs-lookup"><span data-stu-id="76c93-179">Once the installation is complete.</span></span> <span data-ttu-id="76c93-180">Click **Close**.</span><span class="sxs-lookup"><span data-stu-id="76c93-180">Click **Close**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbamboo-tutorial/addon33.png)

1.  <span data-ttu-id="76c93-182">Click **Manage**.</span><span class="sxs-lookup"><span data-stu-id="76c93-182">Click **Manage**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbamboo-tutorial/addon34.png)
    
1. <span data-ttu-id="76c93-184">Click **Configure** to configure the new plugin.</span><span class="sxs-lookup"><span data-stu-id="76c93-184">Click **Configure** to configure the new plugin.</span></span> 

    ![Configure Single Sign-On](./media/kantegassoforbamboo-tutorial/addon3.png)

1. <span data-ttu-id="76c93-186">In the **SAML** section.</span><span class="sxs-lookup"><span data-stu-id="76c93-186">In the **SAML** section.</span></span> <span data-ttu-id="76c93-187">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span><span class="sxs-lookup"><span data-stu-id="76c93-187">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbamboo-tutorial/addon4.png)

1. <span data-ttu-id="76c93-189">Select subscription level as **Basic**.</span><span class="sxs-lookup"><span data-stu-id="76c93-189">Select subscription level as **Basic**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbamboo-tutorial/addon5.png)

1. <span data-ttu-id="76c93-191">On the **App properties** section, perform following steps:</span><span class="sxs-lookup"><span data-stu-id="76c93-191">On the **App properties** section, perform following steps:</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbamboo-tutorial/addon6.png)

    <span data-ttu-id="76c93-193">a.</span><span class="sxs-lookup"><span data-stu-id="76c93-193">a.</span></span> <span data-ttu-id="76c93-194">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for Bamboo Domain and URLs** section in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="76c93-194">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for Bamboo Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="76c93-195">b.</span><span class="sxs-lookup"><span data-stu-id="76c93-195">b.</span></span> <span data-ttu-id="76c93-196">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="76c93-196">Click **Next**.</span></span>

1. <span data-ttu-id="76c93-197">On the **Metadata import** section, perform following steps:</span><span class="sxs-lookup"><span data-stu-id="76c93-197">On the **Metadata import** section, perform following steps:</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbamboo-tutorial/addon7.png)

    <span data-ttu-id="76c93-199">a.</span><span class="sxs-lookup"><span data-stu-id="76c93-199">a.</span></span> <span data-ttu-id="76c93-200">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="76c93-200">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="76c93-201">b.</span><span class="sxs-lookup"><span data-stu-id="76c93-201">b.</span></span> <span data-ttu-id="76c93-202">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="76c93-202">Click **Next**.</span></span>

1. <span data-ttu-id="76c93-203">On the **Name and SSO location** section, perform following steps:</span><span class="sxs-lookup"><span data-stu-id="76c93-203">On the **Name and SSO location** section, perform following steps:</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbamboo-tutorial/addon8.png)

    <span data-ttu-id="76c93-205">a.</span><span class="sxs-lookup"><span data-stu-id="76c93-205">a.</span></span> <span data-ttu-id="76c93-206">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span><span class="sxs-lookup"><span data-stu-id="76c93-206">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="76c93-207">b.</span><span class="sxs-lookup"><span data-stu-id="76c93-207">b.</span></span> <span data-ttu-id="76c93-208">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="76c93-208">Click **Next**.</span></span>

1. <span data-ttu-id="76c93-209">Verify the Signing certificate and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="76c93-209">Verify the Signing certificate and click **Next**.</span></span>   

    ![Configure Single Sign-On](./media/kantegassoforbamboo-tutorial/addon9.png)

1. <span data-ttu-id="76c93-211">On the **Bamboo user accounts** section, perform following steps:</span><span class="sxs-lookup"><span data-stu-id="76c93-211">On the **Bamboo user accounts** section, perform following steps:</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbamboo-tutorial/addon10.png)

    <span data-ttu-id="76c93-213">a.</span><span class="sxs-lookup"><span data-stu-id="76c93-213">a.</span></span> <span data-ttu-id="76c93-214">Select **Create users in Bamboo's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span><span class="sxs-lookup"><span data-stu-id="76c93-214">Select **Create users in Bamboo's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span></span> <span data-ttu-id="76c93-215">of groups separated by comma).</span><span class="sxs-lookup"><span data-stu-id="76c93-215">of groups separated by comma).</span></span>

    <span data-ttu-id="76c93-216">b.</span><span class="sxs-lookup"><span data-stu-id="76c93-216">b.</span></span> <span data-ttu-id="76c93-217">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="76c93-217">Click **Next**.</span></span>

1. <span data-ttu-id="76c93-218">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="76c93-218">Click **Finish**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbamboo-tutorial/addon11.png)

1. <span data-ttu-id="76c93-220">On the **Known domains for Azure AD** section, perform following steps:</span><span class="sxs-lookup"><span data-stu-id="76c93-220">On the **Known domains for Azure AD** section, perform following steps:</span></span>  

    ![Configure Single Sign-On](./media/kantegassoforbamboo-tutorial/addon12.png)

    <span data-ttu-id="76c93-222">a.</span><span class="sxs-lookup"><span data-stu-id="76c93-222">a.</span></span> <span data-ttu-id="76c93-223">Select **Known domains** from the left panel of the page.</span><span class="sxs-lookup"><span data-stu-id="76c93-223">Select **Known domains** from the left panel of the page.</span></span>

    <span data-ttu-id="76c93-224">b.</span><span class="sxs-lookup"><span data-stu-id="76c93-224">b.</span></span> <span data-ttu-id="76c93-225">Enter domain name in the **Known domains** textbox.</span><span class="sxs-lookup"><span data-stu-id="76c93-225">Enter domain name in the **Known domains** textbox.</span></span>

    <span data-ttu-id="76c93-226">c.</span><span class="sxs-lookup"><span data-stu-id="76c93-226">c.</span></span> <span data-ttu-id="76c93-227">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="76c93-227">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="76c93-228">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="76c93-228">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="76c93-229">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="76c93-229">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="76c93-230">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="76c93-230">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="76c93-231">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="76c93-231">Creating an Azure AD test user</span></span>
<span data-ttu-id="76c93-232">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="76c93-232">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="76c93-234">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="76c93-234">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="76c93-235">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="76c93-235">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/kantegassoforbamboo-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="76c93-237">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="76c93-237">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/kantegassoforbamboo-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="76c93-239">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="76c93-239">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/kantegassoforbamboo-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="76c93-241">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="76c93-241">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/kantegassoforbamboo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="76c93-243">a.</span><span class="sxs-lookup"><span data-stu-id="76c93-243">a.</span></span> <span data-ttu-id="76c93-244">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="76c93-244">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="76c93-245">b.</span><span class="sxs-lookup"><span data-stu-id="76c93-245">b.</span></span> <span data-ttu-id="76c93-246">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="76c93-246">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="76c93-247">c.</span><span class="sxs-lookup"><span data-stu-id="76c93-247">c.</span></span> <span data-ttu-id="76c93-248">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="76c93-248">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="76c93-249">d.</span><span class="sxs-lookup"><span data-stu-id="76c93-249">d.</span></span> <span data-ttu-id="76c93-250">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="76c93-250">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-bamboo-test-user"></a><span data-ttu-id="76c93-251">Creating a Kantega SSO for Bamboo test user</span><span class="sxs-lookup"><span data-stu-id="76c93-251">Creating a Kantega SSO for Bamboo test user</span></span>

<span data-ttu-id="76c93-252">To enable Azure AD users to log in to Bamboo, they must be provisioned into Bamboo.</span><span class="sxs-lookup"><span data-stu-id="76c93-252">To enable Azure AD users to log in to Bamboo, they must be provisioned into Bamboo.</span></span> <span data-ttu-id="76c93-253">In Kantega SSO for Bamboo, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="76c93-253">In Kantega SSO for Bamboo, provisioning is a manual task.</span></span>

<span data-ttu-id="76c93-254">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="76c93-254">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="76c93-255">Log in to your Bamboo on-premises server as an administrator.</span><span class="sxs-lookup"><span data-stu-id="76c93-255">Log in to your Bamboo on-premises server as an administrator.</span></span>

1. <span data-ttu-id="76c93-256">Hover on cog and click the **User management**.</span><span class="sxs-lookup"><span data-stu-id="76c93-256">Hover on cog and click the **User management**.</span></span>

    ![Add Employee](./media/kantegassoforbamboo-tutorial/user1.png) 

1. <span data-ttu-id="76c93-258">Click **Users**.</span><span class="sxs-lookup"><span data-stu-id="76c93-258">Click **Users**.</span></span> <span data-ttu-id="76c93-259">Under the **Add user** section, Perform follwing steps:</span><span class="sxs-lookup"><span data-stu-id="76c93-259">Under the **Add user** section, Perform follwing steps:</span></span>

    ![Add Employee](./media/kantegassoforbamboo-tutorial/user2.png) 

    <span data-ttu-id="76c93-261">a.</span><span class="sxs-lookup"><span data-stu-id="76c93-261">a.</span></span> <span data-ttu-id="76c93-262">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="76c93-262">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="76c93-263">b.</span><span class="sxs-lookup"><span data-stu-id="76c93-263">b.</span></span> <span data-ttu-id="76c93-264">In the **Password** textbox, type the password of user.</span><span class="sxs-lookup"><span data-stu-id="76c93-264">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="76c93-265">c.</span><span class="sxs-lookup"><span data-stu-id="76c93-265">c.</span></span> <span data-ttu-id="76c93-266">In the **Confirm Password** textbox, reenter the password of user.</span><span class="sxs-lookup"><span data-stu-id="76c93-266">In the **Confirm Password** textbox, reenter the password of user.</span></span>
    
    <span data-ttu-id="76c93-267">d.</span><span class="sxs-lookup"><span data-stu-id="76c93-267">d.</span></span> <span data-ttu-id="76c93-268">In the **Full Name** textbox, type full name of the user like Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="76c93-268">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>
    
    <span data-ttu-id="76c93-269">e.</span><span class="sxs-lookup"><span data-stu-id="76c93-269">e.</span></span> <span data-ttu-id="76c93-270">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="76c93-270">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="76c93-271">f.</span><span class="sxs-lookup"><span data-stu-id="76c93-271">f.</span></span> <span data-ttu-id="76c93-272">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="76c93-272">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="76c93-273">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="76c93-273">Assigning the Azure AD test user</span></span>

<span data-ttu-id="76c93-274">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for Bamboo.</span><span class="sxs-lookup"><span data-stu-id="76c93-274">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for Bamboo.</span></span>

![Assign User][200] 

<span data-ttu-id="76c93-276">**To assign Britta Simon to Kantega SSO for Bamboo, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="76c93-276">**To assign Britta Simon to Kantega SSO for Bamboo, perform the following steps:**</span></span>

1. <span data-ttu-id="76c93-277">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="76c93-277">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="76c93-279">In the applications list, select **Kantega SSO for Bamboo**.</span><span class="sxs-lookup"><span data-stu-id="76c93-279">In the applications list, select **Kantega SSO for Bamboo**.</span></span>

    ![Configure Single Sign-On](./media/kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_app.png) 

1. <span data-ttu-id="76c93-281">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="76c93-281">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="76c93-283">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="76c93-283">Click **Add** button.</span></span> <span data-ttu-id="76c93-284">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="76c93-284">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="76c93-286">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="76c93-286">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="76c93-287">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="76c93-287">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="76c93-288">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="76c93-288">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="76c93-289">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="76c93-289">Testing single sign-on</span></span>

<span data-ttu-id="76c93-290">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="76c93-290">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="76c93-291">When you click the Kantega SSO for Bamboo tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for Bamboo application.</span><span class="sxs-lookup"><span data-stu-id="76c93-291">When you click the Kantega SSO for Bamboo tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for Bamboo application.</span></span>
<span data-ttu-id="76c93-292">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="76c93-292">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="76c93-293">Additional resources</span><span class="sxs-lookup"><span data-stu-id="76c93-293">Additional resources</span></span>

* [<span data-ttu-id="76c93-294">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="76c93-294">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="76c93-295">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="76c93-295">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/kantegassoforbamboo-tutorial/tutorial_general_01.png
[2]: ./media/kantegassoforbamboo-tutorial/tutorial_general_02.png
[3]: ./media/kantegassoforbamboo-tutorial/tutorial_general_03.png
[4]: ./media/kantegassoforbamboo-tutorial/tutorial_general_04.png

[100]: ./media/kantegassoforbamboo-tutorial/tutorial_general_100.png

[200]: ./media/kantegassoforbamboo-tutorial/tutorial_general_200.png
[201]: ./media/kantegassoforbamboo-tutorial/tutorial_general_201.png
[202]: ./media/kantegassoforbamboo-tutorial/tutorial_general_202.png
[203]: ./media/kantegassoforbamboo-tutorial/tutorial_general_203.png

