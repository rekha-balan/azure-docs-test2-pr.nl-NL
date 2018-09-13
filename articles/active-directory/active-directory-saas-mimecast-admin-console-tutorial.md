---
title: 'Tutorial: Azure Active Directory Integration with Mimecast Admin Console | Microsoft Docs'
description: Learn how to use Mimecast Admin Console with Azure Active Directory to enable single sign-on, automated provisioning, and more!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: 3828767004da4662e9d6bdaec9c1e8fe3f2c713a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551095"
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a><span data-ttu-id="af0c7-103">Tutorial: Azure Active Directory Integration with Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="af0c7-103">Tutorial: Azure Active Directory Integration with Mimecast Admin Console</span></span>
<span data-ttu-id="af0c7-104">The objective of this tutorial is to show the integration of Azure and Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="af0c7-104">The objective of this tutorial is to show the integration of Azure and Mimecast Admin Console.</span></span>  
<span data-ttu-id="af0c7-105">The scenario outlined in this tutorial assumes that you already have the following items:</span><span class="sxs-lookup"><span data-stu-id="af0c7-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="af0c7-106">A valid Azure subscription</span><span class="sxs-lookup"><span data-stu-id="af0c7-106">A valid Azure subscription</span></span>
* <span data-ttu-id="af0c7-107">A Mimecast Admin Console single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="af0c7-107">A Mimecast Admin Console single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="af0c7-108">After completing this tutorial, the Azure AD users you have assigned to Mimecast Admin Console will be able to single sign into the application at your Mimecast Admin Console company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="af0c7-108">After completing this tutorial, the Azure AD users you have assigned to Mimecast Admin Console will be able to single sign into the application at your Mimecast Admin Console company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="af0c7-109">The scenario outlined in this tutorial consists of the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="af0c7-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="af0c7-110">Enabling the application integration for Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="af0c7-110">Enabling the application integration for Mimecast Admin Console</span></span>
2. <span data-ttu-id="af0c7-111">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="af0c7-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="af0c7-112">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="af0c7-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="af0c7-113">Assigning users</span><span class="sxs-lookup"><span data-stu-id="af0c7-113">Assigning users</span></span>

<span data-ttu-id="af0c7-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795008.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="af0c7-114">![Scenario](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795008.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-mimecast-admin-console"></a><span data-ttu-id="af0c7-115">Enabling the application integration for Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="af0c7-115">Enabling the application integration for Mimecast Admin Console</span></span>
<span data-ttu-id="af0c7-116">The objective of this section is to outline how to enable the application integration for Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="af0c7-116">The objective of this section is to outline how to enable the application integration for Mimecast Admin Console.</span></span>

