---
title: 'Tutorial: Azure Active Directory integration with SensoScientific Wireless Temperature Monitoring System | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SensoScientific Wireless Temperature Monitoring System.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 139a40f339c2f403999f1c3b7fe65192d45c84fd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856607"
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a><span data-ttu-id="bc150-103">Tutorial: Azure Active Directory integration with SensoScientific Wireless Temperature Monitoring System</span><span class="sxs-lookup"><span data-stu-id="bc150-103">Tutorial: Azure Active Directory integration with SensoScientific Wireless Temperature Monitoring System</span></span>

<span data-ttu-id="bc150-104">In this tutorial, you learn how to integrate SensoScientific Wireless Temperature Monitoring System with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bc150-104">In this tutorial, you learn how to integrate SensoScientific Wireless Temperature Monitoring System with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bc150-105">Integrating SensoScientific Wireless Temperature Monitoring System with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="bc150-105">Integrating SensoScientific Wireless Temperature Monitoring System with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bc150-106">You can control in Azure AD who has access to SensoScientific Wireless Temperature Monitoring System</span><span class="sxs-lookup"><span data-stu-id="bc150-106">You can control in Azure AD who has access to SensoScientific Wireless Temperature Monitoring System</span></span>
- <span data-ttu-id="bc150-107">You can enable your users to automatically get signed-on to SensoScientific Wireless Temperature Monitoring System (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="bc150-107">You can enable your users to automatically get signed-on to SensoScientific Wireless Temperature Monitoring System (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bc150-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="bc150-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bc150-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="bc150-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc150-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bc150-110">Prerequisites</span></span>

<span data-ttu-id="bc150-111">To configure Azure AD integration with SensoScientific Wireless Temperature Monitoring System, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="bc150-111">To configure Azure AD integration with SensoScientific Wireless Temperature Monitoring System, you need the following items:</span></span>

- <span data-ttu-id="bc150-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="bc150-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bc150-113">A SensoScientific Wireless Temperature Monitoring System single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="bc150-113">A SensoScientific Wireless Temperature Monitoring System single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bc150-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="bc150-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bc150-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="bc150-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bc150-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="bc150-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bc150-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bc150-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bc150-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="bc150-118">Scenario description</span></span>
<span data-ttu-id="bc150-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="bc150-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bc150-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="bc150-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bc150-121">Adding SensoScientific Wireless Temperature Monitoring System from the gallery</span><span class="sxs-lookup"><span data-stu-id="bc150-121">Adding SensoScientific Wireless Temperature Monitoring System from the gallery</span></span>
1. <span data-ttu-id="bc150-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bc150-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-the-gallery"></a><span data-ttu-id="bc150-123">Adding SensoScientific Wireless Temperature Monitoring System from the gallery</span><span class="sxs-lookup"><span data-stu-id="bc150-123">Adding SensoScientific Wireless Temperature Monitoring System from the gallery</span></span>
<span data-ttu-id="bc150-124">To configure the integration of SensoScientific Wireless Temperature Monitoring System into Azure AD, you need to add SensoScientific Wireless Temperature Monitoring System from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="bc150-124">To configure the integration of SensoScientific Wireless Temperature Monitoring System into Azure AD, you need to add SensoScientific Wireless Temperature Monitoring System from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bc150-125">**To add SensoScientific Wireless Temperature Monitoring System from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bc150-125">**To add SensoScientific Wireless Temperature Monitoring System from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bc150-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="bc150-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="bc150-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="bc150-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bc150-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="bc150-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="bc150-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="bc150-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="bc150-133">In the search box, type **SensoScientific Wireless Temperature Monitoring System**.</span><span class="sxs-lookup"><span data-stu-id="bc150-133">In the search box, type **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Creating an Azure AD test user](./media/sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

1. <span data-ttu-id="bc150-135">In the results panel, select **SensoScientific Wireless Temperature Monitoring System**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="bc150-135">In the results panel, select **SensoScientific Wireless Temperature Monitoring System**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bc150-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bc150-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bc150-138">In this section, you configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="bc150-138">In this section, you configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bc150-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SensoScientific Wireless Temperature Monitoring System is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bc150-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SensoScientific Wireless Temperature Monitoring System is to a user in Azure AD.</span></span> <span data-ttu-id="bc150-140">In other words, a link relationship between an Azure AD user and the related user in SensoScientific Wireless Temperature Monitoring System needs to be established.</span><span class="sxs-lookup"><span data-stu-id="bc150-140">In other words, a link relationship between an Azure AD user and the related user in SensoScientific Wireless Temperature Monitoring System needs to be established.</span></span>

<span data-ttu-id="bc150-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SensoScientific Wireless Temperature Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="bc150-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SensoScientific Wireless Temperature Monitoring System.</span></span>

<span data-ttu-id="bc150-142">To configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="bc150-142">To configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bc150-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="bc150-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="bc150-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bc150-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="bc150-145">**[Creating a SensoScientific Wireless Temperature Monitoring System test user](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)** - to have a counterpart of Britta Simon in SensoScientific Wireless Temperature Monitoring System that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="bc150-145">**[Creating a SensoScientific Wireless Temperature Monitoring System test user](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)** - to have a counterpart of Britta Simon in SensoScientific Wireless Temperature Monitoring System that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="bc150-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bc150-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="bc150-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="bc150-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bc150-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bc150-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bc150-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SensoScientific Wireless Temperature Monitoring System application.</span><span class="sxs-lookup"><span data-stu-id="bc150-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SensoScientific Wireless Temperature Monitoring System application.</span></span>

<span data-ttu-id="bc150-150">**To configure Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bc150-150">**To configure Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, perform the following steps:**</span></span>

1. <span data-ttu-id="bc150-151">In the Azure portal, on the **SensoScientific Wireless Temperature Monitoring System** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="bc150-151">In the Azure portal, on the **SensoScientific Wireless Temperature Monitoring System** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="bc150-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bc150-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

1. <span data-ttu-id="bc150-155">On the **SensoScientific Wireless Temperature Monitoring System Domain and URLs** section, no need to perform any steps as the app is already pre-integrated with Azure:</span><span class="sxs-lookup"><span data-stu-id="bc150-155">On the **SensoScientific Wireless Temperature Monitoring System Domain and URLs** section, no need to perform any steps as the app is already pre-integrated with Azure:</span></span>

    ![Configure Single Sign-On](./media/sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

1. <span data-ttu-id="bc150-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="bc150-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

1. <span data-ttu-id="bc150-159">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="bc150-159">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/sensoscientific-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="bc150-161">On the **SensoScientific Wireless Temperature Monitoring System Configuration** section, click **Configure SensoScientific Wireless Temperature Monitoring System** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="bc150-161">On the **SensoScientific Wireless Temperature Monitoring System Configuration** section, click **Configure SensoScientific Wireless Temperature Monitoring System** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bc150-162">Copy the **Sign-Out URL, SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="bc150-162">Copy the **Sign-Out URL, SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

1. <span data-ttu-id="bc150-164">Sign on to your SensoScientific Wireless Temperature Monitoring System application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="bc150-164">Sign on to your SensoScientific Wireless Temperature Monitoring System application as an administrator.</span></span>

1. <span data-ttu-id="bc150-165">In the navigation menu on the top, click **Configuration** and goto **Configure** under **Single Sign On** to open the Single Sign On Settings.</span><span class="sxs-lookup"><span data-stu-id="bc150-165">In the navigation menu on the top, click **Configuration** and goto **Configure** under **Single Sign On** to open the Single Sign On Settings.</span></span>

    ![Configure Single Sign-On](./media/sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

1. <span data-ttu-id="bc150-167">In **Single Sign On Settings** form perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bc150-167">In **Single Sign On Settings** form perform the following steps:</span></span>
 
    <span data-ttu-id="bc150-168">a.</span><span class="sxs-lookup"><span data-stu-id="bc150-168">a.</span></span> <span data-ttu-id="bc150-169">Select **Issuer Name** as Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bc150-169">Select **Issuer Name** as Azure AD.</span></span>
    
    <span data-ttu-id="bc150-170">b.</span><span class="sxs-lookup"><span data-stu-id="bc150-170">b.</span></span> <span data-ttu-id="bc150-171">Paste the **SAML Entity ID** which you have copied from Azure portal into Issuer URL textbox.</span><span class="sxs-lookup"><span data-stu-id="bc150-171">Paste the **SAML Entity ID** which you have copied from Azure portal into Issuer URL textbox.</span></span>
    
    <span data-ttu-id="bc150-172">c.</span><span class="sxs-lookup"><span data-stu-id="bc150-172">c.</span></span> <span data-ttu-id="bc150-173">Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal into Single Sign-On Service URL textbox.</span><span class="sxs-lookup"><span data-stu-id="bc150-173">Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal into Single Sign-On Service URL textbox.</span></span>

    <span data-ttu-id="bc150-174">d.</span><span class="sxs-lookup"><span data-stu-id="bc150-174">d.</span></span> <span data-ttu-id="bc150-175">Paste the **Sign-Out URL** which you have copied from Azure portal into Single Sign-Out Service URL textbox.</span><span class="sxs-lookup"><span data-stu-id="bc150-175">Paste the **Sign-Out URL** which you have copied from Azure portal into Single Sign-Out Service URL textbox.</span></span>

    <span data-ttu-id="bc150-176">e.</span><span class="sxs-lookup"><span data-stu-id="bc150-176">e.</span></span> <span data-ttu-id="bc150-177">Browse the certificate which you have downloaded from Azure portal and upload here.</span><span class="sxs-lookup"><span data-stu-id="bc150-177">Browse the certificate which you have downloaded from Azure portal and upload here.</span></span>
    
    <span data-ttu-id="bc150-178">f.</span><span class="sxs-lookup"><span data-stu-id="bc150-178">f.</span></span> <span data-ttu-id="bc150-179">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="bc150-179">Click **Save**.</span></span>
  
> [!TIP]
> <span data-ttu-id="bc150-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="bc150-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bc150-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="bc150-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bc150-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bc150-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bc150-183">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="bc150-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="bc150-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bc150-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="bc150-186">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bc150-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bc150-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="bc150-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/sensoscientific-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="bc150-189">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="bc150-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/sensoscientific-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="bc150-191">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="bc150-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/sensoscientific-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="bc150-193">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bc150-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/sensoscientific-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bc150-195">a.</span><span class="sxs-lookup"><span data-stu-id="bc150-195">a.</span></span> <span data-ttu-id="bc150-196">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bc150-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bc150-197">b.</span><span class="sxs-lookup"><span data-stu-id="bc150-197">b.</span></span> <span data-ttu-id="bc150-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bc150-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bc150-199">c.</span><span class="sxs-lookup"><span data-stu-id="bc150-199">c.</span></span> <span data-ttu-id="bc150-200">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="bc150-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bc150-201">d.</span><span class="sxs-lookup"><span data-stu-id="bc150-201">d.</span></span> <span data-ttu-id="bc150-202">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="bc150-202">Click **Create**.</span></span>
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a><span data-ttu-id="bc150-203">Creating a SensoScientific Wireless Temperature Monitoring System test user</span><span class="sxs-lookup"><span data-stu-id="bc150-203">Creating a SensoScientific Wireless Temperature Monitoring System test user</span></span>

<span data-ttu-id="bc150-204">To enable Azure AD users to log in to SensoScientific Wireless Temperature Monitoring System, they must be provisioned into SensoScientific Wireless Temperature Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="bc150-204">To enable Azure AD users to log in to SensoScientific Wireless Temperature Monitoring System, they must be provisioned into SensoScientific Wireless Temperature Monitoring System.</span></span> <span data-ttu-id="bc150-205">Work with [SensoScientific Wireless Temperature Monitoring System support team](https://www.sensoscientific.com/contact-us/) to add the users in the SensoScientific Wireless Temperature Monitoring System platform.</span><span class="sxs-lookup"><span data-stu-id="bc150-205">Work with [SensoScientific Wireless Temperature Monitoring System support team](https://www.sensoscientific.com/contact-us/) to add the users in the SensoScientific Wireless Temperature Monitoring System platform.</span></span> <span data-ttu-id="bc150-206">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bc150-206">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bc150-207">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="bc150-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bc150-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SensoScientific Wireless Temperature Monitoring System.</span><span class="sxs-lookup"><span data-stu-id="bc150-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SensoScientific Wireless Temperature Monitoring System.</span></span>

![Assign User][200] 

<span data-ttu-id="bc150-210">**To assign Britta Simon to SensoScientific Wireless Temperature Monitoring System, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bc150-210">**To assign Britta Simon to SensoScientific Wireless Temperature Monitoring System, perform the following steps:**</span></span>

1. <span data-ttu-id="bc150-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="bc150-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="bc150-213">In the applications list, select **SensoScientific Wireless Temperature Monitoring System**.</span><span class="sxs-lookup"><span data-stu-id="bc150-213">In the applications list, select **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Configure Single Sign-On](./media/sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

1. <span data-ttu-id="bc150-215">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="bc150-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="bc150-217">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="bc150-217">Click **Add** button.</span></span> <span data-ttu-id="bc150-218">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="bc150-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="bc150-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="bc150-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="bc150-221">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="bc150-221">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="bc150-222">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="bc150-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bc150-223">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="bc150-223">Testing single sign-on</span></span>

<span data-ttu-id="bc150-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="bc150-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="bc150-225">Click the SensoScientific Wireless Temperature Monitoring System tile in the Access Panel, you will be automatically signed-on to your SensoScientific Wireless Temperature Monitoring System application.</span><span class="sxs-lookup"><span data-stu-id="bc150-225">Click the SensoScientific Wireless Temperature Monitoring System tile in the Access Panel, you will be automatically signed-on to your SensoScientific Wireless Temperature Monitoring System application.</span></span> <span data-ttu-id="bc150-226">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bc150-226">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bc150-227">Additional resources</span><span class="sxs-lookup"><span data-stu-id="bc150-227">Additional resources</span></span>

* [<span data-ttu-id="bc150-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bc150-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="bc150-229">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bc150-229">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/sensoscientific-tutorial/tutorial_general_203.png

