---
title: 'Tutorial: Azure Active Directory integration with Zscaler Beta | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Zscaler Beta.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 56b846ae-a1e7-45ae-a79d-992a87f075ba
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 29637f8a733e9f92f37144491bef4ab4ba5aae07
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856286"
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-beta"></a><span data-ttu-id="fefcd-103">Tutorial: Azure Active Directory integration with Zscaler Beta</span><span class="sxs-lookup"><span data-stu-id="fefcd-103">Tutorial: Azure Active Directory integration with Zscaler Beta</span></span>

<span data-ttu-id="fefcd-104">In this tutorial, you learn how to integrate Zscaler Beta with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fefcd-104">In this tutorial, you learn how to integrate Zscaler Beta with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fefcd-105">Integrating Zscaler Beta with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="fefcd-105">Integrating Zscaler Beta with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fefcd-106">You can control in Azure AD who has access to Zscaler Beta</span><span class="sxs-lookup"><span data-stu-id="fefcd-106">You can control in Azure AD who has access to Zscaler Beta</span></span>
- <span data-ttu-id="fefcd-107">You can enable your users to automatically get signed-on to Zscaler Beta (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="fefcd-107">You can enable your users to automatically get signed-on to Zscaler Beta (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fefcd-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="fefcd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fefcd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="fefcd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fefcd-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fefcd-110">Prerequisites</span></span>

<span data-ttu-id="fefcd-111">To configure Azure AD integration with Zscaler Beta, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="fefcd-111">To configure Azure AD integration with Zscaler Beta, you need the following items:</span></span>

- <span data-ttu-id="fefcd-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="fefcd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fefcd-113">A Zscaler Beta single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="fefcd-113">A Zscaler Beta single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fefcd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="fefcd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fefcd-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="fefcd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fefcd-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="fefcd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fefcd-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fefcd-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fefcd-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="fefcd-118">Scenario description</span></span>
<span data-ttu-id="fefcd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="fefcd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fefcd-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="fefcd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fefcd-121">Adding Zscaler Beta from the gallery</span><span class="sxs-lookup"><span data-stu-id="fefcd-121">Adding Zscaler Beta from the gallery</span></span>
1. <span data-ttu-id="fefcd-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fefcd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-beta-from-the-gallery"></a><span data-ttu-id="fefcd-123">Adding Zscaler Beta from the gallery</span><span class="sxs-lookup"><span data-stu-id="fefcd-123">Adding Zscaler Beta from the gallery</span></span>
<span data-ttu-id="fefcd-124">To configure the integration of Zscaler Beta into Azure AD, you need to add Zscaler Beta from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="fefcd-124">To configure the integration of Zscaler Beta into Azure AD, you need to add Zscaler Beta from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fefcd-125">**To add Zscaler Beta from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fefcd-125">**To add Zscaler Beta from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fefcd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="fefcd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="fefcd-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fefcd-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="fefcd-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="fefcd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="fefcd-133">In the search box, type **Zscaler Beta**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-133">In the search box, type **Zscaler Beta**.</span></span>

    ![Creating an Azure AD test user](./media/zscaler-beta-tutorial/tutorial_zscalerbeta_search.png)

1. <span data-ttu-id="fefcd-135">In the results panel, select **Zscaler Beta**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="fefcd-135">In the results panel, select **Zscaler Beta**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/zscaler-beta-tutorial/tutorial_zscalerbeta_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fefcd-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fefcd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fefcd-138">In this section, you configure and test Azure AD single sign-on with Zscaler Beta based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fefcd-138">In this section, you configure and test Azure AD single sign-on with Zscaler Beta based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fefcd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler Beta is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fefcd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler Beta is to a user in Azure AD.</span></span> <span data-ttu-id="fefcd-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler Beta needs to be established.</span><span class="sxs-lookup"><span data-stu-id="fefcd-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler Beta needs to be established.</span></span>

<span data-ttu-id="fefcd-141">In Zscaler Beta, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="fefcd-141">In Zscaler Beta, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fefcd-142">To configure and test Azure AD single sign-on with Zscaler Beta, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="fefcd-142">To configure and test Azure AD single sign-on with Zscaler Beta, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fefcd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="fefcd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="fefcd-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="fefcd-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
1. <span data-ttu-id="fefcd-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fefcd-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="fefcd-146">**[Creating a Zscaler Beta test user](#creating-a-zscaler-beta-test-user)** - to have a counterpart of Britta Simon in Zscaler Beta that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="fefcd-146">**[Creating a Zscaler Beta test user](#creating-a-zscaler-beta-test-user)** - to have a counterpart of Britta Simon in Zscaler Beta that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="fefcd-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fefcd-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="fefcd-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="fefcd-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fefcd-149">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fefcd-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fefcd-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler Beta application.</span><span class="sxs-lookup"><span data-stu-id="fefcd-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler Beta application.</span></span>

<span data-ttu-id="fefcd-151">**To configure Azure AD single sign-on with Zscaler Beta, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fefcd-151">**To configure Azure AD single sign-on with Zscaler Beta, perform the following steps:**</span></span>

1. <span data-ttu-id="fefcd-152">In the Azure portal, on the **Zscaler Beta** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-152">In the Azure portal, on the **Zscaler Beta** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="fefcd-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fefcd-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/zscaler-beta-tutorial/tutorial_zscalerbeta_samlbase.png)

1. <span data-ttu-id="fefcd-156">On the **Zscaler Beta Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fefcd-156">On the **Zscaler Beta Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/zscaler-beta-tutorial/tutorial_zscalerbeta_url.png)

    <span data-ttu-id="fefcd-158">In the Sign-on URL textbox, type the URL used by your users to sign-on to your Zscaler Beta application.</span><span class="sxs-lookup"><span data-stu-id="fefcd-158">In the Sign-on URL textbox, type the URL used by your users to sign-on to your Zscaler Beta application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fefcd-159">You have to update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="fefcd-159">You have to update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="fefcd-160">Contact [Zscaler Beta Client support team](https://www.zscaler.com/company/contact) to get this value.</span><span class="sxs-lookup"><span data-stu-id="fefcd-160">Contact [Zscaler Beta Client support team](https://www.zscaler.com/company/contact) to get this value.</span></span> 

1. <span data-ttu-id="fefcd-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="fefcd-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/zscaler-beta-tutorial/tutorial_zscalerbeta_certificate.png) 

