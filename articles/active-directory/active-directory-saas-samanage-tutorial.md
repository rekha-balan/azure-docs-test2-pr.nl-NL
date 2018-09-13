---
title: 'Tutorial: Azure Active Directory Integration with Samanage | Microsoft Docs'
description: Learn how to use Samanage with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/24/2017
ms.author: jeedes
ms.openlocfilehash: c81cc8222b2f2e8b3c2035e4dcaa57dfbc0c51f3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553401"
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a><span data-ttu-id="7af70-103">Tutorial: Azure Active Directory integration with Samanage</span><span class="sxs-lookup"><span data-stu-id="7af70-103">Tutorial: Azure Active Directory integration with Samanage</span></span>
<span data-ttu-id="7af70-104">The objective of this tutorial is to show you how to integrate Samanage with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7af70-104">The objective of this tutorial is to show you how to integrate Samanage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7af70-105">Integrating Samanage with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7af70-105">Integrating Samanage with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="7af70-106">You can control in Azure AD who has access to Samanage</span><span class="sxs-lookup"><span data-stu-id="7af70-106">You can control in Azure AD who has access to Samanage</span></span>
* <span data-ttu-id="7af70-107">You can enable your users to automatically get signed-on to Samanage single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="7af70-107">You can enable your users to automatically get signed-on to Samanage single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="7af70-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="7af70-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="7af70-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7af70-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7af70-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7af70-110">Prerequisites</span></span>
<span data-ttu-id="7af70-111">To configure Azure AD integration with Samanage, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7af70-111">To configure Azure AD integration with Samanage, you need the following items:</span></span>

* <span data-ttu-id="7af70-112">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="7af70-112">A valid Azure subscription</span></span>
* <span data-ttu-id="7af70-113">A tenant in Samanage</span><span class="sxs-lookup"><span data-stu-id="7af70-113">A tenant in Samanage</span></span>

>[!NOTE]
><span data-ttu-id="7af70-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7af70-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="7af70-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7af70-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="7af70-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="7af70-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="7af70-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7af70-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7af70-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7af70-118">Scenario description</span></span>
<span data-ttu-id="7af70-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7af70-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="7af70-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7af70-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7af70-121">Adding Samanage from the gallery</span><span class="sxs-lookup"><span data-stu-id="7af70-121">Adding Samanage from the gallery</span></span>
2. <span data-ttu-id="7af70-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="7af70-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-samanage-from-the-gallery"></a><span data-ttu-id="7af70-123">Adding Samanage from the gallery</span><span class="sxs-lookup"><span data-stu-id="7af70-123">Adding Samanage from the gallery</span></span>
<span data-ttu-id="7af70-124">To configure the integration of Samanage into Azure AD, you need to add Samanage from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7af70-124">To configure the integration of Samanage into Azure AD, you need to add Samanage from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7af70-125">**To add Samanage from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7af70-125">**To add Samanage from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7af70-126">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7af70-126">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="7af70-127">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_general_01.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="7af70-127">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_general_01.png "Active Directory")</span></span>
2. <span data-ttu-id="7af70-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="7af70-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="7af70-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="7af70-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="7af70-130">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_general_02.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="7af70-130">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_general_02.png "Applications")</span></span>
4. <span data-ttu-id="7af70-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="7af70-131">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="7af70-132">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_general_03.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="7af70-132">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_general_03.png "Add application")</span></span>
5. <span data-ttu-id="7af70-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="7af70-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="7af70-134">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_general_04.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="7af70-134">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_general_04.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="7af70-135">In the **search box**, type **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="7af70-135">In the **search box**, type **Samanage**.</span></span>
   
   <span data-ttu-id="7af70-136">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_01.png "Application gallery")</span><span class="sxs-lookup"><span data-stu-id="7af70-136">![Application gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_01.png "Application gallery")</span></span>
7. <span data-ttu-id="7af70-137">In the results pane, select **Samanage**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="7af70-137">In the results pane, select **Samanage**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="7af70-138">![Samanage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_02.png "Samanage")</span><span class="sxs-lookup"><span data-stu-id="7af70-138">![Samanage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_02.png "Samanage")</span></span>

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="7af70-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="7af70-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="7af70-140">The objective of this section is to show you how to configure and test Azure AD SSO with Samanage based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7af70-140">The objective of this section is to show you how to configure and test Azure AD SSO with Samanage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7af70-141">For SSO to work, Azure AD needs to know what the counterpart user in Samanage to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="7af70-141">For SSO to work, Azure AD needs to know what the counterpart user in Samanage to an user in Azure AD is.</span></span> <span data-ttu-id="7af70-142">In other words, a link relationship between an Azure AD user and the related user in Samanage needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7af70-142">In other words, a link relationship between an Azure AD user and the related user in Samanage needs to be established.</span></span>

