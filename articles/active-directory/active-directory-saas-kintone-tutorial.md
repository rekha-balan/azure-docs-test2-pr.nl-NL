---
title: 'Tutorial: Azure Active Directory Integration with Kintone | Microsoft Docs'
description: Learn how to use Kintone with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: b7f8da9ff57880a7730b9902f40ec0b3047aa3a7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556159"
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a><span data-ttu-id="8dfca-103">Tutorial: Azure Active Directory Integration with Kintone</span><span class="sxs-lookup"><span data-stu-id="8dfca-103">Tutorial: Azure Active Directory Integration with Kintone</span></span>
<span data-ttu-id="8dfca-104">The objective of this tutorial is to show the integration of Azure and Kintone.</span><span class="sxs-lookup"><span data-stu-id="8dfca-104">The objective of this tutorial is to show the integration of Azure and Kintone.</span></span>  
<span data-ttu-id="8dfca-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="8dfca-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="8dfca-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="8dfca-106">A valid Azure subscription</span></span>
* <span data-ttu-id="8dfca-107">A Kintone single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8dfca-107">A Kintone single sign-on enabled subscription</span></span>

<span data-ttu-id="8dfca-108">After completing this tutorial, the Azure AD users you have assigned to Kintone will be able to single sign into the application at your Kintone company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8dfca-108">After completing this tutorial, the Azure AD users you have assigned to Kintone will be able to single sign into the application at your Kintone company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="8dfca-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8dfca-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="8dfca-110">Enabling the application integration for Kintone</span><span class="sxs-lookup"><span data-stu-id="8dfca-110">Enabling the application integration for Kintone</span></span>
2. <span data-ttu-id="8dfca-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="8dfca-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="8dfca-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="8dfca-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="8dfca-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="8dfca-113">Assigning users</span></span>

<span data-ttu-id="8dfca-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785859.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="8dfca-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785859.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-kintone"></a><span data-ttu-id="8dfca-115">Enabling the application integration for Kintone</span><span class="sxs-lookup"><span data-stu-id="8dfca-115">Enabling the application integration for Kintone</span></span>
<span data-ttu-id="8dfca-116">The objective of this section is to outline how to enable the application integration for Kintone.</span><span class="sxs-lookup"><span data-stu-id="8dfca-116">The objective of this section is to outline how to enable the application integration for Kintone.</span></span>

### <a name="to-enable-the-application-integration-for-kintone-perform-the-following-steps"></a><span data-ttu-id="8dfca-117">To enable the application integration for Kintone, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8dfca-117">To enable the application integration for Kintone, perform the following steps:</span></span>
1. <span data-ttu-id="8dfca-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8dfca-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="8dfca-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="8dfca-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="8dfca-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="8dfca-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="8dfca-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="8dfca-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="8dfca-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="8dfca-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="8dfca-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="8dfca-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="8dfca-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="8dfca-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="8dfca-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="8dfca-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="8dfca-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="8dfca-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="8dfca-127">In the **search box**, type **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="8dfca-127">In the **search box**, type **Kintone**.</span></span>
   
    <span data-ttu-id="8dfca-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785867.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="8dfca-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785867.png "Application Gallery")</span></span>

7. <span data-ttu-id="8dfca-129">In the results pane, select **Kintone**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="8dfca-129">In the results pane, select **Kintone**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="8dfca-130">![Kintone](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785871.png "Kintone")</span><span class="sxs-lookup"><span data-stu-id="8dfca-130">![Kintone](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785871.png "Kintone")</span></span>
   
## <a name="configuring-single-sign-on"></a><span data-ttu-id="8dfca-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="8dfca-131">Configuring single sign-on</span></span>

<span data-ttu-id="8dfca-132">The objective of this section is to outline how to enable users to authenticate to Kintone with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="8dfca-132">The objective of this section is to outline how to enable users to authenticate to Kintone with their account in Azure AD using federation based on the SAML protocol.</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="8dfca-133">To configure single sign-on, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8dfca-133">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="8dfca-134">In the Azure classic portal, on the **Kintone** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="8dfca-134">In the Azure classic portal, on the **Kintone** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
    <span data-ttu-id="8dfca-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785872.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="8dfca-135">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785872.png "Configure Single Sign-On")</span></span>

