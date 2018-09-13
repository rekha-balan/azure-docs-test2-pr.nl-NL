---
title: 'Tutorial: Azure Active Directory Integration with Mimecast Personal Portal | Microsoft Docs'
description: Learn how to use Mimecast Personal Portal with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/03/2017
ms.author: jeedes
ms.openlocfilehash: 6f38e1ad0dc4af35ee35021bc69b75f25bd3092e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660546"
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a><span data-ttu-id="04020-103">Tutorial: Azure Active Directory Integration with Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="04020-103">Tutorial: Azure Active Directory Integration with Mimecast Personal Portal</span></span>
<span data-ttu-id="04020-104">The objective of this tutorial is to show the integration of Azure and Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="04020-104">The objective of this tutorial is to show the integration of Azure and Mimecast Personal Portal.</span></span> 

<span data-ttu-id="04020-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="04020-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="04020-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="04020-106">A valid Azure subscription</span></span>
* <span data-ttu-id="04020-107">A Mimecast Personal Portal single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="04020-107">A Mimecast Personal Portal single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="04020-108">After completing this tutorial, the Azure AD users you have assigned to Mimecast Personal Portal will be able to single sign into the application at your Mimecast Personal Portal company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="04020-108">After completing this tutorial, the Azure AD users you have assigned to Mimecast Personal Portal will be able to single sign into the application at your Mimecast Personal Portal company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="04020-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="04020-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="04020-110">Enabling the application integration for Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="04020-110">Enabling the application integration for Mimecast Personal Portal</span></span>
2. <span data-ttu-id="04020-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="04020-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="04020-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="04020-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="04020-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="04020-113">Assigning users</span></span>

<span data-ttu-id="04020-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC794991.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="04020-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC794991.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-mimecast-personal-portal"></a><span data-ttu-id="04020-115">Enabling the application integration for Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="04020-115">Enabling the application integration for Mimecast Personal Portal</span></span>
<span data-ttu-id="04020-116">The objective of this section is to outline how to enable the application integration for Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="04020-116">The objective of this section is to outline how to enable the application integration for Mimecast Personal Portal.</span></span>

<span data-ttu-id="04020-117">**To enable the application integration for Mimecast Personal Portal, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="04020-117">**To enable the application integration for Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="04020-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="04020-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="04020-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="04020-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="04020-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="04020-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="04020-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="04020-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="04020-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="04020-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="04020-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="04020-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="04020-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="04020-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="04020-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="04020-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="04020-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="04020-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="04020-127">In the **search box**, type **Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="04020-127">In the **search box**, type **Mimecast Personal Portal**.</span></span>
   
   <span data-ttu-id="04020-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC794992.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="04020-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC794992.png "Application Gallery")</span></span>
7. <span data-ttu-id="04020-129">In the results pane, select **Mimecast Personal Portal**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="04020-129">In the results pane, select **Mimecast Personal Portal**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="04020-130">![Mimecast Personal Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC794993.png "Mimecast Personal Portal")</span><span class="sxs-lookup"><span data-stu-id="04020-130">![Mimecast Personal Portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC794993.png "Mimecast Personal Portal")</span></span>
   
## <a name="configuring-single-sign-on"></a><span data-ttu-id="04020-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="04020-131">Configuring single sign-on</span></span>

<span data-ttu-id="04020-132">The objective of this section is to outline how to enable users to authenticate to Mimecast Personal Portal with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="04020-132">The objective of this section is to outline how to enable users to authenticate to Mimecast Personal Portal with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="04020-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="04020-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span>  
<span data-ttu-id="04020-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="04020-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="04020-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="04020-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="04020-136">In the Azure classic portal, on the **Mimecast Personal Portal** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="04020-136">In the Azure classic portal, on the **Mimecast Personal Portal** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="04020-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC794994.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="04020-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC794994.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="04020-138">On the **How would you like users to sign on to Mimecast Personal Portal** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="04020-138">On the **How would you like users to sign on to Mimecast Personal Portal** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="04020-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC794995.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="04020-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC794995.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="04020-140">On the **Configure App URL** page, in the **Mimecast Personal Portal Sign On URL** textbox, type the URL used by your users to sign on to your Mimecast Personal Portal application (e.g.: “https://webmail-uk.mimecast.com” or “https://webmail-us.mimecast.com”), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="04020-140">On the **Configure App URL** page, in the **Mimecast Personal Portal Sign On URL** textbox, type the URL used by your users to sign on to your Mimecast Personal Portal application (e.g.: “https://webmail-uk.mimecast.com” or “https://webmail-us.mimecast.com”), and then click **Next**.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="04020-141">The sign on URL is region specific.</span><span class="sxs-lookup"><span data-stu-id="04020-141">The sign on URL is region specific.</span></span> 
   > 
   
   <span data-ttu-id="04020-142">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC794996.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="04020-142">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC794996.png "Configure App URL")</span></span>