<span data-ttu-id="7af70-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Samanage.</span><span class="sxs-lookup"><span data-stu-id="7af70-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Samanage.</span></span>

<span data-ttu-id="7af70-144">To configure and test Azure AD SSO with Samanage, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7af70-144">To configure and test Azure AD SSO with Samanage, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7af70-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7af70-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7af70-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7af70-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7af70-147">**[Creating a Samanage test user](#creating-a-Samanage-test-user)** - to have a counterpart of Britta Simon in Samanage that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="7af70-147">**[Creating a Samanage test user](#creating-a-Samanage-test-user)** - to have a counterpart of Britta Simon in Samanage that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="7af70-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7af70-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7af70-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7af70-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="7af70-150">Configuring Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="7af70-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="7af70-151">In this section, you enable Azure AD single sign-on in the classic portal and configure SSO in your Samanage application.</span><span class="sxs-lookup"><span data-stu-id="7af70-151">In this section, you enable Azure AD single sign-on in the classic portal and configure SSO in your Samanage application.</span></span>

<span data-ttu-id="7af70-152">**To configure Azure AD SSO with Samanage, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7af70-152">**To configure Azure AD SSO with Samanage, perform the following steps:**</span></span>

1. <span data-ttu-id="7af70-153">In the Azure classic portal, on the **Samanage** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="7af70-153">In the Azure classic portal, on the **Samanage** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="7af70-154">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_general_05.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="7af70-154">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_general_05.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="7af70-155">On the **How would you like users to sign on to Samanage** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7af70-155">On the **How would you like users to sign on to Samanage** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="7af70-156">![Microsoft Azure AD Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_03.png "Microsoft Azure AD Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="7af70-156">![Microsoft Azure AD Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_03.png "Microsoft Azure AD Single Sign-On")</span></span>
3. <span data-ttu-id="7af70-157">On the Configure App Settings dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7af70-157">On the Configure App Settings dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="7af70-158">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_04.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="7af70-158">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_04.png "Configure App URL")</span></span> 
 1. <span data-ttu-id="7af70-159">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<Company Name>.samanage.com/saml_login/<Company Name>`.</span><span class="sxs-lookup"><span data-stu-id="7af70-159">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<Company Name>.samanage.com/saml_login/<Company Name>`.</span></span> 
 2. <span data-ttu-id="7af70-160">click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7af70-160">click **Next**.</span></span>
 
   >[!NOTE]
   ><span data-ttu-id="7af70-161">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="7af70-161">Please note that these are not the real values.</span></span> <span data-ttu-id="7af70-162">You have to update these values with the actual Sign On URL.</span><span class="sxs-lookup"><span data-stu-id="7af70-162">You have to update these values with the actual Sign On URL.</span></span> <span data-ttu-id="7af70-163">To get these values, refer step 8.c for more details or contact Samanage.</span><span class="sxs-lookup"><span data-stu-id="7af70-163">To get these values, refer step 8.c for more details or contact Samanage.</span></span>
   > 
 
4. <span data-ttu-id="7af70-164">On the **Configure single sign-on at Samanage** page, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="7af70-164">On the **Configure single sign-on at Samanage** page, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="7af70-165">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_05.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="7af70-165">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_05.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="7af70-166">In a different web browser window, log into your Samanage company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7af70-166">In a different web browser window, log into your Samanage company site as an administrator.</span></span>
6. <span data-ttu-id="7af70-167">Click **Dashboard** and select **Setup** in left navigation pane.</span><span class="sxs-lookup"><span data-stu-id="7af70-167">Click **Dashboard** and select **Setup** in left navigation pane.</span></span>
   
   <span data-ttu-id="7af70-168">![Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span><span class="sxs-lookup"><span data-stu-id="7af70-168">![Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span></span>
7. <span data-ttu-id="7af70-169">Click **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="7af70-169">Click **Single Sign-On**.</span></span>
   
   <span data-ttu-id="7af70-170">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="7af70-170">![Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span></span>
8. <span data-ttu-id="7af70-171">Navigate to **Login using SAML** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7af70-171">Navigate to **Login using SAML** section, perform the following steps:</span></span>
   
   <span data-ttu-id="7af70-172">![Login using SAML](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span><span class="sxs-lookup"><span data-stu-id="7af70-172">![Login using SAML](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span></span>
 1. <span data-ttu-id="7af70-173">Click **Enable Single Sign-On with SAML**.</span><span class="sxs-lookup"><span data-stu-id="7af70-173">Click **Enable Single Sign-On with SAML**.</span></span>  
 2. <span data-ttu-id="7af70-174">In the **Identity Provider URL** textbox put the value of **Identity Provider ID** from Azure AD application configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="7af70-174">In the **Identity Provider URL** textbox put the value of **Identity Provider ID** from Azure AD application configuration wizard.</span></span>    
 3. <span data-ttu-id="7af70-175">Confirm the **Login URL** matches the **Sign On URL** in step 3.</span><span class="sxs-lookup"><span data-stu-id="7af70-175">Confirm the **Login URL** matches the **Sign On URL** in step 3.</span></span>
 4. <span data-ttu-id="7af70-176">In the **Logout URL** textbox put the value of **Remote Logout URL** from Azure AD application configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="7af70-176">In the **Logout URL** textbox put the value of **Remote Logout URL** from Azure AD application configuration wizard.</span></span>
 5. <span data-ttu-id="7af70-177">In the **SAML Issuer** textbox type the app id URI set in your identity provider.</span><span class="sxs-lookup"><span data-stu-id="7af70-177">In the **SAML Issuer** textbox type the app id URI set in your identity provider.</span></span>
 6. <span data-ttu-id="7af70-178">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Paste your Identity Provider x.509 Certificate below** textbox.</span><span class="sxs-lookup"><span data-stu-id="7af70-178">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Paste your Identity Provider x.509 Certificate below** textbox.</span></span>
 7. <span data-ttu-id="7af70-179">Click **Create users if they do not exist in Samanage**.</span><span class="sxs-lookup"><span data-stu-id="7af70-179">Click **Create users if they do not exist in Samanage**.</span></span>
 8. <span data-ttu-id="7af70-180">Click **Update**.</span><span class="sxs-lookup"><span data-stu-id="7af70-180">Click **Update**.</span></span>
9. <span data-ttu-id="7af70-181">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7af70-181">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
   <span data-ttu-id="7af70-182">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_06.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="7af70-182">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_06.png "Configure Single Sign-On")</span></span>
10. <span data-ttu-id="7af70-183">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="7af70-183">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
    
    <span data-ttu-id="7af70-184">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_07.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="7af70-184">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_07.png "Configure Single Sign-On")</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7af70-185">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7af70-185">Create an Azure AD test user</span></span>
<span data-ttu-id="7af70-186">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7af70-186">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/create_aaduser_00.png)

<span data-ttu-id="7af70-188">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7af70-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7af70-189">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7af70-189">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/create_aaduser_01.png)
2. <span data-ttu-id="7af70-191">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="7af70-191">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="7af70-192">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="7af70-192">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/create_aaduser_02.png)
4. <span data-ttu-id="7af70-194">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="7af70-194">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/create_aaduser_03.png)
5. <span data-ttu-id="7af70-196">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7af70-196">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/create_aaduser_04.png)
 1. <span data-ttu-id="7af70-198">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="7af70-198">As Type Of User, select New user in your organization.</span></span> 
 2. <span data-ttu-id="7af70-199">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7af70-199">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="7af70-200">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7af70-200">Click **Next**.</span></span>
6. <span data-ttu-id="7af70-201">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7af70-201">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/create_aaduser_05.png) 
 1. <span data-ttu-id="7af70-203">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="7af70-203">In the **First Name** textbox, type **Britta**.</span></span>   
 2. <span data-ttu-id="7af70-204">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="7af70-204">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="7af70-205">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7af70-205">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="7af70-206">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="7af70-206">In the **Role** list, select **User**.</span></span> 
 5. <span data-ttu-id="7af70-207">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7af70-207">Click **Next**.</span></span>
7. <span data-ttu-id="7af70-208">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="7af70-208">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/create_aaduser_06.png)
8. <span data-ttu-id="7af70-210">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7af70-210">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/create_aaduser_07.png)  
 1. <span data-ttu-id="7af70-212">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="7af70-212">Write down the value of the **New Password**.</span></span> 
 2. <span data-ttu-id="7af70-213">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="7af70-213">Click **Complete**.</span></span>   