<span data-ttu-id="af0c7-117">**To enable the application integration for Mimecast Admin Console, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="af0c7-117">**To enable the application integration for Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="af0c7-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="af0c7-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="af0c7-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="af0c7-119">![Active Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="af0c7-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="af0c7-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="af0c7-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="af0c7-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="af0c7-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="af0c7-122">![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="af0c7-123">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="af0c7-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="af0c7-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC749321.png "Add application")</span><span class="sxs-lookup"><span data-stu-id="af0c7-124">![Add application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="af0c7-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="af0c7-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="af0c7-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC749322.png "Add an application from gallerry")</span><span class="sxs-lookup"><span data-stu-id="af0c7-126">![Add an application from gallerry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="af0c7-127">In the **search box**, type **Mimecast Admin Console**.</span><span class="sxs-lookup"><span data-stu-id="af0c7-127">In the **search box**, type **Mimecast Admin Console**.</span></span>
   
   <span data-ttu-id="af0c7-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795009.png "Application Gallery")</span><span class="sxs-lookup"><span data-stu-id="af0c7-128">![Application Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795009.png "Application Gallery")</span></span>
7. <span data-ttu-id="af0c7-129">In the results pane, select **Mimecast Admin Console**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="af0c7-129">In the results pane, select **Mimecast Admin Console**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="af0c7-130">![Mimecast Admin Console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795010.png "Mimecast Admin Console")</span><span class="sxs-lookup"><span data-stu-id="af0c7-130">![Mimecast Admin Console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795010.png "Mimecast Admin Console")</span></span>
   
## <a name="configuring-single-sign-on"></a><span data-ttu-id="af0c7-131">Configuring single sign-on</span><span class="sxs-lookup"><span data-stu-id="af0c7-131">Configuring single sign-on</span></span>

<span data-ttu-id="af0c7-132">The objective of this section is to outline how to enable users to authenticate to Mimecast Admin Console with their account in Azure AD using federation based on the SAML protocol.</span><span class="sxs-lookup"><span data-stu-id="af0c7-132">The objective of this section is to outline how to enable users to authenticate to Mimecast Admin Console with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="af0c7-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="af0c7-133">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span>  
<span data-ttu-id="af0c7-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="af0c7-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="af0c7-135">**To configure single sign-on, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="af0c7-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="af0c7-136">In the Azure classic portal, on the **Mimecast Admin Console** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span><span class="sxs-lookup"><span data-stu-id="af0c7-136">In the Azure classic portal, on the **Mimecast Admin Console** application integration page, click **Configure single sign-on** to open the \*\*Configure Single Sign On \*\* dialog.</span></span>
   
   <span data-ttu-id="af0c7-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795011.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="af0c7-137">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795011.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="af0c7-138">On the **How would you like users to sign on to Mimecast Admin Console** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="af0c7-138">On the **How would you like users to sign on to Mimecast Admin Console** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="af0c7-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795012.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="af0c7-139">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795012.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="af0c7-140">On the **Configure App URL** page, in the **Mimecast Admin Console Sign On URL** textbox, type the URL used by your users to sign on to your Mimecast Admin Console application (e.g.: “https://webmail-uk.mimecast.com” or “https://webmail-us.mimecast.com”), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="af0c7-140">On the **Configure App URL** page, in the **Mimecast Admin Console Sign On URL** textbox, type the URL used by your users to sign on to your Mimecast Admin Console application (e.g.: “https://webmail-uk.mimecast.com” or “https://webmail-us.mimecast.com”), and then click **Next**.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="af0c7-141">The sign on URL is region specific.</span><span class="sxs-lookup"><span data-stu-id="af0c7-141">The sign on URL is region specific.</span></span> 
   > 
   
   <span data-ttu-id="af0c7-142">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795013.png "Configure App URL")</span><span class="sxs-lookup"><span data-stu-id="af0c7-142">![Configure App URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795013.png "Configure App URL")</span></span>
4. <span data-ttu-id="af0c7-143">On the **Configure single sign-on at Mimecast Admin Console** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="af0c7-143">On the **Configure single sign-on at Mimecast Admin Console** page, to download your certificate, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
   <span data-ttu-id="af0c7-144">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795014.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="af0c7-144">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795014.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="af0c7-145">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span><span class="sxs-lookup"><span data-stu-id="af0c7-145">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span></span>
6. <span data-ttu-id="af0c7-146">Go to **Services \> Application**.</span><span class="sxs-lookup"><span data-stu-id="af0c7-146">Go to **Services \> Application**.</span></span>
   
   <span data-ttu-id="af0c7-147">![Services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC794998.png "Services")</span><span class="sxs-lookup"><span data-stu-id="af0c7-147">![Services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC794998.png "Services")</span></span>
7. <span data-ttu-id="af0c7-148">Click **Authentication Profiles**.</span><span class="sxs-lookup"><span data-stu-id="af0c7-148">Click **Authentication Profiles**.</span></span>
   
   <span data-ttu-id="af0c7-149">![Authentication Profiles](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC794999.png "Authentication Profiles")</span><span class="sxs-lookup"><span data-stu-id="af0c7-149">![Authentication Profiles](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC794999.png "Authentication Profiles")</span></span>
8. <span data-ttu-id="af0c7-150">Click **New Authentication Profile**.</span><span class="sxs-lookup"><span data-stu-id="af0c7-150">Click **New Authentication Profile**.</span></span>
   
   <span data-ttu-id="af0c7-151">![New Authentication Profiles](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795000.png "New Authentication Profiles")</span><span class="sxs-lookup"><span data-stu-id="af0c7-151">![New Authentication Profiles](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795000.png "New Authentication Profiles")</span></span>
9. <span data-ttu-id="af0c7-152">In the **Authentication Profile** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="af0c7-152">In the **Authentication Profile** section, perform the following steps:</span></span>
   
   <span data-ttu-id="af0c7-153">![Authentication Profile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795015.png "Authentication Profile")</span><span class="sxs-lookup"><span data-stu-id="af0c7-153">![Authentication Profile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795015.png "Authentication Profile")</span></span>
   
   1. <span data-ttu-id="af0c7-154">In the **Description** textbox, type a name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="af0c7-154">In the **Description** textbox, type a name for your configuration.</span></span>
   2. <span data-ttu-id="af0c7-155">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span><span class="sxs-lookup"><span data-stu-id="af0c7-155">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span></span>
   3. <span data-ttu-id="af0c7-156">As **Provider**, select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="af0c7-156">As **Provider**, select **Azure Active Directory**.</span></span>
   4. <span data-ttu-id="af0c7-157">In the Azure classic portal, on the **Configure single sign-on at Mimecast Admin Console** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="af0c7-157">In the Azure classic portal, on the **Configure single sign-on at Mimecast Admin Console** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer URL** textbox.</span></span>
   5. <span data-ttu-id="af0c7-158">In the Azure classic portal, on the **Configure single sign-on at Mimecast Admin Console** dialog page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="af0c7-158">In the Azure classic portal, on the **Configure single sign-on at Mimecast Admin Console** dialog page, copy the **Remote Login URL** value, and then paste it into the **Login URL** textbox.</span></span>
   6. <span data-ttu-id="af0c7-159">In the Azure classic portal, on the **Configure single sign-on at Mimecast Admin Console** dialog page, copy the **Remote Login URL** value, and then paste it into the **Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="af0c7-159">In the Azure classic portal, on the **Configure single sign-on at Mimecast Admin Console** dialog page, copy the **Remote Login URL** value, and then paste it into the **Logout URL** textbox.</span></span>  
      >[!NOTE]
      ><span data-ttu-id="af0c7-160">The Login URL value and the Logout URL value are for the Mimecast Admin Console the same.</span><span class="sxs-lookup"><span data-stu-id="af0c7-160">The Login URL value and the Logout URL value are for the Mimecast Admin Console the same.</span></span> 
      > 
   7. <span data-ttu-id="af0c7-161">Create a **base-64 encoded** file from your downloaded certificate.</span><span class="sxs-lookup"><span data-stu-id="af0c7-161">Create a **base-64 encoded** file from your downloaded certificate.</span></span>  
      
      >[!TIP]
      ><span data-ttu-id="af0c7-162">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="af0c7-162">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span> 
      > 
   8. <span data-ttu-id="af0c7-163">Open your base-64 encoded certificate in notepad, remove the first line (“*--*“) and the last line (“*--*“), copy the remaining content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span><span class="sxs-lookup"><span data-stu-id="af0c7-163">Open your base-64 encoded certificate in notepad, remove the first line (“*--*“) and the last line (“*--*“), copy the remaining content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>
   9. <span data-ttu-id="af0c7-164">Select **Allow Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="af0c7-164">Select **Allow Single Sign On**.</span></span>
   10. <span data-ttu-id="af0c7-165">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="af0c7-165">Click **Save**.</span></span>
10. <span data-ttu-id="af0c7-166">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span><span class="sxs-lookup"><span data-stu-id="af0c7-166">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="af0c7-167">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795016.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="af0c7-167">![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795016.png "Configure Single Sign-On")</span></span>
    
## <a name="configuring-user-provisioning"></a><span data-ttu-id="af0c7-168">Configuring user provisioning</span><span class="sxs-lookup"><span data-stu-id="af0c7-168">Configuring user provisioning</span></span>

<span data-ttu-id="af0c7-169">In order to enable Azure AD users to log into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="af0c7-169">In order to enable Azure AD users to log into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span></span> <span data-ttu-id="af0c7-170">In the case of Mimecast Admin Console, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="af0c7-170">In the case of Mimecast Admin Console, provisioning is a manual task.</span></span>

* <span data-ttu-id="af0c7-171">You need to register a domain before you can create users.</span><span class="sxs-lookup"><span data-stu-id="af0c7-171">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="af0c7-172">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="af0c7-172">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="af0c7-173">Sign on to your **Mimecast Admin Console** as administrator.</span><span class="sxs-lookup"><span data-stu-id="af0c7-173">Sign on to your **Mimecast Admin Console** as administrator.</span></span>
2. <span data-ttu-id="af0c7-174">Go to **Directories \> Internal**.</span><span class="sxs-lookup"><span data-stu-id="af0c7-174">Go to **Directories \> Internal**.</span></span>
   
   <span data-ttu-id="af0c7-175">![Directories](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795003.png "Directories")</span><span class="sxs-lookup"><span data-stu-id="af0c7-175">![Directories](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795003.png "Directories")</span></span>
3. <span data-ttu-id="af0c7-176">Click **Register New Domain**.</span><span class="sxs-lookup"><span data-stu-id="af0c7-176">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="af0c7-177">![Register New Domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795004.png "Register New Domain")</span><span class="sxs-lookup"><span data-stu-id="af0c7-177">![Register New Domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795004.png "Register New Domain")</span></span>
4. <span data-ttu-id="af0c7-178">After your new domain has been created, click **New Address**.</span><span class="sxs-lookup"><span data-stu-id="af0c7-178">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="af0c7-179">![New Address](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795005.png "New Address")</span><span class="sxs-lookup"><span data-stu-id="af0c7-179">![New Address](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795005.png "New Address")</span></span>
5. <span data-ttu-id="af0c7-180">In the new address dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="af0c7-180">In the new address dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="af0c7-181">![Save](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795006.png "Save")</span><span class="sxs-lookup"><span data-stu-id="af0c7-181">![Save](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795006.png "Save")</span></span>
   
   1. <span data-ttu-id="af0c7-182">Type the **Email Address**, **Global Name**, **Password** and **Confirm Password** attributes of a valid AAD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="af0c7-182">Type the **Email Address**, **Global Name**, **Password** and **Confirm Password** attributes of a valid AAD account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="af0c7-183">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="af0c7-183">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="af0c7-184">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="af0c7-184">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console to provision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="af0c7-185">Assigning users</span><span class="sxs-lookup"><span data-stu-id="af0c7-185">Assigning users</span></span>
<span data-ttu-id="af0c7-186">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span><span class="sxs-lookup"><span data-stu-id="af0c7-186">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="af0c7-187">**To assign users to Mimecast Admin Console, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="af0c7-187">**To assign users to Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="af0c7-188">In the Azure classic portal, create a test account.</span><span class="sxs-lookup"><span data-stu-id="af0c7-188">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="af0c7-189">On the **Mimecast Admin Console** application integration page, click **Assign users**.</span><span class="sxs-lookup"><span data-stu-id="af0c7-189">On the **Mimecast Admin Console** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="af0c7-190">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795017.png "Assign Users")</span><span class="sxs-lookup"><span data-stu-id="af0c7-190">![Assign Users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC795017.png "Assign Users")</span></span>
3. <span data-ttu-id="af0c7-191">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span><span class="sxs-lookup"><span data-stu-id="af0c7-191">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="af0c7-192">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC767830.png "Yes")</span><span class="sxs-lookup"><span data-stu-id="af0c7-192">![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-mimecast-admin-console-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="af0c7-193">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="af0c7-193">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="af0c7-194">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="af0c7-194">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>