4. <span data-ttu-id="04020-143">On the **Configure single sign-on at Mimecast Personal Portal** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="04020-143">On the **Configure single sign-on at Mimecast Personal Portal** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
   <span data-ttu-id="04020-144">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC794997.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="04020-144">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC794997.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="04020-145">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span><span class="sxs-lookup"><span data-stu-id="04020-145">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span></span>
6. <span data-ttu-id="04020-146">Go to **Services \> Application**.</span><span class="sxs-lookup"><span data-stu-id="04020-146">Go to **Services \> Application**.</span></span>
   
   <span data-ttu-id="04020-147">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC794998.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="04020-147">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC794998.png "Applications")</span></span>
7. <span data-ttu-id="04020-148">Click **Authentication Profiles**.</span><span class="sxs-lookup"><span data-stu-id="04020-148">Click **Authentication Profiles**.</span></span>
   
   <span data-ttu-id="04020-149">![Authentication Profiles](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC794999.png "Authentication Profiles")</span><span class="sxs-lookup"><span data-stu-id="04020-149">![Authentication Profiles](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC794999.png "Authentication Profiles")</span></span>
8. <span data-ttu-id="04020-150">Click **New Authentication Profile**.</span><span class="sxs-lookup"><span data-stu-id="04020-150">Click **New Authentication Profile**.</span></span>
   
   <span data-ttu-id="04020-151">![New Authentication Profil](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC795000.png "New Authentication Profil")</span><span class="sxs-lookup"><span data-stu-id="04020-151">![New Authentication Profil](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC795000.png "New Authentication Profil")</span></span>
9. <span data-ttu-id="04020-152">In the **Authentication Profile** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="04020-152">In the **Authentication Profile** section, perform the following steps:</span></span>
   
   <span data-ttu-id="04020-153">![Authentication Profil](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC795001.png "Authentication Profil")</span><span class="sxs-lookup"><span data-stu-id="04020-153">![Authentication Profil](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC795001.png "Authentication Profil")</span></span>
   
   1. <span data-ttu-id="04020-154">In the **Description** textbox, type a name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="04020-154">In the **Description** textbox, type a name for your configuration.</span></span>
   2. <span data-ttu-id="04020-155">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="04020-155">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span></span>
   3. <span data-ttu-id="04020-156">As **Provider**, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="04020-156">As **Provider**, select **Azure Active Directory**.</span></span>
   4. <span data-ttu-id="04020-157">In the Azure classic portal, on the **Configure single sign-on at Mimecast Personal Portal** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="04020-157">In the Azure classic portal, on the **Configure single sign-on at Mimecast Personal Portal** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer URL** textbox.</span></span>
   5. <span data-ttu-id="04020-158">In the Azure classic portal, on the **Configure single sign-on at Mimecast Personal Portal** dialog page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="04020-158">In the Azure classic portal, on the **Configure single sign-on at Mimecast Personal Portal** dialog page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.</span></span>
   6. <span data-ttu-id="04020-159">In the Azure classic portal, on the **Configure single sign-on at Mimecast Personal Portal** dialog page, copy the **Remote Login URL** value, and then paste it into the **Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="04020-159">In the Azure classic portal, on the **Configure single sign-on at Mimecast Personal Portal** dialog page, copy the **Remote Login URL** value, and then paste it into the **Logout URL** textbox.</span></span>  
      >[!NOTE]
      ><span data-ttu-id="04020-160">The Login URL value and the Logout URL value are for the -on at Mimecast Personal Portal the same.</span><span class="sxs-lookup"><span data-stu-id="04020-160">The Login URL value and the Logout URL value are for the -on at Mimecast Personal Portal the same.</span></span>
      > 
   7. <span data-ttu-id="04020-161">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="04020-161">Create a **base-64 encoded** file from your downloaded certificate.</span></span>  
      
      >[!TIP]
      ><span data-ttu-id="04020-162">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="04020-162">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
      >  
   8. <span data-ttu-id="04020-163">Open your base-64 encoded certificate in notepad, remove the first line (“*--*“) and the last line (“*--*“), copy the remaining content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span><span class="sxs-lookup"><span data-stu-id="04020-163">Open your base-64 encoded certificate in notepad, remove the first line (“*--*“) and the last line (“*--*“), copy the remaining content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>
   9. <span data-ttu-id="04020-164">Select **Allow Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="04020-164">Select **Allow Single Sign On**.</span></span>
   10. <span data-ttu-id="04020-165">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="04020-165">Click **Save**.</span></span>
