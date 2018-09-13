---
title: 'Tutorial: Azure Active Directory Integration with MCM | Microsoft Docs'
description: Learn how to use MCM with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 7f00799d-e3e9-4ba9-ae4a-fbca843ac5db
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: b99cc56a939b32d053c31e8075a3bb63124cea78
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552617"
---
# <a name="tutorial-azure-active-directory-integration-with-mcm"></a><span data-ttu-id="2e1b2-103">Tutorial: Azure Active Directory integration with MCM</span><span class="sxs-lookup"><span data-stu-id="2e1b2-103">Tutorial: Azure Active Directory integration with MCM</span></span>
<span data-ttu-id="2e1b2-104">The objective of this tutorial is to show you how to integrate MCM with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2e1b2-104">The objective of this tutorial is to show you how to integrate MCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2e1b2-105">Integrating MCM with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="2e1b2-105">Integrating MCM with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="2e1b2-106">You can control in Azure AD who has access to MCM</span><span class="sxs-lookup"><span data-stu-id="2e1b2-106">You can control in Azure AD who has access to MCM</span></span>
* <span data-ttu-id="2e1b2-107">You can enable your users to automatically get signed-on to MCM (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="2e1b2-107">You can enable your users to automatically get signed-on to MCM (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="2e1b2-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="2e1b2-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="2e1b2-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2e1b2-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e1b2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2e1b2-110">Prerequisites</span></span>
<span data-ttu-id="2e1b2-111">To configure Azure AD integration with MCM, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="2e1b2-111">To configure Azure AD integration with MCM, you need the following items:</span></span>

* <span data-ttu-id="2e1b2-112">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="2e1b2-112">A valid Azure subscription</span></span>
* <span data-ttu-id="2e1b2-113">A MCM single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="2e1b2-113">A MCM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2e1b2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="2e1b2-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="2e1b2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="2e1b2-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="2e1b2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2e1b2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2e1b2-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="2e1b2-118">Scenario description</span></span>
<span data-ttu-id="2e1b2-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="2e1b2-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="2e1b2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2e1b2-121">Adding MCM from the gallery</span><span class="sxs-lookup"><span data-stu-id="2e1b2-121">Adding MCM from the gallery</span></span>
2. <span data-ttu-id="2e1b2-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2e1b2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mcm-from-the-gallery"></a><span data-ttu-id="2e1b2-123">Adding MCM from the gallery</span><span class="sxs-lookup"><span data-stu-id="2e1b2-123">Adding MCM from the gallery</span></span>
<span data-ttu-id="2e1b2-124">To configure the integration of MCM into Azure AD, you need to add MCM from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-124">To configure the integration of MCM into Azure AD, you need to add MCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2e1b2-125">**To add MCM from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2e1b2-125">**To add MCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2e1b2-126">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-126">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="2e1b2-127">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_general_01.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="2e1b2-127">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_general_01.png "Active Directory")</span></span>

2. <span data-ttu-id="2e1b2-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="2e1b2-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="2e1b2-130">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_general_02.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="2e1b2-130">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_general_02.png "Applications")</span></span>

4. <span data-ttu-id="2e1b2-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-131">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="2e1b2-132">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_general_03.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="2e1b2-132">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_general_03.png "Add application")</span></span>

5. <span data-ttu-id="2e1b2-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="2e1b2-134">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_general_04.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="2e1b2-134">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_general_04.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="2e1b2-135">In the **search box**, type **MCM**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-135">In the **search box**, type **MCM**.</span></span>
   
    <span data-ttu-id="2e1b2-136">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_mcm_01.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="2e1b2-136">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_mcm_01.png "Application gallery")</span></span>

7. <span data-ttu-id="2e1b2-137">In the results pane, select **MCM**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-137">In the results pane, select **MCM**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="2e1b2-138">![MCM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_mcm_001.png "MCM")</span><span class="sxs-lookup"><span data-stu-id="2e1b2-138">![MCM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_mcm_001.png "MCM")</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2e1b2-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2e1b2-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2e1b2-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with MCM based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2e1b2-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with MCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2e1b2-141">For single sign-on to work, Azure AD needs to know what the counterpart user in MCM to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-141">For single sign-on to work, Azure AD needs to know what the counterpart user in MCM to an user in Azure AD is.</span></span> <span data-ttu-id="2e1b2-142">In other words, a link relationship between an Azure AD user and the related user in MCM needs to be established.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-142">In other words, a link relationship between an Azure AD user and the related user in MCM needs to be established.</span></span>