2. <span data-ttu-id="8dfca-136">On the **How would you like users to sign on to Kintone** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8dfca-136">On the **How would you like users to sign on to Kintone** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="8dfca-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785873.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="8dfca-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785873.png "Configure Single Sign-On")</span></span>

3. <span data-ttu-id="8dfca-138">On the **Configure App URL** page, in the **Kintone Sign On URL** textbox, type your URL using the following pattern "*https://company.kintone.com*", and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8dfca-138">On the **Configure App URL** page, in the **Kintone Sign On URL** textbox, type your URL using the following pattern "*https://company.kintone.com*", and then click **Next**.</span></span>
   
    <span data-ttu-id="8dfca-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785875.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="8dfca-139">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785875.png "Configure App URL")</span></span>

4. <span data-ttu-id="8dfca-140">On the **Configure single sign-on at Kintone** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8dfca-140">On the **Configure single sign-on at Kintone** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
    <span data-ttu-id="8dfca-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785878.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="8dfca-141">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785878.png "Configure Single Sign-On")</span></span>

5. <span data-ttu-id="8dfca-142">In a different web browser window, log into your **Kintone** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="8dfca-142">In a different web browser window, log into your **Kintone** company site as an administrator.</span></span>

6. <span data-ttu-id="8dfca-143">Click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="8dfca-143">Click **Settings**.</span></span>
   
    <span data-ttu-id="8dfca-144">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785879.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="8dfca-144">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785879.png "Settings")</span></span>

7. <span data-ttu-id="8dfca-145">Click **Users & System Administration**.</span><span class="sxs-lookup"><span data-stu-id="8dfca-145">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="8dfca-146">![Users & System Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785880.png "Users & System Administration")</span><span class="sxs-lookup"><span data-stu-id="8dfca-146">![Users & System Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785880.png "Users & System Administration")</span></span>

8. <span data-ttu-id="8dfca-147">Under **System Administration \> Security** click **Login**.</span><span class="sxs-lookup"><span data-stu-id="8dfca-147">Under **System Administration \> Security** click **Login**.</span></span>
   
    <span data-ttu-id="8dfca-148">![Login](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785881.png "Login")</span><span class="sxs-lookup"><span data-stu-id="8dfca-148">![Login](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785881.png "Login")</span></span>

9. <span data-ttu-id="8dfca-149">Click **Enable SAML authentication**.</span><span class="sxs-lookup"><span data-stu-id="8dfca-149">Click **Enable SAML authentication**.</span></span>
   
    <span data-ttu-id="8dfca-150">![SAML Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785882.png "SAML Authentication")</span><span class="sxs-lookup"><span data-stu-id="8dfca-150">![SAML Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785882.png "SAML Authentication")</span></span>

10. <span data-ttu-id="8dfca-151">In the SAML Authentication section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8dfca-151">In the SAML Authentication section, perform the following steps:</span></span>
    
    <span data-ttu-id="8dfca-152">![SAML Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785883.png "SAML Authentication")</span><span class="sxs-lookup"><span data-stu-id="8dfca-152">![SAML Authentication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785883.png "SAML Authentication")</span></span>
    
    1. <span data-ttu-id="8dfca-153">In the Azure classic portal, on the **Configure single sign-on at Kintone** dialog page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="8dfca-153">In the Azure classic portal, on the **Configure single sign-on at Kintone** dialog page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.</span></span>
   
    2. <span data-ttu-id="8dfca-154">In the Azure classic portal, on the **Configure single sign-on at Kintone** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="8dfca-154">In the Azure classic portal, on the **Configure single sign-on at Kintone** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Logout URL** textbox.</span></span>
    
    3. <span data-ttu-id="8dfca-155">Click **Browse** to upload your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="8dfca-155">Click **Browse** to upload your downloaded certificate.</span></span>
    
    4. <span data-ttu-id="8dfca-156">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="8dfca-156">Click **Save**.</span></span>

11. <span data-ttu-id="8dfca-157">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="8dfca-157">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="8dfca-158">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785884.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="8dfca-158">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785884.png "Configure Single Sign-On")</span></span>
    
