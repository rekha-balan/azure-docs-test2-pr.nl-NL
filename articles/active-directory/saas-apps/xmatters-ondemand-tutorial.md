---
title: 'Tutorial: Azure Active Directory integration with xMatters OnDemand | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and xMatters OnDemand.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2018
ms.author: jeedes
ms.openlocfilehash: a235b85887e64e0a5ca35aae8f31734250a78bb5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866610"
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a><span data-ttu-id="87cbe-103">Tutorial: Azure Active Directory integration with xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="87cbe-103">Tutorial: Azure Active Directory integration with xMatters OnDemand</span></span>

<span data-ttu-id="87cbe-104">In this tutorial, you learn how to integrate xMatters OnDemand with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="87cbe-104">In this tutorial, you learn how to integrate xMatters OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="87cbe-105">Integrating xMatters OnDemand with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="87cbe-105">Integrating xMatters OnDemand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="87cbe-106">You can control in Azure AD who has access to xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="87cbe-106">You can control in Azure AD who has access to xMatters OnDemand</span></span>
- <span data-ttu-id="87cbe-107">You can enable your users to automatically get signed-on to xMatters OnDemand (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="87cbe-107">You can enable your users to automatically get signed-on to xMatters OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="87cbe-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="87cbe-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="87cbe-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="87cbe-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87cbe-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="87cbe-110">Prerequisites</span></span>

<span data-ttu-id="87cbe-111">To configure Azure AD integration with xMatters OnDemand, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="87cbe-111">To configure Azure AD integration with xMatters OnDemand, you need the following items:</span></span>

- <span data-ttu-id="87cbe-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="87cbe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="87cbe-113">A xMatters OnDemand single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="87cbe-113">A xMatters OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="87cbe-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="87cbe-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="87cbe-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="87cbe-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="87cbe-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="87cbe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="87cbe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="87cbe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="87cbe-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="87cbe-118">Scenario description</span></span>
<span data-ttu-id="87cbe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="87cbe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="87cbe-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="87cbe-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="87cbe-121">Adding xMatters OnDemand from the gallery</span><span class="sxs-lookup"><span data-stu-id="87cbe-121">Adding xMatters OnDemand from the gallery</span></span>
1. <span data-ttu-id="87cbe-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="87cbe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-xmatters-ondemand-from-the-gallery"></a><span data-ttu-id="87cbe-123">Adding xMatters OnDemand from the gallery</span><span class="sxs-lookup"><span data-stu-id="87cbe-123">Adding xMatters OnDemand from the gallery</span></span>
<span data-ttu-id="87cbe-124">To configure the integration of xMatters OnDemand into Azure AD, you need to add xMatters OnDemand from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="87cbe-124">To configure the integration of xMatters OnDemand into Azure AD, you need to add xMatters OnDemand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="87cbe-125">**To add xMatters OnDemand from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="87cbe-125">**To add xMatters OnDemand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="87cbe-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="87cbe-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="87cbe-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="87cbe-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="87cbe-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="87cbe-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="87cbe-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="87cbe-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="87cbe-133">In the search box, type **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="87cbe-133">In the search box, type **xMatters OnDemand**.</span></span>

    ![Creating an Azure AD test user](./media/xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

1. <span data-ttu-id="87cbe-135">In the results panel, select **xMatters OnDemand**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="87cbe-135">In the results panel, select **xMatters OnDemand**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="87cbe-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="87cbe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="87cbe-138">In this section, you configure and test Azure AD single sign-on with xMatters OnDemand based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="87cbe-138">In this section, you configure and test Azure AD single sign-on with xMatters OnDemand based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="87cbe-139">For single sign-on to work, Azure AD needs to know what the counterpart user in xMatters OnDemand is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="87cbe-139">For single sign-on to work, Azure AD needs to know what the counterpart user in xMatters OnDemand is to a user in Azure AD.</span></span> <span data-ttu-id="87cbe-140">In other words, a link relationship between an Azure AD user and the related user in xMatters OnDemand needs to be established.</span><span class="sxs-lookup"><span data-stu-id="87cbe-140">In other words, a link relationship between an Azure AD user and the related user in xMatters OnDemand needs to be established.</span></span>

<span data-ttu-id="87cbe-141">In xMatters OnDemand, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="87cbe-141">In xMatters OnDemand, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="87cbe-142">To configure and test Azure AD single sign-on with xMatters OnDemand, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="87cbe-142">To configure and test Azure AD single sign-on with xMatters OnDemand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="87cbe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="87cbe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="87cbe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="87cbe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="87cbe-145">**[Creating a xMatters OnDemand test user](#creating-a-xmatters-ondemand-test-user)** - to have a counterpart of Britta Simon in xMatters OnDemand that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="87cbe-145">**[Creating a xMatters OnDemand test user](#creating-a-xmatters-ondemand-test-user)** - to have a counterpart of Britta Simon in xMatters OnDemand that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="87cbe-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="87cbe-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="87cbe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="87cbe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="87cbe-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="87cbe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="87cbe-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your xMatters OnDemand application.</span><span class="sxs-lookup"><span data-stu-id="87cbe-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your xMatters OnDemand application.</span></span>

<span data-ttu-id="87cbe-150">**To configure Azure AD single sign-on with xMatters OnDemand, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="87cbe-150">**To configure Azure AD single sign-on with xMatters OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="87cbe-151">In the Azure portal, on the **xMatters OnDemand** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="87cbe-151">In the Azure portal, on the **xMatters OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="87cbe-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="87cbe-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configure Single Sign-On](./media/xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

1. <span data-ttu-id="87cbe-155">On the **xMatters OnDemand Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="87cbe-155">On the **xMatters OnDemand Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    <span data-ttu-id="87cbe-157">a.</span><span class="sxs-lookup"><span data-stu-id="87cbe-157">a.</span></span> <span data-ttu-id="87cbe-158">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="87cbe-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    <span data-ttu-id="87cbe-159">b.</span><span class="sxs-lookup"><span data-stu-id="87cbe-159">b.</span></span> <span data-ttu-id="87cbe-160">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="87cbe-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > <span data-ttu-id="87cbe-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="87cbe-161">These values are not real.</span></span> <span data-ttu-id="87cbe-162">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="87cbe-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="87cbe-163">Contact [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="87cbe-163">Contact [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/) to get these values.</span></span>

1. <span data-ttu-id="87cbe-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file locally as **c:\\XMatters OnDemand.cer**.</span><span class="sxs-lookup"><span data-stu-id="87cbe-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file locally as **c:\\XMatters OnDemand.cer**.</span></span>

    ![Configure Single Sign-On](./media/xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)

    > [!IMPORTANT]
    > <span data-ttu-id="87cbe-166">You need to forward the certificate to the [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="87cbe-166">You need to forward the certificate to the [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/).</span></span> <span data-ttu-id="87cbe-167">The certificate needs to be uploaded by the xMatters support team before you can finalize the single sign-on configuration.</span><span class="sxs-lookup"><span data-stu-id="87cbe-167">The certificate needs to be uploaded by the xMatters support team before you can finalize the single sign-on configuration.</span></span> 

1. <span data-ttu-id="87cbe-168">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="87cbe-168">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/xmatters-ondemand-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="87cbe-170">On the **xMatters OnDemand Configuration** section, click **Configure xMatters OnDemand** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="87cbe-170">On the **xMatters OnDemand Configuration** section, click **Configure xMatters OnDemand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="87cbe-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="87cbe-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

1. <span data-ttu-id="87cbe-173">In a different web browser window, log in to your XMatters OnDemand company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="87cbe-173">In a different web browser window, log in to your XMatters OnDemand company site as an administrator.</span></span>

1. <span data-ttu-id="87cbe-174">In the toolbar on the top, click **Admin**, and then click **Company Details** in the navigation bar on the left side.</span><span class="sxs-lookup"><span data-stu-id="87cbe-174">In the toolbar on the top, click **Admin**, and then click **Company Details** in the navigation bar on the left side.</span></span>

    <span data-ttu-id="87cbe-175">![Admin](./media/xmatters-ondemand-tutorial/IC776795.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="87cbe-175">![Admin](./media/xmatters-ondemand-tutorial/IC776795.png "Admin")</span></span>

1. <span data-ttu-id="87cbe-176">On the **SAML Configuration** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="87cbe-176">On the **SAML Configuration** page, perform the following steps:</span></span>

    <span data-ttu-id="87cbe-177">![SAML configuration](./media/xmatters-ondemand-tutorial/IC776796.png "SAML configuration")</span><span class="sxs-lookup"><span data-stu-id="87cbe-177">![SAML configuration](./media/xmatters-ondemand-tutorial/IC776796.png "SAML configuration")</span></span>

    <span data-ttu-id="87cbe-178">a.</span><span class="sxs-lookup"><span data-stu-id="87cbe-178">a.</span></span> <span data-ttu-id="87cbe-179">Select **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="87cbe-179">Select **Enable SAML**.</span></span>

    <span data-ttu-id="87cbe-180">b.</span><span class="sxs-lookup"><span data-stu-id="87cbe-180">b.</span></span> <span data-ttu-id="87cbe-181">In the **Identity Provider ID** textbox, paste **SAML Entity ID** value which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="87cbe-181">In the **Identity Provider ID** textbox, paste **SAML Entity ID** value which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="87cbe-182">c.</span><span class="sxs-lookup"><span data-stu-id="87cbe-182">c.</span></span> <span data-ttu-id="87cbe-183">In the **Single Sign On URL** textbox, paste **SAML Single Sign-On Service URL** value which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="87cbe-183">In the **Single Sign On URL** textbox, paste **SAML Single Sign-On Service URL** value which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="87cbe-184">d.</span><span class="sxs-lookup"><span data-stu-id="87cbe-184">d.</span></span> <span data-ttu-id="87cbe-185">In the **Single Logout URL** textbox, paste **Sign-Out URL**, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="87cbe-185">In the **Single Logout URL** textbox, paste **Sign-Out URL**, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="87cbe-186">e.</span><span class="sxs-lookup"><span data-stu-id="87cbe-186">e.</span></span> <span data-ttu-id="87cbe-187">On the Company Details page, at the top, click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="87cbe-187">On the Company Details page, at the top, click **Save Changes**.</span></span>

    <span data-ttu-id="87cbe-188">![Company details](./media/xmatters-ondemand-tutorial/IC776797.png "Company details")</span><span class="sxs-lookup"><span data-stu-id="87cbe-188">![Company details](./media/xmatters-ondemand-tutorial/IC776797.png "Company details")</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="87cbe-189">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="87cbe-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="87cbe-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="87cbe-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="87cbe-192">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="87cbe-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="87cbe-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="87cbe-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/xmatters-ondemand-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="87cbe-195">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="87cbe-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>

    ![Creating an Azure AD test user](./media/xmatters-ondemand-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="87cbe-197">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="87cbe-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>

    ![Creating an Azure AD test user](./media/xmatters-ondemand-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="87cbe-199">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="87cbe-199">On the **User** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](./media/xmatters-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="87cbe-201">a.</span><span class="sxs-lookup"><span data-stu-id="87cbe-201">a.</span></span> <span data-ttu-id="87cbe-202">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="87cbe-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="87cbe-203">b.</span><span class="sxs-lookup"><span data-stu-id="87cbe-203">b.</span></span> <span data-ttu-id="87cbe-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="87cbe-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="87cbe-205">c.</span><span class="sxs-lookup"><span data-stu-id="87cbe-205">c.</span></span> <span data-ttu-id="87cbe-206">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="87cbe-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="87cbe-207">d.</span><span class="sxs-lookup"><span data-stu-id="87cbe-207">d.</span></span> <span data-ttu-id="87cbe-208">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="87cbe-208">Click **Create**.</span></span>

### <a name="creating-a-xmatters-ondemand-test-user"></a><span data-ttu-id="87cbe-209">Creating a xMatters OnDemand test user</span><span class="sxs-lookup"><span data-stu-id="87cbe-209">Creating a xMatters OnDemand test user</span></span>

<span data-ttu-id="87cbe-210">The objective of this section is to create a user called Britta Simon in xMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="87cbe-210">The objective of this section is to create a user called Britta Simon in xMatters OnDemand.</span></span>

<span data-ttu-id="87cbe-211">**If you need to create user manually, perform following steps:**</span><span class="sxs-lookup"><span data-stu-id="87cbe-211">**If you need to create user manually, perform following steps:**</span></span>

1. <span data-ttu-id="87cbe-212">Log in to your **XMatters OnDemand** tenant.</span><span class="sxs-lookup"><span data-stu-id="87cbe-212">Log in to your **XMatters OnDemand** tenant.</span></span>

1.  <span data-ttu-id="87cbe-213">Click **Users** tab. and then click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="87cbe-213">Click **Users** tab. and then click **Add User**.</span></span>

    <span data-ttu-id="87cbe-214">![Users](./media/xmatters-ondemand-tutorial/IC781048.png "Users")</span><span class="sxs-lookup"><span data-stu-id="87cbe-214">![Users](./media/xmatters-ondemand-tutorial/IC781048.png "Users")</span></span>

1. <span data-ttu-id="87cbe-215">In the **Add a User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="87cbe-215">In the **Add a User** section, perform the following steps:</span></span>

    <span data-ttu-id="87cbe-216">![Add a User](./media/xmatters-ondemand-tutorial/IC781049.png "Add a User")</span><span class="sxs-lookup"><span data-stu-id="87cbe-216">![Add a User](./media/xmatters-ondemand-tutorial/IC781049.png "Add a User")</span></span>

    <span data-ttu-id="87cbe-217">a.</span><span class="sxs-lookup"><span data-stu-id="87cbe-217">a.</span></span> <span data-ttu-id="87cbe-218">Select **Active**.</span><span class="sxs-lookup"><span data-stu-id="87cbe-218">Select **Active**.</span></span>

    <span data-ttu-id="87cbe-219">b.</span><span class="sxs-lookup"><span data-stu-id="87cbe-219">b.</span></span> <span data-ttu-id="87cbe-220">In the **User ID** textbox, type the user id of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="87cbe-220">In the **User ID** textbox, type the user id of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="87cbe-221">c.</span><span class="sxs-lookup"><span data-stu-id="87cbe-221">c.</span></span> <span data-ttu-id="87cbe-222">In the **First Name** textbox, type first name of the user like Britta.</span><span class="sxs-lookup"><span data-stu-id="87cbe-222">In the **First Name** textbox, type first name of the user like Britta.</span></span>

    <span data-ttu-id="87cbe-223">d.</span><span class="sxs-lookup"><span data-stu-id="87cbe-223">d.</span></span> <span data-ttu-id="87cbe-224">In the **Last Name** textbox, type last name of the user like Simon.</span><span class="sxs-lookup"><span data-stu-id="87cbe-224">In the **Last Name** textbox, type last name of the user like Simon.</span></span>

    <span data-ttu-id="87cbe-225">e.</span><span class="sxs-lookup"><span data-stu-id="87cbe-225">e.</span></span> <span data-ttu-id="87cbe-226">In the **Site** textbox, Enter the valid site of a valid Azure AD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="87cbe-226">In the **Site** textbox, Enter the valid site of a valid Azure AD account you want to provision.</span></span>

    <span data-ttu-id="87cbe-227">f.</span><span class="sxs-lookup"><span data-stu-id="87cbe-227">f.</span></span> <span data-ttu-id="87cbe-228">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="87cbe-228">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="87cbe-229">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="87cbe-229">Assigning the Azure AD test user</span></span>

<span data-ttu-id="87cbe-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to xMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="87cbe-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to xMatters OnDemand.</span></span>

![Assign User][200] 

<span data-ttu-id="87cbe-232">**To assign Britta Simon to xMatters OnDemand, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="87cbe-232">**To assign Britta Simon to xMatters OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="87cbe-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="87cbe-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="87cbe-235">In the applications list, select **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="87cbe-235">In the applications list, select **xMatters OnDemand**.</span></span>

    ![Configure Single Sign-On](./media/xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

1. <span data-ttu-id="87cbe-237">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="87cbe-237">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="87cbe-239">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="87cbe-239">Click **Add** button.</span></span> <span data-ttu-id="87cbe-240">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="87cbe-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="87cbe-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="87cbe-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="87cbe-243">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="87cbe-243">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="87cbe-244">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="87cbe-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="87cbe-245">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="87cbe-245">Testing single sign-on</span></span>

<span data-ttu-id="87cbe-246">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="87cbe-246">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="87cbe-247">When you click the xMatters OnDemand tile in the Access Panel, you should get automatically signed-on to your xMatters OnDemand application.</span><span class="sxs-lookup"><span data-stu-id="87cbe-247">When you click the xMatters OnDemand tile in the Access Panel, you should get automatically signed-on to your xMatters OnDemand application.</span></span>
<span data-ttu-id="87cbe-248">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="87cbe-248">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="87cbe-249">Additional resources</span><span class="sxs-lookup"><span data-stu-id="87cbe-249">Additional resources</span></span>

* [<span data-ttu-id="87cbe-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="87cbe-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="87cbe-251">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="87cbe-251">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/xmatters-ondemand-tutorial/tutorial_general_203.png