### <a name="create-a-samanage-test-user"></a><span data-ttu-id="7af70-214">Create a Samanage test user</span><span class="sxs-lookup"><span data-stu-id="7af70-214">Create a Samanage test user</span></span>
<span data-ttu-id="7af70-215">In order to enable Azure AD users to log into Samanage, they must be provisioned into Samanage.In the case of Samanage, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="7af70-215">In order to enable Azure AD users to log into Samanage, they must be provisioned into Samanage.In the case of Samanage, provisioning is a manual task.</span></span>

<span data-ttu-id="7af70-216">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7af70-216">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="7af70-217">Log into your Samanage company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="7af70-217">Log into your Samanage company site as an administrator.</span></span>
2. <span data-ttu-id="7af70-218">Click **Dashboard** and select **Setup** in left navigation pan.</span><span class="sxs-lookup"><span data-stu-id="7af70-218">Click **Dashboard** and select **Setup** in left navigation pan.</span></span>
   
   <span data-ttu-id="7af70-219">![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="7af70-219">![Setup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Setup")</span></span>
3. <span data-ttu-id="7af70-220">Click the **Users** tab</span><span class="sxs-lookup"><span data-stu-id="7af70-220">Click the **Users** tab</span></span>
   
   <span data-ttu-id="7af70-221">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Users")</span><span class="sxs-lookup"><span data-stu-id="7af70-221">![Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Users")</span></span>
4. <span data-ttu-id="7af70-222">Click **New User**.</span><span class="sxs-lookup"><span data-stu-id="7af70-222">Click **New User**.</span></span>
   
   <span data-ttu-id="7af70-223">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "New User")</span><span class="sxs-lookup"><span data-stu-id="7af70-223">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "New User")</span></span>