1. <span data-ttu-id="fefcd-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="fefcd-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/zscaler-beta-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="fefcd-165">On the **Zscaler Beta Configuration** section, click **Configure Zscaler Beta** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="fefcd-165">On the **Zscaler Beta Configuration** section, click **Configure Zscaler Beta** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fefcd-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="fefcd-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/zscaler-beta-tutorial/tutorial_zscalerbeta_configure.png) 

1. <span data-ttu-id="fefcd-168">In a different web browser window, log in to your Zscaler Beta company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="fefcd-168">In a different web browser window, log in to your Zscaler Beta company site as an administrator.</span></span>

1. <span data-ttu-id="fefcd-169">In the menu on the top, click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-169">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="fefcd-170">![Administration](./media/zscaler-beta-tutorial/ic800206.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="fefcd-170">![Administration](./media/zscaler-beta-tutorial/ic800206.png "Administration")</span></span>

1. <span data-ttu-id="fefcd-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="fefcd-172">![Manage Users & Authentication](./media/zscaler-beta-tutorial/ic800207.png "Manage Users & Authentication")</span><span class="sxs-lookup"><span data-stu-id="fefcd-172">![Manage Users & Authentication](./media/zscaler-beta-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

1. <span data-ttu-id="fefcd-173">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fefcd-173">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="fefcd-174">![Authentication](./media/zscaler-beta-tutorial/ic800208.png "Authentication")</span><span class="sxs-lookup"><span data-stu-id="fefcd-174">![Authentication](./media/zscaler-beta-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="fefcd-175">a.</span><span class="sxs-lookup"><span data-stu-id="fefcd-175">a.</span></span> <span data-ttu-id="fefcd-176">Select **Authenticate using SAML Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="fefcd-177">b.</span><span class="sxs-lookup"><span data-stu-id="fefcd-177">b.</span></span> <span data-ttu-id="fefcd-178">Click **Configure SAML Single Sign-On Parameters**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

