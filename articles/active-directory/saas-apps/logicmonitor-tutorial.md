---
title: 'Tutorial: Azure Active Directory integration with LogicMonitor | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and LogicMonitor.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 496156c3-0e22-4492-b36f-2c29c055e087
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2018
ms.author: jeedes
ms.openlocfilehash: a6bc220d15e720662eaa9605421e21ccb99892ab
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870253"
---
# <a name="tutorial-azure-active-directory-integration-with-logicmonitor"></a><span data-ttu-id="ad593-103">Tutorial: Azure Active Directory integration with LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="ad593-103">Tutorial: Azure Active Directory integration with LogicMonitor</span></span>

<span data-ttu-id="ad593-104">In this tutorial, you learn how to integrate LogicMonitor with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ad593-104">In this tutorial, you learn how to integrate LogicMonitor with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ad593-105">Integrating LogicMonitor with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ad593-105">Integrating LogicMonitor with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ad593-106">You can control in Azure AD who has access to LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="ad593-106">You can control in Azure AD who has access to LogicMonitor</span></span>
- <span data-ttu-id="ad593-107">You can enable your users to automatically get signed-on to LogicMonitor (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="ad593-107">You can enable your users to automatically get signed-on to LogicMonitor (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ad593-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ad593-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ad593-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="ad593-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad593-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ad593-110">Prerequisites</span></span>

<span data-ttu-id="ad593-111">To configure Azure AD integration with LogicMonitor, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="ad593-111">To configure Azure AD integration with LogicMonitor, you need the following items:</span></span>

- <span data-ttu-id="ad593-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="ad593-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ad593-113">A LogicMonitor single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ad593-113">A LogicMonitor single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ad593-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="ad593-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ad593-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="ad593-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ad593-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="ad593-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ad593-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ad593-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ad593-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="ad593-118">Scenario description</span></span>
<span data-ttu-id="ad593-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="ad593-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ad593-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="ad593-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ad593-121">Adding LogicMonitor from the gallery</span><span class="sxs-lookup"><span data-stu-id="ad593-121">Adding LogicMonitor from the gallery</span></span>
1. <span data-ttu-id="ad593-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ad593-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-logicmonitor-from-the-gallery"></a><span data-ttu-id="ad593-123">Adding LogicMonitor from the gallery</span><span class="sxs-lookup"><span data-stu-id="ad593-123">Adding LogicMonitor from the gallery</span></span>
<span data-ttu-id="ad593-124">To configure the integration of LogicMonitor into Azure AD, you need to add LogicMonitor from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="ad593-124">To configure the integration of LogicMonitor into Azure AD, you need to add LogicMonitor from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ad593-125">**To add LogicMonitor from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ad593-125">**To add LogicMonitor from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ad593-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ad593-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="ad593-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="ad593-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ad593-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ad593-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="ad593-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="ad593-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="ad593-133">In the search box, type **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="ad593-133">In the search box, type **LogicMonitor**.</span></span>

    ![Creating an Azure AD test user](./media/logicmonitor-tutorial/tutorial_logicmonitor_search.png)

1. <span data-ttu-id="ad593-135">In the results panel, select **LogicMonitor**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="ad593-135">In the results panel, select **LogicMonitor**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/logicmonitor-tutorial/tutorial_logicmonitor_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ad593-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ad593-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ad593-138">In this section, you configure and test Azure AD single sign-on with LogicMonitor based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ad593-138">In this section, you configure and test Azure AD single sign-on with LogicMonitor based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ad593-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LogicMonitor is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad593-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LogicMonitor is to a user in Azure AD.</span></span> <span data-ttu-id="ad593-140">In other words, a link relationship between an Azure AD user and the related user in LogicMonitor needs to be established.</span><span class="sxs-lookup"><span data-stu-id="ad593-140">In other words, a link relationship between an Azure AD user and the related user in LogicMonitor needs to be established.</span></span>

<span data-ttu-id="ad593-141">In LogicMonitor, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="ad593-141">In LogicMonitor, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ad593-142">To configure and test Azure AD single sign-on with LogicMonitor, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ad593-142">To configure and test Azure AD single sign-on with LogicMonitor, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ad593-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="ad593-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="ad593-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad593-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="ad593-145">**[Creating a LogicMonitor test user](#creating-a-logicmonitor-test-user)** - to have a counterpart of Britta Simon in LogicMonitor that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="ad593-145">**[Creating a LogicMonitor test user](#creating-a-logicmonitor-test-user)** - to have a counterpart of Britta Simon in LogicMonitor that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="ad593-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ad593-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="ad593-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="ad593-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ad593-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ad593-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ad593-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LogicMonitor application.</span><span class="sxs-lookup"><span data-stu-id="ad593-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LogicMonitor application.</span></span>

<span data-ttu-id="ad593-150">**To configure Azure AD single sign-on with LogicMonitor, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ad593-150">**To configure Azure AD single sign-on with LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="ad593-151">In the Azure portal, on the **LogicMonitor** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ad593-151">In the Azure portal, on the **LogicMonitor** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="ad593-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ad593-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/logicmonitor-tutorial/tutorial_logicmonitor_samlbase.png)

1. <span data-ttu-id="ad593-155">On the **LogicMonitor Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ad593-155">On the **LogicMonitor Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/logicmonitor-tutorial/tutorial_logicmonitor_url.png)

    <span data-ttu-id="ad593-157">a.</span><span class="sxs-lookup"><span data-stu-id="ad593-157">a.</span></span> <span data-ttu-id="ad593-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="ad593-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    <span data-ttu-id="ad593-159">b.</span><span class="sxs-lookup"><span data-stu-id="ad593-159">b.</span></span> <span data-ttu-id="ad593-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="ad593-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ad593-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="ad593-161">These values are not real.</span></span> <span data-ttu-id="ad593-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="ad593-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ad593-163">Contact [LogicMonitor Client support team](https://www.logicmonitor.com/contact/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="ad593-163">Contact [LogicMonitor Client support team](https://www.logicmonitor.com/contact/) to get these values.</span></span> 
 


1. <span data-ttu-id="ad593-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="ad593-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/logicmonitor-tutorial/tutorial_logicmonitor_certificate.png) 

1. <span data-ttu-id="ad593-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="ad593-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/logicmonitor-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="ad593-168">Log in to your **LogicMonitor** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ad593-168">Log in to your **LogicMonitor** company site as an administrator.</span></span>

1. <span data-ttu-id="ad593-169">In the menu on the top, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="ad593-169">In the menu on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="ad593-170">![Settings](./media/logicmonitor-tutorial/ic790052.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="ad593-170">![Settings](./media/logicmonitor-tutorial/ic790052.png "Settings")</span></span>

1. <span data-ttu-id="ad593-171">In the navigation bat on the left side, click **Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="ad593-171">In the navigation bat on the left side, click **Single Sign On**</span></span>
   
    <span data-ttu-id="ad593-172">![Single Sign-On](./media/logicmonitor-tutorial/ic790053.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="ad593-172">![Single Sign-On](./media/logicmonitor-tutorial/ic790053.png "Single Sign-On")</span></span>

1. <span data-ttu-id="ad593-173">In the **Single Sign-on (SSO) settings** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ad593-173">In the **Single Sign-on (SSO) settings** section, perform the following steps:</span></span>
   
    <span data-ttu-id="ad593-174">![Single Sign-On Settings](./media/logicmonitor-tutorial/ic790054.png "Single Sign-On Settings")</span><span class="sxs-lookup"><span data-stu-id="ad593-174">![Single Sign-On Settings](./media/logicmonitor-tutorial/ic790054.png "Single Sign-On Settings")</span></span>
   
    <span data-ttu-id="ad593-175">a.</span><span class="sxs-lookup"><span data-stu-id="ad593-175">a.</span></span> <span data-ttu-id="ad593-176">Select **Enable Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="ad593-176">Select **Enable Single Sign-on**.</span></span>

    <span data-ttu-id="ad593-177">b.</span><span class="sxs-lookup"><span data-stu-id="ad593-177">b.</span></span> <span data-ttu-id="ad593-178">As **Default Role Assignment**, select **readonly**.</span><span class="sxs-lookup"><span data-stu-id="ad593-178">As **Default Role Assignment**, select **readonly**.</span></span>
   
    <span data-ttu-id="ad593-179">c.</span><span class="sxs-lookup"><span data-stu-id="ad593-179">c.</span></span> <span data-ttu-id="ad593-180">Open the downloaded metadata file in notepad, and then paste content of the file into the **Identity Provider Metadata** textbox.</span><span class="sxs-lookup"><span data-stu-id="ad593-180">Open the downloaded metadata file in notepad, and then paste content of the file into the **Identity Provider Metadata** textbox.</span></span>
   
    <span data-ttu-id="ad593-181">d.</span><span class="sxs-lookup"><span data-stu-id="ad593-181">d.</span></span> <span data-ttu-id="ad593-182">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="ad593-182">Click **Save Changes**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ad593-183">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ad593-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="ad593-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad593-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="ad593-186">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ad593-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ad593-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="ad593-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/logicmonitor-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="ad593-189">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="ad593-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/logicmonitor-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="ad593-191">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="ad593-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/logicmonitor-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="ad593-193">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ad593-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/logicmonitor-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ad593-195">a.</span><span class="sxs-lookup"><span data-stu-id="ad593-195">a.</span></span> <span data-ttu-id="ad593-196">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ad593-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ad593-197">b.</span><span class="sxs-lookup"><span data-stu-id="ad593-197">b.</span></span> <span data-ttu-id="ad593-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ad593-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ad593-199">c.</span><span class="sxs-lookup"><span data-stu-id="ad593-199">c.</span></span> <span data-ttu-id="ad593-200">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="ad593-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ad593-201">d.</span><span class="sxs-lookup"><span data-stu-id="ad593-201">d.</span></span> <span data-ttu-id="ad593-202">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ad593-202">Click **Create**.</span></span>
 
### <a name="creating-a-logicmonitor-test-user"></a><span data-ttu-id="ad593-203">Creating a LogicMonitor test user</span><span class="sxs-lookup"><span data-stu-id="ad593-203">Creating a LogicMonitor test user</span></span>

<span data-ttu-id="ad593-204">For Azure AD users to be able to sign in, they must be provisioned to the LogicMonitor application using their Azure Active Directory user names.</span><span class="sxs-lookup"><span data-stu-id="ad593-204">For Azure AD users to be able to sign in, they must be provisioned to the LogicMonitor application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="ad593-205">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ad593-205">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="ad593-206">Log in to your LogicMonitor company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ad593-206">Log in to your LogicMonitor company site as an administrator.</span></span>

1. <span data-ttu-id="ad593-207">In the menu on the top, click **Settings**, and then click **Roles and Users**.</span><span class="sxs-lookup"><span data-stu-id="ad593-207">In the menu on the top, click **Settings**, and then click **Roles and Users**.</span></span>
   
    <span data-ttu-id="ad593-208">![Roles and Users](./media/logicmonitor-tutorial/ic790056.png "Roles and Users")</span><span class="sxs-lookup"><span data-stu-id="ad593-208">![Roles and Users](./media/logicmonitor-tutorial/ic790056.png "Roles and Users")</span></span>

1. <span data-ttu-id="ad593-209">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="ad593-209">Click **Add**.</span></span>

1. <span data-ttu-id="ad593-210">In the **Add an account** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ad593-210">In the **Add an account** section, perform the following steps:</span></span>
   
    <span data-ttu-id="ad593-211">![Add an account](./media/logicmonitor-tutorial/ic790057.png "Add an account")</span><span class="sxs-lookup"><span data-stu-id="ad593-211">![Add an account](./media/logicmonitor-tutorial/ic790057.png "Add an account")</span></span>
   
    <span data-ttu-id="ad593-212">a.</span><span class="sxs-lookup"><span data-stu-id="ad593-212">a.</span></span> <span data-ttu-id="ad593-213">Type the **Username**, **Email**, **Password**, and **Retype password** values of the Azure Active Directory user you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="ad593-213">Type the **Username**, **Email**, **Password**, and **Retype password** values of the Azure Active Directory user you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="ad593-214">b.</span><span class="sxs-lookup"><span data-stu-id="ad593-214">b.</span></span> <span data-ttu-id="ad593-215">Select **Roles**, **View Permissions**, and the **Status**.</span><span class="sxs-lookup"><span data-stu-id="ad593-215">Select **Roles**, **View Permissions**, and the **Status**.</span></span>
   
    <span data-ttu-id="ad593-216">c.</span><span class="sxs-lookup"><span data-stu-id="ad593-216">c.</span></span> <span data-ttu-id="ad593-217">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="ad593-217">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="ad593-218">You can use any other LogicMonitor user account creation tools or APIs provided by LogicMonitor to provision Azure Active Directory user accounts.</span><span class="sxs-lookup"><span data-stu-id="ad593-218">You can use any other LogicMonitor user account creation tools or APIs provided by LogicMonitor to provision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ad593-219">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ad593-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ad593-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="ad593-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LogicMonitor.</span></span>

![Assign User][200] 

<span data-ttu-id="ad593-222">**To assign Britta Simon to LogicMonitor, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ad593-222">**To assign Britta Simon to LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="ad593-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="ad593-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="ad593-225">In the applications list, select **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="ad593-225">In the applications list, select **LogicMonitor**.</span></span>

    ![Configure Single Sign-On](./media/logicmonitor-tutorial/tutorial_logicmonitor_app.png) 

1. <span data-ttu-id="ad593-227">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="ad593-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="ad593-229">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="ad593-229">Click **Add** button.</span></span> <span data-ttu-id="ad593-230">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ad593-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="ad593-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="ad593-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="ad593-233">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="ad593-233">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="ad593-234">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="ad593-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ad593-235">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="ad593-235">Testing single sign-on</span></span>

<span data-ttu-id="ad593-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ad593-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="ad593-237">When you click the LogicMonitor tile in the Access Panel, you should get automatically signed-on to your LogicMonitor application.</span><span class="sxs-lookup"><span data-stu-id="ad593-237">When you click the LogicMonitor tile in the Access Panel, you should get automatically signed-on to your LogicMonitor application.</span></span>
<span data-ttu-id="ad593-238">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ad593-238">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ad593-239">Additional resources</span><span class="sxs-lookup"><span data-stu-id="ad593-239">Additional resources</span></span>

* [<span data-ttu-id="ad593-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ad593-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="ad593-241">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ad593-241">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/logicmonitor-tutorial/tutorial_general_01.png
[2]: ./media/logicmonitor-tutorial/tutorial_general_02.png
[3]: ./media/logicmonitor-tutorial/tutorial_general_03.png
[4]: ./media/logicmonitor-tutorial/tutorial_general_04.png

[100]: ./media/logicmonitor-tutorial/tutorial_general_100.png

[200]: ./media/logicmonitor-tutorial/tutorial_general_200.png
[201]: ./media/logicmonitor-tutorial/tutorial_general_201.png
[202]: ./media/logicmonitor-tutorial/tutorial_general_202.png
[203]: ./media/logicmonitor-tutorial/tutorial_general_203.png