<span data-ttu-id="2e1b2-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in MCM.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in MCM.</span></span>

<span data-ttu-id="2e1b2-144">To configure and test Azure AD single sign-on with MCM, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="2e1b2-144">To configure and test Azure AD single sign-on with MCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2e1b2-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2e1b2-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2e1b2-147">**[Creating a MCM test user](#creating-a-mcm-test-user)** - to have a counterpart of Britta Simon in MCM that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-147">**[Creating a MCM test user](#creating-a-mcm-test-user)** - to have a counterpart of Britta Simon in MCM that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="2e1b2-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2e1b2-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2e1b2-150">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2e1b2-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="2e1b2-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your MCM application.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your MCM application.</span></span>

<span data-ttu-id="2e1b2-152">**To configure Azure AD single sign-on with MCM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2e1b2-152">**To configure Azure AD single sign-on with MCM, perform the following steps:**</span></span>

1. <span data-ttu-id="2e1b2-153">In the Azure classic portal, on the **MCM** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-153">In the Azure classic portal, on the **MCM** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="2e1b2-154">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_general_05.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="2e1b2-154">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_general_05.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="2e1b2-155">On the **How would you like users to sign on to MCM** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-155">On the **How would you like users to sign on to MCM** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="2e1b2-156">![Microsoft Azure AD Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_mcm_03.png "Microsoft Azure AD Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2e1b2-156">![Microsoft Azure AD Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_mcm_03.png "Microsoft Azure AD Single Sign-On")</span></span>

3. <span data-ttu-id="2e1b2-157">On the Configure App Settings dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2e1b2-157">On the Configure App Settings dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="2e1b2-158">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_mcm_04.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="2e1b2-158">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_mcm_04.png "Configure App URL")</span></span>
   
    <span data-ttu-id="2e1b2-159">a.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-159">a.</span></span> <span data-ttu-id="2e1b2-160">In the **Sign On URL** textbox, type: `https://myaba.co.uk/client-access/<company name>/saml.php`.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-160">In the **Sign On URL** textbox, type: `https://myaba.co.uk/client-access/<company name>/saml.php`.</span></span>
   
    <span data-ttu-id="2e1b2-161">b.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-161">b.</span></span> <span data-ttu-id="2e1b2-162">click **Next**</span><span class="sxs-lookup"><span data-stu-id="2e1b2-162">click **Next**</span></span>

4. <span data-ttu-id="2e1b2-163">On the **Configure single sign-on at MCM** page, click **Download metadata**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-163">On the **Configure single sign-on at MCM** page, click **Download metadata**, and then save the certificate file on your computer.</span></span>
   
    <span data-ttu-id="2e1b2-164">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_mcm_05.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2e1b2-164">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_mcm_05.png "Configure Single Sign-On")</span></span>

5. <span data-ttu-id="2e1b2-165">To get SSO configured for your application, contact your MCM support team.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-165">To get SSO configured for your application, contact your MCM support team.</span></span> <span data-ttu-id="2e1b2-166">Attach the downloaded metadata file and share it with MCM team to set up SSO on their side.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-166">Attach the downloaded metadata file and share it with MCM team to set up SSO on their side.</span></span>

6. <span data-ttu-id="2e1b2-167">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-167">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    <span data-ttu-id="2e1b2-168">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_mcm_06.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2e1b2-168">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_mcm_06.png "Configure Single Sign-On")</span></span>

7. <span data-ttu-id="2e1b2-169">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-169">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="2e1b2-170">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_mcm_07.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="2e1b2-170">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_mcm_07.png "Configure Single Sign-On")</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2e1b2-171">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2e1b2-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="2e1b2-172">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-172">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/create_aaduser_00.png)

<span data-ttu-id="2e1b2-174">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2e1b2-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2e1b2-175">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-175">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="2e1b2-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="2e1b2-178">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-178">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/create_aaduser_02.png)

4. <span data-ttu-id="2e1b2-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/create_aaduser_03.png)

5. <span data-ttu-id="2e1b2-182">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2e1b2-182">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/create_aaduser_04.png)
   
    <span data-ttu-id="2e1b2-184">a.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-184">a.</span></span> <span data-ttu-id="2e1b2-185">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-185">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="2e1b2-186">b.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-186">b.</span></span> <span data-ttu-id="2e1b2-187">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-187">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="2e1b2-188">c.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-188">c.</span></span> <span data-ttu-id="2e1b2-189">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-189">Click **Next**.</span></span>