1. <span data-ttu-id="fefcd-179">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span><span class="sxs-lookup"><span data-stu-id="fefcd-179">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="fefcd-180">![Single Sign-On](./media/zscaler-beta-tutorial/ic800209.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="fefcd-180">![Single Sign-On](./media/zscaler-beta-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="fefcd-181">a.</span><span class="sxs-lookup"><span data-stu-id="fefcd-181">a.</span></span> <span data-ttu-id="fefcd-182">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span><span class="sxs-lookup"><span data-stu-id="fefcd-182">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="fefcd-183">b.</span><span class="sxs-lookup"><span data-stu-id="fefcd-183">b.</span></span> <span data-ttu-id="fefcd-184">In the **Attribute containing Login Name** textbox, type **NameID**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-184">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="fefcd-185">c.</span><span class="sxs-lookup"><span data-stu-id="fefcd-185">c.</span></span> <span data-ttu-id="fefcd-186">To upload your downloaded certificate, click **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-186">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="fefcd-187">d.</span><span class="sxs-lookup"><span data-stu-id="fefcd-187">d.</span></span> <span data-ttu-id="fefcd-188">Select **Enable SAML Auto-Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-188">Select **Enable SAML Auto-Provisioning**.</span></span>

1. <span data-ttu-id="fefcd-189">On the **Configure User Authentication** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fefcd-189">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="fefcd-190">![Administration](./media/zscaler-beta-tutorial/ic800210.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="fefcd-190">![Administration](./media/zscaler-beta-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="fefcd-191">a.</span><span class="sxs-lookup"><span data-stu-id="fefcd-191">a.</span></span> <span data-ttu-id="fefcd-192">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-192">Click **Save**.</span></span>

    <span data-ttu-id="fefcd-193">b.</span><span class="sxs-lookup"><span data-stu-id="fefcd-193">b.</span></span> <span data-ttu-id="fefcd-194">Click **Activate Now**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="fefcd-195">Configuring proxy settings</span><span class="sxs-lookup"><span data-stu-id="fefcd-195">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="fefcd-196">To configure the proxy settings in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="fefcd-196">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="fefcd-197">Start **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-197">Start **Internet Explorer**.</span></span>

1. <span data-ttu-id="fefcd-198">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span><span class="sxs-lookup"><span data-stu-id="fefcd-198">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="fefcd-199">![Internet Options](./media/zscaler-beta-tutorial/ic769492.png "Internet Options")</span><span class="sxs-lookup"><span data-stu-id="fefcd-199">![Internet Options](./media/zscaler-beta-tutorial/ic769492.png "Internet Options")</span></span>

1. <span data-ttu-id="fefcd-200">Click the **Connections** tab.</span><span class="sxs-lookup"><span data-stu-id="fefcd-200">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="fefcd-201">![Connections](./media/zscaler-beta-tutorial/ic769493.png "Connections")</span><span class="sxs-lookup"><span data-stu-id="fefcd-201">![Connections](./media/zscaler-beta-tutorial/ic769493.png "Connections")</span></span>

1. <span data-ttu-id="fefcd-202">Click **LAN settings** to open the **LAN Settings** dialog.</span><span class="sxs-lookup"><span data-stu-id="fefcd-202">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

1. <span data-ttu-id="fefcd-203">In the Proxy server section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fefcd-203">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="fefcd-204">![Proxy server](./media/zscaler-beta-tutorial/ic769494.png "Proxy server")</span><span class="sxs-lookup"><span data-stu-id="fefcd-204">![Proxy server](./media/zscaler-beta-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="fefcd-205">a.</span><span class="sxs-lookup"><span data-stu-id="fefcd-205">a.</span></span> <span data-ttu-id="fefcd-206">Select **Use a proxy server for your LAN**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="fefcd-207">b.</span><span class="sxs-lookup"><span data-stu-id="fefcd-207">b.</span></span> <span data-ttu-id="fefcd-208">In the Address textbox, type **gateway.zscalerbeta.net**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-208">In the Address textbox, type **gateway.zscalerbeta.net**.</span></span>

    <span data-ttu-id="fefcd-209">c.</span><span class="sxs-lookup"><span data-stu-id="fefcd-209">c.</span></span> <span data-ttu-id="fefcd-210">In the Port textbox, type **80**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-210">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="fefcd-211">d.</span><span class="sxs-lookup"><span data-stu-id="fefcd-211">d.</span></span> <span data-ttu-id="fefcd-212">Select **Bypass proxy server for local addresses**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="fefcd-213">e.</span><span class="sxs-lookup"><span data-stu-id="fefcd-213">e.</span></span> <span data-ttu-id="fefcd-214">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span><span class="sxs-lookup"><span data-stu-id="fefcd-214">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

1. <span data-ttu-id="fefcd-215">Click **OK** to close the **Internet Options** dialog.</span><span class="sxs-lookup"><span data-stu-id="fefcd-215">Click **OK** to close the **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="fefcd-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="fefcd-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fefcd-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="fefcd-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fefcd-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fefcd-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fefcd-219">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="fefcd-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="fefcd-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fefcd-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="fefcd-222">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fefcd-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fefcd-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="fefcd-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/zscaler-beta-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="fefcd-225">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-225">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/zscaler-beta-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="fefcd-227">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="fefcd-227">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/zscaler-beta-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="fefcd-229">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fefcd-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/zscaler-beta-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fefcd-231">a.</span><span class="sxs-lookup"><span data-stu-id="fefcd-231">a.</span></span> <span data-ttu-id="fefcd-232">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fefcd-233">b.</span><span class="sxs-lookup"><span data-stu-id="fefcd-233">b.</span></span> <span data-ttu-id="fefcd-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fefcd-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fefcd-235">c.</span><span class="sxs-lookup"><span data-stu-id="fefcd-235">c.</span></span> <span data-ttu-id="fefcd-236">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fefcd-237">d.</span><span class="sxs-lookup"><span data-stu-id="fefcd-237">d.</span></span> <span data-ttu-id="fefcd-238">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-beta-test-user"></a><span data-ttu-id="fefcd-239">Creating a Zscaler Beta test user</span><span class="sxs-lookup"><span data-stu-id="fefcd-239">Creating a Zscaler Beta test user</span></span>

<span data-ttu-id="fefcd-240">To enable Azure AD users to log in to Zscaler Beta, they must be provisioned to Zscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="fefcd-240">To enable Azure AD users to log in to Zscaler Beta, they must be provisioned to Zscaler Beta.</span></span> <span data-ttu-id="fefcd-241">In the case of Zscaler Beta, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="fefcd-241">In the case of Zscaler Beta, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="fefcd-242">To configure user provisioning, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fefcd-242">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="fefcd-243">Log in to your **Zscaler Beta** tenant.</span><span class="sxs-lookup"><span data-stu-id="fefcd-243">Log in to your **Zscaler Beta** tenant.</span></span>

1. <span data-ttu-id="fefcd-244">Click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="fefcd-245">![Administration](./media/zscaler-beta-tutorial/ic781035.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="fefcd-245">![Administration](./media/zscaler-beta-tutorial/ic781035.png "Administration")</span></span>

1. <span data-ttu-id="fefcd-246">Click **User Management**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="fefcd-247">![Add](./media/zscaler-beta-tutorial/ic781036.png "Add")</span><span class="sxs-lookup"><span data-stu-id="fefcd-247">![Add](./media/zscaler-beta-tutorial/ic781036.png "Add")</span></span>

1. <span data-ttu-id="fefcd-248">In the **Users** tab, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-248">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="fefcd-249">![Add](./media/zscaler-beta-tutorial/ic781037.png "Add")</span><span class="sxs-lookup"><span data-stu-id="fefcd-249">![Add](./media/zscaler-beta-tutorial/ic781037.png "Add")</span></span>

1. <span data-ttu-id="fefcd-250">In the Add User section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fefcd-250">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="fefcd-251">![Add User](./media/zscaler-beta-tutorial/ic781038.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="fefcd-251">![Add User](./media/zscaler-beta-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="fefcd-252">a.</span><span class="sxs-lookup"><span data-stu-id="fefcd-252">a.</span></span> <span data-ttu-id="fefcd-253">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid Azure AD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="fefcd-253">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid Azure AD account you want to provision.</span></span>

    <span data-ttu-id="fefcd-254">b.</span><span class="sxs-lookup"><span data-stu-id="fefcd-254">b.</span></span> <span data-ttu-id="fefcd-255">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="fefcd-256">You can use any other Zscaler Beta user account creation tools or APIs provided by Zscaler Beta to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="fefcd-256">You can use any other Zscaler Beta user account creation tools or APIs provided by Zscaler Beta to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fefcd-257">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="fefcd-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fefcd-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler Beta.</span><span class="sxs-lookup"><span data-stu-id="fefcd-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler Beta.</span></span>

![Assign User][200] 

<span data-ttu-id="fefcd-260">**To assign Britta Simon to Zscaler Beta, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fefcd-260">**To assign Britta Simon to Zscaler Beta, perform the following steps:**</span></span>

1. <span data-ttu-id="fefcd-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="fefcd-263">In the applications list, select **Zscaler Beta**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-263">In the applications list, select **Zscaler Beta**.</span></span>

    ![Configure Single Sign-On](./media/zscaler-beta-tutorial/tutorial_zscalerbeta_app.png) 

1. <span data-ttu-id="fefcd-265">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="fefcd-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="fefcd-267">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="fefcd-267">Click **Add** button.</span></span> <span data-ttu-id="fefcd-268">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="fefcd-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="fefcd-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="fefcd-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="fefcd-271">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="fefcd-271">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="fefcd-272">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="fefcd-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fefcd-273">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="fefcd-273">Testing single sign-on</span></span>

<span data-ttu-id="fefcd-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="fefcd-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fefcd-275">When you click the Zscaler Beta tile in the Access Panel, you should get automatically signed-on to your Zscaler Beta application.</span><span class="sxs-lookup"><span data-stu-id="fefcd-275">When you click the Zscaler Beta tile in the Access Panel, you should get automatically signed-on to your Zscaler Beta application.</span></span>
<span data-ttu-id="fefcd-276">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fefcd-276">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fefcd-277">Additional resources</span><span class="sxs-lookup"><span data-stu-id="fefcd-277">Additional resources</span></span>

* [<span data-ttu-id="fefcd-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fefcd-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="fefcd-279">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fefcd-279">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/zscaler-beta-tutorial/tutorial_general_01.png
[2]: ./media/zscaler-beta-tutorial/tutorial_general_02.png
[3]: ./media/zscaler-beta-tutorial/tutorial_general_03.png
[4]: ./media/zscaler-beta-tutorial/tutorial_general_04.png

[100]: ./media/zscaler-beta-tutorial/tutorial_general_100.png

[200]: ./media/zscaler-beta-tutorial/tutorial_general_200.png
[201]: ./media/zscaler-beta-tutorial/tutorial_general_201.png
[202]: ./media/zscaler-beta-tutorial/tutorial_general_202.png
[203]: ./media/zscaler-beta-tutorial/tutorial_general_203.png

