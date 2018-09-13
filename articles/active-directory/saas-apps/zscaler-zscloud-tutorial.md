---
title: 'Tutorial: Azure Active Directory integration with Zscaler ZSCloud | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Zscaler ZSCloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: a23d68e0b48a01cf98a5d1cc136a6af46895b0ee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867425"
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a><span data-ttu-id="4a4ff-103">Tutorial: Azure Active Directory integration with Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="4a4ff-103">Tutorial: Azure Active Directory integration with Zscaler ZSCloud</span></span>

<span data-ttu-id="4a4ff-104">In this tutorial, you learn how to integrate Zscaler ZSCloud with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4a4ff-104">In this tutorial, you learn how to integrate Zscaler ZSCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4a4ff-105">Integrating Zscaler ZSCloud with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4a4ff-105">Integrating Zscaler ZSCloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4a4ff-106">You can control in Azure AD who has access to Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="4a4ff-106">You can control in Azure AD who has access to Zscaler ZSCloud</span></span>
- <span data-ttu-id="4a4ff-107">You can enable your users to automatically get signed-on to Zscaler ZSCloud (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="4a4ff-107">You can enable your users to automatically get signed-on to Zscaler ZSCloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4a4ff-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4a4ff-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4a4ff-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="4a4ff-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a4ff-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4a4ff-110">Prerequisites</span></span>

<span data-ttu-id="4a4ff-111">To configure Azure AD integration with Zscaler ZSCloud, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4a4ff-111">To configure Azure AD integration with Zscaler ZSCloud, you need the following items:</span></span>

- <span data-ttu-id="4a4ff-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4a4ff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4a4ff-113">A Zscaler ZSCloud single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4a4ff-113">A Zscaler ZSCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4a4ff-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4a4ff-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4a4ff-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4a4ff-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4a4ff-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4a4ff-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4a4ff-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="4a4ff-118">Scenario description</span></span>
<span data-ttu-id="4a4ff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4a4ff-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4a4ff-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4a4ff-121">Adding Zscaler ZSCloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="4a4ff-121">Adding Zscaler ZSCloud from the gallery</span></span>
1. <span data-ttu-id="4a4ff-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4a4ff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-zscloud-from-the-gallery"></a><span data-ttu-id="4a4ff-123">Adding Zscaler ZSCloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="4a4ff-123">Adding Zscaler ZSCloud from the gallery</span></span>
<span data-ttu-id="4a4ff-124">To configure the integration of Zscaler ZSCloud into Azure AD, you need to add Zscaler ZSCloud from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-124">To configure the integration of Zscaler ZSCloud into Azure AD, you need to add Zscaler ZSCloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4a4ff-125">**To add Zscaler ZSCloud from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4a4ff-125">**To add Zscaler ZSCloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4a4ff-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="4a4ff-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4a4ff-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="4a4ff-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="4a4ff-133">In the search box, type **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-133">In the search box, type **Zscaler ZSCloud**.</span></span>

    ![Creating an Azure AD test user](./media/zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

1. <span data-ttu-id="4a4ff-135">In the results panel, select **Zscaler ZSCloud**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-135">In the results panel, select **Zscaler ZSCloud**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4a4ff-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4a4ff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4a4ff-138">In this section, you configure and test Azure AD single sign-on with Zscaler ZSCloud based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="4a4ff-138">In this section, you configure and test Azure AD single sign-on with Zscaler ZSCloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4a4ff-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler ZSCloud is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler ZSCloud is to a user in Azure AD.</span></span> <span data-ttu-id="4a4ff-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler ZSCloud needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler ZSCloud needs to be established.</span></span>

<span data-ttu-id="4a4ff-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zscaler ZSCloud.</span></span>

<span data-ttu-id="4a4ff-142">To configure and test Azure AD single sign-on with Zscaler ZSCloud, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4a4ff-142">To configure and test Azure AD single sign-on with Zscaler ZSCloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4a4ff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="4a4ff-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="4a4ff-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
1. <span data-ttu-id="4a4ff-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)**  - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)**  - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="4a4ff-146">**[Creating a Zscaler ZSCloud test user](#creating-a-zscaler-zscloud-test-user)** - to have a counterpart of Britta Simon in Zscaler ZSCloud that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-146">**[Creating a Zscaler ZSCloud test user](#creating-a-zscaler-zscloud-test-user)** - to have a counterpart of Britta Simon in Zscaler ZSCloud that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="4a4ff-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="4a4ff-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4a4ff-149">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4a4ff-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4a4ff-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler ZSCloud application.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="4a4ff-151">**To configure Azure AD single sign-on with Zscaler ZSCloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4a4ff-151">**To configure Azure AD single sign-on with Zscaler ZSCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="4a4ff-152">In the Azure portal, on the **Zscaler ZSCloud** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-152">In the Azure portal, on the **Zscaler ZSCloud** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="4a4ff-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

1. <span data-ttu-id="4a4ff-156">On the **Zscaler ZSCloud Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4a4ff-156">On the **Zscaler ZSCloud Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     <span data-ttu-id="4a4ff-158">In the **Sign-on URL** textbox, type the URL used by your users to sign-on to your ZScaler ZSCloud application.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-158">In the **Sign-on URL** textbox, type the URL used by your users to sign-on to your ZScaler ZSCloud application.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="4a4ff-159">You have to update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-159">You have to update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="4a4ff-160">Contact [Zscaler ZSCloud Client support team](https://help.zscaler.com/zia) to get this value.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-160">Contact [Zscaler ZSCloud Client support team](https://help.zscaler.com/zia) to get this value.</span></span> 
 
1. <span data-ttu-id="4a4ff-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

1. <span data-ttu-id="4a4ff-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/zscaler-zscloud-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="4a4ff-165">On the **Zscaler ZSCloud Configuration** section, click **Configure Zscaler ZSCloud** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-165">On the **Zscaler ZSCloud Configuration** section, click **Configure Zscaler ZSCloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4a4ff-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="4a4ff-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

1. <span data-ttu-id="4a4ff-168">In a different web browser window, log in to your ZScaler ZSCloud company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-168">In a different web browser window, log in to your ZScaler ZSCloud company site as an administrator.</span></span>

1. <span data-ttu-id="4a4ff-169">In the menu on the top, click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-169">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="4a4ff-170">![Administration](./media/zscaler-zscloud-tutorial/ic800206.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="4a4ff-170">![Administration](./media/zscaler-zscloud-tutorial/ic800206.png "Administration")</span></span>

1. <span data-ttu-id="4a4ff-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="4a4ff-172">![Manage Users & Authentication](./media/zscaler-zscloud-tutorial/ic800207.png "Manage Users & Authentication")</span><span class="sxs-lookup"><span data-stu-id="4a4ff-172">![Manage Users & Authentication](./media/zscaler-zscloud-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

1. <span data-ttu-id="4a4ff-173">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4a4ff-173">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="4a4ff-174">![Authentication](./media/zscaler-zscloud-tutorial/ic800208.png "Authentication")</span><span class="sxs-lookup"><span data-stu-id="4a4ff-174">![Authentication](./media/zscaler-zscloud-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="4a4ff-175">a.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-175">a.</span></span> <span data-ttu-id="4a4ff-176">Select **Authenticate using SAML Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="4a4ff-177">b.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-177">b.</span></span> <span data-ttu-id="4a4ff-178">Click **Configure SAML Single Sign-On Parameters**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

1. <span data-ttu-id="4a4ff-179">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span><span class="sxs-lookup"><span data-stu-id="4a4ff-179">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="4a4ff-180">![Single Sign-On](./media/zscaler-zscloud-tutorial/ic800209.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="4a4ff-180">![Single Sign-On](./media/zscaler-zscloud-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="4a4ff-181">a.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-181">a.</span></span> <span data-ttu-id="4a4ff-182">Paste the **SAML Single Sign-On Service URL** value into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-182">Paste the **SAML Single Sign-On Service URL** value into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="4a4ff-183">b.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-183">b.</span></span> <span data-ttu-id="4a4ff-184">In the **Attribute containing Login Name** textbox, type **NameID**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-184">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="4a4ff-185">c.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-185">c.</span></span> <span data-ttu-id="4a4ff-186">To upload your downloaded certificate, click **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-186">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="4a4ff-187">d.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-187">d.</span></span> <span data-ttu-id="4a4ff-188">Select **Enable SAML Auto-Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-188">Select **Enable SAML Auto-Provisioning**.</span></span>

1. <span data-ttu-id="4a4ff-189">On the **Configure User Authentication** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4a4ff-189">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="4a4ff-190">![Administration](./media/zscaler-zscloud-tutorial/ic800210.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="4a4ff-190">![Administration](./media/zscaler-zscloud-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="4a4ff-191">a.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-191">a.</span></span> <span data-ttu-id="4a4ff-192">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-192">Click **Save**.</span></span>

    <span data-ttu-id="4a4ff-193">b.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-193">b.</span></span> <span data-ttu-id="4a4ff-194">Click **Activate Now**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="4a4ff-195">Configuring proxy settings</span><span class="sxs-lookup"><span data-stu-id="4a4ff-195">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="4a4ff-196">To configure the proxy settings in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="4a4ff-196">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="4a4ff-197">Start **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-197">Start **Internet Explorer**.</span></span>

1. <span data-ttu-id="4a4ff-198">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-198">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="4a4ff-199">![Internet Options](./media/zscaler-zscloud-tutorial/ic769492.png "Internet Options")</span><span class="sxs-lookup"><span data-stu-id="4a4ff-199">![Internet Options](./media/zscaler-zscloud-tutorial/ic769492.png "Internet Options")</span></span>

1. <span data-ttu-id="4a4ff-200">Click the **Connections** tab.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-200">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="4a4ff-201">![Connections](./media/zscaler-zscloud-tutorial/ic769493.png "Connections")</span><span class="sxs-lookup"><span data-stu-id="4a4ff-201">![Connections](./media/zscaler-zscloud-tutorial/ic769493.png "Connections")</span></span>

1. <span data-ttu-id="4a4ff-202">Click **LAN settings** to open the **LAN Settings** dialog.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-202">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

1. <span data-ttu-id="4a4ff-203">In the Proxy server section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4a4ff-203">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="4a4ff-204">![Proxy server](./media/zscaler-zscloud-tutorial/ic769494.png "Proxy server")</span><span class="sxs-lookup"><span data-stu-id="4a4ff-204">![Proxy server](./media/zscaler-zscloud-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="4a4ff-205">a.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-205">a.</span></span> <span data-ttu-id="4a4ff-206">Select **Use a proxy server for your LAN**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="4a4ff-207">b.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-207">b.</span></span> <span data-ttu-id="4a4ff-208">In the Address textbox, type **gateway.zscalerone.net**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-208">In the Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="4a4ff-209">c.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-209">c.</span></span> <span data-ttu-id="4a4ff-210">In the Port textbox, type **80**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-210">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="4a4ff-211">d.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-211">d.</span></span> <span data-ttu-id="4a4ff-212">Select **Bypass proxy server for local addresses**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="4a4ff-213">e.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-213">e.</span></span> <span data-ttu-id="4a4ff-214">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-214">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

1. <span data-ttu-id="4a4ff-215">Click **OK** to close the **Internet Options** dialog.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-215">Click **OK** to close the **Internet Options** dialog.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4a4ff-216">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4a4ff-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="4a4ff-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="4a4ff-219">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4a4ff-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4a4ff-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/zscaler-zscloud-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="4a4ff-222">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/zscaler-zscloud-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="4a4ff-224">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/zscaler-zscloud-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="4a4ff-226">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4a4ff-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/zscaler-zscloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4a4ff-228">a.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-228">a.</span></span> <span data-ttu-id="4a4ff-229">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4a4ff-230">b.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-230">b.</span></span> <span data-ttu-id="4a4ff-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4a4ff-232">c.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-232">c.</span></span> <span data-ttu-id="4a4ff-233">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4a4ff-234">d.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-234">d.</span></span> <span data-ttu-id="4a4ff-235">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-235">Click **Create**.</span></span>

### <a name="creating-a-zscaler-zscloud-test-user"></a><span data-ttu-id="4a4ff-236">Creating a Zscaler ZSCloud test user</span><span class="sxs-lookup"><span data-stu-id="4a4ff-236">Creating a Zscaler ZSCloud test user</span></span>

<span data-ttu-id="4a4ff-237">To enable Azure AD users to log in to ZScaler ZSCloud, they must be provisioned to ZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-237">To enable Azure AD users to log in to ZScaler ZSCloud, they must be provisioned to ZScaler ZSCloud.</span></span>  
<span data-ttu-id="4a4ff-238">In the case of ZScaler ZSCloud, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-238">In the case of ZScaler ZSCloud, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="4a4ff-239">To configure user provisioning, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4a4ff-239">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="4a4ff-240">Log in to your **Zscaler** tenant.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-240">Log in to your **Zscaler** tenant.</span></span>

1. <span data-ttu-id="4a4ff-241">Click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-241">Click **Administration**.</span></span>   
   
    <span data-ttu-id="4a4ff-242">![Administration](./media/zscaler-zscloud-tutorial/ic781035.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="4a4ff-242">![Administration](./media/zscaler-zscloud-tutorial/ic781035.png "Administration")</span></span>

1. <span data-ttu-id="4a4ff-243">Click **User Management**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-243">Click **User Management**.</span></span>   
        
     <span data-ttu-id="4a4ff-244">![Add](./media/zscaler-zscloud-tutorial/ic781037.png "Add")</span><span class="sxs-lookup"><span data-stu-id="4a4ff-244">![Add](./media/zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

1. <span data-ttu-id="4a4ff-245">In the **Users** tab, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-245">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="4a4ff-246">![Add](./media/zscaler-zscloud-tutorial/ic781037.png "Add")</span><span class="sxs-lookup"><span data-stu-id="4a4ff-246">![Add](./media/zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

1. <span data-ttu-id="4a4ff-247">In the Add User section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4a4ff-247">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="4a4ff-248">![Add User](./media/zscaler-zscloud-tutorial/ic781038.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="4a4ff-248">![Add User](./media/zscaler-zscloud-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="4a4ff-249">a.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-249">a.</span></span> <span data-ttu-id="4a4ff-250">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-250">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="4a4ff-251">b.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-251">b.</span></span> <span data-ttu-id="4a4ff-252">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-252">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="4a4ff-253">You can use any other ZScaler ZSCloud user account creation tools or APIs provided by ZScaler ZSCloud to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-253">You can use any other ZScaler ZSCloud user account creation tools or APIs provided by ZScaler ZSCloud to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4a4ff-254">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4a4ff-254">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4a4ff-255">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-255">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler ZSCloud.</span></span>

![Assign User][200] 

<span data-ttu-id="4a4ff-257">**To assign Britta Simon to Zscaler ZSCloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4a4ff-257">**To assign Britta Simon to Zscaler ZSCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="4a4ff-258">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-258">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="4a4ff-260">In the applications list, select **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-260">In the applications list, select **Zscaler ZSCloud**.</span></span>

    ![Configure Single Sign-On](./media/zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

1. <span data-ttu-id="4a4ff-262">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-262">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="4a4ff-264">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-264">Click **Add** button.</span></span> <span data-ttu-id="4a4ff-265">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="4a4ff-267">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-267">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="4a4ff-268">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-268">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="4a4ff-269">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4a4ff-270">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="4a4ff-270">Testing single sign-on</span></span>

<span data-ttu-id="4a4ff-271">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-271">If you want to test your single sign-on settings, open the Access Panel.</span></span>

<span data-ttu-id="4a4ff-272">When you click the Zscaler ZSCloud tile in the Access Panel, you should get automatically signed-on to your Zscaler ZSCloud application.</span><span class="sxs-lookup"><span data-stu-id="4a4ff-272">When you click the Zscaler ZSCloud tile in the Access Panel, you should get automatically signed-on to your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="4a4ff-273">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4a4ff-273">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4a4ff-274">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4a4ff-274">Additional resources</span></span>

* [<span data-ttu-id="4a4ff-275">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4a4ff-275">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="4a4ff-276">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4a4ff-276">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/zscaler-zscloud-tutorial/tutorial_general_203.png