5. <span data-ttu-id="7af70-224">Type the **Name** and the **Email Address** of an Azure AD account you want to provision and click **Create user**.</span><span class="sxs-lookup"><span data-stu-id="7af70-224">Type the **Name** and the **Email Address** of an Azure AD account you want to provision and click **Create user**.</span></span>
   
   <span data-ttu-id="7af70-225">![Creat User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Creat User")</span><span class="sxs-lookup"><span data-stu-id="7af70-225">![Creat User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Creat User")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="7af70-226">The AAD account holder will receive an email and follow a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="7af70-226">The AAD account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span> <span data-ttu-id="7af70-227">You can use any other Samanage user account creation tools or APIs provided by Samanage to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="7af70-227">You can use any other Samanage user account creation tools or APIs provided by Samanage to provision AAD user accounts.</span></span>
   >  

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7af70-228">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7af70-228">Assign the Azure AD test user</span></span>
<span data-ttu-id="7af70-229">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Samanage.</span><span class="sxs-lookup"><span data-stu-id="7af70-229">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Samanage.</span></span>

<span data-ttu-id="7af70-230">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/assign_aaduser_00.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="7af70-230">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/assign_aaduser_00.png "Assign users")</span></span>

<span data-ttu-id="7af70-231">**To assign Britta Simon to Samanage, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7af70-231">**To assign Britta Simon to Samanage, perform the following steps:**</span></span>

1. <span data-ttu-id="7af70-232">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="7af70-232">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="7af70-233">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/assign_aaduser_01.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="7af70-233">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/assign_aaduser_01.png "Assign users")</span></span>
2. <span data-ttu-id="7af70-234">In the applications list, select **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="7af70-234">In the applications list, select **Samanage**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/tutorial_samanage_08.png)
3. <span data-ttu-id="7af70-236">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="7af70-236">In the menu on the top, click **Users**.</span></span>
   
    <span data-ttu-id="7af70-237">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/assign_aaduser_02.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="7af70-237">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/assign_aaduser_02.png "Assign users")</span></span>
4. <span data-ttu-id="7af70-238">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7af70-238">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="7af70-239">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="7af70-239">In the toolbar on the bottom, click **Assign**.</span></span>
   
    <span data-ttu-id="7af70-240">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/assign_aaduser_03.png "Assign users")</span><span class="sxs-lookup"><span data-stu-id="7af70-240">![Assign users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-samanage-tutorial/assign_aaduser_03.png "Assign users")</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="7af70-241">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="7af70-241">Test single sign-on</span></span>
<span data-ttu-id="7af70-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7af70-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="7af70-243">When you click the Samanage tile in the Access Panel, you should get automatically signed-on to your Samanage application.</span><span class="sxs-lookup"><span data-stu-id="7af70-243">When you click the Samanage tile in the Access Panel, you should get automatically signed-on to your Samanage application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7af70-244">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7af70-244">Additional resources</span></span>
* [<span data-ttu-id="7af70-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7af70-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7af70-246">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7af70-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

































