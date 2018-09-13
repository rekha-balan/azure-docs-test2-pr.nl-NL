---
title: 'Tutorial: Azure Active Directory integration with ServiceNow | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ServiceNow and ServiceNow Express.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 20259958d4d5b8f08a296f986f287636b5b9af66
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661879"
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="4380a-103">Tutorial: Azure Active Directory integration with ServiceNow</span><span class="sxs-lookup"><span data-stu-id="4380a-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>
<span data-ttu-id="4380a-104">In this tutorial, you learn how to integrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4380a-104">In this tutorial, you learn how to integrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4380a-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4380a-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="4380a-106">You can control in Azure AD who has access to ServiceNow and ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="4380a-106">You can control in Azure AD who has access to ServiceNow and ServiceNow Express</span></span>
* <span data-ttu-id="4380a-107">You can enable your users to automatically get signed-on to ServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="4380a-107">You can enable your users to automatically get signed-on to ServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="4380a-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="4380a-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="4380a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4380a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4380a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4380a-110">Prerequisites</span></span>
<span data-ttu-id="4380a-111">To configure Azure AD integration with ServiceNow and ServiceNow Express, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4380a-111">To configure Azure AD integration with ServiceNow and ServiceNow Express, you need the following items:</span></span>

* <span data-ttu-id="4380a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4380a-112">An Azure AD subscription</span></span>
* <span data-ttu-id="4380a-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span><span class="sxs-lookup"><span data-stu-id="4380a-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
* <span data-ttu-id="4380a-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span><span class="sxs-lookup"><span data-stu-id="4380a-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
* <span data-ttu-id="4380a-115">The ServiceNow tenant must have the [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span><span class="sxs-lookup"><span data-stu-id="4380a-115">The ServiceNow tenant must have the [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="4380a-116">This can be done by [submitting a service request](https://hi.service-now.com).</span><span class="sxs-lookup"><span data-stu-id="4380a-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span> 

> [!NOTE]
> <span data-ttu-id="4380a-117">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4380a-117">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="4380a-118">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4380a-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="4380a-119">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="4380a-119">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="4380a-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4380a-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4380a-121">Scenario description</span><span class="sxs-lookup"><span data-stu-id="4380a-121">Scenario description</span></span>
<span data-ttu-id="4380a-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4380a-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4380a-123">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4380a-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4380a-124">Adding ServiceNow from the gallery</span><span class="sxs-lookup"><span data-stu-id="4380a-124">Adding ServiceNow from the gallery</span></span>
2. <span data-ttu-id="4380a-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="4380a-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span></span>

## <a name="adding-servicenow-from-the-gallery"></a><span data-ttu-id="4380a-126">Adding ServiceNow from the gallery</span><span class="sxs-lookup"><span data-stu-id="4380a-126">Adding ServiceNow from the gallery</span></span>
<span data-ttu-id="4380a-127">To configure the integration of ServiceNow or ServiceNow Express into Azure AD, you need to add ServiceNow from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4380a-127">To configure the integration of ServiceNow or ServiceNow Express into Azure AD, you need to add ServiceNow from the gallery to your list of managed SaaS apps.</span></span> 

<span data-ttu-id="4380a-128">**To add ServiceNow from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4380a-128">**To add ServiceNow from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4380a-129">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4380a-129">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="4380a-131">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="4380a-131">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="4380a-132">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="4380a-132">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="4380a-134">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="4380a-134">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="4380a-136">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="4380a-136">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="4380a-138">In the search box, type **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="4380a-138">In the search box, type **ServiceNow**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. <span data-ttu-id="4380a-140">In the results pane, select **ServiceNow**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="4380a-140">In the results pane, select **ServiceNow**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4380a-142">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4380a-142">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4380a-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4380a-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4380a-144">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceNow is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4380a-144">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceNow is to a user in Azure AD.</span></span> <span data-ttu-id="4380a-145">In other words, a link relationship between an Azure AD user and the related user in ServiceNow needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4380a-145">In other words, a link relationship between an Azure AD user and the related user in ServiceNow needs to be established.</span></span>
<span data-ttu-id="4380a-146">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="4380a-146">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceNow.</span></span> <span data-ttu-id="4380a-147">To configure and test Azure AD single sign-on with ServiceNow, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4380a-147">To configure and test Azure AD single sign-on with ServiceNow, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4380a-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4380a-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4380a-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4380a-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - to enable your users to use this feature.</span></span>
3. <span data-ttu-id="4380a-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4380a-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="4380a-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - to have a counterpart of Britta Simon in ServiceNow that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="4380a-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - to have a counterpart of Britta Simon in ServiceNow that is linked to the Azure AD representation of her.</span></span>
5. <span data-ttu-id="4380a-152">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4380a-152">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="4380a-153">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4380a-153">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

> [!NOTE]
> <span data-ttu-id="4380a-154">If you want to configure ServiceNow omit step 2.</span><span class="sxs-lookup"><span data-stu-id="4380a-154">If you want to configure ServiceNow omit step 2.</span></span> <span data-ttu-id="4380a-155">Likewise, if you want to configure ServiceNow Express omit step 1.</span><span class="sxs-lookup"><span data-stu-id="4380a-155">Likewise, if you want to configure ServiceNow Express omit step 1.</span></span>
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="4380a-156">Configuring Azure AD Single Sign-On for ServiceNow</span><span class="sxs-lookup"><span data-stu-id="4380a-156">Configuring Azure AD Single Sign-On for ServiceNow</span></span>
1. <span data-ttu-id="4380a-157">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="4380a-157">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="4380a-158">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-158">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="4380a-159">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4380a-159">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="4380a-160">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-160">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="4380a-161">On the **Configure App Settings** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4380a-161">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="4380a-162">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="4380a-162">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="4380a-163">a.</span><span class="sxs-lookup"><span data-stu-id="4380a-163">a.</span></span> <span data-ttu-id="4380a-164">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="4380a-164">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="4380a-165">b.</span><span class="sxs-lookup"><span data-stu-id="4380a-165">b.</span></span> <span data-ttu-id="4380a-166">In the **Identifier** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="4380a-166">In the **Identifier** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="4380a-167">c.</span><span class="sxs-lookup"><span data-stu-id="4380a-167">c.</span></span> <span data-ttu-id="4380a-168">Click **Next**</span><span class="sxs-lookup"><span data-stu-id="4380a-168">Click **Next**</span></span>

4. <span data-ttu-id="4380a-169">To have Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in the **Auto configure single sign-on** form and click *Configure*.</span><span class="sxs-lookup"><span data-stu-id="4380a-169">To have Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in the **Auto configure single sign-on** form and click *Configure*.</span></span> <span data-ttu-id="4380a-170">Note that the admin username provided must have the **security_admin** role assigned in ServiceNow for this to work.</span><span class="sxs-lookup"><span data-stu-id="4380a-170">Note that the admin username provided must have the **security_admin** role assigned in ServiceNow for this to work.</span></span> <span data-ttu-id="4380a-171">Otherwise, to manually configure ServiceNow to use Azure AD as a SAML identity provider, click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span><span class="sxs-lookup"><span data-stu-id="4380a-171">Otherwise, to manually configure ServiceNow to use Azure AD as a SAML identity provider, click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span></span>
   
    <span data-ttu-id="4380a-172">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="4380a-172">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="4380a-173">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="4380a-173">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="4380a-174">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-174">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="4380a-175">Sign-on to your ServiceNow application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="4380a-175">Sign-on to your ServiceNow application as an administrator.</span></span>

7. <span data-ttu-id="4380a-176">Activate the *Integration - Multiple Provider Single Sign-On Installer* plugin by following the next steps:</span><span class="sxs-lookup"><span data-stu-id="4380a-176">Activate the *Integration - Multiple Provider Single Sign-On Installer* plugin by following the next steps:</span></span>
   
    <span data-ttu-id="4380a-177">a.</span><span class="sxs-lookup"><span data-stu-id="4380a-177">a.</span></span> <span data-ttu-id="4380a-178">In the navigation pane on the left side, go to **System Definition** section and then click **Plugins**.</span><span class="sxs-lookup"><span data-stu-id="4380a-178">In the navigation pane on the left side, go to **System Definition** section and then click **Plugins**.</span></span>
   
    <span data-ttu-id="4380a-179">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span><span class="sxs-lookup"><span data-stu-id="4380a-179">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>
   
    <span data-ttu-id="4380a-180">b.</span><span class="sxs-lookup"><span data-stu-id="4380a-180">b.</span></span> <span data-ttu-id="4380a-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span><span class="sxs-lookup"><span data-stu-id="4380a-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span></span>
   
    <span data-ttu-id="4380a-182">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span><span class="sxs-lookup"><span data-stu-id="4380a-182">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>
   
    <span data-ttu-id="4380a-183">c.</span><span class="sxs-lookup"><span data-stu-id="4380a-183">c.</span></span> <span data-ttu-id="4380a-184">Select the plugin.</span><span class="sxs-lookup"><span data-stu-id="4380a-184">Select the plugin.</span></span> <span data-ttu-id="4380a-185">Rigth click and select **Activate/Upgrade**.</span><span class="sxs-lookup"><span data-stu-id="4380a-185">Rigth click and select **Activate/Upgrade**.</span></span>
   
    <span data-ttu-id="4380a-186">d.</span><span class="sxs-lookup"><span data-stu-id="4380a-186">d.</span></span> <span data-ttu-id="4380a-187">Click the **Activate** button.</span><span class="sxs-lookup"><span data-stu-id="4380a-187">Click the **Activate** button.</span></span>

8. <span data-ttu-id="4380a-188">In the navigation pane on the left side, click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="4380a-188">In the navigation pane on the left side, click **Properties**.</span></span>  
   
    <span data-ttu-id="4380a-189">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="4380a-189">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

9. <span data-ttu-id="4380a-190">On the **Multiple Provider SSO Properties** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4380a-190">On the **Multiple Provider SSO Properties** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="4380a-191">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="4380a-191">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span></span>
   
    <span data-ttu-id="4380a-192">a.</span><span class="sxs-lookup"><span data-stu-id="4380a-192">a.</span></span> <span data-ttu-id="4380a-193">As **Enable multiple provider SSO**, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="4380a-193">As **Enable multiple provider SSO**, select **Yes**.</span></span>
   
    <span data-ttu-id="4380a-194">b.</span><span class="sxs-lookup"><span data-stu-id="4380a-194">b.</span></span> <span data-ttu-id="4380a-195">As **Enable debug logging got the multiple provider SSO integration**, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="4380a-195">As **Enable debug logging got the multiple provider SSO integration**, select **Yes**.</span></span>
   
    <span data-ttu-id="4380a-196">c.</span><span class="sxs-lookup"><span data-stu-id="4380a-196">c.</span></span> <span data-ttu-id="4380a-197">In **The field on the user table that...** textbox, type **user_name**.</span><span class="sxs-lookup"><span data-stu-id="4380a-197">In **The field on the user table that...** textbox, type **user_name**.</span></span>
   
    <span data-ttu-id="4380a-198">d.</span><span class="sxs-lookup"><span data-stu-id="4380a-198">d.</span></span> <span data-ttu-id="4380a-199">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4380a-199">Click **Save**.</span></span>

10. <span data-ttu-id="4380a-200">In the navigation pane on the left side, click **x509 Certificates**.</span><span class="sxs-lookup"><span data-stu-id="4380a-200">In the navigation pane on the left side, click **x509 Certificates**.</span></span>
    
     <span data-ttu-id="4380a-201">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-201">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="4380a-202">On the **X.509 Certificates** dialog, click **New**.</span><span class="sxs-lookup"><span data-stu-id="4380a-202">On the **X.509 Certificates** dialog, click **New**.</span></span>
    
     <span data-ttu-id="4380a-203">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-203">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="4380a-204">On the **X.509 Certificates** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4380a-204">On the **X.509 Certificates** dialog, perform the following steps:</span></span>
    
     <span data-ttu-id="4380a-205">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-205">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
     <span data-ttu-id="4380a-206">a.</span><span class="sxs-lookup"><span data-stu-id="4380a-206">a.</span></span> <span data-ttu-id="4380a-207">Click **New**.</span><span class="sxs-lookup"><span data-stu-id="4380a-207">Click **New**.</span></span>
    
     <span data-ttu-id="4380a-208">b.</span><span class="sxs-lookup"><span data-stu-id="4380a-208">b.</span></span> <span data-ttu-id="4380a-209">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="4380a-209">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
     <span data-ttu-id="4380a-210">c.</span><span class="sxs-lookup"><span data-stu-id="4380a-210">c.</span></span> <span data-ttu-id="4380a-211">Select **Active**.</span><span class="sxs-lookup"><span data-stu-id="4380a-211">Select **Active**.</span></span>
    
     <span data-ttu-id="4380a-212">d.</span><span class="sxs-lookup"><span data-stu-id="4380a-212">d.</span></span> <span data-ttu-id="4380a-213">As **Format**, select **PEM**.</span><span class="sxs-lookup"><span data-stu-id="4380a-213">As **Format**, select **PEM**.</span></span>
    
     <span data-ttu-id="4380a-214">e.</span><span class="sxs-lookup"><span data-stu-id="4380a-214">e.</span></span> <span data-ttu-id="4380a-215">As **Type**, select **Trust Store Cert**.</span><span class="sxs-lookup"><span data-stu-id="4380a-215">As **Type**, select **Trust Store Cert**.</span></span>
    
     <span data-ttu-id="4380a-216">f.</span><span class="sxs-lookup"><span data-stu-id="4380a-216">f.</span></span> <span data-ttu-id="4380a-217">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="4380a-217">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>
    
     <span data-ttu-id="4380a-218">g.</span><span class="sxs-lookup"><span data-stu-id="4380a-218">g.</span></span> <span data-ttu-id="4380a-219">Click **Update**.</span><span class="sxs-lookup"><span data-stu-id="4380a-219">Click **Update**.</span></span>

13. <span data-ttu-id="4380a-220">In the navigation pane on the left side, click **Identity Providers**.</span><span class="sxs-lookup"><span data-stu-id="4380a-220">In the navigation pane on the left side, click **Identity Providers**.</span></span>
    
     <span data-ttu-id="4380a-221">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-221">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

14. <span data-ttu-id="4380a-222">On the **Identity Providers** dialog, click **New**:</span><span class="sxs-lookup"><span data-stu-id="4380a-222">On the **Identity Providers** dialog, click **New**:</span></span>
    
     <span data-ttu-id="4380a-223">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-223">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span></span>

15. <span data-ttu-id="4380a-224">On the **Identity Providers** dialog, click **SAML2 Update1?**:</span><span class="sxs-lookup"><span data-stu-id="4380a-224">On the **Identity Providers** dialog, click **SAML2 Update1?**:</span></span>
    
     <span data-ttu-id="4380a-225">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-225">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span></span>

16. <span data-ttu-id="4380a-226">On the SAML2 Update1 Properties dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4380a-226">On the SAML2 Update1 Properties dialog, perform the following steps:</span></span>
    
     <span data-ttu-id="4380a-227">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-227">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="4380a-228">a.</span><span class="sxs-lookup"><span data-stu-id="4380a-228">a.</span></span> <span data-ttu-id="4380a-229">in the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="4380a-229">in the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="4380a-230">b.</span><span class="sxs-lookup"><span data-stu-id="4380a-230">b.</span></span> <span data-ttu-id="4380a-231">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span><span class="sxs-lookup"><span data-stu-id="4380a-231">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="4380a-232">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span><span class="sxs-lookup"><span data-stu-id="4380a-232">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="4380a-233">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span><span class="sxs-lookup"><span data-stu-id="4380a-233">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span></span>

    <span data-ttu-id="4380a-234">c.</span><span class="sxs-lookup"><span data-stu-id="4380a-234">c.</span></span> <span data-ttu-id="4380a-235">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="4380a-235">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="4380a-236">d.</span><span class="sxs-lookup"><span data-stu-id="4380a-236">d.</span></span> <span data-ttu-id="4380a-237">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span><span class="sxs-lookup"><span data-stu-id="4380a-237">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="4380a-238">e.</span><span class="sxs-lookup"><span data-stu-id="4380a-238">e.</span></span> <span data-ttu-id="4380a-239">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span><span class="sxs-lookup"><span data-stu-id="4380a-239">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="4380a-240">f.</span><span class="sxs-lookup"><span data-stu-id="4380a-240">f.</span></span> <span data-ttu-id="4380a-241">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span><span class="sxs-lookup"><span data-stu-id="4380a-241">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4380a-242">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="4380a-242">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="4380a-243">g.</span><span class="sxs-lookup"><span data-stu-id="4380a-243">g.</span></span> <span data-ttu-id="4380a-244">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span><span class="sxs-lookup"><span data-stu-id="4380a-244">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="4380a-245">h.</span><span class="sxs-lookup"><span data-stu-id="4380a-245">h.</span></span> <span data-ttu-id="4380a-246">In the **Audience URL** textbox, type the URL of your ServiceNow tenant.</span><span class="sxs-lookup"><span data-stu-id="4380a-246">In the **Audience URL** textbox, type the URL of your ServiceNow tenant.</span></span> 

    <span data-ttu-id="4380a-247">i.</span><span class="sxs-lookup"><span data-stu-id="4380a-247">i.</span></span> <span data-ttu-id="4380a-248">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span><span class="sxs-lookup"><span data-stu-id="4380a-248">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="4380a-249">j.</span><span class="sxs-lookup"><span data-stu-id="4380a-249">j.</span></span> <span data-ttu-id="4380a-250">In the NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span><span class="sxs-lookup"><span data-stu-id="4380a-250">In the NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="4380a-251">k.</span><span class="sxs-lookup"><span data-stu-id="4380a-251">k.</span></span> <span data-ttu-id="4380a-252">Deselect **Create an AuthnContextClass**.</span><span class="sxs-lookup"><span data-stu-id="4380a-252">Deselect **Create an AuthnContextClass**.</span></span>

    <span data-ttu-id="4380a-253">l.</span><span class="sxs-lookup"><span data-stu-id="4380a-253">l.</span></span> <span data-ttu-id="4380a-254">In the **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span><span class="sxs-lookup"><span data-stu-id="4380a-254">In the **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span> <span data-ttu-id="4380a-255">This is only needed if you are cloud only organization.</span><span class="sxs-lookup"><span data-stu-id="4380a-255">This is only needed if you are cloud only organization.</span></span> <span data-ttu-id="4380a-256">If you are using on premise ADFS or MFA for authentication then you should not configure this value.</span><span class="sxs-lookup"><span data-stu-id="4380a-256">If you are using on premise ADFS or MFA for authentication then you should not configure this value.</span></span> 

    <span data-ttu-id="4380a-257">m.</span><span class="sxs-lookup"><span data-stu-id="4380a-257">m.</span></span> <span data-ttu-id="4380a-258">In **Clock Skew** textbox, type **60**.</span><span class="sxs-lookup"><span data-stu-id="4380a-258">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="4380a-259">n.</span><span class="sxs-lookup"><span data-stu-id="4380a-259">n.</span></span> <span data-ttu-id="4380a-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span><span class="sxs-lookup"><span data-stu-id="4380a-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span></span>

    <span data-ttu-id="4380a-261">o.</span><span class="sxs-lookup"><span data-stu-id="4380a-261">o.</span></span> <span data-ttu-id="4380a-262">As **x509 Certificate**, select the certificate you have created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="4380a-262">As **x509 Certificate**, select the certificate you have created in the previous step.</span></span>

    <span data-ttu-id="4380a-263">p.</span><span class="sxs-lookup"><span data-stu-id="4380a-263">p.</span></span> <span data-ttu-id="4380a-264">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="4380a-264">Click **Submit**.</span></span> 

1. <span data-ttu-id="4380a-265">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4380a-265">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="4380a-266">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-266">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="4380a-267">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="4380a-267">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="4380a-268">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-268">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="4380a-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="4380a-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span></span>
1. <span data-ttu-id="4380a-270">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="4380a-270">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="4380a-271">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-271">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="4380a-272">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4380a-272">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="4380a-273">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-273">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="4380a-274">On the **Configure App Settings** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4380a-274">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="4380a-275">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="4380a-275">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="4380a-276">a.</span><span class="sxs-lookup"><span data-stu-id="4380a-276">a.</span></span> <span data-ttu-id="4380a-277">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="4380a-277">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="4380a-278">b.</span><span class="sxs-lookup"><span data-stu-id="4380a-278">b.</span></span> <span data-ttu-id="4380a-279">In the **Issuer URL** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="4380a-279">In the **Issuer URL** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="4380a-280">c.</span><span class="sxs-lookup"><span data-stu-id="4380a-280">c.</span></span> <span data-ttu-id="4380a-281">Click **Next**</span><span class="sxs-lookup"><span data-stu-id="4380a-281">Click **Next**</span></span>

4. <span data-ttu-id="4380a-282">Click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span><span class="sxs-lookup"><span data-stu-id="4380a-282">Click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span></span>
   
    <span data-ttu-id="4380a-283">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="4380a-283">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="4380a-284">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4380a-284">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="4380a-285">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-285">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="4380a-286">Sign-on to your ServiceNow Express application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="4380a-286">Sign-on to your ServiceNow Express application as an administrator.</span></span>

7. <span data-ttu-id="4380a-287">In the navigation pane on the left side, click **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="4380a-287">In the navigation pane on the left side, click **Single Sign-On**.</span></span>  
   
    <span data-ttu-id="4380a-288">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="4380a-288">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

8. <span data-ttu-id="4380a-289">On the **Single Sign-On** dialog, click the configuration icon on the upper right and set the following properties:</span><span class="sxs-lookup"><span data-stu-id="4380a-289">On the **Single Sign-On** dialog, click the configuration icon on the upper right and set the following properties:</span></span>
   
    <span data-ttu-id="4380a-290">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span><span class="sxs-lookup"><span data-stu-id="4380a-290">![Configure app URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>
   
    <span data-ttu-id="4380a-291">a.</span><span class="sxs-lookup"><span data-stu-id="4380a-291">a.</span></span> <span data-ttu-id="4380a-292">Toggle **Enable multiple provider SSO** to the right.</span><span class="sxs-lookup"><span data-stu-id="4380a-292">Toggle **Enable multiple provider SSO** to the right.</span></span>
   
    <span data-ttu-id="4380a-293">b.</span><span class="sxs-lookup"><span data-stu-id="4380a-293">b.</span></span> <span data-ttu-id="4380a-294">Toggle **Enable debug logging for the multiple provider SSO integration** to the right.</span><span class="sxs-lookup"><span data-stu-id="4380a-294">Toggle **Enable debug logging for the multiple provider SSO integration** to the right.</span></span>
   
    <span data-ttu-id="4380a-295">c.</span><span class="sxs-lookup"><span data-stu-id="4380a-295">c.</span></span> <span data-ttu-id="4380a-296">In **The field on the user table that...** textbox, type **user_name**.</span><span class="sxs-lookup"><span data-stu-id="4380a-296">In **The field on the user table that...** textbox, type **user_name**.</span></span>
9. <span data-ttu-id="4380a-297">On the **Single Sign-On** dialog, click **Add New Certificate**.</span><span class="sxs-lookup"><span data-stu-id="4380a-297">On the **Single Sign-On** dialog, click **Add New Certificate**.</span></span>
   
    <span data-ttu-id="4380a-298">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-298">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>
10. <span data-ttu-id="4380a-299">On the **X.509 Certificates** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4380a-299">On the **X.509 Certificates** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="4380a-300">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-300">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
    <span data-ttu-id="4380a-301">a.</span><span class="sxs-lookup"><span data-stu-id="4380a-301">a.</span></span> <span data-ttu-id="4380a-302">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="4380a-302">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
    <span data-ttu-id="4380a-303">b.</span><span class="sxs-lookup"><span data-stu-id="4380a-303">b.</span></span> <span data-ttu-id="4380a-304">Select **Active**.</span><span class="sxs-lookup"><span data-stu-id="4380a-304">Select **Active**.</span></span>
    
    <span data-ttu-id="4380a-305">c.</span><span class="sxs-lookup"><span data-stu-id="4380a-305">c.</span></span> <span data-ttu-id="4380a-306">As **Format**, select **PEM**.</span><span class="sxs-lookup"><span data-stu-id="4380a-306">As **Format**, select **PEM**.</span></span>
    
    <span data-ttu-id="4380a-307">d.</span><span class="sxs-lookup"><span data-stu-id="4380a-307">d.</span></span> <span data-ttu-id="4380a-308">As **Type**, select **Trust Store Cert**.</span><span class="sxs-lookup"><span data-stu-id="4380a-308">As **Type**, select **Trust Store Cert**.</span></span>
    
    <span data-ttu-id="4380a-309">e.</span><span class="sxs-lookup"><span data-stu-id="4380a-309">e.</span></span> <span data-ttu-id="4380a-310">Create a Base64 encoded file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="4380a-310">Create a Base64 encoded file from your downloaded certificate.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="4380a-311">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="4380a-311">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
    > 
    > 
    
    <span data-ttu-id="4380a-312">f.</span><span class="sxs-lookup"><span data-stu-id="4380a-312">f.</span></span> <span data-ttu-id="4380a-313">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="4380a-313">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>
    
    <span data-ttu-id="4380a-314">g.</span><span class="sxs-lookup"><span data-stu-id="4380a-314">g.</span></span> <span data-ttu-id="4380a-315">Click **Update**.</span><span class="sxs-lookup"><span data-stu-id="4380a-315">Click **Update**.</span></span>
11. <span data-ttu-id="4380a-316">On the **Single Sign-On** dialog, click **Add New IdP**.</span><span class="sxs-lookup"><span data-stu-id="4380a-316">On the **Single Sign-On** dialog, click **Add New IdP**.</span></span>
    
    <span data-ttu-id="4380a-317">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-317">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>
12. <span data-ttu-id="4380a-318">On the **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4380a-318">On the **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform the following steps:</span></span>
    
    <span data-ttu-id="4380a-319">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-319">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="4380a-320">a.</span><span class="sxs-lookup"><span data-stu-id="4380a-320">a.</span></span> <span data-ttu-id="4380a-321">In the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="4380a-321">In the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="4380a-322">b.</span><span class="sxs-lookup"><span data-stu-id="4380a-322">b.</span></span> <span data-ttu-id="4380a-323">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="4380a-323">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="4380a-324">c.</span><span class="sxs-lookup"><span data-stu-id="4380a-324">c.</span></span> <span data-ttu-id="4380a-325">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span><span class="sxs-lookup"><span data-stu-id="4380a-325">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="4380a-326">d.</span><span class="sxs-lookup"><span data-stu-id="4380a-326">d.</span></span> <span data-ttu-id="4380a-327">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span><span class="sxs-lookup"><span data-stu-id="4380a-327">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="4380a-328">e.</span><span class="sxs-lookup"><span data-stu-id="4380a-328">e.</span></span> <span data-ttu-id="4380a-329">As **Identity Provider Certificate**, select the certificate you have created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="4380a-329">As **Identity Provider Certificate**, select the certificate you have created in the previous step.</span></span>


1. <span data-ttu-id="4380a-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4380a-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform the following steps:</span></span>
   
    <span data-ttu-id="4380a-331">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-331">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="4380a-332">a.</span><span class="sxs-lookup"><span data-stu-id="4380a-332">a.</span></span> <span data-ttu-id="4380a-333">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span><span class="sxs-lookup"><span data-stu-id="4380a-333">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>
   
    <span data-ttu-id="4380a-334">b.</span><span class="sxs-lookup"><span data-stu-id="4380a-334">b.</span></span> <span data-ttu-id="4380a-335">In the **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span><span class="sxs-lookup"><span data-stu-id="4380a-335">In the **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>    
   
    <span data-ttu-id="4380a-336">c.</span><span class="sxs-lookup"><span data-stu-id="4380a-336">c.</span></span> <span data-ttu-id="4380a-337">In the **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span><span class="sxs-lookup"><span data-stu-id="4380a-337">In the **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span></span>
   
    <span data-ttu-id="4380a-338">d.</span><span class="sxs-lookup"><span data-stu-id="4380a-338">d.</span></span> <span data-ttu-id="4380a-339">Deselect **Create an AuthnContextClass**.</span><span class="sxs-lookup"><span data-stu-id="4380a-339">Deselect **Create an AuthnContextClass**.</span></span>

2. <span data-ttu-id="4380a-340">Under **Additional Service Provider Properties**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4380a-340">Under **Additional Service Provider Properties**, perform the following steps:</span></span>
   
    <span data-ttu-id="4380a-341">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-341">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="4380a-342">a.</span><span class="sxs-lookup"><span data-stu-id="4380a-342">a.</span></span> <span data-ttu-id="4380a-343">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span><span class="sxs-lookup"><span data-stu-id="4380a-343">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="4380a-344">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="4380a-344">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span></span>
    > 
    > 
   
    <span data-ttu-id="4380a-345">b.</span><span class="sxs-lookup"><span data-stu-id="4380a-345">b.</span></span> <span data-ttu-id="4380a-346">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span><span class="sxs-lookup"><span data-stu-id="4380a-346">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span></span>
   
    <span data-ttu-id="4380a-347">c.</span><span class="sxs-lookup"><span data-stu-id="4380a-347">c.</span></span> <span data-ttu-id="4380a-348">In the **Audience URI** textbox, type the URL of your ServiceNow tenant.</span><span class="sxs-lookup"><span data-stu-id="4380a-348">In the **Audience URI** textbox, type the URL of your ServiceNow tenant.</span></span> 
   
    <span data-ttu-id="4380a-349">d.</span><span class="sxs-lookup"><span data-stu-id="4380a-349">d.</span></span> <span data-ttu-id="4380a-350">In **Clock Skew** textbox, type **60**.</span><span class="sxs-lookup"><span data-stu-id="4380a-350">In **Clock Skew** textbox, type **60**.</span></span>
   
    <span data-ttu-id="4380a-351">e.</span><span class="sxs-lookup"><span data-stu-id="4380a-351">e.</span></span> <span data-ttu-id="4380a-352">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span><span class="sxs-lookup"><span data-stu-id="4380a-352">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="4380a-353">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span><span class="sxs-lookup"><span data-stu-id="4380a-353">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="4380a-354">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span><span class="sxs-lookup"><span data-stu-id="4380a-354">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span></span>
    > 
    > 
   
    <span data-ttu-id="4380a-355">f.</span><span class="sxs-lookup"><span data-stu-id="4380a-355">f.</span></span> <span data-ttu-id="4380a-356">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4380a-356">Click **Save**.</span></span> 

3. <span data-ttu-id="4380a-357">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4380a-357">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="4380a-358">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-358">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="4380a-359">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="4380a-359">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="4380a-360">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span><span class="sxs-lookup"><span data-stu-id="4380a-360">![Configure single sign-on](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="4380a-361">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="4380a-361">Configuring user provisioning</span></span>
<span data-ttu-id="4380a-362">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="4380a-362">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to ServiceNow.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="4380a-363">To configure user provisioning, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4380a-363">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="4380a-364">In the Azure Management classic portal, on the **ServiceNow** application integration page, click **Configure user provisioning**.</span><span class="sxs-lookup"><span data-stu-id="4380a-364">In the Azure Management classic portal, on the **ServiceNow** application integration page, click **Configure user provisioning**.</span></span> 
   
    <span data-ttu-id="4380a-365">![User provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span><span class="sxs-lookup"><span data-stu-id="4380a-365">![User provisioning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span></span>

2. <span data-ttu-id="4380a-366">On the **Enter your ServiceNow credentials to enable automatic user provisioning** page, provide the following configuration settings:</span><span class="sxs-lookup"><span data-stu-id="4380a-366">On the **Enter your ServiceNow credentials to enable automatic user provisioning** page, provide the following configuration settings:</span></span>
   
     <span data-ttu-id="4380a-367">a.</span><span class="sxs-lookup"><span data-stu-id="4380a-367">a.</span></span> <span data-ttu-id="4380a-368">In the **ServiceNow Instance Name** textbox, type the ServiceNow instance name.</span><span class="sxs-lookup"><span data-stu-id="4380a-368">In the **ServiceNow Instance Name** textbox, type the ServiceNow instance name.</span></span>
   
     <span data-ttu-id="4380a-369">b.</span><span class="sxs-lookup"><span data-stu-id="4380a-369">b.</span></span> <span data-ttu-id="4380a-370">In the **ServiceNow Admin User Name** textbox, type the name of the ServiceNow admin account.</span><span class="sxs-lookup"><span data-stu-id="4380a-370">In the **ServiceNow Admin User Name** textbox, type the name of the ServiceNow admin account.</span></span>
   
     <span data-ttu-id="4380a-371">c.</span><span class="sxs-lookup"><span data-stu-id="4380a-371">c.</span></span> <span data-ttu-id="4380a-372">In the **ServiceNow Admin Password** textbox, type the password for this account.</span><span class="sxs-lookup"><span data-stu-id="4380a-372">In the **ServiceNow Admin Password** textbox, type the password for this account.</span></span>
   
     <span data-ttu-id="4380a-373">d.</span><span class="sxs-lookup"><span data-stu-id="4380a-373">d.</span></span> <span data-ttu-id="4380a-374">Click **validate** to verify your configuration.</span><span class="sxs-lookup"><span data-stu-id="4380a-374">Click **validate** to verify your configuration.</span></span>
   
     <span data-ttu-id="4380a-375">e.</span><span class="sxs-lookup"><span data-stu-id="4380a-375">e.</span></span> <span data-ttu-id="4380a-376">Click the **Next** button to open the **Next steps** page.</span><span class="sxs-lookup"><span data-stu-id="4380a-376">Click the **Next** button to open the **Next steps** page.</span></span>
   
     <span data-ttu-id="4380a-377">f.</span><span class="sxs-lookup"><span data-stu-id="4380a-377">f.</span></span> <span data-ttu-id="4380a-378">If you want to provision all users to this application, select “**Automatically provision all user accounts in the directory to this application**”.</span><span class="sxs-lookup"><span data-stu-id="4380a-378">If you want to provision all users to this application, select “**Automatically provision all user accounts in the directory to this application**”.</span></span> 
   
    <span data-ttu-id="4380a-379">![Next Steps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span><span class="sxs-lookup"><span data-stu-id="4380a-379">![Next Steps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span></span>
   
     <span data-ttu-id="4380a-380">g.</span><span class="sxs-lookup"><span data-stu-id="4380a-380">g.</span></span> <span data-ttu-id="4380a-381">On the **Next steps** page, click **Complete** to save your configuration.</span><span class="sxs-lookup"><span data-stu-id="4380a-381">On the **Next steps** page, click **Complete** to save your configuration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4380a-382">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4380a-382">Creating an Azure AD test user</span></span>
<span data-ttu-id="4380a-383">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4380a-383">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="4380a-385">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4380a-385">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4380a-386">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4380a-386">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="4380a-388">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="4380a-388">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="4380a-389">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="4380a-389">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4380a-391">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="4380a-391">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="4380a-393">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4380a-393">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="4380a-395">a.</span><span class="sxs-lookup"><span data-stu-id="4380a-395">a.</span></span> <span data-ttu-id="4380a-396">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="4380a-396">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="4380a-397">b.</span><span class="sxs-lookup"><span data-stu-id="4380a-397">b.</span></span> <span data-ttu-id="4380a-398">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4380a-398">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="4380a-399">c.</span><span class="sxs-lookup"><span data-stu-id="4380a-399">c.</span></span> <span data-ttu-id="4380a-400">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4380a-400">Click **Next**.</span></span>

6. <span data-ttu-id="4380a-401">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4380a-401">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="4380a-403">a.</span><span class="sxs-lookup"><span data-stu-id="4380a-403">a.</span></span> <span data-ttu-id="4380a-404">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="4380a-404">In the **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="4380a-405">b.</span><span class="sxs-lookup"><span data-stu-id="4380a-405">b.</span></span> <span data-ttu-id="4380a-406">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="4380a-406">In the **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="4380a-407">c.</span><span class="sxs-lookup"><span data-stu-id="4380a-407">c.</span></span> <span data-ttu-id="4380a-408">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4380a-408">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="4380a-409">d.</span><span class="sxs-lookup"><span data-stu-id="4380a-409">d.</span></span> <span data-ttu-id="4380a-410">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="4380a-410">In the **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="4380a-411">e.</span><span class="sxs-lookup"><span data-stu-id="4380a-411">e.</span></span> <span data-ttu-id="4380a-412">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="4380a-412">Click **Next**.</span></span>

7. <span data-ttu-id="4380a-413">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="4380a-413">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="4380a-415">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4380a-415">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="4380a-417">a.</span><span class="sxs-lookup"><span data-stu-id="4380a-417">a.</span></span> <span data-ttu-id="4380a-418">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="4380a-418">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="4380a-419">b.</span><span class="sxs-lookup"><span data-stu-id="4380a-419">b.</span></span> <span data-ttu-id="4380a-420">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="4380a-420">Click **Complete**.</span></span>   

### <a name="creating-a-servicenow-test-user"></a><span data-ttu-id="4380a-421">Creating a ServiceNow test user</span><span class="sxs-lookup"><span data-stu-id="4380a-421">Creating a ServiceNow test user</span></span>
<span data-ttu-id="4380a-422">In this section, you create a user called Britta Simon in ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="4380a-422">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="4380a-423">In this section, you create a user called Britta Simon in ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="4380a-423">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="4380a-424">If you don't know how to add a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span><span class="sxs-lookup"><span data-stu-id="4380a-424">If you don't know how to add a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4380a-425">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4380a-425">Assigning the Azure AD test user</span></span>
<span data-ttu-id="4380a-426">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="4380a-426">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceNow.</span></span>

![Assign User][200] 

<span data-ttu-id="4380a-428">**To assign Britta Simon to ServiceNow, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4380a-428">**To assign Britta Simon to ServiceNow, perform the following steps:**</span></span>

1. <span data-ttu-id="4380a-429">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="4380a-429">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 

2. <span data-ttu-id="4380a-431">In the applications list, select **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="4380a-431">In the applications list, select **ServiceNow**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. <span data-ttu-id="4380a-433">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="4380a-433">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 

4. <span data-ttu-id="4380a-435">In the All Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4380a-435">In the All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="4380a-436">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="4380a-436">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="4380a-438">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="4380a-438">Testing single sign-on</span></span>
<span data-ttu-id="4380a-439">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4380a-439">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4380a-440">When you click the ServiceNow tile in the Access Panel, you should get automatically signed-on to your ServiceNow application.</span><span class="sxs-lookup"><span data-stu-id="4380a-440">When you click the ServiceNow tile in the Access Panel, you should get automatically signed-on to your ServiceNow application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4380a-441">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4380a-441">Additional resources</span></span>
* [<span data-ttu-id="4380a-442">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4380a-442">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4380a-443">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4380a-443">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png



























