6. <span data-ttu-id="2e1b2-190">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2e1b2-190">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/create_aaduser_05.png)
   
    <span data-ttu-id="2e1b2-192">a.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-192">a.</span></span> <span data-ttu-id="2e1b2-193">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-193">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="2e1b2-194">b.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-194">b.</span></span> <span data-ttu-id="2e1b2-195">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-195">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="2e1b2-196">c.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-196">c.</span></span> <span data-ttu-id="2e1b2-197">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="2e1b2-198">d.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-198">d.</span></span> <span data-ttu-id="2e1b2-199">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-199">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="2e1b2-200">e.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-200">e.</span></span> <span data-ttu-id="2e1b2-201">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-201">Click **Next**.</span></span>

7. <span data-ttu-id="2e1b2-202">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-202">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/create_aaduser_06.png)

8. <span data-ttu-id="2e1b2-204">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2e1b2-204">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/create_aaduser_07.png)
   
    <span data-ttu-id="2e1b2-206">a.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-206">a.</span></span> <span data-ttu-id="2e1b2-207">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-207">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="2e1b2-208">b.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-208">b.</span></span> <span data-ttu-id="2e1b2-209">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-209">Click **Complete**.</span></span>   

### <a name="creating-a-mcm-test-user"></a><span data-ttu-id="2e1b2-210">Creating a MCM test user</span><span class="sxs-lookup"><span data-stu-id="2e1b2-210">Creating a MCM test user</span></span>
<span data-ttu-id="2e1b2-211">In this section, you create a user called Britta Simon in MCM.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-211">In this section, you create a user called Britta Simon in MCM.</span></span> <span data-ttu-id="2e1b2-212">Please work with MCM support team to add the users in the MCM platform.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-212">Please work with MCM support team to add the users in the MCM platform.</span></span>

> [!NOTE]
> <span data-ttu-id="2e1b2-213">You can use any other MCM user account creation tools or APIs provided by MCM to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-213">You can use any other MCM user account creation tools or APIs provided by MCM to provision AAD user accounts.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2e1b2-214">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2e1b2-214">Assigning the Azure AD test user</span></span>
<span data-ttu-id="2e1b2-215">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to MCM.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-215">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to MCM.</span></span>

<span data-ttu-id="2e1b2-216">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/assign_aaduser_00.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="2e1b2-216">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/assign_aaduser_00.png "Assign users")</span></span>

<span data-ttu-id="2e1b2-217">**To assign Britta Simon to MCM, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2e1b2-217">**To assign Britta Simon to MCM, perform the following steps:**</span></span>

1. <span data-ttu-id="2e1b2-218">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-218">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="2e1b2-219">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/assign_aaduser_01.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="2e1b2-219">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/assign_aaduser_01.png "Assign users")</span></span>

2. <span data-ttu-id="2e1b2-220">In the applications list, select **MCM**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-220">In the applications list, select **MCM**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/tutorial_mcm_08.png)

3. <span data-ttu-id="2e1b2-222">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-222">In the menu on the top, click **Users**.</span></span>
   
    <span data-ttu-id="2e1b2-223">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/assign_aaduser_02.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="2e1b2-223">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/assign_aaduser_02.png "Assign users")</span></span>

4. <span data-ttu-id="2e1b2-224">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-224">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="2e1b2-225">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-225">In the toolbar on the bottom, click **Assign**.</span></span>
   
    <span data-ttu-id="2e1b2-226">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/assign_aaduser_03.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="2e1b2-226">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mcm-tutorial/assign_aaduser_03.png "Assign users")</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="2e1b2-227">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="2e1b2-227">Testing single sign-on</span></span>
<span data-ttu-id="2e1b2-228">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-228">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2e1b2-229">When you click the MCM tile in the Access Panel, you should get automatically signed-on to your MCM application.</span><span class="sxs-lookup"><span data-stu-id="2e1b2-229">When you click the MCM tile in the Access Panel, you should get automatically signed-on to your MCM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2e1b2-230">Additional resources</span><span class="sxs-lookup"><span data-stu-id="2e1b2-230">Additional resources</span></span>
* [<span data-ttu-id="2e1b2-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2e1b2-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2e1b2-232">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2e1b2-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


