## <a name="configuring-user-provisioning"></a><span data-ttu-id="8dfca-159">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="8dfca-159">Configuring user provisioning</span></span>

<span data-ttu-id="8dfca-160">In order to enable Azure AD users to log into Kintone, they must be provisioned into Kintone.</span><span class="sxs-lookup"><span data-stu-id="8dfca-160">In order to enable Azure AD users to log into Kintone, they must be provisioned into Kintone.</span></span>  
<span data-ttu-id="8dfca-161">In the case of Kintone, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="8dfca-161">In the case of Kintone, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="8dfca-162">To provision a user accounts, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8dfca-162">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="8dfca-163">Log in to your **Kintone** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="8dfca-163">Log in to your **Kintone** company site as an administrator.</span></span>

2. <span data-ttu-id="8dfca-164">Click **Setting**.</span><span class="sxs-lookup"><span data-stu-id="8dfca-164">Click **Setting**.</span></span>
   
    <span data-ttu-id="8dfca-165">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785879.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="8dfca-165">![Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785879.png "Settings")</span></span>

3. <span data-ttu-id="8dfca-166">Click **Users & System Administration**.</span><span class="sxs-lookup"><span data-stu-id="8dfca-166">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="8dfca-167">![User & System Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785880.png "User & System Administration")</span><span class="sxs-lookup"><span data-stu-id="8dfca-167">![User & System Administration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785880.png "User & System Administration")</span></span>

4. <span data-ttu-id="8dfca-168">Under **User Administration**, click **Departments & Users**.</span><span class="sxs-lookup"><span data-stu-id="8dfca-168">Under **User Administration**, click **Departments & Users**.</span></span>
   
    <span data-ttu-id="8dfca-169">![Department & Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785888.png "Department & Users")</span><span class="sxs-lookup"><span data-stu-id="8dfca-169">![Department & Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785888.png "Department & Users")</span></span>

5. <span data-ttu-id="8dfca-170">Click **New User**.</span><span class="sxs-lookup"><span data-stu-id="8dfca-170">Click **New User**.</span></span>
   
    <span data-ttu-id="8dfca-171">![New Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785889.png "New Users")</span><span class="sxs-lookup"><span data-stu-id="8dfca-171">![New Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785889.png "New Users")</span></span>

6. <span data-ttu-id="8dfca-172">In the **New User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8dfca-172">In the **New User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="8dfca-173">![New Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785890.png "New Users")</span><span class="sxs-lookup"><span data-stu-id="8dfca-173">![New Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785890.png "New Users")</span></span>
   
    1. <span data-ttu-id="8dfca-174">Type a **Display Name**, **Login Name**, **New Password**, **Confirm Password**, **E-mail Address** and other details of a valid AAD account you want to provision into the related texboxes.</span><span class="sxs-lookup"><span data-stu-id="8dfca-174">Type a **Display Name**, **Login Name**, **New Password**, **Confirm Password**, **E-mail Address** and other details of a valid AAD account you want to provision into the related texboxes.</span></span>
 
    2. <span data-ttu-id="8dfca-175">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="8dfca-175">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="8dfca-176">You can use any other Kintone user account creation tools or APIs provided by Kintone to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="8dfca-176">You can use any other Kintone user account creation tools or APIs provided by Kintone to provision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="8dfca-177">Assigning users</span><span class="sxs-lookup"><span data-stu-id="8dfca-177">Assigning users</span></span>
<span data-ttu-id="8dfca-178">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="8dfca-178">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-kintone-perform-the-following-steps"></a><span data-ttu-id="8dfca-179">To assign users to Kintone, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8dfca-179">To assign users to Kintone, perform the following steps:</span></span>
1. <span data-ttu-id="8dfca-180">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="8dfca-180">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="8dfca-181">On the \*\*Kintone \*\*application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="8dfca-181">On the \*\*Kintone \*\*application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="8dfca-182">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785891.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="8dfca-182">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC785891.png "Assign Users")</span></span>

3. <span data-ttu-id="8dfca-183">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="8dfca-183">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="8dfca-184">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="8dfca-184">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kintone-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="8dfca-185">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8dfca-185">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="8dfca-186">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8dfca-186">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

