10. <span data-ttu-id="04020-166">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="04020-166">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="04020-167">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC795002.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="04020-167">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC795002.png "Configure Single Sign-On")</span></span>
    
## <a name="configuring-user-provisioning"></a><span data-ttu-id="04020-168">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="04020-168">Configuring user provisioning</span></span>

<span data-ttu-id="04020-169">In order to enable Azure AD users to log into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="04020-169">In order to enable Azure AD users to log into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span></span> <span data-ttu-id="04020-170">In the case of Mimecast Personal Portal, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="04020-170">In the case of Mimecast Personal Portal, provisioning is a manual task.</span></span>

* <span data-ttu-id="04020-171">You need to register a domain before you can create users.</span><span class="sxs-lookup"><span data-stu-id="04020-171">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="04020-172">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="04020-172">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="04020-173">Sign on to your **Mimecast Personal Portal** as administrator.</span><span class="sxs-lookup"><span data-stu-id="04020-173">Sign on to your **Mimecast Personal Portal** as administrator.</span></span>
2. <span data-ttu-id="04020-174">Go to **Directories \> Internal**.</span><span class="sxs-lookup"><span data-stu-id="04020-174">Go to **Directories \> Internal**.</span></span>
   
   <span data-ttu-id="04020-175">![Directories](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC795003.png "Directories")</span><span class="sxs-lookup"><span data-stu-id="04020-175">![Directories](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC795003.png "Directories")</span></span>
3. <span data-ttu-id="04020-176">Click **Register New Domain**.</span><span class="sxs-lookup"><span data-stu-id="04020-176">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="04020-177">![Register New Domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC795004.png "Register New Domain")</span><span class="sxs-lookup"><span data-stu-id="04020-177">![Register New Domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC795004.png "Register New Domain")</span></span>
4. <span data-ttu-id="04020-178">After your new domain has been created, click **New Address**.</span><span class="sxs-lookup"><span data-stu-id="04020-178">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="04020-179">![New Address](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC795005.png "New Address")</span><span class="sxs-lookup"><span data-stu-id="04020-179">![New Address](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC795005.png "New Address")</span></span>
5. <span data-ttu-id="04020-180">In the new address dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="04020-180">In the new address dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="04020-181">![Save](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC795006.png "Save")</span><span class="sxs-lookup"><span data-stu-id="04020-181">![Save](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC795006.png "Save")</span></span>
   
   1. <span data-ttu-id="04020-182">Type the **Email Address**, **Global Name**, **Password** and **Confirm Password** attributes of a valid AAD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="04020-182">Type the **Email Address**, **Global Name**, **Password** and **Confirm Password** attributes of a valid AAD account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="04020-183">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="04020-183">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="04020-184">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="04020-184">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal to provision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="04020-185">Assigning users</span><span class="sxs-lookup"><span data-stu-id="04020-185">Assigning users</span></span>
<span data-ttu-id="04020-186">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="04020-186">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="04020-187">**To assign users to Mimecast Personal Portal, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="04020-187">**To assign users to Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="04020-188">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="04020-188">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="04020-189">On the **Mimecast Personal Portal** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="04020-189">On the **Mimecast Personal Portal** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="04020-190">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC795007.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="04020-190">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC795007.png "Assign Users")</span></span>
3. <span data-ttu-id="04020-191">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="04020-191">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="04020-192">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="04020-192">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-personal-portal-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="04020-193">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="04020-193">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="04020-194">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="04020-194">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>























