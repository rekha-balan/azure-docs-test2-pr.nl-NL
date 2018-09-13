---
title: 'Tutorial: Azure Active Directory integration with PolicyStat | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and PolicyStat.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 571b1723c1c064415e4d8cbee3620799af14d508
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968164"
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a><span data-ttu-id="0aa05-103">Tutorial: Azure Active Directory integration with PolicyStat</span><span class="sxs-lookup"><span data-stu-id="0aa05-103">Tutorial: Azure Active Directory integration with PolicyStat</span></span>

<span data-ttu-id="0aa05-104">In this tutorial, you learn how to integrate PolicyStat with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0aa05-104">In this tutorial, you learn how to integrate PolicyStat with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0aa05-105">Integrating PolicyStat with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="0aa05-105">Integrating PolicyStat with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0aa05-106">You can control in Azure AD who has access to PolicyStat</span><span class="sxs-lookup"><span data-stu-id="0aa05-106">You can control in Azure AD who has access to PolicyStat</span></span>
- <span data-ttu-id="0aa05-107">You can enable your users to automatically get signed-on to PolicyStat (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="0aa05-107">You can enable your users to automatically get signed-on to PolicyStat (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0aa05-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="0aa05-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0aa05-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="0aa05-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0aa05-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0aa05-110">Prerequisites</span></span>

<span data-ttu-id="0aa05-111">To configure Azure AD integration with PolicyStat, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="0aa05-111">To configure Azure AD integration with PolicyStat, you need the following items:</span></span>

- <span data-ttu-id="0aa05-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="0aa05-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0aa05-113">A PolicyStat single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="0aa05-113">A PolicyStat single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0aa05-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="0aa05-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0aa05-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="0aa05-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0aa05-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="0aa05-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0aa05-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0aa05-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0aa05-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="0aa05-118">Scenario description</span></span>
<span data-ttu-id="0aa05-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="0aa05-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0aa05-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="0aa05-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0aa05-121">Adding PolicyStat from the gallery</span><span class="sxs-lookup"><span data-stu-id="0aa05-121">Adding PolicyStat from the gallery</span></span>
1. <span data-ttu-id="0aa05-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0aa05-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-policystat-from-the-gallery"></a><span data-ttu-id="0aa05-123">Adding PolicyStat from the gallery</span><span class="sxs-lookup"><span data-stu-id="0aa05-123">Adding PolicyStat from the gallery</span></span>
<span data-ttu-id="0aa05-124">To configure the integration of PolicyStat into Azure AD, you need to add PolicyStat from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="0aa05-124">To configure the integration of PolicyStat into Azure AD, you need to add PolicyStat from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0aa05-125">**To add PolicyStat from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0aa05-125">**To add PolicyStat from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0aa05-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="0aa05-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="0aa05-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="0aa05-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0aa05-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0aa05-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="0aa05-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="0aa05-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="0aa05-133">In the search box, type **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="0aa05-133">In the search box, type **PolicyStat**.</span></span>

    ![Creating an Azure AD test user](./media/policystat-tutorial/tutorial_policystat_search.png)

1. <span data-ttu-id="0aa05-135">In the results panel, select **PolicyStat**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="0aa05-135">In the results panel, select **PolicyStat**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0aa05-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0aa05-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0aa05-138">In this section, you configure and test Azure AD single sign-on with PolicyStat based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0aa05-138">In this section, you configure and test Azure AD single sign-on with PolicyStat based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0aa05-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PolicyStat is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0aa05-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PolicyStat is to a user in Azure AD.</span></span> <span data-ttu-id="0aa05-140">In other words, a link relationship between an Azure AD user and the related user in PolicyStat needs to be established.</span><span class="sxs-lookup"><span data-stu-id="0aa05-140">In other words, a link relationship between an Azure AD user and the related user in PolicyStat needs to be established.</span></span>

<span data-ttu-id="0aa05-141">In PolicyStat, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="0aa05-141">In PolicyStat, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0aa05-142">To configure and test Azure AD single sign-on with PolicyStat, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="0aa05-142">To configure and test Azure AD single sign-on with PolicyStat, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0aa05-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="0aa05-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="0aa05-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0aa05-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="0aa05-145">**[Creating a PolicyStat test user](#creating-a-policystat-test-user)** - to have a counterpart of Britta Simon in PolicyStat that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="0aa05-145">**[Creating a PolicyStat test user](#creating-a-policystat-test-user)** - to have a counterpart of Britta Simon in PolicyStat that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="0aa05-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0aa05-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="0aa05-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="0aa05-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0aa05-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0aa05-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0aa05-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PolicyStat application.</span><span class="sxs-lookup"><span data-stu-id="0aa05-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PolicyStat application.</span></span>

<span data-ttu-id="0aa05-150">**To configure Azure AD single sign-on with PolicyStat, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0aa05-150">**To configure Azure AD single sign-on with PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="0aa05-151">In the Azure portal, on the **PolicyStat** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="0aa05-151">In the Azure portal, on the **PolicyStat** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="0aa05-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0aa05-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/policystat-tutorial/tutorial_policystat_samlbase.png)

1. <span data-ttu-id="0aa05-155">On the **PolicyStat Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0aa05-155">On the **PolicyStat Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/policystat-tutorial/tutorial_policystat_url.png)

    <span data-ttu-id="0aa05-157">a.</span><span class="sxs-lookup"><span data-stu-id="0aa05-157">a.</span></span> <span data-ttu-id="0aa05-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com`</span><span class="sxs-lookup"><span data-stu-id="0aa05-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com`</span></span>

    <span data-ttu-id="0aa05-159">b.</span><span class="sxs-lookup"><span data-stu-id="0aa05-159">b.</span></span> <span data-ttu-id="0aa05-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="0aa05-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0aa05-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="0aa05-161">These values are not real.</span></span> <span data-ttu-id="0aa05-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="0aa05-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0aa05-163">Contact [PolicyStat Client support team](http://www.policystat.com/support/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="0aa05-163">Contact [PolicyStat Client support team](http://www.policystat.com/support/) to get these values.</span></span> 
 
1. <span data-ttu-id="0aa05-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="0aa05-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/policystat-tutorial/tutorial_policystat_certificate.png) 

1. <span data-ttu-id="0aa05-166">The objective of this section is to outline how to enable users to authenticate to PolicyStat with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="0aa05-166">The objective of this section is to outline how to enable users to authenticate to PolicyStat with their account in Azure AD using federation based on the SAML protocol.</span></span>

    <span data-ttu-id="0aa05-167">The PolicyStat application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span><span class="sxs-lookup"><span data-stu-id="0aa05-167">The PolicyStat application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span>  

     <span data-ttu-id="0aa05-168">The following screenshot shows an example of this.</span><span class="sxs-lookup"><span data-stu-id="0aa05-168">The following screenshot shows an example of this.</span></span>

     <span data-ttu-id="0aa05-169">![Attributes](./media/policystat-tutorial/tutorial_policystat_attribute.png "Attributes")</span><span class="sxs-lookup"><span data-stu-id="0aa05-169">![Attributes](./media/policystat-tutorial/tutorial_policystat_attribute.png "Attributes")</span></span>

1. <span data-ttu-id="0aa05-170">To add the required attribute mappings, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0aa05-170">To add the required attribute mappings, perform the following steps:</span></span>

    | <span data-ttu-id="0aa05-171">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="0aa05-171">Attribute Name</span></span>    |   <span data-ttu-id="0aa05-172">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="0aa05-172">Attribute Value</span></span> |
    |------------------- | -------------------- |
    | <span data-ttu-id="0aa05-173">uid</span><span class="sxs-lookup"><span data-stu-id="0aa05-173">uid</span></span> | <span data-ttu-id="0aa05-174">ExtractMailPrefix([mail])</span><span class="sxs-lookup"><span data-stu-id="0aa05-174">ExtractMailPrefix([mail])</span></span> |
    
    <span data-ttu-id="0aa05-175">a.</span><span class="sxs-lookup"><span data-stu-id="0aa05-175">a.</span></span> <span data-ttu-id="0aa05-176">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="0aa05-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/policystat-tutorial/tutorial_policystat_04.png)

    ![Configure Single Sign-On](./media/policystat-tutorial/tutorial_policystat_addatribute.png)
    
    <span data-ttu-id="0aa05-179">b.</span><span class="sxs-lookup"><span data-stu-id="0aa05-179">b.</span></span> <span data-ttu-id="0aa05-180">In the **Attribute Name** textbox, type **uid**.</span><span class="sxs-lookup"><span data-stu-id="0aa05-180">In the **Attribute Name** textbox, type **uid**.</span></span>

    <span data-ttu-id="0aa05-181">c.</span><span class="sxs-lookup"><span data-stu-id="0aa05-181">c.</span></span> <span data-ttu-id="0aa05-182">In the **Attribute Value** textbox, select **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="0aa05-182">In the **Attribute Value** textbox, select **ExtractMailPrefix()**.</span></span>    
   
    <span data-ttu-id="0aa05-183">d.</span><span class="sxs-lookup"><span data-stu-id="0aa05-183">d.</span></span> <span data-ttu-id="0aa05-184">From the **Mail** list, select **User.mail**.</span><span class="sxs-lookup"><span data-stu-id="0aa05-184">From the **Mail** list, select **User.mail**.</span></span>
    
    <span data-ttu-id="0aa05-185">e.</span><span class="sxs-lookup"><span data-stu-id="0aa05-185">e.</span></span> <span data-ttu-id="0aa05-186">Click **Ok**</span><span class="sxs-lookup"><span data-stu-id="0aa05-186">Click **Ok**</span></span>

1. <span data-ttu-id="0aa05-187">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="0aa05-187">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/policystat-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="0aa05-189">In a different web browser window, log into your PolicyStat company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="0aa05-189">In a different web browser window, log into your PolicyStat company site as an administrator.</span></span>

1. <span data-ttu-id="0aa05-190">Click the **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span><span class="sxs-lookup"><span data-stu-id="0aa05-190">Click the **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span></span>
   
    <span data-ttu-id="0aa05-191">![Administrator Menu](./media/policystat-tutorial/ic808633.png "Administrator Menu")</span><span class="sxs-lookup"><span data-stu-id="0aa05-191">![Administrator Menu](./media/policystat-tutorial/ic808633.png "Administrator Menu")</span></span>

1. <span data-ttu-id="0aa05-192">In the **Setup** section, select **Enable Single Sign-on Integration**.</span><span class="sxs-lookup"><span data-stu-id="0aa05-192">In the **Setup** section, select **Enable Single Sign-on Integration**.</span></span>
   
    <span data-ttu-id="0aa05-193">![Single Sign-On Configuration](./media/policystat-tutorial/ic808634.png "Single Sign-On Configuration")</span><span class="sxs-lookup"><span data-stu-id="0aa05-193">![Single Sign-On Configuration](./media/policystat-tutorial/ic808634.png "Single Sign-On Configuration")</span></span>

1. <span data-ttu-id="0aa05-194">Click **Configure Attributes**, and then, in the **Configure Attributes** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0aa05-194">Click **Configure Attributes**, and then, in the **Configure Attributes** section, perform the following steps:</span></span>
   
    <span data-ttu-id="0aa05-195">![Single Sign-On Configuration](./media/policystat-tutorial/ic808635.png "Single Sign-On Configuration")</span><span class="sxs-lookup"><span data-stu-id="0aa05-195">![Single Sign-On Configuration](./media/policystat-tutorial/ic808635.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="0aa05-196">a.</span><span class="sxs-lookup"><span data-stu-id="0aa05-196">a.</span></span> <span data-ttu-id="0aa05-197">In the **Username Attribute** textbox, type **uid**.</span><span class="sxs-lookup"><span data-stu-id="0aa05-197">In the **Username Attribute** textbox, type **uid**.</span></span>

    <span data-ttu-id="0aa05-198">b.</span><span class="sxs-lookup"><span data-stu-id="0aa05-198">b.</span></span> <span data-ttu-id="0aa05-199">In the **First Name Attribute** textbox, type **firstname** of user **Britta**.</span><span class="sxs-lookup"><span data-stu-id="0aa05-199">In the **First Name Attribute** textbox, type **firstname** of user **Britta**.</span></span>

    <span data-ttu-id="0aa05-200">c.</span><span class="sxs-lookup"><span data-stu-id="0aa05-200">c.</span></span> <span data-ttu-id="0aa05-201">In the **Last Name Attribute** textbox, type **lastname** of user **Simon**.</span><span class="sxs-lookup"><span data-stu-id="0aa05-201">In the **Last Name Attribute** textbox, type **lastname** of user **Simon**.</span></span>

    <span data-ttu-id="0aa05-202">d.</span><span class="sxs-lookup"><span data-stu-id="0aa05-202">d.</span></span> <span data-ttu-id="0aa05-203">In the **Email Attribute** textbox, type **emailaddress** of user **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="0aa05-203">In the **Email Attribute** textbox, type **emailaddress** of user **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="0aa05-204">e.</span><span class="sxs-lookup"><span data-stu-id="0aa05-204">e.</span></span> <span data-ttu-id="0aa05-205">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="0aa05-205">Click **Save Changes**.</span></span>

1. <span data-ttu-id="0aa05-206">Click **Your IDP Metadata**, and then, in the **Your IDP Metadata** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0aa05-206">Click **Your IDP Metadata**, and then, in the **Your IDP Metadata** section, perform the following steps:</span></span>
   
    <span data-ttu-id="0aa05-207">![Single Sign-On Configuration](./media/policystat-tutorial/ic808636.png "Single Sign-On Configuration")</span><span class="sxs-lookup"><span data-stu-id="0aa05-207">![Single Sign-On Configuration](./media/policystat-tutorial/ic808636.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="0aa05-208">a.</span><span class="sxs-lookup"><span data-stu-id="0aa05-208">a.</span></span> <span data-ttu-id="0aa05-209">Open your downloaded metadata file, copy the content, and  then paste it into the **Your Identity Provider Metadata** textbox.</span><span class="sxs-lookup"><span data-stu-id="0aa05-209">Open your downloaded metadata file, copy the content, and  then paste it into the **Your Identity Provider Metadata** textbox.</span></span>

    <span data-ttu-id="0aa05-210">b.</span><span class="sxs-lookup"><span data-stu-id="0aa05-210">b.</span></span> <span data-ttu-id="0aa05-211">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="0aa05-211">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="0aa05-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="0aa05-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0aa05-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="0aa05-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0aa05-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0aa05-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0aa05-215">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0aa05-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="0aa05-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0aa05-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="0aa05-218">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0aa05-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0aa05-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="0aa05-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/policystat-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="0aa05-221">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="0aa05-221">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/policystat-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="0aa05-223">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="0aa05-223">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/policystat-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="0aa05-225">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0aa05-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/policystat-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0aa05-227">a.</span><span class="sxs-lookup"><span data-stu-id="0aa05-227">a.</span></span> <span data-ttu-id="0aa05-228">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0aa05-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0aa05-229">b.</span><span class="sxs-lookup"><span data-stu-id="0aa05-229">b.</span></span> <span data-ttu-id="0aa05-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0aa05-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0aa05-231">c.</span><span class="sxs-lookup"><span data-stu-id="0aa05-231">c.</span></span> <span data-ttu-id="0aa05-232">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="0aa05-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0aa05-233">d.</span><span class="sxs-lookup"><span data-stu-id="0aa05-233">d.</span></span> <span data-ttu-id="0aa05-234">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0aa05-234">Click **Create**.</span></span>
 
### <a name="creating-a-policystat-test-user"></a><span data-ttu-id="0aa05-235">Creating a PolicyStat test user</span><span class="sxs-lookup"><span data-stu-id="0aa05-235">Creating a PolicyStat test user</span></span>

<span data-ttu-id="0aa05-236">In order to enable Azure AD users to log into PolicyStat, they must be provisioned into PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="0aa05-236">In order to enable Azure AD users to log into PolicyStat, they must be provisioned into PolicyStat.</span></span>  

<span data-ttu-id="0aa05-237">PolicyStat supports just in time user provisioning.</span><span class="sxs-lookup"><span data-stu-id="0aa05-237">PolicyStat supports just in time user provisioning.</span></span> <span data-ttu-id="0aa05-238">This means, you do not need to add the users manually to PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="0aa05-238">This means, you do not need to add the users manually to PolicyStat.</span></span> <span data-ttu-id="0aa05-239">The users will get added automatically on their first login through SSO.</span><span class="sxs-lookup"><span data-stu-id="0aa05-239">The users will get added automatically on their first login through SSO.</span></span>

>[!NOTE]
><span data-ttu-id="0aa05-240">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="0aa05-240">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat to provision Azure AD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0aa05-241">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0aa05-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0aa05-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="0aa05-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PolicyStat.</span></span>

![Assign User][200] 

<span data-ttu-id="0aa05-244">**To assign Britta Simon to PolicyStat, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0aa05-244">**To assign Britta Simon to PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="0aa05-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0aa05-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="0aa05-247">In the applications list, select **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="0aa05-247">In the applications list, select **PolicyStat**.</span></span>

    ![Configure Single Sign-On](./media/policystat-tutorial/tutorial_policystat_app.png) 

1. <span data-ttu-id="0aa05-249">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="0aa05-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="0aa05-251">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="0aa05-251">Click **Add** button.</span></span> <span data-ttu-id="0aa05-252">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0aa05-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="0aa05-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="0aa05-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="0aa05-255">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="0aa05-255">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="0aa05-256">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0aa05-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0aa05-257">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="0aa05-257">Testing single sign-on</span></span>

<span data-ttu-id="0aa05-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="0aa05-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0aa05-259">When you click the PolicyStat tile in the Access Panel, you should get automatically signed-on to your PolicyStat application.</span><span class="sxs-lookup"><span data-stu-id="0aa05-259">When you click the PolicyStat tile in the Access Panel, you should get automatically signed-on to your PolicyStat application.</span></span>
<span data-ttu-id="0aa05-260">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0aa05-260">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0aa05-261">Additional resources</span><span class="sxs-lookup"><span data-stu-id="0aa05-261">Additional resources</span></span>

* [<span data-ttu-id="0aa05-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0aa05-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="0aa05-263">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0aa05-263">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/policystat-tutorial/tutorial_general_01.png
[2]: ./media/policystat-tutorial/tutorial_general_02.png
[3]: ./media/policystat-tutorial/tutorial_general_03.png
[4]: ./media/policystat-tutorial/tutorial_general_04.png

[100]: ./media/policystat-tutorial/tutorial_general_100.png

[200]: ./media/policystat-tutorial/tutorial_general_200.png
[201]: ./media/policystat-tutorial/tutorial_general_201.png
[202]: ./media/policystat-tutorial/tutorial_general_202.png
[203]: ./media/policystat-tutorial/tutorial_general_203.png

